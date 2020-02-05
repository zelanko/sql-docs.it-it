---
title: Monitorare l'utilizzo delle risorse (Monitor di sistema) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server], resource usage
- System Monitor [SQL Server], about Windows System Monitor
- resource usage monitoring [SQL Server]
- System Monitor [SQL Server]
- counters [SQL Server], resource usage subjects
- performance counters [SQL Server], resource usage subjects
- Windows System Monitor [SQL Server], about Windows System Monitor
- monitoring [SQL Server], server resource usage
- monitoring resource usage [SQL Server]
- Windows System Monitor [SQL Server]
- database monitoring [SQL Server], resource usage
- database performance [SQL Server], resource usage
- tuning databases [SQL Server], resource usage
- server performance [SQL Server], resource usage
ms.assetid: f2993a28-0b81-46f2-aec0-6877fe990387
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 02d42e48116e893c6bf7d04c2027762555be06f2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68090998"
---
# <a name="monitor-resource-usage-system-monitor"></a>Monitoraggio dell'utilizzo delle risorse (Monitor di sistema)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se si utilizza un sistema operativo server Microsoft Windows, è possibile misurare le prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mediante lo strumento grafico Monitoraggio di sistema. È possibile visualizzare oggetti e contatori delle prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , nonché funzioni di altri oggetti ad esempio processori, memoria, cache, thread e processi. A ognuno di questi oggetti è associato un set di contatori che misurano l'utilizzo dei dispositivi, le lunghezze delle code, i ritardi e altri indicatori di velocità effettiva e congestione interna.  
  
> [!NOTE]  
>  Monitoraggio di sistema sostituisce Performance Monitor nelle versioni successive a Windows NT 4.0.  
  
## <a name="benefits-of-system-monitor"></a>Vantaggi di Monitoraggio di sistema  
 Monitoraggio di sistema consente di monitorare contemporaneamente i contatori del sistema operativo Windows e di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] allo scopo di determinare correlazioni tra le prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Windows. Ad esempio, il monitoraggio parallelo dei contatori di I/O del disco di Windows e dei contatori Gestione buffer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di ottenere una panoramica del funzionamento globale del sistema.  
  
 Monitoraggio di sistema consente di ottenere statistiche sulle attività e le prestazioni correnti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Tramite Monitoraggio di sistema è possibile:  
  
-   Visualizzare i dati simultaneamente da più computer.  
  
-   Visualizzare e modificare i grafici in modo da riflettere l'attività corrente e mostrare i valori dei contatori aggiornati in base alla frequenza specificata dall'utente.  
  
-   Esportare i dati di grafici, log, log degli avvisi e report in applicazioni di foglio di calcolo o di database per modificarli e stamparli.  
  
-   Aggiungere avvisi di sistema che visualizzano un evento del log degli avvisi e avvertono l'amministratore inviando un avviso di rete.  
  
-   Eseguire un'applicazione specifica la prima volta o ogni volta che il valore di un contatore è superiore o inferiore a un valore definito dall'utente.  
  
-   Creare file di log contenenti dati relativi a vari oggetti di diversi computer.  
  
-   Aggiungere a un file le sezioni selezionate in altri file di log per creare un archivio a lungo termine.  
  
-   Visualizzare i report relativi all'attività corrente o creare report dai file di log esistenti.  
  
-   Salvare le impostazioni di un grafico, avviso, log o report o dell'intera area di lavoro per poterle riutilizzare in seguito.  
  
    > [!NOTE]  
    >  Monitoraggio di sistema ha sostituito Performance Monitor dopo Windows NT 4.0. Per tali attività è possibile utilizzare sia Monitoraggio di sistema che Performance Monitor.  
  
## <a name="system-monitor-performance"></a>Prestazioni di Monitoraggio di sistema  
 Il monitoraggio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e del sistema operativo Microsoft Windows per la verifica delle prestazioni viene eseguito per esaminare innanzitutto tre aspetti fondamentali:  
  
-   Attività del disco  
  
-   Utilizzo del processore  
  
-   Utilizzo della memoria  
  
 Il monitoraggio di un computer in cui è in esecuzione Monitoraggio di sistema può determinare un lieve peggioramento delle prestazioni del computer monitorato. Per questo motivo, è consigliabile registrare i dati generati da Monitoraggio di sistema in un altro disco o computer in modo da limitare il carico di lavoro sul computer monitorato oppure eseguire Monitoraggio di sistema da un computer remoto. È inoltre consigliabile monitorare solo i contatori a cui si è interessati. Se il numero dei contatori monitorati è eccessivamente elevato, al processo di monitoraggio verrà aggiunto l'overhead dell'utilizzo delle risorse, che può influire sulle prestazioni del computer monitorato.  
  
## <a name="system-monitor-tasks"></a>Attività di Monitoraggio di sistema  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Viene descritto quando utilizzare Monitoraggio di sistema e ne viene illustrato l'impatto sulle prestazioni.|[Eseguire Monitoraggio di sistema](../../relational-databases/performance-monitor/run-system-monitor.md)|  
|Viene descritto come monitorare i contatori dei dischi per determinare l'attività dei dischi e la quantità di operazioni di I/O generate dai componenti di SQL Server.|[Monitorare l'uso del disco](../../relational-databases/performance-monitor/monitor-disk-usage.md)|  
|Viene descritto come monitorare un'istanza di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per verificare che i valori di utilizzo della CPU rientrino in intervalli normali.|[Monitorare l'uso della CPU](../../relational-databases/performance-monitor/monitor-cpu-usage.md)|  
|Viene descritto come monitorare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per verificare che l'utilizzo della memoria rientri negli intervalli standard.|[Monitorare l'uso della memoria](../../relational-databases/performance-monitor/monitor-memory-usage.md)|  
|Viene descritto come creare un avviso generato nel momento in cui viene raggiunto un valore soglia di un contatore di Monitoraggio di sistema.|[Creare un avviso del database di SQL Server](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)|  
|Viene descritto come creare grafici, avvisi, log e report per monitorare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Creare grafici, avvisi, log e report](../../relational-databases/performance-monitor/create-charts-alerts-logs-and-reports.md)|  
|Vengono elencati oggetti e contatori utilizzati da Monitoraggio di sistema per monitorare le attività nei computer che eseguono un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Usare oggetti di SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md)|  
|Vengono elencati oggetti e contatori utilizzati da Monitoraggio di sistema per monitorare le attività OLTP in memoria.|[Contatori delle prestazioni XTP &#40;OLTP in memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)|  
  
  
