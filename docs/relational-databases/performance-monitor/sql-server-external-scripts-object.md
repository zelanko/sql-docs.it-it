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
ms.openlocfilehash: 36093a4cd91943b3db214dcb9cdeb55bda7399c7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68093514"
---
# <a name="sql-server-external-scripts-object"></a>SQL Server, oggetto External Scripts
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'oggetto **SQLServer:External Scripts** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce i contatori per il monitoraggio delle azioni associate all'esecuzione di script esterni. Per informazioni sull'esecuzione di script esterni, vedere [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
 Nella tabella seguente vengono descritti i contatori dell'oggetto **External Scripts** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
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
  
  
