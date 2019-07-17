---
title: Sys. spatial_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.spatial_indexes_TSQL
- spatial_indexes
- spatial_indexes_TSQL
- sys.spatial_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_indexes catalog view
ms.assetid: 40e967d5-2e8d-45af-bf5e-5251493cf7cb
author: stevestein
ms.author: sstein
ms.openlocfilehash: f3b2172e48ec787c37fd9b3daab6cafb5c49f88f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078632"
---
# <a name="sysspatialindexes-transact-sql"></a>sys.spatial_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rappresenta le principali informazioni per gli indici spaziali.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|\<colonne ereditate >||Eredita le colonne da [Sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).|  
|spatial_index_type|**tinyint**|Tipo di indice spaziale:<br /><br /> 1 = Indice spaziale geometrico<br /><br /> 2 = Indice spaziale geografico|  
|spatial_index_type_desc|**nvarchar(60)**|Descrizione del tipo di indice spaziale:<br /><br /> GEOMETRY = Indice spaziale geometrico<br /><br /> GEOGRAPHY = Indice spaziale geografico|  
|tessellation_scheme|**sysname**|Nome dello schema a mosaico:<br /><br /> GEOMETRY_GRID, GEOMETRY_AUTO_GRID,<br /><br /> GEOGRAPHY_GRID, GEOGRAPHY_AUTO_GRID<br /><br /> Nota: Per informazioni sugli schemi a mosaico, vedere [panoramica degli indici spaziali](../../relational-databases/spatial/spatial-indexes-overview.md).|  
|\<colonne ereditate >||Eredita le colonne da [Sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).<br /><br /> Le colonne ereditate has_filter e filter_definition vengono visualizzate dopo le colonne specifiche per gli indici spaziali.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_index_tessellations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Panoramica degli indici spaziali](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
