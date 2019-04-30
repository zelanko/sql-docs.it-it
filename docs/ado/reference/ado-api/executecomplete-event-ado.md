---
title: Evento ExecuteComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec656a49963eb02cb204d5be96d403726bba8c56
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63301327"
---
# <a name="executecomplete-event-ado"></a>Evento ExecuteComplete (ADO)
Il **ExecuteComplete** eventi viene chiamato dopo che un comando ha terminato l'esecuzione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parametri  
 *RecordsAffected*  
 Oggetto **lungo** valore che indica il numero di record interessati dal comando.  
  
 *pError*  
 Un' [errore](../../../ado/reference/ado-api/error-object.md) oggetto. Viene descritto l'errore generato se il valore di **adStatus** viene **adStatusErrorsOccurred**; in caso contrario, non è impostata.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore dello stato. Quando questo evento viene chiamato, questo parametro è impostato su **adStatusOK** se l'operazione che ha causato l'evento ha esito positivo o a **adStatusErrorsOccurred** se l'operazione non riuscita.  
  
 Prima di questo evento viene restituito, questo parametro impostato su **adStatusUnwantedEvent** per evitare le notifiche successivi.  
  
 *pCommand*  
 Il [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto sul quale è stato eseguito. Contiene un **comando** anche durante la chiamata dell'oggetto **Connection** oppure **Open** senza creare esplicitamente un **comando** , casi in cui il **comando** oggetto viene creato internamente da ADO.  
  
 *pRecordset*  
 Oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto che rappresenta il risultato del comando eseguito. Ciò **Recordset** può essere vuoto. Mai non è necessario eliminare definitivamente questo oggetto Recordset all'interno di questo gestore dell'evento. Questa operazione comporterà una violazione di accesso quando si tenta di ADO per accedere a un oggetto che non esiste più.  
  
 *pConnection*  
 Oggetto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto. La connessione su cui è stata eseguita l'operazione.  
  
## <a name="remarks"></a>Note  
 Un' **ExecuteComplete** evento può verificarsi a causa dell'errore il **connessione.** [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md), **comando.** [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md), **Recordset.** [Aperto](../../../ado/reference/ado-api/open-method-ado-recordset.md), **Recordset.** [Requery](../../../ado/reference/ado-api/requery-method.md), o **Recordset.** [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md) metodi.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)
