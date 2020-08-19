---
description: EventStatusEnum
title: EventStatusEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventStatusEnum
helpviewer_keywords:
- EventStatusEnum enumeration [ADO]
ms.assetid: ebfd4cda-4017-4873-9d28-38b1c7db12a8
author: rothja
ms.author: jroth
ms.openlocfilehash: 3d696d7b971b5f6624a85addb3f023f2090ac90d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443903"
---
# <a name="eventstatusenum"></a>EventStatusEnum
Specifica lo stato corrente dell'esecuzione di un evento.  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adStatusCancel**|4|Richiede l'annullamento dell'operazione che ha causato l'evento.|  
|**adStatusCantDeny**|3|Indica che l'operazione non può richiedere l'annullamento dell'operazione in sospeso.|  
|**adStatusErrorsOccurred**|2|Indica che l'operazione che ha causato l'evento non è riuscita a causa di un errore o di errori.|  
|**adStatusOK**|1|Indica che l'operazione che ha causato l'evento è riuscita.|  
|**adStatusUnwantedEvent**|5|Impedisce le notifiche successive prima del completamento dell'esecuzione del metodo dell'evento.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. EventStatus. CANCEL|  
|AdoEnums. EventStatus. CANTDENY|  
|AdoEnums. EventStatus. ERRORSOCCURRED|  
|AdoEnums. EventStatus. OK|  
|AdoEnums. EventStatus. UNWANTEDEVENT|  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Eventi BeginTransComplete, CommitTransComplete e RollbackTransComplete (ADO)](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)  

        [Eventi ConnectComplete e Disconnect (ADO)](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)  

        [Evento EndOfRecordset (ADO)](../../../ado/reference/ado-api/endofrecordset-event-ado.md)  

        [Evento ExecuteComplete (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)  
    :::column-end:::
    :::column:::
        [Evento FetchComplete (ADO)](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)  

        [Evento InfoMessage (ADO)](../../../ado/reference/ado-api/infomessage-event-ado.md)  

        [Eventi WillChangeField e FieldChangeComplete (ADO)](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)  

        [Eventi WillChangeRecord e RecordChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)  
    :::column-end:::
    :::column:::
        [Eventi WillChangeRecordset e RecordsetChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)  

        [Evento WillConnect (ADO)](../../../ado/reference/ado-api/willconnect-event-ado.md)  

        [Evento WillExecute (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)  

        [Eventi WillMove e MoveComplete (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)  
    :::column-end:::
:::row-end:::
