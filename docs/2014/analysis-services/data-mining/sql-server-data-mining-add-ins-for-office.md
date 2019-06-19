---
title: Dati di SQL Server, componenti aggiuntivi Data Mining per Office | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c9021a19-2c19-4f0a-a293-5f7e0ac2524c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 10015ac40948c95f8c912ba6fdb71147e50bb880
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082885"
---
# <a name="sql-server-data-mining-add-ins-for-office"></a>Componenti aggiuntivi Data mining di SQL Server per Office 2007
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Componenti aggiuntivi Data mining di SQL Server per Office è un semplice set di strumenti per l'analisi predittiva che consente l'utilizzo dei dati in Excel al fine di compilare modelli analitici per stima, indicazioni o esplorazione.  
  
 Le procedure guidate e gli strumenti per la gestione dei dati nei componenti aggiuntivi forniscono istruzioni dettagliate per le seguenti attività comuni di data mining:  
  
-   **Organizzare e pulire i dati prima della modellazione.** Utilizzare i dati archiviati in Excel o in qualsiasi origine dati di Excel. È possibile creare e salvare le connessioni per riutilizzare le origini dati, ripetere i test o rieseguire il training dei modelli.  
  
-   **Eseguire il profiling, campionare e preparare.** Molti data miner esperti indicano che fino al 70-90 percento di un progetto di data mining viene impiegato per la preparazione dei dati. I componenti aggiuntivi possono eseguire questa attività più velocemente, fornendo le visualizzazioni in Excel e procedure guidate che facilitano l'esecuzione delle seguenti attività comuni:  
  
    -   Analizzare i dati e comprenderne la distribuzione e le relative caratteristiche.  
  
    -   Creare set di training e di testing tramite il campionamento casuale o il sovracampionamento.  
  
    -   Individuare gli outlier e rimuoverli o sostituirli.  
  
    -   Rietichettare i dati per migliorare la qualità dell'analisi.  
  
-   **Analizzare i modelli tramite l'apprendimento supervisionato o non supervisionato.** Utilizzare le procedure guidate semplici da utilizzare per eseguire alcune delle attività di data mining più frequenti, tra cui analisi del clustering, Market basket analysis e previsione.  
  
     Alcuni degli algoritmi di apprendimento automatico noti inclusi nei componenti aggiuntivi sono Naïve Bayes, Logistic Regression, Clustering, Time Series e Neural Network.  
  
     Se non si ha alcuna familiarità con il data mining, utilizzare la procedura guidata **Query** per la compilazione delle query di stima.  
  
     Gli utenti esperti possono compilare le query DMX personalizzate con l' **Editor avanzato query**con trascinamento della selezione o automatizzare le stime usando VBA di Excel.  
  
-   **Documentare e gestire.** Dopo aver creato un set di dati e compilato alcuni modelli, documentare il lavoro e le informazioni essenziali generando un riepilogo statistico dei parametri dei dati e il modello.  
  
-   **Esplorare e visualizzare.** Data mining non è un'attività che può essere completamente automatizzata, è necessario esplorare e comprendere i risultati per intraprendere un'azione significativa. I componenti aggiuntivi semplificano l'esplorazione tramite i visualizzatori interattivi dei modelli di Visio ed Excel che consentono di personalizzare i diagrammi del modello e di esportare i grafici e le tabelle in Excel per ulteriori attività di filtro o modifica.  
  
-   **Distribuire e integrare.** Quando si crea un modello utile, inserito il modello in produzione, usando gli strumenti di gestione per esportare il modello dal server sperimentale in un'altra istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     In alternativa, è possibile lasciare il modello nel server in cui è stato creato, ma aggiornare i dati di training ed eseguire le stime utilizzando script DMX o Integration Services.  
  
     Gli utenti esperti apprezzeranno la funzionalità **Traccia** che consente di visualizzare le istruzioni XMLA e DMX inviate al server.  
  
## <a name="getting-started"></a>Introduzione  
 In questi argomenti vengono fornite informazioni sugli strumenti e sulla procedura di impostazione:  
  
-   [Client di Data Mining per Excel &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](../data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
-   [Strumenti di analisi tabelle per Excel](../table-analysis-tools-for-excel.md)  
  
-   [Forme di data mining per Visio](../data-mining-shapes-for-visio.md)  
  
-   [Connessione al server di data mining](../connect-to-a-data-mining-server.md)  
  
## <a name="support-and-requirements"></a>Supporto e requisiti  
 I componenti aggiuntivi Data mining di SQL Server per Office sono disponibili per il download gratuito. Per utilizzare questi strumenti, è necessario che sia già installata una delle seguenti versioni di Office:  
  
-   Office 2010, versione a 32 bit o a 64 bit  
  
-   Office 2013, versione a 32 bit o a 64 bit  
  
> [!WARNING]  
>  Assicurarsi di scaricare la versione dei componenti aggiuntivi che corrisponde alla versione di Excel.  
  
 Per il corretto funzionamento dei componenti aggiuntivi Data mining è necessaria una connessione a una delle edizioni di SQL Server Analysis Services seguenti:  
  
-   Enterprise  
  
-   Business Intelligence  
  
-   Standard  
  
 A seconda dell'edizione di SQL Server Analysis Services a cui ci si connette, alcuni algoritmi avanzati potrebbero non essere disponibili. Per informazioni, vedere [Funzionalità supportate dalle edizioni di SQL Server 2014](https://msdn.microsoft.com/library/cc645993.aspx).  
  
 Per altre informazioni sull'installazione, vedere la pagina nell'area download: [https://www.microsoft.com/download/details.aspx?id=29061](https://www.microsoft.com/download/details.aspx?id=29061)  
  
  
