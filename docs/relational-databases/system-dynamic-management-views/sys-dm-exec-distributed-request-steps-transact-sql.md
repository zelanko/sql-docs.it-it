---
title: DM exec_distributed_request_steps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_distributed_request_steps
- sys.dm_exec_distributed_request_steps management view
ms.assetid: 1954541d-b716-4e03-8fcc-7022f428e01d
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 27df857e8863272f2b502c4950b4cc36ad936978
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52401956"
---
# <a name="sysdmexecdistributedrequeststeps-transact-sql"></a>sys.dm_exec_distributed_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene informazioni su tutti i passaggi che compongono una determinata richiesta PolyBase o query. Elenca una riga per ogni passaggio della query.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|valore di execution_id e step_index costituiscono la chiave per questa visualizzazione. Id numerico univoco associato alla richiesta.|Vedere ID nel [exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|La posizione di questo passaggio della sequenza di passaggi che compongono la richiesta.|0 per (n-1) per una richiesta con passaggi n.|  
|operation_type|**nvarchar(128)**|Tipo dell'operazione rappresentata da questo passaggio.|'MoveOperation', 'OnOperation', 'RandomIDOperation', 'RemoteOperation', 'ReturnOperation', 'ShuffleMoveOperation', 'TempTablePropertiesOperation', 'DropDiagnosticsNotifyOperation', 'HadoopShuffleOperation', 'HadoopBroadCastOperation', 'HadoopRoundRobinOperation'|  
|distribution_type|**nvarchar(32)**|In cui è in esecuzione il passaggio.|'AllComputeNodes ',' 'AllDistributions, 'ComputeNode', 'Distribution', 'AllNodes', "SubsetNodes", 'SubsetDistributions',' non è specificato'.|  
|location_type|**nvarchar(32)**|In cui è in esecuzione il passaggio.|'Compute', 'Head' o 'DMS'. Tutti i passaggi di spostamento dei dati mostrano 'DMS'.|  
|status|**nvarchar(32)**|Stato di questo passaggio|'Sospeso', 'Running', 'Complete', 'Non riuscito', 'UndoFailed', 'PendingCancel', 'annullato', 'Annullate', 'Interrotta'|  
|error_id|**nvarchar(36)**|Id univoco dell'errore associato con questo passaggio, se presente|Vedere id del [sys.dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)il valore è null, se si è verificato alcun errore.|  
|start_time|**datetime**|Tempo in cui è iniziato il passaggio di esecuzione|Minore o uguale all'ora corrente e maggiore o uguale a end_compile_time della query a cui appartiene questo passaggio.|  
|end_time|**datetime**|Ora in cui questo passaggio completato l'esecuzione, è stato annullato o non è riuscito.|Minore o uguale all'ora corrente e maggiore o uguale a start_time, impostato su NULL per la procedura attualmente in esecuzione o in coda.|  
|total_elapsed_time|**int**|Quantità totale di tempo in esecuzione il passaggio della query, in millisecondi|Compreso tra 0 e la differenza tra start_time ed end_time. 0 per i passaggi in coda.|  
|row_count|**bigint**|Numero totale di righe modificate o restituito da questa richiesta|0 per i passaggi che non sono stati modificare o restituiscono dati, numero di righe interessate in caso contrario. Impostare su -1 per i passaggi di migrazione del database.|  
|comando|nvarchar(4000)|Contiene il testo completo del comando di questo passaggio.|Qualsiasi stringa di richiesta valido per un passaggio. Troncata se supera i 4000 caratteri.|  
  
## <a name="see-also"></a>Vedere anche  
 [PolyBase con DMV di risoluzione dei problemi](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative ai database &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
