---
title: Funzione SQLGetTypeInfo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f83b8ce83c1433ce7e20f00580100b65be84961
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63132674"
---
# <a name="sqlgettypeinfo-function"></a>Funzione SQLGetTypeInfo
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLGetTypeInfo** restituisce informazioni sui tipi di dati supportati dall'origine dati. Il driver restituisce le informazioni sotto forma di un set di risultati SQL. I tipi di dati devono essere utilizzati nelle istruzioni Data Definition Language (DDL).  
  
> [!IMPORTANT]  
>  Le applicazioni devono utilizzare i nomi dei tipi restituiti nella colonna TYPE_NAME del **SQLGetTypeInfo** del set di risultati **ALTER TABLE** e **CREATE TABLE** istruzioni. **SQLGetTypeInfo** può restituire più righe con lo stesso valore nella colonna DATA_TYPE.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione per il set di risultati.  
  
 *DataType*  
 [Input] Il tipo di dati SQL. Deve essere uno dei valori di [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) sezione dell'appendice d: Tipi di dati o un tipo di dati specifici del driver SQL. SQL_ALL_TYPES specifica che devono essere restituite informazioni su tutti i tipi di dati.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetTypeInfo** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetTypeInfo** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01S02|Valore di opzione modificato|Un attributo di istruzione specificato non è valido a causa di condizioni di lavoro di implementazione, pertanto è stata temporaneamente sostituito con un valore simile. (Chiamare **SQLGetStmtAttr** per determinare il valore di sostituzione temporaneamente.) Il valore di sostituzione è valido per il *StatementHandle* fino a quando il cursore è chiuso. Gli attributi di istruzione che è possibile modificare sono: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT, and SQL_ATTR_SIMULATE_CURSOR. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|24000|Stato del cursore non valido|Il cursore è stato aperto scegliere il *StatementHandle,* e **SQLFetch** oppure **SQLFetchScroll** fosse stata chiamata. Questo errore viene restituito da Gestione Driver, se **SQLFetch** oppure **SQLFetchScroll** non restituisce SQL_NO_DATA e viene restituito dal driver se **SQLFetch** oppure **SQLFetchScroll** è stato restituito SQL_NO_DATA.<br /><br /> Un set di risultati è stata aperto nel *StatementHandle*, ma **SQLFetch** oppure **SQLFetchScroll** non fosse stata chiamata.|  
|40001|Errore di serializzazione.|Il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY004|Tipo di dati SQL non valido|Il valore specificato per l'argomento *DataType* era un identificatore di tipo di dati SQL ODBC valido né un identificatore di tipo di dati specifici del driver supportata dal driver.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*, quindi è stata chiamata la funzione e, in precedenza, esecuzione completata **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle*. Quindi la funzione è stata chiamata nuovamente sul *StatementHandle*.<br /><br /> È stata chiamata la funzione e, prima completata l'esecuzione, **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLGetTypeInfo** funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|La combinazione delle impostazioni correnti degli attributi di istruzione SQL_ATTR_CURSOR_TYPE e SQL_ATTR_CONCURRENCY non era supportata dall'origine dati o driver.<br /><br /> L'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_VARIABLE e l'attributo SQL_ATTR_CURSOR_TYPE di istruzione è stata impostata su un tipo di cursore per i quali il driver non supporta i segnalibri.|  
|HYT00|Timeout|Il periodo di timeout query scaduto prima che l'origine dati ha restituito il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|(DM) il driver corrispondente per il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **SQLGetTypeInfo** restituisce i risultati come un set di risultati standard, ordinato in base a DATA_TYPE e quindi dalla precisione del tipo di dati esegue il mapping al tipo di dati SQL ODBC corrispondente. Tipi di dati definiti dall'origine dati hanno la precedenza su tipi di dati definito dall'utente. Di conseguenza, l'ordinamento non è necessariamente coerenza, ma può essere generalizzato prima di tutto come DATA_TYPE, seguito da TYPE_NAME, entrambi crescente. Ad esempio, si supponga di che tipi di dati INTEGER e contatore, dove contatore è a incremento automatico, è definita da un'origine dati e che un tipo di dati definito dall'utente WHOLENUM anche è stato definito. Queste verrebbe restituito nell'ordine di numero intero, WHOLENUM e contatore, perché esegue il mapping da vicino ai dati SQL ODBC WHOLENUM tipo SQL_INTEGER, mentre il tipo di dati con incremento automatico, anche se supportato dall'origine dati, non esegue il mapping da vicino a un tipo di dati SQL ODBC. Per informazioni su come è possibile usare queste informazioni, vedere [istruzioni DDL](../../../odbc/reference/develop-app/ddl-statements.md).  
  
 Se il *DataType* argomento specifica un tipo di dati valido per la versione di ODBC supportati dal driver, ma non è supportato dal driver, quindi verrà restituito un set di risultati vuoto.  
  
> [!NOTE]  
>  Per altre informazioni su uso generale, gli argomenti e i dati restituiti di funzioni di catalogo ODBC, vedere [funzioni di catalogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Le colonne seguenti sono state rinominate per ODBC 3. *x*. Le modifiche ai nomi di colonna non influenzano la compatibilità con le versioni precedenti poiché nelle applicazioni associati dal numero di colonna.  
  
|Colonna ODBC 2.0|ODBC 3. *x* colonna|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 Le colonne seguenti sono stati aggiunti al set di risultati restituito da **SQLGetTypeInfo** per ODBC 3. *x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 Nella tabella seguente elenca le colonne nel set di risultati. Le colonne aggiuntive oltre a 19 (INTERVAL_PRECISION) colonna possono essere definite dal driver. Un'applicazione deve accedere a colonne specifiche del driver procede a ritroso dalla fine del set di risultati anziché specificare una posizione ordinale esplicita. Per altre informazioni, vedere [i dati restituiti dalle funzioni catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** potrebbe non restituire tutti i tipi di dati. Ad esempio, un driver potrebbe non restituire i tipi di dati definito dall'utente. Le applicazioni possono usare qualsiasi tipo di dati valido, indipendentemente dal fatto che viene restituita da **SQLGetTypeInfo**. I tipi di dati restituiti da **SQLGetTypeInfo** sono quelli supportati dall'origine dati. Essi devono essere utilizzati nelle istruzioni Data Definition Language (DDL). I driver possono restituire dati di set di risultati usando tipi di dati diversi dai tipi restituiti dal **SQLGetTypeInfo**. Nella creazione di set di risultati di una funzione di catalogo, il driver potrebbe usare un tipo di dati che non è supportato dall'origine dati.  
  
|Nome colonna|colonna<br /><br /> number|Tipo di dati|Commenti|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|Non NULL varchar|Nome del tipo di dati dipende dall'origine dati; ad esempio, "ASCII", "Varchar ()", "MONEY", "LONG VARBINARY" o "() CHAR FOR BIT DATA". Le applicazioni devono usare il nome specificato nel **CREATE TABLE** e **ALTER TABLE** istruzioni.|  
|DATA_TYPE (ODBC 2.0)|2|Smallint non NULL|Tipo di dati SQL. Può trattarsi di un tipo di dati SQL ODBC o un tipo di dati specifici del driver SQL. Per i tipi di dati datetime o intervallo, questa colonna restituisce il tipo di dati concisa (ad esempio SQL_TYPE_TIME o SQL_INTERVAL_YEAR_TO_MONTH). Per un elenco di tipi di dati SQL ODBC validi, vedere [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) nell'appendice d: Tipi di dati. Per informazioni sui tipi di dati specifici del driver SQL, vedere la documentazione del driver.|  
|COLUMN_SIZE (ODBC 2.0)|3|Valore intero|La dimensione massima della colonna per questo tipo di dati supportati dal server. Per i dati numerici, questa è la precisione massima. Per i dati stringa, questa è la lunghezza in caratteri. Per i tipi di dati Data/ora, si tratta della lunghezza in caratteri della rappresentazione di stringa (presupponendo la precisione massima consentita del componente di secondi frazionari). Viene restituito NULL per i tipi di dati in cui le dimensioni di colonna non sono applicabile. Per i tipi di dati di intervallo, questo è il numero di caratteri nella rappresentazione di carattere dell'intervallo di valori letterale (come definito in base all'intervallo iniziali precisione; vedere [lunghezza del tipo di dati intervallo](../../../odbc/reference/appendixes/interval-data-type-length.md) nell'appendice d: Tipi di dati).<br /><br /> Per altre informazioni sulle dimensioni di colonna, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice d: Tipi di dati.|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|Carattere o caratteri utilizzati come prefisso un valore letterale; ad esempio, una virgoletta singola (') per i tipi di dati carattere o 0x per tipi di dati binari. Viene restituito NULL per i tipi di dati in cui un prefisso letterale non è applicabile.|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|Carattere o caratteri utilizzati per terminare un valore letterale; ad esempio, una virgoletta singola (') per tipi di dati carattere. Viene restituito NULL per i tipi di dati in cui un suffisso letterale non è applicabile.|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|Elenco di parole chiave, separati da virgole, corrispondente a ogni parametro a cui l'applicazione può essere specificato in parentesi quando si usa il nome che viene restituito nel campo TYPE_NAME. Le parole chiave nell'elenco possono essere uno dei seguenti: lunghezza, precisione o scala. Vengono visualizzati nell'ordine che la sintassi richiede che vengano utilizzati. Ad esempio, sarebbe CREATE_PARAMS come separatore decimale "precision, scale"; CREATE_PARAMS per VARCHAR equivale al "length". Viene restituito NULL se non sono presenti parametri per la definizione di tipo di dati. ad esempio, numero intero.<br /><br /> Il driver fornisce il testo CREATE_PARAMS nella lingua del paese/area geografica in cui viene usato.|  
|NULLABLE (ODBC 2.0)|7|Smallint non NULL|Indica se il tipo di dati accetta un valore NULL:<br /><br /> SQL_NO_NULLS se il tipo di dati non accetta valori NULL.<br /><br /> SQL_NULLABLE se il tipo di dati ammette valori NULL.<br /><br /> SQL_NULLABLE_UNKNOWN se non è noto se la colonna accetta valori NULL.|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint non NULL|Indica se un tipo di dati carattere è tra maiuscole e minuscole nelle regole di confronto e i confronti:<br /><br /> SQL_TRUE se il tipo di dati è un tipo di dati character e tra maiuscole e minuscole.<br /><br /> SQL_FALSE se il tipo di dati non è un tipo di dati carattere o non è tra maiuscole e minuscole.|  
|RICERCABILE (ODBC 2.0)|9|Smallint non NULL|Utilizzo del tipo di dati in un **in cui** clausola:<br /><br /> SQL_PRED_NONE se la colonna non può essere utilizzata in una **in cui** clausola. (Questo è lo stesso come il valore SQL_UNSEARCHABLE in ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR se la colonna può essere utilizzata una **in cui** clausola, ma solo con i **, ad esempio** predicato. (Questo è lo stesso come il valore SQL_LIKE_ONLY in ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC se la colonna può essere utilizzata una **in cui** clausola con tutti gli operatori di confronto tranne **, ad esempio** (confronto, confronto quantificato, **BETWEEN**,  **DISTINCT**, **India**, **MATCH**, e **UNIQUE**). (Questo è lo stesso come il valore SQL_ALL_EXCEPT_LIKE in ODBC 2. *x*.)<br /><br /> SQL_SEARCHABLE se la colonna può essere utilizzata una **in cui** clausola con qualsiasi operatore di confronto.|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|Indica se il tipo di dati è senza segno:<br /><br /> SQL_TRUE se il tipo di dati è senza segno.<br /><br /> SQL_FALSE se il tipo di dati viene eseguito l'accesso.<br /><br /> Se l'attributo non è applicabile al tipo di dati o il tipo di dati non è numerico, viene restituito NULL.|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint non NULL|Indica se il tipo di dati è disponibili predefinite precisione e scala (che sono specifiche dell'origine dati), ad esempio un tipo di dati money fisse:<br /><br /> Precisione e scala fisse SQL_TRUE se ha già definiti.<br /><br /> Precisione e scala fisse SQL_FALSE se non sono predefiniti.|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|Indica se il tipo di dati è incrementata automaticamente:<br /><br /> SQL_TRUE se il tipo di dati viene incrementato automaticamente.<br /><br /> SQL_FALSE se il tipo di dati non è incrementata automaticamente.<br /><br /> Se l'attributo non è applicabile al tipo di dati o il tipo di dati non è numerico, viene restituito NULL.<br /><br /> Un'applicazione può inserire valori in una colonna con questo attributo, ma in genere non è possibile aggiornare i valori nella colonna.<br /><br /> Quando viene effettuata un'operazione di inserimento in una colonna a incremento automatico, viene inserito un valore univoco nella colonna al momento dell'inserimento. L'incremento non è definito, ma è specifiche dell'origine dati. Un'applicazione non deve presupporre che una colonna a incremento automatico inizia in corrispondenza di qualsiasi particolare punto o incrementi da un particolare valore.|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|Versione localizzata del nome del tipo di dati dipendente dall'origine dati. Se il nome localizzato non è supportato dall'origine dati, viene restituito NULL. Questo nome deve essere visualizzato solo, ad esempio le finestre di dialogo.|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|Scala minima del tipo di dati nell'origine dati. Se a un tipo di dati è associata una scala fissa, le colonne MINIMUM_SCALE e MAXIMUM_SCALE contengono entrambe lo stesso valore. Ad esempio, una colonna SQL_TYPE_TIMESTAMP potrebbe disporre di una scala fissa per i secondi frazionari. Se la scala non è applicabile, viene restituito NULL. Per altre informazioni, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice d: Tipi di dati.|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|Scala massima del tipo di dati nell'origine dati. Se la scala non è applicabile, viene restituito NULL. Se la scala massima non viene definita separatamente nell'origine dati, ma viene invece definita per coincidere con la precisione massima, questa colonna contiene lo stesso valore della colonna COLUMN_SIZE. Per altre informazioni, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice d: Tipi di dati.|  
|SQL_DATA_TYPE (ODBC 3.0)|16|smallint non NULL|Il valore del tipo di dati SQL perché viene visualizzato nel campo SQL_DESC_TYPE del descrittore. Questa colonna corrisponde alla colonna DATA_TYPE, tranne i tipi di dati datetime e interval.<br /><br /> Per i tipi di dati datetime e interval, il campo SQL_DATA_TYPE nel set di risultati restituirà SQL_DATETIME o SQL_INTERVAL, e il campo SQL_DATETIME_SUB restituirà il codice secondario per il tipo di dati datetime o intervallo specifico. (Vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|Quando il valore di SQL_DATA_TYPE è SQL_DATETIME o SQL_INTERVAL, questa colonna contiene il codice secondario/intervallo datetime. Per i tipi di dati diverse da data/ora e intervallo, questo campo è NULL.<br /><br /> Per i tipi di dati datetime o intervallo, il campo SQL_DATA_TYPE nel set di risultati restituirà SQL_DATETIME o SQL_INTERVAL, e il campo SQL_DATETIME_SUB restituirà il codice secondario per il tipo di dati datetime o intervallo specifico. (Vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Valore intero|Se il tipo di dati è un tipo numerico approssimato, questa colonna contiene il valore 2 per indicare che COLUMN_SIZE specifica un numero di bit. Per i tipi numerici esatti, questa colonna contiene il valore 10 per indicare che COLUMN_SIZE specifica un numero di cifre decimali. Negli altri casi la colonna è NULL.|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|Se il tipo di dati è un tipo di dati di intervallo, questa colonna contiene il valore della precisione iniziale intervallo. (Vedere [precisione del tipo di dati di intervallo](../../../odbc/reference/appendixes/interval-data-type-precision.md) nell'appendice d: Tipi di dati.) Negli altri casi la colonna è NULL.|  
  
 Informazioni sugli attributi è possibile applicare ai tipi di dati o per colonne specifiche in un set di risultati. **SQLGetTypeInfo** restituisce informazioni sugli attributi associati ai tipi di dati; **SQLColAttribute** restituisce informazioni sugli attributi associati alle colonne in un set di risultati.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultati|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di informazioni relative a una colonna in un set di risultati|[Funzione SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Imposta il recupero di un blocco di dati o lo scorrimento di un risultato|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Il recupero di una singola riga o un blocco di dati in una direzione di tipo forward-only|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Restituzione di informazioni su un'origine dati o driver|[Funzione SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
