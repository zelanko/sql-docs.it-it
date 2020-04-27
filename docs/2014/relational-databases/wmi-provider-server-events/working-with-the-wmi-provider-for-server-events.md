---
title: Utilizzo del provider WMI per eventi del server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- event notifications [WMI]
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- Service Broker [WMI]
- WMI Provider for Server Events, connection strings
- WMI Provider for Server Events, Service Broker
- notifications [WMI]
- WMI Provider for Server Events, security
ms.assetid: cd974b3b-2309-4a20-b9be-7cfc93fc4389
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0519561b24d8aff32adc7c375657fa85b9dfa496
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68195737"
---
# <a name="working-with-the-wmi-provider-for-server-events"></a>Utilizzo del provider WMI per eventi del server
  In questo argomento vengono fornite linee guida che è consigliabile tenere presenti prima di programmare tramite il provider WMI per eventi del server.  
  
## <a name="enabling-service-broker"></a>Abilitazione di Service Broker  
 Il provider WMI per eventi del server converte query WQL per eventi in notifiche degli eventi nel database di destinazione. Una corretta comprensione del funzionamento delle notifiche degli eventi può risultare utile quando si programma per il provider. Per altre informazioni, vedere [Concetti relativi al provider WMI per eventi del server](https://technet.microsoft.com/library/ms180560.aspx).  
  
 In particolare, poiché le notifiche degli eventi create dal provider WMI utilizzano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per inviare messaggi sugli eventi del server, questo servizio deve essere abilitato ogni volta che vengono generati gli eventi. Se il programma esegue query sugli eventi in un'istanza del server, è necessario abilitare [!INCLUDE[ssSB](../../includes/sssb-md.md)] in msdb di tale istanza, in quanto corrisponde al percorso del servizio [!INCLUDE[ssSB](../../includes/sssb-md.md)] di destinazione (denominato SQL/Notifications/ProcessWMIEventProviderNotification/v1.0) creato dal provider. Se il programma esegue query sugli eventi in un database o in un determinato oggetto di database, è necessario che [!INCLUDE[ssSB](../../includes/sssb-md.md)] sia abilitato nel database di destinazione specifico. Se il servizio di [!INCLUDE[ssSB](../../includes/sssb-md.md)] non è abilitato in seguito alla distribuzione dell'applicazione, qualsiasi evento generato dalla notifica degli eventi sottostante viene inviato alla coda del servizio utilizzato dalla notifica, ma non viene restituito all'applicazione di gestione WMI fino a quando [!INCLUDE[ssSB](../../includes/sssb-md.md)] non è abilitato.  
  
 La query seguente consente di determinare i servizi di Service Broker abilitati in un'istanza del server e il GUID dell'istanza di Service Broker:  
  
```  
SELECT name, is_broker_enabled, service_broker_guid FROM sys.databases;  
```  
  
 Il GUID di Service Broker di msdb è rilevante in quanto corrisponde al percorso del servizio di destinazione del provider.  
  
 Per abilitare [!INCLUDE[ssSB](../../includes/sssb-md.md)] in un database, utilizzare l'opzione ENABLE_BROKER SET dell'istruzione [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) .  
  
## <a name="specifying-a-connection-string"></a>Definizione di una stringa di connessione  
 Le applicazioni indirizzano il provider WMI per eventi del server a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connettendosi a uno spazio dei nomi WMI definito dal provider. Il servizio Windows WMI esegue il mapping di questo spazio dei nomi alla DLL del provider, Sqlwep.dll, e lo carica in memoria. Ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone di uno spazio dei nomi WMI personalizzato, che per \\ \\impostazione predefinita è:. \\ *root*\\*instance_name*radice \Microsoft\SqlServer\ServerEvents. *nome_istanza* viene impostato in modo predefinito su MSSQLSERVER in un'installazione predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions-and-server-authentication"></a>Autorizzazioni e autenticazione del server  
 Per accedere al provider WMI per eventi del server, il client in cui ha origine un'applicazione di gestione WMI deve corrispondere all'account di accesso o al gruppo autenticato di Windows nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificata nella stringa di connessione dell'applicazione.  
  
## <a name="permissions-and-event-notification-scope"></a>Autorizzazioni e ambito delle notifiche degli eventi  
 Il provider WMI per eventi del server converte query WQL in notifiche degli eventi nel database di destinazione. Di conseguenza, l'applicazione chiamante deve disporre non solo delle autorizzazioni minime necessarie per accedere al provider, ma anche delle autorizzazioni corrette nel database per creare le notifiche degli eventi necessarie. Sono necessarie le autorizzazioni seguenti:  
  
-   Per creare una notifica degli eventi il cui ambito è costituito dal database, è necessario disporre almeno dell'autorizzazione CREATE DATABASE DDL EVENT NOTIFICATION per il database corrente.  
  
-   Per creare una notifica degli eventi per un'istruzione DDL il cui ambito è costituito dal server, è necessario disporre almeno dell'autorizzazione CREATE DDL EVENT NOTIFICATION nel server.  
  
-   Per creare una notifica degli eventi per un evento di traccia, è necessario disporre almeno dell'autorizzazione CREATE TRACE EVENT NOTIFICATION nel server.  
  
-   Per creare una notifica degli eventi il cui ambito è costituito da una coda, è necessario disporre almeno dell'autorizzazione ALTER per la coda.  
  
 Per informazioni sull'ambito delle query WQL, vedere [Utilizzo di WQL con il provider WMI per eventi del server](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 Per illustrare l'ambito, si consideri un'applicazione del provider WMI che include la query WQL seguente:  
  
```  
SELECT * FROM ALTER_TABLE  
WHERE DatabaseName = "AdventureWorks2012"   
    AND SchemaName = "Person"  
    AND ObjectName = "Person"  
    AND ObjectType = "TABLE";  
```  
  
 Il provider WMI converte la query in una notifica degli eventi creata nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Di conseguenza, il chiamante deve disporre delle autorizzazioni necessarie per creare tale notifica degli eventi, in particolare dell'autorizzazione CREATE DATABASE DDL EVENT NOTIFICATION nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
 Se una query WQL specifica una notifica degli eventi con ambito a livello di server, ad esempio eseguendo la query SELECT * FROM ALTER_TABLE, l'applicazione chiamante deve disporre dell'autorizzazione CREATE DDL EVENT NOTIFICATION a livello di server. Si noti che le notifiche degli eventi con ambito server vengono archiviate nel database master. Per visualizzare i metadati di tali notifiche, è possibile utilizzare la vista del catalogo [sys.server_event_notifications](/sql/relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql) .  
  
> [!NOTE]  
>  L'ambito della notifica degli eventi creata dal provider WMI (server, database o oggetto) dipende in definitiva dal risultato del processo di verifica delle autorizzazioni utilizzato dal provider WMI, che dipende a sua volta dal set di autorizzazioni dell'utente che chiama il provider e dalla verifica del database su cui vengono eseguite le query.  
>   
>  Nell'esempio precedente il provider tenta innanzitutto di creare una notifica degli eventi il cui ambito è costituito dal database (`ON DATABASE`). Se il provider verifica che il database è presente e che il chiamante dispone delle autorizzazioni necessarie per crearvi una notifica degli eventi, la registrazione ha esito positivo. Se la registrazione ha esito negativo, il provider tenta di creare una notifica degli eventi nel server (`ON SERVER`). Supponendo che il tentativo abbia esito positivo, tutti gli eventi `ALTER_TABLE` che si verificano nel server vengono inviati dal processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al processo del servizio WMI. Il provider, tuttavia, esclude tramite filtro tutti gli eventi che non si applicano al database `AdventureWorks` . Benché questo processo rischi di aumentare la quantità di traffico di rete richiesta per l'ambito dell'evento, offre inoltre la flessibilità necessaria per registrare query WQL nei database prima che questi vengano creati e per ricevere quindi i dati degli eventi in seguito alla creazione del database e all'avvio dell'attività DDL nel database stesso.  
  
## <a name="permissions-and-message-verification"></a>Autorizzazioni e verifica dei messaggi  
 Il provider WMI non invia messaggi per le notifiche degli eventi se si verificano entrambe le condizioni seguenti:  
  
-   L'utente che ha creato la notifica degli eventi tramite il provider WMI non è più presente nel database o non dispone più dell'autorizzazione necessaria per creare una notifica degli eventi simile.  
  
-   Le notifiche degli eventi vengono create negli eventi seguenti.  
  
    -   DROP_LOGIN  
  
    -   ALTER_LOGIN  
  
    -   DROP_USER  
  
    -   ALTER_USER  
  
    -   ADD_ROLE_MEMBER  
  
    -   DROP_ROLE_MEMBER  
  
    -   ADD_SERVER_ROLE_MEMBER  
  
    -   DROP_SERVER_ROLE_MEMBER  
  
    -   DENY o REVOKE (si applica solo alle autorizzazioni ALTER DATABASE, ALTER ANY DATABASE EVENT NOTIFICATION, CREATE DATABASE DDL EVENT NOTIFICATION, CONTROL SERVER, ALTER ANY EVENT NOTIFICATION, CREATE DDL EVENT NOTIFICATION O CREATE TRACE EVENT NOTIFICATION)  
  
## <a name="working-with-event-data-on-the-client-side"></a>Utilizzo dei dati degli eventi sul lato client  
 Dopo che il provider WMI per eventi del server crea la notifica degli eventi necessaria nel database di destinazione, la notifica degli eventi invia i dati dell'evento al servizio di destinazione in msdb denominato **SQL/Notifications/ProcessWMIEventProviderNotification/v 1.0**. Il servizio di destinazione inserisce l'evento in una coda `msdb` in denominata **WMIEventProviderNotificationQueue**. Sia il servizio sia la coda vengono creati dinamicamente dal provider quando si connette per la prima volta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a. Il provider legge quindi i dati degli eventi XML dalla coda e li trasforma in MOF (Managed Object Format) prima di restituirlo all'applicazione client. I dati MOF sono costituiti dalle proprietà dell'evento richiesto dalla query WQL come definizione della classe CIM (Common Information Model). Ogni proprietà dispone di un tipo CIM corrispondente. La proprietà `SPID`, ad esempio, viene restituita come tipo CIM `Sint32`. I tipi CIM per ogni proprietà sono elencati all'interno di ogni classe di evento in [Classi e proprietà del provider WMI per eventi del server](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Concetti relativi al provider WMI per eventi del server](https://technet.microsoft.com/library/ms180560.aspx)  
  
  
