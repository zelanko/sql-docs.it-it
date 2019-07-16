---
title: Salvare e aprire l'esempio di metodi (VB) | Microsoft Docs
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
- Save method [ADO], Visual Basic example
- Open method [ADO]
ms.assetid: ddccdf58-9c57-4c9b-8b7f-0cf193f955fb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d42488f8f167cc7c98f663478c742963d24253c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931192"
---
# <a name="save-and-open-methods-example-vb"></a>Esempio dei metodi Save e Open (VB)
Questi tre esempi che illustrano come il [salvare](../../../ado/reference/ado-api/save-method.md) e [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodi possono essere usati insieme.  
  
 Si supponga che si prevede un viaggio d'affari e vuole portare con sé una tabella da un database. Prima di procedere, si accede ai dati come una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) e salvarlo in un form trasportabile. Quando si arriva a rappresenti la destinazione, è accedere il **Recordset** come un'unità locale disconnesso **Recordset**. Si apportano modifiche per il **Recordset**e quindi salvarlo nuovamente. Infine, quando si ritorna home, riconnettersi al database e aggiornarlo con le modifiche apportate in viaggio.  
  
 In primo luogo, accedere e salvare il ***autori*** tabella.  
  
```  
'BeginSaveVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstAuthors As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "SELECT au_id, au_lname, au_fname, city, phone FROM Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenDynamic, adLockOptimistic, adCmdText  
  
    'For sake of illustration, save the Recordset to a diskette in XML format  
    rstAuthors.Save "c:\Pubs.xml", adPersistXML  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    'clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndSaveVB  
```  
  
 Si è arrivati a questo punto, la destinazione. Si accederà il ***Authors*** tabella come un'unità locale disconnesso **Recordset**. È necessario disporre di **MSPersist** provider nel computer in cui si usa per accedere al file salvato, a:\Pubs.xml.  
  
```  
Attribute VB_Name = "Save"  
```  
  
 Infine, restituire home. A questo punto è possibile aggiornare il database con le modifiche.  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Informazioni sulla persistenza dei Recordset](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Metodo Save](../../../ado/reference/ado-api/save-method.md)
