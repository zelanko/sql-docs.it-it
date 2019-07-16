---
title: Funzionalità di selezione (Data Mining) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a93e503978779e56250ddf190c61b1b2411050b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68183276"
---
# <a name="feature-selection-data-mining"></a>Selezione delle caratteristiche (Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La *selezione delle caratteristiche* è una parte importante del Machine Learning. La selezione delle caratteristiche si riferisce al processo di riduzione degli input per l'elaborazione e l'analisi o di individuazione degli input più significativi. Un termine correlato, *progettazione delle caratteristiche* (o *estrazione delle caratteristiche*), si riferisce al processo di estrazione di informazioni o caratteristiche utili dai dati esistenti.  
  
## <a name="why-do-feature-selection"></a>Perché eseguire la selezione delle caratteristiche?  
 La selezione delle caratteristiche è fondamentale per la creazione di un modello funzionale per diversi motivi. Uno è che la selezione delle caratteristiche implica un certo livello di *riduzione della cardinalità*, per imporre un limite al numero di attributi che possono essere considerati durante la creazione di un modello. I dati contengono quasi sempre più informazioni di quelle necessarie per creare il modello oppure il tipo di informazioni sbagliate. Ad esempio, in un set di dati potrebbero essere contenute 500 colonne in cui vengono descritte le caratteristiche dei clienti. Tuttavia, se i dati di alcune colonne sono di tipo sparse, non sarebbe molto vantaggioso aggiungerli al modello e, se alcune colonne sono duplicate tra loro, l'uso di entrambe le colonne potrebbe influire negativamente sul modello.  
  
 Non solo la selezione delle caratteristiche migliora la qualità del modello, ma rende anche più efficiente il processo di modellazione. Se si usano colonne non necessarie durante la creazione del modello, la quantità di CPU e memoria necessaria per il processo di training sarà maggiore, così come lo spazio di archiviazione richiesto per il modello completato. Anche nei casi in cui le risorse non rappresentano un problema, è comunque preferibile eseguire la selezione delle caratteristiche e identificare le colonne più appropriate, perché le colonne non necessarie possono peggiorare la qualità del modello in diversi modi:  
  
-   I dati poco significativi o ridondanti rendono più difficile individuare modelli significativi.  
  
-   Se il set di dati è di dimensioni elevate, la maggior parte degli algoritmi di data mining richiede un set di dati di training di dimensioni molto maggiori.  
  
 Durante il processo di selezione delle caratteristiche, l'analista o lo strumento o l'algoritmo di modellazione seleziona o elimina attivamente gli attributi in base alla loro utilità per l'analisi.  Gli analisti possono eseguire la progettazione delle caratteristiche per aggiungere caratteristiche e rimuovere o modificare i dati esistenti, mentre l'algoritmo di Machine Learning in genere assegna punteggi alle colonne e convalida la loro utilità nel modello.  
  
 ![Processo di progettazione e selezione di funzioni](../../analysis-services/data-mining/media/ssdm-featureselectionprocess.png "processo di progettazione e selezione di funzioni")  
  
 In breve, la selezione delle caratteristiche consente di risolvere due problemi: la presenza di una quantità eccessiva di dati di scarso valore o di una quantità ridotta di dati di valore elevato. L'obiettivo della selezione delle caratteristiche deve essere identificare il numero minimo di colonne dell'origine dati che sono significative per la creazione di un modello.  
  
## <a name="how-feature-selection-works-in-sql-server-data-mining"></a>Funzionamento della selezione delle caratteristiche in Data Mining di SQL Server  
 La selezione delle caratteristiche viene sempre eseguita prima del training del modello. Con alcuni algoritmi, le tecniche di selezione delle caratteristiche sono "predefinite", in modo da escludere le colonne irrilevanti e individuare automaticamente le migliori caratteristiche. Ogni algoritmo dispone di un proprio set di tecniche predefinite per applicare in modo intelligente la riduzione delle caratteristiche.  Tuttavia, è anche possibile impostare manualmente i parametri per influire sul comportamento della selezione delle caratteristiche.  
  
 Durante la selezione automatica delle caratteristiche, viene calcolato un punteggio per ogni attributo e vengono selezionati solo gli attributi con i punteggi migliori per il modello. Inoltre, è possibile regolare la soglia per i punteggi massimi. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] In Data Mining di SQL Server sono disponibili più metodi per calcolare questi punteggi e il metodo esatto applicato in qualsiasi modello dipende dai fattori seguenti:  
  
-   Algoritmo utilizzato nel modello  
  
-   Tipo di dati dell'attributo  
  
-   Qualsiasi parametro che potrebbe essere stato impostato sul modello  
  
 La selezione delle caratteristiche viene applicata agli input, agli attributi stimabili oppure agli stati di una colonna. Quando il calcolo del punteggio per la selezione delle caratteristiche è terminato, nel processo di compilazione del modello vengono inclusi solo gli attributi e gli stati selezionati dall'algoritmo, che possono essere utilizzati per eventuali stime. Se si sceglie un attributo stimabile che non soddisfa la soglia per la selezione delle caratteristiche, l'attributo può comunque essere utilizzato per le stime, tuttavia queste ultime saranno basate unicamente sulle statistiche globali presenti nel modello.  
  
> [!NOTE]  
>  La selezione delle caratteristiche influisce solo sulle colonne utilizzate nel modello, mentre non ha effetto sull'archiviazione della struttura di data mining. Le colonne rimosse dal modello di data mining sono ancora disponibili nella struttura e i dati delle colonne della struttura di data mining verranno memorizzati nella cache.  
  
### <a name="feature-selection-scores"></a>Punteggi per la selezione delle caratteristiche  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] In Data Mining di SQL Server sono disponibili diversi metodi diffusi e consolidati per il punteggio degli attributi. Lo specifico metodo usato in un particolare algoritmo o set di dati dipende dai tipi di dati e dall'uso delle colonne.  
  
-   Il punteggio di *interesse* viene usato per classificare e ordinare gli attributi in colonne che contengono dati numerici continui non binari.  
  
-   L'*entropia di Shannon* e due punteggi *Bayes* sono disponibili per le colonne contenenti dati discreti e discretizzati. Tuttavia, se nel modello sono contenute colonne continue, il punteggio di interesse verrà utilizzato per valutare tutte le colonne di input e assicurare la coerenza.  
  
#### <a name="interestingness-score"></a>Punteggio di interesse  
 Una caratteristica è interessante se indica informazioni utili. L' *interesse* , tuttavia, può essere misurato in diversi modi.  L'*originalità* potrebbe essere utile nell'individuazione degli outlier, mentre la possibilità di discriminare tra elementi strettamente correlati, ovvero il *peso discriminante*, potrebbe essere più interessante per la classificazione.  
  
 La misura dell'interesse usata in Data Mining di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è *basata sull'entropia*, ovvero gli attributi con distribuzioni casuali hanno un'entropia maggiore e un Information Gain minore. Tali attributi pertanto sono meno interessanti. L'entropia di un determinato attributo viene confrontata con quella di tutti gli altri attributi, come segue:  
  
 Interesse(Attributo) = - (m - Entropia(Attributo)) * (m - Entropia(Attributo))  
  
 Per entropia centrale o m si intende l'entropia dell'intero set di caratteristiche. Sottraendo l'entropia dell'attributo di destinazione dall'entropia centrale, è possibile valutare la quantità di informazioni fornita dall'attributo.  
  
 Questo punteggio viene utilizzato per impostazione predefinita ogni volta che la colonna contiene dati numerici continui non binari.  
  
#### <a name="shannons-entropy"></a>entropia di Shannon  
 L'entropia di Shannon misura l'incertezza di una variabile casuale per un determinato risultato. Ad esempio, l'entropia del lancio di una moneta può essere rappresentata come funzione della probabilità che esca testa.  
  
 In Analysis Services viene utilizzata la formula seguente per il calcolo dell'entropia di Shannon:  
  
 H(X) = -∑ P(xi) log(P(xi))  
  
 Questo metodo di assegnazione dei punteggi è disponibile per gli attributi discreti e discretizzati.  
  
#### <a name="bayesian-with-k2-prior"></a>Bayes con probabilità a priori K2  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] In Data Mining di SQL Server sono disponibili due punteggi per la selezione delle caratteristiche basati su reti Bayes. Una rete Bayes è un grafico *orientato* o *aciclico* di stati e di transizioni tra stati, ossia alcuni stati sono sempre precedenti allo stato corrente, alcuni sono successivi e il grafico non si ripete. Per definizione, le reti Bayes consentono l'utilizzo delle conoscenze precedenti. Tuttavia, la domanda in merito a quali stati precedenti utilizzare nel calcolo delle probabilità degli stati successivi è importante per la progettazione, le prestazioni e l'accuratezza dell'algoritmo.  
  
 L'algoritmo K2 per l'apprendimento di una rete Bayes, sviluppato da Cooper e Herskovits, viene utilizzato spesso nel data mining. È scalabile e consente di analizzare più variabili, ma richiede l'ordinamento delle variabili utilizzate come input. Per altre informazioni, vedere [Learning Bayesian Networks](http://research.microsoft.com/en-us/um/people/heckerman/hgc94uai.pdf) di Chickering, Geiger e Heckerman.  
  
 Questo metodo di assegnazione dei punteggi è disponibile per gli attributi discreti e discretizzati.  
  
#### <a name="bayesian-dirichlet-equivalent-with-uniform-prior"></a>Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme  
 Anche per il punteggio equivalente Bayes Dirichlet (BDE, Bayesian Dirichlet Equivalent) si utilizza l'analisi bayesiana per valutare una rete dato un set di dati. Il metodo di assegnazione dei punteggi BDE, sviluppato da Heckerman, è basato sulla metrica BD sviluppata da Cooper e Herskovits. La distribuzione Dirichlet è una distribuzione multinomiale che descrive la probabilità condizionale di ogni variabile nella rete, oltre a includere molte proprietà utili per l'apprendimento.  
  
 Il metodo equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (BDEU, Bayesian Dirichlet Equivalent with Uniform Prior) presuppone un caso speciale della distribuzione Dirichlet in cui viene utilizzata una costante matematica per creare una distribuzione fissa o uniforme di stati precedenti. Il punteggio BDE presuppone anche un'equivalenza di probabilità, ossia non è possibile prevedere che i dati discriminino strutture equivalenti. In altri termini, se il punteggio di Se A allora B è uguale al punteggio di Se B allora A, non è possibile distinguere le strutture in base ai dati e non è possibile derivare il rapporto di causa ed effetto.  
  
 Per altre informazioni sulle reti Bayes e sull'implementazione di questi metodi di assegnazione dei punteggi, vedere [Learning Bayesian Networks](http://research.microsoft.com/en-us/um/people/heckerman/hgc94uai.pdf).  
  
### <a name="feature-selection-methods-per-algorithm"></a>Metodi di selezione delle caratteristiche per algoritmo  
 Nella tabella seguente sono elencati gli algoritmi che supportano la caratteristica di selezione degli attributi, i metodi utilizzati dall'algoritmo e i parametri impostati per controllare il funzionamento di questa caratteristica:  
  
|Algoritmo|Metodo di analisi|Commenti|  
|---------------|------------------------|--------------|  
|Naive Bayes|Entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Poiché l'algoritmo Microsoft Naive Bayes accetta solo attributi discreti o discretizzati, non può utilizzare il punteggio di interesse.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Naive Bayes](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md).|  
|Decision Trees|Punteggio di interesse<br /><br /> Entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Se esistono colonne contenenti valori continui non binari, viene utilizzato il punteggio di interesse per tutte le colonne, per assicurare coerenza. In caso contrario, viene utilizzato il metodo per implementare la caratteristica di selezione degli attributi predefinito oppure il metodo specificato quando è stato creato il modello.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Guida di riferimento tecnico per l'algoritmo Microsoft Decision Trees](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md).|  
|Neural Network|Punteggio di interesse<br /><br /> Entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Nell'algoritmo Microsoft Neural Network possono essere utilizzati sia i metodi Bayes sia quelli basati sull'entropia, purché nei dati siano contenute colonne continue.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Neural Network](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md).|  
|Logistic Regression|Punteggio di interesse<br /><br /> Entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Sebbene l'algoritmo Microsoft Logistic Regression sia basato sull'algoritmo Microsoft Neural Network, non è possibile personalizzare modelli di regressione logistica per controllare il comportamento della caratteristica di selezione degli attributi. Di conseguenza tale caratteristica viene impostata automaticamente sempre sul metodo più appropriato per l'attributo.<br /><br /> Se tutti gli attributi sono discreti o discretizzati, l'impostazione predefinita è BDEU.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Logistic Regression](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md).|  
|Clustering|Punteggio di interesse|L'algoritmo Microsoft Clustering può utilizzare dati discreti o discretizzati. Tuttavia, perché il punteggio di ogni attributo è calcolato come una distanza e viene rappresentato come un numero continuo, è necessario utilizzare il punteggio di interesse.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Clustering](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md).|  
|Linear Regression|Punteggio di interesse|L'algoritmo Microsoft Linear Regression può utilizzare solo il punteggio di interesse, poiché supporta solo colonne continue.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Linear Regression](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md).|  
|Association Rules<br /><br /> Sequence Clustering|Non usato|La caratteristica di selezione degli attributi non viene richiamata da questi algoritmi.<br /><br /> È tuttavia possibile controllare il comportamento dell'algoritmo e ridurre le dimensioni dei dati di input impostando i valori dei parametri MINIMUM_SUPPORT e MINIMUM_PROBABILIITY.<br /><br /> Per altre informazioni, vedere [Riferimento tecnico per l'algoritmo Microsoft Association Rules](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md) e [Riferimento tecnico per l'algoritmo Microsoft Sequence Clustering](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).|  
|Time Series|Non usato|La selezione delle caratteristiche non si applica ai modelli Time Series.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Time Series](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).|  
  
## <a name="feature-selection-parameters"></a>Parametri della selezione delle caratteristiche  
 Negli algoritmi che supportano la selezione delle caratteristiche è possibile controllare quando tale selezione è abilitata tramite i parametri riportati di seguito. In ogni algoritmo è disponibile un valore predefinito per il numero di input consentiti; tuttavia è possibile eseguire l'override di questo valore predefinito e specificare il numero di attributi. In questa sezione sono elencati i parametri forniti per la gestione della selezione delle caratteristiche.  
  
#### <a name="maximuminputattributes"></a>MAXIMUM_INPUT_ATTRIBUTES  
 Se in un modello è contenuto un numero di colonne maggiore del numero specificato nel parametro *MAXIMUM_INPUT_ATTRIBUTES* , vengono ignorate le colonne che in base all'algoritmo non risultano di interesse.  
  
#### <a name="maximumoutputattributes"></a>MAXIMUM_OUTPUT_ATTRIBUTES  
 In modo analogo, se un modello contiene un numero di colonne stimabili maggiore del numero specificato nel parametro *MAXIMUM_OUTPUT_ATTRIBUTES* , vengono ignorate le colonne che in base all'algoritmo non risultano di interesse.  
  
#### <a name="maximumstates"></a>MAXIMUM_STATES  
 Se un modello contiene un numero di case maggiore del numero specificato nel parametro *MAXIMUM_STATES* , gli stati usati meno di frequente vengono raggruppati e considerati mancanti. Se uno di questi parametri è impostato su 0, la selezione delle caratteristiche viene disabilitata con relativo impatto sui tempi di elaborazione e sulle prestazioni.  
  
 Oltre a questi metodi per la selezione delle caratteristiche, è possibile migliorare la capacità dell'algoritmo di identificare o promuovere attributi significativi impostando i *flag di modellazione* sul modello oppure i *flag di distribuzione* sulla struttura. Per altre informazioni su questi concetti, vedere [Flag di modellazione &#40;Data mining&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md) e [Distribuzioni delle colonne &#40;Data mining&#41;](../../analysis-services/data-mining/column-distributions-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Personalizzare struttura e modelli di data mining](../../analysis-services/data-mining/customize-mining-models-and-structure.md)  
  
  
