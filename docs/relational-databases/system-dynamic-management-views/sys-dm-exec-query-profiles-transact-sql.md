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
ms.openlocfilehash: 1fb79f056e533f4aabacdab5e3467bedce22b696
ms.sourcegitcommit: e0178cb14954c45575a0bab73dcc7547014d03b3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2018
ms.locfileid: "52860094"
---
# <a name="sysdmexecqueryprofiles-transact-sql"></a>sys.dm_exec_query_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Monitora lo stato di avanzamento delle query in tempo reale mentre la query è in esecuzione. Usare, ad esempio, questa DMV per determinare la parte della query la cui esecuzione è lenta. Creare un join di questa DMV ad altre DMV di sistema utilizzando le colonne identificate nel campo descrizione. In alternativa, creare un join di questa DMV con altri contatori di prestazioni, ad esempio Performance Monitor, xperf, usando le colonne di tipo timestamp.  
  
## <a name="table-returned"></a>Tabella restituita  
 I contatori restituiti sono specifici per ogni operatore per ogni thread. I risultati sono dinamici e non corrispondono ai risultati delle opzioni esistenti come SET STATISTICS XML ON che creano l'output solo al termine della query.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|Identifica la sessione in cui viene eseguita la query. Fa riferimento a dm_exec_sessions.session_id.|  
|request_id|**int**|Identifica la richiesta di destinazione. Fa riferimento a dm_exec_sessions.request_id.|  
|sql_handle|**varbinary(64)**|Identifica la query di destinazione. Fa riferimento a dm_exec_query_stats.sql_handle.|  
|plan_handle|**varbinary(64)**|Identificare la query di destinazione (fa riferimento a dm_exec_query_stats.plan_handle.|  
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
 Se il nodo del piano di query non contiene I/O, tutti i contatori correlati alle operazioni di I/O vengono impostati su NULL.  
  
 I contatori correlati alle operazioni di I/O restituiti da questa DMV sono più granulari di quelli restituiti da SET STATISTICS IO nei due modi seguenti:  
  
-   SET STATISTICS IO raggruppa i contatori per tutte le operazioni di I/O in una tabella specifica. Con questa DMV si otterranno contatori separati per ogni nodo del piano di query che esegue operazioni di I/O nella tabella.  
  
-   In caso di analisi parallela, questa DMV restituisce i contatori per ogni thread parallelo usato nell'analisi.
 
A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, le statistiche di esecuzione di query standard dell'infrastruttura di profilatura è presente side-by-side con un'infrastruttura di analisi le statistiche di esecuzione query lightweight. Nuova query esecuzione infrastruttura delle statistiche profilatura riduce l'overhead delle prestazioni di raccolta delle statistiche di esecuzione query per ogni operatore, ad esempio il numero effettivo di righe. Questa funzionalità può essere abilitata tramite globale avvio [flag di traccia 7412](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), o viene attivata automaticamente quando l'evento esteso query_thread_profile viene utilizzato.

>[!NOTE]
> CPU e il tempo trascorso non sono supportati in infrastruttura profilatura delle statistiche esecuzione query lightweight per ridurre l'impatto sulle prestazioni.

SET STATISTICS XML ON e SET STATISTICS PROFILE ON utilizzare sempre le statistiche di esecuzione di query legacy infrastruttura di analisi.

Per abilitare l'output in DM exec_query_profiles effettuare quanto segue:

In [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 e in un secondo momento usare SET STATISTICS PROFILE ON o SET STATISTICS XML ON insieme alle query in corso il controllo. Ciò consente all'infrastruttura di profilatura e produce i risultati nella DMV per la sessione in cui è stato eseguito il comando SET. Se si sta analizzando una query in esecuzione da un'applicazione e non è possibile abilitare le opzioni SET con esso, è possibile creare un evento esteso tramite l'evento query_post_execution_showplan che attiverà l'infrastruttura di profilatura. 

Nelle [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, è possibile essere attivare [flag di traccia 7412](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) o usare l'evento esteso query_thread_profile.

>[!NOTE]
> La query in corso il controllo deve iniziare dopo aver abilitato la profilatura dell'infrastruttura. Se è già in esecuzione la query, avvio una sessione eventi estesi non produrrà i risultati in DM exec_query_profiles.


## <a name="permissions"></a>Permissions  

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], è necessario il `VIEW DATABASE STATE` autorizzazione nel database.   
   
## <a name="examples"></a>Esempi  
 Passaggio 1: accedere a una sessione in cui si intende eseguire la query da analizzare con sys.dm_exec_query_profiles. Per configurare la query per la profilatura utilizzare SET STATISTICS PROFILE in. Eseguire la query in questa stessa sessione.  
  
```  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 Passaggio 2: accedere a una seconda sessione, diversa dalla sessione in cui viene eseguita la query.  
  
 L'istruzione seguente riepiloga lo stato di avanzamento della query attualmente in esecuzione nella sessione 54. A tale scopo, viene calcolato il numero totale di righe di output restituite da tutti i thread per ogni nodo e confrontato con il numero stimato di righe di output per tale nodo.  
  
```  
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
  
  

