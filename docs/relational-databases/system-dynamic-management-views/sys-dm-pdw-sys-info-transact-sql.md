---
description: sys.dm_pdw_sys_info (Transact-SQL)
title: sys.dm_pdw_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c98d2ee4dd5dca1b902963976309fbdc005225cc
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035214"
---
# <a name="sysdm_pdw_sys_info-transact-sql"></a>sys.dm_pdw_sys_info (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Fornisce un set di contatori a livello di appliance che riflettono l'attività complessiva nell'appliance.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|Numero di sessioni attualmente presenti nel sistema.|da 0 a max_active_sessions (vedere di seguito).|  
|idle_sessions|**int**|Numero di sessioni attualmente inattive.||  
|active_requests|**int**|Numero di richieste attive attualmente in esecuzione.||  
|queued_requests|**int**|Numero di richieste attualmente accodate.||  
|active_loads|**int**|Numero di caricamenti attualmente in esecuzione nel sistema.||  
|queued_loads|**int**|Numero di caricamenti in coda in attesa di esecuzione.||  
|active_backups|**int**|Numero di backup attualmente in esecuzione.||  
|active_restores|**int**|Numero di ripristini di backup attualmente in esecuzione.||  
  
## <a name="see-also"></a>Vedere anche  
 [Analisi delle sinapsi di Azure e DMV Parallel data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
