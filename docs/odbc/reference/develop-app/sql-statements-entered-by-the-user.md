---
title: Istruzioni SQL immesse dall'utente | Microsoft Docs
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
ms.openlocfilehash: 78a1653df60b21cde772cbe32a688b3fdef80a42
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086067"
---
# <a name="sql-statements-entered-by-the-user"></a>Istruzioni SQL immesse dall'utente
Anche le applicazioni che eseguono l'analisi ad hoc consentono all'utente di immettere direttamente istruzioni SQL. Ad esempio:  
  
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
  
 Questo approccio semplifica la codifica delle applicazioni; l'applicazione si basa sull'utente per compilare l'istruzione SQL e nell'origine dati per verificare la validità dell'istruzione. Poiché è difficile scrivere un'interfaccia utente grafica che espone adeguatamente le complessità di SQL, è sufficiente chiedere all'utente di immettere il testo dell'istruzione SQL potrebbe essere un'alternativa preferibile. Tuttavia, è necessario che l'utente conosca non solo SQL, ma anche lo schema dell'origine dati su cui si esegue la query. Alcune applicazioni forniscono un'interfaccia utente grafica in base alla quale l'utente può creare un'istruzione SQL di base e fornire anche un'interfaccia di testo con cui l'utente può modificarla.
