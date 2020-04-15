---
title: Istruzioni SQL immesse dall'utente Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf2f8cf36be392cb42a970fa2fb0b19c35daeb39
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301962"
---
# <a name="sql-statements-entered-by-the-user"></a>Istruzioni SQL immesse dall'utente
Le applicazioni che eseguono analisi ad hoc in genere consentono inoltre all'utente di immettere direttamente istruzioni SQL. Ad esempio:  
  
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
  
 Questo approccio semplifica la codifica delle applicazioni; l'applicazione si basa sull'utente per compilare l'istruzione SQL e sull'origine dati per verificare la validità dell'istruzione. Perché è difficile scrivere un'interfaccia utente grafica che espone adeguatamente la complessità di SQL, semplicemente chiedendo all'utente di immettere il testo dell'istruzione SQL può essere un'alternativa preferibile. Tuttavia, ciò richiede all'utente di conoscere non solo SQL, ma anche lo schema dell'origine dati su cui viene eseguita una query. Alcune applicazioni forniscono un'interfaccia utente grafica tramite la quale l'utente può creare un'istruzione SQL di base e fornire anche un'interfaccia di testo con cui l'utente può modificarla.
