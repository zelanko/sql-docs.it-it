---
title: 'Lezione 5: Estendere la serie temporale modellare | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7aad4946-c903-4e25-88b9-b087c20cb67d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2716e985897f8115d189d9410b7cdb13fb1af291
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62822069"
---
# <a name="lesson-5-extending-the-time-series-model"></a>Lezione 5: Estensione del modello Time Series
  In [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise è possibile aggiungere nuovi dati a un modello Time Series e incorporarli automaticamente nel modello. I nuovi dati possono essere aggiunti a un modello di data mining Time Series in uno dei due modi indicati di seguito:  
  
-   Utilizzando PREDICTION JOIN per unire in join i dati in un'origine esterna ai dati di training.  
  
-   Usando una query di stima singleton per specificare i dati un intervallo alla volta.  
  
 Si supponga ad esempio di avere eseguito il training del modello di data mining sui dati di vendita esistenti, alcuni mesi fa. Una volta ottenuti i dati delle nuove vendite, è necessario aggiornare le stime di vendita per incorporare i nuovi dati. È possibile eseguire questa operazione in un unico passaggio, fornendo le cifre relative alle nuove vendite come dati di input e generando le nuove stime in base al set di dati composto.  
  
## <a name="making-predictions-with-extendmodelcases"></a>Esecuzione di stime con EXTEND_MODEL_CASES  
 Di seguito sono riportati esempi generici di una stima basata su serie temporali che utilizza EXTEND_MODEL_CASES. Il primo esempio consente di specificare il numero di stime a partire dall'ultimo intervallo temporale del modello originale:  
  
```  
SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n, EXTEND_MODEL_CASES)   
FROM <mining model>  
PREDICTION JOIN <source query>  
[WHERE <criteria>]  
```  
  
 Il secondo esempio consente di specificare l'intervallo temporale di inizio e di fine delle stime. Questa opzione è importante quando si estendono i case del modello poiché, per impostazione predefinita, gli intervalli temporali utilizzati per le query di stima iniziano sempre dalla fine della serie originale.  
  
```  
SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n-start, n-end, EXTEND_MODEL_CASES)   
FROM <mining model>  
PREDICTION JOIN <source query>  
[WHERE <criteria>}  
```  
  
 In questa esercitazione verranno creati entrambi i tipi di query.  
  
#### <a name="to-create-a-singleton-prediction-query-on-a-time-series-model"></a>Per creare una query di stima singleton in un modello Time Series  
  
1.  Nella **Esplora oggetti**, fare doppio clic sull'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], scegliere **nuova Query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico dell'istruzione singleton nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n, EXTEND_MODEL_CASES)   
    ```  
  
     con:  
  
    ```  
    SELECT [Model Region],  
    PredictTimeSeries([Quantity],6, EXTEND_MODEL_CASES) AS PredictQty  
    ```  
  
     La prima riga consente di recuperare il valore del modello che identifica la serie.  
  
     La seconda riga contiene la funzione di stima, che ottiene 6 stime per Quantity. L'alias `PredictQty` viene assegnato alla colonna del risultato della stima per semplificare la comprensione dei risultati.  
  
4.  Sostituire quanto segue:  
  
    ```  
    FROM <mining model>  
    ```  
  
     con:  
  
    ```  
    FROM [Forecasting_MIXED]  
    ```  
  
5.  Sostituire quanto segue:  
  
    ```  
    PREDICTION JOIN <source query>  
    ```  
  
     con:  
  
    ```  
    NATURAL PREDICTION JOIN   
    (  
       SELECT 1 AS [Reporting Date],  
       '10' AS [Quantity],  
       'M200 Europe' AS [Model Region]  
       UNION SELECT  
       2 AS [Reporting Date],  
       15 AS [Quantity]),  
       'M200 Europe' AS [Model Region]  
    ) AS t  
    ```  
  
6.  Sostituire quanto segue:  
  
    ```  
    [WHERE <criteria>]  
    ```  
  
     con:  
  
    ```  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
     L'istruzione completa dovrebbe risultare analoga alla seguente:  
  
    ```  
    SELECT [Model Region],  
    PredictTimeSeries([Quantity],6, EXTEND_MODEL_CASES) AS PredictQty  
    FROM  
       [Forecasting_MIXED]  
    NATURAL PREDICTION JOIN   
       SELECT 1 AS [ReportingDate],  
      '10' AS [Quantity],  
      'M200 Europe' AS [ModelRegion]  
    UNION SELECT  
      2 AS [ReportingDate],  
      15 AS [Quantity]),  
      'M200 Europe' AS [ModelRegion]  
    ) AS t  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
7.  Nel **File** menu, fare clic su **Salva Dmxquery1.DMX**.  
  
8.  Nel **Salva con nome** della finestra di dialogo passare alla cartella appropriata e assegnare un nome di file `Singleton_TimeSeries_Query.dmx`.  
  
9. Sulla barra degli strumenti, scegliere il **Execute** pulsante.  
  
     La query restituirà le stime delle quantità di vendita relative alla bicicletta M200 in Europa e nell'area del Pacifico.  
  
## <a name="understanding-prediction-start-with-extendmodelcases"></a>Informazioni sull'avvio della stima con EXTEND_MODEL_CASES  
 Una volta create le stime in base al modello originale e ai nuovi dati, è possibile confrontare i risultati per stabilire in che modo l'aggiornamento dei dati di vendita influisce sulle stime. Prima di eseguire questa operazione, rivedere il codice appena creato e notare quanto segue:  
  
-   Sono stati forniti nuovi dati solo per l'Europa.  
  
-   I nuovi dati forniti riguardano solo due mesi.  
  
 Nella tabella seguente viene illustrato come i nuovi valori forniti per il prodotto M200 Europe influiscono sulle stime. Per il prodotto M200 nell'area del Pacifico non sono stati forniti nuovi dati, tuttavia viene ugualmente eseguito il confronto tra le due serie:  
  
 **Prodotto e area: M200 Europe**  
  
|||||  
|-|-|-|-|  
|||Modello esistente (`PredictTimeSeries`)|Modello con dati di vendita aggiornati (`PredictTimeSeries` con `EXTEND_MODEL_CASES`)|  
|M200 Europe|7/25/2008 12:00:00 AM|77|10|  
|M200 Europe|8/25/2008 12:00:00 AM|64|15|  
|M200 Europe|9/25/2008 12:00:00 AM|59|72|  
|M200 Europe|10/25/2008 12:00:00 AM|56|69|  
|M200 Europe|11/25/2008 12:00:00 AM|56|68|  
|M200 Europe|12/25/2008 12:00:00 AM|74|89|  
  
 **Prodotto e area: M200 Pacific**  
  
|||||  
|-|-|-|-|  
|||Modello esistente (`PredictTimeSeries`)|Modello con dati di vendita aggiornati (`PredictTimeSeries` con `EXTEND_MODEL_CASES`)|  
|M200 Pacific|7/25/2008 12:00:00 AM|41|41|  
|M200 Pacific|8/25/2008 12:00:00 AM|44|44|  
|M200 Pacific|9/25/2008 12:00:00 AM|38|38|  
|M200 Pacific|10/25/2008 12:00:00 AM|41|41|  
|M200 Pacific|11/25/2008 12:00:00 AM|36|36|  
|M200 Pacific|12/25/2008 12:00:00 AM|39|39|  
  
 Da questi risultati è possibile dedurre quanto segue:  
  
-   Le prime due stime per la serie M200 Europe corrispondono esattamente ai nuovi dati forniti. In base alle caratteristiche di progettazione, Analysis Services restituisce i nuovi punti dati effettivi anziché eseguire una stima. Quando infatti si estendono i case del modello, gli intervalli temporali utilizzati per le query di stima iniziano sempre dalla fine della serie originale. Se si aggiungono pertanto due nuovi punti dati, le prime due stime restituite si sovrappongono ai nuovi dati.  
  
-   Una volta utilizzati tutti i nuovi punti dati, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] esegue stime in base al modello aggiornato. Pertanto, a partire da settembre 2005, è possibile vedere la differenza tra le stime per la serie M200 Europe nel modello originale, nella colonna a sinistra, e nel modello che utilizza EXTEND_MODEL_CASES, nella colonna a destra. Le stime sono diverse perché il modello è stato aggiornato con i nuovi dati.  
  
## <a name="using-start-and-end-time-steps-to-control-predictions"></a>Utilizzo degli intervalli temporali di inizio e di fine per controllare le stime  
 Se si estende un modello, i nuovi dati vengono sempre aggiunti alla fine della serie. Per l'esecuzione delle stime, tuttavia, gli intervalli di tempo utilizzati per le query di stima iniziano alla fine della serie originale. Se si desidera ottenere solo le nuove stime quando si aggiungono i nuovi dati, è necessario specificare il punto iniziale come numero di intervalli di tempo. Per aggiungere due nuovi punti dati ed eseguire quattro nuove stime, è ad esempio necessario effettuare le seguenti operazioni:  
  
-   Creare un'istruzione PREDICTION JOIN in un modello Time Series e specificare nuovi dati relativi a due mesi.  
  
-   Richiedere stime per quattro intervalli di tempo, dove il punto iniziale è l'intervallo di tempo 3 e il punto finale è l'intervallo di tempo 6.  
  
 In altre parole, se i nuovi dati sono contenuti n intervalli di tempo e si richiedono stime per gli intervalli temporali da 1 a n, le stime coincideranno con lo stesso periodo dei nuovi dati. Per ottenere nuove stime per periodi di tempo non previsti dai dati, è necessario avviare le stime nell'intervallo di tempo n+1 dopo la nuova serie dei dati oppure verificare di aver effettuato la richiesta di ulteriori intervalli di tempo.  
  
> [!NOTE]  
>  Non è possibile eseguire stime cronologiche quando si aggiungono nuovi dati.  
  
 Nell'esempio seguente viene illustrata l'istruzione DMX che consente di ottenere solo le nuove stime per le due serie dell'esempio precedente.  
  
```  
SELECT [Model Region],  
PredictTimeSeries([Quantity],3,6, EXTEND_MODEL_CASES) AS PredictQty  
FROM  
   [Forecasting_MIXED]  
NATURAL PREDICTION JOIN   
   SELECT 1 AS [ReportingDate],  
  '10' AS [Quantity],  
  'M200 Europe' AS [ModelRegion]  
UNION SELECT  
  2 AS [ReportingDate],  
  15 AS [Quantity]),  
  'M200 Europe' AS [ModelRegion]  
) AS t  
WHERE [ModelRegion] = 'M200 Europe'  
```  
  
 I risultati della stima iniziano dall'intervallo di tempo 3, che è successivo ai 2 mesi dei nuovi dati forniti.  
  
 **Prodotto e area: M200 Europe**  
  
 Modello con dati aggiornati (PredictTimeSeries con EXTEND_MODEL_CASES)  
  
||||  
|-|-|-|  
|M200 Europe|9/25/2008 12:00:00 AM|72|  
|M200 Europe|10/25/2008 12:00:00 AM|69|  
|M200 Europe|11/25/2008 12:00:00 AM|68|  
|M200 Europe|12/25/2008 12:00:00 AM|89|  
  
## <a name="making-predictions-with-replacemodelcases"></a>Esecuzione di stime con REPLACE_MODEL_CASES  
 La sostituzione dei case del modello risulta utile qualora si desideri eseguire il training per un modello in un case set, quindi applicare il modello a una serie di dati diversa. Una procedura dettagliata di questo scenario viene presentata nella [lezione 2: Creazione di uno Scenario di previsione &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esempi di query sul modello di serie temporale](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
