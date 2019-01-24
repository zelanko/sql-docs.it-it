---
title: sys.query_store_query_text (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_QUERY_TEXT
- QUERY_STORE_QUERY_TEXT
- SYS.QUERY_STORE_QUERY_TEXT_TSQL
- QUERY_STORE_QUERY_TEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_store_query_text catalog view
- query_store_query_text catalog view
ms.assetid: f7032fa0-7c16-4492-bb82-685806c63a8c
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e41eca10cf5db5e34b5e9e9122eb56a1a236315e
ms.sourcegitcommit: 3d50caa30681bf384f5628b1dd3e06e24fc910cd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54838078"
---
# <a name="sysquerystorequerytext-transact-sql"></a>sys.query_store_query_text (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contiene il [!INCLUDE[tsql](../../includes/tsql-md.md)] testo e l'handle SQL della query.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**query_text_id**|**bigint**|Chiave primaria.|  
|**query_sql_text**|**nvarchar(max)**|Testo SQL della query, come specificato dall'utente. Include gli spazi vuoti, suggerimenti e commenti.|  
|**statement_sql_handle**|**vabinary(64)**|Handle SQL della singola query.|  
|**is_part_of_encrypted_module**|**bit**|Testo della query è una parte di un modulo crittografato.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
|**has_restricted_text**|**bit**|Testo della query contiene una password o altri termini unmentionable.<br/>**Nota:** Azure SQL Data Warehouse restituirà sempre zero (0).|
  
## <a name="permissions"></a>Permissions  
 Richiede la **VIEW DATABASE STATE** l'autorizzazione.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoraggio delle prestazioni tramite Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Stored procedure di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
