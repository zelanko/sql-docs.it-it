---
title: Configurare più subnet gruppi di disponibilità AlwaysOn e le istanze cluster di failover in Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/01/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4c8116462266386457270b16ebcdb684252f5dcf
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66713252"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>Configurare più subnet gruppi di disponibilità AlwaysOn e le istanze cluster di failover

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Quando un'istanza del cluster sempre nel gruppo di disponibilità (AG) o il failover (FCI) si estende su più di un sito, ogni sito in genere ha la propria rete. Spesso questo significa che ogni sito ha un proprio gli indirizzi IP. Ad esempio, gli indirizzi del sito iniziano con 192.168.1. *x* e gli indirizzi del sito B iniziano con 192.168.2. *x*, dove *x* è la parte dell'indirizzo IP univoco per il server. Senza una qualche forma di routing posto al livello di rete, questi server non sarà in grado di comunicare tra loro. Esistono due modi per gestire questo scenario: configurare una rete che collega due diverse subnet, nota come una VLAN, o configurare il routing tra subnet.

## <a name="vlan-based-solution"></a>Soluzione basata su VLAN
 
**Prerequisiti**: Per una soluzione basata su VLAN, ogni server che fanno parte di un gruppo di disponibilità o FCI necessita di due schede di rete (NIC) per la disponibilità appropriata (una scheda NIC porta doppia sarebbe un singolo punto di guasto in un server fisico), in modo che può essere assegnato gli indirizzi IP nella propria subnet native, nonché uno nella VLAN. Si tratta di oltre a eventuali altre esigenze di rete, ad esempio iSCSI, che deve inoltre la propria rete.

La creazione di indirizzi IP per il gruppo di disponibilità o FCI avviene nella VLAN. Nell'esempio seguente, la VLAN dispone di una subnet di 192.168.3. *x*, pertanto l'indirizzo IP creato per il gruppo di disponibilità o FCI è 192.168.3.104. Aggiungere alcuna azione deve essere configurata, poiché è presente un singolo indirizzo IP assegnato al gruppo di disponibilità o FCI.

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Configurazione con Pacemaker

Nell'ambiente Windows, un Windows Server Failover Cluster (WSFC) in modalità nativa supporta più subnet e gestisce più indirizzi IP tramite una dipendenza OR sull'indirizzo IP. In Linux, non è presente alcuna dipendenza OR, ma è possibile ottenere una subnet più corretta in modo nativo con Pacemaker, come illustrato di seguito. È non è possibile farlo utilizzando semplicemente la riga di comando di Pacemaker normale per modificare una risorsa. È necessario modificare le informazioni sul cluster base (implementazione). L'implementazione è un file XML con la configurazione di Pacemaker.

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>Aggiornare l'implementazione

1.  Esportare l'implementazione.

    **Ubuntu e Red Hat Enterprise Linux (RHEL)**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    In cui *filename* è il nome che si desidera chiamare l'implementazione.

2.  Modificare il file generato. Cercare il `<resources>` sezione. Si noterà che le varie risorse che sono state create per il gruppo di disponibilità o FCI. Trovare quello associato all'indirizzo IP. Aggiungere un `<instance attributes>` sezione con le informazioni per il secondo indirizzo IP di sopra o di sotto di quello esistente, ma prima `<operations>`. È simile alla sintassi seguente:

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    in cui *NameForAttribute* è il nome univoco per questo attributo *Score* è il numero assegnato all'attributo, che deve essere maggiore della subnet primaria, *RuleName*è il nome della regola di *ExpressionName* è il nome dell'espressione, ovvero *NodeNameInSubnet2* è il nome del nodo nell'altra subnet, *NameForSecondIP* è associato il secondo indirizzo IP, il nome *IPAddress* è l'indirizzo IP per la seconda subnet *NameForSecondIPNetmask* è il nome associato la netmask, e *Netmask* è la subnet mask per la seconda subnet.
    
    Di seguito viene riportato un esempio.
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  Importare l'implementazione modificata e riconfigurare Pacemaker.

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    in cui *filename* è il nome del file di implementazione con le informazioni sull'indirizzo IP modificati.

### <a name="check-and-verify-failover"></a>Controllare e verificare il failover

1.  Dopo l'implementazione viene correttamente applicata con la configurazione aggiornata, il ping del nome DNS associato alla risorsa indirizzo IP in Pacemaker. Devono riflettere l'indirizzo IP associato alla subnet che ospita il gruppo di disponibilità o FCI.
2.  Eseguire l'altra subnet il gruppo di disponibilità o FCI.
3.  Dopo che il gruppo di disponibilità o FCI è completamente online, il ping del nome DNS associato all'indirizzo IP. Devono riflettere l'indirizzo IP nella subnet di secondo.
4.  Se si desidera, eseguire il gruppo di disponibilità o FCI il failback la subnet originale.
