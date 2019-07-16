---
title: sys.dm_db_column_store_row_group_operational_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 03e97e38eb396aa24c9779d07f269a60f117ab09
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005048"
---
# <a name="sysdmdbcolumnstorerowgroupoperationalstats-transact-sql"></a>sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  I/o, blocco, a livello di riga corrente restituisce e metodo di accesso per i rowgroup compressi in un indice columnstore. Uso **sys.dm_db_column_store_row_group_operational_stats** per tenere traccia della quantità di tempo una query dell'utente deve attendere prima di leggere o scrivere in un rowgroup compresso o una partizione di un indice columnstore e identificare i rowgroup che riscontrano attività dei / o significativa o aree critiche.  
  
 Gli indici columnstore in memoria non vengono visualizzati in questa DMV.  
 
 
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID della tabella contenente l'indice columnstore.|  
|**index_id**|**int**|ID dell'indice columnstore.|  
|**partition_number**|**int**|Numero di partizione in base 1 all'interno dell'indice o heap.|  
|**row_group_id**|**int**|ID del gruppo di righe nell'indice columnstore. Questo è univoco all'interno di una partizione.|  
|**scan_count**|**int**|Numero di analisi tramite il gruppo di righe dall'ultimo riavvio SQL.|  
|**delete_buffer_scan_count**|**int**|Numero di volte in cui che il buffer di eliminazione è stato utilizzato per determinare le righe eliminate in questo rowgroup. Ciò include l'accesso alla tabella hash in memoria e l'albero b sottostante.|  
|**index_scan_count**|**int**|Numero di volte in cui che la partizione dell'indice columnstore è stata analizzata. Questo è lo stesso per tutti i rowgroup nella partizione.|  
|**rowgroup_lock_count**|**bigint**|Conteggio cumulativo delle richieste di blocco per questo gruppo di righe dall'ultimo riavvio SQL.|  
|**rowgroup_lock_wait_count**|**bigint**|Numero cumulativo di volte in cui il motore di database ha atteso il rowgroup blocco dopo l'ultimo riavvio SQL.|  
|**rowgroup_lock_wait_in_ms**|**bigint**|Numero cumulativo di millisecondi il motore di database ha atteso il rowgroup blocco dopo l'ultimo riavvio SQL.|  
  
## <a name="permissions"></a>Permissions  
 Sono richieste le autorizzazioni seguenti:  
  
-   Autorizzazione CONTROL per la tabella specificata da object_id.  
  
-   L'autorizzazione VIEW DATABASE STATE per restituire informazioni su tutti gli oggetti all'interno del database, utilizzando il carattere jolly di oggetto @*object_id* = NULL  
  
 La concessione di VIEW DATABASE STATE consente la restituzione di tutti gli oggetti nel database, indipendentemente dalle eventuali autorizzazioni CONTROL negate per oggetti specifici.  
  
 La negazione di VIEW DATABASE STATE non consente la restituzione di tutti gli oggetti nel database, indipendentemente dalle eventuali autorizzazioni CONTROL concesse per oggetti specifici. Inoltre, quando il carattere jolly di database @*database_id*= NULL è specificato, il database viene omesso.  
  
 Per altre informazioni, vedere [funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funzioni a gestione dinamica e DMV correlate all'indice &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Monitoraggio e ottimizzazione delle prestazioni](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

