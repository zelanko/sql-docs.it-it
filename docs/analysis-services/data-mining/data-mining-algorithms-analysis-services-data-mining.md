---
title: Algoritmi di Data Mining (Analysis Services - Data Mining) | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55b46feab1170d5db9689e9347a37f7353263791
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68183799"
---
# <a name="data-mining-algorithms-analysis-services---data-mining"></a>Algoritmi di data mining (Analysis Services - Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Un *algoritmo* in data mining (o Machine Learning) è un set di approcci euristici e calcoli che consente di creare un modello dai dati. Per creare un modello, tramite l'algoritmo vengono innanzitutto analizzati i dati forniti, ricercando tipi specifici di modelli o tendenze. I risultati dell'analisi vengono usati dall'algoritmo su più interazioni per definire i parametri ottimali per la creazione del modello di data mining. Questi parametri vengono quindi applicati all'intero set di dati per estrarre modelli utilizzabili e statistiche dettagliate.  
  
 Il modello di data mining creato da un algoritmo con i dati in uso può avere forme diverse, tra cui:  
  
-   Set di cluster con cui viene descritto in che modo i case di un set di dati sono correlati.  
  
-   Albero delle decisioni per la stima di un risultato e per la descrizione della modalità con cui criteri diversi possono incidere su tale risultato.  
  
-   Modello matematico per la previsione delle vendite.  
  
-   Set di regole mediante le quali viene descritto in che modo i prodotti vengono raggruppati in una transazione e le probabilità con cui tali prodotti vengano acquistati insieme.  
  
 Gli algoritmi disponibili in Data mining di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono i metodi più diffusi e consolidati per la derivazione dei modelli dai dati. A titolo di esempio, il clustering K-Means è uno degli algoritmi di clustering meno recenti ed è ampiamente disponibile in molti strumenti diversi e con molte implementazioni e opzioni diverse. Tuttavia, l'implementazione specifica del clustering K-Means usata in Data mining di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stata sviluppata da Microsoft Research e quindi ottimizzata per le prestazioni con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Tutti gli algoritmi di data mining di Microsoft possono essere ampiamente personalizzati e sono completamente programmabili tramite le API fornite. È inoltre possibile automatizzare la creazione, la formazione e la ripetizione del training dei modelli usando i componenti di data mining in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 È possibile usare inoltre algoritmi di terze parti che siano conformi alla specifica OLE DB per il data mining o che consentano lo sviluppo di algoritmi personalizzati registrabili come servizi, quindi usati all'interno del framework Data mining di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="choosing-the-right-algorithm"></a>Scelta dell'algoritmo corretto  
 La scelta dell'algoritmo più appropriato da utilizzare per un'attività analitica specifica può rivelarsi complessa. Sebbene sia possibile utilizzare algoritmi diversi per eseguire la stessa attività aziendale, ogni algoritmo produce un risultato diverso e alcuni algoritmi possono produrre più di un tipo di risultato. È ad esempio possibile usare l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees non solo per le stime ma anche per ridurre il numero di colonne in un set di dati, in quanto l'albero delle decisioni può consentire di identificare colonne che non hanno effetto sul modello di data mining finale.  
  
### <a name="choosing-an-algorithm-by-type"></a>Scelta di un algoritmo in base al tipo  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - Data mining di SQL Server include i tipi di algoritmi seguenti:  
  
-   **Algoritmi di classificazione** che consentono di stimare una o più variabili discrete, in base agli altri attributi del set di dati.  
  
-   **Algoritmi di regressione** che consentono di stimare una o più variabili continue, ad esempio profitto o perdita, in base ad altri attributi del set di dati.  
  
-   **Algoritmi di segmentazione** che consentono di dividere i dati in gruppi, o cluster, di elementi con proprietà simili.  
  
-   **Algoritmi di associazione** che consentono di trovare le correlazioni tra attributi diversi in un set di dati. L'applicazione più comune di questo tipo di algoritmo è costituita dall'utilizzo per la creazione di regole di associazione, che è possibile utilizzare in Market basket analysis.  
  
-   **Algoritmi di analisi delle sequenze** che consentono di riepilogare sequenze o episodi frequenti nei dati, ad esempio una serie di clic in un sito Web o una serie di eventi di log che precedono la manutenzione del computer.  
  
 Tuttavia, non esiste alcun motivo per cui sia necessario limitarsi all'utilizzo di un solo algoritmo nelle soluzioni. Analisti esperti utilizzeranno qualche volta un algoritmo per determinare gli input più efficaci, ovvero variabili, quindi applicheranno un algoritmo diverso per stimare un risultato specifico in base a tali dati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - Data mining di SQL Server consente di compilare più modelli in una sola struttura di data mining, pertanto all'interno di una singola soluzione di data mining è possibile usare un algoritmo di clustering, un modello di alberi delle decisioni e un modello Naïve Bayes per ottenere viste diverse sui dati. È possibile usare inoltre più algoritmi in una singola soluzione per eseguire attività separate. Ad esempio, è possibile usare la regressione per ottenere previsioni finanziarie e usare un algoritmo della rete neurale per eseguire un'analisi dei fattori che incidono sulle previsioni.  
  
### <a name="choosing-an-algorithm-by-task"></a>Scelta di un algoritmo in base all'attività  
 Per facilitare la selezione di un algoritmo da utilizzare con un'attività specifica, nella tabella seguente sono disponibili suggerimenti sui tipi di attività per cui ciascun algoritmo viene utilizzato in modo tradizionale.  
  
|Esempi di attività|Algoritmo Microsoft da utilizzare|  
|-----------------------|---------------------------------|  
|**Stima di un attributo discreto:**<br /><br /> Contrassegnare i clienti in un elenco di potenziali acquirenti come buone o scarse possibilità.<br /><br /> Calcolare la probabilità di un errore del server entro i prossimi sei mesi.<br /><br /> Suddividere in categorie i risultati dei pazienti ed esplorare i fattori correlati.|[Algoritmo Microsoft Decision Trees](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo Microsoft Naive Bayes](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)<br /><br /> [Algoritmo Microsoft Clustering](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo Microsoft Neural Network](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)|  
|**Stima di un attributo continuo:**<br /><br /> Prevedere le vendite del prossimo anno.<br /><br /> Stimare i visitatori del sito in base a tendenze storiche passate e stagionali.<br /><br /> Generare un punteggio di rischio in base ai dati demografici.|[Algoritmo Microsoft Decision Trees](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo Microsoft Time Series](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)<br /><br /> [Algoritmo Microsoft Linear Regression](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)|  
|**Stima di una sequenza:**<br /><br /> Eseguire un'analisi clickstream del sito Web di una società.<br /><br /> Analizzare i fattori che portano a un errore del server.<br /><br /> Acquisire e analizzare sequenze di attività durante le visite dei pazienti in uscita, per formulare le procedure consigliate circa le attività comuni.|[Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)|  
|**Ricerca di gruppi di elementi comuni nelle transazioni:**<br /><br /> Utilizzare Market basket analysis per determinare la posizione del prodotto.<br /><br /> Suggerire prodotti aggiuntivi a un cliente per l'acquisto.<br /><br /> Analizzare i dati dei sondaggi provenienti dai visitatori a un evento, per scoprire quali attività o stand fossero correlati, per pianificare le attività future.|[Algoritmo Microsoft Association Rules](../../analysis-services/data-mining/microsoft-association-algorithm.md)<br /><br /> [Algoritmo Microsoft Decision Trees](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)|  
|**Ricerca di gruppi di elementi simili:**<br /><br /> Creare gruppi di profili di rischi dei pazienti in base ad attributi quali i dati demografici e i comportamenti.<br /><br /> Analizzare gli utenti esplorando e comprando modelli.<br /><br /> Identificare i server che dispongono di caratteristiche di utilizzo simili.|[Algoritmo Microsoft Clustering](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
 La tabella seguente fornisce collegamenti a risorse didattiche per ognuno degli algoritmi di data mining disponibili in Data mining di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|||  
|-|-|  
|**Descrizione dell'algoritmo di base**|Vengono spiegati la funzione e il funzionamento dell'algoritmo nonché descritti i possibili scenari aziendali in cui l'algoritmo potrebbe risultare utile.|  
||[Algoritmo Microsoft Association Rules](../../analysis-services/data-mining/microsoft-association-algorithm.md)<br /><br /> [Algoritmo Microsoft Clustering](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo Microsoft Decision Trees](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo Microsoft Linear Regression](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)<br /><br /> [Algoritmo Microsoft Logistic Regression](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)<br /><br /> [Algoritmo Microsoft Naive Bayes](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)<br /><br /> [Algoritmo Microsoft Neural Network](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)<br /><br /> [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)<br /><br /> [Algoritmo Microsoft Time Series](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)|  
|**Riferimento tecnico**|Vengono forniti dettagli tecnici sull'implementazione dell'algoritmo, con riferimenti accademici, se necessario. Sono elencati i parametri che è possibile impostare per controllare il comportamento dell'algoritmo e personalizzare i risultati nel modello. Vengono descritti i requisiti dei dati e forniti suggerimenti sulle prestazioni, se possibile.|  
||[Riferimento tecnico per l'algoritmo Microsoft Association Rules](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Clustering](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Decision Trees](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Linear Regression](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Logistic Regression](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Naive Bayes](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Neural Network](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Sequence Clustering](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)<br /><br /> [Riferimento tecnico per l'algoritmo Microsoft Time Series](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)|  
|**Contenuto del modello**|Viene spiegato come sono strutturate le informazioni all'interno di ciascun tipo di modello di data mining e viene illustrato come interpretare le informazioni archiviate in ognuno dei nodi.|  
||[Contenuto dei modelli di data mining per i modelli di associazione &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli di clustering &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli di albero delle decisioni &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli di regressione lineare &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli di regressione logistica &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli Naïve Bayes &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli di rete neurale &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli Sequence Clustering &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)<br /><br /> [Contenuto dei modelli di data mining per i modelli Time Series &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)|  
|**Query di data mining**|Vengono fornite più query che è possibile utilizzare con ogni tipo di modello. Negli esempi sono incluse query contenuto che consentono di acquisire informazioni sui modelli nel modello e query di stima per facilitare la compilazione di stime in base a tali modelli.|  
||[Esempi di query sul modello di associazione](../../analysis-services/data-mining/association-model-query-examples.md)<br /><br /> [Esempi di query sul modello di clustering](../../analysis-services/data-mining/clustering-model-query-examples.md)<br /><br /> [Esempi di query sul modello di alberi delle decisioni](../../analysis-services/data-mining/decision-trees-model-query-examples.md)<br /><br /> [Esempi di query sul modello di regressione lineare](../../analysis-services/data-mining/linear-regression-model-query-examples.md)<br /><br /> [Esempi di query sul modello di regressione logistica](../../analysis-services/data-mining/logistic-regression-model-query-examples.md)<br /><br /> [Esempi di query sul modello Naive Bayes](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)<br /><br /> [Neural Network Model Query Examples](../../analysis-services/data-mining/neural-network-model-query-examples.md)<br /><br /> [Esempi di query su modelli Sequence Clustering](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)<br /><br /> [Time Series Model Query Examples](../../analysis-services/data-mining/time-series-model-query-examples.md)|  
  
## <a name="related-tasks"></a>Attività correlate  
  
|**Argomento**|**Descrizione**|  
|---------------|---------------------|  
|Determinare l'algoritmo utilizzato da un modello di data mining|[Eseguire query sui parametri usati per creare un modello di data mining](../../analysis-services/data-mining/query-the-parameters-used-to-create-a-mining-model.md)|  
|Creare un algoritmo plug-in personalizzato|[Algoritmi plug-in](../../analysis-services/data-mining/plugin-algorithms.md)|  
|Esplorare un modello utilizzando un visualizzatore specifico dell'algoritmo|[Visualizzatori modello di data mining](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|Visualizzare il contenuto di un modello utilizzando un formato di tabella generico|[Visualizzare un modello utilizzando Microsoft Generic Content Tree Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)|  
|Acquisire informazioni sulla configurazione dei dati e sull'utilizzo degli algoritmi per la creazione di modelli|[Strutture di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)<br /><br /> [Modelli di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di data mining](../../analysis-services/data-mining/data-mining-tools.md)  
  
  
