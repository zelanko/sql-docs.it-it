---
title: XTP Databases di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQL Server 2016 XTP Databases
ms.assetid: 488ff55e-173f-43f6-9bdb-67b35e7cebfe
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e9a1160c858b85907c0a351584f4d45ad783cb00
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158949"
---
# <a name="sql-server-xtp-databases"></a>SQL Server XTP Databases
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

L'oggetto prestazione **SQL Server XTP Databases** fornisce contatori specifici del database OLTP in memoria.

> [!NOTE]
>  I contatori di SQL Server XTP Databases non sono attualmente visibili da sys.dm_os_performance_counters.  I contatori possono essere visualizzati da [Monitor di sistema](../../relational-databases/performance/start-system-monitor-windows.md).

Questa tabella descrive i contatori di **SQL Server XTP Databases** .

|Contatore|Descrizione| 
|-------------|-----------------|  
|**Dimensioni medie dei dati di grandi dimensioni del segmento transazione**|Dimensioni medie del payload di dati di grandi dimensioni del segmento transazione. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Dimensioni medie del segmento transazione**|Dimensioni medie del payload del segmento transazione. Se questo valore si avvicina allo zero, verranno allocate più pagine dall'allocatore di back-end. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Profondità coda thread di scaricamento 256K**|Profondità della coda di thread di scaricamento per richieste I/O di 256K.|
|**Profondità coda thread di scaricamento 4K**|Profondità della coda di thread di scaricamento per richieste I/O di 4K.|
|**Profondità coda thread di scaricamento 64K**|Profondità della coda di thread di scaricamento per richieste I/O di 64K.|
|**IO bloccati thread di scaricamento/sec (256K)**|Numero di richieste I/O di 256K rilevate durante l'elaborazione delle pagine scaricate superiore alla soglia di blocco e che pertanto non possono essere inviate.|
|**IO bloccati thread di scaricamento/sec (4K)**|Numero di richieste I/O di 4K rilevate durante l'elaborazione delle pagine scaricate superiore alla soglia di blocco e che pertanto non possono essere inviate.|
|**IO bloccati thread di scaricamento/sec (64K)**|Numero di richieste I/O di 64K rilevate durante l'elaborazione delle pagine scaricate superiore alla soglia di blocco e che pertanto non possono essere inviate.|
|**Conteggio elenco disponibilità IoPagePool256K**|Numero di pagine nell'elenco di disponibilità del pool di pagine I/O da 256K. Se questo valore si avvicina allo zero, verranno allocate più pagine dall'allocatore di back-end. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Totale allocato IoPagePool256K**|Numero totale di pagine allocate e mantenute dal pool di pagine I/O da 256K dall'allocatore di back-end. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Conteggio elenco disponibilità IoPagePool4K**|Numero di pagine nell'elenco di disponibilità del pool di pagine I/O da 4K. Se questo valore si avvicina allo zero, verranno allocate più pagine dall'allocatore di back-end. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Totale allocato IoPagePool4K**|Numero totale di pagine allocate e mantenute dal pool di pagine I/O da 4K dall'allocatore di back-end. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Conteggio elenco disponibilità IoPagePool64K**|Numero di pagine nell'elenco di disponibilità del pool di pagine I/O da 64K. Se questo valore si avvicina allo zero, verranno allocate più pagine dall'allocatore di back-end. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Totale allocato IoPagePool64K**|Numero totale di pagine allocate e mantenute dal pool di pagine I/O da 64K dall'allocatore di back-end. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Conteggio espansioni MtLog 256K**|Numero di volte in cui un MtLog di 256K viene espanso. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**IO MtLog 256K in sospeso**|Numero di richieste I/O da 256K in sospeso inviate da MtLog.|
|**Percentuale di riempimento pagina MtLog 256K/pagina scaricata**|Percentuale media di riempimento di ogni pagina MtLog di 256K scaricata. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Byte scritti MtLog 256K/sec**|Byte scritti al secondo in oggetti MtLog di 256K. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Conteggio espansioni MtLog 4K**|Numero di volte in cui un MtLog di 4K viene espanso. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**IO MtLog 4K in sospeso**|Numero di richieste I/O da 4K in sospeso inviate da MtLog.|
|**Percentuale di riempimento pagina MtLog 4K/pagina scaricata**|Percentuale media di riempimento di ogni pagina MtLog di 4K scaricata. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Byte scritti MtLog 4K/sec**|Byte scritti al secondo in oggetti MtLog di 4K. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Conteggio espansioni MtLog 64K**|Numero di volte in cui un MtLog di 64K viene espanso. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**IO MtLog 64K in sospeso**|Numero di richieste I/O da 64K in sospeso inviate da MtLog.|
|**Percentuale di riempimento pagina MtLog 64K/pagina scaricata**|Percentuale media di riempimento di ogni pagina MtLog di 64K scaricata. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Byte scritti MtLog 64K/sec**|Byte scritti al secondo in oggetti MtLog di 64K. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Numero di unioni**|Numero di unioni in elaborazione.|
|**Numero di unioni/sec**|Numero medio di unioni create al secondo.|
|**Numero di serializzazioni**|Numero di serializzazioni in elaborazione.|
|**Numero di serializzazioni/sec**|Numero medio di serializzazioni create al secondo.|
|**Conteggio pagine cache finale**|Numero di pagine allocate nella cache finale. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|
|**Conteggio massimo pagine cache finale**|Numero massimo di pagine allocate nella cache finale. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|


## <a name="see-also"></a>Vedere anche  
[Contatori delle prestazioni XTP &#40;OLTP in memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)
