---
title: Creazione di un modello di data mining | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining models, creating
- forecasting [data mining]
- mining models, creating
- clustering [data mining]
- association [data mining]
- data modeling [data mining]
- estimation
- classification [data mining]
ms.assetid: 804b7db3-1f6a-4f73-a81d-bbe02520d7c6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a8893960b5177563ccf98dbd21cb528ce399ea3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086730"
---
# <a name="creating-a-data-mining-model"></a>Creazione di un modello di data mining
  La modellazione dei dati è il passaggio di data mining in cui è possibile creare modelli e tendenze applicando *algoritmi* ai dati. Successivamente è possibile utilizzare tali modelli per l'analisi o per eseguire stime.  
  
 I componenti aggiuntivi Data mining per Office supportano il data mining tramite le procedure guidate che semplificano la creazione di modelli. Le procedure guidate consentono di analizzare i dati, identificare le correlazioni, calcolare il significato statistico di tutte le variabili e selezionare automaticamente il modello migliore.  
  
 Sebbene questa funzionalità sia molto potente quanto gli strumenti data mining forniti da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], la combinazione di procedure guidate e la nota interfaccia di Excel semplifica la creazione, la modifica e l'utilizzo di data mining.  
  
## <a name="advanced-data-mining"></a>Avanzate (Data mining)  
 Le procedure guidate avanzate consentono di creare nuovi modelli di data mining, basati sui dati archiviati in Excel, utilizzando uno degli algoritmi di data mining in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
### <a name="create-mining-structure"></a>Crea struttura di data mining  
 La procedura guidata Crea struttura di data mining consente di compilare una nuova struttura di data mining da utilizzare come base per più modelli di data mining. La procedura guidata consente di riservare una parte dei dati da utilizzare come set di testing, in modo che sia possibile valutare tutti i modelli che utilizzano gli stessi dati in base a standard di test coerenti.  
  
 [Creazione della struttura di data mining &#40;SQL Server i componenti aggiuntivi Data mining&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
### <a name="add-model-to-structure"></a>Aggiunta modello a struttura  
 La procedura guidata Aggiunta modello a struttura consente di scegliere una struttura di data mining esistente e di creare un nuovo modello di data mining per tale struttura. È possibile aggiungere più modelli di data mining a una struttura, modificando i parametri o scegliendo algoritmi di data mining diversi, nonché personalizzare l'output.  
  
 [Aggiunta di un modello alla struttura &#40;componenti aggiuntivi Data mining per Excel&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)  
  
## <a name="analyze-key-influencers-analyze"></a>Analizza fattori di influenza chiave (Analisi)  
 Scegliere un valore della colonna o di output di interesse per consentire all'algoritmo di analizzare tutti i dati di input per identificare i fattori che influiscono maggiormente sulla destinazione. Facoltativamente, è possibile creare un report che confronta due valori qualsiasi in modo da poter visualizzare i cambiamenti dei fattori di influenza.  
  
 Lo strumento **Analizza fattori di influenza chiave** usa l'algoritmo Microsoft Naive Bayes.  
  
 [Analizzare i fattori di influenza chiave &#40;strumenti di analisi tabelle per Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
  
## <a name="associate-data-mining"></a>Associazione (Data mining)  
 La **procedura guidata associazione consente** di compilare un modello di associazione che rileva le associazioni tra gli elementi visualizzati in più transazioni, ad esempio in Market Basket Analysis.  
  
 [Associazione guidata &#40;client di data mining per Excel&#41;](associate-wizard-data-mining-client-for-excel.md)  
  
## <a name="classify-data-mining"></a>Classificazione (Data mining)  
 La procedura guidata **classificazione** compila un modello di classificazione che analizza i fattori che hanno contribuito a un risultato di destinazione. È possibile utilizzare più algoritmi con questa procedura guidata, tra cui Decision Trees, Naive Bayes e Neural Network.  
  
 [Procedura guidata classificazione &#40;componenti aggiuntivi Data mining per Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="cluster-data-mining"></a>Clustering (Data mining)  
 La procedura guidata **cluster** consente di compilare un modello di clustering per rilevare gruppi di righe che condividono caratteristiche simili. Il clustering (talvolta denominato *segmentazione*) è una tecnica di apprendimento non supervisionata molto utile quando si tenta di comprendere i modelli e i raggruppamenti nei nuovi dati.  
  
 L'algoritmo Microsoft Clustering supporta diversi tipi di clustering K-medie ed Expectation Maximization (EM).  
  
 [Creazione guidata Cluster &#40;componenti aggiuntivi Data mining per&#41;Excel ](cluster-wizard-data-mining-add-ins-for-excel.md).  
  
## <a name="detect-categories-analyze"></a>Rileva categorie (Analisi)  
 Lo strumento **Rileva categorie** consente di aggiungere qualsiasi set di dati e di applicare il clustering per trovare i raggruppamenti di dati. È utile per trovare analogie e per creare gruppi da analizzare ulteriormente.  
  
 Lo strumento **Rileva categorie** utilizza l'algoritmo Microsoft Clustering.  
  
 [Rilevare le categorie &#40;strumenti di analisi tabelle per Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
## <a name="estimate-data-mining"></a>Stima (Data mining)  
 La procedura guidata Stima consente di compilare un modello di stima per estrarre modelli di dati e utilizzare tali modelli per stimare valori continui numerici, di data o di ora. Per la creazione del modello viene utilizzato l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Decision Trees.  
  
 [Procedura guidata stima &#40;componenti aggiuntivi Data mining per Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="fill-from-example-analyze"></a>Estendi da esempio (Analisi)  
 Lo strumento **Compila da esempio consente di** imputare i valori mancanti. Fornire alcuni esempi dei valori mancanti per consentire allo strumento di compilare i modelli in base a tutti i dati nella tabella e quindi di consigliare i nuovi valori in base ai modelli nei dati.  
  
 Lo strumento **Compila da esempio** usa l'algoritmo di regressione logistica Microsoft.  
  
 [Da esempio &#40;strumenti di analisi tabelle per Excel&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-analyze"></a>Previsione (Analisi)  
 Lo strumento **previsione** prende i dati che cambiano nel tempo e stima i valori futuri.  
  
 Lo strumento **previsione** utilizza l'algoritmo Microsoft Time Series.  
  
 [Strumenti di analisi tabelle di previsione &#40;per Excel&#41;](forecast-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-data-mining"></a>Previsione (Data mining)  
 La procedura guidata **previsione** consente di compilare un modello di previsione per rilevare modelli in una serie di celle e quindi prevedere valori aggiuntivi.  
  
 [Procedura guidata previsione &#40;componenti aggiuntivi Data mining per Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="highlight-exceptions-analyze"></a>Evidenzia eccezioni (Analisi)  
 Lo strumento **Evidenzia eccezioni** consente di analizzare i modelli in una tabella di dati e di trovare le righe e i valori che non rientrano nel modello. È quindi possibile esaminarli e correggerli e infine rieseguire il modello o contrassegnare i valori per un'azione successiva.  
  
 Lo strumento **Evidenzia eccezioni** utilizza l'algoritmo Microsoft Clustering.  
  
 [Evidenziare le eccezioni &#40;strumenti di analisi tabelle per Excel&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
  
## <a name="prediction-calculator-analyze"></a>Strumento Calcolo stime (Analisi)  
 Questo strumento consente di creare un modello che analizza i fattori che portano ai risultati desiderati e quindi di eseguire la stima di un risultato per un nuovo input, in base ai criteri derivati da questi modelli. Consente inoltre di generare un foglio di lavoro interattivo decisionale che consente di ottenere facilmente nuovi input. È inoltre possibile creare una versione stampata del foglio di lavoro per l'assegnazione dei punteggi da utilizzare offline.  
  
 Lo strumento **Calcolo stime** usa l'algoritmo di regressione logistica Microsoft.  
  
 [Calcolo stime &#40;strumenti di analisi tabelle per Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-goal-seek-analyze"></a>Scenario: Ricerca obiettivo (Analisi)  
 Nello strumento **Ricerca obiettivo** specificare un valore di destinazione e lo strumento identifica i fattori sottostanti che devono essere modificati per soddisfare tale destinazione. Se, ad esempio, si desidera aumentare la soddisfazione chiamate del 20%, è possibile chiedere al modello di eseguire una stima dei fattori da modificare per raggiungere tale obiettivo.  
  
 Lo strumento **Ricerca obiettivo** usa l'algoritmo di regressione logistica Microsoft.  
  
 dettagli  
  
 [Scenario di ricerca obiettivo &#40;strumenti di analisi tabelle per Excel&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-what-if-scenario-analyze"></a>Scenario: Analisi di simulazione (Analisi)  
 Lo strumento **di analisi di** simulazione integra lo strumento **Ricerca obiettivo** . Immettere nello strumento il valore che si desidera modificare per consentire al modello di stimare se tale modifica sarà sufficiente per il raggiungimento del risultato desiderato. È possibile ad esempio chiedere al modello di determinare se l'aggiunta di un operatore telefonico aumenterebbe la soddisfazione dei clienti di un punto.  
  
 Lo strumento **di** simulazione usa l'algoritmo di regressione logistica Microsoft.  
  
 [Scenario di simulazione &#40;strumenti di analisi tabelle per Excel&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="shopping-basket-analysis-analyze"></a>Market basket analysis (Analisi)  
 Lo strumento Market **Basket Analysis** consente di creare gruppi di prodotti che vengono spesso acquistati insieme, per identificare i modelli che possono essere utilizzati per le vendite incrociate o le vendite. Consente inoltre di generare report in base al prezzo e al costo di prodotti correlati per agevolare le decisioni.  
  
 È inoltre possibile utilizzare questo strumento per gli eventi che spesso si verificano insieme, per fattori che portano a una diagnosi o per qualsiasi altro set di risultati e cause potenziali.  
  
 Lo strumento Market **Basket Analysis** utilizza l'algoritmo Microsoft Association Rules.  
  
 [Shopping Basket Analysis &#40;Table AnalysisTools per Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Esplorazione e pulizia dei dati](exploring-and-cleaning-data.md)   
 [Convalida di modelli e utilizzo di modelli per la stima &#40;componenti aggiuntivi Data mining per Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Distribuzione e scalabilità di modelli di data mining &#40;componenti aggiuntivi Data mining per Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
