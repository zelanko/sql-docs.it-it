---
title: Notifiche degli eventi | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications, about
- events [SQL Server], notifications
ms.assetid: 4da73ca1-6c06-4e96-8ab8-2ecba30b6c86
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f5433d6082f2860805368f636383eb2e17959e77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048865"
---
# <a name="event-notifications"></a>Notifiche degli eventi
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Le notifiche degli eventi consentono l'invio di informazioni sugli eventi a un servizio di [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Le notifiche degli eventi vengono eseguite in risposta a una serie di istruzioni DDL (Data Definition Language) [!INCLUDE[tsql](../../includes/tsql-md.md)] ed eventi di Traccia SQL mediante l'invio di informazioni sugli eventi a un servizio [!INCLUDE[ssSB](../../includes/sssb-md.md)] .  
  
 È possibile utilizzare le notifiche degli eventi per eseguire le attività seguenti:  
  
-   Registrare e visualizzare le modifiche o le attività riscontrate sul database.  
  
-   Eseguire un'operazione in risposta a un evento in modo asincrono anziché sincrono.  
  
 Le notifiche degli eventi possono costituire un'alternativa a trigger DDL e Traccia SQL a livello di programmazione.  
  
## <a name="event-notifications-benefits"></a>Vantaggi delle notifiche di eventi  
 Le notifiche degli eventi vengono eseguite in modo asincrono, all'esterno dell'ambito di una transazione. A differenza dei trigger DDL, è pertanto possibile utilizzare le notifiche degli eventi all'interno di un'applicazione di database per rispondere a eventi senza utilizzare le risorse definite dalla transazione immediata.  
  
 A differenza della Traccia SQL, è possibile utilizzare le notifiche degli eventi per eseguire un'operazione all'interno di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in risposta a un evento di Traccia SQL.  
  
 I dati degli eventi possono essere utilizzati in applicazioni eseguite contestualmente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per tenere traccia dello stato di avanzamento e per prendere decisioni. La notifica degli eventi seguente, ad esempio, invia un avviso a un determinato servizio ogni volta che viene eseguita un'istruzione `ALTER TABLE` nel database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE '//Adventure-Works.com/ArchiveService' ,  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
## <a name="event-notifications-concepts"></a>Concetti delle notifiche di eventi  
 Durante la creazione di una notifica degli eventi, vengono aperte una o più conversazioni [!INCLUDE[ssSB](../../includes/sssb-md.md)] tra un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il servizio di destinazione specificato. Tali conversazioni rimangono in genere aperte finché la notifica degli eventi è disponibile come oggetto nell'istanza del server. In alcune situazioni di errore è possibile che le conversazioni vengano chiuse prima dell'eliminazione della notifica. Le conversazioni non vengono mai condivise tra le notifiche degli eventi. A ogni notifica sono associate conversazioni esclusive. Se una conversazione viene terminata in modo esplicito, il servizio di destinazione non potrà più ricevere altri messaggi e la conversazione non verrà riaperta alla successiva attivazione della notifica degli eventi.  
  
 Le informazioni sugli eventi vengono fornite al servizio [!INCLUDE[ssSB](../../includes/sssb-md.md)] sotto forma di variabile di tipo **xml**. Tale variabile fornisce informazioni relative al momento in cui si verifica l'evento, all'oggetto di database interessato, all'istruzione batch [!INCLUDE[tsql](../../includes/tsql-md.md)], nonché informazioni di altro tipo. Per altre informazioni su XML Schema prodotto dalle notifiche degli eventi, vedere [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md).  
  
### <a name="event-notifications-vs-triggers"></a>Notifiche degli eventi e Trigger  
 Nella tabella seguente viene eseguito il confronto fra trigger e notifiche di eventi.  
  
|Trigger|Notifiche degli eventi|  
|--------------|-------------------------|  
|I trigger DML rispondono agli eventi DML (Data Manipulation Language). I trigger DLL rispondono agli eventi DLL (Data Definition Language).|Le notifiche degli eventi rispondono agli eventi DDL e a un subset di eventi di Traccia SQL.|  
|I trigger possono eseguire codice gestito Transact-SQL o CLR (Common Language Runtime).|Le notifiche degli eventi non eseguono codice, ma inviano messaggi **xml** a un servizio di Service Broker.|  
|I trigger vengono elaborati in modo sincrono nell'ambito delle transazioni che ne provocano l'attivazione.|Le notifiche degli eventi possono essere elaborate in modo asincrono e non vengono eseguite nell'ambito delle transazioni che le attivano.|  
|Il consumer di un trigger è strettamente associato all'evento che lo attiva.|Il consumer di una notifica degli eventi non è associato all'evento che la attiva.|  
|I trigger devono essere elaborati nel server locale.|Le notifiche degli eventi possono essere elaborate in un server remoto.|  
|Il rollback dei trigger è possibile.|Il rollback delle notifiche degli eventi non è possibile.|  
|I nomi di trigger DML sono definiti a livello di ambito dello schema. L'ambito dei nomi dei trigger DDL è il server o il database.|L'ambito dei nomi delle notifiche degli eventi è il server o il database. Le notifiche degli eventi in un evento QUEUE_ACTIVATION sono definiti a livello di ambito di una coda specifica.|  
|Il proprietario dei trigger DML è il proprietario delle tabelle sulle quali vengono applicati.|Il proprietario di una notifica degli eventi in una coda può essere diverso dal proprietario dell'oggetto al quale viene applicata.|  
|I trigger supportano la clausola EXECUTE AS.|Le notifiche degli eventi non supportano la clausola EXECUTE AS.|  
|Le informazioni sull'evento di un trigger DDL possono essere acquisite usando la funzione EVENTDATA, che restituisce un tipo di dati **xml** .|Le notifiche degli eventi inviano informazioni **xml** sull'evento a un servizio di Service Broker. Le informazioni vengono formattate con lo stesso schema della funzione EVENTDATA.|  
|I metadati relativi ai trigger si trovano nelle viste del catalogo **sys.triggers** e **sys.server_triggers** .|I metadati relativi alle notifiche degli eventi si trovano nelle viste del catalogo **sys.event_notifications** e **sys.server_event_notifications**.|  
  
### <a name="event-notifications-vs-sql-trace"></a>Notifiche degli eventi e Traccia SQL  
 Nella tabella seguente vengono confrontate le caratteristiche delle notifiche degli eventi e della Traccia SQL per il monitoraggio degli eventi del server.  
  
|Traccia SQL|Notifiche degli eventi|  
|---------------|-------------------------|  
|In Traccia SQL non viene generato alcun overhead di prestazioni associato alle transazioni. L'assemblaggio dei dati risulta efficace.|La creazione di dati di evento in formato XML e l'invio della notifica degli eventi comportano invece un certo overhead.|  
|In Traccia SQL viene eseguito il monitoraggio di qualsiasi classe di evento di traccia.|Le notifiche degli eventi consentono di eseguire il monitoraggio di un subset di classi di evento di traccia, nonché di tutti gli eventi Data Definition Language (DDL).|  
|È possibile personalizzare le colonne di dati da generare in un evento di traccia.|Lo schema dei dati di evento in formato XML restituiti dalle notifiche degli eventi è fisso.|  
|Gli eventi di traccia restituiti da DDL vengono sempre generati senza tener conto dell'eventuale rollback dell'istruzione DDL.|Le notifiche degli eventi non vengono attivate in caso di rollback dell'evento nell'istruzione DDL corrispondente.|  
|La gestione del flusso intermedio dei dati degli eventi di traccia comporta il popolamento e la gestione dei file o delle tabelle di traccia.|La gestione intermedia dei dati relativi alle notifiche degli eventi viene eseguita automaticamente tramite code Service Broker.|  
|Le tracce devono essere riavviate a ogni riavvio del server.|Dopo la registrazione, le notifiche degli eventi vengono mantenute anche in caso di riavvio del server e incluse nelle transazioni.|  
|Dopo l'avvio, non è possibile controllare l'attivazione delle tracce. È possibile utilizzare orari di arresto e di filtro per specificare l'ora di avvio. Per accedere alle tracce, è necessario eseguire il polling del file di traccia corrispondente.|È possibile controllare le notifiche degli eventi eseguendo l'istruzione WAITFOR sulla coda che riceve il messaggio generato dalla notifica. Per accedere alle notifiche, è possibile eseguire il polling della coda.|  
|Per creare una traccia, è necessario disporre almeno dell'autorizzazione ALTER TRACE. È inoltre necessario disporre di un'autorizzazione per creare un file di traccia nel computer corrispondente.|L'autorizzazione minima dipende dal tipo di notifica degli eventi da creare. È inoltre necessaria l'autorizzazione RECEIVE sulla coda corrispondente.|  
|Le tracce possono essere ricevute in remoto.|Le notifiche degli eventi possono essere ricevute in remoto.|  
|Per l'implementazione di eventi di traccia vengono utilizzate stored procedure di sistema.|Per l'implementazione di notifiche di eventi viene usata una combinazione di istruzioni [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssSB](../../includes/sssb-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|Per accedere ai dati degli eventi di traccia a livello di programmazione, è possibile eseguire una query nella tabella di traccia corrispondente, analizzare il file di traccia oppure usare la classe TraceReader di SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects).|Per accedere ai dati degli eventi a livello di programmazione, è possibile eseguire XQuery sui dati degli eventi in formato XML oppure utilizzare le classi di evento di SMO.|  
  
## <a name="event-notification-tasks"></a>Attività della notifica degli eventi.  
  
|Attività|Argomento|  
|----------|-----------|  
|Viene descritto come creare e implementare notifiche degli eventi.|[Implementazione di notifiche degli eventi](../../relational-databases/service-broker/implement-event-notifications.md)|  
|Viene descritto come configurare la sicurezza del dialogo [!INCLUDE[ssSB](../../includes/sssb-md.md)] per le notifiche degli eventi che inviano messaggi a Service Broker su un server remoto.|[Configurazione della sicurezza del dialogo per le notifiche degli eventi](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md)|  
|Viene descritto come restituire informazioni sulle notifiche degli eventi.|[Recupero di informazioni sulle notifiche degli eventi](../../relational-databases/service-broker/get-information-about-event-notifications.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Trigger DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [Trigger DML](../../relational-databases/triggers/dml-triggers.md)   
 [Traccia SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
