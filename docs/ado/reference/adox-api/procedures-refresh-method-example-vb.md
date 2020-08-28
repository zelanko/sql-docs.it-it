---
description: Esempio del metodo Refresh di Procedures (VB)
title: Esempio di metodo Refresh di Procedures (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Refresh method [ADOX], Visual Basic example
ms.assetid: 499679bd-287b-487d-bdfb-3803abffec1c
author: rothja
ms.author: jroth
ms.openlocfilehash: 757c410982f43258f25729f5e88a5705c1ca814d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983492"
---
# <a name="procedures-refresh-method-example-vb"></a>Esempio del metodo Refresh di Procedures (VB)
Nel codice seguente viene illustrato come aggiornare la raccolta [Procedures](./procedures-collection-adox.md) di un [Catalogo](./catalog-object-adox.md). Questa operazione è necessaria prima che sia possibile accedere agli oggetti [procedure](./procedure-object-adox.md) del **Catalogo** .  
  
```  
' BeginProceduresRefreshVB  
Sub Main()  
    On Error GoTo ProcedureRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection  
    cat.Procedures.Refresh  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureRefreshError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndProceduresRefreshVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Catalog (ADOX)](./catalog-object-adox.md)   
 [Raccolta Procedures (ADOX)](./procedures-collection-adox.md)   
 [Metodo Refresh (ADO)](../ado-api/refresh-method-ado.md)