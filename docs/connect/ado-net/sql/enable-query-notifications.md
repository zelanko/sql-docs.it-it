---
title: Abilitazione di notifiche di query
description: Viene illustrato come utilizzare le notifiche delle query, inclusi i requisiti per l'abilitazione e l'utilizzo.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 94b472a1fe040aa3a684d9f7b523ba09c82a651e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452230"
---
# <a name="enabling-query-notifications"></a>Abilitazione di notifiche di query

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Le applicazioni che utilizzano le notifiche di query hanno un insieme comune di requisiti. L'origine dati dell'utente deve essere configurata correttamente per supportare le notifiche di query SQL e l'utente deve disporre delle autorizzazioni corrette sia sul lato client che sul lato server.  
  
Per usare le notifiche di query è necessario:  
  
- Abilitare le notifiche delle query per il database.  
  
- Verificare che l'ID utente utilizzato per la connessione al database disponga delle autorizzazioni necessarie.  
  
- Utilizzare un oggetto <xref:Microsoft.Data.SqlClient.SqlCommand> per eseguire un'istruzione SELECT valida con un oggetto notifica associato, sia <xref:Microsoft.Data.SqlClient.SqlDependency> che <xref:Microsoft.Data.Sql.SqlNotificationRequest>.  
  
- Fornire il codice per elaborare la notifica se i dati monitorati cambiano.  
  
## <a name="query-notifications-requirements"></a>Requisiti per le notifiche delle query  
Le notifiche delle query sono supportate solo per le istruzioni SELECT che soddisfano un elenco di requisiti specifici. Nella tabella seguente vengono forniti i collegamenti alla documentazione relativa a Service Broker e notifiche delle query in documentazione online di SQL Server.  
  
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
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>Attivazione delle notifiche di query per l'esecuzione del codice di esempio  
Per abilitare Service Broker nel database **AdventureWorks** tramite SQL Server Management Studio, eseguire l'istruzione Transact-SQL seguente:  
  
`ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
Per una corretta esecuzione degli esempi di notifica delle query, è necessario eseguire le istruzioni Transact-SQL seguenti sul server di database.  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>Autorizzazioni per le notifiche delle query  
Gli utenti che eseguono comandi che richiedono notifiche devono disporre dell'autorizzazione per il database di notifiche delle QUERY di sottoscrizione nel server.  
  
Il codice lato client eseguito in una situazione di attendibilità parziale richiede il <xref:Microsoft.Data.SqlClient.SqlClientPermission>.  
  
Il codice seguente crea un oggetto <xref:Microsoft.Data.SqlClient.SqlClientPermission>, impostando il <xref:System.Security.Permissions.PermissionState> su <xref:System.Security.Permissions.PermissionState.Unrestricted>. Il <xref:System.Security.CodeAccessPermission.Demand%2A> forza una <xref:System.Security.SecurityException> in fase di esecuzione se a tutti i chiamanti più in alto nello stack di chiamate non è stata concessa l'autorizzazione.  
  
[!code-csharp[DataWorks SqlClientPermission_Demand#1](~/../sqlclient/doc/samples/SqlClientPermission_Demand.cs#1)]
  
## <a name="choosing-a-notification-object"></a>Scelta di un oggetto notifica  
L'API per la notifica di query fornisce due oggetti per l'elaborazione delle notifiche: <xref:Microsoft.Data.SqlClient.SqlDependency> e <xref:Microsoft.Data.Sql.SqlNotificationRequest>.
  
### <a name="using-sqldependency"></a>Utilizzo di SqlDependency  
Per usare <xref:Microsoft.Data.SqlClient.SqlDependency>, è necessario che Service Broker sia abilitato per il database SQL Server usato e gli utenti devono disporre dell'autorizzazioni appropriate per ricevere notifiche. Service Broker oggetti, ad esempio la coda delle notifiche, sono predefiniti.  
  
Inoltre, <xref:Microsoft.Data.SqlClient.SqlDependency> avvia automaticamente un thread di lavoro per elaborare le notifiche man mano che vengono inviate alla coda. analizza anche il messaggio di Service Broker, esponendo le informazioni come dati dell'argomento dell'evento. <xref:Microsoft.Data.SqlClient.SqlDependency> deve essere inizializzato chiamando il metodo `Start` per stabilire una dipendenza dal database. Si tratta di un metodo statico che deve essere chiamato una sola volta durante l'inizializzazione dell'applicazione per ogni connessione al database richiesta. Il metodo di `Stop` deve essere chiamato alla chiusura dell'applicazione per ogni connessione di dipendenza eseguita.  
  
### <a name="using-sqlnotificationrequest"></a>Uso di SqlNotificationRequest  
Al contrario, <xref:Microsoft.Data.Sql.SqlNotificationRequest> necessario implementare l'intera infrastruttura di ascolto autonomamente. Inoltre, è necessario definire tutti gli oggetti Service Broker di supporto, ad esempio la coda, il servizio e i tipi di messaggi supportati dalla coda. Questo approccio manuale è utile se l'applicazione richiede messaggi di notifica speciali o comportamenti di notifica oppure se l'applicazione fa parte di un'applicazione Service Broker più grande.  
  
## <a name="next-steps"></a>Passaggi successivi
- [Notifiche di query in SQL Server](query-notifications-sql-server.md)
