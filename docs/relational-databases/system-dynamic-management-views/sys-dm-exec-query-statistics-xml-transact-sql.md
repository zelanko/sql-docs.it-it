---
title: sys. dm_exec_query_statistics_xml (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: e2bd7a4ce174d547d0cb8d0f9bcb89d23e6543db
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78180091"
---
# <a name="sysdm_exec_query_statistics_xml-transact-sql"></a>sys. dm_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Restituisce il piano di esecuzione della query per le richieste in corso. Utilizzare questa DMV per recuperare Showplan XML con statistiche temporanee. 

## <a name="syntax"></a>Sintassi

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>Argomenti 
*session_id*  
 ID della sessione in cui è in esecuzione il batch da cercare. *session_id* è **smallint**. è possibile ottenere *session_id* dagli oggetti a gestione dinamica seguenti:  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>Tabella restituita

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|ID della sessione. Non ammette i valori NULL.|
|request_id|**int**|ID della richiesta. Non ammette i valori NULL.|
|sql_handle|**varbinary (64)**|Token che identifica in modo univoco il batch o stored procedure di cui fa parte la query. Ammette valori Null.|
|plan_handle|**varbinary (64)**|Token che identifica in modo univoco un piano di esecuzione della query per un batch attualmente in esecuzione. Ammette valori Null.|
|query_plan|**xml**|Contiene la rappresentazione Showplan di runtime del piano di esecuzione della query specificato con *plan_handle* contenenti statistiche parziali. La rappresentazione Showplan è in formato XML. Viene generato un piano per ogni batch contenente ad esempio istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, chiamate di stored procedure e chiamate di funzioni definite dall'utente. Ammette valori Null.|

## <a name="remarks"></a>Osservazioni
Questa funzione di sistema è disponibile a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] partire da SP1. Vedere KB [3190871](https://support.microsoft.com/help/3190871)

Questa funzione di sistema funziona con l'infrastruttura di profilatura delle statistiche di esecuzione di query **standard** e **Lightweight** . Per altre informazioni, vedere [query profiling Infrastructure](../../relational-databases/performance/query-profiling-infrastructure.md).  

Nelle condizioni seguenti non viene restituito alcun output Showplan nella colonna **query_plan** della tabella restituita per **sys. dm_exec_query_statistics_xml**:  
  
-   Se il piano di query che corrisponde al *session_id* specificato non è più in esecuzione, la colonna **query_plan** della tabella restituita è null. Questa condizione, ad esempio, può verificarsi se si verifica un ritardo tra il momento in cui l'handle del piano è stato acquisito e il momento in cui è stato utilizzato con **sys. dm_exec_query_statistics_xml**.  
    
A causa di una limitazione del numero di livelli annidati consentiti nel tipo di dati **XML** , **sys. dm_exec_query_statistics_xml** non può restituire piani di query che soddisfano o superano 128 livelli di elementi annidati. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa condizione impediva il completamento del piano di query e generava l'errore 6335. In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 e versioni successive, la colonna **query_plan** restituisce null.   

## <a name="permissions"></a>Autorizzazioni  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]è richiesta `VIEW SERVER STATE` l'autorizzazione per il server.  
Nei [!INCLUDE[ssSDS](../../includes/sssds-md.md)] livelli Premium, richiede l' `VIEW DATABASE STATE` autorizzazione nel database. Nei [!INCLUDE[ssSDS](../../includes/sssds-md.md)] livelli standard e Basic, richiede l' **amministratore del server** o un account **amministratore Azure Active Directory** .

## <a name="examples"></a>Esempi  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>R. Analisi delle statistiche di esecuzione e del piano di query in tempo reale per un batch in esecuzione  
 Nell'esempio seguente viene eseguita una query su **sys. dm_exec_requests** per trovare la query `session_id` interessante e copiarne l'oggetto dall'output.  
  
```sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 Per ottenere il piano di query e le statistiche di esecuzione in tempo reale, `session_id` usare la copia con la funzione di sistema **sys. dm_exec_query_statistics_xml**.  
  
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
 [Viste a gestione dinamica relative ai database &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

