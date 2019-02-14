---
title: Requisiti di sistema per il Driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e2ccc488c7bdac6e6e73863b55760c622a73474
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/05/2019
ms.locfileid: "55736912"
---
# <a name="system-requirements-for-the-jdbc-driver"></a>Requisiti di sistema per il driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Per accedere a dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] tramite [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], è necessario che nel computer siano installati i componenti seguenti:

- [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ([download](download-microsoft-jdbc-driver-for-sql-server.md))
- Java Runtime Environment

## <a name="java-runtime-environment-requirements"></a>Requisiti di Java Runtime Environment  

 A partire da Microsoft JDBC Driver 7.2 per SQL Server sono supportati Java Development Kit (JDK) 11.0 e Java Runtime Environment (JRE) 11.0.
 
 A partire da Microsoft JDBC Driver 7.0 per SQL Server sono supportati Java Development Kit (JDK) 10.0 e Java Runtime Environment (JRE) 10.0.

 A partire da Microsoft JDBC Driver 6.4 per SQL Server sono supportati Java Development Kit (JDK) 9.0 e Java Runtime Environment (JRE) 9.0.

 A partire da Microsoft JDBC Driver 4.2 per SQL Server sono supportati Java Development Kit (JDK) 8.0 e Java Runtime Environment (JRE) 8.0. Il supporto per l'API della specifica Java Database Connectivity (JDBC) è stato esteso in modo da includere l'API di JDBC 4.1 e 4.2.
  
 A partire da Microsoft JDBC Driver 4.1 per SQL Server sono supportati Java Development Kit (JDK) 7.0 e Java Runtime Environment (JRE) 7.0.
  
 A partire da [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], il supporto del driver JDBC per l'API della specifica Java Database Connectivity (JDBC) è stato esteso in modo da includere l'API JDBC 4.0. L'API JDBC 4.0 è stata introdotta come parte di Java Development Kit (JDK) 6.0 e Java Runtime Environment (JRE) 6.0. JDBC 4.0 è un superset dell'API di JDBC 3.0.
  
 Quando si distribuisce [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] nei sistemi operativi Windows e UNIX, è necessario usare i pacchetti di installazione, rispettivamente *sqljdbc_\<versione>_enu.exe* e *sqljdbc_\<versione>_enu.tar.gz*. Per altre informazioni su come distribuire il Driver JDBC, vedere [distribuzione del Driver JDBC](../../connect/jdbc/deploying-the-jdbc-driver.md) argomento.  

**Microsoft JDBC Driver 7.2 per SQL Server:**  

  JDBC Driver 7.2 include due librerie di classe JAR in ogni pacchetto di installazione: **mssql-jdbc-7.2.0.jre8.jar** e **mssql-jdbc-7.2.0.jre11.jar**.

  7.2 il Driver JDBC è progettato per funzionare con ed essere supportati da tutte le principali macchine virtuali Java, ma è stato testato solo su OpenJDK 8.0, OpenJDK 11.0, Azul Zulu JRE 8.0 e Azul Zulu JRE 11.0.
  
  Di seguito viene riepilogato il supporto fornito dai due file JAR inclusi in Microsoft JDBC Driver 7.2 per SQL Server:  
  
  |JAR|Conformità versione JDBC|Java versione consigliata|Descrizione|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.2.0.jre8.jar|4.2|8|Richiede un Java Runtime Environment (JRE) versione 8.0. Utilizza JRE 7.0 o inferiore genera un'eccezione.<br /><br /> Nuove funzionalità 7.2 includono: Supporto per JDK 11, l'autenticazione di Active Directory Managed Service Identity (MSI), OSGi supporto SQLServerError APIs. |    
|mssql-jdbc-7.2.0.jre11.jar|4.3|10|Richiede Java Runtime Environment (JRE) 11.0. Utilizza JRE 10.0 o inferiore genera un'eccezione.<br /><br /> Nuove funzionalità 7.2 includono: Supporto per JDK 11, l'autenticazione di Active Directory Managed Service Identity (MSI), OSGi supporto SQLServerError APIs. |    


  7.2 il Driver JDBC è disponibile anche nel Repository centrale di Maven e possono essere aggiunti a un progetto Maven aggiungendo il codice seguente nel modello POM. XML:  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.0.jre11</version>
</dependency>
```
 
**Microsoft JDBC Driver 7.0 per SQL Server**  

  JDBC Driver 7.0 include due librerie di classe JAR in ogni pacchetto di installazione: **mssql-jdbc-7.0.0.jre8.jar** e **mssql-jdbc-7.0.0.jre10.jar**.

  JDBC Driver 7.0 è progettato per funzionare con ed essere supportato da tutte le principali macchine virtuali Java, ma è testato solo su OpenJDK 8.0 e 10.0.
  
  Di seguito viene riepilogato il supporto fornito dai due file JAR inclusi in Microsoft JDBC Driver 7.0 per SQL Server:  
  
  |JAR|Conformità versione JDBC|Java versione consigliata|Descrizione|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.0.0.jre8.jar|4.2|8|Richiede un Java Runtime Environment (JRE) versione 8.0. Utilizza JRE 7.0 o inferiore genera un'eccezione.<br /><br /> Nuove funzionalità in 7.0 includono: Supporto per JDK 10, a livello di conformità predefiniti aggiornati per le specifiche JDBC 4.2, supporto di tipi di dati spaziali, proprietà di connessione cancelQueryTimeout, limiti richiesta metodi, proprietà di connessione useBulkCopyForBatchInsert, individuazione dati e classificazione informazioni, estensione della funzionalità UTF-8 e supporto CityHash. |    
|mssql-jdbc-7.0.0.jre10.jar|4.3|10|Richiede Java Runtime Environment (JRE) 10.0. Utilizza JRE 9.0 o inferiore genera un'eccezione.<br /><br /> Nuove funzionalità in 7.0 includono: Supporto per JDK 10, a livello di conformità predefiniti aggiornati per le specifiche JDBC 4.2, supporto di tipi di dati spaziali, proprietà di connessione cancelQueryTimeout, limiti richiesta metodi, proprietà di connessione useBulkCopyForBatchInsert, individuazione dati e classificazione informazioni, estensione della funzionalità UTF-8 e supporto CityHash. |    


  7.0 il Driver JDBC è disponibile anche nel Repository centrale di Maven e possono essere aggiunti a un progetto Maven aggiungendo il codice seguente nel modello POM. XML:  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
</dependency>
```
  
**Microsoft JDBC Driver 6.4 per SQL Server**  

  JDBC Driver 6.4 include tre librerie di classe JAR in ogni pacchetto di installazione: **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** e **mssql-jdbc-6.4.0.jre9.jar**.

  JDBC Driver 6.4 è progettato per funzionare con ed essere supportato da tutte le principali macchine virtuali Java, ma è testato solo su OpenJDK 7.0, 8.0 e 9.0.
  
  Di seguito viene riepilogato il supporto fornito dai tre file JAR inclusi in Microsoft JDBC Driver 6.4 per SQL Server:  
  
  |JAR|Conformità versione JDBC|Java versione consigliata|Descrizione|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|Richiede un Java Runtime Environment (JRE) versione 7.0. Utilizza JRE 6.0 o inferiore genera un'eccezione.<br /><br /> Nuove funzionalità in 6.4 includono: Usare nuovamente l'autenticazione AD Azure per Linux, il metodo di entità e la Password di Kerberos, il rilevamento automatico di REALM in SPN per l'autenticazione tra domini, la delega vincolata Kerberos, Timeout della Query, il timeout del Socket e handle di istruzione preparata. |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|Richiede un Java Runtime Environment (JRE) versione 8.0. Utilizza JRE 7.0 o inferiore genera un'eccezione.<br /><br /> Nuove funzionalità in 6.4 includono: Usare nuovamente l'autenticazione AD Azure per Linux, il metodo di entità e la Password di Kerberos, il rilevamento automatico di REALM in SPN per l'autenticazione tra domini, la delega vincolata Kerberos, Timeout della Query, il timeout del Socket e handle di istruzione preparata. |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|Richiede Java Runtime Environment (JRE) 9.0. Utilizzo di JRE 8.0 o inferiore genera un'eccezione.<br /><br /> Nuove funzionalità in 6.4 includono: Usare nuovamente l'autenticazione AD Azure per Linux, il metodo di entità e la Password di Kerberos, il rilevamento automatico di REALM in SPN per l'autenticazione tra domini, la delega vincolata Kerberos, Timeout della Query, il timeout del Socket e handle di istruzione preparata. |

JDBC Driver 6.4 è disponibile anche nel Repository centrale di Maven e possono essere aggiunti a un progetto Maven aggiungendo il codice seguente nel modello POM. XML 

 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```

**Microsoft JDBC Driver 6.2 per SQL Server:**  
  
  JDBC Driver 6.2 include due librerie di classe JAR in ogni pacchetto di installazione: **mssql-jdbc-6.2.2.jre7.jar** e **mssql-jdbc-6.2.2.jre8.jar**. 
  
 JDBC Driver 6.2 è progettato per funzionare con ed essere supportato da tutte le principali macchine virtuali Java, ma è testato solo su Sun JRE 5.0, 6.0, 7.0 e 8.0.
  
 Di seguito viene offerto un riepilogo del supporto fornito dai due file JAR inclusi in Microsoft JDBC Driver 6.0 e 4.2 per SQL Server:  
  
|JAR|Conformità versione JDBC|Java versione consigliata|Descrizione|  
|---------|-----------------------------|----------------------|-----------------|
|mssql-jdbc-6.2.2.jre7.jar|4.1|7|Richiede un Java Runtime Environment (JRE) versione 7.0. Utilizza JRE 6.0 o inferiore genera un'eccezione.<br /><br /> Nuove funzionalità in 6.2 includono: Usare nuovamente l'autenticazione AD Azure per Linux, il metodo di entità e la Password di Kerberos, il rilevamento automatico di REALM in SPN per l'autenticazione tra domini, la delega vincolata Kerberos, Timeout della Query, il timeout del Socket e handle di istruzione preparata. |  
|mssql-jdbc-6.2.3.jre8.jar|4.2|8|Richiede un Java Runtime Environment (JRE) versione 8.0. Utilizza JRE 7.0 o inferiore genera un'eccezione.<br /><br /> Nuove funzionalità in 6.2 includono: Usare nuovamente l'autenticazione AD Azure per Linux, il metodo di entità e la Password di Kerberos, il rilevamento automatico di REALM in SPN per l'autenticazione tra domini, la delega vincolata Kerberos, Timeout della Query, il timeout del Socket e handle di istruzione preparata|    

  JDBC Driver 6.2 è disponibile anche nel Repository centrale di Maven e possono essere aggiunti a un progetto Maven aggiungendo il codice seguente nel modello POM. XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.2.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 e 4.2 per SQL Server:**  
  
  JDBC Drivers 6.0 e 4.2 includono due librerie di classi JAR in ogni pacchetto di installazione: **sqljdbc41.jar**, e **sqljdbc42.jar**. 
  
 JDBC Driver 6.0 e 4.2 sono progettati per funzionare con ed essere supportati da tutte le principali macchine virtuali Java, ma sono testati solo su Sun JRE 5.0, 6.0, 7.0 e 8.0.
  
 Di seguito viene offerto un riepilogo del supporto fornito dai due file JAR inclusi in Microsoft JDBC Driver 6.0 e 4.2 per SQL Server:  
  
|JAR|Conformità versione JDBC|Java versione consigliata|Descrizione|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|Richiede un Java Runtime Environment (JRE) versione 7.0. Utilizza JRE 6.0 o inferiore genera un'eccezione.<br /><br /> Nuove funzionalità nei pacchetti 6.0 & 4.2 includono: JDBC 4.1 di conformità e la copia Bulk<br /><br /> Inoltre, le nuove funzionalità nel solo pacchetto 6.0 includono: Always Encrypted, i parametri con valori di tabella, autenticazione Azure Active Directory, le connessioni trasparenti ai gruppi di disponibilità AlwaysOn, miglioramento nel recupero di metadati di parametro di query preparata e IDN (Internationalized Domain Name)|  
|sqljdbc42.jar|4.2|8|Richiede un Java Runtime Environment (JRE) versione 8.0. Utilizza JRE 7.0 o inferiore genera un'eccezione.<br /><br /> Nuove funzionalità nei pacchetti 6.0 & 4.2 includono: JDBC 4.1 con JDBC 4.2, conformità, di conformità e la copia Bulk<br /><br /> Inoltre, le nuove funzionalità nel solo pacchetto 6.0 includono: Always Encrypted, i parametri con valori di tabella, autenticazione Azure Active Directory, le connessioni trasparenti ai gruppi di disponibilità AlwaysOn, miglioramento nel recupero di metadati di parametro di query preparata e IDN (Internationalized Domain Name)|  
  
 **Microsoft JDBC Driver 4.1 per SQL Server:**  
  
 JDBC Driver 4.1 include una libreria di classi JAR in ogni pacchetto di installazione: **sqljdbc41.jar**.  
    
|JAR|Descrizione|  
|---------|-----------------|  
|sqljdbc41.jar|La libreria di classi **sqljdbc41.jar** fornisce il supporto per l'API JDBC 4.0 e include tutte le funzionalità di JDBC 4.0 Driver, nonché i metodi dell'API JDBC 4.0. JDBC 4.1 non è supportato (viene generata un'eccezione "SQLFeatureNotSupportedException").<br /><br /> La libreria di classi **sqljdbc41.jar** richiede Java Runtime Environment (JRE) 7.0. Usando **sqljdbc41.jar** in JRE 6.0 e 5.0 genera un'eccezione.<br /><br /> 
  
 JDBC Driver è progettato per funzionare con ed essere supportato da tutte le principali macchine virtuali Java, ma è testato solo su Sun JRE 5.0, 6.0 e 7.0.
  
 Di seguito viene riepilogato il supporto fornito dal file JAR incluso con Microsoft JDBC Driver 4.1 per SQL Server.  
  
|JAR|Versione JDBC|JRE (esecuzione)|JDK (compilazione)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>Requisiti di SQL Server  
 JDBC Driver supporta le connessioni al database SQL di Azure e a SQL Server. Per Microsoft JDBC Driver 4.2 e 4.1 per SQL Server, il supporto inizia con SQL Server 2008.
  
## <a name="operating-system-requirements"></a>Requisiti del sistema operativo  
 Il driver JDBC è stato sviluppato per essere utilizzato su qualsiasi sistema operativo che supporti l'utilizzo di Java Virtual Machine (JVM). Ufficialmente, tuttavia, sono stati testati solo i sistemi operativi Sun Solaris, SUSE Linux e Windows.  
  
## <a name="supported-languages"></a>Lingue supportate  
 JDBC Driver supporta tutte le regole di confronto delle colonne di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni sulle regole di confronto supportate dal driver JDBC, vedere [funzioni internazionali del Driver JDBC](../../connect/jdbc/international-features-of-the-jdbc-driver.md).  
  
 Per altre informazioni sulle regole di confronto, vedere "Uso delle regole di confronto" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
