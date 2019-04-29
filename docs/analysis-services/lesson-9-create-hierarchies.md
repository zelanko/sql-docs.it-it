---
title: 'Lezione 9: Creare gerarchie | Microsoft Docs'
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: da8f3d0fb3f733c5a9307d633025bb67a1a4d8cb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63017282"
---
# <a name="lesson-9-create-hierarchies"></a>Lezione 9: Creare gerarchie
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In questa lezione si procederà alla creazione di gerarchie. Le gerarchie sono gruppi di colonne disposti in livelli. Una gerarchia Geografia potrebbe ad esempio includere i sottolivelli Paese, Stato, Regione e Città. Le gerarchie possono essere visualizzate separatamente rispetto alle altre colonne in un elenco di campi di un'applicazione client di creazione di report, per semplificarne l'esplorazione e l'inserimento in un report da parte degli utenti client. Per altre informazioni, vedere [gerarchie](../analysis-services/tabular-models/hierarchies-ssas-tabular.md).  
  
Per creare gerarchie, si userà Progettazione modelli in *vista diagramma*. Creazione e la gestione delle gerarchie non è supportata in vista dati.  
  
Tempo stimato per il completamento della lezione: **20 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 8: Creare prospettive](../analysis-services/lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Creare gerarchie  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>Per creare una gerarchia Category nella tabella DimProduct  
  
1.  In Progettazione modelli (vista diagramma) fare doppio clic il **DimProduct** tabella > **crea gerarchia**. Verrà visualizzata una nuova gerarchia nella parte inferiore della finestra della tabella. Rinominare la gerarchia **categoria**.  
  
2.  Fare clic e trascinare il **ProductCategoryName** nella nuova colonna **categoria** gerarchia.  
  
3.  Nel **categoria** gerarchia, fare doppio clic sui **ProductCategoryName** > **rinominare**, quindi digitare **categoria**.  
  
    > [!NOTE]  
    > La ridenominazione di una colonna in una gerarchia non comporta la ridenominazione della colonna nella tabella. Una colonna in una gerarchia è solo una rappresentazione della colonna nella tabella.  
  
4.  Fare clic e trascinare il **ProductSubcategoryName** colonna il **categoria** gerarchia. Rinominarlo **Subcategory**. 
  
5.  Fare doppio clic il **ModelName** colonna > **Aggiungi a gerarchia**, quindi selezionare **categoria**. Eseguire la stessa operazione per **EnglishProductName**. Rinominare queste colonne nella gerarchia **Model** e **prodotto**.  

    ![as-tabular-lesson9-category](../analysis-services/media/as-tabular-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>Per creare gerarchie nella tabella DimDate  
  
1.  Nel **DimDate** tabella, creare una nuova gerarchia denominata **calendario**.  
  
3.  Aggiungere le colonne seguenti nell'ordine:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  Nel **DimDate** tabella, creare un **fiscale** gerarchia. Includere le colonne seguenti:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Infine, nella **DimDate** tabella, creare un **ProductionCalendar** gerarchia. Includere le colonne seguenti:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>Quali sono le operazioni successive?
Passare alla lezione successiva: [Lezione 10: Creare partizioni](../analysis-services/lesson-10-create-partitions.md). 
  
  
