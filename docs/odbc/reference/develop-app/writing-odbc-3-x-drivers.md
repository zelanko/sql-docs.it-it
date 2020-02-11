---
title: Scrittura di driver ODBC 3. x | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078902"
---
# <a name="writing-odbc-3x-drivers"></a>Scrittura di driver ODBC 3.x
La tabella seguente illustra il supporto delle funzioni in un ODBC 3. driver *x* e un'applicazione ODBC e mapping eseguito da Gestione driver quando le funzioni vengono chiamate a un ODBC 3. driver *x* .  
  
|Funzione|Supportato<br /><br /> da un<br /><br /> ODBC 3. *x*<br /><br /> driver?|Supportato<br /><br /> da un<br /><br /> ODBC 3. *x*<br /><br /> applicazione?|Mappato/supportato<br /><br /> da ODBC 3. *x*<br /><br /> Gestione driver a<br /><br /> ODBC 3. driver *x* ?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|No|No [1]|Sì|  
|**SQLAllocEnv**|No|No [1]|Sì|  
|**SQLAllocHandle**|Sì|Sì|No|  
|**SQLAllocStmt**|No|No [1]|Sì|  
|**SQLBindCol**|Sì|Sì|No|  
|**SQLBindParam**|No|Sì [2]|Sì|  
|**SQLBindParameter**|Sì|Sì|No|  
|**SQLBrowseConnect**|Sì|Sì|No|  
|**SQLBulkOperations**|Sì|Sì|No|  
|**SQLCancel**|Sì|Sì|No|  
|**SQLCloseCursor**|Sì|Sì|No|  
|**SQLColAttribute**|Sì|Sì|No|  
|**SQLColAttributes**|No [3]|No|Sì|  
|**SQLColumnPrivileges**|Sì|Sì|No|  
|**SQLColumns**|Sì|Sì|No|  
|**SQLConnect**|Sì|Sì|No|  
|**SQLCopyDesc**|Sì|Sì|Sì [4]|  
|**SQLDataSources**|No|Sì|Sì|  
|**SQLDescribeCol**|Sì|Sì|No|  
|**SQLDescribeParam**|Sì|Sì|No|  
|**SQLDisconnect**|Sì|Sì|No|  
|**SQLDriverConnect**|Sì|Sì|No|  
|**SQLDrivers**|No|Sì|Sì|  
|**SQLEndTran**|Sì|Sì|No|  
|**SQLError**|No|No [1]|Sì|  
|**SQLExecDirect**|Sì|Sì|No|  
|**SQLExecute**|Sì|Sì|No|  
|**SQLExtendedFetch**|Sì|No|No|  
|**SQLFetch**|Sì|Sì|No|  
|**SQLFetchScroll**|Sì|Sì|No|  
|**SQLForeignKeys**|Sì|Sì|No|  
|**SQLFreeConnect**|No|Sì [1]|Sì|  
|**SQLFreeEnv**|No|Sì [1]|Sì|  
|**SQLFreeHandle**|Sì|Sì|No|  
|**SQLFreeStmt**|Sì|Sì|No|  
|**SQLGetConnectAttr**|Sì|Sì|No|  
|**SQLGetConnectOption**|No [5]|No [1]|Sì|  
|**SQLGetCursorName**|Sì|Sì|No|  
|**SQLGetData**|Sì|Sì|No|  
|**SQLGetDescField**|Sì|Sì|No|  
|**SQLGetDescRec**|Sì|Sì|No|  
|**SQLGetDiagField**|Sì|Sì|No|  
|**SQLGetDiagRec**|Sì|Sì|No|  
|**SQLGetEnvAttr**|Sì|Sì|No|  
|**SQLGetFunctions**|No [6]|Sì|Sì|  
|**SQLGetInfo**|Sì|Sì|No|  
|**SQLGetStmtAttr**|Sì|Sì|No|  
|**SQLGetStmtOption**|No [5]|No [1]|Sì|  
|**SQLGetTypeInfo**|Sì|Sì|No|  
|**SQLMoreResults**|Sì|Sì|No|  
|**SQLNativeSql**|Sì|Sì|No|  
|**SQLNumParams**|Sì|Sì|No|  
|**SQLNumResultCols**|Sì|Sì|No|  
|**SQLParamData**|Sì|Sì|No|  
|**SQLParamOptions**|No|No|Sì|  
|**SQLPrepare**|Sì|Sì|No|  
|**SQLPrimaryKeys**|Sì|Sì|No|  
|**SQLProcedureColumns**|Sì|Sì|No|  
|**SQLProcedures**|Sì|Sì|No|  
|**SQLPutData**|Sì|Sì|No|  
|**SQLRowCount**|Sì|Sì|No|  
|**SQLSetConnectAttr**|Sì|Sì|No|  
|**SQLSetConnectOption**|No [5]|No [1]|Sì|  
|**SQLSetCursorName**|Sì|Sì|No|  
|**SQLSetDescField**|Sì|Sì|No|  
|**SQLSetDescRec**|Sì|Sì|No|  
|**SQLSetEnvAttr**|Sì|Sì|No|  
|**SQLSetPos**|Sì|Sì|No|  
|**SQLSetParam**|No|No|Sì|  
|**SQLSetScrollOption**|Sì|Sì|No|  
|**SQLSetStmtAttr**|Sì|Sì|No|  
|**SQLSetStmtOption**|No [5]|No [1]|Sì|  
|**SQLSpecialColumns**|Sì|Sì|No|  
|**SQLStatistics**|Sì|Sì|No|  
|**SQLTablePrivileges**|Sì|Sì|No|  
|**SQLTables**|Sì|Sì|No|  
|**SQLTransact**|No|No [1]|Sì|  
  
 [1] Questa funzione è deprecata in ODBC 3. *x*. ODBC 3. le applicazioni *x* non devono usare questa funzione. Tuttavia, un gruppo aperto o un'applicazione compatibile con l'interfaccia della riga di comando ISO può chiamare questa funzione.  
  
 [2] ODBC 3. le applicazioni *x* devono usare **SQLBindParameter** anziché **SQLBindParam**. Tuttavia, un gruppo aperto o un'applicazione compatibile con l'interfaccia della riga di comando ISO può chiamare questa funzione.  
  
 [3] i writer di driver devono tenere presente che ODBC 2. gli attributi di colonna *x* SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE e SQL_COLUMN_LENGTH devono essere supportati con **SQLColAttribute**.  
  
 [4] **SQLCopyDesc** viene implementato parzialmente da Gestione driver quando un descrittore viene copiato tra le connessioni che appartengono a driver diversi. I driver sono necessari per supportare **SQLCopyDesc** tra due connessioni. Le funzioni quali **SQLDrivers**, implementate esclusivamente da Gestione driver, non vengono visualizzate in questo elenco.  
  
 [5] in determinate circostanze, potrebbe essere necessario che i driver supportino questa funzione. Per ulteriori informazioni, vedere la pagina di riferimento di questa funzione.  
  
 [6] il driver può scegliere di supportare **SQLGetFunctions** se il set di funzioni supportate dal driver varia dalla connessione alla connessione.
