---
title: Evento FetchProgress (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FetchProgress
- Recordset::FetchProgress
helpviewer_keywords:
- FetchProgress event [ADO]
ms.assetid: 301716fd-81fc-40eb-8a04-221ef7ab410e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9f7b31524a6c54846072fdce8cca76189c7034ad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698090"
---
# <a name="fetchprogress-event-ado"></a>Evento FetchProgress (ADO)
Il **FetchProgress**eventi viene chiamato periodicamente durante un'operazione asincrona lunga per segnalare il numero di righe attualmente recuperato nel [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parametri  
 *Stato*  
 Oggetto **lungo** valore che indica il numero di record che attualmente sono state recuperate dall'operazione di recupero.  
  
 *MaxProgress*  
 Oggetto **lungo** previsto valore che indica il numero massimo di record da recuperare.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore dello stato.  
  
 *pRecordset*  
 Oggetto **Recordset** oggetto che rappresenta l'oggetto per il quale vengono recuperati i record.  
  
## <a name="remarks"></a>Note  
 Quando si usa **FetchProgress** con un elemento figlio **Recordset**, tenere presente che il *corso* e *MaxProgress* derivano i valori dei parametri da sottostante [Cursor Service](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) set di righe. I valori restituiti rappresentano il numero totale di record nel set di righe sottostanti, non solo il numero di record nel capitolo corrente.  
  
> [!NOTE]
>  Per utilizzare **FetchProgress** con Microsoft Visual Basic, Visual Basic 6.0 o versione successiva è obbligatorio.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)
