---
title: WillMove ed eventi MoveComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::MoveComplete
- WillMove
- MoveComplete
- Recordset::WillMove
helpviewer_keywords:
- MoveComplete event [ADO]
- WillMove event [ADO]
ms.assetid: 1a3d1042-4f30-4526-a0c7-853c242496db
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 88a04ff636f06589515f409b7c2274217ae8f3f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710020"
---
# <a name="willmove-and-movecomplete-events-ado"></a>Eventi WillMove e MoveComplete (ADO)
Il **WillMove** eventi viene chiamato prima che un'operazione in sospeso modifica la posizione corrente nel [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Il **MoveComplete** eventi viene chiamato dopo la posizione corrente nella **Recordset** le modifiche.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parametri  
 *adReason*  
 Un' [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) valore che specifica il motivo di questo evento. Il valore può essere **adRsnMoveFirst**, **adRsnMoveLast**, **adRsnMoveNext**, **adRsnMovePrevious**, **adRsnMove** , oppure **adRsnRequery**.  
  
 *pError*  
 Un' [errore](../../../ado/reference/ado-api/error-object.md) oggetto. Viene descritto l'errore generato se il valore di *adStatus* viene **adStatusErrorsOccurred**; in caso contrario, il parametro non è impostato.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore dello stato.  
  
 Quando **WillMove** viene chiamato, questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento ha esito positivo. È impostato su **adStatusCantDeny** se questo evento non è possibile richiedere l'annullamento dell'operazione in sospeso.  
  
 Quando **MoveComplete** viene chiamato, questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento ha esito positivo o a **adStatusErrorsOccurred** se la operazione non riuscita.  
  
 Prima di **WillMove** restituisce un valore di questo parametro impostato su **adStatusCancel** per richiedere l'annullamento dell'operazione in sospeso o questo parametro impostato su **adStatusUnwantedEvent** Per evitare le notifiche successivi.  
  
 Prima di **MoveComplete** restituisce un valore di questo parametro impostato su **adStatusUnwantedEvent** per evitare le notifiche successivi.  
  
 *pRecordset*  
 Oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto. Il **Recordset** per cui si è verificato questo evento.  
  
## <a name="remarks"></a>Note  
 Oggetto **WillMove** oppure **MoveComplete** evento può verificarsi a causa di quanto segue **Recordset** operazioni: [Aprire](../../../ado/reference/ado-api/open-method-ado-recordset.md), [spostare](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), e [Requery](../../../ado/reference/ado-api/requery-method.md). Questi eventi possono verificarsi a causa delle proprietà seguenti: [Filtro](../../../ado/reference/ado-api/filter-property.md), [indice](../../../ado/reference/ado-api/index-property.md), [segnalibro](../../../ado/reference/ado-api/bookmark-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), e [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md). Questi eventi si verificano anche se un elemento figlio **Recordset** ha **Recordset** eventi connessi e l'elemento padre **Recordset** viene spostato.  
  
 È necessario impostare il *adStatus* parametro per **adStatusUnwantedEvent** per ogni possibile *adReason* valore per interrompere completamente la notifica degli eventi per qualsiasi evento che include un' *adReason* parametro.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
