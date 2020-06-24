---
title: Utilizzo di WQL con il provider WMI per eventi del server
description: Informazioni sul modo in cui le applicazioni di gestione accedono a eventi SQL Server utilizzando il provider WMI per eventi del server eseguendo istruzioni WMI Query Language.
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
ms.openlocfilehash: e6fae362d3a8d1fe387dd7561b1476bb37f0c255
ms.sourcegitcommit: bf5e9cb3a2caa25d0a37f401b3806b7baa5adea8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/24/2020
ms.locfileid: "85295384"
---
# <a name="using-wql-with-the-wmi-provider-for-server-events"></a>Utilizzo di WQL con il provider WMI per eventi del server
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Le applicazioni di gestione accedono agli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando il provider WMI per eventi del server ed eseguendo istruzioni WQL (WMI Query Language). WQL è un subset semplificato del linguaggio SQL (Structured Query Language), con alcune estensioni specifiche di WMI. Quando si utilizza WQL, un'applicazione recupera un tipo di evento da un'istanza specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un database o un oggetto di database (l'unico oggetto attualmente supportato è la coda). Il provider WMI per eventi del server converte la query in una notifica degli eventi creata nel database di destinazione per le notifiche degli eventi con ambito database o oggetto o nel database **Master** per le notifiche degli eventi con ambito server.  
  
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
  
 L'argomento nella clausola `FROM` della query WQL (`DDL_DATABASE_LEVEL_EVENTS`) può essere qualsiasi evento valido per il quale può essere creata una notifica. Gli argomenti nelle clausole `SELECT` e `WHERE` possono specificare qualsiasi proprietà di evento associata a un evento o al relativo evento padre. Per un elenco di eventi e proprietà di evento validi, vedere [notifiche degli eventi (motore di database)](https://technet.microsoft.com/library/ms182602.aspx).  
  
 La sintassi WQL seguente è supportata in modo esplicito dal provider WMI per eventi del server. È possibile specificare elementi di sintassi WQL aggiuntivi. Tali elementi non sono specifici di questo provider e vengono analizzati dal servizio host WMI. Per ulteriori informazioni sul linguaggio WQL (WMI Query Language), vedere la documentazione relativa a WQL in MSDN (Microsoft Developer Network).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SELECT { event_property [ ,...n ] | * }  
FROM event_type   
WHERE where_condition   
```  
  
## <a name="arguments"></a>Argomenti  
 *event_property*  
 Proprietà di un evento. Gli esempi includono **posttime**, **SPID**e **LoginName**. Cercare ogni evento elencato in [classi e proprietà del provider WMI per eventi del server](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md) per determinare le proprietà che possiede. Ad esempio, l'evento DDL_DATABASE_LEVEL_EVENTS include le proprietà **DatabaseName** e **username** . Eredita inoltre le proprietà **SQLInstance**, **LoginName**, **posttime**, **SPID**e **ComputerName** dagli eventi padre.  
  
 **,** *... n*  
 Indica che *event_property* possibile eseguire query più volte, separate da virgole.  
  
 \*  
 Specifica che tutte le proprietà associate a un evento vengono sottoposte a query.  
  
 *event_type*  
 Qualsiasi evento per il quale è possibile creare una notifica. Per un elenco degli eventi disponibili, vedere [classi e proprietà del provider WMI per eventi del server](https://technet.microsoft.com/library/ms186449.aspx). Si noti che i nomi dei *tipi di evento* corrispondono allo stesso *event_type*  |  *event_group* che è possibile specificare quando si crea manualmente una notifica degli eventi usando Crea notifica evento. Esempi di *tipo di evento* includono CREATE_TABLE, LOCK_DEADLOCK, DDL_USER_EVENTS e TRC_DATABASE.  
  
> [!NOTE]  
>  Anche determinate stored procedure di sistema che eseguono operazioni di tipo DDL possono attivare notifiche degli eventi. Testare le notifiche degli eventi per determinarne le risposte alle stored procedure di sistema eseguite. Ad esempio, l'istruzione CREATE TYPE e **sp_addtype** stored procedure genereranno una notifica degli eventi creata in un evento di CREATE_TYPE. Tuttavia, il **sp_rename** stored procedure non genera alcuna notifica degli eventi. Per ulteriori informazioni, vedere[eventi DDL](../../relational-databases/triggers/ddl-events.md).  
  
 *where_condition*  
 Predicato di query clausola WHERE costituito da nomi *event_property* e operatori logici e di confronto. Il *where_condition* determina l'ambito in cui la notifica degli eventi corrispondente è registrata nel database di destinazione. Può anche fungere da filtro per indirizzare un particolare schema o oggetto da cui eseguire una query *event_type.* Per ulteriori informazioni, vedere la sezione Osservazioni di seguito in questo argomento.  
  
 `=`È possibile utilizzare solo l'operando insieme a **DatabaseName**, **SchemaName**e **ObjectName**. Con queste proprietà di evento non è possibile utilizzare altre espressioni.  
  
## <a name="remarks"></a>Commenti  
 Il *where_condition* della sintassi del provider WMI per gli eventi del server determina quanto segue:  
  
-   Ambito dal quale il provider tenta di recuperare il *event_type*specificato, ovvero a livello di server, a livello di database o a livello di oggetto (l'unico oggetto attualmente supportato è Queue). Infine, tale ambito determina il tipo di notifica degli eventi creato nel database di destinazione. Questo processo viene chiamato registrazione della notifica degli eventi.  
  
-   Il database, lo schema e l'oggetto, se appropriato, in cui effettuare la registrazione.  
  
 Il provider WMI per eventi del server utilizza un algoritmo bottom-up, first-fit per produrre l'ambito più ristretto possibile per l'oggetto EVENT NOTIFICATION sottostante. L'algoritmo tenta di ridurre l'attività interna sul server e il traffico di rete tra l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il processo host WMI. Il provider esamina la *event_type* specificata nella clausola from e le condizioni nella clausola WHERE e tenta di registrare la notifica degli eventi sottostante con l'ambito più piccolo possibile. Se tale registrazione non riesce, prova a eseguirla nei successivi ambiti di livello più alto finché l'operazione non riesce. Se l'esito dell'operazione è ancora negativo dopo aver raggiunto l'ambito di livello più alto, ovvero il livello del server, restituisce un errore al consumer.  
  
 Se, ad esempio, si specifica DatabaseName =**'** AdventureWorks **'** nella clausola WHERE, il provider prova a registrare una notifica degli eventi nel [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] database. Se il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] esiste e il client chiamante dispone delle autorizzazioni necessarie per creare una notifica degli eventi in [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], la registrazione riesce. In caso contrario, viene eseguito un tentativo di registrazione della notifica degli eventi a livello di server. La registrazione riesce se il client WMI dispone delle autorizzazioni necessarie. In questo scenario, tuttavia, gli eventi non vengono restituiti al client finché il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] non sarà stato creato.  
  
 Il *where_condition* può fungere anche da filtro per limitare ulteriormente la query a un database, uno schema o un oggetto specifico. Si consideri, ad esempio, la query WQL seguente:  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
 A seconda del risultato del processo di registrazione, questa query WQL può essere registrata a livello di database o di server. Anche se viene registrata a livello di server, tuttavia, il provider alla fine filtra gli eventi `ALTER_TABLE` che non sono applicabili alla tabella `AdventureWorks.Sales.SalesOrderDetail`. In altre parole, il provider restituisce solo le proprietà degli eventi `ALTER_TABLE` che si verificano in quella tabella specifica.  
  
 Se si specifica un'espressione composta, ad esempio `DatabaseName='AW1'` OR `DatabaseName='AW2'`, viene effettuato il tentativo di registrare una singola notifica degli eventi nell'ambito server anziché due notifiche degli eventi separate. La registrazione riesce se il client chiamante dispone di autorizzazioni.  
  
 Se `SchemaName='X' AND ObjectType='Y' AND ObjectName='Z'` tutti gli oggetti sono specificati nella `WHERE` clausola, viene effettuato un tentativo di registrare la notifica degli eventi direttamente sull'oggetto `Z` nello schema `X` . La registrazione riesce se il client dispone di autorizzazioni. Si noti che attualmente gli eventi a livello di oggetto sono supportati solo nelle code e solo per il *event_type*QUEUE_ACTIVATION.  
  
 Notare che non tutti gli eventi possono essere sottoposti a query in qualsiasi ambito specifico. Una query WQL su un evento di traccia quale Lock_Deadlock o un gruppo di eventi di traccia quale TRC_LOCKS può essere, ad esempio, registrata solo a livello di server. Analogamente, anche l'evento CREATE_ENDPOINT e il gruppo di eventi DDL_ENDPOINT_EVENTS possono essere registrati solo a livello di server. Per ulteriori informazioni sull'ambito appropriato per la registrazione degli eventi, vedere [progettazione di notifiche degli eventi](https://technet.microsoft.com/library/ms175854\(v=sql.105\).aspx). Il tentativo di registrare una query WQL il cui *event_type* può essere registrato solo a livello di server viene sempre eseguito a livello di server. La registrazione riesce se il client WMI dispone di autorizzazioni. In caso contrario, al client viene restituito un errore. In alcuni casi, tuttavia, è ancora possibile utilizzare la clausola WHERE come filtro per gli eventi a livello di server in base alle proprietà che corrispondono all'evento. Molti eventi di traccia, ad esempio, dispongono di una proprietà **DatabaseName** che può essere utilizzata nella clausola WHERE come filtro.  
  
 Le notifiche degli eventi con ambito server vengono create nel database **Master** e possono essere sottoposte a query per i metadati utilizzando la vista del catalogo [sys. server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md) .  
  
 Le notifiche degli eventi con ambito database o oggetto vengono create nel database specificato e possono essere sottoposte a query per i metadati utilizzando la vista del catalogo [sys. event_notifications](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md) . È necessario anteporre alla vista del catalogo il nome del database corrispondente.  
  
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
 [Concetti relativi al provider WMI per eventi del server](https://technet.microsoft.com/library/ms180560.aspx)   
 [Notifiche degli eventi (Motore di database)](https://technet.microsoft.com/library/ms182602.aspx)  
  
  
