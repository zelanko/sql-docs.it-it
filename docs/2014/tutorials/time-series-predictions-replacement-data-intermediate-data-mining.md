---
title: Tempo di stime basate su serie utilizzando dati di sostituzione (esercitazione intermedia sul Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a23a6e1d-1d49-41ea-8314-925dc8e4df5e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2b7c23bec5925dbc33d2db7a547daf02f42a6cd7
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52419042"
---
# <a name="time-series-predictions-using-replacement-data-intermediate-data-mining-tutorial"></a>Stime basate su serie temporali utilizzando dati di sostituzione (Esercitazione intermedia sul data mining)
  In questa attività verrà compilato un nuovo modello basato sui dati di vendita mondiali. Verrà quindi creata una query di stima che applica il modello delle vendite mondiali a una delle singole aree.  
  
## <a name="building-a-general-model"></a>Compilazione di un modello generale  
 L'analisi dei risultati del modello di data mining originale ha rivelato differenze rilevanti tra aree e linee di prodotti. Ad esempio, le vendite in America del nord sono state elevate per il modello M200, mentre le vendite del modello T1000 non sono andate altrettanto bene. Tuttavia, l'analisi è complicata dal fatto che alcune serie non contenevano molti dati o dati in un altro punto nel tempo. Alcuni dati erano inoltre mancanti.  
  
 ![Serie di stima delle quantità M200 e T1000](../../2014/tutorials/media/6series-defaultforecasting.gif "serie stima delle quantità M200 e T1000")  
  
 Per risolvere alcuni dei problemi di qualità dei dati, si uniranno i dati dalle vendite di tutto il mondo e si utilizzerà tale set di tendenze di vendita generali per compilare un modello che possa essere applicato per stimare le vendite future in tutte le aree.  
  
 Quando si creano stime, si utilizza il modello generato eseguendo il training sui dati di vendita mondiali, sostituendo tuttavia i punti dati cronologici con i dati di vendita di ogni singola area. In tal modo la forma della tendenza viene mantenuta, ma i valori stimati vengono allineati con le cifre delle vendite cronologiche per ogni area e modello.  
  
## <a name="performing-cross-prediction-with-a-time-series-model"></a>Esecuzione di stime incrociate con un modello Time Series  
 Il processo che prevede l'utilizzo dei dati di una serie per stimare le tendenze in un'altra serie è detto stima incrociata. È possibile utilizzare la stima incrociata in molti scenari, ad esempio, decidere che le vendite di televisori costituiscono una buona stima dell'attività economica complessiva e applicare un modello di cui è stato eseguito il training sulle vendite di televisori ai dati economici generali.  
  
 In SQL Server Data Mining, eseguire una stima incrociata usando il parametro REPLACE_MODEL_CASES all'interno di argomenti della funzione [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
 Nell'attività successiva verrà illustrato come utilizzare REPLACE_MODEL_CASES. Si utilizzeranno i dati delle vendite mondiali uniti per compilare un modello, quindi si creerà una query di stima che esegue il mapping del modello generale ai dati di sostituzione.  
  
 Presupponendo che a questo punto l'utente abbia acquisito familiarità con la compilazione di modelli di data mining, le istruzioni per la compilazione del modello sono state semplificate.  
  
#### <a name="to-build-a-mining-structure-and-mining-model-using-the-aggregated-data"></a>Per compilare una struttura e un modello di data mining utilizzando i dati aggregati  
  
1.  Nelle **Esplora soluzioni**, fare doppio clic su **strutture di Data Mining**, quindi selezionare **nuova struttura di Data Mining** per avviare Creazione guidata di Data Mining.  
  
2.  Nella Creazione guidata modello di data mining effettuare le seguenti selezioni:  
  
    -   Algoritmo: Microsoft Time Series  
  
    -   Utilizzare l'origine dati compilata precedentemente in questa lezione avanzata come origine per il modello. Visualizzare [stime basate su serie temporali avanzate &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md).  
  
         Vista origine dati: `AllRegions`  
  
    -   Scegliere le colonne seguenti per le chiavi della serie e temporale:  
  
         Chiave temporale: ReportingDate  
  
         Chiave: Region  
  
    -   Scegliere le colonne seguenti per `Input` e `Predict`:  
  
         SumQty  
  
         SumAmt  
  
         AvgAmt  
  
         AvgQty  
  
    -   Per la **nome della struttura di Data Mining**, tipo: `All Regions`  
  
    -   Per la **nome del modello di Data Mining**, tipo: `All Regions`  
  
3.  Elaborare la nuova struttura e il nuovo modello.  
  
#### <a name="to-build-the-prediction-query-and-map-the-replacement-data"></a>Per compilare la query di stima ed eseguire il mapping dei dati di sostituzione  
  
1.  Se il modello non è già aperto, fare doppio clic sulla struttura AllRegions e Progettazione modelli di Data Mining, scegliere il **stima modello di Data Mining** scheda.  
  
2.  Nel **modello di Data Mining** riquadro, il modello AllRegions dovrebbe essere già selezionato. Se non è selezionato, fare clic su **Seleziona modello**e quindi selezionare il modello AllRegions.  
  
3.  Nel **Seleziona tabelle di Input** riquadro, fare clic su **Seleziona tabella del Case**.  
  
4.  Nel **Seleziona tabella del** finestra di dialogo, modificare i dati di origine su T1000 Pacific Region e quindi fare clic su **OK**.  
  
5.  Fare clic sulla linea di join tra il modello di data mining e i dati di input e selezionare **Modifica connessioni**. Eseguire il mapping dei dati nella vista origine dati al modello come segue:  
  
    1.  Verificare che la colonna ReportingDate nel modello di data mining viene eseguito il mapping alla colonna ReportingDate nei dati di input.  
  
    2.  Nel **modifica Mapping** finestra di dialogo, nella riga per la colonna del modello AvgQty, fare clic sotto **colonna della tabella** e selezionare T1000 Pacific. Fare clic su **OK**.  
  
         Con questo passaggio viene eseguito il mapping della colonna creata nel modello per stimare la quantità media in base ai dati effettivi dalla serie T1000 per la quantità delle vendite.  
  
    3.  L'area colonna del modello non vengono mappati a qualsiasi colonna di input.  
  
         Poiché il modello ha aggregato i dati in tutte le serie, non è presente alcuna corrispondenza per i valori della serie come T1000 Pacific e viene generato un errore quando viene eseguita la query di stima.  
  
6.  A questo punto si compilerà la query di stima.  
  
     Aggiungere innanzitutto una colonna ai risultati in cui viene restituita l'etichetta AllRegions dal modello insieme alle stime. In questo modo si saprà che i risultati sono basati sul modello generale.  
  
    1.  Nella griglia, fare clic sulla prima riga vuota, sotto **origine**e quindi selezionare il modello di data mining AllRegions.  
  
    2.  Per la **campo**, selezionare l'area.  
  
    3.  Per la **Alias**, digitare **modello usato**.  
  
7.  Aggiungere quindi un'altra etichetta ai risultati in modo da visualizzare le serie a cui si riferisce la stima.  
  
    1.  Fare clic su una riga vuota, quindi in **origine**, selezionare **espressione personalizzata**.  
  
    2.  Nel **Alias** colonna, digitare **ModelRegion**.  
  
    3.  Nel **criteri/argomento** colonna, tipo `'T1000 Pacific'`.  
  
8.  A questo punto si configurerà la funzione di stima incrociata.  
  
    1.  Fare clic su una riga vuota, quindi in **origine**, selezionare **funzione di stima**.  
  
    2.  Nel **campo** colonna, selezionare **PredictTimeSeries**.  
  
    3.  Per la **Alias**, digitare **Predicted Values**.  
  
    4.  Trascinare il campo AvgQty dal **modello di Data Mining** riquadro le **criteri/argomento** colonna mediante un'operazione di trascinamento della selezione.  
  
    5.  Nel **criteri/argomento** colonna, dopo il nome del campo, digitare il testo seguente: `,5, REPLACE_MODEL_CASES`  
  
         Il testo completo della **criteri/argomento** casella di testo deve essere il seguente: `[AllRegions].[AvgQty],5,REPLACE_MODEL_CASES`  
  
9. Fare clic su **risultati**.  
  
## <a name="creating-the-cross-prediction-query-in-dmx"></a>Creazione della query di stima incrociata in DMX  
 È possibile che si sia notato un problema durante la stima incrociata, ovvero che per applicare il modello generale a una serie di dati diversa, ad esempio il modello del prodotto T1000 nell'area North America, è necessario creare una query diversa per ogni serie per poter eseguire il mapping di ogni set di input al modello.  
  
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
  
 Se ad esempio si modificano le condizioni di filtro e le etichette delle colonne sostituendo "Pacific" con "North America", si otterranno stime per il prodotto T1000 in Nord America, sulla base degli schemi nel modello generale.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Confronto delle stime per i modelli di previsione &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempi di query sul modello di serie temporale](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
