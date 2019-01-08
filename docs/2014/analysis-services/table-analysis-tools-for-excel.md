---
title: Strumenti di analisi tabelle per Excel | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- getting started
ms.assetid: 6d9d1481-18e4-4108-9efa-68152b0940c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 596bc66152f36c25169e4a089644042d25f8c13b
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391899"
---
# <a name="table-analysis-tools-for-excel"></a>Strumenti di analisi tabelle per Excel
  Strumenti di data mining nel **Analyze** barra degli strumenti sono il modo più semplice per iniziare a usare il data mining. Ogni strumento analizza automaticamente la distribuzione e il tipo di dati e imposta i parametri per garantire la validità dei risultati. Non è necessario selezionare un algoritmo o configurare parametri complessi.  
  
 ![DM](media/dm-tabletoolsanalyze.gif "DM")  
  
 Il **Analyze** della barra multifunzione include gli strumenti seguenti:  
  
 [Analizza fattori di influenza chiave &#40;strumenti di analisi tabelle per Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 Scegliere un valore della colonna o di output di interesse per consentire all'algoritmo di analizzare tutti i dati di input per identificare i fattori che influiscono maggiormente sulla destinazione. Facoltativamente, è possibile creare un report che confronta due valori qualsiasi in modo da poter visualizzare i cambiamenti dei fattori di influenza.  
  
 Il **analizza fattori di influenza chiave** strumento utilizza l'algoritmo Microsoft Naïve Bayes.  
  
 [Rileva categorie &#40;strumenti di analisi tabelle per Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
 Questo strumento consente di aggiungere un set di dati e di applicare il clustering per trovare i raggruppamenti di dati. È utile per trovare analogie e creare gruppi per analizzare ulteriormente.  
  
 Il **rileva categorie** strumento utilizza l'algoritmo Microsoft Clustering.  
  
 [Estendi da esempio &#40;strumenti di analisi tabelle per Excel&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
 Questo strumento consente di attribuire valori mancanti. Fornire alcuni esempi dei valori mancanti per consentire allo strumento di compilare i modelli in base a tutti i dati nella tabella e quindi di consigliare i nuovi valori in base ai modelli nei dati.  
  
 Il **Estendi da esempio** strumento utilizza l'algoritmo Microsoft Logistic Regression.  
  
 [Prevedere la &#40;strumenti di analisi tabelle per Excel&#41;](forecast-table-analysis-tools-for-excel.md)  
 Questo strumento utilizza dati che cambiano nel tempo ed esegue una stima dei valori futuri.  
  
 Il **previsione** strumento utilizza l'algoritmo Microsoft Time Series.  
  
 [Evidenzia eccezioni &#40;strumenti di analisi tabelle per Excel&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
 Questo strumento analizza i modelli in una tabella di dati e trova le righe e valori che non rientrano nel modello. È quindi possibile esaminarli e correggerli e infine rieseguire il modello o contrassegnare i valori per un'azione successiva.  
  
 Il **evidenzia eccezioni** strumento utilizza l'algoritmo Microsoft Clustering.  
  
 [Ricerca obiettivo &#40;strumenti di analisi tabelle per Excel&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
 Nel **ricerca obiettivo** strumento, si specifica un valore di destinazione e lo strumento identifica i fattori sottostanti che è necessario modificare per soddisfare tale destinazione. Se, ad esempio, si desidera aumentare la soddisfazione chiamate del 20%, è possibile chiedere al modello di eseguire una stima dei fattori da modificare per raggiungere tale obiettivo.  
  
 Il **ricerca obiettivo** strumento utilizza l'algoritmo Microsoft Logistic Regression.  
  
 [Scenario di simulazione &#40;strumenti di analisi tabelle per Excel&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
 Il **analisi di simulazione** strumento integra il **ricerca obiettivo** dello strumento. Immettere nello strumento il valore che si desidera modificare per consentire al modello di stimare se tale modifica sarà sufficiente per il raggiungimento del risultato desiderato. È possibile ad esempio chiedere al modello di determinare se l'aggiunta di un operatore telefonico aumenterebbe la soddisfazione dei clienti di un punto.  
  
 Il **simulazione** strumento utilizza l'algoritmo Microsoft Logistic Regression.  
  
 [Calcolo stime &#40;strumenti di analisi tabelle per Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 Questo strumento consente di creare un modello che analizza i fattori che conducono al risultato di destinazione e quindi stima un risultato per ogni nuovo input, in base alle regole di punteggio derivate dai dati. Inoltre, genera un foglio di lavoro decisionale interattivo che consente di facilitare l'assegnazione del punteggio ai nuovi input. È inoltre possibile creare una versione stampata del foglio di lavoro per l'assegnazione dei punteggi da utilizzare offline.  
  
 Il **calcolo stime** strumento utilizza l'algoritmo Microsoft Logistic Regression.  
  
 [Market Basket Analysis &#40;strumenti di analisi di tabelle per Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
 Questo strumento identifica i modelli che possono essere utilizzati per incentivare le vendite di prodotti correlati. Identifica i gruppi di prodotti frequentemente acquistati insieme e genera i report in base al prezzo e al costo di prodotti correlati per facilitare il processo decisionale.  
  
 Lo strumento non è limitato al Market basket analysis, è possibile applicarlo a qualsiasi problema che si presta all'analisi di associazione. Ad esempio, potrebbe essere necessario cercare gli eventi che spesso si verificano insieme, per fattori che portano a una diagnosi o per qualsiasi altro set di risultati e cause potenziali.  
  
 Il **market Basket Analysis** strumento utilizza l'algoritmo Microsoft Association.  
  
## <a name="requirements-for-the-table-analysis-tools-for-excel"></a>Requisiti di Strumenti di analisi tabelle per Excel  
 Per utilizzare Strumenti di analisi tabelle per Excel, è necessario innanzitutto creare una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Tale connessione consente di accedere agli algoritmi di data mining Microsoft utilizzati per analizzare i dati. Se non è disponibile l'accesso a un'istanza, è consigliabile richiedere all'amministratore di configurare un'istanza che è possibile utilizzare per provare le funzionalità del data mining. Per altre informazioni, vedere [Connetti ai dati di origine &#40;Client di Data Mining per Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Per utilizzare i dati con Strumenti di analisi tabelle, è necessario convertire l'intervallo di dati che si desidera utilizzare in tabelle di Excel.  
  
 Se non è possibile visualizzare il **Analyze** sulla barra multifunzione, provare a fare innanzitutto clic all'interno di una tabella di dati. Il menu viene attivato solo dopo la selezione di una tabella di dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Client di Data Mining per Excel &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)   
 [Risoluzione dei problemi di diagrammi di Visio Data Mining &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)   
 [Elementi inclusi nei componenti aggiuntivi Data mining per Office](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  
