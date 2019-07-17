---
title: Sys.dm_fts_index_population (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_population
- dm_fts_index_population
- sys.dm_fts_index_population_TSQL
- dm_fts_index_population_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_population dynamic management view
ms.assetid: 82d1c102-efcc-4b60-9a5e-3eee299bcb2b
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2c97061b08475549b2e8ebccdc75a56f74eb6614
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265935"
---
# <a name="sysdmftsindexpopulation-transact-sql"></a>sys.dm_fts_index_population (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni sui popolamenti di frasi chiave semantiche e indici full-text in corso in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID del database contenente l'indice full-text in fase di popolamento.|  
|**catalog_id**|**int**|ID del catalogo full-text contenente l'indice full-text.|  
|**table_id**|**int**|ID della tabella per la quale l'indice full-text è in fase di popolamento.|  
|**memory_address**|**varbinary(8)**|Indirizzo di memoria della struttura dei dati interna utilizzata per rappresentare un popolamento attivo.|  
|**population_type**|**int**|Tipo di popolamento. I tipi validi sono:<br /><br /> 1 = Popolamento completo<br /><br /> 2 = Popolamento incrementale basato su timestamp<br /><br /> 3 = Aggiornamento manuale delle modifiche rilevate<br /><br /> 4 = Aggiornamento in background delle modifiche rilevate|  
|**population_type_description**|**nvarchar(120)**|Descrizione del tipo di popolamento.|  
|**is_clustered_index_scan**|**bit**|Indica se il popolamento implica un'analisi dell'indice cluster.|  
|**range_count**|**int**|Numero di intervalli secondari in cui il popolamento è stato suddiviso mediante parallelismo.|  
|**completed_range_count**|**int**|Numero di intervalli per i quali l'elaborazione è completata.|  
|**outstanding_batch_count**|**int**|Numero corrente di batch in attesa per questo popolamento. Per altre informazioni, vedere [fts_outstanding_batches &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md).|  
|**status**|**int**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Stato del popolamento. Nota: alcuni stati sono temporanei. I tipi validi sono:<br /><br /> 3 = avvio in corso<br /><br /> 5 = elaborazione normale in corso<br /><br /> 7 = elaborazione arrestata<br /><br /> Questo stato si verifica ad esempio quando è in corso un'unione automatica.<br /><br /> 11 = popolamento interrotto<br /><br /> 12 = Elaborazione in corso di un'estrazione della somiglianza semantica|  
|**status_description**|**nvarchar(120)**|Descrizione dello stato del popolamento.|  
|**completion_type**|**int**|Stato della modalità di completamento del popolamento.|  
|**completion_type_description**|**nvarchar(120)**|Descrizione del tipo di completamento.|  
|**worker_count**|**int**|Il valore è sempre 0 .|  
|**queued_population_type**|**int**|Tipo di popolamento in base alle modifiche rilevate che verrà eseguito dopo l'eventuale popolamento corrente.|  
|**queued_population_type_description**|**nvarchar(120)**|Descrizione dell'eventuale popolamento successivo. Ad esempio, quando CHANGE TRACKING = AUTO e il popolamento completo iniziale è in corso, questa colonna potrebbe visualizzare un messaggio relativo al popolamento automatico.|  
|**start_time**|**datetime**|Ora di inizio del popolamento.|  
|**incremental_timestamp**|**timestamp**|Rappresenta il timestamp iniziale per il popolamento completo. Per tutti gli altri tipi di popolamento questo valore corrisponde all'ultimo checkpoint di cui è stato eseguito il commit che rappresenta lo stato dei popolamenti.|  
  
## <a name="remarks"></a>Note  
 Quando l'indicizzazione semantica statistica è abilitata in aggiunta all'indicizzazione full-text, l'estrazione semantica e il popolamento di frasi chiave, nonché l'estrazione dei dati di somiglianza del documento, si verificano contemporaneamente all'indicizzazione full-text. Il popolamento dell'indice di somiglianza del documento si verifica successivamente, in una seconda fase. Per altre informazioni, vedere [gestire e monitorare la ricerca semantica](../../relational-databases/search/manage-and-monitor-semantic-search.md).  
  
## <a name="permissions"></a>Permissions  

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, è necessario il `VIEW DATABASE STATE` autorizzazione nel database. Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard e i livelli Basic, è necessario il **amministratore del Server** o un' **amministratore di Azure Active Directory** account.   
  
## <a name="physical-joins"></a>Join fisici  
 ![Join significativi di questa vista a gestione dinamica](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-index-population-1.gif "join significativi di questa vista a gestione dinamica")  
  
## <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
|From|Per|Relazione|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|Uno-a-uno|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|Uno-a-uno|  
|dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|Molti-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funzioni e viste a gestione dinamica la ricerca semantica e ricerca full-Text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

