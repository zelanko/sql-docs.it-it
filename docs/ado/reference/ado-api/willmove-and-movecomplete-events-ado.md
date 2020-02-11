---
title: Eventi WillMove e MoveComplete (ADO) | Microsoft Docs
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
ms.openlocfilehash: c91f3166b493ac1e2fada3e759cb107e34c7ca81
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67945916"
---
# <a name="willmove-and-movecomplete-events-ado"></a>Eventi WillMove e MoveComplete (ADO)
L'evento **WillMove** viene chiamato prima che un'operazione in sospeso modifichi la posizione corrente nel [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). L'evento **MoveComplete** viene chiamato dopo la modifica della posizione corrente nel **Recordset** .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parametri  
 *adReason*  
 Valore [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) che specifica il motivo di questo evento. Il valore può essere **adRsnMoveFirst**, **adRsnMoveLast**, **adRsnMoveNext**, **adRsnMovePrevious**, **adRsnMove**o **adRsnRequery**.  
  
 *pError*  
 Oggetto [Error](../../../ado/reference/ado-api/error-object.md) . Viene descritto l'errore che si è verificato se il valore di *adStatus* è **adStatusErrorsOccurred**; in caso contrario, il parametro non è impostato.  
  
 *adStatus*  
 Valore di stato di [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) .  
  
 Quando viene chiamato **WillMove** , questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento è riuscita. Viene impostato su **adStatusCantDeny** se questo evento non può richiedere l'annullamento dell'operazione in sospeso.  
  
 Quando viene chiamato **MoveComplete** , questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento è stata eseguita correttamente oppure su **adStatusErrorsOccurred** se l'operazione non è riuscita.  
  
 Prima della restituzione di **WillMove** , impostare questo parametro su **adStatusCancel** per richiedere l'annullamento dell'operazione in sospeso oppure impostare questo parametro su **adStatusUnwantedEvent** per impedire le notifiche successive.  
  
 Prima della restituzione di **MoveComplete** , impostare questo parametro su **adStatusUnwantedEvent** per impedire le notifiche successive.  
  
 *pRecordset*  
 Oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) . **Recordset** per il quale si è verificato l'evento.  
  
## <a name="remarks"></a>Osservazioni  
 Un evento **WillMove** o **MoveComplete** può verificarsi a causa delle operazioni **Recordset** seguenti: [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Move](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)e [Requery](../../../ado/reference/ado-api/requery-method.md). Questi eventi possono verificarsi a causa delle proprietà seguenti: [Filter](../../../ado/reference/ado-api/filter-property.md), [index](../../../ado/reference/ado-api/index-property.md), [Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)e [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md). Questi eventi si verificano anche se un **Recordset** figlio contiene eventi **Recordset** connessi e il **Recordset** padre viene spostato.  
  
 È necessario impostare il parametro *adStatus* su **adStatusUnwantedEvent** per ogni possibile valore *adReason* per arrestare completamente la notifica degli eventi per qualsiasi evento che includa un parametro *adReason* .  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo del gestore eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
