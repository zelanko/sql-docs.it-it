---
title: sys.dm_exec_distributed_sql_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_distributed_requests management view
- dm_exec_distributed_requests management view
ms.assetid: d065dc01-35d4-472f-9554-53ac41e7d104
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a63d8a331163283598dd50a418f0dd32f9ac5edd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097794"
---
# <a name="sysdmexecdistributedsqlrequests-transact-sql"></a>sys.dm_exec_distributed_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene informazioni su tutte le distribuzioni di query SQL come parte di un passaggio SQL nella query.  In questa vista mostra i dati per le ultime 1000 richieste; richieste attive dispongano sempre dei dati presenti in questa vista.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|valore di execution_id e step_index costituiscono la chiave per questa visualizzazione. Id numerico univoco associato alla richiesta.|Vedere ID nel [exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|Indice del passaggio della query di di che questo tipo di distribuzione fa parte.|Vedere in step_index [DM exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|compute_node_id|**int**|Tipo dell'operazione rappresentata da questo passaggio.|Vedere in compute_node_id [DM exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|**int**|In cui è in esecuzione il passaggio.|Impostare su -1 per le richieste eseguite nell'ambito del nodo non nell'ambito della distribuzione.|  
|status|**nvarchar(32)**|Stato di questo passaggio|Active, annullati, completato, non riusciti, in coda|  
|error_id|**nvarchar(36)**|Id univoco dell'errore associato con questo passaggio, se presente|Vedere id del [sys.dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)il valore è null, se si è verificato alcun errore.|  
|start_time|**datetime**|Tempo in cui è iniziato il passaggio di esecuzione|Minore o uguale all'ora corrente e maggiore o uguale a end_compile_time della query a cui appartiene questo passaggio.|  
|end_time|**datetime**|Ora in cui questo passaggio completato l'esecuzione, è stato annullato o non è riuscito.|Minore o uguale all'ora corrente e maggiore o uguale a start_time, impostato su NULL per la procedura attualmente in esecuzione o in coda.|  
|total_elapsed_time|**int**|Quantità totale di tempo in esecuzione il passaggio della query, in millisecondi|Compreso tra 0 e la differenza tra start_time ed end_time. 0 per i passaggi in coda.|  
|row_count|**bigint**|Numero totale di righe modificate o restituito da questa richiesta|0 per i passaggi che non sono stati modificare o restituiscono dati, numero di righe interessate in caso contrario. Impostare su -1 per i passaggi di migrazione del database.|  
|spid|**int**|Id di sessione nell'istanza di SQL Server esegue la distribuzione delle query||  
|command|nvarchar(4000)|Contiene il testo completo del comando di questo passaggio.|Qualsiasi stringa di richiesta valido per un passaggio. Troncata se supera i 4000 caratteri.|  
  
## <a name="see-also"></a>Vedere anche  
 [PolyBase con DMV di risoluzione dei problemi](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative ai database &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
