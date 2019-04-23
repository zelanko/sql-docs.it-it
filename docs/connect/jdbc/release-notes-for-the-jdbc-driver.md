---
title: Note sulla versione per il driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5e75f732fc44ee339cb3d9d47518627f264cb8cc
ms.sourcegitcommit: e2d65828faed6f4dfe625749a3b759af9caa7d91
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2019
ms.locfileid: "59671337"
---
# <a name="release-notes-for-the-microsoft-jdbc-driver"></a>Note sulla versione per il driver Microsoft JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questo articolo elenca le versioni del _driver Microsoft JDBC per SQL Server_. Per ogni versione sono elencate e descritte le modifiche.

## <a name="722"></a>7.2.2

### <a name="compliance"></a>Conformità

16 aprile 2019

| Modifica di conformità | Dettagli |
| :---------------- | :------ |
| Scaricare gli aggiornamenti più recenti per il driver JDBC 7.2. | &bull; &nbsp; [Area download Microsoft](https://go.microsoft.com/fwlink/?linkid=2063159)<br/>&bull; &nbsp; [GitHub, 7.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| Completamente conforme alla specifica API JDBC 4.2. | I file JAR nel pacchetto 7.2 sono denominati in base alla compatibilità delle versioni di Java.<br/><br/>Ad esempio, il file mssql-jdbc-7.2.2.jre11.jar dal pacchetto 7.2 deve essere usato con Java 11. |
| Compatibile con Java Development Kit (JDK) versione 11.0 oltre a JDK 1.8. | Il driver Microsoft JDBC 7.2 per SQL Server è ora compatibile con Java Development Kit (JDK) versione 11.0, oltre a JDK 1.8. |
| &nbsp; | &nbsp; |

> [!NOTE]
> È stato rilevato un problema con l'analisi delle istruzioni SQL nel driver JDBC 7.2 Release To Web (RTW) rilasciato il 31 gennaio 2019. È stato eseguito il rollback della modifica e sono stati rilasciati nuovi file JAR (versione 7.2.1) in data 11 febbraio 2019.
>
> È stato pubblicato un altro aggiornamento del driver per risolvere i problemi relativi alla pulizia non corretta di ActivityId. I nuovi file JAR (versione 7.2.2) sono stati rilasciati il 16 aprile 2019.
> 
> È consigliabile aggiornare i progetti per l'uso dei file JAR della versione 7.2.2. Per altre informazioni, vedere le note sulla versione per [GitHub, 7.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1) e [GitHub, 7.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2).

### <a name="active-directory-managed-service-identity-msi-authentication"></a>Autenticazione dell'_identità del servizio gestita_ di Active Directory

| Modifica dell'identità del servizio gestita | Dettagli |
| :--------- | :------ |
| Supporta la modalità di autenticazione dell'identità del servizio gestita di Active Directory. | Questa modalità di autenticazione è applicabile alle risorse di Azure con il supporto per la funzionalità "Identità" abilitato.<br/><br/>Il driver supporta entrambi i tipi di identità del servizio gestita per l'acquisizione di **accessToken** per stabilire una connessione sicura. |
| Altri dettagli e un'applicazione di esempio per usare questa modalità di autenticazione. | Vedere [Connessione con l'autenticazione di Azure Active Directory](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md). |
| &nbsp; | &nbsp; |

### <a name="introduces-open-service-gateway-initiative-osgi-support"></a>Introduce il supporto di _Open Service Gateway Initiative_ (OSGi)

| Modifica per OSGi | Dettagli |
| :---------- | :------ |
| Aggiunta l'implementazione di **DataSourceFactory**. | &bull; &nbsp; `org.osgi.service.jdbc.DataSourceFactory`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory` |
| Aggiunta l'implementazione di **Activator**. | &bull; &nbsp; `org.osgi.framework.BundleActivator`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.Activator` |
| &nbsp; | &nbsp; |

### <a name="introduces-sqlservererror-apis"></a>Introduce le API _SQLServerError_

| Modifica per le API di errore | Dettagli |
| :--------------- | :------ |
| Introduzione dell'API SQLServerError. | API getter per recuperare dettagli aggiuntivi sull'errore generato dal server.<br/><br/>&bull; &nbsp; `SQLServerException.getSQLServerError()`<br/>&bull; &nbsp; `SQLServerError` |
| Dettagli aggiuntivi. | Vedere [Gestione degli errori](../../connect/jdbc/handling-errors.md). |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-163"></a>Aggiornamento di _Microsoft Azure Active Directory Authentication Library (ADAL4J) per Java_, versione 1.6.3

| Modifica per ADAL4J | Dettagli |
| :------------ | :------ |
| Aggiornamento della dipendenza di Maven da ADAL4J alla versione 1.6.3. | &nbsp; |
| Introduce _Java Client Runtime for AutoRest_ come dipendenza Maven, versione 1.6.5. | &nbsp; |
| Dettagli aggiuntivi. | Vedere [Dipendenze delle funzionalità di Microsoft JDBC Driver per SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-key-vault-sdk-for-java-version-120"></a>Aggiornamento di _Microsoft Azure Key Vault SDK for Java_, versione 1.2.0

| Modifica di Key Vault SDK | Dettagli |
| :------------------- | :------ |
| Aggiornamento della dipendenza di Maven da _Microsoft Azure Key Vault SDK for Java_ alla versione 1.2.0. | &nbsp; |
| Introduce _Microsoft Azure SDK per Key Vault WebKey_ come dipendenza Maven, versione 1.2.0. | &nbsp; |
| Dettagli aggiuntivi. | Vedere [Dipendenze delle funzionalità di Microsoft JDBC Driver per SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemi noti

| Problemi noti | Dettagli |
| :----------- | :------ |
| Query con parametri, in alcuni casi. | È stato rilasciato un aggiornamento della versione 7.2.0 (7.2.1) a febbraio 2019 per risolvere questo problema. |
| Pulizia di ActivityId. | È stato rilasciato un aggiornamento della versione 7.2.1 (7.2.2) ad aprile 2019 per risolvere questo problema. |
| &nbsp; | &nbsp; |

## <a name="70"></a>7.0

Il driver Microsoft JDBC 7.0 per SQL Server è completamente conforme alla specifica API JDBC 4.2. I file JAR nel pacchetto 7.0 sono denominati in base alla compatibilità delle versioni di Java. Ad esempio, il file mssql-jdbc-7.0.0.jre10.jar dal pacchetto 7.0 deve essere usato con Java 10.

### <a name="support-for-jdk-10"></a>Supporto per JDK 10

Il driver Microsoft JDBC 7.0 per SQL Server è ora compatibile con Java Development Kit (JDK) versione 10.0, oltre a JDK 1.8. Questo aggiornamento espone anche `Automatic-Module-Name` del driver come `com.microsoft.sqlserver.jdbc` attraverso file manifesto corrispondente.

### <a name="support-for-spatial-datatypes"></a>Supporto per tipi di dati spaziali

Il driver Microsoft JDBC 7.0 per SQL Server offre ora il supporto dei tipi di dati spaziali Geometry e Geography di SQL Server. Per altre informazioni sulle API dei tipi di dati spaziali e su come usarle, vedere [Uso dei tipi di dati spaziali](../../connect/jdbc/use-spatial-datatypes.md).

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>Implementazione per JDBC 4.3 che ha introdotto le API java.sql.Connection beginRequest() ed endRequest()

Il driver Microsoft JDBC 7.0 per SQL Server implementa ora le API `beginRequest()` e `endRequest()` dalla classe `java.sql.Connection`. Queste API sono state introdotte con la specifica JDBC 4.3 e JDK 9. Per altre informazioni sull'implementazione del driver di queste API, vedere [Conformità a JDBC 4.3 per il driver JDBC](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="support-for-sql-data-discovery-and-classification"></a>Supporto di individuazione dati e classificazione SQL

Il driver Microsoft JDBC 7.0 per SQL Server fornisce supporto per l'individuazione di dati SQL e la classificazione con qualsiasi database di destinazione che supporta questa funzionalità. Il driver ora espone le API `SQLServerResultSet.getSensitivityClassification()` per estrarre queste informazioni dal `ResultSet` recuperato.

Per altre informazioni su come usare questa funzionalità con il driver JDBC, vedere l'esempio in [Individuazione dati e classificazione SQL](../../connect/jdbc/data-discovery-classification-sample.md).

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>Aggiunta della proprietà di connessione: useBulkCopyForBatchInsert

Il driver Microsoft JDBC 7.0 per SQL Server introduce una nuova proprietà di connessione, `useBulkCopyForBatchInsert`. Questa proprietà è supportata solo per Azure SQL Data Warehouse.

Questa proprietà è disabilitata per impostazione predefinita. È possibile abilitarla per migliorare le prestazioni delle applicazioni utente quando si esegue il push di grandi quantità di dati in Azure SQL Data Warehouse. L'abilitazione di questa proprietà modifica il comportamento delle operazioni di inserimento batch per passare a operazioni di copia bulk con dati forniti dall'utente. Per altre informazioni su questa proprietà e le relative limitazioni, vedere [Uso dell'API di copia bulk per un'operazione di inserimento batch](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md).

### <a name="added-connection-property-cancelquerytimeout"></a>Aggiunta della proprietà di connessione: cancelQueryTimeout

Il driver Microsoft JDBC 7.0 per SQL Server introduce una nuova proprietà di connessione, `cancelQueryTimeout` per annullare `queryTimeout` su oggetti `java.sql.Connection` e `java.sql.Statement`.

### <a name="added-azure-key-vault-provider-constructors"></a>Aggiunta di costruttori per il provider Azure Key Vault

Il driver Microsoft JDBC 7.0 per SQL Server reintroduce un costruttore rimosso in precedenza, per `SQLServerColumnEncryptionAzureKeyVaultProvider`. È consentita l'autenticazione tramite un metodo personalizzato implementato su `SQLServerKeyVaultAuthenticationCallback` per recuperare un token di accesso.

I nuovi costruttori hanno la definizione seguente:

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

Il driver Microsoft JDBC 7.0 per SQL Server ha aggiornato la dipendenza di Maven da "Microsoft Azure Active Directory Authentication Library (ADAL4J) fo Java" alla versione 1.6.0. Per altre informazioni sulle dipendenze, vedere [Dipendenze delle funzionalità di Microsoft JDBC Driver per SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="64"></a>6.4

Il driver Microsoft JDBC 6.4 per SQL Server è completamente conforme alla specifica JDBC 4.1 e 4.2. I file JAR nel pacchetto 6.4 sono denominati in base alla compatibilità delle versioni di Java. Ad esempio, il file mssql-jdbc-6.4.0.jre8.jar dal pacchetto 6.4 deve essere usato con Java 8.

### <a name="support-for-jdk-9"></a>Supporto per JDK 9

Il driver supporta JDK versione 9.0, oltre a JDK 8.0 e 7.0.

### <a name="jdbc-43-compliance"></a>Conformità a JDBC 4.3

Il driver supporta la specifica Java Database Connectivity API 4.3, oltre a 4.1 e 4.2. I metodi dell'API di JDBC 4.3 sono stati aggiunti ma non ancora implementati. Per informazioni dettagliate, vedere [Conformità a JDBC 4.3 per il driver JDBC](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="added-connection-property-sslprotocol"></a>Aggiunta della proprietà di connessione: sslProtocol

Una nuova proprietà di connessione consente agli utenti di specificare la parola chiave per il protocollo TLS. I valori possibili sono: "TLS", "TLSv1", "TLSv1.1" e "TLSv1.2". Per informazioni dettagliate, vedere [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol).

### <a name="deprecated-connection-property-fipsprovider"></a>Proprietà di connessione deprecata: fipsProvider

La proprietà di connessione `fipsProvider` è stata rimossa dall'elenco delle proprietà di connessione accettate. Per informazioni dettagliate, vedere la [richiesta pull di GitHub](https://github.com/Microsoft/mssql-jdbc/pull/460) correlata.

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>Aggiunta di proprietà di connessione per specificare un TrustManager personalizzato

Il driver supporta ora la specifica di un TrustManager personalizzato con le proprietà di connessione aggiunte `trustManagerClass` e `trustManagerConstructorArg`. È possibile specificare in modo dinamico un set di certificati considerati attendibili per ogni connessione, senza modificare le impostazioni globali per l'ambiente Java Virtual Machine (JVM).

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>Aggiunta del supporto per datetime/smallDatetime nei parametri con valori di tabella

Il driver supporta ora i tipi di dati `datetime` e `smallDatetime` quando si usano parametri con valori di tabella (TVP).

### <a name="added-support-for-the-sqlvariant-datatype"></a>Aggiunta del supporto per il tipo di dati sql_variant

Il driver JDBC supporta ora i tipi di dati `sql_variant` da usare con SQL Server. Il tipo di dati `sql_variant` è supportato anche con funzionalità quali parametri con valori di tabella e copia bulk con le limitazioni seguenti:

* **Per i valori di data**: 

  Quando si usano parametri con valori di tabella per popolare una tabella che contiene valori `datetime`, `smalldatetime` o `date` archiviati in una colonna `sql_variant`, la chiamata del metodo `getDateTime()`, `getSmallDateTime()` o `getDate()` sul set di risultati non funziona e genera l'eccezione seguente:

  `java java.lang.String cannot be cast to java.sql.Timestamp`
    
  In alternativa, usare il metodo `getString()` o `getObject()`.

* **Uso di TVP con sql_variant per valori null**:
  
  Se si usano parametri con valori di tabella per popolare una tabella e inviare un valore NULL al tipo di colonna `sql_variant`, verrà generata un'eccezione. L'inserimento di un valore NULL con il tipo di colonna `sql_variant` in un parametro con valori di tabella non è attualmente supportato.

### <a name="implemented-prepared-statement-metadata-caching"></a>Implementazione della memorizzazione nella cache dei metadati delle istruzioni preparate

Il driver JDBC ha implementato la memorizzazione nella cache dei metadati per le istruzioni preparate per migliorare le prestazioni. Il driver supporta ora la memorizzazione nella cache dei metadati per le istruzioni preparate nel driver con le proprietà di connessione `disableStatementPooling` e `statementPoolingCacheSize`. Questa funzionalità è disabilitata per impostazione predefinita. Per altre informazioni, vedere [Memorizzazione nella cache dei metadati delle istruzioni preparate per il driver JDBC](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md).

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmac"></a>Aggiunta del supporto per l'autenticazione integrata di Azure AD in Linux/Mac

Il driver JDBC supporta ora l'autenticazione integrata di Azure Active Directory in tutti i sistemi operativi supportati (Windows, Linux e Mac) con Kerberos. In alternativa, nei sistemi operativi Windows, gli utenti possono autenticarsi con sqljdbc_auth.

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>Aggiornamento di "Microsoft Azure Active Directory Authentication Library (ADAL4J) per Java" alla versione 1.4.0

Il driver JDBC ha aggiornato la dipendenza di Maven da "Microsoft Azure Active Directory Authentication Library (ADAL4J) for Java" alla versione 1.4.0. Per altre informazioni sulle dipendenze, vedere [Dipendenze delle funzionalità di Microsoft JDBC Driver per SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="62"></a>6.2

Il driver Microsoft JDBC 6.2 per SQL Server è completamente conforme alla specifica JDBC 4.1 e 4.2. I file JAR nel pacchetto 6.2 sono denominati in base alla compatibilità delle versioni di Java. Ad esempio, è consigliato l'uso del file mssql-jdbc-6.2.2.jre8.jar dal pacchetto 6.2 con Java 8.

> [!NOTE]  
> È stato rilevato un problema con il miglioramento della memorizzazione nella cache dei metadati nella versione JDBC 6.2 RTW rilasciata il 29 giugno 2017. È stato eseguito il rollback del miglioramento e sono stati rilasciati nuovi file JAR (versione 6.2.1) in data 17 luglio 2017. 
>
> Un altro miglioramento ha aggiornato la versione della libreria dipendente da Azure Key Vault alla versione 1.0.0 e sono stati rilasciati nuovi file JAR (versione 6.2.2) in data 19 ottobre 2017.
>
> Scaricare gli aggiornamenti più recenti per il driver JDBC 6.2 dall'[Area download Microsoft](https://go.microsoft.com/fwlink/?linkid=852460), da [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) e da [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver). Aggiornare i progetti per l'uso dei file JAR della versione 6.2.2. Per altre informazioni, vedere le note sulla versione per le versioni [6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) e [6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2).

### <a name="azure-ad-support-for-linux"></a>Supporto di Azure AD per Linux

Connettere le applicazioni Linux al database SQL di Azure con l'autenticazione di Azure AD tramite i metodi con nome utente/password e token di accesso.

### <a name="fips-enabled-jvms"></a>JVM abilitate per FIPS

È ora possibile usare il driver JDBC su JVM eseguite in modalità conformità 140 FIPS (Federal informazioni Processing Standard) per soddisfare gli standard federali sulla conformità.

### <a name="kerberos-authentication-improvements"></a>Miglioramenti per l'autenticazione Kerberos

Il driver JDBC include ora il supporto per:

- Metodo basato su entità di sicurezza/password per le applicazioni in cui la configurazione di Kerberos non può essere modificata o non è possibile recuperare un nuovo token o keytab. Questo metodo può essere usato per l'autenticazione in un'istanza di SQL Server che consente solo l'autenticazione Kerberos.
- Autenticazione tra aree di autenticazione che usa l'autenticazione integrata Kerberos senza impostare in modo esplicito il nome dell'entità servizio (SPN) del server. Il driver calcola ora automaticamente l'area di autenticazione anche quando non viene fornita.
- Delega vincolata Kerberos con l'accettazione di credenziali utente rappresentate come oggetto credenziali GSS tramite l'origine dati. Queste credenziali rappresentate vengono poi usate per stabilire una connessione Kerberos.

### <a name="added-timeouts"></a>Aggiunta dei timeout

Il driver JDBC supporta ora i timeout configurabili seguenti. È possibile modificarli in base alle esigenze dell'applicazione.

- Timeout delle query per controllare il numero di secondi di attesa prima che si verifichi un timeout durante l'esecuzione di una query.
- Timeout del socket per specificare il numero di millisecondi di attesa prima che si verifichi un timeout per un'operazione di lettura o accettazione del socket.

## <a name="61"></a>6.1

Il driver Microsoft JDBC 6.1 per SQL Server è completamente conforme alla specifica JDBC 4.1 e 4.2. Questa è la versione open source iniziale del driver JDBC. Contiene i file mssql-jdbc-6.1.0.jre8.jar e mssql-jdbc-6.1.0.jre7.jar, che corrispondono alla compatibilità delle versioni di Java.

## <a name="60"></a>6.0

Il driver Microsoft JDBC 6.0 per SQL Server è completamente conforme alla specifica JDBC 4.1 e 4.2. I file JAR nel pacchetto 6.0 sono denominati in base alla relativa conformità con la versione dell'API JDBC. Ad esempio, il file sqljdbc42.jar dal pacchetto 6.0 è conforme all'API JDBC 4.2. Analogamente, il file sqljdbc41.jar è conforme all'API JDBC 4.1.

Per assicurarsi di avere il file corretto sqljdbc41.jar o sqljdbc42.jar, eseguire le righe di codice seguenti. Se l'output è "Versione driver: 6.0.7507.100", è disponibile il pacchetto del driver JDBC 6.0.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

Il driver supporta la funzionalità Always Encrypted in SQL Server 2016. Questa funzionalità garantisce che i dati sensibili non vengano mai visualizzati in testo non crittografato in un'istanza di SQL Server. Always Encrypted crittografa in modo trasparente i dati nell'applicazione, in modo che SQL Server debba gestire solo i dati crittografati e non i valori di testo non crittografato. In caso di compromissione dell'istanza di SQL Server o del computer host, un utente malintenzionato ottiene solo il testo crittografato dei dati sensibili. Per informazioni dettagliate, vedere [Uso di Always Encrypted con il JDBC Driver](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).

### <a name="internationalized-domain-names"></a>Nomi IDN (Internationalized Domain Name)

Il driver supporta i nomi IDN (Internationalized Domain Name) per i nomi dei server. Per informazioni dettagliate, vedere "Utilizzo di International Domain Names (IDN)" nell'articolo [Caratteristiche internazionali del driver JDBC](../../connect/jdbc/international-features-of-the-jdbc-driver.md).

### <a name="parameterized-queries"></a>Query con parametri

Il driver supporta ora il recupero dei metadati dei parametri con istruzioni preparate per le query complesse, ad esempio le sottoquery e/o i join. Si noti che questo miglioramento è disponibile solo quando si usa SQL Server 2012 e versioni successive.

### <a name="azure-active-directory"></a>Azure Active Directory

L'autenticazione di Azure AD è un meccanismo di connessione al database SQL di Azure v12 tramite identità in Azure AD. Usare l'autenticazione di Azure AD per gestire centralmente le identità degli utenti del database e come alternativa all'autenticazione di SQL Server. 

È possibile usare il driver JDBC 6.0 per specificare le credenziali di Azure AD nella stringa di connessione JDBC per connettersi al database SQL di Azure. Per informazioni dettagliate, vedere la proprietà di autenticazione nell'articolo [Impostazione delle proprietà delle connessioni](../../connect/jdbc/setting-the-connection-properties.md).

### <a name="table-valued-parameters"></a>Parametri con valori di tabella

I parametri con valori di tabella offrono un modo semplice per effettuare il marshalling di più righe di dati da un'applicazione client di SQL Server senza richiedere più round trip o una logica speciale sul lato server per l'elaborazione dei dati. I parametri con valori di tabella possono essere usati per incapsulare le righe di dati in un'applicazione client e inviare i dati al server in un singolo comando con parametri. Le righe di dati in ingresso vengono archiviate in una variabile di tabella su cui è possibile operare tramite Transact-SQL. Per informazioni dettagliate, vedere [Uso di parametri con valori di tabella](../../connect/jdbc/using-table-valued-parameters.md).

### <a name="always-on-availability-groups"></a>Gruppi di disponibilità AlwaysOn

Il driver supporta ora le connessioni trasparenti ai gruppi di disponibilità Always On. Il driver individua rapidamente la topologia AlwaysOn corrente dell'infrastruttura server e si connette in modo trasparente al server attivo corrente.

## <a name="42"></a>4.2

Il driver Microsoft JDBC 4.2 per SQL Server è completamente conforme alla specifica JDBC 4.1 e 4.2. I file JAR nel pacchetto 4.2 sono denominati in base alla relativa conformità con la versione dell'API JDBC. Ad esempio, il file sqljdbc42.jar dal pacchetto 4.2 è conforme all'API JDBC 4.2. Analogamente, il file sqljdbc41.jar è conforme all'API JDBC 4.1.

Per assicurarsi di avere il file corretto sqljdbc41.jar o sqljdbc42.jar, eseguire le righe di codice seguenti. Se l'output è "Versione driver: 4.2.6420.100", è disponibile il pacchetto del driver JDBC 4.2.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>Supporto per JDK 8

Il driver supporta JDK versione 8.0, oltre a JDK 7.0, 6.0 e 5.0.

### <a name="jdbc-41-and-42-compliance"></a>Conformità con JDBC 4.1 e 4.2

Il driver supporta le specifiche Java Database Connectivity API 4.1 e 4.2, oltre a 4.0. Per informazioni dettagliate, vedere [Conformità con JDBC 4.1 per il driver JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) e [Conformità con JDBC 4.2 per il driver JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).

### <a name="bulk-copy"></a>Copia bulk

La funzionalità di copia bulk viene usata per copiare rapidamente grandi quantità di dati in tabelle o viste nei database di SQL Server. Per informazioni dettagliate, vedere [Uso della copia bulk con il driver JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

### <a name="xa-transaction-rollback-option"></a>Opzione di rollback di transazione XA

Il driver include nuove opzioni di timeout per il rollback automatico esistente di transazioni non preparate. Per informazioni dettagliate, vedere [Informazioni sulle transazioni XA](../../connect/jdbc/understanding-xa-transactions.md).

### <a name="new-kerberos-principal-connection-property"></a>Nuova proprietà di connessione principale Kerberos

Il driver usa una nuova proprietà di connessione per aumentare la flessibilità con le connessioni Kerberos. Per informazioni dettagliate, vedere [Uso dell'autenticazione integrata Kerberos per la connessione a SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md).

## <a name="41"></a>4.1

### <a name="support-for-jdk-7"></a>Supporto per JDK 7

Il driver supporta JDK versione 7.0, oltre a JDK 6.0 e 5.0.

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>Le applicazioni JDBC Driver 6.4, 6.0, 4.2 e 4.1 non supportano i computer Itanium

Le applicazioni Microsoft JDBC Driver 6.4, 6.0, 4.2 e 4.1 per SQL Server non supportano i computer Itanium.

## <a name="see-also"></a>Vedere anche

[Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)
