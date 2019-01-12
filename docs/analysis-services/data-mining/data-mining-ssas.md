---
title: Data Mining (SSAS) | Microsoft Docs
ms.date: 01/09/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 163314576f609d6fc34ba55b05eff841d1361182
ms.sourcegitcommit: 1c01af5b02fe185fd60718cc289829426dc86eaa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/10/2019
ms.locfileid: "54185097"
---
# <a name="data-mining-ssas"></a>Data mining (SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

> [!IMPORTANT]
> Il data mining è deprecato in SQL Server Analysis Services 2017. La documentazione non viene aggiornata per le funzionalità deprecate. Per altre informazioni, vedere [compatibilità con le versioni precedenti di Analysis Services (SQL 2017)](../analysis-services-backward-compatibility-sql2017.md).

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un avanzato sistema per le analisi predittive fin dalla versione 2000 e offre funzionalità di data mining in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La combinazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e Data Mining di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce una piattaforma integrata per le analisi predittive che comprende la pulizia e la preparazione dei dati, il Machine Learning e la creazione di report. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Il data mining include più algoritmi standard, inclusi modelli di clustering EM e K-medie, reti neurali, regressione logistica e regressione lineare, alberi delle decisioni e classificatori Naive Bayes. Tutti i modelli dispongono di visualizzazioni integrate che consentono di sviluppare, ridefinire e valutare i modelli.  L'integrazione del data mining nella soluzione di business intelligence consente di prendere decisioni intelligenti sui problemi complessi.  
  
## <a name="benefits-of-data-mining"></a>Vantaggi del data mining  
 Il data mining (anche denominato analisi predittiva e Machine Learning) usa consolidati principi statistici per individuare modelli nei dati. Applicando gli algoritmi di data mining di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ai dati, è possibile prevedere tendenze, identificare modelli, creare regole e indicazioni, analizzare la sequenza di eventi in set di dati complessi e acquisire nuovi approfondimenti.  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]il data mining è efficace, accessibile e integrato con gli strumenti preferiti dagli utenti per l'analisi e la creazione di report.  
  
## <a name="key-data-mining-features"></a>Caratteristiche principali del data mining  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] In Data Mining di SQL Server sono disponibili le caratteristiche seguenti per il supporto di soluzioni di data mining integrate:  
  
-   Più origini dei dati: È possibile usare qualsiasi origine dati tabulari per data mining, inclusi file di testo e fogli di calcolo. È anche possibile eseguire il processo di data mining di cubi OLAP creati in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Tuttavia, non è possibile usare i dati di un database in memoria.  
  
-   Pulizia dati integrata, gestione dati e generazione di report: in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono disponibili strumenti avanzati per il profiling e la pulizia dei dati. È possibile creare processi ETL per la pulizia dei dati in preparazione per la modellazione e ssISnoversion facilita la ripetizione del training e l'aggiornamento dei modelli.  
  
-   Più algoritmi personalizzabili: Oltre a fornire algoritmi quali quelli di clustering, reti neurali e alberi delle decisioni, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining supporta lo sviluppo di algoritmi plug-in personalizzati.  
  
-   Infrastruttura di test del modello: testare i modelli e i set di dati usando importanti strumenti statistici come la convalida incrociata, le matrici di classificazione, i grafici di accuratezza e a dispersione. Creare e gestire facilmente i set di testing e di training.  
  
-   Esecuzione di query e drill-through: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining fornisce il linguaggio DMX per l'integrazione di query di stima nelle applicazioni. È anche possibile recuperare statistiche dettagliate e schemi dai modelli ed eseguire il drill-through nei dati del case.  
  
-   Strumenti client: oltre agli strumenti di sviluppo e progettazione forniti da SQL Server, è possibile usare i componenti aggiuntivi Data mining per Excel per creare ed esplorare i modelli, nonché per eseguirvi query. In alternativa creare client personalizzati, inclusi i servizi Web.  
  
-   Supporto del linguaggio di scripting e API gestita: tutti gli oggetti di data mining sono completamente programmabili. La generazione di script è possibile tramite MDX, XMLA o le estensioni PowerShell per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Utilizzare il linguaggio DMX (Data Mining Extensions) per eseguire query e generare script velocemente.  
  
-   Sicurezza e distribuzione: tramite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene fornita la sicurezza basata su ruoli, incluse autorizzazioni separate relative al drill-through per i dati del modello e della struttura. Distribuzione semplice di modelli agli altri server, in modo che gli utenti possano accedere agli schemi o effettuare stime  
  
## <a name="in-this-section"></a>In questa sezione  
 Negli argomenti di questa sezione sono illustrate le caratteristiche principali di Data mining di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le attività correlate.  
  
-   [Concetti di data mining](../../analysis-services/data-mining/data-mining-concepts.md)  
  
-   [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
-   [Strutture di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
-   [Modelli di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
-   [Test e convalida &#40;Data mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
-   [Query di data mining](../../analysis-services/data-mining/data-mining-queries.md)  
  
-   [Soluzioni di data mining](../../analysis-services/data-mining/data-mining-solutions.md)  
  
-   [Strumenti di data mining](../../analysis-services/data-mining/data-mining-tools.md)  
  
-   [Architettura di data mining](../../analysis-services/data-mining/data-mining-architecture.md)  
  
-   [Panoramica della sicurezza &#40;data mining&#41;](../../analysis-services/data-mining/security-overview-data-mining.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
