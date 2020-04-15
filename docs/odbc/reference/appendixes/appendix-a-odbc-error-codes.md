---
title: 'Appendice A: Codici di errore ODBC Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af288cf9f0564f6fe0dbef14f66143667120c656
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307522"
---
# <a name="appendix-a-odbc-error-codes"></a>Appendice A: codici di errore ODBC
In questo argomento vengono illustrati i valori SQLSTATE per ODBC 3. *x*. Per ulteriori informazioni su ODBC 3. *x* Valori SQLSTATE , vedere [Mapping SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md).  
  
 **SQLGetDiagRec** o **SQLGetDiagField** restituisce i valori SQLSTATE definiti da Open Group *Data Management: STRUCTURED Query Language (SQL), Versione 2* (marzo 1995). I valori SQLSTATE sono stringhe che contengono cinque caratteri. Nella tabella seguente sono elencati i valori SQLSTATE che un driver può restituire per **SQLGetDiagRec**.  
  
 Il valore della stringa di caratteri restituito per un SQLSTATE è costituito da un valore di classe di due caratteri seguito da un valore di sottoclasse di tre caratteri. Il valore della classe "01" indica un avviso ed è accompagnato da un codice restituito di SQL_SUCCESS_WITH_INFO. I valori di classe diversi da "01", ad eccezione della classe "IM", indicano un errore e sono accompagnati da un valore restituito di SQL_ERROR. La classe "IM" è specifica per gli avvisi e gli errori che derivano dall'implementazione di ODBC stesso. Il valore della sottoclasse "000" in qualsiasi classe indica che non esiste alcuna sottoclasse per tale SQLSTATE. L'assegnazione dei valori di classe e sottoclasse è definita da SQL-92.  
  
> [!NOTE]  
>  Anche se l'esecuzione corretta di una funzione è in genere indicata da un valore restituito di SQL_SUCCESS, SQLSTATE 00000 indica anche l'esito positivo.  
  
|SQLSTATE|Errore|Può essere restituito da|  
|--------------|-----------|--------------------------|  
|01000|Avvertenza generale|Tutte le funzioni ODBC ad eccezione di:<br /><br /> **Sqlerror**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|01001|Conflitto di funzionamento del cursoreCursor operation conflict|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|01002|Errore di disconnessione|**Sqldisconnect**|  
|01003|Valore NULL eliminato nella funzione set|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01004|Dati stringa troncati a destra|**SQLBrowseConnect**<br /><br /> **Sqlbulkoperations**<br /><br /> **SQLColAttribute**<br /><br /> **SqlDataSourcesSQLDataSources**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLDrivers**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetEnvAttr (Informazioni in lingua inglese)**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNative**<br /><br /> **SQLSQL SQLParamData (informazioni in lingua inglese) SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetCursorName (Nome cursore)**|  
|01006|Privilegio non revocato|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01007|Privilegio non concesso|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01S00 (inquesto da windows)|Attributo della stringa di connessione non valido|**SQLBrowseConnect**<br /><br /> **SQLDriverConnec**|  
|01S01 (in questo stato di|Errore nella riga|**Sqlbulkoperations**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLSetPos**|  
|01S02 (in questo stato di|Valore dell'opzione modificato|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**|  
|01S06 (in inglese)|Tentativo di recupero prima che il set di risultati restituisca il primo set di righe|**Sqlextendedfetch**<br /><br /> **SQLFetchScroll**|  
|01S07 (intito)|Troncamento frazionario|**Sqlbulkoperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|01S08 (in questo)|Errore durante il salvataggio del DSN del file|**SQLDriverConnect**|  
|01S09 (in titolo della ste92):|Parola chiave non valida|**SQLDriverConnect**|  
|07001|Numero errato di parametri|**SQLExecDirect**<br /><br /> **SQLExecute**|  
|07002|Campo COUNT non corretto|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|07005|Istruzione Prepared non una specifica del *cursore*|**SQLColAttribute**<br /><br /> **SQLDescribeCol**|  
|07006|Violazione dell'attributo del tipo di dati con restrizioniRestricted data type attribute violation|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **Sqlbulkoperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|07009|Indice descrittore non valido|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **Sqlbulkoperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLParamData**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRecSQLSetPos**|  
|07S01 (in titola del sistema)|Utilizzo non valido del parametro predefinito|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**|  
|08001|Il client non è in grado di stabilire la connessione|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|08002|Nome connessione in uso|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLSetConnectAttr**|  
|08003|Connessione non aperta|**SQLAllocHandle**<br /><br /> **Sqldisconnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLNativeSql**<br /><br /> **SQLSetConnectAttr**|  
|08004|Il server ha rifiutato la connessione|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|08007|Errore di connessione durante la transazioneConnection failure during transaction|**SQLEndTran**|  
|08S01|Errore di collegamento di comunicazione|**SQLBrowseConnect**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLCopyDesc (informazioni in lingua inglese)**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNativeSql**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|21S01|L'elenco di valori di inserimento non corrisponde all'elenco di colonne|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|21S02|Il grado della tabella derivata non corrisponde all'elenco di colonne|**Sqlbulkoperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetPos**|  
|22001|Dati stringa troncati a destra|**Sqlbulkoperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetPos**|  
|22002|Variabile indicatore richiesta ma non fornita|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**|  
|22003|Valore numerico non compreso nell'intervallo|**Sqlbulkoperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLGetInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22007|Formato datetime non valido|**Sqlbulkoperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22008|Overflow del campo Datetime|**Sqlbulkoperations**<br /><br /> **SQLExecDirect**<br /><br /> **QLParamData**<br /><br /> **SQLPutData**|  
|22012|Divisione per zero|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLPutData**|  
|22015|Overflow campo intervallo|**Sqlbulkoperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22018|Valore di carattere non valido per la specifica del cast|**Sqlbulkoperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22019|Carattere di escape non valido|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|22025|Sequenza di escape non valida|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|22026|Lunghezza dei dati non corrispondente.|**SQLParamData**|  
|23000|Violazione dei vincoli di integrità|**Sqlbulkoperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|24000|Stato del cursore non valido|**Sqlbulkoperations**<br /><br /> **SQLCloseCursor**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetData**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLNativeSql**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName (Nome cursore)**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|25000|Stato della transazione non valido|**Sqldisconnect**|  
|25S01|Stato della transazione|**SQLEndTran**|  
|25S02 (in questo 25S02)|La transazione è ancora attiva|**SQLEndTran**|  
|25S03|Viene eseguito il rollback della transazioneTransaction is rolled back|**SQLEndTran**|  
|28000|Specifica di autorizzazione non valida|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|34000|Nome di cursore non valido|**SQLExecDirect**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetCursorName (Nome cursore)**|  
|3C000|Nome cursore duplicato|**SQLSetCursorName (Nome cursore)**|  
|3D000|Nome di catalogo non valido|**SQLExecDirect**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetConnectAttr**|  
|3F000|Nome dello schema non valido|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|40001|Errore di serializzazione|**Sqlbulkoperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLParamData**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|40002|Violazione dei vincoli di integrità|**SQLEndTran**|  
|40003|Completamento dell'istruzione sconosciuto|**Sqlbulkoperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|42000|Errore di sintassi o violazione di accesso|**Sqlbulkoperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetPos**|  
|42S01|Tabella o vista di base già esistente|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S02 (in questo)|Tabella o vista di base non trovata|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S11|Indice già esistente|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S12|Indice non trovato|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S21|Colonna già esistente|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S22|Colonna non trovata|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|44000|Violazione della clausola WITH CHECK OPTION|**Sqlbulkoperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|HY000|Errore generale:|Tutte le funzioni ODBC ad eccezione di:<br /><br /> **Sqlerror**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|I001|Errore di allocazione della memoria|Tutte le funzioni ODBC ad eccezione di:<br /><br /> **Sqlerror**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY003|Tipo di buffer dell'applicazione non valido|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLGetData**|  
|HY004|Tipo di dati SQL non valido|**SQLBindParameter**<br /><br /> **SQLGetTypeInfo**|  
|I007|L'istruzione associata non è preparata|**SQLCopyDesc (informazioni in lingua inglese)**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**|  
|I008|Operation canceled|Tutte le funzioni ODBC che possono essere elaborate in modo asincrono:All ODBC functions that can be processed asynchronously:<br /><br /> **SQLBrowseConnect**<br /><br /> **Sqlbulkoperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **Sqldisconnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetData**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|I009|Utilizzo non valido del puntatore null|**SQLAllocHandle**<br /><br /> **SQLBindParameter**<br /><br /> **Sqlbulkoperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLNativeSql**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName (Nome cursore)**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|**SQLAllocHandle**<br /><br /> **SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **Sqlbulkoperations**<br /><br /> **SQLCloseCursor**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLCopyDesc (informazioni in lingua inglese)**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **Sqldisconnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLRowCount**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName (Nome cursore)**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY011|Impossibile impostare l'attributo ora|**Sqlbulkoperations**<br /><br /> **SQLParamData**<br /><br /> **QLSetPos**<br /><br /> **SQLSetStmtAttr**|  
|HY012|Codice operazione transazione non valido|**SQLEndTran**|  
|HY013|Errore di gestione della memoria|Tutte le funzioni ODBC ad eccezione di:<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY014 (informazioni in base al|Limite al numero di maniglie superate|**SQLAllocHandle**|  
|HY015 (informazioni in stato INCUI)|Nessun nome cursore disponibile|**SQLGetCursorName**|  
|HY016 (informazioni in inglese)|Impossibile modificare un descrittore di riga di implementazione|**SQLCopyDesc (informazioni in lingua inglese)**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**|  
|HY017|Utilizzo non valido di un handle di descrittore allocato automaticamente|**SQLFreeHandle**<br /><br /> **SQLSetStmtAttr**|  
|HY018 (INFORMAZIONI in cui è INSTATO)|Richiesta di annullamento rifiutata dal server|**SQLCancel**|  
|HY019|Dati non di carattere e non binari inviati in parti|**SQLPutData**|  
|HY020|Tentativo di concatenare un valore Null|**SQLPutData**|  
|I021|Informazioni sul descrittore incoerenti|**SQLBindParameter**<br /><br /> **SQLCopyDesc (informazioni in lingua inglese)**<br /><br /> **SQLGetDescField**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**|  
|HY024 (informazioni in base al|Valore dell'attributo non valido|**SQLSetConnectAttr**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**|  
|I090|Stringa o lunghezza del buffer non valida|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBrowseConnect**<br /><br /> **Sqlbulkoperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SqlDataSourcesSQLDataSources**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLDrivers**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNativeSql**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName (Nome cursore)**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|I091|Identificatore campo descrittore non valido|**SQLColAttribute**<br /><br /> **SQLGetDescField**<br /><br /> **SQLSetDescField**|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo/opzione non valido|**SQLAllocHandle**<br /><br /> **QLBulkOperations**<br /><br /> **SQLCopyDesc (informazioni in lingua inglese)**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetEnvAttr (Informazioni in lingua inglese)**<br /><br /> **QLParamData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**|  
|I095|Tipo di funzione non compreso nell'intervallo|**SQLGetFunctions**|  
|I096|Tipo di informazioni non valido|**SQLGetInfo**|  
|I097 (informazioni in stato INCUI)|Tipo di colonna non compreso nell'intervallo|**SQLSpecialColumns**|  
|I098 (informazioni in stato IN CUI|Tipo di ambito non compreso nell'intervallo|**SQLSpecialColumns**|  
|I099|Tipo nullable non compreso nell'intervalloNullable type outof-ofrange|**SQLSpecialColumns**|  
|I100|Tipo di opzione di unicità non compresa nell'intervallo|**SQLStatistics**|  
|HY101|Tipo di opzione Di accuratezza fuori intervallo|**SQLStatistics**|  
|I103|Codice di recupero non valido|**SqlDataSourcesSQLDataSources**<br /><br /> **SQLDrivers**|  
|I104|Precisione o valore di scala non valido|**SQLBindParameter**|  
|HY105|Tipo di parametro non valido|**SQLBindParameter**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetDescField**|  
|I106|Tipo di recupero non compreso nell'intervallo|**Sqlextendedfetch**<br /><br /> **SQLFetchScroll**|  
|I107|Valore di riga non compreso nell'intervallo|**Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLSetPos**|  
|I109|Posizione del cursore non valida|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLGetData**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNativeSql**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|HY110|Completamento del driver non valido|**SQLDriverConnect**|  
|HY111|Valore segnalibro non valido|**Sqlextendedfetch**<br /><br /> **SQLFetchScroll**|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **Sqlbulkoperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetData**<br /><br /> **SQLGetEnvAttr (Informazioni in lingua inglese)**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HYT00|Timeout|**SQLBrowseConnect**<br /><br /> **Sqlbulkoperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **Sqlextendedfetch**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HYT01|Timeout connessione scaduto|Tutte le funzioni ODBC ad eccezione di:<br /><br /> **SQLDrivers**<br /><br /> **SqlDataSourcesSQLDataSources**<br /><br /> **SQLGetEnvAttr (Informazioni in lingua inglese)**<br /><br /> **SQLSetEnvAttr**|  
|IM001|Il driver non supporta questa funzione|Tutte le funzioni ODBC ad eccezione di:<br /><br /> **SQLAllocHandle**<br /><br /> **SqlDataSourcesSQLDataSources**<br /><br /> **SQLDrivers**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLGetFunctions**|  
|IM002 (in vi eim.|Nome dell'origine dati non trovato e nessun driver predefinito specificato|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM003|Impossibile caricare il driver specificato|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM004|**SQLAllocHandle** del driver su SQL_HANDLE_ENV non riuscito|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM005|**SQLAllocHandle** del driver in SQL_HANDLE_DBC non riuscita|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM006|**SQLSetConnectAttr** del driver non riuscito|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM007 (invii di iMS77|Nessuna origine dati o driver specificato; finestra di dialogo non consentita|**SQLDriverConnect**|  
|IM008|Finestra di dialogo non riuscita|**SQLDriverConnect**|  
|IM009 (invii di iMSM)|Impossibile caricare la DLL di conversione|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLSetConnectAttr**|  
|IM010 (invii di iMSM)|Nome dell'origine dati troppo lungoData source name too long|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM011|Nome del driver troppo lungo|**SQLBrowseConnect**<br /><br /> **SQLDriverConnect**|  
|IM012 (invii di iMS12)|Errore di sintassi della parola chiave DRIVER|**SQLBrowseConnect**<br /><br /> **SQLDriverConnect**|  
|IM013 (invii di imma)|Errore del file di traccia|Tutte le funzioni ODBC.|  
|IM014 (invii di iMs)|Nome del DSN su file non valido|**SQLDriverConnect**|  
|IM015 (in vi eim.|Origine dati file danneggiato|**SQLDriverConnect**|
