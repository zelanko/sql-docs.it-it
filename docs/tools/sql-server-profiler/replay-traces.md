---
title: Riprodurre le tracce
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: da958d3c-7f3e-44c9-aecc-8a9493bea7c0
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 50ef296f7ce7198dc0e233aca08e33c5f1cf7af0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307465"
---
# <a name="replay-traces"></a>Riprodurre le tracce

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La riproduzione è la possibilità di riprodurre un'attività acquisita in una traccia. Quando si crea o si modifica una traccia, è possibile salvarla in un file per riprodurla successivamente. È possibile usare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per riprodurre l'attività di traccia da un singolo computer. In presenza di carichi di lavoro elevati, utilizzare Distributed Replay Utility per riprodurre dati di traccia da più computer.  
  
 In questa sezione viene descritto come utilizzare le caratteristiche di riproduzione di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Per altre informazioni su Distributed Replay Utility, vedere [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] include un motore di riproduzione a thread multipli in grado di simulare le connessioni utente e l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La funzionalità di riproduzione risulta utile per la risoluzione dei problemi a livello di applicazione o di processo. Dopo aver identificato il problema e implementato le correzioni adeguate, eseguire nell'applicazione o nel processo la traccia con cui è stato rilevato il possibile problema. Riprodurre quindi la traccia originale e confrontare i risultati.  
  
 La riproduzione di tracce supporta il debug eseguito tramite le opzioni **Attiva/Disattiva punto di interruzione** ed **Esegui fino al cursore** del menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]Riproduci**di**. Queste opzioni consentono in modo particolare un miglioramento dell'analisi di script lunghi. La riproduzione della traccia viene suddivisa infatti in segmenti brevi, che possono essere quindi analizzati in modo incrementale.  
  
 Per informazioni sulle autorizzazioni richieste per riprodurre tracce, vedere [Autorizzazioni necessarie per l'esecuzione di SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Requisiti per la riproduzione](../../tools/sql-server-profiler/replay-requirements.md)|Vengono descritti gli eventi che è necessario includere in una definizione di traccia perché questa possa essere riprodotta con [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Opzioni di riproduzione &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-options-sql-server-profiler.md)|Vengono descritte le opzioni disponibili nella finestra di dialogo **Configurazione riproduzione** di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Considerazioni relative alla riproduzione di tracce &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/considerations-for-replaying-traces-sql-server-profiler.md)|Vengono descritti gli eventi di traccia non riproducibili con [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e l'impatto della riproduzione di tracce sulle prestazioni del server.|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
