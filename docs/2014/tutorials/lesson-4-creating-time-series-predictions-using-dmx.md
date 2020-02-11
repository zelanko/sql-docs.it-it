---
title: 'Lezione 4: creazione di stime basate su serie temporali tramite DMX | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6b883e43-209d-489a-8dc3-9349f88acae8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 772e5f5f71ca82dd18fec48730522c80e907414f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63312084"
---
# <a name="lesson-4-creating-time-series-predictions-using-dmx"></a>Lezione 4: Creazione di stime basate su serie temporali utilizzando DMX
  In questa lezione e nella lezione seguente si utilizzerà DMX (Data Mining Extensions) per creare diversi tipi di stime in base ai modelli Time Series creati nella [lezione 1: creazione di un modello di data mining Time Series e della struttura](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md) di data mining e [lezione 2: aggiunta di modelli di data mining alla struttura di data mining Time Series](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md).  
  
 Con un modello Time Series si dispone di numerose opzioni per l'esecuzione di stime:  
  
-   Utilizzare gli schemi e i dati esistenti nel modello di data mining.  
  
-   Utilizzare gli schemi esistenti nel modello di data mining, ma fornire nuovi dati.  
  
-   Aggiungere nuovi dati al modello o aggiornare il modello.  
  
 La sintassi per effettuare questi tipi di stima è riportata di seguito:  
  
 Stima basata su serie temporali predefinita  
 Utilizzare [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx) per restituire il numero specificato di stime dal modello di data mining sottoposto a training.  
  
 Vedere ad esempio [PredictTimeSeries &#40;&#41;DMX](/sql/dmx/predicttimeseries-dmx) o [esempi di query sul modello Time Series](../../2014/analysis-services/data-mining/time-series-model-query-examples.md).  
  
 EXTEND_MODEL_CASES  
 Utilizzare [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx) con l'argomento EXTEND_MODEL_CASES per aggiungere nuovi dati, estendere la serie e creare stime basate sul modello di data mining aggiornato.  
  
 Questa esercitazione contiene un esempio dell'utilizzo di EXTEND_MODEL_CASES.  
  
 REPLACE_MODEL_CASES  
 Utilizzare [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx) con l'argomento REPLACE_MODEL_CASES per sostituire i dati originali con una nuova serie di dati, quindi creare stime basate sull'applicazione dei modelli nel modello di data mining alla nuova serie di dati.  
  
 Per un esempio di come utilizzare REPLACE_MODEL_CASES, vedere [lezione 2: compilazione di uno scenario di previsione &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md).  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione verranno eseguite le attività seguenti:  
  
-   Creare una query per ottenere le stime predefinite sulla base dei dati esistenti.  
  
 Nella lezione successiva verranno eseguite le attività correlate seguenti:  
  
-   Creare una query per fornire nuovi dati e ottenere stime aggiornate.  
  
 Oltre a creare manualmente le query tramite DMX, è anche possibile creare stime tramite il generatore delle query di stima in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="simple-time-series-prediction-query"></a>Semplice query di stima basata su serie temporali  
 Il primo passaggio consiste nell'utilizzare l'istruzione `SELECT FROM` insieme alla funzione `PredictTimeSeries` per creare stime basate su serie temporali. I modelli Time Series supportano una sintassi semplificata per la creazione di stime: non è necessario fornire alcun input, ma è sufficiente specificare il numero di stime da creare. Di seguito è riportato un esempio generico dell'istruzione da utilizzare:  
  
```  
SELECT <select list>   
FROM [<mining model name>]   
WHERE [<criteria>]  
```  
  
 L'elenco di selezione può contenere colonne del modello, ad esempio il nome della linea di prodotti per cui si stanno creando le stime, o funzioni di stima, ad esempio [Lag &#40;dmx&#41;](/sql/dmx/lag-dmx) o [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx), che sono specifici per i modelli di data mining Time Series.  
  
#### <a name="to-create-a-simple-time-series-prediction-query"></a>Per creare una semplice query di stima basata su serie temporali  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]mouse sull'istanza di, scegliere **nuova query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico dell'istruzione nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    <select list>   
    ```  
  
     con:  
  
    ```  
    [Forecasting_MIXED].[ModelRegion],  
    PredictTimeSeries([Forecasting_MIXED].[Quantity],6) AS PredictQty,  
    PredictTimeSeries ([Forecasting_MIXED].[Amount],6) AS PredictAmt  
    ```  
  
     La prima riga consente di recuperare il valore del modello di data mining che identifica la serie.  
  
     La seconda e terza riga utilizzano la funzione `PredictTimeSeries`. Ogni riga stima un attributo diverso, `[Quantity]` o `[Amount]`. I numeri dopo i nomi degli attributi stimabili specificano il numero di intervalli temporali da stimare.  
  
     La clausola `AS` viene utilizzata per fornire un nome per la colonna restituita da ogni funzione di stima. Se non si fornisce un alias, per impostazione predefinita entrambe le colonne vengono restituite con l'etichetta `Expression`.  
  
4.  Sostituire quanto segue:  
  
    ```  
    [<mining model>]   
    ```  
  
     con:  
  
    ```  
    [Forecasting_MIXED]  
    ```  
  
5.  Sostituire quanto segue:  
  
    ```  
    WHERE [criteria>]   
    ```  
  
     con:  
  
    ```  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
     L'istruzione completa dovrebbe risultare analoga alla seguente:  
  
    ```  
    SELECT  
    [Forecasting_MIXED].[ModelRegion],  
    PredictTimeSeries([Forecasting_MIXED].[Quantity],6) AS PredictQty,  
    PredictTimeSeries ([Forecasting_MIXED].[Amount],6) AS PredictAmt  
    FROM   
    [Forecasting_MIXED]  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
6.  Scegliere **Salva DMXQuery1. DMX con nome**dal menu **file** .  
  
7.  Nella finestra di dialogo **Salva con** nome individuare la cartella appropriata e assegnare al file `SimpleTimeSeriesPrediction.dmx`il nome.  
  
8.  Sulla barra degli strumenti fare clic sul pulsante **Esegui** .  
  
     La query restituisce sei stime per ognuna delle due combinazioni di prodotto e area specificate nella clausola `WHERE`.  
  
 Nella lezione successiva verrà creata una query che fornisce nuovi dati al modello e confronta i risultati di tale stima con quella appena creata.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Lezione 5: Estensione del modello Time Series](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
  
## <a name="see-also"></a>Vedere anche  
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)   
 [Ritardo &#40;DMX&#41;](/sql/dmx/lag-dmx)   
 [Esempi di query sul modello Time Series](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [Lezione 2: compilazione di uno scenario di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
  
