---
title: sys. dm _pdw_request_steps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 260b822d111f94fc567704cd908cb5632e3bdcaf
ms.sourcegitcommit: 27c267bf2a3cfaf2abcb5f3777534803bf4cffe5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/31/2019
ms.locfileid: "73240780"
---
# <a name="sysdm_pdw_request_steps-transact-sql"></a>sys. dm _pdw_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Include informazioni su tutti i passaggi che compongono una richiesta o una query specifica in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Elenca una riga per ogni passaggio della query.  
  
|Column Name|tipo di dati|Description|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|request_id e step_index costituiscono la chiave per questa visualizzazione.<br /><br /> ID numerico univoco associato alla richiesta.|Vedere request_id in [sys. dm _pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**Int**|request_id e step_index costituiscono la chiave per questa visualizzazione.<br /><br /> Posizione di questo passaggio nella sequenza di passaggi che costituiscono la richiesta.|da 0 a (n-1) per una richiesta con n passaggi.|  
|operation_type|**nvarchar(35)**|Tipo di operazione rappresentata da questo passaggio.|**Operazioni del piano di query DMS:** ' ReturnOperation ',' PartitionMoveOperation ',' MoveOperation ',' BroadcastMoveOperation ',' ShuffleMoveOperation ',' TrimMoveOperation ',' CopyOperation ',' DistributeReplicatedTableMoveOperation '<br /><br /> **Operazioni del piano di query SQL:** ' OnOperation ',' RemoteOperation '<br /><br /> **Altre operazioni del piano di query:** 'MetaDataCreateOperation', 'RandomIDOperation'<br /><br /> **Operazioni esterne per le letture:** 'HadoopShuffleOperation', 'HadoopRoundRobinOperation', 'HadoopBroadcastOperation'<br /><br /> **Operazioni esterne per MapReduce:** 'HadoopJobOperation', 'HdfsDeleteOperation'<br /><br /> **Operazioni esterne per le Scritture:** 'ExternalExportDistributedOperation', 'ExternalExportReplicatedOperation', 'ExternalExportControlOperation'<br /><br /> Per ulteriori informazioni, vedere "informazioni sui piani di query" nella [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]. <br /><br />  Un piano di query può inoltre essere influenzato dalle impostazioni del database.  Per informazioni dettagliate, vedere [Opzioni ALTER database set](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-set-options?toc=/azure/sql-data-warehouse/toc.json&bc=/azure/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest) .|  
|distribution_type|**nvarchar(32)**|Tipo di distribuzione che verrà sottoposta a questo passaggio.|' AllNodes ',' AllDistributions ',' AllComputeNodes ',' ComputeNode ',' Distribution ',' SubsetNodes ',' SubsetDistributions ',' Unspecified '|  
|location_type|**nvarchar(32)**|Posizione in cui è in esecuzione il passaggio.|' Compute ',' Control ',' DMS '|  
|status|**nvarchar(32)**|Stato di questo passaggio.|In sospeso, in esecuzione, completo, non riuscito, UndoFailed, PendingCancel, annullato, annullato, interrotto|  
|error_id|**nvarchar (36)**|ID univoco dell'errore associato a questo passaggio, se disponibile.|Vedere error_id di [sys. dm _pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). NULL se non si è verificato alcun errore.|  
|start_time|**datetime**|Ora di inizio dell'esecuzione del passaggio.|Minore o uguale all'ora corrente e maggiore o uguale a end_compile_time della query a cui appartiene questo passaggio. Per ulteriori informazioni sulle query, vedere [sys. dm _pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|end_time|**datetime**|Ora di completamento dell'esecuzione di questo passaggio, annullato o non riuscito.|Minore o uguale all'ora corrente e maggiore o uguale a start_time. Impostare su NULL per i passaggi attualmente in esecuzione o in coda.|  
|total_elapsed_time|**Int**|Quantità totale di tempo di esecuzione del passaggio della query, in millisecondi.|Compreso tra 0 e la differenza tra end_time e start_time. 0 per i passaggi in coda.<br /><br /> Se total_elapsed_time supera il valore massimo per un numero intero, total_elapsed_time continuerà a essere il valore massimo. Questa condizione genererà l'avviso "è stato superato il valore massimo".<br /><br /> Il valore massimo in millisecondi equivale a 24,8 giorni.|  
|row_count|**bigint**|Numero totale di righe modificate o restituite dalla richiesta.|0 per i passaggi che non sono stati modificati o restituiscono dati. In caso contrario, numero di righe interessate.|  
|comando|**nvarchar(4000)**|Include il testo completo del comando di questo passaggio.|Qualsiasi stringa di richiesta valida per un passaggio. NULL se l'operazione è di tipo MetaDataCreateOperation. Troncato se è più lungo di 4000 caratteri.|  
  
 Per informazioni sul numero massimo di righe mantenute da questa visualizzazione, vedere la sezione relativa ai valori massimi per la vista di sistema in "valori minimi e massimi" nel [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Transact-SQL SQL Data Warehouse e Parallel data warehouse &#40;viste a gestione dinamica&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
