---
title: sys.dm_exec_query_statistics_xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_statistics_xml
- sys.dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml
helpviewer_keywords:
- sys.dm_exec_query_statistics_xml management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfecb
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 06091ffc26ea036a4a0bd7e30196545bcaca60d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936942"
---
# <a name="sysdmexecquerystatisticsxml-transact-sql"></a>sys.dm_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Restituisce il piano di esecuzione per le richieste in elaborazione delle query. Utilizzare questa DMV per recuperare i file XML dello showplan con le statistiche temporanee. 

## <a name="syntax"></a>Sintassi

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>Argomenti 
*session_id*  
 L'id di sessione è in esecuzione batch per essere cercato. *session_id* viene **smallint**. *session_id* può essere ottenuto dagli oggetti a gestione dinamica seguenti:  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>Tabella restituita

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|ID della sessione. Non ammette i valori NULL.|
|request_id|**int**|ID della richiesta. Non ammette i valori NULL.|
|sql_handle|**varbinary(64)**|È un token che identifica in modo univoco il batch o una stored procedure che fa parte della query. Ammette valori Null.|
|plan_handle|**varbinary(64)**|È un token che identifica in modo univoco un piano di esecuzione di query per un batch attualmente in esecuzione. Ammette valori Null.|
|query_plan|**xml**|Contiene la rappresentazione Showplan del piano di esecuzione di query specificata con il runtime *plan_handle* contenente statistiche parziale. La rappresentazione Showplan è in formato XML. Viene generato un piano per ogni batch contenente ad esempio istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, chiamate di stored procedure e chiamate di funzioni definite dall'utente. Ammette valori Null.|

## <a name="remarks"></a>Note
Questa funzione di sistema è disponibile a partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1. Vedere KB [3190871](https://support.microsoft.com/en-us/help/3190871)

Questa funzione di sistema funziona in entrambe **standard** e **leggero** infrastruttura di analisi delle statistiche di esecuzione di query. Per altre informazioni, vedere [Infrastruttura di profilatura query](../../relational-databases/performance/query-profiling-infrastructure.md).  

Nelle condizioni seguenti, non viene restituito alcun output Showplan nella **query_plan** della colonna della tabella restituita per **DM exec_query_statistics_xml**:  
  
-   Se il piano della query corrisponde all'oggetto specificato *session_id* non è in esecuzione, il **query_plan** colonna della tabella restituita è null. Ad esempio, questa condizione può verificarsi se non si verifica un ritardo tra quando viene acquisito l'handle del piano e quando è stato usato con **DM exec_query_statistics_xml**.  
    
A causa di una limitazione del numero di livelli nidificati consentiti il **xml** tipo di dati **DM exec_query_statistics_xml** non è possibile restituire i piani di query che soddisfino o superano 128 livelli di elementi annidati. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa condizione impediva il completamento del piano di query e generava l'errore 6335. Nelle [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 e versioni successive, il **query_plan** colonna viene restituito NULL.   

## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione `VIEW SERVER STATE` per il server.  

## <a name="examples"></a>Esempi  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>R. Esaminare le statistiche di piano e di esecuzione dinamico delle query per un batch in esecuzione  
 Le seguenti query di esempio **exec_requests** per trovare la query specifica e copiare il `session_id` dall'output.  
  
```sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 Quindi, per ottenere le statistiche di piano e l'esecuzione di query in tempo reale, usare l'insieme copiato `session_id` con funzione di sistema **DM exec_query_statistics_xml**.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_query_statistics_xml(< copied session_id >);  
GO  
```   

 O combinato per tutte le richieste in esecuzione.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_query_statistics_xml(session_id);  
GO  
```   
  
## <a name="see-also"></a>Vedere anche
  [Flag di traccia](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative ai database &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

