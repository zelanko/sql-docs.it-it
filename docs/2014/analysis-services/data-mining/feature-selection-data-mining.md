---
title: Funzionalità di selezione (Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], feature selections
- attributes [data mining]
- feature selection algorithms [Analysis Services]
- data mining [Analysis Services], feature selections
- neural network algorithms [Analysis Services]
- naive bayes algorithms [Analysis Services]
- decision tree algorithms [Analysis Services]
- datasets [Analysis Services]
- clustering algorithms [Analysis Services]
- coding [Data Mining]
ms.assetid: b044e785-4875-45ab-8ae4-cd3b4e3033bb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a1d79bb3810a56e8a1769845131312eab306f223
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084420"
---
# <a name="feature-selection-data-mining"></a>Selezione delle caratteristiche (Data mining)
  *Selezione delle caratteristiche* è un termine comunemente usato nel data mining per descrivere gli strumenti e tecniche disponibili per ridurre gli input a una dimensione gestibile per l'elaborazione e analisi. Selezione delle caratteristiche implica non solo *riduzione della cardinalità*, il che significa che impone un limite arbitraria o predefinita per il numero di attributi che possono essere considerati durante la creazione di un modello, ma anche la scelta degli attributi, vale a dire che l'analista o lo strumento di modellazione attivamente seleziona o Elimina gli attributi in base all'utilità per l'analisi.  
  
 La possibilità di applicare la selezione delle caratteristiche è essenziale per un'analisi efficace, poiché nei set di dati sono spesso contenute molte più informazioni rispetto a quelle necessarie per compilare il modello. Ad esempio, in un set di dati potrebbero essere contenute 500 colonne in cui vengono descritte le caratteristiche dei clienti; tuttavia, se i dati di alcune colonne sono di tipo sparse, non sarebbe molto vantaggioso aggiungerli al modello. Se si mantengono le colonne non necessarie durante la compilazione del modello, la quantità di CPU e memoria necessaria per il processo di training sarà maggiore, così come lo spazio di archiviazione richiesto per il modello completato.  
  
 Anche se le risorse non costituiscono un problema, è generalmente consigliabile rimuovere le colonne non necessarie che potrebbero avere un impatto negativo sulla qualità dei modelli individuati per i motivi seguenti:  
  
-   Alcune colonne sono poco significative o ridondanti. In questo caso risulta più difficile individuare modelli significativi dai dati.  
  
-   Per individuare modelli di qualità, la maggior parte degli algoritmi di data mining richiede un set di dati di training di dimensioni molto maggiori in set di dati di dimensioni elevate, ma i dati di training hanno dimensioni ridotte in alcune applicazioni di data mining.  
  
 Se solo in 50 delle 500 colonne dell'origine dati sono presenti informazioni utili per la compilazione di un modello, è possibile semplicemente non includerle nel modello oppure utilizzare le tecniche di selezione delle caratteristiche per individuare automaticamente le caratteristiche migliori ed escludere i valori che sono statisticamente insignificanti. La selezione delle caratteristiche consente di risolvere i problemi relativi alla presenza di una quantità eccessiva di dati di scarso valore o di una quantità ridotta di dati di valore elevato.  
  
## <a name="feature-selection-in-analysis-services-data-mining"></a>Selezione delle caratteristiche nel data mining in Analysis Services  
 Generalmente, la selezione delle caratteristiche viene eseguita automaticamente in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e in ogni algoritmo è disponibile un set di tecniche predefinite per applicare in modo intelligente la riduzione delle caratteristiche. La selezione delle caratteristiche viene sempre eseguita prima del training del modello per scegliere automaticamente gli attributi di un set di dati che hanno maggiori probabilità di essere utilizzati nel modello. Tuttavia, è anche possibile impostare manualmente i parametri per influire sul comportamento della selezione delle caratteristiche.  
  
 In genere, la selezione delle caratteristiche consente di calcolare un punteggio per ogni attributo, quindi di selezionare solo gli attributi con i punteggi migliori. Inoltre, è possibile regolare la soglia per i punteggi massimi. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono disponibili più metodi per calcolare questi punteggi e il metodo esatto applicato in qualsiasi modello dipende dai fattori seguenti:  
  
-   Algoritmo utilizzato nel modello  
  
-   Tipo di dati dell'attributo  
  
-   Qualsiasi parametro che potrebbe essere stato impostato sul modello  
  
 La selezione delle caratteristiche viene applicata agli input, agli attributi stimabili oppure agli stati di una colonna. Quando il calcolo del punteggio per la selezione delle caratteristiche è terminato, nel processo di compilazione del modello vengono inclusi solo gli attributi e gli stati selezionati dall'algoritmo, che possono essere utilizzati per eventuali stime. Se si sceglie un attributo stimabile che non soddisfa la soglia per la selezione delle caratteristiche, l'attributo può comunque essere utilizzato per le stime, tuttavia queste ultime saranno basate unicamente sulle statistiche globali presenti nel modello.  
  
> [!NOTE]  
>  La selezione delle caratteristiche influisce solo sulle colonne utilizzate nel modello, mentre non ha effetto sull'archiviazione della struttura di data mining. Le colonne rimosse dal modello di data mining sono ancora disponibili nella struttura e i dati delle colonne della struttura di data mining verranno memorizzati nella cache.  
  
### <a name="definition-of-feature-selection-methods"></a>Definizione di metodi per implementare la caratteristica di selezione degli attributi  
 È possibile implementare la caratteristica di selezione degli attributi in molti modi, a seconda del tipo di dati utilizzati e dell'algoritmo scelto per l'analisi. In SQL Server Analysis Services sono disponibili diversi metodi diffusi e consolidati per il punteggio degli attributi. Il metodo applicato in qualsiasi algoritmo o set di dati dipende dai tipi di dati e dall'utilizzo delle colonne.  
  
 Il punteggio di *interesse* viene usato per classificare e ordinare gli attributi in colonne che contengono dati numerici continui non binari.  
  
 L'*entropia di Shannon* e due punteggi *Bayes* sono disponibili per le colonne contenenti dati discreti e discretizzati. Tuttavia, se nel modello sono contenute colonne continue, il punteggio di interesse verrà utilizzato per valutare tutte le colonne di input e assicurare la coerenza.  
  
 Nella sezione seguente viene descritto ogni metodo relativo alla selezione delle caratteristiche.  
  
#### <a name="interestingness-score"></a>Punteggio di interesse  
 Una caratteristica è interessante se indica informazioni utili. Poiché la definizione di ciò che è utile varia a seconda dello scenario, il settore del data mining ha sviluppato i vari modi per misurare *interesse*. Ad esempio, *originalità* potrebbe essere interessante nell'individuazione degli outlier, ma la possibilità di discriminare tra elementi strettamente correlati, o *peso discriminante*, potrebbe essere più interessante per classificazione.  
  
 La misura dell'interesse utilizzata in SQL Server Analysis Services viene *basata sull'entropia*, che indica che gli attributi con distribuzioni casuali hanno un'entropia maggiore e un information gain, tali attributi pertanto sono meno interessante. L'entropia di un determinato attributo viene confrontata con quella di tutti gli altri attributi, come segue:  
  
 Interesse(Attributo) = - (m - Entropia(Attributo)) * (m - Entropia(Attributo))  
  
 Per entropia centrale o m si intende l'entropia dell'intero set di caratteristiche. Sottraendo l'entropia dell'attributo di destinazione dall'entropia centrale, è possibile valutare la quantità di informazioni fornita dall'attributo.  
  
 Questo punteggio viene utilizzato per impostazione predefinita ogni volta che la colonna contiene dati numerici continui non binari.  
  
#### <a name="shannons-entropy"></a>entropia di Shannon  
 L'entropia di Shannon misura l'incertezza di una variabile casuale per un determinato risultato. Ad esempio, l'entropia del lancio di una moneta può essere rappresentata come funzione della probabilità che esca testa.  
  
 In Analysis Services viene utilizzata la formula seguente per il calcolo dell'entropia di Shannon:  
  
 H(X) = -∑ P(xi) log(P(xi))  
  
 Questo metodo di assegnazione dei punteggi è disponibile per gli attributi discreti e discretizzati.  
  
#### <a name="bayesian-with-k2-prior"></a>Bayes con probabilità a priori K2  
 In Analysis Services sono disponibili due punteggi della caratteristica di selezione degli attributi basati su reti Bayes. Una rete Bayes è un grafico *orientato* o *aciclico* di stati e di transizioni tra stati, ossia alcuni stati sono sempre precedenti allo stato corrente, alcuni sono successivi e il grafico non si ripete. Per definizione, le reti Bayes consentono l'utilizzo delle conoscenze precedenti. Tuttavia, la domanda in merito a quali stati precedenti utilizzare nel calcolo delle probabilità degli stati successivi è importante per la progettazione, le prestazioni e l'accuratezza dell'algoritmo.  
  
 L'algoritmo K2 per l'apprendimento di una rete Bayes, sviluppato da Cooper e Herskovits, viene utilizzato spesso nel data mining. È scalabile e consente di analizzare più variabili, ma richiede l'ordinamento delle variabili utilizzate come input. Per altre informazioni, vedere [Learning Bayesian Networks](https://go.microsoft.com/fwlink/?LinkId=105885) di Chickering, Geiger e Heckerman.  
  
 Questo metodo di assegnazione dei punteggi è disponibile per gli attributi discreti e discretizzati.  
  
#### <a name="bayesian-dirichlet-equivalent-with-uniform-prior"></a>Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme  
 Anche per il punteggio equivalente Bayes Dirichlet (BDE, Bayesian Dirichlet Equivalent) si utilizza l'analisi bayesiana per valutare una rete dato un set di dati. Il metodo di assegnazione dei punteggi BDE, sviluppato da Heckerman, è basato sulla metrica BD sviluppata da Cooper e Herskovits. La distribuzione Dirichlet è una distribuzione multinomiale che descrive la probabilità condizionale di ogni variabile nella rete, oltre a includere molte proprietà utili per l'apprendimento.  
  
 Il metodo equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (BDEU, Bayesian Dirichlet Equivalent with Uniform Prior) presuppone un caso speciale della distribuzione Dirichlet in cui viene utilizzata una costante matematica per creare una distribuzione fissa o uniforme di stati precedenti. Il punteggio BDE presuppone anche un'equivalenza di probabilità, ossia non è possibile prevedere che i dati discriminino strutture equivalenti. In altri termini, se il punteggio di Se A allora B è uguale al punteggio di Se B allora A, non è possibile distinguere le strutture in base ai dati e non è possibile derivare il rapporto di causa ed effetto.  
  
 Per altre informazioni sulle reti Bayes e sull'implementazione di questi metodi di assegnazione dei punteggi, vedere [Learning Bayesian Networks](https://go.microsoft.com/fwlink/?LinkId=105885).  
  
### <a name="feature-selection-methods-used-by-analysis-services-algorithms"></a>Metodi per implementare la caratteristica di selezione degli attributi utilizzati dagli algoritmi di Analysis Services  
 Nella tabella seguente sono elencati gli algoritmi che supportano la caratteristica di selezione degli attributi, i metodi utilizzati dall'algoritmo e i parametri impostati per controllare il funzionamento di questa caratteristica:  
  
|Algoritmo|Metodo di analisi|Commenti|  
|---------------|------------------------|--------------|  
|Naive Bayes|Entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Poiché l'algoritmo Microsoft Naive Bayes accetta solo attributi discreti o discretizzati, non può utilizzare il punteggio di interesse.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Naive Bayes](microsoft-naive-bayes-algorithm-technical-reference.md).|  
|Decision Trees|Punteggio di interesse<br /><br /> Entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Se esistono colonne contenenti valori continui non binari, viene utilizzato il punteggio di interesse per tutte le colonne, per assicurare coerenza. In caso contrario, viene utilizzato il metodo per implementare la caratteristica di selezione degli attributi predefinito oppure il metodo specificato quando è stato creato il modello.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Guida di riferimento tecnico per l'algoritmo Microsoft Decision Trees](microsoft-decision-trees-algorithm-technical-reference.md).|  
|Neural Network|Punteggio di interesse<br /><br /> Entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Nell'algoritmo Microsoft Neural Network possono essere utilizzati sia i metodi Bayes sia quelli basati sull'entropia, purché nei dati siano contenute colonne continue.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Neural Network](microsoft-neural-network-algorithm-technical-reference.md).|  
|Logistic Regression|Punteggio di interesse<br /><br /> Entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Sebbene l'algoritmo Microsoft Logistic Regression sia basato sull'algoritmo Microsoft Neural Network, non è possibile personalizzare modelli di regressione logistica per controllare il comportamento della caratteristica di selezione degli attributi. Di conseguenza tale caratteristica viene impostata automaticamente sempre sul metodo più appropriato per l'attributo.<br /><br /> Se tutti gli attributi sono discreti o discretizzati, l'impostazione predefinita è BDEU.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Logistic Regression](microsoft-logistic-regression-algorithm-technical-reference.md).|  
|Clustering|Punteggio di interesse|L'algoritmo Microsoft Clustering può utilizzare dati discreti o discretizzati. Tuttavia, perché il punteggio di ogni attributo è calcolato come una distanza e viene rappresentato come un numero continuo, è necessario utilizzare il punteggio di interesse.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Clustering](microsoft-clustering-algorithm-technical-reference.md).|  
|Linear Regression|Punteggio di interesse|L'algoritmo Microsoft Linear Regression può utilizzare solo il punteggio di interesse, poiché supporta solo colonne continue.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Linear Regression](microsoft-linear-regression-algorithm-technical-reference.md).|  
|Association Rules<br /><br /> Sequence Clustering|Non usato|La caratteristica di selezione degli attributi non viene richiamata da questi algoritmi.<br /><br /> È tuttavia possibile controllare il comportamento dell'algoritmo e ridurre le dimensioni dei dati di input impostando i valori dei parametri MINIMUM_SUPPORT e MINIMUM_PROBABILIITY.<br /><br /> Per altre informazioni, vedere [Riferimento tecnico per l'algoritmo Microsoft Association Rules](microsoft-association-algorithm-technical-reference.md) e [Riferimento tecnico per l'algoritmo Microsoft Sequence Clustering](microsoft-sequence-clustering-algorithm-technical-reference.md).|  
|Time Series|Non usato|La selezione delle caratteristiche non si applica ai modelli Time Series.<br /><br /> Per altre informazioni su questo algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Time Series](microsoft-time-series-algorithm-technical-reference.md).|  
  
## <a name="feature-selection-parameters"></a>Parametri della selezione delle caratteristiche  
 Negli algoritmi che supportano la selezione delle caratteristiche è possibile controllare quando tale selezione è abilitata tramite i parametri riportati di seguito. In ogni algoritmo è disponibile un valore predefinito per il numero di input consentiti; tuttavia è possibile eseguire l'override di questo valore predefinito e specificare il numero di attributi. In questa sezione sono elencati i parametri forniti per la gestione della selezione delle caratteristiche.  
  
#### <a name="maximuminputattributes"></a>MAXIMUM_INPUT_ATTRIBUTES  
 Se in un modello è contenuto un numero di colonne maggiore del numero specificato nel parametro *MAXIMUM_INPUT_ATTRIBUTES* , vengono ignorate le colonne che in base all'algoritmo non risultano di interesse.  
  
#### <a name="maximumoutputattributes"></a>MAXIMUM_OUTPUT_ATTRIBUTES  
 In modo analogo, se un modello contiene un numero di colonne stimabili maggiore del numero specificato nel parametro *MAXIMUM_OUTPUT_ATTRIBUTES* , vengono ignorate le colonne che in base all'algoritmo non risultano di interesse.  
  
#### <a name="maximumstates"></a>MAXIMUM_STATES  
 Se un modello contiene un numero di case maggiore del numero specificato nel parametro *MAXIMUM_STATES* , gli stati usati meno di frequente vengono raggruppati e considerati mancanti. Se uno di questi parametri è impostato su 0, la selezione delle caratteristiche viene disabilitata con relativo impatto sui tempi di elaborazione e sulle prestazioni.  
  
 Oltre a questi metodi per la selezione delle caratteristiche, è possibile migliorare la capacità dell'algoritmo di identificare o promuovere attributi significativi impostando i *flag di modellazione* sul modello oppure i *flag di distribuzione* sulla struttura. Per altre informazioni su questi concetti, vedere [Flag di modellazione &#40;Data mining&#41;](modeling-flags-data-mining.md) e [Distribuzioni delle colonne &#40;Data mining&#41;](column-distributions-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Personalizzare struttura e modelli di data mining](customize-mining-models-and-structure.md)  
  
  
