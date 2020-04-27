---
title: Informazioni sulla pubblicazione, avvisi (pubblicazione transazionale, SQL Server 2005 e versioni successive) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.warningsandagents.tran.f1
ms.assetid: 4d4baf1d-d0a1-4d09-bec7-137811f43f09
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e2ab1c4be29b87e1051daa702ce40905a95e34ab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63022005"
---
# <a name="publication-information-warnings-transactional-publication-sql-server-2005-and-later"></a>Informazioni sulla pubblicazione, Avvisi (pubblicazione transazionale, SQL Server 2005 e versioni successive)
   La scheda **Avvisi** è disponibile per i server di distribuzione che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. La scheda **Avvisi** consente di eseguire le attività seguenti per la pubblicazione selezionata:  
  
-   Consentire la visualizzazione degli avvisi in Monitoraggio replica.  
  
-   Specificare valori soglia associati agli avvisi.  
  
-   Definire messaggi di avviso associati ad avvisi.  
  
## <a name="warnings-thresholds-and-alerts"></a>Avvisi, soglie e messaggi di avviso  
 Per impostazione predefinita, Monitoraggio replica visualizza avvisi per le sottoscrizioni non inizializzate, includendo lo stato **Sottoscrizione non inizializzata** come avviso nella colonna **Stato** delle pagine contenenti informazioni sulla sottoscrizione. Per le pubblicazioni transazionali è possibile specificare se le condizioni aggiuntive seguenti generano avvisi:  
  
-   Scadenza imminente della sottoscrizione.  
  
     Corrisponde all'opzione **Avvisa se una sottoscrizione scade entro il valore soglia**. Se il valore soglia specificato viene raggiunto o superato, lo stato della sottoscrizione viene visualizzato come **Scadenza imminente/Scaduta** , a meno che non sia necessario visualizzare un problema con una priorità più alta.  
  
-   Superamento della latenza specificata. Indica la quantità di tempo che intercorre tra l'esecuzione del commit di una transazione nel server di pubblicazione e l'esecuzione del commit della transazione corrispondente nel Sottoscrittore.  
  
     Corrisponde all'opzione **Avvisa se la latenza supera il valore soglia**. Se il valore soglia specificato viene raggiunto o superato, lo stato della sottoscrizione viene visualizzato come **Prestazioni critiche** , a meno che non sia necessario visualizzare un problema con una priorità più alta. Il valore soglia viene inoltre utilizzato per determinare una valutazione delle prestazioni, visualizzata nella colonna **Prestazioni** delle pagine che contengono informazioni sulle sottoscrizioni. La valutazione delle prestazioni può corrispondere a uno dei valori seguenti:  
  
    -   Eccellenti  
  
    -   Buone  
  
    -   Discrete  
  
    -   Scarse  
  
    -   Critico  
  
 Quando si abilita un avviso, è inoltre necessario impostare un valore soglia. Se, ad esempio, si attiva l'avviso **Avvisa se la latenza supera il valore soglia**, selezionare la quantità di tempo consentita tra il commit di una transazione nel server di pubblicazione e il commit della transazione nel Sottoscrittore.  
  
 Oltre a visualizzare un avviso in Monitoraggio replica, il raggiungimento di un valore soglia può inoltre attivare un messaggio di avviso. Gli avvisi vengono definiti facendo clic su **Configura avvisi** e specificando le informazioni appropriate nella finestra di dialogo **Configura avvisi di replica** .  
  
## <a name="options"></a>Opzioni  
 **Attivata**  
 Selezionare questa opzione per abilitare un avviso e specificare un valore soglia.  
  
 **Avviso**  
 Descrizione dell'avviso associato al valore soglia.  
  
 **Soglia**  
 Consente di specificare un valore per la soglia.  
  
 **Configurare gli avvisi**  
 Selezionare una riga nella griglia **Avvisi** e fare clic su **Configura avvisi** per aprire la finestra di dialogo **Configura avvisi di replica** . Tramite questa finestra di dialogo è possibile definire un avviso associato al valore soglia e all'avviso selezionati.  
  
 **Ignora modifiche**  
 Fare clic su questo pulsante per ignorare le eventuali modifiche apportate agli avvisi e alle soglie.  
  
> [!NOTE]  
>   La scelta del pulsante **Ignora modifiche** non influisce sugli avvisi definiti nella finestra di dialogo **Configura avvisi di replica** .  
  
 **Salva modifiche**  
 Fare clic su questo pulsante per salvare le eventuali modifiche apportate agli avvisi e alle soglie.  
  
## <a name="see-also"></a>Vedi anche  
 [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md)   
 [Visualizzazione delle informazioni ed esecuzione di attività tramite Monitoraggio replica](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitorare le prestazioni con monitoraggio replica](monitor/monitor-performance-with-replication-monitor.md)   
 [Monitoraggio della replica](monitoring-replication.md)   
 [Set Thresholds and Warnings in Replication Monitor](monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
