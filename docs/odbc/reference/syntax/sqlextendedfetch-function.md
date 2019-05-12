---
title: Funzione SQLExtendedFetch | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63030b34e4b607b850f25a67357d62a7184467c8
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537190"
---
# <a name="sqlextendedfetch-function"></a>Funzione SQLExtendedFetch
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: Deprecato  
  
 **Riepilogo**  
 **SQLExtendedFetch** recupera il set di righe specificato dei dati dal set di risultati e restituisce i dati per tutte le colonne associate. I set di righe può essere specificato in una posizione assoluta o relativa o dal segnalibro.  
  
> [!NOTE]
>  In ODBC 3 *. x*, **SQLExtendedFetch** è stata sostituita da **SQLFetchScroll**. ODBC 3 *. x* le applicazioni non devono chiamare **SQLExtendedFetch**; invece di chiamare **SQLFetchScroll**. Esegue il mapping di gestione Driver **SQLFetchScroll** al **SQLExtendedFetch** quando si lavora con un 2 ODBC*x* driver. ODBC 3 *. x* i driver devono supportare **SQLExtendedFetch** se vogliono lavorare con l'API ODBC 2*x* le applicazioni che lo chiamano. Per altre informazioni, vedere "Commenti" e [cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) nell'appendice g: Driver linee guida per la compatibilità con le versioni precedenti.  
  
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
 [Input] Handle di istruzione.  
  
 *FetchOrientation*  
 [Input] Tipo di operazione di recupero. Ciò equivale *FetchOrientation* nelle **SQLFetchScroll**.  
  
 *FetchOffset*  
 [Input] Numero di riga da recuperare. Ciò equivale *FetchOffset* nelle **SQLFetchScroll**, con un'eccezione. Quando *FetchOrientation* è impostato su SQL_FETCH_BOOKMARK, *FetchOffset* è un segnalibro a lunghezza fissa, non un offset dal segnalibro. In altre parole, **SQLExtendedFetch** recupera il segnalibro da questo argomento, non l'attributo di istruzione SQL_ATTR_FETCH_BOOKMARK_PTR. Non supporta i segnalibri di lunghezza variabile e non supporta il recupero di un set di righe in un offset (diverso da 0) da un segnalibro.  
  
 *RowCountPtr*  
 [Output] Puntatore a un buffer in cui restituire il numero di righe effettivamente recuperate. Questo buffer viene usato nello stesso modo del buffer specificato dall'attributo SQL_ATTR_ROWS_FETCHED_PTR istruzione. Questo buffer viene utilizzato solo dai **SQLExtendedFetch**. Non viene usato dal **SQLFetch** oppure **SQLFetchScroll**.  
  
 *RowStatusArray*  
 [Output] Puntatore a una matrice in cui restituire lo stato di ogni riga. Questa matrice viene usata nello stesso modo della matrice specificata dall'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR.  
  
 Tuttavia, l'indirizzo di questa matrice non viene archiviato nel campo SQL_DESC_STATUS_ARRAY_PTR nell'implementazione. Inoltre, questa matrice viene usata solo dai **SQLExtendedFetch** e dai **SQLBulkOperations** con un *operazione* di SQL_ADD o **SQLSetPos**quando viene chiamato dopo **SQLExtendedFetch**. Non viene usato dal **SQLFetch** o **SQLFetchScroll**, e non viene usato dal **SQLBulkOperations** oppure **SQLSetPos** quando vengono chiamati dopo **SQLFetch** oppure **SQLFetchScroll**. Non è inoltre usata quando **SQLBulkOperations** con un *operazione* di SQL_ADD viene chiamato prima di chiamare qualsiasi funzione di recupero. In altre parole, viene usato solo stavu istruzione S7. Non è utilizzato negli Stati di istruzione S5 o S6. Per altre informazioni, vedere [transizioni di istruzione](../../../odbc/reference/appendixes/statement-transitions.md) nell'appendice b: Tabelle della transizione di stato ODBC.  
  
 Le applicazioni devono fornire un puntatore valido nel *RowStatusArray* argomento; in caso contrario, il comportamento di **SQLExtendedFetch** e il comportamento di chiamate a **SQLBulkOperations**oppure **SQLSetPos** dopo che un cursore è stato posizionato dal **SQLExtendedFetch** sono definiti.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLExtendedFetch** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato può essere ottenuto chiamando **SQLError**. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLExtendedFetch** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente. Se si verifica un errore in una singola colonna, **SQLGetDiagField** può essere chiamato con un *DiagIdentifier* di SQL_DIAG_COLUMN_NUMBER per determinare la colonna a cui si è verificato l'errore; e  **SQLGetDiagField** può essere chiamato con un *DiagIdentifier* di SQL_DIAG_ROW_NUMBER per determinare la riga contenente la colonna.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Stringa o dati binari restituiti per una colonna ha comportato il troncamento del carattere non vuote o dati binari non NULL. Se si tratta di un valore stringa, era troncati a destra. Se si tratta di un valore numerico, la parte frazionaria del numero è stata troncata.  (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01S01|Errore nella riga|Si è verificato un errore durante il recupero di una o più righe. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01S06|Tentativo di recupero prima che il set di risultati restituito il primo set di righe|Il set di righe richiesto sovrapposte l'inizio del set di risultati quando la posizione corrente è oltre la prima riga, sia *FetchOrientation* era SQL_PRIOR oppure *FetchOrientation* era SQL_RELATIVE con un negativa *FetchOffset* il cui valore assoluto era minore o uguale al SQL_ROWSET_SIZE corrente. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01S07|Troncamento frazionario.|I dati restituiti per una colonna è stati troncati. Per i tipi di dati numerici, la parte frazionaria del numero è stata troncata. Per ora, timestamp e tipi di dati di intervallo che contiene un componente della fase, la parte frazionaria del tempo sono stata troncata.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07006|Violazione dell'attributo del tipo di dati|Non è possibile convertire un valore di dati per il tipo di dati C specificato da *TargetType* nelle **SQLBindCol**.|  
|07009|Indice del descrittore non valido|Colonna 0 è stato associato **SQLBindCol**, e l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_OFF.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|22002|Variabile indicatore necessaria ma non fornito|I dati NULL è stati recuperati in una colonna la cui proprietà *StrLen_or_IndPtr* effettui **SQLBindCol** era un puntatore null.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|22003|Valore numerico non compreso nell'intervallo|Restituzione del valore numerico (come valore numerico o stringa) per una o più colonne avrebbe causato la parte intera (in contrapposizione frazionari) del numero da troncare.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).<br /><br /> Per altre informazioni, vedere [linee guida per l'intervallo e tipi di dati numerici](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) nell'appendice d: Tipi di dati.|  
|22007|Formato di datetime non valido|Una colonna di tipo carattere nel set di risultati è stata associata a una data, ora o timestamp C struttura e un valore nella colonna non è, rispettivamente, una data non valida, ora o timestamp.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|22012|Divisione per zero|Un valore da un'espressione aritmetica è stato restituito, ciò ha provocato la divisione per zero.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|22015|Overflow del campo Interval|Assegnazione da un numerico esatto o l'intervallo di tipo SQL a un tipo di intervallo C, ha causato una perdita di cifre significative nel campo iniziale.<br /><br /> Durante il recupero di dati a un tipo di intervallo C, si è verificato alcun rappresentazione del valore del tipo SQL nel tipo di intervallo C.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|22018|Valore del carattere non valido per la specifica del cast|Il tipo C è un valore numerico esatto o approssimativo, un valore datetime o un tipo di dati di intervallo; il tipo SQL della colonna è un tipo di dati carattere. e il valore nella colonna non è un valore letterale valido del tipo C associato.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|24000|Stato del cursore non valido|Il *StatementHandle* era stato eseguito, ma è stato associato alcun set di risultati le *StatementHandle*.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLError** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle*, quindi è stata chiamata la funzione anche in questo caso sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLExtendedFetch** funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) specificato *StatementHandle* non è stato eseguito. La funzione è stata chiamata senza chiamare prima il metodo **SQLExecDirect**, **SQLExecute**, o una funzione di catalogo.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.<br /><br /> (DM) **SQLExtendedFetch** è stato chiamato per il *StatementHandle* dopo **SQLFetch** oppure **SQLFetchScroll** è stato chiamato e prima  **SQLFreeStmt** è stato chiamato con l'opzione di SQL_CLOSE.<br /><br /> (DM) **SQLBulkOperations** è stato chiamato per un'istruzione prima **SQLFetch**, **SQLFetchScroll**, oppure **SQLExtendedFetch** è stato chiamato, e quindi **SQLExtendedFetch** è stato chiamato prima **SQLFreeStmt** è stato chiamato con l'opzione di SQL_CLOSE.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY106|Tipo compreso nell'intervallo di recupero|(DM) il valore specificato per l'argomento *FetchOrientation* non è valido. (Vedere "Commenti".)<br /><br /> L'argomento *FetchOrientation* era impostato su SQL_FETCH_BOOKMARK, e l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_OFF.<br /><br /> Il valore dell'opzione istruzione SQL_CURSOR_TYPE era SQL_CURSOR_FORWARD_ONLY e il valore dell'argomento *FetchOrientation* non era SQL_FETCH_NEXT.<br /><br /> L'argomento *FetchOrientation* era SQL_FETCH_RESUME.|  
|HY107|Valore di riga non compreso nell'intervallo|Il valore specificato con l'opzione dell'istruzione SQL_CURSOR_TYPE SQL_CURSOR_KEYSET_DRIVEN, ma il valore specificato con l'attributo di istruzione SQL_KEYSET_SIZE stato maggiore di 0 e minore del valore specificato con l'attributo di istruzione SQL_ROWSET_SIZE .|  
|HY111|Valore di segnalibro non valido|L'argomento *FetchOrientation* era impostato su SQL_FETCH_BOOKMARK e il segnalibro specificato nella *FetchOffset* argomento non valido.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|Origine dati o driver non supporta il tipo di operazione di recupero specificato.<br /><br /> L'origine dati o driver non supporta la conversione specificata dalla combinazione dei *TargetType* nelle **SQLBindCol** e il tipo di dati SQL della colonna corrispondente. Questo errore si applica solo quando il tipo di dati SQL della colonna è stato eseguito il mapping a un tipo di dati specifici del driver SQL.|  
|HYT00|Timeout|Il periodo di timeout query scaduto prima che l'origine dati ha restituito il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtOption**, SQL_QUERY_TIMEOUT.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Il comportamento delle **SQLExtendedFetch** è identica a quella dei **SQLFetchScroll**, con le eccezioni seguenti:  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** usare diversi metodi per restituire il numero di righe recuperate. **SQLExtendedFetch** restituisce il numero di righe recuperate nel  *\*RowCountPtr*; **SQLFetchScroll** restituisce il numero di righe recuperate direttamente al buffer a cui punta SQL_ATTR_ROWS_FETCHED_PTR. Per altre informazioni, vedere la *RowCountPtr* argomento.  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** restituiscono lo stato di ogni riga in matrici di diverse. Per altre informazioni, vedere la *RowStatusArray* argomento.  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** usare diversi metodi per recuperare il segnalibro quando *FetchOrientation* è impostato su SQL_FETCH_BOOKMARK. **SQLExtendedFetch** non supporta a lunghezza variabile segnalibri o durante il recupero dei set di righe in un offset diverso da 0 da un segnalibro. Per altre informazioni, vedere la *FetchOffset* argomento.  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** usare dimensioni di diversi set di righe. **SQLExtendedFetch** Usa il valore dell'attributo di istruzione SQL_ROWSET_SIZE, e **SQLFetchScroll** Usa il valore dell'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE.  
  
-   **SQLExtendedFetch** ha una semantica di gestione degli errori leggermente diversa **SQLFetchScroll**. Per altre informazioni, vedere "Gestione degli errori" nella sezione "Commenti" del [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
-   **SQLExtendedFetch** non supporta offset di associazione (l'attributo dell'istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR).  
  
-   Le chiamate a **SQLExtendedFetch** ReadContentAsBase64 e ReadContentAsBinHex con chiamate al **SQLFetch** oppure **SQLFetchScroll**e se **SQLBulkOperations** viene chiamato prima di chiamare qualsiasi funzione di recupero, **SQLExtendedFetch** non può essere chiamato fino a quando il cursore viene chiuso e riaperto. Vale a dire **SQLExtendedFetch** può essere chiamato solo stavu istruzione S7. Per altre informazioni, vedere [transizioni di istruzione](../../../odbc/reference/appendixes/statement-transitions.md) nell'appendice b: Tabelle della transizione di stato ODBC.  
  
 Quando un'applicazione chiama **SQLFetchScroll** quando si usa un'API ODBC 2 *. x* driver, Driver Manager esegue il mapping di questa chiamata a **SQLExtendedFetch**. Per altre informazioni, vedere "ODBC 2 e SQLFetchScroll *. x* i driver" nella [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 In ODBC 2 *. x*, **SQLExtendedFetch** è stato chiamato per recuperare più righe e **SQLFetch** è stato chiamato per recuperare una singola riga. In ODBC 3 *. x*, d'altra parte, **SQLFetch** può essere chiamato per recuperare più righe.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultati|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Esecuzione di operazioni bulk insert, update o operazioni di eliminazione|[Funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di informazioni relative a una colonna in un set di risultati|[Funzione SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Esecuzione di un'istruzione SQL|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Colonne del set di restituzione del numero di risultati|[Funzione SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Posizionando il cursore, l'aggiornamento dei dati del set di righe o l'aggiornamento o eliminazione dei dati nel set di risultati|[Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|L'impostazione di un attributo di istruzione|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
