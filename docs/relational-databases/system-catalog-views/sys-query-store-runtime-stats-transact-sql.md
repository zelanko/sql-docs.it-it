---
title: Sys. query_store_runtime_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_RUNTIME_STATS_TSQL
- QUERY_STORE_RUNTIME_STATS_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS
- QUERY_STORE_RUNTIME_STATS
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_runtime_stats catalog view
- sys.query_store_runtime_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3ba19045d0184e498b559da0b97b3cd4d95d30c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067943"
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>Sys. query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contiene informazioni sulle informazioni statistiche esecuzione runtime per la query.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|Identificatore della riga che rappresenta le statistiche di esecuzione runtime per il **plan_id**, **execution_type** e **runtime_stats_interval_id**. È univoco solo per gli ultimi intervalli di statistiche di runtime. Per l'intervallo attualmente attivo possono esistere più righe che rappresenta le statistiche di runtime per il piano fa **plan_id**, con il tipo di esecuzione rappresentato dal **execution_type**. In genere, una riga rappresenta le statistiche di runtime che vengono scaricate su disco, mentre altri (s) rappresentano lo stato in memoria. Per ottenere lo stato effettivo per ogni intervallo è pertanto necessario aggregare le metriche, raggruppare **plan_id**, **execution_type** e **runtime_stats_interval_id**.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**plan_id**|**bigint**|Chiave esterna. Crea un join al [Sys. query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**bigint**|Chiave esterna. Crea un join al [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**execution_type**|**tinyint**|Determina il tipo di esecuzione di query:<br /><br /> 0 - esecuzione normale (correttamente completata)<br /><br /> 3 - client ha avviato ha interrotto l'esecuzione<br /><br /> 4 - eccezione ha interrotto l'esecuzione|  
|**execution_type_desc**|**nvarchar(128)**|Descrizione testuale del campo di tipo di esecuzione:<br /><br /> 0 - normale<br /><br /> 3 - interrotta<br /><br /> 4 - eccezione|  
|**first_execution_time**|**datetimeoffset**|Ora della prima esecuzione del piano di query entro l'intervallo di aggregazione. Si riferisce all'ora di fine dell'esecuzione della query.|  
|**last_execution_time**|**datetimeoffset**|Ora dell'ultima esecuzione della query prevede entro l'intervallo di aggregazione. Si riferisce all'ora di fine dell'esecuzione della query.|  
|**count_executions**|**bigint**|Numero totale di esecuzioni del piano di query entro l'intervallo di aggregazione.|  
|**avg_duration**|**float**|La durata per il piano di query entro l'intervallo di aggregazione (espresso in microsecondi).|  
|**last_duration**|**bigint**|Durata ultima per la query prevede entro l'intervallo di aggregazione (espresso in microsecondi).|  
|**min_duration**|**bigint**|Durata minima per il piano di query entro l'intervallo di aggregazione (espresso in microsecondi).|  
|**max_duration**|**bigint**|Durata massima per il piano di query entro l'intervallo di aggregazione (espresso in microsecondi).|  
|**stdev_duration**|**float**|Deviazione standard della durata per il piano di query entro l'intervallo di aggregazione (espresso in microsecondi).|  
|**avg_cpu_time**|**float**|Tempo medio di CPU per il piano di query entro l'intervallo di aggregazione (espresso in microsecondi).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_cpu_time**|**bigint**|Ultimo tempo di CPU per la query prevede entro l'intervallo di aggregazione (espresso in microsecondi).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**min_cpu_time**|**bigint**|Tempo minimo di CPU per il piano di query entro l'intervallo di aggregazione (espresso in microsecondi).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**max_cpu_time**|**bigint**|Tempo di CPU massimo per il piano di query entro l'intervallo di aggregazione (espresso in microsecondi).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**stdev_cpu_time**|**float**|Deviazione standard di tempo della CPU per il piano di query entro l'intervallo di aggregazione (espresso in microsecondi).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**avg_logical_io_reads**|**float**|Numero medio dei / o logiche legge per il piano di query entro l'intervallo di aggregazione. (espresso come un numero di pagine da 8KB lettura).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_logical_io_reads**|**bigint**|Ultimo numero dei / o logiche legge per il piano di query entro l'intervallo di aggregazione. (espresso come un numero di pagine da 8KB lettura).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**min_logical_io_reads**|**bigint**|Numero minimo dei / o logiche legge per il piano di query entro l'intervallo di aggregazione. (espresso come un numero di pagine da 8KB lettura).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**max_logical_io_reads**|**bigint**|Numero massimo dei / o logiche legge per il piano di query entro l'intervallo di aggregazione. (espresso come un numero di pagine da 8KB lettura).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**stdev_logical_io_reads**|**float**|Numero dei / o logiche legge la deviazione standard per il piano di query entro l'intervallo di aggregazione. (espresso come un numero di pagine da 8KB lettura).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**avg_logical_io_writes**|**float**|Numero medio dei / o logiche scrive per il piano di query entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_logical_io_writes**|**bigint**|Ultimo numero dei / o logiche scrive per il piano di query entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**min_logical_io_writes**|**bigint**|Numero minimo dei / o logiche scrive per il piano di query entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**max_logical_io_writes**|**bigint**|Numero massimo dei / o logiche scrive per il piano di query entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**stdev_logical_io_writes**|**float**|Numero dei / o logiche scrive la deviazione standard per il piano di query entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**avg_physical_io_reads**|**float**|Numero medio dei / o fisiche legge per il piano di query entro l'intervallo di aggregazione (espresso come un numero di pagine da 8KB lettura).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_physical_io_reads**|**bigint**|Ultimo numero dei / o fisiche legge per il piano di query entro l'intervallo di aggregazione (espresso come un numero di pagine da 8KB lettura).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**min_physical_io_reads**|**bigint**|Numero minimo dei / o fisiche legge per il piano di query entro l'intervallo di aggregazione (espresso come un numero di pagine da 8KB lettura).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**max_physical_io_reads**|**bigint**|Numero massimo dei / o fisiche legge per il piano di query entro l'intervallo di aggregazione (espresso come un numero di pagine da 8KB lettura).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**stdev_physical_io_reads**|**float**|Numero dei / o fisiche legge la deviazione standard per il piano di query entro l'intervallo di aggregazione (espresso come un numero di pagine da 8KB lettura).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**avg_clr_time**|**float**|Tempo medio di CLR per il piano di query entro l'intervallo di aggregazione (espresso in microsecondi).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_clr_time**|**bigint**|Ultima ora CLR per la query prevede entro l'intervallo di aggregazione (espresso in microsecondi).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**min_clr_time**|**bigint**|Tempo minimo di CLR per il piano di query entro l'intervallo di aggregazione (espresso in microsecondi).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**max_clr_time**|**bigint**|Tempo massimo di CLR per il piano di query entro l'intervallo di aggregazione (espresso in microsecondi).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**stdev_clr_time**|**float**|Deviazione standard di tempo CLR per il piano di query entro l'intervallo di aggregazione (espresso in microsecondi).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**avg_dop**|**float**|Media DOP (grado di parallelismo) per il piano di query entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_dop**|**bigint**|Ultimo valore DOP (grado di parallelismo) per il piano di query entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**min_dop**|**bigint**|Minimo DOP (grado di parallelismo) per il piano di query entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**max_dop**|**bigint**|Massimo grado di Parallelismo (grado di parallelismo) per il piano di query entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**stdev_dop**|**float**|Deviazione standard DOP (grado di parallelismo) per il piano di query entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**avg_query_max_used_memory**|**float**|Memoria Media autorizzazione (indicato come il numero di pagine da 8 KB) per il piano di query entro l'intervallo di aggregazione. Sempre 0 per query che usano in modo nativo compilati procedure ottimizzate per la memoria.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_query_max_used_memory**|**bigint**|Ultimo concessione di memoria (indicato come il numero di pagine da 8 KB) per il piano di query entro l'intervallo di aggregazione. Sempre 0 per query che usano in modo nativo compilati procedure ottimizzate per la memoria.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**min_query_max_used_memory**|**bigint**|Minima concessione di memoria (indicato come il numero di pagine da 8 KB) per il piano di query entro l'intervallo di aggregazione. Sempre 0 per query che usano in modo nativo compilati procedure ottimizzate per la memoria.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**max_query_max_used_memory**|**bigint**|Massima concessione di memoria (indicato come il numero di pagine da 8 KB) per il piano di query entro l'intervallo di aggregazione. Sempre 0 per query che usano in modo nativo compilati procedure ottimizzate per la memoria.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**stdev_query_max_used_memory**|**float**|Deviazione standard (indicata come il numero di pagine da 8 KB) concessione di memoria per il piano di query entro l'intervallo di aggregazione. Sempre 0 per query che usano in modo nativo compilati procedure ottimizzate per la memoria.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**avg_rowcount**|**float**|Numero medio di righe restituite per il piano di query entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_rowcount**|**bigint**|Numero di righe restituite dall'ultima esecuzione del piano di query entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**min_rowcount**|**bigint**|Numero minimo di righe restituite per la query prevede entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**max_rowcount**|**bigint**|Numero massimo di righe restituite per la query prevede entro l'intervallo di aggregazione.|  
|**stdev_rowcount**|**float**|Numero di righe restituite deviazione standard per il piano di query entro l'intervallo di aggregazione.|
|**avg_log_bytes_used**|**float**|Numero medio di byte nel log del database utilizzato dal piano di query, entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_log_bytes_used**|**bigint**|Numero di byte nel log del database utilizzate durante l'ultima esecuzione del piano di query, entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**min_log_bytes_used**|**bigint**|Numero minimo di byte nel log del database utilizzato dal piano di query, entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**max_log_bytes_used**|**bigint**|Numero massimo di byte nel log del database utilizzato dal piano di query, entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**stdev_log_bytes_used**|**float**|Deviazione standard del numero di byte nel log del database utilizzato da un piano di query, entro l'intervallo di aggregazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|  
|**avg_page_server_io_reads**|**float**|Numero medio di pagina legge i/o server per il piano di query entro l'intervallo di aggregazione. (espresso come un numero di pagine da 8KB lettura).<br><br/>**Nota:** Si applica a: Con Iperscalabilità di Database SQL di Azure</br> Azure SQL Data Warehouse, database SQL di Azure, MI (non su scala molto vasta) restituirà sempre zero (0).|
|**last_page_server_io_reads**|**bigint**|Ultimo numero dei / o di pagine server legge per il piano di query entro l'intervallo di aggregazione. (espresso come un numero di pagine da 8KB lettura).<br><br/>**Nota:** Si applica a: Con Iperscalabilità di Database SQL di Azure </br> Azure SQL Data Warehouse, database SQL di Azure, MI (non su scala molto vasta) restituirà sempre zero (0).|
|**min_page_server_io_reads**|**bigint**|Numero minimo di pagina legge i/o server per il piano di query entro l'intervallo di aggregazione. (espresso come un numero di pagine da 8KB lettura).<br><br/>**Nota:** Si applica a: Con Iperscalabilità di Database SQL di Azure </br> Azure SQL Data Warehouse, database SQL di Azure, MI (non su scala molto vasta) restituirà sempre zero (0).|
|**max_page_server_io_reads**|**bigint**|Numero massimo di pagina legge i/o server per il piano di query entro l'intervallo di aggregazione. (espresso come un numero di pagine da 8KB lettura).<br><br/>**Nota:** Si applica a: Con Iperscalabilità di Database SQL di Azure </br> Azure SQL Data Warehouse, database SQL di Azure, MI (non su scala molto vasta) restituirà sempre zero (0).|
|**stdev_page_server_io_reads**|**float**|Numero di server di pagine i/o legge la deviazione standard per il piano di query entro l'intervallo di aggregazione. (espresso come un numero di pagine da 8KB lettura).<br><br/>**Nota:** Si applica a: Con Iperscalabilità di Database SQL di Azure </br> Azure SQL Data Warehouse, database SQL di Azure, MI (non su scala molto vasta) restituirà sempre zero (0).|
  
## <a name="permissions"></a>Permissions  
 Richiede la **VIEW DATABASE STATE** l'autorizzazione.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoraggio delle prestazioni tramite Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Query Store Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
