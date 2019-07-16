---
title: Utilizzo di WQL con il Provider WMI per eventi del Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Server Events, WQL
ms.assetid: 58b67426-1e66-4445-8e2c-03182e94c4be
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 17d28b2d8d2da467fa07bd2c2ddc2de8db207cca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139376"
---
# <a name="using-wql-with-the-wmi-provider-for-server-events"></a>Utilizzo di WQL con il provider WMI per eventi del server
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Le applicazioni di gestione accedono agli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando il provider WMI per eventi del server ed eseguendo istruzioni WQL (WMI Query Language). WQL è un subset semplificato del linguaggio SQL (Structured Query Language), con alcune estensioni specifiche di WMI. Quando si utilizza WQL, un'applicazione recupera un tipo di evento da un'istanza specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un database o un oggetto di database (l'unico oggetto attualmente supportato è la coda). Il Provider WMI per eventi del Server converte la query in una notifica degli eventi creata nel database di destinazione per le notifiche degli eventi con ambito database o con ambito oggetto o nel **master** database per eventi con ambito server notifiche.  
  
 Si consideri, ad esempio, la query WQL seguente:  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS WHERE DatabaseName = 'AdventureWorks'  
```  
  
 Da questa query il provider WMI tenta di produrre l'equivalente della notifica degli eventi sul server di destinazione:  
  
```  
USE AdventureWorks ;  
GO  
  
CREATE EVENT NOTIFICATION SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9  
    ON DATABASE  
    WITH FAN_IN  
    FOR DDL_DATABASE_LEVEL_EVENTS  
    TO SERVICE   
        'SQL/Notifications/ProcessWMIEventProviderNotification/v1.0',  
        'A7E5521A-1CA6-4741-865D-826F804E5135';  
GO  
```  
  
 L'argomento nella clausola `FROM` della query WQL (`DDL_DATABASE_LEVEL_EVENTS`) può essere qualsiasi evento valido per il quale può essere creata una notifica. Gli argomenti nelle clausole `SELECT` e `WHERE` possono specificare qualsiasi proprietà di evento associata a un evento o al relativo evento padre. Per un elenco di eventi validi e le proprietà degli eventi, vedere [le notifiche degli eventi (motore di Database)](https://technet.microsoft.com/library/ms182602.aspx).  
  
 La sintassi WQL seguente è supportata in modo esplicito dal provider WMI per eventi del server. È possibile specificare elementi di sintassi WQL aggiuntivi. Tali elementi non sono specifici di questo provider e vengono analizzati dal servizio host WMI. Per ulteriori informazioni sul linguaggio WQL (WMI Query Language), vedere la documentazione relativa a WQL in MSDN (Microsoft Developer Network).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SELECT { event_property [ ,...n ] | * }  
FROM event_type   
WHERE where_condition   
```  
  
## <a name="arguments"></a>Argomenti  
 *event_property*  
 Proprietà di un evento. Gli esempi includono **PostTime**, **SPID**, e **LoginName**. Cercare ogni evento incluso nella [Provider WMI per la proprietà e le classi di eventi Server](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md) per determinare quali proprietà contiene. Ad esempio, contiene l'evento ddl_database_level_events include il **NomeDatabase** e **UserName** proprietà. Eredita anche il **SQLInstance**, **LoginName**, **PostTime**, **SPID**, e **ComputerName** proprietà dai relativi eventi padre.  
  
 **,** *...n*  
 Indica che *event_property* è possibile eseguire query più volte, separati da virgole.  
  
 \*  
 Specifica che tutte le proprietà associate a un evento vengono sottoposte a query.  
  
 *event_type*  
 Qualsiasi evento per il quale è possibile creare una notifica. Per un elenco di eventi disponibili, vedere [Provider WMI per la proprietà e le classi di eventi Server](https://technet.microsoft.com/library/ms186449.aspx). Si noti che *tipo di evento* nomi corrispondono allo stesso *event_type* | *event_group* che può essere specificata quando si crea manualmente una notifica degli eventi utilizzando CREATE EVENT NOTIFICATION. Esempi di *tipo di evento* includono CREATE_TABLE, LOCK_DEADLOCK, DDL_USER_EVENTS e TRC_DATABASE.  
  
> [!NOTE]  
>  Anche determinate stored procedure di sistema che eseguono operazioni di tipo DDL possono attivare notifiche degli eventi. Testare le notifiche degli eventi per determinarne le risposte alle stored procedure di sistema eseguite. Ad esempio, l'istruzione CREATE TYPE e **sp_addtype** stored procedure attivano una notifica degli eventi creata in un evento CREATE_TYPE. Tuttavia, il **sp_rename** stored procedure non attiva notifiche degli eventi. Per altre informazioni, vedere[eventi DDL](../../relational-databases/triggers/ddl-events.md).  
  
 *where_condition*  
 È un predicato della query clausola WHERE costituito *event_property* nomi e logiche e gli operatori di confronto. Il *where_condition* determina l'ambito in cui la notifica degli eventi corrispondente viene registrata nel database di destinazione. Può anche agire come un filtro a un particolare schema o oggetto da cui alla query di destinazione *event_type.* Per ulteriori informazioni, vedere la sezione Osservazioni di seguito in questo argomento.  
  
 Solo le `=` operando può essere usato insieme al **DatabaseName**, **SchemaName**, e **ObjectName**. Con queste proprietà di evento non è possibile utilizzare altre espressioni.  
  
## <a name="remarks"></a>Note  
 Il *where_condition* del Provider WMI per eventi del Server sintassi determina quanto segue:  
  
-   L'ambito da cui il provider prova a recuperare l'oggetto specificato *event_type*: il livello di server, a livello di database o a livello di oggetto (l'unico oggetto attualmente supportato è coda). Infine, tale ambito determina il tipo di notifica degli eventi creato nel database di destinazione. Questo processo viene chiamato registrazione della notifica degli eventi.  
  
-   Il database, lo schema e l'oggetto, se appropriato, in cui effettuare la registrazione.  
  
 Il provider WMI per eventi del server utilizza un algoritmo bottom-up, first-fit per produrre l'ambito più ristretto possibile per l'oggetto EVENT NOTIFICATION sottostante. L'algoritmo tenta di ridurre l'attività interna sul server e il traffico di rete tra l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il processo host WMI. Il provider esamina il *event_type* specificato nella clausola FROM e le condizioni nella clausola WHERE e prova a registrare la notifica degli eventi sottostante con l'ambito più ristretto possibile. Se tale registrazione non riesce, prova a eseguirla nei successivi ambiti di livello più alto finché l'operazione non riesce. Se l'esito dell'operazione è ancora negativo dopo aver raggiunto l'ambito di livello più alto, ovvero il livello del server, restituisce un errore al consumer.  
  
 Ad esempio, se DatabaseName = **'** AdventureWorks **'** viene specificato nella clausola WHERE, il provider prova a registrare una notifica degli eventi nel [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] database. Se il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] esiste e il client chiamante dispone delle autorizzazioni necessarie per creare una notifica degli eventi in [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], la registrazione riesce. In caso contrario, viene eseguito un tentativo di registrazione della notifica degli eventi a livello di server. La registrazione riesce se il client WMI dispone delle autorizzazioni necessarie. In questo scenario, tuttavia, gli eventi non vengono restituiti al client finché il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] non sarà stato creato.  
  
 Il *where_condition* può anche agire come un filtro per limitare ulteriormente la query per un determinato database, schema o object. Si consideri, ad esempio, la query WQL seguente:  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
 A seconda del risultato del processo di registrazione, questa query WQL può essere registrata a livello di database o di server. Anche se viene registrata a livello di server, tuttavia, il provider alla fine filtra gli eventi `ALTER_TABLE` che non sono applicabili alla tabella `AdventureWorks.Sales.SalesOrderDetail`. In altre parole, il provider restituisce solo le proprietà degli eventi `ALTER_TABLE` che si verificano in quella tabella specifica.  
  
 Se si specifica un'espressione composta, ad esempio `DatabaseName='AW1'` OR `DatabaseName='AW2'`, viene effettuato il tentativo di registrare una singola notifica degli eventi nell'ambito server anziché due notifiche degli eventi separate. La registrazione riesce se il client chiamante dispone di autorizzazioni.  
  
 Se `SchemaName='X' AND ObjectType='Y' AND ObjectName='Z'` sono stata specificata nel `WHERE` clausola, viene effettuato un tentativo di registrare la notifica degli eventi direttamente nell'oggetto `Z` nello schema `X`. La registrazione riesce se il client dispone di autorizzazioni. Si noti che attualmente, gli eventi a livello di oggetto sono supportati solo nelle code e solo per l'evento QUEUE_ACTIVATION *event_type*.  
  
 Notare che non tutti gli eventi possono essere sottoposti a query in qualsiasi ambito specifico. Una query WQL su un evento di traccia quale Lock_Deadlock o un gruppo di eventi di traccia quale TRC_LOCKS può essere, ad esempio, registrata solo a livello di server. Analogamente, anche l'evento CREATE_ENDPOINT e il gruppo di eventi DDL_ENDPOINT_EVENTS possono essere registrati solo a livello di server. Per altre informazioni sull'ambito appropriato per la registrazione degli eventi, vedere [progettare notifiche degli eventi](https://technet.microsoft.com/library/ms175854\(v=sql.105\).aspx). Un tentativo di registrare WQL query la cui proprietà *event_type* può essere registrato solo nel server di livello viene sempre eseguito a livello di server. La registrazione riesce se il client WMI dispone di autorizzazioni. In caso contrario, al client viene restituito un errore. In alcuni casi, tuttavia, è ancora possibile utilizzare la clausola WHERE come filtro per gli eventi a livello di server in base alle proprietà che corrispondono all'evento. Ad esempio, molti eventi di traccia includono una **DatabaseName** proprietà che può essere utilizzato nella clausola WHERE come filtro.  
  
 Le notifiche degli eventi con ambito server vengono creati nel **master** del database e possono eseguire query per i metadati tramite il [server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md) vista del catalogo.  
  
 Con ambito database o le notifiche degli eventi con ambito oggetto vengono creati nel database specificato e possono eseguire query per i metadati usando le [Sys. event_notifications](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md) vista del catalogo. È necessario anteporre alla vista del catalogo il nome del database corrispondente.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-querying-for-events-at-the-server-scope"></a>R. Query su eventi nell'ambito server  
 Nella query WQL seguente vengono recuperate tutte le proprietà di evento per qualsiasi evento di traccia `SERVER_MEMORY_CHANGE` che si verifica sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT * FROM SERVER_MEMORY_CHANGE  
```  
  
### <a name="b-querying-for-events-at-the-database-scope"></a>B. Query su eventi nell'ambito database  
 Nella query WQL seguente vengono recuperate proprietà di evento specifiche per qualsiasi evento che si verifica nel database `AdventureWorks` ed è incluso nel gruppo di eventi `DDL_DATABASE_LEVEL_EVENTS`.  
  
```  
SELECT SPID, SQLInstance, DatabaseName FROM DDL_DATABASE_LEVEL_EVENTS   
WHERE DatabaseName = 'AdventureWorks'   
```  
  
### <a name="c-querying-for-events-at-the-database-scope-filtering-by-schema-and-object"></a>C. Query su eventi nell'ambito database mediante l'applicazione di un filtro per schema e per oggetto  
 Nella query seguente vengono recuperate tutte le proprietà di evento per qualsiasi evento `ALTER_TABLE` che si verifica nella tabella `AdventureWorks.Sales.SalesOrderDetail`.  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Provider WMI per concetti degli eventi Server](https://technet.microsoft.com/library/ms180560.aspx)   
 [Notifiche degli eventi (motore di Database)](https://technet.microsoft.com/library/ms182602.aspx)  
  
  
