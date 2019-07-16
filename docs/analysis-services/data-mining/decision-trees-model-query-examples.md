---
title: Esempi di Query del modello Decision Trees | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2045dfa9923fb745f0f9d3936579a4e73a50564
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210066"
---
# <a name="decision-trees-model-query-examples"></a>Esempi di query sul modello di alberi delle decisioni
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando si crea una query su un modello di data mining, è possibile creare una query sul contenuto, che fornisce dettagli sui criteri individuati durante l'analisi, oppure una query di stima, che utilizza i criteri presenti nel modello di data mining per eseguire stime relative a nuovi dati. Una query sul contenuto per un modello Decision Trees, ad esempio, può fornire statistiche sul numero di case a ogni livello dell'albero o le regole che consentono di distinguere i case. In alternativa, una query di stima esegue il mapping del modello ai nuovi dati per generare indicazioni, classificazioni e così via. Utilizzando una query è inoltre possibile recuperare metadati relativi al modello.  
  
 In questa sezione viene illustrato come creare query per i modelli basati sull'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees.  
  
 **Query sul contenuto**  
  
 [Recupero di parametri di modello dal set di righe dello schema di data mining](#bkmk_Query1)  
  
 [Recupero di dettagli sugli alberi nel modello tramite DMX](#bkmk_Query2)  
  
 [Recupero di sottoalberi dal modello](#bkmk_Query3)  
  
 **Query di stima**  
  
 [Restituzione di stime con probabilità](#bkmk_Query4)  
  
 [Stima delle associazioni da un modello Decision Trees](#bkmk_Query5)  
  
 [Recupero di una formula di regressione da un modello Decision Trees](#bkmk_Query6)  
  
##  <a name="bkmk_top2"></a> Ricerca di informazioni su un modello Decision Trees  
 Per creare query significative sul contenuto di un modello Decision Trees, è necessario comprendere la struttura del contenuto del modello ed essere in grado di individuare il tipo di informazioni archiviate dai diversi tipi di nodo. Per altre informazioni, vedere [Contenuto dei modelli di data mining per i modelli di albero delle decisioni &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Query1"></a> Esempio di Query 1: Recupero di parametri di modello dal set di righe dello schema di data mining  
 L'esecuzione di una query sul set di righe dello schema di data mining consente di trovare i metadati relativi al modello, ad esempio la data e l'ora di creazione, la data e l'ora dell'ultima elaborazione, il nome della struttura di data mining su cui si basa il modello e il nome della colonna utilizzata come attributo stimabile. È inoltre possibile restituire i parametri utilizzati durante la creazione del modello.  
  
```  
select MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Decision Tree'  
```  
  
 Risultati dell'esempio:  
  
 MINING_PARAMETERS  
  
 COMPLEXITY_PENALTY=0.5, MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_OUTPUT_ATTRIBUTES=255,MINIMUM_SUPPORT=10,SCORE_METHOD=4,SPLIT_METHOD=3,FORCE_REGRESSOR=  
  
###  <a name="bkmk_Query2"></a> Esempio di Query 2: Restituzione di dettagli sul contenuto del modello tramite DMX  
 La query seguente restituisce alcune informazioni di base sugli alberi delle decisioni creati al momento della compilazione del modello in [Esercitazione di base sul data mining](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Ogni albero viene archiviato nel proprio nodo. Poiché il modello contiene un singolo attributo stimabile, è presente un solo nodo dell'albero. Se, tuttavia, si crea un modello di associazione utilizzando l'algoritmo Decision Trees, potrebbero essere presenti centinaia di alberi, uno per ciascun prodotto.  
  
 La query restituisce tutti i nodi di tipo 2, ovvero i nodi di livello superiore di un albero che rappresenta un attributo stimabile specifico.  
  
> [!NOTE]  
>  La colonna CHILDREN_CARDINALITY deve essere racchiusa tra parentesi per distinguerla dalla parola chiave riservata MDX con lo stesso nome.  
  
```  
SELECT MODEL_NAME, NODE_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY]  
FROM TM_DecisionTrees.CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 Risultati dell'esempio:  
  
|MODEL_NAME|NODE_NAME|NODE_CAPTION|NODE_SUPPORT|CHILDREN_CARDINALITY|  
|-----------------|----------------|-------------------|-------------------|---------------------------|  
|TM_DecisionTree|000000001|Tutti|12939|5|  
  
 Significato dei risultati In un modello Decision Trees la cardinalità di un nodo specifico indica il numero di figli immediati del nodo. La cardinalità per questo nodo è 5, pertanto il modello ha diviso in cinque sottogruppi la popolazione di destinazione dei potenziali acquirenti di biciclette.  
  
 La query correlata seguente restituisce i figli per questi cinque sottogruppi, insieme alla distribuzione di attributi e valori nei nodi figlio. Poiché le statistiche relative, ad esempio, a supporto, probabilità e varianza vengono archiviate nella tabella annidata NODE_DISTRIBUTION, nell'esempio viene usata la parola chiave `FLATTENED` per restituire le colonne della tabella annidata.  
  
> [!NOTE]  
>  La colonna della tabella annidata SUPPORT deve essere racchiusa tra parentesi per essere distinta dalla parola chiave riservata con lo stesso nome.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT]  
FROM NODE_DISTRIBUTION) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE [PARENT_UNIQUE_NAME] = '000000001'  
```  
  
 Risultati dell'esempio:  
  
|NODE_NAME|NODE_CAPTION|T.ATTRIBUTE_NAME|T.ATTRIBUTE_VALUE|SUPPORT|  
|----------------|-------------------|-----------------------|------------------------|-------------|  
|00000000100|Number Cars Owned = 0|Bike Buyer|Missing|0|  
|00000000100|Number Cars Owned = 0|Bike Buyer|0|1067|  
|00000000100|Number Cars Owned = 0|Bike Buyer|1|1875|  
|00000000101|Number Cars Owned = 3|Bike Buyer|Missing|0|  
|00000000101|Number Cars Owned = 3|Bike Buyer|0|678|  
|00000000101|Number Cars Owned = 3|Bike Buyer|1|473|  
  
 Da questi risultati è possibile determinare che tra i clienti che hanno acquistato una bicicletta ([Bike Buyer] = 1), 1067 possiedono 0 automobili e 473 ne possiedono 3.  
  
###  <a name="bkmk_Query3"></a> Esempio di Query 3: Recupero di sottoalberi dal modello  
 Si supponga di voler individuare altre informazioni sui clienti che hanno acquistato una bicicletta. È possibile visualizzare dettagli aggiuntivi per uno dei sottoalberi usando la funzione [IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md) nella query, come illustrato nell'esempio seguente. La query restituisce il conteggio di acquirenti di biciclette recuperando nodi foglia (NODE_TYPE = 4) dall'albero che contiene i clienti di età maggiore di 42 anni. La query consente di limitare le righe della tabella nidificata a quelle in cui Bike Buyer = 1.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,NODE_TYPE,  
(  
SELECT [SUPPORT] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Bike Buyer' AND ATTRIBUTE_VALUE = '1'  
) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE ISDESCENDANT('0000000010001')  
AND NODE_TYPE = 4  
```  
  
 Risultati dell'esempio:  
  
|NODE_NAME|NODE_CAPTION|t.SUPPORT|  
|----------------|-------------------|---------------|  
|000000001000100|Yearly Income >= 26000 and < 42000|266|  
|00000000100010100|Total Children = 3|75|  
|0000000010001010100|Number Children At Home = 1|75|  
  
## <a name="making-predictions-using-a-decision-trees-model"></a>Esecuzione di stime tramite un modello Decision Trees  
 Poiché gli alberi delle decisioni possono essere utilizzati per svariate attività, incluse la classificazione, la regressione e persino l'associazione, quando si crea una query di stima su un modello Decision Trees, sono disponibili numerose opzioni. Per comprendere i risultati della stima, è necessario saper individuare lo scopo per cui è stato creato il modello. Negli esempi di query seguenti vengono illustrati tre scenari diversi:  
  
-   Restituzione di una stima per un modello di classificazione, insieme alla probabilità che la stima sia corretta, quindi applicazione di un filtro ai risultati in base alla probabilità.  
  
-   Creazione di una query singleton per stimare le associazioni.  
  
-   Recupero della formula di regressione per una parte di un albero delle decisioni in cui la relazione tra l'input e l'output è lineare.  
  
###  <a name="bkmk_Query4"></a> Esempio di Query 4: Restituzione di stime con probabilità  
 Nella query di esempio seguente viene usato il modello di albero delle decisioni creato in [Esercitazione di base sul data mining](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). La query passa in un nuovo set di dati di esempio, dalla tabella dbo.ProspectiveBuyers a [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW, per determinare i clienti inclusi nel nuovo set di dati che acquisteranno una bicicletta.  
  
 La query usa la funzione di stima [PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)che restituisce una tabella annidata contenente informazioni utili sulle probabilità individuate dal modello. La clausola WHERE finale della query filtra i risultati per restituire solo i clienti stimati come probabili acquirenti di una bicicletta per oltre lo 0%.  
  
```  
SELECT  
  [TM_DecisionTree].[Bike Buyer],  
  PredictHistogram([Bike Buyer]) as Results  
From  
  [TM_DecisionTree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [FirstName],  
      [LastName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM_DecisionTree].[First Name] = t.[FirstName] AND  
  [TM_DecisionTree].[Last Name] = t.[LastName] AND  
  [TM_DecisionTree].[Marital Status] = t.[MaritalStatus] AND  
  [TM_DecisionTree].[Gender] = t.[Gender] AND  
  [TM_DecisionTree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM_DecisionTree].[Total Children] = t.[TotalChildren] AND  
  [TM_DecisionTree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM_DecisionTree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM_DecisionTree].[Number Cars Owned] = t.[NumberCarsOwned]  
WHERE [Bike Buyer] = 1  
AND PredictProbability([Bike Buyer]) >'.05'  
```  
  
 Per impostazione predefinita, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce tabelle annidate con l'etichetta di colonna **Expression**. È possibile modificare questa etichetta applicando un alias alla colonna restituita. In tal caso l'alias, in questo esempio **Results**, viene usato sia come intestazione di colonna sia come valore nella tabella annidata. Per visualizzare i risultati, è necessario espandere la tabella nidificata.  
  
 Risultati di esempio con **Bike Buyer** = 1:  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|1|2540|0.634849242045644|0.013562168281562|0|0|  
|0|1460|0.364984174579377|0.00661336932550915|0|0|  
||0|0.000166583374979177|0.000166583374979177|0|0|  
  
 Se il provider non supporta set di righe gerarchici, ad esempio quelli illustrati in questo esempio, è possibile utilizzare la parola chiave FLATTENED nella query per restituire i risultati come tabella contenente valori Null al posto dei valori di colonna ripetuti. Per altre informazioni, vedere [Tabelle annidate &40#;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md) o [Informazioni sull'istruzione DMX Select](../../dmx/understanding-the-dmx-select-statement.md).  
  
###  <a name="bkmk_Query5"></a> Esempio di Query 5: Stima delle associazioni da un modello Decision Trees  
 La query di esempio seguente si basa sulla struttura di data mining di associazione. Per proseguire con l'esempio, è possibile aggiungere un nuovo modello a questa struttura di data mining e selezionare Microsoft Decision Trees come algoritmo. Per altre informazioni su come creare la struttura di data mining di associazione, vedere [lezione 3: Creazione di uno Scenario Market Basket &#40;esercitazione intermedia sul Data Mining&#41;](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a).  
  
 La query di esempio seguente è una query singleton, che può essere creata facilmente in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] scegliendo i campi desiderati e selezionando i valori per i campi in un elenco a discesa.  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
FROM  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Patch kit' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Risultati previsti:  
  
|Modello|  
|-----------|  
|Mountain-200|  
|Mountain Tire Tube|  
|Touring Tire Tube|  
  
 I risultati indicano i tre prodotti migliori da consigliare ai clienti che hanno acquistato un prodotto Patch Kit. È inoltre possibile specificare più prodotti come input per i suggerimenti forniti, digitando i valori o usando la finestra di dialogo **Input query singleton** e aggiungendo o rimuovendo valori. Nella query di esempio seguente viene illustrato il modo in cui vengono specificati più valori su cui basare la stima. I valori sono collegati da una clausola UNION nell'istruzione SELECT che consente di definire i valori di input.  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
From  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Racing Socks' AS [Model]  
  UNION SELECT 'Women''s Mountain Shorts' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Risultati previsti:  
  
|Modello|  
|-----------|  
|Long-Sleeve Logo Jersey|  
|Mountain-400-W|  
|Classic Vest|  
  
###  <a name="bkmk_Query6"></a> Esempio di Query 6: Recupero di una formula di regressione da un modello Decision Trees  
 Quando si crea un modello Decision Trees che contiene una regressione su un attributo continuo, è possibile utilizzare la formula di regressione per eseguire stime oppure estrarre le informazioni sulla formula di regressione. Per altre informazioni sulle query sui modelli di regressione, vedere [Esempi di query sul modello di regressione lineare](../../analysis-services/data-mining/linear-regression-model-query-examples.md).  
  
 Se un modello Decision Trees contiene una combinazione di nodi di regressione e nodi suddivisi in intervalli o attributi discreti, è possibile creare una query che restituisca solo il nodo di regressione. La tabella NODE_DISTRIBUTION contiene i dettagli della formula di regressione. In questo esempio le colonne sono bidimensionali e la tabella NODE_DISTRIBUTION è associata a un alias per semplificare la visualizzazione. In questo modello, tuttavia, non è stato individuato alcun regressore da correlare a Income con altri attributi continui. In questi casi, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce il valore medio dell'attributo e la varianza totale nel modello per l'attributo.  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM DT_Predict. CONTENT  
WHERE NODE_TYPE = 25  
```  
  
 Risultati dell'esempio:  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Yearly Income|Missing|0|0,000457142857142857|0|1|  
|Yearly Income|57220,8876687257|17484|0,999542857142857|1041275619,52776|3|  
||57220,8876687257|0|0|1041216662.54387|11|  
  
 Per altre informazioni sui tipi di valore e le statistiche usate nei modelli di regressione, vedere [Contenuto dei modelli di data mining per i modelli di regressione lineare &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md).  
  
## <a name="list-of-prediction-functions"></a>Elenco delle funzioni di stima  
 Tutti gli algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] supportano un set comune di funzioni. L'algoritmo Decision Trees di [!INCLUDE[msCoName](../../includes/msconame-md.md)] supporta tuttavia le funzioni aggiuntive elencate nella tabella seguente.  
  
|||  
|-|-|  
|Funzione di stima|Uso|  
|[IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md)|Viene determinato se un nodo è figlio di un altro nodo nel modello.|  
|[IsInNode &#40;DMX&#41;](../../dmx/isinnode-dmx.md)|Indica se il nodo specificato contiene o meno il case corrente.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../../dmx/predictadjustedprobability-dmx.md)|Viene restituita la probabilità ponderata.|  
|[PredictAssociation &#40;DMX&#41;](../../dmx/predictassociation-dmx.md)|Viene stimata l'appartenenza a un set di dati associativo.|  
|[PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|Viene restituita una tabella di valori correlati ai valori stimati correnti.|  
|[PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md)|Viene restituito l'oggetto Node_ID per ogni case.|  
|[PredictProbability &#40;DMX&#41;](../../dmx/predictprobability-dmx.md)|Viene restituita la probabilità per il valore stimato.|  
|[PredictStdev &#40;DMX&#41;](../../dmx/predictstdev-dmx.md)|Restituisce la deviazione standard stimata per la colonna specificata.|  
|[PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|Viene restituito il valore di supporto per uno stato specificato.|  
|[PredictVariance &#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|Restituisce la varianza di una colonna specificata.|  
  
 Per un elenco delle funzioni comuni a tutti gli algoritmi di [!INCLUDE[msCoName](../../includes/msconame-md.md)], vedere [Funzioni di stima correlate &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md). Per la sintassi di funzioni specifiche, vedere [Guida di riferimento alle funzioni DMX &#40;Data Mining Extensions&#41;](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Query di data mining](../../analysis-services/data-mining/data-mining-queries.md)   
 [Algoritmo Microsoft Decision Trees](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)   
 [Guida di riferimento tecnico per l'algoritmo Microsoft Decision Trees](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)   
 [Contenuto dei modelli di data mining per i modelli di albero delle decisioni &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
