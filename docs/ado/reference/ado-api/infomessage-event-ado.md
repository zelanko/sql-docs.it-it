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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 25eef06b7e25538cb874d99af98aee95495b95ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932336"
---
# <a name="infomessage-event-ado"></a>Evento InfoMessage (ADO)
Il **InfoMessage** eventi viene chiamato ogni volta che viene generato un avviso durante una **ConnectionEvent** operazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parametri  
 *pError*  
 Un' [errore](../../../ado/reference/ado-api/error-object.md) oggetto. Questo parametro contiene eventuali errori restituiti. Se vengono restituiti più errori, enumerare le **errori** insieme a trovarli.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore dello stato. Se viene generato un avviso, *adStatus* è impostata su **adStatusOK** e il *pError* contiene il messaggio di avviso.  
  
 Prima di questo evento viene restituito, questo parametro impostato su **adStatusUnwantedEvent** per evitare le notifiche successivi.  
  
 *pConnection*  
 Oggetto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto. La connessione per il quale si è verificato l'avviso. Ad esempio, gli avvisi possono verificarsi quando si apre un **connessione** oggetto o l'esecuzione di un [comando](../../../ado/reference/ado-api/command-object-ado.md) in un **connessione**.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
