---
title: Oggetto Latches di SQL Server | Microsoft Docs
description: Informazioni sull'oggetto SQLServer:Latches, che fornisce contatori per monitorare i blocchi di risorsa interni di SQL Server, definiti latch.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Latches object
- SQLServer:Latches
ms.assetid: 2393ea1c-2bf3-41c3-9f37-b9761144eeca
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: d57998b2bbc83a231cd82ceef8846ef21902eccb
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458813"
---
# <a name="sql-server-latches-object"></a>Oggetto Latch di SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  L'oggetto **SQLServer:Latch** in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce contatori per monitorare i blocchi di risorsa interni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , definiti latch. Il monitoraggio dei latch per determinare l'attività degli utenti e l'utilizzo delle risorse può essere utile per identificare eventuali colli di bottiglia.  
  
 Nella tabella seguente vengono descritti i contatori dell'oggetto **Latches** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contatori di SQLServer:Latch|Descrizione|  
|---------------------------------|-----------------|  
|**Tempo medio di attesa latch (ms)**|Tempo medio di attesa di latch da parte delle richieste di latch (in millisecondi).|  
|**Base tempo medio attesa latch**|Solo per uso interno.| 
|**Attese latch/sec**|Numero di richieste di latch non soddisfatte immediatamente.|  
|**Numero di SuperLatch**|Numero di latch utilizzati attualmente come SuperLatch.|  
|**Abbassamenti di livello SuperLatch/sec**|Numero di SuperLatch abbassati al livello di latch normali nell'ultimo secondo.|  
|**Promozioni a SuperLatch/sec**|Numero di latch promossi a SuperLatch nell'ultimo secondo.|  
|**Tempo totale di attesa latch (ms)**|Tempo totale di attesa di latch da parte delle richieste di latch nell'ultimo secondo (in millisecondi).|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
