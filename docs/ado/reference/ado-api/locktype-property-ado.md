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
ms.openlocfilehash: 7b50ab4a6fa31ec74371b86129f30abf11a1ba6c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932258"
---
# <a name="locktype-property-ado"></a>Proprietà LockType (ADO)
Indica il tipo di blocchi inseriti nei record durante la modifica.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) . Il valore predefinito è **adLockReadOnly**.  
  
## <a name="remarks"></a>Osservazioni  
 Impostare la proprietà **LockType** prima di aprire un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) per specificare il tipo di blocco che il provider deve utilizzare per l'apertura. Leggere la proprietà per restituire il tipo di blocco in uso in un oggetto **Recordset** aperto.  
  
 I provider potrebbero non supportare tutti i tipi di blocco. Se un provider non è in grado di supportare l'impostazione **LockType** richiesta, verrà sostituito un altro tipo di blocco. Per determinare l'effettiva funzionalità di blocco disponibile in un oggetto **Recordset** , utilizzare il metodo [Supports](../../../ado/reference/ado-api/supports-method.md) con **ADUpdate** e **adUpdateBatch**.  
  
 L'impostazione **adLockPessimistic** non è supportata se la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su **adUseClient**. Se viene impostato un valore non supportato, non verrà generato alcun errore. verrà invece usato il **LockType** supportato più vicino.  
  
 La proprietà **LockType** è in lettura/scrittura quando il **Recordset** è chiuso e in sola lettura quando è aperto.  
  
> [!NOTE]
>  **Utilizzo servizio dati remoto** Se utilizzata su un oggetto **Recordset** sul lato client, la proprietà **LockType** può essere impostata solo su **adLockBatchOptimistic**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà CursorType, LockType e EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [Esempio di proprietà CursorType, LockType e EditMode (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Metodo CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
