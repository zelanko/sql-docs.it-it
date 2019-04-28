---
title: Esempi di Query del modello di associazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- association algorithms [Analysis Services]
- rules [Data Mining]
- association rules
- content queries [DMX]
ms.assetid: 68b39f5c-c439-44ac-8046-6f2d36649059
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 268685c489d03f7e9055042ab613223146f89600
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62689558"
---
# <a name="association-model-query-examples"></a>Esempi di query sul modello di associazione
  Quando si crea una query su un modello di data mining, è possibile creare una query sul contenuto, tramite cui vengono forniti dettagli sulle regole e i set di elementi individuati durante l'analisi oppure una query di stima, in cui vengono utilizzate le associazioni individuate nei dati per eseguire stime. Per un modello di associazione, le stime sono in genere basate su regole e possono essere utilizzate per fornire indicazioni, mentre le query sul contenuto solitamente esplorano la relazione tra set di elementi. È anche possibile recuperare metadati relativi al modello.  
  
 Questa sezione illustra come creare questi tipi di query per i modelli basati sull'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules.  
  
 **Query sul contenuto**  
  
 [Recupero di dati dei metadati del modello tramite DMX](#bkmk_Query1)  
  
 [Recupero di metadati dal set di righe dello schema](#bkmk_Query2)  
  
 [Recupero dei parametri originali per il modello](#bkmk_Query3)  
  
 [Recupero di un elenco di set di elementi e prodotti](#bkmk_Query4)  
  
 [Restituzione dei primi 10 set di elementi](#bkmk_Query5)  
  
 **Query di stima**  
  
 [Stima degli elementi associati](#bkmk_Query6)  
  
 [Determinazione della confidenza per i set di elementi correlati](#bkmk_Query7)  
  
##  <a name="bkmk_top2"></a> Ricerca di informazioni sul modello  
 In tutti i modelli di data mining viene esposto il contenuto appreso dall'algoritmo secondo uno schema standardizzato, definito set di righe dello schema del modello di data mining. È possibile creare query sul set di righe dello schema del modello di data mining tramite istruzioni Data Mining Extensions (DMX) oppure utilizzando stored procedure [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]è anche possibile eseguire query sui set di righe dello schema direttamente come tabelle di sistema, utilizzando una sintassi simile a SQL.  
  
###  <a name="bkmk_Query1"></a> Esempio di Query 1: Recupero di metadati del modello tramite DMX  
 Con la query seguente vengono restituiti i metadati relativi al modello di associazione `Association`, ad esempio il nome del modello, il database in cui è archiviato e il numero di nodi figlio del modello. Questa query utilizza una query contenuto DMX per recuperare i metadati dal nodo padre del modello:  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  È necessario includere il nome della colonna CHILDREN_CARDINALITY tra parentesi quadre per distinguerlo dalla parola chiave riservata MDX con lo stesso nome.  
  
 Risultati dell'esempio:  
  
|||  
|-|-|  
|MODEL_CATALOG|Association Test|  
|MODEL_NAME|Association Rules|  
|NODE_CAPTION|Association Rules Model|  
|NODE_SUPPORT|14879|  
|CHILDREN_CARDINALITY|942|  
|NODE_DESCRIPTION|Association Rules Model; ITEMSET_COUNT=679; RULE_COUNT=263; MIN_SUPPORT=14; MAX_SUPPORT=4334; MIN_ITEMSET_SIZE=0; MAX_ITEMSET_SIZE=3; MIN_PROBABILITY=0.400390625; MAX_PROBABILITY=1; MIN_LIFT=0.14309369632511; MAX_LIFT=1.95758227647523|  
  
 Per una definizione del significato di queste colonne in un modello di associazione, vedere [Contenuto dei modelli di data mining per i modelli di associazione &#40;Analysis Services - Data mining&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a> Esempio di Query 2: Recupero di metadati aggiuntivi dal set di righe dello Schema  
 Se si esegue una query sul set di righe dello schema di data mining, è possibile trovare le stesse informazioni restituite in una query contenuto DMX. Tuttavia, il set di righe dello schema fornisce alcune colonne aggiuntive, ad esempio la data dell'ultima elaborazione del modello, la struttura di data mining e il nome della colonna utilizzata come attributo stimabile.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, SERVICE_NAME, PREDICTION_ENTITY,   
MINING_STRUCTURE, LAST_PROCESSED  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 Risultati dell'esempio:  
  
|||  
|-|-|  
|MODEL_CATALOG|Adventure Works DW Multidimensional 2012|  
|MODEL_NAME|Association Rules|  
|SERVICE_NAME|Association Rules Model|  
|PREDICTION_ENTITY|v Assoc Seq Line Items|  
|MINING_STRUCTURE|Association Rules|  
|LAST_PROCESSED|9/29/2007 10:21:24 PM|  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="bkmk_Query3"></a> Esempio di Query 3: Recupero dei parametri originali per il modello  
 Con la query seguente viene restituita una singola colonna contenente i dettagli sulle impostazioni dei parametri utilizzate durante la creazione del modello.  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 Risultati dell'esempio:  
  
 MAXIMUM_ITEMSET_COUNT=200000,MAXIMUM_ITEMSET_SIZE=3,MAXIMUM_SUPPORT=1,MINIMUM_SUPPORT=9.40923449156529E-04,MINIMUM_IMPORTANCE=-999999999,MINIMUM_ITEMSET_SIZE=0,MINIMUM_PROBABILITY=0.4  
  
 [Torna all'inizio](#bkmk_top2)  
  
## <a name="finding-information-about-rules-and-itemsets"></a>Ricerca di informazioni su regole e set di elementi  
 Un modello di associazione viene utilizzato in genere per individuare informazioni sui set di elementi frequenti e per estrarre dettagli su regole e set di elementi specifici. Ad esempio, è possibile che si desideri estrarre un elenco di regole classificate come particolarmente interessanti o creare un elenco dei set di elementi più comuni. Tali informazioni vengono recuperate tramite una query sul contenuto DMX. È anche possibile esplorare queste informazioni usando il **Visualizzatore Microsoft Association Rules**.  
  
###  <a name="bkmk_Query4"></a> Esempio di Query 4: Recupero dell'elenco di set di elementi e prodotti  
 Con la query seguente vengono recuperati tutti i set di elementi, insieme a una tabella nidificata in cui sono elencati i prodotti inclusi in ognuno di essi. La colonna NODE_NAME contiene l'ID univoco del set di elementi all'interno del modello, mentre NODE_CAPTION fornisce una descrizione di testo degli elementi. In questo esempio la tabella nidificata è bidimensionale, in modo che il set di elementi che contiene due prodotti genera due righe nei risultati. È possibile omettere la parola chiave FLATTENED se il client supporta dati gerarchici.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
NODE_PROBABILITY, NODE_SUPPORT,  
(SELECT ATTRIBUTE_NAME FROM NODE_DISTRIBUTION) as PurchasedProducts  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 Risultati dell'esempio:  
  
|||  
|-|-|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
|NODE_PROBABILITY|0.291283016331743|  
|NODE_SUPPORT|4334|  
|PURCHASEDPRODUCTS.ATTRIBUTE_NAME|v Assoc Seq Line Items(Sport-100)|  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a> Esempio di Query 5: Restituisce i primi 10 set di elementi  
 In questo esempio viene illustrato come utilizzare alcune delle funzioni di raggruppamento e ordinamento disponibili per impostazione predefinita tramite DMX. La query restituisce i primi 10 set di elementi ordinati per supporto per ogni nodo. Si noti che non è necessario raggruppare in modo esplicito i risultati, come avviene invece in Transact-SQL; tuttavia, è possibile utilizzare un'unica funzione di aggregazione in ogni query.  
  
```  
SELECT TOP 10 (NODE_SUPPORT),NODE_NAME, NODE_CAPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 Risultati dell'esempio:  
  
|||  
|-|-|  
|NODE_SUPPORT|4334|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
  
 [Torna all'inizio](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>Esecuzione di stime tramite il modello  
 Un modello di regole di associazione viene spesso utilizzato per generare indicazioni basate sulle correlazioni individuate nei set di elementi. Pertanto, quando si crea una query di stima basata su un modello di regole di associazione, si utilizzano in genere le regole nel modello per fare supposizioni basate sui nuovi dati.  [PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx) è la funzione che restituisce indicazioni e dispone di diversi argomenti utilizzabili per personalizzare i risultati della query.  
  
 Le query su un modello di associazione possono anche risultare utili, ad esempio, per restituire la confidenza di varie regole e di vari set di elementi, in modo da confrontare l'efficacia di diverse strategie di cross-selling. Negli esempi seguenti viene illustrato come creare tali query.  
  
###  <a name="bkmk_Query6"></a> Esempio di Query 6: Stima degli elementi associati  
 Questo esempio illustra il modello di associazione creato in [Esercitazione intermedia sul data mining &#40;Analysis Services - Data mining&#41;](../../tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md). Viene illustrato come creare una query di stima che indica quali prodotti consigliare a un cliente che ha acquistato un determinato prodotto. Questo tipo di query, in cui i valori vengono forniti al modello in un'istruzione `SELECT...UNION`, è denominata query singleton. Poiché la colonna del modello stimabile che corrisponde ai nuovi valori è una tabella nidificata, è necessario utilizzare una clausola `SELECT` per eseguire il mapping del nuovo valore alla colonna della tabella nidificata, `[Model]`, e un'altra clausola `SELECT` per eseguire il mapping della colonna della tabella nidificata alla colonna a livello di case, `[v Assoc Seq Line Items]`. L'aggiunta della parola chiave INCLUDE-STATISTICS alla query consente di vedere la probabilità e il supporto per le indicazioni.  
  
```  
SELECT PredictAssociation([Association].[vAssocSeqLineItems],INCLUDE_STATISTICS, 3)  
FROM [Association]  
NATURAL PREDICTION JOIN   
(SELECT  
(SELECT 'Classic Vest' as [Model])  
AS [v Assoc Seq Line Items])  
AS t  
```  
  
 Risultati dell'esempio:  
  
|Modello|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283|0.252696|  
|Water Bottle|2866|0.19262|0.175205|  
|Patch kit|2113|0.142012|0.132389|  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a> Esempio di Query 7: Determinazione della confidenza per i set di elementi correlati  
 Mentre le regole sono utili per generare indicazioni, i set di elementi sono più interessanti per un'analisi più approfondita dei modelli nel set di dati. Se ad esempio le indicazioni restituiti con la query dell'esempio precedente non sono soddisfacenti, è possibile esaminare altri set di elementi che contengono il Prodotto A per valutare in modo più efficace se il Prodotto A è un accessorio che i clienti tendono ad acquistare con tutti i tipi di prodotti o se è strettamente correlato all'acquisto di determinati prodotti. Il modo più semplice per esplorare queste relazioni consiste nel filtrare i set di elementi nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association. Tuttavia, è possibile recuperare le stesse informazioni con una query.  
  
 Con la query di esempio seguente vengono restituiti tutti i set di elementi che includono l'articolo Water Bottle, incluso il singolo articolo Water Bottle.  
  
```  
SELECT TOP 100 FROM   
(  
SELECT FLATTENED NODE_CAPTION, NODE_SUPPORT,   
(SELECT ATTRIBUTE_NAME from NODE_DISTRIBUTION  
WHERE ATTRIBUTE_NAME = 'v Assoc Seq Line Items(Water Bottle)') as D  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
) AS Items  
WHERE [D.ATTRIBUTE_NAME] <> NULL  
ORDER BY NODE_SUPPORT DESC  
```  
  
 Risultati dell'esempio:  
  
|NODE_CAPTION|NODE_SUPPORT|D.ATTRIBUTE_NAME|  
|-------------------|-------------------|-----------------------|  
|Water Bottle = Existing|2866|v Assoc Seq Line Items(Water Bottle)|  
|Mountain Bottle Cage = Existing, Water Bottle = Existing|1136|v Assoc Seq Line Items(Water Bottle)|  
|Road Bottle Cage = Existing, Water Bottle = Existing|1068|v Assoc Seq Line Items(Water Bottle)|  
|Water Bottle = Existing, Sport-100 = Existing|734|v Assoc Seq Line Items(Water Bottle)|  
  
 Tramite questa query vengono restituite le righe della tabella nidificata che corrispondono ai criteri e tutte le righe della tabella esterna o del case. Pertanto, è necessario aggiungere una condizione che consente di eliminare le righe della tabella del case contenenti valori Null per il nome dell'attributo di destinazione.  
  
 [Torna all'inizio](#bkmk_top2)  
  
## <a name="function-list"></a>Elenco di funzioni  
 Tutti gli algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] supportano un set comune di funzioni. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules supporta tuttavia le funzioni aggiuntive elencate nella tabella seguente.  
  
|||  
|-|-|  
|Funzione di stima|Uso|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|Viene determinato se un nodo è figlio di un altro nodo nel grafico della rete neurale.|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|Indica se il nodo specificato contiene o meno il case corrente.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|Viene restituita la probabilità ponderata.|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|Viene stimata l'appartenenza a un set di dati associativo.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|Viene restituita una tabella di valori correlati ai valori stimati correnti.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Viene restituito l'oggetto Node_ID per ogni case.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|Viene restituita la probabilità per il valore stimato.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Viene restituito il valore di supporto per uno stato specificato.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Viene restituita la varianza per il valore stimato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Association Rules](microsoft-association-algorithm.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Association Rules](microsoft-association-algorithm-technical-reference.md)   
 [Contenuto dei modelli di data mining per i modelli di associazione &#40;Analysis Services - Data mining&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
