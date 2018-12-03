---
title: Uso di Always Encrypted con i driver PHP per SQL Server | Microsoft Docs
ms.date: 01/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
manager: mbarwin
ms.openlocfilehash: 531286af24740e37e125708a4b874b6aba27c3dc
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52403426"
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>Uso di Always Encrypted con i driver PHP per SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>Applicabile a
 -   Microsoft Driver 5.2 per PHP per SQL Server
 
## <a name="introduction"></a>Introduzione

Questo articolo fornisce informazioni su come sviluppare applicazioni PHP usando [Always Encrypted (motore di Database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e il [driver PHP per SQL Server](../../connect/php/Microsoft-php-driver-for-sql-server.md).

Always Encrypted consente alle applicazioni client di eseguire la crittografia dei dati sensibili senza mai rivelare i dati o le chiavi di crittografia a SQL Server o al database SQL di Azure. Un driver abilitato per Always Encrypted, come ODBC Driver for SQL Server, esegue in modo trasparente la crittografia e la decrittografia dei dati sensibili nell'applicazione client. Il driver determina automaticamente i parametri di query corrispondenti alle colonne di database con dati sensibili (protette mediante Always Encrypted) e crittografa i valori di tali parametri prima di passare i dati a SQL Server o al database SQL di Azure. Analogamente, il driver esegue in modo trasparente la decrittografia dei dati, recuperati dalle colonne di database crittografate nei risultati delle query. Per altre informazioni, vedere [Always Encrypted (motore di database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Il driver PHP per SQL Server usano il Driver ODBC per SQL Server crittografare dati sensibili.

## <a name="prerequisites"></a>Prerequisites

 -   Configurare Always Encrypted nel database. Questa configurazione implica il provisioning di chiavi Always Encrypted e l'impostazione della crittografia per le colonne di database selezionate. Se non è presente un database in cui Always Encrypted è configurato, seguire le istruzioni fornite nel blog di [introduzione a Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted). In particolare, il database deve contenere le definizioni dei metadati per una tabella che contiene uno o più colonne crittografate con tale chiave CEK, Column Master Key (CMK) e una chiave di crittografia di colonna (CEK).
 -   Assicurarsi che il Driver ODBC per SQL Server versione 17 o successiva è installato nel computer di sviluppo. Per informazioni dettagliate, vedere [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="enabling-always-encrypted-in-a-php-application"></a>Abilitazione di Always Encrypted in un'applicazione PHP

Il modo più semplice per abilitare la crittografia dei parametri destinati alle colonne crittografate e la decrittografia dei risultati delle query consiste nell'impostare il valore della parola chiave della stringa di connessione `ColumnEncryption` su `Enabled`. Di seguito è riportati esempi di abilitazione di Always Encrypted nel driver PDO_SQLSRV e SQLSRV:

SQLSRV:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled");
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

Abilitazione di Always Encrypted non è sufficiente per la crittografia o decrittografia abbia esito positivo; è anche necessario assicurarsi che:
 -   L'applicazione abbia le autorizzazioni di database VIEW ANY COLUMN MASTER KEY DEFINITION e VIEW ANY COLUMN ENCRYPTION KEY DEFINITION, necessarie per accedere ai metadati sulle chiavi Always Encrypted nel database. Per informazioni dettagliate, vedere [autorizzazione Database](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
 -   L'applicazione può accedere la CMK che protegge il Cek per le colonne crittografate sottoposti a query. Questo requisito dipende dal provider dell'archivio chiavi contenente la chiave CMK. Per altre informazioni, vedere [uso di archivi di chiavi Master della colonna](#working-with-column-master-key-stores).

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recupero e modifica di dati nelle colonne crittografate

Dopo aver abilitato Always Encrypted per una connessione, è possibile usare le API SQLSRV standard (vedere [riferimento all'API del Driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)) o le API PDO_SQLSRV (vedere [riferimento all'API del Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)) per recuperare o modificare i dati nelle colonne crittografate del database. Supponendo che l'applicazione disponga delle autorizzazioni di database necessari e può accedere alla chiave master di colonna, il driver crittografa eventuali parametri di query destinati alle colonne crittografate e decrittografare i dati recuperati dalle colonne crittografate, comportamento in modo trasparente al applicazione come se le colonne non sono state crittografate.

Se la funzionalità Always Encrypted non è abilitata, le query con parametri destinati alle colonne crittografate hanno esito negativo. I dati possono essere comunque recuperati dalle colonne crittografate, a condizione che non presentino parametri destinati alle colonne crittografate. Tuttavia, il driver non tenterà qualsiasi decrittografia e l'applicazione riceve i dati crittografati binari (come matrici di byte).

La tabella seguente riepiloga il comportamento delle query, a seconda che la funzionalità Always Encrypted sia abilitata o meno:

|Caratteristica della query|Always Encrypted è abilitato e l'applicazione può accedere alle chiavi e ai metadati delle chiavi|Always Encrypted è abilitato e l'applicazione non può accedere alle chiavi o ai metadati delle chiavi|Always Encrypted è disabilitato|
|---|---|---|---|
|Parametri destinati alle colonne crittografate.|I valori dei parametri vengono crittografati in modo trasparente.|Errore|Errore|
|Recupero di dati dalle colonne crittografate, senza parametri destinati alle colonne crittografate.|I risultati delle colonne vengono decrittografati in modo trasparente. L'applicazione riceve i valori di colonna in testo normale. |Errore|I risultati delle colonne crittografate non vengono decrittografate. L'applicazione riceve i valori crittografati come matrici di byte.|
 
Gli esempi seguenti illustrano il recupero e la modifica dei dati nelle colonne crittografate. Gli esempi presuppongono che una tabella con lo schema seguente. Le colonne SSN e BirthDate sono crittografate.
```
CREATE TABLE [dbo].[Patients](
 [PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

### <a name="data-insertion-example"></a>Esempio di inserimento dei dati

Gli esempi seguenti illustrano come usare il driver SQLSRV e PDO_SQLSRV per inserire una riga nella tabella dei pazienti. Tenere presente quanto segue:
 -   Il codice di esempio non contiene alcun elemento specifico per la crittografia. Il driver rileva automaticamente e crittografa i valori dei parametri SSN e BirthDate, che hanno come destinazione le colonne crittografate. In questo modo la crittografia diventa trasparente per l'applicazione.
 -   I valori inseriti nelle colonne di database, incluse quelle crittografate, vengono passati come parametri associati. Quando si inviano valori a colonne non crittografate, l'uso dei parametri è facoltativo, nonostante sia consigliabile per prevenire attacchi SQL injection. È invece necessario usare i parametri in presenza di valori destinati a colonne crittografate. Se i valori inseriti nelle colonne SSN o BirthDate sono stati passati come valori letterali incorporati nell'istruzione della query, la query avrà esito negativo perché il driver non prova a crittografare o in caso contrario elaborare valori letterali nelle query. Di conseguenza, il server li rifiuterà come incompatibili con le colonne crittografate.
 -   Quando si inseriscono valori utilizzando i parametri di associazione, un tipo SQL che è identico al tipo di dati della colonna di destinazione o la cui conversione al tipo di dati della colonna di destinazione è supportata deve essere passato al database. Questo requisito è perché Always Encrypted supporta alcune conversioni di tipo (per informazioni dettagliate, vedere [Always Encrypted (motore di Database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)). I due driver PHP, SQLSRV e PDO_SQLSRV, ognuno ha un meccanismo per consentire all'utente di determinare il tipo SQL del valore. Pertanto, l'utente non dovrà fornire in modo esplicito il tipo SQL.
  -   Per il driver SQLSRV, l'utente è disponibili due opzioni:
   -   Si basano sul driver PHP per determinare e impostare il tipo SQL a destra. In questo caso, l'utente deve usare `sqlsrv_prepare` e `sqlsrv_execute` per eseguire una query con parametri.
   -   Impostare il tipo SQL in modo esplicito.
  -   Per il driver PDO_SQLSRV, l'utente non hanno la possibilità di impostare in modo esplicito il tipo SQL di un parametro. Il driver PDO_SQLSRV automaticamente consente di determinare il tipo SQL quando si associa un parametro.
 -   Per i driver determinare il tipo SQL, esistono alcune limitazioni:
  -   Driver SQLSRV:
   -   Se si desidera ottenere il driver per determinare i tipi SQL per le colonne crittografate, l'utente deve utilizzare `sqlsrv_prepare` e `sqlsrv_execute`.
   -   Se `sqlsrv_query` è preferito, l'utente è responsabile per la specifica dei tipi SQL per tutti i parametri. Il tipo SQL specificato deve includere la lunghezza della stringa per il tipo stringa e la scala e precisione per i tipi decimali.
  -   Driver PDO_SQLSRV:
   -   L'attributo di istruzione `PDO::SQLSRV_ATTR_DIRECT_QUERY` non è supportato in una query con parametri.
   -   L'attributo di istruzione `PDO::ATTR_EMULATE_PREPARES` non è supportato in una query con parametri.
   
Driver SQLSRV e [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel;
$birthDate = "1996-10-19";
$params = array($ssn, $firstName, $lastName, $birthDate);
// during sqlsrv_prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = sqlsrv_prepare($conn, $query, $params);
sqlsrv_execute($stmt);
```

Driver SQLSRV e [sqlsrv_query](../../connect/php/sqlsrv-query.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel";
$birthDate = "1996-10-19";
// need to provide the SQL types for ALL parameters  
// note the SQL types (including the string length) have to be the same at the column definition
$params = array(array(&$ssn, null, null, SQLSRV_SQLTYPE_CHAR(11)),
                array(&$firstName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$lastName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$birthDate, null, null, SQLSRV_SQLTYPE_DATE));
sqlsrv_query($conn, $query, $params);
```

Driver PDO_SQLSRV e [PDO:: Prepare](../../connect/php/pdo-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Able";
$birthDate = "1996-10-19";
// during PDO::prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
$stmt->bindParam(2, $firstName);
$stmt->bindParam(3, $lastName);
$stmt->bindParam(4, $birthDate);
$stmt->execute();
```

### <a name="plaintext-data-retrieval-example"></a>Esempio di recupero dati in testo normale

Gli esempi seguenti illustrano il filtraggio dei dati basata su valori crittografati e il recupero di dati crittografato dalle colonne crittografate usando il driver PDO_SQLSRV e SQLSRV. Tenere presente quanto segue:
 -   Il valore usato nella clausola WHERE per filtrare la colonna SSN deve essere passato usando il parametro bind, in modo che il driver possa crittografarlo in modo trasparente prima dell'invio al server.
 -   Quando si esegue una query con parametri associati, il driver PHP determina automaticamente il tipo SQL per l'utente, a meno che l'utente specifica in modo esplicito il tipo SQL quando si usa il driver SQLSRV.
 -   Tutti i valori stampati dal programma saranno in testo non crittografato, perché il driver decrittografa in modo trasparente i dati recuperati dalle colonne SSN e BirthDate.
 
Nota: Le query possono eseguire confronti di uguaglianza nelle colonne crittografate a solo se la crittografia è deterministica. Per altre informazioni, vedere [Selezione della crittografia deterministica o casuale](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = sqlsrv_prepare($conn, $query, array(&$ssn));
// during sqlsrv_execute, the driver encrypts the ssn value and passes it to the database
sqlsrv_execute($stmt);
// fetch like usual
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
// during PDOStatement::execute, the driver encrypts the ssn value and passes it to the database
$stmt->execute();
// fetch like usual
$row = $stmt->fetch();
```

### <a name="ciphertext-data-retrieval-example"></a>Esempio di recupero dei dati del testo crittografato

Se Always Encrypted non è abilitato, una query può comunque recuperare dati dalle colonne crittografate, a condizione che non presenti parametri destinati alle colonne crittografate.

Gli esempi seguenti illustrano il recupero di dati crittografati binari dalle colonne crittografate usando il driver PDO_SQLSRV e SQLSRV. Tenere presente quanto segue:
 -   Poiché la funzionalità Always Encrypted non è abilitata nella stringa di connessione, la query restituisce i valori crittografati di SSN e BirthDate come matrici di byte. Il programma converte i valori in stringhe.
 -   Una query che recupera dati dalle colonne crittografate con Always Encrypted disabilitato può avere parametri, a condizione che nessuno dei parametri sia destinato a una colonna crittografata. La query seguente filtra in base alla colonna LastName, che non è crittografata nel database. Se la query filtrasse in base a SSN o BirthDate, l'esito sarebbe negativo.
 
SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = sqlsrv_prepare($conn, $query, array(&$lastName));
sqlsrv_execute($stmt);
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $lastName);
$stmt->execute();
$row = $stmt->fetch();
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Come evitare i problemi comuni quando si eseguono query su colonne crittografate

Questa sezione descrive categorie di errori comuni che si verificano quando si eseguono query su colonne crittografate da applicazioni PHP e contiene alcune linee guida su come correggere tali errori.

#### <a name="unsupported-data-type-conversion-errors"></a>Errori di conversione dei tipi di dati non supportati

Always Encrypted supporta alcune conversioni per i tipi di dati crittografati. Per l'elenco dettagliato delle conversioni dei tipi supportati, vedere [Always Encrypted (motore di database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Per evitare errori di conversione dei tipi di dati, eseguire le operazioni seguenti:
 -   Quando si usa il driver SQLSRV con `sqlsrv_prepare` e `sqlsrv_execute` tipo SQL, con la dimensione della colonna e il numero di cifre decimali del parametro viene determinato automaticamente.
 -   Quando si usa il driver PDO_SQLSRV per eseguire una query, il tipo SQL con la dimensione della colonna e il numero di cifre decimali del parametro è determinato inoltre automaticamente
 -   Quando si usa il driver SQLSRV con `sqlsrv_query` per eseguire una query:
  -   Il tipo SQL del parametro è sia esattamente uguale al tipo della colonna di destinazione o la conversione dal tipo SQL al tipo della colonna è supportata.
  -   La precisione e la scala dei parametri destinati alle colonne dei tipi di dati `decimal` e `numeric` di SQL Server sono uguali a quelle configurate per la colonna di destinazione.
  -   La precisione dei parametri destinati alle colonne dei tipi di dati `datetime2`, `datetimeoffset` e `time` di SQL Server non è maggiore della precisione per la colonna di destinazione nelle query che modificano la colonna di destinazione.
 -   Non usare gli attributi di istruzione PDO_SQLSRV `PDO::SQLSRV_ATTR_DIRECT_QUERY` o `PDO::ATTR_EMULATE_PREPARES` in una query con parametri
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Errori causati dal passaggio di testo non crittografato anziché di valori crittografati

Qualsiasi valore destinato a una colonna crittografata deve essere crittografati prima dell'invio al server. Il tentativo di inserire, modificare o filtrare in base a un valore di testo non crittografato in una colonna crittografata genera un errore. Per evitare tali errori, verificare che:
 -   Always Encrypted è abilitato (nella stringa di connessione, impostare il `ColumnEncryption` parola chiave da `Enabled`).
 -   Per inviare i dati destinati alle colonne crittografate venga usata l'associazione dei parametri. Nell'esempio seguente viene illustrata una query che filtra in modo errato un valore letterale o costante in una colonna crittografata (SSN):
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>Controllo dell'impatto di Always Encrypted sulle prestazioni

Considerato che Always Encrypted è una tecnologia di crittografia lato client, la maggior parte del sovraccarico delle prestazioni si verifica sul lato client, non nel database. A parte il costo delle operazioni di crittografia e decrittografia, le altre origini di sovraccarico delle prestazioni sul lato client sono le seguenti:
 -   Round trip aggiuntivi al database per recuperare i metadati per i parametri di query.
 -   Chiamate a un archivio delle chiavi master delle colonne per accedere alla chiave master di una colonna.
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>Round trip per recuperare i metadati per i parametri di query

Se Always Encrypted è abilitato per una connessione, per impostazione predefinita il driver ODBC chiamerà [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) per ogni query con parametri, passando l'istruzione di query (senza i valori dei parametri) a SQL Server. Questa stored procedure analizza l'istruzione di query per scoprire se i parametri devono essere crittografati e, in caso affermativo, restituisce le informazioni relative alla crittografia per ogni parametro consentire al driver di crittografarli.

Poiché i driver PHP consentono all'utente di associare un parametro in un'istruzione preparata senza fornire il codice SQL digitare, quando si associa un parametro in una connessione di Always Encrypted abilitata, il driver PHP chiamare [SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md) di parametro per ottenere il tipo SQL, le dimensioni di colonna e cifre decimali. I metadati vengono quindi utilizzati per chiamare [SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md). Questi extra `SQLDescribeParam` chiamate non richiedono round trip aggiuntivi al database come il Driver ODBC ha già memorizzate le informazioni sul lato client quando `sys.sp_describe_parameter_encryption` è stato chiamato.

I comportamenti precedenti garantiscono un elevato livello di trasparenza per l'applicazione client (e lo sviluppatore dell'applicazione) non è necessario essere a conoscenza di quali query accedono alle colonne crittografate, purché i valori destinati alle colonne crittografate vengano passati al driver in parametri.

A differenza di ODBC Driver for SQL Server, l'abilitazione di Always Encrypted a livello di istruzione/query non è ancora supportata dei driver PHP. 

### <a name="column-encryption-key-caching"></a>Memorizzazione nella cache delle chiavi di crittografia della colonna

Per ridurre il numero di chiamate a un archivio chiavi master della colonna per decrittografare le chiavi di crittografia di colonna (CEK), il driver memorizza nella cache il testo non crittografato dei Cek in memoria. Dopo aver ricevuto la CEK che lo crittografato (chiave ECEK) dai metadati del database, il driver ODBC tenta innanzitutto di trovare CEK crittografato corrispondente al valore della chiave crittografato nella cache. Il driver chiama l'archivio chiavi contenente la chiave CMK solo se non riesce a trovare il testo non crittografato corrispondente CEK nella cache.

Nota: In ODBC Driver for SQL Server, le voci nella cache vengono eliminate dopo un timeout di due ore. Questo comportamento significa che per una determinata chiave ECEK, il driver contatta l'archivio chiavi una sola volta durante il ciclo di vita dell'applicazione o ogni due ore, a seconda del valore è minore.

## <a name="working-with-column-master-key-stores"></a>Uso degli archivi delle chiavi master delle colonne

Per crittografare o decrittografare i dati, il driver deve ottenere una CEK configurato per la colonna di destinazione. Cek vengono archiviati in formato crittografato (ECEKs) nei metadati del database. Ogni chiave CEK dispone di una CMK corrispondente che è stata usata per crittografarlo. Il [metadati del database](../../t-sql/statements/create-column-master-key-transact-sql.md) non archivia la chiave CMK stesso; contiene solo il nome dell'archivio chiavi e informazioni che l'archivio delle chiavi è possibile usare per individuare la chiave CMK.

Per ottenere il valore di testo normale di una chiave ECEK, il driver Ottiene prima di tutto i metadati relativi sia la CEK e le chiavi master di colonna corrispondente e quindi Usa queste informazioni per contattare l'archivio chiavi contenente la chiave CMK e lo richiede, per decrittografare la chiave ECEK. Il driver comunica con un archivio chiavi usando un provider dell'archivio chiavi.

Per il Driver Microsoft 5.3.0 per PHP per SQL Server, sono supportati solo i Provider Store Certificate di Windows e Azure Key Vault. L'altro Provider di archivio chiavi è supportata dal Driver ODBC (Provider di archivio chiavi personalizzato) non è ancora supportato.

### <a name="using-the-windows-certificate-store-provider"></a>Uso del provider per l'archivio certificati Windows

Il Driver ODBC per SQL Server in Windows include un provider di archivio chiavi master di colonna predefiniti per Store il certificato di Windows, denominato `MSSQL_CERTIFICATE_STORE`. (Questo provider non disponibile in macOS o Linux). A questo provider, la chiave CMK è archiviata localmente nel computer client e alcuna configurazione aggiuntiva per l'applicazione non è necessario usarlo con il driver. Tuttavia, l'applicazione deve avere accesso al certificato e la relativa chiave privata nell'archivio. Per altre informazioni, vedere [Creare e archiviare chiavi master della colonna (Always Encrypted)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

### <a name="using-azure-key-vault"></a>Con Azure Key Vault

Azure Key Vault offre un modo per archiviare le chiavi di crittografia, le password e altri segreti tramite Azure e può essere utilizzato per archiviare le chiavi per Always Encrypted. Il Driver ODBC per SQL Server (versione 17 e versioni successive) include un provider dell'archivio chiavi master predefinito per Azure Key Vault. Configurazione di Azure Key Vault di gestire le opzioni di connessione seguente: `KeyStoreAuthentication`, `KeyStorePrincipalId`, e `KeyStoreSecret`. 
 -   `KeyStoreAuthentication` può assumere uno dei due valori stringa possibili: `KeyVaultPassword` e `KeyVaultClientSecret`. Questi valori consentono di controllare il tipo di credenziali di autenticazione con le altre due parole chiave.
 -   `KeyStorePrincipalId` accetta una stringa che rappresenta un identificatore per l'account che cercano di accedere a Azure Key Vault. 
     -   Se `KeyStoreAuthentication` è impostata su `KeyVaultPassword`, quindi `KeyStorePrincipalId` deve essere il nome di un utente di Azure Active Directory.
     -   Se `KeyStoreAuthentication` è impostata su `KeyVaultClientSecret`, quindi `KeyStorePrincipalId` deve essere un ID applicazione client.
 -   `KeyStoreSecret` accetta una stringa che rappresenta un segreto della credenziale. 
     -   Se `KeyStoreAuthentication` è impostata su `KeyVaultPassword`, quindi `KeyStoreSecret` deve essere la password dell'utente. 
     -   Se `KeyStoreAuthentication` è impostata su `KeyVaultClientSecret`, quindi `KeyStoreSecret` deve essere il segreto dell'applicazione associato all'ID client dell'applicazione.

Tutte le tre opzioni devono essere presente nella stringa di connessione per usare Azure Key Vault. È inoltre `ColumnEncryption` deve essere impostata su `Enabled`. Se `ColumnEncryption` è impostata su `Disabled` ma le opzioni di Azure Key Vault sono presenti, lo script continuerà senza errori, ma non verrà eseguita alcuna crittografia.

Negli esempi seguenti illustrano come connettersi a SQL Server con Azure Key Vault.

SQLSRV:

Utilizzo di un account Azure Active Directory:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultPassword", "KeyStorePrincipalId"=>$AADUsername, "KeyStoreAuthentication"=>$AADPassword);
$conn = sqlsrv_connect($server, $connectionInfo);
```
Utilizzo di un ID client dell'applicazione Azure e un segreto:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultClientSecret", "KeyStorePrincipalId"=>$applicationClientID, "KeyStoreAuthentication"=>$applicationClientSecret);
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV: Utilizzo di un account Azure Active Directory:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultPassword; KeyStorePrincipalId = $AADUsername; KeyStoreAuthentication = $AADPassword;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```
Utilizzo di un ID client dell'applicazione Azure e un segreto:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultClientSecret; KeyStorePrincipalId = $applicationClientID; KeyStoreAuthentication = $applicationClientSecret;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>Limitazioni dei driver PHP quando si usa Always Encrypted

SQLSRV e PDO_SQLSRV:
 -   Linux/macOS non supportano Provider Store Certificate di Windows
 -   Forzare la crittografia dei parametri
 -   Abilitazione di Always Encrypted a livello di istruzione 
 -   Quando si usa la crittografia sempre attiva funzionalità non UTF8 impostazioni locali e in Linux e macOS (ad esempio, "it_IT. ISO-8859-1 "), inserimento di dati null o una stringa vuota in una colonna char crittografati potrebbe non funzionare a meno che non tabella codici 1252 è stato installato nel sistema
 
SQLSRV:
 -   Usando `sqlsrv_query` per il parametro di associazione senza specificare il tipo SQL
 -   Usando `sqlsrv_prepare` per l'associazione di parametri in un batch di istruzioni SQL  
 
Solo PDO_SQLSRV:
 -   `PDO::SQLSRV_ATTR_DIRECT_QUERY` attributo di istruzione specificato in una query con parametri
 -   `PDO::ATTR_EMULATE_PREPARE` attributo di istruzione specificato in una query con parametri
 -   associazione di parametri in un batch di istruzioni SQL
 
Il driver PHP anche ereditare le limitazioni imposte dal Driver ODBC per SQL Server e il database. Visualizzare [limitazioni del driver ODBC quando si usa Always Encrypted](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) e [Always Encrypted informazioni sulle funzionalità](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details).  
  
## <a name="see-also"></a>Vedere anche  
[Guida di programmazione per il driver SQL PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Riferimento all'API del driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
