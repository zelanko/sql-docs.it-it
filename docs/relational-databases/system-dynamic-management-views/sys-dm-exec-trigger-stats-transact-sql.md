---
title: sys.dm_exec_trigger_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 42fc6848b89c57e6bfab40f1af96013fc73271f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66462710"
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce dati statistici aggregati sulle prestazioni dei trigger memorizzati nella cache. La vista contiene una riga per ogni trigger e la durata della riga è uguale al periodo in cui il trigger rimane memorizzato nella cache. Quando un trigger viene rimosso dalla cache, le righe corrispondenti vengono eliminate dalla vista. A quel punto, viene generato un evento di traccia SQL di perfomance Statistics simile a **DM exec_query_stats**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID del database in cui è contenuto il trigger.|  
|**object_id**|**int**|Numero di identificazione del trigger.|  
|**type**|**char(2)**|Tipo dell'oggetto:<br /><br /> TA = Trigger di assembly (CLR)<br /><br /> TR = trigger SQL|  
|**Type_desc**|**nvarchar(60)**|Descrizione del tipo di oggetto:<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|Può essere utilizzato per correlare le query nelle **DM exec_query_stats** eseguite dall'interno del trigger.|  
|**plan_handle**|**varbinary(64)**|Identificatore del piano in memoria. Si tratta di un identificatore temporaneo, che rimane costante solo se il piano rimane nella cache. Questo valore può essere utilizzato con il **DM exec_cached_plans** vista a gestione dinamica.|  
|**cached_time**|**datetime**|Ora in cui il trigger è stato aggiunto alla cache.|  
|**last_execution_time**|**datetime**|Ora dell'ultima esecuzione del trigger.|  
|**execution_count**|**bigint**|Il numero di volte in cui è stato eseguito il trigger perché ultima compilazione.|  
|**total_worker_time**|**bigint**|La quantità totale di tempo di CPU, espresso in microsecondi, utilizzato dalle esecuzioni del trigger a partire dalla relativa compilazione.|  
|**last_worker_time**|**bigint**|Tempo di CPU, in microsecondi, utilizzato durante l'ultima esecuzione del trigger.|  
|**min_worker_time**|**bigint**|Tempo di CPU massimo, espresso in microsecondi, utilizzato dal trigger durante una singola esecuzione.|  
|**max_worker_time**|**bigint**|Tempo di CPU massimo, espresso in microsecondi, utilizzato dal trigger durante una singola esecuzione.|  
|**total_physical_reads**|**bigint**|Numero totale di letture fisiche effettuate dalle esecuzioni del trigger dopo l'ultima compilazione.|  
|**last_physical_reads**|**bigint**|Il numero di letture fisiche eseguite l'ultima che esecuzione del trigger.|  
|**min_physical_reads**|**bigint**|Il numero minimo di letture fisiche che questo trigger effettuate durante una singola esecuzione.|  
|**max_physical_reads**|**bigint**|Il numero massimo di letture fisiche che questo trigger effettuate durante una singola esecuzione.|  
|**total_logical_writes**|**bigint**|Numero totale di scritture logiche effettuate dalle esecuzioni del trigger dopo l'ultima compilazione.|  
|**last_logical_writes**|**bigint**|Il numero di scritture logiche eseguite l'ultima che esecuzione del trigger.|  
|**min_logical_writes**|**bigint**|Il numero minimo di scritture logiche questo trigger effettuate durante una singola esecuzione.|  
|**max_logical_writes**|**bigint**|Il numero massimo di scritture logiche questo trigger effettuate durante una singola esecuzione.|  
|**total_logical_reads**|**bigint**|Numero totale di letture logiche effettuate dalle esecuzioni del trigger a partire dalla relativa compilazione.|  
|**last_logical_reads**|**bigint**|Il numero di letture logiche eseguite l'ultima che esecuzione del trigger.|  
|**min_logical_reads**|**bigint**|Il numero minimo di letture logiche questo trigger effettuate durante una singola esecuzione.|  
|**max_logical_reads**|**bigint**|Il numero massimo di letture logiche questo trigger effettuate durante una singola esecuzione.|  
|**total_elapsed_time**|**bigint**|Il tempo totale trascorso, espresso in microsecondi, per le esecuzioni complete del trigger.|  
|**last_elapsed_time**|**bigint**|Tempo trascorso, in microsecondi, per l'ultima esecuzione completata del trigger.|  
|**min_elapsed_time**|**bigint**|Il tempo minimo trascorso, espresso in microsecondi, per qualsiasi esecuzione completata del trigger.|  
|**max_elapsed_time**|**bigint**|Il tempo massimo trascorso, espresso in microsecondi, per qualsiasi esecuzione completata del trigger.| 
|**total_spills**|**bigint**|Il numero totale di pagine dopo l'ultima compilazione siano stati distribuiti tramite l'esecuzione del trigger.<br /><br /> **Si applica a**: A partire da [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**last_spills**|**bigint**|Il numero di pagine ha distribuito l'ultima che esecuzione del trigger.<br /><br /> **Si applica a**: A partire da [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**min_spills**|**bigint**|Il numero minimo di pagine che è mai stati inseriti vuoti questo trigger durante una singola esecuzione.<br /><br /> **Si applica a**: A partire da [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**max_spills**|**bigint**|Il numero massimo di pagine che è mai stati inseriti vuoti questo trigger durante una singola esecuzione.<br /><br /> **Si applica a**: A partire da [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**total_page_server_reads**|**bigint**|Numero totale di letture di server di pagine effettuate dalle esecuzioni del trigger a partire dalla relativa compilazione.<br /><br /> **Si applica a**: Con Iperscalabilità di Database SQL di Azure|  
|**last_page_server_reads**|**bigint**|Il numero di letture di pagine server eseguita l'ultima che esecuzione del trigger.<br /><br /> **Si applica a**: Con Iperscalabilità di Database SQL di Azure|  
|**min_page_server_reads**|**bigint**|Il numero minimo di server di pagina legge che questo trigger effettuate durante una singola esecuzione.<br /><br /> **Si applica a**: Con Iperscalabilità di Database SQL di Azure|  
|**max_page_server_reads**|**bigint**|Il numero massimo di server di pagina legge che questo trigger effettuate durante una singola esecuzione.<br /><br /> **Si applica a**: Con Iperscalabilità di Database SQL di Azure|  

  
## <a name="remarks"></a>Note  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)], le viste a gestione dinamica non possono esporre le informazioni che influenzerebbero l'indipendenza del database o le informazioni sugli altri database a cui l'utente dispone di accesso. Per evitare di esporre queste informazioni, ogni riga che contiene dati che non appartengono al tenant connesso viene filtrata.  

Le statistiche nella vista vengono aggiornate quando viene completata una query.  
  
## <a name="permissions"></a>Permissions  

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], è necessario il `VIEW DATABASE STATE` autorizzazione nel database.   
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni sui primi cinque trigger identificati in base al tempo medio trascorso.  
  
```sql  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Vedere anche  
[Funzioni e viste a gestione dinamica relative all'esecuzione &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
[sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
