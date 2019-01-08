---
title: Esempi di Query del modello Time Series | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time series algorithms [Analysis Services]
- MISSING_VALUE_SUBSTITUTION
- time series [Analysis Services]
- predictions [Analysis Services], time series
- EXTEND_MODEL_CASES parameter
- REPLACE_MODEL_CASES parameter
- prediction queries [DMX]
- PREDICTION_SMOOTHING
- content queries [DMX]
ms.assetid: 9a1c527e-2997-493b-ad6a-aaa71260b018
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4098a1b5eade3705e10ab609c47454564a18101d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511407"
---
# <a name="time-series-model-query-examples"></a>Time Series Model Query Examples
  Quando si crea una query su un modello di data mining, è possibile creare una query sul contenuto, che consente di fornire dettagli sui criteri individuati durante l'analisi, o una query di stima, che consente di utilizzare i criteri presenti nel modello di data mining per eseguire stime relative ai nuovi dati. Una query sul contenuto per un modello Time Series, ad esempio, potrebbe fornire dettagli aggiuntivi sulle strutture periodiche rilevate, mentre una query di stima potrebbe fornire stime per i 5-10 intervalli di tempo successivi. Utilizzando una query è inoltre possibile recuperare metadati relativi al modello.  
  
 In questa sezione viene illustrato come creare entrambi i tipi di query per i modelli basati sull'algoritmo Microsoft Time Series.  
  
 **Query sul contenuto**  
  
 [Recupero di hint di periodicità per il modello](#bkmk_Query1)  
  
 [Recupero dell'equazione per un modello ARIMA](#bkmk_Query2)  
  
 [Recupero dell'equazione per un modello ARTxp](#bkmk_Query3)  
  
 **Query di stima**  
  
 [Informazioni sui casi in cui sostituire o estendere i dati di una serie temporale](#bkmk_ReplaceExtend)  
  
 [Esecuzione di stime con EXTEND_MODEL_CASES](#bkmk_EXTEND)  
  
 [Esecuzione di stime con REPLACE_MODEL_CASES](#bkmk_REPLACE)  
  
 [Sostituzione di valori mancanti nei modelli Time Series](#bkmk_MissingValues)  
  
## <a name="getting-information-about-a-time-series-model"></a>Recupero di informazioni su un modello Time Series  
 Una query sul contenuto del modello può fornire informazioni di base sul modello, ad esempio i parametri utilizzati durante la creazione del modello o l'ora dell'ultima volta in cui è stato elaborato il modello. Nell'esempio seguente viene illustrata la sintassi di base per l'esecuzione di una query sul contenuto del modello utilizzando i set di righe dello schema di data mining.  
  
###  <a name="bkmk_Query1"></a> Esempio di Query 1: Recupero di hint di periodicità per il modello  
 È possibile recuperare le periodicità individuate all'interno della serie temporale eseguendo una query sull'albero ARIMA o ARTXP. Le periodicità nel modello completato, tuttavia, potrebbero non corrispondere ai periodi specificati come hint durante la creazione del modello. Per recuperare gli hint specificati come parametri durante la creazione del modello, è possibile eseguire una query sul contenuto del modello di data mining utilizzando l'istruzione DMX seguente:  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 Risultati parziali:  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY = 0,1, MINIMUM_SUPPORT = 10, PERIODICITY_HINT ={1,3},...|  
  
 L'hint di periodicità predefinito è {1} ed è presente in tutti i modelli. Questo modello di esempio è stato creato con un hint aggiuntivo che potrebbe non essere presente nel modello finale.  
  
> [!NOTE]  
>  Nell'esempio i risultati sono stati troncati per una maggiore leggibilità.  
  
###  <a name="bkmk_Query2"></a> Esempio di Query 2: Recupero dell'equazione per un modello ARIMA  
 È possibile recuperare l'equazione per un modello ARIMA eseguendo una query su qualsiasi nodo in un singolo albero. Ogni albero all'interno di un modello ARIMA rappresenta una periodicità diversa e, in presenza di più serie di dati, ciascuna serie di dati disporrà di un set di alberi di periodicità. Per recuperare l'equazione per una serie di dati specifica, pertanto, è innanzitutto necessario identificare l'albero.  
  
 Il prefisso TA, ad esempio, indica che il nodo fa parte di un albero ARIMA, mentre il prefisso TS viene utilizzato per gli alberi ARTXP. È possibile trovare tutti gli alberi ARIMA eseguendo una query sul contenuto del modello per i nodi con un valore NODE_TYPE di 27. È anche possibile utilizzare il valore di ATTRIBUTE_NAME per individuare il nodo radice ARIMA per una particolare serie di dati. Questo esempio di query consente di trovare i nodi ARIMA che rappresentano le quantità vendute del modello R250 nell'area Europa.  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM Forecasting.CONTENT  
WHERE ATTRIBUTE_NAME = 'R250 Europe: Quantity"  
AND NODE_TYPE = 27  
```  
  
 Utilizzando questo ID del nodo è possibile recuperare dettagli sull'equazione ARIMA per l'albero. L'istruzione DMX seguente recupera la forma abbreviata dell'equazione ARIMA per la serie di dati. Viene inoltre recuperata l'intersezione dalla tabella nidificata, NODE_DISTRIBUTION. In questo esempio l'equazione viene ottenuta facendo riferimento all'ID univoco del nodo TA00000007. Può essere tuttavia necessario utilizzare un ID del nodo diverso ed è possibile ottenere risultati leggermente differenti dal modello.  
  
```  
SELECT FLATTENED NODE_CAPTION as [Short equation],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE   
FROM NODE_DISTRIBUTION) as t  
FROM Forecasting.CONTENT  
WHERE NODE_NAME = 'TA00000007'  
```  
  
 Risultati dell'esempio:  
  
|Short equation|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|--------------------|-----------------------|------------------------|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Intercept)|15.24...|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|1|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|12|  
  
 Per altre indicazioni su come interpretare queste informazioni, vedere [Contenuto dei modelli di data mining per i modelli Time Series &#40;Analysis Services - Data mining&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Query3"></a> Esempio di Query 3: Recupero dell'equazione per un modello ARTXP  
 Per un modello ARTxp, a ogni livello dell'albero vengono archiviate informazioni diverse. Per altre informazioni sulla struttura di un modello ARTxp e su come interpretare le informazioni nell'equazione, vedere [Mining Model Content for Time Series Models &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
 L'istruzione DMX seguente recupera le informazioni su una parte dell'albero ARTxp che rappresenta la quantità di vendite per il modello R250 in Europa.  
  
> [!NOTE]  
>  Il nome della colonna VARIANCE della tabella nidificata deve essere racchiuso tra parentesi per distinguerlo dalla parola chiave riservata con lo stesso nome. Le colonne della tabella nidificata, PROBABILITY e SUPPORT, non sono incluse in quanto vuote nella maggior parte dei casi.  
  
```  
SELECT NODE_CAPTION as [Split information],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
   [VARIANCE]  
   FROM NODE_DISTRIBUTION) AS t  
FROM Forecasting.CONTENT  
WHERE NODE_ATTRIBUTE_NAME = 'R250 Europe:Quantity'  
AND NODE_TYPE = 15  
```  
  
 Per altre indicazioni su come interpretare queste informazioni, vedere [Contenuto dei modelli di data mining per i modelli Time Series &#40;Analysis Services - Data mining&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
## <a name="creating-predictions-on-a-time-series-model"></a>Creazione di stime in un modello Time Series  
 A partire da [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]è possibile aggiungere nuovi dati a un modello Time Series e incorporarli automaticamente nel modello. I nuovi dati possono essere aggiunti a un modello di data mining Time Series in uno dei due modi indicati di seguito:  
  
-   Utilizzare `PREDICTION JOIN` per unire in join i dati in un'origine esterna ai dati di training.  
  
-   Usando una query di stima singleton per specificare i dati un intervallo alla volta. Per informazioni su come creare una query di stima singleton, vedere [interfacce di Data Mining Query](data-mining-query-tools.md).  
  
###  <a name="bkmk_ReplaceExtend"></a> Informazioni sul comportamento delle operazioni di sostituzione ed estensione  
 Quando si aggiungono nuovi dati a un modello Time Series, è possibile specificare se estendere o sostituire i dati di training:  
  
-   **Estendere:** Quando si estende una serie di dati, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aggiunge i nuovi dati alla fine dei dati di training esistenti. Il numero di case di training aumenta.  
  
     L'estensione dei case del modello risulta utile per l'aggiornamento continuo del modello con i dati nuovi. Se, ad esempio, si desidera aumentare il training set nel tempo, è sufficiente estendere il modello.  
  
     Per estendere i dati, creare un'istruzione `PREDICTION JOIN` in un modello Time Series, specificare l'origine dei nuovi dati e utilizzare l'argomento `EXTEND_MODEL_CASES`.  
  
-   **Sostituire:** Quando si sostituiscono i dati nella serie di dati, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mantiene il modello con training, ma usa i nuovi valori per sostituire alcuni o tutti i case di training esistenti. La dimensione dei dati di training pertanto non viene mai modificata, mentre i case vengono sostituiti continuamente con dati più aggiornati. Se si forniscono dati abbastanza nuovi, è possibile sostituire i dati di training con una serie completamente nuova.  
  
     La sostituzione dei case del modello risulta utile qualora si desideri eseguire il training per un modello in un case set, quindi applicare il modello a una serie di dati diversa.  
  
     Per sostituire i dati, creare un'istruzione `PREDICTION JOIN` in un modello Time Series, specificare l'origine dei nuovi dati e utilizzare l'argomento `REPLACE_MODEL_CASES`.  
  
> [!NOTE]  
>  Non è possibile eseguire stime cronologiche quando si aggiungono nuovi dati.  
  
 Indipendentemente dall'operazione eseguita sui dati di training, ovvero estensione o sostituzione, le stime iniziano sempre dal timestamp finale del training set originale. In altre parole, se nei nuovi dati sono contenuti n intervalli di tempo e si richiedono stime per gli intervalli temporali da 1 a n, le stime coincideranno con lo stesso periodo dei nuovi dati e non verranno restituite le stime.  
  
 Per ottenere nuove stime per periodi di tempo che non si sovrappongono ai nuovi dati, è necessario avviare le stime in corrispondenza dell'intervallo di tempo n+1 oppure assicurarsi di richiedere ulteriori intervalli di tempo.  
  
 Si supponga ad esempio che il modello esistente contenga dati relativi a sei mesi. Si desidera estendere il modello aggiungendo le cifre relative alle vendite degli ultimi tre mesi ed effettuare una stima sui prossimi tre mesi. Per ottenere solo le nuove stime quando si aggiungono i nuovi dati, specificare l'intervallo di tempo 4 come punto iniziale e l'intervallo di tempo 7 come punto finale. È anche possibile richiedere un totale di sei stime, ma, in questo caso, gli intervalli di tempo per le prime tre stime si sovrapporrebbero ai nuovi dati aggiunti.  
  
 Per altre informazioni sulla sintassi per l'uso ed esempi di query `REPLACE_MODEL_CASES` e `EXTEND_MODEL_CASES`, vedere [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
###  <a name="bkmk_EXTEND"></a> Esecuzione di stime con EXTEND_MODEL_CASES  
 Il comportamento delle stime varia a seconda se si esegue l'estensione o la sostituzione dei case del modello. Se si estende un modello, i nuovi dati vengono aggiunti alla fine della serie e le dimensioni del set di training aumentano. Gli intervalli di tempo utilizzati per le query di stima iniziano tuttavia sempre alla fine della serie originale. Se si aggiungono pertanto tre nuovi punti dati e si richiedono sei stime, le prime tre stime restituite si sovrappongono tuttavia ai nuovi dati. In questo caso, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce i nuovi punti dati effettivi anziché eseguire una stima, finché non vengono utilizzati tutti i nuovi punti dati. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono quindi eseguite le stime in base alla serie composta.  
  
 Questo comportamento consente di aggiungere nuovi dati e di visualizzare le cifre effettive relative alle vendite nell'apposito grafico, anziché visualizzare le proiezioni.  
  
 Per aggiungere tre nuovi punti dati ed eseguire tre nuove stime, è ad esempio necessario effettuare quanto segue:  
  
-   Creare un'istruzione `PREDICTION JOIN` in un modello Time Series e specificare l'origine di nuovi dati relativi a tre mesi.  
  
-   Richiedere stime per sei intervalli di tempo. A tale scopo, specificare 6 intervalli di tempo, dove il punto iniziale è l'intervallo di tempo 1 e il punto finale è l'intervallo di tempo 7. Questa indicazione si applica solo a EXTEND_MODEL_CASES.  
  
-   Per ottenere solo le nuove stime, specificare 4 come punto iniziale e 7 come punto finale.  
  
-   È necessario utilizzare l'argomento `EXTEND_MODEL_CASES`.  
  
     Le cifre relative alle vendite effettive vengono restituite per i primi tre intervalli di tempo, mentre le stime basate sul modello esteso vengono restituite per i tre intervalli di tempo successivi.  
  
###  <a name="bkmk_REPLACE"></a> Esecuzione di stime con REPLACE_MODEL_CASES  
 Se si sostituiscono i case in un modello, le dimensioni del modello rimangono invariate, ma i singoli case nel modello vengono sostituiti in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Ciò risulta utile per le stime incrociate e scenari in cui è importante mantenere dimensioni consistenti del set di dati di training.  
  
 Si supponga ad esempio che i dati relativi alle vendite di uno dei negozi non siano sufficienti. È possibile creare un modello generale calcolando la media delle vendite per tutti i negozi in una particolare regione, quindi eseguire il training di un modello. Per eseguire stime per il negozio i cui dati relativi alle vendite non sono sufficienti, creare quindi un'istruzione `PREDICTION JOIN` sui nuovi dati di vendita solo per il negozio in questione. In questo caso, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono mantenuti i modelli che derivano dal modello regionale, mentre i case di training esistenti vengono sostituiti con i dati del singolo negozio. Si otterrà pertanto una maggiore corrispondenza tra i valori della stima e le linee di tendenza del singolo negozio.  
  
 Quando si utilizza l'argomento `REPLACE_MODEL_CASES`, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nuovi case vengono continuamente aggiunti alla fine del case set e un numero corrispondente di case viene eliminato dall'inizio del case set. Se si aggiunge una quantità di nuovi dati maggiore rispetto a quella nel set di training originale, i dati meno recenti vengono eliminati in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se si specifica un numero sufficiente di nuovi valori, le stime possono essere basate sui dati completamente nuovi.  
  
 Si supponga ad esempio di avere eseguito il training per il modello in un set di dati di case contenente 1000 righe. Si aggiungono quindi 100 righe di nuovi dati. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono eliminate le prime 100 righe dal set di training e le 100 righe di nuovi dati vengono aggiunte alla fine del set, in modo da ottenere un totale di 1000. Se si aggiungono 1100 righe di dati nuovi, vengono utilizzate solo le 1000 righe più recenti.  
  
 Per fare un altro esempio, si supponga di volere aggiungere nuovi dati relativi a tre mesi ed eseguire tre nuove stime. In tal caso, effettuare quanto segue:  
  
-   Creare un'istruzione `PREDICTION JOIN` in un modello Time Series e utilizzare l'argomento `REPLACE_MODEL_CASE`.  
  
-   Specificare l'origine dei nuovi dati relativi a tre mesi. È possibile che tali dati provengano da un'origine completamente diversa da quella dei dati di training originali.  
  
-   Richiedere stime per sei intervalli di tempo. A tale scopo, specificare 6 intervalli di tempo oppure specificare l'intervallo di tempo 1 come punto iniziale e l'intervallo di tempo 7 come punto finale.  
  
    > [!NOTE]  
    >  A differenza di `EXTEND_MODEL_CASES`, non è possibile restituire gli stessi valori aggiunti come dati di input. Tutti i sei valori restituiti sono stime basate sul modello aggiornato che include sia i vecchi che i nuovi dati.  
  
    > [!NOTE]  
    >  Se con REPLACE_MODEL_CASES si utilizza il timestamp 1 come punto iniziale, si ottengono nuove stime basate sui nuovi dati, che sostituiscono i dati di training precedenti.  
  
 Per altre informazioni sulla sintassi per l'uso ed esempi di query `REPLACE_MODEL_CASES` e `EXTEND_MODEL_CASES`, vedere [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
###  <a name="bkmk_MissingValues"></a> Sostituzione di valori mancanti nei modelli Time Series  
 Quando si aggiungono nuovi dati a un modello Time Series utilizzando un'istruzione `PREDICTION JOIN`, nel nuovo set di dati non può mancare alcun valore. Se una serie è incompleta, il modello deve fornire i valori mancanti utilizzando un valore Null, più medie numeriche, una media numerica specifica o un valore stimato. Se si specifica `EXTEND_MODEL_CASES`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] i valori mancanti vengono sostituiti con stime basate sul modello originale. Se si usa `REPLACE_MODEL_CASES`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sostituisce i valori mancanti con il valore specificato nella *MISSING_VALUE_SUBSTITUTION* parametro.  
  
## <a name="list-of-prediction-functions"></a>Elenco delle funzioni di stima  
 Tutti gli algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] supportano un set comune di funzioni. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series, tuttavia, supporta funzioni aggiuntive, elencate nella tabella seguente.  
  
|||  
|-|-|  
|Funzione di stima|Uso|  
|[Lag &#40;DMX&#41;](/sql/dmx/lag-dmx)|Viene restituito un numero di intervalli di tempo tra la data del case corrente e l'ultima data del set di training.<br /><br /> Un tipico utilizzo di questa funzione consiste nell'identificare i case di training recenti per poter recuperare dati dettagliati sui case.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Restituisce l'ID nodo per la colonna stimabile specificata.<br /><br /> Un tipico utilizzo di questa funzione consiste nell'identificare il nodo che genera un determinato valore stimato per poter esaminare i case associati al nodo o recuperare l'equazione e altri dettagli.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|Restituisce la deviazione standard delle stime nella colonna stimabile specificata.<br /><br /> Questa funzione sostituisce l'argomento INCLUDE_STATISTICS, non supportato per i modelli Time Series.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Restituisce la varianza delle stime per la colonna stimabile specificata.<br /><br /> Questa funzione sostituisce l'argomento INCLUDE_STATISTICS, non supportato per i modelli Time Series.|  
|[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)|Restituisce i valori futuri stimati o cronologici per una serie temporale.<br /><br /> È anche possibile eseguire una query sui modelli della serie temporale con la funzione di stima generale [Predict &#40;DMX&#41;](/sql/dmx/predict-dmx).|  
  
 Per un elenco delle funzioni comuni a tutti gli algoritmi di [!INCLUDE[msCoName](../../includes/msconame-md.md)], vedere [Funzioni di stima generali &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx). Per la sintassi di funzioni specifiche, vedere [Guida di riferimento alle funzioni DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Vedere anche  
 [Query di data mining](data-mining-queries.md)   
 [Algoritmo Microsoft Time Series](microsoft-time-series-algorithm.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Time Series](microsoft-time-series-algorithm-technical-reference.md)   
 [Contenuto dei modelli di data mining per i modelli Time Series &#40;Analysis Services - Data mining&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
