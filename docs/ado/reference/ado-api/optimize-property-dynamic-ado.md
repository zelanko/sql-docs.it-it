---
description: Proprietà dinamica Optimize (ADO)
title: Optimize Property-Dynamic (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
author: rothja
ms.author: jroth
ms.openlocfilehash: 91da30a49a0eff7d8b32274e8486002f78f2a05f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773640"
---
# <a name="optimize-property-dynamic-ado"></a>Proprietà dinamica Optimize (ADO)
Specifica se è necessario creare un indice in un [campo](./field-object.md).  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **booleano** che indica se deve essere creato un indice.  
  
## <a name="remarks"></a>Commenti  
 Un indice può migliorare le prestazioni delle operazioni che consentono di trovare o ordinare i valori in un [Recordset](./recordset-object-ado.md). L'indice è interno a ADO; non è possibile accedervi o usarlo in modo esplicito nell'applicazione.  
  
 Per creare un indice in un campo, impostare la proprietà **optimize** su **true**. Per eliminare l'indice, impostare questa proprietà su **false**.  
  
 **Optimize** è una proprietà dinamica aggiunta alla raccolta [Properties](./properties-collection-ado.md) dell'oggetto [Field](./field-object.md) quando la proprietà [CursorLocation](./cursorlocation-property-ado.md) è impostata su **adUseClient**.  
  
## <a name="usage"></a>Uso  
  
```  
Dim rs As New Recordset  
Dim fld As Field  
rs.CursorLocation = adUseClient      'Enable index creation  
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable  
rs.Open  
Set fld = rs.Fields(0)  
fld.Properties("Optimize") = True    'Create an index  
fld.Properties("Optimize") = False   'Delete an index  
```  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Field](./field-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Optimize (VB)](./optimize-property-example-vb.md)   
 [Esempio di proprietà Optimize (VC + +)](./optimize-property-example-vc.md)   
 [Filter (proprietà)](./filter-property.md)   
 [Metodo Find (ADO)](./find-method-ado.md)   
 [Proprietà Sort](./sort-property.md)