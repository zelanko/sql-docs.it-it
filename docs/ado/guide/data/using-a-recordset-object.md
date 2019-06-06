---
title: Uso di un oggetto Recordset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 01c630d8-eb35-4bd0-a99f-7c0f85316cc1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5fc27ed728483fd42d90e599580ce32194f08b99
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699901"
---
# <a name="using-a-recordset-object"></a>Uso di un oggetto Recordset
In alternativa, è possibile usare **Open** per stabilire una connessione in modo implicito e inviare un comando tramite la connessione in un'unica operazione. Ad esempio, in Visual Basic:  
  
```  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
  
' Create and Open the Recordset object.  
Set oRs = New ADODB.Recordset  
oRs.CursorLocation = adUseClient  
oRs.Open sSQL, sConn, adOpenStatic, _  
               adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
oRs.Close          
Set oRs = Nothing  
```  
  
 Si noti che **oRs.Open** accetta una stringa di connessione (*sConn*), al posto di un **connessione** oggetto (*oConn*), come valore del relativo  **ActiveConnection** parametro. Inoltre viene attivato il tipo di cursore lato client impostando il **CursorLocation** proprietà le **Recordset** oggetto. Anche in questo caso, confrontare questa operazione con il **HelloData** esempio.
