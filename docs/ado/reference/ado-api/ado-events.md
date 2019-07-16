---
title: Eventi ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
ms.assetid: 0ded5ad9-8f83-4224-95af-38512783b972
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 35169313ae487514403f62c8e6d1ba2c262cb8a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921002"
---
# <a name="ado-events"></a>Eventi ADO

|||  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chiamato dopo il **BeginTrans** operazione.|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chiamato dopo il **CommitTrans** operazione.|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Chiamato dopo l'avvio di una connessione.|  
|[Disconnetti](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Chiamato dopo la fine di una connessione.|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|Chiamato quando viene eseguito un tentativo per spostarsi in una riga successiva alla fine del **Recordset**.|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|Chiamato dopo l'esecuzione di un comando è terminata.|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|Chiamato dopo che sono stati recuperati tutti i record in un'operazione di lunga durata asincrona nel **Recordset**.|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|Viene chiamato periodicamente durante un'operazione asincrona lunga per segnalare il numero di righe attualmente recuperato nel **Recordset**.|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Chiamato dopo che il valore di uno o più **campo** oggetti è stato modificato.|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|Chiamato ogni volta che viene generato un avviso durante una **ConnectionEvent** operazione.|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Chiamato dopo la posizione corrente nella **Recordset** le modifiche.|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Chiamato dopo la modifica di uno o più record.|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Chiamato dopo il **Recordset** è stato modificato.|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chiamato dopo il **RollbackTrans** operazione.|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Chiamato prima che un'operazione in sospeso viene modificato il valore di uno o più **campo** gli oggetti di **Recordset**.|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Chiamato prima di uno o più record (righe) nei **Recordset** modificare.|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Chiamato prima che un'operazione in sospeso viene modificato il **Recordset**.|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|Chiamato prima dell'avvio di una connessione.|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|Chiamato poco prima che un comando in sospeso viene eseguita sulla connessione e offre all'utente un'opportunità per esaminare e modificare i parametri di esecuzione in sospeso.|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Il **WillMove** eventi viene chiamato *prima* un'operazione in sospeso modifica la posizione corrente nel **Recordset**.|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Raccolte di ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Proprietà dinamiche ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Costanti enumerate ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Appendice B: Errori ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Gestione degli eventi ADO](../../../ado/guide/data/handling-ado-events.md)   
 [Metodi ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfacce e oggetti ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Proprietà ADO](../../../ado/reference/ado-api/ado-properties.md)
