---
title: Esempio di proprietà StayInSync (VB) | Microsoft Docs
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
- StayInSync property [ADO], Visual Basic example
ms.assetid: b682bcc3-04b3-42b0-86f4-c17e0cd29baf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b8c271409657aa48ea1187c719254f2eef6b89b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711037"
---
# <a name="stayinsync-property-example-vb"></a>Esempio della proprietà StayInSync (VB)
Questo esempio viene illustrato come la [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) proprietà semplifica l'accesso alle righe in un modello gerarchico [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Il ciclo esterno viene visualizzato il nome e cognome, stato e identificazione ogni autore. L'oggetto aggiunto **Recordset** per ogni riga viene recuperato dalle [campi](../../../ado/reference/ado-api/fields-collection-ado.md) insieme e assegnata automaticamente agli **rstTitleAuthor** dal **StayInSync**  proprietà ogni volta che l'elemento padre **Recordset** passa a una nuova riga. Il ciclo interno vengono visualizzati quattro campi di ogni riga nel set di record accodato.  
  
```  
'BeginStayInSyncVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim rst As ADODB.Recordset  
    Dim rstTitleAuthor As New ADODB.Recordset  
    Dim strCnxn As String  
  
    ' Open the connection with Data Shape attributes  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider=MSDataShape;Data Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Create a recordset  
    Set rst = New ADODB.Recordset  
    rst.StayInSync = True  
    rst.Open "SHAPE {select * from Authors} " & _  
                   "APPEND ( { select * from titleauthor} AS chapTitleAuthor " & _  
                   "RELATE au_id TO au_id) ", Cnxn, , , adCmdText  
  
    Set rstTitleAuthor = rst("chapTitleAuthor").Value  
    Do Until rst.EOF  
        Debug.Print rst!au_fname & " " & rst!au_lname & " " & _  
                   rst!State & " " & rst!au_id  
  
        Do Until rstTitleAuthor.EOF  
            Debug.Print rstTitleAuthor(0) & " " & rstTitleAuthor(1) & " " & _  
                   rstTitleAuthor(2) & " " & rstTitleAuthor(3)  
            rstTitleAuthor.MoveNext  
        Loop  
  
        rst.MoveNext  
    Loop  
  
    ' Clean up  
    rst.Close  
    Cnxn.Close  
    Set rst = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' Clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndStayInSyncVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Fields Collection (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Proprietà StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)
