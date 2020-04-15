---
title: Funzione SQLGetTypeInfo . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTypeInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTypeInfo
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC]
ms.assetid: bdedb044-8924-4ca4-85f3-8b37578e0257
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47273c75a005f11b33e9929977b57607b36898de
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303262"
---
# <a name="sqlgettypeinfo-function"></a>Funzione SQLGetTypeInfo
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLGetTypeInfo** restituisce informazioni sui tipi di dati supportati dall'origine dati. Il driver restituisce le informazioni sotto forma di un set di risultati SQL. I tipi di dati sono destinati all'utilizzo nelle istruzioni DDL (Data Definition Language).  
  
> [!IMPORTANT]  
>  Le applicazioni devono utilizzare i nomi dei tipi restituiti nella colonna TYPE_NAME del set di risultati **SQLGetTypeInfo** nelle istruzioni **ALTER TABLE** e **CREATE TABLE.** **SQLGetTypeInfo** può restituire più di una riga con lo stesso valore nella colonna DATA_TYPE.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione per il set di risultati.  
  
 *DataType*  
 [Ingresso] Tipo di dati SQL. Deve essere uno dei valori nella sezione Tipi di [dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) dell'Appendice D: Tipi di dati o un tipo di dati SQL specifico del driver. SQL_ALL_TYPES specifica che devono essere restituite informazioni su tutti i tipi di dati.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetTypeInfo** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetTypeInfo** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S02 (in questo stato di|Valore dell'opzione modificato|Un attributo di istruzione specificato non è valido a causa delle condizioni di lavoro di implementazione, pertanto un valore simile è stato temporaneamente sostituito. Chiamare **SQLGetStmtAttr** per determinare il valore sostituito temporaneamente. Il valore sostitutivo è valido per *il StatementHandle* fino a quando il cursore viene chiuso. Gli attributi di istruzione che possono essere modificati sono: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT e SQL_ATTR_SIMULATE_CURSOR. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|24000|Stato del cursore non valido|Un cursore era aperto su *StatementHandle* e **SQLFetch** o **SQLFetchScroll** era stato chiamato. Questo errore viene restituito da Gestione Driver se **SQLFetch** o **SQLFetchScroll** non ha restituito SQL_NO_DATA e viene restituito dal driver se **SQLFetch** o **SQLFetchScroll** ha restituito SQL_NO_DATA.<br /><br /> Un set di risultati era aperto in *StatementHandle*, ma **SQLFetch** o **SQLFetchScroll** non era stato chiamato.|  
|40001|Errore di serializzazione|È stato eseguito il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY004|Tipo di dati SQL non valido|Il valore specificato per l'argomento *DataType* non è né un identificatore del tipo di dati SQL ODBC valido né un identificatore del tipo di dati specifico del driver supportato dal driver.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*, quindi è stata chiamata la funzione e, prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*. Quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e, prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLGetTypeInfo.This** asynchronous function was still executing when the SQLGetTypeInfo function was called.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|La combinazione delle impostazioni correnti degli attributi di istruzione SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE non è supportata dal driver o dall'origine dati.<br /><br /> L'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_VARIABLE e l'attributo dell'istruzione SQL_ATTR_CURSOR_TYPE è stato impostato su un tipo di cursore per il quale il driver non supporta i segnalibri.|  
|HYT00|Timeout|Il periodo di timeout della query è scaduto prima che l'origine dati restituisca il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver corrispondente a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **SQLGetTypeInfo** restituisce i risultati come set di risultati standard, ordinati in base DATA_TYPE e quindi in base al livello di mapping del tipo di dati al tipo di dati SQL ODBC corrispondente. I tipi di dati definiti dall'origine dati hanno la precedenza sui tipi di dati definiti dall'utente. Di conseguenza, l'ordinamento non è necessariamente coerente, ma può essere generalizzato come DATA_TYPE prima, seguito da TYPE_NAME, entrambi ascendenti. Si supponga, ad esempio, che un'origine dati definisca tipi di dati INTEGER e COUNTER, dove COUNTER viene incrementato automaticamente e che sia stato definito anche un tipo di dati DEFINITO dall'utente WHOLENUM. Questi verrebbero restituiti nell'ordine INTEGER, WHOLENUM e COUNTER, perché WHOLENUM esegue il mapping strettamente al tipo di dati SQL ODBC SQL_INTEGER, mentre il tipo di dati a incremento automatico, anche se supportato dall'origine dati, non viene mappato strettamente a un tipo di dati SQL ODBC. Per informazioni sull'utilizzo di queste informazioni, vedere [Istruzioni DDL](../../../odbc/reference/develop-app/ddl-statements.md).  
  
 Se l'argomento *DataType* specifica un tipo di dati valido per la versione di ODBC supportata dal driver, ma non è supportato dal driver, verrà restituito un set di risultati vuoto.  
  
> [!NOTE]  
>  Per ulteriori informazioni sull'utilizzo generale, gli argomenti e i dati restituiti delle funzioni di catalogo ODBC, vedere Funzioni di [catalogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Le colonne seguenti sono state rinominate per ODBC 3. *x*. Le modifiche del nome della colonna non influiscono sulla compatibilità con le versioni precedenti perché le applicazioni vengono associate in base al numero di colonna.  
  
|Colonna ODBC 2.0|ODBC 3. *x* colonna|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 Le colonne seguenti sono state aggiunte al set di risultati restituito da **SQLGetTypeInfo** per ODBC 3. *x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 Nella tabella seguente sono elencate le colonne del set di risultati. Colonne aggiuntive oltre la colonna 19 (INTERVAL_PRECISION) possono essere definite dal driver. Un'applicazione deve ottenere l'accesso alle colonne specifiche del driver eseguendo il conto alla rovescia dalla fine del set di risultati anziché specificare una posizione ordinale esplicita. Per ulteriori informazioni, vedere [Dati restituiti da Funzioni di catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** potrebbe non restituire tutti i tipi di dati. Ad esempio, un driver potrebbe non restituire tipi di dati definiti dall'utente. Le applicazioni possono utilizzare qualsiasi tipo di dati valido, indipendentemente dal fatto che venga restituito da **SQLGetTypeInfo**. I tipi di dati restituiti da **SQLGetTypeInfo** sono quelli supportati dall'origine dati. Sono destinati all'uso nelle istruzioni DDL (Data Definition Language). I driver possono restituire dati del set di risultati utilizzando tipi di dati diversi dai tipi restituiti da **SQLGetTypeInfo**. Durante la creazione del set di risultati per una funzione di catalogo, il driver potrebbe utilizzare un tipo di dati non supportato dall'origine dati.  
  
|Nome colonna|Colonna<br /><br /> d'acquisto|Tipo di dati|Commenti|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|Varchar non NULL|Nome del tipo di dati dipendente dall'origine dati; ad esempio, "CHAR()", "VARCHAR()", "MONEY", "LONG VARBINARY" o "CHAR ( ) PER BIT DATA". Le applicazioni devono utilizzare questo nome nelle istruzioni **CREATE TABLE** e **ALTER TABLE.**|  
|DATA_TYPE (ODBC 2.0)|2|Smallint non NULL|Tipo di dati SQL. Può trattarsi di un tipo di dati SQL ODBC o di un tipo di dati SQL specifico del driver. Per i tipi di dati datetime o interval, questa colonna restituisce il tipo di dati conciso (ad esempio SQL_TYPE_TIME o SQL_INTERVAL_YEAR_TO_MONTH). Per un elenco dei tipi di dati SQL ODBC validi, vedere [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) nell'Appendice D: tipi di dati. Per informazioni sui tipi di dati SQL specifici del driver, vedere la documentazione del driver.|  
|COLUMN_SIZE (ODBC 2.0)|3|Integer|Dimensione massima della colonna supportata dal server per questo tipo di dati. Per i dati numerici, si tratta della precisione massima. Per i dati stringa, questa è la lunghezza in caratteri. Per i tipi di dati datetime, questa è la lunghezza in caratteri della rappresentazione di stringa (presupponendo la precisione massima consentita del componente secondi frazionari). Viene restituito NULL per i tipi di dati in cui la dimensione della colonna non è applicabile. Per i tipi di dati intervallo, questo è il numero di caratteri nella rappresentazione di caratteri del valore letterale di intervallo (come definito dalla precisione iniziale dell'intervallo; vedere [Interval Data Type Length](../../../odbc/reference/appendixes/interval-data-type-length.md) in Appendix D: Tipi di dati).<br /><br /> Per ulteriori informazioni sulle dimensioni delle colonne, vedere [Dimensioni colonna, Cifre decimali, Trasferimento ottetto lunghezza e Dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice D: tipi di dati.|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|Carattere o caratteri utilizzati per anteporre un valore letterale; ad esempio, una virgoletta singola (') per i tipi di dati carattere o 0x per i tipi di dati binari; Viene restituito NULL per i tipi di dati in cui non è applicabile un prefisso letterale.|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|Carattere o caratteri utilizzati per terminare un valore letterale; ad esempio, una virgoletta singola (') per i tipi di dati carattere; Viene restituito NULL per i tipi di dati in cui non è applicabile un suffisso letterale.|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|Elenco di parole chiave, separate da virgole, corrispondenti a ogni parametro che l'applicazione può specificare tra parentesi quando si utilizza il nome restituito nel campo TYPE_NAME. Le parole chiave nell'elenco possono essere una delle seguenti: lunghezza, precisione o scala. Vengono visualizzati nell'ordine in cui la sintassi richiede l'utilizzo. Ad esempio, CREATE_PARAMS per DECIMAL sarebbe "precision,scale"; CREATE_PARAMS per VARCHAR sarebbe uguale a "lunghezza". Null viene restituito se non sono presenti parametri per la definizione del tipo di dati; ad esempio INTEGER.<br /><br /> Il driver fornisce il testo CREATE_PARAMS nella lingua del paese in cui viene utilizzato.|  
|NULLABLE (ODBC 2.0)|7|Smallint non NULL|Se il tipo di dati accetta un valore NULL:<br /><br /> SQL_NO_NULLS se il tipo di dati non accetta valori NULL.<br /><br /> SQL_NULLABLE se il tipo di dati accetta valori NULL.<br /><br /> SQL_NULLABLE_UNKNOWN se non è noto se la colonna accetta valori NULL.|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint non NULL|Se un tipo di dati carattere fa distinzione tra maiuscole e minuscole nelle regole di confronto e nei confronti:Whether a character data type is case-sensitive in collations and comparisons:<br /><br /> SQL_TRUE se il tipo di dati è un tipo di dati carattere e fa distinzione tra maiuscole e minuscole.<br /><br /> SQL_FALSE se il tipo di dati non è un tipo di dati carattere o non fa distinzione tra maiuscole e minuscole.|  
|RICERCABILE (ODBC 2.0)|9|Smallint non NULL|Modalità di utilizzo del tipo di dati in una clausola **WHERE:**<br /><br /> SQL_PRED_NONE se la colonna non può essere utilizzata in una clausola **WHERE.** (Questo è lo stesso valore SQL_UNSEARCHABLE in ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR se la colonna può essere utilizzata in una clausola **WHERE,** ma solo con il predicato **LIKE.** (Questo è lo stesso valore SQL_LIKE_ONLY in ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC se la colonna può essere utilizzata in una clausola **WHERE** con tutti gli operatori di confronto ad eccezione di **LIKE** (confronto, confronto quantificato, **BETWEEN**, **DISTINCT**, **IN**, **MATCH**e **UNIQUE**). (Questo è lo stesso valore SQL_ALL_EXCEPT_LIKE in ODBC 2. *x*.)<br /><br /> SQL_SEARCHABLE se la colonna può essere utilizzata in una clausola **WHERE** con qualsiasi operatore di confronto.|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|Se il tipo di dati è unsigned:<br /><br /> SQL_TRUE se il tipo di dati è senza segno.<br /><br /> SQL_FALSE se il tipo di dati è firmato.<br /><br /> Se l'attributo non è applicabile al tipo di dati o se il tipo di dati non è numerico, viene restituito NULL.|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint non NULL|Se il tipo di dati dispone di precisione e scala fissa predefinite (specifiche dell'origine dati), ad esempio un tipo di dati money:<br /><br /> SQL_TRUE se dispone di precisione e scala fisse predefinite.<br /><br /> SQL_FALSE se non dispone di precisione e scala fisse predefinite.|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|Se il tipo di dati è a incremento automatico:<br /><br /> SQL_TRUE se il tipo di dati viene incrementato automaticamente.<br /><br /> SQL_FALSE se il tipo di dati non viene incrementato automaticamente.<br /><br /> Se l'attributo non è applicabile al tipo di dati o se il tipo di dati non è numerico, viene restituito NULL.<br /><br /> Un'applicazione può inserire valori in una colonna con questo attributo, ma in genere non può aggiornare i valori nella colonna.<br /><br /> Quando un inserimento viene trasformato in una colonna a incremento automatico, un valore univoco viene inserito nella colonna al momento dell'inserimento. L'incremento non è definito, ma è specifico dell'origine dati. Un'applicazione non deve presupporre che una colonna a incremento automatico inizi in corrispondenza di un determinato punto o aumenti di un valore specifico.|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|Versione localizzata del nome del tipo di dati dipendente dall'origine dati. Se il nome localizzato non è supportato dall'origine dati, viene restituito NULL. Questo nome è destinato solo alla visualizzazione, ad esempio nelle finestre di dialogo.|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|Scala minima del tipo di dati nell'origine dati. Se a un tipo di dati è associata una scala fissa, le colonne MINIMUM_SCALE e MAXIMUM_SCALE contengono entrambe lo stesso valore. Ad esempio, una colonna SQL_TYPE_TIMESTAMP potrebbe avere una scala fissa per i secondi frazionari. Se la scala non è applicabile, viene restituito NULL. Per ulteriori informazioni, vedere [Dimensione colonna, Cifre decimali, Lunghezza ottetto di trasferimento e Dimensioni](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) di visualizzazione nell'Appendice D: Tipi di dati.|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|Scala massima del tipo di dati nell'origine dati. Se la scala non è applicabile, viene restituito NULL. Se la scala massima non viene definita separatamente nell'origine dati, ma viene invece definita come precisione massima, questa colonna contiene lo stesso valore della colonna COLUMN_SIZE. Per ulteriori informazioni, vedere [Dimensione colonna, Cifre decimali, Lunghezza ottetto di trasferimento e Dimensioni](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) di visualizzazione nell'Appendice D: Tipi di dati.|  
|SQL_DATA_TYPE (ODBC 3.0)|16|Smallint NON NULL|Valore del tipo di dati SQL visualizzato nel campo SQL_DESC_TYPE del descrittore. Questa colonna è uguale alla colonna DATA_TYPE, ad eccezione dei tipi di dati interval e datetime.<br /><br /> Per i tipi di dati interval e datetime, il campo SQL_DATA_TYPE nel set di risultati restituirà SQL_INTERVAL o SQL_DATETIME e il campo SQL_DATETIME_SUB restituirà il sottocodice per il tipo di dati interval o datetime specifico. (Vedere [l'Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|Quando il valore di SQL_DATA_TYPE è SQL_DATETIME o SQL_INTERVAL, questa colonna contiene il sottocodice datetime/interval. Per i tipi di dati diversi da datetime e interval, questo campo è NULL.<br /><br /> Per i tipi di dati interval o datetime, il campo SQL_DATA_TYPE nel set di risultati restituirà SQL_INTERVAL o SQL_DATETIME e il campo SQL_DATETIME_SUB restituirà il sottocodice per il tipo di dati interval o datetime specifico. (Vedere [l'Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Integer|Se il tipo di dati è un tipo numerico approssimativo, questa colonna contiene il valore 2 per indicare che COLUMN_SIZE specifica un numero di bit. Per i tipi numerici esatti, questa colonna contiene il valore 10 per indicare che COLUMN_SIZE specifica un numero di cifre decimali. Negli altri casi la colonna è NULL.|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|Se il tipo di dati è un tipo di dati intervallo, questa colonna contiene il valore della precisione di interlinea dell'intervallo. Vedere [Precisione del tipo di dati intervallo](../../../odbc/reference/appendixes/interval-data-type-precision.md) nell'Appendice D: Tipi di dati. In caso contrario, questa colonna è NULL.|  
  
 Le informazioni sugli attributi possono essere applicate ai tipi di dati o a colonne specifiche in un set di risultati. **SQLGetTypeInfo** restituisce informazioni sugli attributi associati ai tipi di dati. **SQLColAttribute** restituisce informazioni sugli attributi associati alle colonne in un set di risultati.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di informazioni su una colonna in un set di risultatiReturning information about a column in a result set|[Funzione SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Recupero di un blocco di dati o scorrimento di un set di risultati|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Recupero di una singola riga o di un blocco di dati in una direzione forward-only|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Restituzione di informazioni su un driver o un'origine datiReturning information about a driver or data source|[Funzione SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
