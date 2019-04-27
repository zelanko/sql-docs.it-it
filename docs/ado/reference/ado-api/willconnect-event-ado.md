---
title: Evento WillConnect (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22d30e389c61a66d417ad5baec99a8834a754047
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642526"
---
# <a name="willconnect-event-ado"></a>Evento WillConnect (ADO)
Il **WillConnect** eventi viene chiamato prima dell'avvio di una connessione.  
  
 **Si applica a:** [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectionString*  
 Oggetto **stringa** che contiene le informazioni di connessione per la connessione in sospeso.  
  
 *UserID*  
 Oggetto **stringa** che contiene un nome utente per la connessione in sospeso.  
  
 *Password*  
 Oggetto **stringa** che contiene una password per la connessione in sospeso.  
  
 *Opzioni*  
 Oggetto **lungo** valore che indica come il provider deve valutare il *ConnectionString*. L'unica possibilità consiste **adAsyncOpen**.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore dello stato.  
  
 Quando questo evento viene chiamato, questo parametro è impostato su **adStatusOK** per impostazione predefinita. È impostato su **adStatusCantDeny** se l'evento non è possibile richiedere l'annullamento dell'operazione in sospeso.  
  
 Prima di questo evento viene restituito, questo parametro impostato su **adStatusUnwantedEvent** per evitare le notifiche successivi. Questo parametro impostato su **adStatusCancel** per richiedere l'operazione di connessione che ha causato l'annullamento della notifica.  
  
 *pConnection*  
 Il [connessione](../../../ado/reference/ado-api/connection-object-ado.md) dell'oggetto per cui si applica questa notifica degli eventi. Modifiche ai parametri del **connessione** per il **WillConnect** gestore dell'evento non avrà alcun effetto **connessione**.  
  
## <a name="remarks"></a>Note  
 Quando **WillConnect** viene chiamato, il *ConnectionString*, *UserID*, *Password*, e *opzioni* parametri vengono impostati sui valori definiti dall'operazione che ha causato questo evento (la connessione in sospeso) e può essere modificato prima della restituzione dell'evento. **WillConnect** può restituire una richiesta di annullamento che la connessione in sospeso.  
  
 Quando questo evento viene annullato, **ConnectComplete** utilizzato per la chiamata relativo *adStatus* parametro impostato su **adStatusErrorsOccurred**.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)
