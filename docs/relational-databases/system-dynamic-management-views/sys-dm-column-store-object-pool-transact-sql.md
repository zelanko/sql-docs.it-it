---
title: sys.dm_column_store_object_pool (Transact-SQL) | Microsoft Docs
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
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265995"
---
# <a name="sysdmcolumnstoreobjectpool-transact-sql"></a>sys.dm_column_store_object_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Restituisce i conteggi dei diversi tipi di oggetto pool di utilizzo della memoria per gli oggetti indice columnstore.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|ID del database. Questo è univoco all'interno di un'istanza di un database di SQL Server o un server di database SQL di Azure. |  
|`object_id`|`int`|ID dell'oggetto. L'oggetto è uno degli oggetti object_type. | 
|`index_id`|`int`|ID dell'indice columnstore.|  
|`partition_number`|`bigint`|Numero di partizione in base 1 all'interno dell'indice o heap. Ogni tabella o vista che include almeno una partizione.| 
|`column_id`|`int`|ID della colonna columnstore. È NULL per DELETE_BITMAP.| 
|`row_group_id`|`int`|ID del rowgroup.|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT - un segmento di colonna. `object_id` è l'ID del segmento. Un segmento archivia tutti i valori per una colonna all'interno di un rowgroup. Ad esempio, se una tabella ha 10 colonne, esistono 10 segmenti di colonna per ogni rowgroup. <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY - globale dizionario che contiene le informazioni di ricerca su tutti i segmenti di colonna nella tabella.<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY - dizionario locale associato a una colonna.<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY - un'altra rappresentazione nel dizionario globale. In questo modo una ricerca inversa del valore da dictionary_id. Utilizzato per creare segmenti compressi come parte del processo Tuple-Mover o il caricamento Bulk.<br /><br /> COLUMN_SEGMENT_DELETE_BITMAP - Elimina una bitmap che tiene traccia di segmento. È presente una singola bitmap delete per ogni partizione.|  
|`access_count`|`int`|Numero di leggere o scrittura gli accessi a questo oggetto.|  
|`memory_used_in_bytes`|`bigint`|Memoria utilizzata da questo oggetto nel pool di oggetti.|  
|`object_load_time`|`datetime`|Ora per quando è stato portato object_id nel pool di oggetti.|  
  
## <a name="permissions"></a>Permissions  

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, è necessario il `VIEW DATABASE STATE` autorizzazione nel database. Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard e i livelli Basic, è necessario il **amministratore del Server** o un' **amministratore di Azure Active Directory** account.   
 
## <a name="see-also"></a>Vedere anche  
  
 [Funzioni a gestione dinamica e DMV correlate all'indice &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Monitoraggio e ottimizzazione delle prestazioni](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
