---
title: 'Funzione SQLExtendedFetch : Documenti Microsoft'
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc832e5a20b1d3c0a1ad63b3e2a070563de2b46d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285981"
---
# <a name="sqlextendedfetch-function"></a>Funzione SQLExtendedFetch
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: Deprecated  
  
 **Riepilogo**  
 **SQLExtendedFetch** recupera il set di righe specificato di dati dal set di risultati e restituisce i dati per tutte le colonne associate. I set di righe possono essere specificati in una posizione assoluta o relativa o in base al segnalibro.  
  
> [!NOTE]
>  In ODBC 3 *.x*, **SQLExtendedFetch** è stato sostituito da **SQLFetchScroll**. Le applicazioni *.x* ODBC 3 non devono chiamare **SQLExtendedFetch**; devono invece chiamare **SQLFetchScroll**. Gestione Driver esegue il mapping **di SQLFetchScroll** a **SQLExtendedFetch** quando si lavora con un driver *.x* ODBC 2. I driver*x* di ODBC 3 devono supportare **SQLExtendedFetch** se desiderano lavorare con le applicazioni *.x* ODBC 2 che lo chiamano. Per ulteriori informazioni, vedere "Commenti" e Cursori a [blocchi, Cursori scorrevoli e Compatibilità con](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) le versioni precedenti nell'Appendice G: Linee guida per i driver per la compatibilità con le versioni precedenti.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLExtendedFetch(  
      SQLHSTMT         StatementHandle,  
      SQLUSMALLINT     FetchOrientation,  
      SQLLEN           FetchOffset,  
      SQLULEN *        RowCountPtr,  
      SQLUSMALLINT *   RowStatusArray);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *Orientamento Fetch*  
 [Ingresso] Tipo di recupero. Equivale a *FetchOrientation* in **SQLFetchScroll**.  
  
 *RecuperaOffset*  
 [Ingresso] Numero della riga da recuperare. Equivale a *FetchOffset* in **SQLFetchScroll**, con un'eccezione. Quando *FetchOrientation* è SQL_FETCH_BOOKMARK, *FetchOffset* è un segnalibro a lunghezza fissa, non un offset da un segnalibro. In altre parole, **SQLExtendedFetch** recupera il segnalibro da questo argomento, non l'attributo dell'istruzione SQL_ATTR_FETCH_BOOKMARK_PTR. Non supporta i segnalibri di lunghezza variabile e non supporta il recupero di un set di righe in corrispondenza di un offset (diverso da 0) da un segnalibro.  
  
 *RowCountPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero di righe effettivamente recuperate. Questo buffer viene utilizzato nello stesso modo in cui viene utilizzato il buffer specificato dall'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR. Questo buffer viene utilizzato solo da **SQLExtendedFetch**. Non viene utilizzato da **SQLFetch** o **SQLFetchScroll**.  
  
 *RowStatusArray*  
 [Uscita] Puntatore a una matrice in cui restituire lo stato di ogni riga. Questa matrice viene utilizzata nello stesso modo della matrice specificata dall'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR.  
  
 Tuttavia, l'indirizzo di questa matrice non viene memorizzato nel campo SQL_DESC_STATUS_ARRAY_PTR nell'IRD. Inoltre, questa matrice viene utilizzata solo da **SQLExtendedFetch** e da **SQLBulkOperations** con *un'operazione* di SQL_ADD o **SQLSetPos** quando viene chiamato dopo **SQLExtendedFetch**. Non viene utilizzato da **SQLFetch** o **SQLFetchScroll**e non viene utilizzato da **SQLBulkOperations** o **SQLSetPos** quando vengono chiamati dopo **SQLFetch** o **SQLFetchScroll**. Inoltre, non viene utilizzato quando **SQLBulkOperations** con *un'operazione* di SQL_ADD viene chiamato prima che venga chiamata qualsiasi funzione di recupero. In altre parole, viene utilizzato solo nello stato di istruzione S7. Non viene utilizzato negli stati di istruzione S5 o S6. Per ulteriori informazioni, vedere [Transizioni](../../../odbc/reference/appendixes/statement-transitions.md) di istruzioni nell'Appendice B: tabelle di transizione dello stato ODBC.  
  
 Le applicazioni devono fornire un puntatore valido nell'argomento *RowStatusArray.* in caso contrario, il comportamento di **SQLExtendedFetch** e il comportamento delle chiamate a **SQLBulkOperations** o **SQLSetPos** dopo che un cursore è stato posizionato da **SQLExtendedFetch** non sono definiti.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLExtendedFetch** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLError**. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLExtendedFetch** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente. Se si verifica un errore in una singola colonna, **SQLGetDiagField** può essere chiamato con un *DiagIdentifier* di SQL_DIAG_COLUMN_NUMBER per determinare la colonna in cui si è verificato l'errore; e **SQLGetDiagField** può essere chiamato con un *DiagIdentifier* di SQL_DIAG_ROW_NUMBER per determinare la riga contenente tale colonna.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Dati stringa o binari restituiti per una colonna hanno determinato il troncamento di caratteri non vuoti o dati binari non NULL. Se si tratta di un valore stringa, è stato troncato a destra. Se si tratta di un valore numerico, la parte frazionaria del numero è stata troncata.  (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S01 (in questo stato di|Errore nella riga|Si è verificato un errore durante il recupero di una o più righe. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S06 (in inglese)|Tentativo di recupero prima che il set di risultati restituisca il primo set di righe|Il set di righe richiesto si sovrapponeva all'inizio del set di risultati quando la posizione corrente era oltre la prima riga e *FetchOrientation* era SQL_PRIOR o *FetchOrientation* era SQL_RELATIVE con un *FetchOffset* negativo il cui valore assoluto era minore o uguale al SQL_ROWSET_SIZE corrente. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S07 (intito)|Troncamento frazionario|I dati restituiti per una colonna sono stati troncati. Per i tipi di dati numerici, la parte frazionaria del numero è stata troncata. Per i tipi di dati time, timestamp e interval contenenti un componente time, la parte frazionaria dell'ora è stata troncata.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07006|Violazione dell'attributo del tipo di dati con restrizioniRestricted data type attribute violation|Impossibile convertire un valore di dati nel tipo di dati C specificato da *TargetType* in **SQLBindCol**.|  
|07009|Indice descrittore non valido|La colonna 0 è stata associata a **SQLBindCol**e l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_OFF.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|22002|Variabile indicatore richiesta ma non fornita|I dati NULL sono stati recuperati in una colonna il cui *StrLen_or_IndPtr* impostato da **SQLBindCol** era un puntatore null.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|22003|Valore numerico non compreso nell'intervallo|La restituzione del valore numerico (come numerico o stringa) per una o più colonne avrebbe causato il troncamento dell'intera parte (anziché frazionaria) del numero.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)<br /><br /> Per altre informazioni, vedere Linee guida per i tipi di [dati numerici e di intervallo](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) nell'Appendice D: Tipi di dati.|  
|22007|Formato datetime non valido|Una colonna di caratteri nel set di risultati è stata associata a una data, ora o timestamp C struttura e un valore nella colonna è stato, rispettivamente, una data, ora o timestamp non valido.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|22012|Divisione per zero|È stato restituito un valore da un'espressione aritmetica, che ha restituito la divisione per zero.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|22015|Overflow campo intervallo|L'assegnazione da un tipo SQL esatto numero o intervallo a un tipo di intervallo C ha causato una perdita di cifre significative nel campo iniziale.<br /><br /> Durante il recupero dei dati in un tipo di intervallo C, non esisteva alcuna rappresentazione del valore del tipo SQL nel tipo di intervallo C.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|22018|Valore di carattere non valido per la specifica del cast|Il tipo C era un numero esatto o approssimativo, un datetime o un tipo di dati interval; il tipo SQL della colonna era un tipo di dati carattere; e il valore nella colonna non è un valore letterale valido del tipo C associato.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|24000|Stato del cursore non valido|*StatementHandle* era in uno stato eseguito, ma a *StatementHandle*non è stato associato alcun set di risultati .|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLError** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*, quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLExtendedFetch.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) *L'oggetto statementHandle* specificato non era in uno stato eseguito. La funzione è stata chiamata senza prima chiamare **SQLExecDirect**, **SQLExecute**o una funzione di catalogo.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) **SQLExtendedFetch** è stato chiamato per il *StatementHandle* dopo **SQLFetch** o **SQLFetchScroll** è stato chiamato e prima **SQLFreeStmt** è stato chiamato con l'opzione SQL_CLOSE.<br /><br /> (DM) **SQLBulkOperations** è stato chiamato per un'istruzione prima **sqlFetch**, **SQLFetchScroll**, o **SQLExtendedFetch** è stato chiamato e quindi **SQLExtendedFetch** è stato chiamato prima **SQLFreeStmt** è stato chiamato con l'opzione SQL_CLOSE.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I106|Tipo di recupero non compreso nell'intervallo|(DM) il valore specificato per l'argomento *FetchOrientation* non è valido. (Vedere "Commenti").")<br /><br /> L'argomento *FetchOrientation* è stato SQL_FETCH_BOOKMARK e l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_OFF.<br /><br /> Il valore dell'opzione di istruzione SQL_CURSOR_TYPE è stato SQL_CURSOR_FORWARD_ONLY e il valore dell'argomento *FetchOrientation* non è SQL_FETCH_NEXT.<br /><br /> L'argomento *FetchOrientation* è stato SQL_FETCH_RESUME.|  
|I107|Valore di riga non compreso nell'intervallo|Il valore specificato con l'opzione SQL_CURSOR_TYPE'istruzione è stato SQL_CURSOR_KEYSET_DRIVEN, ma il valore specificato con l'attributo dell'istruzione SQL_KEYSET_SIZE è maggiore di 0 e minore del valore specificato con l'attributo di istruzione SQL_ROWSET_SIZE.|  
|HY111|Valore segnalibro non valido|L'argomento *FetchOrientation* è stato SQL_FETCH_BOOKMARK e il segnalibro specificato nell'argomento *FetchOffset* non è valido.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il driver o l'origine dati non supporta il tipo di recupero specificato.<br /><br /> Il driver o l'origine dati non supporta la conversione specificata dalla combinazione di *TargetType* in **SQLBindCol** e il tipo di dati SQL della colonna corrispondente. Questo errore si applica solo quando il tipo di dati SQL della colonna è stato mappato a un tipo di dati SQL specifico del driver.|  
|HYT00|Timeout|Il periodo di timeout della query è scaduto prima che l'origine dati restituisca il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtOption**, SQL_QUERY_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Il comportamento di **SQLExtendedFetch** è identico a quello di **SQLFetchScroll**, con le seguenti eccezioni:  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** utilizzano metodi diversi per restituire il numero di righe recuperate. **SQLExtendedFetch** restituisce il numero di righe recuperate in * \*RowCountPtr*; **SQLFetchScroll** restituisce il numero di righe recuperate direttamente nel buffer a cui punta SQL_ATTR_ROWS_FETCHED_PTR. Per altre informazioni, vedere l'argomento *RowCountPtr.For* more information, see the RowCountPtr argument.  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** restituiscono lo stato di ogni riga in matrici diverse. Per altre informazioni, vedere l'argomento *RowStatusArray.For* more information, see the RowStatusArray argument.  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** utilizzano metodi diversi per recuperare il segnalibro quando *FetchOrientation* è SQL_FETCH_BOOKMARK. **SQLExtendedFetch** non supporta i segnalibri di lunghezza variabile o il recupero di set di righe in corrispondenza di un offset diverso da 0 da un segnalibro. Per altre informazioni, vedere il *FetchOffset* argomento.  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** utilizzano dimensioni di set di righe diverse. **SQLExtendedFetch** utilizza il valore dell'attributo di istruzione SQL_ROWSET_SIZE e **SQLFetchScroll** utilizza il valore dell'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE.  
  
-   **SQLExtendedFetch** ha una semantica di gestione degli errori leggermente diversa rispetto a **SQLFetchScroll**. Per ulteriori informazioni, vedere "Gestione degli errori" nella sezione "Commenti" di [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
-   **SQLExtendedFetch** non supporta gli offset di associazione (l'attributo dell'istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR).  
  
-   Le chiamate a **SQLExtendedFetch** non possono essere mismigiate con chiamate a **SQLFetch** o **SQLFetchScroll**e se **SQLBulkOperations** viene chiamato prima che venga chiamata qualsiasi funzione di recupero, **SQLExtendedFetch** non può essere chiamato fino a quando il cursore non viene chiuso e riaperto. Ovvero, **SQLExtendedFetch** può essere chiamato solo nello stato di istruzione S7. Per ulteriori informazioni, vedere [Transizioni](../../../odbc/reference/appendixes/statement-transitions.md) di istruzioni nell'Appendice B: tabelle di transizione dello stato ODBC.  
  
 Quando un'applicazione chiama **SQLFetchScroll** durante l'utilizzo di un driver *.x* ODBC 2, Gestione Driver esegue il mapping di questa chiamata a **SQLExtendedFetch**. Per ulteriori informazioni, vedere "SQLFetchScroll e ODBC 2 *.x* Drivers" in [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 In ODBC 2 *.x*, **SQLExtendedFetch** è stato chiamato per recuperare più righe e **SQLFetch** è stato chiamato per recuperare una singola riga. In ODBC 3 *.x*, d'altra parte, **SQLFetch** può essere chiamato per recuperare più righe.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Esecuzione di operazioni di inserimento, aggiornamento o eliminazione bulk|[Funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di informazioni su una colonna in un set di risultatiReturning information about a column in a result set|[Funzione SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Restituzione del numero di colonne del set di risultatiReturning the number of result set columns|[Funzione SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Posizionamento del cursore, aggiornamento dei dati nel set di righe o aggiornamento o eliminazione di dati nel set di risultati|[Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Impostazione di un attributo di istruzioneSetting a statement attribute|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
