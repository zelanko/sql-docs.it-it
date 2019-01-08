---
title: Utilizzando più set di risultati attivi (MARS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5cbf5efeb5b5381636b57d50b86a5affa4a2595
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52401004"
---
# <a name="using-multiple-active-result-sets-mars"></a>Utilizzo di MARS (Multiple Active Result Set)
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
>  Per impostazione predefinita, la funzionalità MARS non è abilitata. Per utilizzare MARS per la connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, è necessario abilitarlo in modo specifico all'interno di una stringa di connessione. Per ulteriori informazioni, vedere le sezioni relative al provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e al driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, più avanti in questo argomento.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client non limita il numero di istruzioni attive su una connessione.  
  
 Le applicazioni tipiche che non devono eseguire contemporaneamente più stored procedure o più batch costituiti da più istruzioni trarranno vantaggio da MARS senza dovere comprendere il modo in cui MARS viene implementato, mentre le applicazioni con requisiti più complessi dovranno necessariamente comprenderne il funzionamento.  
  
 MARS consente l'esecuzione interleaved di più richieste all'interno di una sola connessione. Ovvero, consente di eseguire un batch e contestualmente di eseguire altre richieste. Notare, tuttavia, che MARS viene definito in termini di interleaving e non in termini di esecuzione parallela.  
  
 L'infrastruttura di MARS consente l'esecuzione di più batch in modo interleaved, sebbene sia possibile passare da un'esecuzione all'altra solo in specifici punti definiti. Inoltre, la maggior parte delle istruzioni deve essere eseguita automaticamente all'interno di un batch. Le istruzioni che restituiscono righe al client, che sono talvolta detti *punti specifici*, possono eseguire l'interleave di esecuzione prima del completamento durante l'invio delle righe al client, ad esempio:  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 Per tutte le altre istruzioni eseguite come parte di una stored procedure o di un batch è necessario attendere il completamento dell'esecuzione prima di potere eseguire le altre richieste MARS.  
  
 Il modo esatto in cui viene eseguito l'interleave dei batch è influenzato da una serie di fattori ed è difficile prevedere la sequenza esatta in cui vengono eseguiti i comandi da più batch contenenti specifici punti. Prestare attenzione in modo da evitare gli effetti collaterali indesiderati dovuti all'esecuzione interleaved di tali batch complessi.  
  
 Per evitare problemi, utilizzare le chiamate API anziché le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] per gestire lo stato della connessione (SET, USE) e le transazioni (BEGIN TRAN, COMMIT, ROLLBACK) senza includere queste istruzioni nei batch costituiti da più istruzioni contenenti inoltre specifici punti e serializzando l'esecuzione di tali batch utilizzando o cancellando tutti i risultati.  
  
> [!NOTE]  
>  Un batch o una stored procedure che avvia una transazione manuale o implicita quando MARS è abilitato deve completare la transazione prima di poter uscire dal batch. In caso contrario, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esegue il rollback di tutte le modifiche apportate dalla transazione al termine del batch. Tale transazione è gestita da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come transazione con ambito batch. Si tratta di un nuovo tipo di transazione introdotto in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] per consentire l'utilizzo delle stored procedure esistenti ben progettate quando MARS è abilitato. Per altre informazioni sulle transazioni con ambito batch, vedere [istruzioni Transaction &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transactions-transact-sql).  
  
 Per un esempio di utilizzo di MARS da ADO, vedere [utilizzo di ADO con SQL Server Native Client](../applications/using-ado-with-sql-server-native-client.md).  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provider OLE DB di SQL Server Native Client  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta MARS tramite l'aggiunta di SSPROP_INIT_MARSCONNECTION proprietà dell'origine dati l'inizializzazione, che viene implementata nel set di proprietà DBPROPSET_SQLSERVERDBINIT. È stata inoltre aggiunta una nuova parola chiave, `MarsConn`, per la stringa di connessione. Accetta i valori `true` o `false`. Il valore predefinito è `false`.  
  
 Il valore predefinito della proprietà dell'origine dati DBPROP_MULTIPLECONNECTIONS è VARIANT_TRUE. Ciò significa che il provider distribuirà più connessioni in modo da supportare più oggetti comando e set di righe simultanei. Quando MARS è abilitato, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client può supportare più oggetti comando e set di righe in una singola connessione, pertanto MULTIPLE_CONNECTIONS è impostato su VARIANT_FALSE per impostazione predefinita.  
  
 Per altre informazioni sui miglioramenti apportati al set di proprietà DBPROPSET_SQLSERVERDBINIT, vedere [proprietà di inizializzazione e autorizzazione](../../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
### <a name="sql-server-native-client-ole-db-provider-example"></a>Esempio di provider OLE DB di SQL Server Native Client  
 In questo esempio viene creato un oggetto origine dati usando il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB nativo e viene abilitato MARS utilizzando la proprietà DBPROPSET_SQLSERVERDBINIT prima che venga creato l'oggetto sessione.  
  
```  
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
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta MARS tramite le aggiunte per il [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) e [SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md) funzioni. SQL_COPT_SS_MARS_ENABLED è stato aggiunto per accettare SQL_MARS_ENABLED_YES o SQL_MARS_ENABLED_NO, con SQL_MARS_ENABLED_NO come impostazione predefinita. È stata inoltre aggiunta una nuova parola chiave, `Mars_Connection`, per la stringa di connessione. Accetta i valori "yes" o "no". Il valore predefinito è "no".  
  
### <a name="sql-server-native-client-odbc-driver-example"></a>Esempio di driver ODBC di SQL Server Native Client  
 In questo esempio, il **SQLSetConnectAttr** funzione viene utilizzata per abilitare MARS prima di chiamare le **SQLDriverConnect** (funzione) per connettersi al database. Una volta che viene effettuata la connessione, due **SQLExecDirect** vengono chiamate le funzioni per creare due set di risultati separati nella stessa connessione.  
  
```  
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
 [Funzionalità di SQL Server Native Client](sql-server-native-client-features.md)   
 [Uso dei set di risultati predefiniti di SQL Server](../../native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
  
