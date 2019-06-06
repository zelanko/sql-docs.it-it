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
manager: jroth
ms.openlocfilehash: 7361b453272289107ea3c5ae268b951178aa1b43
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695503"
---
# <a name="cursortype-property-ado"></a>Proprietà CursorType (ADO)
Indica il tipo di cursore utilizzato una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) valore. Il valore predefinito è **adOpenForwardOnly**.  
  
## <a name="remarks"></a>Note  
 Usare la **CursorType** proprietà per specificare il tipo di cursore che deve essere utilizzato quando si apre il **Recordset** oggetto.  
  
 Solo l'impostazione **adOpenStatic** è supportato se il [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) viene impostata su **adUseClient**. Se è impostato un valore non supportato, non verrà generato alcun errore; è supportato il più vicino **CursorType** verrà utilizzato.  
  
 Se un provider non supporta il tipo di cursore richiesto, può restituire un altro tipo di cursore. Il **CursorType** proprietà verrà modificato per corrispondere al tipo di cursore effettivo in uso quando il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto è aperto. Per verificare funzionalità specifiche del cursore restituito, usare il [supporta](../../../ado/reference/ado-api/supports-method.md) (metodo). Dopo aver chiuso il **Recordset**, il **CursorType** proprietà viene ripristinata l'impostazione originale.  
  
 Il grafico seguente mostra le funzionalità del provider (identificato da **supporta** costanti del metodo) richiesto per ogni tipo di cursore.  
  
|Per un set di record di questo CursorType|Il metodo supporta deve restituire True per tutte le costanti|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|none|  
|**adOpenKeyset**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
  
> [!NOTE]
>  Sebbene **supporta**(**adUpdateBatch**) può essere true per i cursori dinamici e di tipo forward-only, per gli aggiornamenti di batch è necessario utilizzare un cursore statico o keyset. Impostare il [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) proprietà **adLockBatchOptimistic** e il **CursorLocation** proprietà **adUseClient** per abilitare il cursore Servizio per OLE DB, che è necessario per gli aggiornamenti in batch.  
  
 Il **CursorType** è di lettura/scrittura quando il **Recordset** viene chiuso e di sola lettura quando è aperta.  
  
> [!NOTE]
>  **Utilizzo del servizio dati remoto** quando viene usato in un client-side **Recordset** oggetto, il **CursorType** proprietà può essere impostata solo su **adOpenStatic**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [CursorType, LockType ed esempio di proprietà EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType ed EditMode esempio di proprietà (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Metodo Supports](../../../ado/reference/ado-api/supports-method.md)
