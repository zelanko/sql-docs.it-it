---
title: I parametri dell'algoritmo (SQL Server Data Mining Add-ins) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_STATES
- FORCED_REGRESSOR
- PERIODICITY_HINT
- HOLDOUT_SEED
- MAXIMUM_ITEMSET_SIZE
- HIDDEN_NODE_RATIO
- CLUSTERING_METHOD
- FORECAST_METHOD
- STOPPING_TOLERANCE
- MISSING_VALUE_SUBSTITUTION
- MINIMUM_IMPORTANCE
- HISTORIC_MODEL_COUNT
- SPLIT_METHOD
- MAXIMUM_OUTPUT_ATTRIBUTES
- HOLDOUT_PERCENTAGE
- MINIMUM_PROBABILITY
- SAMPLE_SIZE
- HISTORICAL_MODEL_GAP
- CLUSTER_SEED
- SCORE_METHOD
- INSTABILITY_SENSITIVITY
- AUTO_DETECT_PERIODICITY
- MAXIMUM_SEQUENCE_STATES
- MINIMUM_DEPENDENCY_PROBABILITY
- MINIMUM_SUPPORT
- MAXIMUM_SUPPORT
- MINIMUM_ITEMSET_SIZE
- PREDICTION_SMOOTHING
- algorithm parameters
- MAXIMUM_SERIES_VALUE
- MODELLING_CARDINALITY
- MAXIMUM_INPUT_ATTRIBUTES
- MINIMUM_SERIES_VALUE
- MAXIMUM_ITEMSET_COUNT
- CLUSTER_COUNT
- COMPLEXITY_PENALTY
ms.assetid: fcdc3f85-813d-4279-90b0-16e26edd008d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e902272c58f1e841a3108199e53d51ac12f8ae4a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062603"
---
# <a name="algorithm-parameters-sql-server-data-mining-add-ins"></a>Parametri degli algoritmi (componenti aggiuntivi Data mining di SQL Server)
  Quando si esegue il data mining utilizzando Strumenti di analisi tabelle per Excel, non è necessario configurare l'algoritmo o i parametri di data mining. Ogni strumento analizza i dati e seleziona automaticamente i parametri ottimali. Se tuttavia si desidera modificare il modello o creare un modello di data mining da zero, il client di data mining per Excel offre diverse opzioni per la personalizzazione.  
  
-   Creare un modello di data mining manualmente, scegliendo **avanzate** e quindi scegliendo **aggiunta modello a struttura**.  
  
-   Usare una delle modellazioni guidate in Client di Data Mining e fare clic su **parametri** per controllare il comportamento del [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmi di data mining.  
  
-   Fare clic su **Query** per aprire la procedura guidata Query modello e quindi fare clic su **Advanced** per aprire il **Advanced Query Editor di Data Mining**. In questo editor è possibile compilare i modelli utilizzando modelli DMX.  
  
 È inoltre possibile modificare il comportamento dei modelli di data mining già creati o filtrare i risultati impostando i parametri desiderati nel visualizzatore del modello di data mining.  
  
## <a name="list-of-algorithm-parameters"></a>Elenco di parametri degli algoritmi  
 Tutti gli algoritmi [!INCLUDE[msCoName](../includes/msconame-md.md)] possono essere personalizzati impostandone i parametri. Poiché le impostazioni migliori dei parametri dipendono dalla composizione dei dati, la spiegazione completa degli effetti della modifica dei parametri non rientra nell'ambito di questo argomento.  
  
 Nella tabella seguente sono elencati i parametri con una descrizione delle relative funzionalità e vengono forniti collegamenti a ulteriori informazioni tecniche.  
  
|Nome parametro|Campo di utilizzo|Descrizione|  
|--------------------|-------------|-----------------|  
|AUTO_DETECT_PERIODICITY|Algoritmo Microsoft Time Series|Specifica un valore numerico compreso tra 0 e 1 utilizzato per il rilevamento della periodicità. L'impostazione di un valore prossimo a 1 favorisce l'individuazione di numerosi modelli quasi-periodici e la generazione automatica di hint di periodicità. La gestione di un numero elevato di hint di periodicità porterà probabilmente a tempi di esecuzione di training del modello significativamente più lunghi e a modelli più accurati. Se il valore è prossimo allo zero, la periodicità viene rilevata solo per i dati fortemente periodici.<br /><br /> Il valore predefinito è 0,6.|  
|CLUSTER_COUNT|Algoritmo Microsoft Clustering<br /><br /> Algoritmo Microsoft Sequence Clustering|Specifica il numero approssimativo di cluster che devono essere generati dall'algoritmo. Se i dati non consentono di generare il numero approssimativo di cluster, l'algoritmo compila il maggior numero di cluster possibile. Se si imposta CLUSTER_COUNT su 0, l'algoritmo utilizzerà l'euristica per determinare con maggiore accuratezza il numero di cluster da compilare.<br /><br /> Il valore predefinito è 10.|  
|CLUSTER_SEED|Algoritmo Microsoft Clustering|Specifica il numero di inizializzazione utilizzato per la generazione casuale dei cluster per la fase iniziale di compilazione del modello.<br /><br /> Il valore predefinito è 0.|  
|CLUSTERING_METHOD|Algoritmo Microsoft Clustering|Specifica il metodo di clustering utilizzato dall'algoritmo. I metodi di clustering disponibili sono: EM scalabile (1), EM non scalabile (2), K-medie scalabile (3) e K-medie non scalabile (4).<br /><br /> Il valore predefinito è 1.|  
|COMPLEXITY_PENALTY|Algoritmo Microsoft Decision Trees<br /><br /> Algoritmo Microsoft Time Series|Controlla la crescita dell'albero delle decisioni. Un valore basso comporta l'aumento del numero di divisioni, mentre un valore alto comporta la diminuzione del numero di divisioni. Il valore predefinito è basato sul numero di attributi per un modello specifico, come descritto nell'elenco seguente:<br /><br /> Per un numero di attributi compreso tra 1 e 9, il valore predefinito è 0,5.<br /><br /> Per un numero di attributi compreso tra 10 e 99, il valore predefinito è 0,9.<br /><br /> Per un numero di attributi maggiore o uguale a 100, il valore predefinito è 0,99.<br /><br /> Nota: Nei modelli time series, questo parametro si applica solo ai modelli compilati utilizzando l'algoritmo ARTxp o ai modelli misti.|  
|FORCED_REGRESSOR|Algoritmo Microsoft Decision Trees<br /><br /> Algoritmo Microsoft Linear Regression|Forza l'utilizzo, da parte dell'algoritmo, delle colonne indicate come regressori, indipendentemente dall'importanza delle colonne calcolata dall'algoritmo.<br /><br /> Nota: Questo parametro viene utilizzato solo per gli alberi delle decisioni che stimano un attributo continuo. Un modello per la regressione lineare è, per definizione, un tipo speciale di albero delle decisioni che stima attributi continui. Qualsiasi modello di albero delle decisioni può tuttavia contenere un nodo che rappresenta una formula di regressione lineare.|  
|FORECAST_METHOD|Algoritmo Microsoft Time Series|Indica se le stime devono essere fatte utilizzando l'algoritmo ARTxp, l'algoritmo ARIMA o una combinazione di entrambi.<br /><br /> L'impostazione predefinita è MIXED.|  
|HIDDEN_NODE_RATIO|Microsoft Neural Network Algorithm|Specifica il rapporto tra i neuroni nascosti e i neuroni di input e di output. La formula seguente consente di determinare il numero iniziale di neuroni nel livello nascosto:<br /><br /> HIDDEN_NODE_RATIO * SQRT (Totale neuroni di input \* Totale neuroni di output)<br /><br /> Il valore predefinito è 4,0.|  
|HISTORIC_MODEL_COUNT|Algoritmo Microsoft Time Series|Specifica il numero di modelli cronologici che verranno generati.<br /><br /> Il valore predefinito è 1.|  
|HISTORICAL_MODEL_GAP|Algoritmo Microsoft Time Series|Specifica l'intervallo di tempo tra due modelli cronologici consecutivi. Se si imposta questo valore su g, ad esempio, verranno generati modelli cronologici per i dati suddivisi in periodi di tempo in corrispondenza degli intervalli g, 2*g, 3\*g e così via.<br /><br /> Il valore predefinito è 10.|  
|HOLDOUT_PERCENTAGE|Algoritmo Microsoft Logistic Regression<br /><br /> Microsoft Neural Network Algorithm|Specifica la percentuale di case all'interno dei dati di training utilizzata per calcolare l'errore dei dati di controllo nell'ambito dei criteri di interruzione durante l'esecuzione del training del modello di data mining.<br /><br /> Il valore predefinito è 30.<br /><br /> Nota: Questo parametro è diverso dal valore della percentuale dei dati di controllo che si applica a una struttura di data mining.|  
|HOLDOUT_SEED|Algoritmo Microsoft Logistic Regression<br /><br /> Microsoft Neural Network Algorithm|Specifica un numero utilizzato come valore di inizializzazione per il generatore pseudocasuale quando l'algoritmo determina in modo casuale i dati di controllo. Se questo parametro è impostato su 0, l'algoritmo genera il valore di inizializzazione in base al nome del modello di data mining, per garantire che il contenuto del modello rimanga invariato durante la rielaborazione.<br /><br /> Il valore predefinito è 0.<br /><br /> Nota: Questo parametro è diverso dal valore di inizializzazione di controllo che si applica a una struttura di data mining.|  
|INSTABILITY_SENSITIVITY|Algoritmo Microsoft Time Series|Controlla il punto in cui la varianza della stima supera una determinata soglia e l'algoritmo ARTxp elimina le stime. Il valore predefinito è 1.<br /><br /> Nota: Questo parametro si applica solo ai modelli misti o modelli che utilizzano l'algoritmo ARTxp.|  
|MAXIMUM_INPUT_ATTRIBUTES|Algoritmo Microsoft Clustering<br /><br /> Algoritmo Microsoft Decision Trees<br /><br /> Algoritmo Microsoft Linear Regression<br /><br /> Algoritmo Microsoft Naive Bayes<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Algoritmo Microsoft Logistic Regression|Definisce il numero di attributi di input che l'algoritmo è in grado di gestire prima di richiamare la funzionalità di selezione degli attributi. Impostare questo valore su 0 per disabilitare la funzionalità di selezione degli attributi.<br /><br /> Il valore predefinito è 255.|  
|MAXIMUM_ITEMSET_COUNT|Algoritmo Microsoft Association Rules|Specifica il numero massimo di set di elementi da produrre. Se non viene specificato alcun valore, l'algoritmo genera tutti i set di elementi possibili.<br /><br /> Il valore predefinito è 200000.|  
|MAXIMUM_ITEMSET_SIZE|Algoritmo Microsoft Association Rules|Specifica il numero massimo di elementi consentiti in un set di elementi. Se si imposta il valore su 0, non esiste alcun limite per le dimensioni del set di elementi.<br /><br /> Il valore predefinito è 3.|  
|MAXIMUM_OUTPUT_ATTRIBUTES|Algoritmo Microsoft Decision Trees<br /><br /> Algoritmo Microsoft Linear Regression<br /><br /> Algoritmo Microsoft Logistic Regression<br /><br /> Algoritmo Microsoft Naive Bayes<br /><br /> Microsoft Neural Network Algorithm|Definisce il numero di attributi di output che l'algoritmo è in grado di gestire prima di richiamare la funzionalità di selezione degli attributi. Impostare questo valore su 0 per disabilitare la funzionalità di selezione degli attributi.<br /><br /> Il valore predefinito è 255.|  
|MAXIMUM_SEQUENCE_STATES|Algoritmo Microsoft Sequence Clustering|Specifica il numero massimo di stati consentiti in una sequenza. Se si imposta un valore numerico maggiore di 100, l'algoritmo potrebbe creare un modello che non fornisce informazioni significative.<br /><br /> Il valore predefinito è 64.|  
|MAXIMUM_SERIES_VALUE|Algoritmo Microsoft Time Series|Specifica il valore massimo da utilizzare per le stime. Questo parametro viene utilizzato, insieme a MINIMUM_SERIES_VALUE, per vincolare le stime a un intervallo previsto. È possibile, ad esempio, specificare che la quantità stimata per le vendite per qualsiasi giorno non deve mai superare il numero di prodotti in inventario.|  
|MAXIMUM_STATES|Algoritmo Microsoft Clustering<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Algoritmo Microsoft Sequence Clustering|Specifica il numero massimo di stati degli attributi supportati dall'algoritmo. Se il numero di stati di un attributo è maggiore del numero massimo di stati, l'algoritmo utilizza stati più frequenti dell'attributo e ignora gli stati rimanenti.<br /><br /> Il valore predefinito è 100.|  
|MAXIMUM_SUPPORT|Algoritmo Microsoft Association Rules|Specifica il numero massimo di case che possono supportare un determinato set di elementi. I valori minori di 1 rappresentano una percentuale sul totale dei case. I valori maggiori di 1 rappresentano il numero assoluto di case che possono contenere il set di elementi.<br /><br /> Il valore predefinito è 1.|  
|MINIMUM_IMPORTANCE|Algoritmo Microsoft Association Rules|Specifica la soglia di importanza per le regole di associazione. Le regole con importanza inferiore a questo valore vengono escluse.|  
|MINIMUM_ITEMSET_SIZE|Algoritmo Microsoft Association Rules|Specifica il numero minimo di elementi consentiti in un set di elementi.<br /><br /> Il valore predefinito è 1.|  
|MINIMUM_DEPENDENCY_PROBABILITY|Algoritmo Microsoft Naive Bayes|Specifica la probabilità di dipendenza minima tra gli attributi di input e di output. Questo valore viene utilizzato per limitare le dimensioni del contenuto generato dall'algoritmo. Il valore di questa proprietà è compreso tra 0 e 1. Valori maggiori riducono il numero di attributi nel contenuto del modello.<br /><br /> Il valore predefinito è 0.5.|  
|MINIMUM_PROBABILITY|Algoritmo Microsoft Association Rules|Specifica la probabilità minima che una regola sia vera (True). Se si imposta il valore 0,5, ad esempio, non verranno generate regole con probabilità inferiore al 50%.<br /><br /> Il valore predefinito è 0,4.|  
|MINIMUM_SERIES_VALUE|Algoritmo Microsoft Time Series|Specifica il vincolo inferiore per tutte le stime basate su serie temporali. I valori stimati non potranno mai essere inferiori al valore di questo vincolo.|  
|MINIMUM_SUPPORT|Algoritmo Microsoft Association Rules|Specifica il numero minimo di case che devono contenere il set di elementi affinché l'algoritmo possa generare una regola. Se si imposta un valore minore di 1, il numero minimo di case viene indicato come percentuale sul totale dei case. Se si imposta un numero intero maggiore di 1, il numero minimo di case è indicato come numero assoluto di case che devono contenere il set di elementi. Se la memoria è limitata, l'algoritmo può aumentare il valore di questo parametro.<br /><br /> Il valore predefinito è 0,03.|  
|MINIMUM_SUPPORT|Algoritmo Microsoft Clustering|Specifica il numero minimo di case in ogni cluster.<br /><br /> Il valore predefinito è 1.|  
|MINIMUM_SUPPORT|Algoritmo Microsoft Decision Trees|Determina il numero minimo di case foglia necessari per generare una divisione nell'albero delle decisioni.<br /><br /> Il valore predefinito è 10.|  
|MINIMUM_SUPPORT|Algoritmo Microsoft Sequence Clustering|Specifica il numero minimo di case in ogni cluster.<br /><br /> Il valore predefinito è 10.|  
|MINIMUM_SUPPORT|Algoritmo Microsoft Time Series|Specifica il numero minimo di intervalli di tempo necessari per generare una divisione in ogni albero di serie temporali.<br /><br /> Il valore predefinito è 10.|  
|MISSING_VALUE_SUBSTITUTION|Algoritmo Microsoft Time Series|Specifica il metodo utilizzato per riempire i gap nei dati cronologici. Per impostazione predefinita, non sono consentiti gap irregolari o margini discontinui nei dati. I metodi disponibili per riempire i margini o i gap irregolari sono l'utilizzo del valore precedente, l'utilizzo del valore medio o l'utilizzo di una costante numerica specifica.|  
|MODELLING_CARDINALITY|Algoritmo Microsoft Clustering|Specifica il numero di modelli di esempio costruiti durante il processo di clustering.<br /><br /> Il valore predefinito è 10.|  
|PERIODICITY_HINT|Algoritmo Microsoft Time Series|Fornisce un hint all'algoritmo in riferimento alla periodicità dei dati. Se, ad esempio, le vendite variano in base all'anno e l'unità di misura utilizzata nella serie è il mese, la periodicità è 12. Questo parametro viene espresso nel formato {n [, n]}, dove n è qualsiasi numero positivo. Il valore n all'interno delle parentesi quadre [] è facoltativo e può essere ripetuto con la frequenza necessaria.<br /><br /> Il valore predefinito è {1}.|  
|PREDICTION_SMOOTHING|Algoritmo Microsoft Time Series|Controlla la combinazione degli algoritmi Time Series ARTXP e ARIMA. Il valore specificato è valido solo quando il parametro FORECAST_METHOD è impostato su MIXED. I valori devono essere compresi tra 0 e 1. Se il valore è 0, il modello utilizza solo ARTXP. Se il valore è 1, il modello utilizza solo ARIMA. Un valore più vicino allo 0 indica che il risultato viene ponderato maggiormente rispetto all'algoritmo ARTXP. Un valore più vicino a 1 indica che il risultato viene ponderato maggiormente rispetto all'algoritmo ARIMA.|  
|SAMPLE_SIZE|Algoritmo Microsoft Clustering|Specifica il numero di case utilizzati dall'algoritmo a ogni passaggio se il parametro CLUSTERING_METHOD è impostato su uno dei metodi di clustering scalabili. Se si imposta il parametro SAMPLE_SIZE su 0, l'intero set di dati verrà inserito nel cluster in un unico passaggio. Questo può provocare problemi di memoria e prestazioni.<br /><br /> Il valore predefinito è 50000.|  
|SAMPLE_SIZE|Algoritmo Microsoft Logistic Regression<br /><br /> Microsoft Neural Network Algorithm|Specifica il numero di case da utilizzare per eseguire il training del modello. Il provider dell'algoritmo utilizza questo numero o la percentuale del numero totale di case non inclusi nella percentuale di controllo specificata dal parametro HOLDOUT_PERCENTAGE, a seconda del valore minore.<br /><br /> In altre parole, se il parametro HOLDOUT_PERCENTAGE è impostato su 30, l'algoritmo userà il valore di questo parametro o un valore pari al 70% del numero totale di case, a seconda del valore minore.<br /><br /> L'impostazione predefinita è 10000.|  
|SCORE_METHOD|Algoritmo Microsoft Decision Trees|Determina il metodo utilizzato per calcolare il punteggio di divisione. Sono disponibili le opzioni seguenti: (1) entropia, (2) Bayes con probabilità precedente K2 o (3) Bayesian Dirichlet equivalente (Bayes Dirichlet BDE) precedente.<br /><br /> Il valore predefinito è 3.|  
|SPLIT_METHOD|Algoritmo Microsoft Decision Trees|Determina il metodo utilizzato per la divisione del nodo. Sono disponibili le opzioni seguenti: Binario (1), completo (2) o entrambi (3).<br /><br /> Il valore predefinito è 3.|  
|STOPPING_TOLERANCE|Riferimento tecnico per l'algoritmo Microsoft Clustering|Specifica il valore utilizzato per determinare quando viene raggiunta la convergenza e l'algoritmo ha completato la compilazione del modello. La convergenza viene raggiunta quando la variazione complessiva nelle probabilità del cluster è inferiore al rapporto tra il parametro STOPPING_TOLERANCE e la dimensione del modello.<br /><br /> Il valore predefinito è 10.|  
  
### <a name="comments"></a>Commenti  
 Per ulteriori informazioni sugli algoritmi, vedere la documentazione online di SQL Server.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di Data Mining &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md)  
  
  
