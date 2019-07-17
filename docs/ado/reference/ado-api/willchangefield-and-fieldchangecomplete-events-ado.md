---
title: Eventi WillChangeField e FieldChangeComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldChangeComplete
- Recordset::WillChangeField
- Recordset::FieldChangeComplete
- WillChangeField
helpviewer_keywords:
- WillChangeField event [ADO]
- fieldchangecomplete event [ADO]
ms.assetid: 3e49fb89-c45b-4d39-823e-3cc887c59b37
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7484e2a57925cc22c83456c244dc67aded5cefd2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945887"
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>Eventi WillChangeField e FieldChangeComplete (ADO)
Il **WillChangeField** eventi viene chiamato prima che un'operazione in sospeso viene modificato il valore di uno o più [campo](../../../ado/reference/ado-api/field-object.md) oggetti il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Il **FieldChangeComplete** eventi viene chiamato dopo il valore di uno o più **campo** oggetti è stato modificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parametri  
 *cFields*  
 Oggetto **lungo** che indica il numero di **campo** gli oggetti nello *campi*.  
  
 *Fields*  
 Per la **WillChangeField**, il *campi* parametro è una matrice di **varianti** contenente **campo** oggetti con i valori originali. Per la **FieldChangeComplete**, il *campi* parametro è una matrice di **varianti** contenente **campo** oggetti con i valori modificati .  
  
 *pError*  
 Un' [errore](../../../ado/reference/ado-api/error-object.md) oggetto. Viene descritto l'errore generato se il valore di *adStatus* viene **adStatusErrorsOccurred**; in caso contrario, non è impostata.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore dello stato.  
  
 Quando **WillChangeField** viene chiamato, questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento ha esito positivo. È impostato su **adStatusCantDeny** se questo evento non è possibile richiedere l'annullamento dell'operazione in sospeso.  
  
 Quando **FieldChangeComplete** viene chiamato, questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento ha esito positivo o a **adStatusErrorsOccurred** se l'operazione non riuscita.  
  
 Prima di **WillChangeField** restituisce un valore di questo parametro impostato su **adStatusCancel** per richiedere l'annullamento dell'operazione in sospeso.  
  
 Prima di **FieldChangeComplete** restituisce un valore di questo parametro impostato su **adStatusUnwantedEvent** per evitare le notifiche successivi.  
  
 *pRecordset*  
 Oggetto **Recordset** oggetto. Il **Recordset** per cui si è verificato questo evento.  
  
## <a name="remarks"></a>Note  
 Oggetto **WillChangeField** o **FieldChangeComplete** evento può verificarsi quando si imposta la [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà e la chiamata il [Update](../../../ado/reference/ado-api/update-method.md) (metodo) con i parametri di matrice campo e il valore.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)
