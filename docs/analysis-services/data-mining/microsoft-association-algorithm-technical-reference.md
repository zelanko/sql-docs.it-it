---
title: Riferimento tecnico per l'algoritmo Microsoft Association Rules | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 21f779f1e0b1764fd35d6399aa220e244574d576
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68183168"
---
# <a name="microsoft-association-algorithm-technical-reference"></a>Riferimento tecnico per l'algoritmo Microsoft Association Rules
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules è un'implementazione semplice del noto algoritmo Apriori.  
  
 Sia l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees che l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules possono essere usati per analizzare associazioni, ma le regole individuate da ognuno di essi possono essere diverse. In un modello di albero delle decisioni le divisioni che portano a regole specifiche sono basate su Information Gain, mentre in un modello di associazione le regole sono interamente basate sulla confidenza. Pertanto, in un modello di associazione una regola efficace o caratterizzata da una confidenza elevata può non essere necessariamente interessante, in quanto non fornisce nuove informazioni.  
  
## <a name="implementation-of-the-microsoft-association-algorithm"></a>Implementazione dell'algoritmo Microsoft Association Rules  
 L'algoritmo Apriori non analizza modelli, ma piuttosto genera e quindi conteggia *set di elementi candidati*. Un elemento può rappresentare un evento, un prodotto o il valore di un attributo, a seconda del tipo di dati analizzati.  
  
 Nel tipo più comune di modello di associazione a ogni attributo, quale un nome di prodotto o di evento, vengono associate variabili booleane, che rappresentano un valore Sì/No o Mancante/Esistente. Un'analisi di mercato sugli acquisti è un esempio di modello di regole di associazione che utilizza variabili booleane per rappresentare la presenza o l'assenza di determinati prodotti nel carrello degli acquisti di un cliente.  
  
 Per ogni set di elementi l'algoritmo crea quindi punteggi che rappresentano supporto e confidenza. Tali punteggi possono essere utilizzati per classificare e derivare regole interessanti dai set di elementi.  
  
 È inoltre possibile creare modelli di associazione per gli attributi numerici. Se gli attributi sono continui, i numeri possono essere *discretizzati* o raggruppati in bucket. I valori discretizzati possono quindi essere gestiti come valori booleani o come coppie attributo-valore.  
  
### <a name="support-probability-and-importance"></a>Supporto, probabilità e priorità  
 Il*supporto*, definito a volte *frequenza*, indica il numero di case che contengono l'elemento o la combinazione di elementi di destinazione. Nel modello è possibile includere solo gli elementi che hanno almeno la quantità specificata di supporto.  
  
 Per *set di elementi frequente* si intende una raccolta di elementi in cui anche la combinazione di elementi dispone di supporto superiore alla soglia definita dal parametro MINIMUM_SUPPORT. Se ad esempio il set di elementi è {A,B,C} e il valore MINIMUM_SUPPORT è 10, ogni singolo elemento A, B e C e la combinazione di elementi {A,B,C} devono trovarsi in almeno 10 case per essere inclusi nel modello.  
  
 **Nota** È anche possibile controllare il numero di set di elementi in un modello di data mining specificando la lunghezza massima di un set di elementi, dove per lunghezza si intende il numero di elementi.  
  
 Per impostazione predefinita, il supporto di qualsiasi elemento o set di elementi specifico rappresenta un conteggio dei case che contengono l'elemento o gli elementi. Tuttavia, è anche possibile esprimere MINIMUM_SUPPORT come percentuale del totale dei case del set di dati, digitando il numero come valore decimale minore di 1. Se ad esempio si specifica un valore MINIMUM_SUPPORT pari a 0,03, significa che almeno il 3% del totale dei case del set di dati deve contenere l'elemento o il set di elementi ai fini dell'inclusione nel modello. È necessario eseguire prove con il modello per determinare se è preferibile utilizzare un conteggio o una percentuale.  
  
 Viceversa, la soglia per le regole non viene espressa come conteggio o percentuale, ma come probabilità, talvolta definita *confidenza*. Se ad esempio il set di elementi {A,B,C} ricorre in 50 case, ma anche il set di elementi {A,B,D} ricorre in 50 case e il set di elementi {A,B} in altri 50 case, è evidente che {A,B} non è un criterio di stima efficace per {C}. Per ponderare un determinato risultato rispetto a tutti i risultati noti, pertanto, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene calcolata la probabilità della singola regola, ad esempio If {A,B} Then {C}, dividendo il supporto per il set di elementi {A,B,C} per il supporto per tutti i set di elementi correlati.  
  
 È possibile limitare il numero di regole prodotte da un modello impostando un valore per MINIMUM_PROBABILITY.  
  
 Per ogni regola creata, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce un punteggio che ne indica la *priorità*, definita anche come *accuratezza*. L'accuratezza viene calcolata in modo diverso per set di elementi e regole.  
  
 La priorità di un set di elementi viene calcolata come la probabilità del set di elementi divisa per la probabilità composta dei singoli elementi al suo interno. Se ad esempio un set di elementi contiene {A,B}, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono innanzitutto conteggiati tutti i case che contengono questa combinazione A e B; il risultato viene poi diviso per il numero totale di case, quindi la probabilità viene normalizzata.  
  
 La priorità di una regola viene calcolata con la probabilità in forma logaritmica del lato destro della regola, dato il lato sinistro. Ad esempio, nella regola `If {A} Then {B}`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] calcola il rapporto dei case con A e B rispetto ai case con B ma senza A, quindi normalizza tale rapporto usando una scala logaritmica.  
  
### <a name="feature-selection"></a>Selezione caratteristiche  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules non esegue alcun tipo di caratteristica di selezione automatica degli attributi. Al contrario, fornisce i parametri che controllano i dati utilizzati dall'algoritmo, che possono includere limiti sulla dimensione di ogni set di elementi oppure l'impostazione del supporto massimo e minimo richiesto per aggiungere un set di elementi al modello.  
  
-   Per filtrare gli elementi e gli eventi che sono troppo comuni e pertanto non interessanti, ridurre il valore di MAXIMUM_SUPPORT per rimuovere i set di elementi più frequenti dal modello.  
  
-   Per filtrare gli elementi e i set di elementi che sono rari, aumentare il valore di MINIMUM_SUPPORT.  
  
-   Per filtrare le regole, aumentare il valore di MINIMUM_PROBABILITY.  
  
## <a name="customizing-the-microsoft-association-rules-algorithm"></a>Personalizzazione dell'algoritmo Microsoft Association Rules  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules supporta vari parametri che influiscono sul comportamento, sulle prestazioni e sull'accuratezza del modello di data mining risultante.  
  
### <a name="setting-algorithm-parameters"></a>Impostazione dei parametri dell'algoritmo  
 È possibile modificare in qualsiasi momento i parametri per un modello di data mining usando Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. È inoltre possibile modificare i parametri a livello di codice usando il <xref:Microsoft.AnalysisServices.MiningModel.AlgorithmParameters%2A> raccolta in AMO oppure usando il [elemento MiningModels &#40;ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/collections/miningmodels-element-assl) XMLA. Nella tabella seguente viene descritto ogni parametro.  
  
> [!NOTE]  
>  Non è possibile modificare i parametri in un modello esistente utilizzando un'istruzione DMX. è necessario specificare i parametri in DMX CREATE MODEL o ALTER STRUCTURE... ADD MODEL quando si crea il modello.  
  
 *MAXIMUM_ITEMSET_COUNT*  
 Specifica il numero massimo di set di elementi da produrre. Se non si specifica alcun numero, viene utilizzato il valore predefinito.  
  
 Il valore predefinito è 200000.  
  
> [!NOTE]  
>  I set di elementi vengono classificati in base al supporto. Tra i set di elementi con supporto uguale, l'ordinamento è arbitrario.  
  
 *MAXIMUM_ITEMSET_SIZE*  
 Specifica il numero massimo di elementi consentiti in un set di elementi. Se si imposta il valore su 0, non esiste alcun limite per le dimensioni del set di elementi.  
  
 Il valore predefinito è 3.  
  
> [!NOTE]  
>  La riduzione di questo valore può diminuire i tempi necessari per la creazione del modello, perché l'elaborazione del modello si arresta quando viene raggiunto il limite.  
  
 *MAXIMUM_SUPPORT*  
 Specifica il numero massimo di case disponibili per un set di elementi per il supporto. Questo parametro può essere utilizzato per eliminare gli elementi riportati spesso e che quindi possono essere poco significativi.  
  
 I valori minori di 1 rappresentano una percentuale sul totale dei case. I valori maggiori di 1 rappresentano il numero assoluto di case che possono contenere il set di elementi.  
  
 Il valore predefinito è 1.  
  
 *MINIMUM_ITEMSET_SIZE*  
 Specifica il numero minimo di elementi consentiti in un set di elementi. Se si aumenta questo numero, il modello potrebbe contenere un numero minore di set di elementi. Questa funzione può essere utile se ad esempio si desidera ignorare i set di elementi con un singolo elemento.  
  
 Il valore predefinito è 1.  
  
> [!NOTE]  
>  Non è possibile ridurre il tempo di elaborazione del modello aumentando il valore minimo, perché [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve comunque calcolare le probabilità per i singoli elementi come parte dell'elaborazione. Tuttavia, impostando questo valore su un numero più elevato è possibile filtrare i set di elementi più piccoli.  
  
 *MINIMUM_PROBABILITY*  
 Specifica la probabilità minima che una regola sia vera (True).  
  
 Se ad esempio si imposta il valore 0,5, non possono essere generate regole con probabilità inferiore al 50%.  
  
 Il valore predefinito è 0,4.  
  
 *MINIMUM_SUPPORT*  
 Specifica il numero minimo di case che devono contenere il set di elementi affinché l'algoritmo possa generare una regola.  
  
 Se si imposta un valore minore di 1, il numero minimo di case viene calcolato come percentuale del totale dei case.  
  
 Se si imposta un numero intero maggiore di 1, il numero minimo di case viene calcolato come conteggio dei case che devono contenere il set di elementi. Se la memoria è limitata, l'algoritmo può aumentare automaticamente il valore di questo parametro.  
  
 Il valore predefinito è 0,03. Questo significa che per essere incluso nel modello, è necessario che un set di elementi si trovi in almeno il 3% dei case.  
  
 *OPTIMIZED_PREDICTION_COUNT*  
 Definisce il numero di elementi da memorizzare nella cache per ottimizzare la stima.  
  
 Il valore predefinito è 0. Quando viene utilizzata l'impostazione predefinita, l'algoritmo genererà il numero di stime richieste nella query.  
  
 Se si specifica un valore diverso da zero per *OPTIMIZED_PREDICTION_COUNT,* le query di stima potranno restituire al massimo il numero specificato di elementi, anche se si richiedono stime aggiuntive. L'impostazione di un valore può tuttavia migliorare le prestazioni della stima.  
  
 Se ad esempio si imposta il valore 3, l'algoritmo memorizza nella cache solo 3 elementi per la stima. Non è possibile visualizzare stime aggiuntive che potrebbero essere ugualmente probabili per i 3 elementi restituiti.  
  
### <a name="modeling-flags"></a>Flag di modellazione  
 I flag di modellazione seguenti sono supportati per l'uso con l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules.  
  
 NOT NULL  
 Indica che la colonna non può contenere un valore Null. Se [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] rileva un valore Null durante il training del modello, viene generato un errore.  
  
 Si applica alla colonna della struttura di data mining.  
  
 MODEL_EXISTENCE_ONLY  
 Indica che la colonna verrà considerata come se presentasse due stati possibili: **Mancano** e **esistenti**. Un valore Null è un valore mancante.  
  
 Si applica alla colonna del modello di data mining.  
  
## <a name="requirements"></a>Requisiti  
 Un modello di associazione deve contenere una colonna chiave, le colonne di input e una singola colonna stimabile.  
  
### <a name="input-and-predictable-columns"></a>Colonne di input e stimabili  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules supporta colonne di input e colonne stimabili specifiche, riportate nella tabella seguente. Per altre informazioni sul significato dei tipi di contenuto di un modello di data mining, vedere [Tipi di contenuto &#40;Data mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Colonna|Tipi di contenuto|  
|------------|-------------------|  
|Attributo di input|Cyclical, Discrete, Discretized, Key, Table e Ordered|  
|Attributo stimabile|Cyclical, Discrete, Discretized, Table e Ordered|  
  
> [!NOTE]  
>  Sono supportati i tipi di contenuto Cyclical e Ordered ma l'algoritmo li considera come valori discreti e non esegue un'elaborazione speciale.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Association Rules](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Esempi di query sul modello di associazione](../../analysis-services/data-mining/association-model-query-examples.md)   
 [Contenuto dei modelli di data mining per i modelli di associazione &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
