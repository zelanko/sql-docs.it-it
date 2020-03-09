---
title: Abilitazione di notifiche di query
description: Descrizione di come usare le notifiche delle query, inclusi i requisiti per abilitarle e usarle.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: e587639f5323ea76c975e3a8c35d647a7eb3d891
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896968"
---
# <a name="enabling-query-notifications"></a>Abilitazione di notifiche di query

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Le applicazioni che usano le notifiche delle query hanno un set di requisiti comune. L'origine dati dell'utente deve essere configurata correttamente per supportare le notifiche di query SQL e l'utente deve disporre delle autorizzazioni corrette sia sul lato client che sul lato server.  
  
Per usare le notifiche delle query è necessario:  
  
- Abilitare le notifiche delle query per il database.  
  
- Verificare che l'ID utente usato per la connessione al database abbia le autorizzazioni necessarie.  
  
- Usare un oggetto <xref:Microsoft.Data.SqlClient.SqlCommand> per eseguire un'istruzione SELECT valida con un oggetto notifica associato, <xref:Microsoft.Data.SqlClient.SqlDependency> o <xref:Microsoft.Data.Sql.SqlNotificationRequest>.  
  
- Specificare il codice per elaborare la notifica se i dati monitorati cambiano.  
  
## <a name="query-notifications-requirements"></a>Requisiti per le notifiche delle query  
Le notifiche delle query sono supportate solo per le istruzioni SELECT che soddisfano alcuni requisiti specifici. Nella tabella seguente vengono specificati i collegamenti alla documentazione online di SQL Server relativa a Service Broker e alle notifiche delle query.  
  
**Documentazione di SQL Server**  
  
- [Creazione di una query da notificare](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Considerazioni sulla sicurezza relative a Service Broker](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))  
  
- [Protezione e sicurezza (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))  
  
- [Considerazioni sulla sicurezza per Notification Services](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))  
  
- [Autorizzazioni relative alle notifiche delle query](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))  
  
- [Considerazioni sulle funzionalità internazionali di Service Broker](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))  
  
- [Considerazioni sulla progettazione di soluzioni (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))  
  
- [Centro informazioni per lo sviluppatore di Service Broker](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [Guida per gli sviluppatori di Service Broker](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>Abilitazione delle notifiche delle query per l'esecuzione del codice di esempio  
Per abilitare Service Broker nel database **AdventureWorks** tramite SQL Server Management Studio, eseguire l'istruzione Transact-SQL seguente:  
  
`ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
Per un'esecuzione corretta degli esempi di notifica delle query, è necessario eseguire le istruzioni Transact-SQL seguenti nel server di database.  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>Autorizzazioni delle notifiche delle query  
Gli utenti che eseguono comandi che richiedono notifiche devono avere l'autorizzazione per il database SUBSCRIBE QUERY NOTIFICATIONS nel server.  
  
Il codice lato client eseguito in una situazione di attendibilità parziale richiede <xref:Microsoft.Data.SqlClient.SqlClientPermission>.  
  
Il codice seguente crea un oggetto <xref:Microsoft.Data.SqlClient.SqlClientPermission>, impostando <xref:System.Security.Permissions.PermissionState> su <xref:System.Security.Permissions.PermissionState.Unrestricted>. <xref:System.Security.CodeAccessPermission.Demand%2A> forza un oggetto <xref:System.Security.SecurityException> in fase di esecuzione se tutti i chiamanti in posizioni superiori nello stack di chiamate non hanno l'autorizzazione.  
  
[!code-csharp[DataWorks SqlClientPermission_Demand#1](~/../sqlclient/doc/samples/SqlClientPermission_Demand.cs#1)]
  
## <a name="choosing-a-notification-object"></a>Scelta di un oggetto per la notifica  
L'API per la notifica di query fornisce due oggetti per l'elaborazione delle notifiche: <xref:Microsoft.Data.SqlClient.SqlDependency> e <xref:Microsoft.Data.Sql.SqlNotificationRequest>.
  
### <a name="using-sqldependency"></a>Uso di SqlDependency  
Per usare <xref:Microsoft.Data.SqlClient.SqlDependency>, è necessario che Service Broker sia abilitato per il database SQL Server usato e gli utenti devono disporre dell'autorizzazioni appropriate per ricevere notifiche. Gli oggetti Service Broker, come ad esempio la coda delle notifiche, sono predefiniti.  
  
Inoltre, <xref:Microsoft.Data.SqlClient.SqlDependency> avvia automaticamente un thread di lavoro per elaborare le notifiche man mano che queste vengono inviate alla coda e analizza il messaggio Service Broker esponendo le informazioni come dati dell'evento dell'argomento. <xref:Microsoft.Data.SqlClient.SqlDependency> deve essere inizializzato chiamando il metodo `Start` per stabilire una dipendenza dal database. Si tratta di un metodo statico che deve essere chiamato una sola volta durante l'inizializzazione dell'applicazione per ogni connessione al database richiesta. Il metodo `Stop` deve essere chiamato alla chiusura dell'applicazione per ogni connessione di dipendenza eseguita.  
  
### <a name="using-sqlnotificationrequest"></a>Uso di SqlNotificationRequest  
Al contrario, <xref:Microsoft.Data.Sql.SqlNotificationRequest> richiede l'implementazione dell'intera infrastruttura di ascolto. È anche necessario definire tutti gli oggetti Service Broker di supporto, ad esempio la coda, il servizio e i tipi di messaggi supportati dalla coda. Questo approccio manuale è utile se l'applicazione richiede messaggi di notifica o comportamenti di notifica speciali oppure se l'applicazione fa parte di un'applicazione Service Broker più grande.  
  
## <a name="next-steps"></a>Passaggi successivi
- [Notifiche di query in SQL Server](query-notifications-sql-server.md)
