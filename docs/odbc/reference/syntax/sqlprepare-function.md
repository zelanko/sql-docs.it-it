---
title: 'Funzione SQLPrepare : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPrepare
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrepare
helpviewer_keywords:
- SQLPrepare function [ODBC]
ms.assetid: 332e1b4b-b0ed-4e7a-aa4d-4f35f4f4476b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e9aedd665df2a943627207902d592d597c503c63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306882"
---
# <a name="sqlprepare-function"></a>Pagina relativa alla funzione SQLPrepare
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLPrepare** prepara una stringa SQL per l'esecuzione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *StatementText (TestoIstruzioni)*  
 [Ingresso] Stringa di testo SQL.  
  
 *TextLength*  
 [Ingresso] Lunghezza del valore*di StatementText* in caratteri.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLPrepare** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLPrepare** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S02 (in questo stato di|Valore dell'opzione modificato|Un attributo di istruzione specificato non è valido a causa delle condizioni di lavoro di implementazione, pertanto un valore simile è stato temporaneamente sostituito. **SQLGetStmtAttr** può essere chiamato per determinare il valore sostituito temporaneamente. Il valore sostitutivo è valido per *il StatementHandle* fino a quando il cursore viene chiuso. Gli attributi di istruzione che possono essere modificati sono: SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|21S01|L'elenco di valori di inserimento non corrisponde all'elenco di colonne|\**StatementText* contiene un'istruzione **INSERT** e il numero di valori da inserire non corrispondeva al grado della tabella derivata.|  
|21S02|Il grado della tabella derivata non corrisponde all'elenco di colonne|\**StatementText* contiene un'istruzione **CREATE VIEW** e il numero di nomi specificati non corrisponde allo stesso grado della tabella derivata definita dalla specifica della query.|  
|22018|Valore di carattere non valido per la specifica del cast|**StatementText* conteneva un'istruzione SQL che conteneva un valore letterale o un parametro e il valore era incompatibile con il tipo di dati della colonna di tabella associata.|  
|22019|Carattere di escape non valido|L'argomento *StatementText* conteneva un predicato **LIKE** con un **escape** nella clausola **WHERE** e la lunghezza del carattere di escape che segue **ESCAPE** non era uguale a 1.|  
|22025|Sequenza di escape non valida|L'argomento *StatementText* conteneva "**LIKE** _pattern value_ **ESCAPE** _carattere_di escape " nella clausola **WHERE** e il carattere che segue il carattere di escape nel valore del modello non era né "%" né "_".|  
|24000|Stato del cursore non valido|(DM) Un cursore era aperto su *StatementHandle*e **SQLFetch** o **SQLFetchScroll** era stato chiamato.<br /><br /> Un cursore era aperto su *StatementHandle*, ma **SQLFetch** o **SQLFetchScroll** non era stato chiamato.|  
|34000|Nome di cursore non valido|\**StatementText* contiene **un'istruzione DELETE** posizionata o un **UPDATE**posizionato e il cursore a cui fa riferimento l'istruzione da preparare non era aperto.|  
|3D000|Nome di catalogo non valido|Il nome del catalogo specificato in *StatementText* non è valido.|  
|3F000|Nome dello schema non valido|Il nome dello schema specificato in *StatementText* non è valido.|  
|42000|Errore di sintassi o violazione di accesso|\**StatementText* contiene un'istruzione SQL non preparabile o contenente un errore di sintassi.<br /><br /> **StatementText* conteneva un'istruzione per la quale l'utente non disponeva dei privilegi necessari.|  
|42S01|Tabella o vista di base già esistente|\**StatementText* contiene un'istruzione **CREATE TABLE** o **CREATE VIEW** ed esiste già il nome della tabella o il nome della vista specificato.|  
|42S02 (in questo)|Tabella o vista di base non trovata|\**StatementText* contiene un'istruzione **DROP TABLE** o **DROP VIEW** e il nome della tabella o della vista specificato non esiste.<br /><br /> \**StatementText* contiene un'istruzione **ALTER TABLE** e il nome della tabella specificato non esisteva.<br /><br /> \**StatementText* contiene un'istruzione **CREATE VIEW** e non esisteva un nome di tabella o di vista definito dalla specifica della query.<br /><br /> \**StatementText* conteneva un'istruzione **CREATE INDEX** e il nome della tabella specificato non esisteva.<br /><br /> \**StatementText* contiene un'istruzione **GRANT** o **REVOKE** e il nome della tabella o della vista specificato non esisteva.<br /><br /> \**StatementText* contiene un'istruzione **SELECT** e non esisteva un nome di tabella o una vista specificata.<br /><br /> \**StatementText* contiene un'istruzione **DELETE**, **INSERT**o **UPDATE** e il nome di tabella specificato non esisteva.<br /><br /> \**StatementText* contiene un'istruzione **CREATE TABLE** e non esisteva una tabella specificata in un vincolo (che fa riferimento a una tabella diversa da quella creata).|  
|42S11|Indice già esistente|\**StatementText* contiene un'istruzione **CREATE INDEX** e il nome di indice specificato esisteva già.|  
|42S12|Indice non trovato|\**StatementText* conteneva un'istruzione **DROP INDEX** e il nome dell'indice specificato non esisteva.|  
|42S21|Colonna già esistente|\**StatementText* contiene un'istruzione **ALTER TABLE** e la colonna specificata nella clausola **ADD** non è univoca o identifica una colonna esistente nella tabella di base.|  
|42S22|Colonna non trovata|\**StatementText* conteneva un'istruzione **CREATE INDEX** e uno o più nomi di colonna specificati nell'elenco di colonne non esistevano.<br /><br /> \**StatementText* contiene un'istruzione **GRANT** o **REVOKE** e non esisteva un nome di colonna specificato.<br /><br /> \**StatementText* contiene un'istruzione **SELECT**, **DELETE**, **INSERT**o **UPDATE** e non esisteva un nome di colonna specificato.<br /><br /> \**StatementText* contiene un'istruzione **CREATE TABLE** e una colonna specificata in un vincolo (che fa riferimento a una tabella diversa da quella creata) non esisteva.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*, quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|I009|Utilizzo non valido del puntatore null|(DM) *StatementText* era un puntatore null.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLPrepare.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) l'argomento *TextLength* era minore o uguale a 0 ma non uguale a SQL_NTS.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|L'impostazione di concorrenza non è valida per il tipo di cursore definito.<br /><br /> L'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_VARIABLE e l'attributo dell'istruzione SQL_ATTR_CURSOR_TYPE è stato impostato su un tipo di cursore per il quale il driver non supporta i segnalibri.|  
|HYT00|Timeout|Periodo di timeout scaduto prima che l'origine dati restituisca il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 L'applicazione chiama **SQLPrepare** per inviare un'istruzione SQL all'origine dati per la preparazione. Per ulteriori informazioni sull'esecuzione preparata, vedere [Esecuzione preparata](../../../odbc/reference/develop-app/prepared-execution-odbc.md). L'applicazione può includere uno o più indicatori di parametro nell'istruzione SQL. Per includere un marcatore di parametro, l'applicazione incorpora un punto interrogativo (?) nella stringa SQL nella posizione appropriata. Per informazioni sui parametri, vedere [Parametri dell'istruzione](../../../odbc/reference/develop-app/statement-parameters.md).  
  
> [!NOTE]  
>  Se un'applicazione utilizza **SQLPrepare** per preparare e **SQLExecute** per inviare un'istruzione **COMMIT** o **ROLLBACK,** non sarà interoperabile tra i prodotti DBMS. Per eseguire il commit o il rollback di una transazione, chiamare **SQLEndTran**.  
  
 Il driver può modificare l'istruzione per utilizzare il modulo di SQL utilizzato dall'origine dati e quindi inviarlo all'origine dati per la preparazione. In particolare, il driver modifica le sequenze di escape utilizzate per definire la sintassi SQL per determinate funzionalità. (Per una descrizione della grammatica dell'istruzione SQL, vedere [sequenze](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) di escape in ODBC e [Appendice C: grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).) Per il driver, un handle di istruzione è simile a un identificatore di istruzione nel codice SQL incorporato. Se l'origine dati supporta gli identificatori di istruzione, il driver può inviare un identificatore di istruzione e valori di parametro all'origine dati.  
  
 Dopo la preparazione di un'istruzione, l'applicazione utilizza l'handle dell'istruzione per fare riferimento all'istruzione nelle chiamate di funzione successive. L'istruzione preparata associata all'handle dell'istruzione può essere rieseguita chiamando **SQLExecute** finché l'applicazione non libera l'istruzione con una chiamata a **SQLFreeStmt** con l'opzione SQL_DROP o fino a quando l'handle dell'istruzione non viene utilizzato in una chiamata a **SQLPrepare**, **SQLExecDirect**o a una delle funzioni di catalogo (**SQLColumns**, **SQLTables**e così via). Una volta preparata un'istruzione, l'applicazione può richiedere informazioni sul formato del set di risultati. Per alcune implementazioni, la chiamata a **SQLDescribeCol** o **SQLDescribeParam** dopo **SQLPrepare** potrebbe non essere efficiente come la chiamata alla funzione dopo **SQLExecute** o **SQLExecDirect**.  
  
 Alcuni driver non possono restituire errori di sintassi o violazioni di accesso quando l'applicazione chiama **SQLPrepare**. Un driver può gestire gli errori di sintassi e le violazioni di accesso, ma solo gli errori di sintassi, né gli errori di sintassi né le violazioni di accesso. Pertanto, un'applicazione deve essere in grado di gestire queste condizioni quando si chiamano funzioni correlate successive, ad esempio **SQLNumResultCols**, **SQLDescribeCol**, **SQLColAttribute**e **SQLExecute**.  
  
 A seconda delle funzionalità del driver e dell'origine dati, le informazioni sui parametri (ad esempio i tipi di dati) potrebbero essere controllate quando l'istruzione viene preparata (se tutti i parametri sono stati associati) o quando viene eseguita (se tutti i parametri non sono stati associati). Per garantire la massima interoperabilità, un'applicazione deve annullare l'associazione di tutti i parametri applicati a un'istruzione SQL precedente prima di preparare una nuova istruzione SQL nella stessa istruzione. In questo modo si evitano gli errori dovuti all'applicazione delle informazioni sui parametri precedenti alla nuova istruzione.  
  
> [!IMPORTANT]  
>  Il commit di una transazione, chiamando in modo esplicito **SQLEndTran** o utilizzando la modalità autocommit, può causare l'eliminazione dei piani di accesso per tutte le istruzioni su una connessione. Per ulteriori informazioni, vedere i tipi di informazioni SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR in [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [Effetto delle transazioni sui cursori e](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)sulle istruzioni preparate .  
  
## <a name="code-example"></a>Esempio di codice  
 Vedere [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Allocazione di un handle di istruzione|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Associazione di un buffer a un parametro|[Pagina relativa alla funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Esecuzione di un'operazione di commit o rollbackExecuting a commit or rollback operation|[SQLEndTran Function](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Restituzione del numero di righe interessate da un'istruzione|[SQLRowCount Function](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|Impostazione del nome di un cursore|[Funzione SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
