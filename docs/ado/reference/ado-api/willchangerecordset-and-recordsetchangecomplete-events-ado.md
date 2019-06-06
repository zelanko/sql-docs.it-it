---
title: Eventi WillChangeRecordset e RecordsetChangeComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::RecordsetChangeComplete
- RecordsetChangeComplete
- Recordset::WillChangeRecordset
- WillChangeRecordset
helpviewer_keywords:
- RecordsetChangeComplete event [ADO]
- WillChangeRecordset event [ADO]
ms.assetid: d5d44659-e0d9-46d9-a297-99c43555082f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c5ca84c5759523bf17c4e047b22cafbd48dce547
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710069"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>Eventi WillChangeRecordset e RecordsetChangeComplete (ADO)
Il **WillChangeRecordset** eventi viene chiamato prima che un'operazione in sospeso viene modificato il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Il **RecordsetChangeComplete** eventi viene chiamato dopo la **Recordset** è stato modificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parametri  
 *adReason*  
 Un' [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) valore che specifica il motivo di questo evento. Il valore può essere **adRsnRequery**, **adRsnResynch**, **adRsnClose**, **o adRsnOpen**.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore dello stato.  
  
 Quando **WillChangeRecordset** viene chiamato, questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento ha esito positivo. È impostato su **adStatusCantDeny** se questo evento non è possibile richiedere l'annullamento dell'operazione in sospeso.  
  
 Quando **RecordsetChangeComplete** viene chiamato, questo parametro è impostato su **adStatusOK** se è stata completata correttamente, l'operazione che ha causato l'evento **adStatusErrorsOccurred** se l'operazione non è riuscita, oppure **adStatusCancel** se l'operazione associata accettate in precedenza **WillChangeRecordset** evento è stato annullato.  
  
 Prima di **WillChangeRecordset** restituisce un valore di questo parametro impostato su **adStatusCancel** per richiedere l'annullamento dell'operazione in sospeso o impostare questo parametro su adStatusUnwantedEvent per evitare successivi notifiche.  
  
 Prima di **WillChangeRecordset** oppure **RecordsetChangeComplete** restituisce un valore, impostare questo parametro **adStatusUnwantedEvent** per evitare le notifiche successivi.  
  
 *pError*  
 Un' [errore](../../../ado/reference/ado-api/error-object.md) oggetto. Viene descritto l'errore generato se il valore di *adStatus* viene **adStatusErrorsOccurred**; in caso contrario, non è impostata.  
  
 *pRecordset*  
 Oggetto **Recordset** oggetto. Il **Recordset** per cui si è verificato questo evento.  
  
## <a name="remarks"></a>Note  
 Oggetto **WillChangeRecordset** o **RecordsetChangeComplete** evento può verificarsi a causa della **Recordset** [Requery](../../../ado/reference/ado-api/requery-method.md) o[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodi.  
  
 Se il provider non supporta i segnalibri, un **RecordsetChange viene generata** notifica degli eventi si verifica ogni volta che le nuove righe vengono recuperate dal provider. La frequenza dell'evento dipende il **RecordsetCacheSize** proprietà.  
  
 È necessario impostare il **adStatus** parametro per **adStatusUnwantedEvent** per ogni possibile **adReason** valore per arrestare completamente la notifica degli eventi per qualsiasi evento che include un' **adReason** parametro.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)
