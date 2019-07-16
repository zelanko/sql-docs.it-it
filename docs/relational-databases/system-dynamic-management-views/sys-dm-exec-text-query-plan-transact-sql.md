---
title: sys.dm_exec_text_query_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_text_query_plan
- sys.dm_exec_text_query_plan_TSQL
- dm_exec_text_query_plan_TSQL
- sys.dm_exec_text_query_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_text_query_plan dynamic management function
ms.assetid: 9d5e5f59-6973-4df9-9eb2-9372f354ca57
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5016f6f556967fa45364460280080ca829e521b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936886"
---
# <a name="sysdmexectextqueryplan-transact-sql"></a>sys.dm_exec_text_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Restituisce il piano Showplan in formato testo per un batch [!INCLUDE[tsql](../../includes/tsql-md.md)] o per un'istruzione specifica nel batch. Il piano di query specificato tramite l'handle del piano possono essere memorizzati nella cache o attualmente in esecuzione. Questa funzione con valori di tabella è simile a [DM exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md), ma presenta le seguenti differenze:  
  
-   L'output del piano di query viene restituito in formato testo.  
-   Per l'output del piano di query non sono previsti limiti di dimensioni.  
-   È possibile specificare singole istruzioni nel batch.  
  
**Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sys.dm_exec_text_query_plan   
(   
    plan_handle   
    , { statement_start_offset | 0 | DEFAULT }  
        , { statement_end_offset | -1 | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>Argomenti  
*plan_handle*  
È un token che identifica in modo univoco un piano di esecuzione di query per un batch che ha eseguito e il piano risiede nella cache dei piani o attualmente in esecuzione. *plan_handle* viene **varbinary(64)** .   

Il *plan_handle* può essere ottenuto dagli oggetti a gestione dinamica seguenti: 
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
*statement_start_offset* | 0 | DEFAULT  
Indica, in byte, la posizione iniziale della query descritta dalla riga all'interno del testo del batch o dell'oggetto persistente. *statement_start_offset* viene **int**. Il valore 0 indica l'inizio del batch. Il valore predefinito è 0.  
  
È possibile ottenere l'offset iniziale dell'istruzione dagli oggetti a gestione dinamica seguenti:  
  
-  [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-  [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
*statement_end_offset* | -1 | DEFAULT  
Indica, in byte, la posizione finale della query descritta dalla riga all'interno del testo del batch o dell'oggetto persistente.  
  
*statement_start_offset* viene **int**.  
  
Il valore -1 indica la fine del batch. Il valore predefinito è -1.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|ID del database di contesto attivo al momento della compilazione dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] corrispondente a questo piano. Per istruzioni SQL ad hoc e preparate, l'ID del database in cui sono state compilate le istruzioni.<br /><br /> La colonna ammette i valori Null.|  
|**objectid**|**int**|ID dell'oggetto (ad esempio, stored procedure o funzione definita dall'utente) per il piano della query. Per i batch ad hoc e preparate, questa colonna è **null**.<br /><br /> La colonna ammette i valori Null.|  
|**number**|**smallint**|Valore intero della stored procedure numerata. Ad esempio, un gruppo di procedure per la **ordini** dell'applicazione potrebbe essere denominata **orderproc; 1**, **orderproc; 2**e così via. Per i batch ad hoc e preparate, questa colonna è **null**.<br /><br /> La colonna ammette i valori Null.|  
|**encrypted**|**bit**|Indica se la stored procedure corrispondente è crittografata.<br /><br /> 0 = non crittografata<br /><br /> 1 = crittografata<br /><br /> La colonna non ammette i valori Null.|  
|**query_plan**|**nvarchar(max)**|Contiene la rappresentazione Showplan della fase di compilazione del piano di esecuzione di query specificato con *plan_handle*. La rappresentazione Showplan è in formato testo. Viene generato un piano per ogni batch contenente ad esempio istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, chiamate di stored procedure e chiamate di funzioni definite dall'utente.<br /><br /> La colonna ammette i valori Null.|  
  
## <a name="remarks"></a>Note  
 Nelle condizioni seguenti, non viene restituito alcun output Showplan nella **piano** della colonna della tabella restituita per **DM exec_text_query_plan**:  
  
-   Se il piano della query viene specificato tramite *plan_handle* è stato eliminato dalla cache dei piani, il **query_plan** colonna della tabella restituita è null. Ad esempio, questa condizione può verificarsi se non si verifica un ritardo tra quando viene acquisito l'handle del piano e quando è stato usato con **DM exec_text_query_plan**.  
  
-   Alcune istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] non vengono memorizzate nella cache, ad esempio le istruzioni per operazioni bulk o le istruzioni che contengono valori letterali stringa con dimensioni maggiori di 8 KB. Showplan per tali istruzioni non può essere recuperato tramite **DM exec_text_query_plan** perché non sono presenti nella cache.  
  
-   Se un [!INCLUDE[tsql](../../includes/tsql-md.md)] batch o stored procedure contiene una chiamata a una funzione definita dall'utente o una chiamata a codice SQL dinamico, ad esempio tramite EXEC (*stringa*), il piano Showplan XML compilato per la funzione definita dall'utente non è incluso nella tabella restituito da **DM exec_text_query_plan** per la stored procedure o batch. Invece, è necessario eseguire una chiamata separata a **DM exec_text_query_plan** per il *plan_handle* che corrisponde alla funzione definita dall'utente.  
  
Quando viene utilizzata una query ad hoc [semplice](../../relational-databases/query-processing-architecture-guide.md#SimpleParam) oppure [parametrizzazione forzata](../../relational-databases/query-processing-architecture-guide.md#ForcedParam), il **query_plan** colonna conterrà solo il testo dell'istruzione e non il piano di query effettivo. Per restituire il piano di query, chiamare **DM exec_text_query_plan** per l'handle del piano di query con parametri preparata. È possibile determinare se la query è stata parametrizzata facendo riferimento il **sql** della colonna della [Sys. syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) visualizzazione o la colonna di testo del [DM exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)vista a gestione dinamica.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire **DM exec_text_query_plan**, un utente deve essere un membro delle **sysadmin** ruolo predefinito del server o disporre dell'autorizzazione VIEW SERVER STATE nel server.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-retrieving-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>R. Recupero del piano della query memorizzato nella cache per un query o un batch Transact-SQL con esecuzione prolungata  
 Se l'esecuzione di una query o un batch [!INCLUDE[tsql](../../includes/tsql-md.md)] risulta prolungata in una particolare connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile recuperare il piano di esecuzione di tale query o batch per individuare le cause del ritardo. Nell'esempio seguente viene illustrato come recuperare il piano Showplan per una query o un batch con esecuzione prolungata.  
  
> [!NOTE]  
> Per eseguire questo esempio, sostituire i valori per *session_id* e *plan_handle* con valori specifici del server.  
  
 Utilizzare innanzitutto la stored procedure `sp_who` per recuperare l'ID del processo server (SPID, Server Process ID) per il processo che esegue la query o il batch:  
  
```sql  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
 Il set dei risultati restituito da `sp_who` indica che il valore di SPID è `54`. È possibile utilizzare questo SPID con la vista a gestione dinamica `sys.dm_exec_requests` per recuperare l'handle del piano utilizzando la query seguente:  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_requests  
WHERE session_id = 54;  
GO  
```  
  
 La tabella restituita da **exec_requests** indica che l'handle del piano per la query con esecuzione rallentata o il batch è `0x06000100A27E7C1FA821B10600`. Nell'esempio seguente viene restituito il piano di query per l'handle del piano specificato e vengono utilizzati i valori predefiniti 0 e -1 per restituire tutte le istruzioni nella query o nel batch.  
  
```sql  
USE master;  
GO  
SELECT query_plan   
FROM sys.dm_exec_text_query_plan (0x06000100A27E7C1FA821B10600,0,-1);  
GO  
```  
  
### <a name="b-retrieving-every-query-plan-from-the-plan-cache"></a>B. Recupero di tutti i piani di query dalla cache dei piani  
 Per recuperare uno snapshot di tutti i piani di query disponibili nella cache dei piani, è possibile recuperare gli handle per tutti i piani di query nella cache eseguendo una query sulla vista a gestione dinamica `sys.dm_exec_cached_plans`. Gli handle dei piani sono archiviati nella colonna `plan_handle` della vista `sys.dm_exec_cached_plans`. È quindi necessario utilizzare l'operatore CROSS APPLY per passare gli handle dei piani a `sys.dm_exec_text_query_plan` come illustrato di seguito. L'output Showplan per ogni piano disponibile nella cache dei piani è nel `query_plan` colonna della tabella restituita.  
  
```sql  
USE master;  
GO  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_text_query_plan(cp.plan_handle, DEFAULT, DEFAULT);  
GO  
```  
  
### <a name="c-retrieving-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. Recupero di tutti i piani di query per cui il server ha raccolto informazioni statistiche sulle query dalla cache dei piani  
 Per recuperare uno snapshot di tutti i piani di query disponibili nella cache dei piani per i quali il server ha raccolto informazioni statistiche, è possibile recuperare gli handle dei piani per tutti i piani di query nella cache eseguendo una query sulla vista a gestione dinamica `sys.dm_exec_query_stats`. Gli handle dei piani sono archiviati nella colonna `plan_handle` della vista `sys.dm_exec_query_stats`. È quindi necessario utilizzare l'operatore CROSS APPLY per passare gli handle dei piani a `sys.dm_exec_text_query_plan` come illustrato di seguito. L'output Showplan per ogni piano viene indicato nella colonna `query_plan` della tabella restituita.  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset);  
GO  
```  
  
### <a name="d-retrieving-information-about-the-top-five-queries-by-average-cpu-time"></a>D. Recupero di informazioni sulle prime cinque query in base al tempo medio di CPU  
 Nell'esempio seguente vengono restituiti i piani di query e il tempo medio di CPU per le prime cinque query. Il **DM exec_text_query_plan** funzione specifica i valori predefiniti 0 e -1 per restituire tutte le istruzioni nel batch nel piano di query.  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
Plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, 0, -1)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
