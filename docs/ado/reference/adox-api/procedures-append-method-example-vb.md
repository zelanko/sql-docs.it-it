---
description: Esempio del metodo Append di Procedures (VB)
title: Esempio di metodo Append di Procedures (VB) | Microsoft Docs
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
- Append method [ADOX], Visual Basic example
ms.assetid: ce83b966-474b-4f57-8eb9-370996dfc5c0
author: rothja
ms.author: jroth
ms.openlocfilehash: b8b9b58c50a1e3c77a6239c73222ea7a1656b882
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769640"
---
# <a name="procedures-append-method-example-vb"></a>Esempio del metodo Append di Procedures (VB)
Nel codice seguente viene illustrato come utilizzare un oggetto [Command](../ado-api/command-object-ado.md) e il metodo [Append](./append-method-adox-procedures.md) della raccolta [Procedures](./procedures-collection-adox.md) per creare una nuova procedura nell'origine dati sottostante.  
  
```  
' BeginCreateProcedureVB  
Sub Main()  
    On Error GoTo CreateProcedureError  
  
    Dim cnn As New ADODB.Connection  
    Dim cmd As New ADODB.Command  
    Dim prm As ADODB.Parameter  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Connection  
    cnn.Open _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Create the parameterized command (Microsoft Jet specific)  
    Set cmd.ActiveConnection = cnn  
    cmd.CommandText = "PARAMETERS [CustId] Text;" & _  
    "Select * From Customers Where CustomerId = [CustId]"  
  
    ' Open the Catalog  
    Set cat.ActiveConnection = cnn  
  
    ' Create the new Procedure  
    cat.Procedures.Append "CustomerById", cmd  
  
    'Clean  
    cnn.Close  
    Set cat = Nothing  
    Set cmd = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
CreateProcedureError:  
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
' EndCreateProcedureVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà ActiveConnection (ADOX)](./activeconnection-property-adox.md)   
 [Metodo Append (routine ADOX)](./append-method-adox-procedures.md)   
 [Oggetto Catalog (ADOX)](./catalog-object-adox.md)   
 [Oggetto procedure (ADOX)](./procedure-object-adox.md)   
 [Raccolta Procedures (ADOX)](./procedures-collection-adox.md)