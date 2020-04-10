---
title: Creazione di tracce per le operazioni del driver | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 723aeae7-6504-4585-ba8b-3525115bea8b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb926c0696f0e926f91297ee5b719bbafce3eda8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909127"
---
# <a name="tracing-driver-operation"></a>Creazione di tracce
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] supporta l'uso della traccia, o registrazione, per semplificare la risoluzione dei problemi relativi all'uso del driver JDBC nell'applicazione. Per abilitare l'utilizzo delle tracce, nel driver JDBC vengono utilizzate le API di registrazione in java.util.logging, che mettono a disposizione un set di classi per la creazione degli oggetti Logger e LogRecord.  
  
> [!NOTE]  
>  Per il componente nativo (sqljdbc_xa.dll) incluso nel driver JDBC, la creazione di tracce è abilitata grazie al framework Built-In Diagnostics (BID). Per informazioni sul BID, vedere la pagina relativa alla [traccia di accesso ai dati in SQL Server](https://go.microsoft.com/fwlink/?LinkId=70042).  
  
 Quando si sviluppa l'applicazione, è possibile eseguire chiamate a oggetti Logger che consentono di creare oggetti LogRecord, i quali vengono quindi passati a oggetti Handler per l'elaborazione. Sia per gli oggetti Logger che per gli oggetti Handler vengono usati i livelli di registrazione e, facoltativamente, i filtri di registrazione per definire quali LogRecord elaborare. Al termine delle operazioni di registrazione, con gli oggetti Handler possono facoltativamente essere utilizzati gli oggetti Formatter per pubblicare le informazioni sul log.  
  
 Per impostazione predefinita, l'output del framework java.util.logging viene scritto su un file. Tale file deve disporre di autorizzazioni di scrittura per il contesto su cui è in esecuzione il driver JDBC.  
  
> [!NOTE]  
>  Per ulteriori informazioni sull'utilizzo dei vari oggetti di registrazione per la creazione di tracce dei programmi, vedere la documentazione Java Logging APIs (informazioni in lingua inglese) sul sito Web di Sun Microsystems.  
  
 Nelle sezioni seguenti sono descritti i livelli di registrazione e le categorie che è possibile registrare. Vengono inoltre fornite informazioni sull'abilitazione della creazione di tracce nell'applicazione.  
  
## <a name="logging-levels"></a>Livelli di registrazione  
 A ciascun messaggio di log creato è associato un livello di registrazione. Tale livello determina l'importanza del messaggio. Il livello è definito dalla classe **Level** in java.util.logging. Se abilitata per un livello, la registrazione verrà abilitata per tutti i livelli superiori. In questa sezione vengono descritti i livelli di registrazione per le categorie di registrazione pubbliche e interne. Per altre informazioni sulle categorie di registrazione, vedere la sezione Categorie di registrazione in questo articolo.  
  
 Nella tabella seguente sono descritti i vari livelli di registrazione disponibili per le categorie di registrazione pubbliche.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|SEVERE|Indica un problema grave. Si tratta del livello più elevato. Nel driver JDBC viene utilizzato per segnalare errori ed eccezioni.|  
|WARNING|Indica un potenziale problema.|  
|INFO|Fornisce messaggi informativi.|  
|CONFIG|Fornisce messaggi sulla configurazione. Si noti che il driver JDBC non fornisce attualmente alcun messaggio sulla configurazione.|  
|FINE|Fornisce informazioni di base sulle tracce, incluse tutte le eccezioni generate dai metodi pubblici.|  
|FINER|Fornisce informazioni dettagliate sulle tracce, inclusi tutti i punti di ingresso e di uscita dei metodi pubblici con i tipi di dati dei parametri associati, nonché le proprietà pubbliche per le classi pubbliche. Fornisce inoltre parametri di input, parametri di output e valori restituiti del metodo ad eccezione dei tipi di valori restituiti CLOB, BLOB, NCLOB, Reader, \<stream>.|  
|FINEST|Fornisce le informazioni più dettagliate disponibili sulle tracce. È il livello più basso.|  
|OFF|Disattiva la registrazione.|  
|ALL|Abilita la registrazione di tutti i messaggi.|  
  
 Nella tabella seguente sono descritti i vari livelli di registrazione disponibili per le categorie di registrazione interne.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|SEVERE|Indica un problema grave. Si tratta del livello più elevato. Nel driver JDBC viene utilizzato per segnalare errori ed eccezioni.|  
|WARNING|Indica un potenziale problema.|  
|INFO|Fornisce messaggi informativi.|  
|FINE|Fornisce informazioni di base sulle tracce, incluse la creazione e l'eliminazione di oggetti di base. Fornisce inoltre tutte le eccezioni generate dai metodi pubblici.|  
|FINER|Fornisce informazioni dettagliate sulle tracce, inclusi tutti i punti di ingresso e di uscita dei metodi pubblici con i tipi di dati dei parametri associati, nonché le proprietà pubbliche per le classi pubbliche. Fornisce inoltre parametri di input, parametri di output e valori restituiti del metodo ad eccezione dei tipi di valori restituiti CLOB, BLOB, NCLOB, Reader, \<stream>.<br /><br /> Le seguenti categorie di registrazione erano incluse nella versione 1.2 del driver JDBC con il livello di registrazione FINE: [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md), [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), XA e [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md). A partire dalla versione 2.0 sono state aggiornate al livello FINER.|  
|FINEST|Fornisce le informazioni più dettagliate disponibili sulle tracce. È il livello più basso.<br /><br /> Le seguenti categorie di registrazione erano incluse nella versione 1.2 del driver JDBC con il livello di registrazione FINEST: TDS.DATA e TDS.TOKEN. A partire dalla versione 2.0 hanno mantenuto lo stesso livello di registrazione.|  
|OFF|Disattiva la registrazione.|  
|ALL|Abilita la registrazione di tutti i messaggi.|  
  
## <a name="logging-categories"></a>Categorie di registrazione  
 Quando si crea un oggetto Logger, è necessario indicare la categoria o l'entità denominata da cui si desidera ricevere le informazioni sul log. Il driver JDBC supporta le seguenti categorie di registrazione pubbliche, definite tutte nel pacchetto di driver com.microsoft.sqlserver.jdbc.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|Connessione|Consente di registrare i messaggi nella classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Le applicazioni possono impostare il livello di registrazione su FINER.|  
|.|Consente di registrare i messaggi nella classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). Le applicazioni possono impostare il livello di registrazione su FINER.|  
|DataSource|Consente di registrare i messaggi nella classe [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md). Le applicazioni possono impostare il livello di registrazione su FINE.|  
|ResultSet|Consente di registrare i messaggi nella classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md). Le applicazioni possono impostare il livello di registrazione su FINER.|  
|Driver|Consente di registrare i messaggi nella classe [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md). Le applicazioni possono impostare il livello di registrazione su FINER.|  
  
 A partire dalla versione 2.0, il driver Microsoft JDBC fornisce anche il pacchetto com.microsoft.sqlserver.jdbc.internals, che include il supporto per la registrazione per le seguenti categorie di registrazione interne.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|AuthenticationJNI|Registra i messaggi relativi ai problemi di autenticazione integrata di Windows, quando la proprietà di connessione **authenticationScheme** è impostata in modo implicito o esplicito su **NativeAuthentication**.<br /><br /> Le applicazioni possono impostare il livello di registrazione su FINEST e FINE.|  
|SQLServerConnection|Consente di registrare i messaggi nella classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Le applicazioni possono impostare il livello di registrazione su FINE e FINER.|  
|SQLServerDataSource|Consente di registrare i messaggi nelle classi [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md), [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) e [SQLServerPooledConnection](../../connect/jdbc/reference/sqlserverpooledconnection-class.md).<br /><br /> Le applicazioni possono impostare il livello di registrazione su FINER.|  
|InputStream|Consente di registrare i messaggi relativi ai tipi di dati java.io.InputStream e java.io.Reader, nonché ai tipi di dati per i quali è disponibile un identificatore max, ad esempio varchar, nvarchar e varbinary.<br /><br /> Le applicazioni possono impostare il livello di registrazione su FINER.|  
|SQLServerException|Consente di registrare i messaggi nella classe [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md). Le applicazioni possono impostare il livello di registrazione su FINE.|  
|SQLServerResultSet|Consente di registrare i messaggi nella classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md). Le applicazioni possono impostare il livello di registrazione su FINE, FINER e FINEST.|  
|SQLServerStatement|Consente di registrare i messaggi nella classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). Le applicazioni possono impostare il livello di registrazione su FINE, FINER e FINEST.|  
|XA|Consente di registrare i messaggi per tutte le transazioni XA nella classe [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md). Le applicazioni possono impostare il livello di registrazione su FINE e FINER.|  
|KerbAuthentication|Registra i messaggi relativi all'autenticazione Kerberos di tipo 4, quando la proprietà di connessione **authenticationScheme** è impostata su **JavaKerberos**. L'applicazione può impostare il livello di registrazione su FINE o FINER.|  
|TDS.DATA|Registra i messaggi contenenti la conversazione a livello di protocollo TDS tra il driver e SQL Server. Il contenuto dettagliato di ogni pacchetto TDS inviato e ricevuto viene registrato in formato ASCII ed esadecimale. Le credenziali di accesso (nomi utente e password) non vengono registrate. Tutti gli altri dati vengono registrati.<br /><br /> Questa categoria consente di creare messaggi molto dettagliati ed esaustivi e può essere abilitata solo impostando il livello di registrazione su FINEST.|  
|TDS.Channel|Questa categoria consente di eseguire le tracce delle azioni del canale di comunicazione TCP con SQL Server. I messaggi registrati includono l'apertura e la chiusura di socket, nonché le operazioni di lettura e scrittura. Vengono inoltre eseguite le tracce dei messaggi correlati alla definizione di una connessione SSL (Secure Socket Layer) con SQL Server.<br /><br /> Può essere abilitata solo impostando il livello di registrazione su FINE, FINER o FINEST.|  
|TDS.Writer|Questa categoria consente di eseguire le tracce delle operazioni di scrittura nel canale TDS. Si noti che vengono eseguite le tracce solo della lunghezza delle operazioni di scrittura e non del contenuto. Vengono inoltre eseguite le tracce dei problemi quando al server viene inviato un segnale di attenzione per annullare l'esecuzione di un'istruzione.<br /><br /> Può essere abilitata solo impostando il livello di registrazione su FINEST.|  
|TDS.Reader|Questa categoria consente di eseguire le tracce di alcune operazioni di lettura dal canale TDS con livello FINEST. Con tale livello le tracce possono risultare dettagliate. Con i livelli WARNING e SEVERE questa categoria consente di eseguire le tracce quando il driver riceve un protocollo TDS non valido da SQL Server prima della chiusura della connessione.<br /><br /> Può essere abilitata solo impostando il livello di registrazione su FINER e FINEST.|  
|TDS.Command|Questa categoria consente di eseguire la traccia delle transizioni di stato di basso livello e di altre informazioni associate all'esecuzione di comandi TDS, ad esempio le esecuzioni di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)], i recuperi di cursori ResultSet, i commit e così via.<br /><br /> Può essere abilitata solo impostando il livello di registrazione su FINEST.|  
|TDS.TOKEN|Questa categoria consente di registrare solo i token dei pacchetti di flussi TDS e risulta meno dettagliata della categoria TDS.DATA. Può essere abilitata solo impostando il livello di registrazione su FINEST.<br /><br /> Con il livello FINEST questa categoria consente di eseguire le tracce dei token TDS quando vengono elaborati nella risposta. Con il livello SEVERE esegue le tracce quando viene rilevato un token TDS non valido.|  
|SQLServerDatabaseMetaData|Consente di registrare i messaggi nella classe [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md). Le applicazioni possono impostare il livello di registrazione su FINE.|  
|SQLServerResultSetMetaData|Consente di registrare i messaggi nella classe [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md). Le applicazioni possono impostare il livello di registrazione su FINE.|  
|SQLServerParameterMetaData|Consente di registrare i messaggi nella classe [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md). Le applicazioni possono impostare il livello di registrazione su FINE.|  
|SQLServerBlob|Consente di registrare i messaggi nella classe [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md). Le applicazioni possono impostare il livello di registrazione su FINE.|  
|SQLServerClob|Consente di registrare i messaggi nella classe [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md). Le applicazioni possono impostare il livello di registrazione su FINE.|  
|SQLServerSQLXML|Registra i messaggi nella classe SQLServerSQLXML interna. Le applicazioni possono impostare il livello di registrazione su FINE.|  
|SQLServerDriver|Consente di registrare i messaggi nella classe [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md). Le applicazioni possono impostare il livello di registrazione su FINE.|  
|SQLServerNClob|Consente di registrare i messaggi nella classe [SQLServerNClob](../../connect/jdbc/reference/sqlservernclob-class.md). Le applicazioni possono impostare il livello di registrazione su FINE.|  
  
## <a name="enabling-tracing-programmatically"></a>Abilitazione delle tracce a livello di programmazione  
 La creazione di tracce può essere abilitata a livello di programmazione creando un oggetto Logger e indicando la categoria da registrare. Il codice seguente, ad esempio, consente di abilitare la registrazione per le istruzioni SQL:  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.FINER);  
```  
  
 Per disabilitare la registrazione dal codice, utilizzare:  
  
```java
logger.setLevel(Level.OFF);  
```  
  
 Per registrare tutte le categorie disponibili, utilizzare:  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc");  
logger.setLevel(Level.FINE);  
```  
  
 Per disabilitare una categoria specifica, utilizzare:  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.OFF);  
```  
  
## <a name="enabling-tracing-by-using-the-loggingproperties-file"></a>Abilitazione delle tracce tramite il file Logging.Properties  
 La creazione di tracce può inoltre essere abilitata utilizzando il file `logging.properties`, disponibile nella directory `lib` dell'installazione Java Runtime Environment (JRE). Il file può essere utilizzato per impostare i valori predefiniti degli oggetti logger e handler utilizzati una volta abilitate le tracce.  
  
 Di seguito è riportato un esempio delle impostazioni che è possibile configurare nei file `logging.properties`:  
  
```  
# Specify the handler, the handlers will be installed during VM startup.  
handlers= java.util.logging.FileHandler  
  
# Default global logging level.  
.level= OFF  
  
# default file output is in user's home directory.  
java.util.logging.FileHandler.pattern = %h/java%u.log  
java.util.logging.FileHandler.limit = 5000000  
java.util.logging.FileHandler.count = 20  
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter  
java.util.logging.FileHandler.level = FINEST  
  
# Facility specific properties.  
com.microsoft.sqlserver.jdbc.level=FINEST  
  
```  
  
> [!NOTE]  
>  Per impostare le proprietà nel file `logging.properties` è possibile utilizzare l'oggetto LogManager, che fa parte di java.util.logging.  
  
## <a name="see-also"></a>Vedere anche  
 [Diagnosi dei problemi relativi al driver JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
