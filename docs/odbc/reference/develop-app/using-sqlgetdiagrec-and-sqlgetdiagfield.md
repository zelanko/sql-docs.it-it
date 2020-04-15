---
title: Utilizzo di SQLGetDiagRec e SQLGetDiagField . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69a17086253b40469b0ed98cb6f870f319f03f52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306752"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>Uso di SQLGetDiagRec e SQLGetDiagField
Le applicazioni chiamano **SQLGetDiagRec** o **SQLGetDiagField** per recuperare le informazioni di diagnostica. Queste funzioni accettano un handle di ambiente, connessione, istruzione o descrittore e restituiscono la diagnostica dalla funzione che ha utilizzato l'ultimo handle. La diagnostica registrata su un handle specifico viene eliminata quando viene chiamata una nuova funzione usando tale handle. Se la funzione ha restituito più record di diagnostica, l'applicazione chiama queste funzioni più volte; il numero totale di record di stato viene recuperato chiamando **SQLGetDiagField** per il record di intestazione (record 0) con l'opzione SQL_DIAG_NUMBER.  
  
 Le applicazioni recuperano singoli campi di diagnostica chiamando **SQLGetDiagField** e specificando il campo da recuperare. Alcuni campi diagnostici non hanno alcun significato per alcuni tipi di handle. Per un elenco dei campi di diagnostica e dei relativi significati, vedere la descrizione della funzione [SQLGetDiagField.For](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) a list of diagnostic fields and their meanings, see the SQLGetDiagField function description.  
  
 Le applicazioni recuperano sqlSTATE, il codice di errore nativo e il messaggio di diagnostica in una singola chiamata chiamando **SQLGetDiagRec**; **Impossibile utilizzare SQLGetDiagRec** per recuperare informazioni dal record di intestazione.  
  
 Ad esempio, il codice seguente richiede all'utente un'istruzione SQL e la esegue. Se sono state restituite informazioni di diagnostica, chiama **SQLGetDiagField** per ottenere il numero di record di stato e **SQLGetDiagRec** per ottenere SQLSTATE, codice di errore nativo e messaggio di diagnostica da tali record.  
  
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
