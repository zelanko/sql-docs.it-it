---
title: Proprietà PageCount (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ea893a019ab6d1333cecc5da5f1f66928467adfc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931780"
---
# <a name="pagecount-property-ado"></a>Proprietà PageCount (ADO)
Indica quante pagine di dati di [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto contiene.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **lungo** valore che indica il numero di pagine nel **Recordset**.  
  
## <a name="remarks"></a>Note  
 Usare la **PageCount** proprietà per determinare il numero di pagine di dati presenti nel **Recordset** oggetto. *Le pagine* sono gruppi di record con dimensioni uguali i [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) l'impostazione della proprietà. Anche se l'ultima pagina incompleta perché sono presenti record minore del **PageSize** valore, viene conteggiata come una pagina aggiuntiva nel **PageCount** valore. Se il **Recordset** oggetto non supporta questa proprietà, il valore sarà -1 per indicare che il **PageCount** non è possibile determinare.  
  
 Vedere le **PageSize** e [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) le proprietà per più sulle funzionalità relative alle pagina.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [AbsolutePage, PageCount, PageSize esempio di proprietà e (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount, PageSize esempio di proprietà e (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Proprietà AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Proprietà PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [Proprietà RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
