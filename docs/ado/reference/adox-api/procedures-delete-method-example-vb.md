---
title: Esempio di metodo Delete di Procedures (VB) | Microsoft Docs
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
- Delete method [ADOX], Visual Basic example
ms.assetid: 94f1ac93-e778-4a40-a85e-94bce5316ac7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f5c7dfc901434c086b46bfb11c70e1eb2ee3bff7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965366"
---
# <a name="procedures-delete-method-example-vb"></a>Esempio del metodo Delete di Procedures (VB)
Nel codice seguente viene illustrato come eliminare una stored procedure utilizzando il metodo [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) della raccolta [Procedures](../../../ado/reference/adox-api/procedures-collection-adox.md) .  
  
```  
' BeginDeleteProcedureVB  
Sub Main()  
    On Error GoTo DeleteProcedureError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog.  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Delete the procedure.  
    cat.Procedures.Delete "CustomerById"  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
DeleteProcedureError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndDeleteProcedureVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà ActiveConnection (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Metodo Delete (raccolte ADOX)](../../../ado/reference/adox-api/delete-method-adox-collections.md)   
 [Oggetto procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)   
 [Raccolta Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)
