---
title: Esempio di metodo Refresh views (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Refresh method [ADOX]
ms.assetid: cdad2d66-6ade-40dc-9e74-e40cfa9bc127
author: rothja
ms.author: jroth
ms.openlocfilehash: c4b807bbadb5a9b4c8278be8ae895cd6ce4309c0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82752941"
---
# <a name="views-refresh-method-example-vb"></a>Esempio del metodo Refresh di Views (VB)
Nel codice seguente viene illustrato come aggiornare la raccolta [views](../../../ado/reference/adox-api/views-collection-adox.md) di un [Catalogo](../../../ado/reference/adox-api/catalog-object-adox.md). Questa operazione è necessaria prima che sia possibile accedere agli oggetti di [visualizzazione](../../../ado/reference/adox-api/view-object-adox.md) del **Catalogo** .  
  
```  
' BeginViewsRefreshVB  
Sub Main()  
    On Error GoTo ProcedureViewsRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection.  
    cat.Views.Refresh  
  
    'Clean up  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureViewsRefreshError:  
  
    If Not cat Is Nothing Then  
        Set cat = Nothing  
    End If  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndViewsRefreshVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Raccolta di oggetti View (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
