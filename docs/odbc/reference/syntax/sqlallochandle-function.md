---
title: Funzione SQLAllocHandle . Documenti Microsoft
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 178e3fad1ec062dd7f812125da66b7e21a7a4f4b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290211"
---
# <a name="sqlallochandle-function"></a>Funzione SQLAllocHandle
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLAllocHandle** alloca un handle di ambiente, connessione, istruzione o descrittore.  
  
> [!NOTE]  
>  Questa funzione è una funzione generica per l'allocazione di handle che sostituisce le funzioni ODBC 2.0 **SQLAllocConnect**, **SQLAllocEnv**e **SQLAllocStmt**. Per consentire alle applicazioni che chiamano **SQLAllocHandle** di lavorare con ODBC 2. *x,* una chiamata a **SQLAllocHandle** viene mappata in Gestione Driver a **SQLAllocConnect**, **SQLAllocEnv**o **SQLAllocStmt**, a seconda dei casi. Per ulteriori informazioni, vedere "Commenti". Per ulteriori informazioni su ciò che Gestione Driver esegue il mapping di questa funzione a quando un ODBC 3. *l'applicazione x* funziona con un'applicazione ODBC 2. *x,* vedere Mapping delle funzioni di sostituzione per la [compatibilità con le applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)con le versioni precedenti.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *HandleType*  
 [Ingresso] Tipo di handle che deve essere allocato da **SQLAllocHandle.** Deve essere uno dei valori seguenti:   
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN handle viene utilizzato solo da Gestione Driver e dal driver. Le applicazioni non devono utilizzare questo tipo di handle. Per ulteriori informazioni su SQL_HANDLE_DBC_INFO_TOKEN, vedere Sviluppo del [riconoscimento](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)del pool di connessioni in un driver ODBC .  
  
 *InputHandle*  
 [Ingresso] Handle di input nel cui contesto deve essere allocato il nuovo handle. Se *HandleType* è SQL_HANDLE_ENV, si tratta di SQL_NULL_HANDLE. Se *HandleType* è SQL_HANDLE_DBC, deve essere un handle di ambiente e, se è SQL_HANDLE_STMT o SQL_HANDLE_DESC, deve essere un handle di connessione.  
  
 *OutputHandlePtr*  
 [Uscita] Puntatore a un buffer in cui restituire l'handle alla struttura di dati appena allocata.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE o SQL_ERROR.  
  
 Quando si alloca un handle diverso da un handle di ambiente, se **SQLAllocHandle** restituisce SQL_ERROR, imposta *OutputHandlePtr* su SQL_NULL_HDBC, SQL_NULL_HSTMT o SQL_NULL_HDESC, a seconda del valore di *HandleType*, a meno che l'argomento di output non sia un puntatore null. L'applicazione può quindi ottenere informazioni aggiuntive dalla struttura dei dati di diagnostica associata all'handle nell'argomento *InputHandle.*  
  
## <a name="environment-handle-allocation-errors"></a>Errori di allocazione dell'handle di ambienteEnvironment Handle Allocation Errors  
 L'allocazione dell'ambiente si verifica sia all'interno di Gestione Driver che all'interno di ogni driver. L'errore restituito da **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_ENV dipende dal livello in cui si è verificato l'errore.  
  
 Se Gestione Driver non è in grado di allocare memoria per * \*OutputHandlePtr* quando **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_ENV viene chiamato o l'applicazione fornisce un puntatore null per *OutputHandlePtr*, **SQLAllocHandle** restituisce SQL_ERROR. Gestione Driver imposta*OutputHandlePtr* su SQL_NULL_HENV (a meno che l'applicazione non fornisse un puntatore null, che restituisce SQL_ERROR). Non esiste alcun acesempio a cui associare informazioni diagnostiche aggiuntive.  
  
 Gestione Driver non chiama la funzione di allocazione dell'handle di ambiente a livello di driver fino a quando l'applicazione non chiama **SQLConnect**, **SQLBrowseConnect**o **SQLDriverConnect**. Se si verifica un errore nella funzione **SQLAllocHandle** a livello di driver, la funzione **SQLConnect**, **SQLBrowseConnect**o **SQLDriverConnect** a livello di Gestione Driver restituisce SQL_ERROR. La struttura dei dati di diagnostica contiene SQLSTATE IM004 **(SQLAllocHandle** del driver non riuscito). L'errore viene restituito su un handle di connessione.  
  
 Per ulteriori informazioni sul flusso delle chiamate di funzione tra Gestione Driver e un driver, vedere [Funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLAllocHandle** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con *handleType* e *Handle* appropriati impostati sul valore di *InputHandle*. SQL_SUCCESS_WITH_INFO (ma non SQL_ERROR) può essere restituito per il *OutputHandle* argomento. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLAllocHandle** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08003|Connessione non aperta|(DM) l'argomento *HandleType* è stato SQL_HANDLE_STMT o SQL_HANDLE_DESC, ma la connessione specificata dall'argomento *InputHandle* non è stata aperta. Il processo di connessione deve essere completato correttamente (e la connessione deve essere aperta) affinché il driver allochi un handle di istruzione o descrittore.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|(DM) Gestione Driver non è stato in grado di allocare memoria per l'handle specificato.<br /><br /> Il driver non è stato in grado di allocare memoria per l'handle specificato.|  
|I009|Utilizzo non valido del puntatore null|(DM) l'argomento *OutputHandlePtr* era un puntatore null.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) l'argomento *HandleType* è stato SQL_HANDLE_DBC e **SQLSetEnvAttr** non è stato chiamato per impostare l'attributo di ambiente SQL_ODBC_VERSION.<br /><br /> (DM) una funzione in esecuzione in modo asincrono è stata chiamata per **il InputHandle** ed era ancora in esecuzione quando la funzione **SQLAllocHandle** è stata chiamata con **HandleType** impostato su SQL_HANDLE_STMT o SQL_HANDLE_DESC.|  
|HY013|Errore di gestione della memoria|L'argomento *HandleType* è stato SQL_HANDLE_DBC, SQL_HANDLE_STMT o SQL_HANDLE_DESC. e non è stato possibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostanti, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY014 (informazioni in base al|Limite al numero di maniglie superate|È stato raggiunto il limite definito dal driver per il numero di handle che possono essere allocati per il tipo di handle indicato dall'argomento *HandleType.*|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo/opzione non valido|(DM) l'argomento *HandleType* non è: SQL_HANDLE_ENV, SQL_HANDLE_DBC, SQL_HANDLE_STMT o SQL_HANDLE_DESC.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|L'argomento *HandleType* è stato SQL_HANDLE_DESC e il driver era un ODBC 2. *driver x.*|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) l'argomento *HandleType* è stato SQL_HANDLE_STMT e il driver non è un driver ODBC valido.<br /><br /> (DM) l'argomento *HandleType* è stato SQL_HANDLE_DESC e il driver non supporta l'allocazione di un handle descrittore.|  
  
## <a name="comments"></a>Commenti  
 **SQLAllocHandle** viene utilizzato per allocare handle per ambienti, connessioni, istruzioni e descrittori, come descritto nelle sezioni seguenti. Per informazioni generali sulle maniglie, vedere [Maniglie](../../../odbc/reference/develop-app/handles.md).  
  
 Più di un ambiente, connessione o handle di istruzione possono essere allocati da un'applicazione alla volta se più allocazioni sono supportate dal driver. In ODBC non è definito alcun limite per il numero di handle di ambiente, connessione, istruzione o descrittore che possono essere allocati contemporaneamente. I conducenti possono imporre un limite al numero di un determinato tipo di maniglia che può essere assegnato contemporaneamente; per ulteriori informazioni, vedere la documentazione del driver.  
  
 Se l'applicazione chiama **SQLAllocHandle** con * \*OutputHandlePtr* impostato su un handle di ambiente, connessione, istruzione o descrittore già esistente, il driver sovrascrive le informazioni associate all'handle , a meno che l'applicazione non utilizzi il pool di connessioni (vedere "Allocazione di un attributo di ambiente per il pool di connessioni" più avanti in questa sezione). *handle* Gestione Driver non controlla se *l'handle* immesso in * \*OutputHandlePtr* è già in uso, né controlla il contenuto precedente di un handle prima di sovrascriverli.  
  
> [!NOTE]  
>  Programmazione dell'applicazione ODBC non è corretta per chiamare **SQLAllocHandle** due volte con la stessa variabile di applicazione definita per * \*OutputHandlePtr* senza chiamare **SQLFreeHandle** per liberare l'handle prima di riallocherlo. La sovrascrittura degli handle ODBC in questo modo potrebbe causare un comportamento o errori incoerenti da parte dei driver ODBC.  
  
 Nei sistemi operativi che supportano più thread, le applicazioni possono utilizzare lo stesso handle di ambiente, connessione, istruzione o descrittore su thread diversi. I driver devono pertanto supportare l'accesso sicuro e multithread a queste informazioni; Un modo per ottenere questo risultato, ad esempio, consiste nell'utilizzare una sezione critica o un semaforo. Per ulteriori informazioni sul threading, vedere [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
 **SQLAllocHandle** non imposta l'attributo di ambiente SQL_ATTR_ODBC_VERSION quando viene chiamato per allocare un handle di ambiente. l'attributo di ambiente deve essere impostato dall'applicazione oppure SQLSTATE HY010 (errore di sequenza Function) verrà restituito quando **SQLAllocHandle** viene chiamato per allocare un handle di connessione.  
  
 Per le applicazioni conformi agli standard, **SQLAllocHandle** viene mappato a **SQLAllocHandleStd** in fase di compilazione. La differenza tra queste due funzioni è che **SQLAllocHandleStd** imposta il SQL_ATTR_ODBC_VERSIONattributo dall'attributo di ambiente su SQL_OV_ODBC3 quando viene chiamato con il *HandleType* argomento impostato su SQL_HANDLE_ENV. Questa operazione viene eseguita perché le applicazioni conformi agli standard sono sempre ODBC 3. *applicazioni x.* Inoltre, gli standard non richiedono la registrazione della versione dell'applicazione. Questa è l'unica differenza tra queste due funzioni; in caso contrario, sono identici. **SQLAllocHandleStd** è mappato a **SQLAllocHandle** all'interno del gestore dei driver. Pertanto, i driver di terze parti non è necessario implementare **SQLAllocHandleStd**.  
  
 Le applicazioni ODBC 3.8 devono utilizzare:  
  
-   **SQLAllocHandle e non SQLAllocHandleStd** per allocare un handle di ambiente.  
  
-   **SQLSetEnvAttr** per impostare l'attributo di ambiente di SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC3_80.  
  
## <a name="allocating-an-environment-handle"></a>Allocazione di un handle di ambiente  
 Un handle di ambiente fornisce l'accesso a informazioni globali, ad esempio handle di connessione validi e handle di connessione attivi. Per informazioni generali sugli handle di ambiente, vedere Handle di [ambiente](../../../odbc/reference/develop-app/environment-handles.md).  
  
 Per richiedere un handle di ambiente, un'applicazione chiama **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_ENV e un *InputHandle* di SQL_NULL_HANDLE. Il driver alloca memoria per le informazioni sull'ambiente e passa il valore dell'handle associato nel * \*OutputHandlePtr* argomento. L'applicazione passa il * \*valore OutputHandle* in tutte le chiamate successive che richiedono un argomento di handle di ambiente. Per ulteriori informazioni, vedere [Allocazione dell'handle di ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 In un handle di ambiente di Gestione Driver, se esiste già un handle di ambiente del driver, **quindi SQLAllocHandle** con un *HandleType* di SQL_HANDLE_ENV non viene chiamato in tale driver quando viene stabilita una connessione, solo **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_DBC. Se l'handle di ambiente di un driver non esiste nell'handle di ambiente di Gestione Driver, sqlAllocHandle con un HandleType di SQL_HANDLE_ENV e SQLAllocHandle con un HandleType di SQL_HANDLE_DBC vengono chiamati nel driver quando il primo handle di connessione dell'ambiente è connesso al driver.  
  
 Quando Gestione Driver elabora la funzione **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_ENV, controlla la parola chiave **Trace** nella sezione [ODBC] delle informazioni di sistema. Se è impostato su 1, Gestione Driver abilita la traccia per l'applicazione corrente. Se il flag di traccia è impostato, la traccia inizia quando viene allocato il primo handle di ambiente e termina quando viene liberato l'ultimo handle di ambiente. Per ulteriori informazioni, vedere [Configurazione delle origini dati](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Dopo aver allocato un handle di ambiente, un'applicazione deve chiamare **SQLSetEnvAttr** sull'handle di ambiente per impostare l'attributo di ambiente SQL_ATTR_ODBC_VERSION. Se questo attributo non viene impostato prima **sqlAllocHandle** viene chiamato per allocare un handle di connessione nell'ambiente, la chiamata per allocare la connessione restituirà SQLSTATE HY010 (errore di sequenza di funzione). Per ulteriori informazioni, vedere [Dichiarazione della versione ODBC dell'applicazione](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md).  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>Allocazione di ambienti condivisi per il pool di connessioni  
 Gli ambienti possono essere condivisi tra più componenti in un singolo processo. Un ambiente condiviso può essere utilizzato da più di un componente contemporaneamente. Quando un componente utilizza un ambiente condiviso, può utilizzare connessioni in pool, che consentono di allocare e utilizzare una connessione esistente senza ricreare tale connessione.  
  
 Prima di allocare un ambiente condiviso che può essere utilizzato per il pool di connessioni, un'applicazione deve chiamare **SQLSetEnvAttr** per impostare l'attributo di ambiente SQL_ATTR_CONNECTION_POOLING su SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_HENV. **SQLSetEnvAttr** in questo caso viene chiamato con *EnvironmentHandle* impostato su null, che rende l'attributo un attributo a livello di processo.  
  
 Dopo aver abilitato il pool di connessioni, un'applicazione chiama **SQLAllocHandle** con il *HandleType* argomento impostato su SQL_HANDLE_ENV. L'ambiente allocato da questa chiamata sarà un ambiente condiviso implicito perché il pool di connessioni è stato abilitato.  
  
 Quando viene allocato un ambiente condiviso, l'ambiente che verrà utilizzato non viene determinato fino a quando **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_DBC viene chiamato. A questo punto, Gestione Driver tenta di trovare un ambiente esistente che corrisponde agli attributi di ambiente richiesti dall'applicazione. Se tale ambiente non esiste, ne viene creato uno come ambiente condiviso. Gestione Driver mantiene un conteggio dei riferimenti per ogni ambiente condiviso; il conteggio viene impostato su 1 quando l'ambiente viene creato per la prima volta. Se viene trovato un ambiente corrispondente, l'handle di tale ambiente viene restituito all'applicazione e il conteggio dei riferimenti viene incrementato. Un handle di ambiente allocato in questo modo può essere utilizzato in qualsiasi funzione ODBC che accetta un handle di ambiente come argomento di input.  
  
## <a name="allocating-a-connection-handle"></a>Allocazione di un handle di connessione  
 Un handle di connessione fornisce l'accesso a informazioni quali l'istruzione valida e gli handle del descrittore nella connessione e se una transazione è attualmente aperta. Per informazioni generali sugli handle di connessione, vedere Handle di [connessione](../../../odbc/reference/develop-app/connection-handles.md).  
  
 Per richiedere un handle di connessione, un'applicazione chiama **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_DBC. Il *InputHandle* argomento viene impostato sull'handle di ambiente restituito dalla chiamata a **SQLAllocHandle** che ha allocato tale handle. Il driver alloca memoria per le informazioni di connessione e passa il valore dell'handle associato in * \*OutputHandlePtr*. L'applicazione passa il * \*OutputHandlePtr* valore in tutte le chiamate successive che richiedono un handle di connessione. Per ulteriori informazioni, vedere [Allocazione di un handle di connessione](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md).  
  
 Gestione Driver elabora la funzione **SQLAllocHandle** e chiama la funzione **SQLAllocHandle** del driver quando l'applicazione chiama **SQLConnect**, **SQLBrowseConnect**o **SQLDriverConnect**. (Per altre informazioni, vedere [Funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).)  
  
 Se l'attributo di ambiente SQL_ATTR_ODBC_VERSION non viene impostato prima **sqlAllocHandle** viene chiamato per allocare un handle di connessione nell'ambiente, la chiamata per allocare la connessione restituirà SQLSTATE HY010 (errore di sequenza di funzione).  
  
 Quando un'applicazione chiama **SQLAllocHandle** con il *InputHandle* argomento impostato su SQL_HANDLE_DBC e anche impostato su un handle di ambiente condiviso, Gestione Driver tenta di trovare un ambiente condiviso esistente che corrisponde agli attributi di ambiente impostati dall'applicazione. Se tale ambiente non esiste, ne viene creato uno, con un conteggio dei riferimenti (mantenuto da Gestione Driver) pari a 1. Se viene trovato un ambiente condiviso corrispondente, tale handle viene restituito all'applicazione e il relativo conteggio dei riferimenti viene incrementato.  
  
 La connessione effettiva che verrà utilizzata non è determinata da Gestione Driver fino a quando non viene chiamato **SQLConnect** o **SQLDriverConnect.** Gestione Driver utilizza le opzioni di connessione nella chiamata a **SQLConnect** (o le parole chiave di connessione nella chiamata a **SQLDriverConnect**) e gli attributi di connessione impostati dopo l'allocazione di connessione per determinare quale connessione nel pool deve essere utilizzata. Per ulteriori informazioni, vedere [Funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="allocating-a-statement-handle"></a>Allocazione di un handle di istruzione  
 Un handle di istruzione fornisce l'accesso alle informazioni sull'istruzione, ad esempio i messaggi di errore, il nome del cursore e le informazioni sullo stato per l'elaborazione dell'istruzione SQL. Per informazioni generali sugli handle di istruzione, vedere [Handle di istruzione](../../../odbc/reference/develop-app/statement-handles.md).  
  
 Per richiedere un handle di istruzione, un'applicazione si connette a un'origine dati e quindi chiama **SQLAllocHandle** prima di inviare istruzioni SQL. In questa chiamata, *HandleType* deve essere impostato su SQL_HANDLE_STMT e *InputHandle* deve essere impostato sull'handle di connessione restituito dalla chiamata a **SQLAllocHandle** che ha allocato tale handle. Il driver alloca memoria per le informazioni sull'istruzione, associa l'handle dell'istruzione alla connessione specificata e passa il valore dell'handle associato in * \*OutputHandlePtr*. L'applicazione passa il * \*Valore OutputHandlePtr* in tutte le chiamate successive che richiedono un handle di istruzione. Per ulteriori informazioni, vedere [Allocazione di un handle di istruzione](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md).  
  
 Quando l'handle dell'istruzione viene allocato, il driver alloca automaticamente un set di quattro descrittori e assegna gli handle per questi descrittori agli attributi di istruzione SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC, SQL_ATTR_IMP_ROW_DESC e SQL_ATTR_IMP_PARAM_DESC. Questi sono detti descrittori allocati *in modo implicito.* Per allocare un descrittore dell'applicazione in modo esplicito, vedere la sezione seguente, "Allocazione di un handle di descrittore".  
  
## <a name="allocating-a-descriptor-handle"></a>Allocazione di un handle di descrittore  
 Quando un'applicazione chiama **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_DESC, il driver alloca un descrittore dell'applicazione. Questi sono detti descrittori allocati *in modo esplicito.* L'applicazione indica a un driver di utilizzare un descrittore di applicazione allocato in modo esplicito anziché uno allocato automaticamente per un handle di istruzione specificato chiamando la funzione **SQLSetStmtAttr** con il SQL_ATTR_APP_ROW_DESC o SQL_ATTR_APP_PARAM_DESC attributo. Un descrittore di implementazione non può essere allocato in modo esplicito, né può essere specificato un descrittore di implementazione in una chiamata di funzione **SQLSetStmtAttr.An** implementation descriptor cannot be allocated explicitly, nor can be specified an implementation descriptor in an SQLSetStmtAttr function call.  
  
 I descrittori allocati in modo esplicito sono associati a un handle di connessione anziché a un handle di istruzione (come lo sono i descrittori allocati automaticamente). I descrittori rimangono allocati solo quando un'applicazione è effettivamente connessa al database. Poiché i descrittori allocati in modo esplicito sono associati a un handle di connessione, un'applicazione può associare un descrittore allocato in modo esplicito a più di un'istruzione all'interno di una connessione. Un descrittore dell'applicazione allocato in modo implicito, d'altra parte, non può essere associato a più di un handle di istruzione. Non può essere associato ad alcun handle di istruzione diverso da quello per cui è stato allocato. Gli handle di descrittore allocati in modo esplicito possono essere liberati in modo esplicito dall'applicazione o chiamando **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DESC o in modo implicito quando la connessione viene chiusa.  
  
 Quando il descrittore allocato in modo esplicito viene liberato, il descrittore allocato in modo implicito viene nuovamente associato all'istruzione. L'attributo SQL_ATTR_APP_ROW_DESC o SQL_ATTR_APP_PARAM_DESC per tale istruzione viene nuovamente impostato sull'handle del descrittore allocato in modo implicito. Ciò vale per tutte le istruzioni associate al descrittore allocato in modo esplicito nella connessione.  
  
 Per ulteriori informazioni sui descrittori, vedere [Descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Vedere [Programma ODBC di esempio](../../../odbc/reference/sample-odbc-program.md), Funzione [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), Funzione [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [Funzione SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberare un handle di ambiente, connessione, istruzione o descrittore|[SQLFreeHandle Function](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Preparazione di un'istruzione per l'esecuzione|[Pagina relativa alla funzione SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Impostazione di un attributo di connessione|[Pagina relativa alla funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Impostazione di un campo descrittore|[Funzione SQLSetDescFieldSQLSetDescField Function](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Impostazione di un attributo di ambiente|[Funzione SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Impostazione di un attributo di istruzioneSetting a statement attribute|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
