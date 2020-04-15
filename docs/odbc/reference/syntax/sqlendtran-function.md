---
title: 'Funzione SQLEndTran : Documenti Microsoft'
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLEndTran
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cce7792e52fce4984f3da41e11d79c34b6b79e53
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302742"
---
# <a name="sqlendtran-function"></a>SQLEndTran Function
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLEndTran** richiede un'operazione di commit o rollback per tutte le operazioni attive su tutte le istruzioni associate a una connessione. **SQLEndTran** può anche richiedere che venga eseguita un'operazione di commit o rollback per tutte le connessioni associate a un ambiente.  
  
> [!NOTE]  
>  Per ulteriori informazioni su ciò che Gestione Driver esegue il mapping di questa funzione a quando un ODBC 3. *l'applicazione x* funziona con un'applicazione ODBC 2. *x,* vedere Mapping delle funzioni di sostituzione per la [compatibilità con le applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)con le versioni precedenti.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>Argomenti  
 *HandleType*  
 [Ingresso] Identificatore del tipo di handle. Contiene SQL_HANDLE_ENV (se *Handle* è un handle di ambiente) o SQL_HANDLE_DBC (se *Handle* è un handle di connessione).  
  
 *Handle*  
 [Ingresso] Handle, del tipo indicato da *HandleType*, che indica l'ambito della transazione. Vedere "Commenti" per ulteriori informazioni.  
  
 *CompletionTypeCompletionType (Tipo di completament*  
 [Ingresso] Uno dei due valori seguenti:  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLEndTran** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con gli *handleType* e *Handle*appropriati. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLEndTran** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08003|Connessione non aperta|(DM) *il HandleType* è stato SQL_HANDLE_DBC e *l'handle* non era in uno stato connesso.|  
|08007|Errore di connessione durante la transazioneConnection failure during transaction|Il *HandleType* è stato SQL_HANDLE_DBC e la connessione associata *all'handle* non è riuscita durante l'esecuzione della funzione e non è possibile determinare se **l'impegno richiesto** **è** stato eseguito prima dell'errore.|  
|25S01|Stato della transazione sconosciuto|Una o più connessioni in *Handle* non sono riuscite a completare la transazione con il risultato specificato e il risultato è sconosciuto.|  
|25S02 (in questo 25S02)|La transazione è ancora attiva|Il driver non è stato in grado di garantire che tutto il lavoro nella transazione globale possa essere completato in modo atomico e che la transazione sia ancora attiva.|  
|25S03|Viene eseguito il rollback della transazioneTransaction is rolled back|Il driver non è stato in grado di garantire che tutto il lavoro nella transazione globale possa essere completato in modo atomico ed è stato eseguito il rollback di tutto il lavoro nella transazione attiva in *Handle.*|  
|40001|Errore di serializzazione|È stato eseguito il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40002|Violazione dei vincoli di integrità|Il *CompletionType* è stato SQL_COMMIT e l'impegno delle modifiche ha causato la violazione del vincolo di integrità. Di conseguenza, è stato eseguito il rollback della transazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*szMessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *ConnectionHandle*. La funzione è stata chiamata e prima del termine dell'esecuzione della [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) è stata chiamata su *ConnectionHandle*. Quindi la funzione è stata chiamata nuovamente su *ConnectionHandle*.<br /><br /> La funzione è stata chiamata e prima del termine dell'esecuzione di **SQLCancelHandle** è stata chiamata su *ConnectionHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) una funzione in modo asincrono in esecuzione è stata chiamata per un handle di istruzione associato il *ConnectionHandle* ed era ancora in esecuzione quando **SQLEndTran** è stato chiamato.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *ConnectionHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per un handle di istruzione associato a *ConnectionHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per *l'handle* con *HandleType* impostato su SQL_HANDLE_DBC ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per uno degli handle di istruzione associati a *Handle* e SQL_PARAM_DATA_AVAILABLE restituito. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.|  
|HY012|Codice operazione transazione non valido|(DM) il valore specificato per l'argomento *CompletionType* non è SQL_COMMIT né SQL_ROLLBACK.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo/opzione non valido|(DM) il valore specificato per l'argomento *HandleType* non è né SQL_HANDLE_ENV né SQL_HANDLE_DBC.|  
|HY115|SQLEndTran non è consentito per un ambiente che contiene una connessione con l'esecuzione di funzioni asincrone abilitata|(DM) *HandleType* non può essere impostato su SQL_HANDLE_ENV se l'esecuzione asincrona delle funzioni di connessione è abilitata per una connessione nell'ambiente.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, fare riferimento alla sezione Commenti di questo argomento.|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il driver o l'origine dati non supporta l'operazione **ROLLBACK.**|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) Il driver associato a *ConnectionHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 Per un ODBC 3. *x* driver, se *HandleType* è SQL_HANDLE_ENV e *Handle* è un handle di ambiente valido, quindi gestione Driver chiamerà **SQLEndTran** in ogni driver associato all'ambiente. Il *Handle* argomento per la chiamata a un driver sarà l'handle di ambiente del driver. Per un ODBC 2. *x* driver, se *HandleType* è SQL_HANDLE_ENV e *Handle* è un handle di ambiente valido e sono presenti più connessioni in uno stato connesso in tale ambiente, quindi Gestione Driver chiamerà **SQLTransact** nel driver una volta per ogni connessione in uno stato connesso in tale ambiente. Il *Handle* argomento in ogni chiamata sarà l'handle della connessione. In entrambi i casi, il driver tenterà di eseguire il commit o il rollback delle transazioni, a seconda del valore di *CompletionType*, su tutte le connessioni che si trovano in uno stato connesso in tale ambiente. Le connessioni non attive non influiscono sulla transazione.  
  
> [!NOTE]  
>  **Impossibile utilizzare SQLEndTran** per eseguire il commit o il rollback delle transazioni in un ambiente condiviso. SQLSTATE HY092 (Identificatore di attributo/opzione non valido) verrà restituito se **SQLEndTran** viene chiamato con *Handle* impostato sull'handle di un ambiente condiviso o l'handle di una connessione in un ambiente condiviso.  
  
 Gestione Driver restituirà SQL_SUCCESS solo se riceve SQL_SUCCESS per ogni connessione. Se Gestione Driver riceve SQL_ERROR su una o più connessioni, restituisce SQL_ERROR all'applicazione e le informazioni di diagnostica vengono inserite nella struttura di dati di diagnostica dell'ambiente. Per determinare quale connessione o connessioni non è riuscita durante l'operazione di commit o rollback, l'applicazione può chiamare **SQLGetDiagRec** per ogni connessione.  
  
> [!NOTE]  
>  Gestione Driver non simula una transazione globale in tutte le connessioni e pertanto non utilizza protocolli di commit in due fasi.  
  
 Se *CompletionType* è SQL_COMMIT, **SQLEndTran** invia una richiesta di commit per tutte le operazioni attive su qualsiasi istruzione associata a una connessione interessata. Se *CompletionType* è SQL_ROLLBACK, **SQLEndTran** genera una richiesta di rollback per tutte le operazioni attive su qualsiasi istruzione associata a una connessione interessata. Se nessuna transazione è attiva, **SQLEndTran** restituisce SQL_SUCCESS senza alcun effetto sulle origini dati. Per ulteriori informazioni, vedere [Commit e rollback delle transazioni](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md).  
  
 Se il driver è in modalità di commit manuale (chiamando **SQLSetConnectAttr** con l'attributo SQL_ATTR_AUTOCOMMIT impostato su SQL_AUTOCOMMIT_OFF), viene avviata in modo implicito una nuova transazione quando un'istruzione SQL che può essere contenuta all'interno di una transazione viene eseguita sull'origine dati corrente. Per ulteriori informazioni, vedere [Modalità commit](../../../odbc/reference/develop-app/commit-mode.md).  
  
 Per determinare il modo in cui le operazioni sulle transazioni influiscono sui cursori, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CURSOR_ROLLBACK_BEHAVIOR e SQL_CURSOR_COMMIT_BEHAVIOR. Per ulteriori informazioni, vedere i paragrafi seguenti e vedere anche [Effetto delle transazioni sui cursori e](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)sulle istruzioni preparate .  
  
 Se il valore SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR è uguale a SQL_CB_DELETE, **SQLEndTran** chiude ed elimina tutti i cursori aperti in tutte le istruzioni associate alla connessione ed elimina tutti i risultati in sospeso. **SQLEndTran** lascia qualsiasi istruzione presente in uno stato allocato (non preparato); l'applicazione può riutilizzarli per le richieste SQL successive o può chiamare **SQLFreeStmt** o **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_STMT per deallocarle.  
  
 Se il valore SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR è uguale a SQL_CB_CLOSE, **SQLEndTran** chiude tutti i cursori aperti in tutte le istruzioni associate alla connessione. **SQLEndTran** lascia qualsiasi istruzione presente in uno stato preparato; l'applicazione può chiamare **SQLExecute** per un'istruzione associata alla connessione senza prima chiamare **SQLPrepare**.  
  
 Se il valore SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR è uguale a SQL_CB_PRESERVE, **SQLEndTran** non influisce sui cursori aperti associati alla connessione. I cursori rimangono nella riga a cui puntavano prima della chiamata a **SQLEndTran**.  
  
 Per i driver e le origini dati che supportano le transazioni, la chiamata a **SQLEndTran** con SQL_COMMIT o SQL_ROLLBACK quando non è attiva alcuna transazione restituisce SQL_SUCCESS (che indica che non è presente alcun acheta eseguire il commit o il rollback) e non ha alcun effetto sull'origine dati.  
  
 Quando un driver è in modalità autocommit, Gestione Driver non chiama **SQLEndTran** nel driver. **SQLEndTran** restituisce sempre SQL_SUCCESS indipendentemente dal fatto che venga chiamato con un *CompletionType* di SQL_COMMIT o SQL_ROLLBACK.  
  
 I driver o le origini dati che non supportano le transazioni (l'opzione**SQLGetInfo** *option* SQL_TXN_CAPABLE è SQL_TC_NONE) sono in effetti sempre in modalità autocommit e pertanto restituiscono sempre SQL_SUCCESS per **SQLEndTran** indipendentemente dal fatto che vengano chiamati con un *CompletionType* di SQL_COMMIT o SQL_ROLLBACK. Tali driver e origini dati non eseguono effettivamente il rollback delle transazioni quando richiesto.  
  
## <a name="suspended-state"></a>Stato sospeso  
 In Gestione driver che sono stati rilasciati prima di Windows 7, una transazione era attiva se **SQLEndTran** restituito SQL_ERROR dal driver. Tuttavia, era possibile che la transazione sia stata eseguito correttamente il commit sul server, ma il driver sul client non è stato notificato (ad esempio, perché si è verificato un errore di rete). Ciò lascerebbe la connessione in uno stato non valido. A partire da Windows 7, quando **SQLEndTran** restituisce SQL_ERROR, la connessione potrebbe essere in uno stato sospeso. In uno stato sospeso, è possibile chiamare funzioni di sola lettura. Infine, l'applicazione deve chiamare **SQLDisconnect** su una connessione sospesa per rilasciare le risorse.  
  
 Se tutte le condizioni seguenti sono vere, la connessione verrà messa in uno stato sospeso:If all of the following conditions are true, the connection will be put into a suspended state:  
  
-   Il driver restituisce SQL_ERROR da **SQLEndTran**.  
  
-   Il driver è ODBC versione 3.8 o successiva.  
  
-   La versione dell'applicazione è 3.8 o successiva; oppure l'applicazione ODBC 2.x o 3.x ricompilata annulla correttamente la funzione **SQLEndTran** tramite **SQLCancelHandle**.  
  
-   Il driver non ha restituito uno dei seguenti messaggi, che confermano che la transazione non è stata completata:  
  
    -   25S03: viene eseguito il rollback della transazione  
  
    -   40001: Errore di serializzazione  
  
    -   40002: vincolo di integrità  
  
    -   HYC00: funzionalità facoltativa non implementata  
  
 Se **SQLEndTran** è stato chiamato su un handle di ambiente e una delle relative connessioni ha soddisfatto le condizioni precedenti, tutte le connessioni che si connettono allo stesso driver verranno messe nello stato sospeso.  
  
 Dopo che un'applicazione chiama **SQLDisconnect** su una connessione sospesa, la connessione può essere utilizzata per riconnettersi a un'altra origine dati o alla stessa origine dati.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Annullamento di una funzione in esecuzione in modo asincrono su un handle di connessione.|[Funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Restituzione di informazioni su un driver o un'origine datiReturning information about a driver or data source|[Funzione SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Liberare una maniglia|[SQLFreeHandle Function](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Liberare un handle di istruzioneFreeing a statement handle|[Funzione SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Esecuzione asincrona (metodo di polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
