---
title: DM resource_governor_resource_pool_affinity (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_resource_pool_affinity_TSQL
- sys.dm_resource_governor_resource_pool_affinity
- dm_resource_governor_resource_pool_affinity
- dm_resource_governor_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_resource_pool_affinity
- sys.dm_resource_governor_resource_pool_affinity
ms.assetid: a197ec19-a2ba-44f5-a4f2-3eee33ebd77d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3b51cd98cd9ef0e6adc3d17d2b1263a62604ab52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053275"
---
# <a name="sysdmresourcegovernorresourcepoolaffinity-transact-sql"></a>sys.dm_resource_governor_resource_pool_affinity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Consente di tenere traccia dell'affinità di pool di risorse.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|----------------|---------------|-----------------|  
|Pool_id|**int**|ID del pool di risorse. Non ammette i valori Null.|  
|Processor_group|**smallint**|ID del gruppo di processori logici Windows. Non ammette i valori Null.|  
|Scheduler_mask|**bigint**|Maschera binaria che rappresenta le utilità di pianificazione associate a questo pool. Non ammette i valori Null.|  
  
## <a name="remarks"></a>Note  
 I pool creati con un'affinità equivalente ad AUTO non saranno visualizzati in questa vista perché non presentano affinità. Per altre informazioni, vedere la [crea POOL di risorse &#40;Transact-SQL&#41; ](../../t-sql/statements/create-resource-pool-transact-sql.md) e [ALTER RESOURCE POOL &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-resource-pool-transact-sql.md) istruzioni.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
