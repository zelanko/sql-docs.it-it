---
title: sys. dm_column_store_object_pool (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83369736ee18c36b3967bbbd129e0fd64574a2ed
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68265995"
---
# <a name="sysdm_column_store_object_pool-transact-sql"></a>sys. dm_column_store_object_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Restituisce i conteggi dei diversi tipi di utilizzo del pool di memoria oggetto per gli oggetti dell'indice columnstore.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|ID del database. Questa operazione è univoca all'interno di un'istanza di un database SQL Server o di un server di database SQL di Azure. |  
|`object_id`|`int`|ID dell'oggetto. L'oggetto è uno dei object_types. | 
|`index_id`|`int`|ID dell'indice columnstore.|  
|`partition_number`|`bigint`|Numero di partizione in base 1 all'interno dell'indice o heap. Ogni tabella o vista include almeno una partizione.| 
|`column_id`|`int`|ID della colonna columnstore. Questo valore è NULL per DELETE_BITMAP.| 
|`row_group_id`|`int`|ID di rowgroup.|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT-un segmento di colonna. `object_id`ID del segmento. Un segmento archivia tutti i valori di una colonna all'interno di un rowgroup. Se, ad esempio, una tabella contiene 10 colonne, saranno presenti 10 segmenti di colonna per ogni rowgroup. <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY: dizionario globale che contiene informazioni di ricerca per tutti i segmenti di colonna della tabella.<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY: un dizionario locale associato a una colonna.<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY: un'altra rappresentazione del dizionario globale. Questa operazione fornisce una ricerca inversa del valore da dictionary_id. Utilizzato per creare segmenti compressi come parte del motore di tupla o del caricamento bulk.<br /><br /> COLUMN_SEGMENT_DELETE_BITMAP: bitmap che tiene traccia delle eliminazioni di segmenti. Esiste una bitmap Delete per partizione.|  
|`access_count`|`int`|Numero di accessi in lettura o scrittura a questo oggetto.|  
|`memory_used_in_bytes`|`bigint`|Memoria utilizzata da questo oggetto nel pool di oggetti.|  
|`object_load_time`|`datetime`|Tempo di clock per il momento in cui object_id è stato introdotto nel pool di oggetti.|  
  
## <a name="permissions"></a>Autorizzazioni  

In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]è richiesta `VIEW SERVER STATE` l'autorizzazione.   
Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, richiede l' `VIEW DATABASE STATE` autorizzazione nel database. Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli standard e Basic, richiede l' **amministratore del server** o un account **amministratore Azure Active Directory** .   
 
## <a name="see-also"></a>Vedere anche  
  
 [Funzioni e viste a gestione dinamica relative agli indici &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys. dm_db_index_operational_stats &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys. Indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys. Objects &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Monitoraggio e ottimizzazione delle prestazioni](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
