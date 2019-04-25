---
title: Funzione SQLAllocHandle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0a075b96e7a29cef4a10f034147732bf03f64b2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62761772"
---
# <a name="sqlallochandle-function"></a>Funzione SQLAllocHandle
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLAllocHandle** alloca un handle di ambiente, connessione, istruzione o descrittore.  
  
> [!NOTE]  
>  Questa funzione è una funzione generica per l'allocazione di handle che sostituisce le funzioni ODBC 2.0 **SQLAllocConnect**, **SQLAllocEnv**, e **SQLAllocStmt**. Per consentire le applicazioni che chiamano **SQLAllocHandle** per lavorare con l'API ODBC 2. *x* driver, una chiamata a **SQLAllocHandle** viene eseguito il mapping a in Gestione Driver **SQLAllocConnect**, **SQLAllocEnv**, o  **SQLAllocStmt**, nel modo appropriato. Per altre informazioni, vedere "Commenti". Per altre informazioni su quali il Driver Manager esegue il mapping a questa funzione quando un'applicazione ODBC 3. *x* applicazione funziona con un'API ODBC 2. *x* driver, vedere [Mapping di funzioni di sostituzione per la compatibilità con le versioni precedenti di applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *HandleType*  
 [Input] Il tipo di handle deve essere allocata dal **SQLAllocHandle**. Deve essere uno dei valori seguenti:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Handle SQL_HANDLE_DBC_INFO_TOKEN è utilizzato solo da Gestione Driver e del driver. Le applicazioni non devono usare questo tipo di handle. Per altre informazioni sulle SQL_HANDLE_DBC_INFO_TOKEN, vedere [lo sviluppo di riconoscimento dei Pool di connessioni in un Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *InputHandle*  
 [Input] L'handle di input nel cui contesto è necessario allocare il nuovo handle. Se *HandleType* è SQL_HANDLE_ENV, si tratta di SQL_NULL_HANDLE. Se *HandleType* è SQL_HANDLE_DBC, deve trattarsi di un handle di ambiente e se è SQL_HANDLE_STMT o SQL_HANDLE_DESC, deve essere un handle di connessione.  
  
 *OutputHandlePtr*  
 [Output] Puntatore a un buffer in cui restituire l'handle per la struttura di dati appena allocato.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE o SQL_ERROR.  
  
 Quando si alloca un handle diverso da un handle di ambiente, se **SQLAllocHandle** restituisce SQL_ERROR, imposta *OutputHandlePtr* SQL_NULL_HDBC, SQL_NULL_HSTMT o SQL_NULL_HDESC, a seconda di valore del *HandleType*, a meno che l'argomento di output è un puntatore null. L'applicazione può quindi ottenere informazioni aggiuntive dalla struttura di dati di diagnostica associata al punto nel *InputHandle* argomento.  
  
## <a name="environment-handle-allocation-errors"></a>Errori di allocazione di Handle di ambiente  
 Allocazione di ambiente si verifica all'interno di gestione Driver sia all'interno di ogni driver. L'errore restituito da **SQLAllocHandle** con un *HandleType* SQL_HANDLE_ENV dipende dal livello in cui si è verificato l'errore.  
  
 Se Gestione Driver non è possibile allocare memoria per  *\*OutputHandlePtr* quando **SQLAllocHandle** con un *HandleType* SQL_HANDLE_ENV viene chiamato, o l'applicazione fornisce un puntatore null per *OutputHandlePtr*, **SQLAllocHandle** restituisce SQL_ERROR. Gestione Driver imposta **OutputHandlePtr* a SQL_NULL_HENV (a meno che l'applicazione è specificato un puntatore null, che restituisce SQL_ERROR). Non c'è alcun handle al quale associare informazioni diagnostiche aggiuntive.  
  
 Gestione Driver non chiama la funzione di allocazione di handle di ambiente a livello di driver finché l'applicazione chiama **SQLConnect**, **SQLBrowseConnect**, o **SQLDriverConnect**. Se si verifica un errore a livello di driver **SQLAllocHandle** (funzione), quindi il livello di gestione Driver **SQLConnect**, **SQLBrowseConnect**, o  **SQLDriverConnect** funzione restituisce SQL_ERROR. La struttura di dati di diagnostica contiene SQLSTATE IM004 (patente **SQLAllocHandle** non riuscita). Viene restituito l'errore su un handle di connessione.  
  
 Per altre informazioni sul flusso di chiamate di funzione tra il gestore di Driver e un driver, vedere [funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLAllocHandle** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con l'appropriato *HandleType* e *gestire* impostato sul valore di *InputHandle*. SQL_SUCCESS_WITH_INFO (ma non da SQL_ERROR) possono essere restituite per il *OutputHandle* argomento. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLAllocHandle** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08003|Connessione non aperta|(DM) il *HandleType* argomento era SQL_HANDLE_STMT o SQL_HANDLE_DESC, ma la connessione specificata per il *InputHandle* argomento non è aperta. Il processo di connessione deve essere completato (e la connessione deve essere aperta) per il driver ad allocare un'istruzione o un descrittore di handle.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel **MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|(DM) The Driver Manager: Impossibile allocare memoria per l'handle specificato.<br /><br /> Il driver non è riuscito ad allocare memoria per l'handle specificato.|  
|HY009|Utilizzo non valido del puntatore null|(DM) di *OutputHandlePtr* argomento era un puntatore null.|  
|HY010|Errore nella sequenza della funzione|(DM) di *HandleType* argomento era SQL_HANDLE_DBC, e **SQLSetEnvAttr** non è stato chiamato per impostare l'attributo di ambiente SQL_ODBC_VERSION.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione la **InputHandle** ed era ancora in esecuzione quando il **SQLAllocHandle** funzione è stata chiamata con **HandleType** impostata SQL_HANDLE_STMT o SQL_HANDLE_DESC.|  
|HY013|Errore di gestione della memoria|Il *HandleType* argomento era SQL_HANDLE_DBC, SQL_HANDLE_STMT o SQL_HANDLE_DESC; e la chiamata di funzione non è stata elaborata perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di memoria insufficiente condizioni.|  
|HY014|Limita il numero di handle superato|Il limite definito dal driver per il numero di handle che può essere allocata per il tipo di handle indicato per la *HandleType* argomento è stato raggiunto.|  
|HY092|Identificatore di attributo/opzione non è valido|(DM) di *HandleType* argomento non era: SQL_HANDLE_ENV, SQL_HANDLE_DBC, SQL_HANDLE_STMT o SQL_HANDLE_DESC.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|Il *HandleType* argomento era SQL_HANDLE_DESC e il driver è stato un ODBC 2. *x* driver.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|(DM) di *HandleType* argomento era SQL_HANDLE_STMT e il driver non è un driver ODBC valido.<br /><br /> (DM) di *HandleType* argomento era SQL_HANDLE_DESC, e il driver non supporta l'allocazione di un handle di descrittore.|  
  
## <a name="comments"></a>Commenti  
 **SQLAllocHandle** viene usato per allocare gli handle per gli ambienti, le connessioni, le istruzioni e i descrittori, come descritto nelle sezioni seguenti. Per informazioni generali sugli handle, vedere [handle](../../../odbc/reference/develop-app/handles.md).  
  
 Più di un handle di ambiente, connessione o dell'istruzione può essere allocato da un'applicazione in un momento se più le allocazioni sono supportate dal driver. In ODBC è definito alcun limite al numero di ambiente, connessione, istruzione o handle descrittore che possono essere allocati in qualsiasi momento. Driver potrebbero imporre un limite al numero di un determinato tipo di handle che può essere allocata alla volta. per altre informazioni, vedere la documentazione del driver.  
  
 Se l'applicazione chiama **SQLAllocHandle** con  *\*OutputHandlePtr* impostata su un ambiente, connessione, istruzione o handle descrittore che esiste già, il driver sovrascrive il le informazioni associate le *gestire*, a meno che l'applicazione usa connection pooling (vedere "Allocazione di un ambiente di attributo per il pool di connessioni" più avanti in questa sezione). Gestione Driver non verificare se il *gestiscono* immesso nel  *\*OutputHandlePtr* è già in uso né ad controllare il contenuto di un handle precedente prima di sovrascriverli .  
  
> [!NOTE]  
>  Si tratta di programmazione di applicazioni ODBC non corretta per chiamare **SQLAllocHandle** due volte alla stessa variabile di applicazione definita per  *\*OutputHandlePtr* senza chiamare  **SQLFreeHandle** per liberare l'handle prima la riallocazione. Sovrascrittura ODBC gli handle in questo modo potrebbero causare un comportamento non coerente o errori da parte dei driver ODBC.  
  
 Nei sistemi operativi che supportano più thread, le applicazioni possono utilizzare lo stesso handle di ambiente, connessione, istruzione o descrittore su thread diversi. I driver devono supportare pertanto accedere multithread-safe a questa informazioni; un modo per ottenere questo risultato, ad esempio, consiste nell'usare un semaforo o una sezione critica. Per altre informazioni sul threading, vedere [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
 **SQLAllocHandle** non imposta l'attributo di ambiente SQL_ATTR_ODBC_VERSION quando viene chiamata per allocare un handle di ambiente; l'attributo di ambiente deve essere impostato dall'applicazione oppure SQLSTATE HY010 sarà (errore di sequenza di funzioni) restituito quando **SQLAllocHandle** viene chiamata per allocare un handle di connessione.  
  
 Per le applicazioni conformi agli standard, **SQLAllocHandle** viene eseguito il mapping al **SQLAllocHandleStd** in fase di compilazione. La differenza tra queste due funzioni è che **SQLAllocHandleStd** imposta l'attributo di ambiente SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC3 quando viene chiamato con il *HandleType* argomento impostato su SQL _HANDLE_ENV. Questa operazione viene eseguita poiché le applicazioni conformi agli standard sono sempre ODBC 3. *x* applicazioni. Inoltre, gli standard non richiedono la versione dell'applicazione da registrare. Questo è l'unica differenza tra queste due funzioni. in caso contrario, sono identici. **SQLAllocHandleStd** viene eseguito il mapping a **SQLAllocHandle** all'interno di Gestione driver. Di conseguenza, i driver di terze parti non sono necessario implementare **SQLAllocHandleStd**.  
  
 Le applicazioni ODBC 3.8 devono usare:  
  
-   **SQLAllocHandle e non SQLAllocHandleStd** per allocare un handle di ambiente.  
  
-   **SQLSetEnvAttr** su cui impostare l'attributo di ambiente SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3_80.  
  
## <a name="allocating-an-environment-handle"></a>Allocazione di un handle di ambiente  
 Un handle di ambiente fornisce l'accesso alle informazioni globali come gli handle di connessione valida e gli handle di connessione attiva. Per informazioni generali sull'handle di ambiente, vedere [handle di ambiente](../../../odbc/reference/develop-app/environment-handles.md).  
  
 Per richiedere un handle di ambiente, un'applicazione chiama **SQLAllocHandle** con un *HandleType* SQL_HANDLE_ENV e un *InputHandle* di SQL_NULL_HANDLE. Il driver alloca memoria per le informazioni sull'ambiente e passa il valore dell'handle associato di nuovo la  *\*OutputHandlePtr* argomento. L'applicazione passa il  *\*OutputHandle* valore in tutte le chiamate successive che richiedono un argomento dell'handle di ambiente. Per altre informazioni, vedere [allocare l'Handle di ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Con handle di ambiente di gestione di un Driver, se esiste già handle di ambiente del driver, quindi **SQLAllocHandle** con un *HandleType* SQL_HANDLE_ENV non viene chiamato in tale driver quando un connessione viene stabilita, solo **SQLAllocHandle** con un *HandleType* SQL_HANDLE_DBC. Se l'handle di ambiente del driver non esiste in handle di ambiente di gestione Driver, nel driver vengono chiamati sia SQLAllocHandle con un HandleType su SQL_HANDLE_ENV e SQLAllocHandle con un HandleType su SQL_HANDLE_DBC quando la prima connessione handle dell'ambiente è connesso al driver.  
  
 Quando Gestione Driver elabora le **SQLAllocHandle** utilizzabile con un *HandleType* SQL_HANDLE_ENV, controlla la **traccia** parola chiave nella sezione [ODBC] del sistema informazioni. Se è impostato su 1, gestione Driver abilita la traccia per l'applicazione corrente. Se è impostato il flag di traccia, traccia inizia quando l'handle di ambiente prima viene allocato e termina quando l'ultimo handle di ambiente viene liberato. Per altre informazioni, vedere [configurazione di origini dati](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Dopo avere allocato un handle di ambiente, un'applicazione deve chiamare **SQLSetEnvAttr** nell'handle di ambiente per impostare l'attributo di ambiente SQL_ATTR_ODBC_VERSION. Se questo attributo non viene impostato prima **SQLAllocHandle** viene chiamata per allocare un handle di connessione nell'ambiente, la chiamata per allocare la connessione restituisce SQLSTATE HY010 (funzione di errore nella sequenza). Per altre informazioni, vedere [dichiarazione della versione dell'applicazione ODBC](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md).  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>Allocazione di ambienti condivisi per il pool di connessioni  
 Gli ambienti possono essere condivisi tra più componenti su un singolo processo. Un ambiente condiviso può essere utilizzato da più di un componente nello stesso momento. Quando un componente Usa un ambiente condiviso, è possibile usare le connessioni in pool, che consentono di allocare e utilizzare una connessione esistente senza creare di nuovo tale connessione.  
  
 Prima di allocazione di un ambiente condiviso che può essere usato per il pool di connessioni, un'applicazione deve chiamare **SQLSetEnvAttr** su cui impostare l'attributo di ambiente SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_ HENV. **SQLSetEnvAttr** in questo caso viene chiamato con *EnvironmentHandle* impostate su null, che rende l'attributo di un attributo a livello di processo.  
  
 Dopo aver abilitato la limitazione delle richieste di connessione, un'applicazione chiama **SQLAllocHandle** con il *HandleType* argomento impostato su SQL_HANDLE_ENV. L'ambiente allocato da questa chiamata sarà un ambiente condiviso implicito perché il pool di connessioni è stato abilitato.  
  
 Quando viene allocato un ambiente condiviso, l'ambiente che verrà usato viene determinato solo **SQLAllocHandle** con un *HandleType* SQL_HANDLE_DBC viene chiamato. A questo punto, gestione Driver tenta di trovare un ambiente esistente che corrisponde agli attributi ambiente richiesti dall'applicazione. Se non esiste alcun ambiente di questo tipo, ne viene creato come un ambiente condiviso. Gestione Driver mantiene un conteggio dei riferimenti per ogni ambiente condiviso. il conteggio è impostato su 1 quando l'ambiente viene inizialmente creato. Se viene trovato un ambiente corrispondente, l'handle di quell'ambiente viene restituito all'applicazione e il conteggio dei riferimenti viene incrementato. Un handle di ambiente allocato in questo modo può essere utilizzato in una funzione ODBC che accetta un handle di ambiente come argomento di input.  
  
## <a name="allocating-a-connection-handle"></a>Allocazione di un handle di connessione  
 Un handle di connessione fornisce l'accesso a informazioni quali l'istruzione valida e aprire gli handle descrittore nella connessione e indica se una transazione è attualmente. Per informazioni generali sull'handle di connessione, vedere [handle di connessione](../../../odbc/reference/develop-app/connection-handles.md).  
  
 Per richiedere un handle di connessione, un'applicazione chiama **SQLAllocHandle** con un *HandleType* SQL_HANDLE_DBC. Il *InputHandle* argomento è impostato per l'handle di ambiente che è stato restituito dalla chiamata al metodo **SQLAllocHandle** che allocati tale handle. Il driver alloca memoria per le informazioni di connessione e passa di nuovo il valore dell'handle associato  *\*OutputHandlePtr*. L'applicazione passa il  *\*OutputHandlePtr* valore in tutte le chiamate successive che richiedono un handle di connessione. Per altre informazioni, vedere [allocare un Handle di connessione](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md).  
  
 Gestione Driver elabora le **SQLAllocHandle** funzione, il driver chiama **SQLAllocHandle** funzionare quando l'applicazione chiama **SQLConnect**, **SQLBrowseConnect**, o **SQLDriverConnect**. (Per altre informazioni, vedere [funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).)  
  
 Se l'attributo di ambiente SQL_ATTR_ODBC_VERSION non viene impostato prima **SQLAllocHandle** viene chiamata per allocare un handle di connessione nell'ambiente, la chiamata per allocare la connessione restituisce SQLSTATE HY010 (funzione sequenza Errore).  
  
 Quando un'applicazione chiama **SQLAllocHandle** con il *InputHandle* argomento impostato su SQL_HANDLE_DBC e impostata su un handle di ambiente condiviso, gestione Driver tenta di trovare un oggetto condiviso esistente ambiente che corrisponde agli attributi di ambiente impostati dall'applicazione. Se non esiste alcun ambiente di questo tipo, uno viene creato con un conteggio dei riferimenti (gestito da Gestione Driver) pari a 1. Se un oggetto corrispondente condiviso ambiente viene trovato, tale handle viene restituito all'applicazione e il conteggio dei riferimenti viene incrementato.  
  
 La connessione effettiva che verrà usata non è determinata da Gestione Driver finché **SQLConnect** oppure **SQLDriverConnect** viene chiamato. Gestione Driver utilizza le opzioni di connessione nella chiamata a **SQLConnect** (o le parole chiave di connessione nella chiamata a **SQLDriverConnect**) e impostare gli attributi di connessione dopo l'allocazione di connessione per stabilire la connessione nel pool deve essere utilizzata. Per altre informazioni, vedere [funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="allocating-a-statement-handle"></a>Allocazione di un handle di istruzione  
 Un handle di istruzione consente di accedere alle informazioni di istruzione, ad esempio i messaggi di errore, il nome del cursore e le informazioni sullo stato per l'elaborazione di istruzione SQL. Per informazioni generali sull'handle di istruzione, vedere [handle di istruzione](../../../odbc/reference/develop-app/statement-handles.md).  
  
 Per richiedere un handle di istruzione, un'applicazione si connette a un'origine dati e quindi chiama **SQLAllocHandle** prima di inviare istruzioni SQL. In questa chiamata *HandleType* deve essere impostato su SQL_HANDLE_STMT e *InputHandle* deve essere impostato per l'handle di connessione che è stato restituito dalla chiamata al metodo **SQLAllocHandle** che allocato tale handle. Il driver consente di allocare memoria per le informazioni di istruzione, associa l'handle di istruzione con la connessione specificata e passa di nuovo il valore dell'handle associato  *\*OutputHandlePtr*. L'applicazione passa il  *\*OutputHandlePtr* valore in tutte le chiamate successive che richiedono un handle di istruzione. Per altre informazioni, vedere [allocare un Handle di istruzione](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md).  
  
 Quando viene allocato l'handle di istruzione, il driver esegue l'allocazione di un set di descrittori di quattro automaticamente e assegna gli handle per questi descrittori di SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC, SQL_ATTR_IMP_ROW_DESC e SQL_ATTR_IMP_PARAM_DESC attributi di istruzione. Queste sono denominate *implicitamente* allocata descrittori. Per allocare un descrittore applicazione esplicito, vedere la sezione seguente, "Allocazione di un Handle descrittore".  
  
## <a name="allocating-a-descriptor-handle"></a>Allocazione di un Handle descrittore  
 Quando un'applicazione chiama **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_DESC, il driver alloca un descrittore dell'applicazione. Queste sono denominate *in modo esplicito* allocata descrittori. L'applicazione indirizza un driver per utilizzare un descrittore applicazione allocati in modo esplicito anziché uno automaticamente allocato per un handle di istruzione specificato chiamando il **SQLSetStmtAttr** con la SQL_ATTR_APP_ROW_DESC (funzione) attributo SQL_ATTR_APP_PARAM_DESC o. Un descrittore di implementazione non può essere allocato in modo esplicito, né è possibile specificare un descrittore di implementazione una **SQLSetStmtAttr** chiamata di funzione.  
  
 Descrittori allocati in modo esplicito sono associati a un handle di connessione invece di un handle di istruzione (come descrittori allocati automaticamente). Descrittori rimangono allocati solo quando un'applicazione è effettivamente connesso al database. Descrittori allocati in modo esplicito è associato a un handle di connessione, un'applicazione può associare un descrittore allocato in modo esplicito con più di un'istruzione all'interno di una connessione. Un descrittore applicazione implicito allocato, d'altra parte, non può essere associato a più di un handle di istruzione. (Non può essere associato a un handle diverso da quello che è stata allocata per qualsiasi istruzione.) Gli handle di descrittore allocato in modo esplicito possono essere liberati in modo esplicito dall'applicazione o chiamando **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DESC o in modo implicito quando la connessione è chiuso.  
  
 Quando viene liberato il descrittore allocato in modo esplicito, il descrittore allocato in modo implicito anche in questo caso è associato con l'istruzione. (L'attributo SQL_ATTR_APP_ROW_DESC o SQL_ATTR_APP_PARAM_DESC per l'istruzione è impostata nuovamente all'handle di descrittore allocato in modo implicito). Questo vale per tutte le istruzioni che sono state associate con il descrittore allocato in modo esplicito per la connessione.  
  
 Per altre informazioni sui descrittori, vedere [descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Visualizzare [ODBC programma di esempio](../../../odbc/reference/sample-odbc-program.md), [funzione SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), [funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), e [funzione SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Esecuzione di un'istruzione SQL|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Rilascio di un handle di ambiente, connessione, istruzione o descrittore|[Funzione SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Preparazione di un'istruzione per l'esecuzione|[Funzione SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Impostare un attributo di connessione|[Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Impostazione di un campo del descrittore|[Funzione SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|L'impostazione di un attributo di ambiente|[Funzione SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|L'impostazione di un attributo di istruzione|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
