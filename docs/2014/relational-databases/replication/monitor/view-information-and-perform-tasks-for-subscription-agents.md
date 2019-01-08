---
title: Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una sottoscrizione (Monitoraggio replica) | Microsoft Docs
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
ms.assetid: fbb59d31-2424-4552-9195-0da8d83e755f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c1ded219b3b4a103b5cc8f98cdb86c2a8a52e21d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52815713"
---
# <a name="view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-replication-monitor"></a>Visualizzare le informazioni ed eseguire attività degli agenti associati a una sottoscrizione (Monitoraggio replica)
  In Monitoraggio replica sono disponibili due schede che consentono di accedere a informazioni sugli agenti associati a una sottoscrizione:  
  
-   **Tutte le sottoscrizioni**  
  
     In questa scheda vengono visualizzate informazioni su tutte le sottoscrizioni della pubblicazione selezionata.  
  
-   **Elenco verifica sottoscrizioni**  
  
     In questa scheda vengono visualizzate informazioni sulle sottoscrizioni di tutte le pubblicazioni disponibili sul server di pubblicazione selezionato che presentano errori, avvisi o un livello di prestazioni insufficiente. Questa scheda non viene visualizzata per i server di distribuzione che eseguono versioni di SQL Server precedenti a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Per ulteriori informazioni sulle opzioni di ogni scheda, fare clic sulla scheda nel riquadro a destra e quindi fare clic su **?** sulla barra dei menu. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-all-subscriptions-tab"></a>Per visualizzare le informazioni ed eseguire le attività degli agenti associati a una sottoscrizione (scheda Tutte le sottoscrizioni)  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **Tutte le sottoscrizioni** per visualizzare le informazioni relative alle sottoscrizioni. In questa scheda è inoltre possibile accedere a informazioni più dettagliate ed eseguire altre attività:  
  
    -   Per visualizzare informazioni dettagliate sull'agente associato a una sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Visualizza dettagli**. Le informazioni dettagliate includono la cronologia dell'agente e i messaggi di errore, statistiche sulle prestazioni nella replica transazionale e statistiche sulla sincronizzazione dei singoli articoli nella replica di tipo merge.  
  
         A seconda del tipo di sottoscrizione dalla finestra dei dettagli vengono avviate schede diverse: per le sottoscrizioni snapshot la scheda **Cronologia server di distribuzione - Sottoscrittore**, per le sottoscrizioni transazionali le schede **Cronologia server di pubblicazione - server di distribuzione**, **Cronologia server di distribuzione - Sottoscrittore**e **Comandi non distribuiti**e per le sottoscrizioni di tipo merge la scheda **Cronologia sincronizzazione**.  
  
    -   Per sincronizzare una sottoscrizione push, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Avvia sincronizzazione**.  
  
    -   Per reinizializzare una sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Reinizializza sottoscrizione**.  
  
    -   Per convalidare una singola sottoscrizione di tipo merge, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Convalida sottoscrizione**. Per convalidare tutte le sottoscrizioni di una pubblicazione di tipo merge, fare clic con il pulsante destro del mouse sulla pubblicazione e quindi scegliere **Convalida tutte le sottoscrizioni**. Per convalidare tutte le sottoscrizioni di una pubblicazione transazionale, fare clic con il pulsante destro del mouse sulla pubblicazione e quindi scegliere **Convalida sottoscrizioni**.  
  
    -   Per gestire i profili dell'agente, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Profilo agente**. Per altre informazioni, vedere [Usare i profili agenti di replica](../agents/replication-agent-profiles.md).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-subscription-watch-list-tab"></a>Per visualizzare le informazioni ed eseguire le attività degli agenti associati a una sottoscrizione (scheda Elenco verifica sottoscrizioni)  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro e quindi fare clic su un server di pubblicazione.  
  
2.  Fare clic sulla scheda **Elenco verifica sottoscrizioni** per visualizzare le informazioni relative alle sottoscrizioni. In questa scheda è inoltre possibile accedere a informazioni più dettagliate ed eseguire altre attività:  
  
    -   Per visualizzare informazioni dettagliate sull'agente associato a una sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Visualizza dettagli**. Le informazioni dettagliate includono la cronologia dell'agente e i messaggi di errore, statistiche sulle prestazioni nella replica transazionale e statistiche sulla sincronizzazione dei singoli articoli nella replica di tipo merge.  
  
         A seconda del tipo di sottoscrizione dalla finestra dei dettagli vengono avviate schede diverse: per le sottoscrizioni snapshot la scheda **Cronologia server di distribuzione - Sottoscrittore**, per le sottoscrizioni transazionali le schede **Cronologia server di pubblicazione - server di distribuzione**, **Cronologia server di distribuzione - Sottoscrittore**e **Prestazioni**e per le sottoscrizioni di tipo merge la scheda **Cronologia sincronizzazione**.  
  
    -   Per sincronizzare una sottoscrizione push, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Avvia sincronizzazione**.  
  
    -   Per reinizializzare una sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Reinizializza sottoscrizione**.  
  
    -   Per convalidare una singola sottoscrizione di tipo merge, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Convalida sottoscrizione**. Per convalidare tutte le sottoscrizioni di una pubblicazione di tipo merge, fare clic con il pulsante destro del mouse sulla pubblicazione e quindi scegliere **Convalida tutte le sottoscrizioni**. Per convalidare tutte le sottoscrizioni di una pubblicazione transazionale, fare clic con il pulsante destro del mouse sulla pubblicazione e quindi scegliere **Convalida sottoscrizioni**.  
  
    -   Per gestire i profili dell'agente, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Profilo agente**. Per altre informazioni, vedere [Usare i profili agenti di replica](../agents/replication-agent-profiles.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare le informazioni ed eseguire attività per una sottoscrizione &#40;Monitoraggio replica&#41;](view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Monitoraggio della replica](../monitoring-replication.md)  
  
  
