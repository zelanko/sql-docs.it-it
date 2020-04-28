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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931780"
---
# <a name="pagecount-property-ado"></a>Proprietà PageCount (ADO)
Indica il numero di pagine di dati contenute nell'oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **Long** che indica il numero di pagine nel **Recordset**.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **PageCount** per determinare il numero di pagine di dati presenti nell'oggetto **Recordset** . Le *pagine* sono gruppi di record la cui dimensione è uguale all'impostazione della proprietà [pageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) . Anche se l'ultima pagina è incompleta perché sono presenti meno record del valore **pageSize** , viene conteggiata come pagina aggiuntiva nel valore **PageCount** . Se l'oggetto **Recordset** non supporta questa proprietà, il valore sarà-1 per indicare che **PageCount** è determinabile.  
  
 Per ulteriori informazioni sulle funzionalità della pagina, vedere le proprietà **pageSize** e [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà AbsolutePage, PageCount e PageSize (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [Esempio di proprietà AbsolutePage, PageCount e PageSize (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Proprietà AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Proprietà PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [Proprietà RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
