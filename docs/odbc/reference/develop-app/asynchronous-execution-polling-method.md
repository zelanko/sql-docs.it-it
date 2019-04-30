---
title: L'esecuzione asincrona (metodo di Polling) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ca0a5094e40f13aef4b4f87d5642e51e7a9b765
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306294"
---
# <a name="asynchronous-execution-polling-method"></a>Esecuzione asincrona (metodo di polling)
Prima di ODBC 3.8 e Windows 7 SDK, operazioni asincrone sono state consentite solo per le funzioni di istruzione. Per altre informazioni, vedere la **l'esecuzione di istruzione operazioni in modo asincrono**, più avanti in questo argomento.  
  
 ODBC 3.8 in Windows 7 SDK è stato introdotto l'esecuzione asincrona nelle operazioni correlate alla connessione. Per altre informazioni, vedere la **l'esecuzione asincrona di operazioni di connessione** più avanti in questo argomento.  
  
 In Windows 7 SDK, per istruzione asincrona o operazioni di connessione, un'applicazione determinato che l'operazione asincrona è completa usando il metodo di polling. A partire da Windows 8 SDK, è possibile determinare che un'operazione asincrona viene completata tramite il metodo di notifica. Per altre informazioni, vedere [esecuzione asincrona (metodo di notifica)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
 Per impostazione predefinita, i driver di eseguire funzioni ODBC in modo sincrono; vale a dire, l'applicazione chiama una funzione e il driver non restituisce il controllo all'applicazione fino a quando non ha terminato l'esecuzione della funzione. Tuttavia, alcune funzioni possono essere eseguite in modo asincrono; vale a dire, l'applicazione chiama la funzione e il driver, dopo l'elaborazione minimo, restituisce il controllo all'applicazione. L'applicazione può quindi chiamare altre funzioni durante la prima funzione è ancora in esecuzione.  
  
 L'esecuzione asincrona è supportata per la maggior parte delle funzioni che sono in gran parte eseguite sull'origine dati, ad esempio le funzioni per stabilire le connessioni, preparare ed eseguire istruzioni SQL, recuperare i metadati, recuperare i dati e commit delle transazioni. È particolarmente utile quando l'attività viene eseguita sull'origine dati richiede molto tempo, ad esempio un processo di accesso o una query complessa su un database di grandi dimensioni.  
  
 Quando l'applicazione esegue una funzione con un'istruzione o una connessione abilitata per l'elaborazione asincrona, il driver esegue una quantità minima di elaborazione (ad esempio verifica gli argomenti per gli errori), passa l'elaborazione all'origine dati e restituisce controllo all'applicazione con il codice restituito SQL_STILL_EXECUTING. Quindi, l'applicazione esegue altre attività. Per determinare quando ha terminato la funzione asincrona, l'applicazione esegue il polling il driver a intervalli regolari, chiamando la funzione con gli stessi argomenti è stato originariamente usato. Se la funzione è ancora in esecuzione, restituisce SQL_STILL_EXECUTING; Se ha terminato l'esecuzione, viene restituito il codice che avrebbe restituito era eseguita in modo sincrono, come SQL_SUCCESS o SQL_ERROR SQL_NEED_DATA.  
  
 Se viene eseguita una funzione in modo sincrono o asincrono è specifici del driver. Si supponga, ad esempio, che viene memorizzato nella cache i metadati di set di risultati nel driver. In questo caso, richiede pochissimo tempo per eseguire **SQLDescribeCol** e il driver deve semplicemente eseguire la funzione, anziché artificialmente ritardare l'esecuzione. D'altra parte, se il driver deve recuperare i metadati dall'origine dati, deve restituire il controllo all'applicazione mentre sta ottenendo questo risultato. Pertanto, l'applicazione deve essere in grado di gestire un codice restituito diverso da SQL_STILL_EXECUTING dopo l'esecuzione di una funzione in modo asincrono.  
  
## <a name="executing-statement-operations-asynchronously"></a>L'esecuzione di operazioni di istruzione in modo asincrono  
 Le funzioni di istruzione seguenti operano su un'origine dati e possono eseguire in modo asincrono:  
  
||||  
|-|-|-|  
|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
 Esecuzione asincrona delle istruzioni è controllata in una singola istruzione o una singola connessione, a seconda dell'origine dati. Vale a dire, l'applicazione non specifica che una particolare funzione deve essere eseguito in modo asincrono, ma che qualsiasi funzione eseguita in una particolare istruzione deve essere eseguito in modo asincrono. Per trovare istanze cui è supportata, un'applicazione chiama [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) con un'opzione di SQL_ASYNC_MODE. SQL_AM_CONNECTION viene restituito se è supportata l'esecuzione asincrona a livello di connessione (per un handle di istruzione). SQL_AM_STATEMENT se è supportata l'esecuzione asincrona a livello di istruzione.  
  
 Per specificare che le funzioni eseguite con una particolare istruzione devono essere eseguite in modo asincrono, l'applicazione chiama **SQLSetStmtAttr** con il SQL_ATTR_ASYNC_ENABLE attributo e lo imposta su SQL_ASYNC_ENABLE_ON. Se è supportata l'elaborazione asincrona a livello di connessione, l'attributo di istruzione SQL_ATTR_ASYNC_ENABLE è di sola lettura e il relativo valore è quello utilizzato per l'attributo di connessione della connessione in cui l'istruzione è stata allocata. È specifico del driver indica se il valore dell'attributo di istruzione è impostato in fase di allocazione di istruzione o in un secondo momento. Provare a impostarla restituirà SQL_ERROR e SQLSTATE HYC00 (funzionalità facoltativa non implementata).  
  
 Per specificare che le funzioni eseguite con una determinata connessione devono essere eseguite in modo asincrono, l'applicazione chiama **SQLSetConnectAttr** con il SQL_ATTR_ASYNC_ENABLE attributo e lo imposta su SQL_ASYNC_ENABLE_ON. Tutti gli handle di istruzione future allocati per la connessione verranno abilitati per l'esecuzione asincrona; è definito dal driver indica se gli handle di istruzione esistente saranno abilitati per questa azione. Se è impostato SQL_ATTR_ASYNC_ENABLE su SQL_ASYNC_ENABLE_OFF, tutte le istruzioni per la connessione sono in modalità sincrona. Se è abilitata l'esecuzione asincrona mentre è presente un'istruzione attiva nella connessione, viene restituito un errore.  
  
 Per determinare il numero massimo di istruzioni simultanee attive in modalità asincrona in grado di supportare il driver in una determinata connessione, l'applicazione chiama **SQLGetInfo** con l'opzione SQL_MAX_ASYNC_CONCURRENT_STATEMENTS.  
  
 Il codice seguente illustra come funziona il modello di polling:  
  
```  
SQLHSTMT  hstmt1;  
SQLRETURN rc;  
  
// Specify that the statement is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute a SELECT statement asynchronously.  
while ((rc=SQLExecDirect(hstmt1,"SELECT * FROM Orders",SQL_NTS))==SQL_STILL_EXECUTING) {  
   // While the statement is still executing, do something else.  
   // Do not use hstmt1, because it is being used asynchronously.  
}  
  
// When the statement has finished executing, retrieve the results.  
```  
  
 Mentre una funzione è in esecuzione in modo asincrono, l'applicazione può chiamare le funzioni in tutte le altre istruzioni. L'applicazione può anche chiamare funzioni in qualsiasi connessione, ad eccezione di quello associata all'istruzione asincrona. Ma l'applicazione può solo chiamare la funzione originale e le funzioni seguenti (con l'handle di istruzione o la connessione associata, handle di ambiente), dopo un'operazione di istruzione restituisce SQL_STILL_EXECUTING:  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) (nell'handle di istruzione)  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 Se l'applicazione chiama qualsiasi altra funzione con l'istruzione asincrona o con la connessione associata a tale istruzione, la funzione restituisce SQLSTATE HY010 (funzione di errore nella sequenza), ad esempio.  
  
```  
SQLHDBC       hdbc1, hdbc2;  
SQLHSTMT      hstmt1, hstmt2, hstmt3;  
SQLCHAR *     SQLStatement = "SELECT * FROM Orders";  
SQLUINTEGER   InfoValue;  
SQLRETURN     rc;  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt2);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc2, &hstmt3);  
  
// Specify that hstmt1 is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute hstmt1 asynchronously.  
while ((rc = SQLExecDirect(hstmt1, SQLStatement, SQL_NTS)) == SQL_STILL_EXECUTING) {  
   // The following calls return HY010 because the previous call to  
   // SQLExecDirect is still executing asynchronously on hstmt1. The  
   // first call uses hstmt1 and the second call uses hdbc1, on which  
   // hstmt1 is allocated.  
   SQLExecDirect(hstmt1, SQLStatement, SQL_NTS);   // Error!  
   SQLGetInfo(hdbc1, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // Error!  
  
   // The following calls do not return errors. They use a statement  
   // handle other than hstmt1 or a connection handle other than hdbc1.  
   SQLExecDirect(hstmt2, SQLStatement, SQL_NTS);   // OK  
   SQLTables(hstmt3, NULL, 0, NULL, 0, NULL, 0, NULL, 0);   // OK  
   SQLGetInfo(hdbc2, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // OK  
}  
```  
  
 Quando un'applicazione chiama una funzione per determinare se è ancora in esecuzione in modo asincrono, deve usare l'handle di istruzione originale. Questo avviene perché l'esecuzione asincrona viene tenuta traccia in base a una singola istruzione. L'applicazione deve anche fornire i valori validi per gli altri argomenti - degli argomenti originali dovrà svolgere - per superare errori in Gestione Driver. Tuttavia, dopo che il driver controlla l'handle di istruzione e determina che l'istruzione viene eseguita in modo asincrono, ignora tutti gli altri argomenti.  
  
 Durante l'esecuzione di una funzione in modo asincrono, vale a dire, dopo che ha restituito SQL_STILL_EXECUTING e prima che venga restituito un codice diverso - l'applicazione possibile annullarlo chiamando **SQLCancel** o **SQLCancelHandle** con lo stesso handle di istruzione. Non è garantita per annullare l'esecuzione della funzione. Ad esempio, la funzione potrebbe essere già stato completato. Inoltre, il codice restituito da **SQLCancel** oppure **SQLCancelHandle** indica solo se il tentativo di annullare la funzione ha avuto esito positivo, non se è effettivamente annullata la funzione. Per determinare se la funzione è stata annullata, l'applicazione chiama la funzione nuovamente. Se la funzione è stata annullata, viene restituito SQL_ERROR e SQLSTATE HY008 (operazione annullata). Se la funzione non è stata annullata, viene restituito un altro codice, come SQL_SUCCESS, SQL_STILL_EXECUTING o SQL_ERROR con SQLSTATE un diverso.  
  
 Per disabilitare l'esecuzione asincrona di una particolare istruzione quando il driver supporta l'elaborazione asincrona a livello di istruzione, l'applicazione chiama **SQLSetStmtAttr** con il SQL_ATTR_ASYNC_ENABLE attributo e lo imposta su SQL _ ASYNC_ENABLE_OFF. Se il driver supporta l'elaborazione asincrona a livello di connessione, l'applicazione chiama **SQLSetConnectAttr** per impostare SQL_ATTR_ASYNC_ENABLE su SQL_ASYNC_ENABLE_OFF, che disabilita l'esecuzione asincrona di tutte le istruzioni di connessione.  
  
 L'applicazione deve elaborare i record di diagnostica nel ciclo ripetuto della funzione originale. Se **SQLGetDiagField** oppure **SQLGetDiagRec** viene chiamato quando una funzione asincrona è in esecuzione, verrà restituito l'elenco corrente dei record di diagnostica. Ogni volta che la chiamata di funzione originale viene ripetuta, Cancella i record di diagnostica precedenti.  
  
## <a name="executing-connection-operations-asynchronously"></a>L'esecuzione di operazioni di connessione in modo asincrono  
 Prima di ODBC 3.8, l'esecuzione asincrona era consentito per la preparazione, ad esempio operazioni correlate a istruzione, eseguire e recuperare, come operazioni sui metadati di catalogo. A partire da ODBC 3.8, l'esecuzione asincrona è inoltre possibile per le operazioni correlate alla connessione che quali come connettere, disconnettere, commit e rollback.  
  
 Per altre informazioni su ODBC 3.8, vedere [What ' s New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
 L'esecuzione di operazioni di connessione in modo asincrono è utile negli scenari seguenti:  
  
-   Quando un numero ridotto di thread gestisce un numero elevato di dispositivi con dati molto elevate. Per ottimizzare la velocità di risposta e la scalabilità è auspicabile per tutte le operazioni siano asincroni.  
  
-   Quando si desidera la sovrapposizione delle operazioni di database tra più connessioni a ridurre i tempi di trasferimento trascorso.  
  
-   Efficienti chiamate ODBC asincrone e la possibilità di annullare le operazioni di connessione consentono a un'applicazione consentire all'utente di annullare qualsiasi operazione lenta senza dover attendere il timeout.  
  
 Le funzioni seguenti, che operano su handle di connessione, ora possono essere eseguite in modo asincrono:  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 Per determinare se un driver supporta le operazioni asincrone in queste funzioni, un'applicazione chiama **SQLGetInfo** con SQL_ASYNC_DBC_FUNCTIONS. SQL_ASYNC_DBC_CAPABLE viene restituito se le operazioni asincrone sono supportate. SQL_ASYNC_DBC_NOT_CAPABLE viene restituito se non sono supportate le operazioni asincrone.  
  
 Per specificare che le funzioni eseguite con una determinata connessione devono essere eseguite in modo asincrono, l'applicazione chiama **SQLSetConnectAttr** e imposta l'attributo SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE SQL_ASYNC_DBC_ENABLE ATTIVATO. Impostare un attributo di connessione prima di stabilire una connessione sempre esegue in modo sincrono. Inoltre, l'operazione di impostazione della connessione attributo SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE con **SQLSetConnectAttr** viene sempre eseguito in modo sincrono.  
  
 Un'applicazione può attivare l'operazione asincrona prima di effettuare una connessione. Poiché gestione Driver non è possibile determinare quale driver da usare prima di effettuare una connessione, gestione Driver restituirà sempre esito positivo **SQLSetConnectAttr**. Tuttavia, potrebbe non riuscire a connettersi se il driver ODBC non supporta operazioni asincrone.  
  
 In generale, possono esserci al massimo uno in modo asincrono l'esecuzione di funzione associata a un handle di connessione specifico o un handle di istruzione. Tuttavia, un handle di connessione può avere più di un handle di istruzione associati. Se è presente alcuna operazione asincrona in esecuzione nell'handle di connessione, un handle di istruzione associati può eseguire un'operazione asincrona. Analogamente, è possibile avere un'operazione asincrona su un handle di connessione se non sono presenti operazioni asincrone in corso su qualsiasi handle di istruzione associata. Un tentativo di eseguire un'operazione asincrona utilizzando un handle che sta attualmente eseguendo un'operazione asincrona restituirà HY010, "Errore nella funzione sequenza".  
  
 Se un'operazione di connessione restituisce SQL_STILL_EXECUTING, un'applicazione può solo chiamare la funzione originale e le funzioni seguenti per tale handle di connessione:  
  
-   **SQLCancelHandle** (nell'handle di connessione)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (allocando ENV o a due byte)  
  
-   **SQLAllocHandleStd** (allocando ENV o a due byte)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 L'applicazione deve elaborare i record di diagnostica nel ciclo ripetuto della funzione originale. Se SQLGetDiagField o SQLGetDiagRec viene chiamato quando una funzione asincrona è in esecuzione, restituirà l'elenco corrente dei record di diagnostica. Ogni volta che la chiamata di funzione originale viene ripetuta, Cancella i record di diagnostica precedenti.  
  
 Se è in corso una connessione aperta o chiusa in modo asincrono, l'operazione è completata quando l'applicazione riceve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO nella chiamata di funzione originale.  
  
 È stata aggiunta una nuova funzione a ODBC 3.8, **SQLCancelHandle**. Questa funzione Annulla le funzioni di sei connessione (**SQLBrowseConnect**, **SQLConnect**, **SQLDisconnect**, **SQLDriverConnect**, **SQLEndTran**, e **SQLSetConnectAttr**). Un'applicazione deve chiamare **SQLGetFunctions** per determinare se il driver supporta **SQLCancelHandle**. Come per gli **SQLCancel**, se **SQLCancelHandle** restituisce l'esito positivo, questo non significa che l'operazione è stata annullata. Un'applicazione deve chiamare la funzione originale per determinare se l'operazione è stata annullata. **SQLCancelHandle** consente di annullare le operazioni asincrone in handle di connessione o gli handle di istruzione. Usando **SQLCancelHandle** per annullare un'operazione su un'istruzione di handle è uguale alla chiamata al metodo **SQLCancel**.  
  
 Non è necessario supportare entrambe **SQLCancelHandle** e le operazioni di connessione asincrona nello stesso momento. Un driver può supportare operazioni di connessione asincrona, ma non **SQLCancelHandle**, o viceversa.  
  
 Operazioni di connessione asincrona e **SQLCancelHandle** può inoltre essere utilizzato da ODBC 3.x e ODBC 2.x applicazioni con un driver di ODBC 3.8 e gestione dei Driver di ODBC 3.8. Per informazioni su come abilitare un'applicazione precedente per le nuove funzionalità di versione più recente ODBC, vedere [matrice di compatibilità](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
### <a name="connection-pooling"></a>Pool di connessioni  
 Ogni volta che il pool di connessioni è abilitato, le operazioni asincrone sono supportate solo minimamente per stabilire una connessione (con **SQLConnect** e **SQLDriverConnect**) e chiusura di una connessione con **SQLDisconnect**. Ma un'applicazione deve comunque essere in grado di gestire il valore restituito SQL_STILL_EXECUTING dal **SQLConnect**, **SQLDriverConnect**, e **SQLDisconnect**.  
  
 Quando il pool di connessioni è abilitato, **SQLEndTran** e **SQLSetConnectAttr** sono supportati per le operazioni asincrone.  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente viene illustrato come utilizzare **SQLSetConnectAttr** per consentire l'esecuzione asincrona per le funzioni correlate alla connessione.  
  
### <a name="code"></a>Codice  
  
```  
BOOL AsyncConnect (SQLHANDLE hdbc)   
{  
   SQLRETURN r;  
   SQLHANDLE hdbc;  
  
   // Enable asynchronous execution of connection functions.  
   // This must be executed synchronously, that is r != SQL_STILL_EXECUTING  
   r = SQLSetConnectAttr(  
         hdbc,   
         SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE,  
         reinterpret_cast<SQLPOINTER> (SQL_ASYNC_DBC_ENABLE_ON),  
         0);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   TCHAR szConnStrIn[256] = _T("DSN=AsyncDemo");  
  
   r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
  
   if (r == SQL_ERROR)   
   {  
      // Use SQLGetDiagRec to process the error.  
      // If SQLState is HY114, the driver does not support asynchronous execution.  
      return FALSE;  
   }  
  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion, with the same set of arguments.  
      r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   return TRUE;  
}  
  
```  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 In questo esempio vengono illustrate operazioni di commit asincrono. Operazioni di rollback possono essere eseguite anche in questo modo.  
  
### <a name="code"></a>Codice  
  
```  
BOOL AsyncCommit ()   
{  
   SQLRETURN r;   
  
   // Assume that SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE is SQL_ASYNC_DBC_ENABLE_ON.  
  
   r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion with the same set of arguments.  
      r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di istruzioni ODBC](../../../odbc/reference/develop-app/executing-statements-odbc.md)
