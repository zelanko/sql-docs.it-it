---
description: sys. dm_exec_compute_pools (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: bb084b65a4b4e850b5e1966ceb2354d18a0ac095
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447610"
---
# <a name="sysdm_exec_compute_pools-transact-sql"></a>sys. dm_exec_compute_pools (Transact-SQL)
[!INCLUDE[sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|name|`sysname`|Nome del pool di risorse di calcolo. Non ammette i valori Null. Restituisce `default` per il pool di calcolo predefinito. |
|compute_pool_id|`int`|Identificatore univoco per il pool. Chiave per questa visualizzazione.|  
|posizione|`sysname`|Da endpoint a controller in un cluster SQL Big Data. Non ammette i valori Null. |

## <a name="permissions"></a>Autorizzazioni

In è [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] richiesta l' `VIEW SERVER STATE` autorizzazione.

## <a name="see-also"></a>Vedere anche

[Che cosa [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] sono ](../../big-data-cluster/big-data-cluster-overview.md)?
