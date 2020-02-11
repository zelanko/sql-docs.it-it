---
title: Uso di SQLGetDiagRec e SQLGetDiagField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 4f486bb1-fad8-4064-ac9d-61f2de85b68b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23b7539c32b6cb675f8616d9b8ec9db89be1208b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022147"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>Uso di SQLGetDiagRec e SQLGetDiagField
Le applicazioni chiamano **SQLGetDiagRec** o **SQLGetDiagField** per recuperare le informazioni di diagnostica. Queste funzioni accettano un handle di ambiente, connessione, istruzione o descrittore e restituiscono la diagnostica dalla funzione utilizzata per l'ultima volta. La diagnostica registrata su un particolare handle viene eliminata quando viene chiamata una nuova funzione con tale handle. Se la funzione ha restituito più record di diagnostica, l'applicazione chiama queste funzioni più volte; il numero totale di record di stato viene recuperato chiamando **SQLGetDiagField** per il record di intestazione (record 0) con l'opzione SQL_DIAG_NUMBER.  
  
 Le applicazioni recuperano singoli campi di diagnostica chiamando **SQLGetDiagField** e specificando il campo da recuperare. Determinati campi di diagnostica non hanno alcun significato per determinati tipi di handle. Per un elenco dei campi di diagnostica e dei relativi significati, vedere la descrizione della funzione [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) .  
  
 Le applicazioni recuperano l'errore SQLSTATE, il codice di errore nativo e il messaggio di diagnostica in una singola chiamata chiamando **SQLGetDiagRec**; Non è possibile usare **SQLGetDiagRec** per recuperare le informazioni dal record di intestazione.  
  
 Il codice seguente, ad esempio, richiede all'utente un'istruzione SQL e la esegue. Se sono state restituite informazioni di diagnostica, viene chiamato **SQLGetDiagField** per ottenere il numero di record di stato e **SQLGetDiagRec** per ottenere il codice SQLSTATE, il codice di errore nativo e il messaggio di diagnostica da tali record.  
  
```  
SQLCHAR       SqlState[6], SQLStmt[100], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLINTEGER    NativeError;  
SQLSMALLINT   i, MsgLen;  
SQLRETURN     rc1, rc2;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement.  
GetSQLStmt(SQLStmt);  
  
// Execute the SQL statement and return any errors or warnings.  
rc1 = SQLExecDirect(hstmt, SQLStmt, SQL_NTS);  
if ((rc1 == SQL_SUCCESS_WITH_INFO) || (rc1 == SQL_ERROR)) {
   SQLLEN numRecs = 0;
   SQLGetDiagField(SQL_HANDLE_STMT, hstmt, 0, SQL_DIAG_NUMBER, &numRecs, 0, 0);
   // Get the status records.
   i = 1;  
   while (i <= numRecs && (rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
            Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState,NativeError,Msg,MsgLen);  
      i++;  
   }  
}  
  
if ((rc1 == SQL_SUCCESS) || (rc1 == SQL_SUCCESS_WITH_INFO)) {  
   // Process statement results, if any.  
}  
```
