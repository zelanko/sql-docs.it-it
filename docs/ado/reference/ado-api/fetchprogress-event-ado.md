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
ms.openlocfilehash: ab93d8117a5fb3d2bbc95ea33bbacdc7fba3f151
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932824"
---
# <a name="fetchprogress-event-ado"></a>Evento FetchProgress (ADO)
L'evento **FetchProgress**viene chiamato periodicamente durante un'operazione asincrona lunga per segnalare il numero di righe attualmente recuperate nel [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parametri  
 *Corso*  
 Valore **Long** che indica il numero di record attualmente recuperati dall'operazione di recupero.  
  
 *MaxProgress*  
 Valore **Long** che indica il numero massimo di record che devono essere recuperati.  
  
 *adStatus*  
 Valore di stato di [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) .  
  
 *pRecordset*  
 Oggetto **Recordset** che rappresenta l'oggetto per il quale vengono recuperati i record.  
  
## <a name="remarks"></a>Osservazioni  
 Quando si usa **FetchProgress** con un **Recordset**figlio, tenere presente che i valori dei parametri *Progress* e *MaxProgress* sono derivati dal set di righe del [servizio Cursor](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) sottostante. I valori restituiti rappresentano il numero totale di record nel set di righe sottostante, non solo il numero di record nel capitolo corrente.  
  
> [!NOTE]
>  Per usare **FetchProgress** con Microsoft Visual Basic, è necessario Visual Basic 6,0 o versione successiva.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)
