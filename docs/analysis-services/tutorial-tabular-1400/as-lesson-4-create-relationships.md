---
title: 'Analysis Services tutorial-lezione 4: Creare relazioni | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 7f593dafc1a734cd5f3a0c9fde4f47987f0b92af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207392"
---
# <a name="create-relationships"></a>Creare relazioni

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In questa lezione, verificare le relazioni create automaticamente quando sono stati importati i dati e aggiungere nuove relazioni tra tabelle diverse. Una relazione è una connessione tra due tabelle che stabilisce in che modo devono essere correlati i dati nelle due tabelle. Ad esempio, la tabella DimProduct e la tabella DimProductSubcategory dispongono di una relazione basata sul fatto che ogni prodotto appartiene a una sottocategoria. Per altre informazioni, vedere [relazioni](../tabular-models/relationships-ssas-tabular.md).
  
Tempo stimato per il completamento della lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  

Questo articolo fa parte di un'esercitazione di modellazione tabulare, che deve essere completata nell'ordine. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 3: Contrassegna come tabella data](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Esaminare le relazioni esistenti e aggiungere nuove relazioni  

Quando sono stati importati i dati usando recupera dati, si sono ottenute sette tabelle dal database AdventureWorksDW. In genere, quando si importano dati da un'origine relazionale, le relazioni esistenti vengono importate automaticamente insieme ai dati. Affinché recupera dati crei automaticamente le relazioni nel modello di dati, deve esistere relazioni tra le tabelle nell'origine dati.

Prima di procedere alla creazione del modello, è necessario verificare le relazioni tra tabelle è stato creato correttamente. Per questa esercitazione, è anche possibile aggiungere tre nuove relazioni.  

  
#### <a name="to-review-existing-relationships"></a>Per esaminare le relazioni esistenti  
  
1.  Fare clic sui **Model** menu > **visualizzazione modello** > **vista diagramma**.  

    Progettazione modelli viene ora visualizzato nella vista diagramma, un formato grafico per visualizzare tutte le tabelle importate, con linee tra di esse. Le linee tra le tabelle indicano le relazioni create automaticamente quando sono stati importati i dati.
    
    ![as-lesson4-diagram](../tutorial-tabular-1400/media/as-lesson4-diagram.png)
  
    > [!NOTE]
    > Se tutte le relazioni tra le tabelle non è visibile, probabilmente significa che non sono presenti relazioni tra tali tabelle nell'origine dati.

    Includere il maggior numero di tabelle possibile usando i controlli mini mappa nell'angolo inferiore destro della finestra di progettazione del modello. È anche possibile fare clic sulle tabelle e trascinarle in posizioni diverse, avvicinandole o disponendole in un ordine particolare. Lo spostamento delle tabelle non influenza le relazioni tra le tabelle. Per visualizzare tutte le colonne in una determinata tabella, fare clic e trascinare un bordo della tabella per espanderla o ridurla.  
  
2.  Fare clic su linea continua tra il **DimCustomer** tabella e il **DimGeography** tabella. La linea continua tra queste due tabelle illustra che questa relazione è attiva, vale a dire, che viene utilizzato per impostazione predefinita quando si calcola le formule DAX.  
  
    Si noti che il **GeographyKey** colonna il **DimCustomer** tabella e il **GeographyKey** colonna nel **DimGeography** tabella ora entrambe visualizzate all'interno di una finestra. Queste colonne vengono utilizzate nella relazione. Le proprietà della relazione sono ora visualizzate nella **proprietà** finestra.  
  
    > [!TIP]  
    > È anche possibile usare la finestra di dialogo Gestisci relazioni per mostrare le relazioni tra tutte le tabelle in un formato tabella. In Esplora modelli tabulari, fare doppio clic su **relazioni** > **Gestisci relazioni**.
  
3.  Verificare le relazioni seguenti siano state create quando ognuna delle tabelle è stata importata dal database AdventureWorksDW:  
  
    |Attivo|Tabella|Tabella di ricerca correlata|  
    |----------|---------|------------------------|  
    |Yes|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Yes|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Yes|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Yes|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Yes|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Se sono presenti le relazioni mancante, verificare che il modello includa le tabelle seguenti: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory e FactInternetSales. Se si importano tabelle dalla stessa connessione origine dati in momenti distinti, tutte le relazioni tra tali tabelle non vengono create e devono essere create manualmente. Se è visualizzata alcuna relazione, significa che non sono presenti relazioni nell'origine dati. È possibile crearli manualmente nel modello di dati.

### <a name="take-a-closer-look"></a>Un attento

Nella vista diagramma, si noti che una freccia, un asterisco e un numero sulle linee che mostrano la relazione tra tabelle.

![as-lesson4-line](../tutorial-tabular-1400/media/as-lesson4-line.png)

La freccia mostra la direzione del filtro. L'asterisco indica che questa tabella è la *molte* side nella cardinalità della relazione e quella Mostra questa tabella è la *uno* lato della relazione. Se è necessario modificare una relazione. ad esempio, modificare la direzione filtro relazione o la cardinalità, fare doppio clic sulla linea della relazione per aprire la finestra di dialogo Modifica relazione.

![as-lesson4-edit](../tutorial-tabular-1400/media/as-lesson4-edit.png)

Queste funzionalità sono pensate per modellazione avanzata dei dati e all'esterno dell'ambito di questa esercitazione. Per altre informazioni, vedere [bidirezionale tra i filtri per i modelli tabulari in Analysis Services](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md).

In alcuni casi, potrebbe essere necessario creare relazioni aggiuntive tra tabelle nel modello per supportare una logica di business specifica. Per questa esercitazione, è necessario creare tre relazioni aggiuntive tra la tabella FactInternetSales e la tabella DimDate.  
  
#### <a name="to-add-new-relationships-between-tables"></a>Per aggiungere nuove relazioni tra tabelle  
  
1.  In Progettazione modelli, nel **FactInternetSales** di tabella, fare clic e tenere premuto il **OrderDate** colonna, quindi trascinare il cursore il **data** colonna il  **DimDate** di tabella e quindi rilasciare.  

    Verrà visualizzata una linea continua che è stata creata una relazione attiva tra la **OrderDate** colonna il **Internet Sales** tabella e il **data** colonna il  **Data** tabella. 
  
      ![as-lesson4-new](../tutorial-tabular-1400/media/as-lesson4-new.png) 
  
    > [!NOTE]  
    > Quando si creano relazioni, la direzione della cardinalità e filtro tra la tabella primaria e la tabella di ricerca correlata viene selezionata automaticamente.  
  
2.  Nel **FactInternetSales** di tabella, fare clic e tenere premuto il **DueDate** colonna, quindi trascinare il cursore il **data** colonna il **DimDate** tabella e quindi rilasciare.  
  
    Verrà visualizzata una linea punteggiata che è stata creata una relazione inattiva tra la **DueDate** colonna il **FactInternetSales** tabella e il **data** colonna il  **DimDate** tabella. È possibile creare più relazioni tra tabelle, ma può essere attiva una sola relazione per volta. Le relazioni inattive possono essere rese attive eseguire aggregazioni speciali in espressioni DAX personalizzate.  
  
3.  Creare infine un'ulteriore relazione. Nel **FactInternetSales** di tabella, fare clic e tenere premuto il **ShipDate** colonna, quindi trascinare il cursore il **data** colonna il **DimDate** tabella e quindi rilasciare.  
    
     ![as-lesson4-newinactive](../tutorial-tabular-1400/media/as-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Argomenti successivi

[Lezione 5: Creare colonne calcolate](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md).
  
  
  
