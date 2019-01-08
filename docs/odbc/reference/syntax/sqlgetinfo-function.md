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
manager: craigg
ms.openlocfilehash: f0878b7c0d6e7cea6f1dcdc90fa7e78a2680546b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204890"
---
# <a name="sqlgetinfo-function"></a>Funzione SQLGetInfo
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLGetInfo** restituisce informazioni generali sull'origine dati e i driver associato con una connessione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
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
 [Input] Tipo di informazioni.  
  
 *InfoValuePtr*  
 [Output] Puntatore a un buffer in cui si desidera restituire le informazioni. A seconda le *InfoType* richiesto, le informazioni restituite sarà uno dei seguenti: una stringa di caratteri con terminazione null, un valore SQLUSMALLINT, maschera di bit SQLUINTEGER, un flag SQLUINTEGER e un valore binario SQLUINTEGER, o un oggetto Valore SQLULEN.  
  
 Se il *InfoType* l'argomento è SQL_DRIVER_HDESC o SQL_DRIVER_HSTMT, il *InfoValuePtr* argomento è sia di input e output. (Vedere i descrittori SQL_DRIVER_HDESC o SQL_DRIVER_HSTMT più avanti in questa descrizione della funzione per altre informazioni).  
  
 Se *InfoValuePtr* sia impostato su NULL *StringLengthPtr* continuerà a restituire il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui fa riferimento *InfoValuePtr*.  
  
 *BufferLength*  
 [Input] Lunghezza del \* *InfoValuePtr* buffer. Se il valore in  *\*InfoValuePtr* non è una stringa di caratteri o se *InfoValuePtr* è un puntatore null, il *BufferLength* argomento verrà ignorato. Il driver presuppone che le dimensioni di  *\*InfoValuePtr* rappresenti SQLUSMALLINT SQLUINTEGER, in base il *InfoType*. Se  *\*InfoValuePtr* è una stringa Unicode (quando si chiama **SQLGetInfoW**), il *BufferLength* argomento deve essere un numero pari; se non, SQLSTATE HY090 ( Lunghezza della stringa o buffer non valido) viene restituito.  
  
 *StringLengthPtr*  
 [Output] Puntatore a un buffer in cui restituire il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire in **InfoValuePtr*.  
  
 Per i dati di tipo carattere, se il numero di byte disponibili da restituire è maggiore o uguale a *BufferLength*, le informazioni contenute in \* *InfoValuePtr* viene troncato a  *BufferLength* byte meno la lunghezza di una terminazione null di caratteri ed è con terminazione null dal driver.  
  
 Per tutti gli altri tipi di dati, il valore di *BufferLength* viene ignorato e il driver presuppone che la dimensione del \* *InfoValuePtr* rappresenti SQLUSMALLINT SQLUINTEGER, a seconda di  *InfoType*.  
  
## <a name="return-value"></a>Valore restituito  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetInfo** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato può essere ottenuto chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_DBC e un *gestiscono* dei *ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLGetInfo** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Il buffer \* *InfoValuePtr* non era sufficientemente grande per restituire tutte le informazioni richieste. Di conseguenza, le informazioni sono state troncate. Viene restituita la lunghezza delle informazioni richieste nella sua forma non troncato **StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08003|Connessione non aperta|(DM) del tipo di informazioni richieste nella *InfoType* richiede una connessione aperta. Dei tipi di informazioni riservati da ODBC, possono essere restituite solo SQL_ODBC_VER senza una connessione aperta.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver non è riuscito ad allocare memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY024|Valore dell'attributo non valido|(DM) di *InfoType* argomento era SQL_DRIVER_HSTMT e il valore a cui punta *InfoValuePtr* non era un handle di istruzione valida.<br /><br /> (DM) di *InfoType* argomento era SQL_DRIVER_HDESC e il valore a cui punta *InfoValuePtr* non era un handle descrittore valido.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore specificato per l'argomento *BufferLength* era minore di 0.<br /><br /> (DM) il valore specificato per *BufferLength* era un numero dispari, e  *\*InfoValuePtr* era di un tipo di dati Unicode.|  
|HY096|Tipo di informazioni non compreso nell'intervallo|Il valore specificato per l'argomento *InfoType* non è valido per la versione di ODBC supportati dal driver.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Campo facoltativo non implementato|Il valore specificato per l'argomento *InfoType* era un valore specifico del driver che non è supportato dal driver.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|(DM) il driver corrispondente per il *ConnectionHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Vengono visualizzati i tipi di informazioni attualmente definiti in "Informazioni tipi" più avanti in questa sezione; si prevede che più verrà definito per sfruttare i vantaggi di origini dati diverse. Una gamma di tipi di informazioni è riservata da ODBC. gli sviluppatori di driver necessario riservare i valori per il proprio uso specifici del driver da Open Group. **SQLGetInfo** non esegue alcuna conversione Unicode oppure *thunk* (vedere [appendice a: Codici di errore ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) del *riferimento per programmatori ODBC*) per definiti dal driver *tipi*. Per altre informazioni, vedere [tipi di dati specifici del Driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e gli attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md). Il formato delle informazioni restituite nelle \* *InfoValuePtr* dipende il *InfoType* richiesto. **SQLGetInfo** restituirà informazioni in uno dei cinque diversi formati:  
  
-   Una stringa di caratteri con terminazione null  
  
-   Un valore SQLUSMALLINT  
  
-   Maschera di bit SQLUINTEGER  
  
-   Un valore SQLUINTEGER  
  
-   Un valore binario SQLUINTEGER  
  
 Il formato della ognuno dei seguenti tipi di informazioni viene indicato nella descrizione del tipo. L'applicazione deve eseguire il cast di valore restituito in **InfoValuePtr* conseguenza. Per un esempio di come un'applicazione è stato possibile recuperare dati da una maschera di bit SQLUINTEGER, vedere "Esempio di codice".  
  
 Un driver deve restituire un valore per ogni tipo di informazioni che viene definito nelle tabelle seguenti. Se un tipo di informazioni non si applica al driver o origine dati, il driver restituisce uno dei valori elencati nella tabella seguente.  
  
 Stringa di caratteri ("Y" o "N")  
 "N"  
  
 Stringa di caratteri (non "Y" o "N")  
 Stringa vuota  
  
 SQLUSMALLINT  
 0  
  
 Maschera di bit SQLUINTEGER o valore binario SQLUINTEGER  
 0L  
  
 Se un'origine dati non supporta le procedure, ad esempio **SQLGetInfo** restituisce i valori elencati nella tabella seguente per i valori di *InfoType* correlate alle procedure.  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 Stringa vuota  
  
 **SQLGetInfo** restituisce SQLSTATE HY096 (valore dell'argomento non valido) per valori di *InfoType* che rientrano nell'intervallo dei tipi di informazioni riservati per l'utilizzo da ODBC, ma non sono definiti dalla versione di ODBC supportati dal driver. Per determinare quale versione di ODBC un driver conforme, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_DRIVER_ODBC_VER. **SQLGetInfo** restituisce SQLSTATE HYC00 (funzionalità facoltativa non implementata) per valori di *InfoType* che rientrano nell'intervallo dei tipi di informazioni riservati per l'uso di specifiche del driver, ma non sono supportati dal driver.  
  
 Tutte le chiamate a **SQLGetInfo** richiedono una connessione aperta, tranne quando la *InfoType* è SQL_ODBC_VER, che restituisce la versione di gestione Driver.  
  
## <a name="information-types"></a>Tipi di informazioni  
 In questa sezione sono elencati i tipi di informazioni supportati da **SQLGetInfo**. Tipi di informazioni sono raggruppati in modo categorico ed elencati in ordine alfabetico. Tipi di informazioni che sono state aggiunte o rinominati per ODBC 3*x* sono inoltre elencati.  
  
## <a name="driver-information"></a>Informazioni sul driver  
 I valori seguenti del *InfoType* argomento restituiscono informazioni sul driver ODBC, ad esempio il numero di istruzioni attive, il nome dell'origine dati e il livello di conformità agli standard di interfaccia:  
  
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
>  Quando si implementa **SQLGetInfo**, un driver può migliorare le prestazioni riducendo al minimo il numero di volte in cui vengono inviati o richiesti dal server.  
  
## <a name="dbms-product-information"></a>Informazioni sui prodotti DBMS  
 I valori seguenti del *InfoType* argomento restituiscono informazioni relative al prodotto DBMS, ad esempio il nome DBMS e la versione:  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>Informazioni sull'origine dati  
 I valori seguenti del *InfoType* argomento restituiscono informazioni relative all'origine dati, ad esempio caratteristiche e funzionalità delle transazioni:  
  
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
  
## <a name="supported-sql"></a>SQL supportate  
 I valori seguenti del *InfoType* argomento restituiscono informazioni sulle istruzioni SQL supportati dall'origine dati. La sintassi SQL di ogni funzionalità descritto da questi tipi di informazioni è la sintassi SQL-92. Questi tipi di informazioni non descrivono esaustivamente tutta la grammatica SQL-92. Al contrario, descrivono le parti della grammatica per i dati origini offrono in genere diversi livelli di supporto. In particolare, vengono illustrata la maggior parte delle istruzioni DDL di SQL-92.  
  
 Le applicazioni devono determinare il livello di grammatica supportata dal tipo di informazioni SQL_SQL_CONFORMANCE generale e usare gli altri tipi di informazioni per determinare le variazioni del livello di conformità agli standard indicati.  
  
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
 I valori seguenti del *InfoType* argomento restituiscono informazioni sui limiti applicati per gli identificatori e le clausole in istruzioni SQL, ad esempio la lunghezza massima di identificatori e il numero massimo di colonne in un elenco di selezione. Le limitazioni possono essere imposte dal driver o l'origine dati.  
  
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
 I valori seguenti del *InfoType* argomento restituiscono informazioni sulle funzioni scalari supportate dall'origine dati e il driver. Per altre informazioni sulle funzioni scalari, vedere [appendice e: Funzioni scalari](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>Informazioni sulla conversione  
 I valori seguenti del *InfoType* argomenti restituiscono un elenco dei tipi di dati SQL a cui l'origine dati può convertire il tipo di dati SQL specificato con il **CONVERTIRE** funzione scalare:  
  
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
  
## <a name="information-types-added-for-odbc-3x"></a>Tipi di informazioni aggiunte per ODBC 3.x  
 I valori seguenti del *InfoType* argomento sono state aggiunte per ODBC 3*x*:  
  
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
  
## <a name="information-types-renamed-for-odbc-3x"></a>Tipi di informazioni rinominati per ODBC 3.x  
 I valori seguenti del *InfoType* argomento sono state rinominate per ODBC 3*x*.  
  
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
  
## <a name="information-types-deprecated-in-odbc-3x"></a>Tipi di informazioni deprecati in ODBC 3.x  
 I valori seguenti del *InfoType* argomento sono state deprecate in ODBC 3*x*. ODBC 3 *. x* i driver devono continuare a supportare questi tipi di informazioni per garantire la compatibilità con l'API ODBC 2*x* applicazioni. (Per altre informazioni su questi tipi, vedere [supporto di SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md) nell'appendice g: Driver linee guida per la compatibilità con le versioni precedenti.)  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>Descrizioni dei tipi di informazioni  
 Nella tabella seguente sono elencati in ordine alfabetico in ogni tipo di informazioni, la versione di ODBC in cui è stato introdotto e la relativa descrizione.  
  
 SQL_ACCESSIBLE_PROCEDURES ODBC (1.0)  
 Una stringa di caratteri: "Y" se l'utente può eseguire tutte le procedure restituite dal **SQLProcedures**; "N" se vi sono le procedure restituite che l'utente non può eseguire.  
  
 SQL_ACCESSIBLE_TABLES ODBC (1.0)  
 Una stringa di caratteri: "Y" se l'utente è garantita **selezionate** privilegi per tutte le tabelle restituite dal **SQLTables**; "N" se vi sono tabelle restituito che l'utente non può accedere.  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 Un valore SQLUSMALLINT che specifica il numero massimo di ambienti attivi in grado di supportare il driver. Se non esiste un limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione di supporto per le funzioni di aggregazione:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre tutte queste opzioni supportate.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **ALTER dominio** istruzione, come definito in SQL-92, supportati dall'origine dati. Un driver conforme con livello SQL-92 completo restituirà sempre tutte le maschere di bit. Il valore restituito pari a "0" indica che il **ALTER dominio** istruzione non è supportata.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità è racchiusa tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = aggiunta è supportato un vincolo di dominio (livello completo)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter dominio > \<clausola predefinite dominio set > è supportato (livello completo)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<clausola definizione di vincolo name > è supportato per la denominazione vincolo dei domini (livello intermedio)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<clausola di vincolo di dominio di rilascio > è supportato (livello completo)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter dominio > \<clausola default domain rilascio > è supportato (livello completo)  
  
 I bit seguenti specificano supportati \<attributi di vincolo > Se \<Aggiungi vincolo di dominio > è supportato (è impostato il bit SQL_AD_ADD_DOMAIN_CONSTRAINT):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (livello completo) SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (livello completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (livello completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **ALTER TABLE** istruzione supportata dall'origine dati.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità è racchiusa tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<Aggiungi colonna > clausola è supportata, con funzionalità per specificare regole di confronto colonna (livello completo) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<Aggiungi colonna > clausola è supportata, con funzionalità per specificare valori predefiniti delle colonne (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<Aggiungi colonna > è supportato (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT = \<Aggiungi colonna > clausola è supportata, con funzionalità per specificare i vincoli di colonna (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<Aggiungi vincolo di tabella > clausola è supportata (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<definizione del vincolo name > è supportato per la denominazione dei vincoli di colonna e tabella (livello intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<eliminare la colonna > è supportato in serie (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<modificare la colonna > \<clausola default di eliminazione colonna > è supportato (livello intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<eliminare la colonna > è supportato RESTRICT (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<eliminare la colonna > è supportato RESTRICT (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<modificare la colonna > \<clausola default colonna set > è supportato (livello intermedio) (ODBC 3.0)  
  
 I bit seguenti specificano il supporto \<attributi di vincolo > Se è consentito specificare vincoli di colonna o una tabella (è impostato il bit SQL_AT_ADD_CONSTRAINT):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (livello completo) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (livello completo) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (livello completo) (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 Un valore SQLUINTEGER che indica se il driver è possibile di eseguire in modo asincrono le funzioni nell'handle di connessione.  
  
 SQL_ASYNC_DBC_CAPABLE = il driver può eseguire funzioni di connessione in modo asincrono.  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = il driver non è possibile eseguire le funzioni di connessione in modo asincrono.  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 Un valore SQLUINTEGER che indica il livello di supporto asincrono nel driver:  
  
 SQL_AM_CONNECTION = è supportata l'esecuzione asincrona a livello di connessione. Tutti gli handle di istruzione associati a un handle di connessione specificate siano in modalità asincrona o tutti sono in modalità sincrona. Un handle di istruzione in una connessione non può essere in modalità asincrona, mentre un altro handle di istruzione nella stessa connessione è in modalità sincrona e viceversa.  
  
 SQL_AM_STATEMENT = è supportata l'esecuzione asincrona a livello di istruzione. Alcuni handle di istruzione associati a un handle di connessione possono essere in modalità asincrona, mentre altri handle di istruzione nella stessa connessione sono in modalità sincrona.  
  
 SQL_AM_NONE = asincrono in modalità non è supportata.  
  
 SQL_ASYNC_NOTIFICATION  
 Un valore SQLUINTEGER che indica se il driver supporta la notifica asincrona:  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE** notifica esecuzione asincrona è supportata dal driver.  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE** notifica esecuzione asincrona non è supportata dal driver.  
  
 Esistono due categorie di operazioni asincrone ODBC: operazioni asincrone a livello di connessione e istruzione il livello di operazioni asincrone.  Se un driver restituisce SQL_ASYNC_NOTIFICATION_CAPABLE, deve supportare la notifica per tutte le API che può eseguire in modo asincrono.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera il comportamento del driver per quanto riguarda la disponibilità di riga viene conteggiata. Le maschere di bit seguenti vengono usati insieme al tipo di informazioni:  
  
 SQL_BRC_ROLLED_UP = conteggio delle righe per le istruzioni INSERT, DELETE o UPDATE consecutive vengono raggruppate in un unico. Se questo bit non è impostato, i conteggi delle righe sono disponibili per ogni istruzione.  
  
 SQL_BRC_PROCEDURES = conteggio delle righe, se presente, sono disponibili quando un batch viene eseguito in una stored procedure. Se i conteggi delle righe sono disponibili, è possibile eseguire il rollback verso l'alto o singolarmente disponibile, a seconda di bit SQL_BRC_ROLLED_UP.  
  
 SQL_BRC_EXPLICIT = conteggio delle righe, se presente, sono disponibili quando un batch viene eseguito chiamando direttamente **SQLExecute** oppure **SQLExecDirect**. Se i conteggi delle righe sono disponibili, è possibile eseguire il rollback verso l'alto o singolarmente disponibile, a seconda di bit SQL_BRC_ROLLED_UP.  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione di supporto del driver per i batch. Le maschere di bit seguenti vengono usate per determinare quale livello è supportato:  
  
 SQL_BS_SELECT_EXPLICIT = quali driver supporta esplicito batch possono avere set di risultati la generazione di istruzioni.  
  
 SQL_BS_ROW_COUNT_EXPLICIT = driver supporta esplicito batch che può contenere istruzioni di generazione-conteggio delle righe.  
  
 SQL_BS_SELECT_PROC = il driver supporta esplicita procedure che possono avere set di risultati la generazione di istruzioni.  
  
 SQL_BS_ROW_COUNT_PROC = i driver supporta esplicita procedure che possono contenere istruzioni di generazione-conteggio delle righe.  
  
 SQL_BOOKMARK_PERSISTENCE (ODBC 2.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le operazioni tramite la quale la persistenza dei segnalibri.  
  
 Le maschere di bit seguenti vengono usati con il flag per determinare tramite il quale la persistenza dei segnalibri di opzioni:  
  
 SQL_BP_CLOSE = i segnalibri sono validi dopo un'applicazione chiama **SQLFreeStmt** con l'opzione di SQL_CLOSE, o **SQLCloseCursor** per chiudere il cursore associato a un'istruzione.  
  
 SQL_BP_DELETE = il segnalibro per una riga è valida dopo tale riga è stata eliminata.  
  
 SQL_BP_DROP = i segnalibri sono validi dopo un'applicazione chiama **SQLFreeHandle** con un *HandleType* SQL_HANDLE_STMT per un'istruzione drop.  
  
 SQL_BP_TRANSACTION = i segnalibri sono validi dopo un'applicazione esegue il commit o il rollback di una transazione.  
  
 SQL_BP_UPDATE = il segnalibro per una riga è valida dopo che è stata aggiornata alcuna colonna nella riga, incluse le colonne chiave.  
  
 SQL_BP_OTHER_HSTMT = un segnalibro associato con una istruzione può essere utilizzata con un'altra istruzione. A meno che non viene specificato SQL_BP_CLOSE o SQL_BP_DROP, il cursore nella prima istruzione deve essere aperto.  
  
 SQL_CATALOG_LOCATION (ODBC 2.0)  
 Un valore SQLUSMALLINT che indica la posizione del catalogo in un nome di tabella completo:  
  
 SQL_CL_STARTSQL_CL_END  
  
 Ad esempio, un driver Xbase restituisce SQL_CL_START perché il nome della directory (catalogo) si trova all'inizio del nome della tabella, come in \EMPDATA\EMP. DBF. Un driver di ORACLE Server restituisce SQL_CL_END perché il catalogo si trova alla fine del nome della tabella, come in ADMIN.EMP@EMPDATA.  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre SQL_CL_START. Se i cataloghi non sono supportati dall'origine dati, viene restituito un valore pari a 0. Per determinare se sono supportati i cataloghi, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_CATALOG_NAME.  
  
 Ciò *InfoType* è stata rinominata per ODBC 3.0 da ODBC 2.0 *InfoType* SQL_QUALIFIER_LOCATION.  
  
 SQL_CATALOG_NAME (ODBC 3.0)  
 Una stringa di caratteri: "Y" se il server supporta i nomi di catalogo o "N" Se non esiste.  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre "Y".  
  
 SQL_CATALOG_NAME_SEPARATOR ODBC (1.0)  
 Una stringa di caratteri: uno o più caratteri che definisce l'origine dati come separatore tra un nome di catalogo e l'elemento nome completo che segue oppure lo precede.  
  
 Se i cataloghi non sono supportati dall'origine dati, viene restituita una stringa vuota. Per determinare se sono supportati i cataloghi, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_CATALOG_NAME. Restituisce sempre un driver di livello conforme allo standard SQL-92 completo ".".  
  
 Ciò *InfoType* è stata rinominata per ODBC 3.0 da ODBC 2.0 *InfoType* SQL_QUALIFIER_NAME_SEPARATOR.  
  
 SQL_CATALOG_TERM ODBC (1.0)  
 Una stringa di caratteri con il nome del fornitore di origine dati per un catalogo. ad esempio, "database" o "directory". Questa stringa può essere in caso di superiore, inferiore o misto.  
  
 Se i cataloghi non sono supportati dall'origine dati, viene restituita una stringa vuota. Per determinare se sono supportati i cataloghi, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_CATALOG_NAME. Un driver di livello conforme allo standard SQL-92 completo restituirà sempre "catalog".  
  
 Ciò *InfoType* è stata rinominata per ODBC 3.0 da ODBC 2.0 *InfoType* SQL_QUALIFIER_TERM.  
  
 SQL_CATALOG_USAGE (ODBC 2.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le istruzioni in cui è possibile usare i cataloghi.  
  
 Per determinare dove è possibile utilizzare i cataloghi vengono usati le maschere di bit seguenti:  
  
 SQL_CU_DML_STATEMENTS = i cataloghi sono supportati in tutte le istruzioni Data Manipulation Language: **Selezionare**, **inserire**, **aggiornare**, **eliminare**e, se supportato **selezionare per aggiornare** e l'eliminazione e aggiornamento posizionato istruzioni.  
  
 SQL_CU_PROCEDURE_INVOCATION = i cataloghi sono supportati nell'istruzione ODBC procedure chiamata.  
  
 SQL_CU_TABLE_DEFINITION = i cataloghi sono supportati in tutte le istruzioni di definizione di tabella: **Crea tabella**, **Crea vista**, **ALTER TABLE**, **DROP TABLE**, e **DROP VIEW**.  
  
 SQL_CU_INDEX_DEFINITION = i cataloghi sono supportati in tutte le istruzioni di definizione di indice: **Crea indice** e **DROP INDEX**.  
  
 SQL_CU_PRIVILEGE_DEFINITION = i cataloghi sono supportati in tutte le istruzioni di definizione dei privilegi: **CONCESSIONE** e **revocare**.  
  
 Se i cataloghi non sono supportati dall'origine dati, viene restituito un valore pari a 0. Per determinare se sono supportati i cataloghi, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_CATALOG_NAME. Un driver di livello conforme allo standard SQL-92 completo restituirà sempre una maschera di bit con tutti questi set di bit.  
  
 Ciò *InfoType* è stata rinominata per ODBC 3.0 da ODBC 2.0 *InfoType* SQL_QUALIFIER_USAGE.  
  
 SQL_COLLATION_SEQ (ODBC 3.0)  
 Il nome della sequenza di regole di confronto. Si tratta di una stringa di caratteri che indica il nome delle regole di confronto predefinito per il carattere predefinito impostato per il server (ad esempio, ' ISO 8859-1' o EBCDIC). Se questo è sconosciuto, verrà restituita una stringa vuota. Un driver di livello conforme allo standard SQL-92 completo restituirà sempre una stringa non vuota.  
  
 SQL_COLUMN_ALIAS (ODBC 2.0)  
 Una stringa di caratteri: "Y" se l'origine dati supporta gli alias di colonna; in caso contrario, "N".  
  
 Un alias di colonna è un nome alternativo che può essere specificato per una colonna nell'elenco di selezione utilizzando la clausola AS. Un driver conforme a livello di SQL-92 voce restituirà sempre "Y".  
  
 SQL_CONCAT_NULL_BEHAVIOR ODBC (1.0)  
 Un valore SQLUSMALLINT che indica il modo in cui l'origine dati gestisce la concatenazione Null con valori di colonne di tipo carattere i dati con colonne di tipo di dati di caratteri con valori non NULL:  
  
 SQL_CB_NULL = risultato viene valutato come NULL.  
  
 SQL_CB_NON_NULL = risultato è la concatenazione delle colonne con valori non NULL.  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre SQL_CB_NULL.  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_ DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1.0)  
 Maschera di bit SQLUINTEGER. La maschera di bit indica conversioni supportate dall'origine dati con il **CONVERTIRE** funzioni scalari per i dati del tipo denominato nel *InfoType*. Se la maschera di bit uguale a zero, l'origine dati non supporta tutte le conversioni dai dati di tipo denominato, inclusa la conversione al tipo di dati stesso.  
  
 Per determinare se un'origine dati supporta la conversione dei dati SQL_INTEGER al tipo di dati SQL_BIGINT, ad esempio, un'applicazione chiama **SQLGetInfo** con il *InfoType* di SQL_CONVERT_INTEGER. L'applicazione esegue un' **AND** operazione con la maschera di bit restituita e SQL_CVT_BIGINT. Se il valore risultante è diverso da zero, la conversione è supportata.  
  
 Le maschere di bit seguenti vengono usate per determinare quali conversioni supportate:  
  
 SQL_CVT_BIGINT (ODBC 1.0) SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DECIMAL (ODBC 1.0) SQL_CVT_DOUBLE (ODBC 1.0) SQL_CVT_FLOAT (ODBC 1.0) SQL_CVT_INTEGER (ODBC 1.0) SQL SQL_CVT_ SQL_CVT_TIME (ODBC 1.0) DI _CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0) SQL_CVT_LONGVARBINARY (ODBC 1.0) SQL_CVT_LONGVARCHAR (ODBC 1.0) SQL_CVT_NUMERIC (ODBC 1.0) SQL_CVT_REAL ODBC 1.0) SQL_CVT_SMALLINT (ODBC 1.0) TIMESTAMP (ODBC 1.0) SQL_CVT_TINYINT (ODBC 1.0) SQL_CVT_VARBINARY (ODBC 1.0) SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS ODBC (1.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le funzioni di conversione scalari supportate dal driver e origine dati associata.  
  
 La maschera di bit seguente viene usato per determinare le funzioni di conversione supportate:  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME ODBC (1.0)  
 Un valore SQLUSMALLINT che indica se i nomi di correlazione di tabella sono supportati:  
  
 SQL_CN_NONE = correlazione nomi non sono supportati.  
  
 SQL_CN_DIFFERENT = correlazione i nomi sono supportati, ma devono essere diverso dai nomi delle tabelle che rappresentano.  
  
 SQL_CN_ANY = correlazione i nomi sono supportati e possono essere qualsiasi nome definito dall'utente valido.  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre SQL_CN_ANY.  
  
 SQL_CREATE_ASSERTION (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **ASSERZIONE creare** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_CA_CREATE_ASSERTION  
  
 Bit seguenti specificano l'attributo di vincolo supportato se è supportata la possibilità di specificare in modo esplicito gli attributi di vincolo (vedere i tipi di informazioni SQL_ALTER_TABLE e SQL_CREATE_TABLE):  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre tutte queste opzioni supportate. Il valore restituito pari a "0" indica che il **ASSERZIONE creare** istruzione non è supportata.  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **creare SET di caratteri** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre tutte queste opzioni supportate. Il valore restituito pari a "0" indica che il **creare SET di caratteri** istruzione non è supportata.  
  
 SQL_CREATE_COLLATION (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **creare le regole di confronto** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 La maschera di bit seguente viene usato per determinare quali clausole sono supportate:  
  
 SQL_CCOL_CREATE_COLLATION  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre questa opzione come supportato. Il valore restituito pari a "0" indica che il **creare le regole di confronto** istruzione non è supportata.  
  
 SQL_CREATE_DOMAIN (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **crea dominio** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_CDO_CREATE_DOMAIN = il dominio di creare l'istruzione è supportata (livello intermedio).  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION = \<definizione del vincolo name > è supportato per la denominazione dei vincoli di dominio (livello intermedio).  
  
 I bit seguenti specificano la possibilità di creare i vincoli di colonna: SQL_CDO_DEFAULT = è consentito specificare vincoli di dominio (livello intermedio) SQL_CDO_CONSTRAINT = è consentito specificare le impostazioni predefinite di dominio (livello intermedio) SQL_CDO_COLLATION = È consentito specificare le regole di confronto di dominio (livello completo)  
  
 Bit seguenti specificano gli attributi di vincolo supportato se è consentito specificare vincoli di dominio (SQL_CDO_DEFAULT è impostato):  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED (livello completo) SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo) SQL_CDO_CONSTRAINT_DEFERRABLE (livello completo) SQL_CDO_CONSTRAINT_NON_DEFERRABLE (livello completo)  
  
 Il valore restituito pari a "0" indica che il **crea dominio** istruzione non è supportata.  
  
 SQL_CREATE_SCHEMA (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **CREATE SCHEMA** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 Un driver conforme a livello intermedio di SQL-92 restituirà sempre le opzioni SQL_CS_CREATE_SCHEMA e SQL_CS_AUTHORIZATION supportato. Questi deve essere supportati anche a livello di SQL-92 voce, ma non necessariamente come istruzioni SQL. Un driver di livello conforme allo standard SQL-92 completo restituirà sempre tutte queste opzioni supportate.  
  
 SQL_CREATE_TABLE (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **CREATE TABLE** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità è racchiusa tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_CT_CREATE_TABLE = la tabella di creare l'istruzione è supportata. (Entry level)  
  
 SQL_CT_TABLE_CONSTRAINT = è consentito specificare vincoli di tabella (livello transitorio FIPS)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION = il \<definizione nome vincolo > clausola è supportata per la denominazione dei vincoli di colonna e tabella (livello intermedio)  
  
 I bit seguenti specificano la possibilità di creare tabelle temporanee:  
  
 SQL_CT_COMMIT_PRESERVE = Deleted righe vengono mantenute in caso di commit. (Livello completo) SQL_CT_COMMIT_DELETE = eliminate le righe vengono eliminate al momento del commit. (Livello completo) SQL_CT_GLOBAL_TEMPORARY = globale è possibile creare tabelle temporanee. (Livello completo) SQL_CT_LOCAL_TEMPORARY = locale è possibile creare tabelle temporanee. (Livello completo)  
  
 I bit seguenti specificano la possibilità di creare vincoli di colonna:  
  
 SQL_CT_COLUMN_CONSTRAINT = è consentito specificare vincoli di colonna (livello FIPS transitorio) SQL_CT_COLUMN_DEFAULT = è consentito specificare valori predefiniti delle colonne (livello FIPS transitorio) SQL_CT_COLUMN_COLLATION = specificando regole di confronto colonna è supportato (livello completo)  
  
 Bit seguenti specificano gli attributi di vincolo supportato se è consentito specificare vincoli di colonna o una tabella:  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED (livello completo) SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo) SQL_CT_CONSTRAINT_DEFERRABLE (livello completo) SQL_CT_CONSTRAINT_NON_DEFERRABLE (livello completo)  
  
 SQL_CREATE_TRANSLATION (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **traduzione creare** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 La maschera di bit seguente viene usato per determinare quali clausole sono supportate:  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre queste opzioni supportate. Il valore restituito pari a "0" indica che il **traduzione creare** istruzione non è supportata.  
  
 SQL_CREATE_VIEW (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **CREATE VIEW** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 Il valore restituito pari a "0" indica che il **CREATE VIEW** istruzione non è supportata.  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre le opzioni SQL_CV_CREATE_VIEW e SQL_CV_CHECK_OPTION supportato.  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre tutte queste opzioni supportate.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR ODBC (1.0)  
 Un valore SQLUSMALLINT che indica come un **COMMIT** operazione influisce su cursori e le istruzioni preparate nell'origine dati (il comportamento dell'origine dati quando si esegue il commit di una transazione).  
  
 Il valore di questo attributo riflette lo stato corrente dell'impostazione seguente: SQL_COPT_SS_PRESERVE_CURSORS.  
  
 SQL_CB_DELETE = cursori Chiudi ed eliminare le istruzioni preparate. Per usare il cursore anche in questo caso, l'applicazione deve reprepare e rieseguito l'istruzione.  
  
 SQL_CB_CLOSE = chiusura dei cursori. Per le istruzioni preparate, l'applicazione può chiamare **SQLExecute** nell'istruzione senza chiamare **SQLPrepare** nuovamente. Il valore predefinito per il driver ODBC di SQL è SQL_CB_CLOSE. Ciò significa che il driver ODBC di SQL si chiuderà i cursori quando si esegue il commit di una transazione.  
  
 SQL_CB_PRESERVE = cursori Preserve nella stessa posizione come indicato in precedenza il **COMMIT** operazione. L'applicazione può continuare a recuperare i dati oppure è possibile chiudere il cursore ed eseguire nuovamente l'istruzione senza nuovamente preparazione.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR ODBC (1.0)  
 Un valore SQLUSMALLINT che indica come un **ROLLBACK** operazione influisce su cursori e le istruzioni preparate nell'origine dati:  
  
 SQL_CB_DELETE = cursori Chiudi ed eliminare le istruzioni preparate. Per usare il cursore anche in questo caso, l'applicazione deve reprepare e rieseguito l'istruzione.  
  
 SQL_CB_CLOSE = chiusura dei cursori. Per le istruzioni preparate, l'applicazione può chiamare **SQLExecute** nell'istruzione senza chiamare **SQLPrepare** nuovamente.  
  
 SQL_CB_PRESERVE = cursori Preserve nella stessa posizione come indicato in precedenza il **ROLLBACK** operazione. L'applicazione può continuare a recuperare i dati oppure è possibile chiudere il cursore e rieseguito l'istruzione senza repreparing.  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 Un valore SQLUINTEGER che indica il supporto per la sensibilità del cursore:  
  
 SQL_INSENSITIVE = tutti i cursori su handle di istruzione Mostra il set di risultati senza che riflette le modifiche sono state apportate a essa da qualsiasi altro cursore all'interno della stessa transazione.  
  
 SQL_UNSPECIFIED = non viene specificato se i cursori dell'handle di istruzione di rendere visibili le modifiche apportate a un set di risultati, un altro cursore all'interno della stessa transazione. I cursori dell'handle di istruzione potrebbero rendere visibile nessuno, alcuni o tutti tali modifiche.  
  
 SQL_SENSITIVE = cursori sono sensibili alle modifiche apportate da altri cursori all'interno della stessa transazione.  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre l'opzione SQL_UNSPECIFIED supportato.  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre l'opzione SQL_INSENSITIVE supportato.  
  
 SQL_DATA_SOURCE_NAME ODBC (1.0)  
 Una stringa di caratteri con il nome dell'origine dati che è stato usato durante la connessione. Se l'applicazione ha chiamato **SQLConnect**, si tratta del valore della *szDSN* argomento. Se l'applicazione ha chiamato **SQLDriverConnect** oppure **SQLBrowseConnect**, si tratta del valore della parola chiave DSN nella stringa di connessione passata al driver. Se la stringa di connessione non contiene il **DSN** (parola chiave) (ad esempio quando questo contiene il **DRIVER** (parola chiave)), si tratta di una stringa vuota.  
  
 SQL_DATA_SOURCE_READ_ONLY ODBC (1.0)  
 Una stringa di caratteri. "Y" se l'origine dati è impostato su modalità READ ONLY, "N" se è in caso contrario.  
  
 Questa caratteristica si riferisce solo all'origine dati stessa. non è una caratteristica del driver che consente l'accesso all'origine dati. Un driver che è di lettura/scrittura può essere utilizzato con un'origine dati che è di sola lettura. Se un driver è di sola lettura, tutte le origini dati devono essere di sola lettura e deve restituire SQL_DATA_SOURCE_READ_ONLY.  
  
 SQL_DATABASE_NAME ODBC (1.0)  
 Una stringa di caratteri con il nome del database corrente in uso, se l'origine dati definisce un oggetto denominato chiamato "database".  
  
> [!NOTE]
>  In ODBC 3 *. x*, il valore restituito per questo *InfoType* possono essere restituiti chiamando **SQLGetConnectAttr** con un *attributo* argomento di SQL_ATTR_CURRENT_CATALOG.  
  
 SQL_DATETIME_LITERALS (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione di valori letterali datetime di SQL-92 supportati dall'origine dati. Si noti che questi sono i valori letterali di data/ora elencati nella specifica di SQL-92 sono separati dalle clausole di escape letterale di data/ora definite da ODBC. Per altre informazioni sulle clausole di escape letterali di ODBC datetime, vedere [Date, Time e Timestamp valori letterali](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Un driver di livello conformi a FIPS transitorio restituirà sempre il valore "1" nella maschera di bit per bit nell'elenco seguente. Un valore pari a "0" indica che non sono supportati valori letterali datetime di SQL-92.  
  
 Le maschere di bit seguenti vengono usate per determinare quali valori letterali sono supportati:  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_ SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME ODBC (1.0)  
 Una stringa di caratteri con il nome del prodotto DBMS accedono dal driver.  
  
 SQL_DBMS_VER ODBC (1.0)  
 Una stringa di caratteri che indica la versione del prodotto DBMS accedono dal driver. La versione è nel formato # #. # #. # # #, dove le prime due cifre sono la versione principale, le due cifre sono la versione secondaria, mentre le ultime quattro cifre sono la versione di rilascio. Il driver deve eseguire il rendering la versione del prodotto DBMS in questo formato tuttavia anche possibile aggiungere la versione di prodotto specifico DBMS. Ad esempio, "04.01.0000 Rdb 4.1".  
  
 SQL_DDL_INDEX (ODBC 3.0)  
 Un valore SQLUINTEGER che indica il supporto per la creazione ed eliminazione di indici:  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION ODBC (1.0)  
 Un valore SQLUINTEGER che indica che il livello di isolamento predefinito supportato dall'origine dati o driver oppure zero se l'origine dati non supporta le transazioni. I termini seguenti vengono usati per definire i livelli di isolamento delle transazioni:  
  
 **Lettura dirty** 1 transazione modifica una riga. La transazione 2 legge la riga modificata prima della modifica di commit della transazione 1. Se la transazione 1 esegue il rollback della modifica, la transazione 2 hanno leggerà una riga viene considerata mai esistito.  
  
 **Lettura non ripetibile** 1 transazione legge una riga. La transazione 2 aggiorna o elimina tale riga ed esegue il commit di questa modifica. Se la transazione 1 tenta di rilettura di riga, riceverà i valori di riga diversi o individua che la riga è stata eliminata.  
  
 **Righe fantasma** 1 transazione legge un set di righe che soddisfano alcuni criteri di ricerca. La transazione 2 genera una o più righe (tramite gli inserimenti o gli aggiornamenti) che corrispondono ai criteri di ricerca. Se la transazione 1 reexecutes l'istruzione che legge le righe, riceve un set diverso di righe.  
  
 Se l'origine dati supporta le transazioni, il driver restituisce uno delle maschere di bit seguenti:  
  
 SQL_TXN_READ_UNCOMMITTED = Dirty è possibili operazioni di lettura, letture non ripetibili e righe fantasma.  
  
 SQL_TXN_READ_COMMITTED = Dirty non sono consentite letture. Righe fantasma e letture non ripetibili è possibili.  
  
 SQL_TXN_REPEATABLE_READ = Dirty letture non ripetibili e letture non sono possibili. Righe fantasma è possibili.  
  
 SQL_TXN_SERIALIZABLE = le transazioni sono serializzabili. Le transazioni serializzabili non consentono letture dirty, letture non ripetibili o righe fantasma.  
  
 SQL_DESCRIBE_PARAMETER (ODBC 3.0)  
 Una stringa di caratteri: "Y" se i parametri possono essere descritti; "N", se non.  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà in genere "Y", perché sarà supportata la **DESCRIVONO INPUT** istruzione. Perché non si specifica direttamente il supporto SQL sottostante, tuttavia, che descrive i parametri potrebbero non essere supportato, anche in un driver di livello conforme allo standard SQL-92 completo.  
  
 SQL_DM_VER (ODBC 3.0)  
 Una stringa di caratteri con la versione di gestione Driver. La versione è nel formato # #. # #. # # #. # # #, dove:  
  
 Il primo set di due cifre è la versione ODBC principale, ottenuti tramite il SQL_SPEC_MAJOR costante.  
  
 Il secondo set di due cifre è la versione ODBC secondaria, come specificato da di SQL_SPEC_MINOR costante.  
  
 Il terzo set di quattro cifre è il numero di build principale di gestione Driver.  
  
 L'ultimo set di quattro cifre è il numero di build secondaria del Driver Manager.  
  
 La versione di gestione Driver di Windows 7 è 03.80. La versione di gestione Driver di Windows 8 è 03.81.  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 Un valore SQLUINTEGER che indica se il driver supporta il pool compatibile con il driver. (Per altre informazioni, vedere [Driver-Aware Connection Pooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE indica che il driver supporta meccanismo del pool di connessioni compatibile con il driver.  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE indica che il driver non supporta il meccanismo del pool di connessioni compatibile con il driver.  
  
 Un driver non è necessario implementare SQL_DRIVER_AWARE_POOLING_SUPPORTED e gestione Driver non verrà applicata al valore restituito del driver.  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV ODBC (1.0)  
 Un handle di ambiente o handle di connessione, determinata dall'argomento di valore SQLULEN, il driver *InfoType*.  
  
 Questi tipi di informazioni vengono implementati da Gestione Driver da solo.  
  
 SQL_DRIVER_HDESC (ODBC 3.0)  
 Valore di un SQLULEN, determinato dall'handle descrittore di gestione Driver, che deve essere passato in input nell'handle di descrittore del driver \* *InfoValuePtr* dall'applicazione. In questo caso *InfoValuePtr* entrambi un argomento di input e output. L'handle descrittore di input passati \* *InfoValuePtr* deve essere in modo implicito o esplicito allocato sul *ConnectionHandle*.  
  
 L'applicazione deve creare una copia del descrittore di gestione Driver di gestire prima di chiamare **SQLGetInfo** con questo tipo di informazioni, per assicurarsi che l'handle non è vengano sovrascritti nell'output.  
  
 Informazioni di questo tipo viene implementata da Gestione Driver da solo.  
  
 SQL_DRIVER_HLIB (ODBC 2.0)  
 Un valore SQLULEN, il *hinst* dalla libreria di carico restituite a gestione Driver quando caricata la DLL del driver in un sistema operativo Microsoft Windows, o equivalente in un altro sistema operativo. L'handle è valido solo per l'handle di connessione specificato nella chiamata a **SQLGetInfo**.  
  
 Informazioni di questo tipo viene implementata da Gestione Driver da solo.  
  
 SQL_DRIVER_HSTMT ODBC (1.0)  
 Valore un SQLULEN, determinato dall'handle di istruzione di gestione Driver, che deve essere passato in input nell'handle di istruzione del driver \* *InfoValuePtr* dall'applicazione. In questo caso *InfoValuePtr* sia un input e un argomento di output. L'handle di istruzione di input passati \* *InfoValuePtr* deve essere allocato in base all'argomento *ConnectionHandle*.  
  
 L'applicazione deve creare una copia dell'istruzione di gestione Driver gestire prima di chiamare **SQLGetInfo** con questo tipo di informazioni, per garantire che l'handle non è vengano sovrascritti nell'output.  
  
 Informazioni di questo tipo viene implementata da Gestione Driver da solo.  
  
 SQL_DRIVER_NAME ODBC (1.0)  
 Una stringa di caratteri con il nome del file del driver usato per accedere all'origine dati.  
  
 SQL_DRIVER_ODBC_VER (ODBC 2.0)  
 Una stringa di caratteri con la versione di ODBC supportate dal driver. La versione è nel formato # #. # #, dove le prime due cifre sono la versione principale e le due cifre sono la versione secondaria. SQL_SPEC_MAJOR e SQL_SPEC_MINOR definiscono i numeri di versione principale e secondaria. Per la versione di ODBC, descritta in questo manuale, si tratta dei 3 e 0, e il driver deve restituire "03.00".  
  
 Gestione Driver ODBC non modificherà il valore restituito di SQLGetInfo(SQL_DRIVER_ODBC_VER) per mantenere la compatibilità con le versioni precedenti per le applicazioni esistenti. Il driver specifica quale valore verrà restituito. Tuttavia, un driver che supporta l'estendibilità del tipo di dati C deve restituire 3,8 (o versione successiva) quando un'applicazione chiama **SQLSetEnvAttr** su cui impostare SQL_ATTR_ODBC_VERSION 3.8. Per altre informazioni, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 SQL_DRIVER_VER ODBC (1.0)  
 Una stringa di caratteri con la versione del driver e, facoltativamente, una descrizione del driver. Come minimo, la versione è nel formato # #. # #. # # #, dove le prime due cifre sono la versione principale, le due cifre sono la versione secondaria, mentre le ultime quattro cifre sono la versione di rilascio.  
  
 SQL_DROP_ASSERTION (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **ASSERZIONE DROP** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 La maschera di bit seguente viene usato per determinare quali clausole sono supportate:  
  
 SQL_DA_DROP_ASSERTION  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre questa opzione come supportato.  
  
 SQL_DROP_CHARACTER_SET (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **DROP SET di caratteri** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 La maschera di bit seguente viene usato per determinare quali clausole sono supportate:  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre questa opzione come supportato.  
  
 SQL_DROP_COLLATION (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **eliminare le regole di confronto** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 La maschera di bit seguente viene usato per determinare quali clausole sono supportate:  
  
 SQL_DC_DROP_COLLATION  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre questa opzione come supportato.  
  
 SQL_DROP_DOMAIN (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **DROP dominio** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 Un driver conforme a livello intermedio di SQL-92 restituirà sempre tutte queste opzioni supportate.  
  
 SQL_DROP_SCHEMA (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **DROP SCHEMA** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 Un driver conforme a livello intermedio di SQL-92 restituirà sempre tutte queste opzioni supportate.  
  
 SQL_DROP_TABLE (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **DROP TABLE** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 Un driver di livello conformi a FIPS transitorio restituirà sempre tutte queste opzioni supportate.  
  
 SQL_DROP_TRANSLATION (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **eliminare la traduzione** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 La maschera di bit seguente viene usato per determinare quali clausole sono supportate:  
  
 SQL_DTR_DROP_TRANSLATION  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre questa opzione come supportato.  
  
 SQL_DROP_VIEW (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **DROP VIEW** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 Un driver di livello conformi a FIPS transitorio restituirà sempre tutte queste opzioni supportate.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore dinamico che sono supportati dal driver. Questa maschera di bit contiene il subset prima degli attributi. per il sottoinsieme secondo, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES2.  
  
 Le maschere di bit seguenti vengono usate per determinare quali attributi sono supportati:  
  
 SQL_CA1_NEXT = oggetto *FetchOrientation* argomento di SQL_FETCH_NEXT è supportata in una chiamata a **SQLFetchScroll** quando il cursore si trova un cursore dinamico.  
  
 SQL_CA1_ABSOLUTE = *FetchOrientation* gli argomenti del SQL_FETCH_FIRST SQL_FETCH_LAST e SQL_FETCH_ABSOLUTE sono supportati in una chiamata a **SQLFetchScroll** quando il cursore si trova un cursore dinamico. (Il set di righe che verranno recuperati è indipendente dalla posizione corrente del cursore).  
  
 SQL_CA1_RELATIVE = *FetchOrientation* gli argomenti di SQL_FETCH_PRIOR e SQL_FETCH_RELATIVE sono supportati in una chiamata a **SQLFetchScroll** quando il cursore si trova un cursore dinamico. (Il set di righe che verranno recuperati dipende la posizione corrente del cursore. Si noti che questo è separato dal SQL_FETCH_NEXT perché in un cursore forward-only, è supportato solo SQL_FETCH_NEXT.)  
  
 SQL_CA1_BOOKMARK = oggetto *FetchOrientation* argomento impostato su sql_fetch_bookmark è supportato in una chiamata a **SQLFetchScroll** quando il cursore si trova un cursore dinamico.  
  
 SQL_CA1_LOCK_EXCLUSIVE = oggetto *LockType* argomento di SQL_LOCK_EXCLUSIVE è supportata in una chiamata a **SQLSetPos** quando il cursore si trova un cursore dinamico.  
  
 SQL_CA1_LOCK_NO_CHANGE = oggetto *LockType* argomento di SQL_LOCK_NO_CHANGE è supportata in una chiamata a **SQLSetPos** quando il cursore si trova un cursore dinamico.  
  
 SQL_CA1_LOCK_UNLOCK = oggetto *LockType* argomento di SQL_LOCK_UNLOCK è supportata in una chiamata a **SQLSetPos** quando il cursore si trova un cursore dinamico.  
  
 SQL_CA1_POS_POSITION = un' *operazione* argomento di SQL_POSITION è supportata in una chiamata a **SQLSetPos** quando il cursore si trova un cursore dinamico.  
  
 SQL_CA1_POS_UPDATE = un' *operazione* argomento di SQL_UPDATE è supportata in una chiamata a **SQLSetPos** quando il cursore si trova un cursore dinamico.  
  
 SQL_CA1_POS_DELETE = un' *operazione* argomento di SQL_DELETE è supportata in una chiamata a **SQLSetPos** quando il cursore si trova un cursore dinamico.  
  
 SQL_CA1_POS_REFRESH = un' *operazione* argomento di SQL_REFRESH è supportata in una chiamata a **SQLSetPos** quando il cursore si trova un cursore dinamico.  
  
 SQL_CA1_POSITIONED_UPDATE = An UPDATE in cui corrente di SQL istruzione è supportata quando il cursore si trova un cursore dinamico. (Un driver conforme a livello di SQL-92 voce restituirà sempre questa opzione come supportato.)  
  
 SQL_CA1_POSITIONED_DELETE = un'eliminazione in cui corrente di SQL istruzione è supportata quando il cursore si trova un cursore dinamico. (Un driver conforme a livello di SQL-92 voce restituirà sempre questa opzione come supportato.)  
  
 SQL_CA1_SELECT_FOR_UPDATE = un'istruzione SELECT per istruzione UPDATE SQL è supportato quando il cursore si trova un cursore dinamico. (Un driver conforme a livello di SQL-92 voce restituirà sempre questa opzione come supportato.)  
  
 SQL_CA1_BULK_ADD = un' *operazione* argomento di SQL_ADD è supportata in una chiamata a **SQLBulkOperations** quando il cursore si trova un cursore dinamico.  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK = un' *operazione* argomento di SQL_UPDATE_BY_BOOKMARK è supportata in una chiamata a **SQLBulkOperations** quando il cursore si trova un cursore dinamico.  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK = un' *operazione* argomento di SQL_DELETE_BY_BOOKMARK è supportata in una chiamata a **SQLBulkOperations** quando il cursore si trova un cursore dinamico.  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK = un' *operazione* argomento di SQL_FETCH_BY_BOOKMARK è supportata in una chiamata a **SQLBulkOperations** quando il cursore si trova un cursore dinamico.  
  
 Un driver conforme a livello intermedio di SQL-92 in genere restituisce le opzioni SQL_CA1_NEXT SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE supportato, perché supporta i cursori scorrevoli tramite l'istruzione SQL FETCH incorporata. Poiché questo non determinare direttamente il supporto SQL sottostante, tuttavia, i cursori scorrevoli potrebbero non essere supportati, anche per un driver conforme a livello intermedio di SQL-92.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore dinamico che sono supportati dal driver. Questa maschera di bit contiene il subset secondo degli attributi. per il subset prima, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1.  
  
 Le maschere di bit seguenti vengono usate per determinare quali attributi sono supportati:  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = sola lettura con cursori dinamici, in cui non sono consentiti aggiornamenti, sono supportato. (L'attributo di istruzione SQL_ATTR_CONCURRENCY può essere SQL_CONCUR_READ_ONLY per un cursore dinamico).  
  
 SQL_CA2_LOCK_CONCURRENCY = un cursore dinamico che usa il livello più basso di blocco sufficiente per assicurarsi che la riga può essere aggiornata è supportata. (L'attributo di istruzione SQL_ATTR_CONCURRENCY può essere SQL_CONCUR_LOCK per un cursore dinamico). Tali blocchi devono essere coerenti con il livello di isolamento impostato dall'attributo connessione SQL_ATTR_TXN_ISOLATION.  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = un cursore dinamico che usa la concorrenza ottimistica controllo confronto tra le versioni di riga è supportata. (L'attributo di istruzione SQL_ATTR_CONCURRENCY può essere SQL_CONCUR_ROWVER per un cursore dinamico).  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = un cursore dinamico che usa i valori di confronto del controllo della concorrenza ottimistica è supportata. (L'attributo di istruzione SQL_ATTR_CONCURRENCY può essere SQL_CONCUR_VALUES per un cursore dinamico).  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = sono state aggiunte le righe sono visibili a un cursore dinamico; il cursore è possibile scorrere a tali righe. (In cui queste righe vengono aggiunte al cursore è dipendente dal driver).  
  
 SQL_CA2_SENSITIVITY_DELETIONS = Deleted righe non sono più disponibili in un cursore dinamico e non lascino un' "area libera" nel set di risultati. Dopo che il cursore dinamico passa da una riga eliminata, non può restituire a tale riga.  
  
 SQL_CA2_SENSITIVITY_UPDATES = gli aggiornamenti alle righe sono visibili in un cursore dinamico; Se il cursore dinamico consente di scorrere da e restituisce una riga aggiornata, i dati restituiti dal cursore sono i dati aggiornati, non i dati originali.  
  
 SQL_CA2_MAX_ROWS_SELECT = SQL_ATTR_MAX_ROWS l'istruzione attributo influisce **seleziona** istruzioni quando il cursore si trova un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_INSERT = SQL_ATTR_MAX_ROWS l'istruzione attributo influisce **Inserisci** istruzioni quando il cursore si trova un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_DELETE = SQL_ATTR_MAX_ROWS l'istruzione attributo influisce **eliminare** istruzioni quando il cursore si trova un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_UPDATE = SQL_ATTR_MAX_ROWS l'istruzione attributo influisce **UPDATE** istruzioni quando il cursore si trova un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_CATALOG = SQL_ATTR_MAX_ROWS l'istruzione attributo influisce **catalogo** set di risultati quando il cursore si trova un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = SQL_ATTR_MAX_ROWS l'istruzione attributo influisce **selezionate**, **Inserisci**, **Elimina**, e **UPDATE** le istruzioni, e **catalogo** , set di risultati quando il cursore si trova un cursore dinamico.  
  
 SQL_CA2_CRC_EXACT = l'esatto numero di righe è disponibile nel campo di diagnostica SQL_DIAG_CURSOR_ROW_COUNT quando il cursore si trova un cursore dinamico.  
  
 SQL_CA2_CRC_APPROXIMATE = approssimativo un conteggio delle righe è disponibile nel campo di diagnostica SQL_DIAG_CURSOR_ROW_COUNT quando il cursore si trova un cursore dinamico.  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = il driver non garantisce che la simulazione posizionato update o istruzioni di eliminazione influirà solo una riga quando il cursore si trova un cursore dinamico; è responsabilità dell'applicazione per garantire questo. (Se un'istruzione interessa più righe, **SQLExecute** oppure **SQLExecDirect** restituisce SQLSTATE 01001 [conflitto dell'operazione del cursore].) Per impostare questo comportamento, l'applicazione chiama **SQLSetStmtAttr** con il SQL_ATTR_SIMULATE_CURSOR attributo impostato su SQL_SC_NON_UNIQUE.  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = il driver tenta di garantire che simulati per gli aggiornamenti posizionati o istruzioni di eliminazione influirà solo una riga quando il cursore si trova un cursore dinamico. Il driver esegue always tali istruzioni, anche se che potrebbero influire su più righe, ad esempio quando è presente alcuna chiave univoca. (Se un'istruzione interessa più righe, **SQLExecute** oppure **SQLExecDirect** restituisce SQLSTATE 01001 [conflitto dell'operazione del cursore].) Per impostare questo comportamento, l'applicazione chiama **SQLSetStmtAttr** con il SQL_ATTR_SIMULATE_CURSOR attributo impostato su SQL_SC_TRY_UNIQUE.  
  
 SQL_CA2_SIMULATE_UNIQUE = il driver garantisce che simulated posizionato update o istruzioni di eliminazione influirà solo una riga quando il cursore si trova un cursore dinamico. Se il driver non può garantire per una determinata istruzione **SQLExecDirect** oppure **SQLPrepare** restituisce SQLSTATE 01001 (conflitto dell'operazione del cursore). Per impostare questo comportamento, l'applicazione chiama **SQLSetStmtAttr** con il SQL_ATTR_SIMULATE_CURSOR attributo impostato su SQL_SC_UNIQUE.  
  
 SQL_EXPRESSIONS_IN_ORDERBY ODBC (1.0)  
 Una stringa di caratteri: "Y" se l'origine dati supporta le espressioni nel **ORDER BY** elencare; "N" Se non esiste.  
  
 SQL_FILE_USAGE (ODBC 2.0)  
 Un valore SQLUSMALLINT che indica il modo in cui un driver a un solo livello direttamente considera i file in un'origine dati:  
  
 SQL_FILE_NOT_SUPPORTED = il driver non è un driver a un solo livello. Ad esempio, un driver ORACLE è un driver a due livelli.  
  
 SQL_FILE_TABLE = un considera i driver a un solo livello file in un'origine dati come tabelle. Ad esempio, un driver Xbase considera ogni file Xbase come una tabella.  
  
 SQL_FILE_CATALOG = un considera i driver a un solo livello file in un'origine dati come un catalogo. Ad esempio, un driver Microsoft Access considera ogni file di Microsoft Access come un database completo.  
  
 Un'applicazione può utilizzare per determinare come gli utenti la selezione dei dati. Ad esempio, Xbase gli utenti spesso considerare i dati archiviati in file, mentre gli utenti di ORACLE e Microsoft Access in genere considerare i dati come archiviati nelle tabelle.  
  
 Quando un utente seleziona un'origine dati Xbase, l'applicazione è stato possibile visualizzare il Windows **Apri File** finestra di dialogo comune; quando l'utente seleziona un'origine dati Microsoft Access o da ORACLE, l'applicazione è stato possibile visualizzare un oggetto personalizzato  **Seleziona tabella** nella finestra di dialogo.  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore forward-only sono supportati dal driver. Questa maschera di bit contiene il subset prima degli attributi. per il sottoinsieme secondo, vedere SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2.  
  
 Le maschere di bit seguenti vengono usate per determinare quali attributi sono supportati:  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_ UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Per una descrizione di questi maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e sostituire "cursore forward-only" per "cursore dinamico" nelle descrizioni).  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore forward-only sono supportati dal driver. Questa maschera di bit contiene il subset secondo degli attributi. per il subset prima, vedere SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1.  
  
 Le maschere di bit seguenti vengono usate per determinare quali attributi sono supportati:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Per una descrizione di questi maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (e sostituire "cursore forward-only" per "cursore dinamico" nelle descrizioni).  
  
 SQL_GETDATA_EXTENSIONS (ODBC 2.0)  
 Maschera di bit SQLUINTEGER l'enumerazione delle estensioni **SQLGetData**.  
  
 Le maschere di bit seguenti vengono usati con il flag per determinare quali il driver supporta per le estensioni comuni **SQLGetData**:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData** può essere chiamato per tutte le colonne non associata, inclusi quelli prima che l'ultima colonna associata. Si noti che le colonne devono essere chiamate in ordine crescente numero di colonna, a meno che non viene restituito anche SQL_GD_ANY_ORDER.  
  
 SQL_GD_ANY_ORDER = **SQLGetData** possono essere chiamati per colonne non associate in qualsiasi ordine. Si noti che **SQLGetData** può essere chiamato solo per le colonne dopo l'ultima colonna associata, a meno che non viene restituito anche SQL_GD_ANY_COLUMN.  
  
 SQL_GD_BLOCK = **SQLGetData** può essere chiamato per una colonna non associata in qualsiasi riga in un blocco (in cui le dimensioni del set di righe sono maggiore di 1) dei dati dopo tale riga con il posizionamento **SQLSetPos**.  
  
 SQL_GD_BOUND = **SQLGetData** può essere chiamato per le colonne associate, oltre alle colonne non associate. Un driver non può restituire questo valore a meno che non restituisce inoltre SQL_GD_ANY_COLUMN.  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData** può essere chiamata per restituire i valori dei parametri output. Per altre informazioni, vedere [recupero di parametri di Output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
 **SQLGetData** è necessaria per restituire i dati solo da colonne non associate che si verificano dopo l'ultima colonna, associata vengono chiamati in ordine crescente numero di colonna e non sono in una riga in un blocco di righe.  
  
 Se un driver supporta segnalibri (a lunghezza fissa o a lunghezza variabile), deve supportare la chiamata **SQLGetData** sulla colonna 0. Questo supporto è richiesto indipendentemente dalla quali il driver restituisce per una chiamata a **SQLGetInfo** con il SQL_GETDATA_EXTENSIONS *InfoType*.  
  
 SQL_GROUP_BY (ODBC 2.0)  
 Un valore SQLUSMALLINT che specifica la relazione tra le colonne di **GROUP BY** clausola e le colonne non aggregate nell'elenco di selezione:  
  
 SQL_GB_COLLATE = oggetto **COLLATE** clausola può essere specificata alla fine di ogni colonna di raggruppamento. (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED = **GROUP BY** clausole non sono supportate. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = il **GROUP BY** clausola deve contenere tutte le colonne non aggregate nell'elenco di selezione. Non può contenere qualsiasi altra colonna. Ad esempio, **SELECT DEPT, MAX(SALARY) da dipendenti GROUP BY DEPT**. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = il **GROUP BY** clausola deve contenere tutte le colonne non aggregate nell'elenco di selezione. Può contenere colonne che non sono presenti nell'elenco di selezione. Ad esempio, **SELECT DEPT, MAX(SALARY) da dipendenti GROUP BY DEPT, età**. (ODBC 2.0)  
  
 SQL_GB_NO_RELATION = le colonne di **GROUP BY** clausola e l'elenco di selezione non sono correlate. Il significato delle colonne nongrouped, non aggregate nell'elenco di selezione è dipende dall'origine dati. Ad esempio, **SELECT DEPT, retribuzione da dipendente GROUP BY DEPT, età**. (ODBC 2.0)  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre l'opzione SQL_GB_GROUP_BY_EQUALS_SELECT supportato. Un driver di livello conforme allo standard SQL-92 completo restituirà sempre l'opzione SQL_GB_COLLATE supportato. Se nessuna delle opzioni è supportata, il **GROUP BY** clausola non è supportata dall'origine dati.  
  
 SQL_IDENTIFIER_CASE ODBC (1.0)  
 Un SQLUSMALLINT valore come indicato di seguito:  
  
 SQL_IC_UPPER = gli identificatori di SQL non sono tra maiuscole e minuscole e vengono archiviati in lettere maiuscole nel catalogo di sistema.  
  
 SQL_IC_LOWER = gli identificatori di SQL non sono tra maiuscole e minuscole e vengono archiviati in lettere minuscole nel catalogo di sistema.  
  
 SQL_IC_SENSITIVE = vengono memorizzati in minuscolo e maiuscolo nel catalogo di sistema e sono maiuscole / minuscole identificatori in SQL.  
  
 SQL_IC_MIXED = gli identificatori di SQL non sono tra maiuscole e minuscole e vengono archiviati in minuscolo e maiuscolo nel catalogo di sistema.  
  
 Perché non sono mai distinzione maiuscole/minuscole degli identificatori di SQL-92, un driver conforme strettamente a SQL-92 (qualsiasi livello) non restituisce mai l'opzione SQL_IC_SENSITIVE supportato.  
  
 SQL_IDENTIFIER_QUOTE_CHAR ODBC (1.0)  
 La stringa di caratteri che viene usata come delimitatore iniziale e finale di un tra virgolette (Separated Value) identificatore nelle istruzioni SQL. (Gli identificatori passati come argomenti alle funzioni ODBC non è necessario essere racchiusi tra virgolette). Se l'origine dati non supporta gli identificatori delimitati, viene restituito un valore vuoto.  
  
 Questa stringa di caratteri è anche utilizzabile per deve essere racchiuso tra gli argomenti della funzione catalogo quando l'attributo di connessione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE.  
  
 Poiché il carattere di virgoletta identificatore in SQL-92 è il segno di virgolette doppie ("), un driver conforme strettamente a SQL-92 restituirà sempre il carattere virgolette doppie.  
  
 SQL_INDEX_KEYWORDS (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le parole chiave nell'istruzione CREATE INDEX che sono supportate dal driver:  
  
 SQL_IK_NONE = nessuna delle parole chiave è supportata.  
  
 SQL_IK_ASC = ASC (parola chiave) è supportato.  
  
 SQL_IK_DESC = DESC (parola chiave) è supportato.  
  
 SQL_IK_ALL = tutte le parole chiave sono supportate.  
  
 Per vedere se l'istruzione CREATE INDEX è supportata, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_DLL_INDEX.  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione delle visualizzazioni nell'INFORMATION_SCHEMA supportate dal driver. Le viste in e il contenuto di INFORMATION_SCHEMA sono definite in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità è racchiusa tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono usate per determinare quali le viste sono supportate:  
  
 SQL_ISV_ASSERTIONS = identifica le asserzioni del catalogo che appartengono a un determinato utente. (Livello completo)  
  
 SQL_ISV_CHARACTER_SETS = identifica set di caratteri del catalogo che è possibile accedere a un determinato utente. (Livello intermedio)  
  
 SQL_ISV_CHECK_CONSTRAINTS = identifica il controllo di vincoli che appartengono a un determinato utente. (Livello intermedio)  
  
 SQL_ISV_COLLATIONS = identifica le regole di confronto carattere per il catalogo che è possibile accedere a un determinato utente. (Livello completo)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = identifica le colonne per il catalogo che dipendono da domini definiti nel catalogo e sono di proprietà di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_COLUMN_PRIVILEGES = identifica i privilegi sulle colonne delle tabelle persistenti che sono disponibili a o concessi da un determinato utente. (Livello transitorio FIPS)  
  
 SQL_ISV_COLUMNS = identifica le colonne delle tabelle persistenti che è possibile accedere a un determinato utente. (Livello transitorio FIPS)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = simile a CONSTRAINT_TABLE_USAGE-vista, le colonne vengono identificate per i vari vincoli che appartengono a un determinato utente. (Livello intermedio)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = identifica le tabelle utilizzate da vincoli (referenziali, unique e le asserzioni) e sono di proprietà di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = identifica i vincoli di dominio (dei domini nel catalogo) che è possibile accedere a un determinato utente. (Livello intermedio)  
  
 SQL_ISV_DOMAINS = identifica i domini definiti in un catalogo che sono accessibili dall'utente. (Livello intermedio)  
  
 SQL_ISV_KEY_COLUMN_USAGE = identifica le colonne definite nel catalogo sono vincolate come chiavi di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = identifica i vincoli referenziali che appartengono a un determinato utente. (Livello intermedio)  
  
 SQL_ISV_SCHEMATA = identifica gli schemi di proprietà di un determinato utente. (Livello intermedio)  
  
 SQL_ISV_SQL_LANGUAGES = identifica i livelli di conformità SQL, opzioni e i dialetti supportati dall'implementazione SQL. (Livello intermedio)  
  
 SQL_ISV_TABLE_CONSTRAINTS = identifica i vincoli di tabella che appartengono a un determinato utente. (Livello intermedio)  
  
 SQL_ISV_TABLE_PRIVILEGES = identifica i privilegi sulle tabelle permanenti che sono disponibili a o concessi da un determinato utente. (Livello transitorio FIPS)  
  
 SQL_ISV_TABLES = identifica le tabelle persistenti definite in un catalogo che è possibile accedere a un determinato utente. (Livello transitorio FIPS)  
  
 SQL_ISV_TRANSLATIONS = identifica conversioni dei caratteri per il catalogo che è possibile accedere a un determinato utente. (Livello completo)  
  
 SQL_ISV_USAGE_PRIVILEGES = identifica l'utilizzo di privilegi per gli oggetti del catalogo che sono disponibili o proprietà di un determinato utente. (Livello transitorio FIPS)  
  
 SQL_ISV_VIEW_COLUMN_USAGE = identifica le colonne in cui le viste del catalogo che appartengono a un determinato utente sono dipendenti. (Livello intermedio)  
  
 SQL_ISV_VIEW_TABLE_USAGE = identifica le tabelle in cui le viste del catalogo che appartengono a un determinato utente sono dipendenti. (Livello intermedio)  
  
 SQL_ISV_VIEWS = identifica le tabelle visualizzate definite in questo catalogo che è possibile accedere a un determinato utente. (Livello transitorio FIPS)  
  
 SQL_INSERT_STATEMENT (ODBC 3.0)  
 Maschera di bit che indica il supporto per SQLUINTEGER **Inserisci** istruzioni:  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre tutte queste opzioni supportate.  
  
 SQL_INTEGRITY ODBC (1.0)  
 Una stringa di caratteri: "Y" se l'origine dati supporta la funzionalità di miglioramento dell'integrità; "N" Se non esiste.  
  
 Ciò *InfoType* è stata rinominata per ODBC 3.0 da ODBC 2.0 *InfoType* SQL_ODBC_SQL_OPT_IEF.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore keyset sono supportati dal driver. Questa maschera di bit contiene il subset prima degli attributi. per il sottoinsieme secondo, vedere SQL_KEYSET_CURSOR_ATTRIBUTES2.  
  
 Le maschere di bit seguenti vengono usate per determinare quali attributi sono supportati:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Per una descrizione di questi maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e sostituire "gestito da keyset cursor" per "cursore dinamico" nelle descrizioni).  
  
 Un driver conforme a livello intermedio di SQL-92 in genere restituisce le opzioni SQL_CA1_NEXT SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE supportato, perché il driver supporta i cursori scorrevoli tramite l'istruzione SQL FETCH incorporata. Poiché questo non determinare direttamente il supporto SQL sottostante, tuttavia, i cursori scorrevoli potrebbero non essere supportati, anche per un driver conforme a livello intermedio di SQL-92.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore keyset sono supportati dal driver. Questa maschera di bit contiene il subset secondo degli attributi. per il subset prima, vedere SQL_KEYSET_CURSOR_ATTRIBUTES1.  
  
 Le maschere di bit seguenti vengono usate per determinare quali attributi sono supportati:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Per una descrizione di questi maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e sostituire "gestito da keyset cursor" per "cursore dinamico" nelle descrizioni).  
  
 SQL_KEYWORDS (ODBC 2.0)  
 Una stringa di caratteri che contiene un elenco delimitato da virgole di tutte le parole chiave specifiche dell'origine dati. Questo elenco non contiene parole chiave specifiche di ODBC o parole chiave usate da parte dell'origine dati e ODBC. Questo elenco rappresenta tutte le parole chiave riservate; applicazioni interoperative non utilizzare queste parole nei nomi degli oggetti.  
  
 Per un elenco di parole chiave ODBC, vedere [parole chiave riservate](../../../odbc/reference/appendixes/reserved-keywords.md) in [appendice c: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Il **#define** valore SQL_ODBC_KEYWORDS contiene un elenco delimitato da virgole di parole chiave ODBC.  
  
 Appendice C: Grammatica SQL  
  
 SQL_LIKE_ESCAPE_CLAUSE (ODBC 2.0)  
 Una stringa di caratteri: "Y" se l'origine dati supporta un carattere di escape per la percentuale di caratteri (%) e un carattere di sottolineatura (_) di caratteri una **, ad esempio** predicato e il driver supporta la sintassi ODBC per la definizione di un **, ad esempio** predicato carattere di escape. "N" in caso contrario.  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS (ODBC 3.0)  
 Un valore SQLUINTEGER che specifica il numero massimo di istruzioni simultanee attive in modalità asincrona in grado di supportare il driver in una determinata connessione. Se non esiste un limite specifico o il limite è sconosciuto, questo valore è zero.  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2.0)  
 Un valore SQLUINTEGER che specifica la lunghezza massima consentita (numero di caratteri esadecimali, esclusi il prefisso letterale e restituito dal suffisso **SQLGetTypeInfo**) del valore letterale binario in un'istruzione SQL. Ad esempio, il file binario 0xFFAA letterale ha una lunghezza pari a 4. Se è prevista una lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 SQL_MAX_CATALOG_NAME_LEN ODBC (1.0)  
 Un valore SQLUSMALLINT che specifica la lunghezza massima di un nome di catalogo nell'origine dati. Se è prevista una lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 Un driver di livello conformi a FIPS completo restituirà ad almeno 128.  
  
 Ciò *InfoType* è stata rinominata per ODBC 3.0 da ODBC 2.0 *InfoType* SQL_MAX_QUALIFIER_NAME_LEN.  
  
 SQL_MAX_CHAR_LITERAL_LEN (ODBC 2.0)  
 Un valore SQLUINTEGER che specifica la lunghezza massima consentita (numero di caratteri, esclusi il prefisso letterale e restituito dal suffisso **SQLGetTypeInfo**) di un carattere letterale in un'istruzione SQL. Se è prevista una lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 SQL_MAX_COLUMN_NAME_LEN ODBC (1.0)  
 Un valore SQLUSMALLINT che specifica la lunghezza massima di un nome di colonna nell'origine dati. Se è prevista una lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 Un driver di livello conformi a FIPS voce restituirà almeno 18. Un driver conforme a livello intermedio di FIPS restituirà ad almeno 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY (ODBC 2.0)  
 Un valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in una **GROUP BY** clausola. Se non esiste un limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Un driver di livello conformi a FIPS voce restituirà almeno 6. Un driver conforme a livello intermedio di FIPS restituirà almeno 15.  
  
 SQL_MAX_COLUMNS_IN_INDEX (ODBC 2.0)  
 Un valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in un indice. Se non esiste un limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY (ODBC 2.0)  
 Un valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in un **ORDER BY** clausola. Se non esiste un limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Un driver di livello conformi a FIPS voce restituirà almeno 6. Un driver conforme a livello intermedio di FIPS restituirà almeno 15.  
  
 SQL_MAX_COLUMNS_IN_SELECT (ODBC 2.0)  
 Un valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in un elenco di selezione. Se non esiste un limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Un driver di livello conformi a FIPS voce restituirà almeno pari a 100. Un driver conforme a livello intermedio di FIPS restituirà almeno 250.  
  
 SQL_MAX_COLUMNS_IN_TABLE (ODBC 2.0)  
 Un valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in una tabella. Se non esiste un limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Un driver di livello conformi a FIPS voce restituirà almeno pari a 100. Un driver conforme a livello intermedio di FIPS restituirà almeno 250.  
  
 SQL_MAX_CONCURRENT_ACTIVITIES ODBC (1.0)  
 Un valore SQLUSMALLINT che specifica il numero massimo di istruzioni attive in grado di supportare il driver per una connessione. Un'istruzione è definita come attivo se ha i risultati in sospeso, con il termine "risultati" significato le righe da un **seleziona** operazione o righe interessate da un' **inserire**, **UPDATE**, o **Eliminare** operazione (ad esempio, un conteggio delle righe) o se si trova in uno stato NEED_DATA. Questo valore può rispecchiare un limite imposto dal driver o l'origine dati. Se non esiste un limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Ciò *InfoType* è stata rinominata per ODBC 3.0 da ODBC 2.0 *InfoType* SQL_ACTIVE_STATEMENTS.  
  
 SQL_MAX_CURSOR_NAME_LEN ODBC (1.0)  
 Un valore SQLUSMALLINT che specifica la lunghezza massima di un nome di cursore nell'origine dati. Se è prevista una lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 Un driver di livello conformi a FIPS voce restituirà almeno 18. Un driver conforme a livello intermedio di FIPS restituirà ad almeno 128.  
  
 SQL_MAX_DRIVER_CONNECTIONS ODBC (1.0)  
 Un valore SQLUSMALLINT che specifica il numero massimo di connessioni attive in grado di supportare il driver per un ambiente. Questo valore può rispecchiare un limite imposto dal driver o l'origine dati. Se non esiste un limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Ciò *InfoType* è stata rinominata per ODBC 3.0 da ODBC 2.0 *InfoType* SQL_ACTIVE_CONNECTIONS.  
  
 SQL_MAX_IDENTIFIER_LEN (ODBC 3.0)  
 Un SQLUSMALLINT che indica la dimensione massima in caratteri che l'origine dati supporta per i nomi definiti dall'utente.  
  
 Un driver di livello conformi a FIPS voce restituirà almeno 18. Un driver conforme a livello intermedio di FIPS restituirà ad almeno 128.  
  
 SQL_MAX_INDEX_SIZE (ODBC 2.0)  
 Un valore SQLUINTEGER che specifica il numero massimo di byte consentiti nei campi di un indice combinati. Se non esiste un limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 SQL_MAX_PROCEDURE_NAME_LEN ODBC (1.0)  
 Un valore SQLUSMALLINT che specifica la lunghezza massima di un nome di procedure nell'origine dati. Se è prevista una lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 SQL_MAX_ROW_SIZE (ODBC 2.0)  
 Un valore SQLUINTEGER che specifica la lunghezza massima di una singola riga in una tabella. Se non esiste un limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Un driver di livello conformi a FIPS voce restituirà almeno 2.000. Un driver conforme a livello intermedio di FIPS restituirà almeno 8.000.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG (ODBC 3.0)  
 Una stringa di caratteri: "Y" se le dimensioni massime delle righe restituite per il tipo di informazioni SQL_MAX_ROW_SIZE include la lunghezza delle colonne di tutti i SQL_LONGVARBINARY e SQL_LONGVARCHAR nella riga. "N" in caso contrario.  
  
 SQL_MAX_SCHEMA_NAME_LEN ODBC (1.0)  
 Un valore SQLUSMALLINT che specifica la lunghezza massima di un nome di schema dell'origine dati. Se è prevista una lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 Un driver di livello conformi a FIPS voce restituirà almeno 18. Un driver conforme a livello intermedio di FIPS restituirà ad almeno 128.  
  
 Ciò *InfoType* è stata rinominata per ODBC 3.0 da ODBC 2.0 *InfoType* SQL_MAX_OWNER_NAME_LEN.  
  
 SQL_MAX_STATEMENT_LEN (ODBC 2.0)  
 Un valore SQLUINTEGER che specifica la lunghezza massima (numero di caratteri, tra cui lo spazio vuoto) di un'istruzione SQL. Se è prevista una lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 SQL_MAX_TABLE_NAME_LEN ODBC (1.0)  
 Un valore SQLUSMALLINT che specifica la lunghezza massima di un nome di tabella nell'origine dati. Se è prevista una lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 Un driver di livello conformi a FIPS voce restituirà almeno 18. Un driver conforme a livello intermedio di FIPS restituirà ad almeno 128.  
  
 SQL_MAX_TABLES_IN_SELECT (ODBC 2.0)  
 Un valore SQLUSMALLINT che specifica il numero massimo di tabelle consentito nel **FROM** clausola di un **seleziona** istruzione. Se non esiste un limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Un driver di livello conformi a FIPS voce restituirà almeno 15. Un driver conforme a livello intermedio di FIPS restituirà almeno 50.  
  
 SQL_MAX_USER_NAME_LEN (ODBC 2.0)  
 Un valore SQLUSMALLINT che specifica la lunghezza massima di un nome utente nell'origine dati. Se è prevista una lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 SQL_MULT_RESULT_SETS ODBC (1.0)  
 Una stringa di caratteri: "Y" se l'origine dati supporta più set di risultati, "N" Se non esiste.  
  
 Per altre informazioni su più set di risultati, vedere [più risultati](../../../odbc/reference/develop-app/multiple-results.md).  
  
 SQL_MULTIPLE_ACTIVE_TXN ODBC (1.0)  
 Una stringa di caratteri: "Y" se il driver supporta più di una transazione attiva allo stesso tempo, "N" se solo un'unica transazione può essere attiva in qualsiasi momento.  
  
 Le informazioni restituite per questo tipo di informazioni non sono applicabile nel caso di transazioni distribuite.  
  
 SQL_NEED_LONG_DATA_LEN (ODBC 2.0)  
 Una stringa di caratteri: In caso contrario, "Y" se l'origine dati deve la lunghezza di un valore di dati long (tipo di dati è SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo di dati specifici dell'origine dati di tipo long) prima di tale valore viene inviato all'origine dati, "N". Per altre informazioni, vedere [funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 SQL_NON_NULLABLE_COLUMNS ODBC (1.0)  
 Un valore SQLUSMALLINT che specifica se l'origine dati supporta NOT NULL nelle colonne:  
  
 SQL_NNC_NULL = tutte le colonne devono essere nullable.  
  
 SQL_NNC_NON_NULL = colonne non possono essere nullable. (L'origine dati supporta la **non è NULL** vincolo di colonna in **CREATE TABLE** istruzioni.)  
  
 Un driver conforme a livello di SQL-92 voce restituirà SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION (ODBC 2.0)  
 Un valore SQLUSMALLINT che specifica in cui i valori null vengono ordinati in un set di risultati:  
  
 SQL_NC_END = i valori null vengono posizionati alla fine del set di risultati, indipendentemente dalle parole chiave ASC o DESC.  
  
 SQL_NC_HIGH = i valori null vengono posizionati alla parte superiore del set di risultati, a seconda delle parole chiave ASC o DESC.  
  
 SQL_NC_LOW = vengono ordinati i valori null nella parte inferiore del set di risultati, a seconda delle parole chiave ASC o DESC.  
  
 SQL_NC_START = i valori null vengono posizionati all'inizio del set di risultati, indipendentemente dalle parole chiave ASC o DESC.  
  
 SQL_NUMERIC_FUNCTIONS ODBC (1.0)  
 Nota: Il tipo di informazioni è stata introdotta in ODBC 1.0; ogni maschera di bit viene etichettato con la versione in cui è stato introdotto in.  
  
 Maschera di bit SQLUINTEGER l'enumerazione le funzioni numeriche scalari supportate dal driver e origine dati associata.  
  
 Le maschere di bit seguenti vengono usate per determinare quali funzioni numeriche sono supportate:  
  
 SQL_FN_NUM_ABS (ODBC 1.0) SQL_FN_NUM_ACOS (ODBC 1.0) SQL_FN_NUM_ASIN (ODBC 1.0) SQL_FN_NUM_ATAN (ODBC 1.0) SQL_FN_NUM_ATAN2 SQL _ SQL_FN_NUM_DEGREES (ODBC 2.0) SQL_FN_NUM_COT (ODBC 1.0) DI (ODBC 1.0) SQL_FN_NUM_CEILING (ODBC 1.0) SQL_FN_NUM_COS (ODBC 1.0) FN_NUM_EXP (ODBC 1.0) SQL_FN_NUM_FLOOR (ODBC 1.0) SQL_FN_NUM_LOG (ODBC 1.0) SQL_FN_NUM_LOG10 SQL_FN_ SQL_FN_NUM_RAND (ODBC 1.0) DI (ODBC 2.0) SQL_FN_NUM_MOD (ODBC 1.0) SQL_FN_NUM_PI (ODBC 1.0) SQL_FN_NUM_POWER (ODBC 2.0) SQL_FN_NUM_RADIANS (ODBC 2.0) NUM_ROUND (ODBC 2.0) SQL_FN_NUM_SIGN (ODBC 1.0) SQL_FN_NUM_SIN (ODBC 1.0) SQL_FN_NUM_SQRT (ODBC 1.0) SQL_FN_NUM_TAN (ODBC 1.0) SQL_FN_NUM_TRUNCATE (ODBC 2.0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE (ODBC 3.0)  
 Un valore SQLUINTEGER che indica il livello di 3 ODBC*x* interfaccia che il driver conforme.  
  
 SQL_OIC_CORE: Il livello minimo di tutti i driver ODBC sono previsti per la conformità con. Questo livello include gli elementi di interfaccia di base, ad esempio le funzioni di connessione, le funzioni per la preparazione e l'esecuzione di un'istruzione SQL, funzioni dei metadati di set di risultati di base, le funzioni di catalogo di base e così via.  
  
 SQL_OIC_LEVEL1: Un livello tra i segnalibri funzionalità a livello di conformità agli standard, nonché cursori scorrevoli, core, posizionati Aggiorna e consente di eliminare e così via.  
  
 SQL_OIC_LEVEL2: Un livello tra cui funzionalità a livello di livello 1 standard conformità, oltre a funzionalità avanzate come i cursori sensibili; aggiornare, eliminare e aggiornare i segnalibri; supporto delle stored procedure; funzioni di catalogo per le chiavi primarie ed esterne; Supporto multi-catalogo. E così via.  
  
 Per altre informazioni, vedere [livelli di conformità di interfaccia](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 SQL_ODBC_VER ODBC (1.0)  
 Una stringa di caratteri con la versione di a cui è conforme in Gestione Driver ODBC. La versione è nel formato # #. # #. 0000, in cui le prime due cifre sono la versione principale e le due cifre sono la versione secondaria. Viene implementato solo in Gestione Driver.  
  
 SQL_OJ_CAPABILITIES (ODBC 2.01)  
 Maschera di bit SQLUINTEGER l'enumerazione dei tipi di outer join supportati dall'origine dati e driver. Le maschere di bit seguenti vengono usate per determinare i tipi supportati:  
  
 SQL_OJ_LEFT = Left outer join sono supportati.  
  
 SQL_OJ_RIGHT = Right outer join sono supportati.  
  
 SQL_OJ_FULL = Full outer join sono supportati.  
  
 SQL_OJ_NESTED = Nested outer join sono supportati.  
  
 SQL_OJ_NOT_ORDERED = nomi nella clausola ON di outer join non devono essere nello stesso ordine in cui i nomi di tabella corrispondente nella colonna il **OUTER JOIN** clausola.  
  
 SQL_OJ_INNER = interna tabella (tabella di destra in un left outer join) o tabella di sinistra in un right outer join può essere utilizzata anche in un inner join. Ciò non si applica a full outer join, che non dispongono di una tabella interna.  
  
 SQL_OJ_ALL_COMPARISON_OPS = il confronto nella clausola ON può essere uno degli operatori di confronto di ODBC. Se questo bit non è impostato, solo l'operatore di confronto di uguaglianza (=) è utilizzabile nei outer join.  
  
 Se nessuna di queste opzioni viene restituita come supportato, non esiste una clausola outer join è supportata.  
  
 Per informazioni sul supporto degli operatori di join relazionale in un'istruzione SELECT, come definito da SQL-92, vedere SQL_SQL92_RELATIONAL_JOIN_OPERATORS.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT (ODBC 2.0)  
 Una stringa di caratteri: "Y" se le colonne di **ORDER BY** clausola deve essere nell'elenco di selezione; in caso contrario, "N".  
  
 SQL_PARAM_ARRAY_ROW_COUNTS (ODBC 3.0)  
 I conteggi di un SQLUINTEGER enumerare le proprietà del driver riguardanti la disponibilità di riga in un'esecuzione con parametri. Presenta i seguenti valori:  
  
 SQL_PARC_BATCH = individuale i conteggi delle righe sono disponibili per ogni set di parametri. Ciò equivale a livello concettuale per il driver genera un batch di istruzioni SQL, uno per ogni parametro impostato nella matrice. Informazioni estese sull'errore può essere recuperato tramite il campo di descrizione SQL_PARAM_STATUS_PTR.  
  
 SQL_PARC_NO_BATCH = solo una riga il numero è disponibile, ovvero il numero di righe cumulative risultanti dall'esecuzione dell'istruzione per l'intera matrice di parametri. Ciò equivale a livello concettuale a trattare l'istruzione con la matrice di parametri completo come un'unica unità atomica. Gli errori vengono gestiti come se venisse eseguita un'istruzione.  
  
 SQL_PARAM_ARRAY_SELECTS (ODBC 3.0)  
 Un SQLUINTEGER enumerare le proprietà del driver riguardanti la disponibilità del risultato imposta durante l'esecuzione con parametri. Presenta i seguenti valori:  
  
 SQL_PAS_BATCH = è un set di risultati disponibile per ogni set di parametri. Ciò equivale a livello concettuale per il driver genera un batch di istruzioni SQL, uno per ogni parametro impostato nella matrice.  
  
 SQL_PAS_NO_BATCH = è un solo set di risultati disponibile, che rappresenta il risultato cumulativo set risultante dall'esecuzione dell'istruzione per la matrice completa dei parametri. Ciò equivale a livello concettuale a trattare l'istruzione con la matrice di parametri completo come un'unica unità atomica.  
  
 SQL_PAS_NO_SELECT = un driver non supporta un'istruzione di generazione di set di risultati deve essere eseguito con una matrice di parametri.  
  
 SQL_PROCEDURE_TERM ODBC (1.0)  
 Una stringa di caratteri con il nome del fornitore di origine dati per una routine. ad esempio, "procedura di database", "stored procedure", "procedure", "package" o "query archiviata".  
  
 SQL_PROCEDURES ODBC (1.0)  
 Una stringa di caratteri: "Y" se l'origine dati supporta le procedure e il driver supporta la sintassi di chiamata di procedura ODBC; "N" in caso contrario.  
  
 SQL_POS_OPERATIONS (ODBC 2.0)  
 Una maschera di bit SQLINTEGER le operazioni di supporto nell'enumerazione **SQLSetPos**.  
  
 Le maschere di bit seguenti vengono utilizzati con il flag per determinare quali opzioni sono supportate.  
  
 SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE (ODBC 2.0)  
 Un SQLUSMALLINT valore come indicato di seguito:  
  
 SQL_IC_UPPER = tra virgolette gli identificatori di SQL non sono tra maiuscole e minuscole e vengono archiviati in lettere maiuscole nel catalogo di sistema.  
  
 SQL_IC_LOWER = tra virgolette gli identificatori di SQL non sono tra maiuscole e minuscole e vengono archiviati in lettere minuscole nel catalogo di sistema.  
  
 SQL_IC_SENSITIVE = tra virgolette gli identificatori di SQL sono tra maiuscole e minuscole e vengono archiviati in minuscolo e maiuscolo nel catalogo di sistema. (In un database compatibile con SQL-92, gli identificatori tra virgolette sono sempre distinzione maiuscole/minuscole).  
  
 SQL_IC_MIXED = tra virgolette gli identificatori di SQL non sono tra maiuscole e minuscole e vengono archiviati in minuscolo e maiuscolo nel catalogo di sistema.  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre SQL_IC_SENSITIVE.  
  
 SQL_ROW_UPDATES ODBC (1.0)  
 Una stringa di caratteri: "Y" se un cursore keyset o misto gestisce le versioni delle righe o valori per tutte le righe recuperate e pertanto può rilevare gli aggiornamenti che sono stato apportati a una riga da qualsiasi utente, poiché l'ultima operazione di recupero. (Si applica solo agli aggiornamenti, non per eliminazioni o inserimenti). Il driver può restituire il flag SQL_ROW_UPDATED allo stato della riga di matrice quando **SQLFetchScroll** viene chiamato. In caso contrario, "N".  
  
 SQL_SCHEMA_TERM ODBC (1.0)  
 Una stringa di caratteri con il nome del fornitore di origine dati per uno schema. ad esempio, "proprietario", "ID autorizzazione" o "Schema".  
  
 La stringa di caratteri può essere restituita in caso di superiore, inferiore o misto.  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre "schema".  
  
 Ciò *InfoType* è stata rinominata per ODBC 3.0 da ODBC 2.0 *InfoType* SQL_OWNER_TERM.  
  
 SQL_SCHEMA_USAGE (ODBC 2.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le istruzioni in cui gli schemi possono essere utilizzati:  
  
 SQL_SU_DML_STATEMENTS = gli schemi sono supportati in tutte le istruzioni Data Manipulation Language: **Selezionare**, **inserire**, **aggiornare**, **eliminare**e, se supportato **selezionare per aggiornare** e l'eliminazione e aggiornamento posizionato istruzioni.  
  
 SQL_SU_PROCEDURE_INVOCATION = gli schemi sono supportati nell'istruzione ODBC procedure chiamata.  
  
 SQL_SU_TABLE_DEFINITION = gli schemi sono supportati in tutte le istruzioni di definizione di tabella: **Crea tabella**, **Crea vista**, **ALTER TABLE**, **DROP TABLE**, e **DROP VIEW**.  
  
 SQL_SU_INDEX_DEFINITION = gli schemi sono supportati in tutte le istruzioni di definizione di indice: **Crea indice** e **DROP INDEX**.  
  
 SQL_SU_PRIVILEGE_DEFINITION = gli schemi sono supportati in tutte le istruzioni di definizione dei privilegi: **CONCESSIONE** e **revocare**.  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre le opzioni SQL_SU_DML_STATEMENTS SQL_SU_TABLE_DEFINITION e SQL_SU_PRIVILEGE_DEFINITION, come supportato.  
  
 Ciò *InfoType* è stata rinominata per ODBC 3.0 da ODBC 2.0 *InfoType* SQL_OWNER_USAGE.  
  
 SQL_SCROLL_OPTIONS ODBC (1.0)  
 Nota: Il tipo di informazioni è stata introdotta in ODBC 1.0; ogni maschera di bit viene etichettato con la versione in cui è stato introdotto in.  
  
 Maschera di bit SQLUINTEGER l'enumerazione le opzioni di scorrimento supportate per i cursori scorrevoli.  
  
 Le maschere di bit seguenti vengono usate per determinare quali opzioni sono supportate:  
  
 SQL_SO_FORWARD_ONLY = il cursore solo scorre verso il rollforward. ODBC (1.0)  
  
 SQL_SO_STATIC = i dati nel risultato del set è statico. (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN = Salva i driver e Usa le chiavi per ogni riga nel set di risultati. ODBC (1.0)  
  
 SQL_SO_DYNAMIC = mantiene il driver le chiavi per ogni riga nel set di righe (la dimensione del keyset è lo stesso come il set di righe di dimensioni). ODBC (1.0)  
  
 SQL_SO_MIXED = il driver mantiene le chiavi per ogni riga nel keyset e la dimensione del keyset è maggiore della dimensione del set di righe. Il cursore è gestito da keyset all'interno di keyset e dinamici all'esterno di keyset. ODBC (1.0)  
  
 Per informazioni sui cursori scorrevoli, vedere [cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 SQL_SEARCH_PATTERN_ESCAPE ODBC (1.0)  
 Una stringa di caratteri che specifica ciò che il driver supporta come carattere di escape che consente di usare il criterio match metacaratteri sottolineatura (_) e segno di percentuale (%) come caratteri validi in Criteri di ricerca. Questo carattere di escape si applica solo a tali argomenti delle funzioni del catalogo che supportano le stringhe di ricerca. Se questa stringa è vuota, il driver non supporta un carattere di escape di criterio di ricerca.  
  
 Poiché questo tipo di informazioni non indica il supporto generale del carattere di escape di **, ad esempio** predicato, SQL-92 non prevedono requisiti per questa stringa di caratteri.  
  
 Ciò *InfoType* è limitato alle funzioni di catalogo. Per una descrizione dell'uso del carattere di escape nelle stringhe di modello di ricerca, vedere [argomenti del valore criterio](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
 SQL_SERVER_NAME ODBC (1.0)  
 Una stringa di caratteri con il nome di server specifici dell'origine dei dati effettivi. utile quando un nome dell'origine dati viene usato durante **SQLConnect**, **SQLDriverConnect**, e **SQLBrowseConnect**.  
  
 SQL_SPECIAL_CHARACTERS (ODBC 2.0)  
 Una stringa di caratteri che contiene tutti i caratteri speciali (vale a dire, tutti i caratteri eccetto alla z, alla Z, da 0 a 9 e caratteri di sottolineatura) che possono essere utilizzati in un nome di identificatore, ad esempio un nome di tabella, nome della colonna o nome dell'indice, nell'origine dati. Ad esempio, "#$^". Se un identificatore contiene uno o più di questi caratteri, l'identificatore deve essere un identificatore delimitato.  
  
 SQL_SQL_CONFORMANCE (ODBC 3.0)  
 Un valore SQLUINTEGER che indica il livello di SQL-92 supportate dal driver:  
  
 SQL_SC_SQL92_ENTRY = voce livello SQL-92 conformi.  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = FIPS 127-2 transitorio level conformi.  
  
 SQL_SC_SQL92_FULL = completa a livello di SQL-92.  
  
 SQL_SC_ SQL92_INTERMEDIATE = intermedi a livello SQL-92 conformi.  
  
 SQL_SQL92_DATETIME_FUNCTIONS(ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le funzioni scalari datetime supportati dal driver e l'origine dati associata, come definito in SQL-92.  
  
 Le maschere di bit seguenti vengono usate per determinare quali funzioni di data/ora sono supportate:  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE(ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione di regole supportate per un vincolo foreign key in una **eliminare** istruzione, come definito in SQL-92.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate dall'origine dati:  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 Un driver di livello conformi a FIPS transitorio restituirà sempre tutte queste opzioni supportate.  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione di regole supportate per una chiave esterna in un' **UPDATE** istruzione, come definito in SQL-92.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate dall'origine dati:  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 Un driver di livello conforme allo standard SQL-92 completo restituirà sempre tutte queste opzioni supportate.  
  
 SQL_SQL92_GRANT(ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole supportate nel **Concedi** istruzione, come definito in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità è racchiusa tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate dall'origine dati:  
  
 (SQL_SG_INSERT_COLUMN (livello intermedio) SQL_SG_INSERT_TABLE (Entry level) SQL_SG_REFERENCES_TABLE (Entry level) SQL_SG_REFERENCES_COLUMN (Entry level) SQL_SG_SELECT_TABLE (Entry level) SQL_SG_UPDATE_COLUMN SQL_SG_DELETE_TABLE (Entry level) Entry level) SQL_SG_UPDATE_TABLE (Entry level) SQL_SG_USAGE_ON_DOMAIN (livello FIPS transitorio) SQL_SG_USAGE_ON_CHARACTER_SET (livello FIPS transitorio) SQL_SG_USAGE_ON_COLLATION (livello FIPS transitorio) SQL_SG_USAGE_ON_TRANSLATION FIPS (FEDERAL Livello transitorio) SQL_SG_WITH_GRANT_OPTION (Entry level)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS(ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le funzioni scalari valore numerico che sono supportate dal driver e l'origine dati associata, come definito in SQL-92.  
  
 Le maschere di bit seguenti vengono usate per determinare quali funzioni numeriche sono supportate:  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione dei predicati supportati in un' **seleziona** istruzione, come definito in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità è racchiusa tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono usate per determinare quali opzioni sono supportate dall'origine dati:  
  
 SQL_SP_BETWEEN (Entry level) SQL_SP_COMPARISON (Entry level) SQL_SP_EXISTS (Entry level) SQL_SP_IN (Entry level) SQL_SP_ISNOTNULL (Entry level) SQL_SP_ISNULL (Entry level) SQL_SP_LIKE (Entry level) SQL_SP_MATCH_FULL (livello completo) SQL_SP_MATCH_PARTIAL (Livello completo) SQL_SP_MATCH_UNIQUE_FULL (livello completo) SQL_SP_MATCH_UNIQUE_PARTIAL (livello completo) SQL_SP_OVERLAPS (livello FIPS transitorio) SQL_SP_QUANTIFIED_COMPARISON (Entry level) SQL_SP_UNIQUE (Entry level)  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS(ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione gli operatori di join relazionale supportati un' **seleziona** istruzione, come definito in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità è racchiusa tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono usate per determinare quali opzioni sono supportate dall'origine dati:  
  
 SQL_SRJO_CORRESPONDING_CLAUSE (livello intermedio) SQL_SRJO_CROSS_JOIN (livello completo) SQL_SRJO_EXCEPT_JOIN (livello intermedio) SQL_SRJO_FULL_OUTER_JOIN (livello intermedio) SQL_SRJO_INNER_JOIN (livello FIPS transitorio) SQL_SRJO_INTERSECT_JOIN (Livello intermedio) SQL_SRJO_LEFT_OUTER_JOIN (livello FIPS transitorio) SQL_SRJO_NATURAL_JOIN (livello FIPS transitorio) SQL_SRJO_RIGHT_OUTER_JOIN (livello FIPS transitorio) SQL_SRJO_UNION_JOIN (livello completo)  
  
 SQL_SRJO_INNER_JOIN indica il supporto per la **INNER JOIN** sintassi, non per la funzionalità di join interna. Supporto per la **INNER JOIN** sintassi è transitorio FIPS, mentre il supporto per la funzionalità di join interna **voce**.  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole supportate nel **revocare** istruzione, come definito in SQL-92, supportati dall'origine dati.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità è racchiusa tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate dall'origine dati:  
  
 SQL_SR_CASCADE (livello FIPS transitorio) SQL_SR_DELETE_TABLE (Entry level) SQL_SR_GRANT_OPTION_FOR (livello intermedio) SQL_SR_INSERT_COLUMN (livello intermedio) SQL_SR_INSERT_TABLE (Entry level) SQL_SR_REFERENCES_COLUMN (Entry level) SQL_SR_ REFERENCES_TABLE (Entry level) SQL_SR_RESTRICT (livello FIPS transitorio) SQL_SR_SELECT_TABLE (Entry level) SQL_SR_UPDATE_COLUMN (Entry level) SQL_SR_UPDATE_TABLE (Entry level) SQL_SR_USAGE_ON_DOMAIN (livello FIPS transitorio) SQL_SR_USAGE_ON_ SQL_SR_USAGE_ON_TRANSLATION SQL_SR_USAGE_ON_COLLATION (livello FIPS transitorio) CHARACTER_SET (livello FIPS transitorio) (livello transitorio FIPS)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le espressioni di costruttore di valore di riga è supportate in un **seleziona** istruzione, come definito in SQL-92. Le maschere di bit seguenti vengono usate per determinare quali opzioni sono supportate dall'origine dati:  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS(ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le funzioni scalari di stringa supportate dal driver e l'origine dati associata, come definito in SQL-92.  
  
 Le maschere di bit seguenti vengono usate per determinare le funzioni di stringa supportate:  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le espressioni valore supportate, come definito in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità è racchiusa tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono usate per determinare quali opzioni sono supportate dall'origine dati:  
  
 SQL_SVE_CASE (livello intermedio) SQL_SVE_CAST (livello FIPS transitorio) SQL_SVE_COALESCE (livello intermedio) SQL_SVE_NULLIF (livello intermedio)  
  
 SQL_STANDARD_CLI_CONFORMANCE (ODBC 3.0)  
 Maschera di bit SQLUINTEGER enumerazione standard dell'interfaccia della riga o standard a cui il driver conforme. Le maschere di bit seguenti vengono usate per determinare quali il driver conforme con i livelli:  
  
 SQL_SCC_XOPEN_CLI_VERSION1: Il driver conforme con la CLI di gruppo aprire la versione 1.  
  
 SQL_SCC_ISO92_CLI: Il driver conforme con ISO 92 CLI.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore statico che sono supportati dal driver. Questa maschera di bit contiene il subset prima degli attributi. per il sottoinsieme secondo, vedere SQL_STATIC_CURSOR_ATTRIBUTES2.  
  
 Le maschere di bit seguenti vengono usate per determinare quali attributi sono supportati:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Per una descrizione di questi maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e sostituire "cursore statico" per "cursore dinamico" nelle descrizioni).  
  
 Un driver conforme a livello intermedio di SQL-92 in genere restituisce le opzioni SQL_CA1_NEXT SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE supportato, perché il driver supporta i cursori scorrevoli tramite l'istruzione SQL FETCH incorporata. Poiché questo non determinare direttamente il supporto SQL sottostante, tuttavia, i cursori scorrevoli potrebbero non essere supportati, anche per un driver conforme a livello intermedio di SQL-92.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore statico che sono supportati dal driver. Questa maschera di bit contiene il subset secondo degli attributi. per il subset prima, vedere SQL_STATIC_CURSOR_ATTRIBUTES1.  
  
 Le maschere di bit seguenti vengono usate per determinare quali attributi sono supportati:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Per una descrizione di questi maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (e sostituire "cursore statico" per "cursore dinamico" nelle descrizioni).  
  
 SQL_STRING_FUNCTIONS ODBC (1.0)  
 Nota: Il tipo di informazioni è stata introdotta in ODBC 1.0; ogni maschera di bit viene etichettato con la versione in cui è stato introdotto in.  
  
 Maschera di bit SQLUINTEGER l'enumerazione le funzioni di stringa scalare supportate dal driver e origine dati associata.  
  
 Le maschere di bit seguenti vengono usate per determinare le funzioni di stringa supportate:  
  
 SQL_FN_STR_ASCII (ODBC 1.0) SQL_FN_STR_BIT_LENGTH (ODBC 3.0) SQL_FN_STR_CHAR (ODBC 1.0) SQL_FN_STR_CHAR_LENGTH (ODBC 3.0) SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0) SQL_FN_STR_CONCAT (ODBC 1.0) SQL_FN_STR_DIFFERENCE (ODBC 2.0) SQL_FN_STR_INSERT (ODBC 1.0) SQL_FN_STR_LCASE (ODBC 1.0) SQL_FN_STR_LEFT (ODBC 1.0) SQL_FN_STR_LENGTH (ODBC 1.0) SQL_FN_STR_LOCATE (ODBC 1.0) SQL_FN_STR_LTRIM (ODBC 1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0) SQL_FN_STR_REPEAT (ODBC 1.0) SQL_FN_ STR_REPLACE (ODBC 1.0) SQL_FN_STR_RIGHT (ODBC 1.0) SQL_FN_STR_RTRIM (ODBC 1.0) SQL_FN_STR_SOUNDEX (ODBC 2.0) SQL_FN_STR_SPACE (ODBC 2.0) SQL_FN_STR_SUBSTRING (ODBC 1.0) SQL_FN_STR_UCASE (ODBC 1.0)  
  
 Se un'applicazione può chiamare le **LOCATE** funzione scalare con la *string_exp1*, *string_exp2 e*, e *avviare* argomenti, il driver Restituisce la maschera di bit SQL_FN_STR_LOCATE. Se un'applicazione può chiamare la funzione scalare INDIVIDUA solo con il *string_exp1* e *string_exp2 e* argomenti, il driver restituisce la maschera di bit SQL_FN_STR_LOCATE_2. I driver che supportano completamente il **INDIVIDUA** funzioni scalari restituiscono entrambi maschere di bit.  
  
 (Per altre informazioni, vedere [funzioni stringa](../../../odbc/reference/appendixes/string-functions.md) nell'appendice e "funzioni scalari.")  
  
 SQL_SUBQUERIES (ODBC 2.0)  
 Maschera di bit SQLUINTEGER l'enumerazione i predicati che supportano le sottoquery:  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 La maschera di bit SQL_SQ_CORRELATED_SUBQUERIES indica che tutti i predicati che supportano le sottoquery supportano sottoquery correlate.  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre una maschera di bit in cui tutti questi bit vengono impostati.  
  
 SQL_SYSTEM_FUNCTIONS ODBC (1.0)  
 Maschera di bit SQLUINTEGER l'enumerazione di funzioni di sistema scalari supportate dal driver e origine dati associata.  
  
 Le maschere di bit seguenti vengono usate per determinare le funzioni di sistema supportate:  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM ODBC (1.0)  
 Una stringa di caratteri con il nome del fornitore di origine dati per una tabella. ad esempio, "table" o "file".  
  
 Questa stringa di caratteri possibile in caso di superiore, inferiore o misto.  
  
 Un driver conforme a livello di SQL-92 voce verrà sempre restituito "table".  
  
 SQL_TIMEDATE_ADD_INTERVALS (ODBC 2.0)  
 Maschera di bit SQLUINTEGER l'enumerazione supportati dal driver e origine dati associata per la funzione scalare timestampadd non gli intervalli di timestamp.  
  
 Le maschere di bit seguenti vengono usate per determinare quali intervalli sono supportati:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Un driver di livello conformi a FIPS transitorio restituirà sempre una maschera di bit in cui tutti questi bit vengono impostati.  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2.0)  
 Maschera di bit SQLUINTEGER l'enumerazione supportati dal driver e origine dati associata per la funzione scalare timestampdiff non gli intervalli di timestamp.  
  
 Le maschere di bit seguenti vengono usate per determinare quali intervalli sono supportati:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Un driver di livello conformi a FIPS transitorio restituirà sempre una maschera di bit in cui tutti questi bit vengono impostati.  
  
 SQL_TIMEDATE_FUNCTIONS ODBC (1.0)  
 Nota: Il tipo di informazioni è stata introdotta in ODBC 1.0; ogni maschera di bit viene etichettato con la versione in cui è stato introdotto in.  
  
 Maschera di bit SQLUINTEGER l'enumerazione di scalare funzioni di data e ora supportate dal driver e origine dati associata.  
  
 Le maschere di bit seguenti vengono usate per determinare quali funzioni di data e ora sono supportate:  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0) SQL_FN_TD_CURRENT_TIME (ODBC 3.0) SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) SQL_FN_TD_CURDATE (ODBC 1.0) SQL_FN_TD_CURTIME (ODBC 1.0) SQL_FN_TD_DAYNAME (ODBC 2.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0) (SQL_FN_TD_DAYOFWEEK ODBC 1.0) SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_EXTRACT (ODBC 3.0) SQL_FN_TD_HOUR (ODBC 1.0) SQL_FN_TD_MINUTE (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTHNAME (ODBC 2.0) SQL_FN_TD_NOW (ODBC 1.0) SQL_FN_TD_QUARTER (ODBC 1.0) SQL_FN_TD_ SECONDO (ODBC 1.0) SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) SQL_FN_TD_WEEK (ODBC 1.0) SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE ODBC (1.0)  
 Nota: Il tipo di informazioni è stata introdotta in ODBC 1.0; ogni valore restituito viene etichettato con la versione in cui è stato introdotto in.  
  
 Un valore SQLUSMALLINT che descrive il supporto delle transazioni nell'origine dati o driver:  
  
 SQL_TC_NONE = transazioni non supportate. ODBC (1.0)  
  
 SQL_TC_DML = transazioni possono contenere solo le istruzioni Data Manipulation Language (DML) (**selezionate**, **Inserisci**, **UPDATE**, **Elimina** ). Istruzioni Data Definition Language (DDL) errore in delle cause delle transazioni. ODBC (1.0)  
  
 SQL_TC_DDL_COMMIT = transazioni possono contenere solo le istruzioni DML. Istruzioni DDL (**CREATE TABLE**, **DROP INDEX**e così via) ha rilevato in delle cause delle transazioni per eseguire il commit della transazione. (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE = transazioni possono contenere solo le istruzioni DML. Istruzioni DDL ha rilevate in una transazione vengono ignorate. (ODBC 2.0)  
  
 SQL_TC_ALL = transazioni possono contenere istruzioni DDL e le istruzioni DML in qualsiasi ordine. ODBC (1.0)  
  
 (Poiché il supporto delle transazioni è obbligatorio in SQL-92, un driver conforme allo standard SQL-92 [qualsiasi livello] non restituirà mai SQL_TC_NONE.)  
  
 SQL_TXN_ISOLATION_OPTION ODBC (1.0)  
 Maschera di bit SQLUINTEGER l'enumerazione dei livelli di isolamento delle transazioni disponibili dall'origine dati o driver.  
  
 Le maschere di bit seguenti vengono usate con il flag per determinare quali opzioni sono supportate:  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 Per una descrizione di questi livelli di isolamento, vedere la descrizione di SQL_DEFAULT_TXN_ISOLATION.  
  
 Per impostare il livello di isolamento delle transazioni, un'applicazione chiama **SQLSetConnectAttr** per impostare l'attributo SQL_ATTR_TXN_ISOLATION. Per altre informazioni, vedere [funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre SQL_TXN_SERIALIZABLE supportato. Un driver di livello conformi a FIPS transitorio restituirà sempre tutte queste opzioni supportate.  
  
 SQL_UNION (ODBC 2.0)  
 Maschera di bit SQLUINTEGER l'enumerazione il supporto per la **unione** clausola:  
  
 SQL_U_UNION = l'origine dati supporta la **unione** clausola.  
  
 SQL_U_UNION_ALL = l'origine dati supporta la **tutte** parola chiave nel **UNION** clausola. (**SQLGetInfo** in questo caso vengono restituiti sia SQL_U_UNION sia SQL_U_UNION_ALL.)  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre entrambe le opzioni supportate.  
  
 SQL_USER_NAME ODBC (1.0)  
 Una stringa di caratteri con il nome usato in un determinato database, che può essere diverso dal nome dell'account di accesso.  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3.0)  
 Una stringa di caratteri che indica l'anno di pubblicazione della specifica Open Group con il quale la versione di gestione Driver ODBC è completamente conforme.  
  
 SQL_ACCESSIBLE_PROCEDURES ODBC (1.0)  
 Una stringa di caratteri: "Y" se l'utente può eseguire tutte le procedure restituite dal **SQLProcedures**; "N" se vi sono le procedure restituite che l'utente non può eseguire.  
  
 SQL_ACCESSIBLE_TABLES ODBC (1.0)  
 Una stringa di caratteri: "Y" se l'utente è garantita **selezionate** privilegi per tutte le tabelle restituite dal **SQLTables**; "N" se vi sono tabelle restituito che l'utente non può accedere.  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 Un valore SQLUSMALLINT che specifica il numero massimo di ambienti attivi in grado di supportare il driver. Se non esiste un limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione di supporto per le funzioni di aggregazione:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Un driver conforme a livello di SQL-92 voce restituirà sempre tutte queste opzioni supportate.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **ALTER dominio** istruzione, come definito in SQL-92, supportati dall'origine dati. Un driver conforme con livello SQL-92 completo restituirà sempre tutte le maschere di bit. Il valore restituito pari a "0" indica che il **ALTER dominio** istruzione non è supportata.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità è racchiusa tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = aggiunta è supportato un vincolo di dominio (livello completo)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter dominio > \<clausola predefinite dominio set > è supportato (livello completo)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<clausola definizione di vincolo name > è supportato per la denominazione vincolo dei domini (livello intermedio)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<clausola di vincolo di dominio di rilascio > è supportato (livello completo)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter dominio > \<clausola default domain rilascio > è supportato (livello completo)  
  
 I bit seguenti specificano supportati \<attributi di vincolo > Se \<Aggiungi vincolo di dominio > è supportato (è impostato il bit SQL_AD_ADD_DOMAIN_CONSTRAINT):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (livello completo) SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (livello completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (livello completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 Maschera di bit SQLUINTEGER l'enumerazione le clausole nel **ALTER TABLE** istruzione supportata dall'origine dati.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale deve essere supportata questa funzionalità è racchiusa tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<Aggiungi colonna > clausola è supportata, con funzionalità per specificare regole di confronto colonna (livello completo) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<Aggiungi colonna > clausola è supportata, con funzionalità per specificare valori predefiniti delle colonne (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<Aggiungi colonna > è supportato (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT = \<Aggiungi colonna > clausola è supportata, con funzionalità per specificare i vincoli di colonna (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<Aggiungi vincolo di tabella > clausola è supportata (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<definizione del vincolo name > è supportato per la denominazione dei vincoli di colonna e tabella (livello intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<eliminare la colonna > è supportato in serie (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<modificare la colonna > \<clausola default di eliminazione colonna > è supportato (livello intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<eliminare la colonna > è supportato RESTRICT (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<eliminare la colonna > è supportato RESTRICT (livello FIPS transitorio) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<modificare la colonna > \<clausola default colonna set > è supportato (livello intermedio) (ODBC 3.0)  
  
 I bit seguenti specificano il supporto \<attributi di vincolo > Se è consentito specificare vincoli di colonna o una tabella (è impostato il bit SQL_AT_ADD_CONSTRAINT):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (livello completo) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (livello completo) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (livello completo) (ODBC 3.0)  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 Un valore SQLUINTEGER che indica il livello di supporto asincrono nel driver:  
  
 SQL_AM_CONNECTION = è supportata l'esecuzione asincrona a livello di connessione. Tutti gli handle di istruzione associati a un handle di connessione specificate siano in modalità asincrona o tutti sono in modalità sincrona. Un handle di istruzione in una connessione non può essere in modalità asincrona, mentre un altro handle di istruzione nella stessa connessione è in modalità sincrona e viceversa.  
  
 SQL_AM_STATEMENT = è supportata l'esecuzione asincrona a livello di istruzione. Alcuni handle di istruzione associati a un handle di connessione possono essere in modalità asincrona, mentre altri handle di istruzione nella stessa connessione sono in modalità sincrona.  
  
 SQL_AM_NONE = asincrono in modalità non è supportata.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Maschera di bit SQLUINTEGER l'enumerazione il comportamento del driver per quanto riguarda la disponibilità di riga viene conteggiata. Le maschere di bit seguenti vengono usati insieme al tipo di informazioni:  
  
 SQL_BRC_ROLLED_UP = conteggio delle righe per le istruzioni INSERT, DELETE o UPDATE consecutive vengono raggruppate in un unico. Se questo bit non è impostato, i conteggi delle righe sono disponibili per ogni istruzione.  
  
 SQL_BRC_PROCEDURES = conteggio delle righe, se presente, sono disponibili quando un batch viene eseguito in una stored procedure. Se i conteggi delle righe sono disponibili, è possibile eseguire il rollback verso l'alto o singolarmente disponibile, a seconda di bit SQL_BRC_ROLLED_UP.  
  
 SQL_BRC_EXPLICIT = conteggio delle righe, se presente, sono disponibili quando un batch viene eseguito chiamando direttamente **SQLExecute** oppure **SQLExecDirect**. Se i conteggi delle righe sono disponibili, è possibile eseguire il rollback verso l'alto o singolarmente disponibile, a seconda di bit SQL_BRC_ROLLED_UP.  
  
## <a name="example"></a>Esempio  
 **SQLGetInfo** restituisce elenchi di opzioni supportate come maschera di bit SQLUINTEGER in **InfoValuePtr*. La maschera di bit per ogni opzione viene utilizzata con il flag per determinare se l'opzione è supportata.  
  
 Ad esempio, un'applicazione può usare il codice seguente per determinare se la funzione scalare SOTTOSTRINGA è supportata dal driver associato alla connessione.  
  
 Per un altro esempio di utilizzo **SQLGetInfo**, vedere [funzione SQLTables](../../../odbc/reference/syntax/sqltables-function.md).  
  
```  
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
 Restituisce l'impostazione di un attributo di connessione  
 [Funzione SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 Determinare se un driver supporta una funzione  
 [Funzione SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 Restituisce l'impostazione di un attributo di istruzione  
 [Funzione SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 Restituzione di informazioni sui tipi di dati dell'origine dati  
 [Funzione SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
