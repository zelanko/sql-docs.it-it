---
title: Informazioni sul supporto Java EE | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a9448b80-b7a3-49cf-8bb4-322c73676005
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da575f8c0fecd03e21bc2d24800cde05105a5a3c
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/05/2019
ms.locfileid: "55736928"
---
# <a name="understanding-java-ee-support"></a>Informazioni sul supporto Java EE

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Nelle sezioni seguenti viene descritto il supporto fornito da [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] per le caratteristiche API facoltative Java Platform, Enterprise Edition (Java EE) e JDBC 3.0. Gli esempi di codice sorgente forniti in questo sistema di Guida costituiscono un buon riferimento per iniziare a utilizzare queste caratteristiche.  
  
Assicurarsi innanzitutto che l'ambiente Java (JDK, JRE) includa il pacchetto javax.sql. Questo pacchetto è necessario per qualsiasi applicazione JDBC che utilizzi l'API facoltativa. JDK 1.5 e le versioni successive contengono già questo pacchetto, pertanto non è necessario installarlo separatamente.  
  
## <a name="driver-name"></a>Nome del driver

Il nome della classe del driver è **com.microsoft.sqlserver.jdbc.SQLServerDriver**. Per JDBC Driver 4.1, 4.2 e 6.0, il driver è incluso nel file **sqljdbc.jar**, **sqljdbc4.jar**, **sqljdbc41.jar** o **sqljdbc42.jar**.

Per JDBC Driver 6.2, il driver è incluso **mssql-jdbc-6.2.2.jre7.jar** oppure **mssql-jdbc-6.2.2.jre8.jar**.

Per JDBC Driver 6.4, il driver è incluso **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar**, o **mssql-jdbc-6.4.0.jre9.jar**.

Per JDBC Driver 7.0, il driver è incluso **mssql-jdbc-7.0.0.jre8.jar**, o **mssql-jdbc-7.0.0.jre10.jar**.

Per i 7.2 di Driver JDBC, il driver è incluso **mssql-jdbc-7.2.0.jre8.jar**, o **mssql-jdbc-7.2.0.jre11.jar**.
  
Il nome della classe viene usato quando si carica il driver con la classe JDBC DriverManager, nonché quando è necessario specificare il nome della classe del driver in qualsiasi configurazione del driver. Per configurare un'origine dati all'interno di un server applicazioni Java EE potrebbe ad esempio essere necessario immettere il nome della classe del driver.  
  
## <a name="data-sources"></a>Origini dati

Il driver JDBC fornisce supporto per le origini dati Java EE e JDBC 3.0. Il driver JDBC [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) classe è implementata da `com.microsoft.sqlserver.jdbc.SQLServerXADataSource`.  
  
### <a name="datasource-names"></a>Nomi delle origini dati

È possibile stabilire connessioni al database utilizzando le origini dati. Le origini dati disponibili con il driver JDBC sono descritte nella tabella seguente:  
  
|Tipo di origine dati|Nome e descrizione della classe|  
|---------------|--------------------------|  
|DataSource|`com.microsoft.sqlserver.jdbc.SQLServerDataSource` <br/> <br/> Origine dati non per i pool.|  
|ConnectionPoolDataSource|`com.microsoft.sqlserver.jdbc.SQLServerConnectionPoolDataSource` <br/> <br/> Origine dati per la configurazione dei pool di connessioni al server applicazioni JAVA EE. Utilizzata in genere quando l'applicazione è in esecuzione in un server applicazioni JAVA EE.|  
|XADataSource|`com.microsoft.sqlserver.jdbc.SQLServerXADataSource` <br/> <br/> Origine dati per la configurazione delle origini dati JAVA EE XA. Utilizzata in genere quando l'applicazione è in esecuzione in un server applicazioni JAVA EE e in uno strumento di gestione transazioni XA.|  
  
### <a name="data-source-properties"></a>Proprietà dell'origine dati

Tutte le origini dati consentono di impostare e ottenere qualsiasi proprietà associata al set di proprietà del driver sottostante.  
  
Esempi:  
  
`setServerName("localhost");`  
`setDatabaseName("AdventureWorks");`  
  
Di seguito viene illustrato in che modo un'applicazione si connette utilizzando un'origine dati:  

```java
//initialize JNDI ..  
Context ctx = new InitialContext(System.getProperties());
...
DataSource ds = (DataSource) ctx.lookup("MyDataSource");
Connection c = ds.getConnection("user", "pwd");  
```

Per altre informazioni sulle proprietà dell'origine dati, vedere [impostando le proprietà dell'origine dati](../../connect/jdbc/setting-the-data-source-properties.md).  
  
## <a name="see-also"></a>Vedere anche

[Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
