---
title: Componenti fisici dell'appliance
description: Nomi e descrizioni per i componenti fisici dell'infrastruttura PDW e appliance.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5cbed66f53189668518e04848002ae69adb8c614
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400925"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>Componenti fisici dell'appliance-sistema di piattaforma di analisi
Nomi e descrizioni per i componenti fisici dell'infrastruttura PDW e appliance. 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>Diagrammi componente  
Vengono visualizzati i nomi dei componenti fisici e il percorso in cui si trovano nel primo rack di un'appliance a 6 nodi di calcolo.  
  
![Nomi dei componenti dell'area PDW - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames-HP")  
  
Il nome effettivo per i componenti PDW è il nome dell'area PDW, seguito da un trattino, seguito dal nome del componente. Se, ad esempio, il nome dell'area PDW è PDW123, i nomi effettivi sono **PDW123-CTL01**, **PDW123-CMP01**e così via.  
  
Analogamente, il nome effettivo per i componenti dell'infrastruttura del dispositivo è il dominio dell'appliance, seguito da un trattino, seguito dal nome del componente. Ad esempio, se il dominio del dispositivo è FSW123, le macchine virtuali dell'infrastruttura Appliance sono **FSW123-WDS**, **FSW123-ad01**, **FSW123-VMM**e così via.  
  
Ecco una visualizzazione consolidata di un'area PDW con 6 nodi di calcolo.  
  
![Nomi dei componenti PDW](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>Componenti PDW  
Le macchine virtuali PDW fanno parte dell'area PDW.  
  
*PDW_region*-CTL01  
Una macchina virtuale che esegue il nodo di controllo. Questa operazione viene eseguita su HST01 e può eseguire il failover a HST02.  
  
> [!WARNING]  
> SQL Server PDW non supporta la creazione di uno snapshot della macchina virtuale CTL01 tramite la console di gestione di Hyper-V. Gli snapshot si basano sull'archiviazione locale, che causerà errori se la macchina virtuale tenta di eseguire il failover al backup. La creazione di uno snapshot può anche causare problemi di affidabilità con l'altra macchina virtuale che esegue il failover al server passivo.  
  
*PDW_region*-CMP01 tramite *PDW_Region*-CMP06  
Una macchina virtuale che esegue il nodo di calcolo. In questo diagramma a 6 nodi di calcolo, gli host HSA01 tramite HSA06 eseguono le VM del nodo di calcolo CMP01 rispettivamente tramite CMP06.  
  
## <a name="fabric"></a>Componenti dell'infrastruttura Appliance  
Questi componenti fanno parte dell'infrastruttura dell'appliance.  
  
### <a name="virtual-machines"></a>Macchine virtuali  
*appliance_domain*WDS  
Questa macchina virtuale ospita servizi di distribuzione Windows (WDS), che il sistema di piattaforma di analisi usa per distribuire sistemi operativi Windows tramite la rete Appliance. Ospita anche il servizio DHCP, che consente agli host del dispositivo di aggiungersi alla rete Appliance senza avere un indirizzo IP preconfigurato.  
  
La macchina virtuale *appliance_domain*-WDS viene eseguita in HST01 ed è in grado di eseguire il failover in HST02. La macchina virtuale WDS e la macchina virtuale VMM distribuiscono Windows negli host fisici durante l'installazione dell'appliance. Durante il ciclo di vita dell'appliance, WDS e VMM eseguono operazioni come la sostituzione di un host.  
  
*appliance_domain*-VMM  
Il Virtual Machine Manager (VMM) viene eseguito in una macchina virtuale ed è in grado di eseguire il failover a HST02. VMM ospita System Center per distribuire il sistema operativo negli host fisici. VMM fornisce inoltre Windows Server Update Services (WSUS) per applicare o rimuovere gli aggiornamenti di Windows in tutti gli host e le macchine virtuali.  
  
*appliance_domain*-AD01, *appliance_domain*-ad02  
Active Directory Domain Services, che contiene il Domain Name System (DNS), viene eseguito in una macchina virtuale sia in HST01 che in HST02. Per la disponibilità elevata del dispositivo, AD01 e AD02 sono controller di dominio replicati e non eseguono il failover. Se si verifica un errore, l'altro è già disponibile con i dati corretti.  
  
*appliance_domain*-ISCSI01  
Una macchina virtuale ISCSI viene eseguita in ogni host con archiviazione collegata (HSA01-HSA06). Questa macchina virtuale non esegue il failover.  
  
### <a name="hosts"></a>Hosts  
*appliance_domain*-HST01 tramite *appliance_domain*-HST06  
Gli host per le macchine virtuali del nodo di controllo PDW e dell'infrastruttura Appliance. HST03 è un host passivo facoltativo.  
  
*appliance_domain*-HSA01 tramite *appliance_domain*-HSA08  
Host con archiviazione collegata (HSA). Ogni ha un host che esegue una macchina virtuale del nodo di calcolo e una VM ISCSI.  
  
### <a name="cluster-for-pdw"></a>Cluster per PDW  
*appliance_domain*-WFOHST01  
Il cluster PDW è denominato WFOHST01. Gestisce tutti gli host fisici e le macchine virtuali che appartengono a PDW.  
  
### <a name="direct-attached-storage"></a>Archiviazione collegata direttamente  
*appliance_domain*-DAS01 tramite *appliance_domain*-DAS03  
Si tratta dell'archiviazione collegata direttamente connessa ai nodi di calcolo. HP ha una DAS per ogni due nodi di calcolo. Dell e Quantity hanno una DAS per ogni tre nodi di calcolo.  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[Configurazione Appliance &#40;sistema della piattaforma di analisi&#41;](appliance-configuration.md)  
[Attività di gestione degli appliance &#40;sistema di piattaforma di analisi&#41;](appliance-management-tasks.md)  
  
