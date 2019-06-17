---
title: Riferimento tecnico algoritmo Microsoft Decision Trees | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_INPUT_ATTRIBUTES parameter
- SPLIT_METHOD parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- FORCED_REGRESSOR parameter
- decision tree algorithms [Analysis Services]
- decision trees [Analysis Services]
- COMPLEXITY_PENALTY parameter
- SCORE_METHOD parameter
ms.assetid: 1e9f7969-0aa6-465a-b3ea-57b8d1c7a1fd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8b52319eaa9af7305c2d3044f3e19762437fff62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084020"
---
# <a name="microsoft-decision-trees-algorithm-technical-reference"></a>Guida di riferimento tecnico per l'algoritmo Microsoft Decision Trees
  L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees è un algoritmo ibrido che incorpora diversi metodi per la creazione di un albero e supporta più attività analitiche, tra le quali sono incluse la regressione, la classificazione e l'associazione. Tale algoritmo supporta la modellazione di attributi discreti e continui.  
  
 In questo argomento viene illustrata l'implementazione dell'algoritmo, viene mostrato come personalizzarne il comportamento in base alle diverse attività e vengono forniti collegamenti a ulteriori informazioni sull'esecuzione di query sui modelli di albero delle decisioni.  
  
## <a name="implementation-of-the-decision-trees-algorithm"></a>Implementazione dell'algoritmo Decision Trees  
 L'algoritmo Microsoft Decision Trees applica l'approccio Bayes ai modelli di interazione causale apprendimento ottenendo le distribuzioni posteriori approssimative per i modelli. Per una spiegazione dettagliata di questo approccio, vedere il white paper nel sito Microsoft Research relativo alle [informazioni su struttura e parametri](https://go.microsoft.com/fwlink/?LinkId=237640&clcid=0x409).  
  
 La metodologia di valutazione del valore informativo delle *conoscenze precedenti* necessarie per l'apprendimento si basa sul presupposto dell' *equivalenza di probabilità*. Questo presupposto indica che i dati non devono permettere la discriminazione delle strutture di rete che altrimenti rappresenterebbero le stesse asserzioni dell'indipendenza condizionale. Si presuppone che per ogni case sia presente una singola rete Bayes con probabilità a priori, cui è associata una sola misura di confidenza.  
  
 Utilizzando queste reti con probabilità a priori, l'algoritmo calcola quindi le *probabilità a posteriori* relative delle strutture di rete a partire dai dati di training correnti e identifica le strutture di rete con le probabilità a posteriori più elevate.  
  
 L'algoritmo Microsoft Decision Trees utilizza diversi metodi per calcolare l'albero ideale. Il metodo utilizzato dipende dal tipo di attività, ovvero regressione lineare, classificazione o analisi di associazione. Un solo modello può contenere più alberi per i diversi attributi stimabili. Ogni albero può inoltre contenere più rami, a seconda del numero di attributi e valori presenti nei dati. La forma e la profondità dell'albero incorporato in un determinato modello dipendono dal metodo di valutazione e dagli altri parametri utilizzati. Le modifiche apportate ai parametri possono influire anche sul punto in cui i nodi si dividono.  
  
### <a name="building-the-tree"></a>Compilazione dell'albero  
 Quando l'algoritmo Microsoft Decision Trees crea il set dei possibili valori di input, esegue la *feature selection* per identificare gli attributi e i valori che forniscono il maggior numero di informazioni ignorando i valori che sono molto rari. L'algoritmo inoltre inserisce i valori in *contenitori*per crearne raggruppamenti che possano essere elaborati come singole unità al fine di ottimizzare le prestazioni.  
  
 La compilazione di un albero avviene mediante la definizione delle correlazioni tra un input e il risultato di destinazione. Dopo aver correlato tutti gli attributi, l'algoritmo identifica l'attributo specifico che separa i risultati in modo più netto. Il punto di separazione ideale viene misurato mediante un'equazione che calcola l'Information Gain. L'attributo che presenta il miglior punteggio in termini di Information Gain viene utilizzato per dividere i case in subset che vengono quindi analizzati in modo ricorsivo dallo stesso processo fino a quando non sia possibile suddividere ulteriormente l'albero.  
  
 L'equazione esatta utilizzata per valutare l'Information Gain dipende dai parametri impostati quando è stato creato l'algoritmo, dal tipo di dati della colonna stimabile e dal tipo di dati dell'input.  
  
### <a name="discrete-and-continuous-inputs"></a>Input discreti e continui  
 Quando sia l'attributo stimabile sia gli input sono discreti, il conteggio dei risultati per input implica la creazione di una matrice e la generazione di punteggi per ogni cella della matrice.  
  
 Quando invece l'attributo stimabile è discreto e gli input sono continui, l'input delle colonne continue viene discretizzato automaticamente. È possibile accettare l'impostazione predefinita e impostare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sulla ricerca automatica del numero ottimale di contenitori o controllare il modo in cui gli input continui vengono discretizzati impostando le proprietà <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> e <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> . Per altre informazioni, vedere [Modificare la discretizzazione di una colonna in un modello di data mining](change-the-discretization-of-a-column-in-a-mining-model.md).  
  
 Per gli attributi continui, l'algoritmo utilizza una regressione lineare per determinare le divisioni dell'albero delle decisioni.  
  
 Quando l'attributo stimabile è un tipo di dati numerico continuo, la funzionalità di selezione degli attributi viene applicata anche agli output in modo da ridurre il numero possibile di risultati e da velocizzare la compilazione del modello. È possibile modificare la soglia per la funzionalità di selezione degli attributi e di conseguenza aumentare o ridurre il numero di valori possibili impostando il parametro MAXIMUM_OUTPUT_ATTRIBUTES.  
  
 Per una spiegazione più dettagliata sul modo in cui [!INCLUDE[msCoName](../../includes/msconame-md.md)] funzionamento dell'algoritmo Decision Trees con colonne stimabili discrete, vedere [Learning Bayesian Networks: La combinazione di conoscenza e dati statistici](https://go.microsoft.com/fwlink/?LinkId=45963). Per altre informazioni sul funzionamento dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees nel caso di colonne stimabili continue, vedere l'appendice dell'articolo [Autoregressive Tree Models for Time-Series Analysis](https://go.microsoft.com/fwlink/?LinkId=45966)(Modelli di albero autoregressivi per l'analisi delle serie temporali).  
  
### <a name="scoring-methods-and-feature-selection"></a>Metodi di valutazione e caratteristica di selezione degli attributi  
 L'algoritmo Microsoft Decision Trees offre tre formule per valutare l'information gain: Entropia di Shannon, la rete Bayes con K2 precedenti e rete Bayes con a priori a distribuzione Dirichlet uniforme. Tutti e tre i metodi sono consolidati nel campo del data mining. È consigliabile provare a utilizzare diversi parametri e metodi di valutazione in modo da individuare quelli che forniscono i migliori risultati. Per ulteriori informazioni sui metodi di valutazione, vedere [Feature Selection](../../sql-server/install/feature-selection.md).  
  
 Tutti gli algoritmi di data mining di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usano automaticamente la selezione di funzionalità per migliorare l'analisi e ridurre il carico di elaborazione. Il metodo utilizzato per la funzionalità di selezione degli attributi dipende dall'algoritmo impiegato per la compilazione del modello. I parametri dell'algoritmo che controllano la caratteristica di selezione degli attributi per un modello di albero delle decisioni sono MAXIMUM_INPUT_ATTRIBUTES e MAXIMUM_OUTPUT.  
  
|Algoritmo|Metodo di analisi|Commenti|  
|---------------|------------------------|--------------|  
|Decision Trees|Punteggio di interesse<br /><br /> Entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Se esistono colonne contenenti valori continui non binari, viene utilizzato il punteggio di interesse per tutte le colonne, per assicurare coerenza. In caso contrario, viene utilizzato il metodo predefinito o specificato.|  
|Linear Regression|Punteggio di interesse|L'algoritmo Linear Regression può utilizzare solo il punteggio di interesse, perché supporta solo colonne continue.|  
  
### <a name="scalability-and-performance"></a>Scalabilità e prestazioni  
 La classificazione è un'importante strategia di data mining. In genere, la quantità di informazioni necessaria a classificare i case cresce in modo direttamente proporzionale al numero di record di input. Ciò limita le dimensioni dei dati classificabili. L'algoritmo Microsoft Decision Trees utilizza i metodi seguenti per risolvere questi problemi, migliorare le prestazioni ed eliminare le restrizioni relative alla memoria:  
  
-   Funzionalità di selezione degli attributi per ottimizzare la scelta degli attributi.  
  
-   Valutazione con il metodo Bayes per controllare l'aumento delle dimensioni dell'albero.  
  
-   Ottimizzazione della creazione di contenitori per gli attributi continui.  
  
-   Raggruppamento dinamico dei valori di input per individuare i valori più importanti.  
  
 L'algoritmo Microsoft Decision Trees è veloce e scalabile ed è stato progettato per essere facilmente eseguito in parallelo, ovvero per fare in modo che tutti i processori interagiscano per compilare un singolo modello coerente. La combinazione di queste caratteristiche rende il classificatore dell'albero delle decisioni uno strumento ideale per il data mining.  
  
 Se i vincoli relativi alle prestazioni sono rigidi, è possibile migliorare il tempo di elaborazione durante il training di un modello di albero delle decisioni tramite i metodi seguenti. In tal caso, è tuttavia necessario essere consapevoli del fatto che l'eliminazione degli attributi finalizzata al miglioramento delle prestazioni determinerà la modifica dei risultati del modello rendendoli meno rappresentativi della popolazione totale.  
  
-   Aumentare il valore del parametro COMPLEXITY_PENALTY per limitare l'aumento delle dimensioni dell'albero.  
  
-   Limitare il numero di elementi nei modelli di associazione per compilare un numero limitato di alberi.  
  
-   Aumentare il valore del parametro MINIMUM_SUPPORT per evitare l'overfitting.  
  
-   Limitare il numero di valori discreti di qualsiasi attributo a 10 o un numero inferiore. È possibile provare a raggruppare i valori in modi e modelli diversi.  
  
    > [!NOTE]  
    >  È possibile utilizzare gli strumenti di esplorazione dei dati disponibili in  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] per visualizzare la distribuzione di valori nei dati e raggruppare i valori in modo appropriato prima di dare inizio al data mining. Per altre informazioni, vedere [Attività Profiling dati e visualizzatore](../../integration-services/control-flow/data-profiling-task-and-viewer.md). È inoltre possibile usare i [componenti aggiuntivi Data Mining per Excel 2007](https://www.microsoft.com/downloads/details.aspx?FamilyID=7C76E8DF-8674-4C3B-A99B-55B17F3C4C51)per esplorare, raggruppare e rietichettare i dati in Microsoft Excel.  
  
## <a name="customizing-the-decision-trees-algorithm"></a>Personalizzazione dell'algoritmo Decision Trees  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees supporta parametri che influiscono sulle prestazioni e sull'accuratezza del modello di data mining risultante. È anche possibile impostare flag di modellazione nelle colonne del modello o della struttura di data mining per controllare la modalità di elaborazione dei dati.  
  
> [!NOTE]  
>  L'algoritmo Microsoft Decision Trees è disponibile in tutte le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tuttavia alcuni parametri avanzati per la personalizzazione del comportamento dell'algoritmo Microsoft Decision Trees sono disponibili per l'uso solo in versioni specifiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473).  
  
### <a name="setting-algorithm-parameters"></a>Impostazione dei parametri dell'algoritmo  
 Nella tabella seguente vengono descritti i parametri che è possibile utilizzare con l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees.  
  
 *COMPLEXITY_PENALTY*  
 Controlla la crescita dell'albero delle decisioni. Un valore basso comporta l'aumento del numero di divisioni, mentre un valore alto comporta la diminuzione del numero di divisioni. Il valore predefinito è basato sul numero di attributi per un modello specifico, come descritto nell'elenco seguente:  
  
-   Per un numero di attributi compreso tra 1 e 9, il valore predefinito è 0,5.  
  
-   Per un numero di attributi compreso tra 10 e 99, il valore predefinito è 0,9.  
  
-   Per un numero di attributi maggiore o uguale a 100, il valore predefinito è 0,99.  
  
 *FORCE_REGRESSOR*  
 Forza l'algoritmo a utilizzare le colonne specificate come regressori, indipendentemente dall'importanza delle colonne calcolate dall'algoritmo. Questo parametro viene utilizzato solo per gli alberi delle decisioni che stimano un attributo continuo.  
  
> [!NOTE]  
>  Impostando questo parametro, l'algoritmo viene forzato a tentare di utilizzare l'attributo come regressore. L'eventualità che l'attributo venga realmente utilizzato come regressore nel modello finale dipende invece dai risultati dell'analisi. Per individuare le colonne utilizzate come regressori, è possibile eseguire query sul contenuto del modello.  
  
 [Disponibile solo in alcune edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ]  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 Definisce il numero di attributi di input che l'algoritmo è in grado di gestire prima di richiamare la funzionalità di selezione degli attributi.  
  
 Il valore predefinito è 255.  
  
 Impostare questo valore su 0 per disabilitare la funzionalità di selezione degli attributi.  
  
 [Disponibile solo in alcune edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 Definisce il numero di attributi di output che l'algoritmo è in grado di gestire prima di richiamare la funzionalità di selezione degli attributi.  
  
 Il valore predefinito è 255.  
  
 Impostare questo valore su 0 per disabilitare la funzionalità di selezione degli attributi.  
  
 [Disponibile solo in alcune edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
  
 *MINIMUM_SUPPORT*  
 Determina il numero minimo di case foglia necessari per generare una divisione nell'albero delle decisioni.  
  
 Il valore predefinito è 10.  
  
 Può essere necessario aumentare il valore se il set di dati è di dimensioni molto elevate per evitare un overtraining.  
  
 *SCORE_METHOD*  
 Determina il metodo utilizzato per calcolare il punteggio di divisione. Sono disponibili le opzioni seguenti:  
  
|ID|Nome|  
|--------|----------|  
|1|Entropia|  
|3|Bayes con probabilità a priori K2|  
|4|Equivalente Bayes Dirichlet (BDE, Bayesian Dirichlet Equivalent) con probabilità a priori a distribuzione uniforme<br /><br /> (predefinito)|  
  
 Il valore predefinito è 4 o BDE.  
  
 Per una spiegazione relativa ai metodi di valutazione, vedere [Feature Selection](../../sql-server/install/feature-selection.md).  
  
 *SPLIT_METHOD*  
 Determina il metodo utilizzato per la divisione del nodo. Sono disponibili le opzioni seguenti:  
  
|ID|Nome|  
|--------|----------|  
|1|**Binario:** Indica che indipendentemente dal numero effettivo dei valori dell'attributo, l'albero deve essere suddiviso in due rami.|  
|2|**Completamento:** Indica che l'albero possono essere create tante divisioni quanti sono i valori di attributo.|  
|3|**Both:** Specifica che Analysis Services consente di scegliere se usare una divisione binaria o completa per ottenere risultati migliori.|  
  
 Il valore predefinito è 3.  
  
### <a name="modeling-flags"></a>Flag di modellazione  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees supporta i flag di modellazione seguenti. Quando si crea la struttura o il modello di data mining, i flag di modellazione vengono definiti per specificare la modalità di gestione dei valori presenti in ogni colonna durante l'analisi. Per altre informazioni, vedere [Flag di modellazione &#40;data mining&#41;](modeling-flags-data-mining.md).  
  
|Flag di modellazione|Descrizione|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|Indica che la colonna verrà considerata come se presentasse due stati possibili: `Missing` e `Existing`. Un valore Null è un valore mancante.<br /><br /> Si applica alle colonne del modello di data mining.|  
|NOT NULL|Indica che la colonna non può contenere un valore Null. Se Analysis Services rileva un valore Null durante il training del modello, viene generato un errore.<br /><br /> Si applica alle colonne della struttura di data mining.|  
  
### <a name="regressors-in-decision-tree-models"></a>Regressori nei modelli di albero delle decisioni  
 Anche se non si utilizza l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression, qualsiasi modello di albero delle decisioni con input e output numerici continui può contenere nodi che rappresentano una regressione su un attributo continuo.  
  
 Non è necessario specificare che una colonna di dati numerici continui rappresenta un regressore. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees consentirà di utilizzare automaticamente la colonna come potenziale regressore e di suddividere il set di dati in aree con modelli significativi anche se non si imposta il flag REGRESSOR nella colonna.  
  
 È invece possibile utilizzare il parametro FORCE_REGRESSOR per assicurarsi che l'algoritmo consenta l'utilizzo di un determinato regressore. Questo parametro può essere utilizzato solo con gli algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees e [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression. Quando si imposta il flag di modellazione, l'algoritmo tenta di trovare equazioni di regressione nel formato un * C1 + b\*C2 +... per adattare i modelli nei nodi dell'albero. Viene calcolata la somma dei residui e, se la deviazione è eccessiva, nell'albero viene forzata una divisione.  
  
 Se, ad esempio, si stima il comportamento di acquisto dei clienti utilizzando **Income** come attributo ed è stato impostato il flag di modellazione REGRESSOR nella colonna, l'algoritmo tenta innanzitutto di adattare i valori **Income** utilizzando una formula di regressione standard. Se la deviazione è eccessiva, la formula di regressione viene abbandonata e l'albero viene diviso in base a un altro attributo. L'algoritmo Decision Trees tenta quindi di adattare un regressore per il reddito in ognuno dei rami dopo la divisione.  
  
## <a name="requirements"></a>Requisiti  
 Un modello di albero delle decisioni deve contenere una colonna chiave, le colonne di input e almeno una colonna stimabile.  
  
### <a name="input-and-predictable-columns"></a>Colonne di input e stimabili  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees supporta le colonne di input e le colonne stimabili specifiche riportate nella tabella seguente. Per altre informazioni sul significato dei tipi di contenuto usati in un modello di data mining, vedere [Tipi di contenuto &#40;Data mining&#41;](content-types-data-mining.md).  
  
|colonna|Tipi di contenuto|  
|------------|-------------------|  
|Attributo di input|Continuous, Cyclical, Discrete, Discretized, Key, Ordered, Table|  
|Attributo stimabile|Continuous, Cyclical, Discrete, Discretized, Ordered, Table|  
  
> [!NOTE]  
>  Sono supportati i tipi di contenuto Cyclical e Ordered ma l'algoritmo li considera come valori discreti e non esegue un'elaborazione speciale.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Decision Trees](microsoft-decision-trees-algorithm.md)   
 [Esempi di query sul modello di alberi delle decisioni](decision-trees-model-query-examples.md)   
 [Contenuto dei modelli di data mining per i modelli di albero delle decisioni &#40;Analysis Services - Data mining&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
