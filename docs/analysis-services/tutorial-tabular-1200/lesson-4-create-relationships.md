---
title: 'Lezione 4: Creare relazioni | Microsoft Docs'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8cad8c81021587a9dc3742983d7c7c2cd80fc174
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65404853"
---
# <a name="lesson-4-create-relationships"></a>Lezione 4: Crea relazioni
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

In questa lezione verranno verificate le relazioni create automaticamente al momento dell'importazione dei dati e verranno aggiunte nuove relazioni tra tabelle diverse. Una relazione è una connessione tra due tabelle che stabilisce in che modo devono essere correlati i dati nelle due tabelle. Ad esempio, la tabella DimProduct e la tabella DimProductSubcategory dispongono di una relazione basata sul fatto che ogni prodotto appartiene a una sottocategoria. Per altre informazioni, vedere [relazioni](../tabular-models/relationships-ssas-tabular.md).
  
Tempo stimato per il completamento della lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 3: Contrassegna come tabella data](lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Esaminare le relazioni esistenti e aggiungere nuove relazioni  
Quando sono stati importati i dati tramite l'importazione guidata tabella, si sono ottenute sette tabelle dal database AdventureWorksDW. In genere, quando si importano dati da un'origine relazionale, le relazioni esistenti vengono importate automaticamente insieme ai dati. Prima di procedere con la creazione del modello, è tuttavia necessario verificare che le relazioni tra tabelle siano state create correttamente. Per questa esercitazione, verranno inoltre aggiunte tre nuove relazioni.  
  
#### <a name="to-review-existing-relationships"></a>Per esaminare le relazioni esistenti  
  
1.  Fare clic sui **Model** menu > **visualizzazione modello** > **vista diagramma**.  

    La finestra Progettazione modelli viene ora visualizzata nella vista diagramma, un formato grafico in cui sono visualizzate tutte le tabelle importate, con linee tra di esse. Le linee tra le tabelle indicano le relazioni create automaticamente quando sono stati importati i dati.
    
    ![as-tabular-lesson4-diagram](media/as-tabular-lesson4-diagram.png)
  
    Usare i controlli della mini mappa nell'angolo inferiore destro di Progettazione modelli per regolare la vista in modo da includere il maggior numero di tabelle possibile. È possibile fare clic e trascinare le tabelle in posizioni diverse, avvicinandole o disponendole in un ordine particolare. Lo spostamento delle tabelle non influisce sulle relazioni già presenti tra le tabelle. Per visualizzare tutte le colonne in una determinata tabella, fare clic e trascinare un bordo della tabella per espanderla o ridurla.  
  
2.  Fare clic su linea continua tra il **DimCustomer** tabella e il **DimGeography** tabella. La linea continua tra queste due tabelle indica che questa relazione è attiva, ovvero viene utilizzata per impostazione predefinita nel calcolo delle formule DAX.  
  
    Si noti che il **GeographyKey** colonna il **DimCustomer** tabella e il **GeographyKey** colonna nel **DimGeography** tabella ora entrambe visualizzate all'interno di una finestra. Questa visualizzazione sono le colonne utilizzate nella relazione. Le proprietà della relazione sono ora visualizzate nella **proprietà** finestra.  
  
    > [!TIP]  
    > Oltre a usare Progettazione modelli in vista diagramma, è anche possibile usare la finestra di dialogo Gestisci relazioni per mostrare le relazioni tra tutte le tabelle in un formato tabella. Fare doppio clic su **relazioni** in Esplora modelli tabulari e quindi fare clic su **Gestisci relazioni**. La finestra di dialogo Gestisci relazioni per mostrare le relazioni create automaticamente quando sono stati importati i dati.  
  
3.  Utilizzare Progettazione modelli in vista diagramma oppure la finestra di dialogo Gestisci relazioni, per verificare le relazioni seguenti siano state create quando ognuna delle tabelle è stata importata dal database AdventureWorksDW:  
  
    |Attiva|Tabella|Tabella di ricerca correlata|  
    |----------|---------|------------------------|  
    |Yes|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Yes|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Yes|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Yes|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Yes|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Se sono presenti le relazioni nella tabella precedente mancante, verificare che il modello includa le tabelle seguenti: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory e FactInternetSales. Se tabelle della stessa connessione all'origine dati vengono importate in momenti distinti, non verranno create relazioni tra tali tabelle, che dovranno essere create manualmente.  

### <a name="take-a-closer-look"></a>Un attento
Nella vista diagramma, si noterà una freccia, un asterisco e un numero sulle linee che mostrano la relazione tra tabelle.

![as-tabular-lesson4-line](media/as-tabular-lesson4-line.png)

La freccia indica la direzione del filtro, che l'asterisco indica che la tabella è il lato "molti" nella cardinalità della relazione e il 1 sono illustrati in questa tabella è il uno lato della relazione. Se è necessario modificare una relazione. ad esempio, modificare la direzione filtro relazione o la cardinalità, fare doppio clic sulla linea della relazione nella vista diagramma per aprire la finestra di dialogo Modifica relazione.

![as-tabular-lesson4-edit](media/as-tabular-lesson4-edit.png)

È probabile che non sarà mai necessario modificare una relazione. Queste funzionalità sono pensate per modellazione avanzata dei dati e all'esterno dell'ambito di questa esercitazione. Per altre informazioni, vedere [bidirezionale tra i filtri per i modelli tabulari in SQL Server 2016 Analysis Services](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md).

In alcuni casi, potrebbe essere necessario creare relazioni aggiuntive tra tabelle nel modello per supportare una logica di business specifica. Per questa esercitazione, è necessario creare tre relazioni aggiuntive tra la tabella FactInternetSales e la tabella DimDate.  
  
#### <a name="to-add-new-relationships-between-tables"></a>Per aggiungere nuove relazioni tra tabelle  
  
1.  In Progettazione modelli, nel **FactInternetSales** di tabella, fare clic e tenere premuto il **OrderDate** colonna, quindi trascinare il cursore il **data** colonna il  **DimDate** di tabella e quindi rilasciare.  

    Verrà visualizzata una linea continua che è stata creata una relazione attiva tra la **OrderDate** colonna il **Internet Sales** tabella e il **data** colonna il **Data** tabella. 
  
      ![as-tabular-lesson4-new](media/as-tabular-lesson4-new.png) 
  
    > [!NOTE]  
    > Quando si creano relazioni, la direzione della cardinalità e filtro tra la tabella primaria e la tabella di ricerca correlata viene selezionata automaticamente.  
  
2.  Nel **FactInternetSales** di tabella, fare clic e tenere premuto il **DueDate** colonna, quindi trascinare il cursore il **data** colonna il **DimDate** tabella e quindi rilasciare.  
  
    Verrà visualizzata una linea punteggiata che è stata creata una relazione inattiva tra la **DueDate** colonna il **FactInternetSales** tabella e il **data** colonna il  **DimDate** tabella. È possibile creare più relazioni tra tabelle, ma può essere attiva una sola relazione per volta.  
  
3.  Creare infine un'ulteriore relazione; nel **FactInternetSales** di tabella, fare clic e tenere premuto il **ShipDate** colonna, quindi trascinare il cursore il **data** colonna il **DimDate**tabella e quindi rilasciare.  
    
     ![as-tabular-lesson4-newinactive](media/as-tabular-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Quali sono le operazioni successive?
Passare alla lezione successiva: [Lezione 5: Creare colonne calcolate](lesson-5-create-calculated-columns.md).
  
  
  
