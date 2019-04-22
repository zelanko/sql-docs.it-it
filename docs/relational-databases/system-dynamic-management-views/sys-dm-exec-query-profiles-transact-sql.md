---
title: sys.dm_exec_query_profiles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_profiles_TSQL
- sys.dm_exec_query_profiles_TSQL
- dm_exec_query_profiles
- sys.dm_exec_query_profiles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_profiles dynamic management view
ms.assetid: 54efc6cb-eea8-4f6d-a4d0-aa05eeb54081
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 87488f36a4b4b01181cd973a75d6e5c7f2e233d7
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860722"
---
# <a name="sysdmexecqueryprofiles-transact-sql"></a>sys.dm_exec_query_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

Monitora lo stato di avanzamento delle query in tempo reale mentre la query è in esecuzione. Usare, ad esempio, questa DMV per determinare la parte della query la cui esecuzione è lenta. Creare un join di questa DMV ad altre DMV di sistema utilizzando le colonne identificate nel campo descrizione. In alternativa, creare un join di questa DMV con altri contatori di prestazioni, ad esempio Performance Monitor, xperf, usando le colonne di tipo timestamp.  
  
## <a name="table-returned"></a>Tabella restituita  
I contatori restituiti sono specifici per ogni operatore per ogni thread. I risultati sono dinamici e non corrispondono, ad esempio i risultati delle opzioni esistenti `SET STATISTICS XML ON` che creano l'output solo al termine della query.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|Identifica la sessione in cui viene eseguita la query. Fa riferimento a dm_exec_sessions.session_id.|  
|request_id|**int**|Identifica la richiesta di destinazione. Fa riferimento a dm_exec_sessions.request_id.|  
|sql_handle|**varbinary(64)**|È un token che identifica in modo univoco il batch o una stored procedure che fa parte della query. Fa riferimento a dm_exec_query_stats.sql_handle.|  
|plan_handle|**varbinary(64)**|È un token che identifica in modo univoco un piano di esecuzione di query per un batch che ha eseguito e il piano risiede nella cache dei piani o attualmente in esecuzione. Fa riferimento a dm_exec_query_stats. plan_handle.|  
|physical_operator_name|**nvarchar(256)**|Nome dell'operatore fisico.|  
|node_id|**int**|Identifica un nodo operatore nell'albero della query.|  
|thread_id|**int**|Distingue i thread (per una query parallela) che appartengono allo stesso nodo operatore della query.|  
|task_address|**varbinary(8)**|Identifica l'attività SQLOS utilizzata da questo thread. Fa riferimento a dm_os_tasks.task_address.|  
|row_count|**bigint**|Numero di righe restituite finora dall'operatore.|  
|rewind_count|**bigint**|Numero di ripristini finora.|  
|rebind_count|**bigint**|Numero di riassociazioni finora.|  
|end_of_scan_count|**bigint**|Numero di analisi terminate finora.|  
|estimate_row_count|**bigint**|Numero stimato di righe. Può essere utile per confrontare il valore estimated_row_count con il valore row_count effettivo.|  
|first_active_time|**bigint**|Ora, in millisecondi, in cui l'operatore è stato chiamato la prima volta.|  
|last_active_time|**bigint**|Ora, in millisecondi, in cui l'operatore è stato chiamato l'ultima volta.|  
|open_time|**bigint**|Timestamp apertura in millisecondi.|  
|first_row_time|**bigint**|Timestamp in cui è stata aperta la prima riga in millisecondi.|  
|last_row_time|**bigint**|Timestamp in cui è stata aperta l'ultima riga in millisecondi.|  
|close_time|**bigint**|Timestamp chiusura in millisecondi.|  
|elapsed_time_ms|**bigint**|Tempo totale trascorso, in millisecondi, usato finora dalle operazioni del nodo di destinazione.|  
|cpu_time_ms|**bigint**|Totale CPU (in millisecondi) utilizzo finora dalle operazioni del nodo di destinazione.|  
|database_id|**smallint**|ID del database contenente l'oggetto in cui vengono eseguite le letture e le scritture.|  
|object_id|**int**|Identificatore dell'oggetto in cui vengono eseguite le letture e le scritture. Fa riferimento a sys.objects.object_id.|  
|index_id|**int**|Indice in cui viene aperto il set di righe.|  
|scan_count|**bigint**|Numero di analisi tabella/indice.|  
|logical_read_count|**bigint**|Numero di letture logiche.|  
|physical_read_count|**bigint**|Numero di letture fisiche.|  
|read_ahead_count|**bigint**|Numero di letture anticipate.|  
|write_page_count|**bigint**|Numero di scritture di pagina a causa dello spill.|  
|lob_logical_read_count|**bigint**|Numero di letture logiche LOB.|  
|lob_physical_read_count|**bigint**|Numero di letture fisiche LOB.|  
|lob_read_ahead_count|**bigint**|Numero di letture anticipate LOB.|  
|segment_read_count|**int**|Numero di letture anticipate di segmenti.|  
|segment_skip_count|**int**|Numero di segmenti ignorati finora.| 
|actual_read_row_count|**bigint**|Numero di righe lette da un operatore, prima è stato applicato il predicato residuo.| 
|estimated_read_row_count|**bigint**|**Si applica a:** A partire da [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1. <br/>Numero stimato di righe da leggere da un operatore prima che è stato applicato il predicato residuo.|  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Se il nodo del piano di query non dispone di tutti i/o, tutti i contatori relativi ai / O vengono impostati su NULL.  
  
 I contatori relativi ai / O restituiti da questa DMV sono più granulari di quelli restituiti da `SET STATISTICS IO` in due modi seguenti:  
  
-   `SET STATISTICS IO` Raggruppa i contatori per tutti i/o a una determinata tabella insieme. Con questa DMV si otterranno contatori separati per ogni nodo nel piano di query che esegue i/o alla tabella.  
  
-   In caso di analisi parallela, questa DMV restituisce i contatori per ogni thread parallelo usato nell'analisi.
 
A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, il *infrastruttura di analisi statistiche di esecuzione di query standard* presente side-by-side con un *infrastruttura di analisi delle statistiche di esecuzione query lightweight* . `SET STATISTICS XML ON` e `SET STATISTICS PROFILE ON` usano sempre il *infrastruttura di analisi statistiche di esecuzione di query standard*. Per `sys.dm_exec_query_profiles` modo alla compilazione, della query infrastrutture di profilatura deve essere attivato uno. Per altre informazioni, vedere [Infrastruttura di profilatura query](../../relational-databases/performance/query-profiling-infrastructure.md).    

>[!NOTE]
> La query in corso il controllo deve avviare **dopo aver** la query di infrastruttura di analisi è stata abilitata, abilitarla dopo l'avvio della query non produrrà i risultati in `sys.dm_exec_query_profiles`. Per altre informazioni su come abilitare la profilatura infrastrutture di query, vedere [Query profilatura infrastruttura](../../relational-databases/performance/query-profiling-infrastructure.md).

## <a name="permissions"></a>Permissions  

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], è necessario il `VIEW DATABASE STATE` autorizzazione nel database.   
   
## <a name="examples"></a>Esempi  
 Passaggio 1: Accedere a una sessione in cui si prevede di eseguire la query da analizzare con `sys.dm_exec_query_profiles`. Per configurare la query per l'uso del profiling `SET STATISTICS PROFILE ON`. Eseguire la query in questa stessa sessione.  
  
```sql  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above (not needed in SQL Server 2019)  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 Passaggio 2: Account di accesso a una seconda sessione diversa dalla sessione in cui viene eseguita la query.  
  
 L'istruzione seguente riepiloga lo stato di avanzamento della query attualmente in esecuzione nella sessione 54. A tale scopo, viene calcolato il numero totale di righe di output restituite da tutti i thread per ogni nodo e confrontato con il numero stimato di righe di output per tale nodo.  
  
```sql  
--Run this in a different session than the session in which your query is running. 
--Note that you may need to change session id 54 below with the session id you want to monitor.
SELECT node_id,physical_operator_name, SUM(row_count) row_count, 
  SUM(estimate_row_count) AS estimate_row_count, 
  CAST(SUM(row_count)*100 AS float)/SUM(estimate_row_count)  
FROM sys.dm_exec_query_profiles   
WHERE session_id=54
GROUP BY node_id,physical_operator_name  
ORDER BY node_id;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funzioni e viste a gestione dinamica relative all'esecuzione &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
 
