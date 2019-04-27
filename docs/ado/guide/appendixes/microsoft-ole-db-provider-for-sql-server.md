---
title: Provider Microsoft OLE DB per SQL Server | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for SQL Server
- OLE DB provider for SQL Server [ADO]
- SQLOLEDB [ADO]
ms.assetid: 99bc40c4-9181-4ca1-a06f-9a1a914a0b7b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8b5759c0ede8ea6579da11563849df191ad84b1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678669"
---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>Provider Microsoft OLE DB per la panoramica di SQL Server
Il Provider Microsoft OLE DB per SQL Server, SQLOLEDB, consente di ADO per accedere a Microsoft SQL Server.

**NOTA:**  Non è consigliabile usare il driver per i nuovi sviluppi. Viene chiamato il nuovo provider OLE DB di [Driver Microsoft OLE DB per SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) che verrà aggiornato con le funzionalità server più recenti in futuro.

## <a name="connection-string-parameters"></a>Parametri della stringa di connessione
 Per connettersi a questo provider, impostare il *Provider* argomento per il [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà:

```vb
SQLOLEDB
```

 Questo valore può anche essere impostato o letto usando il [Provider](../../../ado/reference/ado-api/provider-property-ado.md) proprietà.

## <a name="typical-connection-string"></a>Stringa di connessione tipica
 Una stringa di connessione tipica per questo provider è:

```vb
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 La stringa è costituita da queste parole chiave:

|Parola chiave|Descrizione|
|-------------|-----------------|
|**Provider**|Specifica il Provider OLE DB per SQL Server.|
|**Zdroj dat** o **Server**|Specifica il nome di un server.|
|**Catalogo iniziale** o **Database**|Specifica il nome di un database nel server.|
|**ID utente** o **uid**|Specifica il nome utente (per l'autenticazione di SQL Server).|
|**La password** o **pwd**|Specifica la password dell'utente (per l'autenticazione di SQL Server).|

> [!NOTE]
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, è necessario specificare **Trusted_Connection = yes** oppure **Integrated Security = SSPI** anziché un ID utente e password informazioni nella stringa di connessione.

## <a name="provider-specific-connection-parameters"></a>Parametri di connessione specifica del provider
 Il provider supporta vari parametri di connessione specifica del provider oltre a quelli definiti da ADO. Come con le proprietà di connessione ADO, è possibile impostare queste proprietà specifiche del provider tramite il [delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta di un [connessione](../../../ado/reference/ado-api/connection-object-ado.md) o può essere impostato come parte del **ConnectionString**.

|Parametro|Descrizione|
|---------------|-----------------|
|Trusted_Connection|Indica la modalità di autenticazione utente. Può essere impostata su **Yes** oppure **No**. Il valore predefinito è **No**. Se questa proprietà è impostata su **Yes**, SQLOLEDB Usa la modalità di autenticazione di Microsoft Windows NT per autorizzare l'accesso utente al database di SQL Server specificato dal **posizione** e [Datasource ](../../../ado/reference/ado-api/datasource-property-ado.md) i valori delle proprietà. Se questa proprietà è impostata su **No**, SQLOLEDB Usa la modalità mista per autorizzare l'accesso utente al database di SQL Server. L'account di accesso di SQL Server e la password vengono specificati nel **Id utente** e **Password** proprietà.|
|Lingua corrente|Indica un nome di lingua di SQL Server. Identifica la lingua utilizzata per la selezione e la formattazione dei messaggi di sistema. Il linguaggio deve essere installato in SQL Server, in caso contrario, apertura della connessione avrà esito negativo.|
|Indirizzo di rete|Indica l'indirizzo di rete del Server SQL specificato per il **posizione** proprietà.|
|Libreria di rete|Indica il nome della libreria di rete (DLL) utilizzata per comunicare con SQL Server. Il nome non deve include il percorso o l'estensione di file DLL. Il valore predefinito è fornito per la configurazione del client SQL Server.|
|Utilizzare Procedure per preparare|Determina se SQL Server crea le stored procedure temporanee quando vengono preparati i comandi (per il **Prepared** proprietà).|
|Conversione automatica|Indica se vengono convertiti nei caratteri OEM/ANSI. Questa proprietà può essere impostata su **True** oppure **False**. Il valore predefinito è **True**. Se questa proprietà è impostata su **True**, SQLOLEDB esegue la conversione di caratteri OEM/ANSI quando le stringhe di caratteri multibyte vengono recuperate da o inviate a SQL Server. Se questa proprietà è impostata su **False**, SQLOLEDB non esegue la conversione dei caratteri OEM/ANSI sui dati di stringa di caratteri multibyte.|
|Packet Size|Indica una dimensione dei pacchetti di rete in byte. Il valore di proprietà delle dimensioni di pacchetto deve essere compreso tra 512 e 32767. Le dimensioni del pacchetto rete SQLOLEDB predefinito sono 4096.|
|Application Name|Indica il nome dell'applicazione client.|
|ID workstation|Stringa che identifica la workstation.|

## <a name="command-object-usage"></a>Utilizzo dell'oggetto Command
 SQLOLEDB accetta un amalgama di ODBC, ANSI e specifiche di SQL Server Transact-SQL come sintassi valida. L'istruzione SQL seguente, ad esempio, utilizza una sequenza di escape ODBC SQL per specificare la funzione per i valori stringa LCASE:

```sql
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE restituisce una stringa di caratteri, convertendo tutti i caratteri maiuscoli nei rispettivi equivalenti minuscoli. La funzione stringa ANSI SQL inferiore esegue la stessa operazione, pertanto l'istruzione SQL seguente è un ANSI equivalente all'istruzione ODBC presentata in precedenza:

```sql
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB elabora correttamente entrambe le versioni dell'istruzione quando vengono specificate come testo per un comando.

## <a name="stored-procedures"></a>Stored procedure
 Quando si esegue SQL Server stored procedure tramite un comando SQLOLEDB, è possibile utilizzare la sequenza di escape ODBC call procedure nel testo del comando. SQLOLEDB Usa quindi il meccanismo di chiamata di procedura remota di SQL Server per ottimizzare l'elaborazione del comando. Ad esempio, l'istruzione ODBC SQL seguente è il testo del comando preferito su un modulo Transact-SQL:

## <a name="odbc-sql"></a>ODBC SQL

```vb
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```sql
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>Funzionalità di SQL Server
 Con SQL Server, ADO possa utilizzare XML for **comandi** input e recuperare i risultati in formato flusso XML invece che nella **Recordset** oggetti. Per altre informazioni, vedere [Using flussi di Input del comando](../../../ado/guide/data/command-streams.md) e [il recupero di set di risultati in flussi](../../../ado/guide/data/retrieving-resultsets-into-streams.md).

### <a name="accessing-sqlvariant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>Accesso ai dati sql_variant tramite MDAC 2.7, MDAC 2.8 o Windows DAC 6.0
 Microsoft SQL Server ha un tipo di dati denominato **sql_variant**. Simile a OLE DB **DBTYPE_VARIANT**, il **sql_variant** tipo di dati può archiviare i dati di diversi tipi. Tuttavia, esistono alcune differenze principali tra **DBTYPE_VARIANT** e **sql_variant**. ADO gestisce anche i dati archiviati come una **sql_variant** valore in modo diverso rispetto a come gestisce altri tipi di dati. Nell'elenco seguente vengono descritti i problemi da prendere in considerazione quando si accede a dati di SQL Server archiviati nelle colonne di tipo **sql_variant**.

-   In MDAC 2.7, MDAC 2.8 e Windows Data Access Components (Windows DAC) 6.0, il Provider OLE DB per SQL Server supporta il **sql_variant** tipo. Non è il Provider OLE DB per ODBC.

-   Il **sql_variant** tipo corrisponde esattamente le **DBTYPE_VARIANT** tipo di dati.  Il **sql_variant** tipo supporta alcuni nuovi sottotipi non supportati dal **DBTYPE_VARIANT,** inclusi **GUID**, **ANSI** (non UNICODE) le stringhe, e **BIGINT**. Usando i sottotipi diversi da quelli elencati in precedenza funzionerà correttamente.

-   Il **sql_variant** sottotipo **numerico** non corrisponde la **DBTYPE_DECIMAL** nella dimensione.

-   Coercizioni dei tipi di dati più comporterà i tipi che non corrispondono. Ad esempio, la coercizione di una **sql_variant** con un sottotipo del **GUID** a un **DBTYPE_VARIANT** comporterà un sottotipo del **safearray**(byte) . Questo tipo di conversione verso un **sql_variant** comporterà un sottotipo di nuove **matrice**(byte).

-   **Recordset** i campi che contengono **sql_variant** dei dati possono essere eseguita in modalità remota (marshalling) o persistente solo se il **sql_variant** contiene specifici sottotipi. Se si tenta in remoto o rendere persistenti i dati con il codice seguente non è supportato sottotipi causerà un errore di run-time (conversione non supportata) dal Provider di persistenza (MSPersist) di Microsoft: **VT_VARIANT**, **VT_RECORD**, **VT_ILLEGAL**, **VT_UNKNOWN**, **VT_BSTR**, e **VT_DISPATCH.**

-   Il Provider OLE DB per SQL Server in MDAC 2.7, MDAC 2.8 e 6.0 di Windows dell'applicazione livello dati include una proprietà dinamica denominata **consentire varianti Native** che, come suggerisce il nome, consente agli sviluppatori di accedere il **sql_variant** in formato nativo in contrapposizione a un **DBTYPE_VARIANT**. Se questa proprietà è impostata e un **Recordset** viene aperto con il motore del cursore Client (**adUseClient**), il **Open** chiamata avrà esito negativo. Se questa proprietà è impostata e un **Recordset** viene aperto con i cursori del server (**adUseServer**), il **Open** chiamata avrà esito positivo, ma che accedono a colonne di tipo **sql_variant** genererà un errore.

-   Nelle applicazioni client che utilizzano MDAC 2.5 **sql_variant** dati possono essere usati con le query su Microsoft SQL Server. Tuttavia, i valori del **sql_variant** data viene considerati come stringhe. Le applicazioni client devono essere aggiornate a MDAC 2.7, MDAC 2.8 o Windows DAC 6.0.

## <a name="recordset-behavior"></a>Comportamento dell'oggetto Recordset
 SQLOLEDB non è possibile utilizzare i cursori di SQL Server per supportare più risultati generati da molti comandi. Se un consumer richiede un set di record che richiedono il supporto di cursore di SQL Server, si verifica un errore se il testo del comando usato più di un unico recordset genera come risultato.

 Scorrevole SQLOLEDB recordset sono supportati dai cursori di SQL Server. SQL Server impone limitazioni sui cursori che sono sensibili alle modifiche apportate da altri utenti del database. In particolare, le righe in alcuni cursori non possono essere ordinate e provare a creare un set di record usando un comando che include una clausola SQL ORDER BY può avere esito negativo.

## <a name="dynamic-properties"></a>Proprietà dinamiche
 Il Provider Microsoft OLE DB per SQL Server inserisce diverse proprietà dinamiche nel **delle proprietà** raccolta di oggetti [connessione](../../../ado/reference/ado-api/connection-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)e [ Comando](../../../ado/reference/ado-api/command-object-ado.md) oggetti.

 Le tabelle seguenti sono un incrociato dei nomi per ogni proprietà dinamica ADO e OLE DB. Riferimento dei programmatori OLE DB è relativo a un nome di proprietà di ADO con il termine "Description". È possibile trovare altre informazioni su queste proprietà in riferimento OLE DB Programmer. Cercare il nome della proprietà OLE DB nell'indice o vedere [appendice c: Proprietà OLE DB](https://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292).

## <a name="connection-dynamic-properties"></a>Proprietà dinamiche di connessione
 Le proprietà seguenti vengono aggiunti per il **le proprietà** insieme del **connessione** oggetto.

|Nome della proprietà ADO|Nome della proprietà OLE DB|
|-----------------------|--------------------------|
|Sessioni attive|DBPROP_ACTIVESESSIONS|
|Interruzione asincrona|DBPROP_ASYNCTXNABORT|
|Commit asincrono|DBPROP_ASYNCTNXCOMMIT|
|Livelli di isolamento autocommit|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|Posizione catalogo|DBPROP_CATALOGLOCATION|
|Termine catalogo|DBPROP_CATALOGTERM|
|Definizione di colonna|DBPROP_COLUMNDEFINITION|
|Timeout di connessione|DBPROP_INIT_TIMEOUT|
|Catalogo corrente|DBPROP_CURRENTCATALOG|
|origine dati|DBPROP_INIT_DATASOURCE|
|Nome origine dati|DBPROP_DATASOURCENAME|
|Oggetto di origine dati modello di Threading|DBPROP_DSOTHREADMODEL|
|Nome DBMS|DBPROP_DBMSNAME|
|Versione DBMS|DBPROP_DBMSVER|
|Extended Properties|DBPROP_INIT_PROVIDERSTRING|
|Supporto GROUP BY|DBPROP_GROUPBY|
|Supporto tabelle eterogenee|DBPROP_HETEROGENEOUSTABLES|
|Distinzione maiuscole/minuscole identificatore|DBPROP_IDENTIFIERCASE|
|Catalogo iniziale|DBPROP_INIT_CATALOG|
|Livelli di isolamento|DBPROP_SUPPORTEDTXNISOLEVELS|
|Mantenimento isolamento|DBPROP_SUPPORTEDTXNISORETAIN|
|Locale Identifier|DBPROP_INIT_LCID|
|Dimensione massima dell'indice|DBPROP_MAXINDEXSIZE|
|Dimensioni massime delle righe|DBPROP_MAXROWSIZE|
|Dimensioni massime riga con BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|Numero massimo di tabelle in SELECT|DBPROP_MAXTABLESINSELECT|
|Più set di parametri|DBPROP_MULTIPLEPARAMSETS|
|Risultati multipli|DBPROP_MULTIPLERESULTS|
|Più oggetti di archiviazione|DBPROP_MULTIPLESTORAGEOBJECTS|
|Aggiornamento tabelle multiple|DBPROP_MULTITABLEUPDATE|
|Ordine delle regole di confronto NULL|DBPROP_NULLCOLLATION|
|Comportamento concatenazione NULL|DBPROP_CONCATNULLBEHAVIOR|
|Versione OLE DB|DBPROP_PROVIDEROLEDBVER|
|Supporto oggetti OLE|DBPROP_OLEOBJECTS|
|Supporto per Rowset aperto|DBPROP_OPENROWSETSUPPORT|
|Colonne ORDER BY nell'elenco di selezione|DBPROP_ORDERBYCOLUMNSINSELECT|
|Disponibilità parametro di output|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Passa per le funzioni di accesso di riferimento|DBPROP_BYREFACCESSORS|
|Password|DBPROP_AUTH_PASSWORD|
|Persist Security Info|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
|Tipo ID persistente|DBPROP_PERSISTENTIDTYPE|
|Comportamento preparazione interruzione|DBPROP_PREPAREABORTBEHAVIOR|
|Comportamento preparazione Commit|DBPROP_PREPARECOMMITBEHAVIOR|
|Termine routine|DBPROP_PROCEDURETERM|
|Messaggio di richiesta|DBPROP_INIT_PROMPT|
|Nome descrittivo del provider|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|Versione del provider|DBPROP_PROVIDERVER|
|Origine dati di sola lettura|DBPROP_DATASOURCEREADONLY|
|Conversioni di set di righe di comando|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|Termine schema|DBPROP_SCHEMATERM|
|Utilizzo dello schema|DBPROP_SCHEMAUSAGE|
|Supporto di SQL|DBPROP_SQLSUPPORT|
|Archiviazione strutturata|DBPROP_STRUCTUREDSTORAGE|
|Supporto delle sottoquery|DBPROP_SUBQUERIES|
|Termine tabella|DBPROP_TABLETERM|
|Transazione DDL|DBPROP_SUPPORTEDTXNDDL|
|ID utente|DBPROP_AUTH_USERID|
|Nome utente|DBPROP_USERNAME|
|Handle di finestra|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>Proprietà dinamiche del recordset
 Le proprietà seguenti vengono aggiunti per il **le proprietà** insieme del **Recordset** oggetto.

|Nome della proprietà ADO|Nome della proprietà OLE DB|
|-----------------------|--------------------------|
|Ordine di accesso|DBPROP_ACCESSORDER|
|Blocca gli oggetti di archiviazione|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo di segnalibro|DBPROP_BOOKMARKTYPE|
|Supporta|DBPROP_IROWSETLOCATE|
|Modificare le righe inserite|DBPROP_CHANGEINSERTEDROWS|
|Privilegi colonna|DBPROP_COLUMNRESTRICT|
|Notifica impostazione colonna|DBPROP_NOTIFYCOLUMNSET|
|Timeout comando|DBPROP_COMMANDTIMEOUT|
|Rinviare colonna|DBPROP_DEFERRED|
|Aggiornamenti degli oggetti di archiviazione di ritardo|DBPROP_DELAYSTORAGEOBJECTS|
|Recupera all'indietro|DBPROP_CANFETCHBACKWARDS|
|Contenere righe|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Righe immobili|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|Segnalibri letterali|DBPROP_LITERALBOOKMARKS|
|Identità di riga letterale|DBPROP_LITERALIDENTITY|
|Numero massimo righe aperte|DBPROP_MAXOPENROWS|
|Numero massimo righe in sospeso|DBPROP_MAXPENDINGROWS|
|Numero massimo di righe|DBPROP_MAXROWS|
|Granularità notifiche|DBPROP_NOTIFICATIONGRANULARITY|
|Fasi di notifica|DBPROP_NOTIFICATIONPHASES|
|Oggetti transazione|DBPROP_TRANSACTEDOBJECT|
|Modifiche di altri utenti visibili|DBPROP_OTHERUPDATEDELETE|
|Inserimenti di altri utenti visibili|DBPROP_OTHERINSERT|
|Proprie modifiche visibili|DBPROP_OWNUPDATEDELETE|
|Inserimenti locali visibili|DBPROP_OWNINSERT|
|Mantieni in caso di interruzione|DBPROP_ABORTPRESERVE|
|Mantieni in caso di Commit|DBPROP_COMMITPRESERVE|
|Riavvio rapido|DBPROP_QUICKRESTART|
|Eventi rientranti|DBPROP_REENTRANTEVENTS|
|Rimuovere le righe eliminate|DBPROP_REMOVEDELETED|
|Riporta modifiche Multiple|DBPROP_REPORTMULTIPLECHANGES|
|Restituisci inserimenti in sospeso|DBPROP_RETURNPENDINGINSERTS|
|Notifica eliminazione riga|DBPROP_NOTIFYROWDELETE|
|Notifica prima modifica riga|DBPROP_NOTIFYROWFIRSTCHANGE|
|Notifica inserimento riga|DBPROP_NOTIFYROWINSERT|
|Privilegi riga|DBPROP_ROWRESTRICT|
|Notifica risincronizzazione riga|DBPROP_NOTIFYROWRESYNCH|
|Modello di Threading riga|DBPROP_ROWTHREADMODEL|
|Notifica annullamento Modifica riga|DBPROP_NOTIFYROWUNDOCHANGE|
|Notifica annullamento eliminazione riga|DBPROP_NOTIFYROWUNDODELETE|
|Notifica annullamento inserimento riga|DBPROP_NOTIFYROWUNDOINSERT|
|Notifica aggiornamento riga|DBPROP_NOTIFYROWUPDATE|
|Notifica modifica posizione recupero gruppo di righe|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|Notifica rilascio gruppo di righe|DBPROP_NOTIFYROWSETRELEASE|
|Scorri indietro|DBPROP_CANSCROLLBACKWARDS|
|Cursore del server|DBPROP_SERVERCURSOR|
|Ignora segnalibri eliminati|DBPROP_BOOKMARKSKIPPED|
|Identità riga forte|DBPROP_STRONGITDENTITY|
|Righe univoche|DBPROP_UNIQUEROWS|
|Aggiornabile|DBPROP_UPDATABILITY|
|Usare i segnalibri|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Proprietà dinamiche di comando
 Le proprietà seguenti vengono aggiunti per il **proprietà** insieme del **comando** oggetto.

|Nome della proprietà ADO|Nome della proprietà OLE DB|
|-----------------------|--------------------------|
|Ordine di accesso|DBPROP_ACCESSORDER|
|Percorso di base|SSPROP_STREAM_BASEPATH|
|Blocca gli oggetti di archiviazione|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo di segnalibro|DBPROP_BOOKMARKTYPE|
|Supporta|DBPROP_IROWSETLOCATE|
|Modificare le righe inserite|DBPROP_CHANGEINSERTEDROWS|
|Privilegi colonna|DBPROP_COLUMNRESTRICT|
|Notifica impostazione colonna|DBPROP_NOTIFYCOLUMNSET|
|Tipo di contenuto|SSPROP_STREAM_CONTENTTYPE|
|Recupero di cursore automaticamente|SSPROP_CURSORAUTOFETCH|
|Rinviare colonna|DBPROP_DEFERRED|
|Posticipa comandi prepare|SSPROP_DEFERPREPARE|
|Aggiornamenti degli oggetti di archiviazione di ritardo|DBPROP_DELAYSTORAGEOBJECTS|
|Recupera all'indietro|DBPROP_CANFETCHBACKWARDS|
|Contenere righe|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Righe immobili|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch|DBPROP_IRowsetResynch|
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|Segnalibri letterali|DBPROP_LITERALBOOKMARKS|
|Identità di riga letterale|DBPROP_LITERALIDENTITY|
|Modalità di blocco|DBPROP_LOCKMODE|
|Numero massimo righe aperte|DBPROP_MAXOPENROWS|
|Numero massimo righe in sospeso|DBPROP_MAXPENDINGROWS|
|Numero massimo di righe|DBPROP_MAXROWS|
|Granularità notifiche|DBPROP_NOTIFICATIONGRANULARITY|
|Fasi di notifica|DBPROP_NOTIFICATIONPHASES|
|Oggetti transazione|DBPROP_TRANSACTEDOBJECT|
|Modifiche di altri utenti visibili|DBPROP_OTHERUPDATEDELETE|
|Inserimenti di altri utenti visibili|DBPROP_OTHERINSERT|
|Proprietà di codifica di output|DBPROP_OUTPUTENCODING|
|Proprietà output Stream|DBPROP_OUTPUTSTREAM|
|Proprie modifiche visibili|DBPROP_OWNUPDATEDELETE|
|Inserimenti locali visibili|DBPROP_OWNINSERT|
|Mantieni in caso di interruzione|DBPROP_ABORTPRESERVE|
|Mantieni in caso di Commit|DBPROP_COMMITPRESERVE|
|Riavvio rapido|DBPROP_QUICKRESTART|
|Eventi rientranti|DBPROP_REENTRANTEVENTS|
|Rimuovere le righe eliminate|DBPROP_REMOVEDELETED|
|Riporta modifiche Multiple|DBPROP_REPORTMULTIPLECHANGES|
|Restituisci inserimenti in sospeso|DBPROP_RETURNPENDINGINSERTS|
|Notifica eliminazione riga|DBPROP_NOTIFYROWDELETE|
|Notifica prima modifica riga|DBPROP_NOTIFYROWFIRSTCHANGE|
|Notifica inserimento riga|DBPROP_NOTIFYROWINSERT|
|Privilegi riga|DBPROP_ROWRESTRICT|
|Notifica risincronizzazione riga|DBPROP_NOTIFYROWRESYNCH|
|Modello di Threading riga|DBPROP_ROWTHREADMODEL|
|Notifica annullamento Modifica riga|DBPROP_NOTIFYROWUNDOCHANGE|
|Notifica annullamento eliminazione riga|DBPROP_NOTIFYROWUNDODELETE|
|Notifica annullamento inserimento riga|DBPROP_NOTIFYROWUNDOINSERT|
|Notifica aggiornamento riga|DBPROP_NOTIFYROWUPDATE|
|Notifica modifica posizione recupero gruppo di righe|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|Notifica rilascio gruppo di righe|DBPROP_NOTIFYROWSETRELEASE|
|Scorri indietro|DBPROP_CANSCROLLBACKWARDS|
|Cursore del server|DBPROP_SERVERCURSOR|
|Dati server all'inserimento|DBPROP_SERVERDATAONINSERT|
|Ignora segnalibri eliminati|DBPROP_BOOKMARKSKIP|
|Identità riga forte|DBPROP_STRONGIDENTITY|
|Aggiornabile|DBPROP_UPDATABILITY|
|Usare i segnalibri|DBPROP_BOOKMARKS|
|Radice XML|SSPROP_STREAM_XMLROOT|
|XSL|SSPROP_STREAM_XSL|

 Per dettagli specifici sull'implementazione e funzionale informazioni relative al Provider OLE DB Microsoft SQL Server, vedere la [Provider di SQL Server](https://msdn.microsoft.com/adf1d6c4-5930-444a-9248-ff1979729635).

## <a name="see-also"></a>Vedere anche
 [Proprietà ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [proprietà del Provider (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
