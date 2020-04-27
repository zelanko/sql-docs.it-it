---
title: EventReasonEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventReasonEnum
helpviewer_keywords:
- EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c37a7385cc3aabb725f86261203d22b5b10c3be6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918868"
---
# <a name="eventreasonenum"></a>EventReasonEnum
Specifica il motivo per cui è stato generato un evento.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|Un'operazione ha aggiunto un nuovo record.|  
|**adRsnClose**|9|Un'operazione ha chiuso il **Recordset**.|  
|**adRsnDelete**|2|Un'operazione ha eliminato un record.|  
|**adRsnFirstChange**|11|Un'operazione ha effettuato la prima modifica a un record.|  
|**adRsnMove**|10|Un'operazione ha spostato il puntatore del record all'interno del **Recordset**.|  
|**adRsnMoveFirst**|12|Un'operazione ha spostato il puntatore del record sul primo record nel **Recordset**.|  
|**adRsnMoveLast**|15|Un'operazione ha spostato il puntatore del record nell'ultimo record del **Recordset**.|  
|**adRsnMoveNext**|13|Un'operazione ha spostato il puntatore del record al record successivo nel **Recordset**.|  
|**adRsnMovePrevious**|14|Un'operazione ha spostato il puntatore del record nel record precedente nel **Recordset**.|  
|**adRsnRequery**|7|Un'operazione ha nuovamente eseguito una query sul [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adRsnResynch**|8|Un'operazione ha risincronizzato il **Recordset** con il database.|  
|**adRsnUndoAddNew**|5|Un'operazione ha invertito l'aggiunta di un nuovo record.|  
|**adRsnUndoDelete**|6|Un'operazione ha annullato l'eliminazione di un record.|  
|**adRsnUndoUpdate**|4|Un'operazione ha invertito l'aggiornamento di un record.|  
|**adRsnUpdate**|3|Un'operazione ha aggiornato un record esistente.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. EventReason. ADDNEW|  
|AdoEnums. EventReason. CLOSE|  
|AdoEnums. EventReason. DELETE|  
|AdoEnums. EventReason. FIRSTCHANGE|  
|AdoEnums. EventReason. MOVE|  
|AdoEnums. EventReason. MOVEFIRST|  
|AdoEnums. EventReason. MOVELAST|  
|AdoEnums. EventReason. MOVENEXT|  
|AdoEnums. EventReason. MOVEPREVIOUS|  
|AdoEnums. EventReason. Requery|  
|AdoEnums. EventReason. Resync|  
|AdoEnums. EventReason. UNDOADDNEW|  
|AdoEnums. EventReason. UNDODELETE|  
|AdoEnums. EventReason. UNDOUPDATE|  
|AdoEnums. EventReason. UPDATE|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Eventi WillChangeRecord e RecordChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[Eventi WillChangeRecordset e RecordsetChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[Eventi WillMove e MoveComplete (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)||
