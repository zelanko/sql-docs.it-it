---
title: sys.dm_exec_query_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_plan_TSQL
- sys.dm_exec_query_plan
- dm_exec_query_plan
- sys.dm_exec_query_plan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_plan dynamic management function
ms.assetid: e26f0867-9be3-4b2e-969e-7f2840230770
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c879af413bd8b3cf4b90e8112f10e5f756201148
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013268"
---
# <a name="sysdmexecqueryplan-transact-sql"></a>sys.dm_exec_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Restituisce il piano Showplan in formato XML per il batch specificato dall'handle di piano. Il piano specificato tramite l'handle di piano può essere memorizzato nella cache o in esecuzione.  
  
il XML schema per Showplan è pubblicato e disponibile all'indirizzo [sito Web Microsoft](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409). È inoltre disponibile nella directory di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sys.dm_exec_query_plan(plan_handle)  
```  
  
## <a name="arguments"></a>Argomenti  
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
|**dbid**|**smallint**|ID del database di contesto attivo al momento della compilazione dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] corrispondente a questo piano. Per istruzioni SQL ad hoc e preparate, l'ID del database in cui sono state compilate le istruzioni.<br /><br /> La colonna ammette i valori Null.|  
|**objectid**|**int**|ID dell'oggetto (ad esempio, stored procedure o funzione definita dall'utente) per il piano della query. Per i batch ad hoc e preparate, questa colonna è **null**.<br /><br /> La colonna ammette i valori Null.|  
|**number**|**smallint**|Valore intero della stored procedure numerata. Ad esempio, un gruppo di procedure per la **ordini** dell'applicazione potrebbe essere denominata **orderproc; 1**, **orderproc; 2**e così via. Per i batch ad hoc e preparate, questa colonna è **null**.<br /><br /> La colonna ammette i valori Null.|  
|**encrypted**|**bit**|Indica se la stored procedure corrispondente è crittografata.<br /><br /> 0 = non crittografata<br /><br /> 1 = crittografata<br /><br /> La colonna non ammette i valori Null.|  
|**query_plan**|**xml**|Contiene la rappresentazione Showplan della fase di compilazione del piano di esecuzione di query specificato con *plan_handle*. La rappresentazione Showplan è in formato XML. Viene generato un piano per ogni batch contenente ad esempio istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, chiamate di stored procedure e chiamate di funzioni definite dall'utente.<br /><br /> La colonna ammette i valori Null.|  
  
## <a name="remarks"></a>Note  
 Nelle condizioni seguenti, non viene restituito alcun output Showplan nella **query_plan** della colonna della tabella restituita per **DM exec_query_plan**:  
  
-   Se il piano della query viene specificato tramite *plan_handle* è stato eliminato dalla cache dei piani, il **query_plan** colonna della tabella restituita è null. Ad esempio, questa condizione può verificarsi se non si verifica un ritardo tra quando viene acquisito l'handle del piano e quando è stato usato con **DM exec_query_plan**.  
  
-   Alcune istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] non vengono memorizzate nella cache, ad esempio le istruzioni per operazioni bulk o le istruzioni che contengono valori letterali stringa con dimensioni maggiori di 8 KB. Showplan XML per tali istruzioni non può essere recuperato tramite **DM exec_query_plan** , a meno che il batch è attualmente in esecuzione perché non sono presenti nella cache.  
  
-   Se un [!INCLUDE[tsql](../../includes/tsql-md.md)] batch o stored procedure contiene una chiamata a una funzione definita dall'utente o una chiamata a codice SQL dinamico, ad esempio tramite EXEC (*stringa*), il piano Showplan XML compilato per la funzione definita dall'utente non è incluso nella tabella restituito da **DM exec_query_plan** per la stored procedure o batch. Invece, è necessario eseguire una chiamata separata a **DM exec_query_plan** per l'handle di piano corrispondente alla funzione definita dall'utente.  
  
 Quando una query ad hoc utilizza la parametrizzazione semplice o forzata, la **query_plan** colonna conterrà solo il testo dell'istruzione e non il piano di query effettivo. Per restituire il piano di query, chiamare **DM exec_query_plan** per l'handle del piano di query con parametri preparata. È possibile determinare se la query è stata parametrizzata facendo riferimento il **sql** della colonna della [Sys. syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) visualizzazione o la colonna di testo del [DM exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)vista a gestione dinamica.  
  
> [!NOTE] 
> A causa di una limitazione del numero di livelli nidificati consentiti il **xml** tipo di dati **DM exec_query_plan** non è possibile restituire i piani di query che soddisfino o superano 128 livelli di elementi annidati. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa condizione impediva il completamento del piano di query e generava l'errore 6335. Nelle [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 e versioni successive, il **query_plan** colonna viene restituito NULL.   
> È possibile usare la [DM exec_text_query_plan &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md) funzione a gestione dinamica per restituire l'output del piano di query in formato testo.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire **DM exec_query_plan**, un utente deve essere un membro del **sysadmin** ruolo predefinito del server o avere il `VIEW SERVER STATE` autorizzazione nel server.  
  
## <a name="examples"></a>Esempi  
 Gli esempi seguenti illustrano come usare il **DM exec_query_plan** vista a gestione dinamica.  
  
 Per visualizzare gli Showplan XML, eseguire le query seguenti nell'Editor di Query del [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], quindi fare clic su **ShowPlanXML** nel **query_plan** colonna della tabella restituita da **vista exec_query_plan**. Il piano Showplan XML verrà visualizzato nel riquadro di riepilogo di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Per salvare il piano Showplan XML in un file, fare doppio clic su **ShowPlanXML** nel **query_plan** colonna, fare clic su **Salva risultati con nome**, denominare il file nel formato \< *file_name*> sqlplan; ad esempio ShowPlanXml.  
  
### <a name="a-retrieve-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. Recupero del piano di query memorizzato nella cache per un query o un batch Transact-SQL con esecuzione prolungata  
 I piani delle query per vari tipi di batch [!INCLUDE[tsql](../../includes/tsql-md.md)], come batch ad hoc, stored procedure e funzioni definite dall'utente, vengono memorizzati nella cache in un'area della memoria denominata cache dei piani. Ogni piano della query memorizzato nella cache è identificato da un ID univoco denominato handle del piano. È possibile specificare l'handle del piano con il **DM exec_query_plan** vista a gestione dinamica per recuperare il piano di esecuzione per un particolare [!INCLUDE[tsql](../../includes/tsql-md.md)] query o batch.  
  
 Se l'esecuzione di una query o un batch [!INCLUDE[tsql](../../includes/tsql-md.md)] risulta prolungata in una particolare connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile recuperare il piano di esecuzione di tale query o batch per individuare le cause del ritardo. Nell'esempio seguente viene illustrato come recuperare il piano Showplan XML per una query o un batch con esecuzione prolungata.  
  
> [!NOTE]  
>  Per eseguire questo esempio, sostituire i valori per *session_id* e *plan_handle* con valori specifici del server.  
  
 Utilizzare innanzitutto la stored procedure `sp_who` per recuperare l'ID del processo server (SPID, Server Process ID) per il processo che esegue la query o il batch:  
  
```sql  
USE master;  
GO  
exec sp_who;  
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
  
 La tabella restituita da **exec_requests** indica che l'handle del piano per la query con esecuzione rallentata o il batch viene `0x06000100A27E7C1FA821B10600`, che è possibile specificare come il *plan_handle* argomento con `sys.dm_exec_query_plan` per recuperare il piano di esecuzione in formato XML come indicato di seguito. Il piano di esecuzione in formato XML per la query con esecuzione rallentata o il batch è contenuto nel **query_plan** della colonna della tabella restituita da `sys.dm_exec_query_plan`.  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_query_plan (0x06000100A27E7C1FA821B10600);  
GO  
```  
  
### <a name="b-retrieve-every-query-plan-from-the-plan-cache"></a>B. Recupero di tutti i piani di query dalla cache dei piani  
 Per recuperare uno snapshot di tutti i piani di query disponibili nella cache dei piani, è possibile recuperare gli handle per tutti i piani di query nella cache eseguendo una query sulla vista a gestione dinamica `sys.dm_exec_cached_plans`. Gli handle dei piani sono archiviati nella colonna `plan_handle` della vista `sys.dm_exec_cached_plans`. È quindi necessario utilizzare l'operatore CROSS APPLY per passare gli handle dei piani a `sys.dm_exec_query_plan` come illustrato di seguito. L'output Showplan XML per ogni piano disponibile nella cache dei piani viene indicato nella colonna `query_plan` della tabella restituita.  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_cached_plans AS cp 
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
GO  
```  
  
### <a name="c-retrieve-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. Recupero di tutti i piani di query per cui sono state raccolte informazioni statistiche sulle query dalla cache dei piani da parte del server  
 Per recuperare uno snapshot di tutti i piani di query disponibili nella cache dei piani per i quali il server ha raccolto informazioni statistiche, è possibile recuperare gli handle dei piani per tutti i piani di query nella cache eseguendo una query sulla vista a gestione dinamica `sys.dm_exec_query_stats`. Gli handle dei piani sono archiviati nella colonna `plan_handle` della vista `sys.dm_exec_query_stats`. È quindi necessario utilizzare l'operatore CROSS APPLY per passare gli handle dei piani a `sys.dm_exec_query_plan` come illustrato di seguito. L'output Showplan XML per ogni piano disponibile nella cache dei piani per cui il server ha raccolto informazioni statistiche viene indicato nella colonna `query_plan` della tabella restituita.  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_query_stats AS qs 
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle);  
GO  
```  
  
### <a name="d-retrieve-information-about-the-top-five-queries-by-average-cpu-time"></a>D. Recupero di informazioni sulle prime cinque query in base al tempo medio di CPU  
 Nell'esempio seguente vengono restituiti i piani e il tempo medio di CPU per le prime cinque query.  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
   plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sys.dm exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [Guida di riferimento a operatori Showplan logici e fisici](../../relational-databases/showplan-logical-and-physical-operators-reference.md)   
 [sys.dm_exec_text_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)  
  
  
