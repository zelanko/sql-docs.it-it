---
title: Provider Microsoft OLE DB per Microsoft Jet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet provider for OLE DB [ADO]
- providers [ADO], OLE DB provider for Microsoft Jet
- OLE DB provider for Microsoft Jet [ADO]
ms.assetid: fd956da1-5203-40af-aa7e-fc13a6c6581f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69d88aebe25f6cfa5490cce736c05780b87eee6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926641"
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Provider Microsoft OLE DB per Microsoft Jet Panoramica
Il Provider OLE DB per Microsoft Jet consente ADO accedere ai database Microsoft Jet.

## <a name="connection-string-parameters"></a>Parametri della stringa di connessione
 Per connettersi a questo provider, impostare il *Provider* argomento delle [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà al seguente:

```vb
Microsoft.Jet.OLEDB.4.0
```

 Leggere il [Provider](../../../ado/reference/ado-api/provider-property-ado.md) proprietà restituirà anche questa stringa.

## <a name="typical-connection-string"></a>Stringa di connessione tipica
 Una stringa di connessione tipica per questo provider è:

```vb
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 La stringa è costituita da queste parole chiave:

|Parola chiave|Descrizione|
|-------------|-----------------|
|**Provider**|Specifica il Provider OLE DB per Microsoft Jet.|
|**Data Source**|Specifica il nome di percorso e il file di database (ad esempio, `c:\Northwind.mdb`).|
|**ID utente**|Specifica il nome utente. Se questa parola chiave non viene specificata, la stringa "`admin`", viene usato per impostazione predefinita.|
|**Password**|Specifica la password dell'utente. Se questa parola chiave non viene specificata, una stringa vuota (""), viene usato per impostazione predefinita.|

> [!NOTE]
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, è necessario specificare **Trusted_Connection = yes** oppure **Integrated Security = SSPI** anziché un ID utente e password informazioni nella stringa di connessione.

## <a name="provider-specific-connection-parameters"></a>Parametri di connessione specifica del provider
 Il Provider OLE DB per Microsoft Jet supporta numerose proprietà dinamiche specifiche del provider oltre a quelle definite da ADO. Come con tutti gli altri **connessione** parametri, essi possono essere impostati tramite il **delle proprietà** raccolta del **connessione** oggetto o come parte della stringa di connessione.

 Nella tabella seguente sono elencate queste proprietà insieme al nome di proprietà OLE DB corrispondente racchiuso tra parentesi.

|Parametro|Descrizione|
|---------------|-----------------|
|Quantità di spazio recuperato OLEDB:Compact Jet (DBPROP_JETOLEDB_COMPACTFREESPACESIZE)|Indica una stima della quantità di spazio, espressa in byte, che può essere recuperato dalla compressione del database. Questo valore è valido solo dopo aver stabilita una connessione al database.|
|Controllo OLEDB:Connection Jet (DBPROP_JETOLEDB_CONNECTIONCONTROL)|Indica se gli utenti possono connettersi al database.|
|Jet OLE DB: creare il Database di sistema (DBPROP_JETOLEDB_CREATESYSTEMDATABASE)|Indica se è necessario creare un database di sistema quando si crea una nuova origine dati.|
|Jet OLEDB: database la modalità di blocco (DBPROP_JETOLEDB_DATABASELOCKMODE)|Indica la modalità di blocco per questo database. Il primo utente ad aprire il database determina la modalità usata quando il database è aperto.|
|Jet OLEDB: database Password (DBPROP_JETOLEDB_DATABASEPASSWORD)|Indica la password del database.|
|Jet OLEDB: non copiare le impostazioni locali in Compact (DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE)|Indica se Jet deve copiare informazioni sulle impostazioni locali quando si compatta un database.|
|Jet OLEDB: la crittografia del Database (DBPROP_JETOLEDB_ENCRYPTDATABASE)|Indica se un database compattato deve essere crittografato. Se questa proprietà non è impostata, il database compattato verrà crittografato se il database originale è stato anche crittografato.|
|Tipo OLEDB:Engine Jet (DBPROP_JETOLEDB_ENGINE)|Indica il motore di archiviazione usato per accedere all'archivio dati corrente.|
|Jet OLEDB:Exclusive Async ritardo (DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY)|Indica la lunghezza massima di tempo, espresso in millisecondi, che Jet possono ritardare asincrone scritture su disco quando il database è aperto in modo esclusivo.<br /><br /> Questa proprietà viene ignorata a meno che **Timeout delle transazioni di Jet OLEDB: Flush** è impostato su 0.|
|Timeout della transazione Jet OLEDB: Flush (DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT)|Indica la quantità di tempo di attesa prima che i dati archiviati in una cache per la scrittura asincrona vengano effettivamente scritti sul disco. Questa impostazione sostituisce i valori per **Jet OLEDB: condiviso ritardo Async** e **Jet OLEDB:Exclusive Async ritardo**.|
|Jet OLEDB: le transazioni di blocco globale (DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS)|Indica se vengono eseguite delle operazioni bulk SQL.|
|Jet OLEDB: operazioni Bulk parziale globali (DBPROP_JETOLEDB_GLOBALBULKPARTIAL)|Indica la password utilizzata per aprire il database.|
|Jet OLEDB: sincronizzazione di Commit implicito (DBPROP_JETOLEDB_IMPLICITCOMMITSYNC)|Indica se le modifiche apportate nelle transazioni implicite interne vengono scritti in modalità sincrona o asincrona.|
|Jet OLEDB:Lock ritardo (DBPROP_JETOLEDB_LOCKDELAY)|Indica il numero di millisecondi di attesa prima di tentare di acquisire un blocco dopo un precedente tentativo non riuscito.|
|Ripetizione dei tentativi OLEDB:Lock Jet (DBPROP_JETOLEDB_LOCKRETRY)|Indica quante volte viene ripetuto un tentativo di accedere a una pagina bloccata.|
|Dimensioni del Buffer OLEDB:Max Jet (DBPROP_JETOLEDB_MAXBUFFERSIZE)|Indica la quantità massima di memoria, espressa in kilobyte, Jet possono utilizzare prima che venga avviato lo scaricamento delle modifiche su disco.|
|Jet OLEDB:Max blocchi per ogni File (DBPROP_JETOLEDB_MAXLOCKSPERFILE)|Indica il numero massimo di blocchi che Jet è possibile inserire in un database. Il valore predefinito è 9500.|
|Jet OLEDB: nuova Password del Database (DBPROP_JETOLEDB_NEWDATABASEPASSWORD)|Indica la nuova password da impostare per questo database. La vecchia password viene archiviata **Jet OLEDB: database Password**.|
|Timeout del comando di Jet OLEDB (DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT)|Indica che il numero di millisecondi prima che una query remota ODBC da Jet raggiungerà il timeout.|
|Jet OLEDB:Page blocca al blocco di tabella (DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK)|Indica il numero di pagine deve essere bloccato all'interno di una transazione prima di Jet tenta di alzare di livello il blocco a un blocco di tabella. Se questo valore è 0, il blocco non viene promossa mai.|
|Timeout OLEDB:Page Jet (DBPROP_JETOLEDB_PAGETIMEOUT)|Indica il numero di millisecondi di che attesa prima di verificare se la cache è non aggiornato con il file di database Jet.|
|Jet OLEDB:Recycle prolungata con valori di pagine (DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES)|Indica se Jet in modo aggressivo deve tentare di recuperare pagine BLOB quando vengono rese disponibili.|
|Percorso OLEDB:Registry Jet (DBPROP_JETOLEDB_REGPATH)|Indica la chiave del Registro di sistema di Windows che contiene i valori per il motore di database Jet.|
|Jet OLEDB:Reset ISAM Stats (DBPROP_JETOLEDB_RESETISAMSTATS)|Indica se lo schema **Recordset** DBSCHEMA_JETOLEDB_ISAMSTATS deve reimpostare i contatori delle prestazioni dopo la restituzione di informazioni sulle prestazioni.|
|Jet OLEDB: condiviso ritardo Async (DBPROP_JETOLEDB_SHAREDASYNCDELAY)|Indica la quantità massima di tempo, espresso in millisecondi, Jet può ritardare asincrone scritture su disco quando il database viene aperto in modalità multiutente.|
|Database di sistema OLEDB Jet (DBPROP_JETOLEDB_SYSDBPATH)|Indica il percorso e il nome del file di informazioni sul gruppo di lavoro (database di sistema).|
|Modalità di Commit OLEDB:Transaction Jet (DBPROP_JETOLEDB_TXNCOMMITMODE)|Indica se Jet scrive i dati su disco in modo sincrono o asincrono quando una transazione viene eseguito il commit.|
|Sincronizzazione di Commit OLEDB:User Jet (DBPROP_JETOLEDB_USERCOMMITSYNC)|Indica se le modifiche apportate nelle transazioni vengono scritti in modalità sincrona o asincrona.|

## <a name="provider-specific-recordset-and-command-properties"></a>Recordset specifici del provider e le proprietà dei comandi
 Il provider Jet supporta anche diverse specifiche del provider **Recordset** e **comando** proprietà. Queste proprietà sono accessibili e impostate tramite il **delle proprietà** insieme delle **Recordset** o **comando** oggetto. La tabella elenca il nome della proprietà ADO e il relativo nome di proprietà OLE DB corrispondente racchiuso tra parentesi.

|Nome proprietà|Descrizione|
|-------------------|-----------------|
|Transazioni OLEDB:Bulk Jet (DBPROP_JETOLEDB_BULKNOTRANSACTIONS)|Indica se vengono eseguite operazioni bulk SQL. Quando sottoposto a transazione, a causa di ritardi di risorse, le operazioni bulk di grandi dimensioni potrebbero non riuscire.|
|Il parametro Jet Fat Cursors (DBPROP_JETOLEDB_ENABLEFATCURSOR)|Indica se Jet deve memorizzare nella cache di più righe quando si popola un recordset per le origini di righe remoto.|
|Dimensione della Cache di cursore OLEDB:Fat Jet (DBPROP_JETOLEDB_FATCURSORMAXROWS)|Indica il numero di righe da memorizzare nella cache quando si usa la memorizzazione nella cache riga archivio dati remoto. Questo valore viene ignorato a meno che **il parametro Jet Cursors Fat** è True.|
|Jet OLEDB: incoerenti (DBPROP_JETOLEDB_INCONSISTENT)|Indica se i risultati della query consentire aggiornamenti non consistenti.|
|Jet OLEDB: blocco granularità (DBPROP_JETOLEDB_LOCKGRANULARITY)|Indica se una tabella viene aperta utilizzando il blocco a livello di riga.|
|Istruzione pass-through di Jet OLEDB (DBPROP_JETOLEDB_ODBCPASSTHROUGH)|Indica che Jet deve passare il testo SQL in un **comando** oggetto per il back-end inalterato.|
|Jet OLEDB:Partial Bulk Ops (DBPROP_JETOLEDB_BULKPARTIAL)|Indica il comportamento di Jet quando le operazioni DML SQL hanno esito negativo.|
|Jet OLEDB:Pass tramite Query Bulk-Op (DBPROP_JETOLEDB_PASSTHROUGHBULKOP)|Indica se le query che non restituiscono un **Recordset** vengono passate all'origine dati senza modifiche.|
|Stringa (DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING) di connessione OLEDB:Pass Jet tramite Query|Indica la stringa di connessione di Jet utilizzata per connettersi a un archivio dati remoto. Questo valore viene ignorato a meno che **Jet OLEDB pass-through istruzione** è True.|
|Jet OLEDB: archiviate Query (DBPROP_JETOLEDB_STOREDQUERY)|Indica se il testo del comando deve essere interpretato come una query archiviata invece un comando SQL.|
|Jet OLEDB: convalidare le regole nel Set (DBPROP_JETOLEDB_VALIDATEONSET)|Indica se le regole di convalida Jet vengono valutate quando i dati di colonna sono impostati oppure quando le modifiche vengono salvate nel database.|

 Per impostazione predefinita, il Provider OLE DB per Microsoft Jet database Microsoft Jet viene aperto in modalità lettura/scrittura. Per aprire un database in modalità sola lettura, impostare il [modalità](../../../ado/reference/ado-api/mode-property-ado.md) proprietà sull'oggetto ADO **connessione** oggetto **adModeRead**.

## <a name="command-object-usage"></a>Utilizzo dell'oggetto Command
 Testo del comando il [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto utilizzi il sottolinguaggio SQL di Microsoft Jet. È possibile specificare le query che restituiscono righe, le query di comando e i nomi di tabella nel testo del comando; Tuttavia, le stored procedure non sono supportate e non devono essere specificate.

## <a name="recordset-behavior"></a>Comportamento dell'oggetto Recordset
 Il motore di database Microsoft Jet non supporta i cursori dinamici. Pertanto, il Provider OLE DB per Microsoft Jet non supporta il **adLockDynamic** tipo di cursore. Quando viene richiesto un cursore dinamico, il provider restituisce un cursore keyset e reimpostare il [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) per indicare il tipo della proprietà [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) restituito. Inoltre, se un aggiornabile **Recordset** è richiesto (**LockType** viene **adLockOptimistic**, **adLockBatchOptimistic**, o **adLockPessimistic**) il provider verrà inoltre restituire un cursore keyset e reimpostare il **CursorType** proprietà.

## <a name="dynamic-properties"></a>Proprietà dinamiche
 Il Provider OLE DB per Microsoft Jet aggiunge numerose proprietà dinamiche nel **delle proprietà** raccolta di oggetti [connessione](../../../ado/reference/ado-api/connection-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)e [Comando](../../../ado/reference/ado-api/command-object-ado.md) oggetti.

 Le tabelle seguenti sono un incrociato dei nomi per ogni proprietà dinamica ADO e OLE DB. Riferimento dei programmatori OLE DB è relativo a un nome della proprietà ADO il termine, "Description". È possibile trovare altre informazioni su queste proprietà in riferimento OLE DB Programmer.

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
|Catalogo corrente|DBPROP_CURRENTCATALOG|
|origine dati|DBPROP_INIT_DATASOURCE|
|Nome origine dati|DBPROP_DATASOURCENAME|
|Oggetto di origine dati modello di Threading|DBPROP_DSOTHREADMODEL|
|Nome DBMS|DBPROP_DBMSNAME|
|Versione DBMS|DBPROP_DBMSVER|
|Supporto GROUP BY|DBPROP_GROUPBY|
|Supporto tabelle eterogenee|DBPROP_HETEROGENEOUSTABLES|
|Distinzione maiuscole/minuscole identificatore|DBPROP_IDENTIFIERCASE|
|Livelli di isolamento|DBPROP_SUPPORTEDTXNISOLEVELS|
|Mantenimento isolamento|DBPROP_SUPPORTEDTXNISORETAIN|
|Locale Identifier|DBPROP_INIT_LCID|
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
|Versione OLE DB|DBPROP_PROVIDEROLEDBVER|
|Supporto oggetti OLE|DBPROP_OLEOBJECTS|
|Supporto per Rowset aperto|DBPROP_OPENROWSETSUPPORT|
|Colonne ORDER BY nell'elenco di selezione|DBPROP_ORDERBYCOLUMNSINSELECT|
|Disponibilità parametro di output|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Passa per le funzioni di accesso di riferimento|DBPROP_BYREFACCESSORS|
|Password|DBPROP_AUTH_PASSWORD|
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
|Set di righe solo Accodamento|DBPROP_APPENDONLY|
|Blocca gli oggetti di archiviazione|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo di segnalibro|DBPROP_BOOKMARKTYPE|
|Supporta|DBPROP_IROWSETLOCATE|
|Segnalibri ordinati|DBPROP_ORDEREDBOOKMARKS|
|Memorizzare nella cache le colonne posticipate|DBPROP_CACHEDEFERRED|
|Modificare le righe inserite|DBPROP_CHANGEINSERTEDROWS|
|Privilegi colonna|DBPROP_COLUMNRESTRICT|
|Notifica impostazione colonna|DBPROP_NOTIFYCOLUMNSET|
|Colonna scrivibile|DBPROP_MAYWRITECOLUMN|
|Rinviare colonna|DBPROP_DEFERRED|
|Aggiornamenti degli oggetti di archiviazione di ritardo|DBPROP_DELAYSTORAGEOBJECTS|
|Recupera all'indietro|DBPROP_CANFETCHBACKWARDS|
|Contenere righe|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Righe immobili|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|Segnalibri letterali|DBPROP_LITERALBOOKMARKS|
|Identità di riga letterale|DBPROP_LITERALIDENTITY|
|Numero massimo righe aperte|DBPROP_MAXOPENROWS|
|Numero massimo righe in sospeso|DBPROP_MAXPENDINGROWS|
|Numero massimo di righe|DBPROP_MAXROWS|
|Utilizzo memoria|DBPROP_MEMORYUSAGE|
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
|Ignora segnalibri eliminati|DBPROP_BOOKMARKSKIPPED|
|Identità riga forte|DBPROP_STRONGITDENTITY|
|Aggiornabile|DBPROP_UPDATABILITY|
|Usare i segnalibri|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Proprietà dinamiche di comando
 Le proprietà seguenti vengono aggiunti per il **proprietà** insieme del **comando** oggetto.

|Nome della proprietà ADO|Nome della proprietà OLE DB|
|-----------------------|--------------------------|
|Ordine di accesso|DBPROP_ACCESSORDER|
|Set di righe solo Accodamento|DBPROP_APPENDONLY|
|Blocca gli oggetti di archiviazione|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo di segnalibro|DBPROP_BOOKMARKTYPE|
|Supporta|DBPROP_IROWSETLOCATE|
|Modificare le righe inserite|DBPROP_CHANGEINSERTEDROWS|
|Privilegi colonna|DBPROP_COLUMNRESTRICT|
|Notifica impostazione colonna|DBPROP_NOTIFYCOLUMNSET|
|Rinviare colonna|DBPROP_DEFERRED|
|Aggiornamenti degli oggetti di archiviazione di ritardo|DBPROP_DELAYSTORAGEOBJECTS|
|Recupera all'indietro|DBPROP_CANFETCHBACKWARDS|
|Contenere righe|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Righe immobili|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
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
|Dati server all'inserimento|DBPROP_SERVERDATAONINSERT|
|Ignora segnalibri eliminati|DBPROP_BOOKMARKSKIP|
|Identità riga forte|DBPROP_STRONGIDENTITY|
|Aggiornabile|DBPROP_UPDATABILITY|
|Usare i segnalibri|DBPROP_BOOKMARKS|

 Per dettagli specifici sull'implementazione e funzionale informazioni relative al Provider OLE DB per Microsoft Jet, vedere [Jet Provider](https://msdn.microsoft.com/library/windows/desktop/ms722791.aspx) nella documentazione di OLE DB.
