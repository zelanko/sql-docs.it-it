---
title: Funzione SQLFreeHandle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0ddaae66e60f77156b2d7c7e975875bb78d56cb
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537323"
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle Function
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLFreeHandle** libera le risorse associate a un handle di ambiente, connessione, istruzione o descrittore specifico.  
  
> [!NOTE]
>  Questa funzione è una funzione generica per il rilascio di handle. Sostituisce le funzioni ODBC 2.0 **SQLFreeConnect** (per il rilascio di un handle di connessione) e **SQLFreeEnv** (per il rilascio di un handle di ambiente). **SQLFreeConnect** e **SQLFreeEnv** sono entrambe deprecate in ODBC 3*x*. **SQLFreeHandle** sostituisce anche la funzione ODBC 2.0 **SQLFreeStmt** (con il SQL_DROP *opzione*) per il rilascio di un handle di istruzione. Per altre informazioni, vedere "Commenti". Per altre informazioni su cosa the Driver Manager esegue il mapping a questa funzione quando un'applicazione ODBC 3 *. x* applicazione funziona con un'API ODBC 2 *. x* driver, vedere [Mapping di funzioni di sostituzione per Aut Compatibilità delle applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>Argomenti  
 *HandleType*  
 [Input] Il tipo di handle da liberare da **SQLFreeHandle**. Deve essere uno dei valori seguenti:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Handle SQL_HANDLE_DBC_INFO_TOKEN è utilizzato solo da Gestione Driver e del driver. Le applicazioni non devono usare questo tipo di handle. Per altre informazioni sulle SQL_HANDLE_DBC_INFO_TOKEN, vedere [lo sviluppo di riconoscimento dei Pool di connessioni in un Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 Se *HandleType* non è uno di questi valori, **SQLFreeHandle** non restituisca SQL_INVALID_HANDLE.  
  
 *Handle*  
 [Input] Handle da liberare.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS o SQL_ERROR, SQL_INVALID_HANDLE.  
  
 Se **SQLFreeHandle** restituisce SQL_ERROR, l'handle sia ancora valido.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLFreeHandle** restituisce SQL_ERROR, un valore SQLSTATE associato possono essere ottenuti dalla struttura di dati di diagnostica per l'handle che **SQLFreeHandle** ha provato a gratuito ma non è riuscito. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLFreeHandle** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver non è riuscito ad allocare memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) di *HandleType* argomento era SQL_HANDLE_ENV e almeno una connessione in uno stato allocato e quelle connesso. **SQLDisconnect** e **SQLFreeHandle** con un *HandleType* SQL_HANDLE_DBC deve essere chiamato per ogni connessione prima di chiamare **SQLFreeHandle** con un *HandleType* SQL_HANDLE_ENV.<br /><br /> (DM) di *HandleType* argomento era SQL_HANDLE_DBC e la funzione è stata chiamata prima di chiamare **SQLDisconnect** per la connessione.<br /><br /> (DM) di *HandleType* argomento era SQL_HANDLE_DBC. Una funzione in modo asincrono in esecuzione è stata chiamata con *gestire* e la funzione era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) di *HandleType* argomento era SQL_HANDLE_STMT. **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato con l'handle di istruzione e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.<br /><br /> (DM) di *HandleType* argomento era SQL_HANDLE_STMT. Una funzione in modo asincrono in esecuzione è stata chiamata nell'handle di istruzione o nell'handle di connessione associata e la funzione era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) di *HandleType* argomento era SQL_HANDLE_DESC. Una funzione in modo asincrono in esecuzione è stata chiamata nell'handle di connessione associata; e la funzione era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) gestisce tutto sussidiari e altre risorse non sono state rilasciate prima **SQLFreeHandle** è stato chiamato.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per uno degli handle di istruzione associati il *gestire* e *HandleType* è stato impostato su SQL_HANDLE_STMT o SQL_HANDLE_DESC restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.|  
|HY013|Errore di gestione della memoria|Il *HandleType* argomento era SQL_HANDLE_STMT o SQL_HANDLE_DESC e la chiamata di funzione non è stata elaborata perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY017|Utilizzo non valido di un handle di descrittore allocato automaticamente.|(DM) di *gestire* argomento è stato impostato per l'handle per un descrittore allocato automaticamente.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|(DM) di *HandleType* argomento era SQL_HANDLE_DESC e il driver ODBC un 2*x* driver.<br /><br /> (DM) di *HandleType* argomento era SQL_HANDLE_STMT e il driver non è un driver ODBC valido.|  
  
## <a name="comments"></a>Commenti  
 **SQLFreeHandle** viene utilizzata per liberare l'handle per gli ambienti, le connessioni, le istruzioni e i descrittori, come descritto nelle sezioni seguenti. Per informazioni generali sugli handle, vedere [handle](../../../odbc/reference/develop-app/handles.md).  
  
 Un'applicazione non deve usare un punto di manipolazione dopo che è stata liberata; Gestione Driver non verifica la validità di un handle di una chiamata di funzione.  
  
## <a name="freeing-an-environment-handle"></a>Rilascio di un Handle di ambiente  
 Prima di chiamare **SQLFreeHandle** con un *HandleType* SQL_HANDLE_ENV, un'applicazione deve chiamare **SQLFreeHandle** con un *HandleType*SQL_HANDLE_DBC per tutte le connessioni allocata con l'ambiente. In caso contrario, la chiamata a **SQLFreeHandle** restituisce SQL_ERROR e l'ambiente e le connessioni attiva rimane valido. Per altre informazioni, vedere [ambiente gestisce](../../../odbc/reference/develop-app/environment-handles.md) e [allocare l'Handle di ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Se l'ambiente è un ambiente condiviso, l'applicazione che chiama **SQLFreeHandle** con un *HandleType* SQL_HANDLE_ENV non avrà più accesso per l'ambiente dopo la chiamata, ma l'ambiente le risorse non sono necessariamente liberate. La chiamata a **SQLFreeHandle** decrementa il conteggio dei riferimenti dell'ambiente. Il conteggio dei riferimenti viene gestito da Gestione Driver. Se non raggiunge lo zero, non viene liberata ambiente condiviso, perché è ancora in uso da un altro componente. Se il conteggio dei riferimenti arriva a zero, vengono liberate le risorse dell'ambiente condiviso.  
  
## <a name="freeing-a-connection-handle"></a>Rilascio di un Handle di connessione  
 Prima di chiamare **SQLFreeHandle** con un *HandleType* SQL_HANDLE_DBC, un'applicazione deve chiamare **SQLDisconnect** per la connessione solo se è disponibile una connessione su questo gestire *.* In caso contrario, la chiamata a **SQLFreeHandle** restituisce SQL_ERROR e la connessione rimane valido.  
  
 Per altre informazioni, vedere [handle di connessione](../../../odbc/reference/develop-app/connection-handles.md) e [disconnessione da un'origine dati o Driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="freeing-a-statement-handle"></a>Rilascio di un handle di istruzione  
 Una chiamata a **SQLFreeHandle** con un *HandleType* SQL_HANDLE_STMT libera tutte le risorse che sono state allocate da una chiamata a **SQLAllocHandle** con un  *HandleType* SQL_HANDLE_STMT. Quando un'applicazione chiama **SQLFreeHandle** per liberare un'istruzione con risultati in sospeso, vengono eliminati i risultati in sospeso. Quando un'applicazione libera un handle di istruzione, il driver libera i quattro descrittori allocati automaticamente associati a tale handle. Per altre informazioni, vedere [istruzione gestisce](../../../odbc/reference/develop-app/statement-handles.md) e [liberando un Handle di istruzione](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 Si noti che **SQLDisconnect** automaticamente elimina eventuali istruzioni e i descrittori di aprire la connessione.  
  
## <a name="freeing-a-descriptor-handle"></a>Rilascio di un Handle descrittore  
 Una chiamata a **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DESC rilascia l'handle descrittore nel *gestire*. La chiamata a **SQLFreeHandle** non rilasci di qualsiasi quantità di memoria allocata dall'applicazione che potrà farvi riferimento da un campo del puntatore (inclusi SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR) il record del descrittore dei *gestire*. La memoria allocata dal driver per i campi che non sono campi puntatore viene liberata quando l'handle viene liberata. Quando viene liberato un handle di descrittore allocato dall'utente, tutte le istruzioni che era stato associato l'handle liberato ripristino relativi handle di descrittore allocato automaticamente corrispondente.  
  
> [!NOTE]
>  ODBC 2*x* driver non supportano liberata handle descrittore, semplicemente perché non supportano allocare gli handle di descrittore.  
  
 Si noti che **SQLDisconnect** automaticamente elimina eventuali istruzioni e i descrittori di aprire la connessione. Quando un'applicazione libera un handle di istruzione, il driver libera tutti i descrittori generati automaticamente associati con tale handle.  
  
 Per altre informazioni sui descrittori, vedere [descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Per ulteriori esempi di codice, vedere [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) e [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
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
|Allocazione di un handle|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Annullare l'elaborazione di istruzione|[SQLCance Functionl](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Impostazione di un nome di cursore|[Funzione SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programma di esempio ODBC](../../../odbc/reference/sample-odbc-program.md)
