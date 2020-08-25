---
description: Proprietà PageCount (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: aa050f7e99115ca13bf8871378ffa21b1f326d94
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773540"
---
# <a name="pagecount-property-ado"></a>Proprietà PageCount (ADO)
Indica il numero di pagine di dati contenute nell'oggetto [Recordset](./recordset-object-ado.md) .  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **Long** che indica il numero di pagine nel **Recordset**.  
  
## <a name="remarks"></a>Commenti  
 Utilizzare la proprietà **PageCount** per determinare il numero di pagine di dati presenti nell'oggetto **Recordset** . Le *pagine* sono gruppi di record la cui dimensione è uguale all'impostazione della proprietà [pageSize](./pagesize-property-ado.md) . Anche se l'ultima pagina è incompleta perché sono presenti meno record del valore **pageSize** , viene conteggiata come pagina aggiuntiva nel valore **PageCount** . Se l'oggetto **Recordset** non supporta questa proprietà, il valore sarà-1 per indicare che **PageCount** è determinabile.  
  
 Per ulteriori informazioni sulle funzionalità della pagina, vedere le proprietà **pageSize** e [AbsolutePage](./absolutepage-property-ado.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà AbsolutePage, PageCount e PageSize (VB)](./absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [Esempio di proprietà AbsolutePage, PageCount e PageSize (VC + +)](./absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Proprietà AbsolutePage (ADO)](./absolutepage-property-ado.md)   
 [Proprietà PageSize (ADO)](./pagesize-property-ado.md)   
 [Proprietà RecordCount (ADO)](./recordcount-property-ado.md)