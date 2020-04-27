---
title: Creare tracce del profiler per la riproduzione (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- replaying queries
- replaying discovers
- events [Analysis Services]
- replaying commands
- Profiler [SQL Server Profiler], Analysis Services
- performance [Analysis Services], replays
- traces [Analysis Services]
ms.assetid: 93b2fc46-7cfb-4ab5-abeb-1475a7d6f0f2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc494fa63064d5c48c94e44cb91db5b1fe0f988d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080139"
---
# <a name="create-profiler-traces-for-replay-analysis-services"></a>Creare tracce del profiler per la riproduzione (Analysis Services)
  Per riprodurre query, individuazioni e comandi [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]inviati dagli utenti a, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] è necessario che raccolga gli eventi richiesti. Per avviare la raccolta di questi eventi, è necessario selezionare opportune classi di evento nella scheda **Selezione eventi** della finestra di dialogo **Proprietà traccia** . Se ad esempio viene selezionata la classe di evento Query Begin, verranno raccolti gli eventi contenenti query e questi eventi verranno utilizzati per la riproduzione. In questo caso il file di traccia conterrà informazioni sufficienti a supportare la riproduzione di transazioni di server nella sequenza originale e in un ambiente distribuito.  
  
## <a name="replay-for-queries"></a>Riproduzione di query  
 Per la riproduzione di query, è necessario che in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] vengano acquisiti gli eventi seguenti:  
  
-   Classe di evento Audit Login con tutte le colonne di dati. Questa classe di evento contiene informazioni sugli utenti connessi e sulle impostazioni della sessione. L'ID di processo server (SPID) contiene il riferimento alla sessione utente. Per altre informazioni, vedere [Colonne di dati degli eventi di controllo di sicurezza](https://docs.microsoft.com/bi-reference/trace-events/security-audit-data-columns).  
  
-   Classe di evento Query Begin con tutte le colonne di dati. Questa classe di evento contiene le informazioni sulla query inviata a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La colonna Event Subclass contiene informazioni sul tipo di query. La colonna TextData contiene il testo effettivo della query. La colonna RequestParameters contiene i parametri per le query con parametri, mentre la colonna RequestProperties contiene le proprietà di una richiesta XMLA (XML for Analysis). Per altre informazioni, vedere [Colonne di dati degli eventi di query](https://docs.microsoft.com/bi-reference/trace-events/queries-events-data-columns).  
  
-   Classe di evento Query End con tutte le colonne di dati. Questa classe di evento verifica lo stato di esecuzione della query. Per altre informazioni, vedere [Colonne di dati degli eventi di query](https://docs.microsoft.com/bi-reference/trace-events/queries-events-data-columns).  
  
## <a name="replay-for-discovers"></a>Riproduzione di richieste di individuazione  
 Per la riproduzione di richieste di individuazione, è necessario che in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] vengano acquisiti gli eventi seguenti:  
  
-   Classe di evento Audit Login con tutte le colonne di dati. Questa classe di evento contiene informazioni sugli utenti connessi e sulle impostazioni della sessione. L'ID di processo server (SPID) contiene il riferimento alla sessione utente. Per altre informazioni, vedere [Colonne di dati degli eventi di controllo di sicurezza](https://docs.microsoft.com/bi-reference/trace-events/security-audit-data-columns).  
  
-   Classe di evento Discover Begin con tutte le colonne di dati. La colonna TextData fornisce il \<RequestType> parte della richiesta Discover e la colonna RequestProperties fornisce le \<proprietà> parte della richiesta di individuazione. La colonna EventSubclass contiene il tipo di richiesta di individuazione. Per altre informazioni, vedere [Colonne di dati degli eventi di individuazione](https://docs.microsoft.com/bi-reference/trace-events/discover-events-data-columns).  
  
-   Classe di evento Discover End con tutte le colonne di dati. Questa classe di evento verifica lo stato della richiesta di individuazione. Per altre informazioni, vedere [Colonne di dati degli eventi di individuazione](https://docs.microsoft.com/bi-reference/trace-events/discover-events-data-columns).  
  
## <a name="replay-for-commands"></a>Riproduzione di comandi  
 Per la riproduzione di comandi, è necessario che in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] vengano acquisiti gli eventi seguenti:  
  
-   Classe di evento Command Begin con tutte le colonne di dati. La colonna TextData fornisce informazioni dettagliate sul comando, ad esempio il tipo di processo, l'ID database e l'ID cubo. La colonna RequestParameters contiene i parametri per i comandi con parametri, mentre la colonna RequestProperties contiene le proprietà di una richiesta XMLA. Per altre informazioni, vedere [Colonne di dati degli eventi di comando](https://docs.microsoft.com/bi-reference/trace-events/command-events-data-columns).  
  
-   Classe di evento Command End con tutte le colonne di dati. Questa classe di evento verifica lo stato del comando. Per altre informazioni, vedere [Colonne di dati degli eventi di comando](https://docs.microsoft.com/bi-reference/trace-events/command-events-data-columns).  
  
## <a name="see-also"></a>Vedi anche  
 [Eventi di traccia Analysis Services](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)   
 [Introduzione al monitoraggio di Analysis Services tramite SQL Server Profiler](introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)  
  
  
