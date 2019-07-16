---
title: 'Analysis Services tutorial-lezione 6: Creare misure | Microsoft Docs'
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
ms.openlocfilehash: 715fe6144cc430e545feb3c484d148531cff6ec9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207327"
---
# <a name="create-measures"></a>Creare misure

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In questa lezione verranno create le misure da includere nel modello. Come per le colonne calcolate create, una misura è un calcolo creato utilizzando una formula DAX. Tuttavia, diversamente dalle colonne calcolate, le misure vengono valutate usando un utente selezionato *filtro*. Ad esempio, una particolare colonna o sezionamento aggiunto al campo etichette di riga in una tabella pivot. Viene quindi calcolato un valore per ogni cella nel filtro tramite la misura applicata. Le misure sono calcoli potenti e flessibili che si desidera includere in quasi tutti i modelli tabulari per eseguire calcoli dinamici su dati numerici. Per altre informazioni, vedere [misure](../tabular-models/measures-ssas-tabular.md).
  
Per creare misure, usare il *griglia delle misure*. Per impostazione predefinita, ogni tabella dispone di una griglia delle misure vuota; Tuttavia, in genere non è creare misure per ogni tabella. La griglia delle misure viene visualizzata sotto una tabella di Progettazione modelli se si trova in Vista dati. Per visualizzare o nascondere la griglia delle misure per una tabella, fare clic sul menu **Tabella** , quindi su **Mostra griglia delle misure**.  
  
È possibile creare una misura facendo clic su una cella vuota nella griglia delle misure, e quindi digitando una formula DAX nella barra della formula. Quando premere INVIO per completare la formula, la misura quindi viene visualizzato nella cella. È anche possibile creare misure con una funzione di aggregazione standard facendo clic su una colonna, e quindi fare clic sul pulsante Somma automatica (**∑**) sulla barra degli strumenti. Le misure create utilizzando la funzionalità Somma automatica vengono visualizzate nella cella della griglia delle misure direttamente sotto la colonna, ma possono essere spostate.  
  
In questa lezione si create misure sia immettendo una formula DAX nella barra della formula e usando la funzionalità Somma automatica.  
  
Tempo stimato per il completamento della lezione: **30 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  

Questo articolo fa parte di un'esercitazione di modellazione tabulare, che deve essere completata nell'ordine. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 5: Creare colonne calcolate](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Creare misure  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>Per creare una misura DaysCurrentQuarterToDate nella tabella DimDate  
  
1.  In Progettazione modelli, scegliere il **DimDate** tabella.  
  
2.  Nella griglia delle misure fare clic sulla cella vuota in alto a sinistra.  
  
3.  Sulla barra della formula digitare la formula seguente:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Si noti che la cella superiore sinistra contiene ora un nome di misura **DaysCurrentQuarterToDate**, seguito dal risultato **92**. Il risultato non è pertinente a questo punto perché non è stato applicato alcun filtro utente.
    
      ![as-lesson6-newmeasure](../tutorial-tabular-1400/media/as-lesson6-newmeasure.png) 
    
    Diversamente dalle colonne calcolate, con le formule di misura è possibile digitare il nome della misura, seguito da due punti, seguiti dall'espressione della formula.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>Per creare una misura DaysInCurrentQuarter nella tabella DimDate  
  
1.  Con il **DimDate** ancora attiva in Progettazione modelli, nella griglia delle misure, fare clic sulla cella vuota sotto la misura creata.  
  
2.  Sulla barra della formula digitare la formula seguente:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Quando si crea un rapporto di confronto tra un periodo incompleto e il periodo precedente. La formula deve tenere conto della proporzione del periodo trascorsa e confrontarla con la stessa proporzione del periodo precedente. In questo caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] Restituisce la proporzione trascorsa nel periodo corrente.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>Per creare una misura InternetDistinctCountSalesOrder nella tabella FactInternetSales  
  
1.  Scegliere il **FactInternetSales** tabella.   
  
2.  Scegliere il **SalesOrderNumber** sull'intestazione di colonna.  
  
3.  Nella barra degli strumenti fare clic sulla freccia giù accanto al pulsante Somma automatica (**∑**), quindi selezionare **DistinctCount**.  
  
    La funzionalità Somma automatica consente di creare automaticamente una misura per la colonna selezionata utilizzando la formula di aggregazione standard DistinctCount.  
    
       ![as-lesson6-newmeasure2](../tutorial-tabular-1400/media/as-lesson6-newmeasure2.png)
  
4.  Nella griglia delle misure fare clic su nuova misura, quindi nel **delle proprietà** finestra, in **nome misura**, rinominare la misura in **InternetDistinctCountSalesOrder**. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>Per creare altre misure nella tabella FactInternetSales  
  
1.  Utilizzando la funzionalità Somma automatica, è possibile creare le misure seguenti e assegnare loro un nome:  

    |Colonna|Nome misura|Somma automatica (∑)|Formula|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Count|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|Sum|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|Sum|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|Sum|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|Sum|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|Sum|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|Sum|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|Sum|=SUM([Freight])|  
  
2.  Facendo clic su una cella vuota nella griglia delle misure e usando la barra della formula, creare, le misure personalizzate seguenti nell'ordine:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Le misure create per la tabella FactInternetSales utilizzabile per analizzare dati finanziari critici, ad esempio vendite, costi e margine di profitto per gli elementi definiti dal filtro selezionato di utenti.  
  
## <a name="whats-next"></a>Argomenti successivi

[Lezione 7: Creare indicatori di prestazioni chiave](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md).  

  
