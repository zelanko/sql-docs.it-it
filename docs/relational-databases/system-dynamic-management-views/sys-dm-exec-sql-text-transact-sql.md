---
title: sys.dm_exec_sql_text (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_sql_text
- sys.dm_exec_sql_text
- sys.dm_exec_sql_text_TSQL
- dm_exec_sql_text_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_sql_text dynamic management function
ms.assetid: 61b8ad6a-bf80-490c-92db-58dfdff22a24
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 48554e48d09822b23320d36080084d4947882736
ms.sourcegitcommit: d92ad400799d8b74d5c601170167b86221f68afb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/16/2019
ms.locfileid: "58080283"
---
# <a name="sysdmexecsqltext-transact-sql"></a>sys.dm_exec_sql_text (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce il testo dell'istruzione SQL batch identificato dall'oggetto specificato *sql_handle*. Questa funzione con valori di tabella sostituisce la funzione di sistema **fn_get_sql**.  
  
 
## <a name="syntax"></a>Sintassi  
  
```  
sys.dm_exec_sql_text(sql_handle | plan_handle)  
```  
  
## <a name="arguments"></a>Argomenti  
*sql_handle*  
È un token che identifica in modo univoco un batch che ha eseguito o attualmente in esecuzione. *valore di sql_handle* viene **varbinary(64)**. 

Il *sql_handle* può essere ottenuto dagli oggetti a gestione dinamica seguenti:  
  
-   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)  
  
-   [sys.dm_exec_xml_handles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)  
  
-   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  
  
*plan_handle*  
È un token che identifica in modo univoco un piano di esecuzione di query per un batch che ha eseguito e il piano risiede nella cache dei piani o attualmente in esecuzione. *plan_handle* viene **varbinary(64)**.   

Il *plan_handle* può essere ottenuto dagli oggetti a gestione dinamica seguenti:    
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|ID del database.<br /><br /> Per istruzioni SQL ad hoc e preparate, l'ID del database in cui sono state compilate le istruzioni.|  
|**objectid**|**int**|ID dell'oggetto.<br /><br /> Per istruzioni SQL ad hoc e preparate viene restituito NULL.|  
|**number**|**smallint**|Per una stored procedure numerata, questa colonna restituisce il numero della stored procedure. Per altre informazioni, vedere [numbered_procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md).<br /><br /> Per istruzioni SQL ad hoc e preparate viene restituito NULL.|  
|**encrypted**|**bit**|1 = Il testo SQL è crittografato.<br /><br /> 0 = Il testo SQL non è crittografato.|  
|**text**|**nvarchar(max** **)**|Testo della query SQL.<br /><br /> Per gli oggetti crittografati viene restituito NULL.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione `VIEW SERVER STATE` per il server.  
  
## <a name="remarks"></a>Note  
Per le query ad hoc, gli handle SQL sono valori basati sul testo SQL inviato al server e possono provenire da qualsiasi database. 

Per alcuni oggetti di database, ad esempio stored procedure, trigger o funzioni, gli handle SQL sono derivati dall'ID di database e dall'ID e dal numero dell'oggetto. 

Handle del piano è un valore hash derivato dal piano compilato dell'intero batch. 

> [!NOTE]
> **DBID** non può essere determinato dalle *sql_handle* query ad hoc. Per determinare **dbid** query ad hoc, usare *plan_handle* invece.
  
## <a name="examples"></a>Esempi 

### <a name="a-conceptual-example"></a>A. Esempio concettuale
Di seguito è riportato un esempio di base per illustrare il passaggio di un **sql_handle** direttamente o con **CROSS APPLY**.
  1.  Creare attività.  
Eseguire T-SQL seguente in una nuova finestra query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].   
      ```sql
      -- Identify current spid (session_id)
      SELECT @@SPID;
      GO
  
      -- Create activity
        WAITFOR DELAY '00:02:00';
      ```
      
    2.  Usando **CROSS APPLY**.  
    Il valore sql_handle restituito da **exec_requests** verranno passati al **DM exec_sql_text** usando **CROSS APPLY**. Aprire una nuova finestra query e passare il valore di spid identificati nel passaggio 1. In questo esempio il valore di spid non dovesse essere `59`.

        ```sql
        SELECT t.*
        FROM sys.dm_exec_requests AS r
        CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t
        WHERE session_id = 59 -- modify this value with your actual spid
         ```      
 
    2.  Il passaggio **sql_handle** direttamente.  
Acquisire le **sql_handle** dalla **exec_requests**. Passare quindi il **sql_handle** direttamente **DM exec_sql_text**. Aprire una nuova finestra query e passare il valore di spid identificati nel passaggio 1 per **exec_requests**. In questo esempio il valore di spid non dovesse essere `59`. Quindi passare l'oggetto restituito **sql_handle** come argomento al **DM exec_sql_text**.

        ```sql
        -- acquire sql_handle
        SELECT sql_handle FROM sys.dm_exec_requests WHERE session_id = 59  -- modify this value with your actual spid
        
        -- pass sql_handle to sys.dm_exec_sql_text
        SELECT * FROM sys.dm_exec_sql_text(0x01000600B74C2A1300D2582A2100000000000000000000000000000000000000000000000000000000000000) -- modify this value with your actual sql_handle
         ```      
    
  
### <a name="b-obtain-information-about-the-top-five-queries-by-average-cpu-time"></a>b. Ottenere informazioni sulle prime cinque query per tempo medio CPU  
 Nell'esempio seguente vengono restituiti il testo dell'istruzione SQL e il tempo medio di CPU per le prime cinque query.  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
    SUBSTRING(st.text, (qs.statement_start_offset/2)+1,   
        ((CASE qs.statement_end_offset  
          WHEN -1 THEN DATALENGTH(st.text)  
         ELSE qs.statement_end_offset  
         END - qs.statement_start_offset)/2) + 1) AS statement_text  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
ORDER BY total_worker_time/execution_count DESC;  
```  
  
### <a name="c-provide-batch-execution-statistics"></a>C. Fornisce statistiche di esecuzione batch  
 Nell'esempio seguente viene restituito il testo delle query SQL eseguite in batch e vengono visualizzate le relative informazioni statistiche.  
  
```sql  
SELECT s2.dbid,   
    s1.sql_handle,    
    (SELECT TOP 1 SUBSTRING(s2.text,statement_start_offset / 2+1 ,   
      ( (CASE WHEN statement_end_offset = -1   
         THEN (LEN(CONVERT(nvarchar(max),s2.text)) * 2)   
         ELSE statement_end_offset END)  - statement_start_offset) / 2+1))  AS sql_statement,  
    execution_count,   
    plan_generation_num,   
    last_execution_time,     
    total_worker_time,   
    last_worker_time,   
    min_worker_time,   
    max_worker_time,  
    total_physical_reads,   
    last_physical_reads,   
    min_physical_reads,    
    max_physical_reads,    
    total_logical_writes,   
    last_logical_writes,   
    min_logical_writes,   
    max_logical_writes    
FROM sys.dm_exec_query_stats AS s1   
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS s2    
WHERE s2.objectid is null   
ORDER BY s1.sql_handle, s1.statement_start_offset, s1.statement_end_offset;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funzioni e viste a gestione dinamica relative all'esecuzione &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_cursors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)   
 [sys.dm_exec_xml_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [Using APPLY](../../t-sql/queries/from-transact-sql.md#using-apply)   [sys.dm_exec_text_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)  

