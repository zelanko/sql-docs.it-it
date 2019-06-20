---
title: Visualizzare il report di log shipping (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- viewing log shipping reports
- displaying log shipping reports
- log shipping [SQL Server], monitoring
- log shipping [SQL Server], viewing reports
ms.assetid: 3b549f2f-3683-45e5-b8e8-8095276c41ab
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85eb934b93d22acc2534d1eb34aa967cbb4f2714
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774253"
---
# <a name="view-the-log-shipping-report-sql-server-management-studio"></a>Visualizzare il report di log shipping (SQL Server Management Studio)
  In questo argomento viene descritta la procedura per visualizzare il report Stato log shipping delle transazioni in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. È possibile eseguire un report sullo stato in un server di monitoraggio, in un server primario o in un server secondario. Per visualizzare le informazioni più complete sulla configurazione per il log shipping, eseguire il report nell'istanza del server di monitoraggio.  
  
 Nel report è indicato lo stato di qualsiasi attività di log shipping il cui stato sia disponibile nell'istanza del server a cui si è connessi. Se l'istanza del server è coinvolta in più configurazioni in ruoli diversi, ad esempio come server di monitoraggio per un database e come server secondario per un altro database, nei risultati visualizzati saranno incluse le informazioni su ogni configurazione dal punto di vista di ogni ruolo. Se inoltre la stored procedure può eseguire la connessione all'istanza del server di monitoraggio per una determinata configurazione per il log shipping, nel report verranno visualizzate ulteriori informazioni su tale configurazione.  
  
 Per ogni ruolo eseguito dall'istanza del server corrente, è possibile visualizzare le informazioni seguenti:  
  
|Role|Informazioni visualizzate|  
|----------|---------------------------|  
|Monitoraggio|Nome e stato di ogni server primario e secondario in cui questa istanza del server è utilizzata come server di monitoraggio.|  
|Primaria|Per ogni database primario, stato e nome dell'istanza del server corrente, come server primario, e nome del database primario. Nel report viene visualizzato lo stato del processo di backup, archiviato localmente nel server primario.<br /><br /> È inoltre presente una riga per ogni server secondario corrispondente. Se nella configurazione è in uso un server di monitoraggio a cui la stored procedure può effettuare la connessione, nelle righe vengono visualizzati lo stato di copia e ripristino del backup del log più recente.|  
|Secondari|Per ogni database secondario, stato e nome dell'istanza del server corrente, come server secondario, e nome del database secondario.<br /><br /> Nel report viene indicato lo stato dei processi di copia e ripristino nel server secondario.<br /><br /> È inoltre presente una riga per il server primario corrispondente. Se nella configurazione è in uso un server di monitoraggio a cui la stored procedure può effettuare la connessione, nelle righe viene visualizzato lo stato del backup del log più recente.|  
  
 Le informazioni visualizzate dipendono dal fatto che l'istanza del server sia un server di monitoraggio, primario o secondario. Se non sono disponibili informazioni, le celle corrispondenti sono disattivate.  
  
 Per ottenere i dati, tramite il report viene chiamata la procedura **sp_help_log_shipping_monitor**. Per informazioni sulle autorizzazioni richieste, vedere [sp_help_log_shipping_monitor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql).  
  
### <a name="to-display-the-transaction-log-shipping-status-report-on-a-server-instance"></a>Per visualizzare il report Stato log shipping delle transazioni su un'istanza del server  
  
1.  Connettersi a un server di monitoraggio, a un server primario o a un server secondario.  
  
2.  In Esplora oggetti fare clic con il pulsante destro del mouse sull'istanza del server, scegliere **Report**e quindi **Report standard**.  
  
3.  Fare clic su **Stato log shipping delle transazioni**.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare il log shipping &#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
  
