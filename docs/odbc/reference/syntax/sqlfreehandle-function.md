---
title: Funzione SQLFreeHandle . Documenti Microsoft
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b136dec98a19676aa67c78615d8fe931f62aafa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285772"
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle Function
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLFreeHandle** libera le risorse associate a un ambiente, una connessione, un'istruzione o un handle di descrittore specifico.  
  
> [!NOTE]
>  Questa funzione è una funzione generica per liberare gli handle. Sostituisce le funzioni ODBC 2.0 **SQLFreeConnect** (per liberare un handle di connessione) e **SQLFreeEnv** (per liberare un handle di ambiente). **SQLFreeConnect** e **SQLFreeEnv** sono entrambi deprecati in ODBC 3 *.x*. **SQLFreeHandle** sostituisce inoltre la funzione ODBC 2.0 **SQLFreeStmt** (con *l'opzione*SQL_DROP ) per aver liberato un handle di istruzione. Per ulteriori informazioni, vedere "Commenti". Per ulteriori informazioni su ciò che Gestione Driver esegue il mapping di questa funzione a quando un'applicazione ODBC 3 *.x* utilizza un driver *.x* ODBC 2, vedere Mapping di funzioni di sostituzione per la [compatibilità con](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)le versioni precedenti delle applicazioni .  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>Argomenti  
 *HandleType*  
 [Ingresso] Tipo di handle che deve essere liberato da **SQLFreeHandle.** Deve essere uno dei valori seguenti:   
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN handle viene utilizzato solo da Gestione Driver e dal driver. Le applicazioni non devono utilizzare questo tipo di handle. Per ulteriori informazioni su SQL_HANDLE_DBC_INFO_TOKEN, vedere Sviluppo del [riconoscimento](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)del pool di connessioni in un driver ODBC .  
  
 Se *HandleType* non è uno di questi valori, **SQLFreeHandle** restituisce SQL_INVALID_HANDLE.  
  
 *Handle*  
 [Ingresso] Handle da liberare.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_ERROR o SQL_INVALID_HANDLE.  
  
 Se **SQLFreeHandle** restituisce SQL_ERROR, l'handle è ancora valido.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLFreeHandle** restituisce SQL_ERROR, un valore SQLSTATE associato può essere ottenuto dalla struttura dei dati di diagnostica per l'handle che **SQLFreeHandle** ha tentato di liberare ma non è stato possibile. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLFreeHandle** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) l'argomento *HandleType* è stato SQL_HANDLE_ENV e almeno una connessione si trovava in uno stato allocato o connesso. **SQLDisconnect** e **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DBC devono essere chiamati per ogni connessione prima di chiamare **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_ENV.<br /><br /> (DM) il *HandleType* argomento è stato SQL_HANDLE_DBC e la funzione è stata chiamata prima di chiamare **SQLDisconnect** per la connessione.<br /><br /> (DM) l'argomento *HandleType* è stato SQL_HANDLE_DBC. Una funzione in esecuzione asincrona è stata chiamata con *Handle* e la funzione era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) l'argomento *HandleType* è stato SQL_HANDLE_STMT. **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato con l'handle dell'istruzione e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) l'argomento *HandleType* è stato SQL_HANDLE_STMT. Una funzione in esecuzione asincrona è stata chiamata sull'handle dell'istruzione o sull'handle di connessione associato e la funzione era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) L'argomento *HandleType* è stato SQL_HANDLE_DESC. Una funzione in esecuzione asincrona è stata chiamata sull'handle di connessione associato; e la funzione era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) Tutti gli handle delle filiali e altre risorse non sono stati rilasciati prima della chiamata di **SQLFreeHandle.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per uno degli handle di istruzione associati *a Handle* e *HandleType* è stato impostato su SQL_HANDLE_STMT o SQL_HANDLE_DESC restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.|  
|HY013|Errore di gestione della memoria|L'argomento *HandleType* è stato SQL_HANDLE_STMT o SQL_HANDLE_DESC e non è stato possibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostanti, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY017|Utilizzo non valido di un handle di descrittore allocato automaticamente.|(DM) L'argomento *Handle* è stato impostato sull'handle per un descrittore allocato automaticamente.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) l'argomento *HandleType* è stato SQL_HANDLE_DESC e il driver era un driver *.x* ODBC 2.<br /><br /> (DM) l'argomento *HandleType* è stato SQL_HANDLE_STMT e il driver non è un driver ODBC valido.|  
  
## <a name="comments"></a>Commenti  
 **SQLFreeHandle** viene utilizzato per liberare gli handle per ambienti, connessioni, istruzioni e descrittori, come descritto nelle sezioni seguenti. Per informazioni generali sulle maniglie, vedere [Maniglie](../../../odbc/reference/develop-app/handles.md).  
  
 Un'applicazione non deve utilizzare un handle dopo che è stato liberato; Gestione Driver non controlla la validità di un handle in una chiamata di funzione.  
  
## <a name="freeing-an-environment-handle"></a>Liberare una maniglia dell'ambienteFreeing an Environment Handle  
 Prima di chiamare **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_ENV, un'applicazione deve chiamare **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DBC per tutte le connessioni allocate nell'ambiente. In caso contrario, la chiamata a **SQLFreeHandle** restituisce SQL_ERROR e l'ambiente e qualsiasi connessione attiva rimane valida. Per ulteriori informazioni, vedere [Handle di ambiente](../../../odbc/reference/develop-app/environment-handles.md) e [Allocazione dell'handle di ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Se l'ambiente è un ambiente condiviso, l'applicazione che chiama **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_ENV non ha più accesso all'ambiente dopo la chiamata, ma le risorse dell'ambiente non vengono necessariamente liberate. La chiamata a **SQLFreeHandle** decrementa il conteggio dei riferimenti dell'ambiente. Il conteggio dei riferimenti viene mantenuto da Gestione Driver. Se non raggiunge lo zero, l'ambiente condiviso non viene liberato, perché è ancora utilizzato da un altro componente. Se il conteggio dei riferimenti raggiunge lo zero, le risorse dell'ambiente condiviso vengono liberate.  
  
## <a name="freeing-a-connection-handle"></a>Liberare un handle di connessioneFreeing a Connection Handle  
 Prima di chiamare **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DBC, un'applicazione deve chiamare **SQLDisconnect** per la connessione se è presente una connessione su questo handle *.* In caso contrario, la chiamata a **SQLFreeHandle** restituisce SQL_ERROR e la connessione rimane valida.  
  
 Per ulteriori informazioni, vedere Handle di [connessione](../../../odbc/reference/develop-app/connection-handles.md) e [disconnessione da un'origine dati o da un driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="freeing-a-statement-handle"></a>Rilascio di un handle di istruzione  
 Una chiamata a **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_STMT libera tutte le risorse allocate da una chiamata a **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_STMT. Quando un'applicazione chiama **SQLFreeHandle** per liberare un'istruzione con risultati in sospeso, i risultati in sospeso vengono eliminati. Quando un'applicazione libera un handle di istruzione, il driver libera i quattro descrittori allocati automaticamente associati a tale handle. Per ulteriori informazioni, vedere Handle di [istruzione](../../../odbc/reference/develop-app/statement-handles.md) e [Liberazione di un handle di istruzione](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 Si noti che **SQLDisconnect** elimina automaticamente tutte le istruzioni e i descrittori aperti sulla connessione.  
  
## <a name="freeing-a-descriptor-handle"></a>Liberare un handle di descrittoreFreeing a Descriptor Handle  
 Una chiamata a **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DESC libera l'handle del descrittore in *Handle*. La chiamata a **SQLFreeHandle** non rilascia la memoria allocata dall'applicazione a cui può fare riferimento un campo puntatore (inclusi SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR) di qualsiasi record descrittore di *Handle*. La memoria allocata dal driver per i campi che non sono campi puntatore viene liberata quando l'handle viene liberato. Quando un handle di descrittore allocato dall'utente viene liberato, tutte le istruzioni che l'handle liberato era stato associato ai rispettivi handle di descrittore allocati automaticamente.  
  
> [!NOTE]
>  I driver *.x* ODBC 2 non supportano la liberazione degli handle di descrittore, così come non supportano l'allocazione degli handle di descrittore.  
  
 Si noti che **SQLDisconnect** elimina automaticamente tutte le istruzioni e i descrittori aperti sulla connessione. Quando un'applicazione libera un handle di istruzione, il driver libera tutti i descrittori generati automaticamente associati a tale handle.  
  
 Per ulteriori informazioni sui descrittori, vedere [Descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Per altri esempi di codice, vedere [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) e [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
### <a name="code"></a>Codice  
  
```cpp  
// SQLFreeHandle.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <stdio.h>  
  
int main() {  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   // Initialize the environment, connection, statement handles.  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   // Allocate the environment.  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set environment attributes.  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
  
   // Allocate the connection.  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
   // Set the login timeout.  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
  
   // Let the user select the data source and connect to the database.  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Free handles, and disconnect.     
   if (hstmt) {   
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
      hstmt = NULL;   
   }  
   if (hdbc) {   
      SQLDisconnect(hdbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      hdbc = NULL;   
   }  
   if (henv) {   
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
      henv = NULL;   
   }  
}  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Allocazione di una maniglia|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCance](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Impostazione del nome di un cursore|[Funzione SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programma di esempio ODBC](../../../odbc/reference/sample-odbc-program.md)
