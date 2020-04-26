---
title: Stime basate su serie temporali utilizzando dati di sostituzione (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a23a6e1d-1d49-41ea-8314-925dc8e4df5e
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c96b70775105ea9446810ac3b064ae7cb07d4337
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63312876"
---
# <a name="time-series-predictions-using-replacement-data-intermediate-data-mining-tutorial"></a>Stime basate su serie temporali utilizzando dati di sostituzione (Esercitazione intermedia sul data mining)
  In questa attività verrà compilato un nuovo modello basato sui dati di vendita mondiali. Verrà quindi creata una query di stima che applica il modello delle vendite mondiali a una delle singole aree.  
  
## <a name="building-a-general-model"></a>Compilazione di un modello generale  
 L'analisi dei risultati del modello di data mining originale ha rivelato differenze rilevanti tra aree e linee di prodotti. Ad esempio, le vendite in America del nord sono state elevate per il modello M200, mentre le vendite del modello T1000 non sono andate altrettanto bene. Tuttavia, l'analisi è complicata dal fatto che alcune serie non hanno molti dati o che i dati sono stati avviati in un momento diverso. Alcuni dati erano inoltre mancanti.  
  
 ![Serie per la stima delle quantità M200 e T1000](../../2014/tutorials/media/6series-defaultforecasting.gif "Serie per la stima delle quantità M200 e T1000")  
  
 Per risolvere alcuni dei problemi di qualità dei dati, si uniranno i dati dalle vendite di tutto il mondo e si utilizzerà tale set di tendenze di vendita generali per compilare un modello che possa essere applicato per stimare le vendite future in tutte le aree.  
  
 Quando si creano stime, si utilizza il modello generato eseguendo il training sui dati di vendita mondiali, sostituendo tuttavia i punti dati cronologici con i dati di vendita di ogni singola area. In tal modo la forma della tendenza viene mantenuta, ma i valori stimati vengono allineati con le cifre delle vendite cronologiche per ogni area e modello.  
  
## <a name="performing-cross-prediction-with-a-time-series-model"></a>Esecuzione di stime incrociate con un modello Time Series  
 Il processo che prevede l'utilizzo dei dati di una serie per stimare le tendenze in un'altra serie è detto stima incrociata. È possibile utilizzare la stima incrociata in molti scenari, ad esempio, decidere che le vendite di televisori costituiscono una buona stima dell'attività economica complessiva e applicare un modello di cui è stato eseguito il training sulle vendite di televisori ai dati economici generali.  
  
 In SQL Server Data mining si esegue la stima incrociata utilizzando il parametro REPLACE_MODEL_CASES all'interno degli argomenti della funzione [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
 Nell'attività successiva verrà illustrato come utilizzare REPLACE_MODEL_CASES. Si utilizzeranno i dati delle vendite mondiali uniti per compilare un modello, quindi si creerà una query di stima che esegue il mapping del modello generale ai dati di sostituzione.  
  
 Presupponendo che a questo punto l'utente abbia acquisito familiarità con la compilazione di modelli di data mining, le istruzioni per la compilazione del modello sono state semplificate.  
  
#### <a name="to-build-a-mining-structure-and-mining-model-using-the-aggregated-data"></a>Per compilare una struttura e un modello di data mining utilizzando i dati aggregati  
  
1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **strutture di data mining**e scegliere **nuova struttura di data** mining per avviare la creazione guidata modello di data mining.  
  
2.  Nella Creazione guidata modello di data mining effettuare le seguenti selezioni:  
  
    -   Algoritmo: Microsoft Time Series  
  
    -   Utilizzare l'origine dati compilata precedentemente in questa lezione avanzata come origine per il modello. Vedere [Advanced Time Series predictions &#40;Intermediate Data mining Tutorial&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md).  
  
         Vista origine dati:`AllRegions`  
  
    -   Scegliere le colonne seguenti per le chiavi della serie e temporale:  
  
         Chiave temporale: ReportingDate  
  
         Chiave: area  
  
    -   Scegliere le colonne seguenti per `Input` e `Predict`:  
  
         SumQty  
  
         SumAmt  
  
         AvgAmt  
  
         AvgQty  
  
    -   Per **Nome struttura di data mining**, digitare:`All Regions`  
  
    -   Per **nome modello di data mining**, digitare:`All Regions`  
  
3.  Elaborare la nuova struttura e il nuovo modello.  
  
#### <a name="to-build-the-prediction-query-and-map-the-replacement-data"></a>Per compilare la query di stima ed eseguire il mapping dei dati di sostituzione  
  
1.  Se il modello non è già aperto, fare doppio clic sulla struttura AllRegions e in Progettazione modelli di data mining fare clic sulla scheda **Stima modello di data mining** .  
  
2.  Nel riquadro **modello di data mining** il modello AllRegions dovrebbe essere già selezionato. Se non è selezionata, fare clic su **Seleziona modello**, quindi selezionare il modello AllRegions.  
  
3.  Nel riquadro **Seleziona tabella/** e di input fare clic su **Seleziona tabella del case**.  
  
4.  Nella finestra di dialogo **Seleziona tabella** impostare l'origine dati su T1000 Pacific Region, quindi fare clic su **OK**.  
  
5.  Fare clic con il pulsante destro del mouse sulla linea di join tra il modello di data mining e i dati di input e scegliere **modifica connessioni**. Eseguire il mapping dei dati nella vista origine dati al modello come segue:  
  
    1.  Verificare che sia stato eseguito il mapping della colonna ReportingDate nel modello di data mining alla colonna ReportingDate nei dati di input.  
  
    2.  Nella finestra di dialogo **Modifica mapping** , nella riga della colonna del modello AvgQty, fare clic in **colonna tabella** , quindi selezionare T1000 Pacific. Quantity. Fare clic su **OK**.  
  
         Con questo passaggio viene eseguito il mapping della colonna creata nel modello per stimare la quantità media in base ai dati effettivi dalla serie T1000 per la quantità delle vendite.  
  
    3.  Non eseguire il mapping dell'area della colonna nel modello a una colonna di input.  
  
         Poiché il modello ha aggregato i dati in tutte le serie, non è presente alcuna corrispondenza per i valori della serie come T1000 Pacific e viene generato un errore quando viene eseguita la query di stima.  
  
6.  A questo punto si compilerà la query di stima.  
  
     Aggiungere innanzitutto una colonna ai risultati in cui viene restituita l'etichetta AllRegions dal modello insieme alle stime. In questo modo si saprà che i risultati sono basati sul modello generale.  
  
    1.  Nella griglia fare clic sulla prima riga vuota, in **origine**, quindi selezionare modello di data mining AllRegions.  
  
    2.  Per **campo**selezionare Region (area).  
  
    3.  Per **alias**digitare **Model used**.  
  
7.  Aggiungere quindi un'altra etichetta ai risultati in modo da visualizzare le serie a cui si riferisce la stima.  
  
    1.  Fare clic su una riga vuota, quindi in **origine**selezionare **espressione personalizzata**.  
  
    2.  Nella colonna **alias** digitare **ModelRegion**.  
  
    3.  Nella colonna **criteri/argomento** Digitare `'T1000 Pacific'`.  
  
8.  A questo punto si configurerà la funzione di stima incrociata.  
  
    1.  Fare clic su una riga vuota, quindi in **origine**selezionare **funzione di stima**.  
  
    2.  Nella colonna **campo** selezionare **PredictTimeSeries**.  
  
    3.  Per **alias**digitare **valori stimati**.  
  
    4.  Trascinare il campo AvgQty dal riquadro **modello di data mining** nella colonna **criteri/argomento** utilizzando l'operazione di trascinamento della selezione.  
  
    5.  Nella colonna **criteri/argomento** , dopo il nome del campo, digitare il testo seguente:`,5, REPLACE_MODEL_CASES`  
  
         Il testo completo della casella di testo **criteri/argomento** dovrebbe essere il seguente:`[AllRegions].[AvgQty],5,REPLACE_MODEL_CASES`  
  
9. Fare clic su **risultati**.  
  
## <a name="creating-the-cross-prediction-query-in-dmx"></a>Creazione della query di stima incrociata in DMX  
 È possibile che si sia notato un problema durante la stima incrociata, ovvero che per applicare il modello generale a una serie di dati diversa, ad esempio il modello del prodotto T1000 nell'area America del Nord, è necessario creare una query diversa per ogni serie per poter eseguire il mapping di ogni set di input al modello.  
  
 Anziché compilare la query nella finestra di progettazione, è tuttavia possibile passare a vista DMX e modificare l'istruzione DMX creata. Ad esempio, l'istruzione DMX seguente rappresenta la query che è stata appena compilata:  
  
```  
SELECT  
      ([All Regions].[Region]) as [Model Used],  
      ('T-1000 Pacific') as [ModelRegion],  
      (PredictTimeSeries([All Regions].[Avg Qty],5, REPLACE_MODEL_CASES)) as [Predicted Quantity]  
     FROM [All Regions]  
PREDICTION JOIN  
    OPENQUERY([Adventure Works DW2003R2], 'SELECT [ReportingDate] FROM  
      (  
       SELECT  ReportingDate, ModelRegion, Quantity, Amount   
       FROM dbo.vTimeSeries   
       WHERE (ModelRegion = N''T1000 Pacific'')  
       ) as [T1000 Pacific]    ')   
    AS t  
ON   
[All Regions].[Reporting Date] = t.[ReportingDate]   
AND   
[All Regions].[Avg Qty] = t.[Quantity]  
```  
  
 Per applicare questo codice a un modello diverso, è sufficiente modificare l'istruzione della query in modo da sostituire la condizione di filtro e aggiornare le etichette associate a ogni risultato.  
  
 Se ad esempio si modificano le condizioni di filtro e le etichette delle colonne sostituendo "Pacific" con "America del Nord", si otterranno stime per il prodotto T1000 in America del Nord, sulla base degli schemi nel modello generale.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Confronto delle stime per i modelli di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Esempi di query sul modello Time Series](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
