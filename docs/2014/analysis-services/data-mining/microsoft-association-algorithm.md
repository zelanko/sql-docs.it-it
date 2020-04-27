---
title: Algoritmo Microsoft Association | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MinimumProbability property
- itemsets [Analysis Services]
- MaximumItemsetCount property
- MinimumSupport property
- OPTIMIZED_PREDICTION_COUNT
- OptimizedPredictionCount property
- MaximumSupport property
- MINIMUM_PROBABILITY
- algorithms [data mining]
- association algorithms [Analysis Services]
- rules [Data Mining]
- association rules
- MinimumItemsetSize property
- market basket analysis [Analysis Services]
- associations [Analysis Services]
- MINIMUM_SUPPORT
- MAXIMUM_SUPPORT
- MINIMUM_ITEMSET_SIZE
- MaximumItemsetSize property
ms.assetid: 8b6b8247-62f9-4f6f-b1af-d01dab290e4c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 44fd6a97cd355ab9bcdd5481fe4ebaa5d13d17c4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78174739"
---
# <a name="microsoft-association-algorithm"></a>Algoritmo Microsoft Association Rules
  L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules è un algoritmo di associazione incluso in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], utile per i motori dei suggerimenti. Un motore dei suggerimenti consiglia prodotti ai clienti in base agli articoli che hanno già acquistato o a cui sono interessati. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules è utile anche per analisi di mercato sugli acquisti. Per un esempio di Market basket analysis, vedere [lezione 3: compilazione di uno scenario Market basket &#40;esercitazione intermedia sul data mining&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md) nell'esercitazione sul data mining.

 I modelli di associazione vengono compilati in base a set di dati che includono sia gli indicatori dei singoli case che gli indicatori degli elementi contenuti nei case. Un gruppo di elementi in un case viene chiamato *set di elementi*. Un modello di associazione è costituito da una serie di set di elementi e di regole che descrivono la modalità di raggruppamento di tali elementi all'interno dei case. È possibile utilizzare le regole identificate dall'algoritmo per stimare i probabili acquisti futuri di un cliente, in base agli elementi già esistenti nel relativo carrello acquisti. Nel diagramma seguente viene illustrata una serie di regole all'interno di un set di elementi.

 ![Set di regole per un modello Association Rules](../media/association.gif "Set di regole per un modello Association Rules")

 Come illustrato nel diagramma, l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules può individuare potenzialmente un numero elevato di regole all'interno di un set di dati. L'algoritmo utilizza due parametri, uno di supporto e l'altro di probabilità, per descrivere i set di elementi e le regole generati. Se ad esempio X e Y rappresentano due elementi contenuti in un carrello acquisti, il parametro di supporto è il numero di case del set di dati che contengono la combinazione di elementi X e Y. Se il parametro di supporto viene usato insieme ai parametri definiti dall'utente, *MINIMUM_SUPPORT* e *MAXIMUM_SUPPORT,* , l'algoritmo controlla il numero di set di elementi generati. Il parametro di probabilità, definito anche *confidenza*, rappresenta la frazione di case del set di dati che contengono sia l'elemento X che l'elemento Y. Se il parametro di probabilità viene usato insieme al parametro *MINIMUM_PROBABILITY* , l'algoritmo controlla il numero di regole generate.

## <a name="example"></a>Esempio
 L'azienda [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] Cycle intende riprogettare la funzionalità del relativo sito Web. L'obiettivo della riprogettazione è aumentare le vendite effettive dei prodotti. Poiché l'azienda registra ogni vendita in un database transazionale, è possibile usare l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules per identificare i set di prodotti che tendono ad essere acquistati insieme. In seguito, è possibile stimare elementi aggiuntivi a cui può essere interessato un cliente, in base agli elementi già esistenti nel relativo carrello acquisti.

## <a name="how-the-algorithm-works"></a>Funzionamento dell'algoritmo
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules attraversa un set di dati per trovare elementi che ricorrono insieme in un case. Successivamente, l'algoritmo raggruppa in set gli elementi associati che ricorrono almeno nel numero di case specificati dal parametro *MINIMUM_SUPPORT* . Un set di elementi, ad esempio, potrebbe essere "Mountain 200=Existing, Sport 100=Existing", con un valore di supporto pari a 710. L'algoritmo genera quindi le regole dai set di elementi. Tali regole vengono utilizzate per stimare la presenza di un elemento nel database, in base alla presenza di altri elementi specifici che l'algoritmo identifica come importanti. Ad esempio, una regola potrebbe essere "if Touring 1000=existing and Road bottle cage=existing, then Water bottle=existing", con un valore di probabilità pari a 0,812. In questo esempio, in base alla presenza di pneumatici Touring 1000 e del contenitore per bottiglie di acqua nel carrello acquisti, l'algoritmo stima che tale carrello contiene probabilmente anche una bottiglia di acqua.

 Per una spiegazione più dettagliata dell'algoritmo, insieme a un elenco di parametri per la personalizzazione del comportamento dell'algoritmo e il controllo dei risultati nel modello di data mining, vedere [Riferimento tecnico per l'algoritmo Microsoft Association Rules](microsoft-association-algorithm-technical-reference.md).

## <a name="data-required-for-association-models"></a>Dati richiesti per i modelli di associazione
 Quando si preparano i dati da utilizzare in un modello Association Rules, verificare che siano chiari i requisiti per l'algoritmo specifico, tra cui la quantità di dati necessari e la modalità di utilizzo dei dati.

 I requisiti per un modello Association Rules sono i seguenti:

-   **Una colonna a chiave singola** Ogni modello deve contenere una colonna numerica o di testo che identifichi in modo univoco ogni record. Le chiavi composte non sono consentite.

-   **Una singola colonna stimabile** Un modello di associazione può includere un'unica colonna stimabile. In genere si tratta della colonna chiave della tabella nidificata, ad esempio il campo in cui sono elencati i prodotti acquistati. I valori devono essere discreti o discretizzati.

-   **Colonne di input** . Le colonne di input devono essere discrete. Spesso, i dati di input per il modello di associazione sono contenuti in due tabelle. Ad esempio, una tabella può contenere informazioni sui clienti mentre l'altra può contenere informazioni sugli acquisti dei clienti. È possibile inserire tali dati nel modello tramite una tabella nidificata. Per altre informazioni sulle tabelle annidate, vedere [Tabelle annidate &#40;Analysis Services - Data mining&#41;](nested-tables-analysis-services-data-mining.md).

 Per informazioni più dettagliate sui tipi di contenuto e i tipi di dati supportati per i modelli di associazione, vedere la sezione Requisiti di [Riferimento tecnico per l'algoritmo Microsoft Association Rules](microsoft-association-algorithm-technical-reference.md).

## <a name="viewing-an-association-model"></a>Visualizzazione di un modello di associazione
 Per esplorare il modello, è possibile usare il **Visualizzatore Microsoft Association Rules**. Quando si visualizza un modello di associazione, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono presentate le correlazioni da diverse angolazioni, in modo che sia possibile identificare più facilmente le relazioni e le regole individuate nei dati. Il riquadro **Set di elementi** del visualizzatore fornisce una suddivisione dettagliata delle combinazioni più comuni, ovvero set di elementi. Il riquadro **Regole** presenta un elenco di regole generalizzate dai dati e consente di aggiungere calcoli di probabilità, nonché di classificare le regole in base all'importanza relativa. Il visualizzatore di reti di dipendenza consente di esplorare visivamente le connessioni tra elementi diversi. Per altre informazioni, vedere [Visualizzare un modello usando il Visualizzatore Microsoft Clustering](browse-a-model-using-the-microsoft-cluster-viewer.md).

 Per altri dettagli sui set di elementi e le regole, è possibile esplorare il modello in [Microsoft Generic Content Tree Viewer](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md). Il contenuto archiviato per il modello include il supporto per ogni set di elementi, un punteggio per ogni regola e altre statistiche. Per altre informazioni, vedere [Contenuto dei modelli di data mining per i modelli di associazione &#40;Analysis Services - Data mining&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md).

## <a name="creating-predictions"></a>Creazione di stime
 Dopo l'elaborazione del modello, è possibile utilizzare le regole e i set di elementi per eseguire stime. In un modello di associazione una stima indica quale elemento è probabile che si verifichi data la presenza dell'elemento specificato. La stima può includere informazioni come la probabilità, il supporto o la priorità. Per alcuni esempi su come creare query su un modello di associazione, vedere [Esempi di query sul modello di associazione](association-model-query-examples.md).

 Per informazioni generali sulla creazione di query su un modello di data mining, vedere [Query di data mining](data-mining-queries.md).

## <a name="performance"></a>Prestazioni
 Il processo di creazione di set di elementi e di conteggio delle correlazioni può richiedere tempi lunghi. Anche se [!INCLUDE[msCoName](../../includes/msconame-md.md)] l'algoritmo Association Rules utilizza tecniche di ottimizzazione per risparmiare spazio e velocizzare l'elaborazione, è necessario tenere presente che i problemi di prestazioni possono verificarsi in condizioni come le seguenti:

-   Il set di dati è di grandi dimensioni con molti singoli elementi.

-   La dimensione minima del set di elementi è impostata su un valore eccessivamente basso.

 Per ridurre i tempi di elaborazione e la complessità dei set di elementi, provare a raggruppare gli elementi correlati per categorie prima di analizzare i dati.

## <a name="remarks"></a>Osservazioni

-   Non supporta l'utilizzo del linguaggio PMML (Predictive Model Markup Language) per la creazione di modelli di data mining.

-   Supporta il drill-through.

-   Supporta l'utilizzo di modelli di data mining OLAP.

-   Supporta la creazione di dimensioni di data mining.

## <a name="see-also"></a>Vedi anche
 [Algoritmi di data mining &#40;Analysis Services-Data mining&#41;](data-mining-algorithms-analysis-services-data-mining.md) [visualizzare un modello utilizzando il contenuto del modello di data mining del Visualizzatore Microsoft Association Rules](browse-a-model-using-the-microsoft-association-rules-viewer.md) [per i modelli di associazione &#40;Analysis Services-Data mining&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md) [esempi di query sul modello](association-model-query-examples.md) di associazione di [riferimento tecnico Microsoft Association](microsoft-association-algorithm-technical-reference.md)


