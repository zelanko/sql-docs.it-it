---
title: Client di data mining per Excel (SQL Server componenti aggiuntivi Data mining) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Data Mining Client
- wizards
- getting started
ms.assetid: e075e2de-11cc-4f71-9603-0b161bca8a24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c2f11ecbdf90aeeb5e0e5a3ef097152898042d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086426"
---
# <a name="data-mining-client-for-excel-sql-server-data-mining-add-ins"></a>Client di data mining per Excel (componenti aggiuntivi Data mining di SQL Server)
  Il client di data mining per Excel è un set di strumenti che consentono di eseguire attività comuni di data mining, dalla pulizia dei dati alla compilazione dei modelli e alle query di stima. È possibile utilizzare i dati in intervalli o tabelle di Excel o accedere alle origini dati esterne.  
  
 ![DM](media/dm-tabletools.gif "DM")  
  
-   [Usare i dati](#bkmk_Data)  
  
     Caricare i dati in Excel ed effettuarne la pulizia, verificare la presenza di outlier e creare riepiloghi statistici. È inoltre possibile eseguire diversi tipi di campionamento, profilare i dati e testare i modelli utilizzando dati esterni. Il client di data mining costituisce il modo più semplice per preparare i dati per l'analisi senza script o processi ETL complessi.  
  
-   [Compilazione di modelli e analisi](#bkmk_Model)  
  
     Questi strumenti offrono le interfacce delle procedure guidate per gli algoritmi di data mining noti ed empiricamente testati, incluso il clustering (k-medie ed EM), l'analisi di associazione, l'analisi delle serie temporali e gli alberi delle decisioni. Le opzioni di modellazione avanzate per ogni procedura guidata consentono di selezionare algoritmi diversi, quali Naïve Bayes o reti neurali, e personalizzare il comportamento, ad esempio le dimensioni iniziali del campionamento o del seeding del cluster.  
  
     Tutti gli algoritmi di data mining sono ospitati in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], rendendo la compilazione di modelli complessi ancora più efficace.  
  
-   [Test, query e convalida di modelli](#bkmk_Validate)  
  
     Il client di data mining fornisce strumenti standard del settore per testare i modelli, inclusi i grafici di accuratezza e la convalida incrociata. Le procedure guidate vengono fornite per semplificare il test della validità del set di dati e della relativa accuratezza. La procedura guidata Query consente di compilare le query per utilizzare i modelli per la stima e l'assegnazione dei punteggi.  
  
-   [Visualizza modelli](#bkmk_ViewModels)  
  
     I grafici generati dalla maggior parte degli strumenti possono essere salvati direttamente in Excel. Per esplorare i modelli, utilizzare i [modelli di esplorazione in Excel &#40;SQL Server componenti aggiuntivi Data Mining&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md) strumento.  
  
-   [Gestione, documentazione e distribuzione](#bkmk_UsageMgmt)  
  
     Il client di data mining per Excel mantiene una connessione attiva al server, pertanto è possibile salvare il modello di data mining nel server per utilizzarlo per ulteriori prove o per distribuirlo in un server di produzione per una maggiore scalabilità.  
  
##  <a name="bkmk_Data"></a>Usare i dati  
 Il gruppo **Preparazione dati** contiene le procedure guidate seguenti che consentono di analizzare e pulire i dati in preparazione alle attività di data mining. La maggior parte delle procedure guidate consente di separare i dati in set di training e di testing.  
  
 [Esplorare &#40;dati SQL Server componenti aggiuntivi Data mining&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 Per la compilazione e l'archiviazione dei modelli i componenti aggiuntivi supportano le connessioni dati seguenti:  
  
-   Connessione a un server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , per l'archiviazione e l'elaborazione di modelli.  
  
-   Connessioni facoltative a origini dati esterne. È possibile compilare il modello utilizzando qualsiasi tipo di dati che può essere definito come origine dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oppure utilizzando i dati già presenti in Excel.  
  
 [Esplorare &#40;dati SQL Server componenti aggiuntivi Data mining&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 La procedura guidata **Esplorazione dati** consente di conoscere il tipo e la quantità di dati della tabella dati mediante la creazione di un grafico della distribuzione e dei valori delle colonne selezionate, una alla volta.  
  
 [&#40;di dati di esempio SQL Server componenti aggiuntivi Data mining&#41;](sample-data-sql-server-data-mining-add-ins.md)  
 La creazione del tipo appropriato di dati per il training e il testing dei modelli costituisce una parte importante del data mining, ma senza gli strumenti appropriati può rivelarsi un'operazione noiosa. La procedura guidata **Dati di esempio** semplifica l'operazione di suddivisione dei dati utilizzati per un modello in due gruppi, uno per la compilazione del modello e uno per il testing. È possibile utilizzare il campionamento casuale o il sovracampionamento.  
  
 [Calcolo stime &#40;strumenti di analisi tabelle per Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 La procedura guidata **Rimozione outlier** offre diversi strumenti per identificare e gestire in modo appropriato gli outlier. Consente di visualizzare la distribuzione dei valori e la relazione tra gli outlier e gli altri dati fornendo la possibilità di decidere se rimuovere o modificare gli outlier.  
  
 [Calcolo stime &#40;strumenti di analisi tabelle per Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 La procedura guidata **Modifica etichette** consente di creare nuove etichette per i dati per semplificare la comprensione dei risultati dell'analisi. È ad esempio possibile rinominare un intervallo di dati con un nome più descrittivo oppure scegliere un valore rappresentativo nell'elenco.  
  
##  <a name="bkmk_Model"></a>Compilazione di modelli e analisi  
 Le opzioni disponibili nella sezione **Modellazione dati** della barra degli strumenti consentono di derivare modelli dai dati, raggruppare le righe di dati in base ad attributi specifici oppure esplorare le associazioni. Le procedure guidate su questa barra multifunzione degli strumenti sono basate sui potenti algoritmi di data mining disponibili in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Diversamente da strumenti simili inclusi in Strumenti di analisi tabelle per Excel, queste procedure guidate consentono di personalizzare il comportamento dell'algoritmo e di utilizzare un'ampia gamma di origini dati.  
  
 [Procedura guidata classificazione &#40;componenti aggiuntivi Data mining per Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
 La procedura guidata **Classificazione** consente di generare un modello di classificazione in base a dati esistenti di una tabella di Excel, un intervallo di Excel o un'origine dati esterna. Un modello di classificazione consente di estrarre modelli dai dati che indicano somiglianze e di eseguire stime basate su raggruppamenti di valori. È possibile utilizzare un modello di classificazione, ad esempio, per stimare i rischi in base ai modelli di ricavo o costi.  
  
 La procedura guidata **Classificazione**  supporta l'uso di questi algoritmi di data mining di Microsoft: Decision Trees, Logistic Regression, Naïve Bayes, Neural Networks.  
  
 [Procedura guidata stima &#40;componenti aggiuntivi Data mining per Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
 La procedura guidata **Valutazione** consente di creare un modello di valutazione. Un modello di valutazione consente di estrarre modelli dai dati e di utilizzarli per stimare un risultato numerico come valuta, importo delle vendite, data o ora.  
  
 La procedura guidata **Valutazione** utilizza questi algoritmi di data mining di Microsoft: Decision Trees, Linear Regression, Logistic Regression e Neural Networks.  
  
 [Analizzare i fattori di influenza chiave &#40;strumenti di analisi tabelle per Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 Le procedura guidata Cluster consente di compilare un modello di clustering. Un modello di clustering consente di rilevare gruppi di righe che condividono caratteristiche simili. Questa procedura guidata è utile per esplorare i modelli in qualsiasi tipo di dati.  
  
 La procedura guidata **Cluster** utilizza l'algoritmo Microsoft Clustering, che include sia k-medie che EM.  
  
 [Associazione guidata &#40;client di data mining per Excel&#41;](associate-wizard-data-mining-client-for-excel.md)  
 La procedura guidata **Associazione** consente di creare un modello di data mining utilizzando l'algoritmo Microsoft Association Rules, che rileva gli elementi o gli eventi che si verificano spesso contemporaneamente. Questo tipo di modello di associazione risulta particolarmente utile per generare suggerimenti e indicazioni.  
  
 La procedura guidata **Associazione** utilizza l'algoritmo Microsoft Association Rules.  
  
 [Procedura guidata previsione &#40;componenti aggiuntivi Data mining per Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
 La procedura guidata **previsione** consente di stimare i valori in una serie temporale. In genere, i dati utilizzati nelle previsioni contengono un tipo di serie temporale, indicatore di data o ID sequenza, che è possibile scegliere per derivare i modelli da utilizzare per la stima di valori futuri.  
  
 La procedura guidata **Previsione** utilizza l'algoritmo Microsoft Time Series.  
  
 [Modellazione avanzata &#40;componenti aggiuntivi Data mining per Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)  
 Se si ha già familiarità con il data mining, è possibile utilizzare le opzioni di modellazione dati **Avanzate** per creare strutture dei dati personalizzate e compilare modelli utilizzando le personalizzazioni non incluse negli altri strumenti e procedure guidate.  
  
##  <a name="bkmk_Validate"></a>Test, query e convalida di modelli  
 Utilizzare le procedure guidate sulla barra degli strumenti **Accuratezza e convalida** per utilizzare test standard del settore per la convalida dell'accuratezza dei modelli e per la valutazione dell'affidabilità del set di dati per la creazione di modelli.  
  
 [Analizzare i fattori di influenza chiave &#40;strumenti di analisi tabelle per Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 Consente di valutare le prestazioni di un modello di data mining tramite la generazione di un grafico di accuratezza o di una grafico a dispersione.  
  
 [Matrice di classificazione &#40;SQL Server i componenti aggiuntivi Data mining&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
 Consente di valutare le prestazioni di un modello di classificazione tramite la creazione di un grafico di riepilogo delle stime accurate e non accurate effettuate dal modello.  
  
 [Grafico dei profitti &#40;SQL Server componenti aggiuntivi Data mining&#41;](profit-chart-sql-server-data-mining-add-ins.md)  
 Consente di capire l'impatto di un modello di data mining tramite la rappresentazione grafica dell'accuratezza delle stime insieme ai costi e ai vantaggi delle azioni intraprese in base alla stima.  
  
 [Convalida incrociata &#40;SQL Server componenti aggiuntivi Data mining&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
 Consente di creare un report in cui è riepilogata l'accuratezza del modello in più sottoinsiemi del set di dati, in modo che sia possibile determinare la stabilità del modello.  
  
 I dati disponibili in una tabella di Excel possono inoltre essere utilizzati come input per query di stima da eseguire su un modello di data mining archiviato nel server.  
  
 [&#40;di query SQL Server componenti aggiuntivi Data mining&#41;](query-sql-server-data-mining-add-ins.md)  
 La procedura guidata **Query** consente di creare stime in base a un modello di data mining esistente.  
  
 [Editor avanzato query di data mining](advanced-data-mining-query-editor.md)  
 Per gli utenti esperti, questo strumento fornisce un'interfaccia di trascinamento a DMX. È possibile creare facilmente query di stima o nuovi modelli senza preoccuparsi della sintassi.  
  
##  <a name="bkmk_ViewModels"></a>Visualizza modelli  
 I modelli creati vengono automaticamente aperti per l'esplorazione. Tuttavia, è possibile esplorare i modelli nel server e generare nuove visualizzazioni. Utilizzare [Forme di Visio](viewing-data-mining-models-in-visio-data-mining-add-ins.md) per esportare i diagrammi di modello in un'area di disegno personalizzabile.  
  
 [Esplorazione di modelli in Excel &#40;SQL Server componenti aggiuntivi Data mining&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
 Visualizzare i modelli creati utilizzando i grafici interattivi personalizzati in ogni tipo di modello.  
  
 [Documentazione di modelli di data mining &#40;componenti aggiuntivi Data mining per Excel&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)  
 Questa procedura guidata consente di creare report che forniscono un riepilogo statistico del set di dati e dei metadati relativi al modello, per semplificare l'analisi e l'interpretazione.  
  
##  <a name="bkmk_UsageMgmt"></a>Gestire, documentare e distribuire  
 Questi strumenti consentono di connettersi a un server di data mining nonché di gestire ed esportare modelli e di monitorare l'attività di data mining.  
  
 [Gestire i modelli &#40;SQL Server componenti aggiuntivi Data mining&#41;](manage-models-sql-server-data-mining-add-ins.md)  
 Se si dispone delle autorizzazioni appropriate, è possibile eliminare, modificare, rinominare o elaborare modelli e strutture di data mining esistenti senza uscire da Excel.  
  
 [Traccia &#40;client di data mining per Excel&#41;](trace-data-mining-client-for-excel.md)  
 Fare clic su **Traccia** per visualizzare un'acquisizione in esecuzione dell'interazione tra il client di Excel e il server [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Tutte le attività vengono archiviate come istruzioni DMX o XMLA in modo da poter risolvere eventuali problemi della sessione di data mining o salvare le informazioni per riutilizzarle in seguito.  
  
 [Connessione al server di data mining](connect-to-a-data-mining-server.md)  
 Per utilizzare Excel come client di data mining, è necessario stabilire una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Tale connessione consente di accedere al motore di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Se si dispone delle autorizzazioni appropriate, tramite la connessione è inoltre possibile archiviare gli eventuali modelli individuati e modificare oggetti di data mining esistenti.  
  
 Sulla barra degli strumenti **Connessioni** sono disponibili procedure guidate per la gestione delle connessioni a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Per utilizzare gli algoritmi e gli strumenti di data mining, è necessario stabilire una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . È possibile creare la connessione durante l'installazione del componente aggiuntivo o aggiungere una connessione in un secondo momento.  
  
 **Per iniziare**  
 Fare clic sul pulsante **Riquadro attività iniziale** per avviare la configurazione guidata che consente di eseguire in modo semplificato il processo di creazione di una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]e di ottenere le autorizzazioni necessarie per il data mining.  
  
 **Guida**  
 Il menu a discesa **?** fornisce collegamenti alla Guida, a siti Web e a una configurazione guidata per il completamento dell'installazione e l'avvio del data mining.  
  
 Nella pagina della Guida sono inoltre presenti collegamenti a risorse online, inclusa la Guida per il componente aggiuntivo, e ulteriori video, demo ed esempi.  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)   
 [Risoluzione dei problemi relativi ai diagrammi di data mining di Visio &#40;componenti aggiuntivi Data mining di SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
