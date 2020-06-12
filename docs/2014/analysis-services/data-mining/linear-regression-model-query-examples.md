---
title: Esempi di query sul modello di regressione lineare | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- linear regression algorithms [Analysis Services]
- linear regression [Analysis Services]
- content queries [DMX]
ms.assetid: fd3cf312-57a1-44b6-b772-fce6fc1c26d7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 02d4b7309d7b5ea3d6295089f0fb2e778b1c9b4b
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522334"
---
# <a name="linear-regression-model-query-examples"></a>Esempi di query sul modello di regressione lineare
  Quando si crea una query su un modello di data mining, è possibile creare una query sul contenuto, che fornisce dettagli sui criteri individuati durante l'analisi, oppure una query di stima, che utilizza i criteri presenti nel modello di data mining per eseguire stime relative a nuovi dati. Una query sul contenuto potrebbe ad esempio fornire dettagli aggiuntivi sulla formula di regressione, mentre una query di stima potrebbe indicare se un nuovo punto dati si adatta al modello. Utilizzando una query è inoltre possibile recuperare metadati relativi al modello.  
  
 In questa sezione viene illustrato come creare query per i modelli basati sull'algoritmo Microsoft Linear Regression.  
  
> [!NOTE]  
>  Poiché la regressione lineare è basata su un case specifico dell'algoritmo Microsoft Decision Trees, sono presenti molte somiglianze e alcuni modelli di albero delle decisioni che utilizzano attributi stimabili continui possono contenere formule di regressione. Per altre informazioni, vedere [Guida di riferimento tecnico per l'algoritmo Microsoft Decision Trees](microsoft-decision-trees-algorithm-technical-reference.md).  
  
 **Query sul contenuto**  
  
 [Utilizzo del set di righe dello schema di data mining per determinare i parametri utilizzati per un modello](#bkmk_Query1)  
  
 [Utilizzo di DMX per restituire la formula di regressione per il modello](#bkmk_Query2)  
  
 [Restituzione solo del coefficiente per il modello](#bkmk_Query3)  
  
 **Query di stima**  
  
 [Stima del reddito mediante una query singleton](#bkmk_Query4)  
  
 [Utilizzo delle funzioni di stima con un modello di regressione](#bkmk_Query5)  
  
##  <a name="finding-information-about-the-linear-regression-model"></a><a name="bkmk_top"></a> Ricerca di informazioni sul modello di regressione lineare  
 La struttura di un modello di regressione lineare è estremamente semplice: il modello di data mining rappresenta i dati come nodo singolo che definisce la formula di regressione. Per altre informazioni, vedere [Contenuto dei modelli di data mining per i modelli di regressione logistica &#40;Analysis Services - Data mining&#41;](mining-model-content-for-logistic-regression-models.md).  
  
 [Torna all'inizio](#bkmk_top)  
  
###  <a name="sample-query-1-using-the-data-mining-schema-rowset-to-determine-parameters-used-for-a-model"></a><a name="bkmk_Query1"></a> Query di esempio 1: Utilizzo del set di righe dello schema di data mining per determinare i parametri utilizzati per un modello  
 Eseguendo una query sul set di righe dello schema di data mining, è possibile trovare i metadati relativi al modello. Tali dati potrebbero includere la data di creazione, la data dell'ultima elaborazione del modello, il nome della struttura di data mining sulla quale si basa il modello e il nome della colonna designata come attributo stimabile. È inoltre possibile restituire i parametri utilizzati durante la creazione del modello.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_PredictIncome'  
```  
  
 Risultati dell'esempio:  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY=0.9,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MINIMUM_SUPPORT=10,<br /><br /> SCORE_METHOD=4,<br /><br /> SPLIT_METHOD=3,<br /><br /> FORCE_REGRESSOR=|  
  
> [!NOTE]  
>  L'impostazione del parametro, "`FORCE_REGRESSOR =` ", indica che il valore corrente per il parametro FORCE_REGRESSOR è Null.  
  
 [Torna all'inizio](#bkmk_top)  
  
###  <a name="sample-query-2-retrieving-the-regression-formula-for-the-model"></a><a name="bkmk_Query2"></a> Query di esempio 2: Recupero della formula di regressione per il modello  
 Nella query seguente viene restituito il contenuto del modello di data mining per un modello di regressione lineare compilato utilizzando la stessa origine dati Targeted Mailing utilizzata in [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md). Questo modello esegue la stima del reddito del cliente in base all'età.  
  
 La query restituisce il contenuto del nodo che contiene la formula di regressione. Ogni variabile e ogni coefficiente vengono archiviati in una riga separata della tabella NODE_DISTRIBUTION nidificata. Se si vuole visualizzare la formula di regressione completa, usare il [Visualizzatore Microsoft Decision Trees](browse-a-model-using-the-microsoft-tree-viewer.md), fare clic sul nodo **(Tutti)** e aprire **Legenda data mining**.  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION as t  
FROM LR_PredictIncome.CONTENT  
```  
  
> [!NOTE]  
>  Se si fa riferimento a colonne singole della tabella nidificata usando una query quale `SELECT <column name> from NODE_DISTRIBUTION`, alcune colonne, ad esempio **SUPPORT** o **PROBABILITY**, devono essere racchiuse tra parentesi per distinguerle dalle parole chiave riservate con lo stesso nome.  
  
 Risultati previsti:  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Yearly Income|Missing|0|0,000457142857142857|0|1|  
|Yearly Income|57220,8876687257|17484|0,999542857142857|1041275619,52776|3|  
|Age|471.687717702463|0|0|126,969442359327|7|  
|Age|234.680904692439|0|0|0|8|  
|Age|45,4269617936399|0|0|126,969442359327|9|  
||35793,5477381267|0|0|1012968919,28372|11|  
  
 In **Legenda data mining**, invece, la formula di regressione appare come segue:  
  
 Yearly Income = 57,220.919 + 471.688 * (Age - 45.427)  
  
 È possibile notare che alcuni numeri di **Legenda data mining**sono arrotondati. In **Legenda data mining** sono tuttavia contenuti sostanzialmente gli stessi valori della tabella NODE_DISTRIBUTION.  
  
 I valori della colonna VALUETYPE indicano il tipo di informazioni contenuto in ogni riga. Questa indicazione risulta utile se i risultati vengono elaborati a livello di programmazione. Nella tabella seguente sono mostrati i tipi di valore che vengono restituiti per una formula di regressione lineare.  
  
|VALUETYPE|  
|---------------|  
|1 (Mancante)|  
|3 (Continuo)|  
|7 (Coefficiente)|  
|8 (Miglioramento punteggio)|  
|9 (Statistiche)|  
|7 (Coefficiente)|  
|8 (Miglioramento punteggio)|  
|9 (Statistiche)|  
|11 (Intercetta)|  
  
 Per altre informazioni sul significato di ciascun tipo di valore per i modelli di regressione, vedere [Contenuto dei modelli di data mining per i modelli di regressione lineare &#40;Analysis Services - Data mining&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md).  
  
 [Torna all'inizio](#bkmk_top)  
  
###  <a name="sample-query-3-returning-only-the-coefficient-for-the-model"></a><a name="bkmk_Query3"></a> Query di esempio 3: Restituzione solo del coefficiente per il modello  
 Utilizzando l'enumerazione VALUETYPE, è possibile restituire solo il coefficiente per l'equazione di regressione, come mostrato nella query seguente:  
  
```  
SELECT FLATTENED MODEL_NAME,  
    (SELECT ATTRIBUTE_VALUE, VALUETYPE  
     FROM NODE_DISTRIBUTION  
     WHERE VALUETYPE = 11)   
AS t  
FROM LR_PredictIncome.CONTENT  
```  
  
 Questa query restituisce due righe, una dal contenuto del modello di data mining e la riga dalla tabella nidificata che contiene il coefficiente. La colonna ATTRIBUTE_NAME non è inclusa, in quanto è sempre vuota per il coefficiente.  
  
|MODEL_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|-----------------|------------------------|-----------------|  
|LR_PredictIncome|||  
|LR_PredictIncome|35793,5477381267|11|  
  
 [Torna all'inizio](#bkmk_top)  
  
## <a name="making-predictions-from-a-linear-regression-model"></a>Esecuzione di stime da un modello di regressione lineare  
 È possibile compilare query di stima sui modelli di regressione lineare utilizzando la scheda Stima modello di data mining in Progettazione modelli di data mining. Il generatore della query di stima è disponibile sia in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , sia in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  È inoltre possibile creare query nei modelli di regressione usando i componenti aggiuntivi Data mining di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] per Excel oppure i componenti aggiuntivi data mining di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] per Excel. Anche se i componenti aggiuntivi Data mining per Excel non creano modelli di regressione, è possibile esplorare ed eseguire una query su qualsiasi modello di data mining archiviato in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 [Torna all'inizio](#bkmk_top)  
  
###  <a name="sample-query-4-predicting-income-using-a-singleton-query"></a><a name="bkmk_Query4"></a> Esempio di query 4: Stima del reddito mediante una query singleton  
 Il modo più semplice per creare una query singleton su un modello di regressione consiste nell'usare la finestra di dialogo **Input query singleton** . È ad esempio possibile compilare la query DMX seguente selezionando il modello di regressione appropriato, scegliendo **query singleton**, quindi digitando `20` come valore per **Age**.  
  
```  
SELECT [LR_PredictIncome].[Yearly Income]  
From   [LR_PredictIncome]  
NATURAL PREDICTION JOIN  
(SELECT 20 AS [Age]) AS t  
```  
  
 Risultati dell'esempio:  
  
|Yearly Income|  
|-------------------|  
|45227,302092176|  
  
 [Torna all'inizio](#bkmk_top)  
  
###  <a name="sample-query-5-using-prediction-functions-with-a-regression-model"></a><a name="bkmk_Query5"></a> Esempio di query 5: Utilizzo delle funzioni di stima con un modello di regressione  
 È possibile utilizzare molte delle funzioni di stima standard con i modelli di regressione lineare. Nell'esempio seguente viene illustrato come aggiungere alcune statistiche descrittive ai risultati della query di stima. Da questi risultati è possibile notare che esiste una deviazione significativa dalla media per questo modello.  
  
```  
SELECT  
  ([LR_PredictIncome].[Yearly Income]) as [PredIncome],  
  (PredictStdev([LR_PredictIncome].[Yearly Income])) as [StDev1]  
From  
  [LR_PredictIncome]  
NATURAL PREDICTION JOIN  
(SELECT 20 AS [Age]) AS t  
```  
  
 Risultati dell'esempio:  
  
|Yearly Income|StDev1|  
|-------------------|------------|  
|45227,302092176|31827,1726561396|  
  
 [Torna all'inizio](#bkmk_top)  
  
## <a name="list-of-prediction-functions"></a>Elenco delle funzioni di stima  
 Tutti gli algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] supportano un set comune di funzioni. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression supporta tuttavia le funzioni aggiuntive elencate nella tabella seguente.  
  
|||  
|-|-|  
|Funzione di stima|Utilizzo|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|Viene determinato se un nodo è figlio di un altro nodo nel modello.|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|Indica se il nodo specificato contiene o meno il case corrente.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|Viene restituito un valore, o un set di valori, stimato per una colonna specificata.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Viene restituito l'oggetto Node_ID per ogni case.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|Viene restituita la deviazione standard per il valore stimato.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Viene restituito il valore di supporto per uno stato specificato.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Restituisce la varianza di una colonna specificata.|  
  
 Per un elenco delle funzioni comuni a tutti gli algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)], vedere [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining-algorithms-analysis-services-data-mining.md). Per altre informazioni su come usare queste funzioni, vedere [Guida di riferimento alle funzioni DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Linear regressione](microsoft-linear-regression-algorithm.md)   
 [Query di data mining](data-mining-queries.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Linear regressione](microsoft-linear-regression-algorithm-technical-reference.md)   
 [Contenuto dei modelli di data mining per i modelli di regressione lineare &#40;Analysis Services - Data mining&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
