---
title: 'Lezione 6: Creare misure | Microsoft Docs'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f8ad53f78acb862101ff633f663ea03198825ab
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404663"
---
# <a name="lesson-6-create-measures"></a>Lezione 6: Creare misure
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

In questa lezione verranno create misure da includere nel modello. Come per le colonne calcolate create nella lezione precedente, una misura è un calcolo creato utilizzando una formula DAX. A differenza delle colonne calcolate, tuttavia, le misure vengono valutate in base a un *filtro*selezionato dall'utente, ad esempio una colonna o un filtro dei dati specifico aggiunto al campo Etichette di riga in una tabella pivot. Viene quindi calcolato un valore per ogni cella nel filtro tramite la misura applicata. Le misure sono calcoli potenti e flessibili che è opportuno includere in quasi tutti i modelli tabulari per eseguire calcoli dinamici su dati numerici. Per altre informazioni, vedere [misure](../tabular-models/measures-ssas-tabular.md).  
  
Per creare misure, si userà il *griglia delle misure*. Per impostazione predefinita, ogni tabella dispone di una griglia delle misure vuota. Tuttavia, in genere, non vengono create misure per ogni tabella. La griglia delle misure viene visualizzata sotto una tabella di Progettazione modelli se si trova in Vista dati. Per visualizzare o nascondere la griglia delle misure per una tabella, fare clic sul menu **Tabella** , quindi su **Mostra griglia delle misure**.  
  
È possibile creare una misura facendo clic su una cella vuota nella griglia delle misure, quindi digitando una formula DAX sulla barra della formula. Quando si preme INVIO per completare la formula, la misura viene visualizzata nella cella. È anche possibile creare misure usando una funzione di aggregazione standard facendo clic su una colonna, quindi sul pulsante Somma automatica (**∑**) sulla barra degli strumenti. Le misure create utilizzando la funzionalità Somma automatica verranno visualizzata nella cella della griglia delle misure direttamente sotto la colonna, ma possono essere spostate.  
  
In questa lezione verranno create misure sia immettendo una formula DAX sulla barra della formula che utilizzando la funzionalità Somma automatica.  
  
Tempo stimato per il completamento della lezione: **30 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 5: Creare colonne calcolate](lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Creare misure  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>Per creare una misura DaysCurrentQuarterToDate nella tabella DimDate  
  
1.  In Progettazione modelli, scegliere il **DimDate** tabella.  
  
2.  Nella griglia delle misure fare clic sulla cella vuota in alto a sinistra.  
  
3.  Sulla barra della formula digitare la formula seguente:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Si noti che la cella superiore sinistra contiene ora un nome di misura **DaysCurrentQuarterToDate**, seguito dal risultato **92**.
    
      ![as-tabular-lesson6-newmeasure](media/as-tabular-lesson6-newmeasure.png) 
    
    Diversamente dalle colonne calcolate, con le formule di misura è possibile digitare il nome della misura, seguito da una virgola, seguita dall'espressione della formula.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>Per creare una misura DaysInCurrentQuarter nella tabella DimDate  
  
1.  Con il **DimDate** ancora attiva in Progettazione modelli, nella griglia delle misure, fare clic sulla cella vuota sotto la misura appena creata.  
  
2.  Sulla barra della formula digitare la formula seguente:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Quando si crea un rapporto di confronto tra un periodo incompleto e il periodo precedente, la formula deve prendere in considerazione la proporzione del periodo trascorsa e confrontarla con la stessa proporzione del periodo precedente. In questo caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] Restituisce la proporzione trascorsa nel periodo corrente.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>Per creare una misura InternetDistinctCountSalesOrder nella tabella FactInternetSales  
  
1.  Scegliere il **FactInternetSales** tabella.   
  
2.  Fare clic sui **SalesOrderNumber** sull'intestazione di colonna.  
  
3.  Nella barra degli strumenti fare clic sulla freccia giù accanto al pulsante Somma automatica (**∑**), quindi selezionare **DistinctCount**.  
  
    La funzionalità Somma automatica consente di creare automaticamente una misura per la colonna selezionata utilizzando la formula di aggregazione standard DistinctCount.  
    
       ![as-tabular-lesson6-newmeasure2](media/as-tabular-lesson6-newmeasure2.png)
  
4.  Nella griglia delle misure fare clic su nuova misura, quindi nel **delle proprietà** finestra, in **nome misura**, rinominare la misura in **InternetDistinctCountSalesOrder**. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>Per creare altre misure nella tabella FactInternetSales  
  
1.  Utilizzando la funzionalità Somma automatica, è possibile creare le misure seguenti e assegnare loro un nome:  
  
    |Nome misura|colonna|Somma automatica (∑)|Formula|  
    |----------------|----------|-----------------|-----------|  
    |InternetOrderLinesCount|SalesOrderLineNumber|Count|=COUNTA([SalesOrderLineNumber])|  
    |InternetTotalUnits|OrderQuantity|Sum|=SUM([OrderQuantity])|  
    |InternetTotalDiscountAmount|DiscountAmount|Sum|=SUM([DiscountAmount])|  
    |InternetTotalProductCost|TotalProductCost|Sum|=SUM([TotalProductCost])|  
    |InternetTotalSales|SalesAmount|Sum|=SUM([SalesAmount])|  
    |InternetTotalMargin|Margin|Sum|=SUM([Margin])|  
    |InternetTotalTaxAmt|TaxAmt|Sum|=SUM([TaxAmt])|  
    |InternetTotalFreight|Freight|Sum|=SUM([Freight])|  
  
2.  Facendo clic su una cella vuota nella griglia delle misure e usando la barra della formula, creare e denominare le misure seguenti nell'ordine:  
  
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
  
## <a name="whats-next"></a>Quali sono le operazioni successive?
Passare alla lezione successiva: [Lezione 7: Creare indicatori di prestazioni chiave](lesson-7-create-key-performance-indicators.md).  

  
