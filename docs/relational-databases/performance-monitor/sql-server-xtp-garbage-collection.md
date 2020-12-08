---
title: XTP Garbage Collection di SQL Server | Microsoft Docs
description: Informazioni sull'oggetto prestazione XTP Garbage Collection di SQL Server, che contiene contatori correlati al Garbage Collector del motore OLTP in memoria.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 64ae91e5-b420-44b4-af1a-f8bca83d7f41
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 48e4b2864465e095220ab238d8288c6e12639dec
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505508"
---
# <a name="sql-server-xtp-garbage-collection"></a>XTP Garbage Collection di SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  L'oggetto prestazione SQL Server XTP Garbage Collection contiene contatori correlati al Garbage Collector del motore OLTP in memoria.  
  
 La tabella descrive i contatori di **SQL Server XTP Garbage Collection** .  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|**Tentativi di analisi di elementi nascosti/sec (GC- pubblicato)**|Numero medio di tentativi di analisi dovuti a conflitti di scrittura durante le operazioni su elementi nascosti eseguite dal Garbage Collector, al secondo. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|  
|**Elementi di lavoro GC principali/sec**|Numero di elementi di lavoro elaborati dal thread GC principale.|  
|**Elemento di lavoro GC parallelo/sec**|Numero di volte in cui un thread parallelo ha eseguito un elemento di lavoro GC.|  
|**Righe elaborate/sec**|Numero medio di righe elaborate dal Garbage Collector, al secondo.|  
|**Righe elaborate/sec (innanzitutto in bucket e rimosse)**|Numero medio di righe elaborate dal Garbage Collector che erano prima nel bucket di hash corrispondente e che è stato possibile rimuovere immediatamente, al secondo.|  
|**Righe elaborate/sec (innanzitutto in bucket)**|Numero medio di righe elaborate dal Garbage Collector che erano prima nel bucket di hash corrispondente, al secondo.|  
|**Righe elaborate/sec (contrassegnate per essere scollegate)**|Numero medio di righe elaborate dal Garbage Collector che erano già contrassegnate per essere scollegate, al secondo.|  
|**Righe elaborate/sec (nessuna operazione necessaria)**|Numero medio di righe elaborate dal Garbage Collector che non richiederanno un'operazione su elementi nascosti, al secondo.|  
|**Righe scadute rimosse/sec operazioni**|Numero medio di righe scadute rimosse durante le operazioni su elementi nascosti, al secondo.|  
|**Righe scadute interessate/sec operazioni**|Numero medio di righe scadute interessate durante le operazioni su elementi nascosti, al secondo.|  
|**Righe in scadenza interessate/sec operazioni**|Numero medio di righe in scadenza interessate durante le operazioni su elementi nascosti, al secondo.|  
|**Righe interessate/sec operazioni**|Numero medio di righe interessate durante le operazioni su elementi nascosti, al secondo.|  
|**Analisi avviate/sec operazioni**|Numero medio di analisi di operazioni su elementi nascosti avviate, al secondo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Contatori delle prestazioni XTP &#40;OLTP in memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
