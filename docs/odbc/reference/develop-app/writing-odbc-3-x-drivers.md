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
ms.openlocfilehash: fb403cef47f901cdb43bbb32c669ba68aa34913d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078902"
---
# <a name="writing-odbc-3x-drivers"></a>Scrittura di driver ODBC 3.x
La tabella seguente illustra il supporto di funzione in un'applicazione ODBC 3. *x* driver e un'applicazione ODBC e il mapping eseguito da Gestione Driver quando le funzioni vengono chiamate su un'applicazione ODBC 3. *x* driver.  
  
|Funzione|Supportato<br /><br /> da un<br /><br /> ODBC 3.*x*<br /><br /> driver?|Supportato<br /><br /> da un<br /><br /> ODBC 3.*x*<br /><br /> applicazione?|Il mapping o supportate<br /><br /> da ODBC 3. *x*<br /><br /> Gestione driver per<br /><br /> un'applicazione ODBC 3. *x* driver?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|No|No[1]|Yes|  
|**SQLAllocEnv**|No|No[1]|Yes|  
|**SQLAllocHandle**|Yes|Sì|No|  
|**SQLAllocStmt**|No|No[1]|Yes|  
|**SQLBindCol**|Yes|Sì|No|  
|**SQLBindParam**|No|Sì [2]|Yes|  
|**SQLBindParameter**|Yes|Sì|No|  
|**SQLBrowseConnect**|Yes|Sì|No|  
|**SQLBulkOperations**|Yes|Sì|No|  
|**SQLCancel**|Yes|Sì|No|  
|**SQLCloseCursor**|Yes|Sì|No|  
|**SQLColAttribute**|Yes|Sì|No|  
|**SQLColAttributes**|No[3]|No|Yes|  
|**SQLColumnPrivileges**|Yes|Sì|No|  
|**SQLColumns**|Yes|Sì|No|  
|**SQLConnect**|Yes|Sì|No|  
|**SQLCopyDesc**|Yes|Yes|Sì [4]|  
|**SQLDataSources**|No|Yes|Yes|  
|**SQLDescribeCol**|Yes|Sì|No|  
|**SQLDescribeParam**|Yes|Sì|No|  
|**SQLDisconnect**|Yes|Sì|No|  
|**SQLDriverConnect**|Yes|Sì|No|  
|**SQLDrivers**|No|Yes|Yes|  
|**SQLEndTran**|Yes|Sì|No|  
|**SQLError**|No|No[1]|Yes|  
|**SQLExecDirect**|Yes|Sì|No|  
|**SQLExecute**|Yes|Sì|No|  
|**SQLExtendedFetch**|Yes|No|No|  
|**SQLFetch**|Yes|Sì|No|  
|**SQLFetchScroll**|Yes|Sì|No|  
|**SQLForeignKeys**|Yes|Sì|No|  
|**SQLFreeConnect**|No|Sì [1]|Yes|  
|**SQLFreeEnv**|No|Sì [1]|Yes|  
|**SQLFreeHandle**|Yes|Sì|No|  
|**SQLFreeStmt**|Yes|Sì|No|  
|**SQLGetConnectAttr**|Yes|Sì|No|  
|**SQLGetConnectOption**|[5]|No[1]|Yes|  
|**SQLGetCursorName**|Yes|Sì|No|  
|**SQLGetData**|Yes|Sì|No|  
|**SQLGetDescField**|Yes|Sì|No|  
|**SQLGetDescRec**|Yes|Sì|No|  
|**SQLGetDiagField**|Yes|Sì|No|  
|**SQLGetDiagRec**|Yes|Sì|No|  
|**SQLGetEnvAttr**|Yes|Sì|No|  
|**SQLGetFunctions**|No[6]|Yes|Yes|  
|**SQLGetInfo**|Yes|Sì|No|  
|**SQLGetStmtAttr**|Yes|Sì|No|  
|**SQLGetStmtOption**|[5]|No[1]|Yes|  
|**SQLGetTypeInfo**|Yes|Sì|No|  
|**SQLMoreResults**|Yes|Sì|No|  
|**SQLNativeSql**|Yes|Sì|No|  
|**SQLNumParams**|Yes|Sì|No|  
|**SQLNumResultCols**|Yes|Sì|No|  
|**SQLParamData**|Yes|Sì|No|  
|**SQLParamOptions**|No|No|Yes|  
|**SQLPrepare**|Yes|Sì|No|  
|**SQLPrimaryKeys**|Yes|Sì|No|  
|**SQLProcedureColumns**|Yes|Sì|No|  
|**SQLProcedures**|Yes|Sì|No|  
|**SQLPutData**|Yes|Sì|No|  
|**SQLRowCount**|Yes|Sì|No|  
|**SQLSetConnectAttr**|Yes|Sì|No|  
|**SQLSetConnectOption**|[5]|No[1]|Yes|  
|**SQLSetCursorName**|Yes|Sì|No|  
|**SQLSetDescField**|Yes|Sì|No|  
|**SQLSetDescRec**|Yes|Sì|No|  
|**SQLSetEnvAttr**|Yes|Sì|No|  
|**SQLSetPos**|Yes|Sì|No|  
|**SQLSetParam**|No|No|Yes|  
|**SQLSetScrollOption**|Yes|Sì|No|  
|**SQLSetStmtAttr**|Yes|Sì|No|  
|**SQLSetStmtOption**|[5]|No[1]|Yes|  
|**SQLSpecialColumns**|Yes|Sì|No|  
|**SQLStatistics**|Yes|Sì|No|  
|**SQLTablePrivileges**|Yes|Sì|No|  
|**SQLTables**|Yes|Sì|No|  
|**SQLTransact**|No|No[1]|Yes|  
  
 [1] questa funzione è deprecata in ODBC 3. *x*. ODBC 3. *x* applicazioni non deve usare questa funzione. Tuttavia, un'applicazione compatibile con ISO CLI o Open Group può chiamare questa funzione.  
  
 [2] ODBC 3. *x* le applicazioni devono utilizzare **SQLBindParameter** anziché **SQLBindParam**. Tuttavia, un'applicazione compatibile con ISO CLI o Open Group può chiamare questa funzione.  
  
 [3] gli sviluppatori di driver di necessario notare che l'API ODBC 2. *x* SQL_COLUMN_PRECISION SQL_COLUMN_SCALE e SQL_COLUMN_LENGTH devono essere supportate con gli attributi di colonna **SQLColAttribute**.  
  
 [4] **SQLCopyDesc** viene implementato parzialmente da Gestione Driver quando un descrittore di vengono copiato tra le connessioni che appartengono a diversi driver. I driver necessari per supportare **SQLCopyDesc** tra due di loro connessioni. Le funzioni come **SQLDrivers**, che vengono implementate esclusivamente da Gestione Driver, non vengono visualizzati nell'elenco.  
  
 [5] in determinate circostanze, i driver potrebbe essere necessario supportare questa funzione. Per altre informazioni, vedere la pagina di riferimento relativa a questa funzione.  
  
 [6] i driver possono scegliere di supportare **SQLGetFunctions** se il set di funzioni supportate dal driver varia da una connessione alla connessione.
