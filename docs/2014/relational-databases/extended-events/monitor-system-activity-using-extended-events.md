---
title: Monitorare l'attività del sistema mediante gli eventi estesi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- xe
- extended events [SQL Server], monitoring system activity
ms.assetid: d83ad88f-818c-49fe-a9a9-299f704fca53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44bb482d1385ad9b22900bb74015a779ea6750d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62638732"
---
# <a name="monitor-system-activity-using-extended-events"></a>Monitorare l'attività del sistema mediante gli eventi estesi
  In questa procedura viene illustrato come utilizzare gli eventi estesi con Analisi eventi per Windows (ETW) al fine di monitorare l'attività del sistema. Viene inoltre indicata la modalità di utilizzo delle istruzioni CREATE EVENT SESSION, ALTER EVENT SESSION e DROP EVENT SESSION.  
  
 Il completamento di tali attività comporta l'utilizzo dell'editor di query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per effettuare la procedura descritta di seguito. La procedura richiede anche l'utilizzo del prompt dei comandi per eseguire comandi ETW.  
  
### <a name="to-monitor-system-activity-using-extended-events"></a>Per monitorare l'attività del sistema mediante gli eventi estesi  
  
1.  Nell'editor di query eseguire le istruzioni indicate di seguito per creare una sessione eventi e aggiungere due eventi. Tali eventi, ovvero checkpoint_begin e checkpoint_end, vengono generati all'inizio e alla fine di un checkpoint del database.  
  
    ```  
    CREATE EVENT SESSION test0  
    ON SERVER  
    ADD EVENT sqlserver.checkpoint_begin,  
    ADD EVENT sqlserver.checkpoint_end  
    WITH (MAX_DISPATCH_LATENCY = 1 SECONDS)  
    go  
    ```  
  
2.  Aggiungere la destinazione di bucket con 32 bucket per contare il numero di checkpoint in base all'ID del database.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    ADD TARGET package0.histogram  
    (  
          SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id'  
    )  
    go  
    ```  
  
3.  Eseguire le istruzioni indicate di seguito per aggiungere la destinazione ETW. Verranno visualizzati gli eventi di inizio e di fine utilizzati per determinare il tempo necessario per il checkpoint.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    ADD TARGET package0.etw_classic_sync_target  
    go  
    ```  
  
4.  Eseguire le istruzioni indicate di seguito per avviare la sessione e iniziare la raccolta degli eventi.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    STATE = start  
    go  
    ```  
  
5.  Eseguire le istruzioni indicate di seguito per generare tre eventi.  
  
    ```  
    USE tempdb  
          checkpoint  
    go  
    USE master  
          checkpoint  
          checkpoint  
    go  
    ```  
  
6.  Eseguire le istruzioni indicate di seguito per visualizzare il conteggio degli eventi.  
  
    ```  
    SELECT CAST(xest.target_data AS xml) Bucketizer_Target_Data_in_XML  
    FROM sys.dm_xe_session_targets xest  
    JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
    JOIN sys.server_event_sessions ses ON xes.name = ses.name  
    WHERE xest.target_name = 'histogram' AND xes.name = 'test0'  
    go  
    ```  
  
7.  Al prompt dei comandi eseguire i comandi indicati di seguito per visualizzare i dati ETW.  
  
    > [!NOTE]  
    >  Per informazioni sul comando **tracerpt** , al prompt dei comandi immettere `tracerpt /?`.  
  
    ```  
    logman query -ets --- List the ETW sessions. This is optional.  
    logman update XE_DEFAULT_ETW_SESSION -fd -ets --- Flush the ETW log.  
    tracerpt %temp%\xeetw.etl -o xeetw.txt --- Dump the events so they can be seen.  
    ```  
  
8.  Eseguire le istruzioni indicate di seguito per arrestare la sessione eventi e rimuoverla dal server.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    STATE = STOP  
    go  
  
    DROP EVENT SESSION test0  
    ON SERVER  
    go  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-event-session-transact-sql)   
 [Viste del catalogo degli eventi estesi &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql)  
 [Viste a gestione dinamica degli eventi estesi](../views/views.md)   
 [Destinazioni degli eventi estesi di SQL Server](../../database-engine/sql-server-extended-events-targets.md)  
  
  
