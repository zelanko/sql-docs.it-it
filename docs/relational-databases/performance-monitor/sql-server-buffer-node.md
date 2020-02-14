---
title: Oggetto Buffer Node di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Buffer Node
- Buffer Node object
ms.assetid: fd3f9f0f-7c38-4cfd-a0c5-ee93dd52d9a5
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 9011394dccf472499c1c8a8bd1023b7c23009883
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "67987218"
---
# <a name="sql-serverbuffer-node"></a>Nodo SQLServer:Buffer
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  L'oggetto **Buffer Node** fornisce contatori che integrano quelli inclusi nell'oggetto **Buffer Manager** . Tale oggetto consente di monitorare la distribuzione della pagina del pool di buffer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ogni nodo NUMA (Non-Uniform Memory Access). È disponibile un'istanza dell'oggetto **Buffer Node** per ogni nodo NUMA utilizzato. In un'architettura non NUMA è disponibile una singola istanza dell'oggetto **Buffer Node** .  
  
## <a name="buffer-node-performance-objects"></a>Oggetti prestazioni Buffer Node  
 Nella tabella seguente vengono descritti gli oggetti prestazioni **Buffer Node** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contatori Buffer Node di SQL Server|Descrizione|  
|-------------------------------------|-----------------|  
|**Pagine di database**|Indica il numero di pagine con contenuto di database nel pool di buffer nel nodo.|  
|**Permanenza presunta delle pagine**|Indica il numero minimo di secondi in cui una pagina viene mantenuta nel pool di buffer nel nodo senza riferimenti.|  
|**Ricerche di pagina nodo locale/sec**|Indica il numero di richieste di ricerca dal nodo soddisfatte dal nodo stesso.|  
|**Ricerche di pagina nodo remoto/sec**|Indica il numero di richieste di ricerca dal nodo soddisfatte da altri nodi.|  
  
 Se SQL Server viene eseguito in componenti hardware non NUMA, i contatori degli oggetti **Buffer Node** e **Buffer Manager** devono corrispondere.  
  
 In componenti hardware NUMA le somme dei rispettivi contatori di tutti gli oggetti **Buffer Node** devono corrispondere alle relative controparti di **Buffer Manager**.  
  
> [!NOTE]  
>  I valori dei contatori e le somme potrebbero non corrispondere esattamente a causa della natura dinamica dei contatori e dell'accuratezza del campionamento.  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto di Gestione buffer di SQL Server](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [Opzioni di configurazione del server Server Memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [Monitoraggio dell'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
