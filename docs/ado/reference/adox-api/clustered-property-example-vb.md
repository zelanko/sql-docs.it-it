---
description: Esempio della proprietà Clustered (VB)
title: Esempio di proprietà Clustered (VB) | Microsoft Docs
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
- Clustered property [ADOX], Visual Basic example
ms.assetid: 1cd30769-c8af-43e7-be27-12ed0434daa1
author: rothja
ms.author: jroth
ms.openlocfilehash: 1992c8c5796052e46719c34ecbc43d6b94553b6e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771140"
---
# <a name="clustered-property-example-vb"></a>Esempio della proprietà Clustered (VB)
In questo esempio viene illustrata la proprietà [Clustered](./clustered-property-adox.md) di un [Indice](./index-object-adox.md). Si noti che i database Microsoft Jet non supportano gli indici cluster, pertanto questo esempio restituirà **false** per la proprietà **Clustered** di tutti gli indici nel database **Northwind** .  
  
```  
' BeginClusteredVB  
Sub Main()  
    On Error GoTo ClusteredXError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tblLoop As ADOX.Table  
    Dim idxLoop As ADOX.Index  
    Dim strCnn As String  
  
    strCnn = "Provider='SQLOLEDB';Data Source='MySqlServer';Initial Catalog='pubs';" & _  
        "Integrated Security='SSPI';"  
    ' Connect to the catalog.  
    cnn.Open strCnn  
    cat.ActiveConnection = cnn  
  
    ' Enumerate the tables.  
    For Each tblLoop In cat.Tables  
        'Enumerate the indexes.  
        For Each idxLoop In tblLoop.Indexes  
            Debug.Print tblLoop.Name & " " & _  
                idxLoop.Name & " " & idxLoop.Clustered  
        Next idxLoop  
    Next tblLoop  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ClusteredXError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndClusteredVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Catalog (ADOX)](./catalog-object-adox.md)   
 [Proprietà Clustered (ADOX)](./clustered-property-adox.md)   
 [Oggetto index (ADOX)](./index-object-adox.md)   
 [Oggetto Table (ADOX)](./table-object-adox.md)