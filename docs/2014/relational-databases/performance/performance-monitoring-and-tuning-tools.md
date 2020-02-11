---
title: Strumenti per il monitoraggio e l'ottimizzazione delle prestazioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- tools [SQL Server], monitoring performance
- monitoring server performance [SQL Server], tools
- monitoring performance [SQL Server], tools
- database performance [SQL Server], tools
- tuning databases [SQL Server], tools
- database monitoring [SQL Server], tools
- performance [SQL Server], monitoring tools
- server performance [SQL Server], tools
ms.assetid: 31529dfe-68e7-49f7-b3c2-39fcecf33a95
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 179944412ed72bc0055bf5c47b788a3a929e9844
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150827"
---
# <a name="performance-monitoring-and-tuning-tools"></a>Strumenti per il monitoraggio e l'ottimizzazione delle prestazioni
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre un set completo di strumenti per il monitoraggio degli [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eventi in e per l'ottimizzazione della progettazione fisica del database. La scelta dello strumento dipende dal tipo di monitoraggio o di ottimizzazione da eseguire e dagli eventi specifici da monitorare.  
  
 Di seguito sono elencati gli strumenti di monitoraggio e ottimizzazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Strumento|Descrizione|  
|----------|-----------------|  
|[sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)|
  [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] tiene traccia degli eventi di elaborazione del motore, ad esempio l'avvio di un batch o di una transazione, consentendo di monitorare l'attività del server e del database, ad esempio deadlock, errori irreversibili o attività di accesso. È possibile acquisire dati di [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] in un file o una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per poterli analizzare in seguito, nonché riprodurre gli eventi acquisiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] passaggio per passaggio e determinare con esattezza quali eventi hanno avuto luogo.|  
|[SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Riesecuzione distribuita possibile utilizzare più computer per riprodurre dati di traccia, simulando un carico di lavoro di importanza critica.|  
|[Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../performance-monitor/monitor-resource-usage-system-monitor.md)|Monitor di sistema tiene traccia principalmente dell'utilizzo delle risorse, ad esempio il numero corrente di richieste di pagine a Gestione buffer, consentendo di monitorare le prestazioni e l'attività del server tramite oggetti e contatori predefiniti o contatori definiti dall'utente per il monitoraggio degli eventi. Monitoraggio di sistema, Performance Monitor in Microsoft Windows NT 4.0, raccoglie misurazioni e valori piuttosto che dati sugli eventi, ad esempio l'utilizzo della memoria, il numero di transazioni attive, il numero di blocchi bloccati o l'attività della CPU. È possibile impostare le soglie per contatori specifici allo scopo di generare avvisi per la notifica agli operatori.<br /><br /> Monitoraggio di sistema funziona con Microsoft Windows Server e i sistemi operativi Windows. Questo strumento consente di monitorare, in remoto o in locale, un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Windows NT 4.0 o versioni successive.<br /><br /> La principale differenza tra [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] e Monitoraggio di sistema consiste nel fatto che [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] esegue il monitoraggio degli eventi del Motore di database, mentre Monitoraggio di sistema esegue il monitoraggio dell'utilizzo delle risorse associate ai processi del server.|  
|[Aprire Monitoraggio attività &#40;SQL Server Management Studio&#41;](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)|Monitoraggio attività di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è utile per le viste ad hoc dell'attività corrente e consente di visualizzare in formato grafico informazioni relative a:<br /><br /> Processi in esecuzione in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Processi bloccati.<br /><br /> Blocchi.<br /><br /> Attività degli utenti.|  
|[Traccia SQL](../sql-trace/sql-trace.md)|
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] Stored procedure che consentono di creare, filtrare e definire la creazione della traccia:<br /><br /> [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)<br /><br /> [sp_trace_generateevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql)<br /><br /> [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)<br /><br /> [sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)<br /><br /> [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)|  
|Log degli errori|Il registro eventi applicazioni di Windows offre una panoramica complessiva degli eventi generati in Windows Server e nei sistemi operativi Windows, nonché degli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e di ricerca full-text. Questo registro contiene informazioni sugli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non disponibili in altro modo. Tali informazioni possono essere utilizzate per risolvere i problemi relativi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Stored procedure di sistema &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)|Le stored procedure di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seguenti offrono una potente alternativa per molte attività di monitoraggio:<br /><br /> [sp_who &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql): <br />                    Visualizza informazioni snapshot sugli utenti e i processi correnti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluse indicazioni sull'istruzione in esecuzione e sull'eventuale blocco dell'istruzione.<br /><br /> [sp_lock &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-lock-transact-sql): segnala informazioni snapshot sui blocchi, inclusi ID oggetto, ID indice, tipo di blocco e tipo o risorsa a cui si applica il blocco.<br /><br /> [sp_spaceused &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql): Visualizza una stima della quantità corrente di spazio su disco utilizzato da una tabella o da un intero database.<br /><br /> [sp_monitor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-monitor-transact-sql): Visualizza le statistiche, tra cui l'utilizzo della CPU, l'utilizzo di I/O e la quantità di tempo di inattività dopo l'ultima esecuzione di **sp_monitor** .|  
|[DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)|Le istruzioni DBCC (Database Console Command) consentono di controllare le statistiche relative alle prestazioni e la consistenza logica e fisica di un database.|  
|[Funzioni predefinite &#40;Transact-SQL&#41;](/sql/t-sql/functions/functions)|Le funzioni predefinite consentono di visualizzare informazioni statistiche snapshot sull'attività di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dall'avvio del server. Questi dati statistici vengono archiviati in contatori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefiniti. Ad esempio, **@@CPU_BUSY ** contiene la quantità di tempo in cui la CPU ha eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il codice. **@@CONNECTIONS ** contiene il numero di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connessioni o di tentativi di connessione. e **@@PACKET_ERRORS ** contiene il numero di pacchetti di rete che si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verificano nelle connessioni.|  
|[Flag di traccia &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)|I flag di traccia consentono di visualizzare informazioni su un'attività specifica del server e vengono utilizzati per la diagnostica di problemi o inconvenienti relativi alle prestazioni, ad esempio catene di deadlock.|  
|[Database Engine Tuning Advisor](database-engine-tuning-advisor.md)|Ottimizzazione guidata motore di database analizza gli effetti delle prestazioni delle istruzioni di [!INCLUDE[tsql](../../../includes/tsql-md.md)] eseguite sui database che si desidera ottimizzare. Ottimizzazione guidata motore di database offre consigli relativi ad aggiunta, rimozione o modifica di indici, viste indicizzate e partizionamento.|  
  
## <a name="choosing-a-monitoring-tool"></a>Scelta di uno strumento di monitoraggio  
 La scelta dello strumento di monitoraggio dipende dall'evento o dall'attività che si desidera monitorare.  
  
|Evento o attività|SQL Server Profiler|Distributed Replay|Monitor di sistema|Monitoraggio attività|Transact-SQL|Log degli errori|  
|-----------------------|-------------------------|------------------------|--------------------|----------------------|-------------------|----------------|  
|Analisi delle tendenze|Sì||Sì||||  
|Riproduzione di eventi acquisiti|Sì (da un singolo computer)|Sì (da più computer)|||||  
|Monitoraggio ad hoc|Sì|||Sì|Sì|Sì|  
|Generazione di avvisi|||Sì||||  
|Interfaccia grafica|Sì||Sì|Sì||Sì|  
|Utilizzo con applicazioni personalizzate|Sì <sup>1</sup>||||Sì||  
  
 <sup>1</sup> utilizzando [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] le stored procedure di sistema.  
  
## <a name="windows-monitoring-tools"></a>Strumenti di monitoraggio di Windows  
 Nei sistemi operativi Windows e in Windows Server 2003 sono inoltre disponibili gli strumenti di monitoraggio indicati di seguito.  
  
|Strumento|Descrizione|  
|----------|-----------------|  
|Gestione attività|Consente di visualizzare un riepilogo dei processi e delle applicazioni eseguite nel sistema.|  
|Agente Network Monitor|Esegue il monitoraggio del traffico di rete.|  
  
 Per ulteriori informazioni sugli strumenti di Windows Server o dei sistemi operativi Windows, consultare la documentazione di Windows.  
  
  
