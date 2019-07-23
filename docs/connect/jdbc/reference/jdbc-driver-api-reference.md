---
title: Informazioni di riferimento sulle API del driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4e1ae9d-18a6-41db-8bd2-9cf0eee4cccb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04cbe39698a99fbde43043b70bb9b1f0e5887f58
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977007"
---
# <a name="jdbc-driver-api-reference"></a>Riferimento all'API del driver JDBC

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Il [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] specifica un'API che può essere usata all'interno del codice di programmazione Java per connettersi e interagire con un database [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].



### <a name="javadocio-website-is-primary"></a>Il sito Web JavaDoc.io è primario

La documentazione di riferimento dell'API Microsoft JDBC è ospitata per la visualizzazione nel sito Web JavaDoc.io. JavaDoc.io è ora il nostro sito Web principale per la documentazione di riferimento per JDBC. La documentazione di riferimento per JDBC su JavaDoc.io è disponibile nel collegamento diretto seguente:

- [https://javadoc.io/doc/com.microsoft.sqlserver/mssql-jdbc/](https://javadoc.io/doc/com.microsoft.sqlserver/mssql-jdbc/)

JavaDoc.io include la documentazione di riferimento per JDBC a partire dalla versione 6,0.

#### <a name="only-legacy-jdbc-documentation-is-here-on-docs"></a>Solo la documentazione di JDBC legacy è disponibile qui in docs

Gli articoli della documentazione di riferimento dell'API **https://docs.microsoft.com/sql/connect/jdbc/reference/** JDBC qui in non vengono più aggiornati quando le classi JDBC vengono aggiornate per le nuove versioni. Tuttavia, gli articoli qui contengono tutti i riferimenti per le versioni JDBC 4,1 e 4,2.

Qui è disponibile anche la documentazione per JDBC versione 6,0 e alcune versioni successive. Tuttavia, per qualsiasi versione 6,0 o successiva, usare il sito Web JavaDoc.io.



### <a name="important-notes"></a>Note importanti

> [!NOTE]  
>  Per informazioni concettuali sull'utilizzo del driver JDBC per, vedere [Cenni preliminari sul driver JDBC](../../../connect/jdbc/overview-of-the-jdbc-driver.md).  
  
> [!IMPORTANT]  
>  Per il supporto della conformità con JDBC 4.1 e 4.2, usare Microsoft JDBC Driver 4.2, o versione successiva, per SQL Server. Le precedenti versioni Microsoft JDBC Drivers 4.1 e 4.0 non supportano i nuovi metodi introdotti con JDBC 4.1 o 4.2.  
>   
>  I dettagli dell'API per la conformità con JDBC 4.1 non sono riportati in questa sezione. Vedere [Conformità con JDBC 4.1 per JDBC Driver](../../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md).  
>   
>  I dettagli dell'API per la conformità con JDBC 4.2 non sono riportati in questa sezione. Vedere [Conformità con JDBC 4.2 per JDBC Driver](../../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).  
>   
>  I dettagli dell'API per la funzionalità di copia bulk, disponibile in Microsoft JDBC Driver 4.2 per SQL Server, non sono riportati in questa sezione. Vedere [Uso della copia bulk con il driver JDBC](../../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).  
>   
>  I dettagli dell'API per Always Encrypted, disponibili a partire da Microsoft JDBC Driver 6.0 per SQL Server, non disponibili in questa sezione. Vedere [Informazioni di riferimento sull'API Always Encrypted per il driver JDBC](../../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  
>   
>  I dettagli dell'API per l'uso di parametri con valori di tabella, disponibili a partire da Microsoft JDBC Driver 6,0 per SQL Server, non sono stati trovati in questa sezione. Vedere [Uso di parametri con valori di tabella](../../../connect/jdbc/using-table-valued-parameters.md)  
>   
>  Microsoft JDBC Driver 6.4 supporta la compilazione con JDK 7.0, 8.0 e 9.0.  
>   
>  Microsoft JDBC Driver 6.2 supporta la compilazione con JDK 7.0 e 8.0.  
>   
>  Microsoft JDBC Driver 6.0 e 4.2 supportano la compilazione con JDK 5.0, 6.0 7.0 e 8.0.  
>   
>  Microsoft JDBC Driver 4.1 supporta la compilazione con JDK 5.0, 6.0 e 7.0.  



## <a name="interfaces"></a>Interfacce  
  
|Nome interfaccia|Descrizione|  
|--------------------|-----------------|  
|[Interfaccia ISQLServerCallableStatement](../../../connect/jdbc/reference/isqlservercallablestatement-interface.md)|Consente di specificare il nome della stored procedure da chiamare insieme ai parametri di input e di output.|  
|[Interfaccia ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md)|Rappresenta una connessione JDBC a un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)|Rappresenta un elenco di proprietà specifiche della connessione a un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando un oggetto [ISQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).|  
|[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)|Rappresenta l'implementazione di base della funzionalità dell'istruzione preparata di JDBC.|  
|[ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)|Rappresenta un set di risultati JDBC.|  
|[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)|Rappresenta l'implementazione di base della funzionalità dell'istruzione JDBC.|
| &nbsp; | &nbsp; |


  
## <a name="classes"></a>Classi  
  
|Nome classe|Descrizione|  
|----------------|-----------------|  
|[DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)|Rappresenta un oggetto di tipo microsoft.sql.DateTimeOffset.|  
|[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)|Rappresenta un oggetto BLOB (Binary Large Object).|  
|[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)|Implementa l'oggetto ISQLServerCallableStatement.|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)|Rappresenta un oggetto CLOB (Character Large Binary Object).|  
|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)|Implementa l'oggetto ISQLServerConnectopn.|  
|[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)|Rappresenta connessioni di database fisiche per le gestioni dei pool di connessioni.|  
|[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)|Rappresenta i metadati per il database.|  
|[SQLServerDataSource](../../../connect/jdbc/reference/isqlserverdatasource-interface.md)|Rappresenta un elenco di proprietà specifiche della connessione a un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando un oggetto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).|  
|[SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)|Rappresenta una object factory per la materializzazione delle origini dati dall'interfaccia JNDI (Java Naming and Directory Interface).|  
|[SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)|Rappresenta il driver JDBC. Questa classe include metodi per la connessione a un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e per il recupero di informazioni sul driver JDBC.|  
|[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)|Rappresenta un'esecuzione non riuscita o incompleta di un'istruzione SQL.|  
|[Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)|Rappresenta un oggetto CLOB (Character Large Binary Object) che utilizza il set di caratteri nazionali.|  
|[SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)|Rappresenta i metadati per i parametri delle istruzioni preparate.|  
|[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)|Rappresenta una connessione di database fisica in un pool di connessioni.|  
|[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)|Implementa l'oggetto ISQLServerPreparedStatement.|  
|[SQLServerResource](../../../connect/jdbc/reference/sqlserverresource-class.md)|Rappresenta una risorsa di tipo stringa di errore localizzata. Questa classe è destinata al solo uso interno.|  
|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)|Implementa l'oggetto ISQLServerResultSet.|  
|[SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)|Rappresenta i metadati delle colonne contenute in un set di risultati.|  
|[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)|Rappresenta il checkpoint in corrispondenza del quale può essere eseguito il rollback di una transazione.|  
|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)|Implementa l'oggetto ISQLServerStatement.|  
|[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)|Rappresenta le connessioni JDBC che possono partecipare alle transazioni distribuite (XA).|  
|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)|Rappresenta una factory per oggetti [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) usata internamente.|  
|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)|Rappresenta un oggetto XAResource per la gestione di transazioni distribuite XA.|
| &nbsp; | &nbsp; |



## <a name="see-also"></a>Vedere anche  
 [Panoramica del driver JDBC](../../../connect/jdbc/overview-of-the-jdbc-driver.md)

