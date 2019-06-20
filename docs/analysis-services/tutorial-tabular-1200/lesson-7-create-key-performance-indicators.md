---
title: 'Lezione 7: Creare indicatori di prestazioni chiave | Microsoft Docs'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 21767c239ed3498e0e593e221203b1cde3b7ae69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65403873"
---
# <a name="lesson-7-create-key-performance-indicators"></a>Lezione 7: Creare indicatori di prestazioni chiave
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

In questa lezione verranno creati indicatori di prestazioni chiave (KPI). Gli indicatori di prestazioni chiave vengono usati per misurare le prestazioni di un valore, definito mediante una misura di *base* , rispetto a un valore *target* , definito anch'esso da una misura o da un valore assoluto. Nelle applicazioni client di creazione di report, gli indicatori KPI possono fornire ai professionisti aziendali un metodo semplice e veloce per comprendere l'andamento aziendale in generale o per identificare le tendenze. Per altre informazioni, vedere [gli indicatori KPI](../tabular-models/kpis-ssas-tabular.md).  
  
Tempo stimato per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 6: Creare misure](lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Creare indicatori di prestazioni chiave  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>Per creare un KPI InternetCurrentQuarterSalesPerformance  
  
1.  In Progettazione modelli, scegliere il **FactInternetSales** tabella (scheda).  
  
2.  Nella griglia delle misure fare clic su una cella vuota.  
  
3.  Sulla barra della formula sopra la tabella digitare la formula seguente: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=IFERROR([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Tale misura definirà fungerà da misura di base per l'indicatore KPI.  
  
4.  Fare doppio clic su **InternetCurrentQuarterSalesPerformance** > **crea KPI**.   
  
5.  Nella finestra di dialogo indicatore di prestazioni chiave (KPI), in **destinazione** selezionate **valore assoluto**, quindi digitare **1.1**.  
  
7.  Nel campo relativo al dispositivo di scorrimento sinistro (in basso) digitare **1**, quindi nel campo relativo al dispositivo di scorrimento destro (in alto), digitare **1.07**.  
  
8.  In **Seleziona stile icona**selezionare un tipo di icona a rombo (rosso), triangolo (giallo) o cerchio (verde).
  
    ![as-tabular-lesson7-kpi](media/as-tabular-lesson7-kpi.png)
    
    > [!TIP]  
    > Si noti l'espandibile **descrizioni** etichetta sotto gli stili di icona disponibili. Questa scheda consente di immettere descrizioni per i vari elementi KPI per renderle più facilmente identificabili nelle applicazioni client.  
  
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
  
5.  In **Definisci soglie stato**far scorrere il dispositivo di scorrimento sinistro (in basso) fino a quando non viene visualizzato **0.8**, quindi far scorrere il dispositivo di scorrimento destro (in alto) fino a quando non viene visualizzato **1.03**.  
  
6.  In **Seleziona stile icona**selezionare un tipo di icona a rombo (rosso), triangolo (giallo) o cerchio (verde), quindi fare clic su **OK**.  
  
## <a name="whats-next"></a>Quali sono le operazioni successive?
Passare alla lezione successiva: [Lezione 8: Creare prospettive](lesson-8-create-perspectives.md).
  
  
