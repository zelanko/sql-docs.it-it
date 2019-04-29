---
title: 'Lezione 2: Aggiunta di modelli di Data Mining per la struttura di Data Mining Time Series | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 75c2a74b-21ce-44fb-a26b-68be4c685c12
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ae0bb91fafb53c0c077a4e0d82558b550d0e6070
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855711"
---
# <a name="lesson-2-adding-mining-models-to-the-time-series-mining-structure"></a>Lezione 2: Aggiunta di modelli di Data Mining per la struttura di Data Mining Time Series
  In questa lezione si aggiungerà un nuovo modello di data mining alla struttura di data mining appena creato in [lezione 1: Creazione di una serie temporale, modello di Data Mining e struttura di Data Mining](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md).  
  
## <a name="alter-mining-structure-statement"></a>Istruzione ALTER MINING STRUCTURE  
 Per aggiungere un nuovo modello di data mining a una struttura di data mining esistente, viene utilizzata la [ALTER MINING STRUCTURE &#40;DMX&#41; ](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016) istruzione. Il codice nell'istruzione può essere suddiviso nelle parti seguenti:  
  
-   Identificazione della struttura di data mining  
  
-   Denominazione del modello di data mining  
  
-   Definizione della colonna chiave  
  
-   Definizione delle colonne stimabili  
  
-   Specifica delle modifiche a livello di algoritmo e parametri  
  
 Di seguito è riportato un esempio generico dell'istruzione ALTER MINING STRUCTURE:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
ADD MINING MODEL [<mining model name>]  
   ([<key columns>],  
    <mining model columns>  
   )  
USING <algorithm name>([<algorithm parameters>])  
[WITH DRILLTHROUGH]  
```  
  
 La prima riga del codice identifica la struttura di data mining esistente a cui verranno aggiunti i modelli di data mining:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 La riga successiva del codice indica il nome del modello di data mining che verrà aggiunto alla struttura di data mining:  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 Per informazioni sulla denominazione di un oggetto in DMX, vedere [identificatori &#40;DMX&#41;](/sql/dmx/identifiers-dmx).  
  
 Le successive righe del codice definiscono le colonne della struttura di data mining che verranno utilizzate dal modello di data mining:  
  
```  
[<key columns>],  
<mining model columns>  
```  
  
 È possibile utilizzare solo colonne già esistenti nella struttura di data mining e la prima colonna nell'elenco deve essere la colonna chiave dalla struttura di data mining.  
  
 Le righe successive del codice definiscono l'algoritmo di data mining che genera il modello di data mining e i parametri che è possibile impostare nell'algoritmo, oltre a specificare se è possibile eseguire il drill-down dal modello di data mining per visualizzare dati dettagliati nei case di training:  
  
```  
USING <algorithm name>([<algorithm parameters>])  
WITH DRILLTHROUGH  
```  
  
 Per altre informazioni sui parametri dell'algoritmo che è possibile modificare, vedere [riferimento tecnico algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
 Per specificare che una colonna nel modello di data mining deve essere utilizzata per la stima, è possibile utilizzare la sintassi seguente:  
  
```  
<mining model column> PREDICT  
```  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione verranno eseguite le attività seguenti:  
  
-   Aggiunta di un nuovo modello di data mining Time Series alla struttura  
  
-   Modifica dei parametri dell'algoritmo per utilizzare un metodo differente di analisi e stima  
  
## <a name="adding-an-arima-time-series-model-to-the-structure"></a>Aggiunta di un modello Time Series ARIMA alla struttura  
 Il primo passaggio consiste nell'aggiunta di un nuovo modello di data mining di previsione alla struttura esistente. Per impostazione predefinita, l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series crea modelli di data mining Time Series tramite due algoritmi, ARIMA e ARTXP, e combinando i risultati. È tuttavia possibile specificare un solo algoritmo da utilizzare o l'esatta combinazione di algoritmi. In questo passaggio si aggiungerà un nuovo modello che utilizza solo l'algoritmo ARIMA. L'algoritmo ARIMA è ottimizzato per le stime a lungo termine.  
  
#### <a name="to-add-an-arima-time-series-mining-model"></a>Per aggiungere un modello di data mining Time Series ARIMA  
  
1.  Nella **Esplora oggetti**, fare doppio clic sull'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], scegliere **nuova Query**, quindi fare clic su **DMX** per aprire l'Editor di Query e una nuova query vuota.  
  
2.  Copiare l'esempio generico dell'istruzione ALTER MINING STRUCTURE nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    <mining structure name>   
    ```  
  
     con:  
  
    ```  
    [Forecasting_MIXED_Structure]  
    ```  
  
4.  Sostituire quanto segue:  
  
    ```  
    <mining model name>   
    ```  
  
     con:  
  
    ```  
    Forecasting_ARIMA  
    ```  
  
5.  Sostituire quanto segue:  
  
    ```  
    <key columns>,  
    ```  
  
     con:  
  
    ```  
    [ReportingDate],  
    [ModelRegion]  
    ```  
  
     Si noti che non è necessario ripetere le informazioni sul tipo di data o sul tipo di contenuto fornite nell'istruzione CREATE MINING MODEL, perché queste informazioni sono già memorizzate nella struttura di data mining.  
  
6.  Sostituire quanto segue:  
  
    ```  
    <mining model columns>  
    ```  
  
     con:  
  
    ```  
    ([Quantity] PREDICT,  
    [Amount] PREDICT  
    )  
    ```  
  
7.  Sostituire quanto segue:  
  
    ```  
    USING <algorithm name>([<algorithm parameters>])   
    [WITH DRILLTHROUGH]  
    ```  
  
     con:  
  
    ```  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
     L'istruzione risultante dovrebbe essere la seguente:  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARIMA]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
8.  Nel **File** menu, fare clic su **Salva Dmxquery1.DMX**.  
  
9. Nel **Salva con nome** della finestra di dialogo passare alla cartella appropriata e assegnare un nome di file `Forecasting_ARIMA.dmx`.  
  
10. Sulla barra degli strumenti, scegliere il **Execute** pulsante.  
  
## <a name="adding-an-artxp-time-series-model-to-the-structure"></a>Aggiunta di un modello Time Series ARTXP alla struttura  
 L'algoritmo ARTXP era l'algoritmo Time Series predefinito in SQL Server 2005 ed è ottimizzato per le stime a breve termine. Per confrontare le stime tramite tutti e tre gli algoritmi Time Series, si aggiungerà un ulteriore modello basato sull'algoritmo ARTXP.  
  
#### <a name="to-add-an-artxp-time-series-mining-model"></a>Per aggiungere un modello di data mining Time Series ARTXP  
  
1.  Copiare il codice seguente in una finestra di query vuota.  
  
     Si noti che non è necessario modificare alcun elemento, ad eccezione del nome del nuovo modello di data mining e del valore del parametro FORECAST_METHOD.  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARTXP]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARTXP')  
    WITH DRILLTHROUGH  
    ```  
  
2.  Nel **File** menu, fare clic su **Salva Dmxquery1.DMX**.  
  
3.  Nel **Salva con nome** della finestra di dialogo passare alla cartella appropriata e assegnare un nome di file `Forecasting_ARTXP.dmx`.  
  
4.  Sulla barra degli strumenti, scegliere il **Execute** pulsante.  
  
 Nella lezione successiva verranno elaborati tutti i modelli e la struttura di data mining.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 3: La serie temporale di elaborazione struttura e modelli](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
