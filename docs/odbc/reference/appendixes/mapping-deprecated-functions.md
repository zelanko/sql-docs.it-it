---
title: Mappatura delle funzioni deprecate Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a4e89cd9281520e70ec5fb289c6050e77ec6194c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299881"
---
# <a name="mapping-deprecated-functions"></a>Mapping di funzioni deprecate
In questa sezione viene descritto come le funzioni deprecate vengono mappate da Gestione Driver ODBC *3.x* per garantire la compatibilità con le versioni precedenti dei driver ODBC *3.x* utilizzati con le applicazioni ODBC *2.x.* Gestione Driver esegue questo mapping indipendentemente dalla versione dell'applicazione. Poiché ognuna delle funzioni ODBC *2.x* nell'elenco seguente viene mappata alla funzione ODBC *3.x* corrispondente quando viene chiamata in un driver ODBC *3.x,* il driver ODBC *3.x* non deve implementare le funzioni ODBC *2.x.*  
  
 Il mapping nell'elenco viene attivato quando il driver è un driver ODBC *3.x* e il driver non supporta la funzione di cui viene eseguito il mapping.  
  
 Nella tabella riportata di seguito sono elencate tutte le funzionalità duplicate introdotte in ODBC *3.x*.  
  
|ODBC *2.x (funzione)*|ODBC *3.x (funzione)*|  
|-------------------------|-------------------------|  
|**SQLAllocConnect (connessione a questo errore)**|**SQLAllocHandle**|  
|**SQLAllocEnv (informazioni in lingua inglese)**|**SQLAllocHandle**|  
|**Istruzione SQLAllocStmt (informazioni in lingua inglese)**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**ATTRIBUTI SQLCol**|**SQLColAttribute**|  
|**Sqlerror**|**SQLGetDiagRec**|  
|**SQLFreeConnect (informazioni in lingua inglese)**|**SQLFreeHandle**|  
|**SQLFreeEnv (informazioni in lingua inglese)**|**SQLFreeHandle**|  
|**SQLFreeStmt** con *un'opzione* di SQL_DROP|**SQLFreeHandle**|  
|**SQLGetConnectOption (Opzione SQLGetConnectOption)**|**SQLGetConnectAttr**|  
|**Opzione SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**Opzioni SQLParam**|**SQLSetStmtAttr**|  
|**Sqlsetconnectoption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption (opzione SQLSetScrollOption)**|**SQLSetStmtAttr**|  
|**Opzione SQLSetStmmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact (transazione SQLTransact)**|**SQLEndTran**|  
  
 [1] Anche se questa funzione non esisteva in ODBC *2.x*, si trova negli standard Open Group e ISO.  
  
 [2] Questa è una funzione ODBC 1.0.  
  
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
