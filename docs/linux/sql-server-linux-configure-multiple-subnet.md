---
title: Configurare un gruppo di disponibilità e un'istanza del cluster di failover con più subnet (Linux)
description: Informazioni su come configurare gruppi di disponibilità Always On e istanze del cluster di failover con più subnet per SQL Server in Linux.
ms.custom: seo-lt-2019
author: liweiSecurity
ms.author: liweiyin
ms.reviewer: VanMSFT
ms.date: 07/28/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 5abe1d99f753e0f41ca74a0864079293800dc1df
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362973"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>Configurare gruppi di disponibilità Always On e istanze del cluster di failover con più subnet

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Quando un gruppo di disponibilità Always On o un'istanza del cluster di failover si estende su più di un sito, in genere ogni sito ha una propria rete. Questo spesso significa che ogni sito dispone di specifici indirizzi IP. Ad esempio, gli indirizzi del sito A iniziano con 192.168.1.*x* e gli indirizzi del sito B iniziano con 192.168.2.*x*, dove *x* è la parte dell'indirizzo IP univoca per il server. Senza un qualche tipo di routing a livello di rete, questi server non saranno in grado di comunicare tra loro. Esistono due modi per gestire questo scenario: configurare una rete che colleghi le due diverse subnet, nota come VLAN, o configurare il routing tra le subnet.

## <a name="vlan-based-solution"></a>Soluzione basata su VLAN
 
**Prerequisito:** Per una soluzione basata su VLAN, ogni server che partecipa a un gruppo di disponibilità o a un'istanza del cluster di failover deve disporre di due schede di interfaccia di rete (NIC) per garantire la corretta disponibilità (una scheda di rete con due porte rappresenterebbe un singolo punto di errore in un server fisico), in modo da consentire di assegnare al server indirizzi IP nella subnet nativa, oltre a uno nella VLAN. Tali elementi sono in aggiunta alle altre esigenze di rete: anche iSCSI, ad esempio, richiede una propria rete.

La creazione degli indirizzi IP per il gruppo di disponibilità o l'istanza del cluster di failover viene eseguita nella VLAN. Nell'esempio seguente la VLAN ha una subnet di 192.168.3.*x*, quindi l'indirizzo IP creato per il gruppo di disponibilità o l'istanza del cluster di failover è 192.168.3.104. Non sono necessarie altre configurazioni, perché al gruppo di disponibilità o all'istanza del cluster di failover è assegnato un solo indirizzo IP.

![Configurare più subnet 01](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Configurazione con Pacemaker

Nel mondo Windows, un cluster di failover di Windows Server (WSFC) supporta in modo nativo più subnet e gestisce più indirizzi IP tramite una dipendenza OR dall'indirizzo IP. In Linux non esiste alcuna dipendenza OR, ma è possibile ottenere più subnet in modo nativo tramite Pacemaker, come illustrato di seguito. Non è possibile eseguire questa operazione semplicemente usando la normale riga di comando di Pacemaker per modificare una risorsa. È necessario modificare il file CIB (Cluster Information Base). Si tratta di un file XML con la configurazione di Pacemaker.

![Configurare più subnet 02](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>Aggiornare il file CIB

1. Esportare il file CIB.

    **Red Hat Enterprise Linux (RHEL) e Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    Dove *filename* è il nome che si vuole assegnare al file CIB.

2. Modificare il file che è stato generato. Cercare la sezione `<resources>`. Sarà possibile visualizzare le varie risorse create per il gruppo di disponibilità o l'istanza del cluster di failover. Individuare quella associata all'indirizzo IP. Aggiungere una sezione `<instance attributes>` con le informazioni per il secondo indirizzo IP sopra o sotto quello esistente, ma prima di `<operations>`. La sintassi è simile alla seguente:

    ```xml
    <instance attributes id="<NameForAttribute>">
        <nvpair id="<NameForIP>" name="ip" value="<IPAddress>"/>
    </instance attributes>
    ```
    
    dove *NameForAttribute* è il nome univoco di questo attributo, *NameForIP* è il nome associato all'indirizzo IP, *IPAddress* è l'indirizzo IP per la seconda subnet.
    
    Di seguito è riportato un esempio.
    
    ```xml
    <instance attributes id="virtualip-instance_attributes">
        <nvpair id="virtualip-instance_attributes-ip" name="ip" value="192.168.1.102"/>
    </instance attributes>
    ```
    
    Per impostazione predefinita, è presente una sola <instance/> nel file XML CIB esportato. Se sono presenti due subnet, è necessario disporre di due voci <instance/>.
    Di seguito è riportato un esempio di voci per due subnet
    
    ```xml
    <instance attributes id="virtualip-instance_attributes1">
        <rule id="Subnet1-IP" score="INFINITY" boolean-op="or">
            <expression id="Subnet1-Node1" attribute="#uname" operation="eq" value="Node1" />
            <expression id="Subnet1-Node2" attribute="#uname" operation="eq" value="Node2" />
        </rule>
        <nvpair id="IP-In-Subnet1" name="ip" value="192.168.1.102"/>
    </instance attributes>
    <instance attributes id="virtualip-instance_attributes2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node1" attribute="#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet2" name="ip" value="192.168.2.102"/>
    </instance attributes>
    ```
   
   Quando la subnet contiene più di un server, si usa 'boolean-op="or"'.


3. Importare il file CIB modificato e riconfigurare Pacemaker.

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

1. Dopo aver applicato correttamente il file CIB con la configurazione aggiornata, effettuare il ping del nome DNS associato alla risorsa indirizzo IP in Pacemaker. Deve riflettere l'indirizzo IP associato alla subnet che attualmente ospita il gruppo di disponibilità o l'istanza del cluster di failover.

2. Eseguire il failover del gruppo di disponibilità o dell'istanza del cluster di failover nell'altra subnet.

3. Quando il gruppo di disponibilità o l'istanza del cluster di failover è completamente online, effettuare il ping del nome DNS associato all'indirizzo IP. Deve riflettere l'indirizzo IP nella seconda subnet.

4. Se si vuole, eseguire nuovamente il failover del gruppo di disponibilità o dell'istanza del cluster di failover sulla subnet originale.

Ecco un post CSS che mostra come configurare CIB per tre subnet. Per informazioni dettagliate, vedere: [Configure multiple-subnet AlwaysOn Availability Group by modifying CIB](https://techcommunity.microsoft.com/t5/sql-server-support/configure-multiple-subnet-alwayson-availability-groups-by/ba-p/1544838) (Configurare il gruppo di disponibilità AlwaysOn su più subnet modificando CIB).
