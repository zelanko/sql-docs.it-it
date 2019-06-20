---
title: Esempio di proprietà InternetTimeout (VB) | Microsoft Docs
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
- InternetTimeout property [ADO], Visual Basic example
ms.assetid: b35d2f4a-449c-4170-aab6-9ff88c890043
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6b08e09e9d46ac31cf08205a7e9336194c4d4858
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712562"
---
# <a name="internettimeout-property-example-vb"></a>Esempio della proprietà InternetTimeout (VB)
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Questo esempio viene illustrato il [InternetTimeout](../../../ado/reference/rds-api/internettimeout-property-rds.md) proprietà, che sia disponibile la [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) e [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) oggetti. Questo esempio Usa la **DataControl** dell'oggetto e imposta il timeout su 20 secondi.  
  
```  
'BeginInternetTimeoutVB  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim dc As RDS.DataControl  
    Dim rst As ADODB.Recordset  
    Set dc = New RDS.DataControl  
  
    dc.Server = "https://MyServer"  
    dc.ExecuteOptions = 1  
    dc.FetchOptions = 1  
    dc.Connect = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    dc.SQL = "SELECT * FROM Authors"  
     ' Wait at least 20 seconds  
    dc.InternetTimeout = 200  
  
    dc.Refresh  
     ' Use another Recordset as a convenience  
    Set rst = dc.Recordset  
    Do While Not rst.EOF  
       Debug.Print rst!au_fname & " " & rst!au_lname  
       rst.MoveNext  
    Loop  
  
    If rst.State = adStateOpen Then rst.Close  
    Set rst = Nothing  
    Set dc = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
    Set dc = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndInternetTimeoutVB  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataSpace Object (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Proprietà InternetTimeout (Servizi Desktop remoto)](../../../ado/reference/rds-api/internettimeout-property-rds.md)


