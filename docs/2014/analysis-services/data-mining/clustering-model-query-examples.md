---
title: Esempi di query sul modello di clustering | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [Data Mining]
- content queries [DMX]
- clustering algorithms [Analysis Services]
ms.assetid: bf2ba332-9bc6-411a-a3af-b919c52432c8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4996ba378319e442df07a4ff09af3404034474d9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66085714"
---
# <a name="clustering-model-query-examples"></a>Esempi di query sul modello di clustering
  Quando si crea una query su un modello di data mining, è possibile recuperare i metadati sul modello oppure creare una query contenuto che fornisca dettagli sui modelli individuati nell'analisi. In alternativa, è possibile creare una query di stima che utilizza i modelli nel modello per eseguire stime per i nuovi dati. Ogni tipo di query fornirà informazioni diverse. Ad esempio, tramite una query contenuto potrebbero essere forniti dettagli aggiuntivi sui cluster trovati, mentre tramite una query di stima potrebbe venir indicato a quale cluster è più probabile che appartenga un nuovo punto dati.  
  
 Questa sezione illustra come creare query per i modelli basati sull'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering.  
  
 **Query sul contenuto**  
  
 [Recupero di metadati del modello tramite DMX](#bkmk_Query1)  
  
 [Recupero di metadati del modello dal set di righe dello schema](#bkmk_Query2)  
  
 [Restituzione di un cluster o di un elenco di cluster](#bkmk_Query3)  
  
 [Restituzione di attributi per un cluster](#bkmk_Query4)  
  
 [Restituzione del profilo di un cluster tramite stored procedure di sistema](#bkmk_Query5)  
  
 [Individuazione dei fattori discriminanti per un cluster](#bkmk_Query6)  
  
 [Restituzione di case appartenenti a un cluster](#bkmk_Query7)  
  
 **Query di stima**  
  
 [Stima dei risultati da un modello di clustering](#bkmk_Query8)  
  
 [Determinazione dell'appartenenza al cluster](#bkmk_Query9)  
  
 [Restituzione di tutti i cluster possibili con probabilità e distanza](#bkmk_Query10)  
  
##  <a name="finding-information-about-the-model"></a><a name="bkmk_top2"></a> Ricerca di informazioni sul modello  
 In tutti i modelli di data mining viene esposto il contenuto appreso dall'algoritmo secondo uno schema standardizzato, definito set di righe dello schema del modello di data mining. È possibile creare query sul set di righe dello schema del modello di data mining tramite istruzioni DMX (Data Mining Extension). In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]è anche possibile eseguire una query direttamente sui set di righe dello schema come tabelle di sistema.  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="sample-query-1-getting-model-metadata-by-using-dmx"></a><a name="bkmk_Query1"></a>Esempio di query 1: recupero di metadati del modello tramite DMX  
 Con la query seguente vengono restituiti i metadati di base sul modello di clustering `TM_Clustering`creato nell'Esercitazione di base sul data mining. I metadati disponibili nel nodo padre di un modello di clustering includono il nome del modello, il database in cui è archiviato e il numero di nodi figlio del modello. Questa query utilizza una query contenuto DMX per recuperare i metadati dal nodo padre del modello:  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  È necessario includere il nome della colonna CHILDREN_CARDINALITY tra parentesi quadre per distinguerlo dalla parola chiave riservata MDX con lo stesso nome.  
  
 Risultati dell'esempio:  
  
|||  
|-|-|  
|MODEL_CATALOG|TM_Clustering|  
|MODEL_NAME|Adventure Works DW|  
|NODE_CAPTION|Modello di cluster|  
|NODE_SUPPORT|12939|  
|CHILDREN_CARDINALITY|10|  
|NODE_DESCRIPTION|Tutti|  
  
 Per una definizione del significato di queste colonne in un modello di clustering, vedere [Contenuto dei modelli di data mining per i modelli di clustering &#40;Analysis Services - Data mining&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md).  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="sample-query-2-retrieving-model-metadata-from-the-schema-rowset"></a><a name="bkmk_Query2"></a> Esempio di query 2: Recupero di metadati del modello dal set di righe dello schema  
 Se si esegue una query sul set di righe dello schema di data mining, è possibile trovare le stesse informazioni restituite in una query contenuto DMX. Tuttavia, il set di righe dello schema contiene alcune colonne aggiuntive, tra cui i parametri utilizzati durante la creazione del modello, la data e l'ora dell'ultima elaborazione del modello e il proprietario del modello.  
  
 Nell'esempio seguente vengono restituite le date di creazione, modifica e ultima elaborazione del modello. Vengono inoltre restituiti i parametri di clustering utilizzati per la compilazione del modello e la dimensione del set di training. Queste informazioni possono essere utili per documentare il modello o per determinare quali opzioni di clustering sono state utilizzate per creare un modello esistente.  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Clustering'  
```  
  
 Risultati dell'esempio:  
  
|||  
|-|-|  
|MODEL_NAME|TM_Clustering|  
|DATE_CREATED|10/12/2007 7:42:51 PM|  
|LAST_PROCESSED|10/12/2007 8:09:54 PM|  
|PREDICTION_ENTITY|Bike Buyer|  
|MINING_PARAMETERS|CLUSTER_COUNT=10,<br /><br /> CLUSTER_SEED=0,<br /><br /> CLUSTERING_METHOD=1,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100,<br /><br /> MINIMUM_SUPPORT=1,<br /><br /> MODELLING_CARDINALITY=10,<br /><br /> SAMPLE_SIZE=50000,<br /><br /> STOPPING_TOLERANCE=10|  
  
 [Torna all'inizio](#bkmk_top2)  
  
## <a name="finding-information-about-clusters"></a>Ricerca di informazioni sui cluster  
 Tramite le query contenuto più utili sui modelli di clustering generalmente viene restituito lo stesso tipo di informazioni che è possibile esplorare usando il **Visualizzatore cluster**. ovvero i profili e le caratteristiche del cluster e l'analisi discriminante tra cluster. In questa sezione vengono forniti esempi di query che recuperano queste informazioni.  
  
###  <a name="sample-query-3-returning-a-cluster-or-list-of-clusters"></a><a name="bkmk_Query3"></a> Esempio di query 3: Restituzione di un cluster o di un elenco di cluster  
 Poiché tutti i cluster includono un nodo di tipo 5, è possibile recuperare facilmente un elenco dei cluster eseguendo una query sul contenuto del modello per individuare solo i nodi di tale tipo. È inoltre possibile filtrare i nodi restituiti per probabilità o per supporto, come illustrato in questo esempio.  
  
```  
SELECT NODE_NAME, NODE_CAPTION ,NODE_SUPPORT, NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 5 AND NODE_SUPPORT > 1000  
```  
  
 Risultati dell'esempio:  
  
|||  
|-|-|  
|NODE_NAME|002|  
|NODE_CAPTION|Cluster 2|  
|NODE_SUPPORT|1649|  
|NODE_DESCRIPTION|English Education=Graduate Degree , 32 <=Age <=48 , Number Cars Owned=0 , 35964.0771121808 <=Yearly Income <=97407.7163393957 , English Occupation=Professional , Commute Distance=2-5 Miles , Region=North America , Bike Buyer=1 , Number Children At Home=0 , Number Cars Owned=1 , Commute Distance=0-1 Miles , English Education=Bachelors , Total Children=1 , Number Children At Home=2 , English Occupation=Skilled Manual , Marital Status=S , Total Children=0 , House Owner Flag=0 , Gender=F , Total Children=2 , Region=Pacific|  
  
 Gli attributi che definiscono il cluster sono disponibili in due colonne del set di righe dello schema di data mining.  
  
-   La colonna NODE_DESCRIPTION contiene un elenco delimitato da virgole di attributi. Si noti che l'elenco di attributi potrebbe essere abbreviato ai fini della visualizzazione.  
  
-   La tabella nidificata nella colonna NODE_DISTRIBUTION contiene l'elenco completo di attributi per il cluster. Se il client non supporta set di righe gerarchici, è possibile restituire la tabella nidificata aggiungendo la parola chiave FLATTENED prima dell'elenco di colonne SELECT. Per altre informazioni sull'uso della parola chiave FLATTENED, vedere [SELECT FROM &#60;model&#62;.CONTENT &#40;DMX&#41;](/sql/dmx/select-from-model-dimension-content-dmx).  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="sample-query-4-returning-attributes-for-a-cluster"></a><a name="bkmk_Query4"></a> Esempio di query 4: Restituzione di attributi per un cluster  
 Nel **Visualizzatore cluster** viene visualizzato un profilo con l'elenco degli attributi e dei valori per ogni cluster. Viene inoltre visualizzato un istogramma che indica la distribuzione dei valori per l'intero popolamento dei case nel modello. Se si esplora il modello nel visualizzatore, è possibile copiare facilmente l'istogramma dalla Legenda data mining e quindi incollarlo in Excel o in un documento di Word. È inoltre possibile utilizzare il riquadro Caratteristiche cluster del visualizzatore per confrontare graficamente gli attributi di cluster diversi.  
  
 Se tuttavia è necessario ottenere valori per più di un cluster alla volta, risulta più semplice eseguire una query sul modello. Ad esempio, quando si esplora il modello, si potrebbe notare che i primi due cluster differiscono tra loro in relazione a un attributo, ovvero `Number Cars Owned`. Pertanto, si desidera estrarre i valori per ogni cluster.  
  
```  
SELECT TOP 2 NODE_NAME,   
(SELECT ATTRIBUTE_VALUE, [PROBABILITY] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Number Cars Owned')  
AS t  
FROM [TM_Clustering].CONTENT  
WHERE NODE_TYPE = 5  
```  
  
 La prima riga del codice specifica che si desiderano solo i primi due cluster.  
  
> [!NOTE]  
>  Per impostazione predefinita, i cluster sono ordinati per supporto. Pertanto, la colonna NODE_SUPPORT può essere omessa.  
  
 La seconda riga del codice aggiunge un'istruzione sub-SELECT che restituisce solo determinate colonne della colonna della tabella nidificata. Limita inoltre le righe della tabella nidificata a quelle correlate all'attributo di destinazione, `Number Cars Owned`. Per semplificare la visualizzazione, la tabella è associata a un alias.  
  
> [!NOTE]  
>  La colonna della tabella nidificata, `PROBABILITY`, deve essere racchiusa tra parentesi quadre perché corrisponde anche al nome di una parola chiave riservata MDX.  
>   
>  Risultati dell'esempio:  
  
|NODE_NAME|T.ATTRIBUTE_VALUE|T.PROBABILITY|  
|----------------|------------------------|-------------------|  
|001|2|0.829207754|  
|001|1|0.109354156|  
|001|3|0.034481552|  
|001|4|0.013503302|  
|001|0|0.013453236|  
|001|Missing|0|  
|002|0|0.576980023|  
|002|1|0.406623939|  
|002|2|0.016380082|  
|002|3|1,60E-05|  
|002|4|0|  
|002|Missing|0|  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="sample-query-5-return-a-cluster-profile-using-system-stored-procedures"></a><a name="bkmk_Query5"></a> Esempio di query 5: Restituzione del profilo di un cluster tramite stored procedure di sistema  
 Come alternativa rapida, anziché scrivere query usando DMX, è anche possibile chiamare le stored procedure di sistema usate da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per gestire i cluster. Nell'esempio seguente viene illustrato come utilizzare le stored procedure interne per restituire il profilo per un cluster con ID 002.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('TM_Clustering", '002',0.0005  
```  
  
 Analogamente, è possibile utilizzare una stored procedure di sistema per restituire le caratteristiche di un cluster specifico, come illustrato nell'esempio seguente:  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('TM_Clustering", '009',0.0005  
```  
  
 Risultati dell'esempio:  
  
|Attributes|Valori|Frequenza|Supporto|  
|----------------|------------|---------------|-------------|  
|Number Children at Home|0|0.999999829076798|899|  
|Region|America del Nord|0.999852875241508|899|  
|Total Children|0|0.993860958572323|893|  
  
> [!NOTE]  
>  Le stored procedure di sistema per il data mining sono per uso interno e [!INCLUDE[msCoName](../../includes/msconame-md.md)] si riserva il diritto di modificarle, se necessario. Per l'utilizzo in un ambiente di produzione, si consiglia di creare query utilizzando DMX, AMO o XMLA.  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="sample-query-6-find-discriminating-factors-for-a-cluster"></a><a name="bkmk_Query6"></a> Esempio di query 6: Individuazione dei fattori discriminanti per un cluster  
 La scheda **Analisi discriminante tra cluster** del **Visualizzatore cluster** consente di confrontare facilmente un cluster con un altro cluster o con tutti i case rimanenti (il complemento del cluster).  
  
 La creazione di query per restituire queste informazioni può tuttavia essere complessa e potrebbe essere necessario eseguire un'elaborazione aggiuntiva sul client per archiviare i risultati temporanei e confrontare i risultati di due o più query. Come alternativa rapida, è possibile utilizzare le stored procedure di sistema.  
  
 Con la query seguente viene restituita una singola tabella che indica i principali fattori discriminanti tra i due cluster con ID nodo 009 e 007. Gli attributi con valori positivi prediligono il cluster 009, mentre quelli con valori negativi il cluster 007.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','007',0.0005,true)  
```  
  
 Risultati dell'esempio:  
  
|Attributes|Valori|Punteggio|  
|----------------|------------|-----------|  
|Region|America del Nord|100|  
|English Occupation|Skilled Manual|94.9003803898654|  
|Region|Europa|-72.5041051379789|  
|English Occupation|Manuale|-69.6503163202722|  
  
 Queste informazioni sono identiche a quelle presentate nel grafico del visualizzatore **Analisi discriminante tra cluster** se si seleziona Cluster 9 dal primo elenco a discesa e Cluster 7 dal secondo elenco a discesa. Per confrontare il cluster 9 con il relativo complemento, utilizzare la stringa vuota nel secondo parametro, come illustrato nell'esempio seguente:  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','',0.0005,true)  
```  
  
> [!NOTE]  
>  Le stored procedure di sistema per il data mining sono per uso interno e [!INCLUDE[msCoName](../../includes/msconame-md.md)] si riserva il diritto di modificarle, se necessario. Per l'utilizzo in un ambiente di produzione, si consiglia di creare query utilizzando DMX, AMO o XMLA.  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="sample-query-7-returning-cases-that-belong-to-a-cluster"></a><a name="bkmk_Query7"></a> Esempio d query 7: Restituzione di case appartenenti a un cluster  
 Se per il modello di data mining è stato abilitato il drill-through, è possibile creare query tramite cui vengono restituite informazioni dettagliate sui case utilizzati nel modello. Inoltre, se il drill-through è stato abilitato per la struttura di data mining, è possibile includere le colonne della struttura sottostante usando la funzione [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx).  
  
 Nell'esempio seguente vengono restituite due colonne utilizzate nel modello, Age e Region, e un'altra colonna, First Name, che non è stata utilizzata nel modello. La query restituisce solo i case classificati in Cluster 1.  
  
```  
SELECT [Age], [Region], StructureColumn('First Name')  
FROM [TM_Clustering].CASES  
WHERE IsInNode('001')  
```  
  
 Per restituire i case che appartengono a un cluster, è necessario conoscere l'ID del cluster. È possibile ottenere questo valore esplorando il modello in uno dei visualizzatori. In alternativa, è possibile rinominare un cluster per farvi riferimento in modo più semplice e in seguito utilizzare il nome al posto di un numero ID. Tenere presente, tuttavia, che i nomi assegnati a un cluster andranno persi se il modello viene rielaborato.  
  
 [Torna all'inizio](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>Esecuzione di stime tramite il modello  
 Anche se il clustering viene solitamente usato per descrivere e comprendere i dati, l'implementazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] consente anche di eseguire una stima sull'appartenenza al cluster e di restituire le probabilità associate alla stima. In questa sezione vengono forniti alcuni esempi su come creare query di stima sui modelli di clustering. È possibile eseguire stime per più case, specificando un'origine dati tabulare, oppure fornire nuovi valori contemporaneamente creando una query singleton. Per maggiore chiarezza, negli esempi di questa sezione vengono usate tutte query singleton.  
  
 Per ulteriori informazioni sulla creazione di query di stima tramite DMX, vedere [interfacce di query di data mining](data-mining-query-tools.md).  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="sample-query-8-predicting-outcomes-from-a-clustering-model"></a><a name="bkmk_Query8"></a> Esempio di query 8: Stima dei risultati da un modello di clustering  
 Se il modello di clustering creato contiene un attributo stimabile, è possibile utilizzarlo per eseguire stime sui risultati. Tuttavia, il modello gestisce l'attributo stimabile in modo diverso a seconda che la colonna stimabile venga impostata su `Predict` o su `PredictOnly`. Se si imposta l'utilizzo della colonna su `Predict`, i valori relativi a tale attributo vengono aggiunti al modello di clustering e vengono visualizzati come attributi nel modello finito. Se invece si imposta l'utilizzo della colonna su `PredictOnly`, i valori non vengono utilizzati per creare cluster. Al contrario, al termine della modalità, l'algoritmo di clustering crea nuovi valori per l'attributo `PredictOnly` in base ai cluster a cui appartiene ogni case.  
  
 Con la query seguente viene fornito un nuovo case singolo al modello, in cui le uniche informazioni sul case sono l'età e il sesso. L'istruzione SELECT specifica la coppia attributo/valore stimabile di interesse, mentre la funzione [PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx) indica la probabilità che un case con tali attributi genererà il risultato di destinazione.  
  
```  
SELECT  
  [TM_Clustering].[Bike Buyer], PredictProbability([Bike Buyer],1)  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 Esempio dei risultati quando l'utilizzo è impostato su `Predict`:  
  
|Bike Buyer|Expression|  
|----------------|----------------|  
|1|0.592924735740338|  
  
 Esempio dei risultati quando l'utilizzo è impostato su `PredictOnly` e il modello viene rielaborato:  
  
|Bike Buyer|Expression|  
|----------------|----------------|  
|1|0.55843544003102|  
  
 In questo esempio la differenza nel modello non è significativa. Tuttavia, talvolta può essere importante individuare le differenze tra la distribuzione effettiva dei valori e le stime del modello. La scheda [PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx) è utile in questo scenario, perché indica il livello di probabilità di un case, dato il modello.  
  
 Il numero restituito dalla funzione PredictCaseLikelihood è una probabilità e pertanto è sempre compreso tra 0 e 1, con il valore 0,5 che rappresenta il risultato casuale. Pertanto, un punteggio minore di 0,5 significa che il case stimato è improbabile, dato il modello, mentre un punteggio maggiore di 0,5 indica che è molto probabile ottenere un fit tra il case stimato e il modello.  
  
 Ad esempio, con la query seguente vengono restituiti due valori che caratterizzano il livello di probabilità di un nuovo case di esempio. Il valore non normalizzato rappresenta la probabilità dato il modello corrente. Quando si utilizza la parola chiave NORMALIZED, il punteggio di probabilità restituito dalla funzione viene adattato dividendo la "probabilità con il modello" per la "probabilità senza il modello".  
  
```  
SELECT  
PredictCaseLikelihood(NORMALIZED) AS [NormalizedValue], PredictCaseLikelihood(NONNORMALIZED) AS [NonNormalizedValue]  
FROM  
  [TM_Clustering_PredictOnly]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 Risultati dell'esempio:  
  
|NormalizedValue|NonNormalizedValue|  
|---------------------|------------------------|  
|5.56438372679893E-11|8,65459953145182E-68|  
  
 Si noti che i numeri di questi risultati sono espressi in formato di notazione scientifica.  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="sample-query-9-determining-cluster-membership"></a><a name="bkmk_Query9"></a> Esempio di query 9: Determinazione dell'appartenenza al cluster  
 In questo esempio vengono usate la funzione [Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx) per restituire il cluster a cui è più probabile che appartenga il nuovo case e la funzione [ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx) per restituire la probabilità di appartenenza a tale cluster.  
  
```  
SELECT Cluster(), ClusterProbability()  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status]) AS t  
```  
  
 Risultati dell'esempio:  
  
|$CLUSTER|Expression|  
|--------------|----------------|  
|Cluster 2|0.397918596951617|  
  
 **Nota** Per impostazione predefinita, `ClusterProbability` la funzione restituisce la probabilità del cluster più probabile. Tuttavia, è possibile specificare un cluster diverso usando la sintassi `ClusterProbability('cluster name')`. In questo caso, tenere presente che i risultati di ogni funzione di stima sono indipendenti dagli altri risultati. Pertanto, il punteggio di probabilità nella seconda colonna può fare riferimento a un cluster diverso rispetto a quello specificato nella prima colonna.  
  
 [Torna all'inizio](#bkmk_top2)  
  
###  <a name="sample-query-10-returning-all-possible-clusters-with-probability-and-distance"></a><a name="bkmk_Query10"></a> Esempio di query 10: Restituzione di tutti i cluster possibili con probabilità e distanza  
 Nell'esempio precedente il punteggio di probabilità non è molto alto. Per determinare se è disponibile un cluster migliore, è possibile usare la funzione [PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx) insieme alla funzione [Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx) per restituire una tabella annidata che includa tutti i cluster possibili, oltre alla probabilità che il nuovo case appartenga a ogni cluster. La parola chiave FLATTENED viene utilizzata per modificare il set di righe gerarchico in una tabella flat per semplificare la visualizzazione.  
  
```  
SELECT FLATTENED PredictHistogram(Cluster())  
From  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status])  
```  
  
|Expression.$CLUSTER|Expression.$DISTANCE|Expression.$PROBABILITY|  
|-------------------------|--------------------------|-----------------------------|  
|Cluster 2|0.602081403048383|0.397918596951617|  
|Cluster 10|0.719691686785675|0.280308313214325|  
|Cluster 4|0.867772590378791|0.132227409621209|  
|Cluster 5|0.931039872200985|0.0689601277990149|  
|Cluster 3|0.942359230072167|0.0576407699278328|  
|Cluster 6|0.958973668972756|0.0410263310272437|  
|Cluster 7|0.979081275926724|0.0209187240732763|  
|Cluster 1|0.999169044818624|0.000830955181376364|  
|Cluster 9|0.999831227795894|0.000168772204105754|  
|Cluster 8|1|0|  
  
 Per impostazione predefinita, i risultati sono classificati per probabilità. I risultati indicano che, anche se la probabilità per Cluster 2 è relativamente bassa, Cluster 2 rappresenta comunque il miglior fit per il nuovo punto dati.  
  
 **Nota** La colonna aggiuntiva, `$DISTANCE`, rappresenta la distanza tra il punto dati e il cluster. Per impostazione predefinita, l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering usa il clustering EM scalabile, che usa più cluster a ogni punto dati e classifica i cluster possibili.  Tuttavia, se si crea il modello di clustering utilizzando l'algoritmo K-medie, è possibile assegnare un unico cluster a ogni punto dati e questa query restituisce solo una riga. Per interpretare i risultati della funzione [PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx) . Per altre informazioni sulle differenze tra i clustering EM e K-medie, vedere [Riferimento tecnico per l'algoritmo Microsoft Clustering](microsoft-clustering-algorithm-technical-reference.md).  
  
 [Torna all'inizio](#bkmk_top2)  
  
## <a name="function-list"></a>Elenco di funzioni  
 Tutti gli algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] supportano un set comune di funzioni. Tuttavia, i modelli compilati usando l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering supportano le funzioni aggiuntive elencate nella tabella seguente.  
  
|||  
|-|-|  
|Funzione di stima|Uso|  
|[Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx)|Restituisce il cluster che con maggiore probabilità contiene il case di input.|  
|[ClusterDistance &#40;DMX&#41;](/sql/dmx/clusterdistance-dmx)|Viene restituita la distanza del case di input dal cluster specificato o la distanza del case di input dal cluster più probabile, se non viene specificato alcun cluster.<br /><br /> Restituisce la probabilità che il case di input appartenga al cluster specificato.|  
|[ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx)|Restituisce la probabilità che il case di input appartenga al cluster specificato.|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|Viene determinato se un nodo è figlio di un altro nodo nel modello.|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|Indica se il nodo specificato contiene o meno il case corrente.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|Viene restituita la probabilità ponderata.|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|Viene stimata l'appartenenza a un set di dati associativo.|  
|[PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx)|Viene restituita la probabilità che un case di input risulti adatto al modello esistente.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|Viene restituita una tabella di valori correlati ai valori stimati correnti.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Viene restituito l'oggetto Node_ID per ogni case.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|Viene restituita la probabilità per il valore stimato.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|Restituisce la deviazione standard stimata per la colonna specificata.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Viene restituito il valore di supporto per uno stato specificato.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Restituisce la varianza di una colonna specificata.|  
  
 Per la sintassi di funzioni specifiche, vedere [Guida di riferimento alle funzioni DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Vedi anche  
 [Query di data mining](data-mining-queries.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Clustering](microsoft-clustering-algorithm-technical-reference.md)   
 [Algoritmo Microsoft Clustering](microsoft-clustering-algorithm.md)  
  
  
