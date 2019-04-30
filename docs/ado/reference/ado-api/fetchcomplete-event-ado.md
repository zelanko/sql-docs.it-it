---
title: Evento FetchComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- FetchComplete event [ADO]
ms.assetid: a28d3858-566c-468d-b070-d1de4339fbea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09ba18e3680579c7a09e4f51f3bfe3e083dda697
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140199"
---
# <a name="fetchcomplete-event-ado"></a>Evento FetchComplete (ADO)
Il **FetchComplete** eventi viene chiamato dopo che sono stati recuperati tutti i record in un'operazione di lunga durata asincrona nel [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parametri  
 *pError*  
 Un' [errore](../../../ado/reference/ado-api/error-object.md) oggetto. Viene descritto l'errore generato se il valore di **adStatus** viene **adStatusErrorsOccurred**; in caso contrario, non è impostata.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore dello stato. Quando questo evento viene chiamato, questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento ha esito positivo o a **adStatusErrorsOccurred** se l'operazione non riuscita.  
  
 Prima di questo evento viene restituito, questo parametro impostato su **adStatusUnwantedEvent** per evitare le notifiche successivi.  
  
 *pRecordset*  
 Oggetto **Recordset** oggetto. L'oggetto per cui sono stati recuperati i record.  
  
## <a name="remarks"></a>Note  
 Per utilizzare **FetchComplete** con Microsoft Visual Basic, Visual Basic 6.0 o versione successiva è obbligatorio.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)
