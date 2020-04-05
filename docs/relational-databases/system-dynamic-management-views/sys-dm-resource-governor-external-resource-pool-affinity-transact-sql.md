---
title: sys.dm_resource_governor_external_resource_pool_affinity (Transact-SQL) Documenti Microsoft
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- sys.dm_resource_governor_external_resource_pool_affinity_TSQL
- dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity
ms.assetid: e32fac49-5161-47c0-8540-af3fe730c00c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 77d0d322139be1f1c6086622855600a7c24fc4c9
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664319"
---
# <a name="sysdm_resource_governor_external_resource_pool_affinity-transact-sql"></a>sys.dm_resource_governor_external_resource_pool_affinity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**Si applica a: ** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] e [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Restituisce informazioni sull'affinità della CPU sulla configurazione del pool di risorse esterno corrente.
  
|Nome colonna|Tipo di dati|Descrizione|
|----------------|---------------|-----------------|
|pool_id|**Int**|ID del pool di risorse esterno. Non ammette i valori Null.|
|processor_group|**Smallint**|ID del gruppo di processori logici Windows. Non ammette i valori Null.|
|cpu_mask|**Bigint**|Maschera binaria che rappresenta le CPU associate al pool. Non ammette i valori Null.|
  
## <a name="remarks"></a>Osservazioni

I pool creati con un'affinità di `AUTO` non vengono visualizzati in questa visualizzazione perché non hanno affinità. Per altre informazioni, vedere le istruzioni [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md) e ALTER EXTERNAL RESOURCE POOL &#40;istruzioni [Transact-SQL&#41;.](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione `VIEW SERVER STATE`.

## <a name="see-also"></a>Vedere anche

[Governance delle risorse per Machine Learning in SQL Server](../../machine-learning/administration/resource-governor.md)

[&#41;Transact-SQL &#40;di sys.dm_resource_governor_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[Opzione di configurazione del server external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
