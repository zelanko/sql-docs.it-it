---
title: Creare una nuova relazione di chiave esterna tra le tabelle esempio (VB) | Microsoft Docs
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
- Key Type property [ADOX], Visual Basic example
- RelatedTable property [ADOX], Visual Basic example
- Keys Append method [ADOX], Visual Basic example
- UpdateRule property [ADOX], Visual Basic example
- RelatedColumn property [ADOX], Visual Basic example
ms.assetid: 13b5b1c3-6af6-439e-bb65-976578ba6bc2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2bb7a08ab3159fa63024c7bc761c8ccec2563a78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706462"
---
# <a name="keys-append-method-key-type-relatedcolumn-relatedtable-and-updaterule-properties-example-vb"></a>Esempio del metodo Append di Keys, di Type di Key e delle proprietà RelatedColumn, RelatedTable e UpdateRule (VB)
Il codice seguente viene illustrato come creare una nuova relazione di chiave esterna tra due tabelle esistente denominato **clienti** e **ordini**.  
  
```  
' BeginCreateKeyVB  
Sub Main()  
    On Error GoTo CreateKeyError  
  
    Dim kyForeign As New ADOX.Key  
    Dim cat As New ADOX.Catalog  
  
    ' Connect to the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Define the foreign key.  
    kyForeign.Name = "CustOrder"  
    kyForeign.Type = adKeyForeign  
    kyForeign.RelatedTable = "Customers"  
    kyForeign.Columns.Append "CustomerId"  
    kyForeign.Columns("CustomerId").RelatedColumn = "CustomerId"  
    kyForeign.UpdateRule = adRICascade  
  
    ' Append the foreign key to the keys collection.  
    cat.Tables("Orders").Keys.Append kyForeign  
  
    'Delete the key t demonstrate the Delete method.  
    cat.Tables("Orders").Keys.Delete kyForeign.Name  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set kyForeign = Nothing  
    Exit Sub  
  
CreateKeyError:  
    Set cat = Nothing  
    Set kyForeign = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndCreateKeyVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Append (metodo) (oggetti Column ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (metodo) (oggetti Key ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Oggetto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [Raccolta di colonne (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Oggetto Key (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)   
 [Raccolta di oggetti Key (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Proprietà Name (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [Proprietà RelatedColumn (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md)   
 [Proprietà RelatedTable (ADOX)](../../../ado/reference/adox-api/relatedtable-property-adox.md)   
 [Oggetto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [Raccolta di tabelle (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Proprietà Type (Key) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md)   
 [Proprietà UpdateRule (ADOX)](../../../ado/reference/adox-api/updaterule-property-adox.md)
