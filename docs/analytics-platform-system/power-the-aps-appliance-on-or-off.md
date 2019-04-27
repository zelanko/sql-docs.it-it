---
title: Accendere il dispositivo attiva o disattiva - sistema di piattaforma Analitica | Microsoft Docs
description: Power l'appliance attiva o disattiva per il sistema di piattaforma Analitica
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 994b0f94448b7fb7901734b2ae737e26be23900f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678629"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>Power l'appliance attiva o disattiva per il sistema di piattaforma Analitica
In questo argomento viene descritto come all'alimentazione accensione o spegnimento Systemappliance la piattaforma Analitica che esegue Parallel Data Warehouse. Dopo un'interruzione dell'alimentazione irreversibili, usare questo argomento quando si sposta un'appliance di sistema di piattaforma Analitica o alla potenza su un dispositivo.  
  
Potenziamento dell'appliance accensione e spegnimento non è lo stesso come avvio e arresto di servizi di appliance. Per informazioni su tale argomento, vedere [stato dei servizi PDW &#40;sistema di piattaforma Analitica&#41;](pdw-services-status.md). Per informazioni sul potenziamento attiva o disattiva un SQL Server 2008 Parallel Data Warehouse, vedere il file della Guida di SQL Server 2008 Parallel Data Warehouse. Per informazioni sul potenziamento attiva o disattiva un SQL Server 2012 AU1 o AU2 Parallel Data Warehouse, vedere il file della Guida per tali versioni.  
  
Quando queste istruzioni specificano la connessione a un nodo di SQL Server PDW, la connessione può essere locale usando dispositivi collegati (KVM) o remota tramite Desktop remoto. Alcune azioni devono essere fisica (attivare un interruttore) e alcune (ad esempio, arresto) può essere fisico o usando Windows comandi.  
  
È possibile effettuare connessioni ai nodi di SQL Server PDW usando gli indirizzi IP assegnati ai nodi, o dal **HST01** computer utilizzando il **gestione Cluster di Failover** (**cluadmin**) oppure **gestione di Hyper-V** (**virtmgmt.msc**) le applicazioni e facendo clic sul nome del nodo.  
  
## <a name="PowerOff"></a>Spegnere l'Appliance  
  
### <a name="before-you-begin"></a>Operazioni preliminari  
Prima di spegnere l'appliance, è necessario terminare tutte le attività nell'appliance. Per terminare tutte le attività:  
  
-   Usare la **sessioni** della Console di amministrazione per identificare gli utenti correnti. Contattarlo e chiedergli di chiudere la sessione.  
  
-   Se necessario è possibile usare la **KILL** istruzione per forzare la chiusura di una connessione client. Prestare attenzione quando si terminare le connessioni. Quando interrotta, alcuni processi transazionale, ad esempio un aggiornamento a esecuzione prolungata, è necessario attività di rollback prima di SQL Server può completare il ripristino del database. Eseguire il rollback un parzialmente completato update o delete, può richiedere tempi lunghi.  
  
### <a name="to-power-off-the-appliance"></a>Per spegnere l'appliance  
  
> [!WARNING]  
> Tutti i passaggi devono essere eseguiti nell'ordine esatto e ogni passaggio è necessario completare prima di eseguita il passaggio successivo, se non diversamente specificato. Eseguire i passaggi nell'ordine errato o senza tempi di attesa per ogni passaggio completare può comportare errori quando il dispositivo è acceso in un secondo momento.  
  
1.  Connettersi al nodo di controllo di PDW (**_PDW_region_-CTL01** ) e accedere con l'account amministratore di dominio di Analitica Platform System appliance.  
  
2.  Eseguire `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` per aprire la **Configuration Manager**.  
  
3.  In Configuration Manager, sotto il **Parallel Data Warehouse topologia** dal menu fare clic sul **stato del servizio** scheda e fare clic su **arrestare area** arrestare i servizi PDW.   
  
4.  Connettersi al  **_appliance_domain_-HST01** e accedere con l'account di amministratore di dominio appliance.  
  
5.  Usando il **gestione Cluster di Failover** connettersi il  **_appliance_domain_-WFOHST01** del cluster, se non è automaticamente connesso e quindi nel riquadro di spostamento, fare clic su **Ruoli**. Nel **ruoli** riquadro:  
  
    1.  Selezione multipla tutte le macchine virtuali. Fare doppio clic su essi e selezionare **Spegni**.  
  
    2.  Attendere che tutte le macchine virtuali selezionate completamento in corso l'arresto.  
  
6.  Chiudi il **gestione Cluster di Failover** dell'applicazione.  
  
7. Arrestare tutti i server tranne  **_appliance_domain_-HST01**.  
  
8. Arrestare il  **_appliance_domain_-HST01** server.  
  
9. Arrestare la distribuzione unità PDU (Power).  
  
## <a name="PowerOn"></a>Accendere il dispositivo  
  
### <a name="to-power-on-the-appliance"></a>Per accendere il dispositivo  
  
> [!WARNING]  
> Tutti i passaggi devono essere eseguiti nell'ordine esatto e ogni passaggio è necessario completare prima di eseguita il passaggio successivo, se non diversamente specificato. Eseguire i passaggi nell'ordine errato o senza tempi di attesa per ogni passaggio completare può comportare errori di avvio.  
  
1.  Accendere l'unità di distribuzione dell'alimentazione (PDU) e attendere che le opzioni per l'avvio automatico.  
  
2.  Accendere il  **_appliance_domain_-HST01** server.  
  
3.  Accedere al  **_appliance_domain_-HST01** come amministratore di dominio appliance.  
  
4.  Avviare il **gestione di Hyper-V** program (**virtmgmt.msc**) e connettersi al  **_appliance_domain_-HST01** se non è connesso per impostazione predefinita.  
  
    1.  Se non è possibile connettersi in base al nome perché il  **_PDW_region_-AD01** è non in esecuzione, provare a connettersi usando l'indirizzo IP.  
  
    2.  Nel **macchine virtuali** riquadro, individuare  **_PDW_region_-AD01** e verificare che sia in esecuzione. In caso contrario, avviare la macchina virtuale e attendere che venga avviata completamente.  
  
5.  Accendere il resto dei server nell'appliance.  
  
6.  Mentre in **HST01** effettuato l'accesso come amministratore di dominio appliance, da **Hyper-V Manager**:  
  
    1.  Connettersi al  **_appliance_domain_-HST02**.  
  
    2.  Nel **macchine virtuali** riquadro, individuare  **_PDW_region_-AD02** e verificare che sia in esecuzione.  In caso contrario, avviare la macchina virtuale e attendere che venga avviata completamente.  
  
7.  Usando il **gestione Cluster di Failover** connettersi al  **_appliance_domain_-WFOHST01** del cluster, se non è automaticamente connesso, quindi nella  **Navigazione** riquadro, fare clic su **ruoli**. Nel **ruoli** riquadro:  
  
    1.  Selezione multipla tutte le macchine virtuali, fare doppio clic su essi e quindi fare clic su **avviare**.  
  
    2.  Attendere che tutte le macchine virtuali selezionate completare l'avvio prima di procedere al passaggio successivo.  
  
    3.  Se necessario per le macchine virtuali che è stato eseguito il failover, arrestarli, spostarli e riavviarli in host primario corretto.  
  
8. Scollegarsi **HST01** se si desidera.  
  
9. Connettersi al  **_PDW_region_-CTL01** usando l'account di amministratore di dominio appliance.  
  
10. Eseguire `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` per avviare il **Configuration Manager**.  
  
11. Nel **Configuration Manager**, nella **Parallel Data Warehouse topologia** dal menu fare clic sul **stato di servizi** scheda e fare clic su **avvia area**per avviare i servizi PDW.  
  
### <a name="to-verify-the-appliance-health"></a>Per verificare l'integrità delle appliance  
Dopo aver avviato l'appliance, aprire il **Console di amministrazione** e selezionare la pagina di integrità per gli avvisi che potrebbero indicare le condizioni di errore. Per altre informazioni, vedere [monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md).  
  
## <a name="see-also"></a>Vedere anche  
[Attività di gestione di Appliance &#40;sistema di piattaforma Analitica&#41;](appliance-management-tasks.md)  
  
