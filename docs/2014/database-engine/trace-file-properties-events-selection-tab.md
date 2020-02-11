---
title: Proprietà file di traccia (scheda Selezione eventi) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracefileproperties.eventsselection.f1
helpviewer_keywords:
- Trace File Properties dialog box
ms.assetid: 158d442f-2225-4173-8545-fb1cf611b4d0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0a6c6da76bd89b4686791087e558ae1f329f57a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088795"
---
# <a name="trace-file-properties-events-selection-tab"></a>Proprietà file di traccia (scheda Selezione eventi)
  Utilizzare la scheda **Selezione eventi** della finestra di dialogo **Proprietà modello di traccia** per visualizzare le proprietà delle colonne della traccia o per eliminare colonne di dati dalla traccia.  
  
 Per visualizzare questa finestra, aprire un file di traccia Scegliere **Proprietà**dal menu **file** , quindi fare clic sulla scheda **Selezione eventi** .  
  
## <a name="options"></a>Opzioni  
 Colonna **eventi**  
 Consente di visualizzare gli eventi inseriti nella traccia organizzati per categoria. Inizialmente sono selezionati tutti gli eventi della traccia. È possibile selezionare gli eventi selezionando le rispettive caselle o colonne di dati. Se si seleziona la casella corrispondente all'evento, verranno selezionate tutte le colonne di dati disponibili per tale evento. Se si seleziona la colonna di dati corrispondente all'evento, quest'ultimo viene selezionato insieme a tutte le altre colonne necessarie. Se si sta visualizzando un file o una tabella di traccia, è possibile deselezionare le caselle di controllo relative agli eventi o alle colonne di dati per ridurre la quantità di dati visibili nella finestra di traccia, facilitandone in tal modo l'analisi. È inoltre possibile modificare i filtri colonna per ridurre la quantità di dati visibili nella finestra di traccia. Per ulteriori informazioni sulle classi degli eventi, vedere [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 Colonne di dati  
 È possibile visualizzare le colonne di dati inserite nella traccia. Tutte le colonne di dati pertinenti nella traccia sono selezionate per impostazione predefinita per ogni evento incluso nella traccia.  
  
 Per specificare i filtri, fare clic sull'intestazione della colonna di dati e immettere i criteri di filtro. Le colonne di dati filtrate sono contrassegnate da un'icona di filtro a sinistra dell'etichetta della colonna nella finestra di dialogo **Modifica filtro** .  
  
 **Mostra tutti gli eventi**  
 Consente di visualizzare tutti gli eventi disponibili. Per impostazione predefinita, vengono visualizzate solo le righe della griglia **Selezione eventi** selezionate. Deselezionare questa casella di controllo per nascondere tutti gli eventi non selezionati nella griglia **Selezione eventi** . Se la casella di controllo **Mostra tutti gli eventi** è selezionata e si sta visualizzando un file o una tabella di traccia, tutti gli eventi registrati nella traccia vengono visualizzati nella finestra di traccia.  
  
 **Mostra tutte le colonne**  
 Consente di visualizzare tutte le colonne di dati disponibili. Per impostazione predefinita, vengono visualizzate solo le colonne di dati selezionate. Deselezionare questa casella di controllo per nascondere tutte le colonne di dati non selezionate nella griglia **Selezione eventi** .  
  
 **Filtri colonne**  
 Apre la finestra di dialogo **Modifica filtro** che visualizza un'icona di filtro a sinistra delle etichette delle colonne di dati filtrate. Utilizzare la finestra di dialogo **Modifica filtro** per modificare i filtri delle colonne di dati.  
  
 **Organizza colonne**  
 Dopo avere selezionato **Eventi** e le colonne di dati da inserire nella traccia, fare clic su **Organizza colonne** per forzare il riordinamento della colonna nella finestra dei risultati della traccia.  
  
## <a name="see-also"></a>Vedere anche  
 [Specificare eventi e colonne di dati per un file di traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Filtrare gli eventi in una traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [Visualizza informazioni sui filtri &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [Modificare un filtro &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)   
 [Modelli e autorizzazioni di SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
  
  
