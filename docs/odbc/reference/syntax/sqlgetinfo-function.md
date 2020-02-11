---
title: Funzione SQLGetInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInfo
helpviewer_keywords:
- SQLGetInfo function [ODBC]
ms.assetid: 49dceccc-d816-4ada-808c-4c6138dccb64
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0e62e7aaba276643a2874a22e74a08214cfe51e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68030666"
---
# <a name="sqlgetinfo-function"></a>Funzione SQLGetInfo
**Conformità**  
 Versione introdotta: ODBC 1,0 Standard Compliance: ISO 92  
  
 **Summary**  
 **SQLGetInfo** restituisce informazioni generali sul driver e sull'origine dati associate a una connessione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLGetInfo(  
     SQLHDBC         ConnectionHandle,  
     SQLUSMALLINT    InfoType,  
     SQLPOINTER      InfoValuePtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *ConnectionHandle*  
 [Input] Handle di connessione.  
  
 *InfoType*  
 Input Tipo di informazioni.  
  
 *InfoValuePtr*  
 Output Puntatore a un buffer in cui restituire le informazioni. A seconda del *InfoType* richiesto, le informazioni restituite saranno una delle seguenti: una stringa di caratteri con terminazione null, un valore SQLUSMALLINT, una maschera di bit SQLUINTEGER, un flag SQLUINTEGER, un valore binario SQLUINTEGER o un valore SQLULEN.  
  
 Se l'argomento *InfoType* è SQL_DRIVER_HDESC o SQL_DRIVER_HSTMT, l'argomento *InfoValuePtr* è sia di input che di output. Per ulteriori informazioni, vedere la SQL_DRIVER_HDESC o i descrittori di SQL_DRIVER_HSTMT più avanti in questa descrizione della funzione.  
  
 Se *InfoValuePtr* è null, *StringLengthPtr* restituisce comunque il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibili per restituire nel buffer a cui punta *InfoValuePtr*.  
  
 *BufferLength*  
 Input Lunghezza del \*buffer *InfoValuePtr* . Se il valore in * \*InfoValuePtr* non è una stringa di caratteri o se *InfoValuePtr* è un puntatore null, l'argomento *bufferLength* viene ignorato. Il driver presuppone che la dimensione di * \*InfoValuePtr* sia SQLUSMALLINT o SQLUINTEGER, in base a *InfoType*. Se * \*InfoValuePtr* è una stringa Unicode (quando si chiama **SQLGetInfoW**), l'argomento *bufferLength* deve essere un numero pari. in caso contrario, viene restituito SQLSTATE HY090 (stringa non valida o lunghezza del buffer).  
  
 *StringLengthPtr*  
 Output Puntatore a un buffer in cui restituire il numero totale di byte, escluso il carattere di terminazione null per i dati di tipo carattere, disponibile per restituire in **InfoValuePtr*.  
  
 Per i dati di tipo carattere, se il numero di byte disponibili per restituire è maggiore o uguale a *bufferLength*, le \*informazioni in *InfoValuePtr* vengono troncate a *bufferLength* bytes meno la lunghezza di un carattere di terminazione null e con terminazione null dal driver.  
  
 Per tutti gli altri tipi di dati, il valore di *bufferLength* viene ignorato e il driver presuppone che le \*dimensioni di *InfoValuePtr* siano SQLUSMALLINT o SQLUINTEGER, a seconda del *InfoType*.  
  
## <a name="return-value"></a>Valore restituito  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetInfo** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con *HandleType* di SQL_HANDLE_DBC e un *handle* di *connectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE restituiti in genere da **SQLGetInfo** e ne viene illustrato ciascuno nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituite da Gestione driver. Il codice restituito associato a ogni valore SQLSTATE è SQL_ERROR, a meno che non sia specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (La funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa, troncati a destra|Il buffer \* *InfoValuePtr* non era sufficientemente grande per restituire tutte le informazioni richieste. Pertanto, le informazioni sono state troncate. La lunghezza delle informazioni richieste nel formato non troncato viene restituita in **StringLengthPtr*. (La funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08003|Connessione non aperta|(DM) il tipo di informazioni richieste in *InfoType* richiede una connessione aperta. Dei tipi di informazioni riservati da ODBC, solo SQL_ODBC_VER possono essere restituiti senza una connessione aperta.|  
|08S01|Errore collegamento comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima del completamento dell'elaborazione della funzione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non esiste un valore SQLSTATE specifico e per il quale non è stato definito alcun valore SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la sua origine.|  
|HY001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore sequenza funzione|(DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *statementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è possibile accedere agli oggetti memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY024|Valore di attributo non valido|(DM) l'argomento *InfoType* è stato SQL_DRIVER_HSTMT e il valore a cui punta *InfoValuePtr* non è un handle di istruzione valido.<br /><br /> (DM) l'argomento *InfoType* è stato SQL_DRIVER_HDESC e il valore a cui punta *InfoValuePtr* non è un handle di descrittore valido.|  
|HY090|Lunghezza della stringa o del buffer non valida|(DM) il valore specificato per l'argomento *bufferLength* è minore di 0.<br /><br /> (DM) il valore specificato per *bufferLength* è un numero dispari e * \*InfoValuePtr* è di un tipo di dati Unicode.|  
|HY096|Tipo di informazioni non compreso nell'intervallo|Il valore specificato per l'argomento *InfoType* non è valido per la versione di ODBC supportata dal driver.|  
|HY117|Connessione sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo le funzioni di disconnessione e di sola lettura.|(DM) per ulteriori informazioni sullo stato Suspended, vedere [funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Campo facoltativo non implementato|Il valore specificato per l'argomento *InfoType* è un valore specifico del driver che non è supportato dal driver.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati abbia risposto alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver che corrisponde a *connectionHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 I tipi di informazioni attualmente definiti sono visualizzati in "tipi di informazioni", più avanti in questa sezione. si prevede che venga definito un numero maggiore per sfruttare le diverse origini dati. Un intervallo di tipi di informazioni è riservato da ODBC. gli sviluppatori di driver devono riservare i valori per l'uso specifico del driver da un gruppo aperto. **SQLGetInfo** non esegue alcuna conversione o *thunk* Unicode (vedere [Appendice A: codici di errore ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) di *riferimento per programmatori ODBC*) per *InfoTypes*definito dal driver. Per ulteriori informazioni, vedere [tipi di dati specifici del driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md). Il formato delle informazioni restituite in \* *InfoValuePtr* dipende dalla *InfoType* richiesta. **SQLGetInfo** restituirà informazioni in uno dei cinque diversi formati:  
  
-   Una stringa di caratteri con terminazione null  
  
-   Valore SQLUSMALLINT  
  
-   Maschera di SQLUINTEGER  
  
-   Valore SQLUINTEGER  
  
-   Valore binario SQLUINTEGER  
  
 Il formato di ognuno dei seguenti tipi di informazioni è indicato nella descrizione del tipo. L'applicazione deve eseguire il cast del valore restituito in **InfoValuePtr* di conseguenza. Per un esempio di come un'applicazione può recuperare i dati da una maschera di maschera SQLUINTEGER, vedere "esempio di codice".  
  
 Un driver deve restituire un valore per ogni tipo di informazioni definito nelle tabelle seguenti. Se un tipo di informazioni non si applica al driver o all'origine dati, il driver restituisce uno dei valori elencati nella tabella seguente.  
  
 Stringa di caratteri ("Y" o "N")  
 "N"  
  
 Stringa di caratteri (non "Y" o "N")  
 Stringa vuota  
  
 SQLUSMALLINT  
 0  
  
 Maschera di SQLUINTEGER o valore binario SQLUINTEGER  
 0L  
  
 Se, ad esempio, un'origine dati non supporta le procedure, **SQLGetInfo** restituisce i valori elencati nella tabella seguente per i valori di *InfoType* correlati alle procedure.  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 Stringa vuota  
  
 **SQLGetInfo** restituisce SQLSTATE HY096 (valore di argomento non valido) per i valori di *InfoType* che si trovano nell'intervallo di tipi di informazioni riservati per l'utilizzo da parte di ODBC, ma che non sono definiti dalla versione di ODBC supportata dal driver. Per determinare la versione di ODBC a cui un driver è conforme, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_DRIVER_ODBC_VER. **SQLGetInfo** restituisce SQLSTATE HYC00 (funzionalità facoltativa non implementata) per i valori di *InfoType* che si trovano nell'intervallo di tipi di informazioni riservati per l'utilizzo specifico del driver, ma non sono supportati dal driver.  
  
 Tutte le chiamate a **SQLGetInfo** richiedono una connessione aperta, tranne quando *InfoType* è SQL_ODBC_VER, che restituisce la versione di gestione driver.  
  
## <a name="information-types"></a>Tipi di informazioni  
 In questa sezione sono elencati i tipi di informazioni supportati da **SQLGetInfo**. I tipi di informazioni vengono raggruppati categoricamente ed elencati in ordine alfabetico. Sono elencati anche i tipi di informazioni aggiunti o rinominati per ODBC 3 *. x* .  
  
## <a name="driver-information"></a>Informazioni sul driver  
 I valori seguenti dell'argomento *InfoType* restituiscono informazioni sul driver ODBC, ad esempio il numero di istruzioni attive, il nome dell'origine dati e il livello di conformità standard dell'interfaccia:  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_FILE_USAGE|  
|SQL_ASYNC_MODE|SQL_GETDATA_EXTENSIONS|  
|SQL_ASYNC_NOTIFICATION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_BATCH_ROW_COUNT|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_BATCH_SUPPORT|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_DATA_SOURCE_NAME|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_DRIVER_AWARE_POOLING_SUPPORTED|SQL_MAX_CONCURRENT_ACTIVITIES|  
|SQL_DRIVER_HDBC|SQL_MAX_DRIVER_CONNECTIONS|  
|SQL_DRIVER_HDESC|SQL_ODBC_INTERFACE_CONFORMANCE|  
|SQL_DRIVER_HENV|SQL_ODBC_STANDARD_CLI_CONFORMANCE|  
|SQL_DRIVER_HLIB|SQL_ODBC_VER|  
|SQL_DRIVER_HSTMT|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_DRIVER_NAME|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DRIVER_ODBC_VER|SQL_ROW_UPDATES|  
|SQL_DRIVER_VER|SQL_SEARCH_PATTERN_ESCAPE|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|SQL_SERVER_NAME|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_STATIC_CURSOR_ATTRIBUTES2|  
  
> [!NOTE]  
>  Quando si implementa **SQLGetInfo**, un driver può migliorare le prestazioni riducendo al minimo il numero di volte in cui le informazioni vengono inviate o richieste dal server.  
  
## <a name="dbms-product-information"></a>Informazioni sul prodotto DBMS  
 I valori seguenti dell'argomento *InfoType* restituiscono informazioni sul prodotto DBMS, ad esempio il nome e la versione del DBMS:  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>Informazioni origine dati  
 I valori seguenti dell'argomento *InfoType* restituiscono informazioni sull'origine dati, ad esempio le caratteristiche del cursore e le funzionalità di transazione:  
  
|||  
|-|-|  
|SQL_ACCESSIBLE_PROCEDURES|SQL_MULT_RESULT_SETS|  
|SQL_ACCESSIBLE_TABLES|SQL_MULTIPLE_ACTIVE_TXN|  
|SQL_BOOKMARK_PERSISTENCE|SQL_NEED_LONG_DATA_LEN|  
|SQL_CATALOG_TERM|SQL_NULL_COLLATION|  
|SQL_COLLATION_SEQ|SQL_PROCEDURE_TERM|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_SCHEMA_TERM|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_SCROLL_OPTIONS|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_TABLE_TERM|  
|SQL_CURSOR_SENSITIVITY|SQL_TXN_CAPABLE|  
|SQL_DATA_SOURCE_READ_ONLY|SQL_TXN_ISOLATION_OPTION|  
|SQL_DEFAULT_TXN_ISOLATION|SQL_USER_NAME|  
|SQL_DESCRIBE_PARAMETER||  
  
## <a name="supported-sql"></a>SQL supportato  
 I valori seguenti dell'argomento *InfoType* restituiscono informazioni sulle istruzioni SQL supportate dall'origine dati. La sintassi SQL di ogni funzionalità descritta da questi tipi di informazioni è la sintassi SQL-92. Questi tipi di informazioni non descrivono esaurientemente l'intera grammatica SQL-92. Al contrario, descrivono le parti della grammatica per le quali le origini dati offrono in genere diversi livelli di supporto. In particolare, viene analizzata la maggior parte delle istruzioni DDL in SQL-92.  
  
 Le applicazioni devono determinare il livello generale della grammatica supportata dal tipo di informazioni SQL_SQL_CONFORMANCE e utilizzare gli altri tipi di informazioni per determinare le variazioni dal livello di conformità standard dichiarato.  
  
|||  
|-|-|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DROP_TABLE|  
|SQL_ALTER_DOMAIN|SQL_DROP_TRANSLATION|  
|SQL_ALTER_SCHEMA|SQL_DROP_VIEW|  
|SQL_ALTER_TABLE|SQL_EXPRESSIONS_IN_ORDERBY|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_GROUP_BY|  
|SQL_CATALOG_LOCATION|SQL_IDENTIFIER_CASE|  
|SQL_CATALOG_NAME|SQL_IDENTIFIER_QUOTE_CHAR|  
|SQL_CATALOG_NAME_SEPARATOR|SQL_INDEX_KEYWORDS|  
|SQL_CATALOG_USAGE|SQL_INSERT_STATEMENT|  
|SQL_COLUMN_ALIAS|SQL_INTEGRITY|  
|SQL_CORRELATION_NAME|SQL_KEYWORDS|  
|SQL_CREATE_ASSERTION|SQL_LIKE_ESCAPE_CLAUSE|  
|SQL_CREATE_CHARACTER_SET|SQL_NON_NULLABLE_COLUMNS|  
|SQL_CREATE_COLLATION|SQL_SQL_CONFORMANCE|  
|SQL_CREATE_DOMAIN|SQL_OJ_CAPABILITIES|  
|SQL_CREATE_SCHEMA|SQL_ORDER_BY_COLUMNS_IN_SELECT|  
|SQL_CREATE_TABLE|SQL_OUTER_JOINS|  
|SQL_CREATE_TRANSLATION|SQL_PROCEDURES|  
|SQL_DDL_INDEX|SQL_QUOTED_IDENTIFIER_CASE|  
|SQL_DROP_ASSERTION|SQL_SCHEMA_USAGE|  
|SQL_DROP_CHARACTER_SET|SQL_SPECIAL_CHARACTERS|  
|SQL_DROP_COLLATION|SQL_SUBQUERIES|  
|SQL_DROP_DOMAIN|SQL_UNION|  
|SQL_DROP_SCHEMA||  
  
## <a name="sql-limits"></a>Limiti SQL  
 I valori seguenti dell'argomento *InfoType* restituiscono informazioni sui limiti applicati agli identificatori e alle clausole nelle istruzioni SQL, ad esempio le lunghezze massime degli identificatori e il numero massimo di colonne in un elenco di selezione. Le limitazioni possono essere imposte dal driver o dall'origine dati.  
  
|||  
|-|-|  
|SQL_MAX_BINARY_LITERAL_LEN|SQL_MAX_IDENTIFIER_LEN|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAX_INDEX_SIZE|  
|SQL_MAX_CHAR_LITERAL_LEN|SQL_MAX_PROCEDURE_NAME_LEN|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAX_ROW_SIZE|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAX_ROW_SIZE_INCLUDES_LONG|  
|SQL_MAX_COLUMNS_IN_INDEX|SQL_MAX_SCHEMA_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAX_STATEMENT_LEN|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAX_TABLE_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAX_TABLES_IN_SELECT|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAX_USER_NAME_LEN|  
  
## <a name="scalar-function-information"></a>Informazioni sulle funzioni scalari  
 I valori seguenti dell'argomento *InfoType* restituiscono informazioni sulle funzioni scalari supportate dall'origine dati e dal driver. Per ulteriori informazioni sulle funzioni scalari, vedere [Appendice E: funzioni scalari](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>Informazioni di conversione  
 I valori seguenti dell'argomento *InfoType* restituiscono un elenco dei tipi di dati SQL in cui l'origine dati può convertire il tipo di dati SQL specificato con la funzione scalare **Convert** :  
  
|||  
|-|-|  
|SQL_CONVERT_BIGINT|SQL_CONVERT_LONGVARBINARY|  
|SQL_CONVERT_BINARY|SQL_CONVERT_LONGVARCHAR|  
|SQL_CONVERT_BIT|SQL_CONVERT_NUMERIC|  
|SQL_CONVERT_CHAR|SQL_CONVERT_REAL|  
|SQL_CONVERT_DATE|SQL_CONVERT_SMALLINT|  
|SQL_CONVERT_DECIMAL|SQL_CONVERT_TIME|  
|SQL_CONVERT_DOUBLE|SQL_CONVERT_TIMESTAMP|  
|SQL_CONVERT_FLOAT|SQL_CONVERT_TINYINT|  
|SQL_CONVERT_INTEGER|SQL_CONVERT_VARBINARY|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_CONVERT_VARCHAR|  
|SQL_CONVERT_INTERVAL_DAY_TIME||  
  
## <a name="information-types-added-for-odbc-3x"></a>Tipi di informazioni aggiunti per ODBC 3. x  
 Sono stati aggiunti i valori seguenti dell'argomento *InfoType* per ODBC 3 *. x*:  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_DRIVER_AWARE_POOLING_SUPPORTED|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DRIVER_HDESC|  
|SQL_ALTER_DOMAIN|SQL_DROP_ASSERTION|  
|SQL_ALTER_SCHEMA|SQL_DROP_CHARACTER_SET|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_DROP_COLLATION|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_DROP_DOMAIN|  
|SQL_ASYNC_MODE|SQL_DROP_SCHEMA|  
|SQL_ASYNC_NOTIFICATION|SQL_DROP_TABLE|  
|SQL_BATCH_ROW_COUNT|SQL_DROP_TRANSLATION|  
|SQL_BATCH_SUPPORT|SQL_DROP_VIEW|  
|SQL_CATALOG_NAME|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|  
|SQL_COLLATION_SEQ|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|  
|SQL_CONVERT_INTERVAL_DAY_TIME|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_ASSERTION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_CREATE_CHARACTER_SET|SQL_INSERT_STATEMENT|  
|SQL_CREATE_COLLATION|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_CREATE_DOMAIN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_SCHEMA|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_CREATE_TABLE|SQL_MAX_IDENTIFIER_LEN|  
|SQL_CREATE_TRANSLATION|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_CURSOR_SENSITIVITY|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DDL_INDEX|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_DESCRIBE_PARAMETER|SQL_STATIC_CURSOR_ATTRIBUTES2|  
|SQL_DM_VER|SQL_XOPEN_CLI_YEAR|  
  
## <a name="information-types-renamed-for-odbc-3x"></a>Tipi di informazioni rinominati per ODBC 3. x  
 I valori seguenti dell'argomento *InfoType* sono stati rinominati per ODBC 3 *. x*.  
  
 SQL_ACTIVE_CONNECTIONS  
 SQL_MAX_DRIVER_CONNECTIONS  
  
 SQL_ACTIVE_STATEMENTS  
 SQL_MAX_CONCURRENT_ACTIVITIES  
  
 SQL_MAX_OWNER_NAME_LEN  
 SQL_MAX_SCHEMA_NAME_LEN  
  
 SQL_MAX_QUALIFIER_NAME_LEN  
 SQL_MAX_CATALOG_NAME_LEN  
  
 SQL_ODBC_SQL_OPT_IEF  
 SQL_INTEGRITY  
  
 SQL_OWNER_TERM  
 SQL_SCHEMA_TERM  
  
 SQL_OWNER_USAGE  
 SQL_SCHEMA_USAGE  
  
 SQL_QUALIFIER_LOCATION  
 SQL_CATALOG_LOCATION  
  
 SQL_QUALIFIER_NAME_SEPARATOR  
 SQL_CATALOG_NAME_SEPARATOR  
  
 SQL_QUALIFIER_TERM  
 SQL_CATALOG_TERM  
  
 SQL_QUALIFIER_USAGE  
 SQL_CATALOG_USAGE  
  
## <a name="information-types-deprecated-in-odbc-3x"></a>Tipi di informazioni deprecati in ODBC 3. x  
 I valori seguenti dell'argomento *InfoType* sono stati deprecati in ODBC 3 *. x*. I driver ODBC 3 *. x* devono continuare a supportare questi tipi di informazioni per la compatibilità con le versioni precedenti delle applicazioni ODBC 2 *. x* . Per ulteriori informazioni su questi tipi, vedere [supporto di SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md) in Appendice G: linee guida per la compatibilità con le versioni precedenti.  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>Descrizioni dei tipi di informazioni  
 Nella tabella seguente vengono elencate in ordine alfabetico ogni tipo di informazioni, la versione di ODBC in cui è stata introdotta e la relativa descrizione.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1,0)  
 Stringa di caratteri: "Y" se l'utente è in grado di eseguire tutte le routine restituite da **SQLProcedures**; "N" se è possibile che vengano restituite procedure che non possono essere eseguite dall'utente.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1,0)  
 Una stringa di caratteri: "Y" se all'utente sono garantiti i privilegi di **selezione** per tutte le tabelle restituite da **SQLTables**; "N" se è possibile che vengano restituite tabelle a cui l'utente non può accedere.  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3,0)  
 Valore SQLUSMALLINT che specifica il numero massimo di ambienti attivi che il driver è in grado di supportare. Se non è presente alcun limite specificato o il limite è sconosciuto, questo valore viene impostato su zero.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3,0)  
 Maschera di SQLUINTEGER che enumera il supporto per le funzioni di aggregazione:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_ALTER_DOMAIN (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **ALTER Domain** , come definito in SQL-92, supportate dall'origine dati. Un driver SQL-92 conforme a livello completo restituirà sempre tutte le maschere di bit. Un valore restituito pari a "0" indica che l'istruzione **ALTER Domain** non è supportata.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = è supportato l'aggiunta di un vincolo di dominio (livello completo)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter Domain> \<set Domain default clause> è supportato (livello completo)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<la clausola di definizione del nome del vincolo> è supportata per la denominazione del vincolo di dominio (livello intermedio)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<drop Domain CONSTRAINT clause> è supportato (livello completo)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter Domain> \<drop Domain default> è supportato (livello completo)  
  
 I seguenti bit specificano gli \<attributi di vincolo supportati \<> se è supportato l'aggiunta di un vincolo di dominio> (il bit SQL_AD_ADD_DOMAIN_CONSTRAINT è impostato):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (livello completo) SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (livello completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (livello completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo)  
  
 SQL_ALTER_TABLE (ODBC 2,0)  
 Maschera di SQLUINTEGER che enumera le clausole nell'istruzione **ALTER TABLE** supportata dall'origine dati.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<aggiungi colonna> clausola è supportata con la funzionalità per specificare le regole di confronto delle colonne (livello completo) (ODBC 3,0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<aggiungi colonna> clausola è supportata con la funzionalità per specificare i valori predefiniti delle colonne (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<aggiungi colonna> supportata (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_ADD_CONSTRAINT = \<aggiungi colonna> clausola è supportata con la funzionalità per specificare i vincoli di colonna (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<clausola Add TABLE Constraint> supportata (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<il nome del vincolo> della definizione è supportato per la denominazione di vincoli di colonna e tabella (livello intermedio) (ODBC 3,0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<DROP COLUMN> Cascade è supportato (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alter Column> \<DROP column default clause> è supportato (livello intermedio) (ODBC 3,0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<DROP COLUMN> Restrict è supportato (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3,0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<DROP COLUMN> Restrict è supportato (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alter Column> \<SET column default clause> è supportato (livello intermedio) (ODBC 3,0)  
  
 I seguenti bit specificano gli \<attributi del vincolo di supporto> se sono supportati i vincoli di colonna o di tabella (il bit SQL_AT_ADD_CONSTRAINT è impostato):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (livello completo) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (livello completo) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (livello completo) (ODBC 3,0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3,8)  
 Valore SQLUINTEGER che indica se il driver è in grado di eseguire funzioni in modo asincrono sull'handle di connessione.  
  
 SQL_ASYNC_DBC_CAPABLE = il driver può eseguire funzioni di connessione in modo asincrono.  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = il driver non è in grado di eseguire funzioni di connessione in modo asincrono.  
  
 SQL_ASYNC_MODE (ODBC 3,0)  
 Valore SQLUINTEGER che indica il livello di supporto asincrono nel driver:  
  
 SQL_AM_CONNECTION = esecuzione asincrona a livello di connessione supportata. Tutti gli handle di istruzione associati a un determinato handle di connessione sono in modalità asincrona o tutti sono in modalità sincrona. Un handle di istruzione in una connessione non può essere in modalità asincrona mentre un altro handle di istruzione nella stessa connessione è in modalità sincrona e viceversa.  
  
 SQL_AM_STATEMENT = esecuzione asincrona a livello di istruzione supportata. Alcuni handle di istruzione associati a un handle di connessione possono essere in modalità asincrona, mentre altri handle di istruzione nella stessa connessione sono in modalità sincrona.  
  
 SQL_AM_NONE = la modalità asincrona non è supportata.  
  
 SQL_ASYNC_NOTIFICATION  
 Valore SQLUINTEGER che indica se il driver supporta la notifica asincrona:  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE** La notifica di esecuzione asincrona è supportata dal driver.  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE** La notifica di esecuzione asincrona non è supportata dal driver.  
  
 Esistono due categorie di operazioni asincrone ODBC: operazioni asincrone a livello di connessione e operazioni asincrone a livello di istruzione.  Se un driver restituisce SQL_ASYNC_NOTIFICATION_CAPABLE, deve supportare le notifiche per tutte le API che possono essere eseguite in modo asincrono.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3,0)  
 Maschera di SQLUINTEGER che enumera il comportamento del driver rispetto alla disponibilità dei conteggi delle righe. Insieme al tipo di informazioni vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_BRC_ROLLED_UP = il numero di righe per le istruzioni INSERT, DELETE o UPDATE consecutive viene sottoposta a rollup. Se questo bit non è impostato, i conteggi delle righe sono disponibili per ogni istruzione.  
  
 SQL_BRC_PROCEDURES = i conteggi delle righe, se presenti, sono disponibili quando un batch viene eseguito in una stored procedure. Se i conteggi delle righe sono disponibili, è possibile eseguirne il rollup o la disponibilità singola, a seconda del SQL_BRC_ROLLED_UP bit.  
  
 SQL_BRC_EXPLICIT = i conteggi delle righe, se presenti, sono disponibili quando un batch viene eseguito direttamente tramite una chiamata a **SQLExecute** o **SQLExecDirect**. Se i conteggi delle righe sono disponibili, è possibile eseguirne il rollup o la disponibilità singola, a seconda del SQL_BRC_ROLLED_UP bit.  
  
 SQL_BATCH_SUPPORT (ODBC 3,0)  
 Maschera di SQLUINTEGER che enumera il supporto del driver per i batch. Per determinare il livello supportato, vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_BS_SELECT_EXPLICIT = il driver supporta batch espliciti che possono avere istruzioni di generazione dei set di risultati.  
  
 SQL_BS_ROW_COUNT_EXPLICIT = il driver supporta batch espliciti che possono includere istruzioni per la generazione di conteggi di righe.  
  
 SQL_BS_SELECT_PROC = il driver supporta procedure esplicite che possono avere istruzioni di generazione del set di risultati.  
  
 SQL_BS_ROW_COUNT_PROC = il driver supporta procedure esplicite che possono avere istruzioni di generazione del conteggio delle righe.  
  
 SQL_BOOKMARK_PERSISTENCE (ODBC 2,0)  
 Maschera di SQLUINTEGER che enumera le operazioni attraverso le quali i segnalibri vengono salvati.  
  
 Le seguenti maschere di maschera vengono utilizzate insieme al flag per determinare il modo in cui i segnalibri delle opzioni vengono mantenuti:  
  
 SQL_BP_CLOSE = i segnalibri sono validi dopo che un'applicazione chiama **SQLFreeStmt** con l'opzione SQL_CLOSE oppure **SQLCloseCursor** per chiudere il cursore associato a un'istruzione.  
  
 SQL_BP_DELETE = il segnalibro per una riga è valido dopo che la riga è stata eliminata.  
  
 SQL_BP_DROP = i segnalibri sono validi dopo che un'applicazione chiama **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_STMT per eliminare un'istruzione.  
  
 SQL_BP_TRANSACTION = i segnalibri sono validi dopo il commit o il rollback di una transazione da parte di un'applicazione.  
  
 SQL_BP_UPDATE = il segnalibro per una riga è valido dopo l'aggiornamento di qualsiasi colonna della riga, incluse le colonne chiave.  
  
 SQL_BP_OTHER_HSTMT = è possibile utilizzare un segnalibro associato a un'istruzione con un'altra istruzione. A meno che non sia specificato SQL_BP_CLOSE o SQL_BP_DROP, il cursore sulla prima istruzione deve essere aperto.  
  
 SQL_CATALOG_LOCATION (ODBC 2,0)  
 Valore SQLUSMALLINT che indica la posizione del catalogo in un nome di tabella qualificato:  
  
 SQL_CL_STARTSQL_CL_END  
  
 Un driver Xbase, ad esempio, restituisce SQL_CL_START perché il nome della directory (Catalog) si trova all'inizio del nome della tabella, come in \EMPDATA\EMP. DBF. Un driver del server ORACLE restituisce SQL_CL_END perché il catalogo si trova alla fine del nome della tabella, come ADMIN.EMP@EMPDATAin.  
  
 Un driver conforme a livello di SQL-92 restituirà sempre SQL_CL_START. Se i cataloghi non sono supportati dall'origine dati, viene restituito il valore 0. Per determinare se i cataloghi sono supportati, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_CATALOG_NAME.  
  
 Questo *InfoType* è stato rinominato per ODBC 3,0 da ODBC 2,0 *InfoType* SQL_QUALIFIER_LOCATION.  
  
 SQL_CATALOG_NAME (ODBC 3,0)  
 Una stringa di caratteri: "Y" Se il server supporta i nomi di catalogo oppure "N" in caso contrario.  
  
 Un driver conforme a SQL-92 restituirà sempre "Y".  
  
 SQL_CATALOG_NAME_SEPARATOR (ODBC 1,0)  
 Una stringa di caratteri: il carattere o i caratteri definiti dall'origine dati come separatore tra un nome di catalogo e l'elemento del nome completo che segue o lo precede.  
  
 Se i cataloghi non sono supportati dall'origine dati, viene restituita una stringa vuota. Per determinare se i cataloghi sono supportati, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_CATALOG_NAME. Un driver conforme a SQL-92 restituirà sempre ".".  
  
 Questo *InfoType* è stato rinominato per ODBC 3,0 da ODBC 2,0 *InfoType* SQL_QUALIFIER_NAME_SEPARATOR.  
  
 SQL_CATALOG_TERM (ODBC 1,0)  
 Stringa di caratteri con il nome del fornitore dell'origine dati per un catalogo. ad esempio, "database" o "directory". Questa stringa può essere in lettere maiuscole, minuscole o miste.  
  
 Se i cataloghi non sono supportati dall'origine dati, viene restituita una stringa vuota. Per determinare se i cataloghi sono supportati, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_CATALOG_NAME. Un driver conforme a SQL-92 restituirà sempre "Catalog".  
  
 Questo *InfoType* è stato rinominato per ODBC 3,0 da ODBC 2,0 *InfoType* SQL_QUALIFIER_TERM.  
  
 SQL_CATALOG_USAGE (ODBC 2,0)  
 Maschera di SQLUINTEGER che enumera le istruzioni in cui è possibile utilizzare i cataloghi.  
  
 Per determinare dove è possibile usare i cataloghi, vengono usate le maschere di maschera seguenti:  
  
 SQL_CU_DML_STATEMENTS = i cataloghi sono supportati in tutte le istruzioni del linguaggio di manipolazione dei dati: **selezionare**, **inserire**, **aggiornare**, **eliminare**e, se supportato, **selezionare per** le istruzioni Update e Delete posizionate.  
  
 SQL_CU_PROCEDURE_INVOCATION = i cataloghi sono supportati nell'istruzione di chiamata della procedura ODBC.  
  
 SQL_CU_TABLE_DEFINITION = i cataloghi sono supportati in tutte le istruzioni di definizione della tabella: **Create Table**, **Create View**, **ALTER TABLE**, **Drop Table**e **Drop View**.  
  
 SQL_CU_INDEX_DEFINITION = i cataloghi sono supportati in tutte le istruzioni per la definizione dell'indice: **create index** e **Drop index**.  
  
 SQL_CU_PRIVILEGE_DEFINITION = i cataloghi sono supportati in tutte le istruzioni di definizione dei privilegi: **Grant** e **Revoke**.  
  
 Se i cataloghi non sono supportati dall'origine dati, viene restituito il valore 0. Per determinare se i cataloghi sono supportati, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_CATALOG_NAME. Un driver conforme a SQL-92 restituirà sempre una maschera di bit con tutti questi set di bit.  
  
 Questo *InfoType* è stato rinominato per ODBC 3,0 da ODBC 2,0 *InfoType* SQL_QUALIFIER_USAGE.  
  
 SQL_COLLATION_SEQ (ODBC 3,0)  
 Nome della sequenza di regole di confronto. Si tratta di una stringa di caratteri che indica il nome delle regole di confronto predefinite per il set di caratteri predefinito per questo server (ad esempio, "ISO 8859-1" o EBCDIC). Se questa operazione è sconosciuta, verrà restituita una stringa vuota. Un driver conforme a SQL-92 restituirà sempre una stringa non vuota.  
  
 SQL_COLUMN_ALIAS (ODBC 2,0)  
 Stringa di caratteri: "Y" se l'origine dati supporta gli alias di colonna; in caso contrario, "N".  
  
 Un alias di colonna è un nome alternativo che può essere specificato per una colonna nell'elenco di selezione usando una clausola AS. Un driver conforme a SQL-92 Entry Level restituirà sempre "Y".  
  
 SQL_CONCAT_NULL_BEHAVIOR (ODBC 1,0)  
 Valore SQLUSMALLINT che indica il modo in cui l'origine dati gestisce la concatenazione di colonne con tipo di dati carattere a valori NULL con colonne con tipo di dati character con valori non NULL:  
  
 SQL_CB_NULL = result è un valore NULL.  
  
 SQL_CB_NON_NULL = result è una concatenazione di colonne o colonne con valori non NULL.  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre SQL_CB_NULL.  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_ DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1,0)  
 Maschera di SQLUINTEGER. La maschera di maschera indica le conversioni supportate dall'origine dati con la funzione di **conversione** scalare per i dati del tipo denominato in *InfoType*. Se la maschera di maschera è uguale a zero, l'origine dati non supporta le conversioni dai dati del tipo denominato, inclusa la conversione nello stesso tipo di dati.  
  
 Per determinare, ad esempio, se un'origine dati supporta la conversione dei dati SQL_INTEGER nel tipo di dati SQL_BIGINT, un'applicazione chiama **SQLGetInfo** con il *InfoType* di SQL_CONVERT_INTEGER. L'applicazione esegue un'operazione **and** con la maschera di maschera restituita e SQL_CVT_BIGINT. Se il valore risultante è diverso da zero, la conversione è supportata.  
  
 Per determinare le conversioni supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_CVT_BIGINT (ODBC 1.0) SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1,0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1,0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DECIMAL (ODBC 1.0) SQL_CVT_DOUBLE (ODBC 1.0) SQL_CVT_FLOAT (ODBC 1.0) SQL_CVT_INTEGER (ODBC 1.0) SQL _CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0) SQL_CVT_LONGVARBINARY (ODBC 1.0) SQL_CVT_LONGVARCHAR (ODBC 1.0) SQL_CVT_NUMERIC (ODBC 1.0) SQL_CVT_REAL ODBC 1.0) SQL_CVT_SMALLINT (ODBC 1.0) SQL_CVT_TIME (ODBC 1.0) SQL_CVT_ TIMESTAMP (ODBC 1.0) SQL_CVT_TINYINT (ODBC 1.0) SQL_CVT_VARBINARY (ODBC 1.0) SQL_CVT_VARCHAR (ODBC 1,0)  
  
 SQL_CONVERT_FUNCTIONS (ODBC 1,0)  
 Maschera di SQLUINTEGER che enumera le funzioni di conversione scalari supportate dal driver e dall'origine dati associata.  
  
 La maschera di maschera seguente viene utilizzata per determinare quali funzioni di conversione sono supportate:  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME (ODBC 1,0)  
 Valore SQLUSMALLINT che indica se sono supportati i nomi di correlazione delle tabelle:  
  
 SQL_CN_NONE = i nomi di correlazione non sono supportati.  
  
 SQL_CN_DIFFERENT = i nomi di correlazione sono supportati, ma devono essere diversi dai nomi delle tabelle che rappresentano.  
  
 SQL_CN_ANY = i nomi di correlazione sono supportati e possono essere qualsiasi nome definito dall'utente valido.  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre SQL_CN_ANY.  
  
 SQL_CREATE_ASSERTION (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **create Assertion** , come definito in SQL-92, supportate dall'origine dati.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_CA_CREATE_ASSERTION  
  
 I seguenti bit specificano l'attributo di vincolo supportato se è supportata la possibilità di specificare in modo esplicito gli attributi di vincolo (vedere i tipi di informazioni SQL_ALTER_TABLE e SQL_CREATE_TABLE):  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 Un driver conforme a SQL-92 restituirà sempre tutte queste opzioni come supportate. Un valore restituito pari a "0" indica che l'istruzione **create Assertion** non è supportata.  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **create character set** , in base a quanto definito in SQL-92, supportato dall'origine dati.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 Un driver conforme a SQL-92 restituirà sempre tutte queste opzioni come supportate. Un valore restituito pari a "0" indica che l'istruzione **create character set** non è supportata.  
  
 SQL_CREATE_COLLATION (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **create Collation** , come definito in SQL-92, supportato dall'origine dati.  
  
 La maschera di maschera seguente viene utilizzata per determinare le clausole supportate:  
  
 SQL_CCOL_CREATE_COLLATION  
  
 Un driver conforme a SQL-92 restituirà sempre questa opzione come supportata. Un valore restituito pari a "0" indica che l'istruzione **create Collation** non è supportata.  
  
 SQL_CREATE_DOMAIN (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **create Domain** , come definito in SQL-92, supportato dall'origine dati.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_CDO_CREATE_DOMAIN = l'istruzione CREATE DOMAIN è supportata (livello intermedio).  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION = \<il nome del vincolo> della definizione è supportato per la denominazione dei vincoli di dominio (livello intermedio).  
  
 I seguenti bit specificano la possibilità di creare vincoli di colonna: SQL_CDO_DEFAULT = la specifica dei vincoli di dominio è supportata (livello intermedio) SQL_CDO_CONSTRAINT = specificare le impostazioni predefinite del dominio è supportato (livello intermedio) SQL_CDO_COLLATION = Impostazione delle regole di confronto del dominio supportata (livello completo)  
  
 I seguenti bit specificano gli attributi di vincolo supportati se sono supportati i vincoli di dominio (SQL_CDO_DEFAULT è impostato):  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED (livello completo) SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo) SQL_CDO_CONSTRAINT_DEFERRABLE (livello completo) SQL_CDO_CONSTRAINT_NON_DEFERRABLE (livello completo)  
  
 Un valore restituito pari a "0" indica che l'istruzione **create Domain** non è supportata.  
  
 SQL_CREATE_SCHEMA (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **create schema** , in base a quanto definito in SQL-92, supportato dall'origine dati.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 Un driver conforme al livello intermedio SQL-92 restituisce sempre le opzioni SQL_CS_CREATE_SCHEMA e SQL_CS_AUTHORIZATION supportate. Questi devono essere supportati anche a livello di voce SQL-92, ma non necessariamente come istruzioni SQL. Un driver conforme a SQL-92 restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_CREATE_TABLE (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **Create Table** , come definito in SQL-92, supportato dall'origine dati.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_CT_CREATE_TABLE = l'istruzione CREATE TABLE è supportata. (Livello di ingresso)  
  
 SQL_CT_TABLE_CONSTRAINT = specifica di vincoli di tabella supportata (livello di transizione FIPS)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION = la \<clausola> per la definizione del nome del vincolo è supportata per la denominazione di vincoli di colonna e tabella (livello intermedio)  
  
 I seguenti bit specificano la possibilità di creare tabelle temporanee:  
  
 SQL_CT_COMMIT_PRESERVE = le righe eliminate vengono mantenute al commit. (Livello completo) SQL_CT_COMMIT_DELETE = le righe eliminate vengono eliminate al commit. (Livello completo) SQL_CT_GLOBAL_TEMPORARY = è possibile creare tabelle temporanee globali. (Livello completo) SQL_CT_LOCAL_TEMPORARY = è possibile creare tabelle temporanee locali. (Livello completo)  
  
 I seguenti bit specificano la possibilità di creare vincoli di colonna:  
  
 SQL_CT_COLUMN_CONSTRAINT = sono supportati i vincoli di colonna (livello di transizione FIPS) SQL_CT_COLUMN_DEFAULT = è supportata la specifica delle impostazioni predefinite della colonna (livello di transizione FIPS) SQL_CT_COLUMN_COLLATION = specifica delle regole di confronto delle colonne supportato (livello completo)  
  
 I seguenti bit specificano gli attributi di vincolo supportati se sono supportati i vincoli di colonna o di tabella:  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED (livello completo) SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo) SQL_CT_CONSTRAINT_DEFERRABLE (livello completo) SQL_CT_CONSTRAINT_NON_DEFERRABLE (livello completo)  
  
 SQL_CREATE_TRANSLATION (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **create Translation** , come definito in SQL-92, supportato dall'origine dati.  
  
 La maschera di maschera seguente viene utilizzata per determinare le clausole supportate:  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 Un driver conforme a SQL-92 restituirà sempre queste opzioni come supportate. Un valore restituito pari a "0" indica che l'istruzione **create Translation** non è supportata.  
  
 SQL_CREATE_VIEW (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **Create View** , come definito in SQL-92, supportato dall'origine dati.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 Un valore restituito pari a "0" indica che l'istruzione **Create View** non è supportata.  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre le opzioni SQL_CV_CREATE_VIEW e SQL_CV_CHECK_OPTION supportate.  
  
 Un driver conforme a SQL-92 restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR (ODBC 1,0)  
 Valore SQLUSMALLINT che indica la modalità di esecuzione di un'operazione di **commit** sui cursori e sulle istruzioni preparate nell'origine dati (il comportamento dell'origine dati quando si esegue il commit di una transazione).  
  
 Il valore di questo attributo rifletterà lo stato corrente dell'impostazione successiva: SQL_COPT_SS_PRESERVE_CURSORS.  
  
 SQL_CB_DELETE = chiusura di cursori ed eliminazione di istruzioni preparate. Per utilizzare di nuovo il cursore, l'applicazione deve ripreparare ed eseguire nuovamente l'istruzione.  
  
 SQL_CB_CLOSE = chiusura cursori. Per le istruzioni preparate, l'applicazione può chiamare **SQLExecute** sull'istruzione senza chiamare nuovamente **SQLPrepare** . Per impostazione predefinita, il driver ODBC SQL è SQL_CB_CLOSE. Ciò significa che il driver ODBC di SQL chiuderà i cursori quando si esegue il commit di una transazione.  
  
 SQL_CB_PRESERVE = mantiene i cursori nella stessa posizione di prima dell'operazione di **commit** . L'applicazione può continuare a recuperare i dati oppure può chiudere il cursore ed eseguire nuovamente l'istruzione senza riprepararla.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR (ODBC 1,0)  
 Valore SQLUSMALLINT che indica il modo in cui un'operazione di **rollback** influiscono sui cursori e sulle istruzioni preparate nell'origine dati:  
  
 SQL_CB_DELETE = chiusura di cursori ed eliminazione di istruzioni preparate. Per utilizzare di nuovo il cursore, l'applicazione deve ripreparare ed eseguire nuovamente l'istruzione.  
  
 SQL_CB_CLOSE = chiusura cursori. Per le istruzioni preparate, l'applicazione può chiamare **SQLExecute** sull'istruzione senza chiamare nuovamente **SQLPrepare** .  
  
 SQL_CB_PRESERVE = mantiene i cursori nella stessa posizione di prima dell'operazione di **rollback** . L'applicazione può continuare a recuperare i dati oppure può chiudere il cursore ed eseguire nuovamente l'istruzione senza riprepararla.  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3,0)  
 Valore SQLUINTEGER che indica il supporto per la sensibilità del cursore:  
  
 SQL_INSENSITIVE = tutti i cursori nell'handle di istruzione visualizzano il set di risultati senza riflettere le modifiche apportate da un altro cursore all'interno della stessa transazione.  
  
 SQL_UNSPECIFIED = non viene specificato se i cursori nell'handle di istruzione rendono visibili le modifiche apportate a un set di risultati da un altro cursore all'interno della stessa transazione. I cursori nell'handle dell'istruzione possono rendere visibile nessuno, alcune o tutte le modifiche.  
  
 SQL_SENSITIVE = i cursori sono sensibili alle modifiche apportate da altri cursori all'interno della stessa transazione.  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre l'opzione SQL_UNSPECIFIED come supportata.  
  
 Un driver conforme a SQL-92 restituirà sempre l'opzione SQL_INSENSITIVE come supportata.  
  
 SQL_DATA_SOURCE_NAME (ODBC 1,0)  
 Stringa di caratteri con il nome dell'origine dati utilizzato durante la connessione. Se l'applicazione ha chiamato **SQLConnect**, questo è il valore dell'argomento *szDSN* . Se l'applicazione ha chiamato **SQLDriverConnect** o **SQLBrowseConnect**, questo è il valore della parola chiave DSN nella stringa di connessione passata al driver. Se la stringa di connessione non contiene la parola chiave **DSN** , ad esempio quando contiene la parola chiave **driver** , si tratta di una stringa vuota.  
  
 SQL_DATA_SOURCE_READ_ONLY (ODBC 1,0)  
 Stringa di caratteri. "Y" se l'origine dati è impostata sulla modalità di sola lettura, "N" in caso contrario.  
  
 Questa caratteristica è pertinente solo per l'origine dati. non è una caratteristica del driver che consente l'accesso all'origine dati. Un driver in lettura/scrittura può essere utilizzato con un'origine dati di sola lettura. Se un driver è di sola lettura, tutte le relative origini dati devono essere di sola lettura e devono restituire SQL_DATA_SOURCE_READ_ONLY.  
  
 SQL_DATABASE_NAME (ODBC 1,0)  
 Stringa di caratteri con il nome del database corrente in uso, se l'origine dati definisce un oggetto denominato denominato "database".  
  
> [!NOTE]
>  In ODBC 3 *. x*, il valore restituito per questo *InfoType* può essere restituito anche chiamando **SQLGetConnectAttr** con un argomento *attribute* di SQL_ATTR_CURRENT_CATALOG.  
  
 SQL_DATETIME_LITERALS (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera i valori letterali datetime di SQL-92 supportati dall'origine dati. Si noti che si tratta dei valori letterali datetime elencati nella specifica SQL-92 e sono distinti dalle clausole Escape letterali datetime definite da ODBC. Per ulteriori informazioni sulle clausole di escape del valore letterale datetime ODBC, vedere [data, ora e valori letterali timestamp](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Un driver con livello di transizione FIPS restituisce sempre il valore "1" nella maschera di bit per i bit nell'elenco seguente. Il valore "0" indica che i valori letterali datetime di SQL-92 non sono supportati.  
  
 Per determinare quali valori letterali sono supportati, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_ SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME (ODBC 1,0)  
 Stringa di caratteri con il nome del prodotto DBMS accessibile dal driver.  
  
 SQL_DBMS_VER (ODBC 1,0)  
 Stringa di caratteri che indica la versione del prodotto DBMS accessibile dal driver. Il formato della versione è # #. # #. # # # #, dove le prime due cifre sono la versione principale, le due cifre successive sono la versione secondaria e le ultime quattro cifre sono la versione di rilascio. Il driver deve eseguire il rendering della versione del prodotto DBMS in questo modulo, ma può anche aggiungere la versione specifica del prodotto DBMS. Ad esempio, "04.01.0000 RDB 4,1".  
  
 SQL_DDL_INDEX (ODBC 3,0)  
 Valore SQLUINTEGER che indica il supporto per la creazione e l'eliminazione di indici:  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION (ODBC 1,0)  
 Valore SQLUINTEGER che indica il livello di isolamento della transazione predefinito supportato dal driver o dall'origine dati oppure zero se l'origine dati non supporta le transazioni. I termini seguenti vengono usati per definire i livelli di isolamento delle transazioni:  
  
 **Lettura dirty** La transazione 1 modifica una riga. La transazione 2 legge la riga modificata prima che la transazione 1 Esegui il commit della modifica. Se la transazione 1 esegue il rollback della modifica, la transazione 2 avrà letto una riga che non è mai esistita.  
  
 **Lettura non ripetibile** La transazione 1 legge una riga. La transazione 2 aggiorna o Elimina la riga ed Esegui il commit della modifica. Se la transazione 1 tenta di rileggere la riga, riceverà valori di riga diversi o scoprirà che la riga è stata eliminata.  
  
 **Fantasma** La transazione 1 legge un set di righe che soddisfano alcuni criteri di ricerca. La transazione 2 genera una o più righe (tramite inserimenti o aggiornamenti) che corrispondono ai criteri di ricerca. Se Transaction 1 esegue nuovamente l'istruzione che legge le righe, riceve un set di righe diverso.  
  
 Se l'origine dati supporta le transazioni, il driver restituirà una delle seguenti maschere di maschera:  
  
 SQL_TXN_READ_UNCOMMITTED = letture dirty, letture non ripetibili e Phantom sono possibili.  
  
 SQL_TXN_READ_COMMITTED = le letture dirty non sono possibili. Sono possibili letture non ripetibili e fantasmi.  
  
 SQL_TXN_REPEATABLE_READ = letture dirty e letture non ripetibili non sono possibili. I Phantom sono possibili.  
  
 SQL_TXN_SERIALIZABLE = le transazioni sono serializzabili. Le transazioni serializzabili non consentono letture dirty, letture non ripetibili o Phantom.  
  
 SQL_DESCRIBE_PARAMETER (ODBC 3,0)  
 Stringa di caratteri: "Y" se è possibile descrivere i parametri; "N", in caso contrario.  
  
 Un driver conforme a livello di SQL-92 restituisce in genere "Y" perché supporterà l'istruzione di **input di descrizione** . Poiché questo non specifica direttamente il supporto SQL sottostante, tuttavia, la descrizione dei parametri potrebbe non essere supportata, neanche in un driver conforme a livello di SQL-92.  
  
 SQL_DM_VER (ODBC 3,0)  
 Stringa di caratteri con la versione di gestione driver. Il formato della versione è # #. # #. # # # #. # # # #, dove:  
  
 Il primo set di due cifre è la versione ODBC principale, come indicato dalla costante SQL_SPEC_MAJOR.  
  
 Il secondo set di due cifre è la versione secondaria di ODBC, come indicato dalla costante SQL_SPEC_MINOR.  
  
 Il terzo set di quattro cifre è il numero di build principale di gestione driver.  
  
 L'ultimo set di quattro cifre è il numero di build secondario di gestione driver.  
  
 La versione di gestione driver di Windows 7 è 03,80. La versione di gestione driver di Windows 8 è 03,81.  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3,8)  
 Valore SQLUINTEGER che indica se il driver supporta il pool compatibile con i driver. Per ulteriori informazioni, vedere [pool di connessioni compatibile](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)con i driver.  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE indica che il driver può supportare il meccanismo di pooling compatibile con i driver.  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE indica che il driver non supporta il meccanismo di pooling compatibile con i driver.  
  
 Non è necessario che un driver implementi SQL_DRIVER_AWARE_POOLING_SUPPORTED e che Gestione driver non soddisfi il valore restituito del driver.  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV (ODBC 1,0)  
 Valore SQLULEN, handle di ambiente o handle di connessione del driver, determinato dall'argomento *InfoType*.  
  
 Questi tipi di informazioni sono implementati solo da Gestione driver.  
  
 SQL_DRIVER_HDESC (ODBC 3,0)  
 Un valore SQLULEN, il punto di controllo del descrittore del driver determinato dall'handle del descrittore di gestione driver, \*che deve essere passato all'input in *InfoValuePtr* dall'applicazione. In questo caso, *InfoValuePtr* è un argomento di input e di output. È necessario che l'handle del \*descrittore di input passato in *InfoValuePtr* sia stato allocato in modo esplicito o implicito in *connectionHandle*.  
  
 L'applicazione deve creare una copia dell'handle del descrittore di gestione driver prima di chiamare **SQLGetInfo** con questo tipo di informazioni, per assicurarsi che l'handle non venga sovrascritto nell'output.  
  
 Questo tipo di informazioni viene implementato da solo Gestione driver.  
  
 SQL_DRIVER_HLIB (ODBC 2,0)  
 Valore SQLULEN, *hInst* dalla libreria di caricamento restituito a gestione driver quando è stata caricata la dll del driver in un sistema operativo Microsoft Windows o equivalente in un altro sistema operativo. L'handle è valido solo per l'handle di connessione specificato nella chiamata a **SQLGetInfo**.  
  
 Questo tipo di informazioni viene implementato da solo Gestione driver.  
  
 SQL_DRIVER_HSTMT (ODBC 1,0)  
 Un valore SQLULEN, il punto di controllo dell'istruzione del driver determinato dall'handle di gestione driver, che deve essere passato all' \*input in *InfoValuePtr* dall'applicazione. In questo caso, *InfoValuePtr* è un argomento di input e di output. L'handle dell'istruzione di input \*passato in *InfoValuePtr* deve essere stato allocato nell'argomento *connectionHandle*.  
  
 L'applicazione deve creare una copia dell'handle di istruzione di gestione driver prima di chiamare **SQLGetInfo** con questo tipo di informazioni, per garantire che l'handle non venga sovrascritto nell'output.  
  
 Questo tipo di informazioni viene implementato da solo Gestione driver.  
  
 SQL_DRIVER_NAME (ODBC 1,0)  
 Stringa di caratteri con il nome file del driver utilizzato per accedere all'origine dati.  
  
 SQL_DRIVER_ODBC_VER (ODBC 2,0)  
 Stringa di caratteri con la versione di ODBC supportata dal driver. Il formato della versione è # #. # #, dove le prime due cifre sono la versione principale e le due cifre successive sono la versione secondaria. SQL_SPEC_MAJOR e SQL_SPEC_MINOR definiscono i numeri di versione principale e secondaria. Per la versione di ODBC descritta in questo manuale, sono 3 e 0 e il driver deve restituire "03,00".  
  
 Gestione driver ODBC non modificherà il valore restituito di SQLGetInfo (SQL_DRIVER_ODBC_VER) per mantenere la compatibilità con le versioni precedenti delle applicazioni esistenti. Il driver specifica il valore che verrà restituito. Tuttavia, un driver che supporta l'estendibilità del tipo di dati C deve restituire 3,8 (o versione successiva) quando un'applicazione chiama **SQLSetEnvAttr** per impostare SQL_ATTR_ODBC_VERSION su 3,8. Per ulteriori informazioni, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 SQL_DRIVER_VER (ODBC 1,0)  
 Una stringa di caratteri con la versione del driver e, facoltativamente, una descrizione del driver. Come minimo, la versione è nel formato # #. # #. # # # #, dove le prime due cifre sono la versione principale, le due cifre successive sono la versione secondaria e le ultime quattro cifre sono la versione di rilascio.  
  
 SQL_DROP_ASSERTION (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **Drop Assertion** , come definito in SQL-92, supportato dall'origine dati.  
  
 La maschera di maschera seguente viene utilizzata per determinare le clausole supportate:  
  
 SQL_DA_DROP_ASSERTION  
  
 Un driver conforme a SQL-92 restituirà sempre questa opzione come supportata.  
  
 SQL_DROP_CHARACTER_SET (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **Drop character set** , in base a quanto definito in SQL-92, supportato dall'origine dati.  
  
 La maschera di maschera seguente viene utilizzata per determinare le clausole supportate:  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 Un driver conforme a SQL-92 restituirà sempre questa opzione come supportata.  
  
 SQL_DROP_COLLATION (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **Drop Collation** , come definito in SQL-92, supportato dall'origine dati.  
  
 La maschera di maschera seguente viene utilizzata per determinare le clausole supportate:  
  
 SQL_DC_DROP_COLLATION  
  
 Un driver conforme a SQL-92 restituirà sempre questa opzione come supportata.  
  
 SQL_DROP_DOMAIN (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **Drop Domain** , come definito in SQL-92, supportato dall'origine dati.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 Un driver conforme a SQL-92 intermedia restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_DROP_SCHEMA (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **Drop schema** , come definito in SQL-92, supportato dall'origine dati.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 Un driver conforme a SQL-92 intermedia restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_DROP_TABLE (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **Drop Table** , come definito in SQL-92, supportato dall'origine dati.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 Un driver con livello di transizione FIPS può restituire sempre tutte queste opzioni come supportate.  
  
 SQL_DROP_TRANSLATION (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **Drop Translation** , come definito in SQL-92, supportato dall'origine dati.  
  
 La maschera di maschera seguente viene utilizzata per determinare le clausole supportate:  
  
 SQL_DTR_DROP_TRANSLATION  
  
 Un driver conforme a SQL-92 restituirà sempre questa opzione come supportata.  
  
 SQL_DROP_VIEW (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **Drop View** , come definito in SQL-92, supportato dall'origine dati.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 Un driver con livello di transizione FIPS può restituire sempre tutte queste opzioni come supportate.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (ODBC 3,0)  
 Maschera di SQLUINTEGER che descrive gli attributi di un cursore dinamico supportati dal driver. Questa maschera di maschera contiene il primo subset di attributi. per il secondo subset, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES2.  
  
 Per determinare quali attributi sono supportati, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_CA1_NEXT = un argomento *FetchOrientation* di SQL_FETCH_NEXT è supportato in una chiamata a **SQLFetchScroll** quando il cursore è un cursore dinamico.  
  
 Gli argomenti SQL_CA1_ABSOLUTE = *FetchOrientation* di SQL_FETCH_FIRST, SQL_FETCH_LAST e SQL_FETCH_ABSOLUTE sono supportati in una chiamata a **SQLFetchScroll** quando il cursore è un cursore dinamico. Il set di righe che verrà recuperato è indipendente dalla posizione corrente del cursore.  
  
 Gli argomenti SQL_CA1_RELATIVE = *FetchOrientation* di SQL_FETCH_PRIOR e SQL_FETCH_RELATIVE sono supportati in una chiamata a **SQLFetchScroll** quando il cursore è un cursore dinamico. Il set di righe che verrà recuperato dipende dalla posizione corrente del cursore. Si noti che questa operazione è separata da SQL_FETCH_NEXT perché in un cursore di sola trasmissione è supportato solo SQL_FETCH_NEXT.  
  
 SQL_CA1_BOOKMARK = un argomento *FetchOrientation* di SQL_FETCH_BOOKMARK è supportato in una chiamata a **SQLFetchScroll** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_LOCK_EXCLUSIVE = un argomento *LockType* di SQL_LOCK_EXCLUSIVE è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_LOCK_NO_CHANGE = un argomento *LockType* di SQL_LOCK_NO_CHANGE è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_LOCK_UNLOCK = un argomento *LockType* di SQL_LOCK_UNLOCK è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_POS_POSITION = un argomento *Operation* of SQL_POSITION è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_POS_UPDATE = un argomento *Operation* of SQL_UPDATE è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_POS_DELETE = un argomento *Operation* of SQL_DELETE è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_POS_REFRESH = un argomento *Operation* of SQL_REFRESH è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_POSITIONED_UPDATE = aggiornamento in cui l'istruzione SQL CURRENT OF è supportata quando il cursore è un cursore dinamico. Un driver conforme a livello di voce SQL-92 restituirà sempre questa opzione come supportata.  
  
 SQL_CA1_POSITIONED_DELETE = un'istruzione DELETE in cui CURRENT OF SQL è supportata quando il cursore è un cursore dinamico. Un driver conforme a livello di voce SQL-92 restituirà sempre questa opzione come supportata.  
  
 SQL_CA1_SELECT_FOR_UPDATE = l'istruzione SQL SELECT FOR UPDATE è supportata quando il cursore è un cursore dinamico. Un driver conforme a livello di voce SQL-92 restituirà sempre questa opzione come supportata.  
  
 SQL_CA1_BULK_ADD = un argomento *Operation* of SQL_ADD è supportato in una chiamata a **SQLBulkOperations** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK = un argomento *Operation* of SQL_UPDATE_BY_BOOKMARK è supportato in una chiamata a **SQLBulkOperations** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK = un argomento *Operation* of SQL_DELETE_BY_BOOKMARK è supportato in una chiamata a **SQLBulkOperations** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK = un argomento *Operation* of SQL_FETCH_BY_BOOKMARK è supportato in una chiamata a **SQLBulkOperations** quando il cursore è un cursore dinamico.  
  
 Un driver conforme al livello intermedio SQL-92 restituisce in genere le opzioni SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE supportate, perché supporta i cursori scorrevoli tramite l'istruzione SQL FETCH incorporata. Poiché questo non determina direttamente il supporto SQL sottostante, tuttavia, i cursori scorrevoli potrebbero non essere supportati, anche per un driver conforme al livello intermedio SQL-92.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (ODBC 3,0)  
 Maschera di SQLUINTEGER che descrive gli attributi di un cursore dinamico supportati dal driver. Questa maschera di maschera contiene il secondo subset di attributi. per il primo subset, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1.  
  
 Per determinare quali attributi sono supportati, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = un cursore dinamico di sola lettura, in cui non sono consentiti aggiornamenti, è supportato. È possibile SQL_CONCUR_READ_ONLY l'attributo SQL_ATTR_CONCURRENCY Statement per un cursore dinamico.  
  
 SQL_CA2_LOCK_CONCURRENCY = un cursore dinamico che utilizza il livello di blocco più basso sufficiente per assicurarsi che la riga possa essere aggiornata sia supportata. È possibile SQL_CONCUR_LOCK l'attributo SQL_ATTR_CONCURRENCY Statement per un cursore dinamico. Questi blocchi devono essere coerenti con il livello di isolamento della transazione impostato dall'attributo di connessione SQL_ATTR_TXN_ISOLATION.  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = un cursore dinamico che utilizza il controllo della concorrenza ottimistica che confronta le versioni di riga è supportato. È possibile SQL_CONCUR_ROWVER l'attributo SQL_ATTR_CONCURRENCY Statement per un cursore dinamico.  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = un cursore dinamico che utilizza il controllo della concorrenza ottimistica che confronta i valori è supportato. È possibile SQL_CONCUR_VALUES l'attributo SQL_ATTR_CONCURRENCY Statement per un cursore dinamico.  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = le righe aggiunte sono visibili a un cursore dinamico. il cursore può scorrere fino a tali righe. (Dove queste righe vengono aggiunte al cursore è dipendente dal driver).  
  
 SQL_CA2_SENSITIVITY_DELETIONS = le righe eliminate non sono più disponibili per un cursore dinamico e non lasciano un "Hole" nel set di risultati; Quando il cursore dinamico scorre da una riga eliminata, non può tornare alla riga.  
  
 SQL_CA2_SENSITIVITY_UPDATES = gli aggiornamenti alle righe sono visibili a un cursore dinamico. Se il cursore dinamico scorre da e torna a una riga aggiornata, i dati restituiti dal cursore sono i dati aggiornati, non i dati originali.  
  
 SQL_CA2_MAX_ROWS_SELECT = l'attributo dell'istruzione SQL_ATTR_MAX_ROWS influiscono sulle istruzioni **Select** quando il cursore è un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_INSERT = l'attributo dell'istruzione SQL_ATTR_MAX_ROWS influiscono sulle istruzioni **Insert** quando il cursore è un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_DELETE = l'attributo dell'istruzione SQL_ATTR_MAX_ROWS influiscono sulle istruzioni **Delete** quando il cursore è un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_UPDATE = l'attributo dell'istruzione SQL_ATTR_MAX_ROWS influiscono sulle istruzioni **Update** quando il cursore è un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_CATALOG = l'attributo dell'istruzione SQL_ATTR_MAX_ROWS influiscono sui set di risultati del **Catalogo** quando il cursore è un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = l'attributo dell'istruzione SQL_ATTR_MAX_ROWS influiscono sulle istruzioni **Select**, **Insert**, **Delete**e **Update** e sui set di risultati del **Catalogo** quando il cursore è un cursore dinamico.  
  
 SQL_CA2_CRC_EXACT = il numero esatto di righe è disponibile nel campo di diagnostica SQL_DIAG_CURSOR_ROW_COUNT quando il cursore è un cursore dinamico.  
  
 SQL_CA2_CRC_APPROXIMATE = il numero di righe approssimativo è disponibile nel campo di diagnostica SQL_DIAG_CURSOR_ROW_COUNT quando il cursore è un cursore dinamico.  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = il driver non garantisce che le istruzioni Update o DELETE posizionate in modo simulato influiscano su una sola riga quando il cursore è un cursore dinamico. è responsabilità dell'applicazione garantire questo problema. Se un'istruzione ha effetto su più di una riga, **SQLExecute** o **SQLExecDirect** restituisce SQLSTATE 01001 [conflitto dell'operazione del cursore]. Per impostare questo comportamento, l'applicazione chiama **SQLSetStmtAttr** con l'attributo SQL_ATTR_SIMULATE_CURSOR impostato su SQL_SC_NON_UNIQUE.  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = il driver tenta di garantire che le istruzioni Update o DELETE posizionate simulate influirà su una sola riga quando il cursore è un cursore dinamico. Il driver esegue sempre tali istruzioni, anche se possono interessare più di una riga, ad esempio quando non è presente alcuna chiave univoca. Se un'istruzione ha effetto su più di una riga, **SQLExecute** o **SQLExecDirect** restituisce SQLSTATE 01001 [conflitto dell'operazione del cursore]. Per impostare questo comportamento, l'applicazione chiama **SQLSetStmtAttr** con l'attributo SQL_ATTR_SIMULATE_CURSOR impostato su SQL_SC_TRY_UNIQUE.  
  
 SQL_CA2_SIMULATE_UNIQUE = il driver garantisce che le istruzioni Update o DELETE posizionate in modo simulato influiscano su una sola riga quando il cursore è un cursore dinamico. Se il driver non è in grado di garantire questa condizione per un'istruzione specificata, **SQLExecDirect** o **SQLPrepare** restituiscono SQLSTATE 01001 (conflitto dell'operazione del cursore). Per impostare questo comportamento, l'applicazione chiama **SQLSetStmtAttr** con l'attributo SQL_ATTR_SIMULATE_CURSOR impostato su SQL_SC_UNIQUE.  
  
 SQL_EXPRESSIONS_IN_ORDERBY (ODBC 1,0)  
 Stringa di caratteri: "Y" se l'origine dati supporta le espressioni nell'elenco **Order by** . "N" in caso contrario.  
  
 SQL_FILE_USAGE (ODBC 2,0)  
 Valore SQLUSMALLINT che indica il modo in cui un driver a un solo livello tratta direttamente i file in un'origine dati:  
  
 SQL_FILE_NOT_SUPPORTED = il driver non è un driver a livello singolo. Un driver ORACLE, ad esempio, è un driver a due livelli.  
  
 SQL_FILE_TABLE = un driver a livello singolo considera i file in un'origine dati come tabelle. Un driver Xbase, ad esempio, considera ogni file Xbase come una tabella.  
  
 SQL_FILE_CATALOG = un driver a livello singolo considera i file in un'origine dati come catalogo. Ad esempio, un driver di Microsoft Access considera ogni file di Microsoft Access come un database completo.  
  
 Un'applicazione può utilizzare questa funzione per determinare la modalità di selezione dei dati da parte degli utenti. Ad esempio, gli utenti di Xbase spesso pensano ai dati archiviati nei file, mentre gli utenti di ORACLE e Microsoft Access considerano in genere i dati archiviati nelle tabelle.  
  
 Quando un utente seleziona un'origine dati Xbase, l'applicazione può visualizzare la finestra di dialogo Apri comune del **file** di Windows; Quando l'utente seleziona un'origine dati Microsoft Access o ORACLE, l'applicazione potrebbe visualizzare una finestra di dialogo **Seleziona tabella** personalizzata.  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1 (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore di sola trasmissione supportati dal driver. Questa maschera di maschera contiene il primo subset di attributi. per il secondo subset, vedere SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2.  
  
 Per determinare quali attributi sono supportati, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_ UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Per le descrizioni di queste maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e sostituire il cursore di sola trasmissione per "cursori dinamici" nelle descrizioni).  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2 (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore di sola trasmissione supportati dal driver. Questa maschera di maschera contiene il secondo subset di attributi. per il primo subset, vedere SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1.  
  
 Per determinare quali attributi sono supportati, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Per le descrizioni di queste maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (e sostituire il cursore di sola trasmissione per "cursori dinamici" nelle descrizioni).  
  
 SQL_GETDATA_EXTENSIONS (ODBC 2,0)  
 Maschera di SQLUINTEGER che enumera le estensioni a **SQLGetData**.  
  
 Le seguenti maschere di maschera vengono utilizzate insieme al flag per determinare le estensioni comuni supportate dal driver per **SQLGetData**:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData** può essere chiamato per qualsiasi colonna non associata, inclusi quelli prima dell'ultima colonna associata. Si noti che le colonne devono essere chiamate in ordine di numero di colonna crescente a meno che non venga restituito anche SQL_GD_ANY_ORDER.  
  
 SQL_GD_ANY_ORDER = **SQLGetData** può essere chiamato per le colonne non vincolate in qualsiasi ordine. Si noti che è possibile chiamare **SQLGetData** solo per le colonne successive all'ultima colonna associata, a meno che non venga restituito anche SQL_GD_ANY_COLUMN.  
  
 SQL_GD_BLOCK = **SQLGetData** può essere chiamato per una colonna non associata in una riga di un blocco (dove le dimensioni del set di righe sono maggiori di 1) di dati dopo il posizionamento su tale riga con **SQLSetPos**.  
  
 SQL_GD_BOUND = **SQLGetData** può essere chiamato per le colonne con binding oltre che per le colonne non vincolate. Un driver non può restituire questo valore a meno che non restituisca anche SQL_GD_ANY_COLUMN.  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData** può essere chiamato per restituire i valori dei parametri di output. Per altre informazioni, vedere [recupero di parametri di output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
 **SQLGetData** è necessario per restituire dati solo da colonne non associate che si verificano dopo l'ultima colonna associata, vengono chiamate in ordine di numero di colonna crescente e non si trovano in una riga in un blocco di righe.  
  
 Se un driver supporta i segnalibri (a lunghezza fissa o a lunghezza variabile), deve supportare la chiamata a **SQLGetData** sulla colonna 0. Questo supporto è necessario indipendentemente dal valore restituito dal driver per una chiamata a **SQLGetInfo** con il SQL_GETDATA_EXTENSIONS *InfoType*.  
  
 SQL_GROUP_BY (ODBC 2,0)  
 Valore SQLUSMALLINT che specifica la relazione tra le colonne nella clausola **Group by** e le colonne non aggregate nell'elenco di selezione:  
  
 SQL_GB_COLLATE = è possibile specificare una clausola **COLLATE** alla fine di ogni colonna di raggruppamento. (ODBC 3,0)  
  
 Le clausole SQL_GB_NOT_SUPPORTED = **Group by** non sono supportate. (ODBC 2,0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = la clausola **Group by** deve contenere tutte le colonne non aggregate nell'elenco di selezione. Non può contenere altre colonne. Selezionare, ad esempio, **reparto, massimo (stipendio) dal gruppo Employee per reparto**. (ODBC 2,0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = la clausola **Group by** deve contenere tutte le colonne non aggregate nell'elenco di selezione. Può contenere colonne che non sono incluse nell'elenco di selezione. Selezionare, ad esempio, **reparto, massimo (stipendio) dal gruppo Employee per reparto, Age**. (ODBC 2,0)  
  
 SQL_GB_NO_RELATION = le colonne nella clausola **Group by** e l'elenco di selezione non sono correlate. Il significato delle colonne non raggruppate non aggregate nell'elenco di selezione è dipendente dall'origine dati. Selezionare, ad esempio, **reparto, stipendio dal gruppo Employee per reparto, Age**. (ODBC 2,0)  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre l'opzione SQL_GB_GROUP_BY_EQUALS_SELECT come supportata. Un driver conforme a SQL-92 restituirà sempre l'opzione SQL_GB_COLLATE come supportata. Se nessuna delle opzioni è supportata, la clausola **Group by** non è supportata dall'origine dati.  
  
 SQL_IDENTIFIER_CASE (ODBC 1,0)  
 Un valore SQLUSMALLINT come segue:  
  
 SQL_IC_UPPER = gli identificatori in SQL non fanno distinzione tra maiuscole e minuscole e vengono archiviati in maiuscolo nel catalogo di sistema.  
  
 SQL_IC_LOWER = gli identificatori in SQL non fanno distinzione tra maiuscole e minuscole e vengono archiviati in minuscolo nel catalogo di sistema.  
  
 SQL_IC_SENSITIVE = gli identificatori in SQL fanno distinzione tra maiuscole e minuscole e vengono archiviati in caso misto nel catalogo di sistema.  
  
 SQL_IC_MIXED = gli identificatori in SQL non fanno distinzione tra maiuscole e minuscole e vengono archiviati in caso misto nel catalogo di sistema.  
  
 Poiché gli identificatori in SQL-92 non fanno mai distinzione tra maiuscole e minuscole, un driver conforme esclusivamente a SQL-92 (qualsiasi livello) non restituirà mai l'opzione SQL_IC_SENSITIVE come supportata.  
  
 SQL_IDENTIFIER_QUOTE_CHAR (ODBC 1,0)  
 Stringa di caratteri utilizzata come delimitatore iniziale e finale di un identificatore racchiuso tra virgolette in istruzioni SQL. (Gli identificatori passati come argomenti alle funzioni ODBC non devono essere racchiusi tra virgolette). Se l'origine dati non supporta gli identificatori delimitati, viene restituito un valore blank.  
  
 Questa stringa di caratteri può essere utilizzata anche per citare argomenti della funzione di catalogo quando l'attributo di connessione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE.  
  
 Poiché il carattere virgoletta identificatore in SQL-92 è costituito dalle virgolette doppie ("), un driver conforme esclusivamente a SQL-92 restituirà sempre il carattere virgolette doppie.  
  
 SQL_INDEX_KEYWORDS (ODBC 3,0)  
 Maschera di SQLUINTEGER che enumera le parole chiave nell'istruzione CREATE INDEX supportate dal driver:  
  
 SQL_IK_NONE = nessuna delle parole chiave è supportata.  
  
 La parola chiave SQL_IK_ASC = ASC è supportata.  
  
 La parola chiave SQL_IK_DESC = DESC è supportata.  
  
 SQL_IK_ALL = tutte le parole chiave sono supportate.  
  
 Per verificare se l'istruzione CREATE INDEX è supportata, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_DLL_INDEX.  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3,0)  
 Maschera di SQLUINTEGER che enumera le viste nel INFORMATION_SCHEMA supportate dal driver. Le visualizzazioni in e il contenuto di INFORMATION_SCHEMA sono definite in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Per determinare quali visualizzazioni sono supportate, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_ISV_ASSERTIONS = identifica le asserzioni del catalogo di proprietà di un determinato utente. (Livello completo)  
  
 SQL_ISV_CHARACTER_SETS = identifica i set di caratteri del catalogo a cui è possibile accedere da un determinato utente. (Livello intermedio)  
  
 SQL_ISV_CHECK_CONSTRAINTS = identifica i vincoli CHECK di proprietà di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_COLLATIONS = identifica le regole di confronto dei caratteri per il catalogo a cui è possibile accedere da un determinato utente. (Livello completo)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = identifica le colonne per il catalogo che dipendono da domini definiti nel catalogo e sono di proprietà di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_COLUMN_PRIVILEGES = identifica i privilegi per le colonne di tabelle permanenti disponibili o concesse da un determinato utente. (Livello di transizione FIPS)  
  
 SQL_ISV_COLUMNS = identifica le colonne delle tabelle permanenti a cui è possibile accedere da un determinato utente. (Livello di transizione FIPS)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = Analogamente alla visualizzazione CONSTRAINT_TABLE_USAGE, le colonne vengono identificate per i vari vincoli di proprietà di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = identifica le tabelle utilizzate da vincoli (referenziali, univoche e ASSERTE) e sono di proprietà di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = identifica i vincoli di dominio (dei domini nel catalogo) a cui è possibile accedere da un determinato utente. (Livello intermedio)  
  
 SQL_ISV_DOMAINS = identifica i domini definiti in un catalogo a cui l'utente può accedere. (Livello intermedio)  
  
 SQL_ISV_KEY_COLUMN_USAGE = identifica le colonne definite nel catalogo vincolate come chiavi da un determinato utente. (Livello intermedio)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = identifica i vincoli referenziali di proprietà di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_SCHEMATA = identifica gli schemi di proprietà di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_SQL_LANGUAGES = identifica i livelli di conformità, le opzioni e i dialetti SQL supportati dall'implementazione SQL. (Livello intermedio)  
  
 SQL_ISV_TABLE_CONSTRAINTS = identifica i vincoli di tabella di proprietà di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_TABLE_PRIVILEGES = identifica i privilegi per le tabelle permanenti disponibili o concesse da un determinato utente. (Livello di transizione FIPS)  
  
 SQL_ISV_TABLES = identifica le tabelle permanenti definite in un catalogo a cui è possibile accedere da un determinato utente. (Livello di transizione FIPS)  
  
 SQL_ISV_TRANSLATIONS = identifica le traduzioni di caratteri per il catalogo a cui è possibile accedere da un determinato utente. (Livello completo)  
  
 SQL_ISV_USAGE_PRIVILEGES = identifica i privilegi di utilizzo per gli oggetti del catalogo disponibili o di proprietà di un determinato utente. (Livello di transizione FIPS)  
  
 SQL_ISV_VIEW_COLUMN_USAGE = identifica le colonne in cui dipendono le viste del catalogo di proprietà di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_VIEW_TABLE_USAGE = identifica le tabelle che dipendono dalle viste del catalogo di proprietà di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_VIEWS = identifica le tabelle visualizzate definite nel catalogo a cui è possibile accedere da un determinato utente. (Livello di transizione FIPS)  
  
 SQL_INSERT_STATEMENT (ODBC 3,0)  
 Maschera di SQLUINTEGER che indica il supporto per le istruzioni **Insert** :  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_INTEGRITY (ODBC 1,0)  
 Stringa di caratteri: "Y" se l'origine dati supporta la funzionalità di miglioramento dell'integrità. "N" in caso contrario.  
  
 Questo *InfoType* è stato rinominato per ODBC 3,0 da ODBC 2,0 *InfoType* SQL_ODBC_SQL_OPT_IEF.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1 (ODBC 3,0)  
 Maschera di SQLUINTEGER che descrive gli attributi di un cursore keyset supportati dal driver. Questa maschera di maschera contiene il primo subset di attributi. per il secondo subset, vedere SQL_KEYSET_CURSOR_ATTRIBUTES2.  
  
 Per determinare quali attributi sono supportati, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Per le descrizioni di queste maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e sostituire "cursore gestito da keyset" per "cursori dinamici" nelle descrizioni).  
  
 Un driver conforme al livello intermedio SQL-92 restituisce in genere le opzioni SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE supportate, poiché il driver supporta i cursori scorrevoli tramite l'istruzione SQL FETCH incorporata. Poiché questo non determina direttamente il supporto SQL sottostante, tuttavia, i cursori scorrevoli potrebbero non essere supportati, anche per un driver conforme al livello intermedio SQL-92.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2 (ODBC 3,0)  
 Maschera di SQLUINTEGER che descrive gli attributi di un cursore keyset supportati dal driver. Questa maschera di maschera contiene il secondo subset di attributi. per il primo subset, vedere SQL_KEYSET_CURSOR_ATTRIBUTES1.  
  
 Per determinare quali attributi sono supportati, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Per le descrizioni di queste maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e sostituire "cursore gestito da keyset" per "cursori dinamici" nelle descrizioni).  
  
 SQL_KEYWORDS (ODBC 2,0)  
 Stringa di caratteri contenente un elenco delimitato da virgole di tutte le parole chiave specifiche dell'origine dati. Questo elenco non contiene parole chiave specifiche di ODBC o parole chiave utilizzate dall'origine dati e da ODBC. Questo elenco rappresenta tutte le parole chiave riservate. le applicazioni interoperative non devono utilizzare queste parole nei nomi degli oggetti.  
  
 Per un elenco delle parole chiave ODBC, vedere [parole chiave riservate](../../../odbc/reference/appendixes/reserved-keywords.md) nell' [Appendice C: grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Il valore **#define** SQL_ODBC_KEYWORDS contiene un elenco delimitato da virgole di parole chiave ODBC.  
  
 Appendice C: Grammatica SQL  
  
 SQL_LIKE_ESCAPE_CLAUSE (ODBC 2,0)  
 Stringa di caratteri: "Y" se l'origine dati supporta un carattere di escape per il carattere di percentuale (%) e il carattere di sottolineatura (_) in un predicato **like** e il driver supportano la sintassi ODBC per la definizione di un carattere di escape del predicato **like** . "N" in caso contrario.  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS (ODBC 3,0)  
 Valore SQLUINTEGER che specifica il numero massimo di istruzioni attive simultanee in modalità asincrona che il driver è in grado di supportare in una determinata connessione. Se non esiste un limite specifico o il limite è sconosciuto, questo valore è zero.  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2,0)  
 Valore SQLUINTEGER che specifica la lunghezza massima (numero di caratteri esadecimali, escluso il prefisso letterale e il suffisso restituiti da **SQLGetTypeInfo**) di un valore letterale binario in un'istruzione SQL. Il valore letterale binario 0xFFAA, ad esempio, ha una lunghezza pari a 4. Se non è presente una lunghezza massima o la lunghezza è sconosciuta, questo valore viene impostato su zero.  
  
 SQL_MAX_CATALOG_NAME_LEN (ODBC 1,0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima del nome di un catalogo nell'origine dati. Se non è presente una lunghezza massima o la lunghezza è sconosciuta, questo valore viene impostato su zero.  
  
 Un driver conforme a FIPS Full Level restituirà almeno 128.  
  
 Questo *InfoType* è stato rinominato per ODBC 3,0 da ODBC 2,0 *InfoType* SQL_MAX_QUALIFIER_NAME_LEN.  
  
 SQL_MAX_CHAR_LITERAL_LEN (ODBC 2,0)  
 Valore SQLUINTEGER che specifica la lunghezza massima (numero di caratteri, escluso il prefisso letterale e il suffisso restituiti da **SQLGetTypeInfo**) di un valore letterale carattere in un'istruzione SQL. Se non è presente una lunghezza massima o la lunghezza è sconosciuta, questo valore viene impostato su zero.  
  
 SQL_MAX_COLUMN_NAME_LEN (ODBC 1,0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima del nome di una colonna nell'origine dati. Se non è presente una lunghezza massima o la lunghezza è sconosciuta, questo valore viene impostato su zero.  
  
 Un driver conforme allo standard FIPS restituisce almeno 18. Un driver conforme a FIPS Intermediate Level restituirà almeno 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY (ODBC 2,0)  
 Valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in una clausola **Group by** . Se non è presente alcun limite specificato o il limite è sconosciuto, questo valore viene impostato su zero.  
  
 Un driver conforme allo standard FIPS restituisce almeno 6. Un driver conforme a FIPS Intermediate Level restituirà almeno 15.  
  
 SQL_MAX_COLUMNS_IN_INDEX (ODBC 2,0)  
 Valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in un indice. Se non è presente alcun limite specificato o il limite è sconosciuto, questo valore viene impostato su zero.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY (ODBC 2,0)  
 Valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in una clausola **Order by** . Se non è presente alcun limite specificato o il limite è sconosciuto, questo valore viene impostato su zero.  
  
 Un driver conforme allo standard FIPS restituisce almeno 6. Un driver conforme a FIPS Intermediate Level restituirà almeno 15.  
  
 SQL_MAX_COLUMNS_IN_SELECT (ODBC 2,0)  
 Valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in un elenco di selezione. Se non è presente alcun limite specificato o il limite è sconosciuto, questo valore viene impostato su zero.  
  
 Un driver con conformità a livello di voce FIPS restituirà almeno 100. Un driver conforme a FIPS Intermediate Level restituirà almeno 250.  
  
 SQL_MAX_COLUMNS_IN_TABLE (ODBC 2,0)  
 Valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in una tabella. Se non è presente alcun limite specificato o il limite è sconosciuto, questo valore viene impostato su zero.  
  
 Un driver con conformità a livello di voce FIPS restituirà almeno 100. Un driver conforme a FIPS Intermediate Level restituirà almeno 250.  
  
 SQL_MAX_CONCURRENT_ACTIVITIES (ODBC 1,0)  
 Valore SQLUSMALLINT che specifica il numero massimo di istruzioni attive che il driver è in grado di supportare per una connessione. Un'istruzione è definita come attiva se presenta risultati in sospeso, con il termine "risultati" che indica le righe di un'operazione **Select** o le righe interessate da un'operazione di **inserimento**, **aggiornamento**o **eliminazione** , ad esempio un conteggio di righe, oppure se si trova in uno stato di NEED_DATA. Questo valore può indicare una limitazione imposta dal driver o dall'origine dati. Se non è presente alcun limite specificato o il limite è sconosciuto, questo valore viene impostato su zero.  
  
 Questo *InfoType* è stato rinominato per ODBC 3,0 da ODBC 2,0 *InfoType* SQL_ACTIVE_STATEMENTS.  
  
 SQL_MAX_CURSOR_NAME_LEN (ODBC 1,0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima del nome di un cursore nell'origine dati. Se non è presente una lunghezza massima o la lunghezza è sconosciuta, questo valore viene impostato su zero.  
  
 Un driver conforme allo standard FIPS restituisce almeno 18. Un driver conforme a FIPS Intermediate Level restituirà almeno 128.  
  
 SQL_MAX_DRIVER_CONNECTIONS (ODBC 1,0)  
 Valore SQLUSMALLINT che specifica il numero massimo di connessioni attive che il driver è in grado di supportare per un ambiente. Questo valore può indicare una limitazione imposta dal driver o dall'origine dati. Se non è presente alcun limite specificato o il limite è sconosciuto, questo valore viene impostato su zero.  
  
 Questo *InfoType* è stato rinominato per ODBC 3,0 da ODBC 2,0 *InfoType* SQL_ACTIVE_CONNECTIONS.  
  
 SQL_MAX_IDENTIFIER_LEN (ODBC 3,0)  
 SQLUSMALLINT che indica la dimensione massima in caratteri supportata dall'origine dati per i nomi definiti dall'utente.  
  
 Un driver conforme allo standard FIPS restituisce almeno 18. Un driver conforme a FIPS Intermediate Level restituirà almeno 128.  
  
 SQL_MAX_INDEX_SIZE (ODBC 2,0)  
 Valore SQLUINTEGER che specifica il numero massimo di byte consentiti nei campi combinati di un indice. Se non è presente alcun limite specificato o il limite è sconosciuto, questo valore viene impostato su zero.  
  
 SQL_MAX_PROCEDURE_NAME_LEN (ODBC 1,0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima del nome di una stored procedure nell'origine dati. Se non è presente una lunghezza massima o la lunghezza è sconosciuta, questo valore viene impostato su zero.  
  
 SQL_MAX_ROW_SIZE (ODBC 2,0)  
 Valore SQLUINTEGER che specifica la lunghezza massima di una singola riga in una tabella. Se non è presente alcun limite specificato o il limite è sconosciuto, questo valore viene impostato su zero.  
  
 Un driver con conformità a livello di voce FIPS restituirà almeno 2.000. Un driver conforme a FIPS Intermediate Level restituirà almeno 8.000.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG (ODBC 3,0)  
 Stringa di caratteri: "Y" se la dimensione massima della riga restituita per il tipo di informazioni SQL_MAX_ROW_SIZE include la lunghezza di tutte le colonne SQL_LONGVARCHAR e SQL_LONGVARBINARY nella riga; "N" in caso contrario.  
  
 SQL_MAX_SCHEMA_NAME_LEN (ODBC 1,0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima di un nome di schema nell'origine dati. Se non è presente una lunghezza massima o la lunghezza è sconosciuta, questo valore viene impostato su zero.  
  
 Un driver conforme allo standard FIPS restituisce almeno 18. Un driver conforme a FIPS Intermediate Level restituirà almeno 128.  
  
 Questo *InfoType* è stato rinominato per ODBC 3,0 da ODBC 2,0 *InfoType* SQL_MAX_OWNER_NAME_LEN.  
  
 SQL_MAX_STATEMENT_LEN (ODBC 2,0)  
 Valore SQLUINTEGER che specifica la lunghezza massima (numero di caratteri, inclusi gli spazi vuoti) di un'istruzione SQL. Se non è presente una lunghezza massima o la lunghezza è sconosciuta, questo valore viene impostato su zero.  
  
 SQL_MAX_TABLE_NAME_LEN (ODBC 1,0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima del nome di una tabella nell'origine dati. Se non è presente una lunghezza massima o la lunghezza è sconosciuta, questo valore viene impostato su zero.  
  
 Un driver conforme allo standard FIPS restituisce almeno 18. Un driver conforme a FIPS Intermediate Level restituirà almeno 128.  
  
 SQL_MAX_TABLES_IN_SELECT (ODBC 2,0)  
 Valore SQLUSMALLINT che specifica il numero massimo di tabelle consentite nella clausola **from** di un'istruzione **SELECT** . Se non è presente alcun limite specificato o il limite è sconosciuto, questo valore viene impostato su zero.  
  
 Un driver con conformità a livello di voce FIPS restituirà almeno 15. Un driver conforme a FIPS Intermediate Level restituirà almeno 50.  
  
 SQL_MAX_USER_NAME_LEN (ODBC 2,0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima di un nome utente nell'origine dati. Se non è presente una lunghezza massima o la lunghezza è sconosciuta, questo valore viene impostato su zero.  
  
 SQL_MULT_RESULT_SETS (ODBC 1,0)  
 Stringa di caratteri: "Y" se l'origine dati supporta più set di risultati, ovvero "N" in caso contrario.  
  
 Per ulteriori informazioni su più set di risultati, vedere [più risultati](../../../odbc/reference/develop-app/multiple-results.md).  
  
 SQL_MULTIPLE_ACTIVE_TXN (ODBC 1,0)  
 Stringa di caratteri: "Y" Se il driver supporta più transazioni attive contemporaneamente, "N" se può essere attiva una sola transazione in qualsiasi momento.  
  
 Le informazioni restituite per questo tipo di informazioni non si applicano in caso di transazioni distribuite.  
  
 SQL_NEED_LONG_DATA_LEN (ODBC 2,0)  
 Stringa di caratteri: "Y" se per l'origine dati è necessaria la lunghezza di un valore di dati Long (il tipo di dati è SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo di dati Long Data Source-Specific) prima che tale valore venga inviato all'origine dati, in caso contrario. Per altre informazioni, vedere [funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 SQL_NON_NULLABLE_COLUMNS (ODBC 1,0)  
 Valore SQLUSMALLINT che specifica se l'origine dati supporta NOT NULL nelle colonne:  
  
 SQL_NNC_NULL = tutte le colonne devono ammettere i valori null.  
  
 SQL_NNC_NON_NULL = le colonne non ammettono valori null. L'origine dati supporta il vincolo di colonna **not null** nelle istruzioni **Create Table** .  
  
 Un driver conforme a SQL-92 Entry Level restituirà SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION (ODBC 2,0)  
 Valore SQLUSMALLINT che specifica dove vengono ordinati i valori NULL in un set di risultati:  
  
 SQL_NC_END = i valori NULL vengono ordinati alla fine del set di risultati, indipendentemente dalle parole chiave ASC o DESC.  
  
 SQL_NC_HIGH = i valori NULL vengono ordinati in corrispondenza dell'estremità superiore del set di risultati, a seconda delle parole chiave ASC o DESC.  
  
 SQL_NC_LOW = i valori NULL vengono ordinati in corrispondenza della parte inferiore del set di risultati, a seconda delle parole chiave ASC o DESC.  
  
 SQL_NC_START = i valori NULL vengono ordinati all'inizio del set di risultati, indipendentemente dalle parole chiave ASC o DESC.  
  
 SQL_NUMERIC_FUNCTIONS (ODBC 1,0)  
 Nota: il tipo di informazioni è stato introdotto in ODBC 1,0; ogni maschera di maschera è contrassegnata con la versione in cui è stata introdotta.  
  
 Maschera di SQLUINTEGER che enumera le funzioni numeriche scalari supportate dal driver e dall'origine dati associata.  
  
 Per determinare quali funzioni numeriche sono supportate sono utilizzate le maschere di maschera seguenti:  
  
 SQL_FN_NUM_ABS (ODBC 1.0) SQL_FN_NUM_ACOS (ODBC 1.0) SQL_FN_NUM_ASIN (ODBC 1.0) SQL_FN_NUM_ATAN (ODBC 1.0) SQL_FN_NUM_ATAN2 (ODBC 1.0) SQL_FN_NUM_CEILING (ODBC 1.0) SQL_FN_NUM_COS (ODBC 1.0) SQL_FN_NUM_COT (ODBC 1.0) SQL_FN_NUM_DEGREES (ODBC 2.0) SQL_ FN_NUM_EXP (ODBC 1.0) SQL_FN_NUM_FLOOR (ODBC 1.0) SQL_FN_NUM_LOG (ODBC 1.0) SQL_FN_NUM_LOG10 (ODBC 2.0) SQL_FN_NUM_MOD (ODBC 1.0) SQL_FN_NUM_PI (ODBC 1.0) SQL_FN_NUM_POWER (ODBC 2.0) SQL_FN_NUM_RADIANS (ODBC 2.0) SQL_FN_NUM_RAND (ODBC 1.0) SQL_FN_ NUM_ROUND (ODBC 2.0) SQL_FN_NUM_SIGN (ODBC 1.0) SQL_FN_NUM_SIN (ODBC 1.0) SQL_FN_NUM_SQRT (ODBC 1.0) SQL_FN_NUM_TAN (ODBC 1.0) SQL_FN_NUM_TRUNCATE (ODBC 2,0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE (ODBC 3,0)  
 Valore SQLUINTEGER che indica il livello dell'interfaccia ODBC 3 *. x* con cui è conforme il driver.  
  
 SQL_OIC_CORE: il livello minimo che tutti i driver ODBC dovranno rispettare. Questo livello include elementi di interfaccia di base quali funzioni di connessione, funzioni per la preparazione e l'esecuzione di un'istruzione SQL, funzioni di metadati del set di risultati di base, funzioni del catalogo di base e così via.  
  
 SQL_OIC_LEVEL1: un livello che include le funzionalità principali del livello di conformità standard, oltre a cursori scorrevoli, segnalibri, aggiornamenti posizionati ed eliminazioni e così via.  
  
 SQL_OIC_LEVEL2: un livello che include la funzionalità del livello di conformità standard di livello 1, oltre A funzionalità avanzate quali i cursori sensibili; aggiornare, eliminare e aggiornare tramite segnalibri; supporto stored procedure; funzioni di catalogo per chiavi primarie ed esterne. supporto per più cataloghi; E così via.  
  
 Per altre informazioni, vedere [livelli di conformità dell'interfaccia](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 SQL_ODBC_VER (ODBC 1,0)  
 Stringa di caratteri con la versione di ODBC a cui è conforme la gestione driver. Il formato della versione è # #. # #. 0000, dove le prime due cifre sono la versione principale e le due cifre successive sono la versione secondaria. Questa operazione è implementata solo in Gestione driver.  
  
 SQL_OJ_CAPABILITIES (ODBC 2,01)  
 Maschera di SQLUINTEGER che enumera i tipi di outer join supportati dal driver e dall'origine dati. Per determinare quali tipi sono supportati, vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_OJ_LEFT = left outer join sono supportati.  
  
 SQL_OJ_RIGHT = right outer join sono supportati.  
  
 SQL_OJ_FULL = full outer join sono supportati.  
  
 SQL_OJ_NESTED = outer join annidati sono supportati.  
  
 SQL_OJ_NOT_ORDERED = i nomi di colonna nella clausola ON del outer join non devono essere nello stesso ordine dei rispettivi nomi di tabella nella clausola **outer join** .  
  
 SQL_OJ_INNER = la tabella interna, ovvero la tabella a destra in una left outer join o la tabella a sinistra in un right outer join, può essere usata anche in un inner join. Questa condizione non si applica ai join full outer, che non dispongono di una tabella interna.  
  
 SQL_OJ_ALL_COMPARISON_OPS = l'operatore di confronto nella clausola ON può essere uno qualsiasi degli operatori di confronto ODBC. Se questo bit non è impostato, è possibile utilizzare solo l'operatore di confronto uguale a (=) negli outer join.  
  
 Se nessuna di queste opzioni viene restituita come supportata, non è supportata alcuna clausola outer join.  
  
 Per informazioni sul supporto degli operatori di join relazionale in un'istruzione SELECT, in base a quanto definito da SQL-92, vedere SQL_SQL92_RELATIONAL_JOIN_OPERATORS.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT (ODBC 2,0)  
 Stringa di caratteri: "Y" se le colonne nella clausola **Order by** devono essere incluse nell'elenco di selezione; in caso contrario, "N".  
  
 SQL_PARAM_ARRAY_ROW_COUNTS (ODBC 3,0)  
 SQLUINTEGER che enumera le proprietà del driver relative alla disponibilità dei conteggi delle righe in un'esecuzione con parametri. Presenta i valori seguenti:  
  
 SQL_PARC_BATCH = i conteggi delle singole righe sono disponibili per ogni set di parametri. Concettualmente equivale al driver che genera un batch di istruzioni SQL, una per ogni set di parametri nella matrice. Le informazioni estese sugli errori possono essere recuperate usando il SQL_PARAM_STATUS_PTR campo del descrittore.  
  
 SQL_PARC_NO_BATCH = è disponibile un solo numero di righe, ovvero il numero di righe cumulativo risultante dall'esecuzione dell'istruzione per l'intera matrice di parametri. Concettualmente equivale a trattare l'istruzione insieme alla matrice di parametri completa come un'unità atomica. Gli errori vengono gestiti come se fosse stata eseguita un'istruzione.  
  
 SQL_PARAM_ARRAY_SELECTS (ODBC 3,0)  
 SQLUINTEGER che enumera le proprietà del driver relative alla disponibilità dei set di risultati in un'esecuzione con parametri. Presenta i valori seguenti:  
  
 SQL_PAS_BATCH = è disponibile un set di risultati per ogni set di parametri. Concettualmente equivale al driver che genera un batch di istruzioni SQL, una per ogni set di parametri nella matrice.  
  
 SQL_PAS_NO_BATCH = è disponibile un solo set di risultati, che rappresenta il set di risultati cumulativo risultante dall'esecuzione dell'istruzione per la matrice di parametri completa. Concettualmente equivale a trattare l'istruzione insieme alla matrice di parametri completa come un'unità atomica.  
  
 SQL_PAS_NO_SELECT = un driver non consente l'esecuzione di un'istruzione che genera un set di risultati con una matrice di parametri.  
  
 SQL_PROCEDURE_TERM (ODBC 1,0)  
 Stringa di caratteri con il nome del fornitore dell'origine dati per una procedura. ad esempio, "database procedure", "stored procedure", "procedura", "pacchetto" o "query archiviata".  
  
 SQL_PROCEDURES (ODBC 1,0)  
 Stringa di caratteri: "Y" se l'origine dati supporta le procedure e il driver supporta la sintassi di chiamata della procedura ODBC; "N" in caso contrario.  
  
 SQL_POS_OPERATIONS (ODBC 2,0)  
 Maschera di tipo SQLINTEGER che enumera le operazioni di supporto in **SQLSetPos**.  
  
 Le seguenti maschere di maschera vengono utilizzate insieme al flag per determinare quali opzioni sono supportate.  
  
 SQL_POS_POSITION (ODBC 2,0) SQL_POS_REFRESH (ODBC 2,0) SQL_POS_UPDATE (ODBC 2,0) SQL_POS_DELETE (ODBC 2,0) SQL_POS_ADD (ODBC 2,0)  
  
 SQL_QUOTED_IDENTIFIER_CASE (ODBC 2,0)  
 Un valore SQLUSMALLINT come segue:  
  
 SQL_IC_UPPER = gli identificatori delimitati in SQL non fanno distinzione tra maiuscole e minuscole e vengono archiviati in maiuscolo nel catalogo di sistema.  
  
 SQL_IC_LOWER = gli identificatori tra virgolette in SQL non fanno distinzione tra maiuscole e minuscole e vengono archiviati in minuscolo nel catalogo di sistema.  
  
 SQL_IC_SENSITIVE = gli identificatori tra virgolette in SQL fanno distinzione tra maiuscole e minuscole e vengono archiviati in maiuscolo e minuscolo nel catalogo di sistema. In un database conforme a SQL-92, gli identificatori delimitati hanno sempre la distinzione tra maiuscole e minuscole.  
  
 SQL_IC_MIXED = gli identificatori tra virgolette in SQL non fanno distinzione tra maiuscole e minuscole e vengono archiviati in lettere maiuscole e minuscole nel catalogo di sistema.  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre SQL_IC_SENSITIVE.  
  
 SQL_ROW_UPDATES (ODBC 1,0)  
 Stringa di caratteri: "Y" Se un cursore gestito da keyset o misto mantiene le versioni di riga o i valori per tutte le righe recuperate e pertanto può rilevare eventuali aggiornamenti apportati a una riga da qualsiasi utente dall'ultimo recupero della riga. Questo vale solo per gli aggiornamenti, non per gli inserimenti o le eliminazioni. Il driver può restituire il flag di SQL_ROW_UPDATED alla matrice di stato della riga quando viene chiamato **SQLFetchScroll** . In caso contrario, "N".  
  
 SQL_SCHEMA_TERM (ODBC 1,0)  
 Stringa di caratteri con il nome del fornitore dell'origine dati per uno schema. ad esempio, "Owner", "Authorization ID" o "schema".  
  
 La stringa di caratteri può essere restituita in lettere maiuscole, minuscole o miste.  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre "schema".  
  
 Questo *InfoType* è stato rinominato per ODBC 3,0 da ODBC 2,0 *InfoType* SQL_OWNER_TERM.  
  
 SQL_SCHEMA_USAGE (ODBC 2,0)  
 Maschera di SQLUINTEGER che enumera le istruzioni in cui è possibile utilizzare gli schemi:  
  
 SQL_SU_DML_STATEMENTS = gli schemi sono supportati in tutte le istruzioni del linguaggio di manipolazione dei dati: **selezionare**, **inserire**, **aggiornare**, **eliminare**e, se supportato, **selezionare per** le istruzioni Update e Delete posizionate.  
  
 SQL_SU_PROCEDURE_INVOCATION = gli schemi sono supportati nell'istruzione di chiamata della procedura ODBC.  
  
 SQL_SU_TABLE_DEFINITION = gli schemi sono supportati in tutte le istruzioni di definizione della tabella: **Create Table**, **Create View**, **ALTER TABLE**, **Drop Table**e **Drop View**.  
  
 SQL_SU_INDEX_DEFINITION = gli schemi sono supportati in tutte le istruzioni per la definizione dell'indice: **create index** e **Drop index**.  
  
 SQL_SU_PRIVILEGE_DEFINITION = gli schemi sono supportati in tutte le istruzioni di definizione dei privilegi: **Grant** e **Revoke**.  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre le opzioni SQL_SU_DML_STATEMENTS, SQL_SU_TABLE_DEFINITION e SQL_SU_PRIVILEGE_DEFINITION, come supportato.  
  
 Questo *InfoType* è stato rinominato per ODBC 3,0 da ODBC 2,0 *InfoType* SQL_OWNER_USAGE.  
  
 SQL_SCROLL_OPTIONS (ODBC 1,0)  
 Nota: il tipo di informazioni è stato introdotto in ODBC 1,0; ogni maschera di maschera è contrassegnata con la versione in cui è stata introdotta.  
  
 Maschera di SQLUINTEGER che enumera le opzioni di scorrimento supportate per i cursori scorrevoli.  
  
 Per determinare quali opzioni sono supportate, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_SO_FORWARD_ONLY = il cursore scorre in futuro. (ODBC 1,0)  
  
 SQL_SO_STATIC = i dati nel set di risultati sono statici. (ODBC 2,0)  
  
 SQL_SO_KEYSET_DRIVEN = il driver Salva e utilizza le chiavi per ogni riga del set di risultati. (ODBC 1,0)  
  
 SQL_SO_DYNAMIC = il driver mantiene le chiavi per ogni riga del set di righe (le dimensioni del keyset sono le stesse delle dimensioni del set di righe). (ODBC 1,0)  
  
 SQL_SO_MIXED = il driver mantiene le chiavi per ogni riga del keyset e le dimensioni del keyset sono maggiori delle dimensioni del set di righe. Il cursore è gestito da keyset all'interno del keyset e dinamico all'esterno del keyset. (ODBC 1,0)  
  
 Per informazioni sui cursori scorrevoli, vedere [cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 SQL_SEARCH_PATTERN_ESCAPE (ODBC 1,0)  
 Stringa di caratteri che specifica il supporto supportato dal driver come carattere di escape che consente di utilizzare i caratteri di sottolineatura (_) del criterio di ricerca e il segno di percentuale (%) come caratteri validi nei criteri di ricerca. Questo carattere di escape si applica solo agli argomenti della funzione di catalogo che supportano le stringhe di ricerca. Se questa stringa è vuota, il driver non supporta un carattere di escape del criterio di ricerca.  
  
 Poiché questo tipo di informazioni non indica il supporto generale del carattere di escape nel predicato **like** , SQL-92 non include i requisiti per questa stringa di caratteri.  
  
 Questo *InfoType* è limitato alle funzioni di catalogo. Per una descrizione dell'uso del carattere di escape nelle stringhe dei criteri di ricerca, vedere [argomenti del valore del modello](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
 SQL_SERVER_NAME (ODBC 1,0)  
 Una stringa di caratteri con il nome del server specifico dell'origine dati effettivo; utile quando si utilizza un nome di origine dati durante **SQLConnect**, **SQLDriverConnect**e **SQLBrowseConnect**.  
  
 SQL_SPECIAL_CHARACTERS (ODBC 2,0)  
 Stringa di caratteri che contiene tutti i caratteri speciali, ovvero tutti i caratteri eccetto dalla a alla z, dalla A alla Z, da 0 a 9 e dal carattere di sottolineatura, che possono essere utilizzati in un nome di identificatore, ad esempio un nome di tabella, un nome di colonna o un nome di indice, nell'origine dati. Ad esempio, "# $ ^". Se un identificatore contiene uno o più di questi caratteri, l'identificatore deve essere un identificatore delimitato.  
  
 SQL_SQL_CONFORMANCE (ODBC 3,0)  
 Valore SQLUINTEGER che indica il livello di SQL-92 supportato dal driver:  
  
 SQL_SC_SQL92_ENTRY = conformità SQL-92 a livello di ingresso.  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = FIPS 127-2 livello di transizione conforme.  
  
 SQL_SC_SQL92_FULL = conformità SQL-92 a livello completo.  
  
 SQL_SC_ SQL92_INTERMEDIATE = conformità SQL-92 a livello intermedio.  
  
 SQL_SQL92_DATETIME_FUNCTIONS (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le funzioni scalari DateTime supportate dal driver e dall'origine dati associata, in base a quanto definito in SQL-92.  
  
 Per determinare quali funzioni DateTime sono supportate sono utilizzate le maschere di maschera seguenti:  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le regole supportate per una chiave esterna in un'istruzione **Delete** , come definito in SQL-92.  
  
 Per determinare le clausole supportate dall'origine dei dati, vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 Un driver con livello di transizione FIPS può restituire sempre tutte queste opzioni come supportate.  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le regole supportate per una chiave esterna in un'istruzione **Update** , come definito in SQL-92.  
  
 Per determinare le clausole supportate dall'origine dei dati, vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 Un driver conforme a SQL-92 restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_SQL92_GRANT (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole supportate nell'istruzione **Grant** , come definito in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Per determinare le clausole supportate dall'origine dei dati, vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_SG_DELETE_TABLE (livello di ingresso) SQL_SG_INSERT_COLUMN (livello intermedio) SQL_SG_INSERT_TABLE (livello di ingresso) SQL_SG_REFERENCES_TABLE (livello di ingresso) SQL_SG_REFERENCES_COLUMN (livello di ingresso) SQL_SG_SELECT_TABLE (livello di ingresso) SQL_SG_UPDATE_COLUMN ( Livello di ingresso SQL_SG_UPDATE_TABLE (livello di ingresso) SQL_SG_USAGE_ON_DOMAIN (livello di transizione FIPS) SQL_SG_USAGE_ON_CHARACTER_SET (livello di transizione FIPS) SQL_SG_USAGE_ON_COLLATION (livello di transizione FIPS) SQL_SG_USAGE_ON_TRANSLATION (FIPS Livello di transizione) SQL_SG_WITH_GRANT_OPTION (livello di ingresso)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le funzioni scalari del valore numerico supportate dal driver e dall'origine dati associata, in base a quanto definito in SQL-92.  
  
 Per determinare quali funzioni numeriche sono supportate sono utilizzate le maschere di maschera seguenti:  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera i predicati supportati in un'istruzione **Select** , come definito in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Per determinare quali opzioni sono supportate dall'origine dati, vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_SP_BETWEEN (livello di ingresso) SQL_SP_COMPARISON (livello di ingresso) SQL_SP_EXISTS (livello di ingresso) SQL_SP_IN (livello di ingresso) SQL_SP_ISNOTNULL (livello di ingresso) SQL_SP_ISNULL (livello di ingresso) SQL_SP_LIKE (livello di ingresso) SQL_SP_MATCH_FULL (livello completo) SQL_SP_MATCH_PARTIAL (Livello completo) SQL_SP_MATCH_UNIQUE_FULL (livello completo) SQL_SP_MATCH_UNIQUE_PARTIAL (livello completo) SQL_SP_OVERLAPS (livello di transizione FIPS) SQL_SP_QUANTIFIED_COMPARISON (livello di ingresso) SQL_SP_UNIQUE (livello di ingresso)  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera gli operatori di join relazionale supportati in un'istruzione **Select** , come definito in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Per determinare quali opzioni sono supportate dall'origine dati, vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_SRJO_CORRESPONDING_CLAUSE (livello intermedio) SQL_SRJO_CROSS_JOIN (livello completo) SQL_SRJO_EXCEPT_JOIN (livello intermedio) SQL_SRJO_FULL_OUTER_JOIN (livello intermedio) SQL_SRJO_INNER_JOIN (livello di transizione FIPS) SQL_SRJO_INTERSECT_JOIN (Livello intermedio) SQL_SRJO_LEFT_OUTER_JOIN (livello di transizione FIPS) SQL_SRJO_NATURAL_JOIN (livello di transizione FIPS) SQL_SRJO_RIGHT_OUTER_JOIN (livello di transizione FIPS) SQL_SRJO_UNION_JOIN (livello completo)  
  
 SQL_SRJO_INNER_JOIN indica il supporto per la sintassi **inner join** , non per la funzionalità inner join. Il supporto per la sintassi **inner join** è la transizione FIPS, mentre il supporto per la funzionalità inner join è **entry**.  
  
 SQL_SQL92_REVOKE (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole supportate nell'istruzione **Revoke** , come definito in SQL-92, supportato dall'origine dati.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Per determinare le clausole supportate dall'origine dei dati, vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_SR_CASCADE (livello di transizione FIPS) SQL_SR_DELETE_TABLE (livello di ingresso) SQL_SR_GRANT_OPTION_FOR (livello intermedio) SQL_SR_INSERT_COLUMN (livello intermedio) SQL_SR_INSERT_TABLE (livello di ingresso) SQL_SR_REFERENCES_COLUMN (livello di ingresso) SQL_SR_ REFERENCES_TABLE (livello di ingresso) SQL_SR_RESTRICT (livello di transizione FIPS) SQL_SR_SELECT_TABLE (livello di ingresso) SQL_SR_UPDATE_COLUMN (livello di ingresso) SQL_SR_UPDATE_TABLE (livello di ingresso) SQL_SR_USAGE_ON_DOMAIN (livello di transizione FIPS) SQL_SR_USAGE_ON_ CHARACTER_SET (livello di transizione FIPS) SQL_SR_USAGE_ON_COLLATION (livello di transizione FIPS) SQL_SR_USAGE_ON_TRANSLATION (livello di transizione FIPS)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le espressioni del costruttore di valori di riga supportate in un'istruzione **Select** , come definito in SQL-92. Per determinare quali opzioni sono supportate dall'origine dati, vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le funzioni scalari di stringa supportate dal driver e dall'origine dati associata, in base a quanto definito in SQL-92.  
  
 Per determinare quali funzioni stringa sono supportate sono utilizzate le maschere di maschera seguenti:  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le espressioni di valore supportate, come definito in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Per determinare quali opzioni sono supportate dall'origine dati, vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_SVE_CASE (livello intermedio) SQL_SVE_CAST (livello di transizione FIPS) SQL_SVE_COALESCE (livello intermedio) SQL_SVE_NULLIF (livello intermedio)  
  
 SQL_STANDARD_CLI_CONFORMANCE (ODBC 3,0)  
 Maschera di SQLUINTEGER che enumera lo standard dell'interfaccia della riga di comando o gli standard a cui è conforme il driver. Per determinare i livelli di conformità del driver vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_SCC_XOPEN_CLI_VERSION1: il driver è conforme all'interfaccia della riga di comando del gruppo aperto versione 1.  
  
 SQL_SCC_ISO92_CLI: il driver è conforme all'interfaccia della riga di comando ISO 92.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1 (ODBC 3,0)  
 Maschera di SQLUINTEGER che descrive gli attributi di un cursore statico supportati dal driver. Questa maschera di maschera contiene il primo subset di attributi. per il secondo subset, vedere SQL_STATIC_CURSOR_ATTRIBUTES2.  
  
 Per determinare quali attributi sono supportati, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Per le descrizioni di queste maschere di maschera, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e sostituire "static Cursor" per "Dynamic Cursor" nelle descrizioni).  
  
 Un driver conforme al livello intermedio SQL-92 restituisce in genere le opzioni SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE supportate, poiché il driver supporta i cursori scorrevoli tramite l'istruzione SQL FETCH incorporata. Poiché questo non determina direttamente il supporto SQL sottostante, tuttavia, i cursori scorrevoli potrebbero non essere supportati, anche per un driver conforme al livello intermedio SQL-92.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2 (ODBC 3,0)  
 Maschera di SQLUINTEGER che descrive gli attributi di un cursore statico supportati dal driver. Questa maschera di maschera contiene il secondo subset di attributi. per il primo subset, vedere SQL_STATIC_CURSOR_ATTRIBUTES1.  
  
 Per determinare quali attributi sono supportati, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Per le descrizioni di queste maschere di maschera, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (e sostituire "static Cursor" per "Dynamic Cursor" nelle descrizioni).  
  
 SQL_STRING_FUNCTIONS (ODBC 1,0)  
 Nota: il tipo di informazioni è stato introdotto in ODBC 1,0; ogni maschera di maschera è contrassegnata con la versione in cui è stata introdotta.  
  
 Maschera di SQLUINTEGER che enumera le funzioni di stringa scalari supportate dal driver e dall'origine dati associata.  
  
 Per determinare quali funzioni stringa sono supportate sono utilizzate le maschere di maschera seguenti:  
  
 SQL_FN_STR_ASCII (ODBC 1.0) SQL_FN_STR_BIT_LENGTH (ODBC 3.0) SQL_FN_STR_CHAR (ODBC 1.0) SQL_FN_STR_CHAR_LENGTH (ODBC 3.0) SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0) SQL_FN_STR_CONCAT (ODBC 1.0) SQL_FN_STR_DIFFERENCE (ODBC 2.0) SQL_FN_STR_INSERT (ODBC 1.0) SQL_FN_STR_LCASE (ODBC 1.0) SQL_FN_STR_LEFT (ODBC 1.0) SQL_FN_STR_LENGTH (ODBC 1.0) SQL_FN_STR_LOCATE (ODBC 1,0) SQL_FN_STR_LTRIM (ODBC 1,0) SQL_FN_STR_OCTET_LENGTH (ODBC 3,0) SQL_FN_STR_POSITION (ODBC 3.0) SQL_FN_STR_REPEAT (ODBC 1.0) SQL_FN_ STR_REPLACE (ODBC 1.0) SQL_FN_STR_RIGHT (ODBC 1.0) SQL_FN_STR_RTRIM (ODBC 1.0) SQL_FN_STR_SOUNDEX (ODBC 2.0) SQL_FN_STR_SPACE (ODBC 2.0) SQL_FN_STR_SUBSTRING (ODBC 1.0) SQL_FN_STR_UCASE (ODBC 1,0)  
  
 Se un'applicazione può chiamare la funzione scalare **locate** con gli argomenti *string_exp1*, *string_exp2*e *Start* , il driver restituisce la maschera di SQL_FN_STR_LOCATE. Se un'applicazione può chiamare la funzione scalare LOCAte solo con gli argomenti *string_exp1* e *string_exp2* , il driver restituisce la maschera di SQL_FN_STR_LOCATE_2. I driver che supportano completamente la funzione scalare **locate** restituiscono entrambe le maschere di maschera.  
  
 Per ulteriori informazioni, vedere [funzioni di stringa](../../../odbc/reference/appendixes/string-functions.md) nell'appendice E, "funzioni scalari".  
  
 SQL_SUBQUERIES (ODBC 2,0)  
 Maschera di SQLUINTEGER che enumera i predicati che supportano sottoquery:  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 La maschera di maschera di SQL_SQ_CORRELATED_SUBQUERIES indica che tutti i predicati che supportano sottoquery supportano sottoquery correlate.  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre una maschera di bit in cui tutti questi bit sono impostati.  
  
 SQL_SYSTEM_FUNCTIONS (ODBC 1,0)  
 Maschera di SQLUINTEGER che enumera le funzioni di sistema scalari supportate dal driver e dall'origine dati associata.  
  
 Per determinare quali funzioni di sistema sono supportate, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM (ODBC 1,0)  
 Stringa di caratteri con il nome del fornitore dell'origine dati per una tabella. ad esempio, "Table" o "file".  
  
 Questa stringa di caratteri può essere in lettere maiuscole, minuscole o miste.  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre "Table".  
  
 SQL_TIMEDATE_ADD_INTERVALS (ODBC 2,0)  
 Maschera di SQLUINTEGER che enumera gli intervalli di timestamp supportati dal driver e dall'origine dati associata per la funzione scalare TIMESTAMPADD.  
  
 Per determinare gli intervalli supportati, vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Un driver con livello di transizione FIPS, restituirà sempre una maschera di bit in cui tutti questi bit sono impostati.  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2,0)  
 Maschera di SQLUINTEGER che enumera gli intervalli di timestamp supportati dal driver e dall'origine dati associata per la funzione scalare TIMESTAMPDIFF.  
  
 Per determinare gli intervalli supportati, vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Un driver con livello di transizione FIPS, restituirà sempre una maschera di bit in cui tutti questi bit sono impostati.  
  
 SQL_TIMEDATE_FUNCTIONS (ODBC 1,0)  
 Nota: il tipo di informazioni è stato introdotto in ODBC 1,0; ogni maschera di maschera è contrassegnata con la versione in cui è stata introdotta.  
  
 Maschera di SQLUINTEGER che enumera le funzioni di data e ora scalari supportate dal driver e dall'origine dati associata.  
  
 Per determinare quali funzioni di data e ora sono supportate, vengono utilizzate le maschere di comando seguenti:  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0) SQL_FN_TD_CURRENT_TIME (ODBC 3.0) SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) SQL_FN_TD_CURDATE (ODBC 1.0) SQL_FN_TD_CURTIME (ODBC 1,0) SQL_FN_TD_DAYNAME (ODBC 2.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0) SQL_FN_TD_DAYOFWEEK ( ODBC 1.0) SQL_FN_TD_DAYOFYEAR (ODBC 1,0) SQL_FN_TD_EXTRACT (ODBC 3.0) SQL_FN_TD_HOUR (ODBC 1.0) SQL_FN_TD_MINUTE (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTHNAME (ODBC 2.0) SQL_FN_TD_NOW (ODBC 1.0) SQL_FN_TD_QUARTER (ODBC 1.0) SQL_FN_TD_ SECONDO (ODBC 1.0) SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) SQL_FN_TD_WEEK (ODBC 1.0) SQL_FN_TD_YEAR (ODBC 1,0)  
  
 SQL_TXN_CAPABLE (ODBC 1,0)  
 Nota: il tipo di informazioni è stato introdotto in ODBC 1,0; ogni valore restituito viene identificato con la versione in cui è stata introdotta.  
  
 Valore SQLUSMALLINT che descrive il supporto delle transazioni nel driver o nell'origine dati:  
  
 SQL_TC_NONE = le transazioni non sono supportate. (ODBC 1,0)  
  
 SQL_TC_DML = le transazioni possono contenere solo istruzioni DML (Data Manipulation Language) (**Select**, **Insert**, **Update**, **Delete**). Le istruzioni DDL (Data Definition Language) rilevate in una transazione generano un errore. (ODBC 1,0)  
  
 SQL_TC_DDL_COMMIT = le transazioni possono contenere solo istruzioni DML. Le istruzioni DDL (**Create Table**, **Drop index**e così via) rilevate in una transazione determinano il commit della transazione. (ODBC 2,0)  
  
 SQL_TC_DDL_IGNORE = le transazioni possono contenere solo istruzioni DML. Le istruzioni DDL rilevate in una transazione vengono ignorate. (ODBC 2,0)  
  
 SQL_TC_ALL = le transazioni possono contenere istruzioni DDL e istruzioni DML in qualsiasi ordine. (ODBC 1,0)  
  
 Poiché il supporto delle transazioni è obbligatorio in SQL-92, un driver conforme a SQL-92 [any level] non restituirà mai SQL_TC_NONE.)  
  
 SQL_TXN_ISOLATION_OPTION (ODBC 1,0)  
 Maschera di SQLUINTEGER che enumera i livelli di isolamento delle transazioni disponibili dal driver o dall'origine dati.  
  
 Le seguenti maschere di maschera vengono utilizzate insieme al flag per determinare quali opzioni sono supportate:  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 Per le descrizioni di questi livelli di isolamento, vedere la descrizione di SQL_DEFAULT_TXN_ISOLATION.  
  
 Per impostare il livello di isolamento della transazione, un'applicazione chiama **SQLSetConnectAttr** per impostare l'attributo SQL_ATTR_TXN_ISOLATION. Per ulteriori informazioni, vedere [funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre SQL_TXN_SERIALIZABLE come supportato. Un driver con livello di transizione FIPS può restituire sempre tutte queste opzioni come supportate.  
  
 SQL_UNION (ODBC 2,0)  
 Maschera di SQLUINTEGER che enumera il supporto per la clausola **Union** :  
  
 SQL_U_UNION = l'origine dati supporta la clausola **Union** .  
  
 SQL_U_UNION_ALL = l'origine dati supporta la parola chiave **All** nella clausola **Union** . (**SQLGetInfo** restituisce sia SQL_U_UNION che SQL_U_UNION_ALL in questo caso).  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre entrambe le opzioni come supportate.  
  
 SQL_USER_NAME (ODBC 1,0)  
 Stringa di caratteri con il nome usato in un determinato database, che può essere diverso dal nome dell'account di accesso.  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3,0)  
 Stringa di caratteri che indica l'anno di pubblicazione della specifica del gruppo aperto con cui la versione di gestione driver ODBC è completamente conforme.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1,0)  
 Stringa di caratteri: "Y" se l'utente è in grado di eseguire tutte le routine restituite da **SQLProcedures**; "N" se è possibile che vengano restituite procedure che non possono essere eseguite dall'utente.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1,0)  
 Una stringa di caratteri: "Y" se all'utente sono garantiti i privilegi di **selezione** per tutte le tabelle restituite da **SQLTables**; "N" se è possibile che vengano restituite tabelle a cui l'utente non può accedere.  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3,0)  
 Valore SQLUSMALLINT che specifica il numero massimo di ambienti attivi che il driver è in grado di supportare. Se non è presente alcun limite specificato o il limite è sconosciuto, questo valore viene impostato su zero.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3,0)  
 Maschera di SQLUINTEGER che enumera il supporto per le funzioni di aggregazione:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Un driver conforme a SQL-92 Entry Level restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_ALTER_DOMAIN (ODBC 3,0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **ALTER Domain** , come definito in SQL-92, supportate dall'origine dati. Un driver SQL-92 conforme a livello completo restituirà sempre tutte le maschere di bit. Un valore restituito pari a "0" indica che l'istruzione **ALTER Domain** non è supportata.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = è supportato l'aggiunta di un vincolo di dominio (livello completo)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter Domain> \<set Domain default clause> è supportato (livello completo)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<la clausola di definizione del nome del vincolo> è supportata per la denominazione del vincolo di dominio (livello intermedio)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<drop Domain CONSTRAINT clause> è supportato (livello completo)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter Domain> \<drop Domain default> è supportato (livello completo)  
  
 I seguenti bit specificano gli \<attributi di vincolo supportati \<> se è supportato l'aggiunta di un vincolo di dominio> (il bit SQL_AD_ADD_DOMAIN_CONSTRAINT è impostato):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (livello completo) SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (livello completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (livello completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo)  
  
 SQL_ALTER_TABLE (ODBC 2,0)  
 Maschera di SQLUINTEGER che enumera le clausole nell'istruzione **ALTER TABLE** supportata dall'origine dati.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Per determinare le clausole supportate sono utilizzate le maschere di comando seguenti:  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<aggiungi colonna> clausola è supportata con la funzionalità per specificare le regole di confronto delle colonne (livello completo) (ODBC 3,0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<aggiungi colonna> clausola è supportata con la funzionalità per specificare i valori predefiniti delle colonne (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<aggiungi colonna> supportata (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_ADD_CONSTRAINT = \<aggiungi colonna> clausola è supportata con la funzionalità per specificare i vincoli di colonna (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<clausola Add TABLE Constraint> supportata (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<il nome del vincolo> della definizione è supportato per la denominazione di vincoli di colonna e tabella (livello intermedio) (ODBC 3,0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<DROP COLUMN> Cascade è supportato (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alter Column> \<DROP column default clause> è supportato (livello intermedio) (ODBC 3,0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<DROP COLUMN> Restrict è supportato (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3,0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<DROP COLUMN> Restrict è supportato (livello di transizione FIPS) (ODBC 3,0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alter Column> \<SET column default clause> è supportato (livello intermedio) (ODBC 3,0)  
  
 I seguenti bit specificano gli \<attributi del vincolo di supporto> se sono supportati i vincoli di colonna o di tabella (il bit SQL_AT_ADD_CONSTRAINT è impostato):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (livello completo) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (livello completo) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (livello completo) (ODBC 3,0)  
  
 SQL_ASYNC_MODE (ODBC 3,0)  
 Valore SQLUINTEGER che indica il livello di supporto asincrono nel driver:  
  
 SQL_AM_CONNECTION = esecuzione asincrona a livello di connessione supportata. Tutti gli handle di istruzione associati a un determinato handle di connessione sono in modalità asincrona o tutti sono in modalità sincrona. Un handle di istruzione in una connessione non può essere in modalità asincrona mentre un altro handle di istruzione nella stessa connessione è in modalità sincrona e viceversa.  
  
 SQL_AM_STATEMENT = esecuzione asincrona a livello di istruzione supportata. Alcuni handle di istruzione associati a un handle di connessione possono essere in modalità asincrona, mentre altri handle di istruzione nella stessa connessione sono in modalità sincrona.  
  
 SQL_AM_NONE = la modalità asincrona non è supportata.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3,0)  
 Maschera di SQLUINTEGER che enumera il comportamento del driver rispetto alla disponibilità dei conteggi delle righe. Insieme al tipo di informazioni vengono utilizzate le maschere di maschera seguenti:  
  
 SQL_BRC_ROLLED_UP = il numero di righe per le istruzioni INSERT, DELETE o UPDATE consecutive viene sottoposta a rollup. Se questo bit non è impostato, i conteggi delle righe sono disponibili per ogni istruzione.  
  
 SQL_BRC_PROCEDURES = i conteggi delle righe, se presenti, sono disponibili quando un batch viene eseguito in una stored procedure. Se i conteggi delle righe sono disponibili, è possibile eseguirne il rollup o la disponibilità singola, a seconda del SQL_BRC_ROLLED_UP bit.  
  
 SQL_BRC_EXPLICIT = i conteggi delle righe, se presenti, sono disponibili quando un batch viene eseguito direttamente tramite una chiamata a **SQLExecute** o **SQLExecDirect**. Se i conteggi delle righe sono disponibili, è possibile eseguirne il rollup o la disponibilità singola, a seconda del SQL_BRC_ROLLED_UP bit.  
  
## <a name="example"></a>Esempio  
 **SQLGetInfo** restituisce elenchi di opzioni supportate come maschera di maschera SQLUINTEGER in **InfoValuePtr*. La maschera di maschera per ogni opzione viene utilizzata insieme al flag per determinare se l'opzione è supportata.  
  
 Ad esempio, un'applicazione può usare il codice seguente per determinare se la funzione scalare della sottostringa è supportata dal driver associato alla connessione.  
  
 Per un altro esempio di uso di **SQLGetInfo**, vedere [funzione SQLTables](../../../odbc/reference/syntax/sqltables-function.md).  
  
```cpp  
SQLUINTEGER fFuncs;  
  
SQLGetInfo(hdbc,   
           SQL_STRING_FUNCTIONS,  
           (SQLPOINTER)&fFuncs,  
           sizeof(fFuncs),  
           NULL);  
  
// SUBSTRING supported  
if (fFuncs & SQL_FN_STR_SUBSTRING)   
   ;   // do something  
  
// SUBSTRING not supported  
else  
   ;   // do something else  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
 Restituzione dell'impostazione di un attributo di connessione  
 [Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 Determinare se un driver supporta una funzione  
 [SQLGetFunctions Function](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 Restituzione dell'impostazione di un attributo di istruzione  
 [Funzione SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 Restituzione di informazioni sui tipi di dati di un'origine dati  
 [Funzione SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni di riferimento sulle API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
