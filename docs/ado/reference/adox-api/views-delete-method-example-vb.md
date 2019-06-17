---
title: Viste di esempio del metodo Delete (VB) | Microsoft Docs
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
- Delete method [ADOX]
ms.assetid: 17df2a83-4166-4df8-8c17-0a33aaac8582
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 15070d0d89e63bc84e4a4a9ca0ed9091d9f0878e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697052"
---
# <a name="views-delete-method-example-vb"></a>Esempio del metodo Delete di Views (VB)
Il codice seguente viene illustrato come utilizzare il [eliminare](../../../ado/reference/adox-api/delete-method-adox-collections.md) metodo per eliminare una vista dal catalogo.  
  
```  
' BeginDeleteViewVB  
Sub Main()  
    On Error GoTo DeleteViewError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    'Delete the View  
    cat.Views.Delete "AllCustomers"  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
DeleteViewError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndDeleteViewVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Elimina metodo (raccolte ADOX)](../../../ado/reference/adox-api/delete-method-adox-collections.md)   
 [Raccolta di oggetti View (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
