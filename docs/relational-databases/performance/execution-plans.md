---
title: Piani di esecuzione | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- query execution plans
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753f
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 9bf75c2d176c4ea2c596f29f1ddda910e794ae12
ms.sourcegitcommit: ba7fb4b9b4f0dbfe77a7c6906a1fde574e5a8e1e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303234"
---
# <a name="execution-plans"></a>Piani di esecuzione
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Per poter eseguire le query, il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] deve analizzare l'istruzione per determinare il modo più efficiente di accedere ai dati necessari. Questa analisi viene gestita da un componente denominato Query Optimizer. I dati di input per Query Optimizer sono costituiti dalla query, dallo schema del database (definizioni di tabella e indice) e dalle statistiche del database. L'output di Query Optimizer è un piano di esecuzione della query, talvolta definito piano di query o semplicemente piano di esecuzione.   

Il piano di esecuzione di una query è costituito dalla definizione degli elementi seguenti: 

* La sequenza di accesso alle tabelle di origine.  
  In genere il server di database può utilizzare molte sequenze diverse per accedere alle tabelle di base e quindi compilare il set di risultati. Ad esempio, se un'istruzione `SELECT` fa riferimento a tre tabelle, il server di database può accedere innanzitutto a `TableA`, usare i dati di `TableA` per estrarre le righe corrispondenti da `TableB`, quindi usare i dati di `TableB` per estrarre i dati da `TableC`. Di seguito vengono indicate le altre sequenze di accesso alle tabelle utilizzabili dal server di database:  
  `TableC`, `TableB`, `TableA`o  
  `TableB`, `TableA`, `TableC`o  
  `TableB`, `TableC`, `TableA`o  
  `TableC`, `TableA`, `TableB`  

* I metodi utilizzati per estrarre i dati da ogni tabella.  
  Per accedere ai dati di ogni tabella sono in genere disponibili metodi diversi. Se sono necessarie solo alcune righe con valori di chiave specifici, il server di database può utilizzare un indice. Se sono necessarie tutte le righe della tabella, il server di database può ignorare gli indici ed eseguire un'analisi di tabella. Se sono necessarie tutte le righe di una tabella, ma l'indice contiene colonne chiave incluse in una clausola `ORDER BY`, è consigliabile eseguire l'analisi dell'indice anziché della tabella per evitare che il set di risultati venga ordinato separatamente. Se una tabella è di dimensioni molto ridotte, l'analisi della tabella può rappresentare il metodo più efficiente per quasi tutti gli accessi alla tabella.

> [!TIP]
> Per altre informazioni sull'elaborazione delle query e i piani di esecuzione delle query, vedere la [Guida sull'architettura di elaborazione delle query](../../relational-databases/query-processing-architecture-guide.md).

## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Infrastruttura di profilatura query](../../relational-databases/performance/query-profiling-infrastructure.md)  
  
-   [Visualizzare e salvare piani di esecuzione](../../relational-databases/performance/display-and-save-execution-plans.md)  
  
-   [Confrontare e analizzare i piani di esecuzione](../../relational-databases/performance/compare-and-analyze-execution-plans.md)  

-   [Guide di piano](../../relational-databases/performance/plan-guides.md)  

## <a name="see-also"></a>Vedere anche  
 [Monitoraggio e ottimizzazione delle prestazioni](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [Strumenti per il monitoraggio e l'ottimizzazione delle prestazioni](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [Guida sull'architettura di elaborazione delle query](../../relational-databases/query-processing-architecture-guide.md)    
 [Statistiche sulle query dinamiche](../../relational-databases/performance/live-query-statistics.md)     
 [Monitoraggio attività](../../relational-databases/performance-monitor/activity-monitor.md)     
 [Monitoraggio delle prestazioni tramite Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [Flag di traccia](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [Guida di riferimento a operatori Showplan logici e fisici](../../relational-databases/showplan-logical-and-physical-operators-reference.md)
