---
title: sys.dm_os_tasks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_tasks
- sys.dm_os_tasks_TSQL
- dm_os_tasks_TSQL
- dm_os_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_tasks dynamic management view
ms.assetid: 180a3c41-e71b-4670-819d-85ea7ef98bac
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6737242e5cf6cf39e846dba5e3d4b61168d8c694
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62627915"
---
# <a name="sysdmostasks-transact-sql"></a>sys.dm_os_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce una riga per ogni attività in corso nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Per chiamare questo elemento dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oppure [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], usare il nome **sys.dm_pdw_nodes_os_tasks**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|Indirizzo di memoria dell'oggetto.|  
|**task_state**|**nvarchar(60)**|Stato dell'attività. I possibili valori sono i seguenti:<br /><br /> IN SOSPESO: in attesa di un thread di lavoro.<br /><br /> ESEGUIBILE: Eseguibile, ma in attesa di ricevere un quantum.<br /><br /> CORSA: in esecuzione nell'utilità di pianificazione.<br /><br /> SOSPESO: Ha un ruolo di lavoro, ma è in attesa di un evento.<br /><br /> OPERAZIONE ESEGUITA: Completata.<br /><br /> SPINLOOP: Bloccato in uno spinlock.|  
|**context_switches_count**|**int**|Numero di cambi di contesto dell'utilità di pianificazione completati dall'attività.|  
|**pending_io_count**|**int**|Numero di I/O fisici eseguiti dall'attività.|  
|**pending_io_byte_count**|**bigint**|Numero totale di byte degli I/O eseguiti dall'attività.|  
|**pending_io_byte_average**|**int**|Numero medio di byte degli I/O eseguiti dall'attività.|  
|**scheduler_id**|**int**|ID dell'utilità di pianificazione padre. Si tratta di un handle per le informazioni dell'utilità di pianificazione per l'attività. Per altre informazioni, vedere [DM os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|**session_id**|**smallint**|ID della sessione associata all'attività.|  
|**exec_context_id**|**int**|ID del contesto di esecuzione associato all'attività.|  
|**request_id**|**int**|ID della richiesta dell'attività. Per altre informazioni, vedere [exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|**worker_address**|**varbinary(8)**|Indirizzo di memoria del thread di lavoro che sta eseguendo l'attività.<br /><br /> NULL = Per poter essere eseguita, l'attività è in attesa di un thread di lavoro oppure l'esecuzione dell'attività è stata completata.<br /><br /> Per altre informazioni, vedere [DM os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|**host_address**|**varbinary(8)**|Indirizzo di memoria dell'host.<br /><br /> 0 = Per creare l'attività non è stato utilizzato alcun host. Ciò semplifica l'identificazione dell'host utilizzato per creare l'attività.<br /><br /> Per altre informazioni, vedere [sys.dm_os_hosts &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md).|  
|**parent_task_address**|**varbinary(8)**|Indirizzo di memoria dell'attività padre dell'oggetto.|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo in questa distribuzione.|  
  
## <a name="permissions"></a>Permissions

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], è necessario il `VIEW DATABASE STATE` autorizzazione nel database.   

## <a name="examples"></a>Esempi  
  
### <a name="a-monitoring-parallel-requests"></a>A. Monitoraggio di richieste in parallelo  
 Le richieste che vengono eseguite in parallelo, verranno visualizzate più righe per la stessa combinazione di (\<**session_id**>, \< **request_id**>). Usare la query seguente per trovare le [configurare il max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) per tutte le richieste attive.  
  
> [!NOTE]  
>  Oggetto **request_id** è univoco all'interno di una sessione.  
  
```  
SELECT  
    task_address,  
    task_state,  
    context_switches_count,  
    pending_io_count,  
    pending_io_byte_count,  
    pending_io_byte_average,  
    scheduler_id,  
    session_id,  
    exec_context_id,  
    request_id,  
    worker_address,  
    host_address  
  FROM sys.dm_os_tasks  
  ORDER BY session_id, request_id;  
```  
  
### <a name="b-associating-session-ids-with-windows-threads"></a>B. Associazione di ID di sessione con thread di Windows  
 È possibile utilizzare la query seguente per associare un valore di ID di sessione a un ID di thread di Windows. È possibile monitorare le prestazioni del thread utilizzando Performance Monitor di Windows. La query seguente non restituisce informazioni per le sessioni sospese.  
  
```  
SELECT STasks.session_id, SThreads.os_thread_id  
  FROM sys.dm_os_tasks AS STasks  
  INNER JOIN sys.dm_os_threads AS SThreads  
    ON STasks.worker_address = SThreads.worker_address  
  WHERE STasks.session_id IS NOT NULL  
  ORDER BY STasks.session_id;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
  [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


