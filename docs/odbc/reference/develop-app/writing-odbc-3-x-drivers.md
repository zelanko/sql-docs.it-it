---
title: La scrittura di driver ODBC 3.x | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f548e1496ce45d9fdb4677fd9659de349e5c5cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62636106"
---
# <a name="writing-odbc-3x-drivers"></a>Scrittura di driver ODBC 3.x
La tabella seguente illustra il supporto di funzione in un'applicazione ODBC 3. *x* driver e un'applicazione ODBC e il mapping eseguito da Gestione Driver quando le funzioni vengono chiamate su un'applicazione ODBC 3. *x* driver.  
  
|Funzione|Supportato<br /><br /> da un<br /><br /> ODBC 3.*x*<br /><br /> driver?|Supportato<br /><br /> da un<br /><br /> ODBC 3.*x*<br /><br /> applicazione?|Il mapping o supportate<br /><br /> da ODBC 3. *x*<br /><br /> Gestione driver per<br /><br /> un'applicazione ODBC 3. *x* driver?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|No|No[1]|Yes|  
|**SQLAllocEnv**|No|No[1]|Yes|  
|**SQLAllocHandle**|Yes|Yes|No|  
|**SQLAllocStmt**|No|No[1]|Yes|  
|**SQLBindCol**|Yes|Yes|No|  
|**SQLBindParam**|No|Sì [2]|Yes|  
|**SQLBindParameter**|Yes|Yes|No|  
|**SQLBrowseConnect**|Yes|Yes|No|  
|**SQLBulkOperations**|Yes|Yes|no|  
|**SQLCancel**|Yes|Yes|no|  
|**SQLCloseCursor**|Yes|Yes|No|  
|**SQLColAttribute**|Yes|Yes|no|  
|**SQLColAttributes**|No[3]|No|Yes|  
|**SQLColumnPrivileges**|Yes|Yes|No|  
|**SQLColumns**|Yes|Yes|No|  
|**SQLConnect**|Yes|Yes|no|  
|**SQLCopyDesc**|Yes|Yes|Sì [4]|  
|**SQLDataSources**|no|Yes|Yes|  
|**SQLDescribeCol**|Yes|Yes|No|  
|**SQLDescribeParam**|Yes|Yes|No|  
|**SQLDisconnect**|Yes|Yes|No|  
|**SQLDriverConnect**|Yes|Yes|No|  
|**SQLDrivers**|no|Yes|Yes|  
|**SQLEndTran**|Yes|Yes|No|  
|**SQLError**|no|No[1]|Yes|  
|**SQLExecDirect**|Yes|Yes|No|  
|**SQLExecute**|Yes|Yes|No|  
|**SQLExtendedFetch**|Yes|No|No|  
|**SQLFetch**|Yes|Yes|no|  
|**SQLFetchScroll**|Yes|Yes|No|  
|**SQLForeignKeys**|Yes|Yes|no|  
|**SQLFreeConnect**|No|Sì [1]|Yes|  
|**SQLFreeEnv**|No|Sì [1]|Yes|  
|**SQLFreeHandle**|Yes|Yes|no|  
|**SQLFreeStmt**|Yes|Yes|No|  
|**SQLGetConnectAttr**|Yes|Yes|no|  
|**SQLGetConnectOption**|No[5]|No[1]|Yes|  
|**SQLGetCursorName**|Yes|Yes|No|  
|**SQLGetData**|Yes|Yes|no|  
|**SQLGetDescField**|Yes|Yes|No|  
|**SQLGetDescRec**|Yes|Yes|no|  
|**SQLGetDiagField**|Yes|Yes|No|  
|**SQLGetDiagRec**|Yes|Yes|No|  
|**SQLGetEnvAttr**|Yes|Yes|no|  
|**SQLGetFunctions**|No[6]|Yes|Yes|  
|**SQLGetInfo**|Yes|Yes|No|  
|**SQLGetStmtAttr**|Yes|Yes|No|  
|**SQLGetStmtOption**|No[5]|No[1]|Yes|  
|**SQLGetTypeInfo**|Yes|Yes|No|  
|**SQLMoreResults**|Yes|Yes|No|  
|**SQLNativeSql**|Yes|Yes|No|  
|**SQLNumParams**|Yes|Yes|No|  
|**SQLNumResultCols**|Yes|Yes|No|  
|**SQLParamData**|Yes|Yes|no|  
|**SQLParamOptions**|No|No|Yes|  
|**SQLPrepare**|Yes|Yes|No|  
|**SQLPrimaryKeys**|Yes|Yes|No|  
|**SQLProcedureColumns**|Yes|Yes|No|  
|**SQLProcedures**|Yes|Yes|no|  
|**SQLPutData**|Yes|Yes|no|  
|**SQLRowCount**|Yes|Yes|no|  
|**SQLSetConnectAttr**|Yes|Yes|No|  
|**SQLSetConnectOption**|No[5]|No[1]|Yes|  
|**SQLSetCursorName**|Yes|Yes|No|  
|**SQLSetDescField**|Yes|Yes|no|  
|**SQLSetDescRec**|Yes|Yes|No|  
|**SQLSetEnvAttr**|Yes|Yes|No|  
|**SQLSetPos**|Yes|Yes|No|  
|**SQLSetParam**|No|No|Yes|  
|**SQLSetScrollOption**|Yes|Yes|No|  
|**SQLSetStmtAttr**|Yes|Yes|No|  
|**SQLSetStmtOption**|No[5]|No[1]|Yes|  
|**SQLSpecialColumns**|Yes|Yes|No|  
|**SQLStatistics**|Yes|Yes|No|  
|**SQLTablePrivileges**|Yes|Yes|No|  
|**SQLTables**|Yes|Yes|No|  
|**SQLTransact**|No|No[1]|Yes|  
  
 [1] questa funzione è deprecata in ODBC 3. *x*. ODBC 3. *x* applicazioni non deve usare questa funzione. Tuttavia, un'applicazione compatibile con ISO CLI o Open Group può chiamare questa funzione.  
  
 [2] ODBC 3. *x* le applicazioni devono utilizzare **SQLBindParameter** anziché **SQLBindParam**. Tuttavia, un'applicazione compatibile con ISO CLI o Open Group può chiamare questa funzione.  
  
 [3] gli sviluppatori di driver di necessario notare che l'API ODBC 2. *x* SQL_COLUMN_PRECISION SQL_COLUMN_SCALE e SQL_COLUMN_LENGTH devono essere supportate con gli attributi di colonna **SQLColAttribute**.  
  
 [4] **SQLCopyDesc** viene implementato parzialmente da Gestione Driver quando un descrittore di vengono copiato tra le connessioni che appartengono a diversi driver. I driver necessari per supportare **SQLCopyDesc** tra due di loro connessioni. Le funzioni come **SQLDrivers**, che vengono implementate esclusivamente da Gestione Driver, non vengono visualizzati nell'elenco.  
  
 [5] in determinate circostanze, i driver potrebbe essere necessario supportare questa funzione. Per altre informazioni, vedere la pagina di riferimento relativa a questa funzione.  
  
 [6] i driver possono scegliere di supportare **SQLGetFunctions** se il set di funzioni supportate dal driver varia da una connessione alla connessione.
