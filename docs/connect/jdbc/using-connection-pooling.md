---
title: Uso del pool di connessioni | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 699d4e8a-34bf-4c60-b0d5-4a10dad6084a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69aa4d7f29d8c7963f9b300f868bc8265cde2fd0
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026368"
---
# <a name="using-connection-pooling"></a>Uso del pool di connessioni

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornisce supporto per il pool di connessioni Java Platform, Enterprise Edition (Java EE). Il driver JDBC implementa le interfacce richieste della versione JDBC 3.0 per consentire al driver di partecipare all'implementazione del pool di connessioni del fornitore di applicazioni middleware conformi con JDBC 3.0. Applicazioni middleware quali i server di applicazioni Java EE offrono spesso servizi aggiuntivi conformi con il pool di connessioni. Il driver JDBC parteciperà alle connessioni in pool in questi ambienti.  
  
> [!NOTE]  
> Sebbene il driver JDBC supporti il pool di connessioni Java EE, non è tuttavia in grado di fornire la propria implementazione del pool. Per la gestione delle connessioni, il driver si basa su server applicazioni Java di terze parti.  
  
## <a name="remarks"></a>Remarks

Le classi per l'implementazione del pool di connessioni sono le seguenti:  
  
| Classe                                                           | Implementa                                                    | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --------------------------------------------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| com.microsoft.sqlserver.jdbc. SQLServerXADataSource             | javax.sql.ConnectionPoolDataSource e javax.sql.XADataSource | È consigliabile usare la classe [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) per tutte le esigenze del server Java EE, in quanto implementa tutte le interfacce del pool JDBC 3.0 e XA.                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| com.microsoft.sqlserver.jdbc. SQLServerConnectionPoolDataSource | javax.sql.ConnectionPoolDataSource                            | Questa classe è una connection factory che consente al server applicazioni Java EE di inserire il proprio pool di connessioni nelle connessioni fisiche. Se la configurazione del fornitore Java EE richiede una classe che implementa javax.sql.ConnectionPoolDataSource, specificare il nome della classe come [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md). In genere si consiglia di usare la classe [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) in quanto implementa entrambe le interfacce di pool e XA ed è stata verificata in più configurazioni del server Java EE. |
  
 Il codice dell'applicazione JDBC deve sempre chiudere esplicitamente le connessioni per trarre il massimo vantaggio dal pool. Quando l'applicazione chiude in modo esplicito una connessione, l'implementazione del pool consente di riutilizzare immediatamente la connessione. Se la connessione non viene chiusa, le altre applicazioni non possono riutilizzarla. Le applicazioni possono usare il costrutto `finally` per assicurarsi che le connessioni in pool siano chiuse anche se si è verificata un'eccezione.  
  
> [!NOTE]  
> Il driver JDBC non chiama attualmente la stored procedure sp_reset_connection quando restituisce la connessione al pool, ma si basa su server applicazioni Java di terze parti per restituire le connessioni allo stato originale.  
  
## <a name="see-also"></a>Vedere anche

[Connessione a SQL Server con il driver JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
