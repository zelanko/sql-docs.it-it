---
title: Tempo di stime basate su serie utilizzando dati aggiornati (esercitazione intermedia sul Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: af73681d-ce1c-4b6e-b195-6df3d2fb5275
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2017defaba74071b1a12bee14a5d8907e4c71cda
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63067557"
---
# <a name="time-series-predictions-using-updated-data-intermediate-data-mining-tutorial"></a>Stime basate su serie temporali utilizzando dati aggiornati (Esercitazione intermedia sul data mining)
    
## <a name="creating-predictions-using-the-extended-sales-data"></a>Creazione di stime tramite dati di vendita estesi  
 In questa lezione verrà creata una query di stima che aggiunge i nuovi dati di vendita al modello. Estendendo il modello con nuovi dati, è possibile ottenere stime aggiornate che includono i punti dati più recenti.  
  
 La creazione di stime basate su serie temporali che utilizzano nuovi dati è semplice: sufficiente aggiungere il parametro EXTEND_MODEL_CASES per il [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx) funzione, specificare l'origine dei nuovi dati e specificare quante si desidera ottenere stime.  
  
> [!WARNING]  
>  Il parametro EXTEND_MODEL_CASES è facoltativo. Per impostazione predefinita, il modello viene esteso ogni volta che si crea una query di stima basata su serie temporali mediante l'unione in join di nuovi dati come input.  
  
#### <a name="to-build-the-prediction-query-and-add-new-data"></a>Per compilare la query di stima ed aggiungere nuovi dati  
  
1.  Se il modello non è già aperto, fare doppio clic sulla struttura di previsione e Progettazione modelli di Data Mining, scegliere il **stima modello di Data Mining** scheda.  
  
2.  Nel **modello di Data Mining** riquadro, il modello Forecasting dovrebbe essere già selezionato. Se non è selezionato, fare clic su **Seleziona modello**e quindi selezionare il modello di previsione.  
  
3.  Nel **Seleziona tabelle di Input** riquadro, fare clic su **Seleziona tabella del Case**.  
  
4.  Nel **Seleziona tabella del** finestra di dialogo, selezionare l'origine dati, [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)].  
  
     Nell'elenco di viste origine dati, selezionare NewSalesData e quindi fare clic su **OK**.  
  
5.  Il pulsante destro dell'area di progettazione e selezionare **Modifica connessioni**.  
  
6.  Usando il **modifica Mapping** dialogo casella, eseguire il mapping di colonne del modello alle colonne nei dati esterni come indicato di seguito:  
  
    -   Eseguire il mapping alla colonna NewDate nei dati di input la colonna ReportingDate nel modello di data mining.  
  
    -   Eseguire il mapping alla colonna NewAmount nei dati di input la colonna Amount nel modello di data mining.  
  
    -   Mapping della colonna Quantity nel modello di data mining alla colonna NewQty nei dati di input.  
  
    -   Eseguire il mapping alla colonna della serie nei dati di input la colonna ModelRegion nel modello di data mining.  
  
7.  A questo punto si compilerà la query di stima.  
  
     Aggiungere innanzitutto una colonna alla query di stima per restituire la serie a cui si applica la stima.  
  
    1.  Nella griglia, fare clic sulla prima riga vuota, sotto **origine**e quindi selezionare Forecasting.  
  
    2.  Nel **campo** colonna, selezionare Model Region e per **Alias**, tipo `Model Region`.  
  
8.  Aggiungere, quindi, e modificare la funzione di stima.  
  
    1.  Fare clic su una riga vuota, quindi in **origine**, selezionare **funzione di stima**.  
  
    2.  Per la **campo**, selezionare **PredictTimeSeries**.  
  
    3.  Per la **Alias**, digitare **Predicted Values**.  
  
    4.  Trascinare il campo Quantity dal **modello di Data Mining** riquadro le **criteri/argomento** colonna.  
  
    5.  Nel **criteri/argomento** colonna, dopo il nome del campo, digitare il testo seguente:  **5,EXTEND_MODEL_CASES**  
  
         Il testo completo della **criteri/argomento** casella di testo deve essere il seguente: `[Forecasting].[Quantity],5,EXTEND_MODEL_CASES`  
  
9. Fare clic su **risultati** ed esaminare i risultati.  
  
     Le stime iniziano a luglio (il primo intervallo di tempo dopo la fine dei dati originali) e terminano a novembre (il quinto intervallo di tempo dopo la fine dei dati originali).  
  
 È possibile osservare che, per utilizzare questo tipo di query di stima in modo efficiente, è necessario sapere quando terminano i dati precedenti e quanti intervalli di tempo sono presenti nei nuovi dati.  
  
 In questo modello, ad esempio, le serie dei dati originali terminano a giugno e i dati sono per i mesi di luglio, agosto e settembre.  
  
 Le stime che utilizzano EXTEND_MODEL_CASES iniziano sempre alla fine della serie di dati originali. Pertanto, se si desidera ottenere solo le stime per i mesi sconosciuti, è necessario specificare i punti iniziale e finale per la stima. Entrambi valori vengono specificati come un numero di intervalli di tempo che iniziano dalla fine dei dati precedenti.  
  
 Nella procedura riportata di seguito viene illustrato come eseguire questa operazione.  
  
### <a name="change-the-start-and-end-points-of-the-predictions"></a>Modificare i punti iniziale e finale delle stime  
  
1.  Nel generatore delle Query di stima fare clic su **Query** per passare alla vista DMX.  
  
2.  Individuare l'istruzione DMX che contiene la funzione PredictTimeSeries e modificarla come segue:  
  
     `PredictTimeSeries([Forecasting 12].[Quantity],4,6,EXTEND_MODEL_CASES)`  
  
3.  Fare clic su **risultati** ed esaminare i risultati.  
  
     Ora le stime iniziano a ottobre (il quarto intervallo di tempo, contando dalla fine dei dati originali) e terminano a dicembre (il sesto intervallo di tempo, contando dalla fine dei dati originali).  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Tempo di stime basate su serie utilizzando dati di sostituzione &#40;esercitazione intermedia sul Data Mining dei dati&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento tecnico per l'algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Contenuto dei modelli di data mining per i modelli Time Series &#40;Analysis Services - Data mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
