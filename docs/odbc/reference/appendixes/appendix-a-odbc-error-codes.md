---
title: 'Appendice A: Codici di errore ODBC | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error codes [ODBC]
- SQLSTATE [ODBC]
- error codes [ODBC], SQLSTATE
ms.assetid: c06902e4-721d-42e2-b818-05f0e18e4ce0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e93e9dd8da111d367657d99dfba19513ff7f7539
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026786"
---
# <a name="appendix-a-odbc-error-codes"></a>Appendice A: Codici di errore ODBC
In questo argomento vengono descritti i valori SQLSTATE per ODBC 3. *x*. Per altre informazioni su ODBC 3. *x* valori SQLSTATE, vedere [mapping di SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md).  
  
 **SQLGetDiagRec** oppure **SQLGetDiagField** restituisce i valori SQLSTATE come definito da Open Group *gestione dati: Structured Query Language (SQL), versione 2* (marzo 1995). I valori SQLSTATE sono stringhe che contengono cinque caratteri. La tabella seguente elenca i valori SQLSTATE per grado di restituire un driver **SQLGetDiagRec**.  
  
 Il valore di stringa di caratteri per un valore SQLSTATE restituito è costituito da un valore di classe di due caratteri seguito da un valore di sottoclasse di tre caratteri. Il valore di classe "01" indica un possibile problema ed è accompagnato da un codice restituito di SQL_SUCCESS_WITH_INFO. I valori della classe diversa da "01", ad eccezione della classe "Messaggistica immediata," indicano un errore e sono accompagnati da un valore restituito SQL_ERROR. La classe "IM" è specifico di avvisi ed errori che derivano da un'implementazione di ODBC stesso. Il valore di sottoclasse "000" in qualsiasi classe indica che non vi sia alcun sottoclasse per tale SQLSTATE. L'assegnazione di valori di classe e dalla sottoclasse è definito da SQL-92.  
  
> [!NOTE]  
>  Sebbene la corretta esecuzione di una funzione è in genere indicata dal valore restituito SQL_SUCCESS, anche il valore SQLSTATE 00000 indica l'esito positivo.  
  
|SQLSTATE|Errore|Può essere restituito da|  
|--------------|-----------|--------------------------|  
|01000|Avviso generale|Tutte le funzioni ODBC, ad eccezione di:<br /><br /> **SQLError**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|01001|Conflitto dell'operazione del cursore|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|01002|Errore di disconnessione|**SQLDisconnect**|  
|01003|Valore NULL eliminato nella funzione sui set|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01004|Dati troncati a destra di tipo stringa|**SQLBrowseConnect**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLDataSources**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLDrivers**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetEnvAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNative**<br /><br /> **Sql SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetCursorName**|  
|01006|Privilegio non revocato.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01007|Privilegio non concesso|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01S00|Attributo della stringa di connessione non è valido|**SQLBrowseConnect**<br /><br /> **SQLDriverConnec**|  
|01S01|Errore nella riga|**SQLBulkOperations**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLSetPos**|  
|01S02|Valore di opzione modificato|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**|  
|01S06|Tentativo di recupero prima che il set di risultati restituito il primo set di righe|**SQLExtendedFetch**<br /><br /> **SQLFetchScroll**|  
|01S07|Troncamento frazionario.|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|01S08|Errore durante il salvataggio di DSN su File|**SQLDriverConnect**|  
|01S09|Parola chiave non valida|**SQLDriverConnect**|  
|07001|Numero errato di parametri|**SQLExecDirect**<br /><br /> **SQLExecute**|  
|07002|Campo COUNT non corretto|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|07005|Istruzione preparata non un *specifica di cursore.*|**SQLColAttribute**<br /><br /> **SQLDescribeCol**|  
|07006|Violazione dell'attributo del tipo di dati|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|07009|Indice del descrittore non valido|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLParamData**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRecSQLSetPos**|  
|07S01|Utilizzo non valido del parametro predefinito|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**|  
|08001|Impossibile stabilire la connessione client|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|08002|Nome della connessione in uso|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLSetConnectAttr**|  
|08003|Connessione non aperta|**SQLAllocHandle**<br /><br /> **SQLDisconnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLNativeSql**<br /><br /> **SQLSetConnectAttr**|  
|08004|Il server ha rifiutato la connessione|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|08007|Errore di connessione durante la transazione|**SQLEndTran**|  
|08S01|Errore del collegamento di comunicazione|**SQLBrowseConnect**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNativeSql**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|21S01|Elenco di valori di inserimento non corrisponde elenco colonne|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|21S02|Livello di tabella derivata corrisponde a elenco di colonne|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetPos**|  
|22001|Dati troncati a destra di tipo stringa|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetPos**|  
|22002|Variabile indicatore necessaria ma non fornito|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**|  
|22003|Valore numerico non compreso nell'intervallo|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLGetInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22007|Formato di datetime non valido|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22008|Overflow del campo DateTime|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **QLParamData**<br /><br /> **SQLPutData**|  
|22012|Divisione per zero|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLPutData**|  
|22015|Overflow del campo Interval|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22018|Valore del carattere non valido per la specifica del cast|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22019|Carattere di escape non valido|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|22025|Sequenza di escape non valido|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|22026|Lunghezza dei dati non corrispondente.|**SQLParamData**|  
|23000|Violazione di vincolo di integrità|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|24000|Stato del cursore non valido|**SQLBulkOperations**<br /><br /> **SQLCloseCursor**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetData**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLNativeSql**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|25000|Stato della transazione non valido|**SQLDisconnect**|  
|25S01|Stato della transazione|**SQLEndTran**|  
|25S02|Transazione è ancora attiva|**SQLEndTran**|  
|25S03|Viene eseguito il rollback delle transazioni|**SQLEndTran**|  
|28000|Specifica di autorizzazione non valido|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|34000|Nome di cursore non valido|**SQLExecDirect**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetCursorName**|  
|3C000|Nome di cursore duplicato|**SQLSetCursorName**|  
|3D000|Nome catalogo non valido|**SQLExecDirect**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetConnectAttr**|  
|3F000|Nome dello schema non valido|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|40001|Errore di serializzazione.|**SQLBulkOperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLParamData**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|40002|Violazione di vincolo di integrità|**SQLEndTran**|  
|40003|Completamento dell'istruzione sconosciuto|**SQLBulkOperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|42000|La sintassi o violazione di accesso|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetPos**|  
|42S01|Tabella di base o vista già esistente|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S02|Tabella di base o della vista non trovato|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S11|L'indice esiste già|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S12|Indice non trovato|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S21|Esiste già una colonna|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S22|Colonna non trovata|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|44000|Violazione della clausola WITH CHECK OPTION|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|HY000|Errore generale|Tutte le funzioni ODBC, ad eccezione di:<br /><br /> **SQLError**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY001|Errore di allocazione della memoria|Tutte le funzioni ODBC, ad eccezione di:<br /><br /> **SQLError**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY003|Tipo di buffer dell'applicazione non valido|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLGetData**|  
|HY004|Tipo di dati SQL non valido|**SQLBindParameter**<br /><br /> **SQLGetTypeInfo**|  
|HY007|L'istruzione associata non è pronto|**SQLCopyDesc**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**|  
|HY008|Operazione annullata|Tutte le funzioni ODBC che possono essere elaborate in modo asincrono:<br /><br /> **SQLBrowseConnect**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLDisconnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetData**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY009|Utilizzo non valido del puntatore null|**SQLAllocHandle**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLNativeSql**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY010|Errore nella sequenza della funzione|**SQLAllocHandle**<br /><br /> **SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLCloseCursor**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLDisconnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLRowCount**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY011|Impossibile impostare l'attributo adesso|**SQLBulkOperations**<br /><br /> **SQLParamData**<br /><br /> **QLSetPos**<br /><br /> **SQLSetStmtAttr**|  
|HY012|Codice operativo della transazione non valido|**SQLEndTran**|  
|HY013|Errore di gestione della memoria|Tutte le funzioni ODBC, ad eccezione di:<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY014|Limita il numero di handle superato|**SQLAllocHandle**|  
|HY015|Nessun nome di cursore disponibile.|**SQLGetCursorName**|  
|HY016|Non è possibile modificare un descrittore delle righe di implementazione|**SQLCopyDesc**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**|  
|HY017|Utilizzo non valido di un handle di descrittore allocato automaticamente|**SQLFreeHandle**<br /><br /> **SQLSetStmtAttr**|  
|HY018|Richiesta di annullamento. il server ha rifiutato|**SQLCancel**|  
|HY019|Dati non letterali e non binari inviati in parti|**SQLPutData**|  
|HY020|Tenta di concatenare un valore null|**SQLPutData**|  
|HY021|Informazioni descrittore incoerenti.|**SQLBindParameter**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLGetDescField**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**|  
|HY024|Valore dell'attributo non valido|**SQLSetConnectAttr**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**|  
|HY090|Lunghezza della stringa o buffer non valido|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBrowseConnect**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDataSources**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLDrivers**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNativeSql**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY091|Identificatore del campo del descrittore non valido|**SQLColAttribute**<br /><br /> **SQLGetDescField**<br /><br /> **SQLSetDescField**|  
|HY092|Identificatore di attributo/opzione non è valido|**SQLAllocHandle**<br /><br /> **QLBulkOperations**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetEnvAttr**<br /><br /> **QLParamData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**|  
|HY095|Tipo di funzione non compreso nell'intervallo|**SQLGetFunctions**|  
|HY096|Tipo di informazioni non valide|**SQLGetInfo**|  
|HY097|Tipo di colonna non compreso nell'intervallo|**SQLSpecialColumns**|  
|HY098|Tipo di ambito non compreso nell'intervallo|**SQLSpecialColumns**|  
|HY099|Tipo che ammette valori null non compreso nell'intervallo|**SQLSpecialColumns**|  
|HY100|Tipo di opzione di univocità non compreso nell'intervallo|**SQLStatistics**|  
|HY101|Tipo di opzione di accuratezza non compreso nell'intervallo|**SQLStatistics**|  
|HY103|Codice di recupero non valido|**SQLDataSources**<br /><br /> **SQLDrivers**|  
|HY104|Valore di precisione o scala non valido|**SQLBindParameter**|  
|HY105|Tipo di parametro non valido|**SQLBindParameter**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetDescField**|  
|HY106|Tipo compreso nell'intervallo di recupero|**SQLExtendedFetch**<br /><br /> **SQLFetchScroll**|  
|HY107|Valore di riga non compreso nell'intervallo|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLSetPos**|  
|HY109|Posizione del cursore non valido|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLGetData**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNativeSql**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|HY110|Completamento del driver non è valido|**SQLDriverConnect**|  
|HY111|Valore di segnalibro non valido|**SQLExtendedFetch**<br /><br /> **SQLFetchScroll**|  
|HYC00|Funzionalità opzionale non implementata|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetData**<br /><br /> **SQLGetEnvAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HYT00|Timeout|**SQLBrowseConnect**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HYT01|Timeout di connessione scaduto|Tutte le funzioni ODBC, ad eccezione di:<br /><br /> **SQLDrivers**<br /><br /> **SQLDataSources**<br /><br /> **SQLGetEnvAttr**<br /><br /> **SQLSetEnvAttr**|  
|IM001|Driver non supporta questa funzione|Tutte le funzioni ODBC, ad eccezione di:<br /><br /> **SQLAllocHandle**<br /><br /> **SQLDataSources**<br /><br /> **SQLDrivers**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLGetFunctions**|  
|IM002|Nome dell'origine dati non trovato e driver predefinito non specificato|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM003|Non è stato possibile caricare il driver specificato|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM004|Patente **SQLAllocHandle** su SQL_HANDLE_ENV non è riuscita|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM005|Patente **SQLAllocHandle** su SQL_HANDLE_DBC non è riuscita|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM006|Patente **SQLSetConnectAttr** non è riuscita|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM007|Nessuna origine dati o il driver specificato; finestra di dialogo non consentito|**SQLDriverConnect**|  
|IM008|Finestra di dialogo non è riuscita|**SQLDriverConnect**|  
|IM009|Impossibile caricare la DLL di conversione|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLSetConnectAttr**|  
|IM010|Nome dell'origine dati troppo lungo|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM011|Nome del driver troppo lungo|**SQLBrowseConnect**<br /><br /> **SQLDriverConnect**|  
|IM012|Errore di sintassi della parola chiave DRIVER|**SQLBrowseConnect**<br /><br /> **SQLDriverConnect**|  
|IM013|Errore del file di traccia|Tutte le funzioni ODBC.|  
|IM014|Nome non valido del DSN su File|**SQLDriverConnect**|  
|IM015|Origine dati file danneggiato|**SQLDriverConnect**|
