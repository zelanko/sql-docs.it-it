---
title: "Lezione 3: uso dell'utilità del prompt dei comandi dta | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 30f27f4d-8852-4b12-ba62-57f63e496f1d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e2881a2a118306f9d567236516f05bb29ad2d60a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68186576"
---
# <a name="lesson-3-using-the-dta-command-prompt-utility"></a>Lezione 3: Uso dell'utilità del prompt dei comandi dta
  L'utilità del prompt dei comandi **dta** offre una funzionalità aggiuntiva rispetto allo strumento Ottimizzazione guidata motore di database.  
  
 È possibile utilizzare gli strumenti XML preferiti per creare file di input per l'utilità adottando XML Schema di Ottimizzazione guidata motore di database. Questo schema viene installato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed è disponibile in: C:\Programmi (x86)\Microsoft SQL Server\110\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd.  
  
 XML Schema di Ottimizzazione guidata motore di database è inoltre disponibile online nel [sito Web Microsoft](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409).  
  
 XML Schema dello strumento Ottimizzazione guidata motore di database garantisce una maggiore flessibilità per l'impostazione delle opzioni di ottimizzazione. Ad esempio, questo schema consente di eseguire analisi di simulazione. Nell'analisi di simulazione è necessario specificare un set di strutture di progettazione fisica ipotetica per il database che si desidera ottimizzare e quindi eseguire l'analisi con lo strumento Ottimizzazione guidata motore di database per verificare se questa progettazione fisica ipotetica sarà in grado di migliorare le prestazioni dell'elaborazione delle query. Questo tipo di analisi ha il vantaggio di valutare la nuova configurazione senza l'overhead dovuto all'effettiva implementazione. Se la progettazione fisica ipotetica non determina i miglioramenti nelle prestazioni desiderati, è possibile modificarla e analizzarla nuovamente con facilità fino a quando non sarà stata raggiunta la configurazione che produce i risultati richiesti.  
  
 Usando l'XML Schema dello strumento Ottimizzazione guidata motore di database e l'utilità del prompt dei comandi **dta** , è anche possibile integrare la funzionalità dello strumento Ottimizzazione guidata motore di database negli script e usarla con altri strumenti per la progettazione del database.  
  
 In questa lezione non verrà illustrata la funzionalità relativa agli input in formato XML dello strumento Ottimizzazione guidata motore di database.  
  
 Questa lezione offre un'introduzione alla sintassi di base dell'utilità del prompt dei comandi **dta** , all'accesso alla Guida e alle procedure per ottimizzare semplici carichi di lavoro.  
  
 Questa lezione contiene l'argomento seguente:  
  
-   Avvio dell'utilità del prompt dei comandi **DTA** e ottimizzazione di un carico di lavoro  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Avvio dell'utilità del prompt dei comandi dta e ottimizzazione di un carico di lavoro](lesson-1-1-tuning-a-workload.md)  
  
  
