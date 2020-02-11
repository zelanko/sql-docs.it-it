---
title: Esempio di metodi Save e Open (VB) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931192"
---
# <a name="save-and-open-methods-example-vb"></a>Esempio dei metodi Save e Open (VB)
Questi tre esempi illustrano il modo in cui i metodi [Save](../../../ado/reference/ado-api/save-method.md) e [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) possono essere usati insieme.  
  
 Si supponga che si stia procedendo a un viaggio di lavoro e che si voglia eseguire una tabella da un database. Prima di procedere, è possibile accedere ai dati come [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) e salvarli in un modulo trasportabile. Quando si arriva alla destinazione, si accede al **Recordset** come **Recordset**locale disconnesso. Apportare modifiche al **Recordset**e quindi salvarlo di nuovo. Infine, quando si torna a casa, si esegue nuovamente la connessione al database e la si aggiorna con le modifiche apportate in viaggio.  
  
 Per prima cosa, accedere alla tabella ***authors*** e salvarla.  
  
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
  
 A questo punto, si è arrivati alla destinazione. Sarà possibile accedere alla tabella ***authors*** come **Recordset**locale e disconnesso. È necessario disporre del provider **MSPersist** nel computer in uso per accedere al file salvato, a:\pubs.XML.  
  
```  
Attribute VB_Name = "Save"  
```  
  
 Infine, viene restituito Home. A questo punto, aggiornare il database con le modifiche apportate.  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Open (recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Oggetto recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Ulteriori informazioni sulla persistenza dei recordset](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Metodo Save](../../../ado/reference/ado-api/save-method.md)
