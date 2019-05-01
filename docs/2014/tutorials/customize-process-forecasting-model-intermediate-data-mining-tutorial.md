---
title: Personalizzazione ed elaborazione del modello di previsione (esercitazione intermedia di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4bd25e15-9d9e-4528-b7bc-ccb856643aec
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d2d0e73d1d9a4058ff63320552604b2bfa1bca8a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63249396"
---
# <a name="customizing-and-processing-the-forecasting-model-intermediate-data-mining-tutorial"></a>Personalizzazione ed elaborazione del modello di previsione (Esercitazione intermedia sul data mining)
  L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series fornisce parametri che influiscono sulle modalità di creazione di un modello e di analisi dei dati temporali. La modifica di queste proprietà può influire in modo significativo sul modo in cui il modello di data mining esegue le stime.  
  
 In questa attività dell'esercitazione si modificherà il modello nel modo seguente:  
  
1.  Si personalizzerà il modo in cui il modello gestisce i periodi di tempo aggiungendo un nuovo valore per il *PERIODICITY_HINT* parametro.  
  
2.  Si apprenderà sulle due altri parametri importanti per l'algoritmo Microsoft Time Series: FORECAST_METHOD che consente di controllare il metodo utilizzato per la previsione e PREDICTION_SMOOTHING che consente di personalizzare la combinazione delle stime a breve termine e a lungo termine.  
  
3.  Facoltativamente, si indicherà in che modo si desidera che l'algoritmo attribuisca i valori mancanti.  
  
4.  Dopo avere apportato tutte le modifiche, si procederà alla distribuzione e all'elaborazione del modello.  
  
## <a name="setting-time-series-parameters"></a>Impostazione dei parametri di Time Series  
 **Hint di periodicità**  
  
 Il *PERIODICITY_HINT* parametro fornisce all'algoritmo informazioni sui periodi di tempo aggiuntivi previsti nei dati. Per impostazione predefinita, i modelli Time Series tenteranno di rilevare automaticamente un modello nei dati. Se tuttavia si conosce già il ciclo temporale previsto, l'indicazione di un hint di periodicità può migliorare potenzialmente l'accuratezza del modello. Se si fornisce tuttavia l'hint di periodicità errato, l'accuratezza può diminuire. Di conseguenza, in caso di dubbi sul valore da utilizzare, è preferibile utilizzare il valore predefinito.  
  
 Ad esempio, la vista utilizzata per questo modello aggrega dati di vendita da [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] su base mensile. Ogni intervallo di tempo utilizzato dal modello rappresenta pertanto un mese e tutte le stime saranno anch'esse indicate in termini di mesi. Poiché ci sono 12 mesi in un anno e si prevede che i modelli di vendita ripetano più o meno su base annuale, imposterà il *PERIODICITY_HINT* parametro per `12`, per indicare che 12 intervalli di tempo (mesi) costituiscono uno ciclo di vendite completo.  
  
 **Metodo di previsione**  
  
 Il *FORECAST_METHOD* parametro controlla se l'algoritmo time series è ottimizzato per le stime a breve o a lungo termine. Per impostazione predefinita, il *FORECAST_METHOD* parametro è impostato su MIXED e ciò significa che due diversi algoritmi vengono combinati e bilanciati per fornire risultati ottimali per la stima sia a breve termine e a lungo termine.  
  
 Se tuttavia si desidera utilizzare un algoritmo particolare, è possibile modificare il valore in ARIMA o ARTXP.  
  
 **Visual Studio a lungo termine ponderato. Stime a breve termine**  
  
 È inoltre possibile personalizzare la modalità di combinazione delle stime a lungo e a breve termine tramite il parametro PREDICTION_SMOOTHING. Per impostazione predefinita, questo parametro è impostato su 0,5, che generalmente fornisce il miglior bilanciamento per l'accuratezza complessiva.  
  
#### <a name="to-change-the-algorithm-parameters"></a>Per modificare i parametri dell'algoritmo  
  
1.  Nel **modelli di Data Mining** scheda, fare doppio clic su **Forecasting**e selezionare **imposta parametri algoritmo**.  
  
2.  Nel `PERIODICITY_HINT` riga del **i parametri dell'algoritmo** della finestra di dialogo fare clic sui **valore** colonna, quindi digitare `{12}`, incluse le parentesi graffe.  
  
     Per impostazione predefinita, verrà aggiunto il valore {1}.  
  
3.  Nel `FORECAST_METHOD` di righe, verificare che il **valore** casella di testo è sia vuota o impostata per `MIXED`. Se è stato inserito un valore diverso, digitare `MIXED` per il parametro di ripristinare il valore predefinito.  
  
4.  Nel **PREDICTION_SMOOTHING** righe, verificare che il **valore** casella di testo è sia vuota o impostata su 0,5. Se è stato inserito un valore diverso, fare clic su **valore** e il tipo `0.5` per il parametro di ripristinare il valore predefinito.  
  
    > [!NOTE]  
    >  Il parametro PREDICTION_SMOOTHING è disponibile solo in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise. Non è pertanto possibile visualizzare o modificare il valore di tale parametro in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard. Il comportamento predefinito consiste tuttavia nell'utilizzare entrambi gli algoritmi con un fattore di ponderazione equivalente.  
  
5.  Fare clic su **OK**.  
  
## <a name="handling-missing-data-optional"></a>Gestione di dati mancanti (facoltativo)  
 In diversi casi, è possibile che nei dati di vendita siano presenti gap riempiti con valori Null oppure che un negozio non sia stato in grado di inviare il report prima della scadenza, lasciando una cella vuota alla fine della serie. In questi scenari, in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] viene generato l'errore seguente e il modello non viene elaborato.  
  
 "Errore (Data mining): Timestamp non sincronizzati a partire dalla serie \<nome serie >, del modello di data mining, \<nome modello >. Tutte le serie temporali devono terminare allo stesso contrassegno temporale e i punti dati non possono essere omessi arbitrariamente. Se si imposta il parametro MISSING_VALUE_SUBSTITUTION su Previous o su una costante numerica, i punti dati mancanti verranno aggiunti automaticamente ove possibile."  
  
 Per evitare l'errore, è possibile impostare [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in modo da fornire automaticamente nuovi valori per riempire i gap tramite i metodi seguenti:  
  
-   Utilizzo di un valore medio. La media viene calcolata utilizzando tutti i valori validi nella stessa serie di dati.  
  
-   Utilizzo del valore precedente. È possibile sostituire i valori precedenti di più celle mancanti, ma non è possibile riempire i valori iniziali.  
  
-   Utilizzo di un valore costante fornito dall'utente.  
  
#### <a name="to-specify-that-gaps-be-filled-by-averaging-values"></a>Per specificare che le lacune vengano colmate tramite valori medi  
  
1.  Nel **modelli di Data Mining** scheda, fare doppio clic il **Forecasting** colonna e selezionare **imposta parametri algoritmo**.  
  
2.  Nel **parametri algoritmo** nella finestra di dialogo il **MISSING_VALUE_SUBSTITUTION** riga, fare clic sul **valore** colonna e digitare `Mean`.  
  
## <a name="build-the-model"></a>Compilare il modello  
 Per utilizzare il modello, è necessario distribuirlo a un server ed elaborarlo mediante l'esecuzione di dati di training tramite l'algoritmo.  
  
#### <a name="to-process-the-forecasting-model"></a>Per elaborare il modello di previsione  
  
1.  Nel **modello di Data Mining** dal menu del [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], selezionare **Elabora struttura di Data Mining e tutti i modelli**.  
  
2.  Nella finestra di avviso che chiede se si desidera compilare e distribuire il progetto, fare clic su **Sì**.  
  
3.  Nel **Elabora struttura di Data Mining - Forecasting** della finestra di dialogo fare clic su **eseguire**.  
  
     Il **stato elaborazione** verrà visualizzata la finestra di dialogo per visualizzare le informazioni sull'elaborazione di modelli. L'elaborazione del modello può richiedere alcuni minuti.  
  
4.  Al termine dell'elaborazione, fare clic su **Close** per chiudere il **stato elaborazione** nella finestra di dialogo.  
  
5.  Fare clic su **Close** per uscire dalle **Elabora struttura di Data Mining - Forecasting** nella finestra di dialogo.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Esplorazione del modello di previsione &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento tecnico per l'algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Requisiti e considerazioni sull'elaborazione &#40;data mining&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
