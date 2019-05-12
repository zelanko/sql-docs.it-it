---
title: Funzione SQLPrepare | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c77f8e6bd137b557b150ba91c143abb5438778c8
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536626"
---
# <a name="sqlprepare-function"></a>Pagina relativa alla funzione SQLPrepare
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
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
 [Input] Handle di istruzione.  
  
 *StatementText*  
 [Input] Stringa di testo SQL.  
  
 *TextLength*  
 [Input] Lunghezza di **StatementText* in caratteri.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLPrepare** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLPrepare** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01S02|Valore di opzione modificato|Un attributo di istruzione specificato non è valido a causa di condizioni di lavoro di implementazione, pertanto è stata temporaneamente sostituito con un valore simile. (**SQLGetStmtAttr** può essere chiamato per determinare quale sia il valore di sostituzione temporaneamente.) Il valore di sostituzione è valido per il *StatementHandle* fino a quando il cursore è chiuso. Gli attributi di istruzione che è possibile modificare sono: SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|21S01|Elenco di valori di inserimento non corrisponde elenco colonne|\**StatementText* contenute un' **Inserisci** istruzione e il numero di valori da inserire non corrisponde il grado della tabella derivata.|  
|21S02|Livello di tabella derivata corrisponde a elenco di colonne|\**StatementText* contenuti un **CREATE VIEW** istruzione e il numero dei nomi specificato non è lo stesso livello della tabella derivata definita nella specifica di query.|  
|22018|Valore del carattere non valido per la specifica del cast|**StatementText* conteneva un'istruzione SQL che conteneva un valore letterale o un parametro e il valore è incompatibile con il tipo di dati della colonna della tabella associata.|  
|22019|Carattere di escape non valido|L'argomento *StatementText* contenuta una **, ad esempio** predicato con un **ESCAPE** nel **dove** clausola e la lunghezza del carattere di escape carattere che segue **ESCAPE** non è uguale a 1.|  
|22025|Sequenza di escape non valido|L'argomento *StatementText* contenute "**quali** _valore di schema_ **ESCAPE** _caratterediescape_"nel **in cui** clausola e il carattere che segue il carattere di escape nel valore del modello è stato"%"né"_".|  
|24000|Stato del cursore non valido|(DM) un cursore è stato aperto scegliere il *StatementHandle*, e **SQLFetch** oppure **SQLFetchScroll** fosse stata chiamata.<br /><br /> Un cursore è stato aperto nel *StatementHandle*, ma **SQLFetch** oppure **SQLFetchScroll** non fosse stata chiamata.|  
|34000|Nome di cursore non valido|\**StatementText* contenuti un posizionati **eliminare** o un oggetto posizionato **UPDATE**, e il cursore fa riferimento l'istruzione preparata non è stato aperto.|  
|3D000|Nome catalogo non valido|Il nome del catalogo specificato nel *StatementText* non è valido.|  
|3F000|Nome dello schema non valido|Il nome dello schema specificato nel *StatementText* non è valido.|  
|42000|La sintassi o violazione di accesso|\**StatementText* conteneva un'istruzione SQL che non è stato degli elementi preparabili o contenuto un errore di sintassi.<br /><br /> **StatementText* conteneva un'istruzione per il quale l'utente non dispone dei privilegi necessari.|  
|42S01|Tabella di base o vista già esistente|\**StatementText* contenuti un **CREATE TABLE** oppure **CREATE VIEW** istruzione e il nome della tabella o vista nome specificato esiste già.|  
|42S02|Tabella di base o della vista non trovato|\**StatementText* contenuti un **DROP TABLE** o una **DROP VIEW** istruzione e la vista nome non esiste o il nome di tabella specificata.<br /><br /> \**StatementText* contenute un' **ALTER TABLE** istruzione e il nome della tabella specificata non esiste.<br /><br /> \**StatementText* contenuti un **CREATE VIEW** istruzione e un nome di tabella o vista nome definito dalla specifica di query non esiste.<br /><br /> \**StatementText* contenuti un **CREATE INDEX** istruzione e il nome della tabella specificata non esiste.<br /><br /> \**StatementText* contenuti un **concessione** oppure **revocare** istruzione e la vista nome non esiste o il nome di tabella specificata.<br /><br /> \**StatementText* contenuti un **selezionare** istruzione e una vista nome non esiste o il nome di tabella specificata.<br /><br /> \**StatementText* contenuti un **eliminare**, **Inserisci**, oppure **UPDATE** istruzione e il nome della tabella specificata non esiste.<br /><br /> \**StatementText* contenuti un **CREATE TABLE** istruzione e una tabella specificata in un vincolo (riferimento a una tabella diverso da quello creato) non esiste.|  
|42S11|L'indice esiste già|\**StatementText* contenuti un **CREATE INDEX** istruzione e il nome dell'indice specificato esiste già.|  
|42S12|Indice non trovato|\**StatementText* contenuti un **DROP INDEX** istruzione e il nome dell'indice specificato non esiste.|  
|42S21|Esiste già una colonna|\**StatementText* contenute un' **ALTER TABLE** istruzione e la colonna specificata nel **aggiungere** clausola non è univoca oppure per identificare una colonna esistente nella tabella di base.|  
|42S22|Colonna non trovata|\**StatementText* contenuti un **CREATE INDEX** istruzione e uno o più della colonna dei nomi specificati nell'elenco delle colonne non esiste.<br /><br /> \**StatementText* contenuti un **concessione** oppure **revocare** informativa e un nome di colonna specificato non esiste.<br /><br /> \**StatementText* contenuti un **seleziona**, **eliminare**, **inserire**, o **UPDATE** informativa e un nome di colonna specificato non esiste.<br /><br /> \**StatementText* contenuti un **CREATE TABLE** istruzione e una colonna specificata in un vincolo (riferimento a una tabella diverso da quello creato) non esiste.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle*, quindi è stata chiamata la funzione anche in questo caso sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY009|Utilizzo non valido del puntatore null|(DM) *StatementText* era un puntatore null.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLPrepare** funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) dell'argomento *SetFocus per effettuare* era minore o uguale a 0 ma non è uguale a SQL_NTS.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|L'impostazione di concorrenza non è valido per il tipo di cursore definito.<br /><br /> L'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_VARIABLE e l'attributo SQL_ATTR_CURSOR_TYPE di istruzione è stata impostata su un tipo di cursore per i quali il driver non supporta i segnalibri.|  
|HYT00|Timeout|Il periodo di timeout è scaduto prima che l'origine dati ha restituito il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 L'applicazione chiama **SQLPrepare** per inviare un'istruzione SQL per l'origine dati per la preparazione. Per altre informazioni sull'esecuzione preparata, vedere [esecuzione preparata](../../../odbc/reference/develop-app/prepared-execution-odbc.md). L'applicazione può includere uno o più indicatori di parametro nell'istruzione SQL. Per includere un marcatore di parametro, l'applicazione incorpora un punto interrogativo (?) nella stringa SQL in corrispondenza della posizione appropriata. Per informazioni sui parametri, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md).  
  
> [!NOTE]  
>  Se un'applicazione utilizza **SQLPrepare** preparare e **SQLExecute** per inviare un **COMMIT** oppure **ROLLBACK** istruzione, non sarà interoperabilità tra prodotti DBMS. Per eseguire il commit o rollback della transazione, chiamare **SQLEndTran**.  
  
 Il driver è possibile modificare l'istruzione per usare il modulo di SQL dall'origine dati e quindi inviarlo per l'origine dati per la preparazione. In particolare, il driver consente di modificare le sequenze di escape utilizzate per definire la sintassi SQL per determinate funzionalità. (Per una descrizione della grammatica di istruzione SQL, vedere [sequenze di Escape in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) e [appendice c: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).) Per il driver, un handle di istruzione è simile a un identificatore di istruzione nel codice SQL incorporato. Se l'origine dati supporta gli identificatori di istruzione, il driver può inviare un identificatore di istruzione e i valori dei parametri per l'origine dati.  
  
 Dopo che viene preparata un'istruzione, l'applicazione usa l'handle di istruzione per vedere l'informativa nelle successive chiamate di funzione. L'istruzione preparata associata all'handle di istruzione può essere eseguita nuovamente chiamando **SQLExecute** fino a quando l'applicazione rilascia l'istruzione con una chiamata a **SQLFreeStmt** con l'opzione SQL_DROP o fino a quando non viene utilizzato l'handle di istruzione in una chiamata a **SQLPrepare**, **SQLExecDirect**, o una delle funzioni di catalogo (**SQLColumns**,  **SQLTables**e così via). Dopo l'applicazione viene preparata un'istruzione, è possibile richiedere informazioni sul formato del set di risultati. Per alcune implementazioni, la chiamata **SQLDescribeCol** oppure **SQLDescribeParam** dopo **SQLPrepare** potrebbe non essere più efficiente la chiamata alla funzione dopo **SQLExecute** oppure **SQLExecDirect**.  
  
 Alcuni driver non è possibile restituire gli errori di sintassi o violazioni di accesso quando l'applicazione chiama **SQLPrepare**. Un driver può gestire gli errori di sintassi e violazioni di accesso, solo gli errori di sintassi o gli errori di sintassi né violazioni di accesso. Pertanto, un'applicazione deve essere in grado di gestire queste condizioni durante la chiamata successiva correlati, ad esempio le funzioni **SQLNumResultCols**, **SQLDescribeCol**, **SQLColAttribute**, e **SQLExecute**.  
  
 A seconda delle funzionalità del driver e origine dati, le informazioni sui parametri (ad esempio, i tipi di dati) potrebbero essere archiviati quando l'istruzione viene preparata (se tutti i parametri sono stati associati) o quando viene eseguito (se tutti i parametri non sono stati associati). Per garantire la massima interoperabilità, un'applicazione deve annullare l'associazione di tutti i parametri che applicato a un'istruzione SQL precedente prima di preparare una nuova istruzione SQL nella stessa istruzione. Ciò impedisce che gli errori dovuti ai vecchi informazioni sul parametro cui applicare la nuova istruzione.  
  
> [!IMPORTANT]  
>  Commit di una transazione, in modo esplicito chiamando **SQLEndTran** o la possibilità di lavorare in modalità autocommit, possono causare l'origine dati eliminare i piani di accesso per tutte le istruzioni in una connessione. Per altre informazioni, vedere i tipi di informazioni SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR nelle [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [effettiva delle transazioni su cursori e istruzioni preparate](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Visualizzare [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Allocare un handle di istruzione|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Associazione di un buffer a una colonna in un set di risultati|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Associazione di un buffer a un parametro|[Funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|L'esecuzione di un'operazione di commit o rollback|[Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Esecuzione di un'istruzione SQL|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Restituzione del numero di righe interessate da un'istruzione|[Funzione SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|Impostazione di un nome di cursore|[Funzione SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
