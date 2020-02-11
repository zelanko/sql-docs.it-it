---
title: Esecuzione asincrona (metodo di notifica) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e509dad9-5263-4a10-9a4e-03b84b66b6b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 66b806b698164b306eee4dc7d4c48fbe7835adae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077057"
---
# <a name="asynchronous-execution-notification-method"></a>Esecuzione asincrona (metodo di notifica)
ODBC consente l'esecuzione asincrona di operazioni di connessione e istruzioni. Un thread dell'applicazione può chiamare una funzione ODBC in modalità asincrona e la funzione può restituire prima del completamento dell'operazione, consentendo al thread dell'applicazione di eseguire altre attività. In Windows 7 SDK, per le operazioni di connessione o di istruzione asincrone, un'applicazione ha determinato che l'operazione asincrona è stata completata utilizzando il metodo di polling. Per ulteriori informazioni, vedere [esecuzione asincrona (metodo di polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). A partire da Windows 8 SDK, è possibile determinare il completamento di un'operazione asincrona tramite il metodo di notifica.  
  
 Nel metodo di polling, le applicazioni devono chiamare la funzione asincrona ogni volta che desidera lo stato dell'operazione. Il metodo di notifica è simile a callback e attendi in ADO.NET. ODBC, tuttavia, utilizza gli eventi Win32 come oggetto notifica.  
  
 Non è possibile utilizzare contemporaneamente la libreria di cursori ODBC e la notifica asincrona ODBC. L'impostazione di entrambi gli attributi restituirà un errore con SQLSTATE S1119 (la libreria di cursori e la notifica asincrona non possono essere abilitati contemporaneamente).  
  
 Per informazioni sugli sviluppatori di driver, vedere [notifica del completamento della funzione asincrona](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md) .  
  
> [!NOTE]  
>  Il metodo di notifica non è supportato con la libreria di cursori. Un'applicazione riceverà un messaggio di errore se tenta di abilitare la libreria di cursori tramite SQLSetConnectAttr, quando il metodo di notifica è abilitato.  
  
## <a name="overview"></a>Panoramica  
 Quando una funzione ODBC viene chiamata in modalità asincrona, il controllo viene restituito immediatamente all'applicazione chiamante con il codice restituito SQL_STILL_EXECUTING. L'applicazione deve eseguire ripetutamente il polling della funzione fino a quando non viene restituito un valore diverso da SQL_STILL_EXECUTING. Il ciclo di polling aumenta l'utilizzo della CPU, causando scarse prestazioni in molti scenari asincroni.  
  
 Ogni volta che viene usato il modello di notifica, il modello di polling è disabilitato. Le applicazioni non devono chiamare nuovamente la funzione originale. Chiamare la [funzione SQLCompleteAsync](../../../odbc/reference/syntax/sqlcompleteasync-function.md) per completare l'operazione asincrona. Se un'applicazione chiama di nuovo la funzione originale prima del completamento dell'operazione asincrona, la chiamata restituirà SQL_ERROR con SQLSTATE IM017 (il polling è disabilitato in modalità di notifica asincrona).  
  
 Quando si utilizza il modello di notifica, l'applicazione può chiamare **SQLCancel** o **SQLCancelHandle** per annullare un'istruzione o un'operazione di connessione. Se la richiesta di annullamento ha esito positivo, ODBC restituirà SQL_SUCCESS. Questo messaggio non indica che la funzione è stata effettivamente annullata; indica che la richiesta di annullamento è stata elaborata. Indica se la funzione è effettivamente annullata, dipendente dal driver e dipendente dall'origine dati. Quando un'operazione viene annullata, l'evento viene comunque segnalato da Gestione driver. Gestione driver restituisce SQL_ERROR nel buffer del codice restituito e lo stato è SQLSTATE HY008 (operazione annullata) per indicare che l'annullamento è stato eseguito correttamente. Se la funzione ha completato la normale elaborazione, gestione driver restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
### <a name="downlevel-behavior"></a>Comportamento di livello inferiore  
 La versione di gestione driver ODBC che supporta la notifica completata è ODBC 3,81.  
  
|Versione ODBC applicazione|Versione di gestione driver|Versione driver|Comportamento|  
|------------------------------|----------------------------|--------------------|--------------|  
|Nuova applicazione di qualsiasi versione ODBC|ODBC 3,81|Driver ODBC 3,80|L'applicazione può utilizzare questa funzionalità se il driver supporta questa funzionalità. in caso contrario, la gestione driver si errori.|  
|Nuova applicazione di qualsiasi versione ODBC|ODBC 3,81|Driver pre-ODBC 3,80|Se il driver non supporta questa funzionalità, gestione driver restituirà un errore.|  
|Nuova applicazione di qualsiasi versione ODBC|Pre-ODBC 3,81|Qualsiasi|Quando l'applicazione utilizza questa funzionalità, una vecchia gestione driver prenderà in considerazione i nuovi attributi come attributi specifici del driver e il driver dovrebbe essere in errore. Un nuovo gestore di driver non passerà questi attributi al driver.|  
  
 Prima di utilizzare questa funzionalità, è necessario che in un'applicazione venga verificata la versione di gestione driver. In caso contrario, se un driver scritto male non viene eliminato e la versione di gestione driver è precedente a ODBC 3,81, il comportamento non è definito.  
  
## <a name="use-cases"></a>Casi di utilizzo  
 In questa sezione vengono illustrati i casi di utilizzo per l'esecuzione asincrona e il meccanismo di polling.  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>Integrazione di dati da più origini ODBC  
 Un'applicazione di integrazione dei dati recupera in modo asincrono i dati da più origini dati. Alcuni dati sono provenienti da origini dati remote e alcuni dati appartengono a file locali. L'applicazione non può continuare fino al completamento delle operazioni asincrone.  
  
 Anziché eseguire ripetutamente il polling di un'operazione per determinare se è completa, l'applicazione può creare un oggetto evento e associarlo a un handle di connessione ODBC o a un handle di istruzione ODBC. L'applicazione chiama quindi le API di sincronizzazione del sistema operativo per attendere un oggetto evento o molti oggetti evento (eventi ODBC e altri eventi Windows). L'oggetto evento verrà segnalato da ODBC quando viene completata l'operazione asincrona ODBC corrispondente.  
  
 In Windows, verranno utilizzati gli oggetti evento Win32 e che forniranno all'utente un modello di programmazione unificato. I gestori di driver su altre piattaforme possono utilizzare l'implementazione dell'oggetto evento specifico di tali piattaforme.  
  
 Nell'esempio di codice seguente viene illustrato l'utilizzo della notifica asincrona di connessione e di istruzione:  
  
```  
// This function opens NUMBER_OPERATIONS connections and executes one query on statement of each connection.  
// Asynchronous Notification is used  
  
#define NUMBER_OPERATIONS 5  
int AsyncNotificationSample(void)  
{  
    RETCODE     rc;  
  
    SQLHENV     hEnv              = NULL;  
    SQLHDBC     arhDbc[NUMBER_OPERATIONS]         = {NULL};  
    SQLHSTMT    arhStmt[NUMBER_OPERATIONS]        = {NULL};  
  
    HANDLE      arhDBCEvent[NUMBER_OPERATIONS]    = {NULL};  
    RETCODE     arrcDBC[NUMBER_OPERATIONS]        = {0};  
    HANDLE      arhSTMTEvent[NUMBER_OPERATIONS]   = {NULL};  
    RETCODE     arrcSTMT[NUMBER_OPERATIONS]       = {0};  
  
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &hEnv);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    rc = SQLSetEnvAttr(hEnv,  
        SQL_ATTR_ODBC_VERSION,  
        (SQLPOINTER) SQL_OV_ODBC3_80,  
        SQL_IS_INTEGER);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    // Connection operations begin here  
  
    // Alloc NUMBER_OPERATIONS connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_DBC, hEnv, &arhDbc[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable DBC Async on all connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE, (SQLPOINTER)SQL_ASYNC_DBC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Application must create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhDBCEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhDBCEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all connection handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_EVENT, arhDBCEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate connect establishing  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLDriverConnect(arhDbc[i], NULL, (SQLTCHAR*)TEXT("Driver={ODBC Driver 11 for SQL Server};SERVER=dp-srv-sql2k;DATABASE=pubs;UID=sa;PWD=XYZ;"), SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE); // Wait All  
  
    // Complete connect API calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], & arrcDBC[i]);  
    }  
  
    BOOL fFail = FALSE; // Whether some connection openning fails.  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcDBC[i]) )   
            fFail = TRUE;  
    }  
  
    // If some SQLDriverConnect() fail, clean up.  
    if (fFail)  
    {  
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {  
                SQLDisconnect(arhDbc[i]); // This is also async  
            }  
            else  
            {  
                SetEvent(arhDBCEvent[i]); // Previous SQLDriverConnect() failed. No need to call SQLDisconnect().  
            }  
        }  
        WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE);   
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {     
                SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], &arrcDBC[i]);; // To Complete  
            }  
        }  
  
        goto Cleanup;  
    }  
  
    // Statement Operations begin here  
  
    // Alloc statement handle  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_STMT, arhDbc[i], &arhStmt[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable STMT Async on all statement handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_ENABLE, (SQLPOINTER)SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhSTMTEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhSTMTEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all statement handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_STMT_EVENT, arhSTMTEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate SQLExecDirect() calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLExecDirect(arhStmt[i], (SQLTCHAR*)TEXT("select au_lname, au_fname from authors"), SQL_NTS);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE); // Wait All  
  
    // Now, call SQLCompleteAsync to complete the operation and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return values  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        //Do some binding jobs here, set SQL_ATTR_ROW_ARRAY_SIZE   
    }  
  
    // Now, initiate fetching  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLFetch(arhStmt[i]);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE);   
  
    // Now, to complete the operations and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    // USE fetched data here!!  
  
Cleanup:  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhStmt[NUMBER_OPERATIONS])  
        {  
            SQLFreeHandle(SQL_HANDLE_STMT, arhStmt[i]);  
            arhStmt[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhSTMTEvent[i])  
        {  
            CloseHandle(arhSTMTEvent[i]);  
            arhSTMTEvent[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDbc[i])  
        {  
            SQLFreeHandle(SQL_HANDLE_DBC, arhDbc[i]);  
            arhDbc[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDBCEvent[i])  
        {  
            CloseHandle(arhDBCEvent[i]);  
            arhDBCEvent[i] = NULL;  
        }  
    }  
  
    if (hEnv)  
    {  
        SQLFreeHandle(SQL_HANDLE_ENV, hEnv);  
        hEnv = NULL;  
    }  
  
    return 0;  
}  
  
```  
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>Determinare se un driver supporta la notifica asincrona  
 Un'applicazione ODBC può determinare se un driver ODBC supporta la notifica asincrona chiamando [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md). Gestione driver ODBC chiamerà di conseguenza il **SQLGetInfo** del driver con SQL_ASYNC_NOTIFICATION.  
  
```  
SQLUINTEGER InfoValue;  
SQLLEN      cbInfoLength;  
  
SQLRETURN retcode;  
retcode = SQLGetInfo (hDbc,   
                      SQL_ASYNC_NOTIFICATION,   
                      &InfoValue,  
                      sizeof(InfoValue),  
                      NULL);  
if (SQL_SUCCEEDED(retcode))  
{  
if (SQL_ASYNC_NOTIFICATION_CAPABLE == InfoValue)  
      {  
          // The driver supports asynchronous notification  
      }  
      else if (SQL_ASYNC_NOTIFICATION_NOT_CAPABLE == InfoValue)  
      {  
          // The driver does not support asynchronous notification  
      }  
}  
```  
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>Associazione di un handle di evento Win32 a un handle ODBC  
 Le applicazioni sono responsabili della creazione di oggetti evento Win32 utilizzando le corrispondenti funzioni Win32. Un'applicazione può associare un handle di evento Win32 a un handle di connessione ODBC o un handle di istruzione ODBC.  
  
 Gli attributi di connessione SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE e SQL_ATTR_ASYNC_DBC_EVENT determinare se ODBC viene eseguito in modalità asincrona e se ODBC Abilita la modalità di notifica per un handle di connessione. Gli attributi di istruzione SQL_ATTR_ASYNC_ENABLE e SQL_ATTR_ASYNC_STMT_EVENT determinare se ODBC viene eseguito in modalità asincrona e se ODBC Abilita la modalità di notifica per un handle di istruzione.  
  
|SQL_ATTR_ASYNC_ENABLE o SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT o SQL_ATTR_ASYNC_DBC_EVENT|Mode|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|Abilitare|non null|Notifica asincrona|  
|Abilitare|Null|Polling asincrono|  
|Disabilitazione|qualsiasi|Sincrono|  
  
 Un'applicazione può disabilitare temporaneamente la modalità operativa asincrona. ODBC ignora i valori di SQL_ATTR_ASYNC_DBC_EVENT se l'operazione asincrona a livello di connessione è disabilitata. ODBC ignora i valori di SQL_ATTR_ASYNC_STMT_EVENT se l'operazione asincrona a livello di istruzione è disabilitata.  
  
 Chiamata sincrona di **SQLSetStmtAttr** e **SQLSetConnectAttr**  
 -   **SQLSetConnectAttr** supporta le operazioni asincrone, ma la chiamata di **sqlsetconnectattr** per impostare SQL_ATTR_ASYNC_DBC_EVENT è sempre sincrona.  
  
-   **SQLSetStmtAttr** non supporta l'esecuzione asincrona.  
  
 Scenario di errore  
 Quando **SQLSetConnectAttr** viene chiamato prima di stabilire una connessione, gestione driver non è in grado di determinare quale driver utilizzare. Pertanto, gestione driver restituisce l'esito positivo per **SQLSetConnectAttr** , ma è possibile che l'attributo non sia pronto per l'impostazione nel driver. Questi attributi vengono impostati da Gestione driver quando l'applicazione chiama una funzione di connessione. Gestione driver potrebbe essere in errore perché il driver non supporta le operazioni asincrone.  
  
 Ereditarietà degli attributi di connessione  
 In genere, le istruzioni di una connessione erediteranno gli attributi di connessione. Tuttavia, l'attributo SQL_ATTR_ASYNC_DBC_EVENT non è ereditabile e influiscono solo sulle operazioni di connessione.  
  
 Per associare un handle di evento a un handle di connessione ODBC, un'applicazione ODBC chiama l'API ODBC **SQLSetConnectAttr** e specifica SQL_ATTR_ASYNC_DBC_EVENT come attributo e l'handle di evento come valore dell'attributo. Il nuovo attributo ODBC SQL_ATTR_ASYNC_DBC_EVENT è di tipo SQL_IS_POINTER.  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 In genere, le applicazioni creano oggetti evento di reimpostazione automatica. L'oggetto evento non viene reimpostato da ODBC. Le applicazioni devono verificare che l'oggetto non sia in stato segnalato prima di chiamare qualsiasi funzione ODBC asincrona.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT è un attributo di solo Gestione driver che non verrà impostato nel driver.  
  
 Il valore predefinito di SQL_ATTR_ASYNC_DBC_EVENT è NULL. Se il driver non supporta le notifiche asincrone, il recupero o l'impostazione di SQL_ATTR_ASYNC_DBC_EVENT restituirà SQL_ERROR con SQLSTATE HY092 (identificatore di opzione/attributo non valido).  
  
 Se l'ultimo valore di SQL_ATTR_ASYNC_DBC_EVENT impostato su un handle di connessione ODBC non è NULL e l'applicazione Abilita la modalità asincrona impostando l'attributo SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE con SQL_ASYNC_DBC_ENABLE_ON, chiamando qualsiasi connessione ODBC la funzione che supporta la modalità asincrona riceve una notifica di completamento. Se l'ultimo valore SQL_ATTR_ASYNC_DBC_EVENT impostato su un handle di connessione ODBC è NULL, ODBC non invierà l'applicazione a nessuna notifica, indipendentemente dal fatto che sia abilitata la modalità asincrona.  
  
 Un'applicazione può impostare SQL_ATTR_ASYNC_DBC_EVENT prima o dopo l'impostazione dell'attributo SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE.  
  
 Le applicazioni possono impostare l'attributo SQL_ATTR_ASYNC_DBC_EVENT in un handle di connessione ODBC prima di chiamare una funzione di connessione (**SQLConnect**, **SQLBrowseConnect**o **SQLDriverConnect**). Poiché Gestione driver ODBC non sa quale driver ODBC verrà usato dall'applicazione, restituirà SQL_SUCCESS. Quando l'applicazione chiama una funzione di connessione, gestione driver ODBC verificherà se il driver supporta la notifica asincrona. Se il driver non supporta la notifica asincrona, gestione driver ODBC restituirà SQL_ERROR con SQLSTATE S1_118 (il driver non supporta la notifica asincrona). Se il driver supporta la notifica asincrona, gestione driver ODBC chiamerà il driver e imposterà gli attributi corrispondenti SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK e SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT.  
  
 Analogamente, un'applicazione chiama **SQLSetStmtAttr** in un handle di istruzione ODBC e specifica l'attributo SQL_ATTR_ASYNC_STMT_EVENT per abilitare o disabilitare la notifica asincrona a livello di istruzione. Poiché una funzione di istruzione viene sempre chiamata dopo che è stata stabilita la connessione, **SQLSetStmtAttr** restituirà SQL_ERROR con SQLSTATE S1_118 (il driver non supporta la notifica asincrona) immediatamente se il driver corrispondente non supporta le operazioni asincrone oppure il driver supporta l'operazione asincrona ma non supporta la notifica asincrona.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 SQL_ATTR_ASYNC_STMT_EVENT, che può essere impostato su NULL, è un attributo di solo Gestione driver che non verrà impostato nel driver.  
  
 Il valore predefinito di SQL_ATTR_ASYNC_STMT_EVENT è NULL. Se il driver non supporta la notifica asincrona, ottenere o impostare l'attributo SQL_ATTR_ASYNC_ STMT_EVENT restituirà SQL_ERROR con SQLSTATE HY092 (identificatore di opzione/attributo non valido).  
  
 Un'applicazione non deve associare lo stesso handle di evento a più di un handle ODBC. In caso contrario, una notifica andrà persa se due chiamate di funzione ODBC asincrone vengono completate su due handle che condividono lo stesso handle di evento. Per evitare che un handle di istruzione erediti lo stesso handle di evento dall'handle di connessione, ODBC restituisce SQL_ERROR con SQLSTATE IM016 (Impossibile impostare l'attributo dell'istruzione nell'handle di connessione) se un'applicazione imposta SQL_ATTR_ASYNC_STMT_EVENT per un handle di connessione.  
  
### <a name="calling-asynchronous-odbc-functions"></a>Chiamata di funzioni ODBC asincrone  
 Dopo l'abilitazione della notifica asincrona e l'avvio di un'operazione asincrona, l'applicazione può chiamare qualsiasi funzione ODBC. Se la funzione appartiene al set di funzioni che supportano l'operazione asincrona, l'applicazione riceverà una notifica di completamento al termine dell'operazione, indipendentemente dal fatto che la funzione abbia avuto esito positivo o negativo.  L'unica eccezione è che l'applicazione chiama una funzione ODBC con una connessione o un handle di istruzione non valido. In questo caso, ODBC non otterrà l'handle di evento e lo imposterà sullo stato segnalato.  
  
 L'applicazione deve garantire che l'oggetto evento associato si trovi in uno stato non segnalato prima di avviare un'operazione asincrona sull'handle ODBC corrispondente. L'oggetto evento non viene reimpostato da ODBC.  
  
### <a name="getting-notification-from-odbc"></a>Recupero di notifiche da ODBC  
 Un thread dell'applicazione può chiamare **WaitForSingleObject** per attendere un handle di evento o chiamare **WaitForMultipleObjects** per attendere una matrice di handle di eventi e rimanere sospesi fino a quando uno o tutti gli oggetti evento non vengono segnalati o non è trascorso l'intervallo di timeout.  
  
```  
DWORD dwStatus = WaitForSingleObject(  
                        hEvent,  // The event associated with the ODBC handle  
                        5000     // timeout is 5000 millisecond   
);  
  
If (dwStatus == WAIT_TIMEOUT)  
{  
    // time-out interval elapsed before all the events are signaled.   
}  
Else  
{  
    // Call the corresponding Asynchronous ODBC API to complete all processing and retrieve the return code.  
}  
```
