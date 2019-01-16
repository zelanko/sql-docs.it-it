---
title: Uso di Always Encrypted con ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
ms.author: v-chojas
manager: craigg
author: MightyPen
ms.openlocfilehash: f91ba6d5e7120f26c4ce4f8572eea779cdddebfc
ms.sourcegitcommit: 170c275ece5969ff0c8c413987c4f2062459db21
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/11/2019
ms.locfileid: "54226688"
---
# <a name="using-always-encrypted-with-the-odbc-driver-for-sql-server"></a>Uso di Always Encrypted con ODBC Driver for SQL Server
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

### <a name="applicable-to"></a>Applicabile a

- ODBC Driver 13.1 for SQL Server
- ODBC Driver 17 for SQL Server

### <a name="introduction"></a>Introduzione

Questo articolo fornisce informazioni su come sviluppare applicazioni ODBC usando [Always Encrypted (motore di Database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e il [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

Always Encrypted consente alle applicazioni client di eseguire la crittografia dei dati sensibili senza mai rivelare i dati o le chiavi di crittografia a SQL Server o al database SQL di Azure. Di tutto ciò si occupa un driver abilitato per Always Encrypted, come ODBC Driver for SQL Server, che esegue in modo trasparente la crittografia e la decrittografia dei dati sensibili nell'applicazione client. Il driver determina automaticamente i parametri di query corrispondenti alle colonne di database con dati sensibili (protette mediante Always Encrypted) e crittografa i valori di tali parametri prima di passare i dati a SQL Server o al database SQL di Azure. Analogamente, il driver esegue in modo trasparente la decrittografia dei dati, recuperati dalle colonne di database crittografate nei risultati delle query. Per altre informazioni, vedere [Always Encrypted (motore di database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md).

### <a name="prerequisites"></a>Prerequisites

Configurare Always Encrypted nel database. Ciò implica il provisioning di chiavi Always Encrypted e l'impostazione della crittografia per le colonne di database selezionate. Se non è presente un database in cui Always Encrypted è configurato, seguire le istruzioni fornite nel blog di [introduzione a Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted). In particolare, il database deve contenere le definizioni dei metadati per una tabella che contiene uno o più colonne crittografate con tale chiave CEK, Column Master Key (CMK) e una chiave di crittografia di colonna (CEK).

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>Abilitazione di Always Encrypted in un'applicazione ODBC

Il modo più semplice per abilitare la crittografia dei parametri e la decrittografia di colonna crittografati con set di risultati consiste nell'impostare il valore della `ColumnEncryption` parola chiave della stringa di connessione **Enabled**. Di seguito è riportato un esempio di stringa di connessione che abilita la Always Encrypted:

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

Always Encrypted può anche essere abilitato nella configurazione di DSN, usando la stessa chiave e valore (che eseguirà l'override di impostazione stringa di connessione, se presente), o a livello di codice con il `SQL_COPT_SS_COLUMN_ENCRYPTION` attributo pre-connessione. Impostarlo in questo modo esegue l'override del valore impostato nella stringa di connessione o DSN:

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

Dopo aver abilitato per la connessione, è possibile modificare il comportamento di Always Encrypted per le singole query. Visualizzare [controllare le prestazioni impatto di Always Encrypted](#controlling-the-performance-impact-of-always-encrypted) sotto per altre informazioni.

Si noti che l'abilitazione di Always Encrypted non è sufficiente per la crittografia o decrittografia abbia esito positivo; è anche necessario assicurarsi che:

- L'applicazione abbia le autorizzazioni di database *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , necessarie per accedere ai metadati sulle chiavi Always Encrypted nel database. Per informazioni dettagliate, vedere [autorizzazioni di Database](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).

- L'applicazione può accedere la CMK che protegge il Cek per le colonne crittografate sottoposti a query. Questo processo dipende il provider dell'archivio chiavi che archivia la chiave CMK. Visualizzare [uso di archivi di chiavi Master della colonna](#working-with-column-master-key-stores) per altre informazioni.

### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recupero e modifica di dati nelle colonne crittografate

Dopo aver abilitato Always Encrypted per una connessione, è possibile usare le API ODBC standard (vedere [codice di esempio ODBC](https://code.msdn.microsoft.com/windowsapps/ODBC-sample-191624ae/sourcecode?fileId=51137&pathId=1980325953) oppure [riferimento per programmatori ODBC](https://msdn.microsoft.com/library/ms714177(v=vs.85).aspx)) per recuperare o modificare i dati in colonne crittografate del database. Supponendo che l'applicazione ha richiesto autorizzazioni di database e possono accedere alla chiave master di colonna, il driver verrà crittografato eventuali parametri di query che interessano le colonne crittografate e decrittografare i dati recuperati dalle colonne crittografate, si comporta in modo trasparente per il applicazione come se le colonne non sono state crittografate.

Se Always Encrypted non è abilitato, le query con parametri destinati alle colonne crittografate avranno esito negativo. I dati possono essere comunque recuperati dalle colonne crittografate, a condizione che non presentino parametri destinati alle colonne crittografate. Tuttavia, il driver non tenterà di qualsiasi decrittografia e l'applicazione riceverà dati crittografati binari (come matrici di byte).

La tabella seguente riepiloga il comportamento delle query, a seconda che la funzionalità Always Encrypted sia abilitata o meno:

|Caratteristica della query | Always Encrypted è abilitato e l'applicazione può accedere alle chiavi e ai metadati delle chiavi|Always Encrypted è abilitato e l'applicazione non può accedere alle chiavi o ai metadati delle chiavi | Always Encrypted è disabilitato|
|:---|:---|:---|:---|
| Parametri destinati alle colonne crittografate. | I valori dei parametri vengono crittografati in modo trasparente. | Errore | Errore|
| Recupero di dati dalle colonne crittografate, senza parametri destinati alle colonne crittografate.| I risultati delle colonne vengono decrittografati in modo trasparente. L'applicazione riceve i valori di colonna in testo normale. | Errore | I risultati delle colonne crittografate non vengono decrittografate. L'applicazione riceve i valori crittografati come matrici di byte.

Gli esempi seguenti illustrano il recupero e la modifica dei dati nelle colonne crittografate. Gli esempi presuppongono che una tabella con lo schema seguente. Si noti che le colonne SSN e BirthDate nascita sono crittografate.

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
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] )
 GO
```

#### <a name="data-insertion-example"></a>Esempio di inserimento dei dati

Questo esempio illustra come inserire una riga nella tabella Patients. Si noti quanto segue:

- Il codice di esempio non contiene alcun elemento specifico per la crittografia. Il driver rileva automaticamente e crittografa i valori dei parametri SSN e data, che hanno come destinazione le colonne crittografate. In questo modo la crittografia diventa trasparente per l'applicazione.

- I valori inseriti nelle colonne di database, incluse quelle crittografate, vengono passati come parametri associati (vedere [Funzione SQLBindParameter](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx)). Quando si inviano valori a colonne non crittografate, l'uso dei parametri è facoltativo, nonostante sia consigliabile per prevenire attacchi SQL injection. È invece necessario usare i parametri in presenza di valori destinati a colonne crittografate. Se i valori inseriti nelle colonne SSN o BirthDate sono stati passati come valori letterali incorporati nell'istruzione della query, la query avrà esito negativo perché il driver non prova a crittografare o in caso contrario elaborare valori letterali nelle query. Di conseguenza, il server li rifiuterà come incompatibili con le colonne crittografate.

- Il tipo SQL del parametro inserito nella colonna SSN è impostato su SQL_CHAR, che esegue il mapping per il **char** tipo di dati di SQL Server (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`). Se il tipo del parametro è stato impostato su SQL_WCHAR, che esegue il mapping a **nchar**, la query avrà esito negativo, come Always Encrypted non supporta le conversioni sul lato server da valori nchar crittografati a valori char crittografato. Vedere [riferimento per programmatori ODBC: Appendice d: Tipi di dati](https://msdn.microsoft.com/library/ms713607.aspx) per informazioni sui mapping dei tipi di dati.

```
    SQL_DATE_STRUCT date;
    SQLLEN cbdate;   // size of date structure  

    SQLCHAR SSN[12];
    strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

    SQLWCHAR* firstName = L"Catherine";
    SQLWCHAR* lastName = L"Abel";
    SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

    // Initialize the date structure  
    date.day = 10;
    date.month = 9;
    date.year = 1996;

    // Size of structures   
    cbdate = sizeof(SQL_DATE_STRUCT);

    SQLRETURN rc = 0;

    string queryText = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?) ";

    rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

    //SSN
    rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);
    //FirstName
    rc = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)firstName, 0, &cbFirstName);
    //LastName
    rc = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);
    //BirthDate
    rc = SQLBindParameter(hstmt, 4, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 10, 0, (SQLPOINTER)&date, 0, &cbdate);

    rc = SQLExecute(hstmt);
```

#### <a name="plaintext-data-retrieval-example"></a>Esempio di recupero dati in testo normale

L'esempio seguente illustra come filtrare i dati in base ai valori crittografati e recuperare i dati in testo non crittografato dalle colonne crittografate. Si noti quanto segue:

- Il valore usato nella clausola WHERE per filtrare la colonna SSN deve essere passato usando SQLBindParameter, in modo che il driver possa crittografarlo in modo trasparente prima dell'invio al server.

- Tutti i valori stampati dal programma saranno in testo non crittografato, perché il driver decrittografa in modo trasparente i dati recuperati dalle colonne SSN e BirthDate.

> [!NOTE]
> Le query possono eseguire confronti di uguaglianza nelle colonne crittografate solo se la crittografia è deterministica. Per altre informazioni, vedere [Selezione della crittografia deterministica o casuale](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[SSN] = ? ";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//SSN
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="ciphertext-data-retrieval-example"></a>Esempio di recupero dei dati del testo crittografato

Se Always Encrypted non è abilitato, una query può comunque recuperare dati dalle colonne crittografate, a condizione che non presenti parametri destinati alle colonne crittografate.

L'esempio seguente illustra come recuperare dati crittografati binari da colonne crittografate. Si noti quanto segue:

- Considerato che Always Encrypted non è abilitato nella stringa di connessione, la query restituirà i valori crittografati di SSN e BirthDate come matrici di byte (il programma converte i valori in stringhe).
- Una query che recupera dati dalle colonne crittografate con Always Encrypted disabilitato può avere parametri, a condizione che nessuno dei parametri sia destinato a una colonna crittografata. La query precedente filtra in base alla colonna LastName, non è crittografata nel database. Se la query avesse filtrato per SSN o data di nascita, avrebbe avuto esito negativo.


```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[LastName] = ?";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//LastName
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Come evitare i problemi comuni quando si eseguono query su colonne crittografate

Questa sezione descrive categorie di errori comuni che si verificano quando si eseguono query su colonne crittografate da applicazioni ODBC e contiene alcune linee guida su come correggere tali errori.

##### <a name="unsupported-data-type-conversion-errors"></a>Errori di conversione dei tipi di dati non supportati

Always Encrypted supporta alcune conversioni per i tipi di dati crittografati. Per l'elenco dettagliato delle conversioni dei tipi supportati, vedere [Always Encrypted (motore di database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Per evitare errori di conversione tipo di dati, assicurarsi di osservare quanto riportato di seguito quando si usa la funzione SQLBindParameter con parametri destinati alle colonne crittografate:

- Il tipo SQL del parametro è sia esattamente uguale al tipo della colonna di destinazione o la conversione dal tipo SQL al tipo della colonna è supportata.

- La precisione e la scala dei parametri destinati alle colonne dei tipi di dati `decimal` e `numeric` di SQL Server sono uguali a quelle configurate per la colonna di destinazione.

- La precisione dei parametri destinati alle colonne dei tipi di dati `datetime2`, `datetimeoffset` e `time` di SQL Server non è maggiore della precisione per la colonna di destinazione nelle query che modificano la colonna di destinazione.  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Errori causati dal passaggio di testo non crittografato anziché di valori crittografati

Qualsiasi valore destinato a una colonna crittografata deve essere crittografati prima dell'invio al server. Il tentativo di inserire, modificare o filtrare in base a un valore di testo non crittografato in una colonna crittografata genererà un errore. Per evitare tali errori, verificare che:

- Always Encrypted è abilitato (nel DSN, la stringa di connessione, prima ci si connette, impostando il `SQL_COPT_SS_COLUMN_ENCRYPTION` attributo di connessione per una connessione specifica, o il `SQL_SOPT_SS_COLUMN_ENCRYPTION` attributo di istruzione per una specifica istruzione).

- Sia usato SQLBindParameter per inviare i dati destinati alle colonne crittografate. L'esempio seguente illustra una query che filtra in modo errato in base a un valore letterale o costante in una colonna crittografata (SSN), anziché passare il valore letterale come argomento a SQLBindParameter.

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>Precauzioni quando si usano SQLSetPos e SQLMoreResults

#### <a name="sqlsetpos"></a>SQLSetPos

Il `SQLSetPos` API consente a un'applicazione aggiornare righe nel buffer che sono stati associati con SQLBindCol e in quale riga è stata precedentemente recuperati dati usando un set di risultati. A causa del comportamento di riempimento asimmetrica dei tipi a lunghezza fissa crittografati, è possibile modificare in modo imprevisto i dati di tali colonne durante l'esecuzione di aggiornamenti su altre colonne nella riga. Con Always Encrypted, verranno inseriti i valori di carattere di lunghezza fissa se il valore è inferiore alla dimensione del buffer.

Per attenuare questo problema, usare il `SQL_COLUMN_IGNORE` flag per ignorare le colonne che non verranno aggiornate come parte del `SQLBulkOperations` e quando si usa `SQLSetPos` cursori in base gli aggiornamenti.  Tutte le colonne che non vengono modificate direttamente dall'applicazione devono essere ignorate, sia per le prestazioni e per evitare il troncamento delle colonne che sono associati a un buffer *inferiori* alle loro dimensioni effettive (DB). Per altre informazioni, vedere [riferimento alle funzioni SQLSetPos](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx).

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults & SQLDescribeCol

Possono chiamare programmi applicativi [SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx) per restituire i metadati sulle colonne nelle istruzioni preparate.  Se Always Encrypted è abilitato, la chiamata `SQLMoreResults` *prima* chiamata `SQLDescribeCol` provoca [sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) per essere chiamato, che non correttamente restituisce il testo non crittografato metadati per le colonne crittografate. Per evitare questo problema, chiamare `SQLDescribeCol` nelle istruzioni preparate *prima* chiamata `SQLMoreResults`.

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controllo dell'impatto di Always Encrypted sulle prestazioni

Considerato che Always Encrypted è una tecnologia di crittografia lato client, la maggior parte del sovraccarico delle prestazioni si verifica sul lato client, non nel database. A parte il costo delle operazioni di crittografia e decrittografia, le altre origini di sovraccarico delle prestazioni sul lato client sono le seguenti:

- Round trip aggiuntivi al database per recuperare i metadati per i parametri di query.

- Chiamate a un archivio delle chiavi master delle colonne per accedere alla chiave master di una colonna.

Questa sezione descrive le ottimizzazioni delle prestazioni predefinite in ODBC Driver for SQL Server e come controllare l'impatto sulle prestazioni esercitato dai due fattori descritti.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controllo dei round trip per recuperare i metadati per i parametri di query

Se la funzionalità Always Encrypted è abilitata per una connessione, per impostazione predefinita il driver chiamerà [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) per ogni query con parametri, passando l'istruzione di query (senza i valori dei parametri) a SQL Server. Questa stored procedure analizza l'istruzione di query per scoprire se i parametri devono essere crittografati e, in caso affermativo, restituisce le informazioni relative alla crittografia per ogni parametro consentire al driver di crittografarli. Il comportamento descritto garantisce all'applicazione client un elevato livello di trasparenza: non è necessario che l'applicazione (e lo sviluppatore dell'applicazione) sappiano quali query accedono alle colonne crittografate, a condizione che i valori destinati alle colonne crittografate vengano passati al driver nei parametri.

### <a name="per-statement-always-encrypted-behavior"></a>Per ogni istruzione Always Encrypted comportamento

Per controllare l'impatto sulle prestazioni di recupero dei metadati di crittografia per le query con parametri, è possibile modificare il comportamento di Always Encrypted per le singole query, se è stata abilitata per la connessione. In questo modo, è possibile assicurarsi che `sys.sp_describe_parameter_encryption` venga richiamato solo per le query con parametri destinati alle colonne crittografate. Si noti, tuttavia, che in tal modo si riduce la trasparenza della crittografia. Se si esegue la crittografia di colonne aggiuntive nel database, potrebbe essere necessario modificare il codice dell'applicazione per allinearlo alle modifiche dello schema.

Per controllare il comportamento di Always Encrypted di un'istruzione, chiamare SQLSetStmtAttr per impostare il `SQL_SOPT_SS_COLUMN_ENCRYPTION` attributo di istruzione a uno dei valori seguenti:

|valore|Descrizione|
|-|-|
|`SQL_CE_DISABLED` (0)|Always Encrypted è disabilitato per l'istruzione|
|`SQL_CE_RESULTSETONLY` (1)|Solo decrittografia. Set di risultati e i valori restituiti vengono decrittografati e i parametri non sono crittografati|
|`SQL_CE_ENABLED` (3) | Always Encrypted è abilitato e usato per entrambi i parametri e i risultati|

Nuovo handle di istruzione creati da una connessione con Always Encrypted abilitata per impostazione predefinita a SQL_CE_ENABLED. Quelli creati da una connessione è disabilitata per impostazione predefinita a SQL_CE_DISABLED (e non è possibile abilitare Always Encrypted su di essi.)

Se la maggior parte delle query di un'applicazione client di accedere alle colonne crittografate, si consiglia quanto segue:

- Impostare la parola chiave della stringa di connessione `ColumnEncryption` su `Enabled`.

- Impostare il `SQL_SOPT_SS_COLUMN_ENCRYPTION` dell'attributo `SQL_CE_DISABLED` sulle istruzioni che non accedono alle colonne crittografate. Verrà disabilitato entrambi chiamata `sys.sp_describe_parameter_encryption` , nonché i tentativi di decrittografare tutti i valori nel risultato impostato.
    
- Impostare il `SQL_SOPT_SS_COLUMN_ENCRYPTION` dell'attributo `SQL_CE_RESULTSETONLY` sulle istruzioni che non dispongono di parametri che richiedono la crittografia, ma che recuperano dati dalle colonne crittografate. Questo modo verranno disabilitati la chiamata `sys.sp_describe_parameter_encryption` e crittografia dei parametri. I risultati contenenti colonne crittografate continueranno a essere decrittografati.

## <a name="always-encrypted-security-settings"></a>Crittografia sempre attiva le impostazioni di sicurezza

### <a name="force-column-encryption"></a>Crittografia di colonna

Per applicare la crittografia di un parametro, impostare il `SQL_CA_SS_FORCE_ENCRYPT` campo di descrizione del parametro di implementazione (IPD) tramite una chiamata alla funzione SQLSetDescField. Un valore diverso da zero, il driver restituire un errore quando i metadati di crittografia non viene restituito per il parametro associato.

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

Se SQL Server indica al driver che il parametro non deve essere crittografato, le query che usano il parametro avranno esito negativo. Si aumenta così la protezione contro attacchi alla sicurezza, come un'istanza di SQL Server compromessa che invia metadati di crittografia non corretti al client, con il conseguente possibile rischio di divulgazione dei dati.

### <a name="column-encryption-key-caching"></a>Memorizzazione nella cache delle chiavi di crittografia della colonna

Per ridurre il numero di chiamate a un archivio chiavi master della colonna per decrittografare le chiavi di crittografia di colonna, il driver memorizza nella cache il testo non crittografato dei Cek in memoria. La cache CEK è globale per il driver e non sono associati a qualsiasi un'unica connessione. Dopo aver ricevuto la chiave ECEK dai metadati del database, il driver tenta innanzitutto di trovare CEK crittografato corrispondente al valore della chiave crittografato nella cache. Il driver chiama l'archivio chiavi contenente la chiave CMK solo se non riesce a trovare il testo non crittografato corrispondente CEK nella cache.

> [!NOTE]
> In ODBC Driver for SQL Server, non vengono rimosse le voci nella cache dopo un timeout di due ore. Ciò significa che per una determinata chiave ECEK, il driver contatta l'archivio chiavi una sola volta durante il ciclo di vita dell'applicazione o ogni due ore, a seconda del valore è minore.

A partire da 17.1 il Driver ODBC per SQL Server, il timeout della cache CEK può essere regolato usando il `SQL_COPT_SS_CEKCACHETTL` attributo di connessione, che specifica il numero di secondi una CEK rimarrà nella cache. A causa della natura globale della cache, questo attributo può essere modificato da un handle di connessione valido per il driver. Quando la cache risulta ridotto durata (TTL) dei Cek esistente che potrebbe superare la durata TTL del nuovo inoltre vengono eliminati. Se è 0, non vengono memorizzati nella cache Cek.

### <a name="trusted-key-paths"></a>Percorsi di chiave attendibili

A partire 17.1 il Driver ODBC per SQL Server, il `SQL_COPT_SS_TRUSTEDCMKPATHS` attributo di connessione consente a un'applicazione in modo da richiedere che le operazioni di crittografia sempre attiva usano solo un elenco specificato di CMK, identificato da loro i percorsi delle chiavi. Per impostazione predefinita, questo attributo è NULL, che indica che il driver accetta qualsiasi percorso della chiave. Per usare questa funzionalità, impostare `SQL_COPT_SS_TRUSTEDCMKPATHS` in modo che punti a una stringa di caratteri "wide" delimitato da null, con terminazione null che elenca i percorsi di chiave consentiti. La memoria a cui fa riferimento questo attributo deve rimanere valida durante le operazioni di crittografia o decrittografia utilizzando l'handle di connessione in cui è impostato---su cui il driver viene verificato se il percorso CMK come specificato dai metadati del server senza in questo elenco. Se il percorso CMK non è presente nell'elenco, l'operazione ha esito negativo. L'applicazione può modificare il contenuto della memoria che punta questo attributo, per modificare l'elenco di CMK attendibili, senza impostare l'attributo nuovamente.

## <a name="working-with-column-master-key-stores"></a>Uso degli archivi delle chiavi master delle colonne

Per crittografare o decrittografare i dati, il driver deve ottenere una CEK configurato per la colonna di destinazione. Cek vengono archiviati in formato crittografato (ECEKs) nei metadati del database. Ogni chiave CEK dispone di una CMK corrispondente che è stata usata per crittografarlo. Il [metadati del database](../../t-sql/statements/create-column-master-key-transact-sql.md) non archivia la chiave CMK stesso; contiene solo il nome dell'archivio chiavi e le informazioni che l'archivio chiavi è possibile usare per individuare la chiave CMK.

Per ottenere il valore di testo normale di una chiave ECEK, il driver Ottiene prima di tutto i metadati relativi sia la CEK e le chiavi master di colonna corrispondente e quindi Usa queste informazioni per contattare l'archivio chiavi contenente la chiave CMK e lo richiede, per decrittografare la chiave ECEK. Il driver comunica con un archivio chiavi usando un provider dell'archivio chiavi.

### <a name="built-in-keystore-providers"></a>Provider dell'archivio chiavi predefinite

Il Driver ODBC per SQL Server viene fornito con i provider dell'archivio chiavi predefinite seguenti:

| nome | Descrizione | Nome del provider (metadati) |Disponibilità|
|:---|:---|:---|:---|
|Insieme di credenziali chiave di Azure |Gli archivi CMK in Azure Key Vault | `AZURE_KEY_VAULT` |Windows, macOS, Linux|
|Archivio certificati Windows|Archivia CMK in locale nell'archivio chiavi Windows| `MSSQL_CERTIFICATE_STORE`|Windows|

- È necessario che l'utente (o l'amministratore del database) verifichi che il nome del provider, configurato nei metadati della chiave master della colonna, sia corretto e che il percorso della chiave master sia conforme al formato del percorso della chiave per il provider specificato. È consigliabile configurare le chiavi usando strumenti come SQL Server Management Studio, che genera automaticamente i nomi di provider e i percorsi di chiave validi quando viene eseguita l'istruzione [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md) .

- È necessario verificare che l'applicazione possa accedere alla chiave nell'archivio chiavi. Questa operazione comportare l'accesso da parte dell'applicazione alla chiave e/o all'archivio chiavi, a seconda dell'archivio, o l'esecuzione di altri passaggi di configurazione specifici dell'archivio chiavi. Ad esempio, per accedere a un'istanza di Azure Key Vault, è necessario fornire le credenziali corrette dell'archivio chiavi.

### <a name="using-the-azure-key-vault-provider"></a>Uso di Azure Key Vault Provider

L'insieme di credenziali delle chiavi di Azure rappresenta una scelta valida per archiviare e gestire le chiavi master delle colonne per Always Encrypted, soprattutto se le applicazioni sono ospitate in Azure. Il Driver ODBC per SQL Server in Windows, macOS e Linux include un provider di archivio chiavi master di colonna predefiniti per Azure Key Vault. Visualizzare [Azure Key Vault - passo a passo](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/), [Introduzione a Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/), e [la creazione di chiavi Master della colonna in Azure Key Vault](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2) per altre informazioni sulla configurazione di una chiave di Azure Insieme di credenziali per Always Encrypted.

> [!NOTE]
> In Linux e macOS, per la versione del driver 17.2 e versioni successive, `libcurl` è necessaria per usare questo provider, ma non è una dipendenza esplicita poiché altre operazioni con il driver non sono necessario. Se si verifica un errore relative a `libcurl`, assicurarsi sia installato.

Il driver supporta l'autenticazione ad Azure Key Vault usando i seguenti tipi di credenziali:

- Nome utente/Password - con questo metodo, le credenziali sono il nome di un utente di Azure Active Directory e la relativa password.

- Client - ID/segreto con questo metodo, le credenziali sono un ID client applicazione e un segreto dell'applicazione.

Per consentire al driver di utilizzare CMK archiviati in Azure Key Vault per la crittografia di colonna, usare la parola chiave solo nella stringa di connessione seguente:

|Tipo di credenziali| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|Nome utente/password| `KeyVaultPassword`|Nome entità utente|Password|
|ID o il segreto client| `KeyVaultClientSecret`|ID client|Segreto|

#### <a name="example-connection-strings"></a>Esempi di stringhe di connessione

Le stringhe di connessione seguenti illustrano come eseguire l'autenticazione ad Azure Key Vault con i due tipi di credenziali:

**ID client/segreto**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**Nome utente/Password**

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

Non altre ODBC dell'applicazione sono necessarie modifiche per usare Azure Key Vault per archiviazione di chiavi master di colonna.

### <a name="using-the-windows-certificate-store-provider"></a>Uso del provider per l'archivio certificati Windows

Il Driver ODBC per SQL Server in Windows include un provider di archivio chiavi master di colonna predefiniti per Store il certificato di Windows, denominato `MSSQL_CERTIFICATE_STORE`. (Questo provider non disponibile in macOS o Linux). A questo provider, la chiave CMK è archiviata localmente nel computer client e alcuna configurazione aggiuntiva per l'applicazione non è necessario usarlo con il driver. Tuttavia, l'applicazione deve avere accesso al certificato e la relativa chiave privata nell'archivio. Per altre informazioni, vedere [Creare e archiviare chiavi master della colonna (Always Encrypted)](https://docs.microsoft.com/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted).

### <a name="using-custom-keystore-providers"></a>Uso di provider di archivi chiavi personalizzati

Il Driver ODBC per SQL Server supporta anche i provider di archivio chiavi personalizzati di terze parti tramite l'interfaccia CEKeystoreProvider. In questo modo un'applicazione di caricare, query e configurare i provider dell'archivio chiavi in modo che possono essere utilizzati dal driver per accedere alle colonne crittografate. Le applicazioni possono interagire direttamente con un provider dell'archivio chiavi per crittografare Cek per l'archiviazione in SQL Server ed eseguire attività oltre che accedono a colonne crittografate con ODBC; per altre informazioni, vedere [provider di archivio chiavi personalizzati](../../connect/odbc/custom-keystore-providers.md).

Due attributi di connessione vengono utilizzati per interagire con i provider dell'archivio chiavi personalizzato. ovvero:

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

Nel primo caso viene usato per caricare ed enumerare i provider dell'archivio chiavi caricato, mentre quest'ultimo consente le comunicazioni di provider dell'applicazione. Questi attributi di connessione possono essere utilizzati in qualsiasi momento, prima o dopo aver stabilito una connessione, poiché l'interazione di provider dell'applicazione non comporta la comunicazione con SQL Server. Tuttavia, poiché il driver non è ancora stato caricato, impostazione e recupero di questi attributi prima della connessione determinerà che vengano elaborati da Gestione Driver e potrebbe non produrre i risultati previsti.

#### <a name="loading-a-keystore-provider"></a>Il caricamento di un Provider dell'archivio chiavi

L'impostazione di `SQL_COPT_SS_CEKEYSTOREPROVIDER` attributo di connessione consente a un'applicazione client caricare una libreria del provider, rendendo disponibili per l'uso dei provider dell'archivio chiavi contenuti al suo interno.

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| Argomento | Descrizione |
|:---|:---|
|`ConnectionHandle`|[Input] Handle di connessione. Deve essere un handle di connessione valida, ma i provider caricati tramite handle di una connessione sono accessibili da qualsiasi altro nello stesso processo.|
|`Attribute`|[Input] Attributo da impostare: il `SQL_COPT_SS_CEKEYSTOREPROVIDER` costante.|
|`ValuePtr`|[Input] Puntatore a una stringa di caratteri con terminazione null che specifica il nome del file della libreria del provider. Per SQLSetConnectAttrA, si tratta di una stringa (multibyte) ANSI. Per SQLSetConnectAttrW, questa è una stringa Unicode (wchar_t).|
|`StringLength`|[Input] La lunghezza della stringa ValuePtr, o SQL_NTS.|

Il driver tenta di caricare la libreria identificata dal parametro ValuePtr usando la libreria dinamica definite dalla piattaforma meccanismo di caricamento (`dlopen()` in Linux e macOS, `LoadLibrary()` su Windows), e aggiunge tutti i provider definiti al suo interno all'elenco di provider noto al driver. È possibile che si verifichino gli errori seguenti:

| Errore | Descrizione |
|:--|:--|
|`CE203`|Non è stato possibile caricare la libreria dinamica.|
|`CE203`|Il simbolo "CEKeyStoreProvider" esportato non è stato trovato nella libreria.|
|`CE203`|Uno o più provider nella raccolta sono già caricati.|

`SQLSetConnectAttr` Restituisce l'errore normale o valori di esito positivo e informazioni aggiuntive sono disponibili per individuare eventuali errori che si sono verificati tramite il meccanismo di diagnostica ODBC standard.

> [!NOTE]
> Il programmatore di applicazioni è necessario assicurarsi che tutti i provider personalizzati vengono caricati prima dell'invio tramite qualsiasi connessione qualsiasi query che li richiedono. In caso contrario, viene generato l'errore seguente:

| Errore | Descrizione |
|:--|:--|
|`CE200`|Provider dell'archivio chiavi %1 non trovato. Assicurarsi che la libreria del provider dell'archivio chiavi appropriata è stata caricata.|

> [!NOTE]
> Implementatori dei provider dell'archivio chiavi deve evitare di usare `MSSQL` nel nome propri provider personalizzati. Questo termine è riservato esclusivamente per l'uso di Microsoft e può causare conflitti con i provider predefiniti future. Utilizzo di questo termine il nome di un provider personalizzato può comportare un avviso di ODBC.

#### <a name="getting-the-list-of-loaded-providers"></a>Recupero dell'elenco dei provider caricato

Recupero di questo attributo di connessione consente a un'applicazione client determinare i provider dell'archivio chiavi attualmente caricati nel driver (incluse quelle compilate). Questa operazione può essere eseguita solo dopo la connessione.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| Argomento | Descrizione |
|:---|:---|
|`ConnectionHandle`|[Input] Handle di connessione. Deve essere un handle di connessione valida, ma i provider caricati tramite handle di una connessione sono accessibili da qualsiasi altro nello stesso processo.|
|`Attribute`|[Input] Attributo da recuperare: il `SQL_COPT_SS_CEKEYSTOREPROVIDER` costante.|
|`ValuePtr`|[Output] Puntatore alla memoria in cui si desidera restituire il successivo nome provider caricato.|
|`BufferLength`|[Input] La lunghezza del buffer ValuePtr.|
|`StringLengthPtr`|[Output] Un puntatore a un buffer in cui restituire il numero totale di byte (escluso il carattere di terminazione null) disponibile da restituire in \*ValuePtr. Se ValuePtr è un puntatore null, non viene restituita alcuna lunghezza. Se il valore dell'attributo è una stringa di caratteri e il numero di byte disponibili da restituire è maggiore di BufferLength meno la lunghezza della terminazione null di caratteri, i dati in \*ValuePtr viene troncato a BufferLength meno la lunghezza del carattere di terminazione null ed è con terminazione null dal driver.|

Per consentire il recupero dell'intero elenco, ogni operazione Get restituisce il nome del provider corrente e incrementa un contatore interno a quello successivo. Quando questo contatore raggiunge la fine dell'elenco, una stringa vuota ("") viene restituito, e il contatore viene reimpostato; operazioni Get successive quindi proseguono nuovamente dall'inizio dell'elenco.

### <a name="communicating-with-keystore-providers"></a>Comunicazione con i provider dell'archivio chiavi

Il `SQL_COPT_SS_CEKEYSTOREDATA` attributo di connessione consente a un'applicazione client comunicare con i provider dell'archivio chiavi caricato per la configurazione di parametri aggiuntivi, trasparenza, materiale e così via. La comunicazione tra un'applicazione client e un provider segue un protocollo di richiesta-risposta semplice, basato su Get e Set di richieste che utilizzano questo attributo di connessione. La comunicazione viene avviata solo dall'applicazione client.

> [!NOTE]
> A causa della natura di ODBC chiama (SQLGet/SetConnectAttr) possa rispondere del CEKeyStoreProvider impostazione dei dati con la risoluzione del contesto di connessione ODBC interface solo supporta.

L'applicazione comunica con i provider dell'archivio chiavi tramite il driver tramite la struttura CEKeystoreData:

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```
| Argomento | Descrizione |
|:---|:---|
|`name`|[Input] Al momento di Set, il nome del provider per cui i dati vengono inviati. Ignorato su Get. Stringa con terminazione null, i caratteri "wide".|
|`dataSize`|[Input] Le dimensioni della matrice di dati seguendo la struttura.|
|`data`|[InOut] Al Set di dati da inviare al provider. Può trattarsi di dati arbitrari. il driver esegue alcun tentativo di interpretarlo. Dopo Get, il buffer per ricevere i dati letti dal provider.|

#### <a name="writing-data-to-a-provider"></a>La scrittura di un provider di dati

Oggetto `SQLSetConnectAttr` chiamare usando il `SQL_COPT_SS_CEKEYSTOREDATA` attributo scrive un "pacchetto" di dati per il provider dell'archivio chiavi specificato.
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| Argomento | Descrizione |
|:---|:---|
|`ConnectionHandle`| [Input] Handle di connessione. Deve essere un handle di connessione valida, ma i provider caricati tramite handle di una connessione sono accessibili da qualsiasi altro nello stesso processo.|
|`Attribute`|[Input] Attributo da impostare: il `SQL_COPT_SS_CEKEYSTOREDATA` costante.|
|`ValuePtr`|[Input] Puntatore a una struttura CEKeystoreData. Il campo del nome della struttura identifica il provider a cui è destinato il tipo di dati.|
|`StringLength`|[Input] Costante SQL_IS_POINTER|

Altre informazioni dettagliate sull'errore possono essere ottenute tramite [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

> [!NOTE]
> Il provider può utilizzare l'handle di connessione per associare i dati scritti da una connessione specifica, se lo desidera. Ciò è utile per l'implementazione di configurazione per ogni connessione. Anche possibile ignorare il contesto di connessione e trattare i dati in modo identico, indipendentemente dalla connessione utilizzata per inviare i dati. Visualizzare [contesto di associazione](../../connect/odbc/custom-keystore-providers.md#context-association) per altre informazioni.

#### <a name="reading-data-from-a-provider"></a>La lettura dei dati da un provider

Una chiamata a `SQLGetConnectAttr` usando il `SQL_COPT_SS_CEKEYSTOREDATA` attributo legge un "pacchetto" di dati dal *l'ultimo scritto-a-* provider. Se non CE n'erano, si verifica un errore nella sequenza della funzione. I responsabili dell'implementazione del provider dell'archivio chiavi sono invitati ad aiutarsi "fittizio" scritture di byte 0 come modo di selezione del provider per operazioni di lettura senza causare effetti collaterali, se ha senso eseguire questa operazione.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| Argomento | Descrizione |
|:---|:---|
|`ConnectionHandle`|[Input] Handle di connessione. Deve essere un handle di connessione valida, ma i provider caricati tramite handle di una connessione sono accessibili da qualsiasi altro nello stesso processo.|
|`Attribute`|[Input] Attributo da recuperare: il `SQL_COPT_SS_CEKEYSTOREDATA` costante.|
|`ValuePtr`|[Output] Un puntatore a una struttura CEKeystoreData in cui vengono inseriti i dati letti dal provider.|
|`BufferLength`|[Input] Costante SQL_IS_POINTER|
|`StringLengthPtr`|[Output] Un puntatore a un buffer in cui si desidera restituire BufferLength. Se * ValuePtr non è un puntatore null, viene restituita alcuna lunghezza.|

Il chiamante deve garantire che un buffer di lunghezza sufficiente seguire la struttura CEKEYSTOREDATA viene allocato per il provider da scrivere in. Al momento della restituzione, il relativo campo dataSize viene aggiornato con la lunghezza effettiva dei dati letti dal provider. Altre informazioni dettagliate sull'errore possono essere ottenute tramite [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

Questa interfaccia non inserisce alcun requisito aggiuntivo sul formato dei dati trasferiti tra un'applicazione e un provider dell'archivio chiavi. Ogni provider è possibile definire il proprio formato di protocollo/dati, a seconda delle esigenze.

Per un esempio di implementazione di un proprio provider di archivio chiavi, vedere [provider dell'archivio chiavi personalizzati](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>Limitazioni del driver ODBC quando si usa Always Encrypted

### <a name="asynchronous-operations"></a>Operazioni asincrone
Mentre il driver ODBC consentirà l'utilizzo di [operazioni asincrone](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md) con Always Encrypted, è una riduzione delle prestazioni sulle operazioni quando è abilitato per Always Encrypted. La chiamata a `sys.sp_describe_parameter_encryption` per determinare i metadati di crittografia per l'istruzione blocca e causerà il driver di attesa per il server restituire i metadati prima di restituire `SQL_STILL_EXECUTING`.

### <a name="retrieve-data-in-parts-with-sqlgetdata"></a>Recuperare i dati in parti con SQLGetData
Prima di ODBC Driver 17 for SQL Server non era possibile recuperare i caratteri crittografati e le colonne di dati binari in parti con SQLGetData. Ora è possibile eseguire una sola chiamata a SQLGetData, con un buffer di lunghezza sufficiente per contenere i dati dell'intera colonna.

### <a name="send-data-in-parts-with-sqlputdata"></a>Inviare i dati in parti con SQLPutData
Con SQLPutData non è possibile inviare i dati a scopo di inserimento o confronto. È possibile eseguire una sola chiamata a SQLPutData, con un buffer che contiene tutti i dati. Per l'inserimento di dati Long in colonne crittografate, usare l'API della copia bulk, descritta nella sezione successiva, con un file di dati di input.

### <a name="encrypted-money-and-smallmoney"></a>Smallmoney e money crittografati
I parametri non possono destinare le colonne crittografate **money** o **smallmoney**, in quanto non esiste un tipo di dati ODBC specifico che esegue il mapping a questi tipi. Si generano così errori di conflitto del tipo di operando.

## <a name="bulk-copy-of-encrypted-columns"></a>Copia bulk di colonne crittografate

A partire da ODBC Driver 17 for SQL Server, è possibile usare le [funzioni di copia bulk di SQL](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md) e l'utilità **bcp** supportata con Always Encrypted. Sia il testo non crittografato (crittografato in inserimento e decrittografato in recupero) sia il testo crittografato (verbatim trasferito) possono essere inseriti e recuperati usando le API di copia bulk (bcp_&#42;) e l'utilità **bcp**.

- Per recuperare il testo crittografato nel formato varbinary(max) (ad esempio per il caricamento bulk in un database diverso), connettersi senza l'opzione `ColumnEncryption`, oppure impostarla su `Disabled`, ed eseguire l'operazione BCP OUT.

- Per inserire e recuperare testo non crittografato e consentire al driver di eseguire la crittografia e la decrittografia in modo trasparente, impostare semplicemente `ColumnEncryption` su `Enabled`. In caso contrario, la funzionalità dell'API BCP rimane invariata.

- Per inserire testo crittografato nel formato varbinary (max) (ad esempio il testo recuperato descritto in precedenza), impostare l'opzione `BCPMODIFYENCRYPTED` su TRUE ed eseguire l'operazione BCP IN. Affinché i dati risultanti possano essere decrittografati, verificare che il valore CEK della colonna di destinazione sia lo stesso dal quale è stato originariamente ottenuto il testo crittografato.

Quando si usa la **bcp** utilità: Per controllare il `ColumnEncryption` impostazione, utilizzare l'opzione -D e specificare un DSN che contiene il valore desiderato. Per inserire testo crittografato, verificare che il `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` dell'utente è attivata.

Nella tabella seguente fornisce un riepilogo delle azioni quando si opera su una colonna crittografata:

|`ColumnEncryption`|Direzione BCP|Descrizione|
|----------------|-------------|-----------|
|`Disabled`|OUT (al client)|Recupera testo crittografato. Il tipo di dati osservati **varbinary (max)**.|
|`Enabled`|OUT (al client)|Recupera in testo normale. Il driver decrittograferà i dati della colonna.|
|`Disabled`|IN (per server)|Inserisce testo crittografato. Questo è destinato in modo non trasparente lo spostamento dei dati crittografati senza richiedere deve essere decrittografato. L'operazione avrà esito negativo se il `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` opzione non è impostata sull'utente o BCPMODIFYENCRYPTED non è impostata sull'handle di connessione. Per altre informazioni, vedere più avanti.|
|`Enabled`|IN (per server)|Inserisce testo normale. Il driver crittograferà i dati della colonna.|

### <a name="the-bcpmodifyencrypted-option"></a>L'opzione BCPMODIFYENCRYPTED

Per evitare il danneggiamento dei dati, il server in genere non consente l'inserimento di testo crittografato direttamente in una colonna crittografata e quindi tenta di eseguire questa operazione avrà esito negativo; Tuttavia, per il caricamento bulk dei dati crittografati usando l'API BCP, l'impostazione il `BCPMODIFYENCRYPTED` [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) opzione su TRUE consentirà testo crittografato da inserire direttamente e riduce il rischio di danneggiare i dati crittografati tramite impostazione di `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` opzione sull'account utente. Ciononostante, le chiavi devono corrispondere ai dati ed è consigliabile eseguire alcuni controlli di sola lettura dei dati inseriti dopo l'inserimento bulk e prima di poterlo usare.

Per altre informazioni, vedere [Migrare dati sensibili protetti da Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).

## <a name="always-encrypted-api-summary"></a>Riepilogo delle API Always Encrypted

### <a name="connection-string-keywords"></a>Parole chiave per le stringhe di connessione

|nome|Descrizione|  
|----------|-----------------|  
|`ColumnEncryption`|Valori accettati sono `Enabled` / `Disabled`.<br>`Enabled`: abilita o disabilita la funzionalità Always Encrypted per la connessione.<br>`Disabled`: disabilita la funzionalità Always Encrypted per la connessione. <br><br>Il valore predefinito è `Disabled`.|  
|`KeyStoreAuthentication` | Valori validi: `KeyVaultPassword`, `KeyVaultClientSecret` |
|`KeyStorePrincipalId` | Quando `KeyStoreAuthentication`  =  `KeyVaultPassword`, impostare questo valore su un nome di entità utente di Active Directory valido di Azure. <br>Quando `KeyStoreAuthetication`  =  `KeyVaultClientSecret` impostare questo valore su una Azure Active Directory Application ID Client valido |
|`KeyStoreSecret` | Quando `KeyStoreAuthentication`  =  `KeyVaultPassword` impostare questo valore per la password per il nome utente corrispondente. <br>Quando `KeyStoreAuthentication`  =  `KeyVaultClientSecret` impostare questo valore per il segreto dell'applicazione associata a una Azure Active Directory Application ID Client valido|

### <a name="connection-attributes"></a>Attributi di connessione

|nome|Tipo|Descrizione|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|Pre-connessione|`SQL_COLUMN_ENCRYPTION_DISABLE` (0): disabilitare Always Encrypted <br>`SQL_COLUMN_ENCRYPTION_ENABLE` (1)-- Abilita Always Encrypted|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|Post-connessione|[Impostare] Tentativo di caricamento CEKeystoreProvider<br>[Introduzione] Restituire un nome CEKeystoreProvider|
|`SQL_COPT_SS_CEKEYSTOREDATA`|Post-connessione|[Impostare] Scrivere dati CEKeystoreProvider<br>[Introduzione] Leggere i dati da CEKeystoreProvider|
|`SQL_COPT_SS_CEKCACHETTL`|Post-connessione|[Impostare] Impostare la cache CEK durata (TTL)<br>[Introduzione] Ottenere la durata (TTL) di cache CEK corrente|
|`SQL_COPT_SS_TRUSTEDCMKPATHS`|Post-connessione|[Impostare] Impostare il puntatore di percorsi CMK attendibile<br>[Introduzione] Ottenere il puntatore di percorsi CMK attendibile corrente|

### <a name="statement-attributes"></a>Attributi di istruzione

|nome|Descrizione|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED` (0), always Encrypted è disabilitato per l'istruzione <br>`SQL_CE_RESULTSETONLY` (1): solo la decrittografia. Set di risultati e i valori restituiti vengono decrittografati e i parametri non sono crittografati <br>`SQL_CE_ENABLED` (3), always Encrypted è abilitato e usato per entrambi i parametri e i risultati|

### <a name="descriptor-fields"></a>Campi del descrittore

|Campo IPD|Dimensioni/tipo|Valore predefinito|Descrizione|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD (2 byte)|0|Se 0 (impostazione predefinita): decisione per crittografare questo parametro viene determinato in base alla disponibilità dei metadati di crittografia.<br><br>Quando è diverso da zero: se i metadati di crittografia sono disponibili per questo parametro, viene crittografato. In caso contrario, la richiesta ha esito negativo con errore [CE300] crittografia obbligatoria [Microsoft] [ODBC Driver 13 for SQL Server] è stata specificata per un parametro ma i metadati di crittografia non è stato fornito dal server.|

### <a name="bcpcontrol-options"></a>bcp_control opzioni

|Nome opzione|Valore predefinito|Descrizione|
|-|-|-|
|`BCPMODIFYENCRYPTED` (21)|FALSE|Se è TRUE, consente valori varbinary (max) deve essere inserito in una colonna crittografata. Se è FALSE, impedisce l'inserimento a meno che non corretto dei metadati di tipo e la crittografia viene fornito.|

## <a name="see-also"></a>Vedere anche

- [Always Encrypted (motore di database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Blog sulla Crittografia sempre attiva](https://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

