---
title: Utilizzo di SQLGetDiagRec e SQLGetDiagField | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 1db402e7c015ef50ce47b5137e670d9f1836a326
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208404"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>Uso di SQLGetDiagRec e SQLGetDiagField
Le applicazioni chiamano **SQLGetDiagRec** oppure **SQLGetDiagField** per recuperare le informazioni di diagnostica. Queste funzioni accettano un handle di ambiente, connessione, istruzione o descrittore e restituiscono diagnostica dalla funzione che infine utilizzato tale handle. I dati di diagnostica registrati su un handle specifico vengono rimossi quando viene chiamata una funzione di nuovo utilizzando l'handle. Se la funzione ha restituito più record di diagnostica, l'applicazione chiama le funzioni più volte; il numero totale di record di stato viene recuperato chiamando **SQLGetDiagField** per il record di intestazione (record 0) con l'opzione SQL_DIAG_NUMBER.  
  
 Applicazioni di recuperano i singoli campi di diagnostica chiamando **SQLGetDiagField** e specificando il campo da recuperare. Determinati campi di diagnostica non hanno alcun significato per determinati tipi di handle. Per un elenco di campi di diagnostica e i relativi significati, vedere la [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descrizione della funzione.  
  
 Le applicazioni di recuperare il valore SQLSTATE, codice di errore nativo e messaggio di diagnostica in una singola chiamata chiamando **SQLGetDiagRec**; **SQLGetDiagRec** non può essere usato per recuperare informazioni dal record di intestazione.  
  
 Ad esempio, il codice seguente richiede l'immissione di un'istruzione SQL e lo esegue. Se le informazioni di diagnostica è state restituite, chiama il metodo **SQLGetDiagField** per ottenere il numero di record di stato e **SQLGetDiagRec** per ottenere il valore SQLSTATE, codice di errore nativo e messaggio di diagnostica da quelli record.  
  
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
