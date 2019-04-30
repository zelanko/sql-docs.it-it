---
title: Eventi ConnectComplete e Disconnect (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Disconnect
- Connection::ConnectComplete
- ConnectComplete
- Connection::Disconnect
helpviewer_keywords:
- Disconnect event [ADO]
- ConnectComplete event [ADO]
ms.assetid: 568f5252-d069-4d99-a01b-2ada87ad1304
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1466b8f718318d8224ec2c7dcf3e873139fffed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309144"
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>Eventi ConnectComplete e Disconnect (ADO)
Il **ConnectComplete** eventi viene chiamato dopo l'avvio di una connessione. Il **Disconnect** eventi viene chiamato dopo la fine di una connessione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parametri  
 *pError*  
 Un' [errore](../../../ado/reference/ado-api/error-object.md) oggetto. Viene descritto l'errore generato se il valore di *adStatus* viene **adStatusErrorsOccurred**; in caso contrario, non è impostata.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore indica che è sempre **adStatusOK**.  
  
 Quando **ConnectComplete** viene chiamato, questo parametro è impostato su **adStatusCancel** se un **WillConnect** eventi ha richiesto l'annullamento della connessione in sospeso.  
  
 Prima che l'evento restituito, questo parametro impostato su **adStatusUnwantedEvent** per evitare le notifiche successivi. Tuttavia, chiudere e riaprire il [connessione](../../../ado/reference/ado-api/connection-object-ado.md) fa in modo che questi eventi si verifichi nuovamente.  
  
 *pConnection*  
 Il **connessione** dell'oggetto per cui si applica questo evento.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)
