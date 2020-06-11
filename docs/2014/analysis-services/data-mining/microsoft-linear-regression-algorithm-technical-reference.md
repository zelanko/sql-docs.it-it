---
title: Riferimento tecnico per l'algoritmo Microsoft Linear regressione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- AUTO_DETECT_PERIODICITY parameter
- linear regression algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 7807b5ff-8e0d-418d-a05b-b1a9644536d2
author: minewiskan
ms.author: owend
ms.openlocfilehash: 20acb57a4c2ddb60d2daefc6733ac7ef52310f3c
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522007"
---
# <a name="microsoft-linear-regression-algorithm-technical-reference"></a>Riferimento tecnico per l'algoritmo Microsoft Linear Regression
  L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression è una versione speciale dell'algoritmo Microsoft Decision Trees ottimizzata per la modellazione delle coppie di attributi continui. In questo argomento viene illustrata l'implementazione dell'algoritmo, viene mostrato come personalizzarne il comportamento e vengono forniti collegamenti a ulteriori informazioni sull'esecuzione di query sui modelli.  
  
## <a name="implementation-of-the-linear-regression-algorithm"></a>Implementazione dell'algoritmo Linear Regression  
 L'algoritmo Microsoft Decision Trees può essere utilizzato per diverse attività, quali regressione lineare, classificazione e analisi di associazione. Per implementare questo algoritmo allo scopo di eseguire la regressione lineare, i parametri dell'algoritmo vengono controllati per limitare l'aumento delle dimensioni dell'albero e mantenere tutti i dati del modello in un solo nodo. In altre parole, anche se la regressione lineare è basata su un albero delle decisioni, l'albero contiene una sola radice e nessun ramo, ovvero tutti i dati si trovano nel nodo radice.  
  
 A tale scopo, il parametro *MINIMUM_LEAF_CASES* dell'algoritmo viene impostato su un valore uguale a o maggiore del numero totale di case utilizzati dall'algoritmo per il training del modello di data mining. Se si imposta il parametro in questo modo, l'algoritmo non crea mai una divisione ed esegue pertanto una regressione lineare.  
  
 Il formato dell'equazione che rappresenta la linea di regressione, nota come equazione di regressione, è generalmente y = ax + b. La variabile Y rappresenta la variabile di output, X rappresenta la variabile di input mentre a e b sono coefficienti modificabili. È possibile recuperare i coefficienti, le intercette e altre informazioni sulla formula di regressione eseguendo una query sul modello di data mining completato. Per altre informazioni, vedere [Esempi di query sul modello di regressione lineare](linear-regression-model-query-examples.md).  
  
### <a name="scoring-methods-and-feature-selection"></a>Metodi di valutazione e caratteristica di selezione degli attributi  
 Tutti gli algoritmi di data mining di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usano automaticamente la selezione di funzionalità per migliorare l'analisi e ridurre il carico di elaborazione. Il metodo utilizzato per la caratteristica di selezione degli attributi nella regressione lineare è il punteggio di interesse, perché il modello supporta solo colonne continue. Nella tabella seguente viene mostrata per riferimento la differenza nella caratteristica di selezione degli attributi tra l'algoritmo Linear Regression e l'algoritmo Decision Trees.  
  
|Algoritmo|Metodo di analisi|Commenti|  
|---------------|------------------------|--------------|  
|Linear Regression|Punteggio di interesse|Valore predefinito.<br /><br /> Gli altri metodi relativi alla caratteristica di selezione degli attributi disponibili con l'algoritmo Decision Trees si applicano solo alle variabili discrete e non sono pertanto validi per i modelli di regressione lineare.|  
|Decision Trees|Punteggio di interesse<br /><br /> Entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Se esistono colonne contenenti valori continui non binari, viene utilizzato il punteggio di interesse per tutte le colonne, per assicurare coerenza. In caso contrario, viene utilizzato il metodo predefinito o specificato.|  
  
 I parametri dell'algoritmo che controllano la caratteristica di selezione degli attributi per un modello di albero delle decisioni sono MAXIMUM_INPUT_ATTRIBUTES e MAXIMUM_OUTPUT.  
  
## <a name="customizing-the-linear-regression-algorithm"></a>Personalizzazione dell'algoritmo Linear Regression  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression supporta vari parametri che influiscono sul comportamento, sulle prestazioni e sull'accuratezza del modello di data mining risultante. È anche possibile impostare flag di modellazione nelle colonne del modello o della struttura di data mining per controllare la modalità di elaborazione dei dati.  
  
### <a name="setting-algorithm-parameters"></a>Impostazione dei parametri dell'algoritmo  
 Nella tabella seguente sono elencati i parametri forniti per l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*MAXIMUM_INPUT_ATTRIBUTES*|Definisce il numero di attributi di input che l'algoritmo è in grado di gestire prima di richiamare la funzionalità di selezione degli attributi. Impostare questo valore su 0 per disabilitare la funzionalità di selezione degli attributi.<br /><br /> Il valore predefinito è 255.|  
|*MAXIMUM_OUTPUT_ATTRIBUTES*|Definisce il numero di attributi di output che l'algoritmo è in grado di gestire prima di richiamare la funzionalità di selezione degli attributi. Impostare questo valore su 0 per disabilitare la funzionalità di selezione degli attributi.<br /><br /> Il valore predefinito è 255.|  
|*FORCE_REGRESSOR*|Forza l'utilizzo, da parte dell'algoritmo, delle colonne indicate come regressori, indipendentemente dall'importanza delle colonne calcolata dall'algoritmo.|  
  
### <a name="modeling-flags"></a>Flag di modellazione  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression supporta i flag di modellazione indicati di seguito. Quando si crea la struttura o il modello di data mining, i flag di modellazione vengono definiti per specificare la modalità di gestione dei valori presenti in ogni colonna durante l'analisi. Per altre informazioni, vedere [Flag di modellazione &#40;data mining&#41;](modeling-flags-data-mining.md).  
  
|Flag di modellazione|Descrizione|  
|-------------------|-----------------|  
|NOT NULL|Indica che la colonna non può contenere un valore Null. Se Analysis Services rileva un valore Null durante il training del modello, viene generato un errore.<br /><br /> Si applica alle colonne della struttura di data mining.|  
|REGRESSOR|Indica che la colonna contiene valori numerici continui che devono essere considerati come potenziali variabili indipendenti durante l'analisi.<br /><br /> Nota: l'applicazione di un flag REGRESSOR a una colonna non ne garantisce l'uso come regressore nel modello finale.<br /><br /> Si applica alle colonne del modello di data mining.|  
  
### <a name="regressors-in-linear-regression-models"></a>Regressori nei modelli di regressione lineare  
 I modelli di regressione lineare si basano sull'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees. Tuttavia, anche se non si utilizza l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression, qualsiasi modello di albero delle decisioni può contenere un albero o i nodi che rappresentano una regressione su un attributo continuo.  
  
 Non è necessario specificare che una colonna continua rappresenta un regressore. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees suddividerà il set di dati in aree con modelli significativi anche se non si imposta il flag REGRESSOR nella colonna. La differenza è che quando si imposta il flag di modellazione, l'algoritmo tenterà di trovare equazioni di regressione nel formato a * C1 + b \* C2 +... per adattare i modelli nei nodi dell'albero. Viene calcolata la somma dei residui e, se la deviazione è eccessiva, nell'albero viene forzata una divisione.  
  
 Ad esempio, se si stima il comportamento di acquisto dei clienti usando **Reddito** come attributo e si imposta il flag di modellazione REGRESSOR nella colonna, per prima cosa l'algoritmo tenterà di adattare i valori **Reddito** usando una formula di regressione standard. Se la deviazione è eccessiva, la formula di regressione viene abbandonata e l'albero viene diviso in base a un altro attributo. L'algoritmo Decision Trees tenta quindi di adattare un regressore per il reddito in ognuno dei rami dopo la divisione.  
  
 È possibile utilizzare il parametro FORCED_REGRESSOR per assicurarsi che l'algoritmo impieghi un determinato regressore. Questo parametro può essere utilizzato con gli algoritmi Microsoft Decision Trees e Microsoft Linear Regression.  
  
## <a name="requirements"></a>Requisiti  
 Un modello di regressione lineare deve contenere una colonna chiave, le colonne di input e almeno una colonna stimabile.  
  
### <a name="input-and-predictable-columns"></a>Colonne di input e stimabili  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression supporta le colonne di input e le colonne stimabili specifiche riportate nella tabella seguente. Per altre informazioni sul significato dei tipi di contenuto usati in un modello di data mining, vedere [Tipi di contenuto &#40;Data mining&#41;](content-types-data-mining.md).  
  
|Colonna|Tipi di contenuto|  
|------------|-------------------|  
|Attributo di input|Continuous, Cyclical, Key, Table e Ordered|  
|Attributo stimabile|Continuous, Cyclical e Ordered|  
  
> [!NOTE]  
>  I tipi di contenuto `Cyclical` e `Ordered` sono supportati, ma l'algoritmo li considera come valori discreti e non esegue un'elaborazione speciale.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Linear regressione](microsoft-linear-regression-algorithm.md)   
 [Esempi di query sul modello di regressione lineare](linear-regression-model-query-examples.md)   
 [Contenuto dei modelli di data mining per i modelli di regressione lineare &#40;Analysis Services - Data mining&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
