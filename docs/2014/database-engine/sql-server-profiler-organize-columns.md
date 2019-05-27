---
title: SQL Server Profiler - organizza colonne | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.organize.columns.f1
ms.assetid: bf5674f4-da5e-43f9-aeb2-76ca37993790
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f0ad3d1204e8c27d91ecb3b586d56a27d45eeb4e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089763"
---
# <a name="sql-server-profiler---organize-columns"></a>SQL Server Profiler - Organizza colonne
  Utilizzare la finestra di dialogo **Organizza colonne** per selezionare le colonne di dati per il raggruppamento o l'aggregazione degli eventi visualizzati in una traccia, in modo da semplificare la visualizzazione e l'analisi di tabelle o di file di traccia di grandi dimensioni.  
  
 A seguito di un'operazione di aggregazione, tutti gli eventi presenti nella traccia vengono spostati e compressi in corrispondenza del rispettivo tipo di classe di evento. A sinistra del nome della classe di evento viene visualizzato un segno più (**+**). Quando si fa clic sul segno più, la classe di evento si espande ed è possibile visualizzare tutti gli eventi del tipo in questione.  
  
 A seguito di un'operazione di raggruppamento, vengono organizzate insieme tutte le classi di evento di un tipo specifico nell'area di visualizzazione della finestra di traccia. Gli eventi non vengono tuttavia compressi in corrispondenza del tipo di classe di evento.  
  
 Quando si raggruppano o aggregano gli eventi nell'area di visualizzazione della finestra di traccia, le colonne selezionate per il raggruppamento o l'aggregazione rimangono fisse nella finestra di visualizzazione, ma è possibile scorrere a destra o a sinistra per visualizzare tutte le altre colonne di dati.  
  
 Per accedere a questa finestra di dialogo, aprire una tabella o un file di traccia esistente e quindi scegliere **Proprietà** dal menu [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] **di** . Nella finestra di dialogo **Proprietà traccia** selezionare la scheda **Selezione eventi** e quindi fare clic su **Organizza colonne**. È inoltre possibile fare clic su **Organizza colonne** nella scheda **Selezione eventi** durante la creazione di una nuova traccia.  
  
## <a name="options"></a>Opzioni  
 **Gruppi**  
 Consente di spostare i nomi delle colonne di dati sotto **Gruppi** per raggruppare o aggregare le classi di evento nella finestra di traccia.  
  
 Per aggregare gli eventi, spostare una colonna di dati all'interno di **Gruppi**. In questo modo, tutti gli eventi di un tipo specifico vengono compressi in corrispondenza del nome del tipo di classe di evento nell'area di visualizzazione della finestra di traccia. A sinistra del nome della classe di evento viene visualizzato un segno più (**+**). Fare clic su questo segno per espandere il tipo di classe di evento e visualizzare tutti gli eventi. È possibile attivare e disattivare l'aggregazione e il raggruppamento scegliendo **Visualizzazione aggregata** o **Visualizzazione a gruppi** dal menu **Visualizza** .  
  
 Per raggruppare gli eventi, spostare più colonne di dati all'interno di **Gruppi**. In questo modo, tutti gli eventi di un tipo specifico vengono raggruppati insieme nell'area di visualizzazione della finestra di traccia, senza venire compressi in corrispondenza di ogni nome del tipo di classe di evento. È possibile passare dalla visualizzazione a gruppi a quella non a gruppi e viceversa scegliendo **Visualizzazione a gruppi** dal menu Visualizza. Se si spostano più colonne di dati all'interno di **Gruppi**, l'opzione che consente di passare a una **visualizzazione aggregata** non è disponibile.  
  
 **Colonne**  
 Elenco delle colonne di dati disponibili che possono essere spostate in **Gruppi**. Fare clic sul segno più (**+**) a sinistra di **Colonne** per espandere l'elenco.  
  
 **Su**  
 Dopo aver selezionato una colonna di dati, fare clic su **Su** per spostare le colonne di dati all'interno di **Gruppi**. Facendo clic su **Su** , è inoltre possibile riorganizzare la visualizzazione delle colonne nella finestra di traccia.  
  
 **Giù**  
 Dopo aver selezionato una colonna di dati, fare clic su **Giù** per spostare le colonne di dati all'esterno di **Gruppi**. Facendo clic su **Giù** , è inoltre possibile riorganizzare la visualizzazione delle colonne nella finestra di traccia.  
  
## <a name="see-also"></a>Vedere anche  
 [Organizzare le colonne visualizzate in una traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [Creare una traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [Creare un modello di traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)   
 [Aprire un file di traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [Aprire una tabella di traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
  
