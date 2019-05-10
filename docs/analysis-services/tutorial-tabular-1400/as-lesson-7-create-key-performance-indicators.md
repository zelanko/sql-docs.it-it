---
title: 'Analysis Services tutorial-lezione 7: Creare indicatori di prestazioni chiave | Microsoft Docs'
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
ms.openlocfilehash: 5f3b3de71cb60a27613482255556bfbff6bcc8cf
ms.sourcegitcommit: 6193aa9b4967302424270d67c27dbc601ca6849a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877625"
---
# <a name="create-key-performance-indicators"></a>Creare indicatori di prestazioni chiave

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In questa lezione si creare indicatori di prestazioni chiave (KPI). Gli indicatori KPI vengono usati per misurare le prestazioni di un valore definito da una *Base* misura, in un *destinazione* definito anch'esso da una misura o da un valore assoluto. Nelle applicazioni client di creazione di report, gli indicatori KPI possono fornire ai professionisti aziendali un metodo semplice e veloce per comprendere l'andamento aziendale in generale o per identificare le tendenze. Per altre informazioni, vedere [gli indicatori KPI](../tabular-models/kpis-ssas-tabular.md)
  
Tempo stimato per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  

Questo articolo fa parte di un'esercitazione di modellazione tabulare, che deve essere completata nell'ordine. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 6: Creare misure](../tutorial-tabular-1400/as-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Creare indicatori di prestazioni chiave  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>Per creare un KPI InternetCurrentQuarterSalesPerformance  
  
1.  In Progettazione modelli, scegliere il **FactInternetSales** tabella.  
  
2.  Nella griglia delle misure fare clic su una cella vuota.  
  
3.  Sulla barra della formula sopra la tabella digitare la formula seguente: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=IF([InternetPreviousQuarterSalesProportionToQTD]<>0,([InternetCurrentQuarterSales]-[InternetPreviousQuarterSalesProportionToQTD])/[InternetPreviousQuarterSalesProportionToQTD],BLANK()) 
    ```

    Questa misura viene usata come misura di Base per l'indicatore KPI.  
  
4.  Nella griglia delle misure, fare doppio clic su **InternetCurrentQuarterSalesPerformance** > **Create KPI**.   
  
5.  Nella finestra di dialogo indicatore di prestazioni chiave (KPI), in **destinazione** selezionate **valore assoluto**, quindi digitare **1.1**.  
  
7.  Nel campo relativo al dispositivo di scorrimento sinistro (in basso) digitare **1**, quindi nel campo relativo al dispositivo di scorrimento destro (in alto), digitare **1.07**.  
  
8.  In **Seleziona stile icona**selezionare un tipo di icona a rombo (rosso), triangolo (giallo) o cerchio (verde).
  
    ![as-lesson7-kpi](../tutorial-tabular-1400/media/as-lesson7-kpi.png)
    
    > [!TIP]  
    > Si noti l'espandibile **descrizioni** etichetta sotto gli stili di icona disponibili. Utilizzare le descrizioni per i vari elementi KPI per renderle più facilmente identificabili nelle applicazioni client.  
  
9. Fare clic su **OK** per completare l'indicatore KPI.  
  
    Nella griglia delle misure osservare l'icona accanto al **InternetCurrentQuarterSalesPerformance** misure. Questa icona indica che la misura funge da valore di base per un indicatore KPI.  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>Per creare un KPI InternetCurrentQuarterMarginPerformance  
  
1.  Nella griglia delle misure per la **FactInternetSales** di tabella, fare clic su una cella vuota.  
  
2.  Sulla barra della formula sopra la tabella digitare la formula seguente:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Fare doppio clic su **InternetCurrentQuarterMarginPerformance** > **crea KPI**.  
  
4.  Nella finestra di dialogo indicatore di prestazioni chiave (KPI), in **destinazione** selezionate **valore assoluto**, quindi digitare **1,25**.   
  
5.  Nel campo di dispositivo di scorrimento sinistro (in basso) scorrere fino a quando non viene visualizzato il campo **0.8**, quindi far scorrere il dispositivo di scorrimento destro (in alto) fino a quando non viene visualizzato il campo **1.03**.  
  
6.  In **Seleziona stile icona**selezionare un tipo di icona a rombo (rosso), triangolo (giallo) o cerchio (verde), quindi fare clic su **OK**.  
  
## <a name="whats-next"></a>Quali sono le operazioni successive?

[Lezione 8: Creare prospettive](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md).
  
  
