---
description: Esempio delle proprietà Command e CommandText (VB)
title: Esempio di proprietà Command e CommandText (VB) | Microsoft Docs
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
- CommandText property [ADOX], Visual Basic example
- Command property [ADOX], Visual Basic example
ms.assetid: 413263a8-05c0-4404-929d-69f82b987ba3
author: rothja
ms.author: jroth
ms.openlocfilehash: 23136450602552394eb20a4ace7272081d9bf68f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770956"
---
# <a name="command-and-commandtext-properties-example-vb"></a>Esempio delle proprietà Command e CommandText (VB)
Nel codice seguente viene illustrato come utilizzare la proprietà [Command](./command-property-adox.md) per aggiornare il testo di una stored procedure.  
  
```  
' BeginProcedureTextVB  
Sub Main()  
    On Error GoTo ProcedureTextError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim cmd As New ADODB.Command  
  
    ' Open the connection.  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Open the catalog.  
    Set cat.ActiveConnection = cnn  
  
    ' Get the command.  
    Set cmd = cat.Procedures("CustomerById").Command  
  
    ' Update the CommandText.  
    cmd.CommandText = "Select CustomerId, CompanyName, ContactName " & _  
        "From Customers " & _  
        "Where CustomerId = [CustId]"  
  
    ' Update the procedure.  
    Set cat.Procedures("CustomerById").Command = cmd  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cmd = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ProcedureTextError:  
    Set cat = Nothing  
    Set cmd = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndProcedureTextVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà ActiveConnection (ADOX)](./activeconnection-property-adox.md)   
 [Oggetto Catalog (ADOX)](./catalog-object-adox.md)   
 [Proprietà Command (ADOX)](./command-property-adox.md)   
 [Oggetto procedure (ADOX)](./procedure-object-adox.md)   
 [Raccolta Procedures (ADOX)](./procedures-collection-adox.md)