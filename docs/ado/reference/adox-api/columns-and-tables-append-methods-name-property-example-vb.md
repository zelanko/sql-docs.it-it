---
description: Esempio dei metodi Append di Columns e Tables e della proprietà Name (VB)
title: Metodi di Accodamento di colonne e tabelle, esempio di proprietà Name (VB) | Microsoft Docs
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
- Name property [ADOX], Visual Basic example
- Append method [ADOX], Visual Basic example
ms.assetid: 678e5546-df5d-4cd0-bfe9-6cf13cb385c0
author: rothja
ms.author: jroth
ms.openlocfilehash: 0a62e610ae47243e8200a9422639569e91ce2c4c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771050"
---
# <a name="columns-and-tables-append-methods-name-property-example-vb"></a>Esempio dei metodi Append di Columns e Tables e della proprietà Name (VB)
Nel codice seguente viene illustrato come creare una nuova tabella.  
  
```  
' BeginCreateTableVB  
Sub Main()  
    On Error GoTo CreateTableError  
  
    Dim tbl As New Table  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    tbl.Name = "MyTable"  
    tbl.Columns.Append "Column1", adInteger  
    tbl.Columns.Append "Column2", adInteger  
    tbl.Columns.Append "Column3", adVarWChar, 50  
    cat.Tables.Append tbl  
    Debug.Print "Table 'MyTable' is added."  
  
    'Delete the table as this is a demonstration.  
    cat.Tables.Delete tbl.Name  
    Debug.Print "Table 'MyTable' is deleted."  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set tbl = Nothing  
    Exit Sub  
  
CreateTableError:  
  
    Set cat = Nothing  
    Set tbl = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateTableVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Append (colonne ADOX)](./append-method-adox-columns.md)   
 [Metodo Append (tabelle ADOX)](./append-method-adox-tables.md)   
 [Oggetto Column (ADOX)](./column-object-adox.md)   
 [Raccolta Columns (ADOX)](./columns-collection-adox.md)   
 [Proprietà Name (ADOX)](./name-property-adox.md)   
 [Oggetto Table (ADOX)](./table-object-adox.md)   
 [Raccolta Tables (ADOX)](./tables-collection-adox.md)