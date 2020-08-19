---
description: Esecuzione asincrona (metodo di polling)
title: Esecuzione asincrona (metodo di polling) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17199fb610f707c77a6610d34c8b1a5f0166de13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424853"
---
# <a name="asynchronous-execution-polling-method"></a>Esecuzione asincrona (metodo di polling)
Prima di ODBC 3,8 e Windows 7 SDK, le operazioni asincrone erano consentite solo su funzioni di istruzione. Per ulteriori informazioni, vedere l'articolo relativo alle **operazioni di esecuzione di istruzioni in modo asincrono**, più avanti in questo argomento.  
  
 ODBC 3,8 in Windows 7 SDK ha introdotto l'esecuzione asincrona sulle operazioni correlate alla connessione. Per ulteriori informazioni, vedere la sezione **esecuzione asincrona delle operazioni di connessione** , più avanti in questo argomento.  
  
 In Windows 7 SDK, per le operazioni di connessione o di istruzione asincrone, un'applicazione ha determinato che l'operazione asincrona è stata completata utilizzando il metodo di polling. A partire da Windows 8 SDK, è possibile determinare il completamento di un'operazione asincrona tramite il metodo di notifica. Per ulteriori informazioni, vedere [esecuzione asincrona (metodo di notifica)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
 Per impostazione predefinita, i driver eseguono le funzioni ODBC in modo sincrono; ovvero, l'applicazione chiama una funzione e il driver non restituisce il controllo all'applicazione fino a quando non termina l'esecuzione della funzione. Alcune funzioni, tuttavia, possono essere eseguite in modo asincrono. ovvero, l'applicazione chiama la funzione e il driver, dopo l'elaborazione minima, restituisce il controllo all'applicazione. L'applicazione può quindi chiamare altre funzioni mentre è ancora in esecuzione la prima funzione.  
  
 L'esecuzione asincrona è supportata per la maggior parte delle funzioni che vengono ampiamente eseguite sull'origine dati, ad esempio le funzioni per stabilire le connessioni, preparare ed eseguire istruzioni SQL, recuperare metadati, recuperare dati ed eseguire il commit delle transazioni. Risulta particolarmente utile quando l'attività eseguita nell'origine dati richiede molto tempo, ad esempio un processo di accesso o una query complessa su un database di grandi dimensioni.  
  
 Quando l'applicazione esegue una funzione con un'istruzione o una connessione abilitata per l'elaborazione asincrona, il driver esegue una quantità minima di elaborazione (ad esempio, controllando gli argomenti per gli errori), passa l'elaborazione all'origine dati e restituisce il controllo all'applicazione con il codice restituito SQL_STILL_EXECUTING. L'applicazione esegue quindi altre attività. Per determinare quando la funzione asincrona è stata completata, l'applicazione esegue il polling del driver a intervalli regolari chiamando la funzione con gli stessi argomenti usati originariamente. Se la funzione è ancora in esecuzione, restituisce SQL_STILL_EXECUTING; Se l'esecuzione è terminata, viene restituito il codice che sarebbe stato eseguito in modo sincrono, ad esempio SQL_SUCCESS, SQL_ERROR o SQL_NEED_DATA.  
  
 Se una funzione viene eseguita in modo sincrono o asincrono, è specifica del driver. Si supponga, ad esempio, che i metadati del set di risultati siano memorizzati nella cache del driver. In questo caso, è necessario molto tempo per eseguire **SQLDescribeCol** e il driver deve semplicemente eseguire la funzione anziché ritardare artificialmente l'esecuzione. D'altra parte, se il driver deve recuperare i metadati dall'origine dati, deve restituire il controllo all'applicazione mentre sta eseguendo questa operazione. Pertanto, l'applicazione deve essere in grado di gestire un codice restituito diverso da SQL_STILL_EXECUTING alla prima esecuzione di una funzione in modo asincrono.  
  
## <a name="executing-statement-operations-asynchronously"></a>Esecuzione di operazioni di istruzione in modo asincrono  
 Le funzioni di istruzione seguenti operano su un'origine dati e possono essere eseguite in modo asincrono:  

:::row:::
    :::column:::
        [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)  
        [SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)  
        [SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)  
        [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)  
        [SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)  
        [SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
        [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
        [SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)  
        [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)  
    :::column-end:::
    :::column:::
        [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
        [SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
        [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)  
        [SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
        [SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)  
        [SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)  
        [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
        [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)  
        [SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)  
    :::column-end:::
    :::column:::
        [SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
        [SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
        [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)  
        [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)  
        [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)  
        [SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)  
        [SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)  
        [SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
        [SQLTables](../../../odbc/reference/syntax/sqltables-function.md)  
    :::column-end:::
:::row-end:::

 L'esecuzione asincrona dell'istruzione viene controllata in base a un'istruzione o a una singola connessione, a seconda dell'origine dati. In altre parole, l'applicazione specifica che una particolare funzione deve essere eseguita in modo asincrono, ma che qualsiasi funzione eseguita su un'istruzione specifica deve essere eseguita in modo asincrono. Per scoprire quale è supportato, un'applicazione chiama [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) con un'opzione di SQL_ASYNC_MODE. Viene restituito SQL_AM_CONNECTION se è supportata l'esecuzione asincrona a livello di connessione (per un handle di istruzione). SQL_AM_STATEMENT se è supportata l'esecuzione asincrona a livello di istruzione.  
  
 Per specificare che le funzioni eseguite con un'istruzione specifica devono essere eseguite in modo asincrono, l'applicazione chiama **SQLSetStmtAttr** con l'attributo SQL_ATTR_ASYNC_ENABLE e la imposta su SQL_ASYNC_ENABLE_ON. Se è supportata l'elaborazione asincrona a livello di connessione, l'attributo dell'istruzione SQL_ATTR_ASYNC_ENABLE è di sola lettura e il relativo valore corrisponde all'attributo Connection della connessione in cui è stata allocata l'istruzione. È specifico del driver se il valore dell'attributo dell'istruzione viene impostato in fase di allocazione dell'istruzione o in un secondo momento. Il tentativo di impostare la funzione restituirà SQL_ERROR e SQLSTATE HYC00 (funzionalità facoltativa non implementata).  
  
 Per specificare che le funzioni eseguite con una connessione specifica devono essere eseguite in modo asincrono, l'applicazione chiama **SQLSetConnectAttr** con l'attributo SQL_ATTR_ASYNC_ENABLE e la imposta su SQL_ASYNC_ENABLE_ON. Tutti gli handle di istruzione futuri allocati nella connessione verranno abilitati per l'esecuzione asincrona. viene definito dal driver se gli handle di istruzione esistenti verranno abilitati da questa azione. Se SQL_ATTR_ASYNC_ENABLE è impostato su SQL_ASYNC_ENABLE_OFF, tutte le istruzioni sulla connessione sono in modalità sincrona. Viene restituito un errore se l'esecuzione asincrona è abilitata mentre è presente un'istruzione attiva sulla connessione.  
  
 Per determinare il numero massimo di istruzioni attive simultanee in modalità asincrona che il driver è in grado di supportare in una determinata connessione, l'applicazione chiama **SQLGetInfo** con l'opzione SQL_MAX_ASYNC_CONCURRENT_STATEMENTS.  
  
 Il codice seguente illustra il funzionamento del modello di polling:  
  
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
  
 Mentre una funzione viene eseguita in modo asincrono, l'applicazione può chiamare funzioni su qualsiasi altra istruzione. L'applicazione può anche chiamare funzioni su qualsiasi connessione, ad eccezione di quella associata all'istruzione asincrona. Tuttavia, l'applicazione può chiamare solo la funzione originale e le funzioni seguenti (con l'handle dell'istruzione o la connessione associata, handle di ambiente), dopo che un'operazione di istruzione restituisce SQL_STILL_EXECUTING:  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) (nell'handle dell'istruzione)  
  
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
  
 Se l'applicazione chiama qualsiasi altra funzione con l'istruzione asincrona o con la connessione associata a tale istruzione, la funzione restituisce SQLSTATE HY010 (Error Sequence Function), ad esempio.  
  
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
  
 Quando un'applicazione chiama una funzione per determinare se è ancora in esecuzione in modo asincrono, deve utilizzare l'handle di istruzione originale. Questo perché l'esecuzione asincrona viene rilevata in base all'istruzione. L'applicazione deve inoltre fornire valori validi per gli altri argomenti. gli argomenti originali eseguiranno questa operazione per ottenere il controllo degli errori passato in Gestione driver. Tuttavia, dopo che il driver controlla l'handle dell'istruzione e determina che l'istruzione viene eseguita in modo asincrono, ignora tutti gli altri argomenti.  
  
 Mentre una funzione viene eseguita in modo asincrono, ovvero dopo che ha restituito SQL_STILL_EXECUTING e prima di restituire un codice diverso, l'applicazione può annullarla chiamando **SQLCancel** o **SQLCancelHandle** con lo stesso handle di istruzione. Questa operazione non è garantita per annullare l'esecuzione della funzione. Ad esempio, è possibile che la funzione sia già stata completata. Inoltre, il codice restituito da **SQLCancel** o **SQLCancelHandle** indica solo se il tentativo di annullamento della funzione ha avuto esito positivo, non se la funzione è stata effettivamente annullata. Per determinare se la funzione è stata annullata, l'applicazione chiama di nuovo la funzione. Se la funzione è stata annullata, restituisce SQL_ERROR e SQLSTATE HY008 (operazione annullata). Se la funzione non è stata annullata, restituisce un altro codice, ad esempio SQL_SUCCESS, SQL_STILL_EXECUTING o SQL_ERROR con un valore SQLSTATE diverso.  
  
 Per disabilitare l'esecuzione asincrona di un'istruzione specifica quando il driver supporta l'elaborazione asincrona a livello di istruzione, l'applicazione chiama **SQLSetStmtAttr** con l'attributo SQL_ATTR_ASYNC_ENABLE e la imposta su SQL_ASYNC_ENABLE_OFF. Se il driver supporta l'elaborazione asincrona a livello di connessione, l'applicazione chiama **SQLSetConnectAttr** per impostare SQL_ATTR_ASYNC_ENABLE su SQL_ASYNC_ENABLE_OFF, che disabilita l'esecuzione asincrona di tutte le istruzioni nella connessione.  
  
 L'applicazione deve elaborare i record di diagnostica nel ciclo ripetuto della funzione originale. Se viene chiamato **SQLGetDiagField** o **SQLGetDiagRec** durante l'esecuzione di una funzione asincrona, viene restituito l'elenco corrente dei record di diagnostica. Ogni volta che viene ripetuta la chiamata di funzione originale, cancella i record di diagnostica precedenti.  
  
## <a name="executing-connection-operations-asynchronously"></a>Esecuzione di operazioni di connessione in modo asincrono  
 Prima di ODBC 3,8, era consentita l'esecuzione asincrona per operazioni correlate alle istruzioni, ad esempio preparazione, esecuzione e recupero, nonché per le operazioni sui metadati del catalogo. A partire da ODBC 3,8, è possibile eseguire un'esecuzione asincrona anche per le operazioni correlate alla connessione, ad esempio Connect, Disconnect, commit e rollback.  
  
 Per ulteriori informazioni su ODBC 3,8, vedere Novità [di odbc 3,8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
 L'esecuzione di operazioni di connessione in modo asincrono è utile negli scenari seguenti:  
  
-   Quando un numero ridotto di thread gestisce un numero elevato di dispositivi con tassi di dati molto elevati. Per ottimizzare la velocità di risposta e la scalabilità, è consigliabile che tutte le operazioni siano asincrone.  
  
-   Quando si desidera sovrapporre le operazioni di database su più connessioni per ridurre i tempi di trasferimento trascorsi.  
  
-   Le chiamate ODBC asincrone efficienti e la possibilità di annullare le operazioni di connessione consentono a un'applicazione di annullare qualsiasi operazione lenta senza dover attendere il timeout.  
  
 Le funzioni seguenti, che operano sugli handle di connessione, possono ora essere eseguite in modo asincrono:  

:::row:::
    :::column:::
        [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)  
        [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)  
    :::column-end:::
    :::column:::
        [SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)  
        [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
    :::column-end:::
    :::column:::
        [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)  
        [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
    :::column-end:::
:::row-end:::

 Per determinare se un driver supporta operazioni asincrone su queste funzioni, un'applicazione chiama **SQLGetInfo** con SQL_ASYNC_DBC_FUNCTIONS. Se sono supportate le operazioni asincrone, viene restituito SQL_ASYNC_DBC_CAPABLE. Viene restituito SQL_ASYNC_DBC_NOT_CAPABLE se le operazioni asincrone non sono supportate.  
  
 Per specificare che le funzioni eseguite con una connessione specifica devono essere eseguite in modo asincrono, l'applicazione chiama **SQLSetConnectAttr** e imposta l'attributo SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE su SQL_ASYNC_DBC_ENABLE_ON. L'impostazione di un attributo di connessione prima di stabilire una connessione viene sempre eseguita in modo sincrono. Inoltre, l'operazione di impostazione dell'attributo di connessione SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE con **SQLSetConnectAttr** viene sempre eseguita in modo sincrono.  
  
 Un'applicazione può abilitare l'operazione asincrona prima di effettuare una connessione. Poiché Gestione driver non è in grado di determinare quale driver utilizzare prima di effettuare una connessione, gestione driver restituirà sempre l'esito positivo in **SQLSetConnectAttr**. Tuttavia, potrebbe non riuscire a connettersi se il driver ODBC non supporta le operazioni asincrone.  
  
 In generale, può essere presente al massimo una funzione in esecuzione asincrona associata a un handle di connessione o un handle di istruzione specifico. Un handle di connessione può tuttavia avere più di un handle di istruzione associato. Se non è stata eseguita alcuna operazione asincrona sull'handle di connessione, un handle di istruzione associato può eseguire un'operazione asincrona. Analogamente, è possibile disporre di un'operazione asincrona su un handle di connessione se non sono in corso operazioni asincrone su un handle di istruzione associato. Un tentativo di eseguire un'operazione asincrona utilizzando un handle che esegue un'operazione asincrona restituirà HY010, "errore della sequenza di funzioni".  
  
 Se un'operazione di connessione restituisce SQL_STILL_EXECUTING, un'applicazione può chiamare solo la funzione originale e le funzioni seguenti per tale handle di connessione:  
  
-   **SQLCancelHandle** (nell'handle di connessione)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (allocazione di ENV/DBC)  
  
-   **SQLAllocHandleStd** (allocazione di ENV/DBC)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 L'applicazione deve elaborare i record di diagnostica nel ciclo ripetuto della funzione originale. Se viene chiamato SQLGetDiagField o SQLGetDiagRec durante l'esecuzione di una funzione asincrona, viene restituito l'elenco corrente dei record di diagnostica. Ogni volta che viene ripetuta la chiamata di funzione originale, cancella i record di diagnostica precedenti.  
  
 Se una connessione viene aperta o chiusa in modo asincrono, l'operazione viene completata quando l'applicazione riceve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO nella chiamata di funzione originale.  
  
 È stata aggiunta una nuova funzione a ODBC 3,8, **SQLCancelHandle**. Questa funzione Annulla le sei funzioni di connessione (**SQLBrowseConnect**, **SQLConnect**, **Disconnect**, **SQLDriverConnect**, **SQLEndTran**e **SQLSetConnectAttr**). Un'applicazione deve chiamare **SQLGetFunctions** per determinare se il driver supporta **SQLCancelHandle**. Come per **SQLCancel**, se **SQLCancelHandle** restituisce Success, non significa che l'operazione è stata annullata. Per determinare se l'operazione è stata annullata, un'applicazione deve chiamare nuovamente la funzione originale. **SQLCancelHandle** consente di annullare le operazioni asincrone sugli handle di connessione o sugli handle di istruzione. L'utilizzo di **SQLCancelHandle** per annullare un'operazione in un handle di istruzione equivale alla chiamata a **SQLCancel**.  
  
 Non è necessario supportare contemporaneamente le operazioni di connessione **SQLCancelHandle** e asincrona. Un driver può supportare le operazioni di connessione asincrone, ma non **SQLCancelHandle**, o viceversa.  
  
 Le operazioni di connessione asincrona e **SQLCancelHandle** possono inoltre essere utilizzate dalle applicazioni ODBC 3. x e ODBC 2. x con un driver ODBC 3,8 e gestione driver ODBC 3,8. Per informazioni su come consentire a un'applicazione precedente di utilizzare le nuove funzionalità nella versione ODBC successiva, vedere [Compatibility Matrix](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
### <a name="connection-pooling"></a>Pool di connessioni  
 Quando il pool di connessioni è abilitato, le operazioni asincrone sono supportate solo in modo minimo per stabilire una connessione (con **SQLConnect** e **SQLDriverConnect**) e la chiusura di una connessione con **SqlConnection**. Tuttavia, un'applicazione deve comunque essere in grado di gestire la SQL_STILL_EXECUTING valore restituito da **SQLConnect**, **SQLDriverConnect**e **Disconnect**.  
  
 Quando il pool di connessioni è abilitato, **SQLEndTran** e **SQLSetConnectAttr** sono supportati per le operazioni asincrone.  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente viene illustrato come utilizzare **SQLSetConnectAttr** per abilitare l'esecuzione asincrona per le funzioni correlate alla connessione.  
  
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
 In questo esempio vengono illustrate le operazioni di commit asincrono. Anche le operazioni di rollback possono essere eseguite in questo modo.  
  
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
