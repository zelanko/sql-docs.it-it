---
title: Conversioni implicite del cursore (ODBC) Documenti Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ced726893b0f287db6b1fec7c8d16c6b844eea2b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298381"
---
# <a name="implicit-cursor-conversions-odbc"></a>Conversioni implicite dei cursori (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Le applicazioni possono richiedere un tipo di cursore tramite [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) e quindi eseguire un'istruzione SQL non supportata dai cursori del server del tipo richiesto. Una chiamata a SQLExecute o **SQLExecDirect** restituisce SQL_SUCCESS_WITH_INFO e SQLGetDiagRec restituisce:A call to **SQLExecute** or SQLExecDirect returns SQL_SUCCESS_WITH_INFO and **SQLGetDiagRec** returns:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 L'applicazione può determinare il tipo di cursore utilizzato chiamando **SQLGetStmtOption** impostato su SQL_CURSOR_TYPE. La conversione del tipo di cursore viene applicata a una sola istruzione. Il successivo **SQLExecDirect** o **SQLExecute** verrà eseguito utilizzando le impostazioni del cursore dell'istruzione originale.  
  
## <a name="see-also"></a>Vedere anche  
 [Dettagli di programmazione del cursore &#40;&#41;ODBCCursor Programming Details to ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
