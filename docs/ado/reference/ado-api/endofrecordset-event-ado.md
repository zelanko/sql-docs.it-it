---
title: Evento EndOfRecordset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords:
- EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 414094da95076a7fb3781877645c5d43a03e6a7f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698213"
---
# <a name="endofrecordset-event-ado"></a>Evento EndOfRecordset (ADO)
Il **EndOfRecordset** eventi viene chiamato quando viene eseguito un tentativo per spostarsi in una riga successiva alla fine del [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parametri  
 *fMoreData*  
 Oggetto **VARIANT_BOOL** valore che, se impostata su VARIANT_TRUE, indica più righe sono stati aggiunti per il **Recordset**.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore dello stato.  
  
 Quando **EndOfRecordset** viene chiamato, questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento ha esito positivo. È impostato su **adStatusCantDeny** se questo evento non è possibile richiedere l'annullamento dell'operazione che ha causato questo evento.  
  
 Prima di **EndOfRecordset** restituisce un valore di questo parametro impostato su **adStatusUnwantedEvent** per evitare le notifiche successivi.  
  
 *pRecordset*  
 Oggetto **Recordset** oggetto. Il **Recordset** per cui si è verificato questo evento.  
  
## <a name="remarks"></a>Note  
 Un' **EndOfRecordset** evento può verificarsi se il [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) operazione ha esito negativo.  
  
 Questo gestore eventi viene chiamato quando viene effettuato un tentativo di spostare oltre la fine del **Recordset** oggetto, forse in seguito alla chiamata **MoveNext**. Tuttavia, mentre in questo caso, è possibile recuperare altri record da un database e li aggiunge alla fine della **Recordset**. In questo caso, impostare *fMoreData* VARIANT_TRUE e ritorno dal **EndOfRecordset**. Quindi chiamare **MoveNext** nuovamente di accedere ai record appena recuperati.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)
