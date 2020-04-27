---
title: Creazione di stime basate su serie temporali (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: fb22cffa-ac99-4d34-ac4a-9c93068e33e8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ca1aa4022931c78f6139a8058c05adc707af5e77
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63313886"
---
# <a name="creating-time-series-predictions-intermediate-data-mining-tutorial"></a>Creazione di stime basate su serie temporali (Esercitazione intermedia sul data mining)
  Nelle attività precedenti di questa lezione è stato creato un modello Time Series e sono stati esplorati i risultati. Per impostazione predefinita, in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] viene sempre creato un set di cinque (5) stime per un modello Time Series e i valori stimati vengono visualizzati come parte del grafico di previsione. È tuttavia possibile creare previsioni compilando query di stima DMX (Data Mining Extensions).  
  
 In questa attività verrà creata una query di stima che genera le stesse stime esaminate in precedenza nel visualizzatore. Questa attività presuppone che siano già state completate le lezioni dell'Esercitazione di base sul data mining e che si abbia familiarità con l'utilizzo del generatore delle query di stima. Verrà ora illustrato come creare query specifiche per i modelli Time Series.  
  
## <a name="creating-time-series-predictions"></a>Creazione di stime basate su serie temporali  
 In genere il primo passaggio per creare una query di stima consiste nel selezionare un modello di data mining e una tabella di input. Tuttavia, un modello Time Series non richiede input aggiuntivi per una stima normale. Non è pertanto necessario specificare una nuova origine dati durante l'esecuzione di stime, a meno che non si aggiungano o sostituiscano dati nel modello.  
  
 Ai fini di questa lezione è necessario specificare il numero di intervalli per la stima. È inoltre possibile specificare il nome della serie per ottenere una stima per una determinata combinazione di prodotto e area.  
  
#### <a name="to-select-a-model-and-input-table"></a>Per selezionare un modello e una tabella di input  
  
1.  Nella scheda **Stima modello** di data mining di progettazione modelli di data mining fare clic su **Seleziona modello**nella casella **modello di data mining** .  
  
2.  Nella finestra di dialogo **Seleziona modello di data mining** espandere la struttura Forecasting, selezionare il modello **Forecasting** dall'elenco, quindi fare clic su **OK**.  
  
3.  Ignorare la casella **Seleziona tabella/** e di input.  
  
    > [!NOTE]  
    >  Per i modelli Time Series non è necessario specificare un input distinto, a meno che non si stia eseguendo una stima incrociata.  
  
4.  Nella colonna **origine** , nella griglia della scheda **Stima modello di data mining** , fare clic sulla cella nella prima riga vuota, quindi selezionare **modello di data mining Forecasting**.  
  
5.  Nella colonna **campo** selezionare area del **modello**.  
  
     L'identificatore della serie verrà aggiunto alla query di stima per indicare a quale combinazione di modello e area si applica la stima.  
  
6.  Fare clic sulla riga vuota successiva nella colonna **origine** , quindi selezionare **funzione di stima**.  
  
7.  Nella colonna **campo** selezionare **PredictTimeSeries**.  
  
    > [!NOTE]  
    >  Con i modelli Time Series è inoltre possibile utilizzare la funzione `Predict`. Per impostazione predefinita, tuttavia, la funzione Predict crea una sola stima per ogni serie. Pertanto, per specificare più passaggi di stima, è necessario utilizzare la funzione **PredictTimeSeries** .  
  
8.  Nel riquadro **modello di data mining** selezionare la colonna modello di data mining **Amount.** Trascinare Amount nella casella **criteri/argomento** per la funzione **PredictTimeSeries** aggiunta in precedenza.  
  
9. Fare clic sulla casella **criteri/argomento** e digitare una virgola, seguita da **5**, dopo il nome del campo.  
  
     Il testo nella casella **criteri/argomento** dovrebbe ora visualizzare quanto segue:  
  
     `[Forecasting].[Amount],5`  
  
10. Nella colonna **alias** Digitare `PredictAmount`.  
  
11. Fare clic sulla riga vuota successiva nella colonna **origine** , quindi selezionare di nuovo **funzione di stima** .  
  
12. Nella colonna **campo** selezionare **PredictTimeSeries**.  
  
13. Nel riquadro **modello di data mining** selezionare la colonna Quantity e quindi trascinarla nella casella **criteri/argomento** della seconda funzione **PredictTimeSeries** .  
  
14. Fare clic sulla casella **criteri/argomento** e digitare una virgola, seguita da **5**, dopo il nome del campo.  
  
     Il testo nella casella **criteri/argomento** dovrebbe ora visualizzare quanto segue:  
  
     `[Forecasting].[ Quantity],5`  
  
15. Nella colonna **alias** Digitare `PredictQuantity`.  
  
16. Fare clic su **passa alla visualizzazione risultati della query**.  
  
     I risultati della query verranno visualizzati in formato tabulare.  
  
 Tenere presente che sono stati creati tre tipi diversi di risultati nel generatore di query, uno che utilizza i valori di una colonna e due che ottengono i valori stimati da una funzione di stima. I risultati della query contengono pertanto tre colonne distinte. La prima colonna contiene l'elenco di combinazioni di prodotto e area, mentre la seconda e la terza contengono ciascuna una tabella nidificata dei risultati della stima. Ogni tabella nidificata contiene intervalli temporali e valori stimati, come nella tabella di esempio seguente:  
  
 Risultati di esempio (le quantità sono troncate a due posizioni decimali):  
  
 **M200 Europe PredictAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|7/25/2008|99978,00|  
|8/25/2008|145575,07|  
|9/25/2008|116835,19|  
|10/25/2008|116537,38|  
|11/25/2008|107760,55|  
  
 **M200 Europe PredictQuantity**  
  
|$TIME|Quantità|  
|-----------|--------------|  
|7/25/2008|52|  
|8/25/2008|67|  
|9/25/2008|58|  
|10/25/2008|57|  
|11/25/2008|54|  
  
 **M200 America del Nord-PredictAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|7/25/2008|348533,93|  
|8/25/2008|340097,98|  
|9/25/2008|257986,19|  
|10/25/2008|374658,24|  
|11/25/2008|379241,44|  
  
 **M200 America del Nord-PredictQuantity**  
  
|$TIME|Quantità|  
|-----------|--------------|  
|7/25/2008|272|  
|8/25/2008|152|  
|9/25/2008|250|  
|10/25/2008|181|  
|11/25/2008|290|  
  
> [!WARNING]  
>  Le date utilizzate nel database di esempio sono state modificate per questa versione. Se si utilizza una versione precedente dei dati di esempio, è possibile che vengano visualizzati risultati diversi.  
  
## <a name="saving-the-prediction-results"></a>Salvataggio dei risultati della stima  
 Le opzioni per l'utilizzo dei risultati della stima sono molte. È possibile rendere i risultati bidimensionali, copiare i dati dalla vista dei risultati e incollarli in un foglio di lavoro di Excel o in un altro file.  
  
 Per semplificare il processo di salvataggio dei risultati, in Data Mining Designer è inoltre possibile salvare i dati in una vista origine dati. La funzionalità per salvare risultati in una vista origine dati è disponibile solo in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. I risultati possono essere archiviati solo in un formato bidimensionale.  
  
#### <a name="to-flatten-the-results-in-the-results-pane"></a>Per convertire i dati in formato flat nel riquadro Risultati  
  
1.  In Generatore di query di stima fare clic su **passa alla visualizzazione di progettazione query**.  
  
     La visualizzazione cambierà per consentire la modifica manuale del testo della query DMX.  
  
2.  Digitare la parola chiave `FLATTENED` dopo la parola chiave `SELECT`. Il testo completo della query dovrebbe risultare analogo al seguente:  
  
    ```  
    SELECT FLATTENED  
      [Forecasting].[Model Region],  
      (PredictTimeSeries([Forecasting].[Amount],5)) as [PredictAmount],  
      (PredictTimeSeries([Forecasting].[Quantity],5)) as [PredictQuantity]  
    FROM  
      [Forecasting]  
    ```  
  
3.  Facoltativamente, è possibile digitare una clausola per limitare i risultati, simile all'esempio seguente:  
  
    ```  
    SELECT FLATTENED  
      [Forecasting].[Model Region],  
      (PredictTimeSeries([Forecasting].[Amount],5)) as [PredictAmount],  
      (PredictTimeSeries([Forecasting].[Quantity],5)) as [PredictQuantity]  
    FROM  
      [Forecasting]  
    WHERE [Forecasting].[Model Region] = 'M200 North America'   
    OR [Forecasting].[Model Region] = 'M200 Europe'  
  
    ```  
  
4.  Fare clic su **passa alla visualizzazione risultati della query**.  
  
#### <a name="to-export-prediction-query-results"></a>Per esportare i risultati della query di stima  
  
1.  Fare clic su **Salva risultati query**.  
  
2.  Nella finestra di dialogo **Salva risultati query di data mining** selezionare [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]per **origine dati**. Se si desidera salvare i dati in un database relazionale diverso, è inoltre possibile creare una nuova origine dati.  
  
3.  Nella colonna **nome tabella** Digitare un nuovo nome di tabella temporanea, ad esempio **stime dei test**.  
  
4.  Fare clic su **Save**.  
  
    > [!NOTE]  
    >  Per visualizzare la tabella creata, creare una connessione al motore di database dell'istanza in cui sono stati salvati i dati, quindi creare una query.  
  
## <a name="conclusion"></a>Conclusioni  
 Si è appreso come compilare un modello Time Series di base, interpretare le previsioni e creare stime.  
  
 Le attività restanti in questa esercitazione sono facoltative e descrivono stime avanzate basate su serie temporali. Se si decide di procedere, verrà illustrata la procedura per aggiungere nuovi dati al modello e creare stime nella serie estesa. Verrà inoltre illustrata la procedura per eseguire una stima incrociata, tramite la tendenza nel modello ma sostituendo i dati con una nuova serie di dati.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Stime avanzate basate su serie temporali &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Time Series Model Query Examples](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  
