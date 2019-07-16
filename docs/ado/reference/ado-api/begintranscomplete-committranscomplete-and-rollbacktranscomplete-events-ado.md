---
title: Gli eventi di BeginTrans, CommitTrans e RollbackTrans (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommitTransComplete
- Connection::BeginTransComplete
- Connection::RollbackTransComplete
- Connection::CommitTransComplete
- RollbackTransComplete
- BeginTransComplete
helpviewer_keywords:
- CommitTransComplete event [ADO]
- RollbackTransComplete event [ADO]
- BeginTransComplete event [ADO]
ms.assetid: ec4e4b38-e9c6-4757-b2ef-4e468ae5f1d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 750e89e97eb916c7db23e71475b753a57a4d90e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920440"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete, CommitTransComplete e RollbackTransComplete (ADO)
Questi eventi verranno chiamati al termine dell'operazione associato nel [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto termina l'esecuzione.  
  
-   **BeginTransComplete** viene chiamato dopo il [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) operazione.  
  
-   **CommitTransComplete** viene chiamato dopo il [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) operazione.  
  
-   **RollbackTransComplete** viene chiamato dopo il [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) operazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parametri  
 *TransactionLevel*  
 Oggetto **lungo** valore contenente il nuovo livello di transazione delle **BeginTrans** che ha causato questo evento.  
  
 *pError*  
 Un' [errore](../../../ado/reference/ado-api/error-object.md) oggetto. Viene descritto l'errore generato se il valore di EventStatusEnum **adStatusErrorsOccurred**; in caso contrario, non è impostata.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore dello stato. Quando viene chiamato uno di questi eventi, questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento ha esito positivo o a **adStatusErrorsOccurred** se l'operazione non riuscita.  
  
 Questi eventi possono evitare le notifiche successivi impostando questo parametro su **adStatusUnwantedEvent** prima che l'evento restituito.  
  
 *pConnection*  
 Il **connessione** dell'oggetto per cui si è verificato questo evento.  
  
## <a name="remarks"></a>Note  
 In Visual C++, più **connessioni** possono condividere lo stesso evento metodo di gestione. Il metodo Usa l'oggetto restituito **connessione** oggetto per determinare quale oggetto ha causato l'evento.  
  
 Se il [attributi](../../../ado/reference/ado-api/attributes-property-ado.md) è impostata su **adXactCommitRetaining** oppure **adXactAbortRetaining**, una nuova transazione viene avviata dopo il commit o il rollback di una transazione. Usare la **BeginTransComplete** Ignora tutto dell'evento, ma il primo evento di inizio transazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans, CommitTrans e RollbackTrans (esempio di metodi (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Metodi BeginTrans, CommitTrans e RollbackTrans (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
