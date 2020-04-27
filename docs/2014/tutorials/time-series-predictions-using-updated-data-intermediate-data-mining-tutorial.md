---
title: Stime basate su serie temporali con dati aggiornati (Esercitazione intermedia sul data mining) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067557"
---
# <a name="time-series-predictions-using-updated-data-intermediate-data-mining-tutorial"></a>Stime basate su serie temporali utilizzando dati aggiornati (Esercitazione intermedia sul data mining)
    
## <a name="creating-predictions-using-the-extended-sales-data"></a>Creazione di stime tramite dati di vendita estesi  
 In questa lezione verrà creata una query di stima che aggiunge i nuovi dati di vendita al modello. Estendendo il modello con nuovi dati, è possibile ottenere stime aggiornate che includono i punti dati più recenti.  
  
 La creazione di stime basate su serie temporali che utilizzano nuovi dati è semplice: è sufficiente aggiungere il parametro EXTEND_MODEL_CASES alla funzione [&#41;DMX PredictTimeSeries &#40;](/sql/dmx/predicttimeseries-dmx) , specificare l'origine dei nuovi dati e specificare il numero di stime che si desidera ottenere.  
  
> [!WARNING]  
>  Il parametro EXTEND_MODEL_CASES è facoltativo. Per impostazione predefinita, il modello viene esteso ogni volta che si crea una query di stima basata su serie temporali mediante l'unione in join di nuovi dati come input.  
  
#### <a name="to-build-the-prediction-query-and-add-new-data"></a>Per compilare la query di stima ed aggiungere nuovi dati  
  
1.  Se il modello non è già aperto, fare doppio clic sulla struttura di previsione e in Progettazione modelli di data mining fare clic sulla scheda **Stima modello di data mining** .  
  
2.  Nel riquadro **modello di data mining** è necessario che la previsione del modello sia già selezionata. Se non è selezionata, fare clic su **Seleziona modello**, quindi selezionare il modello, previsione.  
  
3.  Nel riquadro **Seleziona tabella/** e di input fare clic su **Seleziona tabella del case**.  
  
4.  Nella finestra di dialogo **Seleziona tabella** selezionare l'origine dati, [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)].  
  
     Dall'elenco di viste origine dati selezionare NewSalesData e quindi fare clic su **OK**.  
  
5.  Fare clic con il pulsante destro del mouse sulla superficie dell'area di progettazione e scegliere **modifica connessioni**.  
  
6.  Utilizzando la finestra di dialogo **Modifica mapping** , eseguire il mapping delle colonne del modello alle colonne nei dati esterni come indicato di seguito:  
  
    -   Eseguire il mapping della colonna ReportingDate nel modello di data mining alla colonna NewDate nei dati di input.  
  
    -   Eseguire il mapping della colonna Amount nel modello di data mining alla colonna NewAmount nei dati di input.  
  
    -   Eseguire il mapping della colonna Quantity nel modello di data mining alla colonna NewQty nei dati di input.  
  
    -   Eseguire il mapping della colonna ModelRegion nel modello di data mining alla colonna serie nei dati di input.  
  
7.  A questo punto si compilerà la query di stima.  
  
     Aggiungere innanzitutto una colonna alla query di stima per restituire la serie a cui si applica la stima.  
  
    1.  Nella griglia fare clic sulla prima riga vuota, in **origine**, quindi selezionare previsioni.  
  
    2.  Nella colonna **campo** selezionare area del modello e per **alias**digitare `Model Region`.  
  
8.  Aggiungere, quindi, e modificare la funzione di stima.  
  
    1.  Fare clic su una riga vuota, quindi in **origine**selezionare **funzione di stima**.  
  
    2.  In **campo**selezionare **PredictTimeSeries**.  
  
    3.  Per **alias**digitare **valori stimati**.  
  
    4.  Trascinare la quantità di campo dal riquadro **modello di data mining** nella colonna **criteri/argomento** .  
  
    5.  Nella colonna **criteri/argomento** , dopo il nome del campo, digitare il testo seguente: **5 EXTEND_MODEL_CASES**  
  
         Il testo completo della casella di testo **criteri/argomento** dovrebbe essere il seguente:`[Forecasting].[Quantity],5,EXTEND_MODEL_CASES`  
  
9. Fare clic su **risultati** ed esaminare i risultati.  
  
     Le stime iniziano a luglio (il primo intervallo di tempo dopo la fine dei dati originali) e terminano a novembre (il quinto intervallo di tempo dopo la fine dei dati originali).  
  
 È possibile osservare che, per utilizzare questo tipo di query di stima in modo efficiente, è necessario sapere quando terminano i dati precedenti e quanti intervalli di tempo sono presenti nei nuovi dati.  
  
 In questo modello, ad esempio, le serie dei dati originali terminano a giugno e i dati sono per i mesi di luglio, agosto e settembre.  
  
 Le stime che utilizzano EXTEND_MODEL_CASES iniziano sempre alla fine della serie di dati originali. Pertanto, se si desidera ottenere solo le stime per i mesi sconosciuti, è necessario specificare i punti iniziale e finale per la stima. Entrambi valori vengono specificati come un numero di intervalli di tempo che iniziano dalla fine dei dati precedenti.  
  
 Nella procedura riportata di seguito viene illustrato come eseguire questa operazione.  
  
### <a name="change-the-start-and-end-points-of-the-predictions"></a>Modificare i punti iniziale e finale delle stime  
  
1.  In Generatore di query di stima fare clic su **query** per passare alla visualizzazione DMX.  
  
2.  Individuare l'istruzione DMX che contiene la funzione PredictTimeSeries e modificarla come segue:  
  
     `PredictTimeSeries([Forecasting 12].[Quantity],4,6,EXTEND_MODEL_CASES)`  
  
3.  Fare clic su **risultati** ed esaminare i risultati.  
  
     Ora le stime iniziano a ottobre (il quarto intervallo di tempo, contando dalla fine dei dati originali) e terminano a dicembre (il sesto intervallo di tempo, contando dalla fine dei dati originali).  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Stime basate su serie temporali che utilizzano dati sostitutivi &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Riferimento tecnico per l'algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Contenuto dei modelli di data mining per i modelli Time Series &#40;Analysis Services - Data mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
