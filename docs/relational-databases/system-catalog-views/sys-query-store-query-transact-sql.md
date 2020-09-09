---
description: sys. query_store_query (Transact-SQL)
title: sys. query_store_query (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_QUERY
- SYS.QUERY_STORE_QUERY_TSQL
- SYS.QUERY_STORE_QUERY
- QUERY_STORE_QUERY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_query catalog view
- sys.query_store_query catalog view
ms.assetid: bdee149e-7556-4fc3-8242-925dd4b7b6ac
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e96891721e5c42deb03e697c06a7f99ce353ad99
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546718"
---
# <a name="sysquery_store_query-transact-sql"></a>sys. query_store_query (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  Contiene informazioni sulla query e le relative statistiche di esecuzione di runtime aggregate associate.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**query_id**|**bigint**|Chiave primaria.|  
|**query_text_id**|**bigint**|Chiave esterna. Join a [sys. query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|  
|**context_settings_id**|**bigint**|Chiave esterna. Join a [sys. query_context_settings &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|  
|**object_id**|**bigint**|ID dell'oggetto di database di cui fa parte la query (stored procedure, trigger, CLR UDF/UDAgg e così via). 0 se la query non viene eseguita come parte di un oggetto di database (query ad hoc).<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|  
|**batch_sql_handle**|**varbinary(64)**|ID del batch di istruzioni di cui fa parte la query. Popolato solo se la query fa riferimento a tabelle temporanee o variabili di tabella.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre *null*.|  
|**query_hash**|**binario (8)**|Hash MD5 della singola query, basato sull'albero delle query logiche. Include gli hint di ottimizzazione.|  
|**is_internal_query**|**bit**|La query è stata generata internamente.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|  
|**query_parameterization_type**|**tinyint**|Tipo di parametrizzazione:<br /><br /> 0 - Nessuno<br /><br /> 1-utente<br /><br /> 2-semplice<br /><br /> 3-forzata<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|  
|**query_parameterization_type_desc**|**nvarchar(60)**|Descrizione testuale per il tipo di parametrizzazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre *None*.|  
|**initial_compile_start_time**|**datetimeoffset**|Ora di inizio compilazione.|  
|**last_compile_start_time**|**datetimeoffset**|Ora di inizio compilazione.|  
|**last_execution_time**|**datetimeoffset**|L'ora dell'ultima esecuzione fa riferimento all'ora dell'ultima fine della query o del piano.|  
|**last_compile_batch_sql_handle**|**varbinary(64)**|Handle dell'ultimo batch SQL in cui la query è stata usata per la prima volta. Può essere fornito come input per [sys. dm_exec_sql_text &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) per ottenere il testo completo del batch.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre *null*.|  
|**last_compile_batch_offset_start**|**bigint**|Informazioni che possono essere fornite a sys. dm_exec_sql_text insieme a last_compile_batch_sql_handle.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_compile_batch_offset_end**|**bigint**|Informazioni che possono essere fornite a sys. dm_exec_sql_text insieme a last_compile_batch_sql_handle.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|  
|**count_compiles**|**bigint**|Statistiche di compilazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre uno (1).|  
|**avg_compile_duration**|**float**|Statistiche di compilazione in microsecondi.|  
|**last_compile_duration**|**bigint**|Statistiche di compilazione in microsecondi.|  
|**avg_bind_duration**|**float**|Statistiche di binding in microsecondi.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|  
|**last_bind_duration**|**bigint**|Statistiche di binding.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|  
|**avg_bind_cpu_time**|**float**|Statistiche di binding.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|  
|**last_bind_cpu_time**|**bigint**|Statistiche di binding.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|  
|**avg_optimize_duration**|**float**|Statistiche di ottimizzazione in microsecondi.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_optimize_duration**|**bigint**|Statistiche di ottimizzazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**avg_optimize_cpu_time**|**float**|Statistiche di ottimizzazione in microsecondi.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_optimize_cpu_time**|**bigint**|Statistiche di ottimizzazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**avg_compile_memory_kb**|**float**|Statistiche memoria di compilazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**last_compile_memory_kb**|**bigint**|Statistiche memoria di compilazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**max_compile_memory_kb**|**bigint**|Statistiche memoria di compilazione.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**is_clouddb_internal_query**|**bit**|Sempre 0 in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] locale.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione **View database state** .  
  
## <a name="see-also"></a>Vedere anche  
 [sys. database_query_store_options &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys. query_context_settings &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys. query_store_plan &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys. query_store_query_text &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys. query_store_runtime_stats &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys. query_store_runtime_stats_interval &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoraggio delle prestazioni tramite Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Stored procedure di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
