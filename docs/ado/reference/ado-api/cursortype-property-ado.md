---
title: Proprietà CursorType (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CursorType
helpviewer_keywords:
- CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4dc881b96a1e2641d4946340c9462455197f2043
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919250"
---
# <a name="cursortype-property-ado"></a>Proprietà CursorType (ADO)
Indica il tipo di cursore utilizzato in un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) . Il valore predefinito è **adOpenForwardOnly**.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **CursorType** per specificare il tipo di cursore da utilizzare per l'apertura dell'oggetto **Recordset** .  
  
 Se la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su **adUseClient**, è supportata solo un'impostazione di **adOpenStatic** . Se viene impostato un valore non supportato, non verrà generato alcun errore. verrà invece usato il **CursorType** supportato più vicino.  
  
 Se un provider non supporta il tipo di cursore richiesto, può restituire un altro tipo di cursore. La proprietà **CursorType** verrà modificata in modo da corrispondere al tipo di cursore effettivo in uso quando l'oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) è aperto. Per verificare funzionalità specifiche del cursore restituito, utilizzare il metodo [Supports](../../../ado/reference/ado-api/supports-method.md) . Dopo aver chiuso il **Recordset**, viene ripristinata l'impostazione originale della proprietà **CursorType** .  
  
 Il grafico seguente mostra la funzionalità del provider (identificata da **supporta** le costanti di metodo) obbligatoria per ogni tipo di cursore.  
  
|Per un recordset di questo CursorType|Il metodo Supports deve restituire true per tutte queste costanti|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|none|  
|**adOpenKeyset**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
  
> [!NOTE]
>  Sebbene **Supports**(**adUpdateBatch**) possa essere true per i cursori dinamici e di tipo "Only", per gli aggiornamenti in batch è necessario usare un cursore keyset o static. Impostare la proprietà [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) su **adLockBatchOptimistic** e la proprietà **CursorLocation** su **adUseClient** per abilitare il servizio Cursor per OLE DB, che è necessario per gli aggiornamenti in batch.  
  
 La proprietà **CursorType** è in lettura/scrittura quando il **Recordset** è chiuso e in sola lettura quando è aperto.  
  
> [!NOTE]
>  **Utilizzo servizio dati remoto** Se utilizzata su un oggetto **Recordset** sul lato client, la proprietà **CursorType** può essere impostata solo su **adOpenStatic**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà CursorType, LockType e EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [Esempio di proprietà CursorType, LockType e EditMode (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Metodo Supports](../../../ado/reference/ado-api/supports-method.md)
