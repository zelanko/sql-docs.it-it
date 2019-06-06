---
title: Chiama una Stored Procedure con un comando | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4763939e3eccd0bf4783df87141619cbc0fb011c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702322"
---
# <a name="calling-a-stored-procedure-with-a-command"></a>Chiamata di una stored procedure con Command
È possibile utilizzare un comando per chiamare una stored procedure. Nell'esempio di codice alla fine di questo argomento si riferisce a una stored procedure nel database di esempio Northwind, chiamato CustOrdersOrders, che viene definito come segue.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 Vedere la documentazione di SQL Server per altre informazioni su come definire e chiamare le stored procedure.  
  
 È simile al comando usato questa stored procedure [parametri dell'oggetto Command](../../../ado/guide/data/command-object-parameters.md). Accetta il parametro ID cliente e restituisce informazioni sugli ordini del cliente. Esempio di codice seguente usa questa stored procedure come origine per un oggetto ADO **Recordset**.  
  
 Utilizzando la stored procedure consente di accedere a un'altra funzionalità di ADO: il **parametri** collection **aggiornare** (metodo). Mediante questo metodo, ADO possa popolare automaticamente in tutte le informazioni sui parametri richiesti dal comando in fase di esecuzione. Si verifica una riduzione delle prestazioni usando questa tecnica, poiché ADO debba eseguire query sull'origine dati per le informazioni sui parametri.  
  
 Esistono altre differenze sostanziali tra l'esempio di codice seguente e il codice nel [parametri dell'oggetto Command](../../../ado/guide/data/command-object-parameters.md), in cui i parametri sono stati immessi manualmente. In questo codice viene innanzitutto impostata la **Prepared** proprietà **True** perché è una stored procedure SQL Server e viene precompilata dalla definizione. Secondo, il **CommandType** proprietà delle **comando** oggetto modificato in **adCmdStoredProc** nel secondo esempio per informare ADO che il comando è una stored procedure.  
  
 Infine, nel secondo esempio il parametro deve farvi riferimento.{0}{0}i indice quando si imposta il valore, perché si potrebbe non conosce il nome del parametro in fase di progettazione. Se si conosce il nome del parametro, è possibile impostare il nuovo [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) proprietà delle **comando** dell'oggetto su True e fare riferimento al nome della proprietà. Ci si potrebbe chiedere perché la posizione del primo parametro indicato nella stored procedure (@CustomerID) è 1 anziché 0 (`objCmd(1) = "ALFKI"`). Questo avviene perché il parametro 0 contiene un valore restituito dalla procedura di SQL Server archiviati.  
  
```  
'BeginAutoParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set CommandText equal to the stored procedure name.  
    objCmd.CommandText = "CustOrdersOrders"  
    objCmd.CommandType = adCmdStoredProc  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Automatically fill in parameter info from stored procedure.  
    objCmd.Parameters.Refresh  
  
    ' Set the param value.  
    objCmd(1) = "ALFKI"  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' ...then set new param value, re-execute command, and display.  
    objCmd(1) = "CACTU"  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndAutoParamCmd  
  
'BeginNewConnection  
Private Function GetNewConnection() As ADODB.Connection  
    Dim oCn As New ADODB.Connection  
    Dim sCnStr As String  
  
    sCnStr = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    oCn.Open sCnStr  
  
    If oCn.State = adStateOpen Then  
        Set GetNewConnection = oCn  
    End If  
  
End Function  
'EndNewConnection  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Articolo della Knowledge Base 117500](https://go.microsoft.com/fwlink/?LinkId=117500)
