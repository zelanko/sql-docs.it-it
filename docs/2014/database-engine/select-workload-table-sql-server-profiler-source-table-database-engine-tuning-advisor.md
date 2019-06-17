---
title: SQL Server Profiler - origine tabella-Ottimizzazione guidata motore Database - Seleziona tabella carico di lavoro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.tools.sourcetable.f1
helpviewer_keywords:
- Select Workload Table dialog box
- Source Table dialog box
ms.assetid: 51185be7-7092-480a-a52c-cf7786c4a0a0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 973680d07c3bd6a304e63f4b3fde0e228f0f7bff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088875"
---
# <a name="sql-server-profiler---source-table-database-engine-tuning-advisor---select-workload-table"></a>Tabella di SQL Server Profiler - origine tabella-Ottimizzazione guidata motore Database - selezionare il carico di lavoro
  Questa finestra di dialogo viene usata in Microsoft [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] e in Ottimizzazione guidata [!INCLUDE[ssDE](../includes/ssde-md.md)] per selezionare tabelle.  
  
 In [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], usare la finestra di dialogo **Tabella di origine** per specificare una tabella di origine per una tabella di traccia. Si tratta di una tabella dalla quale viene caricata una traccia e il cui contenuto viene visualizzato o utilizzato per riprodurre la traccia.  
  
 In Ottimizzazione guidata [!INCLUDE[ssDE](../includes/ssde-md.md)], usare la finestra di dialogo **Seleziona tabella carico di lavoro** per selezionare una tabella di database contenente informazioni di traccia di [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] da usare come carico di lavoro per l'ottimizzazione o per visualizzare un'anteprima del contenuto della tabella prima di avviare l'analisi per l'ottimizzazione.  
  
## <a name="options"></a>Opzioni  
 **SQL Server**  
 Indica l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a cui si è attualmente connessi. Questo campo viene popolato automaticamente e non è possibile aggiornarlo.  
  
 **Database**  
 Consente di specificare il database che include la tabella di traccia.  
  
 **Proprietario**  
 Indica il proprietario della tabella di traccia. Questo campo viene popolato automaticamente con il valore **dbo**.  
  
 **Tabella**  
 Consente di specificare il nome della tabella di traccia dalla quale leggere la traccia.  
  
## <a name="see-also"></a>Vedere anche  
 [Salvare i risultati della traccia in una tabella &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)   
 [Modelli e autorizzazioni di SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [Database Engine Tuning Advisor](../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
