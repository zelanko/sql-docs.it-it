---
title: Riferimento tecnico per l'algoritmo Microsoft Neural Network | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- HIDDEN_NODE_RATIO parameter
- MAXIMUM_INPUT_ATTRIBUTES parameter
- HOLDOUT_PERCENTAGE parameter
- neural network algorithms [Analysis Services]
- output layer [Data Mining]
- neural networks
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- MAXIMUM_STATES parameter
- SAMPLE_SIZE parameter
- hidden layer
- hidden neurons
- input layer [Data Mining]
- activation function [Data Mining]
- Back-Propagated Delta Rule network
- neural network model [Analysis Services]
- coding [Data Mining]
- HOLDOUT_SEED parameter
ms.assetid: b8fac409-e3c0-4216-b032-364f8ea51095
author: minewiskan
ms.author: owend
ms.openlocfilehash: bf7db49fd2b6a86e9b113dbede785379f910b978
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84521767"
---
# <a name="microsoft-neural-network-algorithm-technical-reference"></a>Microsoft Neural Network Algorithm Technical Reference
  L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network usa una rete *perceptron multistrato* , chiamata anche *rete Delta Rule con retropropagazione*, costituita da un massimo di tre livelli neurali o *perceptron*. Tali livelli rappresentano rispettivamente un livello di input, un livello nascosto facoltativo e un livello di output.  
  
 Una descrizione dettagliata delle reti neurali perceptron multistrato esula dagli argomenti trattati nella presente documentazione. In questo argomento viene illustrata l'implementazione di base dell'algoritmo, inclusi il metodo utilizzato per normalizzare i valori di input e output e i metodi relativi alla caratteristica di selezione degli attributi utilizzati per ridurre la cardinalità degli attributi. Vengono inoltre descritti i parametri e altre impostazioni che è possibile utilizzare per personalizzare il comportamento dell'algoritmo e vengono forniti collegamenti a informazioni aggiuntive relative all'esecuzione di query sul modello.  
  
## <a name="implementation-of-the-microsoft-neural-network-algorithm"></a>Implementazione dell'algoritmo Microsoft Neural Network  
 In una rete neurale perceptron multistrato ogni neurone riceve uno o più input e produce uno o più output identici. Ogni output è una funzione semplice non lineare della somma degli input ricevuti dal neurone. Gli input passano dai nodi del livello di input ai nodi del livello nascosto, quindi ai nodi del livello di output. Non esistono connessioni tra i neuroni all'interno di un livello. Se non è disponibile un livello nascosto, come accade nei modelli di regressione logistica, gli input passano direttamente dai nodi del livello di input ai nodi del livello di output.  
  
 Una rete neurale creata con l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network include tre tipi di neuroni:  
  
-   `Input neurons`  
  
 I neuroni di input forniscono i valori degli attributi per il modello di data mining. Per gli attributi di input discreti, un neurone di input rappresenta generalmente un singolo stato derivato da questo tipo di attributo. Se i dati di training contengono valori Null per l'attributo, sono inclusi anche i valori mancanti. Se nei dati di training sono inclusi valori Null, un attributo di input discreto che include più di due stati genera un neurone di input per ogni stato e un neurone di input per uno stato mancante. Un attributo di input continuo genera due neuroni di input: un neurone per uno stato mancante e uno per il valore dell'attributo continuo stesso. I neuroni di input inviano gli input a uno o più neuroni nascosti.  
  
-   `Hidden neurons`  
  
 I neuroni nascosti ricevono gli input dai neuroni di input e inviano gli output ai neuroni di output.  
  
-   `Output neurons`  
  
 I neuroni di output rappresentano i valori degli attributi stimabili per il modello di data mining. Per gli attributi di input discreti, un neurone di output rappresenta generalmente un singolo stato stimato per un attributo stimabile, inclusi i valori mancanti. Ad esempio, un attributo stimabile binario genera un nodo di output che descrive uno stato mancante o esistente, indicando se è disponibile un valore per tale attributo. Una colonna booleana utilizzata come attributo stimabile genera tre neuroni di output: un neurone per i valori True, uno per i valori False e un altro per uno stato mancante o esistente. Un attributo stimabile discreto che include più di due stati genera un neurone di output per ogni stato e un neurone di output per uno stato mancante o esistente. Le colonne stimabili continue generano due neuroni di output: un neurone per uno stato mancante o esistente e uno per il valore della colonna continua stessa. Se vengono generati più di 500 neuroni di output esaminando il set di colonne stimabili, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera un nuova rete nel modello di data mining per rappresentare i neuroni di output aggiuntivi.  
  
 Un neurone riceve l'input dagli altri neuroni o da altri dati, a seconda del livello della rete in cui si trova. Un neurone di input riceve gli input dai dati originali. I neuroni di output e i neuroni nascosti ricevono gli input dall'output degli altri neuroni della rete neurale. Gli input stabiliscono le relazioni tra i neuroni e le relazioni vengono utilizzate come percorso di analisi per un set di case specifico.  
  
 A ogni input viene assegnato un valore, denominato *peso*, che ne rappresenta la pertinenza o la priorità per il neurone nascosto o per il neurone di output. Maggiore è il peso assegnato a un input, più rilevante, o prioritario, è il rispettivo valore. I pesi possono essere negativi, ovvero l'input può inibire un neurone specifico anziché attivarlo. Il valore di ogni input viene moltiplicato per il peso in modo da evidenziare la rispettiva priorità per un neurone specifico. Nel caso di pesi negativi, moltiplicando il valore per il peso si riduce la priorità dell'input.  
  
 A ogni neurone viene assegnata una funzione semplice non lineare, denominata *funzione di attivazione*, che ne rappresenta la pertinenza o la priorità per il livello corrispondente di una rete neurale. Per la funzione di attivazione, i neuroni nascosti usano una funzione di *tangente iperbolica* (tanh), mentre i neuroni di output utilizzano una funzione *sigmoidale* . Entrambe le funzioni sono funzioni non lineari continue che consentono alla rete neurale di modellare relazioni non lineari tra i neuroni di input e di output.  
  
### <a name="training-neural-networks"></a>Reti neurali di training  
 Il training di un modello di data mining che utilizza l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network implica varie operazioni. Tali operazioni vengono notevolmente influenzate dai valori specificati per i parametri disponibili per l'algoritmo.  
  
 L'algoritmo inizialmente valuta ed estrae i dati di training dall'origine dei dati. Una percentuale dei dati di training, denominati *dati di controllo*, viene riservata per la valutazione dell'accuratezza della rete. Durante il processo di training, la rete viene valutata immediatamente dopo ogni iterazione sui dati di training. Quando l'accuratezza non aumenta più, il processo di training viene arrestato.  
  
 I valori dei parametri *SAMPLE_SIZE* e *HOLDOUT_PERCENTAGE* vengono usati per determinare il numero di case di campionamento da estrarre dai dati di training e il numero di case da riservare per i dati di controllo. Il valore del parametro *HOLDOUT_SEED* viene usato per la determinazione casuale dei singoli case da riservare per i dati di controllo.  
  
> [!NOTE]  
>  Questi parametri dell'algoritmo sono diversi dalle proprietà HOLDOUT_SIZE e HOLDOUT_SEED, che vengono applicate a una struttura di data mining per definire un set di dati di testing.  
  
 Successivamente l'algoritmo determina il numero e la complessità delle reti supportate dal modello di data mining. Se il modello di data mining contiene uno o più attributi utilizzati solo per la stima, l'algoritmo crea una singola rete che rappresenta tutti gli attributi. Se il modello di data mining contiene uno o più attributi utilizzati sia per l'input che per la stima, il provider dell'algoritmo costruisce una rete per ogni attributo.  
  
 Per gli attributi di input e stimabili con valori discreti, ogni neurone di input o di output rappresenta rispettivamente un singolo stato. Per gli attributi di input e stimabili con valori continui, ogni neurone di input o di output rappresenta rispettivamente l'intervallo e la distribuzione dei valori dell'attributo. Il numero massimo di stati supportato in ognuno dei due casi dipende dal valore del parametro *MAXIMUM_STATES* dell'algoritmo. Se il numero di stati per un attributo specifico supera il valore del parametro *MAXIMUM_STATES* dell'algoritmo, vengono scelti gli stati più frequenti o rilevanti per tale attributo, fino al numero massimo di stati consentiti, mentre gli stati rimanenti vengono raggruppati come valori mancanti da usare a scopo di analisi.  
  
 L'algoritmo usa quindi il valore del parametro *HIDDEN_NODE_RATIO* durante la determinazione del numero iniziale di neuroni per creare il livello nascosto. È possibile impostare il parametro *HIDDEN_NODE_RATIO* su 0 per impedire la creazione di un livello nascosto nelle reti generate dall'algoritmo per il modello di data mining, in modo che la rete neurale venga considerata come una regressione logistica.  
  
 Il provider dell'algoritmo valuta contemporaneamente il peso di tutti gli input della rete in modo iterativo, considerando il set di dati di training riservato in precedenza e confrontando il valore noto effettivo per ogni case nei dati di controllo con la stima della rete, mediante un processo noto come *apprendimento in batch*. Dopo che l'algoritmo ha valutato l'intero set di dati di training, esamina il valore stimato ed effettivo per ogni neurone. L'algoritmo calcola l'eventuale grado di errore e modifica i pesi associati agli input di tale neurone, procedendo a ritroso dai neuroni di output ai neuroni di input in un processo noto come *retropropagazione*. Successivamente, l'algoritmo ripete il processo sull'intero set di dati di training. Poiché l'algoritmo può supportare molti pesi e neuroni di output, viene utilizzato l'algoritmo basato su gradienti coniugati per gestire il processo di training al fine di assegnare e valutare i pesi per gli input. Una descrizione dettagliata dell'algoritmo basato su gradienti coniugati esula dagli argomenti trattati nella presente documentazione.  
  
### <a name="feature-selection"></a>Selezione caratteristiche  
 Se il numero degli attributi di input è maggiore del valore del parametro *MAXIMUM_INPUT_ATTRIBUTES* , oppure se il numero di attributi stimabili è maggiore del valore del parametro *MAXIMUM_OUTPUT_ATTRIBUTES* , viene usato un algoritmo di selezione delle caratteristiche per ridurre la complessità delle reti incluse nel modello di data mining. La caratteristica di selezione degli attributi riduce il numero degli attributi di input o stimabili, in quanto vengono scelti quelli statisticamente più rilevanti per il modello.  
  
 Tutti gli algoritmi di data mining [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizzano automaticamente la caratteristica di selezione degli attributi per migliorare l'analisi e ridurre il carico di elaborazione. Il metodo utilizzato per la caratteristica di selezione degli attributi nei modelli di reti neurali dipende dal tipo di dati dell'attributo. Nella tabella seguente sono mostrati per riferimento i metodi relativi alla caratteristica di selezione degli attributi utilizzati per i modelli di reti neurali e quelli utilizzati per l'algoritmo Logistic Regression, che si basa sull'algoritmo Neural Network.  
  
|Algoritmo|Metodo di analisi|Commenti|  
|---------------|------------------------|--------------|  
|Neural Network|Punteggio di interesse<br /><br /> Entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Nell'algoritmo Neural Network possono essere utilizzati sia i metodi Bayes sia quelli basati sull'entropia, purché nei dati siano contenute colonne continue.<br /><br /> Valore predefinito.|  
|Logistic Regression|Punteggio di interesse<br /><br /> Entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Poiché non è possibile passare un parametro a questo algoritmo per controllare il comportamento della caratteristica di selezione degli attributi, vengono utilizzate le impostazioni predefinite. Se pertanto tutti gli attributi sono discreti o discretizzati, l'impostazione predefinita è BDEU.|  
  
 I parametri dell'algoritmo che controllano la caratteristica di selezione degli attributi per un modello di rete neurale sono MAXIMUM_INPUT_ATTRIBUTES, MAXIMUM_OUTPUT_ATTRIBUTES e MAXIMUM_STATES. È inoltre possibile controllare il numero di livelli nascosti impostando il parametro HIDDEN_NODE_RATIO.  
  
### <a name="scoring-methods"></a>Metodi di valutazione  
 La*valutazione* è una sorta di normalizzazione che, nel contesto del training di un modello di rete neurale, indica il processo di conversione di un valore, ad esempio un'etichetta di testo discreta, in un valore che può essere confrontato con altri tipi di input e ponderato nella rete. Se ad esempio un attributo di input è Gender e i valori possibili sono Male e Female, mentre un altro attributo di input è Income, con un intervallo variabile di valori, i valori per ogni attributo non sono direttamente confrontabili e pertanto devono essere codificati in una scala comune in modo da consentirne il calcolo del peso. La valutazione è il processo in base al quale tali input vengono normalizzati in valori numerici, nello specifico in un intervallo di probabilità. Le funzioni utilizzate per la normalizzazione consentono inoltre di distribuire in modo più uniforme il valore di input in modo che valori estremi non alterino i risultati dell'analisi.  
  
 Vengono inoltre codificati gli output della rete neurale. Quando per l'output è disponibile una sola destinazione (ovvero la stima) oppure più destinazioni utilizzate esclusivamente per la stima e non per l'input, il modello crea una sola rete e la normalizzazione dei valori potrebbe sembrare non necessaria. Se tuttavia per l'input e la stima vengono utilizzati più attributi, il modello deve creare più reti, pertanto tutti i valori devono essere normalizzati e anche gli output devono essere codificati quando escono dalla rete.  
  
 La codifica per gli input si basa sulla somma di ogni valore discreto nei case di training e sulla moltiplicazione del valore ottenuto per il rispettivo peso. Questa operazione viene definita *somma ponderata*e viene passata alla funzione di attivazione nel livello nascosto. Per la codifica viene utilizzato un punteggio z, come illustrato di seguito:  
  
 **Valori discreti**  
  
 μ = p: probabilità precedente di uno stato  
  
 StdDev = sqrt (p (1-p))  
  
 **Valori continui**  
  
 Valore presente = 1-μ/σ  
  
 Nessun valore esistente =-μ/σ  
  
 Dopo che i valori sono stati codificati, gli input vengono sottoposti alla somma ponderata, in cui i pesi sono rappresentati dai bordi delle reti.  
  
 Per la codifica degli output viene utilizzata la funzione sigmoidale, le cui proprietà la rendono molto utile per la stima. In base a una di tali proprietà, indipendentemente da come vengono ridimensionati i valori originali e indipendentemente dal fatto che tali valori siano negativi o positivi, l'output di questa funzione è sempre un valore compreso tra 0 e 1, ovvero un valore appropriato per la stima delle probabilità. Un'altra proprietà utile è la funzione sigmoidale con effetto di smussatura, in base alla quale man mano che i valori si allontanano dal punto di flesso, la probabilità del valore si sposta lentamente verso 0 o 1.  
  
## <a name="customizing-the-neural-network-algorithm"></a>Personalizzazione dell'algoritmo Neural Network  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network supporta vari parametri che influiscono sul comportamento, sulle prestazioni e sull'accuratezza del modello di data mining risultante. È inoltre possibile modificare la modalità con cui il modello elabora i dati impostando flag di modellazione nelle colonne oppure impostando flag di distribuzione per specificare come devono essere gestiti i valori all'interno della colonna.  
  
### <a name="setting-algorithm-parameters"></a>Impostazione dei parametri dell'algoritmo  
 Nella tabella seguente vengono descritti i parametri che possono essere utilizzati con l'algoritmo Microsoft Neural Network.  
  
 HIDDEN_NODE_RATIO  
 Specifica il rapporto tra i neuroni nascosti e i neuroni di input e di output. La formula seguente consente di determinare il numero iniziale di neuroni nel livello nascosto:  
  
 HIDDEN_NODE_RATIO * SQRT (Totale neuroni di input \* Totale neuroni di output)  
  
 Il valore predefinito è 4,0.  
  
 HOLDOUT_PERCENTAGE  
 Specifica la percentuale di case all'interno dei dati di training utilizzata per calcolare l'errore dei dati di controllo nell'ambito dei criteri di interruzione durante l'esecuzione del training del modello di data mining.  
  
 Il valore predefinito è 30.  
  
 HOLDOUT_SEED  
 Specifica un numero utilizzato come valore di inizializzazione per il generatore pseudocasuale quando l'algoritmo determina in modo casuale i dati di controllo. Se questo parametro è impostato su 0, l'algoritmo genera il valore di inizializzazione in base al nome del modello di data mining, per garantire che il contenuto del modello rimanga invariato durante la rielaborazione.  
  
 Il valore predefinito è 0.  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 Determina il numero massimo di attributi di input che è possibile fornire all'algoritmo prima di utilizzare la caratteristica di selezione degli attributi. Se si imposta il valore su 0, la caratteristica di selezione degli attributi viene disabilitata per gli attributi di input.  
  
 Il valore predefinito è 255.  
  
 MAXIMUM_OUTPUT_ATTRIBUTES  
 Determina il numero massimo di attributi di output che è possibile fornire all'algoritmo prima di utilizzare la caratteristica di selezione degli attributi. Se si imposta il valore su 0, la caratteristica di selezione degli attributi viene disabilitata per gli attributi di output.  
  
 Il valore predefinito è 255.  
  
 MAXIMUM_STATES  
 Specifica il numero massimo di stati discreti per attributo supportato dall'algoritmo. Se il numero di stati per un attributo specifico è maggiore del numero specificato per questo parametro, l'algoritmo utilizza gli stati più frequenti per tale attributo e considera gli stati rimanenti come mancanti.  
  
 Il valore predefinito è 100.  
  
 SAMPLE_SIZE  
 Specifica il numero di case da utilizzare per eseguire il training del modello. L'algoritmo utilizza il valore minore tra questo numero e la percentuale del numero totale di case non inclusi nei dati di controllo specificata dal parametro HOLDOUT_PERCENTAGE.  
  
 In altre parole, se il parametro HOLDOUT_PERCENTAGE è impostato su 30, l'algoritmo utilizzerà il valore di questo parametro o un valore uguale al 70% del numero totale di case, a seconda del valore minore.  
  
 Il valore predefinito è 10000.  
  
### <a name="modeling-flags"></a>Flag di modellazione  
 Di seguito sono indicati i flag di modellazione che è possibile utilizzare con l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network.  
  
 NOT NULL  
 Indica che la colonna non può contenere un valore Null. Se Analysis Services rileva un valore Null durante il training del modello, viene generato un errore.  
  
 Si applica alle colonne della struttura di data mining.  
  
 MODEL_EXISTENCE_ONLY  
 Indica che per il modello si deve considerare solo se un valore di attributo esiste oppure manca. Non è importante il valore esatto.  
  
 Si applica alle colonne del modello di data mining.  
  
### <a name="distribution-flags"></a>Flag di distribuzione  
 Di seguito sono indicati i flag di distribuzione il cui utilizzo è supportato con l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network. I flag sono utilizzati solo come hint per il modello. Se l'algoritmo rileva una distribuzione diversa, verrà utilizzata la distribuzione rilevata, non la distribuzione fornita nell'hint.  
  
 Normale  
 Indica che valori all'interno della colonna devono essere trattati come se rappresentassero la distribuzione normale o di Gauss.  
  
 Uniforme  
 Indica che valori all'interno della colonna devono essere trattati come se fossero distribuiti uniformemente, ovvero la probabilità di qualsiasi valore è approssimativamente uguale ed è una funzione del numero complessivo di valori.  
  
 Logaritmica normale  
 Indica che valori all'interno della colonna devono essere trattati come se fossero distribuiti in base alla curva di *logaritmo normale* , ovvero il logaritmo dei valori è distribuito in modo normale.  
  
## <a name="requirements"></a>Requisiti  
 Un modello di rete neurale deve contenere almeno una colonna di input e una colonna di output.  
  
### <a name="input-and-predictable-columns"></a>Colonne di input e stimabili  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network supporta le colonne di input e le colonne stimabili specifiche riportate nella tabella seguente.  
  
|Colonna|Tipi di contenuto|  
|------------|-------------------|  
|Attributo di input|Continuous, Cyclical, Discrete, Discretized, Key, Table e Ordered|  
|Attributo stimabile|Continuous, Cyclical, Discrete, Discretized e Ordered|  
  
> [!NOTE]  
>  Sono supportati i tipi di contenuto Cyclical e Ordered ma l'algoritmo li considera come valori discreti e non esegue un'elaborazione speciale.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Neural Network](microsoft-neural-network-algorithm.md)   
 [Contenuto del modello di data mining per i modelli di rete neurale &#40;Analysis Services-Data mining&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Esempi di query sul modello di rete neurale](neural-network-model-query-examples.md)  
  
  
