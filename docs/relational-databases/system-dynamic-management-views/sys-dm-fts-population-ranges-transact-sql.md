---
title: sys. dm_fts_population_ranges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_population_ranges
- sys.dm_fts_population_ranges_TSQL
- dm_fts_population_ranges_TSQL
- dm_fts_population_ranges
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_population_ranges dynamic management view
ms.assetid: 58d8564b-9c43-4965-a31c-2893890334ef
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4b023dcfbf413162c6118ec7f590c1e2326a7813
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738648"
---
# <a name="sysdm_fts_population_ranges-transact-sql"></a>sys.dm_fts_population_ranges (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce informazioni sugli intervalli specifici correlati a un popolamento dell'indice full-text in corso.  
   
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**memory_address**|**varbinary (8)**|Indirizzo dei buffer di memoria allocati per l'attività correlata all'intervallo secondario corrente del popolamento di un indice full-text.|  
|**parent_memory_address**|**varbinary (8)**|Indirizzo dei buffer di memoria che rappresentano l'oggetto padre di tutti gli intervalli di popolamento correlati a un indice full-text.|  
|**is_retry**|**bit**|Se il valore è 1, questo intervallo secondario è responsabile del nuovo tentativo di esecuzione di righe in cui si sono verificati errori.|  
|**session_id**|**smallint**|ID della sessione che elabora l'attività.|  
|**processed_row_count**|**int**|Numero di righe elaborate dall'intervallo. Lo stato viene mantenuto e calcolato ogni 5 minuti, anziché con il commit di ogni batch.|  
|**error_count**|**int**|Numero di righe in cui l'intervallo ha rilevato errori. Lo stato viene mantenuto e calcolato ogni 5 minuti, anziché con il commit di ogni batch.|  
  
## <a name="permissions"></a>Autorizzazioni  

In è [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] richiesta l' `VIEW SERVER STATE` autorizzazione.   
Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, richiede l' `VIEW DATABASE STATE` autorizzazione nel database. Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli standard e Basic, richiede l' **amministratore del server** o un account **amministratore Azure Active Directory** .   
 
## <a name="physical-joins"></a>Join fisici  
 ![Join significativi di questa DMV](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-population-ranges-1.gif "Join significativi di questa DMV")  
  
## <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
|From|A|Relazione|  
|----------|--------|------------------|  
|dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|Molti-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
  [Funzioni e viste a gestione dinamica per la ricerca full-text e la ricerca semantica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

