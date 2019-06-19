---
title: Componenti fisici Appliance - sistema di piattaforma Analitica | Microsoft Docs
description: I nomi e descrizioni per i componenti fisici dell'infrastruttura appliance e PDW.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0adbd92d1a29a98a80de65268c53ea63e3941d07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639933"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>Componenti fisici Appliance - sistema di piattaforma Analitica
I nomi e descrizioni per i componenti fisici dell'infrastruttura appliance e PDW. 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>Diagrammi dei componenti  
Mostra i nomi dei componenti fisici e in cui si trovano nel primo rack di un'appliance di 6 nodi.  
  
![Nomi dei componenti area PDW - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames-HP")  
  
Il nome effettivo per i componenti PDW è il nome dell'area PDW, seguito da un trattino, seguito dal nome del componente. Ad esempio, se il nome dell'area PDW PDW123, i nomi effettivi vengono **PDW123 CTL01**, **PDW123-CMP01**e così via.  
  
Analogamente, il nome effettivo per i componenti dell'infrastruttura di appliance è il dominio dell'appliance, seguito da un trattino, seguito dal nome del componente. Ad esempio, se il dominio di appliance è FSW123, l'infrastruttura di appliance le macchine virtuali vengono **FSW123 WDS**, **FSW123 AD01**, **FSW123 VMM**e così via.  
  
Ecco una visualizzazione consolidata di un'area PDW con 6 nodi di calcolo.  
  
![Nomi dei componenti PDW](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>Componenti PDW  
Le macchine virtuali PDW fanno parte dell'area PDW.  
  
*PDW_region*-CTL01  
Una macchina virtuale che esegue il nodo di controllo. Ciò viene eseguito su HST01 ed eseguire il failover a HST02.  
  
> [!WARNING]  
> SQL Server PDW non supporta la creazione di uno snapshot della macchina virtuale CTL01 utilizzando Gestione di Hyper-V. Gli snapshot si basano su archiviazione locale, che causerà errori se la macchina virtuale tenta di eseguire il failover al relativo backup. Creazione di uno snapshot può anche causare problemi di affidabilità con l'altra VM che il failover al server passivo.  
  
*PDW_region*-CMP01 attraverso *PDW_Region*-CMP06  
Una macchina virtuale che esegue il nodo di calcolo. In questo diagramma di nodo di calcolo di 6, gli host HSA01 tramite HSA06 esecuzione nodo di calcolo CMP01 macchine virtuali tramite CMP06 rispettivamente.  
  
## <a name="fabric"></a>Componenti dell'infrastruttura di Appliance  
Questi componenti fanno parte dell'infrastruttura di appliance.  
  
### <a name="virtual-machines"></a>Macchine virtuali  
*appliance_domain*-WDS  
In questo host di macchine virtuali Windows Deployment Services (WDS), che usa il sistema di piattaforma Analitica distribuire sistemi operativi Windows in rete appliance. Ospita anche il servizio DHCP, che consente agli host l'accessorio alla rete appliance senza la necessità di un indirizzo IP configurato in precedenza.  
  
Il *appliance_domain*macchina virtuale - servizi di distribuzione Windows viene eseguito su HST01 ed eseguire il failover a HST02. La macchina virtuale di servizi di distribuzione Windows e la macchina virtuale VMM, distribuire Windows in host fisici durante l'installazione di appliance. Durante il ciclo di vita di appliance, WDS e VMM eseguire operazioni come la sostituzione di un host.  
  
*appliance_domain*-VMM  
Virtual Machine Manager (VMM) viene eseguito in una macchina virtuale ed eseguire il failover a HST02. VMM ospita System Center per distribuire il sistema operativo negli host fisici. VMM fornisce anche Windows Server Update Services (WSUS) per applicare o rimuovere gli aggiornamenti di Windows in tutti gli host e macchine virtuali.  
  
*appliance_domain*-AD01, *appliance_domain*-AD02  
Active Directory Domain Services, che contiene il sistema DNS (Domain Name), viene eseguito in una macchina virtuale sia HST01 HST02. Per la disponibilità elevata dell'appliance AD01 e AD02 sono controller di dominio replicato e avviene il failover. Se uno ha esito negativo, l'altro è già disponibile con i dati corretti.  
  
*appliance_domain*-ISCSI01  
Una macchina virtuale ISCSI viene eseguito in ognuno degli host con archiviazione collegata (HSA01 HSA06). Questa macchina virtuale non esegue il failover.  
  
### <a name="hosts"></a>Host  
*appliance_domain*-HST01 through *appliance_domain*-HST06  
Gli host per controllo PDW appliance e nodo fabric macchine virtuali. HST03 è host passivo facoltativo.  
  
*appliance_domain*-HSA01 attraverso *appliance_domain*-HSA08  
Gli host con archiviazione collegata (HSA). Ogni HAS host viene eseguito un nodo di calcolo della macchina virtuale e una VM ISCSI.  
  
### <a name="cluster-for-pdw"></a>Cluster per PDW  
*appliance_domain*-WFOHST01  
Il cluster PDW è denominato WFOHST01. Gestisce tutti gli host fisici e macchine virtuali che appartengono a PDW.  
  
### <a name="direct-attached-storage"></a>Direct Attached Storage  
*appliance_domain*-DAS01 through *appliance_domain*-DAS03  
Questo è l'archiviazione collegata direttamente connesso ai nodi di calcolo. HP è uno DAS per ogni due nodi di calcolo. Dell e quantum hanno uno DAS per ogni tre nodi di calcolo.  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[La configurazione dell'Appliance &#40;sistema di piattaforma Analitica&#41;](appliance-configuration.md)  
[Attività di gestione di Appliance &#40;sistema di piattaforma Analitica&#41;](appliance-management-tasks.md)  
  
