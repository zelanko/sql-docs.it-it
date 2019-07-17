---
title: DM xtp_system_memory_consumers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xtp_system_memory_consumers
- sys.dm_xtp_system_memory_consumers_TSQL
- sys.dm_xtp_system_memory_consumers
- dm_xtp_system_memory_consumers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_system_memory_consumers dynamic management view
ms.assetid: 9eb0dd82-7920-42e0-9e50-7ce6e7ecee8b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 83e9368b562a7ac200171dc814830b21d677770a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090092"
---
# <a name="sysdmxtpsystemmemoryconsumers-transact-sql"></a>sys.dm_xtp_system_memory_consumers (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Segnala i consumer di memoria a livello di sistema per [!INCLUDE[hek_2](../../includes/hek-2-md.md)]. La memoria per i consumer proviene dal pool predefinito (se l'allocazione è nel contesto di un thread utente) o nel pool interno (se l'allocazione è nel contesto di un thread di sistema).  
  
```  
-- system memory consumers @ instance  
select * from sys.dm_xtp_system_memory_consumers  
```  
  
 Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Nome colonna|type|Descrizione|  
|-----------------|----------|-----------------|  
|memory_consumer_id|**bigint**|ID interno del consumer di memoria.|  
|memory_consumer_type|**int**|Numero intero che rappresenta il tipo del consumer di memoria con uno dei valori seguenti:<br /><br /> 0 - non deve essere visualizzato. Aggrega l'utilizzo della memoria due o più consumer.<br /><br /> 1 - ELENCO LOOKASIDE DA: Tiene traccia dell'utilizzo di memoria per un lookaside del sistema.<br /><br /> 2 - VARHEAP: Tiene traccia dell'utilizzo di memoria per un heap a lunghezza variabile.<br /><br /> 4: riserva di paging IO: Tiene traccia dell'utilizzo di memoria per un pool di pagine di sistema utilizzato per le operazioni dei / o.|  
|memory_consumer_type_desc|**nvarchar(16)**|Descrizione del tipo del consumer di memoria:<br /><br /> 0 - non deve essere visualizzato.<br /><br /> 1 - LOOKASIDE<br /><br /> 2 - VARHEAP<br /><br /> 4 - PGPOOL|  
|memory_consumer_desc|**nvarchar(64)**|Descrizione dell'istanza del consumer di memoria:<br /><br /> VARHEAP: <br />Heap di sistema. Uso generale. Utilizzato solo per allocare gli elementi di lavoro di Garbage Collection.<br />oppure<br />Heap di lookaside. Utilizzato da looksides quando il numero di elementi contenuti nell'elenco raggiunge un limite predeterminato (in genere circa 5.000 elementi).<br /><br /> PGPOOL: Per il sistema dei / o i pool vi sono tre dimensioni diverse: Riserva di paging System 4K, System 64 KB riserva di paging e System 256K pagina del pool.|  
|lookaside_id|**bigint**|ID del provider di memoria dell'elenco lookaside e locale a livello di thread.|  
|pagepool_id|**bigint**|ID del provider di memoria del pool di pagine e locale a livello di thread.|  
|allocated_bytes|**bigint**|Numero di byte riservati al consumer.|  
|used_bytes|**bigint**|Byte utilizzati dal consumer. Si applica solo ai consumer di memoria varheap.|  
|allocation_count|**int**|Numero di allocazioni.|  
|partition_count|**int**|Solo per uso interno.|  
|sizeclass_count|**int**|Solo per uso interno.|  
|min_sizeclass|**int**|Solo per uso interno.|  
|max_sizeclass|**int**|Solo per uso interno.|  
|memory_consumer_address|**varbinary**|Indirizzo interno del consumer.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE nel server.  
  
## <a name="user-scenario"></a>Scenario utente  
  
```  
-- system memory consumers @ instance  
selectmemory_consumer_type_desc,   
allocated_bytes/1024 as allocated_bytes_kb,   
used_bytes/1024 as used_bytes_kb, allocation_count  
from sys.dm_xtp_system_memory_consumers  
```  
  
 Nell'output vengono mostrati tutti i consumer di memoria a livello di sistema. Ad esempio, vi sono consumer per transazioni LOOKASIDE.  
  
```  
memory_consumer_type_name           memory_consumer_desc                           allocated_bytes_kb   used_bytes_kb        allocation_count  
-------------------------------          ---------------------                          -------------------  --------------        ----------------  
VARHEAP                                  Lookaside heap                                 0                    0                    0  
VARHEAP                                  System heap                                    768                  0                    2  
LOOKASIDE                                GC transaction map entry                       64                   64                   910  
LOOKASIDE                                Redo transaction map entry                     128                  128                  1260  
LOOKASIDE                                Recovery table cache entry                     448                  448                  8192  
LOOKASIDE                                Transaction recent rows                        3264                 3264                 4444  
LOOKASIDE                                Range cursor                                   0                    0                    0  
LOOKASIDE                                Hash cursor                                    3200                 3200                 11070  
LOOKASIDE                                Transaction save-point set entry               0                    0                    0  
LOOKASIDE                                Transaction partially-inserted rows set        704                  704                  1287  
LOOKASIDE                                Transaction constraint set                     576                  576                  1940  
LOOKASIDE                                Transaction save-point set                     0                    0                    0  
LOOKASIDE                                Transaction write set                          704                  704                  672  
LOOKASIDE                                Transaction scan set                           320                  320                  156  
LOOKASIDE                                Transaction read set                           704                  704                  343  
LOOKASIDE                                Transaction                                    4288                 4288                 1459  
PGPOOL                                   System 256K page pool                          5120                 5120                 20  
PGPOOL                                   System 64K page pool                           0                    0                    0  
PGPOOL                                   System 4K page pool                            24                   24                   6  
```  
  
 Per visualizzare la memoria totale utilizzata dagli allocatori di sistema:  
  
```  
select sum(allocated_bytes)/(1024*1024) as total_allocated_MB, sum(used_bytes)/(1024*1024) as total_used_MB   
from sys.dm_xtp_system_memory_consumers  
  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
2                    2  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Memoria-con ottimizzazione per la tabella viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
