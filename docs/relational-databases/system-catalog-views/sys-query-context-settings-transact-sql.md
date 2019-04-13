---
title: sys.query_context_settings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS
- QUERY_CONTEXT_SETTINGS
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_context_settings catalog view
ms.assetid: 3c1887df-6bd8-491e-82fc-d25ad9589faf
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6c7ab77981c329c334b22d6fd9735188882b385c
ms.sourcegitcommit: acb5de9f493238180d13baa302552fdcc30d83c0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/12/2019
ms.locfileid: "59542141"
---
# <a name="sysquerycontextsettings-transact-sql"></a>sys.query_context_settings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contiene informazioni sulla semantica che interessano le impostazioni di contesto associate a una query. Sono disponibili numerose impostazioni del contesto in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che influenzano la semantica di query (definendo il risultato corretto della query). Lo stesso testo di query compilato con impostazioni diverse può produrre risultati diversi (a seconda dei dati sottostanti).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**context_settings_id**|**bigint**|Chiave primaria. Questo valore è esposto in Showplan XML per le query.|  
|**set_options**|**varbinary(8)**|Maschera di bit che riflette lo stato delle diverse opzioni SET. Per altre informazioni, vedere [exec_plan_attributes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md).|  
|**language_id**|**smallint**|L'id della lingua. Per altre informazioni, vedere [Sys. syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).|  
|**date_format**|**smallint**|Il formato di Data. Per altre informazioni, vedere [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md).|  
|**date_first**|**tinyint**|Il primo valore di Data. Per altre informazioni, vedere [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md).|  
|**status**|**varbinary(2)**|Campo di maschera di bit che indica i tipo di query o un contesto in cui query è stata eseguita. <br />Valore della colonna può essere una combinazione di più flag (espressa in formato esadecimale):<br /><br /> 0x0 - query normali (Nessun flag specifico)<br /><br /> 0x1 - query eseguita tramite una delle API stored procedure del cursore<br /><br /> 0x2 - query per le notifiche<br /><br /> 0x4 - interno della query<br /><br /> 0x8 - automatica query con parametri senza parametrizzazione universale<br /><br /> 0x10 - recupero di cursore refresh query<br /><br /> 0x20 - query che viene viene utilizzata nelle richieste di aggiornamento del cursore<br /><br /> 0x40 - set di risultati iniziale viene restituito quando viene aperto un cursore (recupero automatico del cursore)<br /><br /> 0x80 - query crittografata<br /><br /> 0x100 - query nel contesto del predicato di sicurezza a livello di riga|  
|**required_cursor_options**|**int**|Opzioni di cursore specificate dall'utente, ad esempio il tipo di cursore.|  
|**acceptable_cursor_options**|**int**|Opzioni di cursore che potrebbero essere convertite in modo implicito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per supportare l'esecuzione dell'istruzione.|  
|**merge_action_type**|**smallint**|Il tipo di piano di esecuzione di trigger utilizzato come risultato di una **MERGE** istruzione.<br /><br /> 0 indica un piano non-trigger, un piano di trigger che non viene eseguito come risultato di una **MERGE** istruzione o un piano di trigger che viene eseguita come risultato di una **MERGE** istruzione che specifica solo un **Eliminare** azione.<br /><br /> 1 indica un' **inserire** piano di trigger che viene eseguito come risultato di una **MERGE** istruzione.<br /><br /> 2 indica un' **UPDATE** piano di trigger che viene eseguito come risultato di una **MERGE** istruzione.<br /><br /> 3 indica che un **eliminare** piano di trigger che viene eseguito come risultato di una **MERGE** istruzione contenente un corrispondente **Inserisci** o **UPDATE** azione.<br /><br /> <br /><br /> Per i trigger nidificati eseguiti da azioni a catena, questo valore è l'azione del **MERGE** istruzione che provoca la propagazione.|  
|**default_schema_id**|**int**|ID dello schema predefinito, che consente di risolvere i nomi che non sono completi.|  
|**is_replication_specific**|**bit**|Utilizzato per la replica.|  
|**is_contained**|**varbinary(1)**|1 indica un database indipendente.|  
  
## <a name="permissions"></a>Permissions  
 Richiede la **VIEW DATABASE STATE** l'autorizzazione.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoraggio delle prestazioni tramite Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Stored procedure di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
