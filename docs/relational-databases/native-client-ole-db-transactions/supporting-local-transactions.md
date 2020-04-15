---
title: Supporto delle transazioni locali | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- SQL Server Native Client OLE DB provider, transactions
- local transactions [OLE DB]
ms.assetid: 78f2e5fc-b6fb-4eda-9f71-991a4d6c4902
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8533747bbe5ccb79a06b10a754c4af45ab241843
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280204"
---
# <a name="supporting-local-transactions"></a>Supporto delle transazioni locali
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Una sessione delimita l'ambito della transazione per una transazione locale del provider OLE DB di Native Client.A session dellimits transaction scope for a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider local transaction. Quando, nella direzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un consumer, il provider OLE DB Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Client invia una richiesta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un'istanza connessa di , la richiesta costituisce un'unità di lavoro per il provider OLE DB Native Client. Le transazioni locali eseguono sempre il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wrapping di una o più unità di lavoro in una singola sessione del provider OLE DB di Native Client.Local transactions always wrap one or more units of work on a single Native Client OLE DB provider session.  
  
 Utilizzando la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modalità autocommit del provider OLE DB Native Client predefinita, una singola unità di lavoro viene considerata come l'ambito di una transazione locale. Solo un unità partecipa alla transazione locale. Quando viene creata una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sessione, il provider OLE DB Native Client inizia una transazione per la sessione. Al completamento di un'unità, viene eseguito il commit del lavoro. In caso di errore, viene eseguito il rollback di eventuali lavori iniziati e viene segnalato l'errore al consumer. In entrambi i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] casi, il provider OLE DB Native Client inizia una nuova transazione locale per la sessione in modo che tutto il lavoro venga eseguito all'interno di una transazione.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider OLE DB Native Client può indirizzare un controllo più preciso sull'ambito delle transazioni locali utilizzando l'interfaccia **ITransactionLocal.** Quando una sessione del consumer inizia una transazione, tutte le unità di lavoro della sessione che si trovano tra il punto di inizio della transazione e le chiamate finali al metodo **Commit** o **Abort** vengono trattate come un'unità atomica. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client avvia in modo implicito una transazione quando viene richiesto dal consumer. Se il consumer non richiede la memorizzazione, la sessione ripristina il comportamento a livello di transazione padre, più comunemente la modalità AutoCommit.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta i parametri **ITransactionLocal::StartTransaction** come indicato di seguito.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*isoLevel*[in]|Il livello di isolamento da utilizzare con questa transazione. Nelle transazioni locali, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta quanto segue:<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> Nota: a partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], ISOLATIONLEVEL_SNAPSHOT è valido per l'argomento *isoLevel* indipendentemente dall'abilitazione del controllo delle versioni per il database. Se tuttavia l'utente tenta di eseguire un'istruzione e il controllo delle versioni non è abilitato e/o il database non è di sola lettura, si verifica un errore. Si verifica poi l'errore XACT_E_ISOLATIONLEVEL se ISOLATIONLEVEL_SNAPSHOT è specificato come *isoLevel* ed è stata stabilita una connessione a una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedente a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|*isoFlags*[in]|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce un errore per qualsiasi valore diverso da zero.|  
|*pOtherOptions*[in]|Se non NULL, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client richiede l'oggetto options dall'interfaccia. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce XACT_E_NOTIMEOUT se il membro *ulTimeout* dell'oggetto opzioni non è zero. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client ignora il valore del membro *szDescription.*|  
|*pulTransactionLevel*[out]|Se non NULL, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce il livello annidato della transazione.|  
  
 Per le transazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] locali, il provider OLE DB Native Client implementa i parametri **ITransaction::Abort** come indicato di seguito.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*pboidReason*[in]|Ignorato se impostato. Può essere NULL.|  
|*fRetaining*[in]|Quando è TRUE, una nuova transazione viene iniziata implicitamente per la sessione. È necessario che il consumer esegua il commit o termini la transazione. Quando FALSE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il provider OLE DB Native Client torna alla modalità di commit automatico per la sessione.|  
|*fAsync*[in]|L'interruzione asincrona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è supportata dal provider OLE DB Native Client. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce XACT_E_NOTSUPPORTED se il valore non è FALSE.|  
  
 Per le transazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] locali, il provider OLE DB Native Client implementa i parametri **ITransaction::Commit** come indicato di seguito.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*fRetaining*[in]|Quando è TRUE, una nuova transazione viene iniziata implicitamente per la sessione. È necessario che il consumer esegua il commit o termini la transazione. Quando FALSE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il provider OLE DB Native Client torna alla modalità di commit automatico per la sessione.|  
|*grfTC*[in]|I valori asincroni e di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fase uno non sono supportati dal provider OLE DB di Native Client. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce XACT_E_NOTSUPPORTED per qualsiasi valore diverso da XACTTC_SYNC.|  
|*grfRM*[in]|Deve essere 0.|  
  
 I [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] set di righe del provider OLE DB Native Client nella sessione vengono mantenuti in un'operazione di commit o interruzione locale in base ai valori delle proprietà del set di righe DBPROP_ABORTPRESERVE e DBPROP_COMMITPRESERVE. Per impostazione predefinita, queste [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proprietà sono sia VARIANT_FALSE e tutti i set di righe del provider OLE DB Native Client nella sessione vengono persi dopo un'operazione di interruzione o commit.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client non implementa l'interfaccia **ITransactionObject.** Un tentativo del consumer di recuperare un riferimento dell'interfaccia restituisce E_NOINTERFACE.  
  
 Questo esempio usa **ITransactionLocal**.  
  
```  
// Interfaces used in the example.  
IDBCreateSession*   pIDBCreateSession   = NULL;  
ITransaction*       pITransaction       = NULL;  
IDBCreateCommand*   pIDBCreateCommand   = NULL;  
IRowset*            pIRowset            = NULL;  
  
HRESULT             hr;  
  
// Get the command creation and local transaction interfaces for the  
// session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
if (FAILED(hr = pIDBCreateCommand->QueryInterface(IID_ITransactionLocal,  
    (void**) &pITransaction)))  
    {  
    // Process error. Release any references and return.  
    }  
  
// Start the local transaction.  
if (FAILED(hr = ((ITransactionLocal*) pITransaction)->StartTransaction(  
    ISOLATIONLEVEL_REPEATABLEREAD, 0, NULL, NULL)))  
    {  
    // Process error from StartTransaction. Release any references and  
    // return.  
    }  
  
// Get data into a rowset, then update the data. Functions are not  
// illustrated in this example.  
if (FAILED(hr = ExecuteCommand(pIDBCreateCommand, &pIRowset)))  
    {  
    // Release any references and return.  
    }  
  
// If rowset data update fails, then terminate the transaction, else  
// commit. The example doesn't retain the rowset.  
if (FAILED(hr = UpdateDataInRowset(pIRowset, bDelayedUpdate)))  
    {  
    // Get error from update, then terminate.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, XACTTC_SYNC, 0)))  
        {  
        // Get error from failed commit.  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Transazioni](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [Utilizzo dell'isolamento dello snapshot](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
  
  
