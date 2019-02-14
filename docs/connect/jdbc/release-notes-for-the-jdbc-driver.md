---
title: Note sulla versione per il Driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/29/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b7f863c7534421fa6e091e793297b4be3f73542
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/05/2019
ms.locfileid: "55737062"
---
# <a name="release-notes-for-the-jdbc-driver"></a>Note sulla versione per il driver JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-72-for-sql-server"></a>Aggiornamenti in Microsoft JDBC Driver 7.2 per SQL Server

Microsoft JDBC Driver 7.2 per SQL Server è completamente conforme alla specifica di API di JDBC 4.2. I file JAR nel pacchetto 7,2 sono denominati in base alla compatibilità delle versioni di Java. Ad esempio, il file mssql-jdbc-7.2.0.jre11.jar dal pacchetto 7,2 deve essere utilizzato con Java 11.

### <a name="support-for-jdk-11"></a>Supporto per JDK 11

Microsoft JDBC Driver 7.2 per SQL Server è ora compatibile con Java Development Kit (JDK) versione 11.0, oltre a JDK 1.8.

### <a name="support-for-active-directory-managed-service-identity-msi-authentication"></a>Supporto per l'autenticazione di Active Directory Managed Service Identity (MSI)

Microsoft JDBC Driver 7.2 per SQL Server supporta ora la modalità di autenticazione di Active Directory Managed Service Identity (MSI). Questa modalità di autenticazione è applicabile in risorse di Azure con supporto per funzionalità "Identity" abilitata. Entrambi i tipi di identità di sistema gestito (MSI) sono supportati dal driver per acquisire **accessToken** per stabilire una connessione sicura.

Altre informazioni e un'applicazione di esempio per usare questa modalità di autenticazione sono disponibili qui: [Connessione tramite autenticazione di Azure Active Directory](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)

### <a name="osgi-support"></a>Supporto OSGi

Microsoft JDBC Driver 7.2 per SQL Server introduce il supporto OSGi al driver mediante l'aggiunta di seguito le implementazioni per `org.osgi.service.jdbc.DataSourceFactory` e `org.osgi.framework.BundleActivator` :

- `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory`
- `com.microsoft.sqlserver.jdbc.osgi.Activator`

### <a name="sqlservererror-apis"></a>API SQLServerError

Microsoft JDBC Driver 7.2 per SQL Server introduce `SQLServerException.getSQLServerError()` e `SQLServerError` getter API per recuperare i dettagli aggiuntivi sull'errore generato dal server. Per altre informazioni, vedere [Handling Errors](../../connect/jdbc/handling-errors.md) (Gestione degli errori).

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-163"></a>Aggiornamento di "Microsoft Azure Active Directory Authentication Library (ADAL4J) per Java" alla versione 1.6.3

Microsoft JDBC Driver 7.2 per SQL Server ha aggiornato la dipendenza Maven "Microsoft Azure Active Directory Authentication Library (ADAL4J) per Java" alla versione 1.6.3, che introduce anche "Runtime Client Java per AutoRest" come dipendenza Maven (versione: 1.6.5). Per altre informazioni sulle dipendenze, vedere [dipendenze delle funzionalità di Microsoft JDBC Driver per SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

### <a name="updated-microsoft-azure-key-vault-sdk-for-java-version-120"></a>Versione aggiornata di "Microsoft Azure Key Vault SDK per Java": 1.2.0

Microsoft JDBC Driver 7.2 per SQL Server ha aggiornato la dipendenza Maven in "Microsoft Azure Key Vault SDK for Java" alla versione 1.2.0, che introduce anche "Microsoft Azure SDK per Key Vault WebKey" come dipendenza Maven (versione: 1.2.0). Per altre informazioni sulle dipendenze, vedere [dipendenze delle funzionalità di Microsoft JDBC Driver per SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

### <a name="known-issues"></a>Problemi noti

Con Microsoft JDBC Driver 7.2 per SQL Server, esiste un problema noto con alcune query con parametri. Un aggiornamento della versione 7.2 (v7.2.1), verranno presto rilasciate per risolvere questo problema.


## <a name="updates-in-microsoft-jdbc-driver-70-for-sql-server"></a>Aggiornamenti in Microsoft JDBC Driver 7.0 per SQL Server

Microsoft JDBC Driver 7.0 per SQL Server è completamente conforme alla specifica di API di JDBC 4.2. I file JAR nel pacchetto 7.0 sono denominati in base alla compatibilità delle versioni di Java. Ad esempio, il file mssql-jdbc-7.0.0.jre10.jar dal pacchetto 7.0 deve essere utilizzato con Java 10.

### <a name="support-for-jdk-10"></a>Supporto per JDK 10

Microsoft JDBC Driver 7.0 per SQL Server è ora compatibile con Java Development Kit (JDK) versione 10.0, oltre a JDK 1.8. Questo aggiornamento espone anche il driver `Automatic-Module-Name` come `com.microsoft.sqlserver.jdbc` attraverso file manifesto corrispondente.

### <a name="support-for-spatial-datatypes"></a>Supporto per tipi di dati spaziali

Microsoft JDBC Driver 7.0 per SQL Server fornisce ora supporto per SQL Server spaziali tipi di dati Geometry e Geography. Per altre informazioni sul tipo di dati spaziale API e su come usarli, vedere [utilizzando i tipi di dati spaziali](../../connect/jdbc/use-spatial-datatypes.md).

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>Implementazione per JDBC 4.3 che ha introdotto le API java.sql.Connection beginRequest() ed endRequest()

Microsoft JDBC Driver 7.0 per SQL Server ora implements `beginRequest()` e `endRequest()` API dal `java.sql.Connection` classe. Queste API sono state introdotte con le specifiche JDBC 4.3 e JDK 9. Per altre informazioni sull'implementazione del driver di queste API, vedere [conformità a JDBC 4.3 per JDBC Driver](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="support-for-sql-data-discovery-and-classification"></a>Supporto di individuazione dati e classificazione SQL

Microsoft JDBC Driver 7.0 per SQL Server fornisce supporto per l'individuazione di dati SQL e la classificazione con qualsiasi database di destinazione che supporta questa funzionalità. Il driver ora espone `SQLServerResultSet.getSensitivityClassification()` API per estrarre queste informazioni dal recupero `ResultSet`.

Per altre informazioni su come usare questa funzionalità con il Driver JDBC, vedere l'esempio nella [SQL individuazione dati e classificazione](../../connect/jdbc/data-discovery-classification-sample.md).

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>Aggiunta di proprietà di connessione: useBulkCopyForBatchInsert

Microsoft JDBC Driver 7.0 per SQL Server introduce una nuova proprietà di connessione, `useBulkCopyForBatchInsert`. Questa proprietà è supportata solo per Azure SQL Data Warehouse.

Questa proprietà è disabilitata per impostazione predefinita. È possibile abilitarlo per migliorare le prestazioni delle applicazioni utente quando si eseguono il push dei dati di grandi quantità in Azure SQL Data Warehouse. Abilitazione di questa proprietà viene modificato il comportamento delle operazioni di inserimento batch per passare a operazioni di copia bulk con dati forniti dall'utente. Per altre informazioni su questa proprietà e le relative limitazioni, vedere [usando API della copia Bulk per batch di operazioni di inserimento](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md).

### <a name="added-connection-property-cancelquerytimeout"></a>Aggiunta di proprietà di connessione: cancelQueryTimeout

Microsoft JDBC Driver 7.0 per SQL Server introduce una nuova proprietà di connessione `cancelQueryTimeout`, per annullare `queryTimeout` sul `java.sql.Connection` e `java.sql.Statement` oggetti.

### <a name="added-azure-key-vault-provider-constructors"></a>Costruttori di Azure Key Vault Provider aggiunti

Microsoft JDBC Driver 7.0 per SQL Server è stata reintrodotta un costruttore rimosso in precedenza, per `SQLServerColumnEncryptionAzureKeyVaultProvider`. È consentita l'autenticazione tramite un metodo personalizzato implementato sulla `SQLServerKeyVaultAuthenticationCallback` per recuperare un token di accesso.

I nuovi costruttori sono la definizione seguente:

```java
/* This constructor is added to provide backward compatibility with 6.0
* version of the driver. It is marked deprecated for removal in the next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-160"></a>Aggiornamento di "Microsoft Azure Active Directory Authentication Library (ADAL4J) per Java" alla versione 1.6.0

Microsoft JDBC Driver 7.0 per SQL Server ha aggiornato la dipendenza Maven "Microsoft Azure Active Directory Authentication Library (ADAL4J) per Java" alla versione 1.6.0. Per altre informazioni sulle dipendenze, vedere [dipendenze delle funzionalità di Microsoft JDBC Driver per SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>Aggiornamenti in Microsoft JDBC Driver 6.4 per SQL Server

Microsoft JDBC Driver 6.4 per SQL Server è completamente compatibile con le specifiche JDBC 4.1 e 4.2. I file JAR nel pacchetto di 6,4 sono denominati in base alla compatibilità delle versioni di Java. Ad esempio, il file mssql-jdbc-6.4.0.jre8.jar dal pacchetto di 6,4 deve essere utilizzato con Java 8.

### <a name="support-for-jdk-9"></a>Supporto per JDK 9

Il driver supporta JDK versione 9.0, oltre a JDK 8.0 e 7.0.

### <a name="jdbc-43-compliance"></a>Conformità a JDBC 4.3

Il driver supporta la specifica Java Database Connectivity API 4.3, oltre a 4.1 e 4.2. I metodi dell'API di JDBC 4.3 vengono aggiunte ma non ancora implementati. Per informazioni dettagliate, vedere [Conformità a JDBC 4.3 per il driver JDBC](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="added-connection-property-sslprotocol"></a>Aggiunta di proprietà di connessione: sslProtocol

Una nuova proprietà di connessione consente agli utenti di specificare la parola chiave protocollo TLS. I valori possibili sono: "TLS", "TLSv1", "TLSv1.1" e "TLSv1.2". Per informazioni dettagliate, vedere [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol).

### <a name="deprecated-connection-property-fipsprovider"></a>Deprecato proprietà di connessione: fipsProvider

La proprietà di connessione `fipsProvider` viene rimosso dall'elenco delle proprietà di connessione accettata. Per informazioni dettagliate, vedere i relativi [richiesta pull di GitHub](https://github.com/Microsoft/mssql-jdbc/pull/460).

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>Proprietà di connessione aggiunta per un trustmanager personalizzato

Il driver ora supporta trustmanager personalizzato con aggiunte `trustManagerClass` e `trustManagerConstructorArg` "trustmanagerconstructorarg". È possibile specificare in modo dinamico un set di certificati considerati attendibili in una singola connessione senza modificare le impostazioni globali per l'ambiente di Java virtual machine (JVM).

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>Aggiunta del supporto per datetime/smallDatetime nei parametri con valori di tabella

Il driver ora supporta i tipi di dati `datetime` e `smallDatetime` quando si utilizza parametri con valori di tabella (TVP).

### <a name="added-support-for-the-sqlvariant-datatype"></a>Aggiunta del supporto per il tipo di dati sql_variant

Il Driver JDBC ora supporta `sql_variant` tipi di dati da utilizzare con SQL Server. Il `sql_variant` supportato anche il tipo di dati con funzionalità quali TVP e copia bulk con le limitazioni seguenti:

* **Per i valori di data**: 

  Quando si usa TVP per popolare una tabella che contiene `datetime`, `smalldatetime`, o `date` i valori archiviati in un `sql_variant` colonna, una chiamata di `getDateTime()`, `getSmallDateTime()`, o `getDate()` metodo sul set di risultati non funziona e Genera l'eccezione seguente:

  `java java.lang.String cannot be cast to java.sql.Timestamp`
    
  In alternativa, usare il `getString()` o `getObject()` metodo invece.

* **Uso di TVP con sql_variant per valori null**:
  
  Se si usa TVP per popolare una tabella e l'invio di un valore NULL per il `sql_variant` tipo di colonna, che si incontrano un'eccezione. Inserimento di un valore NULL con il tipo di colonna `sql_variant` in TVP non è attualmente supportata.

### <a name="implemented-prepared-statement-metadata-caching"></a>Implementata la memorizzazione nella cache dei metadati di istruzione preparata

Il Driver JDBC è implementata la memorizzazione nella cache dei metadati istruzione preparata per migliorare le prestazioni. Il driver ora supporta la memorizzazione nella cache dei metadati di istruzione preparata nel driver con `disableStatementPooling` e `statementPoolingCacheSize` "trustmanagerconstructorarg". Questa funzionalità è disabilitata per impostazione predefinita. Per altre informazioni, vedere [preparato memorizzazione nella cache dei metadati di istruzione per il Driver JDBC](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md).

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmac"></a>Aggiunta del supporto per Azure AD per l'autenticazione integrata, in Linux/Mac

Il driver JDBC supporta ora l'autenticazione integrata di Azure Active Directory in tutti i sistemi operativi supportati (Windows, Linux e Mac) con Kerberos. In alternativa, nei sistemi operativi Windows, utenti possono autenticarsi con sqljdbc_auth.

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>Aggiornamento di "Microsoft Azure Active Directory Authentication Library (ADAL4J) per Java" alla versione 1.4.0

Il Driver JDBC ha aggiornato la dipendenza Maven "Microsoft Azure Active Directory Authentication Library (ADAL4J) per Java" alla versione 1.4.0. Per altre informazioni sulle dipendenze, vedere [dipendenze delle funzionalità di Microsoft JDBC Driver per SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Aggiornamenti in Microsoft JDBC Driver 6.2 per SQL Server

Microsoft JDBC Driver 6.2 per SQL Server è completamente compatibile con le specifiche JDBC 4.1 e 4.2. I file JAR nel pacchetto 6.2 sono denominati in base alla compatibilità delle versioni di Java. Ad esempio, il file mssql-jdbc-6.2.2.jre8.jar dal pacchetto 6.2 è consigliato per l'uso con Java 8.

> [!NOTE]  
> Un problema con il miglioramento di memorizzazione nella cache dei metadati è stato trovato nella versione RTW 6.2 JDBC rilasciata il 29 giugno 2017. È stato eseguito il rollback il miglioramento e nuovo file con estensione jar (versione 6.2.1) sono state rilasciate 17 luglio 2017. 
>
> Un altro miglioramento aggiornato la versione della libreria dipendente da Azure Key Vault a 1.0.0 e nuovo file con estensione jar (versione 6.2.2) sono stati rilasciati il 19 ottobre 2017.
>
> Scaricare gli aggiornamenti più recenti per JDBC Driver 6.2 dal [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2), e [Maven Central](https://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22). Aggiornare i progetti per l'uso di 6.2.2 rilasciare i file con estensione jar. Per altre informazioni, visualizzare le note sulla versione per [6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) e [6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2).

### <a name="azure-ad-support-for-linux"></a>Supporto di Azure AD per Linux

Connettere le applicazioni di Linux a Database SQL di Azure con l'autenticazione di Azure AD tramite i metodi di token nome utente/password e l'accesso.

### <a name="fips-enabled-jvms"></a>JVM abilitato FIPS

Il Driver JDBC ora utilizzabile nella JVM eseguiti in modalità di compatibilità 140 Federal informazioni Processing Standard (FIPS) per soddisfare gli standard federali sulla conformità.

### <a name="kerberos-authentication-improvements"></a>Miglioramenti di autenticazione Kerberos

Il Driver JDBC include ora il supporto per:

- Metodo di entità e la password per le applicazioni in cui la configurazione di Kerberos non può essere modificata o non è possibile recuperare un nuovo token o keytab. Questo metodo può essere utilizzato per l'autenticazione a un'istanza di SQL Server che consente solo l'autenticazione Kerberos.
- Autenticazione tra aree che usa l'autenticazione integrata Kerberos senza impostare in modo esplicito il nome SPN del server. Il driver adesso viene calcolato automaticamente l'area di autenticazione anche quando esso non viene fornito.
- La delega vincolata Kerberos mediante l'accettazione di rappresentare le credenziali dell'utente come un oggetto credenziali GSS tramite l'origine dati. Questa credenziale rappresentata viene quindi usata per stabilire una connessione di Kerberos.

### <a name="added-timeouts"></a>Aggiunta dei timeout

Il Driver JDBC ora supporta i timeout configurabili seguenti. È possibile modificarli in base alle esigenze dell'applicazione.

- Timeout della query per controllare il numero di secondi di attesa prima che si verifica un timeout durante l'esecuzione di una query.
- Timeout del socket per specificare il numero di millisecondi di attesa prima che si verifica un timeout su un socket di lettura o accettare.

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Aggiornamenti in Microsoft JDBC Driver 6.1 per SQL Server

Microsoft JDBC Driver 6.1 per SQL Server è completamente compatibile con le specifiche JDBC 4.1 e 4.2. Si tratta della versione open source iniziale del Driver JDBC. Contiene i file mssql-jdbc-6.1.0.jre8.jar e mssql-jdbc-6.1.0.jre7.jar, che corrispondono alla compatibilità delle versioni di Java.

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Aggiornamenti in Microsoft JDBC Driver 6.0 per SQL Server

Microsoft JDBC Driver 6.0 per SQL Server è completamente compatibile con le specifiche JDBC 4.1 e 4.2. I file JAR nel pacchetto 6.0 sono denominate secondo la conformità con la versione dell'API di JDBC. Ad esempio, il file sqljdbc42.jar dal pacchetto 6.0 è conforme a JDBC API 4.2. Analogamente, il file sqljdbc41.jar è conforme con JDBC 4.1 di API.

Per assicurarsi di avere il file di sqljdbc41.jar o sqljdbc42.jar a destra, eseguire le seguenti righe di codice. Se l'output è "versione del Driver: versione 6.0.7507.100 ", è necessario il pacchetto di JDBC Driver 6.0.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Crittografia sempre attiva

Il driver supporta la funzionalità Always Encrypted in SQL Server 2016. Questa funzionalità garantisce che i dati sensibili non viene mai visualizzati in testo non crittografato in un'istanza di SQL Server. Always Encrypted crittografa in modo trasparente i dati nell'applicazione, in modo che SQL Server debba gestire solo i dati crittografati e non i valori di testo non crittografato. In caso di compromissione dell'istanza di SQL Server o del computer host, un utente malintenzionato ottiene solo il testo crittografato dei dati sensibili. Per informazioni dettagliate, vedere [Uso di Always Encrypted con il JDBC Driver](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).

### <a name="internationalized-domain-names"></a>Nomi IDN (Internationalized Domain Name)

Il driver supporta internationalized domain Name (IDN) per i nomi dei server. Per informazioni dettagliate, vedere "Utilizzo di International Domain Names" nel [caratteristiche internazionali del Driver JDBC](../../connect/jdbc/international-features-of-the-jdbc-driver.md) articolo.

### <a name="parameterized-queries"></a>Query con parametri

Il driver supporta ora il recupero dei metadati dei parametri con istruzioni preparate per le query complesse, ad esempio le sottoquery e/o i join. Si noti che questo miglioramento è disponibile solo quando si usa SQL Server 2012 e versioni successive.

### <a name="azure-active-directory"></a>Azure Active Directory

Autenticazione di Azure AD è un meccanismo di connessione alla versione 12 del Database SQL di Azure tramite identità in Azure AD. Usare l'autenticazione di Azure AD per gestire centralmente le identità degli utenti del database e come alternativa all'autenticazione di SQL Server. 

È possibile usare JDBC Driver 6.0 per specificare le credenziali di Azure AD nella stringa di connessione JDBC per connettersi al Database SQL di Azure. Per informazioni dettagliate, vedere la proprietà di autenticazione nel [impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md) articolo.

### <a name="table-valued-parameters"></a>Parametri con valori di tabella

I parametri con valori di tabella offrono un modo semplice per effettuare il marshalling di più righe di dati da un'applicazione client di SQL Server senza richiedere più round trip o una logica speciale sul lato server per l'elaborazione dei dati. I parametri con valori di tabella possono essere usati per incapsulare le righe di dati in un'applicazione client e inviare i dati al server in un singolo comando con parametri. Le righe di dati in ingresso vengono archiviate in una variabile di tabella che è possibile quindi utilizzare tramite Transact-SQL. Per informazioni dettagliate, vedere [utilizzando i parametri con valori di tabella](../../connect/jdbc/using-table-valued-parameters.md).

### <a name="always-on-availability-groups"></a>Gruppi di disponibilità AlwaysOn

Il driver ora supporta le connessioni trasparenti ai gruppi di disponibilità AlwaysOn. Il driver individua rapidamente la topologia AlwaysOn corrente dell'infrastruttura server e si connette in modo trasparente al server attivo corrente.

## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Aggiornamenti in Microsoft JDBC Driver 4.2 per SQL Server e versioni successive

Microsoft JDBC Driver 4.2 per SQL Server è completamente compatibile con le specifiche JDBC 4.1 e 4.2. I file JAR nel pacchetto 4.2 sono denominate secondo la conformità con la versione dell'API di JDBC. Ad esempio, il file sqljdbc42.jar dal pacchetto 4.2 è conforme a JDBC API 4.2. Analogamente, il file sqljdbc41.jar è conforme con JDBC 4.1 di API.

Per verificare che è necessario il sqljdbc42.jar corretto o il file sqljdbc41.jar, eseguire le seguenti righe di codice. Se l'output è "versione del Driver: 4.2.6420.100 ", è necessario il pacchetto di Driver JDBC 4.2.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>Supporto per JDK 8

Il driver supporta JDK versione 8.0, oltre a JDK 7.0, 6.0 e 5.0.

### <a name="jdbc-41-and-42-compliance"></a>Conformità con JDBC 4.1 e 4.2

Il driver supporta le specifiche Java Database Connectivity API 4.1 e 4.2, oltre a 4.0. Per informazioni dettagliate, vedere [conformità a JDBC 4.1 per il Driver JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) e [conformità con JDBC 4.2 per il Driver JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).

### <a name="bulk-copy"></a>Copia bulk

La funzionalità di copia bulk viene usata per copiare rapidamente grandi quantità di dati in tabelle o viste nei database di SQL Server. Per informazioni dettagliate, vedere [Uso della copia bulk con il driver JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

### <a name="xa-transaction-rollback-option"></a>Opzione di rollback di transazione XA

Il driver include nuove opzioni di timeout per il rollback automatico esistente di transazioni non preparate. Per informazioni dettagliate, vedere [Understanding XA transactions](../../connect/jdbc/understanding-xa-transactions.md).

### <a name="new-kerberos-principal-connection-property"></a>Nuova proprietà di connessione principale Kerberos

Il driver usa una nuova proprietà di connessione per aumentare la flessibilità con le connessioni Kerberos. Per informazioni dettagliate, vedere [Uso dell'autenticazione integrata Kerberos per la connessione a SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md).

## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Aggiornamenti in Microsoft JDBC Driver 4.1 per SQL Server e versioni successive

### <a name="support-for-jdk-7"></a>Supporto per JDK 7

Il driver supporta JDK versione 7.0, oltre a JDK 6.0 e 5.0.

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>Le applicazioni JDBC Driver 6.4, 6.0, 4.2 e 4.1 non supportano i computer Itanium

Le applicazioni Microsoft JDBC Driver 6.4, 6.0, 4.2 e 4.1 per SQL Server non supportano i computer Itanium.

## <a name="see-also"></a>Vedere anche

[Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)
