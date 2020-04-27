---
title: Esempi di query sul modello Naive Bayes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- naive bayes model [Analysis Services]
- naive bayes algorithms [Analysis Services]
- content queries [DMX]
ms.assetid: e642bd7d-5afa-4dfb-8cca-4f84aadf61b0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b713d9918dabcbaabba2085710dfaa5ed5d3a33b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66083275"
---
# <a name="naive-bayes-model-query-examples"></a>Esempi di query sul modello Naive Bayes
  Quando si crea una query su un modello di data mining, è possibile creare una query sul contenuto, che consente di fornire dettagli sui criteri individuati durante l'analisi, o una query di stima, che consente di utilizzare i criteri presenti nel modello di data mining per eseguire stime relative ai nuovi dati. È inoltre possibile recuperare metadati relativi al modello tramite una query sul set di righe dello schema di data mining. In questa sezione viene illustrato come creare entrambi i tipi di query per i modelli basati sull'algoritmo Microsoft Naive Bayes.  
  
 **Query sul contenuto**  
  
 [Recupero di metadati del modello tramite DMX](#bkmk_Query1)  
  
 [Recupero di un riepilogo di dati di training](#bkmk_Query2)  
  
 [Ricerca di ulteriori informazioni sugli attributi](#bkmk_Query3)  
  
 [Utilizzo di stored procedure di sistema](#bkmk_Query4)  
  
 **Query di stima**  
  
 [Stima dei risultati mediante una query singleton](#bkmk_Query5)  
  
 [Recupero di stime con valori di probabilità e supporto](#bkmk_Query6)  
  
 [Stima delle associazioni](#bkmk_Query7)  
  
## <a name="finding-information-about-a-naive-bayes-model"></a>Ricerca di informazioni su un modello Naive Bayes  
 Il contenuto di un modello Naive Bayes fornisce informazioni aggregate sulla distribuzione di valori nei dati di training. Tramite la creazione di query sui set di righe dello schema di data mining è possibile inoltre recuperare informazioni sui metadati del modello.  
  
###  <a name="sample-query-1-getting-model-metadata-by-using-dmx"></a><a name="bkmk_Query1"></a>Esempio di query 1: recupero di metadati del modello tramite DMX  
 Tramite l'esecuzione di una query sul set di righe dello schema di data mining, è possibile trovare i metadati per il modello. Tali dati possono includere la data di creazione del modello, la data dell'ultima elaborazione del modello, il nome della struttura di data mining su cui si basa il modello e il nome delle colonne utilizzate come attributo stimabile. È inoltre possibile restituire i parametri utilizzati durante la creazione del modello.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, DATE_CREATED, LAST_PROCESSED,  
SERVICE_NAME, PREDICTION_ENTITY, FILTER  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_NaiveBayes_Filtered'  
```  
  
 Risultati dell'esempio:  
  
|||  
|-|-|  
|MODEL_CATALOG|AdventureWorks|  
|MODEL_NAME|TM_NaiveBayes_Filtered|  
|DATE_CREATED|3/1/2008 19:15|  
|LAST_PROCESSED|3/2/2008 20:00|  
|SERVICE_NAME|Microsoft_Naive_Bayes|  
|PREDICTION_ENTITY|Bike Buyer,Yearly Income|  
|FILTER|[Region] = 'Europe' OR [Region] = 'America del Nord'|  
  
 Il modello utilizzato per questo esempio si basa sul modello Naive Bayes creato nell' [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md), ma è stato modificato tramite l'aggiunta di un secondo attributo stimabile e l'applicazione di un filtro ai dati di training.  
  
###  <a name="sample-query-2-retrieving-a-summary-of-training-data"></a><a name="bkmk_Query2"></a> Esempio di query 2: Recupero di un riepilogo di dati di training  
 In un modello Naive Bayes il nodo delle statistiche marginali consente di archiviare informazioni aggregate sulla distribuzione di valori nei dati di training. Questo riepilogo risulta particolarmente utile in quanto consente di non dover creare query SQL sui dati di training per trovare le stesse informazioni.  
  
 Nell'esempio seguente viene utilizzata una query sul contenuto DMX per recuperare i dati dal nodo (NODE_TYPE = 24). Poiché le statistiche vengono archiviate in una tabella nidificata, viene utilizzata la parola chiave FLATTENED per rendere più semplice la visualizzazione dei risultati.  
  
```  
SELECT FLATTENED MODEL_NAME,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT], [PROBABILITY], VALUETYPE FROM NODE_DISTRIBUTION) AS t  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
> [!NOTE]  
>  È necessario includere i nomi delle colonne SUPPORT e PROBABILITY tra parentesi quadre per distinguerli dalle parole chiave riservate MDX degli stessi nomi.  
  
 Risultati parziali:  
  
|MODEL_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|0|1|  
|TM_NaiveBayes|Bike Buyer|0|8869|0,507263784|4|  
|TM_NaiveBayes|Bike Buyer|1|8615|0,492736216|4|  
|TM_NaiveBayes|Sesso|Missing|0|0|1|  
|TM_NaiveBayes|Sesso|F|8656|0.495081217|4|  
|TM_NaiveBayes|Sesso|M|8828|0.504918783|4|  
  
 Questi risultati indicano, ad esempio, il numero di case di training per ogni valore discreto (VALUETYPE = 4), insieme alla probabilità calcolata, adattata per i valori mancanti (VALUETYPE = 1).  
  
 Per una definizione dei valori forniti nella tabella NODE_DISTRIBUTION in un modello Naive Bayes, vedere [Contenuto dei modelli di data mining per i modelli Naive Bayes &#40;Analysis Services - Data mining&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md). Per altre informazioni sull'influenza dei valori mancanti sui calcoli di probabilità e supporto, vedere [Valori mancanti &#40;Analysis Services - Data mining&#41;](missing-values-analysis-services-data-mining.md).  
  
###  <a name="sample-query-3-finding-more-information-about-attributes"></a><a name="bkmk_Query3"></a> Esempio di query 3: Ricerca di ulteriori informazioni sugli attributi  
 Poiché un modello Naive Bayes spesso contiene informazioni complesse sulle relazioni fra attributi diversi, il modo più semplice per visualizzare tali relazioni consiste nell'utilizzare il [Visualizzatore Microsoft Naive Bayes](browse-a-model-using-the-microsoft-naive-bayes-viewer.md). È tuttavia possibile creare query DMX per restituire i dati.  
  
 Nell'esempio seguente viene illustrato come restituire informazioni dal modello su un particolare attributo, `Region`.  
  
```  
SELECT NODE_TYPE, NODE_CAPTION,   
NODE_PROBABILITY, NODE_SUPPORT, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE ATTRIBUTE_NAME = 'Region'  
```  
  
 Questa query restituisce due tipi di nodi: il nodo che rappresenta l'attributo di input (NODE_TYPE = 10) e i nodi per ogni valore dell'attributo (NODE_TYPE = 11). La didascalia del nodo viene utilizzata per identificare il nodo, anziché il nome dello stesso, in quanto mostra sia il nome che il valore dell'attributo.  
  
|NODE_TYPE|NODE_CAPTION|NODE_PROBABILITY|NODE_SUPPORT|MSOLAP_NODE_SCORE|NODE_TYPE|  
|----------------|-------------------|-----------------------|-------------------|-------------------------|----------------|  
|10|Bike Buyer -> Region|1|17484|84.51555875|10|  
|11|Bike Buyer -> Region = Missing|0|0|0|11|  
|11|Bike Buyer -> Region = North America|0.508236102|8886|0|11|  
|11|Bike Buyer -> Region = Pacific|0.193891558|3390|0|11|  
|11|Bike Buyer -> Region = Europe|0.29787234|5208|0|11|  
  
 Alcune delle colonne archiviate nei nodi corrispondono a quelle che è possibile ottenere dai nodi delle statistiche marginali, ad esempio il punteggio di probabilità e i valori di supporto del nodo. Tuttavia, MSOLAP_NODE_SCORE è un valore speciale fornito solo per i nodi dell'attributo di input e indica l'importanza relativa di questo attributo nel modello. Gran parte delle stesse informazioni è disponibile nel riquadro Rete di dipendenze, ma il visualizzatore non fornisce punteggi.  
  
 La query seguente restituisce i punteggi di importanza di tutti gli attributi nel modello:  
  
```  
SELECT NODE_CAPTION, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 10  
ORDER BY MSOLAP_NODE_SCORE DESC  
```  
  
 Risultati dell'esempio:  
  
|NODE_CAPTION|MSOLAP_NODE_SCORE|  
|-------------------|-------------------------|  
|Bike Buyer -> Total Children|181.3654836|  
|Bike Buyer -> Commute Distance|179.8419482|  
|Bike Buyer -> English Education|156.9841928|  
|Bike Buyer -> Number Children At Home|111.8122599|  
|Bike Buyer -> Region|84.51555875|  
|Bike Buyer -> Marital Status|23.13297354|  
|Bike Buyer -> English Occupation|2.832069191|  
  
 Esplorando il contenuto del modello in [Microsoft Generic Content Tree Viewer](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md), sarà possibile identificare le statistiche più interessanti. Alcuni degli esempi più semplici sono stati già illustrati qui. Molto spesso diventa necessario invece eseguire più query o archiviare i risultati ed elaborarli sul client.  
  
###  <a name="sample-query-4-using-system-stored-procedures"></a><a name="bkmk_Query4"></a> Esempio di query 4: Utilizzo di stored procedure di sistema  
 Oltre a scrivere query sul contenuto personalizzate, è possibile utilizzare alcune stored procedure di sistema di Analysis Services per esplorare i risultati. Per utilizzare una stored procedure di sistema, aggiungere davanti al nome della stessa la parola chiave CALL:  
  
```  
CALL GetPredictableAttributes ('TM_NaiveBayes')  
```  
  
 Risultati parziali:  
  
|ATTRIBUTE_NAME|NODE_UNIQUE_NAME|  
|---------------------|------------------------|  
|Bike Buyer|100000001|  
  
> [!NOTE]  
>  Queste stored procedure di sistema vengono utilizzate nelle comunicazioni interne tra il server di Analysis Services e il client e risultano utili solo durante lo sviluppo e il test di modelli di data mining. Le query destinate a un sistema di produzione, invece, devono essere scritte sempre tramite DMX.  
  
 Per altre informazioni sulle stored procedure di sistema di Analysis Services, vedere [Stored procedure di data mining &#40;Analysis Services - Data mining&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining).  
  
## <a name="using-a-naive-bayes-model-to-make-predictions"></a>Utilizzo di un modello Naive Bayes per eseguire stime  
 L'algoritmo Microsoft Naive Bayes in genere viene utilizzato meno per la stima che per l'esplorazione di relazioni tra attributi di input e stimabili. Tuttavia, il modello supporta l'utilizzo di funzioni di stima sia per la stima che per l'associazione.  
  
###  <a name="sample-query-5-predicting-outcomes-using-a-singleton-query"></a><a name="bkmk_Query5"></a> Esempio di query 5: Stima dei risultati mediante una query singleton  
 Nella query seguente viene utilizzata una query singleton per fornire un nuovo valore e stimare, in base al modello, se è probabile che un cliente con queste caratteristiche acquisti una bicicletta. Il modo più semplice per creare una query singleton in un modello di regressione consiste nell'utilizzare la finestra di dialogo **Input query singleton** . È ad esempio possibile compilare la query DMX seguente selezionando il modello `TM_NaiveBayes` , scegliendo **Query singleton**, quindi selezionando valori dagli elenchi a discesa per `[Commute Distance]` e `Gender`.  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 Risultati dell'esempio:  
  
|Expression|  
|----------------|  
|0|  
  
 Tramite la funzione di stima viene restituito il valore più probabile, in questo caso, 0, che indica che è improbabile che questo tipo di cliente acquisti una bicicletta.  
  
###  <a name="sample-query-6-getting-predictions-with-probability-and-support-values"></a><a name="bkmk_Query6"></a>Esempio di query 6: recupero di stime con valori di probabilità e supporto  
 Oltre a stimare un risultato, spesso si desidera conoscere l'attendibilità della stima. Nella query seguente viene usata la stessa query singleton dell'esempio precedente, ma viene aggiunta la funzione di stima [PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx) per restituire una tabella annidata contenente statistiche a supporto della stima.  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer]),  
  PredictHistogram([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 Risultati dell'esempio:  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|0|10161.5714|0.581192599|0.010530981|0|0|  
|1|7321.428768|0.418750215|0.008945684|0|0|  
||0.999828444|5.72E-05|5.72E-05|0|0|  
  
 Nella riga finale nella tabella vengono mostrate le modifiche apportate a supporto e probabilità per il valore mancante. I valori della varianza e della deviazione standard sono sempre 0, perché tramite i modelli Naive Bayes non è possibile modellare valori continui.  
  
###  <a name="sample-query-7-predicting-associations"></a><a name="bkmk_Query7"></a>Esempio di query 7: stima delle associazioni  
 L'algoritmo Microsoft Naive Bayes può essere utilizzato per l'analisi di associazione, se nella struttura di data mining è contenuta una tabella nidificata con l'attributo stimabile come chiave. Ad esempio, è possibile compilare un modello Naive Bayes tramite la struttura di data mining creata in [Lezione 3: Compilazione di uno scenario Market Basket &#40;Esercitazione intermedia sul data mining&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md) dell'esercitazione sul data mining. Il modello utilizzato in questo esempio è stato modificato per aggiungere informazioni sul reddito e sulla regione del cliente nella tabella del case.  
  
 Nell'esempio di query seguente viene illustrata una query singleton che stima prodotti relativi ad acquisti del prodotto, `'Road Tire Tube'`. È possibile utilizzare queste informazioni per consigliare prodotti a un tipo specifico di cliente.  
  
```  
SELECT   PredictAssociation([Association].[v Assoc Seq Line Items])  
FROM [Association_NB]  
NATURAL PREDICTION JOIN  
(SELECT 'High' AS [Income Group],  
  'Europe' AS [Region],  
  (SELECT 'Road Tire Tube' AS [Model])   
AS [v Assoc Seq Line Items])   
AS t  
```  
  
 Risultati parziali:  
  
|Modello|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
|Touring-2000|  
|Touring-1000|  
  
## <a name="function-list"></a>Elenco di funzioni  
 Tutti gli algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] supportano un set comune di funzioni. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes supporta tuttavia le funzioni aggiuntive elencate nella tabella seguente.  
  
|||  
|-|-|  
|Funzione di stima|Uso|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|Viene determinato se un nodo è figlio di un altro nodo nel modello.|  
|[Predict &#40;DMX&#41;](/sql/dmx/predict-dmx)|Viene restituito un valore, o un set di valori, stimato per una colonna specificata.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|Viene restituita la probabilità ponderata.|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|Viene stimata l'appartenenza a un set di dati associativo.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Viene restituito l'oggetto Node_ID per ogni case.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|Viene restituita la probabilità per il valore stimato.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Viene restituito il valore di supporto per uno stato specificato.|  
  
 Per la sintassi di funzioni specifiche, vedere [Guida di riferimento alle funzioni DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Vedi anche  
 [Riferimento tecnico per l'algoritmo Microsoft Naive Bayes](microsoft-naive-bayes-algorithm-technical-reference.md)   
 [Algoritmo Microsoft Naive Bayes](microsoft-naive-bayes-algorithm.md)   
 [Contenuto dei modelli di data mining per i modelli Naïve Bayes &#40;Analysis Services - Data mining&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  
