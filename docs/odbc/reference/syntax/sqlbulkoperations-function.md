---
title: Funzione SQLBulkOperations . Documenti Microsoft
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f4f294a6d84856bc3065b599a370bb5658e3ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301331"
---
# <a name="sqlbulkoperations-function"></a>Funzione SQLBulkOperations
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLBulkOperations** esegue inserimenti in blocco e operazioni di segnalibro in blocco, tra cui aggiornamento, eliminazione e recupero per segnalibro.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *Operazione*  
 [Ingresso] Operazione da eseguire:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 Per ulteriori informazioni, vedere "Commenti".  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLBulkOperations** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLBulkOperations** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
 Per tutti gli SQLSTATE che possono restituire SQL_SUCCESS_WITH_INFO o SQL_ERROR (ad eccezione di 01xxx SQLSTATEs), viene restituito SQL_SUCCESS_WITH_INFO se si verifica un errore in uno o più, ma non in tutte le righe di un'operazione multiriga, e SQL_ERROR viene restituito se si verifica un errore in un'operazione a riga singola.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Troncamento a destra dei dati stringaString data right truncation|*L'argomento Operation* è stato SQL_FETCH_BY_BOOKMARK e i dati stringa o binari restituiti per una colonna o colonne con un tipo di dati di SQL_C_CHAR o SQL_C_BINARY hanno determinato il troncamento di caratteri non vuoti o dati binari non NULL.|  
|01S01 (in questo stato di|Errore nella riga|*L'argomento Operation* è stato SQL_ADD e si è verificato un errore in una o più righe durante l'esecuzione dell'operazione, ma almeno una riga è stata aggiunta correttamente. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)<br /><br /> (Questo errore viene generato solo quando un'applicazione utilizza un ODBC 2. *x* driver.)|  
|01S07 (intito)|Troncamento frazionario|*L'argomento Operation* era SQL_FETCH_BY_BOOKMARK, il tipo di dati del buffer dell'applicazione non era SQL_C_CHAR o SQL_C_BINARY e i dati restituiti ai buffer dell'applicazione per una o più colonne venivano troncati. Per i tipi di dati numerici C, la parte frazionaria del numero è stata troncata. Per i tipi di dati di ora, timestamp e intervallo C che contengono un componente ora, la parte frazionaria dell'ora è stata troncata.)<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07006|Violazione dell'attributo del tipo di dati con restrizioniRestricted data type attribute violation|Il *Operation* argomento è stato SQL_FETCH_BY_BOOKMARK e il valore dei dati di una colonna nel set di risultati non è stato possibile convertire nel tipo di dati specificato dal *TargetType* argomento nella chiamata a **SQLBindCol**.<br /><br /> *L'argomento Operation* è stato SQL_UPDATE_BY_BOOKMARK o SQL_ADD e non è stato possibile convertire il valore dei dati nei buffer dell'applicazione nel tipo di dati di una colonna nel set di risultati.|  
|07009|Indice descrittore non valido|*L'argomento Operation* è stato SQL_ADD ed è stata associata una colonna con un numero di colonna maggiore del numero di colonne nel set di risultati.|  
|21S02|Il grado della tabella derivata non corrisponde all'elenco di colonne|L'argomento *Operazione* è stata SQL_UPDATE_BY_BOOKMARK; e nessuna colonna era aggiornabile perché tutte le colonne erano non associate o di sola lettura oppure il valore nel buffer di lunghezza/indicatore associato era SQL_COLUMN_IGNORE.|  
|22001|Troncamento a destra dei dati stringaString data right truncation|L'assegnazione di un carattere o di un valore binario a una colonna nel set di risultati ha comportato il troncamento di caratteri o byte non vuoti (per i caratteri) o non null (per binari).|  
|22003|Valore numerico non compreso nell'intervallo|*L'argomento Operation* è stato SQL_ADD o SQL_UPDATE_BY_BOOKMARK e l'assegnazione di un valore numerico a una colonna nel set di risultati ha causato il troncamento dell'intera parte del numero anziché frazionaria.<br /><br /> L'argomento *Operation* è stato SQL_FETCH_BY_BOOKMARK e la restituzione del valore numerico per una o più colonne associate avrebbe causato una perdita di cifre significative.|  
|22007|Formato datetime non valido|*L'argomento Operazione* è stato SQL_ADD o SQL_UPDATE_BY_BOOKMARK e l'assegnazione di un valore di data o timestamp a una colonna nel set di risultati ha causato il campo anno, mese o giorno non compreso nell'intervallo.<br /><br /> L'argomento *Operazione* è stato SQL_FETCH_BY_BOOKMARK e la restituzione del valore data o timestamp per una o più colonne associate avrebbe fatto sì che il campo anno, mese o giorno non fosse compreso nell'intervallo.|  
|22008|Overflow del campo Data/ora|*L'argomento Operation* è stato SQL_ADD o SQL_UPDATE_BY_BOOKMARK e le prestazioni dell'aritmetica datetime sui dati inviati a una colonna nel set di risultati hanno restituito un campo datetime (anno, mese, giorno, ora, minuto o secondo campo) del risultato che non rientra nell'intervallo di valori consentito per il campo o non è valido in base alle regole naturali del calendario gregoriano per datetime.<br /><br /> *L'argomento Operation* è stato SQL_FETCH_BY_BOOKMARK e l'esecuzione dell'aritmetica datetime sui dati recuperati dal set di risultati ha determinato un campo datetime (anno, mese, giorno, ora, minuto o secondo campo) del risultato che non rientra nell'intervallo di valori consentito per il campo o non è valido in base alle regole naturali del calendario gregoriano per datetime.|  
|22015|Overflow campo intervallo|*L'argomento Operation* è stato SQL_ADD o SQL_UPDATE_BY_BOOKMARK e l'assegnazione di un tipo di dati numerico o di intervallo C esatto a un tipo di dati SQL a intervalli ha causato una perdita di cifre significative.<br /><br /> L'argomento *Operazione* è stato SQL_ADD o SQL_UPDATE_BY_BOOKMARK. durante l'assegnazione a un tipo SQL intervallo, non è stata rappresentazione del valore del tipo C nel tipo SQL di intervallo.<br /><br /> *L'argomento Operation* è stato SQL_FETCH_BY_BOOKMARK e l'assegnazione da un tipo SQL esatto numerico o a intervallo a un tipo di intervallo C ha causato una perdita di cifre significative nel campo iniziale.<br /><br /> L'argomento *Operazione* è stato SQL_FETCH_BY_BOOKMARK; durante l'assegnazione a un tipo di intervallo C, non è stata rappresentazione del valore del tipo SQL nel tipo di intervallo C.|  
|22018|Valore di carattere non valido per la specifica del cast|L'argomento *Operazione* è stato SQL_FETCH_BY_BOOKMARK; il tipo C era un numero esatto o approssimativo, un datetime o un tipo di dati interval; il tipo SQL della colonna era un tipo di dati carattere; e il valore nella colonna non è un valore letterale valido del tipo C associato.<br /><br /> L'argomento *Operazione* è stata SQL_ADD o SQL_UPDATE_BY_BOOKMARK; il tipo SQL era un numero esatto o approssimativo, un datetime o un tipo di dati interval; il tipo C è stato SQL_C_CHAR; e il valore nella colonna non è un valore letterale valido del tipo SQL associato.|  
|23000|Violazione dei vincoli di integrità|L'argomento *Operazione* è stato SQL_ADD, SQL_DELETE_BY_BOOKMARK o SQL_UPDATE_BY_BOOKMARK ed è stato violato un vincolo di integrità.<br /><br /> *L'argomento Operation* è stato SQL_ADD e una colonna non associata è definita come NOT NULL e non ha alcun valore predefinito.<br /><br /> *L'argomento Operation* è stato SQL_ADD, la lunghezza specificata nel buffer *di StrLen_or_IndPtr* associato è stata SQL_COLUMN_IGNORE e la colonna non ha un valore predefinito.|  
|24000|Stato del cursore non valido|*StatementHandle* era in uno stato eseguito, ma a *StatementHandle*non è stato associato alcun set di risultati .|  
|40001|Errore di serializzazione|È stato eseguito il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|42000|Errore di sintassi o violazione di accesso|Il driver non è stato in grado di bloccare la riga in base alle esigenze per eseguire l'operazione richiesta nell'argomento *Operation.*|  
|44000|Violazione della clausola WITH CHECK OPTION|*L'argomento Operazione* è stato SQL_ADD o SQL_UPDATE_BY_BOOKMARK e l'inserimento o l'aggiornamento è stato eseguito su una tabella visualizzata (o una tabella derivata dalla tabella visualizzata) creata specificando **WITH CHECK OPTION**, in modo che una o più righe interessate dall'inserimento o dall'aggiornamento non siano più presenti nella tabella visualizzata.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*. Quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLBulkOperations.This** asynchronous function was still executing when the SQLBulkOperations function was called.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) *L'oggetto statementHandle* specificato non era in uno stato eseguito. La funzione è stata chiamata senza prima chiamare **SQLExecDirect**, **SQLExecute**o una funzione di catalogo.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) Il driver era un ODBC 2. *x* driver e **SQLBulkOperations** è stato chiamato per un *StatementHandle* prima **SQLFetchScroll** o **SQLFetch** è stato chiamato.<br /><br /> (DM) **SQLBulkOperations** è stato chiamato dopo **sqlExtendedFetch** è stato chiamato su *StatementHandle*.|  
|HY011|Impossibile impostare l'attributo ora|(DM) Il driver era un ODBC 2. *x* e l'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR è stato impostato tra le chiamate a **SQLFetch** o **SQLFetchScroll** e **SQLBulkOperations**.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|L'argomento *Operazione* è stato SQL_ADD o SQL_UPDATE_BY_BOOKMARK. un valore di dati non era un puntatore null; il tipo di dati C è stato SQL_C_BINARY o SQL_C_CHAR; e il valore della lunghezza della colonna era minore di 0, ma non uguale a SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NTS o SQL_NULL_DATA oppure minore o uguale a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Il valore in un buffer di lunghezza/indicatore è stato SQL_DATA_AT_EXEC; il tipo SQL è SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo di dati specifico dell'origine dati long. e il tipo di informazioni SQL_NEED_LONG_DATA_LEN in **SQLGetInfo** era "Y".<br /><br /> *L'argomento Operation* è stato SQL_ADD, l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARK è stato impostato su SQL_UB_VARIABLE e la colonna 0 è stata associata a un buffer la cui lunghezza non è uguale alla lunghezza massima per il segnalibro per il set di risultati. Questa lunghezza è disponibile nel campo SQL_DESC_OCTET_LENGTH dell'IRD e può essere ottenuta chiamando **SQLDescribeCol**, **SQLColAttribute**o **SQLGetDescField**.|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo non valido|(DM) il valore specificato per l'argomento *Operation* non è valido.<br /><br /> *L'argomento Operation* è stato SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK e l'attributo dell'istruzione SQL_ATTR_CONCURRENCY è stato impostato su SQL_CONCUR_READ_ONLY.<br /><br /> *L'argomento Operation* è stato SQL_DELETE_BY_BOOKMARK, SQL_FETCH_BY_BOOKMARK o SQL_UPDATE_BY_BOOKMARK e la colonna del segnalibro non è stata associata oppure l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_OFF.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il driver o l'origine dati non supporta l'operazione richiesta nell'argomento *Operation.*|  
|HYT00|Timeout|Il periodo di timeout della query è scaduto prima che l'origine dati restituisca il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr** con un *attributo* argomento di SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
  
> [!CAUTION]  
>  Per informazioni sugli stati dell'istruzione **SQLBulkOperations** possono essere chiamati e cosa deve fare per garantire la compatibilità con ODBC 2. *x,* vedere la sezione [Cursori a blocchi, Cursori scorrevoli e Compatibilità con](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) le versioni precedenti nell'Appendice G: Linee guida per i driver per la compatibilità con le versioni precedenti.  
  
 Un'applicazione utilizza **SQLBulkOperations** per eseguire le operazioni seguenti nella tabella o vista di base che corrisponde alla query corrente:  
  
-   Aggiungere nuove righe.  
  
-   Aggiornare un set di righe in cui ogni riga è identificata da un segnalibro.  
  
-   Eliminare un set di righe in cui ogni riga è identificata da un segnalibro.  
  
-   Recuperare un set di righe in cui ogni riga è identificata da un segnalibro.  
  
 Dopo una chiamata a **SQLBulkOperations**, la posizione del cursore di blocco non è definita. L'applicazione deve chiamare **SQLFetchScroll** per impostare la posizione del cursore. Un'applicazione deve chiamare **SQLFetchScroll** solo con un *argomento FetchOrientation* di SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE o SQL_FETCH_BOOKMARK. La posizione del cursore non è definita se l'applicazione chiama **SQLFetch** o **SQLFetchScroll** con un *argomento FetchOrientation* di SQL_FETCH_PRIOR, SQL_FETCH_NEXT o SQL_FETCH_RELATIVE.  
  
 Una colonna può essere ignorata nelle operazioni bulk eseguite da una chiamata a **SQLBulkOperations** impostando il buffer di lunghezza/indicatore della colonna specificato nella chiamata a **SQLBindCol**, su SQL_COLUMN_IGNORE.  
  
 Non è necessario che l'applicazione imposti l'attributo dell'istruzione SQL_ATTR_ROW_OPERATION_PTR quando chiama **SQLBulkOperations** perché le righe non possono essere ignorate quando si eseguono operazioni bulk con questa funzione.  
  
 Il buffer a cui fa riferimento l'attributo dell'istruzione SQL_ATTR_ROWS_FETCHED_PTR contiene il numero di righe interessate da una chiamata a **SQLBulkOperations**.  
  
 Quando *l'argomento Operation* è SQL_ADD o SQL_UPDATE_BY_BOOKMARK e l'elenco di selezione della specifica di query associata al cursore contiene più di un riferimento alla stessa colonna, è definito dal driver se viene generato un errore o il driver ignora i riferimenti duplicati ed esegue le operazioni richieste.  
  
 Per ulteriori informazioni sull'utilizzo di **SQLBulkOperations**, vedere [Aggiornamento dei dati con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).  
  
## <a name="performing-bulk-inserts"></a>Esecuzione di inserimenti di massaPerforming Bulk Inserts  
 Per inserire dati con **SQLBulkOperations**, un'applicazione esegue la sequenza di passaggi seguente:  
  
1.  Esegue una query che restituisce un set di risultati.  
  
2.  Imposta l'attributo dell'istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe che desidera inserire.  
  
3.  Chiama **SQLBindCol** per associare i dati che si desidera inserire. I dati sono associati a una matrice con una dimensione uguale al valore di SQL_ATTR_ROW_ARRAY_SIZE.  
  
    > [!NOTE]  
    >  La dimensione della matrice a cui fa riferimento l'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR deve essere uguale a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR deve essere un puntatore null.  
  
4.  Chiama **SQLBulkOperations**(*StatementHandle,* SQL_ADD) per eseguire l'inserimento.  
  
5.  Se l'applicazione ha impostato l'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR, è possibile esaminare questa matrice per visualizzare il risultato dell'operazione.  
  
 Se un'applicazione associa la colonna 0 prima di chiamare **SQLBulkOperations** con *un* Operation argomento di SQL_ADD, il driver aggiornerà i buffer di colonna 0 associati con i valori del segnalibro per la riga appena inserita. Affinché ciò si verifichi, l'applicazione deve aver impostato l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS su SQL_UB_VARIABLE prima di eseguire l'istruzione. (Questo non funziona con un ODBC 2. *x* driver.)  
  
 I dati lunghi possono essere aggiunti in parti da SQLBulkOperations, usando le chiamate a SQLParamData e SQLPutData.Long data can be added in parts by SQLBulkOperations, by using calls to SQLParamData and SQLPutData. Per altre informazioni, vedere "Fornire dati lunghi per inserimenti e aggiornamenti bulk" più avanti in questa guida di riferimento sulla funzione.  
  
 Non è necessario che l'applicazione chiami **SQLFetch** o **SQLFetchScroll** prima di chiamare **SQLBulkOperations** (tranne quando si va contro un ODBC 2.* x* driver; vedere [Compatibilità con le versioni precedenti e Conformità agli standard](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)).  
  
 Il comportamento è definito dal driver se **SQLBulkOperations**, con un *Operation* argomento di SQL_ADD , viene chiamato su un cursore che contiene colonne duplicate. Il driver può restituire un SQLSTATE definito dal driver, aggiungere i dati alla prima colonna visualizzata nel set di risultati o eseguire altri comportamenti definiti dal driver.  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>Esecuzione di aggiornamenti in blocco tramite segnalibri  
 Per eseguire aggiornamenti in blocco utilizzando i segnalibri con **SQLBulkOperations**, un'applicazione esegue i passaggi seguenti in sequenza:  
  
1.  Imposta l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS su SQL_UB_VARIABLE.  
  
2.  Esegue una query che restituisce un set di risultati.  
  
3.  Imposta l'attributo dell'istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe che desidera aggiornare.  
  
4.  Chiama **SQLBindCol** per associare i dati che si desidera aggiornare. I dati sono associati a una matrice con una dimensione uguale al valore di SQL_ATTR_ROW_ARRAY_SIZE. Chiama anche **SQLBindCol** per associare la colonna 0 (la colonna del segnalibro).  
  
5.  Copia i segnalibri per le righe che è interessato ad aggiornare nella matrice associata alla colonna 0.  
  
6.  Aggiorna i dati nei buffer associati.  
  
    > [!NOTE]  
    >  La dimensione della matrice a cui fa riferimento l'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR deve essere uguale a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR deve essere un puntatore null.  
  
7.  Chiama **SQLBulkOperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK).  
  
    > [!NOTE]  
    >  Se l'applicazione ha impostato l'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR, è possibile esaminare questa matrice per visualizzare il risultato dell'operazione.  
  
8.  Facoltativamente, chiama **SQLBulkOperations**(*StatementHandle*, SQL_FETCH_BY_BOOKMARK) per recuperare i dati nei buffer dell'applicazione associati per verificare che l'aggiornamento si sia verificato.  
  
9. Se i dati sono stati aggiornati, il driver modifica il valore nella matrice di stato della riga per le righe appropriate in SQL_ROW_UPDATED.  
  
 Gli aggiornamenti di massa eseguiti da **SQLBulkOperations** possono includere dati lunghi utilizzando le chiamate a **SQLParamData** e **SQLPutData**. Per altre informazioni, vedere "Fornire dati lunghi per inserimenti e aggiornamenti bulk" più avanti in questa guida di riferimento sulla funzione.  
  
 Se i segnalibri vengono mantenuti tra i cursori, non è necessario che l'applicazione chiami **SQLFetch** o **SQLFetchScroll** prima dell'aggiornamento tramite segnalibri. Può utilizzare i segnalibri che ha memorizzato da un cursore precedente. Se i segnalibri non vengono mantenuti tra i cursori, l'applicazione deve chiamare **SQLFetch** o **SQLFetchScroll** per recuperare i segnalibri.  
  
 Il comportamento è definito dal driver se **SQLBulkOperations**, con un *Operation* argomento di SQL_UPDATE_BY_BOOKMARK, viene chiamato su un cursore che contiene colonne duplicate. Il driver può restituire un SQLSTATE definito dal driver, aggiornare la prima colonna visualizzata nel set di risultati o eseguire altri comportamenti definiti dal driver.  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>Esecuzione di recuperamenti in blocco tramite segnalibriPerforming Bulk Fetches Using Bookmarks  
 Per eseguire recuperi di massa utilizzando i segnalibri con **SQLBulkOperations**, un'applicazione esegue i passaggi seguenti in sequenza:  
  
1.  Imposta l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS su SQL_UB_VARIABLE.  
  
2.  Esegue una query che restituisce un set di risultati.  
  
3.  Imposta l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe che desidera recuperare.  
  
4.  Chiama **SQLBindCol** per associare i dati che desidera recuperare. I dati sono associati a una matrice con una dimensione uguale al valore di SQL_ATTR_ROW_ARRAY_SIZE. Chiama anche **SQLBindCol** per associare la colonna 0 (la colonna del segnalibro).  
  
5.  Copia i segnalibri per le righe che è interessato a recuperare nella matrice associata alla colonna 0. (Si presuppone che l'applicazione abbia già ottenuto i segnalibri separatamente.)  
  
    > [!NOTE]  
    >  La dimensione della matrice a cui fa riferimento l'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR deve essere uguale a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR deve essere un puntatore null.  
  
6.  Chiama **SQLBulkOperations**(*StatementHandle,* SQL_FETCH_BY_BOOKMARK).  
  
7.  Se l'applicazione ha impostato l'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR, è possibile esaminare questa matrice per visualizzare il risultato dell'operazione.  
  
 Se i segnalibri vengono mantenuti tra i cursori, non è necessario che l'applicazione chiami **SQLFetch** o **SQLFetchScroll** prima di eseguire il recupero tramite segnalibri. Può utilizzare i segnalibri che ha memorizzato da un cursore precedente. Se i segnalibri non vengono mantenuti tra i cursori, l'applicazione deve chiamare **SQLFetch** o **SQLFetchScroll** una volta per recuperare i segnalibri.  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>Esecuzione di eliminazioni in blocco tramite segnalibri  
 Per eseguire eliminazioni in blocco utilizzando i segnalibri con **SQLBulkOperations**, un'applicazione esegue i passaggi seguenti in sequenza:  
  
1.  Imposta l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS su SQL_UB_VARIABLE.  
  
2.  Esegue una query che restituisce un set di risultati.  
  
3.  Imposta l'attributo dell'istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe che desidera eliminare.  
  
4.  Chiama **SQLBindCol** per associare la colonna 0 (la colonna del segnalibro).  
  
5.  Copia i segnalibri per le righe che è interessato ad eliminare nella matrice associata alla colonna 0.  
  
    > [!NOTE]  
    >  La dimensione della matrice a cui fa riferimento l'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR deve essere uguale a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR deve essere un puntatore null.  
  
6.  Chiama **SQLBulkOperations**(*StatementHandle,* SQL_DELETE_BY_BOOKMARK).  
  
7.  Se l'applicazione ha impostato l'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR, è possibile esaminare questa matrice per visualizzare il risultato dell'operazione.  
  
 Se i segnalibri vengono mantenuti tra i cursori, l'applicazione non deve chiamare **SQLFetch** o **SQLFetchScroll** prima di eliminarli dai segnalibri. Può utilizzare i segnalibri che ha memorizzato da un cursore precedente. Se i segnalibri non vengono mantenuti tra i cursori, l'applicazione deve chiamare **SQLFetch** o **SQLFetchScroll** una volta per recuperare i segnalibri.  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>Fornire dati lunghi per inserimenti e aggiornamenti in blocco  
 È possibile fornire dati lunghi per gli inserimenti e gli aggiornamenti bulk eseguiti dalle chiamate a **SQLBulkOperations**. Per inserire o aggiornare dati lunghi, un'applicazione esegue i passaggi seguenti oltre ai passaggi descritti nelle sezioni "Esecuzione di inserimenti in blocco" e "Esecuzione di aggiornamenti in blocco tramite segnalibri" più indietro in questo argomento.  
  
1.  Quando associa i dati utilizzando **SQLBindCol**, l'applicazione inserisce un valore definito dall'applicazione, ad esempio il numero di colonna, nel buffer * \*TargetValuePtr* per le colonne data-at-execution. Il valore può essere utilizzato in un secondo momento per identificare la colonna.  
  
     L'applicazione inserisce il risultato della macro SQL_LEN_DATA_AT_EXEC(*length*) nel buffer * \*StrLen_or_IndPtr.* Se il tipo di dati SQL della colonna è SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo di dati specifico dell'origine dati long e il driver restituisce "Y" per il tipo di informazioni SQL_NEED_LONG_DATA_LEN in **SQLGetInfo**, *length* è il numero di byte di dati da inviare per il parametro; in caso contrario, deve essere un valore non negativo e viene ignorato.  
  
2.  Quando **SQLBulkOperations** viene chiamato, se sono presenti colonne data-at-execution, la funzione restituisce SQL_NEED_DATA e procede al passaggio 3, che segue. Se non sono presenti colonne data-at-execution, il processo è completo.  
  
3.  L'applicazione chiama **SQLParamData** per recuperare l'indirizzo del buffer * \*TargetValuePtr* per la prima colonna data-at-execution da elaborare. **SQLParamData** restituisce SQL_NEED_DATA. L'applicazione recupera il valore definito dall'applicazione dal buffer * \*TargetValuePtr.*  
  
    > [!NOTE]  
    >  Sebbene i parametri data-at-execution siano simili alle colonne data-at-execution, il valore restituito da **SQLParamData** è diverso per ognuno di essi.  
  
     Le colonne Data-at-execution sono colonne in un set di righe per le quali verranno inviati dati con **SQLPutData** quando una riga viene aggiornata o inserita con **SQLBulkOperations**. Sono associati a **SQLBindCol**. Il valore restituito da **SQLParamData** è l'indirizzo della riga nel buffer*TargetValuePtr* che viene elaborato.  
  
4.  L'applicazione chiama **SQLPutData** una o più volte per inviare i dati per la colonna. È necessaria più di una chiamata se non è possibile restituire tutti i valori di dati nel buffer * \*TargetValuePtr* specificato in **SQLPutData**; più chiamate a **SQLPutData** per la stessa colonna sono consentite solo quando si inviano dati di tipo carattere C a una colonna con un tipo di dati carattere, binario o specifico dell'origine dati o quando si inviano dati C binari a una colonna con un tipo di dati carattere, binario o specifico dell'origine dati.  
  
5.  L'applicazione chiama nuovamente **SQLParamData** per segnalare che tutti i dati sono stati inviati per la colonna.  
  
    -   Se sono presenti più colonne data-at-execution, **SQLParamData** restituisce SQL_NEED_DATA e l'indirizzo del buffer *TargetValuePtr* per la successiva colonna data-at-execution da elaborare. L'applicazione ripete i passaggi 4 e 5.  
  
    -   Se non sono presenti altre colonne data-at-execution, il processo è completo. Se l'istruzione è stata eseguita correttamente, **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; se l'esecuzione non è riuscita, restituisce SQL_ERROR. A questo punto, **SQLParamData** può restituire qualsiasi SQLSTATE che può essere restituito da **SQLBulkOperations**.  
  
 Se l'operazione viene annullata o si verifica un errore in **SQLParamData** o **SQLPutData** dopo **SQLBulkOperations** restituisce SQL_NEED_DATA e prima dell'invio dei dati per tutte le colonne data-at-execution, l'applicazione può chiamare solo **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**o **SQLPutData** per l'istruzione o la connessione associata all'istruzione. Se chiama qualsiasi altra funzione per l'istruzione o la connessione associata all'istruzione, la funzione restituisce SQL_ERROR e SQLSTATE HY010 (errore di sequenza di funzione).  
  
 Se l'applicazione chiama **SQLCancel** mentre il driver richiede ancora dati per le colonne data-at-esecuzione, il driver annulla l'operazione. L'applicazione può quindi chiamare nuovamente **SQLBulkOperations;** l'annullamento non influisce sullo stato del cursore o sulla posizione corrente del cursore.  
  
## <a name="row-status-array"></a>Matrice di stato riga  
 La matrice di stato della riga contiene i valori di stato per ogni riga di dati nel set di righe dopo una chiamata a **SQLBulkOperations**. Il driver imposta i valori di stato in questa matrice dopo una chiamata a **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**o **SQLBulkOperations**. Questa matrice viene inizialmente popolata da una chiamata a **SQLBulkOperations** se **SQLFetch** o **SQLFetchScroll** non è stato chiamato prima di **SQLBulkOperations**. Questa matrice fa riferimento all'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR. Il numero di elementi nelle matrici di stato delle righe deve essere uguale al numero di righe nel set di righe (come definito dall'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE). Per informazioni su questa matrice di stato di riga, vedere [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente vengono recuperate 10 righe di dati alla volta dalla tabella Customers. Viene quindi richiesto all'utente di eseguire un'azione. Per ridurre il traffico di rete, il buffer di esempio aggiorna, elimina e inserisce localmente nelle matrici associate, ma in corrispondenza degli offset oltre i dati del set di righe. Quando l'utente sceglie di inviare aggiornamenti, eliminazioni e inserimenti all'origine dati, il codice imposta l'offset dell'associazione in modo appropriato e chiama **SQLBulkOperations**. Per semplicità, l'utente non può memorizzare nel buffer più di 10 aggiornamenti, eliminazioni o inserimenti.  
  
```cpp  
// SQLBulkOperations_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include "stdio.h"  
  
#define UPDATE_ROW 100  
#define DELETE_ROW 101  
#define ADD_ROW 102  
#define SEND_TO_DATA_SOURCE 103  
#define UPDATE_OFFSET 10  
#define INSERT_OFFSET 20  
#define DELETE_OFFSET 30  
  
// Define structure for customer data (assume 10 byte maximum bookmark size).  
typedef struct tagCustStruct {  
   SQLCHAR Bookmark[10];  
   SQLINTEGER BookmarkLen;  
   SQLUINTEGER CustomerID;  
   SQLINTEGER CustIDInd;  
   SQLCHAR CompanyName[51];  
   SQLINTEGER NameLenOrInd;  
   SQLCHAR Address[51];  
   SQLINTEGER AddressLenOrInd;  
   SQLCHAR Phone[11];  
   SQLINTEGER PhoneLenOrInd;  
} CustStruct;  
  
// Allocate 40 of these structures. Elements 0-9 are for the current rowset,  
// elements 10-19 are for the buffered updates, elements 20-29 are for  
// the buffered inserts, and elements 30-39 are for the buffered deletes.  
CustStruct CustArray[40];  
SQLUSMALLINT RowStatusArray[10], Action, RowNum, NumUpdates = 0, NumInserts = 0,  
NumDeletes = 0;  
SQLLEN BindOffset = 0;  
SQLRETURN retcode;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLHSTMT hstmt = NULL;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Set the following statement attributes:  
   // SQL_ATTR_CURSOR_TYPE:           Keyset-driven  
   // SQL_ATTR_ROW_BIND_TYPE:         Row-wise  
   // SQL_ATTR_ROW_ARRAY_SIZE:        10  
   // SQL_ATTR_USE_BOOKMARKS:         Use variable-length bookmarks  
   // SQL_ATTR_ROW_STATUS_PTR:        Points to RowStatusArray  
   // SQL_ATTR_ROW_BIND_OFFSET_PTR:   Points to BindOffset  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_KEYSET_DRIVEN, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER)sizeof(CustStruct), 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_USE_BOOKMARKS, (SQLPOINTER)SQL_UB_VARIABLE, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_OFFSET_PTR, &BindOffset, 0);  
  
   // Bind arrays to the bookmark, CustomerID, CompanyName, Address, and Phone columns.  
   retcode = SQLBindCol(hstmt, 0, SQL_C_VARBOOKMARK, CustArray[0].Bookmark, sizeof(CustArray[0].Bookmark), &CustArray[0].BookmarkLen);  
   retcode = SQLBindCol(hstmt, 1, SQL_C_ULONG, &CustArray[0].CustomerID, 0, &CustArray[0].CustIDInd);  
   retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, CustArray[0].CompanyName, sizeof(CustArray[0].CompanyName), &CustArray[0].NameLenOrInd);  
   retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, CustArray[0].Address, sizeof(CustArray[0].Address), &CustArray[0].AddressLenOrInd);  
   retcode = SQLBindCol(hstmt, 4, SQL_C_CHAR, CustArray[0].Phone, sizeof(CustArray[0].Phone), &CustArray[0].PhoneLenOrInd);  
  
   // Execute a statement to retrieve rows from the Customers table.  
   retcode = SQLExecDirect(hstmt, (SQLCHAR*)"SELECT CustomerID, CompanyName, Address, Phone FROM Customers", SQL_NTS);  
  
   // Fetch and display the first 10 rows.  
   retcode = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
   // DisplayCustData(CustArray, 10);  
  
   // Call GetAction to get an action and a row number from the user.  
   // while (GetAction(&Action, &RowNum)) {  
   Action = SQL_FETCH_NEXT;  
   RowNum = 2;  
   switch (Action) {  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         // DisplayCustData(CustArray, 10);  
         break;  
  
      case UPDATE_ROW:  
         // Check if we have reached the maximum number of buffered updates.  
         if (NumUpdates < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered updates section of CustArray, copy the bookmark of the row  
            // being updated to the same element, and increment the update counter.  
            // Checking to see we have not already buffered an update for this  
            // row not shown.  
            // GetNewCustData(CustArray, UPDATE_OFFSET + NumUpdates);  
            memcpy(CustArray[UPDATE_OFFSET + NumUpdates].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
            CustArray[UPDATE_OFFSET + NumUpdates].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
            NumUpdates++;  
         } else {  
            printf("Buffers full. Send buffered changes to the data source.");  
         }  
         break;  
      case DELETE_ROW:  
         // Check if we have reached the maximum number of buffered deletes.  
         if (NumDeletes < 10) {  
            // Copy the bookmark of the row being deleted to the next available element  
            // of the buffered deletes section of CustArray and increment the delete  
            // counter. Checking to see we have not already buffered an update for  
            // this row not shown.  
            memcpy(CustArray[DELETE_OFFSET + NumDeletes].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
  
            CustArray[DELETE_OFFSET + NumDeletes].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
  
            NumDeletes++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case ADD_ROW:  
         // reached maximum number of buffered inserts?  
         if (NumInserts < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered inserts section of CustArray and increment insert counter.  
            // GetNewCustData(CustArray, INSERT_OFFSET + NumInserts);  
            NumInserts++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case SEND_TO_DATA_SOURCE:  
         // If there are any buffered updates, inserts, or deletes, set the array size  
         // to that number, set the binding offset to use the data in the buffered  
         // update, insert, or delete part of CustArray, and call SQLBulkOperations to  
         // do the updates, inserts, or deletes. Because we will never have more than  
         // 10 updates, inserts, or deletes, we can use the same row status array.  
         if (NumUpdates) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumUpdates, 0);  
            BindOffset = UPDATE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_UPDATE_BY_BOOKMARK);  
            NumUpdates = 0;  
         }  
  
         if (NumInserts) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumInserts, 0);  
            BindOffset = INSERT_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_ADD);  
            NumInserts = 0;  
         }  
  
         if (NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumDeletes, 0);  
            BindOffset = DELETE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_DELETE_BY_BOOKMARK);  
            NumDeletes = 0;  
         }  
  
         // If there were any updates, inserts, or deletes, reset the binding offset  
         // and array size to their original values.  
         if (NumUpdates || NumInserts || NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
            BindOffset = 0;  
         }  
         break;  
   }  
   // }  
  
   // Close the cursor.  
   SQLFreeStmt(hstmt, SQL_CLOSE);  
}  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Recupero di un blocco di dati o scorrimento di un set di risultati|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Ottenere un singolo campo di un descrittoreGetting a single field of a descriptor|[Funzione SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Recupero di più campi di un descrittoreGetting multiple fields of a descriptor|[Funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Impostazione di un singolo campo di un descrittore|[Funzione SQLSetDescFieldSQLSetDescField Function](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Impostazione di più campi di un descrittore|[Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Posizionamento del cursore, aggiornamento dei dati nel set di righe o aggiornamento o eliminazione di dati nel set di righe|[Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Impostazione di un attributo di istruzioneSetting a statement attribute|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
