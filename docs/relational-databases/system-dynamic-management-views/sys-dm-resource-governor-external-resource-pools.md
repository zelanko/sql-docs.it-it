---
description: sys. dm_resource_governor_external_resource_pools (Transact-SQL)
title: sys. dm_resource_governor_external_resource_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.technology: machine-learning-services
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pools_TSQL
- sys.dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_external_resource_pools
- sys.dm_resource_governor_external_resource_pools
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 32df69f207de0e1c604c10d58f4d28b4a3a34aa5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454856"
---
# <a name="sysdm_resource_governor_external_resource_pools-transact-sql"></a>sys. dm_resource_governor_external_resource_pools (Transact-SQL)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Restituisce informazioni sullo stato corrente del pool di risorse esterne, la configurazione corrente dei pool di risorse e le statistiche del pool di risorse. 
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
|Nome colonna      |Tipo di dati      |Descrizione|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|ID del pool di risorse. Non ammette i valori Null. |
| name|**sysname**|Nome del pool di risorse. Non ammette i valori Null. 
| pool_version|**int**|Numero di versione interno.|
| max_cpu_percent|**int**|Configurazione corrente per la larghezza di banda media massima della CPU concessa per tutte le richieste nel pool di risorse, in caso di contesa di CPU. Non ammette i valori Null. |
| max_processes|**int**|Numero massimo di processi esterni simultanei. Il valore predefinito, 0, non specifica alcun limite. Non ammette i valori Null.|
| max_memory_percent|**int**|Configurazione corrente della percentuale di memoria totale del server utilizzabile dalle richieste in questo pool di risorse. Non ammette i valori Null. |
| statistics_start_time|**datetime**|Ora di reimpostazione delle statistiche per questo pool. Non ammette i valori Null. 
| peak_memory_kb|**bigint**|Quantità massima di memoria utilizzata, in kilobyte, per il pool di risorse. Non ammette i valori Null. |
| write_io_count|**int**|Il totale degli I/O di scrittura generati dalla reimpostazione delle statistiche di Resource Governor. Non ammette i valori Null. |
| read_io_count|**int**|Il totale degli I/O di lettura generati dalla reimpostazione delle statistiche di Resource Governor. Non ammette i valori Null. |
| total_cpu_kernel_ms|**bigint**|Tempo del kernel dell'utente della CPU cumulativo, espresso in millisecondi, dalla reimpostazione delle statistiche di Resource Governor. Non ammette i valori Null. |
| total_cpu_user_ms|**bigint**|Tempo dell'utente della CPU cumulativo, espresso in millisecondi, dalla reimpostazione delle statistiche di Resource Governor. Non ammette i valori Null. |
| active_processes_count|**int**|Numero di processi esterni in esecuzione al momento della richiesta. Non ammette i valori Null. |

 
## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione `VIEW SERVER STATE`.

> [!NOTE]
> SQL Machine Learning Services 2019 per Linux non supporta la possibilità di impostare l'affinità di CPU.

## <a name="see-also"></a>Vedere anche  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
