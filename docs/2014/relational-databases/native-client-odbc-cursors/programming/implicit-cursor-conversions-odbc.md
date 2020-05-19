---
title: Conversioni implicite di cursori (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 99395f9a8dbcb812f5a7764634d42489526875af
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705608"
---
# <a name="implicit-cursor-conversions-odbc"></a>Conversioni implicite dei cursori (ODBC)
  Le applicazioni possono richiedere un tipo di cursore tramite [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) e quindi eseguire un'istruzione SQL non supportata dai cursori del server del tipo richiesto. Una chiamata a **SQLExecute** o **SQLExecDirect** restituisce SQL_SUCCESS_WITH_INFO e **SQLGetDiagRec** restituisce:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 L'applicazione può determinare il tipo di cursore usato chiamando **SQLGetStmtOption** impostato su SQL_CURSOR_TYPE. La conversione del tipo di cursore viene applicata a una sola istruzione. Il successivo **SQLExecDirect** o **SQLExecute** verrà eseguito utilizzando le impostazioni originali del cursore dell'istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Dettagli sulla programmazione dei cursori &#40;&#41;ODBC](cursor-programming-details-odbc.md)  
  
  
