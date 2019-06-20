---
title: Scenario dell'esercitazione di Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2f5b1a42-b814-4d7d-b603-5383d9ac66b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 323c98b56e2d77c529fb2adf913b15e51bd77900
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062436"
---
# <a name="analysis-services-tutorial-scenario"></a>Scenario di Analysis Services Tutorial
  Questa esercitazione si riferisce alla società fittizia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] è una multinazionale che produce e commercializza biciclette in acciaio e in materiali compositi sui mercati dell'America del Nord, dell'Europa e dell'Asia. La sede centrale di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] si trova a Bothell, nello stato di Washington, e vi lavorano 500 dipendenti. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] dispone inoltre di numerosi team di vendita dislocati nelle diverse aree di mercato.  
  
 Negli ultimi anni [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] ha acquistato un piccolo impianto di produzione in Messico, Importadores Neptuno, presso il quale vengono realizzati diversi componenti di assemblaggio essenziali per la gamma di prodotti di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] . Tali componenti vengono quindi consegnati alla sede di Bothell per l'assemblaggio finale dei prodotti. Nel 2005, tutte le attività di produzione e distribuzione relative al gruppo di prodotti delle biciclette da turismo sono state concentrate nell'impianto Importadores Neptuno.  
  
 Dopo un anno di esercizio particolarmente favorevole, la società [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] intende ora ampliare la sua quota di mercato puntando sull'invio di messaggi pubblicitari mirati ai clienti migliori, sull'incremento della disponibilità dei prodotti tramite un sito Web esterno e sulla riduzione dei prezzi di vendita ottenuto grazie a un abbattimento dei costi di produzione.  
  
## <a name="current-analysis-environment"></a>Ambiente di analisi attuale  
 Per supportare la necessità di analisi dei dati dei reparti vendite e marketing nonché della direzione, la società attualmente estrae i dati transazionali dal database [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] e le informazioni non transazionali, come ad esempio gli obiettivi di vendita, da fogli di calcolo. Tali informazioni vengono poi consolidate nel data warehouse relazionale **AdventureWorksDW2012** . Il data warehouse, tuttavia, presenta i seguenti problemi:  
  
-   I report sono statici. Gli utenti non possono esplorare i dati in modo interattivo nei report per ottenere informazioni più dettagliate, come è invece possibile fare utilizzando una tabella pivot di [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel. Sebbene il set di report predefiniti esistente si riveli sufficiente per molti utenti, gli utenti più esperti devono disporre di accesso diretto alle query del database per generare query interattive e report specializzati. Data la complessità del database **AdventureWorksDW2012** , tali utenti, tuttavia, impiegano una quantità eccessiva di tempo per capire come creare query efficienti.  
  
-   Le prestazioni delle query sono estremamente variabili. Alcune query, ad esempio, restituiscono i risultati molto rapidamente, in pochi secondi, mentre altre impiegano molti minuti.  
  
-   Le tabelle di aggregazione sono difficili da gestire. Per migliorare i tempi di risposta alle query, il team del data warehouse di [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] ha compilato numerose tabelle di aggregazione nel database **AdventureWorksDW2012** . Ad esempio, è stata compilata una tabella riepilogativa delle vendite in base al mese. Tuttavia, se da un lato le tabelle di aggregazione consentono di migliorare in modo significativo le prestazioni delle query, l'infrastruttura che mantiene le tabelle nel tempo è fragile e soggetta a errori.  
  
-   La logica per i calcoli complessi è nascosta nelle definizioni dei report ed è di difficile condivisione tra i report. Poiché la logica di business viene generata separatamente per ogni report, le informazioni di riepilogo risultano talvolta diverse tra i report. La direzione non ritiene pertanto totalmente attendibili i report del data warehouse.  
  
-   Gli utenti in unità aziendali diverse sono interessati a diverse modalità di visualizzazione dei dati. I gruppi vengono distratti e confusi da elementi esterni non rilevanti.  
  
-   La logica dei calcoli costituisce un problema di particolare importanza per quanto riguarda la creazione di report specializzati. Poiché è necessario definire la logica dei calcoli separatamente per ogni report, non esiste un controllo centralizzato sulla modalità di definizione di tale logica. Ad esempio, gli utenti pur essendo consapevoli del fatto che è consigliabile utilizzare tecniche statistiche semplici come lo spostamento dei valori medi, non sono in grado tuttavia di creare i calcoli e quindi non utilizzano tali tecniche.  
  
-   È difficile combinare set correlati di informazioni. Le query specializzate che combinano due set di informazioni correlate, ad esempio le vendite e gli obiettivi di vendita, sono di difficile creazione per gli utenti aziendali. Dal momento che tali query superano la capacità massima del database, la società ha chiesto agli utenti di richiedere al team del data warehouse set di dati di argomenti incrociati. Di conseguenza, sono stati definiti solo pochi report predefiniti che consentono di combinare i dati di più argomenti. Non è facile inoltre modificare i report a causa della loro complessità.  
  
-   I report creati negli Stati Uniti riportano principalmente informazioni commerciali. Gli utenti delle filiali al di fuori degli Stati Uniti non concordano con questo tipo di attenzione e desiderano poter visualizzare i report in valute e linguaggi diversi.  
  
-   È difficile controllare le informazioni. L'ufficio finanziario attualmente usa il database **AdventureWorksDW2012** solo come origine dati per l'esecuzione bulk delle query. I dati vengono quindi scaricati in fogli di calcolo separati e viene impiegata una notevole quantità di tempo per preparare i dati ed elaborare i fogli di calcolo. I report finanziari della società sono pertanto difficili da preparare, controllare e gestire.  
  
## <a name="the-solution"></a>Soluzione  
 Il team del data warehouse ha eseguito recentemente una verifica della progettazione del sistema di analisi corrente. La verifica include un'analisi della relazione tra le problematiche correnti e le necessità future. Il team del data warehouse ha concluso che il database **AdventureWorksDW2012** rappresenta un database dimensionale progettato correttamente con dimensioni conformi e chiavi sostitutive. Le dimensioni conformi consento di utilizzare la dimensione in più data mart, ad esempio una dimensione temporale o del prodotto. Le chiavi surrogate sono chiavi artificiali che consentono il collegamento delle tabelle dei fatti e delle dimensioni e che vengono utilizzate per assicurare univocità e il miglioramento delle prestazioni. Il team del data warehouse ha anche determinato che non esistono attualmente problemi significativi relativi al carico e alla gestione delle tabelle di base nel database **AdventureWorksDW2012** . Il team ha pertanto deciso di usare [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per ottenere quanto segue:  
  
-   Rendere disponibile un accesso ai dati unificato tramite un livello di metadati comune per l'esecuzione di analisi e la creazione di report.  
  
-   Semplificare la visualizzazione dei dati accelerando l'attività di sviluppo di query interattive e predefinite nonché di report predefiniti.  
  
-   Creare correttamente query che consentono di combinare i dati di più argomenti.  
  
-   Gestire le aggregazioni.  
  
-   Archiviare e riutilizzare calcoli complessi.  
  
-   Rendere disponibile una versione localizzata per gli utenti aziendali che si trovano al di fuori degli Stati Uniti.  
  
 Nelle lezioni dell'esercitazione su Analysis Services vengono fornite istruzioni sulla compilazione di un database del cubo che soddisfa tutti questi obiettivi. Per iniziare, passare alla prima lezione: [Lezione 1: Creare un nuovo progetto di modello tabulare](lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Modellazione multidimensionale &#40;esercitazione di AdventureWorks&#41;](multidimensional-modeling-adventure-works-tutorial.md)  
  
  
