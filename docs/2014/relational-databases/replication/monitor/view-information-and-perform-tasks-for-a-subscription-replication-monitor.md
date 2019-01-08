---
title: Visualizzare le informazioni ed eseguire attività per una sottoscrizione (Monitoraggio replica) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], viewing information
- subscriptions [SQL Server replication], Replication Monitor tasks
- viewing subscription information
ms.assetid: 54aac83b-6f29-40d7-8901-cf059749867f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6984e2c104502dbca2e2284e98ddeefe77b1ca86
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52784618"
---
# <a name="view-information-and-perform-tasks-for-a-subscription-replication-monitor"></a>Visualizzare le informazioni ed eseguire attività per una sottoscrizione (Monitoraggio replica)
  In Monitoraggio replica sono disponibili le schede seguenti, che includono informazioni sulle sottoscrizioni:  
  
-   **Tutte le sottoscrizioni**  
  
     In questa scheda vengono visualizzate informazioni su tutte le sottoscrizioni della pubblicazione selezionata.  
  
-   **Elenco verifica sottoscrizioni**  
  
     In questa scheda vengono visualizzate informazioni sulle sottoscrizioni di tutte le pubblicazioni disponibili sul server di pubblicazione selezionato che presentano errori, avvisi o un livello di prestazioni insufficiente. Questa scheda non viene visualizzata per i server di distribuzione che eseguono versioni di SQL Server precedenti a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Per ulteriori informazioni sulle opzioni di ogni scheda, fare clic sulla scheda nel riquadro a destra e quindi fare clic su **?** sulla barra dei menu. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-all-subscriptions-tab"></a>Per visualizzare informazioni ed eseguire attività per le sottoscrizioni nella scheda Tutte le sottoscrizioni  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Per visualizzare le informazioni sulle sottoscrizioni, fare clic sulla scheda **Tutte le sottoscrizioni** . Per visualizzare solo le sottoscrizioni in uno stato specifico, ad esempio in sincronizzazione, selezionare un'opzione nell'elenco a discesa **Mostra** .  
  
3.  Per visualizzare e modificare le proprietà della sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Proprietà**. In questa scheda è inoltre possibile accedere a informazioni più dettagliate ed eseguire altre attività. Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una sottoscrizione &#40;Monitoraggio replica&#41;](view-information-and-perform-tasks-for-subscription-agents.md).  
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-subscription-watch-list-tab"></a>Per visualizzare informazioni ed eseguire attività per le sottoscrizioni nella scheda Elenco verifica sottoscrizioni  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro e quindi fare clic su un server di pubblicazione.  
  
2.  Per visualizzare informazioni sulle sottoscrizioni, fare clic sulla scheda **Elenco verifica sottoscrizioni** .  
  
3.  Selezionare il tipo di sottoscrizione da visualizzare nell'elenco a discesa **Mostra sottoscrizioni \<TipoSottoscrizione>**. Per visualizzare solo le sottoscrizioni in uno stato specifico, ad esempio in sincronizzazione, selezionare un'opzione nell'elenco a discesa **Mostra** .  
  
4.  Per visualizzare e modificare le proprietà della sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Proprietà**. In questa scheda è inoltre possibile accedere a informazioni più dettagliate ed eseguire altre attività. Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una sottoscrizione &#40;Monitoraggio replica&#41;](view-information-and-perform-tasks-for-subscription-agents.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà delle sottoscrizioni push](../view-and-modify-push-subscription-properties.md)   
 [Visualizzare e modificare le proprietà delle sottoscrizioni pull](../view-and-modify-pull-subscription-properties.md)   
 [Monitoraggio della replica](../monitoring-replication.md)  
  
  
