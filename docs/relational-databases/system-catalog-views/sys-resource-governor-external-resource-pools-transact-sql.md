---
description: sys. resource_governor_external_resource_pools (Transact-SQL)
title: sys. resource_governor_external_resource_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_external_resource_pools
- sys.resource_governor_external_resource_pools_TSQL
- resource_governor_external_resource_pools
- resource_governor_external_resource_pools_TSQL
helpviewer_keywords:
- sys.resource_governor_external_resource_pools
- resource_governor_external_resource_pools
ms.assetid: 75063e36-a91b-496f-9936-88f3d57bd447
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6e75047b9f65136a4b41f248ee948555fdb526e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447863"
---
# <a name="sysresource_governor_external_resource_pools-transact-sql"></a>sys. resource_governor_external_resource_pools (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]
**Si applica a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]e [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Restituisce la configurazione del pool di risorse esterne archiviato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ogni riga della vista determina la configurazione di un pool.
  
|Nome colonna|Tipo di dati|Descrizione|
|-----------------|---------------|-----------------|
|external_pool_id|**int**|ID univoco del pool di risorse. Non ammette i valori Null.|
|name|**sysname**|Nome del pool di risorse. Non ammette i valori Null.|
|max_cpu_percent|**int**|Larghezza di banda media massima della CPU concessa per tutte le richieste nel pool di risorse, in caso di contesa di CPU. Non ammette i valori Null.|
|max_memory_percent|**int**|Percentuale di memoria totale del server utilizzabile dalle richieste in questo pool di risorse. Non ammette i valori Null. Il valore massimo effettivo dipende dai valori minimi del pool. Ad esempio, impostando max_memory_percent su 100, il valore massimo effettivo risulta inferiore.|
|max_processes|**int**|Numero massimo di processi esterni simultanei. Il valore predefinito, 0, non specifica alcun limite. Non ammette i valori Null.|
|version|**bigint**|Numero di versione interno.|
  
## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione VIEW SERVER STATE.

## <a name="see-also"></a>Vedere anche

[Governance delle risorse per Machine Learning in SQL Server](../../machine-learning/administration/resource-governor.md)

[Viste del catalogo di Resource Governor &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)

[sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)

[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)

[sys. dm_resource_governor_resource_pool_affinity &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[Opzione di configurazione del server external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
