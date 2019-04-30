---
title: Supporto delle transazioni locali | Documenti di Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b75104940cca183005f8a465ea19d0a517247c25
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213819"
---
# <a name="supporting-local-transactions"></a>Supporto delle transazioni locali
  Una sessione delimita l'ambito della transazione per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transazione locale del provider OLE DB Native Client. Quando, su indicazione di un consumer, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client invia una richiesta a un'istanza connessa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la richiesta costituisce un'unità di lavoro per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client. Le transazioni locali eseguono sempre il wrapping uno o più unità di lavoro in una singola [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sessione del provider OLE DB Native Client.  
  
 Usando il valore predefinito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modalità autocommit del provider OLE DB Native Client, una singola unità di lavoro viene considerata come l'ambito di una transazione locale. Solo un unità partecipa alla transazione locale. Quando viene creata una sessione, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client inizia una transazione per la sessione. Al completamento di un'unità, viene eseguito il commit del lavoro. In caso di errore, viene eseguito il rollback di eventuali lavori iniziati e viene segnalato l'errore al consumer. In entrambi i casi il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client inizia una nuova transazione locale per la sessione in modo che tutto il lavoro viene eseguito all'interno di una transazione.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider OLE DB Native Client può indirizzare un controllo più preciso sull'ambito di transazione locale usando il **ITransactionLocal** interfaccia. Quando una sessione del consumer inizia una transazione, tutte le unità di lavoro della sessione che si trovano tra il punto di inizio della transazione e le chiamate finali al metodo **Commit** o **Abort** vengono trattate come un'unità atomica. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client inizia implicitamente una transazione quando vengono indirizzati a tale scopo dal consumer. Se il consumer non richiede la memorizzazione, la sessione ripristina il comportamento a livello di transazione padre, più comunemente la modalità AutoCommit.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta **ITransactionLocal:: StartTransaction** parametri come indicato di seguito.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*isoLevel*[in]|Il livello di isolamento da utilizzare con questa transazione. Nelle transazioni locali il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta i seguenti:<br /><br /> -ISOLATIONLEVEL_UNSPECIFIED<br />-ISOLATIONLEVEL_CHAOS<br />-   ISOLATIONLEVEL_READUNCOMMITTED<br />-ISOLATIONLEVEL_READCOMMITTED<br />-ISOLATIONLEVEL_REPEATABLEREAD<br />-   ISOLATIONLEVEL_CURSORSTABILITY<br />-ISOLATIONLEVEL_REPEATABLEREAD<br />-   ISOLATIONLEVEL_SERIALIZABLE<br />-ISOLATIONLEVEL_ISOLATED<br />-ISOLATIONLEVEL_SNAPSHOT **Nota:**  A partire [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], ISOLATIONLEVEL_SNAPSHOT è valido per il *isoLevel* argomento se il controllo delle versioni è abilitata per il database. Se tuttavia l'utente tenta di eseguire un'istruzione e il controllo delle versioni non è abilitato e/o il database non è di sola lettura, si verifica un errore. Si verifica poi l'errore XACT_E_ISOLATIONLEVEL se ISOLATIONLEVEL_SNAPSHOT è specificato come *isoLevel* ed è stata stabilita una connessione a una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedente a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|*isoFlags*[in]|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce un errore per qualsiasi valore diverso da zero.|  
|*pOtherOptions*[in]|Se non è NULL, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client richiede che l'oggetto di opzioni dall'interfaccia. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce XACT_E_NOTIMEOUT se l'oggetto di opzioni *ulTimeout* membro è diverso da zero. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client ignora il valore della *szDescription* membro.|  
|*pulTransactionLevel*[out]|Se non è NULL, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce il livello nidificato della transazione.|  
  
 Per le transazioni locali, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB Native Client provider implementa **ITransaction:: Abort** parametri come indicato di seguito.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*pboidReason*[in]|Ignorato se impostato. Può essere NULL.|  
|*fRetaining*[in]|Quando è TRUE, una nuova transazione viene iniziata implicitamente per la sessione. È necessario che il consumer esegua il commit o termini la transazione. Se è FALSE, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client Ripristina la modalità autocommit per la sessione.|  
|*fAsync*[in]|Interruzione asincrona non è supportata dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce XACT_E_NOTSUPPORTED se il valore non è FALSE.|  
  
 Per le transazioni locali, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB Native Client provider implementa **ITransaction:: commit** parametri come indicato di seguito.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*fRetaining*[in]|Quando è TRUE, una nuova transazione viene iniziata implicitamente per la sessione. È necessario che il consumer esegua il commit o termini la transazione. Se è FALSE, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client Ripristina la modalità autocommit per la sessione.|  
|*grfTC*[in]|Asincrono e restituisce una fase non sono supportati dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce XACT_E_NOTSUPPORTED per qualsiasi valore diverso da XACTTC_SYNC.|  
|*grfRM*[in]|Deve essere 0.|  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] set di righe OLE DB Native Client provider nella sessione vengono mantenuti in fase di commit locali o interrompere l'operazione in base ai valori delle proprietà set di righe DBPROP_ABORTPRESERVE e DBPROP_COMMITPRESERVE. Per impostazione predefinita, queste proprietà sono VARIANT_FALSE sia tutti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] set di righe OLE DB Native Client provider nella sessione vengono persi in seguito a un'operazione di interruzione o commit.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client non implementa le **ITransactionObject** interfaccia. Un tentativo del consumer di recuperare un riferimento dell'interfaccia restituisce E_NOINTERFACE.  
  
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
 [Transazioni](transactions.md)   
 [Uso dell'isolamento dello snapshot](../native-client/features/working-with-snapshot-isolation.md)  
  
  
