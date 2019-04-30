---
title: Funzione SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLEndTran
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa1b2afec38116bef3ae90d75607d21c9a92cd80
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062259"
---
# <a name="sqlendtran-function"></a>SQLEndTran Function
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLEndTran** richiede un'operazione di commit o rollback per tutte le operazioni attive in tutte le istruzioni associate a una connessione. **SQLEndTran** può inoltre richiedere che per tutte le connessioni associate a un ambiente di eseguire un'operazione di commit o rollback.  
  
> [!NOTE]  
>  Per altre informazioni su quali il Driver Manager esegue il mapping a questa funzione quando un'applicazione ODBC 3. *x* applicazione funziona con un'API ODBC 2. *x* driver, vedere [Mapping di funzioni di sostituzione per la compatibilità con le versioni precedenti di applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>Argomenti  
 *HandleType*  
 [Input] Identificatore del tipo di handle. Contiene entrambi SQL_HANDLE_ENV (se *gestiscono* è un handle di ambiente) o SQL_HANDLE_DBC (se *gestire* è un handle di connessione).  
  
 *Handle*  
 [Input] L'handle, del tipo indicato dal *HandleType*, che indica l'ambito della transazione. Per altre informazioni, vedere "Commenti".  
  
 *CompletionType*  
 [Input] Uno dei due valori seguenti:  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLEndTran** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con l'appropriato *HandleType*e *gestire*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLEndTran** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08003|Connessione non aperta|(DM) di *HandleType* era SQL_HANDLE_DBC e il *gestire* non era in uno stato connesso.|  
|08007|Errore di connessione durante la transazione|Il *HandleType* era SQL_HANDLE_DBC e la connessione è associato il *gestire* non è riuscita durante l'esecuzione della funzione e non può essere determinato se richiesto  **Eseguire il COMMIT** oppure **ROLLBACK** si è verificato prima dell'errore.|  
|25S01|Stato della transazione sconosciuto|Uno o più delle connessioni in *gestire* non è riuscito a completare la transazione con il risultato specificato e il risultato è sconosciuto.|  
|25S02|Transazione è ancora attiva|Il driver non è in grado di garantire che tutte le operazioni nella transazione globale è stato possibile completare in modo atomico e la transazione è ancora attiva.|  
|25S03|Viene eseguito il rollback delle transazioni|Il driver non è in grado di garantire che tutte le operazioni nella transazione globale è stato possibile completare in modo atomico e tutto il lavoro nella transazione attiva in *gestire* è stato eseguito il rollback.|  
|40001|Errore di serializzazione.|Il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40002|Violazione di vincolo di integrità|Il *CompletionType* era SQL_COMMIT, e il commit delle modifiche ha causato la violazione di vincolo dell'integrità. Di conseguenza, il rollback della transazione.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*szMessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *ConnectionHandle*. La funzione è stata chiamata e prima di completare l'esecuzione [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) è stato chiamato sulle *ConnectionHandle*. Quindi la funzione è stata chiamata nuovamente sul *ConnectionHandle*.<br /><br /> La funzione è stata chiamata e prima di completare l'esecuzione **SQLCancelHandle** è stato chiamato sulle *ConnectionHandle* da un thread diverso in un'applicazione multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per un handle di istruzione associato a una funzione in modo asincrono in esecuzione la *ConnectionHandle* ed era ancora in esecuzione quando **SQLEndTran** è stato chiamato.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *ConnectionHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per un handle di istruzione è associato il *ConnectionHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *gestiscono* con *HandleType* impostato su SQL_HANDLE_DBC ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per uno degli handle di istruzione associati *gestire* e SQL_PARAM_DATA_AVAILABLE restituito. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.|  
|HY012|Codice operativo della transazione non valido|(DM) il valore specificato per l'argomento *CompletionType* era né SQL_COMMIT o SQL_ROLLBACK.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY092|Identificatore di attributo/opzione non è valido|(DM) il valore specificato per l'argomento *HandleType* era SQL_HANDLE_ENV né SQL_HANDLE_DBC.|  
|HY115|SQLEndTran non è consentito per un ambiente che contiene una connessione con l'esecuzione della funzione asincrona abilitata|(DM) *HandleType* non può essere impostato su SQL_HANDLE_ENV se l'esecuzione asincrona delle funzioni di connessione è abilitata per una connessione nell'ambiente.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, fare riferimento alla sezione dei commenti di questo argomento.|  
|HYC00|Funzionalità opzionale non implementata|L'origine dati o driver non supporta il **ROLLBACK** operazione.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *ConnectionHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 Per un database ODBC 3. *x* driver, se *HandleType* è SQL_HANDLE_ENV e *gestire* è un handle di ambiente valido, quindi il Driver Manager chiamerà **SQLEndTran**in ogni driver associato all'ambiente. Il *gestire* argomento per la chiamata a un driver saranno handle di ambiente del driver. Per un database ODBC 2. *x* driver, se *HandleType* è SQL_HANDLE_ENV e *gestire* è un handle di ambiente valido e non esistono più connessioni in uno stato connesso in tale ambiente, quindi il Driver Manager chiamerà **SQLTransact** nel driver una volta per ogni connessione in uno stato connesso in quell'ambiente. Il *gestire* argomento in ogni chiamata sarà handle di connessione. In entrambi i casi, il driver tenterà di eseguire il commit o il rollback delle transazioni, in base al valore *CompletionType*, su tutte le connessioni che sono in uno stato connesso in tale ambiente. Le connessioni che non sono attive non influenzano la transazione.  
  
> [!NOTE]  
>  **SQLEndTran** non può essere usato per eseguire il commit o il rollback delle transazioni in un ambiente condiviso. SQLSTATE HY092 verrà restituito (identificatore di attributo/opzione non valida) se **SQLEndTran** viene chiamato con *gestire* impostata su entrambi l'handle di un ambiente condiviso o l'handle di una connessione su un oggetto condiviso ambiente.  
  
 Gestione Driver restituisce SQL_SUCCESS solo se riceve SQL_SUCCESS per ogni connessione. Se in una o più connessioni, gestione Driver riceve SQL_ERROR, restituisce SQL_ERROR all'applicazione e le informazioni di diagnostica viene inserite nella struttura di dati di diagnostica dell'ambiente. Per determinare quale connessione o connessioni non è riuscita durante l'operazione di commit o rollback, l'applicazione può chiamare **SQLGetDiagRec** per ogni connessione.  
  
> [!NOTE]  
>  Gestione Driver non simula una transazione globale tra tutte le connessioni e pertanto non utilizza i protocolli di commit in due fasi.  
  
 Se *CompletionType* SQL_COMMIT, viene **SQLEndTran** genera una richiesta di commit di tutte le operazioni attive in qualsiasi istruzione associato a una connessione interessata. Se *CompletionType* SQL_ROLLBACK, viene **SQLEndTran** genera una richiesta di rollback di tutte le operazioni attive in qualsiasi istruzione associato a una connessione interessata. Se non sono attiva, nessuna transazione **SQLEndTran** restituisce SQL_SUCCESS senza alcun effetto su tutte le origini dati. Per altre informazioni, vedere [Committing e rollback transazioni](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md).  
  
 Se il driver si trova in modalità di commit manuale (chiamando **SQLSetConnectAttr** con il SQL_ATTR_AUTOCOMMIT attributo impostato su SQL_AUTOCOMMIT_OFF), una nuova transazione viene avviata in modo implicito quando un'istruzione SQL che può essere contenuta all'interno di un transazione viene eseguita sull'origine dati corrente. Per altre informazioni, vedere [modalità di Commit](../../../odbc/reference/develop-app/commit-mode.md).  
  
 Per determinare i cursori di influenza delle operazioni di transazione, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CURSOR_ROLLBACK_BEHAVIOR e SQL_CURSOR_COMMIT_BEHAVIOR. Per altre informazioni, vedere i paragrafi seguenti e vedere anche [effettiva delle transazioni su cursori e istruzioni preparate](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
 Se il valore SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR è uguale a, SQL_CB_DELETE **SQLEndTran** chiude e consente di eliminare tutti i cursori aperti su tutte le istruzioni associate alla connessione e Cancella tutti i risultati in sospeso. **SQLEndTran** esce da qualsiasi istruzione presente in uno stato (non preparato) allocato; l'applicazione può riutilizzarli per le richieste successive di SQL oppure chiamare **SQLFreeStmt** oppure **SQLFreeHandle** con una *HandleType* SQL_HANDLE_STMT dealloca.  
  
 Se il valore SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR è uguale a, SQL_CB_CLOSE **SQLEndTran** chiude i cursori aperti vengono su tutte le istruzioni associate alla connessione. **SQLEndTran** esce da qualsiasi istruzione presente in uno stato preparato; l'applicazione può chiamare **SQLExecute** per un'istruzione associata alla connessione senza prima chiamare **SQLPrepare**.  
  
 Se il valore SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR è uguale a, SQL_CB_PRESERVE **SQLEndTran** influisce sui cursori aperti associati alla connessione. I cursori rimangono in corrispondenza della riga a cui prima della chiamata a **SQLEndTran**.  
  
 Per i driver e origini dati che supportano le transazioni, la chiamata **SQLEndTran** con SQL_COMMIT o SQL_ROLLBACK quando non è attiva alcuna transazione restituisce SQL_SUCCESS (che indica che non vi sia alcun lavoro da eseguire il commit o rollback) e non ha alcun effetto sull'origine dati.  
  
 Quando un driver in modalità autocommit, gestione Driver non chiama **SQLEndTran** nel driver. **SQLEndTran** sempre restituisce SQL_SUCCESS indipendentemente dal fatto che venga chiamato con un *CompletionType* di SQL_COMMIT o SQL_ROLLBACK.  
  
 Origini dati o driver che non supportano le transazioni (**SQLGetInfo** *opzione* SQL_TXN_CAPABLE è SQL_TC_NONE) sono sempre in modo efficace in modalità autocommit e pertanto sempre restituito SQL_SUCCESS per **SQLEndTran** se vengono chiamati con un *CompletionType* di SQL_COMMIT o SQL_ROLLBACK. Tali driver e origini dati effettivamente il rollback delle transazioni quando richiesto per eseguire questa operazione.  
  
## <a name="suspended-state"></a>Stato di sospensione  
 In Gestioni di Driver che sono state rilasciate prima di Windows 7, era attiva una transazione se **SQLEndTran** restituito SQL_ERROR dal driver. Tuttavia, è possibile che la transazione era stato eseguito correttamente il commit nel server, ma il driver del client non ha ricevuto notifica (ad esempio perché si è verificato un errore di rete). La connessione Ciò lascia in uno stato non valido. A partire da Windows 7, quando **SQLEndTran** restituisce SQL_ERROR, la connessione potrebbero essere in uno stato sospeso. In uno stato sospeso, è possibile chiamare le funzioni di sola lettura. Infine, l'applicazione deve chiamare **SQLDisconnect** su una connessione sospesi per rilasciare le risorse.  
  
 Se tutte le condizioni seguenti sono vere, la connessione viene inserita in uno stato sospeso:  
  
-   Il driver restituisce da SQL_ERROR **SQLEndTran**.  
  
-   Il driver è ODBC 3.8, o versione successiva.  
  
-   La versione dell'applicazione è 3.8 o versioni successive; o l'applicazione ricompilata 2.x o 3.x ODBC consente di annullare correttamente la **SQLEndTran** funzionare attraverso **SQLCancelHandle**.  
  
-   Il driver non ha restituito uno dei due messaggi seguenti, che consentono di verificare che la transazione non è stata completata:  
  
    -   25S03: Viene eseguito il rollback delle transazioni  
  
    -   40001: Errore di serializzazione.  
  
    -   40002: vincolo di integrità  
  
    -   HYC00: Funzionalità opzionale non implementata  
  
 Se **SQLEndTran** è stato chiamato in un ambiente handle e una delle relative connessioni soddisfatte le condizioni precedenti, tutte le connessioni la connessione per lo stesso driver verranno inserite in stato sospeso.  
  
 Dopo che un'applicazione chiama **SQLDisconnect** su una connessione sospesa, la connessione può essere usata per riconnettersi a un'altra origine dati o la stessa origine dati.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Annullamento di una funzione in esecuzione in modalità asincrona su un handle di connessione.|[Funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Restituzione di informazioni su un'origine dati o driver|[Funzione SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Rilascio di un handle|[Funzione SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Rilascio di un handle di istruzione|[Funzione SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Esecuzione asincrona (metodo di polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
