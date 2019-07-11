---
title: Mapping di funzioni deprecate | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], about mapping deprecated functions
- backward compatibility [ODBC], mapping deprecated functions
- deprecated functions [ODBC]
- compatibility [ODBC], mapping deprecated functions
- functions [ODBC], mapping deprecated functions
- mapping deprecated functions [ODBC]
ms.assetid: ee462617-1d79-4c88-afeb-b129cff34cc6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0568306ad0e2fd8a73737bf80a4270e8eaa3ed18
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793178"
---
# <a name="mapping-deprecated-functions"></a>Mapping di funzioni deprecate
Questa sezione vengono descritte le funzioni come deprecate vengono mappati da ODBC *3.x* gestione Driver per garantire la compatibilità con le versioni precedenti di ODBC *3.x* driver che vengono usati con ODBC *2.x* le applicazioni. Gestione Driver esegue il mapping indipendentemente dalla versione dell'applicazione. Poiché ogni ODBC *2.x* funzioni nell'elenco seguente viene mappato a ODBC corrispondente *3.x* funzione quando viene chiamato in un database ODBC *3.x* driver ODBC *3.x* driver non deve implementare ODBC *2.x* funzioni.  
  
 Il mapping nell'elenco viene attivato quando il driver è un database ODBC *3.x* e il driver non supporta la funzione che viene eseguito il mapping.  
  
 Nella tabella seguente sono elencate le funzionalità di tutti i duplicati che è stato introdotto in ODBC *3.x*.  
  
|ODBC *2.x* (funzione)|ODBC *3.x* (funzione)|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLFreeStmt** con un *opzione* di SQL_DROP|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] anche se questa funzione non esisteva in ODBC *2.x*, si trova negli standard Open Group e ISO.  
  
 [2] si tratta di una funzione ODBC 1.0.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Mapping di SQLAllocConnect](../../../odbc/reference/appendixes/sqlallocconnect-mapping.md)  
  
-   [Mapping di SQLAllocEnv](../../../odbc/reference/appendixes/sqlallocenv-mapping.md)  
  
-   [Mapping di SQLAllocStmt](../../../odbc/reference/appendixes/sqlallocstmt-mapping.md)  
  
-   [Mapping di SQLBindParam](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)  
  
-   [Mapping di SQLColAttributes](../../../odbc/reference/appendixes/sqlcolattributes-mapping.md)  
  
-   [Mapping di SQLError](../../../odbc/reference/appendixes/sqlerror-mapping.md)  
  
-   [Mapping di SQLFreeConnect](../../../odbc/reference/appendixes/sqlfreeconnect-mapping.md)  
  
-   [Mapping di SQLFreeEnv](../../../odbc/reference/appendixes/sqlfreeenv-mapping.md)  
  
-   [Mapping di SQLFreeStmt](../../../odbc/reference/appendixes/sqlfreestmt-mapping.md)  
  
-   [Mapping di SQLGetConnectOption](../../../odbc/reference/appendixes/sqlgetconnectoption-mapping.md)  
  
-   [Mapping di SQLGetStmtOption](../../../odbc/reference/appendixes/sqlgetstmtoption-mapping.md)  
  
-   [Mapping di SQLInstallTranslator](../../../odbc/reference/appendixes/sqlinstalltranslator-mapping.md)  
  
-   [Mapping di SQLParamOptions](../../../odbc/reference/appendixes/sqlparamoptions-mapping.md)  
  
-   [Mapping di SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)  
  
-   [Mapping di SQLSetParam](../../../odbc/reference/appendixes/sqlsetparam-mapping.md)  
  
-   [Mapping di SQLSetScrollOptions](../../../odbc/reference/appendixes/sqlsetscrolloptions-mapping.md)  
  
-   [Mapping di SQLSetStmtOption](../../../odbc/reference/appendixes/sqlsetstmtoption-mapping.md)  
  
-   [Mapping di SQLTransact](../../../odbc/reference/appendixes/sqltransact-mapping.md)
