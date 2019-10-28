---
title: Monitorare l'attività del sistema mediante gli eventi estesi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- xe
- extended events [SQL Server], monitoring system activity
ms.assetid: d83ad88f-818c-49fe-a9a9-299f704fca53
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 56286a2684f5b8b7f7af9915f3148c0a4c99771e
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72906083"
---
# <a name="monitor-system-activity-using-extended-events"></a>Monitorare l'attività del sistema mediante gli eventi estesi

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

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
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [Viste del catalogo degli eventi estesi &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Viste a gestione dinamica degli eventi estesi](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [Destinazioni degli eventi estesi di SQL Server](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)  
  
  
