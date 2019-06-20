---
title: Le istruzioni SQL immesse dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- user-entered SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], entered by user
ms.assetid: 109af162-93ba-425a-8fe5-49c7dc7cc784
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 28256433802d686f4362b2b733fc2d2b13e65302
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149142"
---
# <a name="sql-statements-entered-by-the-user"></a>Istruzioni SQL immesse dall'utente
Le applicazioni che eseguono l'analisi ad hoc anche comunemente consentono all'utente di immettere istruzioni SQL direttamente. Ad esempio:  
  
```  
SQLCHAR *     Statement, SqlState[6], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLSMALLINT   i, MsgLen;  
SQLINTEGER    NativeError;  
SQLRETURN     rc1, rc2;  
  
// Prompt user for SQL statement.  
GetSQLStatement(Statement);  
  
// Execute the statement directly. Because it will be executed only once,  
// do not prepare it.  
rc1 = SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Process any errors or returned information.  
if ((rc1 == SQL_ERROR) || rc1 == SQL_SUCCESS_WITH_INFO) {  
   i = 1;  
   while ((rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
         Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState, NativeError, Msg, MsgLen);  
      i++;  
   }  
}  
```  
  
 Questo approccio semplifica la scrittura del codice dell'applicazione; l'applicazione si basa sull'utente per compilare l'istruzione SQL e nell'origine dei dati per controllare la validità dell'istruzione. Poiché è difficile scrivere un'interfaccia utente grafica che espone in modo adeguato le complicazioni del SQL, è sufficiente che chiede all'utente di immettere il testo dell'istruzione SQL può essere un'alternativa preferibile. Tuttavia, questo richiede all'utente di conoscere non solo SQL, ma anche lo schema dell'origine dati sottoposto a query. Alcune applicazioni forniscono un'interfaccia utente grafica mediante il quale l'utente può creare un'istruzione SQL di base e anche fornire un'interfaccia di testo con cui l'utente può modificarlo.
