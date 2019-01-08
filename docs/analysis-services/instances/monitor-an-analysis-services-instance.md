---
title: Monitorare una panoramica di istanza di Analysis Services | Microsoft Docs
ms.date: 11/16/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ac0f94b7f12cdba6237b2694114580f56dc6597
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540463"
---
# <a name="monitoring-overview"></a>Panoramica del monitoraggio
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services include numerosi strumenti che consentono di monitorare ed e ottimizzare le prestazioni dei server. La scelta dello strumento dipende dal tipo di monitoraggio o di ottimizzazione da eseguire e dagli eventi specifici da monitorare.

Per altre informazioni sul monitoraggio di SQL Server Analysis Services, vedere la [Guida operativa di SQL Server 2008 R2](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
## <a name="monitoring-tools"></a>Strumenti di monitoraggio  

|Strumento  |Descrizione  |
|---------|---------|
|[SQL Server Profiler](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)      |   Tiene traccia degli eventi di processo del motore. Acquisisce anche i dati relativi a tali eventi, che consente di monitorare l'attività del server e database.      |
| [Eventi estesi](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)     |   Una traccia leggero delle prestazioni e monitoraggio di sistema che usa un numero molto ridotto le risorse di sistema, rendendolo uno strumento ideale per la diagnosi dei problemi nei server di produzione e test.       |
| [Viste a gestione dinamica &#40;viste a gestione dinamica&#41;](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)      |   Query che restituiscono informazioni relative agli oggetti del modello, le operazioni server e lo stato del server. La query, basata su SQL, è un'interfaccia al set di righe dello schema.      |
| [Eventi di traccia](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)     |  Seguire l'attività di un'istanza di acquisizione e analizzando gli eventi di traccia generati dall'istanza. Gli eventi di traccia vengono raggruppati in modo da trovare più facilmente gli eventi di traccia correlati.        |
|   [Contatori delle prestazioni](../../analysis-services/instances/performance-counters-ssas.md)\*    |    Con Performance Monitor è possibile monitorare le prestazioni di un'istanza di Microsoft SQL Server Analysis Services (SSAS) tramite i contatori delle prestazioni.     |
|[Log operazioni](../../analysis-services/instances/performance-counters-ssas.md)\*|Un'istanza di SQL Server Analysis Services registrerà le notifiche di server, errori e avvisi per il file msmdsrv log: uno per ogni istanza installata. |

\* Si applica a SQL Server Analysis Services solo.

## <a name="see-also"></a>Vedere anche

[Monitorare le metriche dei server Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-monitor)   
[Configurare la registrazione diagnostica per Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-logging)
