---
title: Oggetto Buffer Node di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Buffer Node
- Buffer Node object
ms.assetid: fd3f9f0f-7c38-4cfd-a0c5-ee93dd52d9a5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 14659e4c1191e2260bccdbcd612f510770913629
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84998165"
---
# <a name="sql-serverbuffer-node"></a>Nodo SQLServer:Buffer
  L'oggetto **Buffer Node** fornisce contatori che integrano quelli inclusi nell'oggetto **Buffer Manager** . Tale oggetto consente di monitorare la distribuzione della pagina del pool di buffer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ogni nodo NUMA (Non-Uniform Memory Access). È disponibile un'istanza dell'oggetto **Buffer Node** per ogni nodo NUMA utilizzato. In un'architettura non NUMA è disponibile una singola istanza dell'oggetto **Buffer Node** .  
  
## <a name="buffer-node-performance-objects"></a>Oggetti prestazioni Buffer Node  
 Nella tabella seguente vengono descritti gli oggetti prestazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Buffer Node**di**.  
  
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
 [Oggetto di Gestione buffer di SQL Server](sql-server-buffer-manager-object.md)   
 [Opzioni di configurazione del server Server Memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [Monitoraggio dell'utilizzo delle risorse &#40;Monitor di sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
