---
title: Utilizzando più set di risultati attivi (MARS) | Microsoft Docs
description: Utilizzo di MARS (Multiple Active Result Set)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, MARS
- MSOLEDBSQL, MARS
- data access [OLE DB Driver for SQL Server], MARS
- Multiple Active Result Sets
- OLE DB Driver for SQL Server, MARS
- MARS [SQL Server]
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 37a2a695e93d8783e6fd0c88319fed9eda55d8cd
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802868"
---
# <a name="using-multiple-active-result-sets-mars"></a>Utilizzo di MARS (Multiple Active Result Set)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

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
>  Per impostazione predefinita, la funzionalità MARS non è abilitata. Per utilizzare MARS per la connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con Driver OLE DB per SQL Server, è necessario impostarla all'interno di una stringa di connessione. Per altre informazioni, vedere il Driver OLE DB per le sezioni di SQL Server, più avanti in questo argomento.  
  
 Driver OLE DB per SQL Server non limita il numero di istruzioni attive su una connessione.  
  
 Le applicazioni tipiche che non devono eseguire contemporaneamente più stored procedure o più batch costituiti da più istruzioni trarranno vantaggio da MARS senza dovere comprendere il modo in cui MARS viene implementato, mentre le applicazioni con requisiti più complessi dovranno necessariamente comprenderne il funzionamento.  
  
 MARS consente l'esecuzione interleaved di più richieste all'interno di una sola connessione. Ovvero, consente di eseguire un batch e contestualmente di eseguire altre richieste. Notare, tuttavia, che MARS viene definito in termini di interleaving e non in termini di esecuzione parallela.  
  
 L'infrastruttura di MARS consente l'esecuzione di più batch in modo interleaved, sebbene sia possibile passare da un'esecuzione all'altra solo in specifici punti definiti. Inoltre, la maggior parte delle istruzioni deve essere eseguita automaticamente all'interno di un batch. Le istruzioni che restituiscono righe al client, definite talvolta *punti specifici* possono eseguire l'interleave dell'esecuzione prima del completamento durante l'invio delle righe al client, ad esempio:  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 Per tutte le altre istruzioni eseguite come parte di una stored procedure o di un batch è necessario attendere il completamento dell'esecuzione prima di potere eseguire le altre richieste MARS.  
  
 Il modo esatto in cui viene eseguito l'interleave dei batch è influenzato da una serie di fattori ed è difficile prevedere la sequenza esatta in cui vengono eseguiti i comandi da più batch contenenti specifici punti. Prestare attenzione in modo da evitare gli effetti collaterali indesiderati dovuti all'esecuzione interleaved di tali batch complessi.  
  
 Per evitare problemi, utilizzare le chiamate API anziché le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] per gestire lo stato della connessione (SET, USE) e le transazioni (BEGIN TRAN, COMMIT, ROLLBACK) senza includere queste istruzioni nei batch costituiti da più istruzioni contenenti inoltre specifici punti e serializzando l'esecuzione di tali batch utilizzando o cancellando tutti i risultati.  
  
> [!NOTE]  
>  Un batch o una stored procedure che avvia una transazione manuale o implicita quando MARS è abilitato deve completare la transazione prima di poter uscire dal batch. In caso contrario, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esegue il rollback di tutte le modifiche apportate dalla transazione al termine del batch. Tale transazione è gestita da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come transazione con ambito batch. Si tratta di un nuovo tipo di transazione introdotto in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] per consentire l'utilizzo delle stored procedure esistenti ben progettate quando MARS è abilitato. Per altre informazioni sulle transazioni con ambito batch, vedere [istruzioni Transaction &#40;Transact-SQL&#41;](../../../t-sql/statements/statements.md).  
  
 Per un esempio di utilizzo di MARS da ADO, vedere [utilizzo di ADO con il Driver OLE DB per SQL Server](../../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
## <a name="in-memory-oltp"></a>OLTP in memoria  
 OLTP in memoria supporta MARS tramite query e stored procedure compilate in modo nativo. MARS consente richiedendo dati a più query senza la necessità di recuperare completamente ogni set prima di inviare una richiesta per recuperare le righe da un nuovo set di risultati di risultati. Per leggere correttamente da più set di risultati aperti, è necessario utilizzare una connessione MARS abilitato.  
  
 MARS è disabilitato per impostazione predefinita, pertanto è necessario abilitare in modo esplicito aggiungendo `MultipleActiveResultSets=True` a una stringa di connessione. Nell'esempio seguente viene illustrato come connettersi a un'istanza di SQL Server e specificare che è abilitato MARS:  
  
```  
Data Source=MSSQL; Initial Catalog=AdventureWorks; Integrated Security=SSPI; MultipleActiveResultSets=True  
```  
  
 MARS con OLTP In memoria corrisponde essenzialmente come MARS nella parte rimanente del motore SQL. Di seguito sono elencate le differenze quando si utilizza MARS nelle tabelle ottimizzate per la memoria e in modo nativo stored procedure compilate.  
  
 **Le tabelle ottimizzate per la memoria e MARS**  
  
 Di seguito è le differenze tra le tabelle basate su disco e ottimizzate per la memoria quando si utilizza un MARS abilitato connessione:  
  
-   Due istruzioni possono modificare i dati nello stesso oggetto di destinazione, ma se entrambi provano a modificare lo stesso record di un conflitto di scrittura-scrittura causerà l'operazione di nuovo esito negativo. Tuttavia, se entrambe le operazioni di modificano record diversi, le operazioni avrà esito positivo.  
  
-   Ogni istruzione viene eseguita nell'isolamento dello SNAPSHOT in modo che le nuove operazioni non è possibile visualizzare le modifiche apportate dalle istruzioni esistente. Anche se vengono eseguite le istruzioni simultanee nella stessa transazione il motore SQL consente di creare transazioni con ambito batch per ogni istruzione che sono isolate tra loro. Le transazioni con ambito batch, tuttavia, sono ancora associate insieme in modo da eseguire il rollback di una transazione con ambito batch influisce su altri registri nello stesso batch.  
  
-   Operazioni DDL non sono consentite nelle transazioni utente in modo che hanno immediatamente esito negativo.  
  
 **MARS e stored procedure compilate in modo nativo**  
  
 Le stored procedure compilate in modo nativo possono essere eseguiti in connessioni MARS abilitato e possono essere eseguito in un'altra istruzione solo quando viene rilevato un punto di sospensione. Un punto di sospensione richiede un'istruzione SELECT, che è l'unica istruzione in una stored procedure compilata in modo nativo che può essere eseguito in un'altra istruzione. Se un'istruzione SELECT non è presente nella routine che non produrrà, verrà eseguito fino al completamento prima di iniziano le altre istruzioni.  
  
 **Transazioni OLTP In memoria e MARS**  
  
 Le modifiche apportate dalle informative e i blocchi atomici che sono di tipo interleaved sono isolate tra loro. Ad esempio, se un'istruzione o un blocco atomic apporta alcune modifiche e quindi restituisce l'esecuzione di un'altra istruzione, la nuova istruzione non vedranno le modifiche apportate dalla prima istruzione. Inoltre, quando la prima istruzione riprende l'esecuzione, non rileverà eventuali modifiche apportate da tutte le altre istruzioni. Le istruzioni visualizzate solo le modifiche che sono completate e commit eseguite prima dell'avvio dell'istruzione.  
  
 Una nuova transazione utente può essere avviata all'interno della transazione utente corrente usando l'istruzione BEGIN TRANSACTION: questo è supportato solo in modalità di interoperabilità in modo che l'istruzione BEGIN TRANSACTION può essere chiamato solo da un'istruzione T-SQL e non da all'interno di un compilate in modo nativo stored procedura. È possibile creare un salvataggio scegliere in una transazione con transazioni di salvare o una chiamata API a transazione. Save(save_point_name) per eseguire il rollback del punto di salvataggio. Questa funzionalità è abilitata solo da istruzioni T-SQL e non da all'interno di alle stored procedure compilate.  
  
 **Gli indici columnstore e MARS**  
  
 SQL Server (a partire da 2016) supporta MARS con indici columnstore. SQL Server 2014 usa MARS per le connessioni di sola lettura alle tabelle con un indice columnstore.    Tuttavia, SQL Server 2014 non supporta MARS per le operazioni simultanee di Data Manipulation Language (DML) su una tabella con indice columnstore. Quando questo si verifica, SQL Server termina le connessioni e interrompe le transazioni.   SQL Server 2012 con gli indici columnstore di sola lettura e MARS non è applicabile ad essi.  
  
## <a name="ole-db-driver-for-sql-server"></a>Driver OLE DB per SQL Server  
 Il driver OLE DB per SQL Server supporta MARS tramite l'aggiunta della proprietà di inizializzazione dell'origine dati SSPROP_INIT_MARSCONNECTION, implementata nel set di proprietà DBPROPSET_SQLSERVERDBINIT. È stata aggiunta anche una nuova parola chiave, **MarsConn**, per la stringa di connessione. Accetta **true** oppure **false** valori; **false** è il valore predefinito.  
  
 Il valore predefinito della proprietà dell'origine dati DBPROP_MULTIPLECONNECTIONS è VARIANT_TRUE. Ciò significa che il provider distribuirà più connessioni in modo da supportare più oggetti comando e set di righe simultanei. Quando MARS è abilitato, il driver OLE DB per SQL Server può supportare più oggetti comando e set di righe in una singola connessione, pertanto MULTIPLE_CONNECTIONS è impostato su VARIANT_FALSE per impostazione predefinita.  
  
 Per altre informazioni sui miglioramenti apportati al set di proprietà DBPROPSET_SQLSERVERDBINIT, vedere [proprietà di inizializzazione e autorizzazione](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
### <a name="ole-db-driver-for-sql-server-example"></a>Esempio del driver OLE DB per SQL Server  
 In questo esempio viene creato un oggetto origine dati usando il driver OLE DB per SQL Server e viene abilitato MARS usando il set di proprietà DBPROPSET_SQLSERVERDBINIT prima che venga creato l'oggetto della sessione.  
  
```  
#include <msoledbsql.h>  
  
IDBInitialize *pIDBInitialize = NULL;  
IDBCreateSession *pIDBCreateSession = NULL;  
IDBProperties *pIDBProperties = NULL;  
  
// Create the data source object.  
hr = CoCreateInstance(CLSID_MSOLEDBSQL, NULL,  
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

  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per funzionalità di SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 
  
  
