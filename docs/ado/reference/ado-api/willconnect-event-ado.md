---
description: Evento WillConnect (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4a63bf9d324fc9c2e0363576814e1c97c9ad6aeb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776860"
---
# <a name="willconnect-event-ado"></a>Evento WillConnect (ADO)
L'evento **WillConnect** viene chiamato prima dell'avvio di una connessione.  
  
 **Si applica a:** [oggetto Connection (ADO)](./connection-object-ado.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectionString*  
 **Stringa** che contiene le informazioni di connessione per la connessione in sospeso.  
  
 *UserID*  
 **Stringa** che contiene un nome utente per la connessione in sospeso.  
  
 *Password*  
 **Stringa** che contiene una password per la connessione in sospeso.  
  
 *Opzioni*  
 Valore **Long** che indica la modalità di valutazione di *ConnectionString*da parte del provider. L'unica opzione è **adAsyncOpen**.  
  
 *adStatus*  
 Valore di stato di [EventStatusEnum](./eventstatusenum.md) .  
  
 Quando viene chiamato questo evento, questo parametro è impostato su **adStatusOK** per impostazione predefinita. Viene impostato su **adStatusCantDeny** se l'evento non può richiedere l'annullamento dell'operazione in sospeso.  
  
 Prima della restituzione di questo evento, impostare questo parametro su **adStatusUnwantedEvent** per impedire le notifiche successive. Impostare questo parametro su **adStatusCancel** per richiedere l'operazione di connessione che ha causato l'annullamento della notifica.  
  
 *pConnection*  
 Oggetto [connessione](./connection-object-ado.md) per il quale viene applicata la notifica degli eventi. Le modifiche apportate ai parametri della **connessione** dal gestore dell'evento **WillConnect** non avranno effetto sulla **connessione**.  
  
## <a name="remarks"></a>Commenti  
 Quando viene chiamato **WillConnect** , i parametri *ConnectionString*, *userid*, *password*e *options* sono impostati sui valori stabiliti dall'operazione che ha causato l'evento (la connessione in sospeso) e possono essere modificati prima che l'evento venga restituito. **WillConnect** può restituire una richiesta di annullamento della connessione in sospeso.  
  
 Quando questo evento viene annullato, **ConnectComplete** viene chiamato con il parametro *adStatus* impostato su **adStatusErrorsOccurred**.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](./ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../guide/data/ado-event-handler-summary.md)