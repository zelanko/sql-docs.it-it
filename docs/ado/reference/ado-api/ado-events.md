---
description: Eventi ADO
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 07ef1c379dcf59b386b86d5b9fce38f77c521e01
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451423"
---
# <a name="ado-events"></a>Eventi ADO

|Event|Descrizione|  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chiamato dopo l'operazione **BeginTrans** .|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chiamato dopo l'operazione **CommitTrans** .|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Chiamato dopo l'avvio di una connessione.|  
|[Disconnetti](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Chiamato al termine di una connessione.|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|Chiamato quando viene eseguito un tentativo di spostarsi in una riga oltre la fine del **Recordset**.|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|Chiamato dopo il completamento dell'esecuzione di un comando.|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|Chiamato dopo che tutti i record di un'operazione asincrona lunga sono stati recuperati nel **Recordset**.|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|Chiamato periodicamente durante un'operazione asincrona lunga per segnalare il numero di righe attualmente recuperate nel **Recordset**.|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Chiamato dopo che il valore di uno o più oggetti **Field** è stato modificato.|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|Chiamato ogni volta che viene generato un avviso durante un'operazione **ConnectionEvent** .|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Chiamato dopo la modifica della posizione corrente nel **Recordset** .|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Chiamato dopo la modifica di uno o più record.|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Chiamato dopo che il **Recordset** è stato modificato.|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Chiamato dopo l'operazione **RollbackTrans** .|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Chiamato prima che un'operazione in sospeso modifichi il valore di uno o più oggetti **Field** nel **Recordset**.|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Chiamato prima della modifica di uno o più record (righe) nel **Recordset** .|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Chiamato prima che un'operazione in sospeso modifichi il **Recordset**.|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|Chiamato prima dell'avvio di una connessione.|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|Viene chiamato subito prima dell'esecuzione di un comando in sospeso su questa connessione e offre all'utente la possibilità di esaminare e modificare i parametri di esecuzione in sospeso.|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|L'evento **WillMove** viene chiamato *prima* che un'operazione in sospeso modifichi la posizione corrente nel **Recordset**.|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Raccolte ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Proprietà dinamiche ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Costanti enumerate ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Appendice B: errori ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Gestione degli eventi ADO](../../../ado/guide/data/handling-ado-events.md)   
 [Metodi ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Oggetti e interfacce ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Proprietà ADO](../../../ado/reference/ado-api/ado-properties.md)
