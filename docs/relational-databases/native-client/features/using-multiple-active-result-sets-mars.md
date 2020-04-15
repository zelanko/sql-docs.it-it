---
title: Uso di MARS (Multiple Active Result Set) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, MARS
- SQLNCLI, MARS
- data access [SQL Server Native Client], MARS
- Multiple Active Result Sets
- SQL Server Native Client, MARS
- MARS [SQL Server]
- SQL Server Native Client ODBC driver, MARS
ms.assetid: ecfd9c6b-7d29-41d8-af2e-89d7fb9a1d83
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fdf953bd5cb1835b2d2f6cc0e868a3687e53e852
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303210"
---
# <a name="using-multiple-active-result-sets-mars"></a>Utilizzo di MARS (Multiple Active Result Set)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] è stato introdotto il supporto di MARS (Multiple Active Result Set) nelle applicazioni che accedono al [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] le applicazioni di database non erano in grado di gestire più istruzioni attive in una connessione. Quando si utilizza il set di risultati predefinito di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'applicazione deve elaborare o annullare tutti i set di risultati da un batch prima che possa eseguire qualsiasi altro batch o connessione. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ha introdotto un nuovo attributo di connessione che consente alle applicazioni di avere più di una richiesta in sospeso per connessione e in particolare, per avere più di un set di risultati predefinito attivo per connessione.  
  
 MARS semplifica la progettazione delle applicazioni grazie alle nuove funzionalità seguenti:  
  
-   Le applicazioni possono avere più set di risultati predefiniti aperti e interfacciarsi per eseguirne la lettura.  
  
-   Le applicazioni possono eseguire altre istruzioni, ad esempio INSERT, UPDATE, DELETE e chiamate alle stored procedure, mentre sono aperti i set di risultati predefiniti.  
  
 Le applicazioni che utilizzano MARS troveranno vantaggiose le linee guida seguenti:  
  
-   I set di risultati predefiniti devono essere utilizzati per i set di risultati temporanei o i set di risultati brevi generati da singole istruzioni SQL (SELECT, DML con OUTPUT, RECEIVE, READ TEXT e così via).  
  
-   I cursori server devono essere utilizzati per i set di risultati di lunga durata o di grandi dimensioni generati da singole istruzioni SQL.  
  
-   Leggere sempre fino alla fine dei risultati per le richieste procedurali indipendentemente dalla restituzione dei risultati e per i batch che restituiscono più risultati.  
  
-   Quando possibile, utilizzare le chiamate API per modificare le proprietà di connessione e gestire le transazioni anziché le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
-   In MARS la rappresentazione con ambito sessione non è consentita durante l'esecuzione di batch simultanei.  

> [!NOTE]
> Per impostazione predefinita, la funzionalità MARS non è abilitata dal driver. Per utilizzare MARS [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ci si connette a con Native Client, è necessario abilitare in modo specifico MARS all'interno di una stringa di connessione. Tuttavia, alcune applicazioni possono abilitare MARS per impostazione predefinita, se l'applicazione rileva che il driver supporta MARS. Per queste applicazioni, è possibile disabilitare MARS nella stringa di connessione in base alle esigenze. Per ulteriori informazioni, vedere le sezioni relative al provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e al driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, più avanti in questo argomento.

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client non limita il numero di istruzioni attive su una connessione.  
  
 Le applicazioni tipiche che non devono avere più di un singolo batch con più istruzioni o l'esecuzione contemporanea di stored procedure trarranno vantaggio da MARS senza dover comprendere come viene implementato MARS. mentre le applicazioni con requisiti più complessi dovranno necessariamente comprenderne il funzionamento.  
  
 MARS consente l'esecuzione interleaved di più richieste all'interno di una sola connessione. Ovvero, consente di eseguire un batch e contestualmente di eseguire altre richieste. Notare, tuttavia, che MARS viene definito in termini di interleaving e non in termini di esecuzione parallela.  
  
 L'infrastruttura di MARS consente l'esecuzione di più batch in modo interleaved, sebbene sia possibile passare da un'esecuzione all'altra solo in specifici punti definiti. Inoltre, la maggior parte delle istruzioni deve essere eseguita automaticamente all'interno di un batch. Le istruzioni che restituiscono righe al client, a volte definite *yield point*, possono interfoliare l'esecuzione prima del completamento mentre le righe vengono inviate al client, ad esempio:  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 Per tutte le altre istruzioni eseguite come parte di una stored procedure o di un batch è necessario attendere il completamento dell'esecuzione prima di potere eseguire le altre richieste MARS.  
  
 Il modo esatto in cui viene eseguito l'interleave dei batch è influenzato da una serie di fattori ed è difficile prevedere la sequenza esatta in cui vengono eseguiti i comandi da più batch contenenti specifici punti. Prestare attenzione in modo da evitare gli effetti collaterali indesiderati dovuti all'esecuzione interleaved di tali batch complessi.  
  
 Per evitare problemi, utilizzare le chiamate API anziché le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] per gestire lo stato della connessione (SET, USE) e le transazioni (BEGIN TRAN, COMMIT, ROLLBACK) senza includere queste istruzioni nei batch costituiti da più istruzioni contenenti inoltre specifici punti e serializzando l'esecuzione di tali batch utilizzando o cancellando tutti i risultati.  
  
> [!NOTE]  
>  Un batch o una stored procedure che avvia una transazione manuale o implicita quando MARS è abilitato deve completare la transazione prima di poter uscire dal batch. In caso contrario, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esegue il rollback di tutte le modifiche apportate dalla transazione al termine del batch. Tale transazione è gestita da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come transazione con ambito batch. Si tratta di un nuovo tipo di transazione introdotto in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] per consentire l'utilizzo delle stored procedure esistenti ben progettate quando MARS è abilitato. Per altre informazioni sulle transazioni con ambito batch, vedere [Istruzioni Transaction &#40;Transact-SQL&#41;](~/t-sql/statements/statements.md).  
  
 Per un esempio di utilizzo di MARS da ADO, vedere [Utilizzo di ADO con SQL Server Native Client](../../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md).  
  
## <a name="in-memory-oltp"></a>OLTP in memoria  
 OLTP in memoria supporta MARS con query e stored procedure compilate in modo nativo. MARS consente la richiesta di dati restituiti da più query senza la necessità di recuperare completamente ogni set di risultati prima di inviare una richiesta di recupero delle righe di un nuovo set di risultati. Per leggere correttamente da più set di risultati aperti è necessario utilizzare una connessione abilitata per MARS.  
  
 Per impostazione predefinita, MARS è disabilitato. È pertanto necessario abilitarlo in modo esplicito aggiungendo `MultipleActiveResultSets=True` a una stringa di connessione. L'esempio seguente illustra come connettersi a un'istanza di SQL Server e specificare che MARS è abilitato:  
  
```  
Data Source=MSSQL; Initial Catalog=AdventureWorks; Integrated Security=SSPI; MultipleActiveResultSets=True  
```  
  
 MARS con OLTP in memoria è essenzialmente uguale a MARS nel resto del motore SQL. Di seguito sono elencate le differenze nell'uso di MARS nelle tabelle ottimizzate per la memoria e nelle stored procedure compilate in modo nativo.  
  
 **MARS e tabelle ottimizzate per la memoria**  
  
 Di seguito sono riportate le differenze tra le tabelle basate su disco e quelle ottimizzate per la memoria quando si usa una connessione abilitata per MARS:  
  
-   Due istruzioni possono modificare i dati nello stesso oggetto di destinazione, ma se entrambe tentano di modificare lo stesso record, la nuova operazione non riuscirà a causa di un conflitto di scrittura-scrittura. Tuttavia, se entrambe le operazioni modificano record diversi, le operazioni riusciranno.  
  
-   Ogni istruzione viene eseguita in isolamento SNAPSHOT, quindi le nuove operazioni non possono vedere le modifiche apportate dalle istruzioni esistenti. Anche se le istruzioni simultanee vengono eseguite nella stessa transazione, il motore SQL crea transazioni con ambito batch isolate l'una dall'altra per ogni istruzione. Le transazioni con ambito batch rimangono tuttavia associate tra loro. Di conseguenza, il rollback di una transazione con ambito batch influisce sulle altre nello stesso batch.  
  
-   Le operazioni DDL non sono consentite nelle transazioni utente e avranno esito negativo immediato.  
  
 **MARS e stored procedure compilate in modo nativo**  
  
 Le stored procedure compilate in modo nativo possono essere eseguite in connessioni abilitate per MARS e possono cedere il controllo dell'esecuzione a un'altra istruzione solo quando viene rilevato un punto specifico. Per un punto specifico è necessaria un'istruzione SELECT, ovvero l'unica all'interno di una stored procedure compilata in modo nativo che può cedere il controllo dell'esecuzione a un'altra istruzione. Se nella procedura non è presente un'istruzione SELECT, il controllo dell'esecuzione non verrà ceduto e la procedura continuerà fino al completamento prima che vengano avviate altre istruzioni.  
  
 **MARS e transazioni OLTP in memoria**  
  
 Le modifiche apportate dalle istruzioni e dai blocchi ATOMIC interleaved sono isolate l'una dall'altra. Se, ad esempio, un'istruzione o un blocco ATOMIC apporta alcune modifiche e quindi cede il controllo dell'esecuzione a un'altra istruzione, la nuova istruzione non vedrà le modifiche apportate dalla prima istruzione. Inoltre, quando la prima istruzione riprende l'esecuzione, non vedrà le modifiche apportate da altre istruzioni. Le istruzioni vedranno solo le modifiche completate e di cui è stato eseguito il commit prima dell'avvio dell'istruzione.  
  
 Una nuova transazione utente può essere avviata all'interno della transazione utente corrente utilizzando l'istruzione BEGIN TRANSACTION, supportata solo in modalità di interoperabilità, pertanto l'istruzione BEGIN TRANSACTION può essere chiamata solo da un'istruzione T-SQL e non dall'interno di una stored procedure compilata in modo nativo. È possibile creare un punto di salvataggio in una transazione usando SAVE TRANSACTION o una chiamata API alla transazione. Salvare (save_point_name) per eseguire il rollback al punto di salvataggio. Anche questa funzionalità è abilitata solo da istruzioni T-SQL e non dall'interno di stored procedure compilate in modo nativo.  
  
 **MARS e indici columnstore**  
  
 SQL Server (a partire dalla versione 2016) supporta MARS con indici columnstore. SQL Server 2014 usa MARS per le connessioni di sola lettura alle tabelle con un indice columnstore.    Tuttavia, SQL Server 2014 non supporta MARS per le operazioni simultanee di Data Manipulation Language (DML) su una tabella con indice columnstore. Quando questo si verifica, SQL Server termina le connessioni e interrompe le transazioni.   SQL Server 2012 include indici columnstore di sola lettura e MARS non è applicabile.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provider OLE DB di SQL Server Native Client  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta MARS tramite l'aggiunta della proprietà di inizializzazione dell'origine dati SSPROP_INIT_MARSCONNECTION, implementata nel set di proprietà DBPROPSET_SQLSERVERDBINIT. È stata aggiunta anche una nuova parola chiave, **MarsConn**, per la stringa di connessione. Accetta valori **true** o **false**; **false** è l'impostazione predefinita.  
  
 Il valore predefinito della proprietà dell'origine dati DBPROP_MULTIPLECONNECTIONS è VARIANT_TRUE. Ciò significa che il provider distribuirà più connessioni in modo da supportare più oggetti comando e set di righe simultanei. Quando MARS è [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] abilitato, Native Client può supportare più oggetti comando e set di righe in una singola connessione, pertanto MULTIPLE_CONNECTIONS è impostato su VARIANT_FALSE per impostazione predefinita.  
  
 Per altre informazioni sui miglioramenti apportati al set di proprietà DBPROPSET_SQLSERVERDBINIT, vedere [Proprietà di inizializzazione e di autorizzazione](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
### <a name="sql-server-native-client-ole-db-provider-example"></a>Esempio di provider OLE DB di SQL Server Native Client  
 In questo esempio, un oggetto origine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dati viene creato utilizzando il provider OLE DB nativo e MARS viene abilitato utilizzando la proprietà DBPROPSET_SQLSERVERDBINIT impostata prima della creazione dell'oggetto sessione.  
  
```cpp
#include <sqlncli.h>  
  
IDBInitialize *pIDBInitialize = NULL;  
IDBCreateSession *pIDBCreateSession = NULL;  
IDBProperties *pIDBProperties = NULL;  
  
// Create the data source object.  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL,  
   CLSCTX_INPROC_SERVER,  
   IID_IDBInitialize,   
    (void**)&pIDBInitialize);  
  
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void**)&pIDBProperties);  
  
// Set the MARS property.  
DBPROP rgPropMARS;  
  
// The following is necessary since MARS is off by default.  
rgPropMARS.dwPropertyID = SSPROP_INIT_MARSCONNECTION;  
rgPropMARS.dwOptions = DBPROPOPTIONS_REQUIRED;  
rgPropMARS.dwStatus = DBPROPSTATUS_OK;  
rgPropMARS.colid = DB_NULLID;  
V_VT(&(rgPropMARS.vValue)) = VT_BOOL;  
V_BOOL(&(rgPropMARS.vValue)) = VARIANT_TRUE;  
  
// Create the structure containing the properties.  
DBPROPSET PropSet;  
PropSet.rgProperties = &rgPropMARS;  
PropSet.cProperties = 1;  
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;  
  
// Get an IDBProperties pointer and set the initialization properties.  
pIDBProperties->SetProperties(1, &PropSet);  
pIDBProperties->Release();  
  
// Initialize the data source object.  
hr = pIDBInitialize->Initialize();  
  
//Create a session object from a data source object.  
IOpenRowset * pIOpenRowset = NULL;  
hr = IDBInitialize->QueryInterface(IID_IDBCreateSession, (void**)&pIDBCreateSession));  
hr = pIDBCreateSession->CreateSession(  
   NULL,             // pUnkOuter  
   IID_IOpenRowset,  // riid  
  &pIOpenRowset ));  // ppSession  
  
// Create a rowset with a firehose mode cursor.  
IRowset *pIRowset = NULL;  
DBPROP rgRowsetProperties[2];  
  
// To get a firehose mode cursor request a   
// forward only read only rowset.  
rgRowsetProperties[0].dwPropertyID = DBPROP_IRowsetLocate;  
rgRowsetProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[0].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[0].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[0].vValue));  
rgRowsetProperties[0].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[0].vValue.boolVal = VARIANT_FALSE;  
  
rgRowsetProperties[1].dwPropertyID = DBPROP_IRowsetChange;  
rgRowsetProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[1].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[1].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[1].vValue));  
rgRowsetProperties[1].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[1].vValue.boolVal = VARIANT_FALSE;  
  
DBPROPSET rgRowsetPropSet[1];  
rgRowsetPropSet[0].rgProperties = rgRowsetProperties  
rgRowsetPropSet[0].cProperties = 2  
rgRowsetPropSet[0].guidPropertySet = DBPROPSET_ROWSET;  
  
hr = pIOpenRowset->OpenRowset (NULL,  
   &TableID,  
   NULL,  
   IID_IRowset,  
   1,  
   rgRowsetPropSet  
   (IUnknown**)&pIRowset);  
```  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC di SQL Server Native Client  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta MARS tramite aggiunte alle funzioni [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [SQLGetConnectAttr.](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) SQL_COPT_SS_MARS_ENABLED è stato aggiunto per accettare SQL_MARS_ENABLED_YES o SQL_MARS_ENABLED_NO, con SQL_MARS_ENABLED_NO come impostazione predefinita. Inoltre, è stata aggiunta una nuova parola chiave della stringa di connessione, **Mars_Connection**, come aggiunta. Accetta i valori "yes" o "no". Il valore predefinito è "no".  
  
### <a name="sql-server-native-client-odbc-driver-example"></a>Esempio di driver ODBC di SQL Server Native Client  
 In questo esempio, la funzione **SQLSetConnectAttr** viene utilizzata per abilitare MARS prima di chiamare la funzione **SQLDriverConnect** per connettere il database. Una volta stabilita la connessione, vengono chiamate due funzioni **SQLExecDirect** per creare due set di risultati separati nella stessa connessione.  
  
```cpp
#include <sqlncli.h>  
  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_MARS_ENABLED, SQL_MARS_ENABLED_YES, SQL_IS_UINTEGER);  
SQLDriverConnect(hdbc, hwnd,   
   "DRIVER=SQL Server Native Client 10.0;  
   SERVER=(local);trusted_connection=yes;", SQL_NTS, szOutConn,   
   MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt2);  
  
// The 2nd execute would have failed with connection busy error if  
// MARS were not enabled.  
SQLExecDirect(hstmt1, L"SELECT * FROM Authors", SQL_NTS);  
SQLExecDirect(hstmt2, L"SELECT * FROM Titles", SQL_NTS);  
  
// Result set processing can interleave.  
SQLFetch(hstmt1);  
SQLFetch(hstmt2);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Utilizzo dei set di risultati predefiniti di SQL Server](../../../relational-databases/native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
  
