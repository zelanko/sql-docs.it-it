---
title: Proprietà modello (scheda Selezione eventi) di traccia | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracetemplateproperties.eventsselection.f1
helpviewer_keywords:
- Trace Template Properties dialog box
ms.assetid: 5b202457-ab42-4902-8012-7f3f40aa09f5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ac74d361758cda8ec0b345b93e542d96c709e586
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773457"
---
# <a name="trace-template-properties-events-selection-tab"></a>Proprietà modello di traccia (scheda Selezione eventi)
  Utilizzare la scheda **Selezione eventi** della finestra di dialogo **Proprietà modello di traccia** per visualizzare, modificare o specificare classi di evento e colonne di dati da includere in un modello di traccia di [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] .  
  
## <a name="options"></a>Opzioni  
 Colonna**Eventi**   
 Consente di specificare gli eventi che devono essere inseriti nella traccia selezionando o deselezionando la casella di controllo nella colonna di evento. Gli eventi sono organizzati in base alla categoria.  
  
 Se è stato selezionato **Basa il nuovo modello sul seguente modello esistente** nella scheda **Generale** , gli eventi vengono selezionati automaticamente in base al modello indicato. Per ulteriori informazioni sulle classi degli eventi, vedere [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 Colonne di dati  
 Consente di specificare le colonne di dati che devono essere inserite nella traccia selezionando la casella corrispondente all'evento e alla colonna di dati necessari. Per ogni evento incluso nella traccia, se la casella di controllo corrispondente all'evento è selezionata, per impostazione predefinita vengono selezionate tutte le relative colonne di dati. Se è stato selezionato **Basa il nuovo modello sul seguente modello esistente** nella scheda **Generale** , le colonne di dati e i filtri vengono selezionati automaticamente in base al modello indicato.  
  
 Per specificare i filtri, fare clic sull'intestazione della colonna di dati e immettere i criteri di filtro. Le colonne di dati filtrate sono contrassegnate da un'icona di filtro a sinistra dell'etichetta della colonna nella finestra di dialogo **Modifica filtro** .  
  
 **Mostra tutti gli eventi**  
 Consente di visualizzare tutti gli eventi disponibili. Se si sta creando un nuovo modello non basato su uno esistente, questa opzione è selezionata per impostazione predefinita. Deselezionare questa casella di controllo per nascondere tutti gli eventi non selezionati nella griglia **Selezione eventi** .  
  
 **Mostra tutte le colonne**  
 Consente di visualizzare tutte le colonne di dati disponibili. Se si sta creando un nuovo modello non basato su uno esistente, questa opzione è selezionata per impostazione predefinita. Deselezionare questa casella di controllo per nascondere tutte le colonne di dati non selezionate nella griglia **Selezione eventi** .  
  
 **Filtri colonne**  
 Consente di aprire la finestra di dialogo **Modifica filtro** , che visualizza un'icona di filtro a sinistra dell'etichetta della colonna di dati. Utilizzare la finestra di dialogo **Modifica filtro** per modificare i filtri delle colonne di dati.  
  
 **Organizza colonne**  
 Consente di modificare l'ordine delle colonne nella traccia e di raggruppare i risultati in base a una o più colonne.  
  
## <a name="see-also"></a>Vedere anche  
 [Specificare eventi e colonne di dati per un file di traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Organizzare le colonne visualizzate in una traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [Filtrare gli eventi in una traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [Visualizzare informazioni sui filtri &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [Modificare un filtro &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [Modelli e autorizzazioni di SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
