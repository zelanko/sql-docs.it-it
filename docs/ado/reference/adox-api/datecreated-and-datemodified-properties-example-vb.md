---
title: Esempio di proprietà DateCreated e DateModified (VB) | Microsoft Docs
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
- DateCreated property [ADOX], Visual Basic example
- DateModified property [ADOX], Visual Basic example
ms.assetid: d608ea35-6e68-402f-8184-a5041e408678
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 96ca853100baddd94d29331416215278d493388f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966591"
---
# <a name="datecreated-and-datemodified-properties-example-vb"></a>Esempio delle proprietà DateCreated e DateModified (VB)
In questo esempio vengono illustrate le proprietà [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) e [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) mediante l'aggiunta di una nuova [colonna](../../../ado/reference/adox-api/column-object-adox.md) a una [tabella](../../../ado/reference/adox-api/table-object-adox.md) esistente e la creazione di una nuova **tabella**. Per eseguire questo esempio, è necessaria la procedura DateOutput.  
  
```  
' BeginDateCreatedVB  
Sub Main()  
    On Error GoTo DateCreatedXError  
  
    Dim cat As New ADOX.Catalog  
    Dim tblEmployees As ADOX.Table  
    Dim tblNewTable As ADOX.Table  
  
    ' Connect to the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    With cat  
        Set tblEmployees = .Tables("Employees")  
  
        ' Print current information about the Employees table.  
        DateOutput "Current properties", tblEmployees  
  
        ' Create and append column to the Employees table.  
        tblEmployees.Columns.Append "NewColumn", adInteger  
        .Tables.Refresh  
  
        ' Print new information about the Employees table.  
        DateOutput "After creating a new column", tblEmployees  
  
        ' Delete new column because this is a demonstration.  
        tblEmployees.Columns.Delete "NewColumn"  
  
        ' Create and append new Table object to the Northwind database.  
        Set tblNewTable = New ADOX.Table  
        tblNewTable.Name = "NewTable"  
        tblNewTable.Columns.Append "NewColumn", adInteger  
        .Tables.Append tblNewTable  
        .Tables.Refresh  
  
        ' Print information about the new Table object.  
        DateOutput "After creating a new table", .Tables("NewTable")  
  
        ' Delete new Table object because this is a demonstration.  
        .Tables.Delete tblNewTable.Name  
    End With  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
DateCreatedXError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
  
Sub DateOutput(strTemp As String, tblTemp As ADOX.Table)  
    ' Print DateCreated and DateModified information about  
    ' specified Table object.  
    Debug.Print strTemp  
    Debug.Print "    Table: " & tblTemp.Name  
    Debug.Print "        DateCreated = " & tblTemp.DateCreated  
    Debug.Print "        DateModified = " & tblTemp.DateModified  
    Debug.Print  
End Sub  
' EndDateCreatedVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà DateCreated (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)   
 [Proprietà DateModified (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)   
 [Oggetto procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)   
 [Raccolta Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Oggetto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)   
 [Raccolta di oggetti View (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
