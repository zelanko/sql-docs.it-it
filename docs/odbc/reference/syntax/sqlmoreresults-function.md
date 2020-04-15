---
title: Funzione SQLMoreResults . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLMoreResults
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLMoreResults
helpviewer_keywords:
- SQLMoreResults function [ODBC]
ms.assetid: bf169ed5-4d55-412c-b184-12065a726e89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78bbb277e4b783eb46c79f59939a1080feae2b60
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304742"
---
# <a name="sqlmoreresults-function"></a>Funzione SQLMoreResults
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLMoreResults** determina se sono disponibili più risultati in un'istruzione contenente istruzioni **SELECT**, **UPDATE**, **INSERT**o **DELETE** e, in caso affermativo, inizializza l'elaborazione per tali risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE, OR SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLMoreResults** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLMoreResults** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S02 (in questo stato di|Il valore dell'opzione è cambiato|Valore di un attributo di istruzione modificato durante l'elaborazione del batch. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|40001|Errore di serializzazione|È stato eseguito il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione **SQLMoreResults** è stata chiamata e, prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*. Quindi la funzione **SQLMoreResults** è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione **SQLMoreResults** è stata chiamata e, prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLMoreResults.This** asynchronous function was still executing when the SQLMoreResults function was called.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **Le** istruzioni SELECT restituiscono set di risultati. **Le**istruzioni UPDATE , **INSERT**e **DELETE** restituiscono un conteggio delle righe interessate. Se una di queste istruzioni viene raggruppata in batch, inviata con matrici di parametri (numerate in ordine crescente di parametri, nell'ordine in cui vengono visualizzate nel batch) o nelle procedure, possono restituire più set di risultati o conteggi di righe. Per informazioni sui batch di istruzioni e matrici di parametri, vedere [Batch di istruzioni SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md) e matrici di valori di [parametro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Dopo l'esecuzione del batch, l'applicazione viene posizionata sul primo set di risultati. L'applicazione può chiamare **SQLBindCol**, **SQLBulkOperations**, **SQLFetch**, **SQLGetData**, **SQLFetchScroll**, **SQLSetPos**e tutte le funzioni di metadati, nel primo o in qualsiasi set di risultati successivi, come se fosse presente un solo set di risultati. Al termine dell'operazione con il primo set di risultati, l'applicazione chiama **SQLMoreResults** per passare al set di risultati successivo. Se è disponibile un altro set di risultati o un altro conteggio, **SQLMoreResults** restituisce SQL_SUCCESS e inizializza il set di risultati o il conteggio per un'ulteriore elaborazione. Se tra le istruzioni che generano set di risultati vengono visualizzate istruzioni che generano conteggio righe, è possibile eseguire il decontrollo di tali istruzioni chiamando **SQLMoreResults**. Dopo aver chiamato **SQLMoreResults** per le istruzioni **UPDATE**, **INSERT**o **DELETE,** un'applicazione può chiamare **SQLRowCount**.  
  
 Se è presente un set di risultati corrente con righe non recuperate, **SQLMoreResults** elimina il set di risultati e rende disponibile il set di risultati o il conteggio successivo. Se tutti i risultati sono stati elaborati, **SQLMoreResults** restituisce SQL_NO_DATA. Per alcuni driver, i parametri di output e i valori restituiti non sono disponibili fino a quando non sono stati elaborati tutti i set di risultati e i conteggi delle righe. Per tali driver, i parametri di output e i valori restituiti diventano disponibili quando **SQLMoreResults** restituisce SQL_NO_DATA.  
  
 Tutte le associazioni stabilite per il set di risultati precedente rimangono ancora valide. Se le strutture di colonne sono diverse per questo set di risultati, la chiamata a **SQLFetch** o **SQLFetchScroll** può causare un errore o un troncamento. Per evitare questo problema, l'applicazione deve chiamare **SQLBindCol** per riassociare in modo esplicito come appropriato (o farlo impostando i campi del descrittore). In alternativa, l'applicazione può chiamare **SQLFreeStmt** con *un'opzione* di SQL_UNBIND per annullare l'associazione di tutti i buffer di colonna.  
  
 I valori degli attributi dell'istruzione, ad esempio il tipo di cursore, la concorrenza del cursore, la dimensione del keyset o la lunghezza massima, possono cambiare quando l'applicazione si sposta nel batch mediante chiamate a **SQLMoreResults**. In questo caso, **SQLMoreResults** restituirà SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (il valore dell'opzione è stato modificato).  
  
 La chiamata a **SQLCloseCursor**o **SQLFreeStmt** con un'opzione di SQL_CLOSE, elimina tutti i set di risultati e i conteggi di righe disponibili in seguito all'esecuzione del batch. *Option* L'handle dell'istruzione torna allo stato allocato o preparato. La chiamata a **SQLCancel** per annullare una funzione in modo asincrono quando un batch è stato eseguito e l'handle dell'istruzione è nello stato eseguito, posizionato nel cursore o asincrono determina che tutti i set di risultati e i conteggi delle righe generati dal batch vengano eliminati se la chiamata di annullamento ha avuto esito positivo. L'istruzione torna quindi allo stato preparato o allocato.  
  
 Se un batch di istruzioni o una routine combina altre istruzioni SQL con istruzioni **SELECT**, **UPDATE**, **INSERT**e **DELETE,** queste altre istruzioni non influiscono su **SQLMoreResults**.  
  
 Per ulteriori informazioni, vedere [Risultati multipli](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Se un'istruzione di aggiornamento, inserimento o eliminazione in un batch di istruzioni non influisce sulle righe dell'origine dati, **SQLMoreResults** restituisce SQL_SUCCESS. Questo comportamento è diverso dal caso di un'istruzione di aggiornamento, inserimento o eliminazione eseguita tramite **SQLExecDirect**, **SQLExecute**o **SQLParamData**, che restituisce SQL_NO_DATA se non influisce su alcuna riga dell'origine dati. Se un'applicazione chiama **SQLRowCount** per recuperare il conteggio delle righe dopo una chiamata a **SQLMoreResults** non ha interessato alcuna riga, **SQLRowCount** restituirà SQL_NO_DATA.  
  
 Per ulteriori informazioni sulla sequenza valida delle funzioni di elaborazione dei risultati, vedere [Appendice B: Tabelle](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)di transizione dello stato ODBC .  
  
 Per ulteriori informazioni sui parametri di output SQL_PARAM_DATA_AVAILABLE e trasmessi, vedere Recupero di parametri di [output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="availability-of-row-counts"></a>Disponibilità dei conteggi delle righe  
 Quando un batch contiene più istruzioni di generazione di conteggio righe consecutive, è possibile che questi conteggi di righe vengano raggruppati in un solo conteggio di righe. Ad esempio, se un batch dispone di cinque istruzioni di inserimento, alcune origini dati sono in grado di restituire cinque conteggi di righe individuali. Alcune altre origini dati restituiscono un solo conteggio di righe che rappresenta la somma dei cinque conteggi di righe individuali.  
  
 Quando un batch contiene una combinazione di istruzioni che generano set di risultati e di generazione di conteggi delle righe, i conteggi delle righe possono essere o meno disponibili. Il comportamento del driver rispetto alla disponibilità dei conteggi di righe viene enumerato nel tipo di informazioni SQL_BATCH_ROW_COUNT disponibile tramite una chiamata a **SQLGetInfo**. Si supponga, ad esempio, che il batch contenga **un'istruzione SELECT**, seguita da due **INSERT**s e un'altra **istruzione SELECT**. Sono quindi possibili i seguenti casi:  
  
-   I conteggi di riga corrispondenti alle due istruzioni **INSERT** non sono disponibili affatto. La prima chiamata a **SQLMoreResults** verrà posizionato sul set di risultati della seconda istruzione **SELECT.**  
  
-   I conteggi di riga corrispondenti alle due istruzioni **INSERT** sono disponibili singolarmente. Una chiamata a **SQLGetInfo** non restituisce il bit di SQL_BRC_ROLLED_UP per il tipo di informazioni SQL_BATCH_ROW_COUNT. La prima chiamata a **SQLMoreResults** posizionerà l'utente in base al conteggio delle righe della prima **istruzione INSERT**e la seconda chiamata verrà posizionata sul conteggio delle righe del secondo **file INSERT**. La terza chiamata a **SQLMoreResults** posizionerà l'utente sul set di risultati della seconda istruzione **SELECT.**  
  
-   I conteggi di riga **corrispondenti ai** due inserimenti vengono raggruppati in un numero di righe singolo disponibile. Una chiamata a **SQLGetInfo** restituisce il bit di SQL_BRC_ROLLED_UP per il tipo di informazioni SQL_BATCH_ROW_COUNT. La prima chiamata a **SQLMoreResults** verrà posizionata sul conteggio delle righe di rollup e la seconda chiamata a **SQLMoreResults** verrà posizionata sul set di risultati del secondo **SELECT**.  
  
 Alcuni driver rendono i conteggi delle righe disponibili solo per i batch espliciti e non per le stored procedure.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Recupero di un blocco di dati o scorrimento di un set di risultati|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Recupero di una singola riga o di un blocco di dati in una direzione forward-only|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Recupero di parte o di tutta una colonna di dati|[Funzione SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recupero di parametri di output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
