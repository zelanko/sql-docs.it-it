---
title: Usare SQL Server Profiler per monitorare Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 190ae82b43f7a4f311d358ea9597a10cd5cc39dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68181225"
---
# <a name="use-sql-server-profiler-to-monitor-analysis-services"></a>Usare SQL Server Profiler per il monitoraggio di Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] consente di tenere traccia degli eventi di elaborazione del motore, ad esempio l'avvio di un batch o di una transazione, e di acquisire i dati relativi a tali eventi consentendo in questo modo di monitorare l'attività del server e del database, ad esempio query utente o attività di accesso. È possibile acquisire i dati di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] in un file o in una tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per poterli analizzare in seguito, nonché riprodurre gli eventi acquisiti nella stessa istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o in un'istanza diversa per analizzare in modo approfondito cosa sia avvenuto. È possibile riprodurre gli eventi in tempo reale oppure in fasi successive. Risulta inoltre particolarmente utile far eseguire gli eventi di traccia assieme ai contatori delle prestazioni nello stesso computer. SQL Profiler è in grado di correlare gli eventi di traccia e i contatori delle prestazioni in base all'orario e visualizzarli insieme in un'unica cronologia. Gli eventi di traccia restituiscono un maggior numero di dettagli mentre i contatori delle prestazioni offrono una vista aggregata. Per informazioni su come creare ed eseguire tracce, vedere [Creare tracce del profiler per la riproduzione &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md).  
  
 Gli argomenti disponibili in questa sezione sono descritti nella tabella seguente.  
  
## <a name="in-this-section"></a>In questa sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Introduzione al monitoraggio di Analysis Services tramite SQL Server Profiler](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)|Descrive l'utilizzo di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per il monitoraggio di un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Creare tracce del profiler per la riproduzione &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)|Descrive i requisiti per la creazione di una traccia per la riproduzione tramite [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Eventi di traccia di Analysis Services](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)|Descrive le classi di evento di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Queste classi di evento eseguono il mapping ad azioni generate da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e vengono utilizzate per le riproduzioni delle tracce.|  
  

  
  
