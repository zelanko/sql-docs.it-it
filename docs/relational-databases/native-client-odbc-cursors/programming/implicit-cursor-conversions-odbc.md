---
title: Conversioni implicite dei cursori (ODBC) | Documenti di Microsoft
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eebbfcefdf5c4c9e2d6ed1409e3c119f598a22d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013605"
---
# <a name="implicit-cursor-conversions-odbc"></a>Conversioni implicite dei cursori (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Le applicazioni possono richiedere un tipo di cursore attraverso [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) e quindi eseguire un'istruzione SQL che non è supportata dai cursori server del tipo richiesto. Una chiamata a **SQLExecute** oppure **SQLExecDirect** restituisce SQL_SUCCESS_WITH_INFO e **SQLGetDiagRec** restituisce:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 L'applicazione può determinare il tipo di cursore viene ora viene usato chiamando **SQLGetStmtOption** impostato su SQL_CURSOR_TYPE. La conversione del tipo di cursore viene applicata a una sola istruzione. Alla successiva **SQLExecDirect** oppure **SQLExecute** verrà eseguita usando le impostazioni del cursore istruzione originale.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulla programmazione dei cursori &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
