---
title: sys. dm_exec_compute_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_compute_pools
- dm_exec_compute_pools_TSQL
- dm_exec_compute_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_compute_pools dynamic management view
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d749b9a7d9689426bffafe20ee7ab46ce199ffbb
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75254608"
---
# <a name="sysdm_exec_compute_pools-transact-sql"></a>sys. dm_exec_compute_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|name|`sysname`|Nome del pool di risorse di calcolo. Non ammette i valori Null. Restituisce `default` per il pool di calcolo predefinito. |
|compute_pool_id|`int`|Identificatore univoco per il pool. Chiave per questa visualizzazione.|  
|location|`sysname`|Da endpoint a controller in un cluster SQL Big Data. Non ammette i valori Null. |

## <a name="permissions"></a>Autorizzazioni

In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]è richiesta `VIEW SERVER STATE` l'autorizzazione.

## <a name="see-also"></a>Vedere anche

[Che cosa [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)]sono ](../../big-data-cluster/big-data-cluster-overview.md)?
