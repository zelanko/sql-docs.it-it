---
title: (ADO) proprietà dinamica Optimize | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931859"
---
# <a name="optimize-property-dynamic-ado"></a>Proprietà dinamica Optimize (ADO)
Specifica se è necessario creare un indice in una [campo](../../../ado/reference/ado-api/field-object.md).  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **booleana** valore che indica se è necessario creare un indice.  
  
## <a name="remarks"></a>Note  
 Un indice può migliorare le prestazioni delle operazioni di ricerca o ordinare i valori in una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). L'indice è interna all'ADO. in modo esplicito non è possibile accedere o usarla nell'applicazione.  
  
 Per creare un indice su un campo, impostare il **Ottimizza** proprietà **True**. Per eliminare l'indice, impostare questa proprietà su **False**.  
  
 **Ottimizzare** viene aggiunta una proprietà dinamica per il [campo](../../../ado/reference/ado-api/field-object.md) oggetto [delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta quando la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su **adUseClient**.  
  
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
 [Ottimizzare l'esempio di proprietà (VB)](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [Ottimizzare l'esempio di proprietà (VC + +)](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [Proprietà filtro](../../../ado/reference/ado-api/filter-property.md)   
 [Metodo Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Proprietà Sort](../../../ado/reference/ado-api/sort-property.md)
