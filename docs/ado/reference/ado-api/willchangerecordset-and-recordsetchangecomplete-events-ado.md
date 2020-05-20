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
author: rothja
ms.author: jroth
ms.openlocfilehash: 90bfb1c947c02540d07c3cbc11e45436f8bd4a58
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764472"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>Eventi WillChangeRecordset e RecordsetChangeComplete (ADO)
L'evento **WillChangeRecordset** viene chiamato prima che un'operazione in sospeso modifichi il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). L'evento **RecordsetChangeComplete** viene chiamato dopo che il **Recordset** è stato modificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parametri  
 *adReason*  
 Valore [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) che specifica il motivo di questo evento. Il valore può essere **adRsnRequery**, **adRsnResynch**, **adRsnClose**, **adRsnOpen**.  
  
 *adStatus*  
 Valore di stato di [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) .  
  
 Quando viene chiamato **WillChangeRecordset** , questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento è riuscita. Viene impostato su **adStatusCantDeny** se questo evento non può richiedere l'annullamento dell'operazione in sospeso.  
  
 Quando viene chiamato **RecordsetChangeComplete** , questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento è riuscita, **adStatusErrorsOccurred** se l'operazione ha esito negativo o **AdStatusCancel** se l'operazione associata all'evento **WillChangeRecordset** precedentemente accettato è stata annullata.  
  
 Prima della restituzione di **WillChangeRecordset** , impostare questo parametro su **adStatusCancel** per richiedere l'annullamento dell'operazione in sospeso o impostare questo parametro su adStatusUnwantedEvent per impedire le notifiche successive.  
  
 Prima della restituzione di **WillChangeRecordset** o **RecordsetChangeComplete** , impostare questo parametro su **adStatusUnwantedEvent** per impedire le notifiche successive.  
  
 *pError*  
 Oggetto [Error](../../../ado/reference/ado-api/error-object.md) . Viene descritto l'errore che si è verificato se il valore di *adStatus* è **adStatusErrorsOccurred**; in caso contrario, non è impostato.  
  
 *pRecordset*  
 Oggetto **Recordset** . **Recordset** per il quale si è verificato l'evento.  
  
## <a name="remarks"></a>Commenti  
 È possibile che si verifichi un evento **WillChangeRecordset** o **RecordsetChangeComplete** a causa della [Requery](../../../ado/reference/ado-api/requery-method.md) o dei metodi [aperti](../../../ado/reference/ado-api/open-method-ado-recordset.md) del **Recordset** .  
  
 Se il provider non supporta i segnalibri, viene generata una notifica di evento **RecordsetChange** ogni volta che le nuove righe vengono recuperate dal provider. La frequenza di questo evento dipende dalla proprietà **RecordsetCacheSize** .  
  
 È necessario impostare il parametro **adStatus** su **adStatusUnwantedEvent** per ogni possibile valore **adReason** per arrestare completamente la notifica degli eventi per qualsiasi evento che includa un parametro **adReason** .  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)
