---
title: Viste di sistema, Stored procedure, viste a gestione dinamica e tipi di attesa per OLTP In memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: efaa59e3-dbfa-407f-b1aa-cb0c6602ea17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d047cbc4fe3ba3f4945acd9da4f627a05992e779
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52406161"
---
# <a name="system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp"></a>Viste di sistema, stored procedure, tipi di attesa e DMV per OLTP in memoria
  Questo argomento fornisce brevi descrizioni e collegamenti ai numerosi oggetti di database che supportano OLTP In memoria.  
  
### <a name="system-views"></a>Viste di sistema  
  
|Vista di sistema|Descrizione|Funzionalità OLTP in memoria|  
|-----------------|-----------------|-----------------------------|  
|[sys.data_spaces &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-data-spaces-transact-sql)|Verifica se un filegroup contiene dati ottimizzati per la memoria.|Le colonne seguenti indicano valori aggiuntivi: **tipo** e **type_desc**.|  
|[sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)|Verifica se un indice è contenuto in una tabella ottimizzata per la memoria.|Le colonne seguenti indicano valori aggiuntivi: **tipo** e **type_desc**.|  
|[sys.parameters &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameters-transact-sql)|Verifica che un parametro non ammetta i valori Null (per un'esecuzione più efficiente di una stored procedure compilata in modo nativo).|**is_nullable** colonna.|  
|[Sys.all_sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql)|Verifica che una stored procedure sia compilata in modo nativo.|**uses_native_compilation** colonna.|  
|[sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)|Verifica che una stored procedure sia compilata in modo nativo.|**uses_native_compilation** colonna.|  
|[table_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-table-types-transact-sql)|Verifica che una tabella sia ottimizzata per la memoria.|**is_memory_optimized** colonna.|  
|[sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|Controllare se una tabella con ottimizzazione per la memoria e controlla l'impostazione di durabilità di una tabella.|**durabilità**, **durability_desc**, e **is_memory_optimized** colonne.|  
|[sys.hash_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-hash-indexes-transact-sql)|Mostra gli indici hash di una tabella ottimizzata per la memoria.|Specifico di OLTP in memoria.|  
  
### <a name="metadata-functions"></a>Funzioni per i metadati  
  
|Funzione per i metadati|Descrizione|Funzionalità OLTP in memoria|  
|-----------------------|-----------------|-----------------------------|  
|[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|Verifica che gli oggetti di database siano ottimizzati per la memoria.|**ExecIsWithNativeCompilation** e **TableIsMemoryOptimized** proprietà.<br /><br /> Il **IsSchemaBound** proprietà supporta il tipo di oggetto Procedure (restituisce 0 per le stored procedure anziché NULL).|  
|[SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|Verifica che un server supporti OLTP In memoria.|**IsXTPSupported** proprietà.|  
  
### <a name="system-stored-procedures"></a>Stored procedure di sistema  
  
|Stored procedure|Descrizione|  
|----------------------|-----------------|  
|[sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)|Associare un database OLTP In memoria a un pool di risorse.|  
|[Sys.sp_xtp_checkpoint_force_garbage_collection &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-checkpoint-force-garbage-collection-transact-sql)|Avviare la procedura di garbage collection in un database OLTP In memoria.|  
|[Sys. sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql)|Abilitare della raccolta di statistiche per stored procedure compilate in modo nativo|  
|[Sys. sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql)|Abilitare la raccolta di statistiche di query per stored procedure compilate in modo nativo|  
|[Sys. sp_xtp_merge_checkpoint_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql)|Unire file di dati e differenziali.|  
|[Sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)|Rimuovere l'associazione tra un database e un pool di risorse.|  
  
## <a name="dynamic-management-views-dmvs"></a>Viste a gestione dinamica (DMV)  
 Sono disponibili diverse viste a gestione dinamica per le tabelle ottimizzate per la memoria.  
  
 Per informazioni dettagliate, vedere [viste a gestione dinamica ottimizzati per la memoria nella tabella &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql).  
  
## <a name="wait-types"></a>Tipi di attesa  
 Esistono diversi tipi di attesa che supportano OLTP In memoria.  
  
 Per informazioni dettagliate, vedere i tipi che hanno il prefisso di attesa **WAIT_XTP**, e **XTPPROC** nel [DM os_wait_stats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql) argomento.  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [Supporto di Transact-SQL per OLTP in memoria](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
