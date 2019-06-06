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
manager: jroth
ms.openlocfilehash: ba7675f5fe0abe02130de3c6bfc905070b24ec10
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697940"
---
# <a name="eventreasonenum"></a>EventReasonEnum
Specifica il motivo che ha causato un evento si verifichi.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|Un'operazione di aggiunta di un nuovo record.|  
|**adRsnClose**|9|Un'operazione ha chiuso il **Recordset**.|  
|**adRsnDelete**|2|Un'operazione ha eliminato un record.|  
|**adRsnFirstChange**|11|Un'operazione eseguita alla prima modifica a un record.|  
|**adRsnMove**|10|Un'operazione ha spostato il puntatore di record all'interno di **Recordset**.|  
|**adRsnMoveFirst**|12|Un'operazione ha spostato il puntatore di record del primo record di **Recordset**.|  
|**adRsnMoveLast**|15|Un'operazione ha spostato il puntatore di record dell'ultimo record di **Recordset**.|  
|**adRsnMoveNext**|13|Un'operazione ha spostato il puntatore di record sul record successivo nella **Recordset**.|  
|**adRsnMovePrevious**|14|Un'operazione ha spostato il puntatore di record per record precedente la **Recordset**.|  
|**adRsnRequery**|7|Un'operazione rieseguita la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adRsnResynch**|8|Un'operazione di risincronizzata il **Recordset** con il database.|  
|**adRsnUndoAddNew**|5|Un'operazione ha annullato l'aggiunta di un nuovo record.|  
|**adRsnUndoDelete**|6|Un'operazione ha annullato l'eliminazione di un record.|  
|**adRsnUndoUpdate**|4|Un'operazione ha annullato l'aggiornamento di un record.|  
|**adRsnUpdate**|3|Un'operazione ha aggiornato un record esistente.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.EventReason.ADDNEW|  
|AdoEnums.EventReason.CLOSE|  
|AdoEnums.EventReason.DELETE|  
|AdoEnums.EventReason.FIRSTCHANGE|  
|AdoEnums.EventReason.MOVE|  
|AdoEnums.EventReason.MOVEFIRST|  
|AdoEnums.EventReason.MOVELAST|  
|AdoEnums.EventReason.MOVENEXT|  
|AdoEnums.EventReason.MOVEPREVIOUS|  
|AdoEnums.EventReason.REQUERY|  
|AdoEnums.EventReason.RESYNCH|  
|AdoEnums.EventReason.UNDOADDNEW|  
|AdoEnums.EventReason.UNDODELETE|  
|AdoEnums.EventReason.UNDOUPDATE|  
|AdoEnums.EventReason.UPDATE|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Eventi WillChangeRecord e RecordChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[Eventi WillChangeRecordset e RecordsetChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[Eventi WillMove e MoveComplete (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)||
