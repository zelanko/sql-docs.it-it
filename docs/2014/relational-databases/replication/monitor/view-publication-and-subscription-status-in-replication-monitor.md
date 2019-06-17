---
title: Visualizzare lo stato delle pubblicazioni e delle sottoscrizioni in Monitoraggio replica | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Log Reader Agent, monitoring
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- publications [SQL Server replication], viewing information
- Snapshot Agent, monitoring
- Distribution Agent, monitoring
- monitoring performance [SQL Server replication], publication status
- monitoring performance [SQL Server replication], subscription status
- subscriptions [SQL Server replication], viewing status
- Replication Monitor, publication and subscription status
ms.assetid: 16590771-9867-463e-a973-36a5c145ac16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9dad3a2c5f7073ea63608ba5234061a3ffa2102c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62666946"
---
# <a name="view-publication-and-subscription-status-in-replication-monitor"></a>Visualizzazione dello stato delle pubblicazioni e delle sottoscrizioni in Monitoraggio replica
  In Monitoraggio replica per[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono visualizzate informazioni sullo stato delle pubblicazioni e delle sottoscrizioni:  
  
-   Lo stato di una pubblicazione è determinato dallo stato con priorità più alta delle relative sottoscrizioni. Ad esempio, se una sottoscrizione a una pubblicazione presenta un errore e in un'altra sottoscrizione viene rilevato un problema di prestazioni, per la pubblicazione viene visualizzato uno stato di errore.  
  
-   Lo stato di una sottoscrizione è determinato dallo stato degli agenti associati alla sottoscrizione. Nel caso della replica di tipo merge si tratta dell'agente di merge. Nella replica transazionale, può trattarsi dell'agente di lettura log o dell'agente di distribuzione (viene visualizzato lo stato con priorità più alta). Lo stato può anche essere determinato dall'agente di lettura coda se si utilizzano sottoscrizioni ad aggiornamento in coda. Nella replica snapshot, si tratta dell'agente snapshot o dell'agente di distribuzione (viene visualizzato lo stato con priorità più alta).  
  
 Le tabelle riportate nelle sezioni seguenti includono i valori possibili per lo stato delle pubblicazioni e delle sottoscrizioni. Tre dei valori di stato vengono visualizzati solo se si raggiunge o supera una soglia:  
  
-   Scadenza imminente  
  
     Questo valore di stato si applica a tutti i tipi di replica. Per altre informazioni, vedere [Set Thresholds and Warnings in Replication Monitor](set-thresholds-and-warnings-in-replication-monitor.md).  
  
-   Prestazioni critiche  
  
     Questo valore di stato si applica alla replica transazionale e alla replica di tipo merge. Per altre informazioni, vedere [Monitorare le prestazioni con Monitoraggio replica](monitor-performance-with-replication-monitor.md).  
  
-   Merge con esecuzione prolungata  
  
     Questo valore di stato si applica alla replica di tipo merge. Per altre informazioni, vedere [Monitorare le prestazioni con Monitoraggio replica](monitor-performance-with-replication-monitor.md).  
  
 Oltre allo stato delle pubblicazioni e delle sottoscrizioni, nella replica di tipo merge è possibile ottenere statistiche a livello di articolo che offrono informazioni dettagliate sul tempo ancora necessario per completare una fase di merge, sul tempo impiegato per l'elaborazione di un determinato articolo, sul tipo di connessione utilizzato da un Sottoscrittore e su altri aspetti importanti. Le statistiche vengono visualizzate nella finestra Agente di merge in Monitoraggio replica. Nella replica snapshot e transazionale vengono offerte informazioni dettagliate sull'elaborazione dell'agente di distribuzione.  
  
 **Per visualizzare lo stato delle pubblicazioni e delle sottoscrizioni**  
  
-   Monitoraggio replica: [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](view-information-and-perform-tasks-replication-monitor.md).
  
  
## <a name="publication-status-values"></a>Valori di stato delle pubblicazioni  
 Nella tabella seguente vengono mostrati i valori di stato delle pubblicazioni e le relative icone in ordine di priorità.  
  
|Stato|Icona|  
|------------|----------|  
|Errore|![Icona interfaccia utente: errore](../media/repl-icon-error.gif "Icona interfaccia utente: errore")|  
|Prestazioni critiche|![Icona interfaccia utente: avviso](../media/repl-icon-warn.gif "Icona interfaccia utente: avviso")|  
|Ripetizione comando non riuscito|![Icona interfaccia utente: nuovo tentativo dell'agente di replica](../media/repl-icon-retry.gif "Icona interfaccia utente: nuovo tentativo dell'agente di replica")|  
|OK|none|  
  
## <a name="subscription-status-values"></a>Valori di stato delle sottoscrizioni  
 Nelle tabelle seguenti vengono mostrati i valori di stato delle sottoscrizioni e le relative icone in ordine di priorità. Una sottoscrizione può essere caratterizzata contemporaneamente da due stati, ad esempio **Scadenza imminente/Scaduta** e **Ripetizione comando non riuscito**. Viene visualizzato lo stato con priorità più alta.  
  
 I valori di stato **Prestazioni critiche**, **Scadenza imminente/Scaduta**e **Non inizializzata** sono avvisi. Se viene visualizzato un avviso, in Monitoraggio replica viene inoltre segnalato se un agente è in esecuzione. Ad esempio, lo stato potrebbe essere **In esecuzione, Prestazioni critiche**.  
  
### <a name="transactional-subscriptions"></a>Sottoscrizioni transazionali  
  
|Stato|Icona|  
|------------|----------|  
|Errore|![Icona interfaccia utente: errore](../media/repl-icon-error.gif "Icona interfaccia utente: errore")|  
|Prestazioni critiche|![Icona interfaccia utente: avviso](../media/repl-icon-warn.gif "Icona interfaccia utente: avviso")|  
|Scadenza imminente/Scaduta|![Icona interfaccia utente: avviso](../media/repl-icon-warn.gif "Icona interfaccia utente: avviso")|  
|Sottoscrizione non inizializzata|![Icona interfaccia utente: avviso](../media/repl-icon-warn.gif "Icona interfaccia utente: avviso")|  
|Ripetizione comando non riuscito|![Icona interfaccia utente: nuovo tentativo dell'agente di replica](../media/repl-icon-retry.gif "Icona interfaccia utente: nuovo tentativo dell'agente di replica")|  
|Non in esecuzione|![Icona interfaccia utente: agente di replica arrestato](../media/repl-icon-stopped.gif "Icona interfaccia utente: agente di replica arrestato")|  
|In esecuzione|![Icona interfaccia utente: agente di replica in esecuzione](../media/repl-icon-running.gif "Icona interfaccia utente: agente di replica in esecuzione")|  
  
### <a name="merge-subscriptions"></a>Sottoscrizioni di tipo merge  
  
|Stato|Icona|  
|------------|----------|  
|Errore|![Icona interfaccia utente: errore](../media/repl-icon-error.gif "Icona interfaccia utente: errore")|  
|Prestazioni critiche|![Icona interfaccia utente: avviso](../media/repl-icon-warn.gif "Icona interfaccia utente: avviso")|  
|Merge con esecuzione prolungata|![Icona interfaccia utente: avviso](../media/repl-icon-warn.gif "Icona interfaccia utente: avviso")|  
|Scadenza imminente/Scaduta|![Icona interfaccia utente: avviso](../media/repl-icon-warn.gif "Icona interfaccia utente: avviso")|  
|Sottoscrizione non inizializzata|![Icona interfaccia utente: avviso](../media/repl-icon-warn.gif "Icona interfaccia utente: avviso")|  
|Ripetizione comando non riuscito|![Icona interfaccia utente: nuovo tentativo dell'agente di replica](../media/repl-icon-retry.gif "Icona interfaccia utente: nuovo tentativo dell'agente di replica")|  
|Sincronizzazione in corso|![Icona interfaccia utente: agente di replica in esecuzione](../media/repl-icon-running.gif "Icona interfaccia utente: agente di replica in esecuzione")|  
|Non in sincronizzazione|![Icona interfaccia utente: agente di replica arrestato](../media/repl-icon-stopped.gif "Icona interfaccia utente: agente di replica arrestato")|  
  
### <a name="snapshot-subscriptions"></a>Sottoscrizioni snapshot  
  
|Stato|Icona|  
|------------|----------|  
|Errore|![Icona interfaccia utente: errore](../media/repl-icon-error.gif "Icona interfaccia utente: errore")|  
|Scadenza imminente/Scaduta|![Icona interfaccia utente: avviso](../media/repl-icon-warn.gif "Icona interfaccia utente: avviso")|  
|Sottoscrizione non inizializzata|![Icona interfaccia utente: avviso](../media/repl-icon-warn.gif "Icona interfaccia utente: avviso")|  
|Ripetizione comando non riuscito|![Icona interfaccia utente: nuovo tentativo dell'agente di replica](../media/repl-icon-retry.gif "Icona interfaccia utente: nuovo tentativo dell'agente di replica")|  
|Sincronizzazione in corso|![Icona interfaccia utente: agente di replica in esecuzione](../media/repl-icon-running.gif "Icona interfaccia utente: agente di replica in esecuzione")|  
|Non in sincronizzazione|![Icona interfaccia utente: agente di replica arrestato](../media/repl-icon-stopped.gif "Icona interfaccia utente: agente di replica arrestato")|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio della replica](../monitoring-replication.md)  
  
  
