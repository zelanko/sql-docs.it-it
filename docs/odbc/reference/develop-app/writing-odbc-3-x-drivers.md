---
title: Scrittura di driver ODBC 3.x Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62f2a701fd5ac94c92d41494a4fd1ab023edaf25
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300361"
---
# <a name="writing-odbc-3x-drivers"></a>Scrittura di driver ODBC 3.x
Nella tabella seguente viene illustrato il supporto delle funzioni in un ODBC 3. *x* e un'applicazione ODBC e il mapping eseguito da Gestione Driver quando le funzioni vengono chiamate su un ODBC 3. *driver x.*  
  
|Funzione|Supportato<br /><br /> da un<br /><br /> ODBC 3. *x (in* questo modo<br /><br /> autista?|Supportato<br /><br /> da un<br /><br /> ODBC 3. *x (in* questo modo<br /><br /> Applicazione?|Mappato/supportato<br /><br /> dall'ODBC 3. *x (in* questo modo<br /><br /> Gestione driver per<br /><br /> un ODBC 3. *x* driver?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect (connessione a questo errore)**|No|No[1]|Sì|  
|**SQLAllocEnv (informazioni in lingua inglese)**|No|No[1]|Sì|  
|**SQLAllocHandle**|Sì|Sì|No|  
|**Istruzione SQLAllocStmt (informazioni in lingua inglese)**|No|No[1]|Sì|  
|**SQLBindCol**|Sì|Sì|No|  
|**SQLBindParam (informazioni in lingua inglese)**|No|Sì[2]|Sì|  
|**SQLBindParameter**|Sì|Sì|No|  
|**SQLBrowseConnect**|Sì|Sì|No|  
|**Sqlbulkoperations**|Sì|Sì|No|  
|**SQLCancel**|Sì|Sì|No|  
|**SQLCloseCursor**|Sì|Sì|No|  
|**SQLColAttribute**|Sì|Sì|No|  
|**ATTRIBUTI SQLCol**|No[3]|No|Sì|  
|**SQLColumnPrivileges**|Sì|Sì|No|  
|**SQLColumns**|Sì|Sì|No|  
|**SQLConnect**|Sì|Sì|No|  
|**SQLCopyDesc (informazioni in lingua inglese)**|Sì|Sì|Sì[4]|  
|**SqlDataSourcesSQLDataSources**|No|Sì|Sì|  
|**SQLDescribeCol**|Sì|Sì|No|  
|**SQLDescribeParam**|Sì|Sì|No|  
|**Sqldisconnect**|Sì|Sì|No|  
|**SQLDriverConnect**|Sì|Sì|No|  
|**SQLDrivers**|No|Sì|Sì|  
|**SQLEndTran**|Sì|Sì|No|  
|**Sqlerror**|No|No[1]|Sì|  
|**SQLExecDirect**|Sì|Sì|No|  
|**SQLExecute**|Sì|Sì|No|  
|**Sqlextendedfetch**|Sì|No|No|  
|**SQLFetch**|Sì|Sì|No|  
|**SQLFetchScroll**|Sì|Sì|No|  
|**SQLForeignKeys**|Sì|Sì|No|  
|**SQLFreeConnect (informazioni in lingua inglese)**|No|Sì[1]|Sì|  
|**SQLFreeEnv (informazioni in lingua inglese)**|No|Sì[1]|Sì|  
|**SQLFreeHandle**|Sì|Sì|No|  
|**SQLFreeStmt**|Sì|Sì|No|  
|**SQLGetConnectAttr**|Sì|Sì|No|  
|**SQLGetConnectOption (Opzione SQLGetConnectOption)**|No[5]|No[1]|Sì|  
|**SQLGetCursorName**|Sì|Sì|No|  
|**SQLGetData**|Sì|Sì|No|  
|**SQLGetDescField**|Sì|Sì|No|  
|**SQLGetDescRec**|Sì|Sì|No|  
|**SQLGetDiagField**|Sì|Sì|No|  
|**SQLGetDiagRec**|Sì|Sì|No|  
|**SQLGetEnvAttr (Informazioni in lingua inglese)**|Sì|Sì|No|  
|**SQLGetFunctions**|No[6]|Sì|Sì|  
|**SQLGetInfo**|Sì|Sì|No|  
|**SQLGetStmtAttr**|Sì|Sì|No|  
|**Opzione SQLGetStmtOption**|No[5]|No[1]|Sì|  
|**SQLGetTypeInfo**|Sì|Sì|No|  
|**SQLMoreResults**|Sì|Sì|No|  
|**SQLNativeSql**|Sì|Sì|No|  
|**SQLNumParams**|Sì|Sì|No|  
|**SQLNumResultCols**|Sì|Sì|No|  
|**SQLParamData**|Sì|Sì|No|  
|**Opzioni SQLParam**|No|No|Sì|  
|**SQLPrepare**|Sì|Sì|No|  
|**SQLPrimaryKeys**|Sì|Sì|No|  
|**SQLProcedureColumns**|Sì|Sì|No|  
|**SQLProcedures**|Sì|Sì|No|  
|**SQLPutData**|Sì|Sì|No|  
|**SQLRowCount**|Sì|Sì|No|  
|**SQLSetConnectAttr**|Sì|Sì|No|  
|**Sqlsetconnectoption**|No[5]|No[1]|Sì|  
|**SQLSetCursorName (Nome cursore)**|Sì|Sì|No|  
|**SQLSetDescField**|Sì|Sì|No|  
|**SQLSetDescRec**|Sì|Sì|No|  
|**SQLSetEnvAttr**|Sì|Sì|No|  
|**SQLSetPos**|Sì|Sì|No|  
|**SQLSetParam (informazioni in lingua inglese)**|No|No|Sì|  
|**SQLSetScrollOption (opzione SQLSetScrollOption)**|Sì|Sì|No|  
|**SQLSetStmtAttr**|Sì|Sì|No|  
|**Opzione SQLSetStmmtOption**|No[5]|No[1]|Sì|  
|**SQLSpecialColumns**|Sì|Sì|No|  
|**SQLStatistics**|Sì|Sì|No|  
|**SQLTablePrivileges**|Sì|Sì|No|  
|**SQLTables**|Sì|Sì|No|  
|**SQLTransact (transazione SQLTransact)**|No|No[1]|Sì|  
  
 [1] Questa funzione è deprecata in ODBC 3. *x*. ODBC 3. *x* applicazioni non devono utilizzare questa funzione. Tuttavia, un'applicazione Open Group o ISO CLI compatibile può chiamare questa funzione.  
  
 [2] ODBC 3. *X* applicazioni devono utilizzare **SQLBindParameter** anziché **SQLBindParam**. Tuttavia, un'applicazione Open Group o ISO CLI compatibile può chiamare questa funzione.  
  
 [3] I writer di driver devono notare che ODBC 2. *Gli* attributi di colonna x devono essere supportati SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE e SQL_COLUMN_LENGTH con **SQLColAttribute**.  
  
 **[4] SQLCopyDesc** viene parzialmente implementato da Gestione Driver quando viene copiato un descrittore tra connessioni appartenenti a driver diversi. I driver sono necessari per supportare **SQLCopyDesc** in due delle proprie connessioni. Funzioni come **SQLDrivers**, implementate esclusivamente da Gestione Driver, non vengono visualizzate in questo elenco.  
  
 [5] In determinate circostanze, i driver potrebbero avere bisogno di supportare questa funzione. Per altre informazioni, vedere la pagina di riferimento di questa funzione.  
  
 [6] Il driver può scegliere di supportare **SQLGetFunctions** se il set di funzioni che il driver supporta varia da connessione a connessione.
