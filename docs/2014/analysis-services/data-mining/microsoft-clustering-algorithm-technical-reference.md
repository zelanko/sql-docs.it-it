---
title: Riferimento tecnico per l'algoritmo Microsoft Clustering | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [Data Mining]
- MAXIMUM_INPUT_ATTRIBUTES parameter
- CLUSTER_SEED parameter
- MODELLING_CARDINALITY parameter
- MINIMUM_SUPPORT parameter
- STOPPING_TOLERANCE parameter
- MAXIMUM_STATES parameter
- SAMPLE_SIZE parameter
- CLUSTERING_METHOD parameter
- soft clustering [Data Mining]
- clustering algorithms [Analysis Services]
- CLUSTER_COUNT parameter
ms.assetid: ec40868a-6dc7-4dfa-aadc-dedf69e555eb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d48dd57d71d04611947e0ec6158b29c97a6b7646
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084025"
---
# <a name="microsoft-clustering-algorithm-technical-reference"></a>Riferimento tecnico per l'algoritmo Microsoft Clustering
  In questa sezione viene illustrata l'implementazione dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering, inclusi i parametri che è possibile utilizzare per controllare il comportamento dei modelli di clustering. Vengono inoltre fornite istruzioni su come migliorare le prestazioni durante la creazione e l'elaborazione di modelli di clustering.  
  
 Per ulteriori informazioni sull'utilizzo dei modelli di clustering, vedere gli argomenti seguenti:  
  
-   [Contenuto dei modelli di data mining per i modelli di clustering &#40;Analysis Services - Data mining&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
-   [Esempi di query sul modello di clustering](clustering-model-query-examples.md)  
  
## <a name="implementation-of-the-microsoft-clustering-algorithm"></a>Implementazione dell'algoritmo Microsoft Clustering  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering rende disponibili due metodi per la creazione di cluster e l'assegnazione di punti dati ai cluster. Il primo, l'algoritmo *K-means* , è un metodo di tipo hard clustering, ovvero un punto dati può appartenere a un unico cluster e viene calcolata una singola probabilità per l'appartenenza di ogni punto dati a tale cluster. Il secondo, *Expectation Maximization* (EM), è un metodo di tipo *soft clustering* , ovvero un punto dati appartiene sempre a più cluster e viene calcolata una probabilità per ogni combinazione di punto dati e cluster.  
  
 È possibile scegliere l'algoritmo da usare impostando il parametro *CLUSTERING_METHOD* . Il metodo predefinito per il clustering è EM scalabile.  
  
### <a name="em-clustering"></a>Clustering EM  
 Nel clustering EM l'algoritmo perfeziona in modo iterativo un modello di cluster iniziale per il fit dei dati e determina la probabilità che un punto dati esista in un cluster. L'algoritmo termina il processo quando si ottiene il fit del modello probabilistico ai dati. La funzione utilizzata per determinare il fit è la probabilità in forma logaritmica dei dati, dato il modello.  
  
 Se durante il processo vengono generati cluster vuoti o se l'appartenenza di uno o più cluster è minore di una data soglia, i cluster con popolazioni basse vengono reinizializzati su nuovi punti e l'algoritmo EM viene rieseguito.  
  
 I risultati del metodo di clustering EM sono probabilistici, ovvero ogni punto dati appartiene a tutti i cluster, ma ogni assegnazione di un punto dati a un cluster presenta una probabilità diversa. Poiché il metodo consente la sovrapposizione dei cluster, la somma degli elementi di tutti i cluster può essere maggiore del totale degli elementi del set di training. Nei risultati del modello di data mining i punteggi che indicano il supporto vengono adattati per tenere conto di questa situazione.  
  
 L'algoritmo EM è l'algoritmo predefinito utilizzato nei modelli di clustering Microsoft. Viene utilizzato come predefinito perché offre più vantaggi rispetto al clustering K-means:  
  
-   Richiede al massimo un'analisi del database.  
  
-   Funziona anche se la quantità di memoria RAM è limitata.  
  
-   Ha la possibilità di utilizzare un cursore forward-only.  
  
-   Offre prestazioni più elevate rispetto agli approcci di campionamento.  
  
 L'implementazione Microsoft prevede due opzioni: EM scalabile e non scalabile. Per impostazione predefinita, nell'algoritmo EM scalabile vengono utilizzati i primi 50.000 record per inizializzare l'analisi iniziale. Se l'operazione riesce, il modello utilizza solo questi dati. Se non è possibile ottenere il fit del modello utilizzando 50.000 record, vengono letti altri 50.000 record. Nell'algoritmo EM non scalabile viene letto l'intero set di dati, indipendentemente dalla dimensione. Con questo metodo è possibile creare cluster più accurati, ma i requisiti di memoria possono essere significativi. Poiché EM scalabile opera su un buffer locale, le iterazioni nei dati sono molto più veloci e l'algoritmo utilizza la memoria cache della CPU in modo molto più efficace rispetto a EM non scalabile. Inoltre, EM scalabile è tre volte più veloce di EM non scalabile, anche se tutti i dati possono rientrare nella memoria principale. Nella maggior parte dei casi, il miglioramento delle prestazioni non implica una riduzione della qualità del modello completo.  
  
 Per un report tecnico in cui viene descritta l'implementazione di EM nell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering, vedere [Adattamento dell'algoritmo di clustering EM (Expectation Maximization) a database di grandi dimensioni](https://go.microsoft.com/fwlink/?LinkId=45964).  
  
### <a name="k-means-clustering"></a>Clustering K-means  
 Il clustering K-means è un metodo noto che consiste nell'assegnare l'appartenenza a un cluster riducendo le differenze tra gli elementi di un cluster e massimizzando allo stesso tempo la distanza tra i cluster. Il termine "means" in K-means fa riferimento al *centroide* del cluster, ovvero un punto dati scelto arbitrariamente e quindi perfezionato in modo iterativo finché non rappresenta la media reale di tutti i punti dati del cluster. La lettera "K" fa riferimento a un numero arbitrario di punti utilizzati per inizializzare il processo di clustering. L'algoritmo K-means calcola le distanze euclidee al quadrato tra i record di dati in un cluster e il vettore che rappresenta la media del cluster, quindi converge su un set finale di K cluster quando la somma raggiunge il valore minimo.  
  
 L'algoritmo K-means assegna ogni punto dati esattamente a un unico cluster e non consente incertezze nell'appartenenza. L'appartenenza a un cluster è espressa come distanza dal centro.  
  
 In genere, l'algoritmo K-means viene utilizzato per la creazione di cluster di attributi continui, in cui il calcolo della distanza da una media è un processo diretto. Tuttavia, l'implementazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] adatta il metodo K-means agli attributi discreti dei cluster, utilizzando le probabilità.  Per gli attributi discreti, la distanza di un punto dati da un determinato cluster viene calcolata come segue:  
  
 1 - P (punto dati, cluster)  
  
> [!NOTE]  
>  L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering non espone la funzione di distanza utilizzata nel calcolo di K-means e le misurazioni della distanza non sono disponibili nel modello completato. Tuttavia, è possibile utilizzare una funzione di stima per restituire un valore che corrisponde alla distanza, in cui la distanza viene calcolata come la probabilità che un punto dati appartenga al cluster. Per altre informazioni, vedere [ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx).  
  
 L'algoritmo K-means prevede due metodi di campionamento del set di dati: K-means non scalabile, che carica l'intero set di dati ed esegue un unico passaggio di clustering, oppure K-means scalabile, in cui l'algoritmo usa i primi 50.000 case e legge altri case solo se sono necessari più dati per ottenere un modello appropriato ai dati.  
  
### <a name="updates-to-the-microsoft-clustering-algorithm-in-sql-server-2008"></a>Aggiornamenti all'algoritmo Microsoft Clustering in SQL Server 2008  
 In SQL Server 2008 la configurazione predefinita dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering è stata modificata in modo da usare il parametro interno, NORMALIZATION = 1. La normalizzazione viene eseguita usando le statistiche z-score e presuppone una distribuzione normale. Lo scopo di questa modifica apportata al comportamento predefinito è ridurre l'effetto di attributi che potrebbero avere grandezze eccessive e molti outlier. Tuttavia, è possibile che la normalizzazione z-score alteri i risultati di clustering su distribuzioni che non sono normali (ad esempio, le distribuzioni uniformi). Per impedire la normalizzazione e ottenere lo stesso comportamento dell'algoritmo di clustering K-means di SQL Server 2005, è possibile usare la finestra di dialogo di **impostazione dei parametri** per aggiungere il parametro personalizzato, NORMALIZATION, e impostare il valore corrispondente su 0.  
  
> [!NOTE]  
>  Il parametro NORMALIZATION è una proprietà interna dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering e non è supportato. In generale l'uso della normalizzazione è consigliato nei modelli di clustering per migliorare i risultati del modello.  
  
## <a name="customizing-the-microsoft-clustering-algorithm"></a>Personalizzazione dell'algoritmo Microsoft Clustering  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering supporta vari parametri che influiscono sul comportamento, sulle prestazioni e sull'accuratezza del modello di data mining risultante.  
  
### <a name="setting-algorithm-parameters"></a>Impostazione dei parametri dell'algoritmo  
 Nella tabella seguente sono descritti i parametri che possono essere utilizzati con l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering. Tali parametri influiscono sia sulle prestazioni che sull'accuratezza del modello di data mining risultante.  
  
 CLUSTERING_METHOD  
 Specifica il metodo di clustering utilizzato dall'algoritmo. Sono disponibili i metodi di clustering seguenti:  
  
|ID|Metodo|  
|--------|------------|  
|1|EM scalabile|  
|2|EM non scalabile|  
|3|K-means scalabile|  
|4|K-means non scalabile|  
  
 Il valore predefinito è 1 (EM scalabile).  
  
 CLUSTER_COUNT  
 Specifica il numero approssimativo di cluster che devono essere generati dall'algoritmo. Se i dati non consentono di generare il numero approssimativo di cluster, l'algoritmo compila il maggior numero di cluster possibile. Se si imposta CLUSTER_COUNT su 0, l'algoritmo utilizzerà l'euristica per determinare con maggiore accuratezza il numero di cluster da compilare.  
  
 Il valore predefinito è 10.  
  
 CLUSTER_SEED  
 Specifica il numero di inizializzazione utilizzato per la generazione casuale dei cluster per la fase iniziale di compilazione del modello.  
  
 Modificando questo numero, è possibile cambiare il modo in cui vengono compilati i cluster iniziali, quindi confrontare i modelli compilati utilizzando valori di inizializzazione diversi. Se il valore di inizializzazione viene modificato ma i cluster trovati non cambiano di molto, il modello può essere considerato relativamente stabile.  
  
 Il valore predefinito è 0.  
  
 MINIMUM_SUPPORT  
 Specifica il numero minimo di case necessari per compilare un cluster. Se il numero di case nel cluster è minore di questo numero, il cluster viene considerato vuoto e viene ignorato.  
  
 Se si imposta un numero eccessivamente alto, è possibile che non vengano riscontrati cluster validi.  
  
> [!NOTE]  
>  Se si utilizza EM, ovvero il metodo di clustering predefinito, alcuni cluster possono avere un valore di supporto minore di quello specificato. Ogni case viene infatti valutato per rilevarne l'appartenenza a tutti i cluster possibili e per alcuni cluster può essere disponibile solo un supporto minimo.  
  
 Il valore predefinito è 1.  
  
 MODELLING_CARDINALITY  
 Specifica il numero di modelli di esempio costruiti durante il processo di clustering.  
  
 Riducendo il numero di modelli candidati, è possibile migliorare le prestazioni rischiando però di non riscontrare alcuni modelli candidati validi.  
  
 Il valore predefinito è 10.  
  
 STOPPING_TOLERANCE  
 Specifica il valore utilizzato per determinare quando viene raggiunta la convergenza e l'algoritmo ha completato la compilazione del modello. La convergenza viene raggiunta quando la variazione complessiva nelle probabilità del cluster è inferiore al rapporto tra il parametro STOPPING_TOLERANCE e la dimensione del modello.  
  
 Il valore predefinito è 10.  
  
 SAMPLE_SIZE  
 Specifica il numero di case utilizzati dall'algoritmo a ogni passaggio se il parametro CLUSTERING_METHOD è impostato su uno dei metodi di clustering scalabili. Se si imposta il parametro SAMPLE_SIZE su 0, l'intero set di dati verrà inserito nel cluster in un unico passaggio. Il caricamento dell'intero set di dati in un unico passaggio può generare problemi di memoria e prestazioni.  
  
 Il valore predefinito è 50000.  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 Specifica il numero massimo di attributi di input che l'algoritmo è in grado di gestire prima di richiamare la caratteristica di selezione degli attributi. Se si imposta il valore 0, indica che non esiste un numero massimo di attributi.  
  
 Se si aumenta il numero di attributi, si può verificare una riduzione significativa delle prestazioni.  
  
 Il valore predefinito è 255.  
  
 MAXIMUM_STATES  
 Specifica il numero massimo di stati degli attributi supportati dall'algoritmo. Se il numero di stati di un attributo è maggiore del numero massimo, l'algoritmo utilizza gli stati più frequenti dell'attributo e ignora gli stati rimanenti.  
  
 Se si aumenta il numero di stati, si può verificare una riduzione significativa delle prestazioni.  
  
 Il valore predefinito è 100.  
  
### <a name="modeling-flags"></a>Flag di modellazione  
 L'algoritmo supporta i flag di modellazione seguenti. I flag di modellazione, definiti durante la creazione della struttura o del modello di data mining, specificano la modalità di gestione dei valori in ogni colonna durante l'analisi.  
  
|Flag di modellazione|Descrizione|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|La colonna verrà considerata come se disponesse di due stati possibili: Missing ed Existing. Un valore Null è un valore mancante.<br /><br /> Si applica alla colonna del modello di data mining.|  
|NOT NULL|La colonna non può contenere un valore Null. Se Analysis Services rileva un valore Null durante il training del modello, viene generato un errore.<br /><br /> Si applica alla colonna della struttura di data mining.|  
  
## <a name="requirements"></a>Requisiti  
 Un modello di clustering deve contenere una colonna chiave e le colonne di input. È inoltre possibile definire le colonne di input come stimabili. Le colonne impostate su `Predict Only` non vengono utilizzate per la compilazione di cluster. La distribuzione di questi valori nel cluster viene calcolata dopo la compilazione dei cluster.  
  
### <a name="input-and-predictable-columns"></a>Colonne di input e stimabili  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering supporta specifiche colonne di input e colonne stimabili, riportate nella tabella seguente. Per altre informazioni sul significato dei tipi di contenuto usati in un modello di data mining, vedere [Tipi di contenuto &#40;Data mining&#41;](content-types-data-mining.md).  
  
|Colonna|Tipi di contenuto|  
|------------|-------------------|  
|Attributo di input|Continuous, Cyclical, Discrete, Discretized, Key, Table, Ordered|  
|Attributo stimabile|Continuous, Cyclical, Discrete, Discretized, Table, Ordered|  
  
> [!NOTE]  
>  Sono supportati i tipi di contenuto Cyclical e Ordered ma l'algoritmo li considera come valori discreti e non esegue un'elaborazione speciale.  
  
## <a name="see-also"></a>Vedi anche  
 [Algoritmo Microsoft Clustering](microsoft-clustering-algorithm.md)   
 [Esempi di query sul modello di clustering](clustering-model-query-examples.md)   
 [Contenuto dei modelli di data mining per i modelli di clustering &#40;Analysis Services - Data mining&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
  
