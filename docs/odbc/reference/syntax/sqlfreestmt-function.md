---
title: SqlFreeStmt (funzione) Documenti Microsoft
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e252769c26a5491100094b1243b9c2c6bb67d94d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285701"
---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt Function
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLFreeStmt** interrompe l'elaborazione associata a un'istruzione specifica, chiude tutti i cursori aperti associati all'istruzione, elimina i risultati in sospeso o, facoltativamente, libera tutte le risorse associate all'handle dell'istruzione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione  
  
 *Opzione*  
 [Ingresso] Una delle seguenti opzioni:  
  
 SQL_ CLOSE: chiude il cursore associato a *StatementHandle* (se ne è stato definito uno) ed elimina tutti i risultati in sospeso. L'applicazione può riaprire il cursore in un secondo momento eseguendo nuovamente un'istruzione **SELECT** con valori di parametro uguali o diversi. Se non è aperto alcun cursore, questa opzione non ha alcun effetto per l'applicazione. **SQLCloseCursor** può anche essere chiamato per chiudere un cursore. Per ulteriori informazioni, consultate [Chiusura del cursore.](../../../odbc/reference/develop-app/closing-the-cursor.md)  
  
 SQL_DROP: questa opzione è deprecata. Una chiamata a **SQLFreeStmt** con *un'opzione* di SQL_DROP viene mappata in Gestione Driver a [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
 SQL_UNBIND: imposta il campo SQL_DESC_COUNT di ARD su 0, rilasciando tutti i buffer di colonna associati da **SQLBindCol** per *l'oggetto StatementHandle*specificato. In questo modo non viene annullata l'associazione della colonna del segnalibro. a tale scopo, il campo SQL_DESC_DATA_PTR dell'ARD per la colonna del segnalibro è impostato su NULL. Si noti che se questa operazione viene eseguita su un descrittore allocato in modo esplicito condiviso da più di un'istruzione, l'operazione influirà sulle associazioni di tutte le istruzioni che condividono il descrittore. Per ulteriori informazioni, vedere [Panoramica del recupero dei risultati (base)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 SQL_RESET_PARAMS: imposta il campo SQL_DESC_COUNT di APD su 0, rilasciando tutti i buffer di parametri impostati da **SQLBindParameter** per *l'oggetto StatementHandle*specificato. Se questa operazione viene eseguita su un descrittore allocato in modo esplicito condiviso da più di un'istruzione, questa operazione influirà sulle associazioni di tutte le istruzioni che condividono il descrittore. Per ulteriori informazioni, vedere [Parametri di associazione](../../../odbc/reference/develop-app/binding-parameters-odbc.md).  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLFreeStmt** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *Handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLFreeStmt** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando **SQLFreeStmt** è stato chiamato.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata con *Option* impostato su SQL_RESET_PARAMS prima che i dati venisseero recuperati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono è stata chiamata per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I092 (informazioni in stato IN CUI|Tipo di opzione fuori intervallo|(DM) Il valore specificato per l'argomento *Opzione* non è:<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Chiamare **SQLFreeStmt** con l'opzione SQL_CLOSE equivale a chiamare **SQLCloseCursor**, con la differenza che **SQLFreeStmt** con SQL_CLOSE non influisce sull'applicazione se sull'istruzione non è aperto alcun cursore. Se non è aperto alcun cursore, una chiamata a **SQLCloseCursor** restituisce SQLSTATE 24000 (stato del cursore non valido).  
  
 Un'applicazione non deve utilizzare un handle di istruzione dopo che è stato liberato; Gestione Driver non controlla la validità di un handle in una chiamata di funzione.  
  
## <a name="example"></a>Esempio  
 È una buona pratica di programmazione per liberare maniglie. Tuttavia, per semplicità, l'esempio seguente non include il codice che libera gli handle allocati. Per un esempio di come liberare gli handle, vedere [Funzione SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
```cpp  
// SQLFreeStmt.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
   retCode = SQLFreeStmt(hstmt, SQL_UNBIND);  
   retCode = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
}  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Allocazione di una maniglia|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Chiusura di un cursore|[Funzione SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Liberare una maniglia|[SQLFreeHandle Function](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Impostazione del nome di un cursore|[Funzione SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
