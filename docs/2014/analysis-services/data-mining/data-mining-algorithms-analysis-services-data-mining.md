---
title: Algoritmi di Data Mining (Analysis Services - Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- segmentation algorithms [Analysis Services]
- clustering [Data Mining]
- learning algorithms
- data mining [Analysis Services], models
- algorithms [data mining]
- mining models [Analysis Services], algorithms
- inductive learning
- mining models [Analysis Services], creating
- data mining [Analysis Services], algorithms
- machine learning algorithms [Analysis Services]
ms.assetid: ed1fc83b-b98c-437e-bf53-4ff001b92d64
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 490857f9a8c95853d3f89bc8b0cfb85a165f1fd1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722824"
---
# <a name="data-mining-algorithms-analysis-services---data-mining"></a>Algoritmi di data mining (Analysis Services - Data mining)
  Oggetto *algoritmo di data mining* è un set di approcci euristici e calcoli che crea un modello di data mining dai dati. Per creare un modello, tramite l'algoritmo vengono innanzitutto analizzati i dati forniti, ricercando tipi specifici di modelli o tendenze. I risultati dell'analisi vengono utilizzati dall'algoritmo per definire i parametri ottimali per la creazione del modello di data mining. Questi parametri vengono quindi applicati all'intero set di dati per estrarre modelli utilizzabili e statistiche dettagliate.  
  
 Il modello di data mining creato da un algoritmo con i dati in uso può avere forme diverse, tra cui:  
  
-   Set di cluster con cui viene descritto in che modo i case di un set di dati sono correlati.  
  
-   Albero delle decisioni per la stima di un risultato e per la descrizione della modalità con cui criteri diversi possono incidere su tale risultato.  
  
-   Modello matematico per la previsione delle vendite.  
  
-   Set di regole mediante le quali viene descritto in che modo i prodotti vengono raggruppati in una transazione e le probabilità con cui tali prodotti vengano acquistati insieme.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornisce più algoritmi utilizzabili nelle soluzioni di data mining. Questi algoritmi sono implementazioni di alcune delle metodologie più diffuse utilizzate in un data mining. Tutti gli algoritmi di data mining di Microsoft possono essere personalizzati e sono completamente programmabili tramite API specificate o utilizzando i componenti di data mining in SQL Server Integration Services.  
  
 È anche possibile usare gli algoritmi di terze parti conformi con OLE DB specifiche di Data Mining o lo sviluppo di algoritmi personalizzati registrabili come servizi, quindi usati all'interno del framework Data Mining di SQL Server.  
  
## <a name="choosing-the-right-algorithm"></a>Scelta dell'algoritmo corretto  
 La scelta dell'algoritmo più appropriato da utilizzare per un'attività analitica specifica può rivelarsi complessa. Sebbene sia possibile utilizzare algoritmi diversi per eseguire la stessa attività aziendale, ogni algoritmo produce un risultato diverso e alcuni algoritmi possono produrre più di un tipo di risultato. È ad esempio possibile usare l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees non solo per le stime ma anche per ridurre il numero di colonne in un set di dati, in quanto l'albero delle decisioni può consentire di identificare colonne che non hanno effetto sul modello di data mining finale.  
  
### <a name="choosing-an-algorithm-by-type"></a>Scelta di un algoritmo in base al tipo  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono inclusi i tipi di algoritmi seguenti:  
  
-   **Algoritmi di classificazione** che consentono di stimare una o più variabili discrete, in base agli altri attributi del set di dati.  
  
-   **Gli algoritmi di regressione** stimare una o più variabili continue, ad esempio profitto o perdita, in base ad altri attributi nel set di dati.  
  
-   **Algoritmi di segmentazione** che consentono di dividere i dati in gruppi, o cluster, di elementi con proprietà simili.  
  
-   **Algoritmi di associazione** che consentono di trovare le correlazioni tra attributi diversi in un set di dati. L'applicazione più comune di questo tipo di algoritmo è costituita dall'utilizzo per la creazione di regole di associazione, che è possibile utilizzare in Market basket analysis.  
  
-   **Algoritmi di analisi delle sequenze** riepilogare sequenze o episodi nei dati, ad esempio un flusso di percorso Web frequenti.  
  
 Tuttavia, non esiste alcun motivo per cui sia necessario limitarsi all'utilizzo di un solo algoritmo nelle soluzioni. Analisti esperti utilizzeranno qualche volta un algoritmo per determinare gli input più efficaci, ovvero variabili, quindi applicheranno un algoritmo diverso per stimare un risultato specifico in base a tali dati. Data Mining di SQL Server consente di compilare più modelli in una sola struttura di data mining, pertanto all'interno di una singola soluzione di data mining è possibile utilizzare un algoritmo di clustering, un modello di alberi delle decisioni e un modello Naive Bayes per ottenere viste diverse sui dati. È possibile utilizzare inoltre più algoritmi in una singola soluzione per eseguire attività separate. Ad esempio, è possibile utilizzare la regressione per ottenere previsioni finanziarie e utilizzare un algoritmo della rete neurale per eseguire un'analisi dei fattori che incidono sulle vendite.  
  
### <a name="choosing-an-algorithm-by-task"></a>Scelta di un algoritmo in base all'attività  
 Per facilitare la selezione di un algoritmo da utilizzare con un'attività specifica, nella tabella seguente sono disponibili suggerimenti sui tipi di attività per cui ciascun algoritmo viene utilizzato in modo tradizionale.  
  
|Esempi di attività|Algoritmo Microsoft da utilizzare|  
|-----------------------|---------------------------------|  
|**Stima di un attributo discreto**<br /><br /> Contrassegnare i clienti in un elenco di potenziali acquirenti come buone o scarse possibilità.<br /><br /> Calcolare la probabilità di un errore del server entro i prossimi sei mesi.<br /><br /> Suddividere in categorie i risultati dei pazienti ed esplorare i fattori correlati.|[Algoritmo Microsoft Decision Trees](microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo Microsoft Naive Bayes](microsoft-naive-bayes-algorithm.md)<br /><br /> [Algoritmo Microsoft Clustering](microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo Microsoft Neural Network](microsoft-neural-network-algorithm.md)|  
|**Stima di un attributo continuo**<br /><br /> Prevedere le vendite del prossimo anno.<br /><br /> Stimare i visitatori del sito in base a tendenze storiche passate e stagionali.<br /><br /> Generare un punteggio di rischio in base ai dati demografici.|[Algoritmo Microsoft Decision Trees](microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo Microsoft Time Series](microsoft-time-series-algorithm.md)<br /><br /> [Algoritmo Microsoft Linear Regression](microsoft-linear-regression-algorithm.md)|  
|**Stima di una sequenza**<br /><br /> Eseguire un'analisi clickstream del sito Web di una società.<br /><br /> Analizzare i fattori che portano a un errore del server.<br /><br /> Acquisire e analizzare sequenze di attività durante le visite dei pazienti in uscita, per formulare le procedure consigliate circa le attività comuni.|[Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md)|  
|**Ricerca di gruppi di elementi comuni nelle transazioni**<br /><br /> Utilizzare Market basket analysis per determinare la posizione del prodotto.<br /><br /> Suggerire prodotti aggiuntivi a un cliente per l'acquisto.<br /><br /> Analizzare i dati dei sondaggi provenienti dai visitatori a un evento, per scoprire quali attività o stand fossero correlati, per pianificare le attività future.|[Algoritmo Microsoft Association Rules](microsoft-association-algorithm.md)<br /><br /> [Algoritmo Microsoft Decision Trees](microsoft-decision-trees-algorithm.md)|  
|**Ricerca di gruppi di elementi simili**<br /><br /> Creare gruppi di profili di rischi dei pazienti in base ad attributi quali i dati demografici e i comportamenti.<br /><br /> Analizzare gli utenti esplorando e comprando modelli.<br /><br /> Identificare i server che dispongono di caratteristiche di utilizzo simili.|[Algoritmo Microsoft Clustering](microsoft-clustering-algorithm.md)<br /><br /> [Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
 Nella tabella seguente vengono forniti i collegamenti a risorse didattiche per ognuno degli algoritmi di data mining disponibili in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
|||  
|-|-|  
|**Descrizione dell'algoritmo di base**|Vengono spiegati la funzione e il funzionamento dell'algoritmo nonché descritti i possibili scenari aziendali in cui l'algoritmo potrebbe risultare utile.|  
||[Algoritmo Microsoft Association Rules](microsoft-association-algorithm.md)<br /><br /> [Algoritmo Microsoft Clustering](microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo Microsoft Decision Trees](microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo Microsoft Linear Regression](microsoft-linear-regression-algorithm.md)<br /><br /> [Algoritmo Microsoft Logistic Regression](microsoft-logistic-regression-algorithm.md)<br /><br /> [Algoritmo Microsoft Naive Bayes](microsoft-naive-bayes-algorithm.md)<br /><br /> [Algoritmo Microsoft Neural Network](microsoft-neural-network-algorithm.md)<br /><br /> [Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md)<br /><br /> [Algoritmo Microsoft Time Series](microsoft-time-series-algorithm.md)|  
|**Riferimento tecnico**|Vengono forniti dettagli tecnici sull'implementazione dell'algoritmo, con riferimenti accademici, se necessario. Sono elencati i parametri che è possibile impostare per controllare il comportamento dell'algoritmo e personalizzare i risultati nel modello. Vengono descritti i requisiti dei dati e forniti suggerimenti sulle prestazioni, se possibile.|  
||[Riferimento tecnico per l'algoritmo Microsoft Association Rules](microsoft-association-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Clustering](microsoft-clustering-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Decision Trees](microsoft-decision-trees-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Linear Regression](microsoft-linear-regression-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Logistic Regression](microsoft-logistic-regression-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Naive Bayes](microsoft-naive-bayes-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Neural Network](microsoft-neural-network-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Sequence Clustering](microsoft-sequence-clustering-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Time Series](microsoft-time-series-algorithm-technical-reference.md)|  
|**Contenuto del modello**|Viene spiegato come sono strutturate le informazioni all'interno di ciascun tipo di modello di data mining e viene illustrato come interpretare le informazioni archiviate in ognuno dei nodi.|  
||[Contenuto dei modelli di data mining per i modelli di associazione &#40;Analysis Services - Data mining&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli di clustering &#40;Analysis Services - Data mining&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli di albero delle decisioni &#40;Analysis Services - Data mining&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli di regressione lineare &#40;Analysis Services - Data mining&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli di regressione logistica &#40;Analysis Services - Data mining&#41;](mining-model-content-for-logistic-regression-models.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli Naïve Bayes &#40;Analysis Services - Data mining&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli di rete neurale &#40;Analysis Services - Data mining&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli Sequence Clustering &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-sequence-clustering-models.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli Time Series &#40;Analysis Services - Data mining&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)|  
|**Query di data mining**|Vengono fornite più query che è possibile utilizzare con ogni tipo di modello. Negli esempi sono incluse query contenuto che consentono di acquisire informazioni sui modelli nel modello e query di stima per facilitare la compilazione di stime in base a tali modelli.|  
||[Esempi di query sul modello di associazione](association-model-query-examples.md)<br /><br /> [Esempi di query sul modello di clustering](clustering-model-query-examples.md)<br /><br /> [Esempi di query sul modello di alberi delle decisioni](decision-trees-model-query-examples.md)<br /><br /> [Esempi di query sul modello di regressione lineare](linear-regression-model-query-examples.md)<br /><br /> [Esempi di query sul modello di regressione logistica](logistic-regression-model-query-examples.md)<br /><br /> [Esempi di query sul modello Naive Bayes](naive-bayes-model-query-examples.md)<br /><br /> [Neural Network Model Query Examples](neural-network-model-query-examples.md)<br /><br /> [Esempi di query su modelli Sequence Clustering](sequence-clustering-model-query-examples.md)<br /><br /> [Time Series Model Query Examples](time-series-model-query-examples.md)|  
  
## <a name="related-tasks"></a>Attività correlate  
  
|**Argomento**|**Descrizione**|  
|---------------|---------------------|  
|Determinare l'algoritmo utilizzato da un modello di data mining|[Eseguire query sui parametri usati per creare un modello di data mining](query-the-parameters-used-to-create-a-mining-model.md)|  
|Creare un algoritmo plug-in personalizzato|[Algoritmi plug-in](plugin-algorithms.md)|  
|Esplorare un modello utilizzando un visualizzatore specifico dell'algoritmo|[Visualizzatori modello di data mining](data-mining-model-viewers.md)|  
|Visualizzare il contenuto di un modello utilizzando un formato di tabella generico|[Visualizzare un modello utilizzando Microsoft Generic Content Tree Viewer](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)|  
|Acquisire informazioni sulla configurazione dei dati e sull'utilizzo degli algoritmi per la creazione di modelli|[Strutture di data mining &#40;Analysis Services - Data mining&#41;](mining-structures-analysis-services-data-mining.md)<br /><br /> [Modelli di data mining &#40;Analysis Services - Data mining&#41;](mining-models-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di data mining](data-mining-tools.md)  
  
  
