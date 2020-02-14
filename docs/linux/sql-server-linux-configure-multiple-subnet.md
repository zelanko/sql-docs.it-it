---
title: Configurare un gruppo di disponibilità e un'istanza del cluster di failover con più subnet (Linux)
description: Informazioni su come configurare gruppi di disponibilità Always On e istanze del cluster di failover con più subnet per SQL Server in Linux.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/01/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: af017cf5d36075fdba6de31aa841e980cc20e175
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76911019"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>Configurare gruppi di disponibilità Always On e istanze del cluster di failover con più subnet

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Quando un gruppo di disponibilità Always On o un'istanza del cluster di failover si estende su più di un sito, in genere ogni sito ha una propria rete. Questo spesso significa che ogni sito dispone di specifici indirizzi IP. Ad esempio, gli indirizzi del sito A iniziano con 192.168.1.*x* e gli indirizzi del sito B iniziano con 192.168.2.*x*, dove *x* è la parte dell'indirizzo IP univoca per il server. Senza un qualche tipo di routing a livello di rete, questi server non saranno in grado di comunicare tra loro. Esistono due modi per gestire questo scenario: configurare una rete che colleghi le due diverse subnet, nota come VLAN, o configurare il routing tra le subnet.

## <a name="vlan-based-solution"></a>Soluzione basata su VLAN
 
**Prerequisito:** Per una soluzione basata su VLAN, ogni server che partecipa a un gruppo di disponibilità o a un'istanza del cluster di failover deve disporre di due schede di interfaccia di rete (NIC) per garantire la corretta disponibilità (una scheda di rete con due porte rappresenterebbe un singolo punto di errore in un server fisico), in modo da consentire di assegnare al server indirizzi IP nella subnet nativa, oltre a uno nella VLAN. Tali elementi sono in aggiunta alle altre esigenze di rete: anche iSCSI, ad esempio, richiede una propria rete.

La creazione degli indirizzi IP per il gruppo di disponibilità o l'istanza del cluster di failover viene eseguita nella VLAN. Nell'esempio seguente la VLAN ha una subnet di 192.168.3.*x*, quindi l'indirizzo IP creato per il gruppo di disponibilità o l'istanza del cluster di failover è 192.168.3.104. Non sono necessarie altre configurazioni, perché al gruppo di disponibilità o all'istanza del cluster di failover è assegnato un solo indirizzo IP.

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Configurazione con Pacemaker

Nel mondo Windows, un cluster di failover di Windows Server (WSFC) supporta in modo nativo più subnet e gestisce più indirizzi IP tramite una dipendenza OR dall'indirizzo IP. In Linux non esiste alcuna dipendenza OR, ma è possibile ottenere più subnet in modo nativo tramite Pacemaker, come illustrato di seguito. Non è possibile eseguire questa operazione semplicemente usando la normale riga di comando di Pacemaker per modificare una risorsa. È necessario modificare il file CIB (Cluster Information Base). Si tratta di un file XML con la configurazione di Pacemaker.

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>Aggiornare il file CIB

1.  Esportare il file CIB.

    **Red Hat Enterprise Linux (RHEL) e Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    Dove *filename* è il nome che si vuole assegnare al file CIB.

2.  Modificare il file che è stato generato. Cercare la sezione `<resources>`. Sarà possibile visualizzare le varie risorse create per il gruppo di disponibilità o l'istanza del cluster di failover. Individuare quella associata all'indirizzo IP. Aggiungere una sezione `<instance attributes>` con le informazioni per il secondo indirizzo IP sopra o sotto quello esistente, ma prima di `<operations>`. La sintassi è simile alla seguente:

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    dove *NameForAttribute* è il nome univoco per questo attributo, *Score* è il numero assegnato all'attributo, che deve essere superiore a quello della subnet primaria, *RuleName* è il nome della regola, *ExpressionName* è il nome dell'espressione, *NodeNameInSubnet2* è il nome del nodo nell'altra subnet, *NameForSecondIP* è il nome associato al secondo indirizzo IP, *IPAddress* è l'indirizzo IP per la seconda subnet, *NameForSecondIPNetmask* è il nome associato alla netmask e *Netmask* è la netmask per la seconda subnet.
    
    Di seguito è riportato un esempio.
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  Importare il file CIB modificato e riconfigurare Pacemaker.

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    dove *filename* è il nome del file CIB con le informazioni sull'indirizzo IP modificate.

### <a name="check-and-verify-failover"></a>Controllare e verificare il failover

1.  Dopo aver applicato correttamente il file CIB con la configurazione aggiornata, effettuare il ping del nome DNS associato alla risorsa indirizzo IP in Pacemaker. Deve riflettere l'indirizzo IP associato alla subnet che attualmente ospita il gruppo di disponibilità o l'istanza del cluster di failover.
2.  Eseguire il failover del gruppo di disponibilità o dell'istanza del cluster di failover nell'altra subnet.
3.  Quando il gruppo di disponibilità o l'istanza del cluster di failover è completamente online, effettuare il ping del nome DNS associato all'indirizzo IP. Deve riflettere l'indirizzo IP nella seconda subnet.
4.  Se si vuole, eseguire nuovamente il failover del gruppo di disponibilità o dell'istanza del cluster di failover sulla subnet originale.
