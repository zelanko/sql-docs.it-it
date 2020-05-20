---
title: Evento InfoMessage (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
author: rothja
ms.author: jroth
ms.openlocfilehash: c5fc0adfec791294bb6c680dab94078b8a63ec07
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758687"
---
# <a name="infomessage-event-ado"></a>Evento InfoMessage (ADO)
L'evento **InfoMessage** viene chiamato ogni volta che viene generato un avviso durante un'operazione **ConnectionEvent** .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parametri  
 *pError*  
 Oggetto [Error](../../../ado/reference/ado-api/error-object.md) . Questo parametro contiene gli eventuali errori restituiti. Se vengono restituiti più errori, enumerare la raccolta di **errori** per trovarli.  
  
 *adStatus*  
 Valore di stato di [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) . Se viene generato un avviso, *adStatus* è impostato su **adStatusOK** e *perror* contiene l'avviso.  
  
 Prima della restituzione di questo evento, impostare questo parametro su **adStatusUnwantedEvent** per impedire le notifiche successive.  
  
 *pConnection*  
 Oggetto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) . Connessione per la quale si è verificato l'avviso. Ad esempio, è possibile che si verifichino avvisi durante l'apertura di un oggetto **connessione** o l'esecuzione di un [comando](../../../ado/reference/ado-api/command-object-ado.md) in una **connessione**.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo del gestore eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
