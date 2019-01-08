---
title: Oggetto External Scripts di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- External Scripts object
- SQLServer:External Scripts
ms.assetid: 8a75ccce-b174-4937-bc92-8e413b55afe1
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: aae70901fe5422b035a147e11b228fb224028c08
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380028"
---
# <a name="sql-server-external-scripts-object"></a>SQL Server, oggetto External Scripts
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'oggetto **SQLServer:External Scripts** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce i contatori per il monitoraggio delle azioni associate all'esecuzione di script esterni. Per informazioni sull'esecuzione di script esterni, vedere [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
 La tabella seguente illustra i contatori **External Scripts** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contatori External Scripts di SQL Server|Descrizione|  
|------------------------------------------|-----------------|  
|**Execution Errors**|Numero di errori rilevati durante l'esecuzione di script esterni.|  
|**Accessi tramite autenticazione implicita**|Numero di accessi dai processi satellite autenticati tramite autenticazione implicita.|  
|**Parallel Executions**|Numero di script esterni eseguiti con @parallel = 1.|  
|**SQL CC Executions**|Numero di script esterni eseguiti con contesto di calcolo SQL.|  
|**Streaming Executions**|Numero di script esterni eseguiti con il parametro @r_rowsPerRead.|  
|**Total Execution Time (ms)**|Tempo totale impiegato per l'esecuzione di script esterni.|  
|**Total Executions**|Numero di script esterni eseguiti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio dell'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
