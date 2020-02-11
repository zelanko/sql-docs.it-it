---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e8bb3c3787effe8418db735a72425a793b73e35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931859"
---
# <a name="optimize-property-dynamic-ado"></a>Proprietà dinamica Optimize (ADO)
Specifica se è necessario creare un indice in un [campo](../../../ado/reference/ado-api/field-object.md).  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **booleano** che indica se deve essere creato un indice.  
  
## <a name="remarks"></a>Osservazioni  
 Un indice può migliorare le prestazioni delle operazioni che consentono di trovare o ordinare i valori in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). L'indice è interno a ADO; non è possibile accedervi o usarlo in modo esplicito nell'applicazione.  
  
 Per creare un indice in un campo, impostare la proprietà **optimize** su **true**. Per eliminare l'indice, impostare questa proprietà su **false**.  
  
 **Optimize** è una proprietà dinamica aggiunta alla raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) dell'oggetto [Field](../../../ado/reference/ado-api/field-object.md) quando la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su **adUseClient**.  
  
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
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Optimize (VB)](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [Esempio di proprietà Optimize (VC + +)](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [Filter (proprietà)](../../../ado/reference/ado-api/filter-property.md)   
 [Metodo Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Proprietà Sort](../../../ado/reference/ado-api/sort-property.md)
