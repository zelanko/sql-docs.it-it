---
title: "Analysis Services lezione supplementare dell'esercitazione: Righe di dettaglio | Microsoft Docs"
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
ms.openlocfilehash: bad45d18c351e838ec944b1ae67e3ce88c7e1d20
ms.sourcegitcommit: a6949111461eda0cc9a71689f86b517de3c5d4c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263313"
---
# <a name="supplemental-lesson---detail-rows"></a>Lezione supplementare - Righe di dettaglio

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In questa lezione supplementare si usare l'Editor DAX per definire un'espressione di righe di dettaglio personalizzata. Un'espressione di righe di dettaglio è una proprietà su una misura, fornendo agli utenti finali ulteriori informazioni sui risultati aggregati di una misura. 
  
Tempo stimato per il completamento della lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  

Questo articolo lezione supplementare fa parte di un'esercitazione di modellazione tabulare. Prima di eseguire le attività in questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti o avere un progetto di modello di esempio Adventure Works Internet Sales completato.  
  
## <a name="whats-the-issue"></a>Che cos'è il problema?

Esaminiamo i dettagli della misura InternetTotalSales, prima di aggiungere un'espressione di righe di dettaglio.

1.  In SSDT scegliere il **Model** menu > **analizza in Excel** aprire Excel e creare una tabella pivot vuota.
  
2.  Nella **PivotTable Fields**, aggiungere il **InternetTotalSales** misure dalla tabella FactInternetSales **valori**, **CalendarYear** da la tabella DimDate **colonne**, e **EnglishCountryRegionName** al **righe**. La tabella pivot offre ora i risultati aggregati dalla misura InternetTotalSales per area e anno. 

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-pivottable.png)

3. Nella tabella pivot, fare doppio clic su un valore aggregato per un anno e un nome di area. Di seguito sono stati selezionati l'Australia e l'anno 2014. Viene aperto un nuovo foglio contenente i dati, ma non molto utili.

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-sheet.png)
  
Che cosa si vuole vedere di seguito è riportata una tabella contenente colonne e righe di dati che contribuiscono al risultato aggregato della misura InternetTotalSales. A tale scopo, è possibile aggiungere un'espressione di righe di dettaglio come proprietà della misura.

## <a name="add-a-detail-rows-expression"></a>Aggiungere un'espressione di righe di dettaglio

#### <a name="to-create-a-detail-rows-expression"></a>Per creare un'espressione di righe di dettaglio 
  
1. Nella griglia delle misure della tabella FactInternetSales, fare clic sui **InternetTotalSales** misure. 

2. Nelle **delle proprietà** > **espressione di righe di dettaglio**, fare clic sul pulsante dell'editor per aprire l'Editor DAX.

    ![as-lesson-detail-rows-ellipse](../tutorial-tabular-1400/media/as-lesson-detail-rows-ellipse.png)

3. Nell'Editor DAX immettere l'espressione seguente:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    Questa espressione consente di specificare i nomi, le colonne, e i risultati delle misure dalla tabella FactInternetSales e tabelle correlate vengono restituiti quando un utente fa doppio clic su un risultato aggregato in una tabella pivot o un report.

4. Tornare a Excel ed eliminare il foglio creato nel passaggio 3, quindi fare doppio clic su un valore aggregato. Questa volta, con una proprietà di espressione di righe di dettaglio definita per la misura, un nuovo foglio apre contenente dati molto più utili.

    ![as-lesson-detail-rows-detailsheet](../tutorial-tabular-1400/media/as-lesson-detail-rows-detailsheet.png)

5. Ridistribuire il modello.

  
## <a name="see-also"></a>Vedere anche  

[Funzione SELECTCOLUMNS (DAX)](/dax/selectcolumns-function-dax)  
[Lezione supplementare - Sicurezza dinamica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[Lezione supplementare - Gerarchie incomplete](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)  
