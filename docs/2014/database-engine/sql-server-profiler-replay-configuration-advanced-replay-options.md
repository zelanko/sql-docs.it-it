---
title: SQL Server Profiler - configurazione riproduzione (opzioni avanzate di riproduzione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.generaloptions.advanced.f1
helpviewer_keywords:
- Replay Configuration dialog box
ms.assetid: b4eb34f7-3af6-4a44-ba7e-2b8430ec3cd7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0bf91032c1514037c754fd489ac266cf68063fa4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089726"
---
# <a name="sql-server-profiler---replay-configuration-advanced-replay-options"></a>SQL Server Profiler - Configurazione riproduzione (Opzioni avanzate di riproduzione)
  La scheda **Opzioni avanzate di riproduzione** della finestra di dialogo **Configurazione riproduzione** consente di specificare la modalità di riproduzione di un file di traccia.  
  
 Per visualizzare questa finestra utilizzare [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] per aprire un file o una tabella di traccia che contiene gli eventi appropriati per la riproduzione. Per altre informazioni, vedere [Requisiti per la riproduzione](../tools/sql-server-profiler/replay-requirements.md). Con la tabella o il file di traccia aperto, scegliere **Avvia** dal menu **Riproduci**, connettersi all'istanza di SQL Server in cui si vuole riprodurre la traccia e quindi fare clic sulla scheda **Opzioni avanzate di riproduzione** .  
  
## <a name="options"></a>Opzioni  
 **Riproduci SPID di sistema**  
 Consente di specificare se [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] esegue la riproduzione degli SPID (System Process Identifier).  
  
 **Riproduci un solo SPID**  
 Consente di riprodurre solo l'attività del file di traccia di origine correlata allo SPID selezionato.  
  
 **SPID da riprodurre**  
 Consente di specificare lo SPID da riprodurre.  
  
 **Limite di tempo per la riproduzione**  
 Consente di riprodurre solo una parte del file di traccia di origine.  
  
 **Ora inizio**  
 Data e ora nel file di traccia di origine in corrispondenza delle quali deve iniziare la riproduzione.  
  
 **Ora fine**  
 Data e ora nel file di traccia di origine in corrispondenza delle quali deve essere arrestata la riproduzione.  
  
 **Intervallo di attesa Health Monitor (sec)**  
 Consente di specificare l'intervallo di attesa in secondi per la riproduzione. Il valore predefinito è 3600 secondi (1 ora). Questa impostazione influisce sulla quantità di tempo durante la quale è consentita l'esecuzione di un processo prima che venga terminato da Health Monitor.  
  
 **Intervallo di polling Health Monitor (sec)**  
 Consente di specificare l'intervallo di polling in secondi di Health Monitor durante la riproduzione. Il valore predefinito è 60 secondi. Questo valore consente di configurare la frequenza con cui Health Monitor esegue il polling di candidati per la terminazione.  
  
 **Abilita monitoraggio processi bloccati di SQL Server**  
 Consente di abilitare un processo che esegue la ricerca di processi bloccati e di blocco.  
  
 **Intervallo di attesa monitoraggio processi bloccati (sec)**  
 Consente di configurare la frequenza con cui i processi bloccati o di blocco vengono cercati tramite il monitoraggio dei processi bloccati.  
  
## <a name="see-also"></a>Vedere anche  
 [Riprodurre una tabella di traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [Riprodurre un file di traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [Riprodurre le tracce](../tools/sql-server-profiler/replay-traces.md)  
  
  
