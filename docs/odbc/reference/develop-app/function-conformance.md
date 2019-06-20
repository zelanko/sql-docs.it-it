---
title: Funzione della conformità | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], function
- function conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: bb5d68cf-d238-481e-babc-2e9401b4700e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6cb2f56113487922866573caf3b5f8b67fff7c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061579"
---
# <a name="function-conformance"></a>Conformità della funzione
Nella tabella seguente indica il livello di conformità di ogni funzione ODBC, in cui si è ben definito.  
  
|Funzione|Livello di conformità|  
|--------------|-----------------------|  
|**SQLAllocHandle**|Core|  
|**SQLBindCol**|Core|  
|**SQLBindParameter**|Core[1]|  
|**SQLBrowseConnect**|Livello 1|  
|**SQLBulkOperations**|Livello 1|  
|**SQLCancel**|Core[1]|  
|**SQLCloseCursor**|Core|  
|**SQLColAttribute**|Core[1]|  
|**SQLColumnPrivileges**|Livello 2|  
|**SQLColumns**|Core|  
|**SQLConnect**|Core|  
|**SQLCopyDesc**|Core|  
|**SQLDataSources**|Core|  
|**SQLDescribeCol**|Core[1]|  
|**SQLDescribeParam**|Livello 2|  
|**SQLDisconnect**|Core|  
|**SQLDriverConnect**|Core|  
|**SQLDrivers**|Core|  
|**SQLEndTran**|Core[1]|  
|**SQLExecDirect**|Core|  
|**SQLExecute**|Core|  
|**SQLFetch**|Core|  
|**SQLFetchScroll**|Core[1]|  
|**SQLForeignKeys**|Livello 2|  
|**SQLFreeHandle**|Core|  
|**SQLFreeStmt**|Core|  
|**SQLGetConnectAttr**|Core|  
|**SQLGetCursorName**|Core|  
|**SQLGetData**|Core|  
|**SQLGetDescField**|Core|  
|**SQLGetDescRec**|Core|  
|**SQLGetDiagField**|Core|  
|**SQLGetDiagRec**|Core|  
|**SQLGetEnvAttr**|Core|  
|**SQLGetFunctions**|Core|  
|**SQLGetInfo**|Core|  
|**SQLGetStmtAttr**|Core|  
|**SQLGetTypeInfo**|Core|  
|**SQLMoreResults**|Livello 1|  
|**SQLNativeSql**|Core|  
|**SQLNumParams**|Core|  
|**SQLNumResultCols**|Core|  
|**SQLParamData**|Core|  
|**SQLPrepare**|Core|  
|**SQLPrimaryKeys**|Livello 1|  
|**SQLProcedureColumns**|Livello 1|  
|**SQLProcedures**|Livello 1|  
|**SQLPutData**|Core|  
|**SQLRowCount**|Core|  
|**SQLSetConnectAttr**|Core[2]|  
|**SQLSetCursorName**|Core|  
|**SQLSetDescField**|Core[1]|  
|**SQLSetDescRec**|Core|  
|**SQLSetEnvAttr**|Core[2]|  
|**SQLSetPos**|Livello 1 [1]|  
|**SQLSetStmtAttr**|Core[2]|  
|**SQLSpecialColumns**|Core[1]|  
|**SQLStatistics**|Core|  
|**SQLTablePrivileges**|Livello 2|  
|**SQLTables**|Core|  
  
 [1] importanti funzionalità di questa funzione sono disponibili solo a livelli superiori di conformità.  
  
 [2] impostazione determinati attributi su valori non predefiniti varia in base al livello di conformità. Per altre informazioni, vedere la sezione successiva [conformità dell'attributo](../../../odbc/reference/develop-app/attribute-conformance.md).
