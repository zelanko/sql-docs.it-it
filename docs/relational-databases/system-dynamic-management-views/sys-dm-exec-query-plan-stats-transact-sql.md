---
title: sys.dm_exec_query_plan_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_plan_stats
- sys.dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats
helpviewer_keywords:
- sys.dm_exec_query_plan_stats management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfacb
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: c4d4f58161885519767e299683fe32b5197a045f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66198212"
---
# <a name="sysdmexecqueryplanstats-transact-sql"></a>sys.dm_exec_query_plan_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

Restituisce l'equivalente dell'ultimo piano di esecuzione effettivo per un piano di query memorizzati nella cache in precedenza.

## <a name="syntax"></a>Sintassi

```
sys.dm_exec_query_plan_stats(plan_handle)  
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

## <a name="table-returned"></a>Tabella restituita

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|
|**dbid**|**smallint**|ID del database di contesto attivo al momento della compilazione dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] corrispondente a questo piano. Per istruzioni SQL ad hoc e preparate, l'ID del database in cui sono state compilate le istruzioni.<br /><br /> La colonna ammette i valori Null.|  
|**objectid**|**int**|ID dell'oggetto (ad esempio, stored procedure o funzione definita dall'utente) per il piano della query. Per i batch ad hoc e preparate, questa colonna è **null**.<br /><br /> La colonna ammette i valori Null.|  
|**number**|**smallint**|Valore intero della stored procedure numerata. Ad esempio, un gruppo di procedure per la **ordini** dell'applicazione potrebbe essere denominata **orderproc; 1**, **orderproc; 2**e così via. Per i batch ad hoc e preparate, questa colonna è **null**.<br /><br /> La colonna ammette i valori Null.|  
|**encrypted**|**bit**|Indica se la stored procedure corrispondente è crittografata.<br /><br /> 0 = non crittografata<br /><br /> 1 = crittografata<br /><br /> La colonna non ammette i valori Null.|  
|**query_plan**|**xml**|Contiene il runtime noto ultimo rappresentazione Showplan del piano di esecuzione query effettivo che viene specificato con *plan_handle*. La rappresentazione Showplan è in formato XML. Viene generato un piano per ogni batch contenente ad esempio istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, chiamate di stored procedure e chiamate di funzioni definite dall'utente.<br /><br /> La colonna ammette i valori Null.| 

## <a name="remarks"></a>Note
Questa funzione di sistema è disponibile a partire [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.4.

Questa funzione prevede il consenso esplicito e richiede l'abilitazione del [flag di traccia](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451. a partire da [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.5, per eseguire questa operazione a livello di database, vedere l'opzione LAST_QUERY_PLAN_STATS in [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

Questa funzione di sistema funziona con il **leggero** infrastruttura di analisi delle statistiche di esecuzione di query. Per altre informazioni, vedere [Infrastruttura di profilatura query](../../relational-databases/performance/query-profiling-infrastructure.md).  

Nelle condizioni seguenti, l'output uno Showplan **equivalente a un piano di esecuzione effettivo** viene restituito nel **query_plan** colonna della tabella restituita per **sys.dm_exec_query_plan_ statistiche**:  

-   Il piano è reperibile nel [DM exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md).     
    **AND**    
-   La query in fase di esecuzione è complesso o maggior consumo di risorse.

Nelle condizioni seguenti, una **semplificata <sup>1</sup>**  viene restituito nell'output Showplan il **query_plan** colonna della tabella restituita per **sys.dm_exec_ query_plan_stats**:  

-   Il piano è reperibile nel [DM exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md).     
    **AND**    
-   La query è molto semplice, in genere suddivisi in categorie come parte di un carico di lavoro OLTP.

<sup>1</sup> partire [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 2.5 CTP, si riferisce a un piano Showplan contenente solo l'operatore di nodo radice (SELECT). Per la [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.4 si riferisce al piano memorizzato nella cache come disponibili tramite `sys.dm_exec_cached_plans`.

Le seguenti condizioni **viene restituito alcun output** dalla **sys.dm_exec_query_plan_stats**:

-   Il piano di query specificato tramite *plan_handle* sia stato rimosso dalla cache dei piani.     
    **OR**    
-   In primo luogo il piano di query non è memorizzabile nella cache. Per altre informazioni, vedere [esecuzione prevede la memorizzazione nella cache e riutilizzo ](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse).
  
> [!NOTE] 
> A causa di una limitazione del numero di livelli nidificati consentiti il **xml** tipo di dati **DM exec_query_plan** non è possibile restituire i piani di query che soddisfino o superano 128 livelli di elementi annidati. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa condizione impediva il piano di query da restituire e genera [errore 6335](../../relational-databases/errors-events/database-engine-events-and-errors.md#errors-6000-to-6999). Nelle [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 e versioni successive, il **query_plan** colonna viene restituito NULL.  

## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione `VIEW SERVER STATE` per il server.  

## <a name="examples"></a>Esempi  
  
### <a name="a-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan"></a>A. Ricerca per l'ultima noto effettivo nel piano di esecuzione per un piano memorizzato nella cache specifico  
 Le seguenti query di esempio **DM exec_cached_plans** per trovare il piano e copia interessanti relativi `plan_handle` dall'output.  
  
```sql  
SELECT * FROM sys.dm_exec_cached_plans;  
GO  
```  
  
Quindi, per ottenere l'ultimo piano di esecuzione di query noto, usare l'insieme copiato `plan_handle` con funzione di sistema **sys.dm_exec_query_plan_stats**.  
  
```sql  
SELECT * FROM sys.dm_exec_query_plan_stats(< copied plan_handle >);  
GO  
```   

### <a name="b-looking-at-last-known-actual-query-execution-plan-for-all-cached-plans"></a>B. Ricerca per l'ultima noto effettivo nel piano di esecuzione per tutti i piani memorizzati nella cache
  
```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps;  
GO  
```   

### <a name="c-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan-and-query-text"></a>C. Ricerca per l'ultima noto effettivo nel piano di esecuzione per un piano memorizzato nella cache specifico e il testo della query

```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps
WHERE st.text LIKE 'SELECT * FROM Person.Person%';  
GO  
```   

### <a name="d-look-at-cached-events-for-trigger"></a>D. Esaminare eventi memorizzati nella cache per il trigger

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

## <a name="see-also"></a>Vedere anche
  [Flag di traccia](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative all'esecuzione &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  

