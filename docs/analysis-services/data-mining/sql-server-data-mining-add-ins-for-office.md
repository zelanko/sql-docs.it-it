---
title: Dati di SQL Server, componenti aggiuntivi Data Mining per Office | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 89986d3c8de4a1cbefbccf285a92a2dc19c6c7aa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151405"
---
# <a name="sql-server-data-mining-add-ins-for-office"></a>Componenti aggiuntivi Data mining di SQL Server per Office 2007

  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Componenti aggiuntivi Data mining di SQL Server per Office è un semplice set di strumenti per l'analisi predittiva che consente l'utilizzo dei dati in Excel al fine di compilare modelli analitici per stima, indicazioni o esplorazione.  
  
> [!IMPORTANT]
> Il componente aggiuntivo data mining di dati per Office non è supportato in Office 2016 o versione successiva.
  
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
 Per altre informazioni, vedere [Elementi inclusi nei componenti aggiuntivi Data mining per Office](http://go.microsoft.com/fwlink/p/?LinkId=616849)  
  
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
  
 A seconda dell'edizione di SQL Server Analysis Services a cui ci si connette, alcuni algoritmi avanzati potrebbero non essere disponibili. Per informazioni, vedere [Funzionalità supportate dalle edizioni di SQL Server 2016](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).  
  
 Per altre informazioni sull'installazione, vedere la pagina nell'area download: [http://www.microsoft.com/download/details.aspx?id=29061](http://www.microsoft.com/download/details.aspx?id=29061)  
  
  
