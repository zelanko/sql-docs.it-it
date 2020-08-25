---
description: Esempio del metodo Append di Views (VB)
title: Esempio di metodo Append views (VB) | Microsoft Docs
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
- Append method [ADOX]
ms.assetid: b5b4c082-ac29-4f49-a8b8-e21b554c9b0d
author: rothja
ms.author: jroth
ms.openlocfilehash: 172b45d111b74f81e416118f489ef3e0a40dd871
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768970"
---
# <a name="views-append-method-example-vb"></a>Esempio del metodo Append di Views (VB)
Nel codice seguente viene illustrato come utilizzare un oggetto [Command](../ado-api/command-object-ado.md) e il metodo [Append](./append-method-adox-views.md) della raccolta [views](./views-collection-adox.md) per creare una nuova visualizzazione nell'origine dati sottostante.  
  
```  
' BeginCreateViewVB  
Sub Main()  
    On Error GoTo CreateViewError  
  
    Dim cmd As New ADODB.Command  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Create the command representing the view.  
    cmd.CommandText = "Select * From Customers"  
  
    ' Create the new View  
    cat.Views.Append "AllCustomers", cmd  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set cmd = Nothing  
    Exit Sub  
  
CreateViewError:  
  
    Set cat = Nothing  
    Set cmd = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateViewVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà ActiveConnection (ADOX)](./activeconnection-property-adox.md)   
 [Metodo Append (viste ADOX)](./append-method-adox-views.md)   
 [Oggetto Catalog (ADOX)](./catalog-object-adox.md)   
 [Oggetto View (ADOX)](./view-object-adox.md)   
 [Raccolta Views (ADOX)](./views-collection-adox.md)