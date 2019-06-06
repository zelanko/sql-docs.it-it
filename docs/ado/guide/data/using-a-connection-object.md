---
title: Uso di un oggetto connessione | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 4b34f971-5699-43e7-9b15-137d334fa66e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b19713028bcc5569a6a4aace4528e7c725cf7d0e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704549"
---
# <a name="using-a-connection-object"></a>Uso di un oggetto Connection
Prima di aprire una **connessione** dell'oggetto, è necessario definire alcune informazioni sull'origine dati e tipo di connessione. Viene assegnata la maggior parte di queste informazioni il *ConnectionString* parametro del [metodo Open](../../../ado/reference/ado-api/open-method-ado-connection.md) sul **connessione** oggetto, o tramite il [ConnectionString proprietà](../../../ado/reference/ado-api/connectionstring-property-ado.md) nella **connessione** oggetto. Una stringa di connessione è costituita da un elenco di coppie di argomento/valore separate da punti e virgola, con i valori racchiusi tra virgolette singole. Ad esempio:  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  È anche possibile specificare un nome di origine dati ODBC (DSN) o in un file di Data Link (UDL) in una stringa di connessione. Per altre informazioni sui nomi, vedere [gestione di origini dati](../../../odbc/admin/managing-data-sources.md) nel riferimento per programmatori ODBC. Per altre informazioni sui file UDL, vedere [Introduzione all'API di collegamento dati](https://msdn.microsoft.com/95c180ea-bd4f-4dca-b95a-576afd135bbc) nel riferimento delle per programmatori OLE DB.  
  
 In genere, si stabilisce una connessione chiamando il **venga** metodo con un oggetto appropriato un *stringa di connessione* come parametro. Nel frammento di codice Visual Basic seguente è riportato un esempio:  
  
```  
Dim oConn As ADODB.Connection  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
' Open a connection.  
Set oConn = New ADODB.Connection  
.Open   
  
' Make a query over the connection.  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
Set oRs = New ADODB.Recordset  
oRs.Open sSQL, , adOpenStatic, adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
' Close the connection.  
oConn.Close  
Set oConn = Nothing  
  
```  
  
 Di seguito **oRs.Open** accetta un **connessione** oggetto (*oConn*) variabile come valore del relativo *ActiveConnection* parametro. Inoltre, il **Connection.CursorLocation** proprietà si presuppone che il valore predefinito **adUseServer**. Per ovviare a questo per il [HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md) riportato nella sezione precedente. L'istruzione seguente comporta errori di run-time.  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```
