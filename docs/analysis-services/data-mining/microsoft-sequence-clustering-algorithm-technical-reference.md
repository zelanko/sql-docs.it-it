---
title: Riferimento tecnico algoritmo Microsoft Sequence Clustering | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 331a7c4df759114e18fd47007058ddc38b2f77d9
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52418382"
---
# <a name="microsoft-sequence-clustering-algorithm-technical-reference"></a>Riferimento tecnico per l'algoritmo Microsoft Sequence Clustering
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  L'algoritmo Microsoft Sequence Clustering è un algoritmo ibrido in cui viene usata l'analisi delle catene di Markov per identificare le sequenze ordinate e consente di combinare i risultati di tale analisi con le tecniche di clustering per generare cluster in base alle sequenze e agli altri attributi del modello. In questo argomento viene illustrato come implementare e personalizzare l'algoritmo e vengono descritti requisiti speciali per i modelli Sequence Clustering.  
  
 Per informazioni più generali sull'algoritmo, che includono le modalità di esplorazione e di esecuzione di query sui modelli Sequence Clustering, vedere [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md).  
  
## <a name="implementation-of-the-microsoft-sequence-clustering-algorithm"></a>Implementazione dell'algoritmo Microsoft Sequence Clustering  
 Il modello Microsoft Sequence Clustering usano i modelli Markov per identificare le sequenze e determinare la probabilità delle sequenze. Un modello Markov è un grafico diretto che archivia le transizioni tra stati diversi. L'algoritmo Microsoft Sequence Clustering usano catene di Markov di ordine n, non un modello Markov nascosto.  
  
 Il numero di ordini di una catena Markov indica quanti stati vengono usati per determinare la probabilità degli stati correnti. In un modello Markov di primo ordine la probabilità dello stato corrente dipende solo dallo stato precedente. In una catena Markov di secondo ordine la probabilità di un stato dipende dai due stati precedenti e così via. Per ogni catena Markov una matrice della transizione archivia le transizioni per ogni combinazione di stati. Con l'aumentare della lunghezza della catena di Markov, aumenta anche la dimensione della matrice in modo esponenziale e la matrice diventa di tipo sparse. Anche il tempo di elaborazione aumenta proporzionalmente.  
  
 Potrebbe risultare utile visualizzare la catena usando l'esempio di analisi clickstream che analizza le visite alle pagine Web di un sito. Ogni utente crea una lunga sequenza di clic per ogni sessione. Quando si crea un modello per analizzare il comportamento dell'utente in un sito Web, il set di dati usato per il training è una sequenza di URL convertiti in un grafico che include il conteggio di tutte le istanze dello stesso percorso di clic. Nel grafico sono indicate ad esempio la probabilità che l'utente si sposti da pagina 1 a pagina 2 (10%), la probabilità che l'utente si sposti da pagina 1 a pagina 3 (20%) e così via. Unendo tutti i possibili percorsi e pezzi di percorso si ottiene un grafico che potrebbe essere molto più lungo e più complesso di qualsiasi singolo percorso osservato.  
  
 L'algoritmo Microsoft Sequence Clustering usano per impostazione predefinita il metodo di clustering Expectation Maximization (EM). Per altre informazioni, vedere [Riferimento tecnico per l'algoritmo Microsoft Clustering](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md).  
  
 Le destinazioni del clustering sono attributi sia sequenziali che non sequenziali. Ogni cluster viene selezionato casualmente mediante una distribuzione di probabilità. Ogni cluster ha una catena Markov, che rappresenta il set completo di percorsi, e una matrice, che contiene le probabilità e le transizioni degli stati di sequenza. In base alla distribuzione iniziale, viene usata la regola Bayes per calcolare la probabilità di un attributo, inclusa una sequenza, in un cluster specifico.  
  
 L'algoritmo Microsoft Sequence Clustering supporta l'aggiunta di attributi non sequenziali al modello. Ciò significa che questi attributi aggiuntivi vengono combinati con gli attributi di sequenza per creare cluster di case con attributi simili, come accade in un tipico modello di clustering.  
  
 Un modello Sequence Clustering tende a creare molti più cluster rispetto a un tipico modello di clustering. L'algoritmo Microsoft Sequence Clustering esegue pertanto la *decomposizione del cluster*per separare i cluster in base alle sequenze e ad altri attributi.  
  
### <a name="feature-selection-in-a-sequence-clustering-model"></a>Caratteristica di selezione degli attributi in un modello Sequence Clustering  
 La caratteristica di selezione degli attributi non viene richiamata in caso di compilazione delle sequenze, tuttavia si applica in fase di clustering.  
  
|Tipo di modello|Metodo relativo alla caratteristica di selezione degli attributi|Commenti|  
|----------------|------------------------------|--------------|  
|Sequence Clustering|Non usato|La caratteristica di selezione degli attributi non viene richiamata. È tuttavia possibile controllare il comportamento dell'algoritmo impostando i valori dei parametri MINIMUM_SUPPORT e MINIMUM_PROBABILIITY.|  
|Clustering|Punteggio di interesse|Anche se l'algoritmo Clustering può usare algoritmi discreti o discretizzati, il punteggio di ogni attributo viene calcolato come distanza ed è continuo. Viene pertanto usato il punteggio di interesse.|  
  
 Per altre informazioni, vedere [Feature Selection](http://msdn.microsoft.com/library/73182088-153b-4634-a060-d14d1fd23b70).  
  
### <a name="optimizing-performance"></a>Ottimizzazione delle prestazioni  
 L'algoritmo Microsoft Sequence Clustering supporta varie modalità di ottimizzazione dell'elaborazione:  
  
-   Controllo del numero di cluster generati mediante l'impostazione di un valore per il parametro CLUSTER_COUNT.  
  
-   Riduzione del numero di sequenze incluse come attributi mediante l'aumento del valore del parametro MINIMUM_SUPPORT. Di conseguenza, le sequenze rare vengono eliminate.  
  
-   Riduzione della complessità prima dell'elaborazione del modello mediante il raggruppamento degli attributi correlati.  
  
 In generale, è possibile ottimizzare le prestazioni di un modello di catene Markov di ordine n in diversi modi:  
  
-   Controllando la lunghezza delle possibili sequenze.  
  
-   Riducendo a livello di codice il valore di n.  
  
-   Archiviando solo le probabilità che superano una soglia specificata.  
  
 Una descrizione esaustiva di questi metodi esula dall'ambito del presente argomento.  
  
## <a name="customizing-the-sequence-clustering-algorithm"></a>Personalizzazione dell'algoritmo Sequence Clustering  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering supporta vari parametri che influiscono sul comportamento, sulle prestazioni e sull'accuratezza del modello di data mining risultante. È inoltre possibile modificare il comportamento del modello completato impostando flag di modellazione che controllano la modalità di elaborazione dei dati di training da parte dell'algoritmo.  
  
### <a name="setting-algorithm-parameters"></a>Impostazione dei parametri dell'algoritmo  
 Nella tabella seguente sono descritti i parametri che possono essere usati con l'algoritmo Microsoft Sequence Clustering.  
  
 CLUSTER_COUNT  
 Specifica il numero approssimativo di cluster che devono essere generati dall'algoritmo. Se i dati non consentono di generare il numero approssimativo di cluster, l'algoritmo compila il maggior numero di cluster possibile. Se si imposta su 0 il parametro CLUSTER_COUNT, l'algoritmo utilizzerà l'euristica per determinare con maggiore accuratezza il numero di cluster da compilare.  
  
 Il valore predefinito è 10.  
  
> [!NOTE]  
>  La specifica di un numero diverso da zero funge da hint per l'algoritmo, che procede con l'obiettivo di individuare il numero specificato ma potrebbe individuarne un numero maggiore o minore.  
  
 MINIMUM_SUPPORT  
 Specifica il numero minimo di case richiesto come supporto per un attributo per la creazione di un cluster.  
  
 Il valore predefinito è 10.  
  
 MAXIMUM_SEQUENCE_STATES  
 Specifica il numero massimo di stati consentiti in una sequenza.  
  
 Se si imposta un valore numerico maggiore di 100, l'algoritmo potrebbe creare un modello che non fornisce informazioni significative.  
  
 Il valore predefinito è 64.  
  
 MAXIMUM_STATES  
 Specifica il numero massimo di stati per un attributo fuori sequenza supportato dall'algoritmo. Se il numero di stati per un attributo fuori sequenza è maggiore del numero massimo di stati, l'algoritmo utilizza stati più frequenti dell'attributo e considera gli stati rimanenti come **Missing**.  
  
 Il valore predefinito è 100.  
  
### <a name="modeling-flags"></a>Flag di modellazione  
 Di seguito sono indicati i flag di modellazione il cui utilizzo è supportato con l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering.  
  
 NOT NULL  
 Indica che la colonna non può contenere un valore Null. Se Analysis Services rileva un valore Null durante il training del modello, viene generato un errore.  
  
 Si applica alla colonna della struttura di data mining.  
  
 MODEL_EXISTENCE_ONLY  
 Indica che la colonna verrà considerata come se presentasse due stati possibili: **Mancano** e **esistenti**. Un valore Null viene considerato come valore **Missing** .  
  
 Si applica alla colonna del modello di data mining.  
  
 Per altre informazioni sull'uso di valori Missing nei modelli di data mining e su come tali valori influiscono sui punteggi di probabilità, vedere [Valori mancanti &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).  
  
## <a name="requirements"></a>Requisiti  
 La tabella del case deve includere una colonna relativa agli ID e può contenere altre colonne che archiviano attributi sul case.  
  
 L'algoritmo Microsoft Sequence Clustering richiede informazioni sulla sequenza, archiviate come tabella nidificata. Nella tabella nidificata deve essere presente un'unica colonna Key Sequence. Una colonna **Key Sequence** può contenere qualsiasi tipo di dati che è possibile ordinare, inclusi tipi di dati string, ma deve contenere valori univoci per ogni case. Prima di elaborare il modello, è inoltre necessario assicurarsi che sia la tabella del case sia la tabella nidificata vengano ordinate in ordine crescente sulla chiave che correla le tabelle.  
  
> [!NOTE]  
>  Se si crea un modello che usano l'algoritmo di Microsoft Sequence ma non usano una colonna Sequence, il modello risultante non conterrà alcuna sequenza, ma raggrupperà semplicemente i case in base ad altri attributi inclusi nel modello.  
  
### <a name="input-and-predictable-columns"></a>Colonne di input e stimabili  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering supporta colonne di input e colonne stimabili specifiche, riportate nella tabella seguente. Per altre informazioni sul significato dei tipi di contenuto usati in un modello di data mining, vedere [Tipi di contenuto &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|colonna|Tipi di contenuto|  
|------------|-------------------|  
|Attributo di input|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Table e Ordered|  
|Attributo stimabile|Continuous, Cyclical, Discrete, Discretized, Table e Ordered|  
  
## <a name="remarks"></a>Note  
  
-   Usare la funzione [PredictSequence &#40;DMX&#41;](../../dmx/predictsequence-dmx.md) per la stima delle sequenze. Per altre informazioni sulle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che supportano la stima delle sequenze, vedere [funzionalità supportate dalle edizioni di SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
-   L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering non supporta l'uso dello standard PMML (Predictive Model Markup Language) per la creazione dei modelli di data mining.  
  
-   L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering supporta il drill-through, l'utilizzo di modelli di data mining OLAP e l'utilizzo di dimensioni di data mining.  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Sequence Clustering Model Query Examples](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Contenuto dei modelli di data mining per i modelli Sequence Clustering &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
