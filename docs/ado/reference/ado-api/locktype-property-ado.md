---
title: Proprietà LockType (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05670439a8f14018a999557dd135912e0c2e0159
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864097"
---
# <a name="locktype-property-ado"></a>Proprietà LockType (ADO)
Indica il tipo di blocchi sul record durante la modifica.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valore. Il valore predefinito è **adLockReadOnly**.  
  
## <a name="remarks"></a>Note  
 Impostare il **LockType** proprietà prima di aprire un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) per specificare il tipo di blocco che il provider deve utilizzare all'apertura dell'oggetto. Leggere la proprietà per restituire il tipo di blocco in uso su un elemento aperto **Recordset** oggetto.  
  
 I provider potrebbero non supportare tutti i tipi di blocco. Se un provider non supporta l'oggetto richiesto **LockType** impostazione, sostituirà un altro tipo di blocco. Per determinare la funzionalità di blocco disponibile in un **Recordset** dell'oggetto, utilizzare il [supporta](../../../ado/reference/ado-api/supports-method.md) metodo con **valori adUpdate** e **adUpdateBatch**.  
  
 Il **adLockPessimistic** impostazione non è supportata se il [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) viene impostata su **adUseClient**. Se è impostato un valore non supportato, non verrà generato alcun errore; è supportato il più vicino **LockType** verrà utilizzato.  
  
 Il **LockType** è di lettura/scrittura quando il **Recordset** viene chiuso e di sola lettura quando è aperta.  
  
> [!NOTE]
>  **Utilizzo del servizio dati remoto** quando viene usato in un client-side **Recordset** oggetto, il **LockType** proprietà può essere impostata solo su **adLockBatchOptimistic**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [CursorType, LockType ed esempio di proprietà EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType ed EditMode esempio di proprietà (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Metodo CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
