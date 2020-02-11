---
title: Esempio di proprietà ActiveConnection di Catalog (VB) | Microsoft Docs
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
- ActiveConnection property [ADOX], Visual Basic example
ms.assetid: bb3274b1-764d-43a7-a49f-ef55680ecd26
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4c6d30aeeb650525873669ccd175155c7e69cd0b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967112"
---
# <a name="catalog-activeconnection-property-example-vb"></a>Esempio della proprietà ActiveConnection di Catalog (VB)
Impostando la proprietà [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) su una connessione aperta valida, viene aperto il catalogo. Da un catalogo aperto, è possibile accedere agli oggetti dello schema contenuti nel catalogo.  
  
```  
' BeginOpenConnectionVB  
Sub Main()  
    On Error GoTo OpenConnectionError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Debug.Print cat.Tables(0).Type  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
OpenConnectionError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndOpenConnectionVB  
```  
  
 L'impostazione della proprietà **ActiveConnection** su una stringa di connessione valida consente inoltre di aprire il catalogo.  
  
```  
Attribute VB_Name = "Catalog"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà ActiveConnection (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Oggetto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [Raccolta Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Proprietà Type (Table) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)
