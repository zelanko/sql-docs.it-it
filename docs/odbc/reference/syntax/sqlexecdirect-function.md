---
title: Funzione SQLExecDirect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExecDirect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecDirect
helpviewer_keywords:
- SQLExecDirect function [ODBC]
ms.assetid: 985fcee1-f204-425c-bdd1-deb0e7d7bbd9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0fa34020478308c1e0d5c5fe112bbeb04920f07e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003118"
---
# <a name="sqlexecdirect-function"></a>Funzione SQLExecDirect
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLExecDirect** esegue un'istruzione preparabile, usando i valori correnti delle variabili di marcatore di parametro, se sono presenti parametri nell'istruzione. **SQLExecDirect** il modo più semplice per inviare un'istruzione SQL per una singola esecuzione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *StatementText*  
 [Input] Istruzione SQL da eseguire.  
  
 *TextLength*  
 [Input] Lunghezza di **StatementText* in caratteri.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE o SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLExecDirect** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato può essere ottenuto chiamando **SQLGetDiagRec** con un *HandleType* SQL_HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLExecDirect** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01001|Conflitto dell'operazione del cursore|\**StatementText* indipendente posizionata un'istruzione update o delete e più righe oppure nessuna riga sono stati aggiornati o eliminati. (Per altre informazioni sugli aggiornamenti per più di una riga, vedere la descrizione del SQL_ATTR_SIMULATE_CURSOR *attributo* nelle **SQLSetStmtAttr**.)<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01003|Valore NULL eliminato nella funzione sui set|L'argomento *StatementText* contenuta una funzione sui set (ad esempio **AVG**, **MAX**, **MIN**e così via), ma non la **conteggio**  set (funzione) e l'argomento NULL i valori sono stati eliminati prima la funzione è stata applicata. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Dati binari o di stringa restituito per un input/output o parametro di output ha comportato il troncamento del carattere non vuote o dati binari non NULL. Se si tratta di un valore stringa, era troncati a destra. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01006|Privilegio non revocato.|\**StatementText* contenuti un **revocare** istruzione e l'utente non dispone del privilegio specificato. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01007|Privilegio non concesso|*\*StatementText* era un **concessione** istruzione e l'utente non è stato possibile concedere il privilegio specificato.|  
|01S02|Valore di opzione modificato|Un attributo di istruzione specificato non è valido a causa di condizioni di lavoro di implementazione, pertanto è stata temporaneamente sostituito con un valore simile. (**SQLGetStmtAttr** può essere chiamato per determinare quale sia il valore di sostituzione temporaneamente.) Il valore di sostituzione è valido per il *StatementHandle* fino a quando il cursore è chiuso, a quel punto l'attributo dell'istruzione viene ripristinato il valore precedente. Gli attributi di istruzione che è possibile modificare sono:<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT  SQL_ ATTR_SIMULATE_CURSOR<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01S07|Troncamento frazionario.|I dati restituiti per un input/output o parametro di output è stato troncato in modo che la parte frazionaria di un tipo di dati numerici sono stata troncata o la parte frazionaria del componente di un tipo di dati di ora, timestamp o intervallo di tempo è stata troncata.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07002|Campo COUNT non corretto|Il numero di parametri specificati in **SQLBindParameter** era minore rispetto al numero di parametri nell'istruzione SQL racchiusa \* *StatementText*.<br /><br /> **SQLBindParameter** è stato chiamato con *ParameterValuePtr* impostata su un puntatore null *StrLen_or_IndPtr* non è impostata su SQL_NULL_DATA o SQL_DATA_AT_EXEC, e *InputOutputType*  non impostata su SQL_PARAM_OUTPUT, in modo che il numero di parametri specificato nel **SQLBindParameter** è maggiore del numero di parametri nell'istruzione SQL contenuti in **StatementText* .|  
|07006|Violazione dell'attributo del tipo di dati|Il valore di dati identificato dal *ValueType* argomento nella **SQLBindParameter** per non è stato possibile convertire il parametro associato al tipo di dati identificato dal *ParameterType*nell'argomento **SQLBindParameter**.<br /><br /> Il valore di dati restituito per un parametro di associazione come SQL_PARAM_OUTPUT o SQL_PARAM_INPUT_OUTPUT non è stato possibile convertire il tipo di dati identificato dal *ValueType* nell'argomento **SQLBindParameter**.<br /><br /> (Se non è stato possibile convertire i valori dei dati per una o più righe, ma una o più righe sono state restituite correttamente, questa funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07007|Violazione del valore del parametro con restrizioni|Il tipo di parametro SQL_PARAM_INPUT_OUTPUT_STREAM serve solo per un parametro che invia e riceve i dati in parti. Un buffer di input associato non è consentito per questo tipo di parametro.<br /><br /> Questo errore si verifica quando il tipo di parametro è SQL_PARAM_INPUT_OUTPUT e quando le \* *StrLen_or_IndPtr* specificata in **SQLBindParameter** non è uguale a SQL_NULL_DATA, SQL_DEFAULT_ PARAM, SQL_LEN_DATA_AT_EXEC(len) o SQL_DATA_AT_EXEC.|  
|07S01|Utilizzo non valido del parametro predefinito|Un valore del parametro, impostata con **SQLBindParameter**era SQL_DEFAULT_PARAM e il parametro corrispondente non è un valore predefinito.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|21S01|Elenco di valori di inserimento non corrisponde elenco colonne|\**StatementText* contenute un' **Inserisci** istruzione e il numero di valori da inserire non corrisponde il grado della tabella derivata.|  
|21S02|Livello di tabella derivata corrisponde a elenco di colonne|\**StatementText* contenuti un **CREATE VIEW** istruzione e l'elenco di colonna non qualificati (il numero di colonne specificato per la visualizzazione nel *colonna identificatore* gli argomenti di SQL istruzione) contenuti nomi di più rispetto al numero di colonne della tabella derivata definita dal *query-specification* argomento dell'istruzione SQL.|  
|22001|Dati di tipo stringa, troncamento a destra|L'assegnazione di un carattere o un valore binario a una colonna ha comportato il troncamento dei dati di tipo carattere non vuote o dati binari non null.|  
|22002|Variabile indicatore necessaria ma non fornito|I dati NULL è stati associati a un parametro di output il cui *StrLen_or_IndPtr* effettui **SQLBindParameter** era un puntatore null.|  
|22003|Valore numerico non compreso nell'intervallo|**StatementText* conteneva un'istruzione SQL contenente un parametro numerico associato o un valore letterale e il valore ha causato la parte intera (in contrapposizione frazionari) del numero da troncare quando assegnato alla colonna della tabella associata.<br /><br /> Restituzione di un valore numerico (come valore numerico o stringa) per uno o più parametri di input/output o di output avrebbe causato la parte intera (in contrapposizione frazionari) del numero da troncare.|  
|22007|Formato di datetime non valido|**StatementText* conteneva un'istruzione SQL contenente una data, ora o timestamp struttura come parametro di associazione e il parametro è, rispettivamente, una data non valida, ora o timestamp.<br /><br /> Un parametro di input/output o di output è stato associato a una data, ora o timestamp C struttura e un valore nel parametro restituito non è, rispettivamente, una data non valida, ora o timestamp. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|22008|Overflow del campo DateTime|**StatementText* contenuta un'istruzione SQL che contiene un'espressione datetime che, quando calcolato, dà come risultato una data, ora o timestamp struttura che non è valida.<br /><br /> Un'espressione datetime calcolate per input/output o parametro di output ha comportato una data, ora o struttura di timestamp C che non è valido.|  
|22012|Divisione per zero|**StatementText* conteneva un'istruzione SQL contenente un'espressione aritmetica che ha causato la divisione per zero.<br /><br /> Un'espressione aritmetica calcolato per input/output o un parametro di output ha comportato la divisione per zero.|  
|22015|Overflow del campo Interval|*\*StatementText* contiene un parametro numerico o intervallo esatto che, quando convertito in un intervallo di tipo di dati SQL, ha causato una perdita di cifre significative.<br /><br /> *\*StatementText* contiene un parametro di intervallo con più di un campo che, quando convertito in un tipo di dati numerici in una colonna, non aveva alcuna rappresentazione nel tipo di dati numerici.<br /><br /> *\*StatementText* conteneva dati di parametro che è stati assegnati a un intervallo di tipo SQL e si è verificato alcuna rappresentazione del valore di tipo C in un intervallo di tipo SQL.<br /><br /> Assegnazione di un parametro di input/output o di output che è stato un numerico esatto o l'intervallo di tipo SQL a un tipo di intervallo C ha causato una perdita di cifre significative.<br /><br /> Quando un parametro di input/output o di output è stato assegnato a una struttura di intervallo C, si è verificato alcun rappresentazione dei dati nella struttura di dati di intervallo.|  
|22018|Valore del carattere non valido per la specifica del cast|*\*StatementText* contenevano un tipo C che è un valore numerico esatto o approssimativo, un valore datetime o un tipo di dati di intervallo, il tipo SQL della colonna è un tipo di dati carattere; e il valore nella colonna non è un valore letterale valido del tipo C associato.<br /><br /> Quando è stato restituito un parametro di input/output o di output, il tipo SQL è un valore numerico esatto o approssimativo, un valore datetime o un tipo di dati di intervallo. il tipo C è stata SQL_C_CHAR; e il valore nella colonna non è un valore letterale valido del tipo SQL associato.|  
|22019|Carattere di escape non valido|\**StatementText* conteneva un'istruzione SQL che conteneva una **, ad esempio** predicato con un **ESCAPE** nel **dove** clausola e la lunghezza del carattere di escape carattere che segue **ESCAPE** non è uguale a 1.|  
|22025|Sequenza di escape non valido|\**StatementText* conteneva un'istruzione SQL contenente " **, ad esempio** _valore di schema_ **ESCAPE** _carattere di escape_ "nel **in cui** clausola e il carattere che segue il carattere di escape nel valore del modello non corrisponde a uno di"%"o"_".|  
|23000|Violazione di vincolo di integrità|**StatementText* conteneva un'istruzione SQL contenente un parametro o valore letterale. Il valore del parametro non NULL per una colonna definita come NOT NULL nella colonna della tabella associati, un valore duplicato è stato fornito per una colonna vincolata a contenere solo valori univoci, o un altro vincolo di integrità è stato violato.|  
|24000|Stato del cursore non valido|Un cursore è posizionato in corrispondenza di *StatementHandle* dal **SQLFetch** oppure **SQLFetchScroll**. Questo errore viene restituito da Gestione Driver, se **SQLFetch** oppure **SQLFetchScroll** non restituisce SQL_NO_DATA e viene restituito dal driver se **SQLFetch** oppure **SQLFetchScroll** è stato restituito SQL_NO_DATA.<br /><br /> Il cursore è stato aperto, ma non posizionato in corrispondenza di *StatementHandle*.<br /><br /> **StatementText* indipendente posizionata un'istruzione update o delete, e il cursore era posizionato prima dell'inizio del set di risultati o dopo la fine del set di risultati.|  
|34000|Nome di cursore non valido|**StatementText* indipendente posizionata un'istruzione update o delete e il cursore fa riferimento l'istruzione eseguita non è stato aperto.|  
|3D000|Nome catalogo non valido|Il nome del catalogo specificato nel *StatementText* non è valido.|  
|3F000|Nome dello schema non valido|Il nome dello schema specificato nel *StatementText* non è valido.|  
|40001|Errore di serializzazione.|Il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|42000|La sintassi o violazione di accesso|\**StatementText* conteneva un'istruzione SQL che non è stato degli elementi preparabili o contenuto un errore di sintassi.<br /><br /> L'utente non dispone dell'autorizzazione per eseguire l'istruzione SQL contenuto in **StatementText*.|  
|42S01|Tabella di base o vista già esistente|\**StatementText* contenuti un **CREATE TABLE** oppure **CREATE VIEW** istruzione e il nome della tabella o vista nome specificato esiste già.|  
|42S02|Tabella di base o della vista non trovato|\**StatementText* contenuti un **DROP TABLE** o una **DROP VIEW** istruzione e la vista nome non esiste o il nome di tabella specificata.<br /><br /> \**StatementText* contenute un' **ALTER TABLE** istruzione e il nome della tabella specificata non esiste.<br /><br /> \**StatementText* contenuti un **CREATE VIEW** istruzione e un nome di tabella o vista nome definito dalla specifica di query non esiste.<br /><br /> \**StatementText* contenuti un **CREATE INDEX** istruzione e il nome della tabella specificata non esiste.<br /><br /> \**StatementText* contenuti un **concessione** oppure **revocare** istruzione e la vista nome non esiste o il nome di tabella specificata.<br /><br /> \**StatementText* contenuti un **selezionare** istruzione e una vista nome non esiste o il nome di tabella specificata.<br /><br /> \**StatementText* contenuti un **eliminare**, **Inserisci**, oppure **UPDATE** istruzione e il nome della tabella specificata non esiste.<br /><br /> \**StatementText* contenuti un **CREATE TABLE** istruzione e una tabella specificata in un vincolo (riferimento a una tabella diverso da quello creato) non esiste.<br /><br /> \**StatementText* contenuti un **CREATE SCHEMA** istruzione e una vista nome non esiste o il nome di tabella specificata.|  
|42S11|L'indice esiste già|\**StatementText* contenuti un **CREATE INDEX** istruzione e il nome dell'indice specificato esiste già.<br /><br /> \**StatementText* contenuti un **CREATE SCHEMA** istruzione e il nome dell'indice specificato esiste già.|  
|42S12|Indice non trovato|\**StatementText* contenuti un **DROP INDEX** istruzione e il nome dell'indice specificato non esiste.|  
|42S21|Esiste già una colonna|\**StatementText* contenute un' **ALTER TABLE** istruzione e la colonna specificata nel **aggiungere** clausola non è univoca oppure per identificare una colonna esistente nella tabella di base.|  
|42S22|Colonna non trovata|\**StatementText* contenuti un **CREATE INDEX** istruzione e uno o più della colonna dei nomi specificati nell'elenco delle colonne non esiste.<br /><br /> \**StatementText* contenuti un **concessione** oppure **revocare** informativa e un nome di colonna specificato non esiste.<br /><br /> \**StatementText* contenuti un **seleziona**, **eliminare**, **inserire**, o **UPDATE** informativa e un nome di colonna specificato non esiste.<br /><br /> \**StatementText* contenuti un **CREATE TABLE** istruzione e una colonna specificata in un vincolo (riferimento a una tabella diverso da quello creato) non esiste.<br /><br /> \**StatementText* contenuti un **CREATE SCHEMA** informativa e un nome di colonna specificato non esiste.|  
|44000|Violazione della clausola WITH CHECK OPTION|L'argomento *StatementText* contenuta un' **Inserisci** istruzione eseguita su una tabella visualizzata o una tabella derivata nella tabella visualizzata in cui è stato creato specificando **WITH CHECK OPTION**, in modo che uno o più righe interessate dal **Inserisci** istruzione non saranno presente nella tabella visualizzata.<br /><br /> L'argomento *StatementText* contenuta un' **UPDATE** istruzione eseguita su una tabella visualizzata o una tabella derivata nella tabella visualizzata in cui è stato creato specificando **WITH CHECK OPTION**, in modo che uno o più righe interessate dal **UPDATE** istruzione non saranno presente nella tabella visualizzata.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle*. Quindi la funzione è stata chiamata nuovamente sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY009|Utilizzo non valido del puntatore null|(DM) **StatementText* era un puntatore null.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLExecDirect** funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) dell'argomento *SetFocus per effettuare* era minore o uguale a 0 ma non è uguale a SQL_NTS.<br /><br /> Un valore del parametro, impostata con **SQLBindParameter**, era un puntatore null e il valore di lunghezza parametro non è 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM, o minore o uguale a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Un valore del parametro, impostata con **SQLBindParameter**, non era un puntatore null; è stato il tipo di dati C SQL_C_BINARY o SQL_C_CHAR; e il valore di lunghezza del parametro è minore di 0 ma non è stato SQL_NTS, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_ PARAM, o minore o uguale a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Valore di lunghezza parametro vincolato dalle **SQLBindParameter** era impostata su SQL_DATA_AT_EXEC; il tipo SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY, o un tipo di dati specifici dell'origine dati di tipo long; e le informazioni di SQL_NEED_LONG_DATA_LEN digitare **SQLGetInfo** è "Y".|  
|HY105|Tipo di parametro non valido|Il valore specificato per l'argomento *InputOutputType* nelle **SQLBindParameter** era SQL_PARAM_OUTPUT e il parametro di un parametro di input.|  
|HY109|Posizione del cursore non valido|\**StatementText* indipendente posizionata un'istruzione update o delete, e il cursore era posizionato (da **SQLSetPos** oppure **SQLFetchScroll**) su una riga che era stata eliminata o non è stato possibile recuperare.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|La combinazione delle impostazioni correnti degli attributi di istruzione SQL_ATTR_CURSOR_TYPE e SQL_ATTR_CONCURRENCY non era supportata dall'origine dati o driver.<br /><br /> L'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_VARIABLE e l'attributo SQL_ATTR_CURSOR_TYPE di istruzione è stata impostata su un tipo di cursore per i quali il driver non supporta i segnalibri.|  
|HYT00|Timeout|Il periodo di timeout query scaduto prima che l'origine dati ha restituito il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 L'applicazione chiama **SQLExecDirect** per inviare un'istruzione SQL per l'origine dati. Per altre informazioni sull'esecuzione diretta, vedere [esecuzione diretta](../../../odbc/reference/develop-app/direct-execution-odbc.md). Il driver consente di modificare l'istruzione per usare il modulo di SQL dall'origine dati e quindi lo invia all'origine dati. In particolare, il driver consente di modificare le sequenze di escape utilizzate per definire alcune funzionalità in SQL. Per la sintassi di sequenze di escape, vedere [sequenze di Escape in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md).  
  
 L'applicazione può includere uno o più indicatori di parametro nell'istruzione SQL. Per includere un marcatore di parametro, l'applicazione incorpora un punto interrogativo (?) nell'istruzione SQL in corrispondenza della posizione appropriata. Per informazioni sui parametri, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Se l'istruzione SQL è un **selezionate** istruzione e se l'applicazione ha chiamato **SQLSetCursorName** per associare un cursore con un'istruzione, quindi il driver utilizza il cursore specificato. In caso contrario, il driver genera un nome di cursore.  
  
 Se l'origine dati è in modalità di commit manuale (che richiede di avviare le transazioni esplicite) e non è già stata avviata una transazione, il driver viene avviato una transazione prima di inviare l'istruzione SQL. Per altre informazioni, vedere [modalità di Commit manuale](../../../odbc/reference/develop-app/manual-commit-mode.md).  
  
 Se un'applicazione utilizza **SQLExecDirect** per inviare un **COMMIT** oppure **ROLLBACK** istruzione, non sarà possibile interoperabile tra prodotti DBMS. Per eseguire il commit o rollback della transazione, un'applicazione chiama **SQLEndTran**.  
  
 Se **SQLExecDirect** riscontrino un parametro data-at-execution, viene restituito SQL_NEED_DATA. L'applicazione invia i dati usando **SQLParamData** e **SQLPutData**. Visualizzare [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), e [invio di dati Long](../../../odbc/reference/develop-app/sending-long-data.md).  
  
 Se **SQLExecDirect** esegue un aggiornamento con ricerca, inserimento o istruzione delete che non influiscono su tutte le righe nell'origine dati, la chiamata a **SQLExecDirect** restituisce SQL_NO_DATA.  
  
 Se il valore dell'attributo di istruzione SQL_ATTR_PARAMSET_SIZE è maggiore di 1 e l'istruzione SQL contiene almeno un marcatore di parametro **SQLExecDirect** eseguirà l'istruzione SQL una volta per ogni set di valori di parametro da le matrici a cui fa riferimento il *ParameterValuePointer* argomento nella chiamata a **SQLBindParameter**. Per altre informazioni, vedere [matrici di valori di parametro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Se sono attivati i segnalibri e viene eseguita una query che non supportano i segnalibri, il driver deve tentare di assegnare l'ambiente con uno che supporta segnalibri se si modifica un valore di attributo e restituendo un valore SQLSTATE 01S02 (valore dell'opzione modificato). Se l'attributo non può essere modificato, il driver deve restituire SQLSTATE HY024 (valore di attributo non valido).  
  
> [!NOTE]  
>  Quando si usa il pool di connessioni, un'applicazione non deve eseguire istruzioni SQL che modificano il database o il contesto del database, ad esempio la **utilizzo** _database_ istruzione in SQL Server, che viene modificato il catalogo utilizzato da un'origine dati.  
  
## <a name="code-example"></a>Esempio di codice  
 Visualizzare [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), e [ODBC programma di esempio](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultati|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|L'esecuzione di un'operazione di commit o rollback|[Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Il recupero di più righe di dati|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Imposta il recupero di un blocco di dati o lo scorrimento di un risultato|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Restituzione di un nome di cursore|[Funzione SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Durante il recupero o parte di una colonna di dati|[Funzione SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Restituisce il parametro successivo per l'invio di dati|[Funzione SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Preparazione di un'istruzione per l'esecuzione|[Funzione SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|L'invio dei dati di parametro in fase di esecuzione|[Funzione SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Impostazione di un nome di cursore|[Funzione SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|L'impostazione di un attributo di istruzione|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
