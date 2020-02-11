---
title: sys. dm_exec_query_parallel_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_parallel_workers_TSQL
- dm_exec_query_parallel_workers
- sys.dm_exec_query_parallel_workers_TSQL
- sys.dm_exec_query_parallel_workers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_parallel_workers dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9f
author: pelopes
ms.author: pelopes
manager: ajayj
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 000dd995427f8eafec759688db1ab76a6546b789
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68263265"
---
# <a name="sysdm_exec_query_parallel_workers-transact-sql"></a>sys.dm_exec_query_parallel_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Restituisce informazioni sulla disponibilità del ruolo di lavoro per nodo.  
  
|Nome|Tipo di dati|Descrizione|  
|----------|---------------|-----------------|  
|**node_id**|**int**|ID del nodo NUMA.|  
|**scheduler_count**|**int**|Numero di utilità di pianificazione in questo nodo.|  
|**max_worker_count**|**int**|Numero massimo di ruoli di lavoro per le query parallele.|  
|**reserved_worker_count**|**int**|Numero di ruoli di lavoro riservati da query parallele, più il numero di ruoli di lavoro principali utilizzati da tutte le richieste.| 
|**free_worker_count**|**int**|Numero di thread di lavoro disponibili per le attività.<br /><br />**Nota:** ogni richiesta in ingresso utilizza almeno un ruolo di lavoro, che viene sottratto dal numero di thread di lavoro liberi.  È possibile che il numero di thread di lavoro libero possa essere un numero negativo in un server con carico elevato.| 
|**used_worker_count**|**int**|Numero di thread di lavoro utilizzati da query parallele.|  
  
## <a name="permissions"></a>Autorizzazioni  

In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]è richiesta `VIEW SERVER STATE` l'autorizzazione.   
Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, richiede l' `VIEW DATABASE STATE` autorizzazione nel database. Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli standard e Basic, richiede l' **amministratore del server** o un account **amministratore Azure Active Directory** .   
 
## <a name="examples"></a>Esempi  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>R. Visualizzazione della disponibilità corrente del ruolo di lavoro parallelo  

```sql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funzioni e viste a gestione dinamica relative all'esecuzione &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys. dm_os_workers &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
