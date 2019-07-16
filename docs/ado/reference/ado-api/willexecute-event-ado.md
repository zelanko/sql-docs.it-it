---
title: Evento WillExecute (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0e7c29be102e9c5c7709816895a6647c95337c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936619"
---
# <a name="willexecute-event-ado"></a>Evento WillExecute (ADO)
Il **WillExecute** evento chiamato poco prima dell'esecuzione di un comando in attesa su una connessione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parametri  
 *Origine*  
 Oggetto **stringa** che contiene un comando SQL o un nome di stored procedure.  
  
 *CursorType*  
 Oggetto [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) che contiene il tipo di cursore per il **Recordset** che verrà aperto. Con questo parametro, è possibile modificare il cursore in qualsiasi tipo durante un **Recordset**[metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) operazione. *CursorType* verranno ignorati per qualsiasi altra operazione.  
  
 *LockType*  
 Oggetto [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) che contiene il tipo di blocco per il **Recordset** che verrà aperto. Con questo parametro, è possibile modificare il blocco per qualsiasi tipo durante un **RecordsetOpen** operazione. *LockType* verranno ignorati per qualsiasi altra operazione.  
  
 *Opzioni*  
 Oggetto **lungo** valore che indica le opzioni che possono essere utilizzate per eseguire il comando o aprire il **Recordset**.  
  
 *adStatus*  
 Un' [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valore di stato che può essere **adStatusCantDeny** oppure **adStatusOK** quando questo evento viene chiamato. Se si tratta **adStatusCantDeny**, questo evento potrebbe non richiedere l'annullamento dell'operazione in sospeso.  
  
 *pCommand*  
 Il [comandi ADO (Object)](../../../ado/reference/ado-api/command-object-ado.md) dell'oggetto per cui si applica questa notifica degli eventi.  
  
 *pRecordset*  
 Il [Recordset ADO (Object)](../../../ado/reference/ado-api/recordset-object-ado.md) dell'oggetto per cui si applica questa notifica degli eventi.  
  
 *pConnection*  
 Il [connessione ADO (Object)](../../../ado/reference/ado-api/connection-object-ado.md) dell'oggetto per cui si applica questa notifica degli eventi.  
  
## <a name="remarks"></a>Note  
 Oggetto **WillExecute** evento può verificarsi a causa di una connessione.  [Eseguire il metodo (connessione ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md), [metodo Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md), o [metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo la *pConnection* parametro dovrebbe contengono sempre un riferimento valido a un **connessione** oggetto. Se l'evento è dovuto al fatto **Connection**, il *pRecordset* e *pCommand* parametri vengono impostati **Nothing**. Se l'evento è dovuto al fatto **Open**, il *pRecordset* parametro farà riferimento il **Recordset** oggetto e il *pCommand* parametro è impostato su **Nothing**. Se l'evento è dovuto al fatto **Command. Execute**, il *pCommand* parametro farà riferimento il **comando** oggetto e il *pRecordset* parametro è impostato su **Nothing**.  
  
 **WillExecute** consente di esaminare e modificare i parametri di esecuzione in sospeso. Questo evento può restituire una richiesta di annullamento che i comandi in sospeso.  
  
> [!NOTE]
>  Se originale dell'origine per un **comandi** è un flusso specificato dal parametro il [proprietà CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md) proprietà, assegnando una nuova stringa per il **WillExecute** _Origine_ l'origine del parametro viene modificato il **comando**. Il **CommandStream** proprietà verrà cancellata e il [proprietà CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) proprietà verrà aggiornata con la nuova origine. Il flusso originale specificato da **CommandStream** verrà rilasciato e non è accessibile.  
  
 Se il sottolinguaggio della nuova stringa di origine è diverso dall'impostazione originale della [proprietà Dialect](../../../ado/reference/ado-api/dialect-property.md) proprietà (che corrispondessero alle **CommandStream**), il sottolinguaggio corretto deve essere specificato impostando il **sottolinguaggio** proprietà dell'oggetto comando fa *pCommand*.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di modello di eventi ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
