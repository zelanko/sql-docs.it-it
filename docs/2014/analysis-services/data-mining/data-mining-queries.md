---
title: Query di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- prediction queries [Analysis Services]
- queries [DMX], creating
- prediction queries [DMX]
- Prediction Query Builder
- mining models [Analysis Services], querying
ms.assetid: 802806a6-69bb-4c3c-b9aa-d1a1ddfc7fc2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bfce63f3686f06c0289c818daac82f336fb2b17
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084965"
---
# <a name="data-mining-queries"></a>Query di data mining
  Le query di data mining sono utili per molti scopi. È possibile scegliere:  
  
-   Applicare il modello ai nuovi dati per eseguire una o più stime. È possibile fornire valori di input come parametri o in un batch.  
  
-   Ottenere un riepilogo statistico dei dati utilizzati per il training.  
  
-   Estrarre schemi e regole o generare un profilo del case tipico che rappresenta uno schema nel modello.  
  
-   Estrarre formule di regressione e altri calcoli che consentono di spiegare i modelli.  
  
-   Ottenere i case adatti per uno schema particolare.  
  
-   Recuperare dettagli su singoli case utilizzati nel modello, tra cui i dati non utilizzati nell'analisi.  
  
-   Ripetere il training di un modello aggiungendo nuovi dati o eseguire una stima incrociata.  
  
 In questa sezione viene fornita una panoramica delle informazioni necessarie per iniziare a utilizzare le query di data mining. Vengono descritti i tipi di query che è possibile creare sugli oggetti di data mining, introdotti gli strumenti e i linguaggi delle query, nonché forniti collegamenti a esempi di query che è possibile creare sui modelli compilati utilizzando gli algoritmi disponibili in Data mining di SQL Server.  
  
 [Informazioni sulle query di data mining](#bkmk_Understand)  
  
 [Interfacce e strumenti di query](#bkmk_Interfaces)  
  
 [Query per tipi di modelli diversi](#bkmk_ModelTypes)  
  
 [Requisiti](#bkmk_Reqs)  
  
##  <a name="understanding-data-mining-queries"></a><a name="bkmk_Understand"></a>Informazioni sulle query di data mining  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta i tipi di query seguenti:  
  
-   [Query di stima &#40;Data Mining&#41;](prediction-queries-data-mining.md)  
  
     Query mediante le quali vengono eseguite inferenze in base agli schemi del modello e dai dati di input.  
  
-   [Query sul contenuto &#40;Data mining&#41;](content-queries-data-mining.md)  
  
     Query mediante le quali vengono restituiti metadati, statistiche e altre informazioni sul modello stesso.  
  
-   [Query drill-through &#40;Data mining&#41;](drillthrough-queries-data-mining.md)  
  
     Query mediante le quali è possibile recuperare i dati del case sottostanti per il modello o persino i dati della struttura che non è stata utilizzata nel modello.  
  
-   [Query di definizione dei dati &#40;Data mining&#41;](data-definition-queries-data-mining.md)  
  
     Query mediante le quali non vengono restituite informazioni dal modello, ma piuttosto vengono utilizzate per compilare modelli e strutture o per aggiornare i dati in un modello o una struttura.  
  
 Prima di creare query, è consigliabile acquisire familiarità con le differenze tra i modelli creati con ognuno degli algoritmi di data mining forniti da SQL Server.  
  
-   Visualizzare ed esplorare ogni tipo di modello tramite i visualizzatori di data mining personalizzati forniti per ogni tipo di algoritmo. Per altre informazioni, vedere [Attività e procedure relative al visualizzatore modello di data mining](mining-model-viewer-tasks-and-how-tos.md).  
  
-   Verificare il contenuto di ogni tipo di modello tramite **Microsoft Generic Content Tree Viewer**. Per interpretare queste informazioni, consultare [Contenuto del modello di data mining &#40;Analysis Services - Data mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
##  <a name="query-tools-and-interfaces"></a><a name="bkmk_Interfaces"></a>Interfacce e strumenti di query  
 È possibile compilare in modo interattivo query di data mining tramite uno degli strumenti di query forniti da SQL Server. Il generatore delle query di stima con interfaccia grafica è disponibile sia in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] sia in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se si utilizza il generatore delle query di stima per la prima volta, è consigliabile attenersi ai passaggi descritti in [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md) per acquisire familiarità con l'interfaccia. Per una rapida panoramica dei passaggi, vedere la sezione relativa alla creazione di una Query in [Creare una query di stima utilizzando Generatore query di stima](create-a-prediction-query-using-the-prediction-query-builder.md).  
  
 Il generatore delle query di stima è utile per avviare le query che verranno personalizzate in un secondo momento. È possibile aggiungere facilmente origini dati ed eseguire il relativo mapping alle colonne, quindi passare alla vista DMX e personalizzare la query aggiungendo una clausola WHERE o altre funzioni.  
  
 Una volta acquisita familiarità con i modelli di data mining e con la compilazione di query, queste ultime possono anche essere scritte direttamente tramite DMX (Data Mining Extensions). DMX è un linguaggio di query simile a Transact-SQL che può essere utilizzato da molti client diversi ed è lo strumento ideale per la creazione sia di stime personalizzate sia di query complesse. Per un'introduzione a DMX, vedere [Creazione ed esecuzione di query sui modelli di data mining con DMX: esercitazioni &#40;Analysis Services - Data mining&#41;](../../tutorials/create-query-data-mining-models-dmx-tutorials.md).  
  
 Gli editor DMX sono forniti sia in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] sia in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Il generatore delle query di stima può essere utilizzato anche per avviare le query, quindi per modificare la vista nell'editor di testo e copiare l'istruzione DMX in un altro client. Per ulteriori informazioni, vedere [interfacce di query di data mining](data-mining-query-tools.md).  
  
 È possibile comporre a livello di codice istruzioni DMX e inviarle dal client al server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tramite AMO o XMLA. Tuttavia, DMX è il linguaggio che è necessario utilizzare per creare query su un modello di data mining.  
  
 È inoltre possibile eseguire una query sui metadati, sulle statistiche o su parte del contenuto del modello tramite DMV basate sui set di righe dello schema di data mining. Queste DMV facilitano il recupero delle informazioni sul modello tramite la digitazione di istruzioni SELECT; tuttavia non è possibile creare stime. Per altre informazioni sulle DMV supportate da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Utilizzare DMV per monitorare Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md).  
  
 Infine, è possibile creare query di data mining da utilizzare nei pacchetti di Integration Services tramite l' [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)o la [Data Mining Query Transformation](../../integration-services/data-flow/transformations/data-mining-query-transformation.md). L'attività del flusso di controllo supporta più tipi di query DMX, mentre la trasformazione del flusso di dati supporta solo le query che vengono utilizzate nei dati del flusso di dati, ovvero le query in cui viene utilizzata la sintassi PREDICTION JOIN.  
  
##  <a name="queries-for-different-model-types"></a><a name="bkmk_ModelTypes"></a> Query per tipi diversi di modelli  
 L'algoritmo utilizzato durante la creazione del modello influenza ampiamente il tipo di informazioni che è possibile ottenere da una query di data mining. Il motivo di tali differenze consiste nel fatto che ogni algoritmo consente di elaborare i dati in modo differente e di archiviare tipi diversi di modelli. Ad esempio, alcuni algoritmi consentono di creare cluster, altri invece alberi. Pertanto, potrebbe essere necessario utilizzare funzioni di stima e di query specifiche, a seconda del tipo di modello in uso.  
  
 Nell'elenco seguente viene fornito un riepilogo delle funzioni che è possibile utilizzare nelle query:  
  
-   **Funzioni di stima generali:** La `Predict` funzione è polimorfica, ovvero funziona con tutti i tipi di modello. Questa funzione consentirà di rilevare automaticamente il tipo di modello in uso. Per tale funzione verrà richiesto di aggiungere ulteriori parametri. Per altre informazioni, vedere [Predict &#40;DMX&#41;](/sql/dmx/predict-dmx).  
  
    > [!WARNING]  
    >  Non tutti i modelli vengono utilizzati per eseguire stime. Ad esempio, è possibile creare un modello di clustering che non dispone di un attributo stimabile. Tuttavia, anche se un modello non dispone di un attributo stimabile, è possibile creare query di stima tramite cui vengono restituiti altri tipi di informazioni utili dal modello.  
  
-   **Funzioni di stima personalizzate:** in ogni tipo di modello è disponibile un set di funzioni di stima progettate per essere utilizzate con gli schemi creati da tale algoritmo.  
  
     Ad esempio, la funzione `Lag` è fornita per i modelli Time Series, per consentire di visualizzare i dati cronologici utilizzati per il modello. Per i modelli di clustering, le funzioni come `ClusterDistance` sono più significative.  
  
     Per ulteriori informazioni sulle funzioni supportate per ogni tipo di modello, vedere i collegamenti seguenti:  
  
    |||  
    |-|-|  
    |[Esempi di query sul modello di associazione](association-model-query-examples.md)|[Algoritmo Microsoft Naive Bayes](microsoft-naive-bayes-algorithm.md)|  
    |[Esempi di query sul modello di clustering](clustering-model-query-examples.md)|[Esempi di query sul modello di rete neurale](neural-network-model-query-examples.md)|  
    |[Esempi di query sul modello di alberi delle decisioni](decision-trees-model-query-examples.md)|[Sequence Clustering Model Query Examples](sequence-clustering-model-query-examples.md)|  
    |[Esempi di query sul modello di regressione lineare](linear-regression-model-query-examples.md)|[Time Series Model Query Examples](time-series-model-query-examples.md)|  
    |[Esempi di query sul modello di regressione logistica](logistic-regression-model-query-examples.md)||  
  
     È anche possibile chiamare le funzioni VBA o creare delle proprie funzioni. Per altre informazioni, vedere [Funzioni &#40;DMX&#41;](/sql/dmx/functions-dmx).  
  
-   **Statistiche generali:** esistono alcune funzioni che possono essere utilizzate con quasi ogni tipo di modello e tramite cui viene restituito un set standard di statistiche descrittive, ad esempio la deviazione standard.  
  
     Ad esempio, tramite la funzione `PredictHistogram` viene restituita una tabella in cui sono elencati tutti gli stati della colonna specificata.  
  
     Per altre informazioni, vedere [Funzioni di stima correlate &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx).  
  
-   **Statistiche personalizzate:** vengono fornite funzioni di supporto aggiuntive per ogni tipo di modello per generare statistiche attinenti all'attività analitica specifica.  
  
     Ad esempio, quando si utilizza un modello di clustering, è possibile utilizzare la funzione `PredictCaseLikelihood` per restituire il punteggio di probabilità associato a un determinato case e a un cluster. Tuttavia, se è stato creato un modello di regressione lineare, sarebbe più utile recuperare il coefficiente e intercettarlo utilizzando una query sul contenuto.  
  
-   **Funzioni relative al contenuto del modello:** il *contenuto* di tutti i modelli viene rappresentato in un formato standardizzato che consente di recuperare le informazioni con una query semplice. È possibile creare query sul contenuto del modello tramite DMX. È anche possibile ottenere alcuni tipi di contenuto del modello utilizzando i set di righe dello schema di data mining.  
  
     Nel contenuto del modello, il significato di ogni riga o nodo della tabella restituito differisce a seconda del tipo di algoritmo utilizzato per compilare il modello, nonché del tipo di dati della colonna. Per altre informazioni, vedere [Query sul contenuto &#40;Data mining&#41;](content-queries-data-mining.md).  
  
##  <a name="requirements"></a><a name="bkmk_Reqs"></a> Requisiti  
 Prima che sia possibile creare una query su un modello, deve essere stato elaborato il modello di data mining. Per l'elaborazione degli oggetti [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono necessarie autorizzazioni speciali. Per altre informazioni sull'elaborazione dei modelli di data mining, vedere [Requisiti e considerazioni sull'elaborazione &#40;data mining&#41;](processing-requirements-and-considerations-data-mining.md).  
  
 Per eseguire query su un modello di data mining sono necessari diversi livelli di autorizzazioni, a seconda del tipo di query in esecuzione. Ad esempio, l'esecuzione del drill-through ai dati del case o della struttura richiede in genere autorizzazioni aggiuntive che possono essere impostate sull'oggetto della struttura o del modello di data mining.  
  
 Tuttavia, se nella query vengono utilizzati dati esterni e sono incluse istruzioni quali OPENROWSET o OPENQUERY, il database sul quale si sta eseguendo una query deve consentire l'abilitazione di queste istruzioni ed è necessario disporre dell'autorizzazione per gli oggetti di database sottostanti.  
  
 Per altre informazioni sui contesti di protezione richiesti per eseguire query di data mining, vedere [Panoramica della sicurezza &#40;data mining&#41;](security-overview-data-mining.md)  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 Negli argomenti di questa sezione viene presentato dettagliatamente ogni tipo di query di data mining e vengono forniti collegamenti a esempi dettagliati di creazione di query sui modelli di data mining.  
  
 [Query di stima &#40;Data Mining&#41;](prediction-queries-data-mining.md)  
  
 [Query sul contenuto &#40;Data mining&#41;](content-queries-data-mining.md)  
  
 [Query drill-through &#40;Data mining&#41;](drillthrough-queries-data-mining.md)  
  
 [Query di definizione dei dati &#40;Data mining&#41;](data-definition-queries-data-mining.md)  
  
 [Interfacce di query di data mining](data-mining-query-tools.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Utilizzare questi collegamenti per informazioni sulla creazione e sull'utilizzo di query di data mining.  
  
|Attività|Collegamenti|  
|-----------|-----------|  
|Visualizzare esercitazioni e procedure dettagliate su query di data mining|[Lezione 6: Creazione e utilizzo di stime &#40;Esercitazione di base sul data mining&#41;](../../tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)<br /><br /> [Esercitazione su DMX per le stime basate su serie temporali](../../tutorials/time-series-prediction-dmx-tutorial.md)|  
|Utilizzare strumenti query di data mining in SQL Server Management Studio e [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|[Creare una query DMX in SQL Server Management Studio](create-a-dmx-query-in-sql-server-management-studio.md)<br /><br /> [Creare una query di stima utilizzando Generatore query di stima](create-a-prediction-query-using-the-prediction-query-builder.md)<br /><br /> [Applicare le funzioni di stima a un modello](apply-prediction-functions-to-a-model.md)<br /><br /> [Modificare manualmente un query di stima](manually-edit-a-prediction-query.md)|  
|Utilizzare i dati esterni presenti nelle query di stima|[Scegliere ed eseguire il mapping di dati di input per una query di stima](choose-and-map-input-data-for-a-prediction-query.md)<br /><br /> [Scegliere ed eseguire il mapping di dati di input per una query di stima](choose-and-map-input-data-for-a-prediction-query.md)|  
|Utilizzo dei risultati delle query|[Visualizzare e salvare i risultati di una query di stima](view-and-save-the-results-of-a-prediction-query.md)|  
|Utilizzare modelli di query DMX e XMLA forniti in Management Studio|[Creare una query di stima singleton da un modello](create-a-singleton-prediction-query-from-a-template.md)<br /><br /> [Creare una query di data mining usando XMLA](create-a-data-mining-query-by-using-xmla.md)<br /><br /> [Usare i modelli di Analysis Services in SQL Server Management Studio](../instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|Acquisire ulteriori informazioni sulle query sul contenuto e visualizzare esempi|[Creare una query sul contenuto di un modello di data mining](create-a-content-query-on-a-mining-model.md)<br /><br /> [Eseguire query sui parametri utilizzati per creare un modello di data mining](query-the-parameters-used-to-create-a-mining-model.md)<br /><br /> [Query sul contenuto &#40;Data mining&#41;](content-queries-data-mining.md)|  
|Impostare opzioni di query e risolvere problemi relativi ad autorizzazioni ed errori attinenti alle query|[Modificare il valore di timeout per le query di data mining](data-mining-queries.md)|  
|Utilizzare i componenti di data mining in Integration Services|[Attività Query di data mining](../../integration-services/control-flow/data-mining-query-task.md)<br /><br /> [Query di data mining - trasformazione](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|  
  
## <a name="see-also"></a>Vedi anche  
 [Algoritmi di data mining &#40;Analysis Services-&#41;di data mining](data-mining-algorithms-analysis-services-data-mining.md)   
 [Contenuto dei modelli di data mining &#40;Analysis Services - Data mining&#41;](mining-model-content-analysis-services-data-mining.md)  
  
  
