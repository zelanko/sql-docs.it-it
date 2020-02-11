---
title: Proprietà tabella di traccia (scheda Selezione eventi) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracetableproperties.eventsselection.f1
helpviewer_keywords:
- Trace Table Properties dialog box
ms.assetid: fa21df6a-b6b5-4b15-9104-957385821594
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 404b1d5d8467fe5840a6f53007bd55bc58cdf19f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089536"
---
# <a name="trace-table-properties-events-selection-tab"></a>Proprietà tabella di traccia (scheda Selezione eventi)
  Utilizzare la scheda **Selezione eventi** nella finestra di dialogo **Proprietà tabella di traccia** per visualizzare le proprietà degli eventi e delle colonne di dati della traccia o per rimuovere eventi e colonne.  
  
 Per visualizzare questa finestra, aprire una tabella di traccia mediante [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] , scegliere **Proprietà** dal menu **File**e quindi fare clic sulla scheda **Selezione eventi** .  
  
## <a name="options"></a>Opzioni  
 Colonna **eventi**  
 Consente di visualizzare gli eventi inseriti nella traccia organizzati per categoria. È possibile selezionare gli eventi selezionando le rispettive caselle o colonne di dati. Se si seleziona la casella corrispondente all'evento, verranno selezionate tutte le colonne di dati disponibili per tale evento. Se si seleziona la colonna di dati corrispondente all'evento, quest'ultimo viene selezionato insieme a tutte le altre colonne necessarie. Se si sta visualizzando un file o una tabella di traccia, è possibile deselezionare le caselle di controllo relative agli eventi o alle colonne di dati per ridurre la quantità di dati visibili nella finestra di traccia, facilitandone in tal modo l'analisi. È inoltre possibile modificare i filtri colonna per ridurre la quantità di dati visibili nella finestra di traccia. Per ulteriori informazioni sulle classi degli eventi, vedere [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 Altre colonne di dati  
 È possibile visualizzare le colonne di dati inserite nella traccia. Tutte le colonne di dati pertinenti nella traccia sono selezionate per impostazione predefinita per ogni evento incluso nella traccia.  
  
 Per specificare i filtri, fare clic sull'intestazione della colonna di dati e immettere i criteri di filtro. Le colonne di dati filtrate sono contrassegnate da un'icona di filtro a sinistra dell'etichetta della colonna nella finestra di dialogo **Modifica filtro** .  
  
 **Mostra tutti gli eventi**  
 Consente di visualizzare tutti gli eventi disponibili. Per impostazione predefinita, vengono visualizzate solo le righe della griglia **Selezione eventi** selezionate. Deselezionare questa casella di controllo per nascondere tutti gli eventi non selezionati nella griglia **Selezione eventi** . Se la casella di controllo **Mostra tutti gli eventi** è selezionata e si sta visualizzando un file o una tabella di traccia, tutti gli eventi registrati nella traccia vengono visualizzati nella finestra di traccia.  
  
 **Mostra tutte le colonne**  
 Consente di visualizzare tutte le colonne di dati disponibili. Per impostazione predefinita, vengono visualizzate solo le colonne di dati selezionate. Deselezionare questa casella di controllo per nascondere tutte le colonne di dati non selezionate nella griglia **Selezione eventi** .  
  
 **Filtri colonne**  
 Consente di aprire la finestra di dialogo **Modifica filtro** che visualizza un'icona di filtro a sinistra dell'etichetta di colonna. È possibile utilizzare questa finestra di dialogo per modificare i filtri delle colonne di dati.  
  
 **Organizza colonne**  
 Dopo avere selezionato **Eventi** e le colonne di dati da inserire nella traccia, fare clic su **Organizza colonne** per forzare il riordinamento della colonna nella finestra dei risultati della traccia.  
  
## <a name="see-also"></a>Vedere anche  
 [Aprire una tabella di traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [Modelli e autorizzazioni di SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
