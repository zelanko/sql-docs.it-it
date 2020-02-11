---
title: Esempi di query sul modello di rete neurale | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- neural network algorithms [Analysis Services]
- content queries [DMX]
- neural network model [Analysis Services]
ms.assetid: 81b06183-620f-4e0c-bc10-532e6a1f0829
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a249a83aba62c7881be024caa3931cb5ad07204
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66083289"
---
# <a name="neural-network-model-query-examples"></a>Esempi di query sul modello di rete neurale
  Quando si crea una query su un modello di data mining, è possibile creare una query sul contenuto che consente di ottenere dettagli sui criteri individuati durante l'analisi oppure una query di stima in cui vengono utilizzati i criteri presenti nel modello per eseguire stime relative a nuovi dati. Una query sul contenuto per un modello di rete neurale potrebbe ad esempio recuperare metadati del modello, quale il numero di livelli nascosti. In alternativa, una query di stima potrebbe suggerire classificazioni basate su un input e, facoltativamente, indicare le probabilità per ogni classificazione.  
  
 In questa sezione viene illustrato come creare query per i modelli basati sull'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network.  
  
 **Query sul contenuto**  
  
 [Recupero di metadati del modello tramite DMX](#bkmk_Query1)  
  
 [Recupero di metadati del modello dal set di righe dello schema](#bkmk_Query2)  
  
 [Recupero degli attributi di input per il modello](#bkmk_Query3)  
  
 [Recupero di pesi dal livello nascosto](#bkmk_Query4)  
  
 **Query di stima**  
  
 [Creazione di una stima singleton](#bkmk_Query5)  
  
## <a name="finding-information-about-a-neural-network-model"></a>Ricerca di informazioni su un modello di rete neurale  
 In tutti i modelli di data mining viene esposto il contenuto appreso dall'algoritmo secondo uno schema standardizzato, definito set di righe dello schema del modello di data mining. Queste informazioni forniscono dettagli sul modello e includono i metadati di base, le strutture individuate nell'analisi e i parametri utilizzati in fase di elaborazione. È possibile creare query sul contenuto del modello tramite istruzioni DMX (Data Mining Extension).  
  
###  <a name="bkmk_Query1"></a>Esempio di query 1: recupero di metadati del modello tramite DMX  
 Nella query seguente vengono restituiti metadati di base relativi a un modello compilato tramite l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network. In un modello di rete neurale il nodo padre include solo il nome del modello, il nome del database in cui questo è archiviato e il numero di nodi figlio. Il nodo delle statistiche marginali (NODE_TYPE = 24) fornisce tuttavia sia questi metadati di base, sia alcune statistiche derivate relative alle colonne di input utilizzate nel modello.  
  
 La query di esempio seguente è basata sul modello di data mining creato nell' [Esercitazione intermedia sul data mining](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md), denominato `Call Center Default NN`. Il modello utilizza i dati di un call center per esplorare le possibili correlazioni tra personale e numero di chiamate, ordini e problemi. L'istruzione DMX recupera dati dal nodo delle statistiche marginali del modello di rete neurale. La query include la parola chiave FLATTENED, in quanto le statistiche di interesse degli attributi di input vengono archiviate in una tabella nidificata, NODE_DISTRIBUTION. Se tuttavia il provider della query supporta set di righe gerarchici, non è necessario utilizzare la parola chiave FLATTENED.  
  
```  
SELECT FLATTENED MODEL_CATALOG, MODEL_NAME,   
(    SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
     [SUPPORT], [PROBABILITY], VALUETYPE   
     FROM NODE_DISTRIBUTION  
) AS t  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 24  
```  
  
> [!NOTE]  
>  I nomi delle colonne `[SUPPORT]` e `[PROBABILITY]` della tabella nidificata devono essere racchiusi tra parentesi per distinguerli dalle parole chiave riservate con lo stesso nome.  
  
 Risultati dell'esempio:  
  
|MODEL_CATALOG|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|--------------------|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Average Time Per Issue|Missing|0|0|1|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Average Time Per Issue|< 64,7094100096|11|0,407407407|5|  
  
 Per una definizione del significato delle colonne nel set di righe dello schema, nel contesto di un modello di rete neurale, vedere [Contenuto dei modelli di data mining per i modelli di rete neurale &#40;Analysis Services - Data mining&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Query2"></a>Esempio di query 2: recupero di metadati del modello dal set di righe dello schema  
 È possibile trovare le stesse informazioni restituite in una query sul contenuto DMX eseguendo una query sul set di righe dello schema di data mining. Tuttavia, il set di righe dello schema contiene alcune colonne aggiuntive, Nella query di esempio seguente vengono restituite la data di creazione, di modifica e dell'ultima elaborazione del modello. La query restituisce anche le colonne stimabili che non sono facilmente reperibili dal contenuto del modello e i parametri utilizzati per compilare il modello. Queste informazioni possono risultare utili per documentare il modello.  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center Default NN'  
```  
  
 Risultati dell'esempio:  
  
|||  
|-|-|  
|MODEL_NAME|Call Center Default NN|  
|DATE_CREATED|1/10/2008 5:07:38 PM|  
|LAST_PROCESSED|1/10/2008 5:24:02 PM|  
|PREDICTION_ENTITY|Average Time Per Issue,<br /><br /> Grade Of Service,<br /><br /> Number Of Orders|  
|MINING_PARAMETERS|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=0<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100, SAMPLE_SIZE=10000, HIDDEN_NODE_RATIO=4|  
  
###  <a name="bkmk_Query3"></a>Esempio di query 3: recupero degli attributi di input per il modello  
 È possibile recuperare le coppie valore/attributo di input utilizzate per creare il modello eseguendo una query sui nodi figlio (NODE_TYPE = 20) del livello di input (NODE_TYPE = 18). Nella query seguente viene restituito un elenco di attributi di input dalle descrizioni di nodo.  
  
```  
SELECT NODE_DESCRIPTION  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 Risultati dell'esempio:  
  
|NODE_DESCRIPTION|  
|-----------------------|  
|Average Time Per Issue=64.7094100096 - 77.4002099712|  
|Day Of Week=Fri.|  
|Level 1 Operators|  
  
 In questo contesto vengono mostrate solo alcune righe rappresentative dei risultati. È tuttavia possibile notare che NODE_DESCRIPTION fornisce informazioni leggermente diverse a seconda del tipo di dati dell'attributo di input.  
  
-   Se l'attributo è un valore discreto o discretizzato, vengono restituiti l'attributo e il rispettivo valore o intervallo discretizzato.  
  
-   Se l'attributo è un tipo di dati numerici continuo, NODE_DESCRIPTION contiene solo il nome dell'attributo. È tuttavia possibile recuperare la tabella NODE_DISTRIBUTION nidificata per ottenere la media o restituire NODE_RULE per ottenere i valori minimo e massimo dell'intervallo numerico.  
  
 Nella query seguente viene illustrato come eseguire una query nella tabella NODE_DISTRIBUTION nidificata per restituire gli attributi in una colonna e i rispettivi valori in un'altra colonna. Per gli attributi continui, il valore dell'attributo à rappresentato dalla relativa media.  
  
```  
SELECT FLATTENED   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE  
FROM NODE_DISTRIBUTION) as t  
FROM [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 21  
```  
  
 Risultati dell'esempio:  
  
|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|-----------------------|------------------------|  
|Average Time Per Issue|64,7094100096 - 77,4002099712|  
|Day Of Week|Fri.|  
|Level 1 Operators|3,2962962962963|  
  
 I valori minimo e massimo dell'intervallo vengono archiviati nella colonna NODE_RULE e sono rappresentati come un frammento XML, come mostrato nell'esempio seguente:  
  
```  
<NormContinuous field="Level 1 Operators">    
  <LinearNorm orig="2.83967303681711" norm="-1" />    
  <LinearNorm orig="3.75291955577548" norm="1" />    
</NormContinuous>    
```  
  
###  <a name="bkmk_Query4"></a>Esempio di query 4: recupero di pesi dal livello nascosto  
 Il contenuto di un modello di una rete neurale è strutturato in modo da agevolare il recupero dei dettagli relativi a un qualsiasi nodo della rete. Gli ID dei nodi forniscono inoltre informazioni che consentono di identificare le relazioni tra i tipi di nodo.  
  
 Nella query seguente viene indicato come recuperare i coefficienti archiviati in un particolare nodo del livello nascosto. Il livello nascosto è costituito da un nodo di libreria (NODE_TYPE = 19), che contiene solo metadati, e da più nodi figlio (NODE_TYPE = 22), che contengono i coefficienti per le varie combinazioni di attributi e valori. Tramite questa query vengono restituiti solo i nodi di coefficiente.  
  
```  
SELECT FLATTENED TOP 1 NODE_UNIQUE_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM  [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 22  
AND [PARENT_UNIQUE_NAME] = '40000000200000000' FROM [Call Center Default NN].CONTENT  
```  
  
 Risultati dell'esempio:  
  
|NODE_UNIQUE_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|------------------------|-----------------------|------------------------|-----------------|  
|70000000200000000|6000000000000000a|-0,178616518|7|  
|70000000200000000|6000000000000000b|-0,267561918|7|  
|70000000200000000|6000000000000000c|0,11069497|7|  
|70000000200000000|6000000000000000d|0,123757712|7|  
|70000000200000000|6000000000000000e|0.294565343|7|  
|70000000200000000|6000000000000000f|0.22245318|7|  
|70000000200000000||0,188805045|7|  
  
 I risultati parziali riportati in questo ambito indicano il modo in cui il contenuto del modello di rete neurale correla il nodo nascosto ai nodi di input.  
  
-   I nomi univoci dei nodi nel livello nascosto iniziano sempre con 70000000.  
  
-   I nomi univoci dei nodi nel livello di input iniziano sempre con 60000000.  
  
 Questi risultati suggeriscono pertanto che al nodo con ID 70000000200000000 vengono passati sei coefficienti diversi (VALUETYPE = 7), con i valori inclusi nella colonna ATTRIBUTE_VALUE. È possibile determinare esattamente a quale attributo di input si riferisce il coefficiente utilizzando l'ID del nodo presente nella colonna ATTRIBUTE_NAME. L'ID del nodo 6000000000000000a si riferisce, ad esempio, al valore e all'attributo di input `Day of Week = 'Tue.'` . È possibile usare l'ID del nodo per creare una query o passare al nodo usando [Microsoft Generic Content Tree Viewer](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
 Analogamente, se si esegue una query sulla tabella NODE_DISTRIBUTION dei nodi nel livello di output (NODE_TYPE = 23), è possibile vedere i coefficienti per ogni valore di output. Nel livello di output tuttavia i puntatori si riferiscono nuovamente ai nodi del livello nascosto. Per altre informazioni, vedere [Contenuto dei modelli di data mining per i modelli di rete neurale &#40;Analysis Services - Data mining&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
## <a name="using-a-neural-network-model-to-make-predictions"></a>Utilizzo di un modello di rete neurale per eseguire stime  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network supporta sia la classificazione sia la regressione. È possibile utilizzare funzioni di stima con questi modelli per fornire nuovi dati e creare stime batch o singleton.  
  
###  <a name="bkmk_Query5"></a>Esempio di query 5: creazione di una stima singleton  
 Il modo più semplice per compilare una query di stima su un modello di rete neurale consiste nell'utilizzare il generatore delle query di stima, disponibile nella scheda **Stima modello di data mining** di Progettazione modelli di data mining sia in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , sia in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. È possibile esplorare il modello nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network per filtrare gli attributi di interesse e visualizzare le tendenze, quindi passare alla scheda **Stima modello di data mining** per creare una query e stimare i nuovi valori per tali tendenze.  
  
 È ad esempio possibile esplorare il modello Call Center per visualizzare le correlazioni tra i volumi degli ordini e altri attributi. A tale scopo, aprire il modello nel Visualizzatore e in **input**selezionare ** \<tutti>**.  Per **Output**selezionare quindi **Number of Orders**. In **Valore 1**selezionare l'intervallo che rappresenta il maggior numero di ordini e in **Valore 2**selezionare l'intervallo che rappresenta il minor numero di ordini. È possibile visualizzare rapidamente tutti gli attributi correlati dal modello con il volume degli ordini.  
  
 Esplorando i risultati nel visualizzatore, è possibile notare che in alcuni giorni della settimana i volumi degli ordini sono bassi e che sembra esserci una correlazione tra un aumento delle vendite e un aumento nel numero di operatori. È quindi possibile utilizzare una query di stima sul modello per testare un'ipotesi di simulazione e verificare se un aumento del numero degli operatori del livello 2 in un giorno in cui i volumi di ordini sono bassi comporta un aumento anche degli ordini. A questo scopo, creare una query simile alla seguente:  
  
```  
SELECT Predict([Call Center Default NN].[Number of Orders]) AS [Predicted Orders],  
PredictProbability([Call Center Default NN].[Number of Orders]) AS [Probability]  
FROM [Call Center Default NN]  
NATURAL PREDICTION JOIN   
(SELECT 'Tue.' AS [Day of Week],  
13 AS [Level 2 Operators]) AS t  
```  
  
 Risultati dell'esempio:  
  
|Predicted Orders|Probabilità|  
|----------------------|-----------------|  
|364|0,9532...|  
  
 Il volume delle vendite stimato è più elevato dell'intervallo corrente di vendite per martedì (Tuesday) e la probabilità della stima è molto elevata. Potrebbe tuttavia essere necessario creare più stime tramite un'elaborazione batch per testare una varietà di ipotesi relative al modello.  
  
> [!NOTE]  
>  I componenti aggiuntivi Data mining per Excel 2007 forniscono procedure guidate di regressione logistica che semplificano la risoluzione di problemi complessi, ad esempio il numero di operatori di livello 2 necessari per migliorare il livello del servizio e raggiungere un livello desiderato per un turno specifico. I componenti aggiuntivi per il data mining sono disponibili gratuitamente per il download e includono procedure guidate basate su algoritmi di rete neurale e o regressione logistica. Per altre informazioni, vedere il sito Web relativo ai [componenti aggiuntivi Data mining per Office 2007](https://go.microsoft.com/fwlink/?LinkID=117790) .  
  
## <a name="list-of-prediction-functions"></a>Elenco delle funzioni di stima  
 Tutti gli algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] supportano un set comune di funzioni. Non sono presenti funzioni di stima specifiche dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network, tuttavia l'algoritmo supporta le funzioni elencate nella tabella seguente.  
  
|||  
|-|-|  
|Funzione di stima|Uso|  
|[&#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|Viene determinato se un nodo è figlio di un altro nodo nel grafico della rete neurale.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|Viene restituita la probabilità ponderata.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|Viene restituita una tabella di valori correlati ai valori stimati correnti.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Viene restituita la varianza per il valore stimato.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|Viene restituita la probabilità per il valore stimato.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|Viene restituita la deviazione standard per il valore stimato.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Per i modelli di regressione logistica e di rete neurale, viene restituito un singolo valore che rappresenta la dimensione del set di training per l'intero modello.|  
  
 Per la sintassi di funzioni specifiche, vedere [Guida di riferimento alle funzioni DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Neural Network](microsoft-neural-network-algorithm.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Neural Network](microsoft-neural-network-algorithm-technical-reference.md)   
 [Contenuto del modello di data mining per i modelli di rete neurale &#40;Analysis Services-Data mining&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Lezione 5: creazione di modelli di rete neurale e di regressione logistica &#40;esercitazione intermedia sul data mining&#41;](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
  
