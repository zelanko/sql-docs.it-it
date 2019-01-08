---
title: Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una pubblicazione (Monitoraggio replica) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], viewing information
- viewing replication agent information
- agents [SQL Server replication], tasks in Replication Monitor
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a92f56a6a9c68d984323ba8801755f87a1eaaec7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52758033"
---
# <a name="view-information-and-perform-tasks-for-the-agents-associated-with-a-publication-replication-monitor"></a>Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una pubblicazione (Monitoraggio replica)
  In Monitoraggio replica è disponibile la scheda **Agenti** , in cui sono presenti informazioni sugli agenti associati alla pubblicazione selezionata. L'agente di distribuzione e l'agente di merge sono associati alle sottoscrizioni. Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una sottoscrizione &#40;Monitoraggio replica&#41;](view-information-and-perform-tasks-for-subscription-agents.md).  
  
 In questa scheda vengono visualizzate informazioni relative agli agenti seguenti:  
  
-   Agente snapshot, utilizzato da tutte le pubblicazioni.  
  
-   Agente di lettura log, utilizzato da tutte le pubblicazioni transazionali.  
  
-   Agente di lettura coda, utilizzato dalle pubblicazioni transazionali abilitate per le sottoscrizioni ad aggiornamento in coda.  
  
 Per visualizzare altre informazioni relative alle opzioni della scheda, fare clic su **?** sulla barra dei menu. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-publication"></a>Per visualizzare informazioni ed eseguire attività relative agli agenti associati a una pubblicazione  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Per visualizzare le informazioni sugli agenti, fare clic sulla scheda **Agenti** . In questa scheda è inoltre possibile accedere a informazioni più dettagliate ed eseguire altre attività:  
  
    -   Per visualizzare informazioni dettagliate su un agente, ad esempio messaggi informativi ed eventuali messaggi di errore, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Visualizza dettagli**.  
  
    -   Per visualizzare informazioni dettagliate sul processo eseguito dall'agente, ad esempio la pianificazione, i dettagli sui passaggi del processo e così via, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Proprietà**.  
  
    -   Per gestire i profili dell'agente, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Profilo agente**. Per altre informazioni, vedere [Usare i profili agenti di replica](../agents/replication-agent-profiles.md).  
  
    -   Per avviare un agente non in esecuzione, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Avvia agente**.  
  
    -   Per arrestare l'esecuzione di un agente, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Arresta agente**.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare valori di soglia e avvisi in Monitoraggio replica](set-thresholds-and-warnings-in-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività per una pubblicazione &#40;Monitoraggio replica&#41;](view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Amministrazione dell'agente di replica](../agents/replication-agent-administration.md)   
 [Monitoraggio della replica](../monitoring-replication.md)  
  
  
