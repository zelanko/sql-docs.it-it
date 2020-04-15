---
title: Conformità alle funzioni Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33cd0ad4269ed59e31c8ab343ddbb01806afce04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305592"
---
# <a name="function-conformance"></a>Conformità della funzione
Nella tabella seguente viene indicato il livello di conformità di ogni funzione ODBC, in cui questa operazione è ben definita.  
  
|Funzione|Livello di conformità|  
|--------------|-----------------------|  
|**SQLAllocHandle**|Core|  
|**SQLBindCol**|Core|  
|**SQLBindParameter**|Nucleo[1]|  
|**SQLBrowseConnect**|Livello 1|  
|**Sqlbulkoperations**|Livello 1|  
|**SQLCancel**|Nucleo[1]|  
|**SQLCloseCursor**|Core|  
|**SQLColAttribute**|Nucleo[1]|  
|**SQLColumnPrivileges**|Livello 2|  
|**SQLColumns**|Core|  
|**SQLConnect**|Core|  
|**SQLCopyDesc (informazioni in lingua inglese)**|Core|  
|**SqlDataSourcesSQLDataSources**|Core|  
|**SQLDescribeCol**|Nucleo[1]|  
|**SQLDescribeParam**|Livello 2|  
|**Sqldisconnect**|Core|  
|**SQLDriverConnect**|Core|  
|**SQLDrivers**|Core|  
|**SQLEndTran**|Nucleo[1]|  
|**SQLExecDirect**|Core|  
|**SQLExecute**|Core|  
|**SQLFetch**|Core|  
|**SQLFetchScroll**|Nucleo[1]|  
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
|**SQLGetEnvAttr (Informazioni in lingua inglese)**|Core|  
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
|**SQLSetConnectAttr**|Nucleo[2]|  
|**SQLSetCursorName (Nome cursore)**|Core|  
|**SQLSetDescField**|Nucleo[1]|  
|**SQLSetDescRec**|Core|  
|**SQLSetEnvAttr**|Nucleo[2]|  
|**SQLSetPos**|Livello 1[1]|  
|**SQLSetStmtAttr**|Nucleo[2]|  
|**SQLSpecialColumns**|Nucleo[1]|  
|**SQLStatistics**|Core|  
|**SQLTablePrivileges**|Livello 2|  
|**SQLTables**|Core|  
  
 [1] Le caratteristiche significative di questa funzione sono disponibili solo a livelli di conformità più elevati.  
  
 [2] L'impostazione di determinati attributi su valori non predefiniti dipende dal livello di conformità. Per ulteriori informazioni, vedere la sezione successiva, [Conformità attributi](../../../odbc/reference/develop-app/attribute-conformance.md).
