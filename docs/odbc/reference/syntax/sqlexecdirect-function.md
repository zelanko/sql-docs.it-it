---
title: SQLExecDirect (funzione) . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5739e397467deb684a4cd6c7b13a507f30b53fa7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286111"
---
# <a name="sqlexecdirect-function"></a>Funzione SQLExecDirect
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLExecDirect** esegue un'istruzione preparabile, utilizzando i valori correnti delle variabili del marcatore di parametro se esistono parametri nell'istruzione. **SQLExecDirect** è il modo più veloce per inviare un'istruzione SQL per l'esecuzione una tantera.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *StatementText (TestoIstruzioni)*  
 [Ingresso] Istruzione SQL da eseguire.  
  
 *TextLength*  
 [Ingresso] Lunghezza del valore*di StatementText* in caratteri.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE o SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLExecDirect** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *Handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLExecDirect** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01001|Conflitto di funzionamento del cursoreCursor operation conflict|\**StatementText* contiene un'istruzione di aggiornamento o eliminazione posizionata e nessuna riga o più di una riga è stata aggiornata o eliminata. Per ulteriori informazioni sugli aggiornamenti a più righe, vedere la descrizione *dell'attributo* SQL_ATTR_SIMULATE_CURSOR in **SQLSetStmtAttr**.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01003|Valore NULL eliminato nella funzione set|L'argomento *StatementText* contiene una funzione set (ad esempio **AVG**, **MAX**, **MIN**e così via), ma non la funzione **set COUNT** e i valori degli argomenti NULL sono stati eliminati prima dell'applicazione della funzione. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Dati stringa o binari restituiti per un parametro di input/output o di output hanno determinato il troncamento di caratteri non vuoti o dati binari non NULL. Se si tratta di un valore stringa, è stato troncato a destra. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01006|Privilegio non revocato|\**StatementText* conteneva un'istruzione **REVOKE** e l'utente non disponeva del privilegio specificato. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01007|Privilegio non concesso|StatementText era un'istruzione **GRANT** e all'utente non è stato possibile concedere il privilegio specificato. * \**|  
|01S02 (in questo stato di|Valore dell'opzione modificato|Un attributo di istruzione specificato non è valido a causa delle condizioni di lavoro di implementazione, pertanto un valore simile è stato temporaneamente sostituito. **SQLGetStmtAttr** può essere chiamato per determinare il valore sostituito temporaneamente. Il valore sostitutivo è valido per *il StatementHandle* fino a quando il cursore viene chiuso, a quel punto l'attributo di istruzione viene ripristinato il valore precedente. Gli attributi dell'istruzione che possono essere modificati sono:The statement attributes that can be changed are:<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ ATTR_SIMULATE_CURSOR<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S07 (intito)|Troncamento frazionario|I dati restituiti per un parametro di input/output o di output sono stati troncati in modo che la parte frazionaria di un tipo di dati numerico sia stata troncata o che la parte frazionaria del componente ora di un tipo di dati time, timestamp o interval sia stata troncata.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07002|Campo COUNT non corretto|Il numero di parametri specificato in **SQLBindParameter** è minore del \*numero di parametri nell'istruzione SQL contenuta in *StatementText*.<br /><br /> **SQLBindParameter** è stato chiamato con *ParameterValuePtr* impostato su un puntatore null, *StrLen_or_IndPtr* non impostato su SQL_NULL_DATA o SQL_DATA_AT_EXEC e *InputOutputType* non impostato su SQL_PARAM_OUTPUT, in modo che il numero di parametri specificati in **SQLBindParameter** sia maggiore del numero di parametri nell'istruzione SQL contenuta in *StatementText *.|  
|07006|Violazione dell'attributo del tipo di dati con restrizioniRestricted data type attribute violation|Impossibile convertire il valore di dati identificato dall'argomento *ValueType* in **SQLBindParameter** per il parametro associato nel tipo di dati identificato dall'argomento *ParameterType* in **SQLBindParameter**.<br /><br /> Il valore dei dati restituito per un parametro associato come SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT non può essere convertito nel tipo di dati identificato dall'argomento *ValueType* in **SQLBindParameter**.<br /><br /> Se non è stato possibile convertire i valori dei dati per una o più righe, ma una o più righe sono state restituite correttamente, questa funzione restituisce SQL_SUCCESS_WITH_INFO.|  
|07007|Violazione del valore dei parametri con restrizioni|Il tipo di parametro SQL_PARAM_INPUT_OUTPUT_STREAM viene utilizzato solo per un parametro che invia e riceve dati nelle parti. Un buffer associato di input non è consentito per questo tipo di parametro.<br /><br /> Questo errore si verifica quando il tipo \*di parametro è SQL_PARAM_INPUT_OUTPUT e quando il *StrLen_or_IndPtr* specificato in **SQLBindParameter** non è uguale a SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_LEN_DATA_AT_EXEC(len) o SQL_DATA_AT_EXEC.|  
|07S01 (in titola del sistema)|Utilizzo non valido del parametro predefinito|Un valore di parametro, impostato con **SQLBindParameter**, è stato SQL_DEFAULT_PARAM e il parametro corrispondente non dispone di un valore predefinito.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|21S01|L'elenco di valori di inserimento non corrisponde all'elenco di colonne|\**StatementText* contiene un'istruzione **INSERT** e il numero di valori da inserire non corrispondeva al grado della tabella derivata.|  
|21S02|Il grado della tabella derivata non corrisponde all'elenco di colonne|\**StatementText* conteneva un'istruzione **CREATE VIEW** e l'elenco di colonne non qualificate (il numero di colonne specificato per la visualizzazione negli argomenti *dell'identificatore* di colonna dell'istruzione SQL) conteneva più nomi del numero di colonne nella tabella derivata definita dall'argomento *query-specification* dell'istruzione SQL.|  
|22001|Dati stringa, troncamento a destra|L'assegnazione di un carattere o di un valore binario a una colonna ha determinato il troncamento di dati di tipo carattere non vuoto o dati binari non null.|  
|22002|Variabile indicatore richiesta ma non fornita|I dati NULL sono stati associati a un parametro di output il cui *StrLen_or_IndPtr* impostato da **SQLBindParameter** era un puntatore null.|  
|22003|Valore numerico non compreso nell'intervallo|**StatementText* conteneva un'istruzione SQL che conteneva un parametro numerico associato o un valore letterale e il valore causava il troncamento dell'intera parte (anziché frazionaria) del numero quando viene assegnata alla colonna della tabella associata.<br /><br /> La restituzione di un valore numerico (come numerico o stringa) per uno o più parametri di input/output o output avrebbe causato il troncamento dell'intera parte (anziché frazionaria).|  
|22007|Formato datetime non valido|**StatementText* contiene un'istruzione SQL che contiene una struttura di data, ora o timestamp come parametro associato e il parametro era, rispettivamente, una data, ora o timestamp non valido.<br /><br /> Un parametro di input/output o di output è stato associato a una struttura C di data, ora o timestamp e un valore nel parametro restituito è stato, rispettivamente, una data, un'ora o un timestamp non valido. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|22008|Overflow del campo Datetime|**StatementText* contiene un'istruzione SQL che contiene un'espressione datetime che, quando calcolata, ha restituito una struttura di data, ora o timestamp non valida.<br /><br /> Un'espressione datetime calcolata per un parametro di input/output o di output ha restituito una struttura C di data, ora o timestamp non valida.|  
|22012|Divisione per zero|**StatementText* contiene un'istruzione SQL che contiene un'espressione aritmetica che ha causato la divisione per zero.<br /><br /> Un'espressione aritmetica calcolata per un parametro di input/output o di output ha restituito la divisione per zero.|  
|22015|Overflow campo intervallo|StatementText conteneva un parametro numerico o intervallo esatto che, quando viene convertito in un tipo di dati SQL a intervalli, causava una perdita di cifre significative. * \**<br /><br /> StatementText conteneva un parametro di intervallo con più di un campo che, quando viene convertito in un tipo di dati numerico in una colonna, non disponeva di alcuna rappresentazione nel tipo di dati numerico. * \**<br /><br /> StatementText conteneva i dati del parametro assegnati a un tipo SQL a intervallo e non esisteva alcuna rappresentazione del valore del tipo C nel tipo SQL di intervallo. * \**<br /><br /> L'assegnazione di un parametro di input/output o di output che era un tipo SQL esatto numerico o a intervallo a un tipo di intervallo C ha causato una perdita di cifre significative.<br /><br /> Quando un parametro di input/output o di output è stato assegnato a una struttura di intervallo C, non esisteva alcuna rappresentazione dei dati nella struttura di dati dell'intervallo.|  
|22018|Valore di carattere non valido per la specifica del cast|StatementText conteneva un tipo C che era un numero esatto o approssimativo, un datetime o un tipo di dati interval; * \** il tipo SQL della colonna era un tipo di dati carattere; e il valore nella colonna non è un valore letterale valido del tipo C associato.<br /><br /> Quando viene restituito un parametro di input/output o di output, il tipo SQL era un numero esatto o approssimativo, un datetime o un tipo di dati interval; il tipo C è stato SQL_C_CHAR; e il valore nella colonna non è un valore letterale valido del tipo SQL associato.|  
|22019|Carattere di escape non valido|\**StatementText* conteneva un'istruzione SQL che conteneva un predicato **LIKE** con un **escape** nella clausola **WHERE** e la lunghezza del carattere di escape che segue **ESCAPE** non era uguale a 1.|  
|22025|Sequenza di escape non valida|\**StatementText* conteneva un'istruzione SQL che conteneva "**LIKE** _pattern value_ **ESCAPE** character di _escape_" nella clausola **WHERE** e il carattere che segue il carattere di escape nel valore del modello non era uno di "%" o "_".|  
|23000|Violazione dei vincoli di integrità|**StatementText* contiene un'istruzione SQL che contiene un parametro o un valore letterale. Il valore del parametro era NULL per una colonna definita come NOT NULL nella colonna della tabella associata, è stato fornito un valore duplicato per una colonna vincolata a contenere solo valori univoci o è stato violato un altro vincolo di integrità.|  
|24000|Stato del cursore non valido|Un cursore è stato posizionato su *StatementHandle* da **SQLFetch** o **SQLFetchScroll**. Questo errore viene restituito da Gestione Driver se **SQLFetch** o **SQLFetchScroll** non ha restituito SQL_NO_DATA e viene restituito dal driver se **SQLFetch** o **SQLFetchScroll** ha restituito SQL_NO_DATA.<br /><br /> Un cursore era aperto ma non posizionato su *StatementHandle*.<br /><br /> **StatementText* contiene un'istruzione di aggiornamento o eliminazione posizionata e il cursore è stato posizionato prima dell'inizio del set di risultati o dopo la fine del set di risultati.|  
|34000|Nome di cursore non valido|**StatementText* conteneva un'istruzione di aggiornamento o eliminazione posizionata e il cursore a cui fa riferimento l'istruzione in esecuzione non era aperto.|  
|3D000|Nome di catalogo non valido|Il nome del catalogo specificato in *StatementText* non è valido.|  
|3F000|Nome dello schema non valido|Il nome dello schema specificato in *StatementText* non è valido.|  
|40001|Errore di serializzazione|È stato eseguito il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|42000|Errore di sintassi o violazione di accesso|\**StatementText* contiene un'istruzione SQL non preparabile o contenente un errore di sintassi.<br /><br /> L'utente non disponedelle dell'autorizzazione per eseguire l'istruzione SQL contenuta in* a0> *.|  
|42S01|Tabella o vista di base già esistente|\**StatementText* contiene un'istruzione **CREATE TABLE** o **CREATE VIEW** ed esiste già il nome della tabella o il nome della vista specificato.|  
|42S02 (in questo)|Tabella o vista di base non trovata|\**StatementText* contiene un'istruzione **DROP TABLE** o **DROP VIEW** e il nome della tabella o della vista specificato non esiste.<br /><br /> \**StatementText* contiene un'istruzione **ALTER TABLE** e il nome della tabella specificato non esisteva.<br /><br /> \**StatementText* contiene un'istruzione **CREATE VIEW** e non esisteva un nome di tabella o di vista definito dalla specifica della query.<br /><br /> \**StatementText* conteneva un'istruzione **CREATE INDEX** e il nome della tabella specificato non esisteva.<br /><br /> \**StatementText* contiene un'istruzione **GRANT** o **REVOKE** e il nome della tabella o della vista specificato non esisteva.<br /><br /> \**StatementText* contiene un'istruzione **SELECT** e non esisteva un nome di tabella o una vista specificata.<br /><br /> \**StatementText* contiene un'istruzione **DELETE**, **INSERT**o **UPDATE** e il nome di tabella specificato non esisteva.<br /><br /> \**StatementText* contiene un'istruzione **CREATE TABLE** e non esisteva una tabella specificata in un vincolo (che fa riferimento a una tabella diversa da quella creata).<br /><br /> \**StatementText* contiene un'istruzione **CREATE SCHEMA** e non esisteva un nome di tabella o una vista specificata.|  
|42S11|Indice già esistente|\**StatementText* contiene un'istruzione **CREATE INDEX** e il nome di indice specificato esisteva già.<br /><br /> \**StatementText* contiene un'istruzione **CREATE SCHEMA** e il nome di indice specificato esisteva già.|  
|42S12|Indice non trovato|\**StatementText* conteneva un'istruzione **DROP INDEX** e il nome dell'indice specificato non esisteva.|  
|42S21|Colonna già esistente|\**StatementText* contiene un'istruzione **ALTER TABLE** e la colonna specificata nella clausola **ADD** non è univoca o identifica una colonna esistente nella tabella di base.|  
|42S22|Colonna non trovata|\**StatementText* conteneva un'istruzione **CREATE INDEX** e uno o più nomi di colonna specificati nell'elenco di colonne non esistevano.<br /><br /> \**StatementText* contiene un'istruzione **GRANT** o **REVOKE** e non esisteva un nome di colonna specificato.<br /><br /> \**StatementText* contiene un'istruzione **SELECT**, **DELETE**, **INSERT**o **UPDATE** e non esisteva un nome di colonna specificato.<br /><br /> \**StatementText* contiene un'istruzione **CREATE TABLE** e una colonna specificata in un vincolo (che fa riferimento a una tabella diversa da quella creata) non esisteva.<br /><br /> \**StatementText* contiene un'istruzione **CREATE SCHEMA** e non esisteva un nome di colonna specificato.|  
|44000|Violazione della clausola WITH CHECK OPTION|L'argomento *StatementText* conteneva un'istruzione **INSERT** eseguita su una tabella visualizzata o una tabella derivata dalla tabella visualizzata creata specificando **WITH CHECK OPTION**, in modo che una o più righe interessate dall'istruzione **INSERT** non saranno più presenti nella tabella visualizzata.<br /><br /> L'argomento *StatementText* conteneva un'istruzione **UPDATE** eseguita su una tabella visualizzata o una tabella derivata dalla tabella visualizzata creata specificando **WITH CHECK OPTION**, in modo che una o più righe interessate dall'istruzione **UPDATE** non saranno più presenti nella tabella visualizzata.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*. Quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|I009|Utilizzo non valido del puntatore null|(DM) -*StatementText* è un puntatore null.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLExecDirect.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) l'argomento *TextLength* era minore o uguale a 0 ma non uguale a SQL_NTS.<br /><br /> Un valore di parametro, impostato con **SQLBindParameter**, è un puntatore null e il valore della lunghezza del parametro non è 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM o minore o uguale a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Un valore di parametro, impostato con **SQLBindParameter**, non è un puntatore null. il tipo di dati C è stato SQL_C_BINARY o SQL_C_CHAR; e il valore della lunghezza del parametro era minore di 0 ma non era SQL_NTS, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM o minore o uguale a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Un valore di lunghezza di parametro associato da **SQLBindParameter** è stato impostato su SQL_DATA_AT_EXEC; il tipo SQL è SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo di dati specifico dell'origine dati long. e il tipo di informazioni SQL_NEED_LONG_DATA_LEN in **SQLGetInfo** era "Y".|  
|HY105|Tipo di parametro non valido|Il valore specificato per l'argomento *InputOutputType* in **SQLBindParameter** è stato SQL_PARAM_OUTPUT e il parametro è un parametro di input.|  
|I109|Posizione del cursore non valida|\**StatementText* contiene un'istruzione di aggiornamento o eliminazione posizionata e il cursore è stato posizionato (da **SQLSetPos** o **SQLFetchScroll**) su una riga che era stata eliminata o non poteva essere recuperata.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|La combinazione delle impostazioni correnti degli attributi di istruzione SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE non è supportata dal driver o dall'origine dati.<br /><br /> L'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_VARIABLE e l'attributo dell'istruzione SQL_ATTR_CURSOR_TYPE è stato impostato su un tipo di cursore per il quale il driver non supporta i segnalibri.|  
|HYT00|Timeout|Il periodo di timeout della query è scaduto prima che l'origine dati restituisca il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 L'applicazione chiama **SQLExecDirect** per inviare un'istruzione SQL all'origine dati. Per ulteriori informazioni sull'esecuzione diretta, vedere [esecuzione diretta](../../../odbc/reference/develop-app/direct-execution-odbc.md). Il driver modifica l'istruzione per utilizzare il modulo di SQL utilizzato dall'origine dati e quindi lo invia all'origine dati. In particolare, il driver modifica le sequenze di escape utilizzate per definire determinate funzionalità in SQL. Per la sintassi delle sequenze di escape, vedere Sequenze di [escape in ODBC.](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)  
  
 L'applicazione può includere uno o più indicatori di parametro nell'istruzione SQL. Per includere un marcatore di parametro, l'applicazione incorpora un punto interrogativo (?) nell'istruzione SQL nella posizione appropriata. Per informazioni sui parametri, vedere [Parametri dell'istruzione](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Se l'istruzione SQL è un'istruzione **SELECT** e se l'applicazione ha chiamato **SQLSetCursorName** per associare un cursore a un'istruzione, il driver utilizza il cursore specificato. In caso contrario, il driver genera un nome di cursore.  
  
 Se l'origine dati è in modalità di commit manuale (che richiede l'avvio esplicito della transazione) e non è già stata avviata una transazione, il driver avvia una transazione prima di inviare l'istruzione SQL. Per ulteriori informazioni, vedere [Modalità di commit manuale](../../../odbc/reference/develop-app/manual-commit-mode.md).  
  
 Se un'applicazione utilizza **SQLExecDirect** per inviare un'istruzione **COMMIT** o **ROLLBACK,** non sarà interoperabile tra i prodotti DBMS. Per eseguire il commit o il rollback di una transazione, un'applicazione chiama **SQLEndTran**.  
  
 Se **SQLExecDirect** rileva un parametro data-at-execution, restituisce SQL_NEED_DATA. L'applicazione invia i dati utilizzando **SQLParamData** e **SQLPutData**. Vedere [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)e [Invio di dati lunghi](../../../odbc/reference/develop-app/sending-long-data.md).  
  
 Se **SQLExecDirect** esegue un'istruzione di aggiornamento, inserimento o eliminazione ricercata che non influisce sulle righe dell'origine dati, la chiamata a **SQLExecDirect** restituisce SQL_NO_DATA.  
  
 Se il valore dell'attributo dell'istruzione SQL_ATTR_PARAMSET_SIZE è maggiore di 1 e l'istruzione SQL contiene almeno un indicatore di parametro, **SQLExecDirect** eseguirà l'istruzione SQL una volta per ogni set di valori di parametro dalle matrici a cui fa riferimento l'argomento *ParameterValuePointer* nella chiamata a **SQLBindParameter**. Per ulteriori informazioni, vedere [Matrici di valori di parametro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Se i segnalibri sono attivati e viene eseguita una query che non supporta i segnalibri, il driver deve tentare di costringere l'ambiente a uno che supporta i segnalibri modificando un valore di attributo e restituendo SQLSTATE 01S02 (valore di opzione modificato). Se l'attributo non può essere modificato, il driver deve restituire SQLSTATE HY024 (valore dell'attributo non valido).  
  
> [!NOTE]  
>  Quando si utilizza il pool di connessioni, un'applicazione non deve eseguire istruzioni SQL che modificano il database o il contesto del database, ad esempio l'istruzione **USE** del _database_ in SQL ServerSQL Server, che modifica il catalogo utilizzato da un'origine dati.  
  
## <a name="code-example"></a>Esempio di codice  
 Vedere [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)ed [Esempio di programma ODBC](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Esecuzione di un'operazione di commit o rollbackExecuting a commit or rollback operation|[SQLEndTran Function](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Recupero di più righe di dati|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Recupero di un blocco di dati o scorrimento di un set di risultati|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Restituzione del nome di un cursore|[Funzione SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Recupero di parte o di tutta una colonna di dati|[Funzione SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Restituzione del parametro successivo per l'invio dei dati per|[Funzione SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Preparazione di un'istruzione per l'esecuzione|[Pagina relativa alla funzione SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Invio dei dati dei parametri in fase di esecuzioneSending parameter data at execution time|[Funzione SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Impostazione del nome di un cursore|[Funzione SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|Impostazione di un attributo di istruzioneSetting a statement attribute|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
