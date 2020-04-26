---
title: Specificare eventi e colonne di dati per un file di traccia (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- adding events
- traces [SQL Server], data columns
- deleting events
- removing events
- traces [SQL Server], events
ms.assetid: 7da715a3-2f03-4063-b6a4-20fd7b44e675
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 33e11dde29a9f2b016f5f70fa3c12bd728928f93
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63267422"
---
# <a name="specify-events-and-data-columns-for-a-trace-file-sql-server-profiler"></a>Specificare eventi e colonne di dati per un file di traccia (SQL Server Profiler)
  In questo argomento viene descritto come specificare le classi degli eventi e le colonne di dati per le tracce utilizzando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-specify-events-and-data-columns-for-a-trace"></a>Per specificare eventi e colonne di dati per una traccia  
  
1.  Nella finestra di dialogo **Proprietà traccia** o **Proprietà modello di traccia** fare clic sulla scheda **Selezione eventi** .  
  
     La scheda **Selezione eventi** contiene un controllo griglia, ovvero una tabella che include tutte le classi di evento tracciabili. La tabella contiene una riga per ogni classe di evento. Le classi di evento possono differire leggermente a seconda del tipo e della versione del server cui si è connessi. Le classi di eventi sono identificate nella colonna **Eventi**della griglia e sono raggruppate per categoria di eventi. Nelle altre colonne sono elencate le colonne di dati che possono essere restituite per ogni classe di evento.  
  
2.  Nella scheda **Selezione eventi**usare il controllo griglia per aggiungere o rimuovere eventi e colonne di dati dal file di traccia.  
  
3.  Per rimuovere eventi dalla traccia, deselezionare la casella di controllo nella colonna **Eventi** relativa a ogni classe di evento.  
  
4.  Per includere eventi in una traccia, selezionare la casella nella colonna **Eventi** per ogni classe di evento oppure selezionare una colonna di dati corrispondente a un evento.  
  
> [!IMPORTANT]  
>  Se la traccia verrà correlata ai dati di Monitoraggio di sistema o di Performance Monitor, è necessario includere nella traccia le colonne di dati **Ora di inizio** e **Ora di fine** .  
  
 Quando si include una classe di evento, nella traccia vengono inserite tutte le colonne di dati associate se è stata selezionata la casella corrispondente a un evento. Se è stata selezionata la casella per una colonna specifica, nella traccia verrà inclusa solo tale colonna.  
  
1.  Per rimuovere colonne di dati da una classe di evento, deselezionare le caselle di controllo della colonna di dati nella riga della classe oppure fare clic con il pulsante destro del mouse sull'intestazione della colonna e selezionare l'opzione **Deseleziona colonna** .  
  
2.  Applicare facoltativamente filtri alla traccia. Per altre informazioni, vedere [Filtrare eventi in una traccia &#40;SQL Server Profiler&#41;](filter-events-in-a-trace-sql-server-profiler.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
