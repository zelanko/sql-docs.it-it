---
title: Monitorare i componenti di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: e8f1b16b-ea40-4e12-886c-967ebda4e6e4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9c0534bf3a12aa81a9fc84d0e2c4f82a189748a0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150755"
---
# <a name="monitor-sql-server-components"></a>Monitorare i componenti di SQL Server
  Il monitoraggio è importante perché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce un servizio in un ambiente dinamico. i dati nell'applicazione cambiano, il tipo di accesso richiesto dagli utenti cambia, la modalità di connessione degli utenti cambia. Possono cambiare anche i tipi delle applicazioni che accedono a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in grado di gestire automaticamente le risorse a livello di sistema, quali la memoria e lo spazio su disco, per ridurre al minimo la necessità di ingenti interventi di ottimizzazione manuale a livello di sistema. Il monitoraggio consente agli amministratori di identificare le tendenze delle prestazioni per determinare i casi in cui è necessario apportare modifiche.  
  
 Per monitorare in modo efficiente qualsiasi componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , effettuare le operazioni seguenti:  
  
1.  Determinare gli obiettivi del monitoraggio.  
  
2.  Selezionare lo strumento appropriato.  
  
3.  Identificare i componenti di cui eseguire il monitoraggio.  
  
4.  Selezionare la metrica per tali componenti.  
  
5.  Eseguire il monitoraggio del server.  
  
6.  Analizzare i dati.  
  
 I singoli passaggi sono descritti in dettaglio di seguito.  
  
## <a name="determine-your-monitoring-goals"></a>Individuazione degli obiettivi del monitoraggio  
 Per eseguire in modo efficace il monitoraggio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario identificare chiaramente il motivo del monitoraggio. Di seguito sono riportati alcuni dei possibili motivi:  
  
-   Definire una base di riferimento delle prestazioni.  
  
-   Identificare le variazioni di prestazioni nel tempo.  
  
-   Diagnosticare problemi specifici relativi alle prestazioni.  
  
-   Identificare componenti o processi da ottimizzare.  
  
-   Confrontare l'effetto di diverse applicazioni client in termini di prestazioni.  
  
-   Controllare l'attività degli utenti.  
  
-   Testare un server con carichi diversi.  
  
-   Testare l'architettura del database.  
  
-   Testare i piani di manutenzione.  
  
-   Testare i piani di backup e ripristino.  
  
-   Stabilire i casi in cui è necessario modificare la configurazione hardware.  
  
## <a name="select-the-appropriate-tool"></a>Selezione dello strumento appropriato  
 Dopo aver determinato i motivi per cui eseguire il monitoraggio, è necessario selezionare gli strumenti appropriati per il tipo di monitoraggio scelto. Nell'ambiente operativo Windows e in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è incluso un set completo di strumenti per il monitoraggio dei server in ambienti caratterizzati da un elevato numero di transazioni. Tali strumenti consentono di ottenere informazioni sulla condizione di un'istanza di Motore di database di SQL Server o di un'istanza di SQL Server Analysis Services.  
  
 Di seguito sono riportati gli strumenti disponibili in Windows per il monitoraggio delle applicazioni in esecuzione in un server:  
  
-   Monitor di sistema, che consente di raccogliere e visualizzare dati in tempo reale su attività quali l'utilizzo della memoria, del disco e del processore.  
  
-   Avvisi e registri di prestazioni  
  
-   Gestione attività  
  
 Per ulteriori informazioni sugli strumenti di Windows Server o Windows, vedere la documentazione di Windows.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce gli strumenti seguenti per il monitoraggio dei componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Traccia SQL  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]  
  
-   Distributed Replay Utility  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Monitoraggio attività  
  
-   
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Showplan grafico  
  
-   Stored procedure  
  
-   Comandi DBCC (Database Console Commands)  
  
-   Funzioni predefinite  
  
-   Flag di traccia  
  
 Per altre informazioni sugli strumenti di monitoraggio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Strumenti per il monitoraggio e l'ottimizzazione delle prestazioni](performance-monitoring-and-tuning-tools.md).  
  
## <a name="identify-the-components-to-monitor"></a>Identificazione dei componenti di cui eseguire il monitoraggio  
 Il terzo passaggio della procedura di monitoraggio di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste nell'identificazione dei componenti monitorati. Se, ad esempio, si utilizza [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per tracciare un server, è possibile definire la traccia per raccogliere dati su eventi specifici. È inoltre possibile escludere eventi non applicabili alla situazione corrente.  
  
## <a name="select-metrics-for-monitored-components"></a>Selezione della metrica per i componenti monitorati  
 Dopo aver identificato i componenti di cui eseguire il monitoraggio, è necessario determinarne la metrica. Dopo aver selezionato gli eventi da includere in una traccia, è, ad esempio, possibile scegliere di includere solo i dati specifici sugli eventi. Limitando la traccia ai soli dati pertinenti si ridurranno al minimo le risorse di sistema necessarie per eseguire la traccia.  
  
## <a name="monitor-the-server"></a>Monitoraggio del server  
 Per eseguire il monitoraggio del server, utilizzare lo strumento configurato per la raccolta dei dati. Dopo aver definito una traccia, è, ad esempio, possibile eseguire la traccia per raccogliere i dati sugli eventi generati nel server.  
  
## <a name="analyze-the-data"></a>Analisi dei dati  
 Al termine della traccia, analizzare i dati per verificare se sono stati raggiunti gli obiettivi di monitoraggio. In caso contrario, modificare i componenti o la metrica utilizzati per il monitoraggio del server.  
  
 Di seguito viene descritto il processo di acquisizione dei dati di evento e di utilizzo di tali dati.  
  
1.  Applicare filtri per limitare i dati di evento raccolti.  
  
     La limitazione dei dati di evento consente di concentrarsi sugli eventi pertinenti per lo scenario di monitoraggio. Se, ad esempio, si desidera eseguire il monitoraggio per individuare le query lente, è possibile utilizzare un filtro per monitorare solo le query inviate dall'applicazione, per le quali il tempo di esecuzione è superiore ai 30 secondi in un particolare database. Per altre informazioni, vedere [Impostare un filtro di traccia &#40;Transact-SQL&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md) e [Filtrare eventi in una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md).  
  
2.  Eseguire il monitoraggio degli eventi (acquisizione).  
  
     Non appena viene abilitato, il monitoraggio acquisisce i dati dall'applicazione specificata, dall'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o dal sistema operativo. Se, ad esempio, si esegue il monitoraggio dell'attività del disco tramite Monitor di sistema, vengono acquisiti dati evento quali le letture e le scritture su disco. Questi dati verranno quindi visualizzati sullo schermo. Per altre informazioni, vedere [Monitoraggio dell'utilizzo delle risorse&#40;Monitor di sistema&#41;](../performance-monitor/monitor-resource-usage-system-monitor.md).  
  
3.  Salvare i dati evento acquisiti.  
  
     Il salvataggio dei dati evento acquisiti consente di poterli analizzare in un secondo momento o persino di riprodurli tramite Distributed Replay Utility o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. I dati evento acquisiti vengono salvati in un file che può essere ricaricato e analizzato nello strumento in cui è stato creato in origine. 
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] consente il salvataggio dei dati evento in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il salvataggio dei dati evento acquisiti è importante per la creazione di dati di riferimento per le prestazioni. I dati di riferimento per le prestazioni vengono salvati e utilizzati per il confronto con dati evento più recenti allo scopo di verificare se le prestazioni sono ottimali. Per altre informazioni, vedere [Modelli e autorizzazioni di SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md).  
  
4.  Creare modelli di traccia contenenti le impostazioni specificate per l'acquisizione degli eventi.  
  
     I modelli di traccia includono informazioni specifiche sugli eventi stessi, i dati di evento e i filtri utilizzati per l'acquisizione dei dati. È possibile utilizzare tali modelli per eseguire il monitoraggio di un set di eventi specifico in un secondo momento senza ridefinire gli eventi, i dati di evento e i filtri. Se, ad esempio, si desidera eseguire un monitoraggio frequente del numero di deadlock e degli utenti interessati, è possibile creare un modello per la definizione di tali eventi, dati evento e filtri evento, salvare il modello e quindi riapplicare il filtro in occasione del successivo monitoraggio dei deadlock. 
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] usa modelli di traccia per questo scopo. Per altre informazioni, vedere [Impostare i valori predefiniti per una definizione di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)e [Creare un modello di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md).  
  
5.  Analizzare i dati evento acquisiti.  
  
     Ai fini dell'analisi, i dati evento acquisiti e salvati vengono caricati nell'applicazione utilizzata per l'acquisizione. È, ad esempio, possibile caricare nuovamente in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] una traccia acquisita di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per attività di visualizzazione e analisi. Per altre informazioni, vedere [Visualizzare e analizzare le tracce con SQL Server Profiler](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md).  
  
     L'analisi dei dati di evento consente di individuare gli eventi verificatisi e di determinarne le cause. In base a tali informazioni è possibile apportare modifiche che possono incidere positivamente sulle prestazioni, ad esempio aggiungere memoria, modificare gli indici, risolvere problemi di codifica di istruzioni Transact-SQL o stored procedure e così via, a seconda del tipo di analisi eseguito. È ad esempio possibile utilizzare Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] per analizzare una traccia acquisita di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e creare indicazioni per gli indici sulla base dei risultati.  
  
6.  Riprodurre i dati di evento acquisiti.  
  
     In tal modo è possibile creare una copia di prova dell'ambiente di database da cui sono stati acquisiti i dati e quindi ripetere gli eventi acquisiti così come si sono verificati nel sistema reale. Questa funzionalità è disponibile solo con Distributed Replay Utility o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. È possibile riprodurre gli eventi con la stessa velocità originale, nel modo più rapido possibile (per sottoporre il sistema a condizioni estreme) oppure, come è più probabile, un passaggio per volta per analizzare il sistema dopo ogni singolo evento. La possibilità di analizzare eventi reali in un ambiente di prova consente di evitare danni al sistema di produzione. Per altre informazioni, vedere [Riprodurre le tracce](../../tools/sql-server-profiler/replay-traces.md).  
  
  
