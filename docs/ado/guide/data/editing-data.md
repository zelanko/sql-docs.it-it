---
title: Modifica di dati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
author: rothja
ms.author: jroth
ms.openlocfilehash: cc80c8ad9985efc21e2f583d8ca72751e21c1a2b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761037"
---
# <a name="editing-data"></a>Modifica dei dati
È stato illustrato come usare ADO per connettersi a un'origine dati, eseguire un comando, ottenere i risultati in un oggetto **Recordset** e spostarsi all'interno del **Recordset**. Questa sezione è incentrata sulla successiva operazione ADO fondamentale: modifica dei dati.  
  
 Questa sezione continua a usare il **Recordset** di esempio introdotto nell' [esame dei dati](../../../ado/guide/data/examining-data.md), con una modifica importante. Per aprire il **Recordset**, viene usato il codice seguente:  
  
```  
'BeginEditIntro  
    Dim strSQL As String  
    Dim objRs1 As ADODB.Recordset  
  
    strSQL = "SELECT * FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
  
    objRs1.Open strSQL, GetNewConnection, adOpenStatic, _  
                adLockBatchOptimistic, adCmdText  
  
    ' Disconnect the Recordset from the Connection object.  
    Set objRs1.ActiveConnection = Nothing  
'EndEditIntro  
```  
  
 La modifica importante del codice comporta l'impostazione della proprietà **CursorLocation** dell'oggetto **Connection** uguale a **adUseClient** nella funzione *GetNewConnection* (mostrata nell'esempio seguente), che indica l'utilizzo di un cursore client. Per ulteriori informazioni sulle differenze tra i cursori lato client e lato server, vedere informazioni sui [blocchi e sui cursori](../../../ado/guide/data/understanding-cursors-and-locks.md).  
  
 L'impostazione **adUseClient** della proprietà **CursorLocation** sposta la posizione del cursore dall'origine dati (la SQL Server, in questo caso) al percorso del codice client (la workstation desktop). Questa impostazione impone a ADO di richiamare il motore del cursore client per OLE DB sul client per creare e gestire il cursore.  
  
 È anche possibile notare che il parametro **LockType** del metodo **Open** è stato modificato in **adLockBatchOptimistic**. Verrà aperto il cursore in modalità batch. Il provider memorizza nella cache più modifiche e le scrive nell'origine dati sottostante solo quando si chiama il metodo **UpdateBatch** . Le modifiche apportate al **Recordset** non verranno aggiornate nel database fino a quando non viene chiamato il metodo **UpdateBatch** .  
  
 Infine, il codice in questa sezione usa una versione modificata della funzione GetNewConnection. Questa versione della funzione restituisce ora un cursore sul lato client. La funzione ha un aspetto simile al seguente:  
  
```  
'BeginNewConnection  
Public Function GetNewConnection() As ADODB.Connection  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim strConnStr As String  
  
    strConnStr = "Provider='SQLOLEDB';Initial Catalog='Northwind';" & _  
                 "Data Source='MySqlServer';Integrated Security='SSPI';"  
  
    objConn.ConnectionString = strConnStr  
    objConn.CursorLocation = adUseClient  
    objConn.Open  
  
    Set GetNewConnection = objConn  
  
    Exit Function  
  
ErrHandler:  
    Set objConn = Nothing  
    Set GetNewConnection = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Function  
'EndNewConnection  
```  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Modifica di record esistenti](../../../ado/guide/data/editing-existing-records.md)  
  
-   [Aggiunta di record](../../../ado/guide/data/adding-records.md)  
  
-   [Determinazione delle funzionalità supportate](../../../ado/guide/data/determining-what-is-supported.md)  
  
-   [Eliminazione di record con il metodo Delete](../../../ado/guide/data/deleting-records-using-the-delete-method.md)  
  
-   [Alternative: uso di istruzioni SQL](../../../ado/guide/data/alternatives-using-sql-statements.md)
