---
title: Provider Microsoft OLE DB per ODBC | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for ODBC [ADO]
- providers [ADO], OLE DB provider for ODBC
ms.assetid: 2dc0372d-e74d-4d0f-9c8c-04e5a168c148
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e75b79934022743ba806722427dd37ab733bc2f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62853324"
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Provider Microsoft OLE DB per ODBC Panoramica
Per un programmatore di ADO o servizi desktop remoto, un mondo ideale sarebbe uno dei dati di ogni origine espone un'interfaccia OLE DB, in modo da ADO è stato possibile chiamare direttamente nell'origine dati. Anche se un numero sempre maggiore di fornitori di database implementa le interfacce OLE DB, alcune origini dati non sono ancora esposti in questo modo. Tuttavia, la maggior parte dei sistemi DBMS in uso oggi accessibili tramite ODBC.

 Driver ODBC sono disponibili per i principali DBMS in uso oggi stesso, tra cui Microsoft SQL Server, Microsoft Access (motore di database Microsoft Jet) e Microsoft FoxPro, oltre ai prodotti del database non Microsoft, ad esempio Oracle.

 Il Provider ODBC di Microsoft, tuttavia, consente di ADO per connettersi a qualsiasi origine dati ODBC. Il provider è a thread libero e abilitata per Unicode.

 Il provider supporta le transazioni, anche se diversi motori di DBMS offrono diversi tipi di supporto delle transazioni. Microsoft Access, ad esempio, supporta le transazioni nidificate fino a cinque livelli.

 Questo è il provider predefinito per ADO e sono supportati tutti i metodi e proprietà ADO dipende dal provider.

## <a name="connection-string-parameters"></a>Parametri della stringa di connessione
 Per connettersi a questo provider, impostare il **Provider =** argomento delle [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà:

```
MSDASQL
```

 Leggere il [Provider](../../../ado/reference/ado-api/provider-property-ado.md) proprietà restituirà anche questa stringa.

## <a name="typical-connection-string"></a>Stringa di connessione tipica
 Una stringa di connessione tipica per questo provider è:

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 La stringa è costituita da queste parole chiave:

|Parola chiave|Descrizione|
|-------------|-----------------|
|**Provider**|Specifica il provider OLE DB per ODBC.|
|**DSN**|Specifica il nome dell'origine dati.|
|**UID**|Specifica il nome utente.|
|**PWD**|Specifica la password dell'utente.|
|**URL**|Specifica l'URL di un file o directory pubblicata in una cartella Web.|

 Poiché si tratta di provider predefinito per ADO, se si omette il **Provider =** parametro della stringa di connessione ADO tenterà di stabilire una connessione al provider.

> [!NOTE]
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, è necessario specificare **Trusted_Connection = yes** oppure **Integrated Security = SSPI** anziché un ID utente e password informazioni nella stringa di connessione.

 Il provider non supporta parametri di connessione specifico oltre a quelli definiti da ADO. Tuttavia, il provider passerà a eventuali parametri di connessione non ADO da Gestione driver ODBC.

 Poiché è possibile omettere il **Provider** parametro, pertanto è possibile comporre una stringa di connessione ADO è identica alla stringa di connessione ODBC per la stessa origine dati. Usare gli stessi nomi di parametro (**DRIVER =**, **DATABASE =**, **DSN =** e così via), i valori e la sintassi come si sarebbe durante la composizione di una stringa di connessione ODBC. È possibile connettersi con o senza un nome di origine di dati predefiniti (DSN) o FileDSN.

## <a name="syntax-with-a-dsn-or-filedsn"></a>Sintassi con un DSN o FileDSN:

```
"[Provider=MSDASQL;] { DSN=name | FileDSN=filename } ;
[DATABASE=database;] UID=user; PWD=password"
```

## <a name="syntax-without-a-dsn-dsn-less-connection"></a>Sintassi senza un DSN (DSN senza connessione):

```
"[Provider=MSDASQL;] DRIVER=driver; SERVER=server;
DATABASE=database; UID=MyUserID; PWD=MyPassword"
```

## <a name="remarks"></a>Note
 Se si usa un' **DSN** oppure **FileDSN**, deve essere definito tramite Amministrazione origine dati ODBC nel Pannello di controllo di Windows. In Microsoft Windows 2000, l'amministratore ODBC si trova in strumenti di amministrazione. Nelle versioni precedenti di Windows, è denominata l'icona del ruolo Amministratore ODBC **ODBC a 32 bit** o semplicemente **ODBC**.

 Come alternativa all'impostazione di un **DSN**, è possibile specificare il driver ODBC (**DRIVER =**), ad esempio "SQL Server"; il nome del server (**SERVER =**); e il nome del database (**DATABASE =**).

 È anche possibile specificare un nome di account utente (**UID =**) e la password per l'account utente (**PWD =**) nei parametri ODBC specifiche o nello standard definiti da ADO *utente* e *password* parametri.

 Anche se un **DSN** già una definizione specifica un database, è possibile specificare *una* *database* parametro oltre a un **DSN** per la connessione per un database diverso. È consigliabile includere sempre *il* *database* parametro quando si usa un **DSN**. Ciò garantisce che la connessione al database corretto se un altro utente modificato il parametro predefinito del database dall'ultima ricerca i **DSN** definizione.

## <a name="provider-specific-connection-properties"></a>Proprietà di connessione specifiche del provider
 Il provider OLE DB per ODBC aggiunte diverse proprietà per il [delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) insieme delle **connessione** oggetto. Nella tabella seguente sono elencate queste proprietà con il nome della proprietà OLE DB corrispondente racchiuso tra parentesi.

|Nome proprietà|Descrizione|
|-------------------|-----------------|
|Procedure accessibile (KAGPROP_ACCESSIBLEPROCEDURES)|Indica se l'utente ha accesso alle stored procedure.|
|Tabella accessibile (KAGPROP_ACCESSIBLETABLES)|Indica se l'utente dispone dell'autorizzazione per eseguire le istruzioni SELECT sulle tabelle del database.|
|Istruzioni attive (KAGPROP_ACTIVESTATEMENTS)|Indica il numero di handle che può supportare un driver ODBC in una connessione.|
|Nome driver (KAGPROP_DRIVERNAME)|Indica il nome del file del driver ODBC.|
|Versione del driver ODBC (KAGPROP_DRIVERODBCVER)|Indica la versione di ODBC che supporta questo driver.|
|File Usage (KAGPROP_FILEUSAGE)|Indica il modo in cui il driver considera un file in un'origine dati. come una tabella o come un catalogo.|
|Ad esempio la clausola di Escape (KAGPROP_LIKEESCAPECLAUSE)|Indica se il driver supporta la definizione e l'uso di un carattere di escape per il carattere di percentuale (%) e sottolineare il carattere (_) nel predicato LIKE di una clausola WHERE.|
|Numero massimo di colonne in Group By (KAGPROP_MAXCOLUMNSINGROUPBY)|Indica il numero massimo di colonne che possono essere incluse nella clausola GROUP BY di un'istruzione SELECT.|
|Numero massimo di colonne nell'indice (KAGPROP_MAXCOLUMNSININDEX)|Indica il numero massimo di colonne che possono essere inclusi in un indice.|
|Numero massimo di colonne nella clausola Order By (KAGPROP_MAXCOLUMNSINORDERBY)|Indica il numero massimo di colonne che possono essere incluse nella clausola ORDER BY di un'istruzione SELECT.|
|Numero massimo di colonne nell'istruzione Select (KAGPROP_MAXCOLUMNSINSELECT)|Indica il numero massimo di colonne che possono essere elencati nella parte SELECT di un'istruzione SELECT.|
|Numero massimo di colonne nella tabella (KAGPROP_MAXCOLUMNSINTABLE)|Indica il numero massimo di colonne consentite in una tabella.|
|Funzioni numeriche (KAGPROP_NUMERICFUNCTIONS)|Indica le funzioni numeriche sono supportate dal driver ODBC. Per un elenco di nomi di funzione e i valori associati usati in questa maschera di bit, vedere [appendice e: Funzioni scalari](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), nella documentazione relativa a ODBC.|
|Funzionalità di outer Join (KAGPROP_OJCAPABILITY)|Indica i tipi di OUTER join è supportata dal provider.|
|Outer join (KAGPROP_OUTERJOINS)|Indica se il provider supporta gli OUTER join.|
|Caratteri speciali (KAGPROP_SPECIALCHARACTERS)|Indica quali caratteri hanno un significato speciale per il driver ODBC.|
|Stored procedure (KAGPROP_PROCEDURES)|Indica se le stored procedure sono disponibili per l'uso con il driver ODBC.|
|Funzioni stringa (KAGPROP_STRINGFUNCTIONS)|Indica le funzioni di stringa supportate dal driver ODBC. Per un elenco di nomi di funzione e i valori associati usati in questa maschera di bit, vedere [appendice e: Funzioni scalari](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), nella documentazione relativa a ODBC.|
|Funzioni di sistema (KAGPROP_SYSTEMFUNCTIONS)|Indica le funzioni di sistema supportate dal driver ODBC. Per un elenco di nomi di funzione e i valori associati usati in questa maschera di bit, vedere [appendice e: Funzioni scalari](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), nella documentazione relativa a ODBC.|
|Funzioni di data e ora (KAGPROP_TIMEDATEFUNCTIONS)|Indica quali funzioni di data e ora sono supportate dal driver ODBC. Per un elenco di nomi di funzione e i valori associati usati in questa maschera di bit, vedere [appendice e: Funzioni scalari](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), nella documentazione relativa a ODBC.|
|Supporto della grammatica SQL (KAGPROP_ODBCSQLCONFORMANCE)|Indica la grammatica SQL che supporti il driver ODBC.|

## <a name="provider-specific-recordset-and-command-properties"></a>Recordset specifici del provider e le proprietà dei comandi
 Il provider OLE DB per ODBC aggiunte diverse proprietà per il **delle proprietà** insieme delle **Recordset** e **comando** oggetti. Nella tabella seguente sono elencate queste proprietà con il nome della proprietà OLE DB corrispondente racchiuso tra parentesi.

|Nome proprietà|Descrizione|
|-------------------|-----------------|
|Query Based Updates/Deletes/Inserts (KAGPROP_QUERYBASEDUPDATES)|Indica se gli aggiornamenti, eliminazioni e inserimenti possono essere eseguiti tramite query SQL.|
|Tipo di concorrenza ODBC (KAGPROP_CONCURRENCY)|Indica il metodo utilizzato per ridurre i potenziali problemi causati da due utenti che cercano di accedere contemporaneamente gli stessi dati dall'origine dati.|
|Accessibilità BLOB sul cursore Forward-Only (KAGPROP_BLOBSONFOCURSOR)|Indica se BLOB **campi** sono accessibili quando si usa un cursore forward-only.|
|Includere SQL_FLOAT e SQL_DOUBLE SQL_REAL nelle clausole WHERE QBU (KAGPROP_INCLUDENONEXACT)|Indica se i valori SQL_FLOAT e SQL_DOUBLE SQL_REAL possono essere incluso in una clausola WHERE QBU.|
|Posizione nell'ultima riga dopo l'inserimento (KAGPROP_POSITIONONNEWROW)|Indica che dopo l'inserimento di un nuovo record in una tabella, l'ultima riga della tabella saranno forniti alla riga corrente.|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|Indica se il **IRowsetChange** interfaccia fornisce il supporto di informazioni estese.|
|Tipo di cursore ODBC (KAGPROP_CURSOR)|Indica il tipo di cursore utilizzato per il **Recordset**.|
|Generare un set di righe che può essere sottoposta a marshalling (KAGPROP_MARSHALLABLE)|Indica che il driver ODBC genera un oggetto recordset che può essere sottoposta a marshalling|

## <a name="command-text"></a>Testo comando
 Modalità di utilizzo di [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto dipende in gran parte dall'origine dati e il tipo di istruzione di query o un comando verranno accettati.

 ODBC fornisce una sintassi specifica per la chiamata di stored procedure. Per il [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) proprietà di un **comando** oggetto, il *CommandText* argomento per il **Execute** metodo su un [ Connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto, o il *origine* argomento per il **Open** metodo su un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto, passa una stringa con questa sintassi:

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , ... ]] ) ] }"
```

 Ogni **?** fa riferimento a un oggetto di [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) raccolta. Il primo **?** i riferimenti **parametri**(0), alla successiva **?** i riferimenti **parametri**(1), e così via.

 I parametri di riferimento sono facoltativi e dipendono dalla struttura della stored procedure. Se si desidera chiamare una stored procedure che non definisce alcun parametro, la stringa di sarebbe simile al seguente:

```
"{ call procedure }"
```

 Se si dispongono di due parametri di query, la stringa sarà simile alla seguente:

```
"{ call procedure ( ?, ? ) }"
```

 Se la stored procedure restituirà un valore, il valore restituito viene considerato come un altro parametro. Se non si dispone di alcun parametro di query, ma è un valore restituito, la stringa sarà simile alla seguente:

```
"{ ? = call procedure }"
```

 Infine, se si ha un valore restituito e due parametri di query, la stringa sarà simile alla seguente:

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>Comportamento dell'oggetto Recordset
 Le tabelle seguenti elencano i metodi ADO standard e le proprietà disponibili in un **Recordset** aprire l'oggetto con questo provider.

 Per informazioni più dettagliate sui **Recordset** comportamento per la configurazione del provider, eseguire il [supporta](../../../ado/reference/ado-api/supports-method.md) metodo ed enumerare il **proprietà** raccolta del **Recordset** per determinare se sono presenti proprietà dinamiche specifiche del provider.

 Disponibilità di standard ADO **Recordset** proprietà:

|Proprietà|ForwardOnly|Dynamic|Keyset|Static|
|--------------|-----------------|-------------|------------|------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|non disponibile|non disponibile|lettura/scrittura|lettura/scrittura|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|non disponibile|non disponibile|lettura/scrittura|lettura/scrittura|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|lettura/scrittura|lettura/scrittura|lettura/scrittura|lettura/scrittura|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Sola lettura|Sola lettura|Sola lettura|Sola lettura|
|[Segnalibro](../../../ado/reference/ado-api/bookmark-property-ado.md)|non disponibile|non disponibile|lettura/scrittura|lettura/scrittura|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|lettura/scrittura|lettura/scrittura|lettura/scrittura|lettura/scrittura|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|lettura/scrittura|lettura/scrittura|lettura/scrittura|lettura/scrittura|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|lettura/scrittura|lettura/scrittura|lettura/scrittura|lettura/scrittura|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|Sola lettura|Sola lettura|Sola lettura|Sola lettura|
|[Filter](../../../ado/reference/ado-api/filter-property.md)|lettura/scrittura|lettura/scrittura|lettura/scrittura|lettura/scrittura|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|lettura/scrittura|lettura/scrittura|lettura/scrittura|lettura/scrittura|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|lettura/scrittura|lettura/scrittura|lettura/scrittura|lettura/scrittura|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|lettura/scrittura|lettura/scrittura|lettura/scrittura|lettura/scrittura|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|lettura/scrittura|non disponibile|Sola lettura|Sola lettura|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|lettura/scrittura|lettura/scrittura|lettura/scrittura|lettura/scrittura|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|lettura/scrittura|non disponibile|Sola lettura|Sola lettura|
|[Origine](../../../ado/reference/ado-api/source-property-ado-recordset.md)|lettura/scrittura|lettura/scrittura|lettura/scrittura|lettura/scrittura|
|[Stato](../../../ado/reference/ado-api/state-property-ado.md)|Sola lettura|Sola lettura|Sola lettura|Sola lettura|
|[Stato](../../../ado/reference/ado-api/status-property-ado-recordset.md)|Sola lettura|Sola lettura|Sola lettura|Sola lettura|

 Il [esempio di AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) e [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) proprietà sono di sola scrittura se ADO viene usato con la versione 1.0 di Provider Microsoft OLE DB per ODBC.

 Disponibilità di standard ADO **Recordset** metodi:

|Metodo|ForwardOnly|Dynamic|Keyset|Static|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Yes|Yes|Yes|Yes|
|[Annulla](../../../ado/reference/ado-api/cancel-method-ado.md)|Yes|Yes|Yes|Yes|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Yes|Yes|Yes|Yes|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Yes|Yes|Yes|Yes|
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|No|No|Yes|Yes|
|[Chiudi](../../../ado/reference/ado-api/close-method-ado.md)|Yes|Yes|Yes|Yes|
|[Elimina](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Yes|Yes|Yes|Yes|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Yes|Yes|Yes|Yes|
|[Sposta](../../../ado/reference/ado-api/move-method-ado.md)|Yes|Yes|Yes|Yes|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Yes|Yes|Yes|Yes|
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|no|Yes|Yes|Yes|
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Yes|Yes|Yes|Yes|
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|No|Yes|Yes|Yes|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)*|Yes|Yes|Yes|Yes|
|[Aprire](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Yes|Yes|Yes|Yes|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Yes|Yes|Yes|Yes|
|[Resync](../../../ado/reference/ado-api/resync-method.md)|No|No|Yes|Yes|
|[Supporti](../../../ado/reference/ado-api/supports-method.md)|Yes|Yes|Yes|Yes|
|[Update](../../../ado/reference/ado-api/update-method.md)|Yes|Yes|Yes|Yes|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Yes|Yes|Yes|Yes|

 * Non supportato per i database Microsoft Access.

## <a name="dynamic-properties"></a>Proprietà dinamiche
 Il Provider Microsoft OLE DB per ODBC inserisce diverse proprietà dinamiche nel **delle proprietà** raccolta di oggetti [connessione](../../../ado/reference/ado-api/connection-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)e [Comando](../../../ado/reference/ado-api/command-object-ado.md) oggetti.

 Le tabelle seguenti sono un incrociato dei nomi per ogni proprietà dinamica ADO e OLE DB. Riferimento dei programmatori OLE DB è relativo a un nome della proprietà ADO il termine, "Description". È possibile trovare altre informazioni su queste proprietà in riferimento OLE DB Programmer. Cercare il nome della proprietà OLE DB nell'indice o vedere [appendice c: Proprietà OLE DB](https://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292).

## <a name="connection-dynamic-properties"></a>Proprietà dinamiche di connessione
 Le proprietà seguenti vengono aggiunti per il **connessione** dell'oggetto **proprietà** raccolta.

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
|Location|DBPROP_INIT_LOCATION|
|Dimensione massima dell'indice|DBPROP_MAXINDEXSIZE|
|Dimensioni massime delle righe|DBPROP_MAXROWSIZE|
|Dimensioni massime riga con BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|Numero massimo di tabelle in SELECT|DBPROP_MAXTABLESINSELECT|
|Modalità|DBPROP_INIT_MODE|
|Più set di parametri|DBPROP_MULTIPLEPARAMSETS|
|Risultati multipli|DBPROP_MULTIPLERESULTS|
|Più oggetti di archiviazione|DBPROP_MULTIPLESTORAGEOBJECTS|
|Aggiornamento tabelle multiple|DBPROP_MULTITABLEUPDATE|
|Ordine delle regole di confronto NULL|DBPROP_NULLCOLLATION|
|Comportamento concatenazione NULL|DBPROP_CONCATNULLBEHAVIOR|
|Servizi OLE DB|DBPROP_INIT_OLEDBSERVICES|
|Versione OLE DB|DBPROP_PROVIDEROLEDBVER|
|Supporto oggetti OLE|DBPROP_OLEOBJECTS|
|Supporto per Rowset aperto|DBPROP_OPENROWSETSUPPORT|
|Colonne ORDER BY nell'elenco di selezione|DBPROP_ORDERBYCOLUMNSINSELECT|
|Disponibilità parametro di output|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Password|DBPROP_AUTH_PASSWORD|
|Passa per le funzioni di accesso di riferimento|DBPROP_BYREFACCESSORS|
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
 Le proprietà seguenti vengono aggiunti per il **Recordset** dell'oggetto **proprietà** raccolta.

|Nome della proprietà ADO|Nome della proprietà OLE DB|
|-----------------------|--------------------------|
|Ordine di accesso|DBPROP_ACCESSORDER|
|Blocca gli oggetti di archiviazione|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo di segnalibro|DBPROP_BOOKMARKTYPE|
|Supporta|DBPROP_IROWSETLOCATE|
|Modificare le righe inserite|DBPROP_CHANGEINSERTEDROWS|
|Privilegi colonna|DBPROP_COLUMNRESTRICT|
|Notifica impostazione colonna|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|Ignora segnalibri eliminati|DBPROP_BOOKMARKSKIPPED|
|Identità riga forte|DBPROP_STRONGITDENTITY|
|Righe univoche|DBPROP_UNIQUEROWS|
|Aggiornabile|DBPROP_UPDATABILITY|
|Usare i segnalibri|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Proprietà dinamiche di comando
 Le proprietà seguenti vengono aggiunti per il **comandi** dell'oggetto **proprietà** raccolta.

|Nome della proprietà ADO|Nome della proprietà OLE DB|
|-----------------------|--------------------------|
|Ordine di accesso|DBPROP_ACCESSORDER|
|Blocca gli oggetti di archiviazione|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo di segnalibro|DBPROP_BOOKMARKTYPE|
|Supporta|DBPROP_IROWSETLOCATE|
|Modificare le righe inserite|DBPROP_CHANGEINSERTEDROWS|
|Privilegi colonna|DBPROP_COLUMNRESTRICT|
|Notifica impostazione colonna|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|Ignora segnalibri eliminati|DBPROP_BOOKMARKSKIP|
|Identità riga forte|DBPROP_STRONGIDENTITY|
|Aggiornabile|DBPROP_UPDATABILITY|
|Usare i segnalibri|DBPROP_BOOKMARKS|

 Per informazioni dettagliate e sull'implementazione funzionale informazioni sui Provider Microsoft OLE DB per ODBC, vedere la [riferimento per programmatori OLE DB](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) o visitare il sito di accesso ai dati e Web Storage Developer Center su MSDN.

## <a name="see-also"></a>Vedere anche
 [Oggetto (ADO) Command](../../../ado/reference/ado-api/command-object-ado.md) [proprietà CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) [oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [proprietà ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [eseguire Metodo (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md) [metodo (Recordset ADO) Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) [insieme di parametri (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md) [raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [Proprietà del provider (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [supporta (metodo)](../../../ado/reference/ado-api/supports-method.md)
