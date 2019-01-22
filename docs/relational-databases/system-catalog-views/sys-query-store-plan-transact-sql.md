---
title: sys.query_store_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_PLAN_TSQL
- SYS.QUERY_STORE_PLAN
- SYS.QUERY_STORE_PLAN_TSQL
- QUERY_STORE_PLAN
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_plan catalog view
- sys.query_store_plan catalog view
ms.assetid: b4d05439-6360-45db-b1cd-794f4a64935e
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ea7c955718dbe6d2437b44b915057fc095151dc4
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/22/2019
ms.locfileid: "54419796"
---
# <a name="sysquerystoreplan-transact-sql"></a>sys.query_store_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contiene informazioni su ogni piano di esecuzione associato a una query.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|
|**plan_id**|**bigint**|Chiave primaria.|  
|**query_id**|**bigint**|Chiave esterna. Crea un join al [Sys. query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md).|  
|**plan_group_id**|**bigint**|ID del gruppo del piano. Query basate su cursori richiedono in genere più (popolare e recuperare) piani. Popolare e si applica ai piani di recupero vengono compilati insieme nello stesso gruppo.<br /><br /> 0 indica che piano non è presente in un gruppo.|  
|**engine_version**|**nvarchar(32)**|Versione del modulo di gestione usato per compilare il piano nella **'revisione'** formato.|  
|**compatibility_level**|**smallint**|Livello di compatibilità del database del database di cui viene fatto riferimento nella query.|  
|**query_plan_hash**|**binary(8)**|Hash MD5 del singolo piano.|  
|**query_plan**|**nvarchar(max)**|Showplan XML per il piano di query.|  
|**is_online_index_plan**|**bit**|Piano è stato usato durante la compilazione di un indice online.|  
|**is_trivial_plan**|**bit**|Piano è un semplice (output nella fase 0 di query optimizer).|  
|**is_parallel_plan**|**bit**|Piano è parallelo.|  
|**is_forced_plan**|**bit**|Piano viene contrassegnato come forzata quando l'utente esegue stored procedure **sys.sp_query_store_force_plan**. Meccanismo di utilizzo forzato *non garantisce* verrà utilizzato per la query fa riferimento esattamente questo piano **query_id**. Uso forzato del piano fa in modo che query da compilare nuovamente e in genere produce esattamente il piano identici o simile al piano di cui fa riferimento **plan_id**. Se uso forzato del piano non riesce, **force_failure_count** viene incrementato e **last_force_failure_reason** viene popolato con il motivo dell'errore.|  
|**is_natively_compiled**|**bit**|Piano include procedure ottimizzate per la memoria compilate in modo nativo. (0 = FALSE, 1 = TRUE).|  
|**force_failure_count**|**bigint**|Numero di volte in cui è Impossibile forzare l'utilizzo di questo piano. Può essere incrementato solo quando la query viene ricompilata (*non a ogni esecuzione*). Viene reimpostato su 0 ogni volta **is_plan_forced** viene modificato da **FALSE** al **TRUE**.|  
|**last_force_failure_reason**|**int**|Motivo di uso forzato del piano perché non è riuscito.<br /><br /> 0: nessun errore, in caso contrario, numero di errore dell'errore che ha causato l'utilizzo forzato esito negativo<br /><br /> 8637: ONLINE_INDEX_BUILD<br /><br /> 8683: INVALID_STARJOIN<br /><br /> 8684: TIME_OUT<br /><br /> 8689: NO_DB<br /><br /> 8690: HINT_CONFLICT<br /><br /> 8691: SETOPT_CONFLICT<br /><br /> 8694: DQ_NO_FORCING_SUPPORTED<br /><br /> 8698: NO_PLAN<br /><br /> 8712: NO_INDEX<br /><br /> 8713: VIEW_COMPILE_FAILED<br /><br /> \<altro valore >: GENERAL_FAILURE|  
|**last_force_failure_reason_desc**|**nvarchar(128)**|Descrizione testuale del last_force_failure_reason_desc.<br /><br /> ONLINE_INDEX_BUILD: query tenta di modificare i dati mentre la tabella di destinazione ha un indice che viene compilato online<br /><br /> INVALID_STARJOIN: piano contiene specifica StarJoin non valida<br /><br /> TIME_OUT: Numero di Query Optimizer ha superato di operazioni consentite durante la ricerca del piano specificato dal piano forzato<br /><br /> NO_DB: Un database specificato nel piano non esiste<br /><br /> HINT_CONFLICT: Impossibile compilare la query piano è in conflitto con un hint di query<br /><br /> DQ_NO_FORCING_SUPPORTED: Impossibile eseguire query piano è in conflitto con l'uso di query distribuita o operazioni full-text.<br /><br /> NO_PLAN: Query processor non è stato possibile generare il piano di query perché il piano forzato non è stato possibile verificare la validità per la query<br /><br /> NO_INDEX: Indice specificato nel piano non è più presente<br /><br /> VIEW_COMPILE_FAILED: Non è stato possibile forzare il piano di query a causa di un problema in una vista indicizzata a cui fa riferimento il piano<br /><br /> GENERAL_FAILURE: errore generale di forzatura (non coperte da motivi sopra)|  
|**count_compiles**|**bigint**|Pianificare le statistiche di compilazione.|  
|**initial_compile_start_time**|**datetimeoffset**|Pianificare le statistiche di compilazione.|  
|**last_compile_start_time**|**datetimeoffset**|Pianificare le statistiche di compilazione.|  
|**last_execution_time**|**datetimeoffset**|Ora dell'ultima esecuzione si riferisce all'ultima ora di fine del piano di query /.|  
|**avg_compile_duration**|**float**|Pianificare le statistiche di compilazione.|  
|**last_compile_duration**|**bigint**|Pianificare le statistiche di compilazione.|  
|**plan_forcing_type**|**int**|Tipo di utilizzo forzato del piano.<br /><br />0: Nessuno<br /><br />1: MANUAL<br /><br />2: AUTO|  
|**plan_forcing_type_desc**|**nvarchar(60)**|Descrizione di plan_forcing_type testo.<br /><br />NONE: Nessun utilizzo forzato del piano<br /><br />MANUAL: Piano forzato da utente<br /><br />AUTO: Piano forzato dall'ottimizzazione automatica|  

## <a name="plan-forcing-limitations"></a>Limitazioni di uso forzato del piano
Query Store è dotato di un meccanismo per imporre a Query Optimizer l'uso di determinati piani di esecuzione. Esistono tuttavia alcune limitazioni che possono impedire l'imposizione di un piano. 

In primo luogo, se il piano contiene i costrutti seguenti:
* Istruzione Insert bulk.
* Istruzione Insert bulk.
* Riferimento a una tabella esterna
* Query distribuita o operazioni full-text
* Uso di query globali 
* Cursori
* Specifica di join a stella non valida 

In secondo luogo, quando gli oggetti su cui si basa il piano non sono più disponibili:
* Database (se il database da cui ha avuto origine il piano non esiste più)
* Indice (non più esistente o disabilitato)

Infine, problemi del piano stesso:
* Piano non valido per query
* Numero di operazioni consentite per Query Optimizer superato
* XML del piano formato in modo non corretto

## <a name="permissions"></a>Permissions  
 Richiede la **VIEW DATABASE STATE** l'autorizzazione.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoraggio delle prestazioni tramite Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Query Store Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
