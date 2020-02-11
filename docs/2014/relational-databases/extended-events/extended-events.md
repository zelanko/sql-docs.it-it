---
title: Eventi estesi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server]
- xe
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 485c748aad8b07a5e8b92a02c03d51a82e5f362a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62990699"
---
# <a name="extended-events"></a>Eventi estesi
  Gli eventi estesi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono dotati di un'architettura estremamente scalabile e configurabile che consente agli utenti di raccogliere le informazioni necessarie per diagnosticare o identificare un problema legato alle prestazioni.  
  
 Per ulteriori informazioni sugli eventi estesi, visitare il sito Web [Eventi estesi di SQL Server](https://blogs.msdn.com/b/extended_events/).  
  
## <a name="benefits-of-includessnoversionincludesssnoversion-mdmd-extended-events"></a>Vantaggi degli eventi estesi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Si tratta di un sistema di monitoraggio delle prestazioni leggero in cui vengono utilizzate poche risorse per le prestazioni. Con gli eventi estesi sono disponibili due interfacce utente grafiche (**creazione guidata nuova sessione** e **nuova sessione**) per creare, modificare, visualizzare e analizzare i dati della sessione.  
  
## <a name="extended-events-concepts"></a>Concetti degli eventi estesi  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Gli eventi estesi (eventi estesi) si basano su concetti esistenti, ad esempio un evento o un consumer di eventi, usano i concetti di Event Tracing for Windows e introduce nuovi concetti.  
  
 Nella seguente tabella vengono descritti i concetti negli eventi estesi.  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Pacchetti degli eventi estesi di SQL Server](sql-server-extended-events-packages.md)|Vengono descritti i pacchetti degli eventi estesi che contengono oggetti utilizzati per ottenere ed elaborare dati durante l'esecuzione di una sessione degli eventi estesi.|  
|[Destinazioni degli eventi estesi di SQL Server](../../database-engine/sql-server-extended-events-targets.md)|Vengono descritti i consumer di eventi che possono ricevere dati durante una sessione dell'evento.|  
|[Motore degli eventi estesi di SQL Server](sql-server-extended-events-engine.md)|Viene descritto il motore che implementa e gestisce una sessione degli eventi estesi.|  
|[Sessioni Eventi estesi di SQL Server](sql-server-extended-events-sessions.md)|Viene descritta la sessione Eventi estesi.|  
  
## <a name="extended-events-architecture"></a>Architettura degli eventi estesi  
 Gli eventi estesi (Eventi estesi) costituiscono un sistema generale di gestione degli eventi per sistemi server. L'infrastruttura degli eventi estesi supporta la correlazione di dati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e in certe condizioni, la correlazione di dati dal sistema operativo e dalle applicazioni di database. Nel secondo caso, l'output degli eventi estesi deve essere indirizzato a ETW (Event Tracing for Windows) per correlare i dati degli eventi con i dati degli eventi delle applicazioni o del sistema operativo.  
  
 In tutte le applicazioni sono presenti punti di esecuzione utili sia all'interno che all'esterno di un'applicazione. All'interno dell'applicazione, l'elaborazione asincrona può essere accodata utilizzando informazioni raccolte durante l'esecuzione iniziale di un'attività. All'esterno dell'applicazione, i punti di esecuzione forniscono utilità di monitoraggio con informazioni sulle caratteristiche relative al funzionamento e alle prestazioni dell'applicazione monitorata.  
  
 Gli eventi estesi supportano l'utilizzo di dati degli eventi all'esterno di un processo. Questi dati sono in genere utilizzati da:  
  
-   strumenti di analisi, ad esempio Traccia SQL e il Monitoraggio di sistema.  
  
-   strumenti di log, ad esempio il registro eventi di Windows o il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Utenti che amministrano un prodotto o sviluppano applicazioni su un prodotto.  
  
 Gli aspetti chiave della progettazione degli eventi estesi sono i seguenti:  
  
-   Il motore degli eventi estesi è agnostico in termini di eventi. In questo modo, il motore è in grado di associare qualsiasi evento a qualsiasi destinazione perché il motore non è vincolato al contenuto dell'evento. Per ulteriori informazioni sul motore degli eventi estesi, vedere [SQL Server Extended Events Engine](sql-server-extended-events-engine.md).  
  
-   Gli eventi sono separati dai consumer di eventi chiamati *destinazioni* negli eventi estesi. Ciò significa che qualsiasi destinazione può ricevere qualsiasi evento. Inoltre, qualsiasi evento generato può essere utilizzato automaticamente dalla destinazione, che può scrivere nel log o fornire un contesto dell'evento supplementare. Per ulteriori informazioni, vedere [SQL Server Extended Events Targets](../../database-engine/sql-server-extended-events-targets.md).  
  
-   Gli eventi sono distinti dall'azione da intraprendere quando un evento si verifica. Di conseguenza, qualsiasi azione può essere associata a qualsiasi evento.  
  
-   I predicati consentono di filtrare dinamicamente i casi in cui i dati degli eventi devono essere acquisiti. Questa possibilità garantisce maggiore flessibilità per l'infrastruttura degli eventi estesi. Per ulteriori informazioni, vedere [SQL Server Extended Events Packages](sql-server-extended-events-packages.md).  
  
 Gli eventi estesi possono generare in modo sincrono dati degli eventi (e in modo asincrono elaborare tali dati) il che fornisce una soluzione flessibile per la gestione degli eventi. Inoltre, gli eventi estesi forniscono le funzionalità seguenti:  
  
-   Approccio unificato alla gestione degli eventi nel sistema server, consentendo agli utenti di isolare eventi specifici ai fini della risoluzione dei problemi.  
  
-   Supporto e integrazione con gli strumenti ETW esistenti.  
  
-   Meccanismo di gestione degli eventi interamente configurabile, basato su [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Possibilità di monitorare dinamicamente i processi attivi, con un impatto minimo su tali processi.  
  
-   Sessione di integrità di sistema predefinita che viene eseguita senza effetti visibili sulle prestazioni. Tale sessione consente di raccogliere dati di sistema che è possibile utilizzare per risolvere i problemi relativi alle prestazioni. Per altre informazioni, vedere [Utilizzare la sessione system_health](use-the-ssms-xe-profiler.md).  
  
## <a name="extended-events-tasks"></a>Attività degli eventi estesi  
 L'utilizzo di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] per eseguire funzioni, DMV e istruzioni DDL (Data Definition Language) [!INCLUDE[tsql](../../includes/tsql-md.md)] o viste del catalogo consente di creare soluzioni per la risoluzione dei problemi relativi agli eventi estesi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] semplici o complesse per l'ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Utilizzare **Esplora oggetti** per gestire sessioni di eventi.|[Gestire sessioni di eventi in Esplora oggetti](../../ssms/object/object-explorer.md)|  
|Viene descritto come creare una sessione di eventi estesi.|[Creare una sessione Eventi estesi](../../database-engine/create-an-extended-events-session.md)|  
|Viene descritto come visualizzare e aggiornare i dati di destinazione.|[Visualizzare i dati della sessione eventi](../../database-engine/view-event-session-data.md)|  
|Viene descritto come utilizzare gli strumenti degli eventi estesi per creare e gestire sessioni di eventi estesi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Strumenti degli eventi estesi](extended-events-tools.md)|  
|Viene descritto come alterare una sessione Eventi estesi.|[Modificare una sessione Eventi estesi](alter-an-extended-events-session.md)|  
|Viene descritto come copiare o esportare dati di destinazione.|[Copiare o esportare i dati di destinazione](../../database-engine/copy-or-export-target-data.md)|  
|Viene descritto come modificare la vista dei risultati della traccia per personalizzare la modalità di analisi dei dati.|[Modificare la visualizzazione dei risultati della traccia](../../database-engine/modify-the-trace-results-view.md)|  
|Viene descritto come ottenere informazioni sui campi associati agli eventi.|[Recuperare i campi per tutti gli eventi](../../database-engine/get-the-fields-for-all-events.md)|  
|Viene descritto come individuare gli eventi disponibili nei pacchetti registrati.|[Visualizzare gli eventi per i pacchetti registrati](../../database-engine/view-the-events-for-registered-packages.md)|  
|Viene descritto come individuare le destinazioni degli eventi estesi disponibili nei pacchetti registrati.|[Visualizzare le destinazioni degli eventi estesi per i pacchetti registrati](../../database-engine/view-the-extended-events-targets-for-registered-packages.md)|  
|Viene descritto come visualizzare gli eventi e le azioni Eventi estesi equivalenti a ogni evento di Traccia SQL e alle colonne associate.|[Visualizzare gli eventi estesi equivalenti alle classi di eventi di Traccia SQL](view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|Viene descritto come trovare i parametri che è possibile impostare quando si utilizza l'argomento ADD TARGET in CREATE EVENT SESSION o ALTER EVENT SESSION.|[Recuperare i parametri configurabili per l'argomento ADD TARGET](../../database-engine/get-the-configurable-parameters-for-the-add-target-argument.md)|  
|Viene descritto come convertire uno script di Traccia SQL esistente in una sessione Eventi estesi.|[Convertire uno script di Traccia SQL esistente in una sessione Eventi estesi](convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|Viene descritto come determinare quali query mantengono il blocco, il piano della query e lo stack [!INCLUDE[tsql](../../includes/tsql-md.md)] al momento del blocco.|[Individuare le query che mantengono attivi i blocchi](determine-which-queries-are-holding-locks.md)|  
|Viene descritto come individuare l'origine dei blocchi che hanno effetti negativi sulle prestazioni del database.|[Cercare gli oggetti con il maggior numero di blocchi acquisiti](find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|Viene illustrato come utilizzare gli eventi estesi con Analisi eventi per Windows al fine di monitorare l'attività del sistema.|[Monitorare l'attività del sistema mediante gli eventi estesi](monitor-system-activity-using-extended-events.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni livello dati](../data-tier-applications/data-tier-applications.md)   
 [Supporto dell'applicazione livello dati per oggetti e versioni di SQL Server](../data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)   
 [Distribuire un'applicazione livello dati](../data-tier-applications/deploy-a-data-tier-application.md)   
 [Monitorare le applicazioni livello dati](../data-tier-applications/monitor-data-tier-applications.md)   
 [Viste a gestione dinamica degli eventi estesi](../views/views.md)   
 [Viste del catalogo degli eventi estesi &#40;&#41; Transact-SQL] (~/Relational-Databases/System-catalog-views/Extended-Events-catalog-views-Transact-SQL  
  
  
