---
title: Memory Node di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: ed5f54ae9e24574589f880f864645a634d78e177
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380008"
---
# <a name="sql-server-memory-node"></a>SQL Server, Memory Node
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
 [Monitoraggio dell'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Oggetto di Gestione buffer di SQL Server](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
