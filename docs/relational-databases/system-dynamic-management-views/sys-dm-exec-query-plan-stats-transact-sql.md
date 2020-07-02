---
title: sys. dm_exec_query_plan_stats (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 3bd7aa786466f3bde9aa42d75437d2406ef1e808
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734748"
---
# <a name="sysdm_exec_query_plan_stats-transact-sql"></a>sys. dm_exec_query_plan_stats (Transact-SQL)
[!INCLUDE[SQL Server 2019](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

Restituisce l'equivalente dell'ultimo piano di esecuzione effettivo noto per un piano di query precedentemente memorizzato nella cache.

## <a name="syntax"></a>Sintassi

```
sys.dm_exec_query_plan_stats(plan_handle)  
``` 

## <a name="arguments"></a>Argomenti 
*plan_handle*  
È un token che identifica in modo univoco un piano di esecuzione di query per un batch eseguito e il relativo piano risiede nella cache dei piani oppure è attualmente in esecuzione. *plan_handle* è di tipo **varbinary (64)**.   

Il *plan_handle* può essere ottenuto dagli oggetti a gestione dinamica seguenti:  
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys. dm_exec_procedure_stats &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys. dm_exec_trigger_stats &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  

## <a name="table-returned"></a>Tabella restituita

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|
|**dbid**|**smallint**|ID del database di contesto attivo al momento della compilazione dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] corrispondente a questo piano. Per istruzioni SQL ad hoc e preparate, l'ID del database in cui sono state compilate le istruzioni.<br /><br /> La colonna ammette i valori Null.|  
|**ObjectId**|**int**|ID dell'oggetto (ad esempio, stored procedure o funzione definita dall'utente) per il piano della query. Per i batch ad hoc e preparati, questa colonna è **null**.<br /><br /> La colonna ammette i valori Null.|  
|**number**|**smallint**|Valore intero della stored procedure numerata. Ad esempio, le procedure utilizzate per l'applicazione **orders** potrebbero essere denominate **orderproc;1**, **orderproc;2** e così via. Per i batch ad hoc e preparati, questa colonna è **null**.<br /><br /> La colonna ammette i valori Null.|  
|**crittografati**|**bit**|Indica se la stored procedure corrispondente è crittografata.<br /><br /> 0 = non crittografata<br /><br /> 1 = crittografata<br /><br /> La colonna non ammette i valori Null.|  
|**query_plan**|**xml**|Contiene l'ultima rappresentazione Showplan Runtime nota del piano di esecuzione della query effettivo specificato con *plan_handle*. La rappresentazione Showplan è in formato XML. Viene generato un piano per ogni batch contenente ad esempio istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, chiamate di stored procedure e chiamate di funzioni definite dall'utente.<br /><br /> La colonna ammette i valori Null.| 

## <a name="remarks"></a>Osservazioni
Questa funzione di sistema è disponibile a partire dalla [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] versione CTP 2,4.

Questa funzione prevede il consenso esplicito e richiede l'abilitazione del [flag di traccia](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451. a partire da [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.5, per eseguire questa operazione a livello di database, vedere l'opzione LAST_QUERY_PLAN_STATS in [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

Questa funzione di sistema funziona con l'infrastruttura di profilatura delle statistiche di esecuzione delle query **Lightweight** . Per altre informazioni, vedere [query profiling Infrastructure](../../relational-databases/performance/query-profiling-infrastructure.md).  

Showplan output by sys. dm_exec_query_plan_stats contiene le informazioni seguenti:
-  Tutte le informazioni in fase di compilazione trovate nel piano memorizzato nella cache
-  Informazioni di runtime, ad esempio il numero effettivo di righe per operatore, il tempo di esecuzione totale della CPU e il tempo di esecuzione, gli avvisi di fuoriuscita, la DOP effettiva, la memoria massima utilizzata e la memoria concessa

Nelle condizioni seguenti viene restituito un output di Showplan **equivalente a un piano di esecuzione effettivo** nella colonna **query_plan** della tabella restituita per **sys. dm_exec_query_plan_stats**:  

-   Il piano si trova in [sys. dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md).     
    **E**    
-   La query eseguita è complessa o richiede risorse.

Nelle condizioni seguenti viene restituito un output di Showplan ** <sup>1</sup> semplificato** nella colonna **query_plan** della tabella restituita per **sys. dm_exec_query_plan_stats**:  

-   Il piano si trova in [sys. dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md).     
    **E**    
-   La query è abbastanza semplice, in genere categorizzata come parte di un carico di lavoro OLTP.

<sup>1</sup> a partire dalla [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] versione CTP 2,5, si riferisce a uno Showplan che contiene solo l'operatore nodo radice (Select). Per [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] la versione CTP 2,4 si riferisce al piano memorizzato nella cache come disponibile tramite `sys.dm_exec_cached_plans` .

Nelle condizioni seguenti **non viene restituito alcun output** da **sys. dm_exec_query_plan_stats**:

-   Il piano di query specificato utilizzando *plan_handle* è stato eliminato dalla cache dei piani.     
    **OR**    
-   Il piano di query non è stato inserito nella cache. Per ulteriori informazioni, vedere [memorizzazione nella cache e riutilizzo del piano di esecuzione ](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse).
  
> [!NOTE] 
> A causa di una limitazione del numero di livelli annidati consentiti nel tipo di dati **XML** , **sys. dm_exec_query_plan** non può restituire piani di query che soddisfano o superano 128 livelli di elementi annidati. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa condizione impediva la restituzione del piano di query e generava l' [errore 6335](../../relational-databases/errors-events/database-engine-events-and-errors.md#errors-6000-to-6999). In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 e versioni successive, la colonna **QUERY_PLAN** restituisce null.  

## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione `VIEW SERVER STATE` per il server.  

## <a name="examples"></a>Esempi  
  
### <a name="a-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan"></a>R. Esame dell'ultimo piano di esecuzione effettivo della query noto per un piano specifico memorizzato nella cache  
 Nell'esempio seguente viene eseguita una query su **sys. dm_exec_cached_plans** per trovare il piano interessante e copiarne l'oggetto `plan_handle` dall'output.  
  
```sql  
SELECT * FROM sys.dm_exec_cached_plans;  
GO  
```  
  
Quindi, per ottenere l'ultimo piano di esecuzione effettivo della query, usare l'oggetto copiato `plan_handle` con la funzione di sistema **sys. dm_exec_query_plan_stats**.  
  
```sql  
SELECT * FROM sys.dm_exec_query_plan_stats(< copied plan_handle >);  
GO  
```   

### <a name="b-looking-at-last-known-actual-query-execution-plan-for-all-cached-plans"></a>B. Esame dell'ultimo piano di esecuzione effettivo della query noto per tutti i piani memorizzati nella cache
  
```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps;  
GO  
```   

### <a name="c-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan-and-query-text"></a>C. Esame dell'ultimo piano di esecuzione effettivo della query noto per un piano e un testo della query specifici memorizzati nella cache

```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps
WHERE st.text LIKE 'SELECT * FROM Person.Person%';  
GO  
```   

### <a name="d-look-at-cached-events-for-trigger"></a>D. Esaminare gli eventi memorizzati nella cache per il trigger

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

## <a name="see-also"></a>Vedere anche
  [Flag di traccia](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Viste a gestione dinamica e funzioni &#40;&#41;Transact-SQL](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative all'esecuzione &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  

