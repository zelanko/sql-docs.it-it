---
title: Sequence Clustering Model Query Examples | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- sequence clustering algorithms [Analysis Services]
- content queries [DMX]
- sequence [Analysis Services]
ms.assetid: 64bebcdc-70ab-43fb-8d40-57672a126602
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8f5776d2a7523f4d56bb48926a8f0bf0929e87f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732885"
---
# <a name="sequence-clustering-model-query-examples"></a>Sequence Clustering Model Query Examples
  Quando si crea una query su un modello di data mining, è possibile scegliere tra due tipi: una query sul contenuto, che fornisce dettagli sulle informazioni archiviate nel modello o una query di stima, che utilizza i criteri presenti nel modello per eseguire stime basate sui nuovi dati forniti. Per un modello Sequence Clustering, le query sul contenuto in genere forniscono dettagli aggiuntivi sui cluster trovati o sulle transizioni all'interno di tali cluster. Utilizzando una query è inoltre possibile recuperare metadati relativi al modello.  
  
 Le query di stima su un modello Sequence Clustering di solito generano indicazioni basate sulle sequenze e sulle transizioni, su attributi fuori sequenza inclusi nel modello o su una combinazione di attributi di sequenza e fuori sequenza.  
  
 In questa sezione viene illustrato come creare entrambi i tipi di query per i modelli basati sull'algoritmo Microsoft Sequence Clustering. Per informazioni generali sulla creazione di query, vedere [Query di data mining](data-mining-queries.md).  
  
 **Content Queries**  
  
 [Utilizzo di un set di righe dello schema di data mining per la restituzione di parametri del modello](#bkmk_Query1)  
  
 [Come ottenere un elenco di sequenze per uno stato](#bkmk_Query2)  
  
 [Utilizzo di stored procedure di sistema](#bkmk_Query3)  
  
 **Query di stima**  
  
 [Stimare lo stato o gli stati successivi](#bkmk_Query4)  
  
##  <a name="bkmk_ContentQueries"></a> Ricerca di informazioni sul modello Sequence Clustering  
 Per creare query significative sul contenuto di un modello di data mining, è necessario comprendere la struttura del contenuto del modello ed essere in grado di individuare il tipo di informazioni archiviate dai diversi tipi di nodo. Per altre informazioni, vedere [Contenuto dei modelli di data mining per i modelli Sequence Clustering &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-sequence-clustering-models.md).  
  
###  <a name="bkmk_Query1"></a> Esempio di Query 1: Utilizzo dei set di righe dello Schema di Data Mining per restituire i parametri di modello  
 L'esecuzione di una query sul set di righe dello schema di data mining consente di trovare vari tipi di informazioni sul modello, inclusi i metadati di base, la data e l'ora di creazione e dell'ultima elaborazione del modello, il nome della struttura di data mining su cui si basa il modello e la colonna utilizzata come attributo stimabile.  
  
 Nella query seguente vengono restituiti i parametri utilizzati per la compilazione e il training del modello, `[Sequence Clustering]`. È possibile creare questo modello nella Lezione 5 dell' [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md).  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Sequence Clustering'  
```  
  
 Risultati dell'esempio:  
  
|MINING_PARAMETERS|  
|------------------------|  
|CLUSTER_COUNT=15,MINIMUM_SUPPORT=10,MAXIMUM_STATES=100,MAXIMUM_SEQUENCE_STATES=64|  
  
 Notare che questo modello è stato compilato tramite il valore predefinito pari a 10 per CLUSTER_COUNT. Quando si specifica un numero di cluster diverso da zero per CLUSTER_COUNT, tale numero viene considerato dall'algoritmo come un'indicazione del numero approssimativo di cluster da trovare. Nel processo di analisi, tuttavia, l'algoritmo potrebbe trovare un numero maggiore o minore di cluster. In questo caso ha rilevato che 15 cluster si adattano ai dati di training. Pertanto, l'elenco di valori dei parametri per il modello completato riporta il conteggio dei cluster determinato dall'algoritmo, non il valore passato durante la creazione del modello.  
  
 Per osservare la differenza tra questo comportamento e la determinazione del miglior numero di cluster da parte dell'algoritmo, è possibile provare a creare un altro modello di clustering che utilizzi gli stessi dati, impostando CLUSTER_COUNT su 0. Quando si esegue questa operazione, l'algoritmo rileva 32 cluster. Pertanto, l'utilizzo del valore predefinito di 10 per CLUSTER_COUNT limita il numero di risultati.  
  
 Per impostazione predefinita, viene utilizzato il valore pari a 10 in quanto in genere la riduzione del numero di cluster consente di esplorare e comprendere più facilmente i raggruppamenti nei dati. Tuttavia, ogni modello e set di dati è diverso. È possibile provare a utilizzare altri numeri di cluster per vedere quale valore del parametro produce il modello più accurato.  
  
###  <a name="bkmk_Query2"></a> Esempio di Query 2: Come ottenere un elenco di sequenze per uno stato  
 Il contenuto del modello di data mining archivia le sequenze trovate nei dati di training come primo stato associato a un elenco di tutti i secondi stati correlati. Il primo stato viene utilizzato come etichetta della sequenza e i secondi stati correlati vengono definiti transizioni.  
  
 La query seguente, ad esempio, restituisce l'elenco completo dei primi stati del modello, prima che le sequenze vengono raggruppate in cluster.  È possibile ottenere questo elenco restituendo l'elenco di sequenze (NODE_TYPE = 13) che dispongono del nodo radice del modello come elemento padre (PARENT_UNIQUE_NAME = 0). La parola chiave FLATTENED rende più semplice la lettura dei risultati.  
  
> [!NOTE]  
>  I nomi delle colonne, PARENT_UNIQUE_NAME, Support e Probability, devono essere racchiusi tra parentesi quadre affinché possano essere distinti dalle parole chiave riservate con gli stessi nomi.  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME,  
(SELECT ATTRIBUTE_VALUE AS [Product 1],  
[Support] AS [Sequence Support],   
[Probability] AS [Sequence Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_TYPE = 13  
AND [PARENT_UNIQUE_NAME] = 0  
```  
  
 Risultati parziali:  
  
|NODE_UNIQUE_NAME|Product 1|Sequence Support|Sequence Probability|  
|------------------------|---------------|----------------------|--------------------------|  
|1081327|Missing|0|#######|  
|1081327|All-Purpose Bike Stand|17|0,00111|  
|1081327|Bike Wash|64|0,00418|  
|1081327|(righe 4-36 omesse)|||  
|1081327|Women's Mountain Shorts|506|0,03307|  
  
 L'elenco delle sequenze nel modello viene sempre organizzato in ordine alfabetico crescente. L'ordine delle sequenze è importante in quanto è possibile trovare le transizioni correlate analizzando il numero progressivo della sequenza. Il valore `Missing` equivale sempre alla transizione 0.  
  
 Nei risultati precedenti, ad esempio, il prodotto "Women's Mountain Shorts" è il numero progressivo 37 nel modello. Queste informazioni possono essere utilizzate per visualizzare tutti i prodotti acquistati dopo "Women's Mountain Shorts."  
  
 A questo scopo, è necessario innanzitutto fare riferimento al valore restituito per NODE_UNIQUE_NAME nella query precedente per ottenere l'ID del nodo contenente tutte le sequenze per il modello. Il valore viene quindi passato alla query come ID del nodo padre, per ottenere solo le transizioni incluse in questo nodo che contengono anche un elenco di tutte le sequenze per il modello. Se invece si desidera visualizzare l'elenco di transizioni per un cluster specifico, è possibile passare l'ID del nodo del cluster e vedere solo le sequenze associate a quel cluster.  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_DESCRIPTION = 'Transition row for sequence state 37'  
AND [PARENT_UNIQUE_NAME] = '1081327'  
```  
  
 Risultati dell'esempio:  
  
|NODE_UNIQUE_NAME|  
|------------------------|  
|1081365|  
  
 Il nodo rappresentato da questo ID contiene un elenco delle sequenze che seguono il prodotto "Women's Mountain Shorts", insieme ai valori di supporto e probabilità.  
  
```  
SELECT FLATTENED  
(SELECT ATTRIBUTE_VALUE AS Product2,  
[Support] AS [P2 Support],  
[Probability] AS [P2 Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_UNIQUE_NAME = '1081365'  
```  
  
 Risultati dell'esempio:  
  
|t.Product2|t.P2 Support|t.P2 Probability|  
|----------------|------------------|----------------------|  
|Missing|230,7419|0,456012|  
|Classic Vest|8,16129|0,016129|  
|Cycling Cap|60,83871|0,120235|  
|Half-Finger Gloves|30,41935|0,060117|  
|Long-Sleeve Logo Jersey|86,80645|0,171554|  
|Racing Socks|28,93548|0,057185|  
|Short-Sleeve Classic Jersey|60,09677|0,118768|  
  
 Notare che il supporto per le varie sequenze correlate a Women's Mountain Shorts è 506 nel modello. Anche i valori di supporto per le transizioni ammontano a 506. Appare tuttavia alquanto strano che i numeri non siano interi se ci si aspetta che il supporto rappresenti semplicemente un conteggio dei case che contengono ogni transizione. Poiché il metodo per la creazione di cluster calcola un'appartenenza parziale, la probabilità di qualsiasi transizione all'interno di un cluster deve essere ponderata rispetto alla probabilità di appartenere a quel particolare cluster.  
  
 Se ad esempio ci sono quattro cluster, una determinata sequenza potrebbe avere un'opportunità del 40% di appartenere al cluster 1, un'opportunità del 30% di appartenere al cluster 2, un'opportunità del 20% di appartenere al cluster 3 e un'opportunità del 10% di appartenere al cluster 4. Dopo che l'algoritmo ha determinato il cluster a cui la transizione appartiene con maggiore probabilità, pondera le probabilità all'interno del cluster rispetto alla probabilità precedente del cluster.  
  
###  <a name="bkmk_Query3"></a> Esempio di Query 3: Utilizzo del sistema di Stored procedure  
 Gli esempi di query appena descritti dimostrano che le informazioni archiviate nel modello sono complesse e che per ottenere quelle desiderate potrebbe essere necessario creare più query. Tuttavia, il visualizzatore Microsoft Sequence Clustering offre un set di potenti strumenti per l'esplorazione grafica delle informazioni contenute in un modello Sequence Clustering e consente anche di eseguire query e il drill-down nel modello.  
  
 Nella maggior parte dei casi le informazioni presentate nel visualizzatore di Microsoft Sequence Clustering vengono create tramite le stored procedure di sistema di Analysis Services per eseguire query sul modello. È possibile scrivere query DMX (Data Mining Extensions) sul contenuto del modello per recuperare le stesse informazioni, ma le stored procedure di sistema di Analysis Services forniscono un comodo collegamento per l'esplorazione o il test dei modelli.  
  
> [!NOTE]  
>  Le stored procedure di sistema vengono utilizzate per elaborazioni interne da parte del server e dei client forniti da Microsoft per l'interazione con il server di Analysis Services. Pertanto, Microsoft si riserva il diritto di modificarle in qualsiasi momento. Sebbene vengono descritte qui per comodità, il loro l'utilizzo non è supportato in un ambiente di produzione. Per assicurare la stabilità e la compatibilità in un ambiente di produzione, è necessario scrivere le query sempre tramite DMX.  
  
 In questa sezione sono illustrati alcuni esempi di utilizzo di stored procedure di sistema per la creazione di query in un modello Sequence Clustering:  
  
#### <a name="cluster-profiles-and-sample-cases"></a>Profili cluster e case di esempio  
 La scheda Profili cluster contiene un elenco dei cluster presenti nel modello, la dimensione di ciascuno di essi e un istogramma che indica gli stati inclusi nel cluster. Esistono due stored procedure di sistema che è possibile utilizzare nelle query per recuperare informazioni simili:  
  
-   `GetClusterProfile` restituisce le caratteristiche del cluster, con tutte le informazioni trovate nella tabella NODE_DISTRIBUTION per il cluster.  
  
-   `GetNodeGraph` restituisce nodi e bordi che è possibile utilizzare per costruire una rappresentazione grafico-matematica dei cluster, corrispondente a quella contenuta nella prima scheda della vista di Sequence Clustering. I nodi sono cluster e i bordi rappresentano fattori di ponderazione o il livello di attendibilità.  
  
 Nell'esempio seguente viene illustrato come utilizzare la stored procedure di sistema, `GetClusterProfiles`, per restituire tutti i cluster nel modello, con i rispettivi profili. Questa stored procedure esegue una serie di istruzioni DMX che restituiscono il set completo di profili nel modello. Tuttavia, per utilizzarla, è necessario conoscere l'indirizzo del modello.  
  
 `CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('Sequence Clustering', 2147483647, 0)`  
  
 Nell'esempio seguente viene illustrato come recuperare il profilo per un cluster specifico, Cluster 12, tramite la stored procedure di sistema `GetNodeGraph`e l'indicazione dell'ID del cluster che generalmente corrisponde al numero nel nome del cluster.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','12',0)  
```  
  
 Se si omette l'ID del cluster, come mostrato nella query seguente, `GetNodeGraph` restituisce un elenco ordinato e bidimensionale di tutti i profili cluster:  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','',0)  
```  
  
 La scheda **Profilo cluster** visualizza inoltre un istogramma di case di esempio del modello che rappresentano i case idealizzati per il modello. Essi non vengono archiviati nel modello con le stesse modalità dei dati di training e richiedono una sintassi speciale per il recupero.  
  
```  
SELECT * FROM [Sequence Clustering].SAMPLE_CASES WHERE IsInNode('12')  
```  
  
 Per altre informazioni, vedere [SELECT FROM &#60;model&#62;.SAMPLE_CASES &#40;DMX&#41;](/sql/dmx/select-from-model-dmx).  
  
#### <a name="cluster-characteristics-and-cluster-discrimination"></a>Caratteristiche cluster e analisi discriminante tra cluster.  
 La scheda **Caratteristiche cluster** riepiloga gli attributi principali di ogni cluster, classificati per probabilità. È possibile scoprire quanti case appartengono a un cluster e novità la distribuzione di case nel cluster: Ogni caratteristica dispone di un determinato supporto. Per vedere le caratteristiche di un determinato cluster, è necessario conoscerne l'ID.  
  
 Negli esempi seguenti viene utilizzata la stored procedure di sistema, `GetClusterCharacteristics`, per restituire tutte le caratteristiche di Cluster 12 che hanno un punteggio di probabilità superiore alla soglia specificata di 0.0005.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','12',0.0005)  
```  
  
 Per restituire le caratteristiche di tutti i cluster, è necessario lasciare l'ID del cluster vuoto.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','',0.0005)  
```  
  
 Nell'esempio seguente la stored procedure di sistema `GetClusterDiscrimination` viene chiamata per confrontare le caratteristiche di Cluster 1 e Cluster 12.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('Sequence Clustering','1','12',0.0005,true)  
```  
  
 Se si desidera scrivere query in DMX per confrontare due cluster, o mettere a confronto un cluster e il relativo complemento, è necessario recuperare prima un set di caratteristiche, quindi le caratteristiche per il cluster specifico di interesse e confrontare i due set. Questo scenario è più complicato e in genere richiede un'elaborazione del client.  
  
#### <a name="states-and-transitions"></a>Stati e transizioni  
 La scheda **Transizioni di stato** di Microsoft Sequence Clustering esegue query complicate sul back end per recuperare e confrontare le statistiche per diversi cluster. La riproduzione di questi risultati richiede una query più complessa e alcune elaborazioni del client.  
  
 È tuttavia possibile utilizzare le query DMX descritte nell'esempio 2 della sezione [Query sul contenuto](#bkmk_ContentQueries)per recuperare probabilità e stati per sequenze o singole transizioni.  
  
## <a name="using-the-model-to-make-predictions"></a>Utilizzo del modello per l'esecuzione di stime  
 Le query di stima su un modello Sequence Clustering possono utilizzare molte delle funzioni di stima utilizzate con gli altri modelli di clustering. È anche possibile usare la funzione di stima speciale [PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx)per generare indicazioni o eseguire stime degli stati successivi.  
  
###  <a name="bkmk_Query4"></a> Esempio di Query 4: Stimare lo stato successivo o gli Stati  
 È possibile usare la funzione [PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx) per stimare lo stato successivo più probabile, dato un determinato valore. È inoltre possibile stimare più stati successivi e restituire, ad esempio, un elenco dei primi tre prodotti che un cliente potrebbe acquistare per presentare un elenco di raccomandazioni.  
  
 La query di esempio seguente è una query di stima singleton che restituisce le prime cinque stime, insieme alla relativa probabilità. Poiché il modello include una tabella nidificata, è necessario utilizzare la tabella nidificata, `[v Assoc Seq Line Items]`, come riferimento della colonna durante l'esecuzione di stime. Inoltre, quando vengono forniti valori come input, è necessario unire la tabella del case e le colonne della tabella nidificata, come mostrato dalle istruzioni SELECT nidificate.  
  
```  
SELECT FLATTENED PredictSequence([v Assoc Seq Line Items], 7)  
FROM [Sequence Clustering]  
NATURAL PREDICTION JOIN  
(SELECT  (SELECT 1 as [Line Number],  
   'All-Purpose Bike Stand' as [Model]) AS [v Assoc Seq Line Items])   
AS t  
```  
  
 Risultati dell'esempio:  
  
|Expression.$Sequence|Expression.Line Number|Expression.Model|  
|--------------------------|----------------------------|----------------------|  
|1||Cycling Cap|  
|2||Cycling Cap|  
|3||Sport-100|  
|4||Long-Sleeve Logo Jersey|  
|5||Half-Finger Gloves|  
|6||All-Purpose Bike Stand|  
|7||All-Purpose Bike Stand|  
  
 I risultati includono tre colonne, anche se se ne potrebbe prevedere solo una, in quanto la query restituisce sempre una colonna per la tabella del case. Qui i risultati sono resi in formato bidimensionale. In caso contrario, la query restituirebbe una sola colonna contenente due colonne della tabella nidificata.  
  
 La colonna $sequence è una colonna restituita per impostazione predefinita dalla funzione `PredictSequence` per ordinare i risultati della stima. La colonna `[Line Number]`è necessaria per mettere in corrispondenza le chiavi della sequenza nel modello, ma le chiavi non vengono restituite.  
  
 È interessante notare che le sequenze con la stima più alta dopo All-Purpose Bike Stand sono Cycling Cap e Cycling Cap. Non si tratta di un errore. A seconda di come i dati vengono presentati al cliente, e dalla modalità di raggruppamento durante il training del modello, è molto frequente disporre di sequenze di questo tipo. Un cliente potrebbe acquistare ad esempio un cappellino da ciclista (rosso) e quindi un altro cappellino da ciclista (blu) o acquistarne due di seguito se non è possibile specificare la quantità.  
  
 I valori nelle righe 6 e 7 sono segnaposti. Quando si raggiunge la fine della catena di possibili transizioni, anziché terminare i risultati della stima, il valore passato come input viene aggiunto ai risultati. Se ad esempio, il numero di stime è stato aumentato a 20, i valori per le righe 6-20 sarà sempre lo stesso, All-Purpose Bike Stand.  
  
## <a name="function-list"></a>Elenco di funzioni  
 Tutti gli algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] supportano un set comune di funzioni. L'algoritmo Sequence Clustering di [!INCLUDE[msCoName](../../includes/msconame-md.md)] supporta tuttavia le funzioni aggiuntive elencate nella tabella seguente.  
  
|||  
|-|-|  
|Funzione di stima|Uso|  
|[Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx)|Viene restituito il cluster con la più alta probabilità di contenere il case di input.|  
|[ClusterDistance &#40;DMX&#41;](/sql/dmx/clusterdistance-dmx)|Viene restituita la distanza del case di input dal cluster specificato o la distanza del case di input dal cluster più probabile, se non viene specificato alcun cluster.<br /><br /> Questa funzione può essere utilizzata con qualsiasi tipo di modello di clustering (EM, K-medie, ecc.), ma i risultati variano in base all'algoritmo.|  
|[ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx)|Restituisce la probabilità che il case di input appartenga al cluster specificato.|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|Indica se il nodo specificato contiene o meno il case corrente.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|Viene restituita la probabilità adattata dello stato specificato.|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|Consente di stimare l'appartenenza associativa.|  
|[PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx)|Viene restituita la probabilità che un case di input risulti adatto al modello esistente.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|Restituisce una tabella che rappresenta un istogramma per la stima di una colonna specificata.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Viene restituito il Node_ID del nodo in cui è classificato il case.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|Viene restituita la probabilità per uno stato specificato.|  
|[PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx)|Vengono stimati i valori di sequenza futuri per un set specificato di dati in sequenza.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|Restituisce la deviazione standard stimata per la colonna specificata.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Viene restituito il valore di supporto per uno stato specificato.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Restituisce la varianza di una colonna specificata.|  
  
 Per un elenco delle funzioni comuni a tutti gli algoritmi di [!INCLUDE[msCoName](../../includes/msconame-md.md)], vedere [Funzioni di stima correlate &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx). Per la sintassi di funzioni specifiche, vedere [Guida di riferimento alle funzioni DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Vedere anche  
 [Query di data mining](data-mining-queries.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Sequence Clustering](microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md)   
 [Contenuto dei modelli di data mining per i modelli Sequence Clustering &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-sequence-clustering-models.md)  
  
  
