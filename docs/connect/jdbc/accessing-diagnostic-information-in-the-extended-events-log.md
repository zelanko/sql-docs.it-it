---
title: Accesso alle informazioni di diagnostica nel log degli eventi estesi
description: Informazioni su come accedere agli eventi estesi nel server correlati a eventi da Microsoft JDBC Driver per SQL Server.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a79e9468-2257-4536-91f1-73b008c376c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 98d2ffca0ca9f8bab6f481ddf654bd388ecba4d7
ms.sourcegitcommit: 37a3e2c022c578fc3a54ebee66d9957ff7476922
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922256"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Accesso alle informazioni di diagnostica nel log degli eventi estesi
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  In [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] con l'aggiornamento della traccia ([Creazione di tracce](../../connect/jdbc/tracing-driver-operation.md)) è stato possibile semplificare la correlazione di eventi client con informazioni di diagnostica, ad esempio errori di connessione, provenienti dal buffer circolare della connettività del server e informazioni sulle prestazioni dell'applicazione nel log degli eventi estesi. Per informazioni sulla lettura del registro eventi esteso, vedere [Eventi estesi](../../relational-databases/extended-events/extended-events.md).  
  
## <a name="details"></a>Dettagli  
 Per operazioni di connessione, tramite [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] verrà inviato un ID connessione client. In caso di errore di connessione, è possibile accedere al buffer circolare della connettività, [Connectivity troubleshooting in SQL Server 2008 with the Connectivity Ring Buffer](/archive/blogs/sql_protocols/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer) (Risoluzione dei problemi relativi alla connettività in SQL Server 2008 con il buffer circolare della connettività), individuare il campo **ClientConnectionID** e ottenere le informazioni di diagnostica sul problema di connessione. Gli ID di connessione client vengono registrati nel buffer circolare solo se si verifica un errore. In caso di errore di connessione prima dell'invio del pacchetto di preaccesso, l'ID di connessione client non verrà generato. L'ID di connessione client è un GUID a 16 byte. È possibile trovare l'ID di connessione client anche nell'output di destinazione degli eventi estesi, se l'azione **client_connection_id** viene aggiunta agli eventi in una sessione di eventi estesi. Se si necessita di un ulteriore supporto diagnostico del driver client, è possibile abilitare la traccia e rieseguire il comando di connessione per osservare il campo **ClientConnectionID** nella traccia.  
  
 È possibile ottenere l'ID di connessione client a livello di codice usando l'[interfaccia ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md). L'ID connessione sarà inoltre disponibile in tutte le eccezioni correlate alla connessione.  
  
 Quando si verifica un errore di connessione, con l'ID connessione client nelle informazioni relative alla traccia Built-In Diagnostics (BID) del server e nel buffer circolare è possibile semplificare la correlazione delle connessioni client alle connessioni nel server. Per altre informazioni sulle tracce BID nel server, vedere la pagina relativa alla [traccia di accesso ai dati](https://go.microsoft.com/fwlink/?LinkId=125805). Si noti che nell'articolo sulla traccia di accesso ai dati sono inoltre contenute informazioni su una traccia di accesso ai dati che non si applica a [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]. Vedere [Creazione di tracce](../../connect/jdbc/tracing-driver-operation.md) per informazioni sull'esecuzione di una traccia di accesso ai dati usando [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 Il driver JDBC invia anche un ID attività specifico del thread. L'ID attività viene acquisito nelle sessioni di eventi estesi se avviate con l'opzione TRACK_CAUSAILITY abilitata. Per problemi di prestazioni con una connessione attiva, è possibile ottenere l'ID attività dalla traccia del client (campo ActivityID) e quindi individuare l'ID attività nell'output degli eventi estesi. L'ID attività negli eventi estesi è un GUID a 16 byte, non lo stesso del GUID per l'ID connessione client, aggiunto con un numero di sequenza a 4 byte. Il numero di sequenza rappresenta l'ordine di una richiesta all'interno di un thread. ActivityId viene inviato per le istruzioni batch SQL e per le richieste RPC. Per abilitare l'invio di ActivityId al server, è innanzitutto necessario specificare la seguente coppia chiave-valore nel file Logging.Properties:  
  
```
com.microsoft.sqlserver.jdbc.traceactivity = on  
```  
  
 Qualsiasi valore diverso da `on` (con distinzione tra maiuscole e minuscole) disabiliterà l'invio di ActivityId.  
  
 Per altre informazioni, vedere [Creazione di tracce](../../connect/jdbc/tracing-driver-operation.md). Questo flag di traccia viene utilizzato con i logger degli oggetti JDBC corrispondenti per stabilire se tracciare e inviare ActivityId nel driver JDBC. Oltre ad aggiornare il file Logging.Properties, è necessario abilitare il logger com.microsoft.sqlserver.jdbc al livello FINER o superiore. Se si vuole inviare ActivityId al server per le richieste effettuate da una classe specifica, è necessario abilitare il logger della classe corrispondente al livello FINER o FINEST. Se ad esempio la classe è SQLServerStatement, abilitare il logger com.microsoft.sqlserver.jdbc.SQLServerStatement.  
  
 Di seguito è riportato un esempio in cui viene usato [!INCLUDE[tsql](../../includes/tsql-md.md)] per avviare una sessione di eventi estesi che verrà archiviata in un buffer circolare e che registrerà l'ID attività inviato da un client nelle operazioni batch e RPC:  
  
```sql
create event session MySession on server  
add event connectivity_ring_buffer_recorded,  
add event sql_statement_starting (action (client_connection_id)),  
add event sql_statement_completed (action (client_connection_id)),  
add event rpc_starting (action (client_connection_id)),  
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## <a name="see-also"></a>Vedere anche

[Diagnosi dei problemi relativi al driver JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
