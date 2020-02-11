---
title: Personalizzazione ed elaborazione del modello di previsione (Esercitazione intermedia sul data mining) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63249396"
---
# <a name="customizing-and-processing-the-forecasting-model-intermediate-data-mining-tutorial"></a>Personalizzazione ed elaborazione del modello di previsione (Esercitazione intermedia sul data mining)
  L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series fornisce parametri che influiscono sulle modalità di creazione di un modello e di analisi dei dati temporali. La modifica di queste proprietà può influire in modo significativo sul modo in cui il modello di data mining esegue le stime.  
  
 In questa attività dell'esercitazione si modificherà il modello nel modo seguente:  
  
1.  Si Personalizza il modo in cui il modello gestisce i periodi di tempo aggiungendo un nuovo valore per il parametro *PERIODICITY_HINT* .  
  
2.  Si conosceranno altri due importanti parametri per l'algoritmo Microsoft Time Series: FORECAST_METHOD che consente di controllare il metodo utilizzato per la previsione e PREDICTION_SMOOTHING che consente di personalizzare la combinazione di stime a lungo e breve termine.  
  
3.  Facoltativamente, si indicherà in che modo si desidera che l'algoritmo attribuisca i valori mancanti.  
  
4.  Dopo avere apportato tutte le modifiche, si procederà alla distribuzione e all'elaborazione del modello.  
  
## <a name="setting-time-series-parameters"></a>Impostazione dei parametri di Time Series  
 **Hint di periodicità**  
  
 Il *PERIODICITY_HINT* parametro fornisce all'algoritmo informazioni sui periodi di tempo aggiuntivi che si prevede di visualizzare nei dati. Per impostazione predefinita, i modelli Time Series tenteranno di rilevare automaticamente un modello nei dati. Se tuttavia si conosce già il ciclo temporale previsto, l'indicazione di un hint di periodicità può migliorare potenzialmente l'accuratezza del modello. Se si fornisce tuttavia l'hint di periodicità errato, l'accuratezza può diminuire. Di conseguenza, in caso di dubbi sul valore da utilizzare, è preferibile utilizzare il valore predefinito.  
  
 Ad esempio, la vista utilizzata per questo modello aggrega dati di vendita da [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] su base mensile. Ogni intervallo di tempo utilizzato dal modello rappresenta pertanto un mese e tutte le stime saranno anch'esse indicate in termini di mesi. Poiché sono presenti 12 mesi in un anno e si prevede che i modelli di vendita vengano ripetuti più o meno su base annuale, impostare ** il parametro PERIODICITY_HINT `12`su per indicare che 12 intervalli di tempo (mesi) costituiscono un ciclo di vendita completo.  
  
 **Metodo di previsione**  
  
 Il parametro *FORECAST_METHOD* controlla se l'algoritmo Time Series è ottimizzato per le stime a breve o a lungo termine. Per impostazione predefinita, il parametro *FORECAST_METHOD* è impostato su Mixed, il che significa che due algoritmi diversi vengono combinati e bilanciati per fornire risultati validi sia per la stima a breve termine che per quella a lungo termine.  
  
 Se tuttavia si desidera utilizzare un algoritmo particolare, è possibile modificare il valore in ARIMA o ARTXP.  
  
 **Ponderazione delle stime a lungo termine e a breve termine**  
  
 È inoltre possibile personalizzare la modalità di combinazione delle stime a lungo e a breve termine tramite il parametro PREDICTION_SMOOTHING. Per impostazione predefinita, questo parametro è impostato su 0,5, che generalmente fornisce il miglior bilanciamento per l'accuratezza complessiva.  
  
#### <a name="to-change-the-algorithm-parameters"></a>Per modificare i parametri dell'algoritmo  
  
1.  Nella scheda **modelli di data mining** fare clic con il pulsante destro del mouse su **previsione**, quindi scegliere **Imposta parametri algoritmo**.  
  
2.  Nella `PERIODICITY_HINT` riga della finestra di dialogo **parametri algoritmo** fare clic sulla colonna **valore** , quindi digitare `{12}`, incluse le parentesi graffe.  
  
     Per impostazione predefinita, verrà aggiunto il valore {1}.  
  
3.  Nella `FORECAST_METHOD` riga verificare che la casella di testo **valore** sia vuota o impostata su `MIXED`. Se è stato inserito un valore diverso, digitare `MIXED` per ripristinare il valore predefinito del parametro.  
  
4.  Nella riga **PREDICTION_SMOOTHING** verificare che la casella di testo **valore** sia vuota o impostata su 0,5. Se è stato immesso un valore diverso, **** fare clic su `0.5` valore e digitare per ripristinare il valore predefinito del parametro.  
  
    > [!NOTE]  
    >  Il parametro PREDICTION_SMOOTHING è disponibile solo in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise. Non è pertanto possibile visualizzare o modificare il valore di tale parametro in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard. Il comportamento predefinito consiste tuttavia nell'utilizzare entrambi gli algoritmi con un fattore di ponderazione equivalente.  
  
5.  Fare clic su **OK**.  
  
## <a name="handling-missing-data-optional"></a>Gestione di dati mancanti (facoltativo)  
 In diversi casi, è possibile che nei dati di vendita siano presenti gap riempiti con valori Null oppure che un negozio non sia stato in grado di inviare il report prima della scadenza, lasciando una cella vuota alla fine della serie. In questi scenari, in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] viene generato l'errore seguente e il modello non viene elaborato.  
  
 "Errore (data mining): timestamp non sincronizzati a partire dal \<nome della serie di serie>, del modello \<di data mining, nome modello>. Tutte le serie temporali devono terminare allo stesso contrassegno temporale e i punti dati non possono essere omessi arbitrariamente. Se si imposta il parametro MISSING_VALUE_SUBSTITUTION su Previous o su una costante numerica, i punti dati mancanti verranno aggiunti automaticamente ove possibile."  
  
 Per evitare l'errore, è possibile impostare [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in modo da fornire automaticamente nuovi valori per riempire i gap tramite i metodi seguenti:  
  
-   Utilizzo di un valore medio. La media viene calcolata utilizzando tutti i valori validi nella stessa serie di dati.  
  
-   Utilizzo del valore precedente. È possibile sostituire i valori precedenti di più celle mancanti, ma non è possibile riempire i valori iniziali.  
  
-   Utilizzo di un valore costante fornito dall'utente.  
  
#### <a name="to-specify-that-gaps-be-filled-by-averaging-values"></a>Per specificare che le lacune vengano colmate tramite valori medi  
  
1.  Nella scheda **modelli di data mining** fare clic con il pulsante destro del mouse sulla colonna **previsione** , quindi scegliere **Imposta parametri algoritmo**.  
  
2.  Nella **MISSING_VALUE_SUBSTITUTION** riga della finestra di dialogo **parametri algoritmo** fare clic sulla colonna **valore** , quindi digitare `Mean`.  
  
## <a name="build-the-model"></a>Compilare il modello  
 Per utilizzare il modello, è necessario distribuirlo a un server ed elaborarlo mediante l'esecuzione di dati di training tramite l'algoritmo.  
  
#### <a name="to-process-the-forecasting-model"></a>Per elaborare il modello di previsione  
  
1.  Scegliere **Elabora struttura di data mining e tutti i modelli**dal menu modello di [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] **data mining** .  
  
2.  Quando si chiede se si desidera compilare e distribuire il progetto, fare clic su **Sì**.  
  
3.  Nella finestra di dialogo **Elabora struttura di data mining-previsione** , fare clic su **Esegui**.  
  
     Verrà visualizzata la finestra di dialogo **stato** elaborazione per visualizzare le informazioni sull'elaborazione del modello. L'elaborazione del modello può richiedere alcuni minuti.  
  
4.  Al termine dell'elaborazione, fare clic su **Chiudi** per uscire dalla finestra di dialogo **stato** elaborazione.  
  
5.  Fare di nuovo clic su **Chiudi per chiudere** la finestra di dialogo **Elabora struttura di data mining-previsione** .  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Esplorazione del modello di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento tecnico per l'algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Requisiti e considerazioni sull'elaborazione &#40;&#41;di data mining](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
