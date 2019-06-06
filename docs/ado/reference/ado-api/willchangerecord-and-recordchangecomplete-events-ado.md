---
title: Eventi WillChangeRecord e RecordChangeComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ef2e02ec156aeed69089a585d743e16e592eb95f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710153"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>Eventi WillChangeRecord e RecordChangeComplete (ADO)
Il **WillChangeRecord** eventi viene chiamato prima uno o più record (righe) [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) modificare. Il **RecordChangeComplete** eventi viene chiamato dopo che uno o più record di modifica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parametri  
 *adReason*  
 Un' [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) valore che specifica il motivo di questo evento. Il valore può essere **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**, o **adRsnFirstChange**.  
  
 *cRecords*  
 Oggetto **lungo** valore che indica il numero di record di modifica (interessato).  
  
 *pError*  
 Un' [errore](../../../ado/reference/ado-api/error-object.md) oggetto. Viene descritto l'errore generato se il valore di *adStatus* viene **adStatusErrorsOccurred**; in caso contrario, non è impostata.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore dello stato.  
  
 Quando **WillChangeRecord** viene chiamato, questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento ha esito positivo. È impostato su **adStatusCantDeny** se questo evento non è possibile richiedere l'annullamento dell'operazione in sospeso.  
  
 Quando **RecordChangeComplete** viene chiamato, questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento ha esito positivo o a **adStatusErrorsOccurred** se l'operazione non riuscita.  
  
 Prima di **WillChangeRecord** restituisce un valore di questo parametro impostato su **adStatusCancel** per richiedere l'annullamento dell'operazione che ha causato questo evento o imposta questo parametro su  **adStatusUnwantedEvent** per evitare le notifiche successivi.  
  
 Prima di **RecordChangeComplete** restituisce un valore di questo parametro impostato su **adStatusUnwantedEvent** per evitare le notifiche successivi.  
  
 *pRecordset*  
 Oggetto **Recordset** oggetto. Il **Recordset** per cui si è verificato questo evento.  
  
## <a name="remarks"></a>Note  
 Oggetto **WillChangeRecord** oppure **RecordChangeComplete** evento può verificarsi per il primo campo modificato in una riga a causa di quanto segue **Recordset** operazioni: [Update](../../../ado/reference/ado-api/update-method.md), [eliminare](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), e [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md). Il valore della **Recordset** [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) determina le operazioni che causano il verificarsi degli eventi.  
  
 Durante la **WillChangeRecord** evento, il **Recordset** [filtro](../../../ado/reference/ado-api/filter-property.md) è impostata su **adFilterAffectedRecords**. È possibile modificare questa proprietà durante l'elaborazione dell'evento.  
  
 È necessario impostare il **adStatus** parametro per **adStatusUnwantedEvent** per ogni possibile **adReason** valore per arrestare completamente la notifica degli eventi per qualsiasi evento che include un' **adReason** parametro.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)
