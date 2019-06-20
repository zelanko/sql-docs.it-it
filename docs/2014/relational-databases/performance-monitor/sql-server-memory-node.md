---
title: Memory Node di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 32a2296fdb68e640ce8ebfc8dd9cdb351666b337
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63250575"
---
# <a name="sql-server-memory-node"></a>SQL Server, Memory Node
  L'oggetto **Memory Node** di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce contatori per il monitoraggio dell'utilizzo della memoria del server in nodi NUMA.  
  
## <a name="memory-node-counters"></a>Contatori Memory Node  
 Nella tabella seguente vengono descritti i contatori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Memory Node** .  
  
|Contatori Memory Manager di SQL Server|Descrizione|  
|----------------------------------------|-----------------|  
|**Memoria nodo database (KB)**|Specifica la quantità di memoria utilizzata dal server nel nodo per le pagine del database.|  
|**Memoria nodo disponibile (KB)**|Specifica la quantità di memoria non utilizzata dal server nel nodo.|  
|**Memoria nodo esterna (KB)**|Specifica la quantità di memoria non locale NUMA nel nodo.|  
|**Memoria nodo prelevata (KB)**|Specifica la quantità di memoria utilizzata dal server nel nodo per scopi diversi dalle pagine del database.|  
|**Memoria nodo di destinazione**|Specifica la quantità di memoria ideale per il nodo.|  
|**Memoria nodo totale**|Indica la quantità totale di memoria riservata dal server nel nodo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio dell'utilizzo delle risorse &#40;Monitor di sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [Oggetto di Gestione buffer di SQL Server](sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
