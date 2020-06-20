---
title: Batch di istruzioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC], batches
- batches [ODBC]
- ODBC applications, statements
- multiple statements, batches
- SQLMoreResults function
- SQLExecDirect function
ms.assetid: 057d7c1c-1428-4780-9447-a002ea741188
author: rothja
ms.author: jroth
ms.openlocfilehash: 4818b67766dafe851035041c8fd5137a0dfade73
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84999197"
---
# <a name="batches-of-statements"></a>Batch di istruzioni
  Un batch di [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzioni contiene due o più istruzioni, separate da un punto e virgola (;), compilate in una singola stringa passata a **SQLExecDirect** o alla [funzione SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360). Ad esempio:  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 I batch possono essere più efficienti rispetto all'invio separato delle istruzioni in quanto il traffico di rete viene spesso ridotto. Utilizzare [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) per posizionare il set di risultati successivo al termine del set di risultati corrente.  
  
 I batch possono essere sempre utilizzati quando gli attributi del cursore ODBC sono impostati sui valori predefiniti di un cursore forward only in sola lettura con dimensioni del set di righe pari a 1.  
  
 Se un batch viene eseguito quando si utilizzano cursori del server in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], questi ultimi vengono convertiti implicitamente in set di risultati predefiniti. **SQLExecDirect** o **sqlexecute** restituiscono SQL_SUCCESS_WITH_INFO e una chiamata a **SQLGetDiagRec** restituisce:  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di istruzioni &#40;ODBC&#41;](executing-statements-odbc.md)  
  
  
