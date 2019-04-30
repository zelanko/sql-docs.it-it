---
title: Tabelle e colonne metodi Append oggetti esempio della proprietà Name (VB) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2bdd2643fdeb0f317e47c4d54b8b1ca62dec4109
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63183959"
---
# <a name="columns-and-tables-append-methods-name-property-example-vb"></a>Esempio dei metodi Append di Columns e Tables e della proprietà Name (VB)
Il codice seguente viene illustrato come creare una nuova tabella.  
  
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
 [Append (metodo) (oggetti Column ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (metodo) (oggetti Table ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Oggetto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [Raccolta di colonne (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Proprietà Name (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [Oggetto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [Raccolta di oggetti Table (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
