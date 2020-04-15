---
title: 'Proprietà SQLGetInfo : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 514922fd085cfd2ba19eb5c07dd844db82d55202
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303343"
---
# <a name="sqlgetinfo-function"></a>Funzione SQLGetInfo
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLGetInfo** restituisce informazioni generali sul driver e sull'origine dati associati a una connessione.  
  
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
  
 *Infotype*  
 [Ingresso] Tipo di informazioni.  
  
 *InfoValuePtr*  
 [Uscita] Puntatore a un buffer in cui restituire le informazioni. A seconda *dell'InfoType* richiesto, le informazioni restituite saranno una delle seguenti: una stringa di caratteri con terminazione null, un valore SQLUSMALLINT, una maschera di bit SQLUINTEGER, un flag SQLUINTEGER, un valore binario SQLUINTEGER o un valore SQLULEN.  
  
 Se l'argomento *InfoType* è SQL_DRIVER_HDESC o SQL_DRIVER_HSTMT, l'argomento *InfoValuePtr* è sia di input che di output. Per ulteriori informazioni, vedere i descrittori di SQL_DRIVER_HDESC o SQL_DRIVER_HSTMT più avanti in questa descrizione della funzione.  
  
 Se *InfoValuePtr* è NULL, *StringLengthPtr* restituirà comunque il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *InfoValuePtr*.  
  
 *BufferLength*  
 [Ingresso] Lunghezza del \*buffer *InfoValuePtr.* Se il valore in * \*InfoValuePtr* non è una stringa di caratteri o se *InfoValuePtr* è un puntatore null, il *BufferLength* argomento viene ignorato. Il driver presuppone che la dimensione di * \*InfoValuePtr* sia SQLUSMALLINT o SQLUINTEGER, in base a *InfoType*. Se * \*InfoValuePtr* è una stringa Unicode (quando si chiama **SQLGetInfoW**), l'argomento *BufferLength* deve essere un numero pari. in caso contrario, viene restituito SQLSTATE HY090 (stringa non valida o lunghezza del buffer).  
  
 *StringLengthPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione in*InfoValuePtr*.  
  
 Per i dati di tipo carattere, se il numero di byte \*disponibili per la restituzione è maggiore o uguale a *BufferLength*, le informazioni in *InfoValuePtr* vengono troncate a *BufferLength* byte meno la lunghezza di un carattere di terminazione null e vengono con terminazione null dal driver.  
  
 Per tutti gli altri tipi di dati, il valore di *BufferLength* viene ignorato e il driver presuppone che la dimensione di \* *InfoValuePtr* sia SQLUSMALLINT o SQLUINTEGER, a seconda di *InfoType*.  
  
## <a name="return-value"></a>Valore restituito  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetInfo** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_DBC e un *handle* di *ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLGetInfo** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Il \*buffer *InfoValuePtr* non era sufficientemente grande per restituire tutte le informazioni richieste. Pertanto, le informazioni sono state troncate. La lunghezza delle informazioni richieste nel relativo formato non troncato viene restituita in *, StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08003|Connessione non aperta|(DM) Il tipo di informazioni richieste in *InfoType* richiede una connessione aperta. Dei tipi di informazioni riservati da ODBC, solo SQL_ODBC_VER può essere restituito senza una connessione aperta.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY024 (informazioni in base al|Valore dell'attributo non valido|(DM) l'argomento *InfoType* è stato SQL_DRIVER_HSTMT e il valore a cui fa riferimento *InfoValuePtr* non è un handle di istruzione valido.<br /><br /> (DM) l'argomento *InfoType* è stato SQL_DRIVER_HDESC e il valore a cui fa riferimento *InfoValuePtr* non è un handle di descrittore valido.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore specificato per l'argomento *BufferLength* è minore di 0.<br /><br /> (DM) il valore specificato per *BufferLength* era un numero dispari e * \*InfoValuePtr* era di un tipo di dati Unicode.|  
|I096|Tipo di informazioni fuori intervallo|Il valore specificato per l'argomento *InfoType* non è valido per la versione di ODBC supportata dal driver.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Campo facoltativo non implementatoOptional field not implemented|Il valore specificato per l'argomento *InfoType* è un valore specifico del driver non supportato dal driver.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver che corrisponde a *ConnectionHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 I tipi di informazioni attualmente definiti vengono visualizzati in "Tipi di informazioni" più avanti in questa sezione; si prevede che ne verranno definite altre per sfruttare le diverse origini dati. Un intervallo di tipi di informazioni è riservato da ODBC; gli sviluppatori di driver devono riservare i valori per il proprio utilizzo specifico del driver da Open Group. **SQLGetInfo** non esegue alcuna conversione Unicode o *thunking* (vedere [Appendice A: Codici](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) di errore ODBC di *ODBC Programmer's Reference*) per *InfoTypes*definiti dal driver . Per ulteriori informazioni, vedere [Tipi di dati specifici del driver, Tipi di descrittore, Tipi di informazioni, Tipi di diagnostica e Attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md). Il formato delle informazioni \*restituite in *InfoValuePtr* dipende dall'InfoType richiesto. *InfoType* **SQLGetInfo** restituirà informazioni in uno dei cinque formati diversi:  
  
-   Una stringa di caratteri con terminazione nullA null-terminated character string  
  
-   Valore SQLUSMALLINT  
  
-   Una maschera di bit SQLUINTEGERAn SQLUINTEGER bitmask  
  
-   Valore SQLUINTEGER  
  
-   Valore binario SQLUINTEGER  
  
 Il formato di ciascuno dei seguenti tipi di informazioni è indicato nella descrizione del tipo. L'applicazione deve eseguire di conseguenza il cast del valore restituito in *: InfoValuePtr.* Per un esempio di come un'applicazione potrebbe recuperare dati da una maschera di bit SQLUINTEGER, vedere "Esempio di codice".  
  
 Un driver deve restituire un valore per ogni tipo di informazioni definito nelle tabelle seguenti. Se un tipo di informazioni non si applica al driver o all'origine dati, il driver restituisce uno dei valori elencati nella tabella seguente.  
  
 Stringa di caratteri ("Y" o "N")  
 "N"  
  
 Stringa di caratteri (non "Y" o "N")  
 stringa vuota  
  
 SQLUSMALLINT (informazioni in lingua inglese)  
 0  
  
 Maschera di bit SQLUINTEGER o valore binario SQLUINTEGER  
 0L  
  
 Ad esempio, se un'origine dati non supporta le procedure, **SQLGetInfo** restituisce i valori elencati nella tabella seguente per i valori di *InfoType* correlati alle procedure.  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 stringa vuota  
  
 **SQLGetInfo** restituisce SQLSTATE HY096 (valore argomento non valido) per i valori di *InfoType* che si trovano nell'intervallo di tipi di informazioni riservati per l'utilizzo da ODBC, ma non sono definiti dalla versione di ODBC supportata dal driver. Per determinare la versione di ODBC che un driver è conforme, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_DRIVER_ODBC_VER. **SQLGetInfo** restituisce SQLSTATE HYC00 (funzionalità facoltativa non implementata) per i valori di *InfoType* che si trovano nell'intervallo di tipi di informazioni riservati per l'utilizzo specifico del driver ma non sono supportati dal driver.  
  
 Tutte le chiamate a **SQLGetInfo** richiedono una connessione aperta, tranne quando il *InfoType* è SQL_ODBC_VER, che restituisce la versione di Gestione Driver.  
  
## <a name="information-types"></a>Tipi di informazioni  
 In questa sezione sono elencati i tipi di informazioni supportati da **SQLGetInfo**. I tipi di informazioni sono raggruppati in modo categorico ed elencati in ordine alfabetico. Vengono elencati anche i tipi di informazioni che sono stati aggiunti o rinominati per ODBC 3 *.x.*  
  
## <a name="driver-information"></a>Informazioni sul conducente  
 I seguenti valori dell'argomento *InfoType* restituiscono informazioni sul driver ODBC, ad esempio il numero di istruzioni attive, il nome dell'origine dati e il livello di conformità degli standard dell'interfaccia:  
  
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
 I seguenti valori dell'argomento *InfoType* restituiscono informazioni sul prodotto DBMS, ad esempio il nome e la versione del sistema DBMS:  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>Informazioni sull'origine dati  
 I seguenti valori dell'argomento *InfoType* restituiscono informazioni sull'origine dati, ad esempio le caratteristiche del cursore e le funzionalità delle transazioni:  
  
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
 I valori seguenti dell'argomento *InfoType* restituiscono informazioni sulle istruzioni SQL supportate dall'origine dati. La sintassi SQL di ogni funzionalità descritta da questi tipi di informazioni è la sintassi SQL-92. Questi tipi di informazioni non descrivono in modo esaustivo l'intera grammatica SQL-92. Al contrario, descrivono quelle parti della grammatica per cui le origini dati offrono in genere diversi livelli di supporto. In particolare, la maggior parte delle istruzioni DDL in SQL-92 sono coperti.  
  
 Le applicazioni devono determinare il livello generale di grammatica supportata dal tipo di informazioni SQL_SQL_CONFORMANCE e utilizzare gli altri tipi di informazioni per determinare le variazioni dal livello di conformità degli standard indicato.  
  
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
 I valori seguenti dell'argomento *InfoType* restituiscono informazioni sui limiti applicati agli identificatori e alle clausole nelle istruzioni SQL, ad esempio la lunghezza massima degli identificatori e il numero massimo di colonne in un elenco di selezione. Le limitazioni possono essere imposte dal driver o dall'origine dati.  
  
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
 I valori seguenti dell'argomento *InfoType* restituiscono informazioni sulle funzioni scalari supportate dall'origine dati e dal driver. Per ulteriori informazioni sulle funzioni scalari, vedere [Appendice E: Funzioni scalari](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>Informazioni sulla conversione  
 I valori seguenti dell'argomento *InfoType* restituiscono un elenco dei tipi di dati SQL in cui l'origine dati può convertire il tipo di dati SQL specificato con la funzione scalare **CONVERT:**  
  
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
  
## <a name="information-types-added-for-odbc-3x"></a>Tipi di informazioni aggiunti per ODBC 3.x  
 Per ODBC 3 *.x*sono stati aggiunti i seguenti valori dell'argomento *InfoType* :  
  
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
 I seguenti valori dell'argomento *InfoType* sono stati rinominati per ODBC 3 *.x*.  
  
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
 I seguenti valori dell'argomento *InfoType* sono stati deprecati in ODBC 3 *.x*. I driver*x* ODBC 3 devono continuare a supportare questi tipi di informazioni per garantire la compatibilità con le applicazioni *.x* ODBC 2. Per altre informazioni su questi tipi, vedere [Supporto di SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md) nell'Appendice G: Linee guida per i driver per la compatibilità con le versioni precedenti.  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>Descrizioni del tipo di informazioni  
 Nella tabella seguente sono elencati in ordine alfabetico ogni tipo di informazioni, la versione di ODBC in cui è stato introdotto e la relativa descrizione.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 Una stringa di caratteri: "Y" se l'utente può eseguire tutte le routine restituite da **SQLProcedures**; "N" se possono essere restituite procedure che l'utente non può eseguire.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 Una stringa di caratteri: "Y" se all'utente sono garantiti i privilegi **SELECT** per tutte le tabelle restituite da **SQLTables**; "N" se potrebbero essere restituite tabelle a cui l'utente non può accedere.  
  
 SQL_ACTIVE_ENVIRONMENTS(ODBC 3.0)  
 Valore SQLUSMALLINT che specifica il numero massimo di ambienti attivi che il driver può supportare. Se non esiste alcun limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 SQL_AGGREGATE_FUNCTIONS(ODBC 3.0)  
 Una maschera di bit SQLUINTEGER che enumera il supporto per le funzioni di aggregazione:An SQLUINTEGER bitmask enumerating support for aggregation functions:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **ALTER DOMAIN,** come definito in SQL-92, supportata dall'origine dati. Un driver conforme al livello completo SQL-92 restituirà sempre tutte le maschere di bit. Un valore restituito pari a "0" indica che l'istruzione **ALTER DOMAIN** non è supportata.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale questa funzionalità deve essere supportata viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT: l'aggiunta di un vincolo di dominio è supportata (livello completo)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT \<- modifica \<del dominio> impostare la clausola predefinita del dominio> è supportata (livello completo)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION: \<la clausola di definizione del nome del vincolo> è supportata per il vincolo di dominio di denominazione (livello intermedio)The type - constraint name definition clause> is supported for naming domain constraint (Intermediate level)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT: \<è supportata la clausola del vincolo di dominio di eliminazione> (livello completo)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT \<- modifica \<del dominio> eliminare la clausola predefinita del dominio> è supportata (livello completo)  
  
 I bit seguenti specificano gli attributi di vincolo supportati \<> se \<è supportato l'> vincolo di dominio aggiuntivo (il bit di SQL_AD_ADD_DOMAIN_CONSTRAINT è impostato):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (Livello completo)SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (Livello completo)SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (livello completo)SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **ALTER TABLE** supportata dall'origine dati.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale questa funzionalità deve essere supportata viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_AT_ADD_COLUMN_COLLATION: \<è supportata la clausola di aggiunta di> di colonna, con funzionalità per specificare le regole di confronto delle colonne (livello completo) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT: \<è supportata l'aggiunta di una clausola di> di colonna, con funzionalità per specificare i valori predefiniti delle colonne (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE: \<è supportata la> di aggiunta di colonne (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT: \<è supportata l'aggiunta di una colonna> clausola, con funzionalità per specificare i vincoli di colonna (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT: \<è supportata l'aggiunta di un vincolo di tabella> la clausola (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION: \<la definizione del nome del vincolo> è supportata per la denominazione dei vincoli di colonna e di tabella (livello intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE \<- eliminare la colonna> è supportato CASCADE (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT \<- modifica \<colonna> clausola predefinita di colonna di rilascio> è supportato (livello intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT \<- colonna di rilascio> è supportato RESTRICT (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT \<- drop column> è supportato RESTRICT (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT \<- modifica \<la colonna> imposta la clausola predefinita della colonna> è supportata (livello intermedio) (ODBC 3.0)  
  
 I bit seguenti specificano gli attributi del vincolo di supporto \<> se è supportata la specifica di vincoli di colonna o di tabella (il bit SQL_AT_ADD_CONSTRAINT è impostato):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (livello completo) (ODBC 3.0)SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo) (ODBC 3.0)SQL_AT_CONSTRAINT_DEFERRABLE (livello completo) (ODBC 3.0)SQL_AT_CONSTRAINT_NON_DEFERRABLE (livello completo) (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 Valore SQLUINTEGER che indica se il driver può eseguire funzioni in modo asincrono sull'handle di connessione.  
  
 SQL_ASYNC_DBC_CAPABLE: il driver può eseguire le funzioni di connessione in modo asincrono.  
  
 SQL_ASYNC_DBC_NOT_CAPABLE - Il driver non può eseguire le funzioni di connessione in modo asincrono.  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 Valore SQLUINTEGER che indica il livello di supporto asincrono nel driver:  
  
 SQL_AM_CONNECTION: è supportata l'esecuzione asincrona a livello di connessione. Tutti gli handle di istruzione associati a un determinato handle di connessione sono in modalità asincrona o tutti in modalità sincrona. Un handle di istruzione su una connessione non può essere in modalità asincrona mentre un altro handle di istruzione sulla stessa connessione è in modalità sincrona e viceversa.  
  
 SQL_AM_STATEMENT: è supportata l'esecuzione asincrona a livello di istruzione. Alcuni handle di istruzione associati a un handle di connessione possono essere in modalità asincrona, mentre altri handle di istruzione nella stessa connessione sono in modalità sincrona.  
  
 SQL_AM_NONE: la modalità asincrona non è supportata.  
  
 SQL_ASYNC_NOTIFICATION  
 Valore SQLUINTEGER che indica se il driver supporta la notifica asincrona:  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE** La notifica di esecuzione asincrona è supportata dal driver.  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE** La notifica di esecuzione asincrona non è supportata dal driver.  
  
 Esistono due categorie di operazioni asincrone ODBC: operazioni asincrone a livello di connessione e operazioni asincrone a livello di istruzione.  Se un driver restituisce SQL_ASYNC_NOTIFICATION_CAPABLE, deve supportare la notifica per tutte le API che può eseguire in modo asincrono.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera il comportamento del driver rispetto alla disponibilità dei conteggi di riga. Le maschere di bit seguenti vengono utilizzate insieme al tipo di informazioni:  
  
 SQL_BRC_ROLLED_UP: i conteggi delle righe per le istruzioni INSERT, DELETE o UPDATE consecutive vengono raggruppati in uno. Se questo bit non è impostato, i conteggi delle righe sono disponibili per ogni istruzione.  
  
 SQL_BRC_PROCEDURES: i conteggi delle righe, se presenti, sono disponibili quando un batch viene eseguito in una stored procedure. Se i conteggi delle righe sono disponibili, è possibile eseguire il rollup o essere disponibili singolarmente, a seconda del bit SQL_BRC_ROLLED_UP.  
  
 SQL_BRC_EXPLICIT: i conteggi delle righe, se presenti, sono disponibili quando un batch viene eseguito direttamente chiamando **SQLExecute** o **SQLExecDirect**. Se i conteggi delle righe sono disponibili, è possibile eseguire il rollup o essere disponibili singolarmente, a seconda del bit SQL_BRC_ROLLED_UP.  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera il supporto del driver per i batch. Le maschere di bit seguenti vengono utilizzate per determinare quale livello è supportato:The following bitmasks are used to determine which level is supported:  
  
 SQL_BS_SELECT_EXPLICIT: il driver supporta batch espliciti che possono avere istruzioni di generazione del set di risultati.  
  
 SQL_BS_ROW_COUNT_EXPLICIT: il driver supporta batch espliciti che possono avere istruzioni di generazione di conteggio delle righe.  
  
 SQL_BS_SELECT_PROC: il driver supporta procedure esplicite che possono avere istruzioni di generazione del set di risultati.  
  
 SQL_BS_ROW_COUNT_PROC: il driver supporta procedure esplicite che possono avere istruzioni di generazione del conteggio delle righe.  
  
 SQL_BOOKMARK_PERSISTENCE(ODBC 2.0)  
 Maschera di bit SQLUINTEGER che enumera le operazioni tramite le quali i segnalibri vengono mantenuti.  
  
 Le maschere di bit seguenti vengono utilizzate con il flag per determinare tramite quali opzioni i segnalibri persistono:  
  
 SQL_BP_CLOSE i segnalibri sono validi dopo che un'applicazione chiama **SQLFreeStmt** con l'opzione SQL_CLOSE o **SQLCloseCursor** per chiudere il cursore associato a un'istruzione.  
  
 SQL_BP_DELETE: il segnalibro per una riga è valido dopo l'eliminazione di tale riga.  
  
 SQL_BP_DROP segnalibri sono validi dopo che un'applicazione chiama **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_STMT per eliminare un'istruzione.  
  
 SQL_BP_TRANSACTION i segnalibri sono validi dopo il commit o il rollback di una transazione da parte di un'applicazione.  
  
 SQL_BP_UPDATE: il segnalibro per una riga è valido dopo l'aggiornamento di qualsiasi colonna in tale riga, incluse le colonne chiave.  
  
 SQL_BP_OTHER_HSTMT: un segnalibro associato a un'istruzione può essere utilizzato con un'altra istruzione. A meno che non venga specificata SQL_BP_CLOSE o SQL_BP_DROP, il cursore sulla prima istruzione deve essere aperto.  
  
 SQL_CATALOG_LOCATION(ODBC 2.0)  
 Valore SQLUSMALLINT che indica la posizione del catalogo in un nome di tabella completo:  
  
 SQL_CL_STARTSQL_CL_END  
  
 Ad esempio, un driver Xbase restituisce SQL_CL_START perché il nome della directory (catalogo) si trova all'inizio del nome della tabella, come in EMPDATA EMP. Dbf. Un driver ORACLE Server restituisce SQL_CL_END perché il catalogo si ADMIN.EMP@EMPDATAtrova alla fine del nome della tabella, come in .  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà sempre SQL_CL_START. Se i cataloghi non sono supportati dall'origine dati, viene restituito il valore 0. Per determinare se i cataloghi sono supportati, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_CATALOG_NAME.  
  
 Questo *InfoType* è stato rinominato per ODBC 3.0 dal SQL_QUALIFIER_LOCATION *InfoType* di ODBC 2.0.  
  
 SQL_CATALOG_NAME (ODBC 3.0)  
 Una stringa di caratteri: "Y" se il server supporta i nomi dei cataloghi, o "N" in caso contrario.  
  
 Un driver conforme al livello SQL-92 Full restituirà sempre "Y".  
  
 SQL_CATALOG_NAME_SEPARATOR(ODBC 1.0)  
 Una stringa di caratteri: il carattere o i caratteri che l'origine dati definisce come separatore tra un nome di catalogo e l'elemento del nome completo che lo segue o lo precede.  
  
 Se i cataloghi non sono supportati dall'origine dati, viene restituita una stringa vuota. Per determinare se i cataloghi sono supportati, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_CATALOG_NAME. Un driver di livello conforme allo standard SQL-92 Full restituirà sempre ".".  
  
 Questo *InfoType* è stato rinominato per ODBC 3.0 dal SQL_QUALIFIER_NAME_SEPARATOR ODBC 2.0 *InfoType.*  
  
 SQL_CATALOG_TERM(ODBC 1.0)  
 Una stringa di caratteri con il nome del fornitore dell'origine dati per un catalogo. ad esempio, "database" o "directory". Questa stringa può essere maiuscola, minuscola o mista.  
  
 Se i cataloghi non sono supportati dall'origine dati, viene restituita una stringa vuota. Per determinare se i cataloghi sono supportati, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_CATALOG_NAME. Un driver di livello conforme allo standard SQL-92 Full restituirà sempre "catalogo".  
  
 Questo *InfoType* è stato rinominato per ODBC 3.0 dal SQL_QUALIFIER_TERM *InfoType* di ODBC 2.0.  
  
 SQL_CATALOG_USAGE(ODBC 2.0)  
 Maschera di bit SQLUINTEGER che enumera le istruzioni in cui è possibile utilizzare i cataloghi.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare dove è possibile utilizzare i cataloghi:The following bitmasks are used to determine where catalogs can be used:  
  
 SQL_CU_DML_STATEMENTS cataloghi sono supportati in tutte le istruzioni Data Manipulation Language: **SELECT**, **INSERT**, **UPDATE**, **DELETE**e, se supportate, SELECT **FOR UPDATE** e istruzioni di aggiornamento ed eliminazione posizionate.  
  
 SQL_CU_PROCEDURE_INVOCATION: i cataloghi sono supportati nell'istruzione di chiamata di routine ODBC.  
  
 SQL_CU_TABLE_DEFINITION i cataloghi sono supportati in tutte le istruzioni di definizione di tabella: **CREATE TABLE**, **CREATE VIEW**, **ALTER TABLE**, DROP **TABLE**e **DROP VIEW**.  
  
 SQL_CU_INDEX_DEFINITION cataloghi sono supportati in tutte le istruzioni di definizione dell'indice: **CREATE INDEX** e **DROP INDEX**.  
  
 SQL_CU_PRIVILEGE_DEFINITION : i cataloghi sono supportati in tutte le istruzioni di definizione dei privilegi: **GRANT** e **REVOKE**.  
  
 Se i cataloghi non sono supportati dall'origine dati, viene restituito il valore 0. Per determinare se i cataloghi sono supportati, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_CATALOG_NAME. Un driver di livello conforme allo standard SQL-92 Full restituirà sempre una maschera di bit con tutti questi bit impostati.  
  
 Questo *InfoType* è stato rinominato per ODBC 3.0 dal SQL_QUALIFIER_USAGE *InfoType* di ODBC 2.0.  
  
 SQL_COLLATION_SEQ (ODBC 3.0)  
 Nome della sequenza di confronto. Si tratta di una stringa di caratteri che indica il nome delle regole di confronto predefinite per il set di caratteri predefinito per questo server (ad esempio, 'ISO 8859-1' o EBCDIC). Se questo è sconosciuto, verrà restituita una stringa vuota. Un driver di livello conforme allo standard SQL-92 Full restituirà sempre una stringa non vuota.  
  
 SQL_COLUMN_ALIAS(ODBC 2.0)  
 Una stringa di caratteri: "Y" se l'origine dati supporta gli alias di colonna; in caso contrario, "N".  
  
 Un alias di colonna è un nome alternativo che può essere specificato per una colonna nell'elenco di selezione utilizzando una clausola AS. Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre "Y".  
  
 SQL_CONCAT_NULL_BEHAVIOR(ODBC 1.0)  
 Valore SQLUSMALLINT che indica come l'origine dati gestisce la concatenazione di colonne di tipo di dati carattere con valori NULL con colonne di tipo di dati carattere con valori non NULL:An SQLUSMALLINT value that indicates how the data source handles the concatenation of NULL valued character data type columns with non-NULL valued character data type columns:  
  
 SQL_CB_NULL: il risultato è NULL.  
  
 SQL_CB_NON_NULL: il risultato è la concatenazione di colonne o colonne con valori non NULL.  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre SQL_CB_NULL.  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR SQL_CONVERT_CHAR (ODBC 1.0)  
 Maschera di bit SQLUINTEGER. La maschera di bit indica le conversioni supportate dall'origine dati con la funzione scalare **CONVERT** per i dati del tipo denominato nel *InfoType*. Se la maschera di bit è uguale a zero, l'origine dati non supporta le conversioni dai dati del tipo denominato, inclusa la conversione nello stesso tipo di dati.  
  
 Ad esempio, per determinare se un'origine dati supporta la conversione dei dati SQL_INTEGER nel tipo di dati SQL_BIGINT, un'applicazione chiama **SQLGetInfo** con il *InfoType* di SQL_CONVERT_INTEGER. L'applicazione esegue un'operazione **AND** con la maschera di bit restituita e SQL_CVT_BIGINT. Se il valore risultante è diverso da zero, la conversione è supportata.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali conversioni sono supportate:The following bitmasks are used to determine which conversions are supported:  
  
 SQL_CVT_BIGINT (ODBC 1.0)SQL_CVT_BINARY (ODBC 1.0)SQL_CVT_BIT (ODBC 1.0) SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5)SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0)SQL_CVT_DECIMAL (ODBC 1.0)SQL_CVT_FLOAT SQL_CVT_DOUBLE (ODBC 1.0)SQL_CVT_INTEGER (ODBC 1.0)SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0)SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0)SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0)(ODBC 3.0)SQL_CVT_LONGVARCHAR (ODBC 1.0)SQL_CVT_NUMERIC(ODBC 1.0)(ODBC 1.0)(ODBC 1.0)SQL_ (ODBC 1.0)SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 1.0)SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0)SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0)(ODBC 3.0)(ODBC 1.0)SQL_CVT_LONGVARCHAR (ODBC 1.0)SQL_ (ODBC 1.0)SQL_ (ODBC 1.0)(ODBC 1.0)SQL_ (ODBC 1.0)SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 1.0)SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0)SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0)(ODBC 3.0)SQL_CVT_LONGVARCHAR (ODBC 1.0)SQL_CVT_LONGVARCHAR (ODBC 1.0)(ODBC 1.0)SQL_ (ODBC 1.0)(ODBC 1.0)SQL_ (ODBC 1.0)SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 1.0)SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0)SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0)(ODBC 3.0 SQL_CVT_LONGVARBINARY)SQL_CVT_LONGVARCHAR (ODBC 1.0)SQL_CVT_LONGVARCHAR (ODBC 1.0)(ODBC 1.0)SQL_ (ODBC CVT_REAL ODBC 1.0)SQL_CVT_SMALLINT (ODBC 1.0)SQL_CVT_TIME (ODBC 1.0)SQL_CVT_TIMESTAMP (ODBC 1.0)SQL_CVT_TINYINT (ODBC 1.0)SQL_CVT_VARBINARY (ODBC 1.0)SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS(ODBC 1.0)  
 Maschera di bit SQLUINTEGER che enumera le funzioni di conversione scalari supportate dal driver e dall'origine dati associata.  
  
 La maschera di bit seguente viene utilizzata per determinare quali funzioni di conversione sono supportate:The following bitmask is used to determine which conversion functions are supported:  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME(ODBC 1.0)  
 Valore SQLUSMALLINT che indica se i nomi di correlazione delle tabelle sono supportati:  
  
 SQL_CN_NONE: i nomi di correlazione non sono supportati.  
  
 SQL_CN_DIFFERENT: i nomi di correlazione sono supportati, ma devono essere diversi dai nomi delle tabelle che rappresentano.  
  
 SQL_CN_ANY: i nomi di correlazione sono supportati e possono essere qualsiasi nome definito dall'utente valido.  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre SQL_CN_ANY.  
  
 SQL_CREATE_ASSERTION(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **CREATE ASSERTION,** come definito in SQL-92, supportato dall'origine dati.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_CA_CREATE_ASSERTION  
  
 I bit seguenti specificano l'attributo del vincolo supportato se la possibilità di specificare gli attributi del vincolo in modo esplicito è supportata (vedere i tipi di informazioni SQL_ALTER_TABLE e SQL_CREATE_TABLE):  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà sempre tutte queste opzioni come supportate. Un valore restituito pari a "0" indica che l'istruzione **CREATE ASSERTION** non è supportata.  
  
 SQL_CREATE_CHARACTER_SET(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **CREATE CHARACTER SET,** come definito in SQL-92, supportato dall'origine dati.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà sempre tutte queste opzioni come supportate. Un valore restituito pari a "0" indica che l'istruzione **CREATE CHARACTER SET** non è supportata.  
  
 SQL_CREATE_COLLATION(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **CREATE COLLATION,** come definito in SQL-92, supportato dall'origine dati.  
  
 La maschera di bit seguente viene utilizzata per determinare quali clausole sono supportate:The following bitmask is used to determine which clauses are supported:  
  
 SQL_CCOL_CREATE_COLLATION  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà sempre questa opzione come supportata. Un valore restituito pari a "0" indica che l'istruzione **CREATE COLLATION** non è supportata.  
  
 SQL_CREATE_DOMAIN(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **CREATE DOMAIN,** come definito in SQL-92, supportata dall'origine dati.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_CDO_CREATE_DOMAIN- L'istruzione CREATE DOMAIN è supportata (livello intermedio).  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION: \<la definizione del nome del vincolo> è supportata per la denominazione dei vincoli di dominio (livello intermedio).  
  
 I bit seguenti specificano la possibilità di creare vincoli di colonna:SQL_CDO_DEFAULT : l'impostazione di vincoli di dominio è supportata (livello intermedio)SQL_CDO_CONSTRAINT - la specifica dei valori predefiniti del dominio è supportata (livello intermedio)SQL_CDO_COLLATION- Specificare le regole di confronto del dominio è supportata (livello completo)  
  
 I bit seguenti specificano gli attributi di vincolo supportati se è supportata la specifica dei vincoli di dominio (SQL_CDO_DEFAULT è impostata):  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED (livello completo)SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (Livello completo)SQL_CDO_CONSTRAINT_DEFERRABLE (Livello completo)SQL_CDO_CONSTRAINT_NON_DEFERRABLE (livello completo)  
  
 Un valore restituito pari a "0" indica che l'istruzione **CREATE DOMAIN** non è supportata.  
  
 SQL_CREATE_SCHEMA(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **CREATE SCHEMA,** come definito in SQL-92, supportata dall'origine dati.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 Un driver di livello conforme allo standard SQL-92 Intermediate restituirà sempre le opzioni SQL_CS_CREATE_SCHEMA e SQL_CS_AUTHORIZATION come supportate. Questi devono essere supportati anche a livello di voce SQL-92, ma non necessariamente come istruzioni SQL. Un driver di livello conforme allo standard SQL-92 Full restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_CREATE_TABLE (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **CREATE TABLE,** come definito in SQL-92, supportato dall'origine dati.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale questa funzionalità deve essere supportata viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_CT_CREATE_TABLE: è supportata l'istruzione CREATE TABLE. (Livello di ingresso)  
  
 SQL_CT_TABLE_CONSTRAINT: la specifica dei vincoli di tabella è supportata (livello FIPS Transitional)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION: \<la clausola> di definizione del nome del vincolo è supportata per la denominazione dei vincoli di colonna e tabella (livello intermedio)  
  
 I bit seguenti specificano la possibilità di creare tabelle temporanee:  
  
 SQL_CT_COMMIT_PRESERVE: le righe eliminate vengono mantenute al commit. (Livello completo) SQL_CT_COMMIT_DELETE: le righe eliminate vengono eliminate al commit. (Livello completo) SQL_CT_GLOBAL_TEMPORARY: è possibile creare tabelle temporanee globali. (Livello completo) SQL_CT_LOCAL_TEMPORARY: è possibile creare tabelle temporanee locali. (Livello completo)  
  
 I bit seguenti specificano la possibilità di creare vincoli di colonna:The following bits specify the ability to create column constraints:  
  
 SQL_CT_COLUMN_CONSTRAINT: la specifica dei vincoli di colonna è supportata (livello FIPS Transitional)SQL_CT_COLUMN_DEFAULT - è supportata la specifica dei valori predefiniti delle colonne (livello FIPS Transitional)SQL_CT_COLUMN_COLLATION: la specifica delle regole di confronto delle colonne è supportata (livello completo)  
  
 I bit seguenti specificano gli attributi di vincolo supportati se è supportata la specifica di vincoli di colonna o di tabella:The following bits specify the supported constraint attributes if specifying column or table constraints is supported:  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED (livello completo)SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (Livello completo)SQL_CT_CONSTRAINT_DEFERRABLE (Livello completo)SQL_CT_CONSTRAINT_NON_DEFERRABLE (Livello completo)  
  
 SQL_CREATE_TRANSLATION(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **CREATE TRANSLATION,** come definito in SQL-92, supportata dall'origine dati.  
  
 La maschera di bit seguente viene utilizzata per determinare quali clausole sono supportate:The following bitmask is used to determine which clauses are supported:  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà sempre queste opzioni come supportate. Un valore restituito pari a "0" indica che l'istruzione **CREATE TRANSLATION** non è supportata.  
  
 SQL_CREATE_VIEW(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **CREATE VIEW,** come definito in SQL-92, supportato dall'origine dati.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 Un valore restituito pari a "0" indica che l'istruzione **CREATE VIEW** non è supportata.  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre le opzioni SQL_CV_CREATE_VIEW e SQL_CV_CHECK_OPTION come supportate.  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR(ODBC 1.0)  
 Valore SQLUSMALLINT che indica in che modo un'operazione **COMMIT** influisce sui cursori e sulle istruzioni preparate nell'origine dati (il comportamento dell'origine dati quando si esegue il commit di una transazione).  
  
 Il valore di questo attributo rifletterà lo stato corrente dell'impostazione successiva: SQL_COPT_SS_PRESERVE_CURSORS.  
  
 SQL_CB_DELETE: chiudere i cursori ed eliminare le istruzioni preparate. Per utilizzare nuovamente il cursore, l'applicazione deve ripreparare ed eseguire nuovamente l'istruzione.  
  
 SQL_CB_CLOSE: chiudere i cursori. Per le istruzioni preparate, l'applicazione può chiamare **SQLExecute** sull'istruzione senza chiamare nuovamente **SQLPrepare.** L'impostazione predefinita per il driver ODBC SQL è SQL_CB_CLOSE. Ciò significa che il driver ODBC SQL chiuderà i cursori quando si esegue il commit di una transazione.  
  
 SQL_CB_PRESERVE: mantiene i cursori nella stessa posizione di prima dell'operazione **COMMIT.** L'applicazione può continuare a recuperare i dati oppure può chiudere il cursore e rieseguire l'istruzione senza prepararla nuovamente.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR(ODBC 1.0)  
 Valore SQLUSMALLINT che indica come un'operazione **ROLLBACK** influisce sui cursori e sulle istruzioni preparate nell'origine dati:  
  
 SQL_CB_DELETE: chiudere i cursori ed eliminare le istruzioni preparate. Per utilizzare nuovamente il cursore, l'applicazione deve ripreparare ed eseguire nuovamente l'istruzione.  
  
 SQL_CB_CLOSE: chiudere i cursori. Per le istruzioni preparate, l'applicazione può chiamare **SQLExecute** sull'istruzione senza chiamare nuovamente **SQLPrepare.**  
  
 SQL_CB_PRESERVE - Mantiene i cursori nella stessa posizione di prima dell'operazione **ROLLBACK.** L'applicazione può continuare a recuperare i dati oppure può chiudere il cursore ed eseguire nuovamente l'istruzione senza riprepararla.  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 Valore SQLUINTEGER che indica il supporto per la sensibilità del cursore:  
  
 SQL_INSENSITIVE: tutti i cursori sull'handle dell'istruzione mostrano il set di risultati senza riflettere le modifiche apportate da qualsiasi altro cursore all'interno della stessa transazione.  
  
 SQL_UNSPECIFIED: non viene specificato se i cursori sull'handle dell'istruzione rendono visibili le modifiche apportate a un set di risultati da un altro cursore all'interno della stessa transazione. I cursori sull'handle dell'istruzione possono rendere visibili nessuna, alcune o tutte queste modifiche.  
  
 SQL_SENSITIVE: i cursori sono sensibili alle modifiche apportate da altri cursori all'interno della stessa transazione.  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre l'opzione SQL_UNSPECIFIED come supportata.  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà sempre l'opzione SQL_INSENSITIVE come supportata.  
  
 SQL_DATA_SOURCE_NAME(ODBC 1.0)  
 Stringa di caratteri con il nome dell'origine dati utilizzato durante la connessione. Se l'applicazione denominata **SQLConnect**, questo è il valore dell'argomento *szDSN.* Se l'applicazione denominata **SQLDriverConnect** o **SQLBrowseConnect**, questo è il valore della parola chiave DSN nella stringa di connessione passata al driver. Se la stringa di connessione non contiene la parola chiave **DSN** (ad esempio quando contiene la parola chiave **DRIVER),** si tratta di una stringa vuota.  
  
 SQL_DATA_SOURCE_READ_ONLY(ODBC 1.0)  
 Stringa di caratteri. "Y" se l'origine dati è impostata sulla modalità READ ONLY, "N" in caso contrario.  
  
 Questa caratteristica riguarda solo l'origine dati stessa; non è una caratteristica del driver che consente l'accesso all'origine dati. Un driver di lettura/scrittura può essere utilizzato con un'origine dati di sola lettura. Se un driver è di sola lettura, tutte le relative origini dati devono essere di sola lettura e devono restituire SQL_DATA_SOURCE_READ_ONLY.  
  
 SQL_DATABASE_NAME(ODBC 1.0)  
 Una stringa di caratteri con il nome del database corrente in uso, se l'origine dati definisce un oggetto denominato denominato "database".  
  
> [!NOTE]
>  In ODBC 3 *.x*, il valore restituito per questo *InfoType* può essere restituito anche chiamando **SQLGetConnectAttr** con un *attributo* argomento di SQL_ATTR_CURRENT_CATALOG.  
  
 SQL_DATETIME_LITERALS (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera i valori letterali datetime SQL-92 supportati dall'origine dati. Si noti che questi sono i valori letterali datetime elencati nella specifica SQL-92 e sono separati dalle clausole di escape dei valori letterali datetime definite da ODBC. Per ulteriori informazioni sulle clausole di escape dei valori letterali datetime ODBC, vedere [Valori letterali Date, Time e Timestamp](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Un driver di livello conforme a FIPS Transitional restituirà sempre il valore "1" nella maschera di bit per i bit nell'elenco seguente. Il valore "0" indica che i valori letterali datetime SQL-92 non sono supportati.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali valori letterali sono supportati:The following bitmasks are used to determine which literals are supported:  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME (ODBC 1.0)  
 Una stringa di caratteri con il nome del prodotto DBMS a cui accede il driver.  
  
 SQL_DBMS_VER(ODBC 1.0)  
 Stringa di caratteri che indica la versione del prodotto DBMS a cui accede il driver. La versione è nel formato "" , in cui le prime due cifre sono la versione principale, le due cifre successive sono la versione secondaria e le ultime quattro cifre sono la versione di rilascio. Il driver deve eseguire il rendering della versione del prodotto DBMS in questo formato, ma può anche aggiungere la versione specifica del prodotto DBMS. Ad esempio, "04.01.0000 Rdb 4.1".  
  
 SQL_DDL_INDEX(ODBC 3.0)  
 Valore SQLUINTEGER che indica il supporto per la creazione e l'eliminazione di indici:  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION(ODBC 1.0)  
 Valore SQLUINTEGER che indica il livello di isolamento delle transazioni predefinito supportato dal driver o dall'origine dati oppure zero se l'origine dati non supporta le transazioni. Per definire i livelli di isolamento delle transazioni vengono utilizzati i termini seguenti:  
  
 **Sporco Lettura** La transazione 1 modifica una riga. La transazione 2 legge la riga modificata prima che la transazione 1 esetrai il commit della modifica. Se la transazione 1 esegue il rollback della modifica, la transazione 2 avrà letto una riga che si ritiene non sia mai esistita.  
  
 **Lettura non ripetibile** La transazione 1 legge una riga. La transazione 2 aggiorna o elimina tale riga ed esegue il commit di questa modifica. Se la transazione 1 tenta di rileggere la riga, riceverà valori di riga diversi o scoprirà che la riga è stata eliminata.  
  
 **Fantasma** La transazione 1 legge un set di righe che soddisfano alcuni criteri di ricerca. La transazione 2 genera una o più righe (tramite inserimenti o aggiornamenti) che corrispondono ai criteri di ricerca. Se la transazione 1 esegue nuovamente l'istruzione che legge le righe, riceve un set di righe diverso.  
  
 Se l'origine dati supporta le transazioni, il driver restituisce una delle maschere di bit seguenti:  
  
 SQL_TXN_READ_UNCOMMITTED - Letture sporche, letture non ripetibili e fantasmi sono possibili.  
  
 SQL_TXN_READ_COMMITTED - Le letture sporche non sono possibili. Letture non ripetibili e fantasmi sono possibili.  
  
 SQL_TXN_REPEATABLE_READ - Letture sporche e letture non ripetibili non sono possibili. I fantasmi sono possibili.  
  
 SQL_TXN_SERIALIZABLE: le transazioni sono serializzabili. Le transazioni serializzabili non consentono letture dirty, letture non ripetibili o fantasma.  
  
 SQL_DESCRIBE_PARAMETER(ODBC 3.0)  
 Una stringa di caratteri: "Y" se i parametri possono essere descritti; "N", se non.  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà in genere "Y" perché supporterà l'istruzione **DESCRIBE INPUT.** Poiché questo non specifica direttamente il supporto SQL sottostante, tuttavia, la descrizione dei parametri potrebbe non essere supportata, anche in un driver conforme al livello sql-92.  
  
 SQL_DM_VER (ODBC 3.0)  
 Una stringa di caratteri con la versione di Gestione Driver. La versione ha il formato : . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .  
  
 Il primo set di due cifre è la versione ODBC principale, come specificato dalla costante SQL_SPEC_MAJOR.  
  
 Il secondo set di due cifre è la versione ODBC secondaria, come specificato dalla costante SQL_SPEC_MINOR.  
  
 Il terzo set di quattro cifre è il numero di build principale di Gestione Driver.  
  
 L'ultimo set di quattro cifre è il numero di build secondario di Gestione Driver.  
  
 La versione di Gestione driver di Windows 7 è 03.80. La versione di Gestione driver di Windows 8 è 03.81.  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 Valore SQLUINTEGER che indica se il pool in grado di riconoscere i driver supporta il driver. Per ulteriori informazioni, vedere [Pool di connessioni in base](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)al driver .  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE indica che il driver può supportare il meccanismo di pooling in grado di riconoscere i driver.  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE indica che il driver non supporta il meccanismo di pooling in grado di riconoscere i driver.  
  
 Non è necessario che un driver implementi SQL_DRIVER_AWARE_POOLING_SUPPORTED e Gestione Driver non rispetterà il valore restituito del driver.  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV(ODBC 1.0)  
 Valore SQLULEN, l'handle di ambiente del driver o l'handle di connessione, determinato dall'argomento *InfoType*.  
  
 Questi tipi di informazioni vengono implementati solo da Gestione Driver.  
  
 SQL_DRIVER_HDESC (ODBC 3.0)  
 Un valore SQLULEN, l'handle del descrittore del driver determinato dall'handle del \*descrittore di Gestione Driver, che deve essere passato all'input in *InfoValuePtr* dall'applicazione. In questo caso, *InfoValuePtr* è sia un argomento di input che un argomento di output. L'handle del \*descrittore di input passato in *InfoValuePtr* deve essere stato allocato in modo esplicito o implicito in *ConnectionHandle*.  
  
 L'applicazione deve eseguire una copia dell'handle del descrittore di Gestione Driver prima di chiamare **SQLGetInfo** con questo tipo di informazioni, per assicurarsi che l'handle non venga sovrascritto nell'output.  
  
 Questo tipo di informazioni viene implementato solo da Gestione Driver.  
  
 SQL_DRIVER_HLIB(ODBC 2.0)  
 Un valore SQLULEN, *l'hinst* dalla libreria di caricamento restituito a Gestione Driver quando è stata caricata la DLL del driver in un sistema operativo Microsoft Windows o equivalente in un altro sistema operativo. L'handle è valido solo per l'handle di connessione specificato nella chiamata a **SQLGetInfo**.  
  
 Questo tipo di informazioni viene implementato solo da Gestione Driver.  
  
 SQL_DRIVER_HSTMT(ODBC 1.0)  
 Un valore SQLULEN, l'handle dell'istruzione del driver determinato dall'handle \*dell'istruzione Gestione Driver, che deve essere passato all'input in *InfoValuePtr* dall'applicazione. In questo caso, *InfoValuePtr* è sia un argomento di input che un argomento di output. L'handle dell'istruzione di input passato in \* *InfoValuePtr* deve essere stato allocato nell'argomento *ConnectionHandle*.  
  
 L'applicazione deve eseguire una copia dell'handle dell'istruzione di Gestione Driver prima di chiamare **SQLGetInfo** con questo tipo di informazioni, per garantire che l'handle non venga sovrascritto nell'output.  
  
 Questo tipo di informazioni viene implementato solo da Gestione Driver.  
  
 SQL_DRIVER_NAME(ODBC 1.0)  
 Una stringa di caratteri con il nome file del driver utilizzato per accedere all'origine dati.  
  
 SQL_DRIVER_ODBC_VER(ODBC 2.0)  
 Stringa di caratteri con la versione di ODBC supportata dal driver. La versione è nel formato "" e le prime due cifre sono la versione principale e le due cifre successive sono la versione secondaria. SQL_SPEC_MAJOR e SQL_SPEC_MINOR definiscono i numeri di versione principale e secondaria. Per la versione di ODBC descritta in questo manuale, questi sono 3 e 0 e il driver deve restituire "03.00".  
  
 Gestione Driver ODBC non modificherà il valore restituito di SQLGetInfo(SQL_DRIVER_ODBC_VER) per mantenere la compatibilità con le versioni precedenti per le applicazioni esistenti. Il driver specifica quale valore verrà restituito. Tuttavia, un driver che supporta l'estensibilità del tipo di dati C deve restituire 3.8 (o superiore) quando un'applicazione chiama SQLSetEnvAttr per impostare SQL_ATTR_ODBC_VERSION su 3.8.However, a driver that supports C data type extensibility must return 3.8 (or higher) when an application calls **SQLSetEnvAttr** to set SQL_ATTR_ODBC_VERSION to 3.8. Per ulteriori informazioni, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 SQL_DRIVER_VER (ODBC 1.0)  
 Una stringa di caratteri con la versione del driver e, facoltativamente, una descrizione del driver. Come minimo, la versione è nel formato " . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .  
  
 SQL_DROP_ASSERTION(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **DROP ASSERTION,** come definito in SQL-92, supportato dall'origine dati.  
  
 La maschera di bit seguente viene utilizzata per determinare quali clausole sono supportate:The following bitmask is used to determine which clauses are supported:  
  
 SQL_DA_DROP_ASSERTION  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà sempre questa opzione come supportata.  
  
 SQL_DROP_CHARACTER_SET(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **DROP CHARACTER SET,** come definito in SQL-92, supportato dall'origine dati.  
  
 La maschera di bit seguente viene utilizzata per determinare quali clausole sono supportate:The following bitmask is used to determine which clauses are supported:  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà sempre questa opzione come supportata.  
  
 SQL_DROP_COLLATION (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **DROP COLLATION,** come definito in SQL-92, supportato dall'origine dati.  
  
 La maschera di bit seguente viene utilizzata per determinare quali clausole sono supportate:The following bitmask is used to determine which clauses are supported:  
  
 SQL_DC_DROP_COLLATION  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà sempre questa opzione come supportata.  
  
 SQL_DROP_DOMAIN(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **DROP DOMAIN,** come definito in SQL-92, supportato dall'origine dati.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 Un driver di livello conforme allo standard SQL-92 Intermediate restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_DROP_SCHEMA(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **DROP SCHEMA,** come definito in SQL-92, supportato dall'origine dati.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 Un driver di livello conforme allo standard SQL-92 Intermediate restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_DROP_TABLE (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **DROP TABLE,** come definito in SQL-92, supportato dall'origine dati.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 Un driver di livello conforme a FIPS Transitional restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_DROP_TRANSLATION(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **DROP TRANSLATION,** come definito in SQL-92, supportato dall'origine dati.  
  
 La maschera di bit seguente viene utilizzata per determinare quali clausole sono supportate:The following bitmask is used to determine which clauses are supported:  
  
 SQL_DTR_DROP_TRANSLATION  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà sempre questa opzione come supportata.  
  
 SQL_DROP_VIEW(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **DROP VIEW,** come definito in SQL-92, supportato dall'origine dati.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 Un driver di livello conforme a FIPS Transitional restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore dinamico supportati dal driver. Questa maschera di bit contiene il primo sottoinsieme di attributi; per il secondo sottoinsieme, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES2.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali attributi sono supportati:  
  
 SQL_CA1_NEXT - Un *argomento FetchOrientation* di SQL_FETCH_NEXT è supportato in una chiamata a **SQLFetchScroll** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_ABSOLUTE gli argomenti *FetchOrientation* di SQL_FETCH_FIRST, SQL_FETCH_LAST e SQL_FETCH_ABSOLUTE sono supportati in una chiamata a **SQLFetchScroll** quando il cursore è un cursore dinamico. Il set di righe che verrà recuperato è indipendente dalla posizione corrente del cursore.  
  
 SQL_CA1_RELATIVE gli argomenti *FetchOrientation* di SQL_FETCH_PRIOR e SQL_FETCH_RELATIVE sono supportati in una chiamata a **SQLFetchScroll** quando il cursore è un cursore dinamico. Il set di righe che verrà recuperato dipende dalla posizione corrente del cursore. Si noti che questo è separato da SQL_FETCH_NEXT perché in un cursore forward-only, è supportata solo SQL_FETCH_NEXT.)  
  
 SQL_CA1_BOOKMARK - Un argomento *FetchOrientation* di SQL_FETCH_BOOKMARK è supportato in una chiamata a **SQLFetchScroll** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_LOCK_EXCLUSIVE- Un *LockType* argomento di SQL_LOCK_EXCLUSIVE è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_LOCK_NO_CHANGE: un argomento *LockType* di SQL_LOCK_NO_CHANGE è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_LOCK_UNLOCK: un argomento *LockType* di SQL_LOCK_UNLOCK è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_POS_POSITION: un argomento *Operation* di SQL_POSITION è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_POS_UPDATE: un argomento *Operation* di SQL_UPDATE è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_POS_DELETE: un argomento *Operation* di SQL_DELETE è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_POS_REFRESH: un argomento *Operation* di SQL_REFRESH è supportato in una chiamata a **SQLSetPos** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_POSITIONED_UPDATE - Un'istruzione UPDATE WHERE CURRENT OF SQL è supportata quando il cursore è un cursore dinamico. (Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre questa opzione come supportata.)  
  
 SQL_CA1_POSITIONED_DELETE - Un'istruzione DELETE WHERE CURRENT OF SQL è supportata quando il cursore è un cursore dinamico. (Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre questa opzione come supportata.)  
  
 SQL_CA1_SELECT_FOR_UPDATE: un'istruzione SQL SELECT FOR UPDATE è supportata quando il cursore è un cursore dinamico. (Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre questa opzione come supportata.)  
  
 SQL_CA1_BULK_ADD: un argomento *Operation* di SQL_ADD è supportato in una chiamata a **SQLBulkOperations** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK: un argomento *Operation* di SQL_UPDATE_BY_BOOKMARK è supportato in una chiamata a **SQLBulkOperations** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK: un argomento *Operation* di SQL_DELETE_BY_BOOKMARK è supportato in una chiamata a **SQLBulkOperations** quando il cursore è un cursore dinamico.  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK: un argomento *Operation* di SQL_FETCH_BY_BOOKMARK è supportato in una chiamata a **SQLBulkOperations** quando il cursore è un cursore dinamico.  
  
 Un driver di livello conforme SQL-92 intermedio in genere restituisce le opzioni SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE come supportato, perché supporta i cursori scorrevoli tramite l'istruzione SQL FETCH incorporata. Poiché questo non determina direttamente il supporto SQL sottostante, tuttavia, cursori scorrevoli potrebbero non essere supportati, anche per un driver di livello conforme SQL-92 intermedio.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore dinamico supportati dal driver. Questa maschera di bit contiene il secondo sottoinsieme di attributi; per il primo sottoinsieme, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali attributi sono supportati:  
  
 SQL_CA2_READ_ONLY_CONCURRENCY: è supportato un cursore dinamico di sola lettura, in cui non sono consentiti aggiornamenti. (L'attributo dell'istruzione SQL_ATTR_CONCURRENCY può essere SQL_CONCUR_READ_ONLY per un cursore dinamico).  
  
 SQL_CA2_LOCK_CONCURRENCY: un cursore dinamico che utilizza il livello più basso di blocco sufficiente per assicurarsi che la riga possa essere aggiornata sia supportata. L'attributo dell'istruzione SQL_ATTR_CONCURRENCY può essere SQL_CONCUR_LOCK per un cursore dinamico. Questi blocchi devono essere coerenti con il livello di isolamento della transazione impostato dall'attributo di connessione SQL_ATTR_TXN_ISOLATION.  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY: è supportato un cursore dinamico che utilizza il controllo della concorrenza ottimistica per confrontare le versioni di riga. È possibile SQL_CONCUR_ROWVER l'attributo dell'istruzione SQL_ATTR_CONCURRENCY per un cursore dinamico.  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY: è supportato un cursore dinamico che utilizza il controllo della concorrenza ottimistica per confrontare i valori. L'attributo dell'istruzione SQL_ATTR_CONCURRENCY può essere SQL_CONCUR_VALUES per un cursore dinamico.  
  
 SQL_CA2_SENSITIVITY_ADDITIONS: le righe aggiunte sono visibili a un cursore dinamico; il cursore può scorrere fino a quelle righe. (Dove queste righe vengono aggiunte al cursore è dipendente dal driver.)  
  
 SQL_CA2_SENSITIVITY_DELETIONS - Le righe eliminate non sono più disponibili per un cursore dinamico e non lasciano un "buco" nel set di risultati; dopo che il cursore dinamico scorre da una riga eliminata, non può tornare a tale riga.  
  
 SQL_CA2_SENSITIVITY_UPDATES: gli aggiornamenti alle righe sono visibili a un cursore dinamico; se il cursore dinamico scorre da e ritorna a una riga aggiornata, i dati restituiti dal cursore sono i dati aggiornati, non i dati originali.  
  
 SQL_CA2_MAX_ROWS_SELECT: l'attributo dell'istruzione SQL_ATTR_MAX_ROWS influisce sulle istruzioni **SELECT** quando il cursore è un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_INSERT: l'attributo dell'istruzione SQL_ATTR_MAX_ROWS influisce sulle istruzioni **INSERT** quando il cursore è un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_DELETE: l'attributo dell'istruzione SQL_ATTR_MAX_ROWS influisce sulle istruzioni **DELETE** quando il cursore è un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_UPDATE: l'attributo dell'istruzione SQL_ATTR_MAX_ROWS influisce sulle istruzioni **UPDATE** quando il cursore è un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_CATALOG: l'attributo dell'istruzione SQL_ATTR_MAX_ROWS influisce sui set di risultati **CATALOG** quando il cursore è un cursore dinamico.  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL: l'attributo dell'istruzione SQL_ATTR_MAX_ROWS influisce sulle istruzioni **SELECT**, **INSERT**, **DELETE**e **UPDATE** e **CATALOG,** quando il cursore è un cursore dinamico.  
  
 SQL_CA2_CRC_EXACT: il conteggio esatto delle righe è disponibile nel campo di diagnostica SQL_DIAG_CURSOR_ROW_COUNT quando il cursore è un cursore dinamico.  
  
 SQL_CA2_CRC_APPROXIMATE: nel campo di diagnostica SQL_DIAG_CURSOR_ROW_COUNT è disponibile un conteggio approssimativo delle righe quando il cursore è un cursore dinamico.  
  
 SQL_CA2_SIMULATE_NON_UNIQUE - Il driver non garantisce che le istruzioni di aggiornamento o eliminazione posizionate simulate avranno effetto solo su una riga quando il cursore è un cursore dinamico. è responsabilità dell'applicazione garantirlo. Se un'istruzione interessa più di una riga, **SQLExecute** o **SQLExecDirect** restituisce SQLSTATE 01001 [Conflitto di operazione cursore]. Per impostare questo comportamento, l'applicazione chiama **SQLSetStmtAttr** con l'attributo SQL_ATTR_SIMULATE_CURSOR impostato su SQL_SC_NON_UNIQUE.  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE - Il driver tenta di garantire che le istruzioni di aggiornamento o eliminazione posizionate simulate avranno effetto solo su una riga quando il cursore è un cursore dinamico. Il driver esegue sempre tali istruzioni, anche se potrebbero interessare più di una riga, ad esempio quando non è presente alcuna chiave univoca. Se un'istruzione interessa più di una riga, **SQLExecute** o **SQLExecDirect** restituisce SQLSTATE 01001 [Conflitto di operazione cursore]. Per impostare questo comportamento, l'applicazione chiama **SQLSetStmtAttr** con l'attributo SQL_ATTR_SIMULATE_CURSOR impostato su SQL_SC_TRY_UNIQUE.  
  
 SQL_CA2_SIMULATE_UNIQUE- Il driver garantisce che le istruzioni di aggiornamento o eliminazione posizionate simulate influiscano solo su una riga quando il cursore è un cursore dinamico. Se il driver non è in grado di garantire questo per una determinata istruzione, **SQLExecDirect** o **SQLPrepare** restituiscono SQLSTATE 01001 (conflitto di operazione cursore). Per impostare questo comportamento, l'applicazione chiama **SQLSetStmtAttr** con l'attributo SQL_ATTR_SIMULATE_CURSOR impostato su SQL_SC_UNIQUE.  
  
 SQL_EXPRESSIONS_IN_ORDERBY(ODBC 1.0)  
 Una stringa di caratteri: "Y" se l'origine dati supporta le espressioni nell'elenco **ORDER BY;** "N" in caso contrario.  
  
 SQL_FILE_USAGE (ODBC 2.0)  
 Valore SQLUSMALLINT che indica come un driver a livello singolo considera direttamente i file in un'origine dati:An SQLUSMALLINT value that indicates how a single-tier driver directly treats files in a data source:  
  
 SQL_FILE_NOT_SUPPORTED - Il driver non è un driver a livello singolo. Ad esempio, un driver ORACLE è un driver a due livelli.  
  
 SQL_FILE_TABLE: un driver a livello singolo considera i file in un'origine dati come tabelle. Ad esempio, un driver Xbase considera ogni file Xbase come una tabella.  
  
 SQL_FILE_CATALOG: un driver a livello singolo considera i file in un'origine dati come un catalogo. Ad esempio, un driver di Microsoft Access considera ogni file di Microsoft Access come un database completo.  
  
 Un'applicazione può utilizzare questo per determinare come gli utenti selezioneranno i dati. Ad esempio, gli utenti di Xbase spesso pensano ai dati come memorizzati nei file, mentre gli utenti di ORACLE e Microsoft Access generalmente pensano ai dati come memorizzati nelle tabelle.  
  
 Quando un utente seleziona un'origine dati Xbase, l'applicazione potrebbe visualizzare la finestra di dialogo comune **Di Windows File Open;** quando l'utente seleziona un'origine dati Microsoft Access o ORACLE, l'applicazione potrebbe visualizzare una finestra di dialogo **Seleziona tabella** personalizzata.  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore forward-only supportati dal driver. Questa maschera di bit contiene il primo sottoinsieme di attributi; per il secondo sottoinsieme, vedere SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali attributi sono supportati:  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Per le descrizioni di queste maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e sostituire "cursore forward-only" per "cursore dinamico" nelle descrizioni).  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore forward-only supportati dal driver. Questa maschera di bit contiene il secondo sottoinsieme di attributi; per il primo sottoinsieme, vedere SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali attributi sono supportati:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 Per le descrizioni di queste maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (e sostituire "cursore forward-only" per "cursore dinamico" nelle descrizioni).  
  
 SQL_GETDATA_EXTENSIONS(ODBC 2.0)  
 Maschera di bit SQLUINTEGER che enumera le estensioni a **SQLGetData**.  
  
 Le maschere di bit seguenti vengono utilizzate con il flag per determinare le estensioni comuni supportate dal driver per **SQLGetData**:  
  
 SQL_GD_ANY_COLUMN **SQLGetData** può essere chiamato per qualsiasi colonna non associata, inclusi quelli prima dell'ultima colonna associata. Si noti che le colonne devono essere chiamate in ordine crescente di numero di colonna, a meno che non venga restituito SQL_GD_ANY_ORDER.  
  
 SQL_GD_ANY_ORDER **SQLGetData** può essere chiamato per le colonne non associate in qualsiasi ordine. Si noti che **SQLGetData** può essere chiamato solo per le colonne dopo l'ultima colonna associata, a meno che non venga restituito SQL_GD_ANY_COLUMN.  
  
 SQL_GD_BLOCK **SQLGetData** può essere chiamato per una colonna non associata in qualsiasi riga in un blocco (in cui la dimensione del set di righe è maggiore di 1) di dati dopo il posizionamento in tale riga con **SQLSetPos**.  
  
 SQL_GD_BOUND **SQLGetData** può essere chiamato per le colonne associate oltre alle colonne non associate. Un driver non può restituire questo valore a meno che non restituisca anche SQL_GD_ANY_COLUMN.  
  
 SQL_GD_OUTPUT_PARAMS **SQLGetData** può essere chiamato per restituire i valori dei parametri di output. Per ulteriori informazioni, vedere Recupero di parametri di [output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
 **SQLGetData** è necessario per restituire i dati solo da colonne non associate che si verificano dopo l'ultima colonna associata, vengono chiamati in ordine di numero di colonna crescente e non sono in una riga in un blocco di righe.  
  
 Se un driver supporta i segnalibri (a lunghezza fissa o a lunghezza variabile), deve supportare la chiamata di SQLGetData nella colonna 0.If a driver supports bookmarks (either fixed-length or variable-length), it must support support calling **SQLGetData** on column 0. Questo supporto è necessario indipendentemente da ciò che il driver restituisce per una chiamata a **SQLGetInfo** con il SQL_GETDATA_EXTENSIONS *InfoType*.  
  
 SQL_GROUP_BY(ODBC 2.0)  
 Valore SQLUSMALLINT che specifica la relazione tra le colonne nella clausola **GROUP BY** e le colonne non aggregate nell'elenco di selezione:  
  
 SQL_GB_COLLATE: è possibile specificare una clausola **COLLATE** alla fine di ogni colonna di raggruppamento. (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED: le clausole **GROUP BY** non sono supportate. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT: la clausola **GROUP BY** deve contenere tutte le colonne non aggregate nell'elenco di selezione. Non può contenere altre colonne. Ad esempio, **SELECT DEPT, MAX(SALARY) FROM EMPLOYEE GROUP BY DEPT**. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT: la clausola **GROUP BY** deve contenere tutte le colonne non aggregate nell'elenco di selezione. Può contenere colonne non presenti nell'elenco di selezione. Ad esempio, **SELECT DEPT, MAX(SALARY) FROM EMPLOYEE GROUP BY DEPT, AGE**. (ODBC 2.0)  
  
 SQL_GB_NO_RELATION: le colonne nella clausola **GROUP BY** e nell'elenco di selezione non sono correlate. Il significato delle colonne non raggruppate e non aggregate nell'elenco di selezione dipende dall'origine dati. Ad esempio, **SELECT DEPT, SALARY DA EMPLOYEE GROUP BY DEPT, AGE**. (ODBC 2.0)  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre l'opzione SQL_GB_GROUP_BY_EQUALS_SELECT come supportata. Un driver di livello conforme allo standard SQL-92 Full restituirà sempre l'opzione SQL_GB_COLLATE come supportata. Se nessuna delle opzioni è supportata, la clausola **GROUP BY** non è supportata dall'origine dati.  
  
 SQL_IDENTIFIER_CASE (ODBC 1.0)  
 Un valore SQLUSMALLINT come segue:  
  
 SQL_IC_UPPER: gli identificatori in SQL non fanno distinzione tra maiuscole e minuscole e vengono archiviati in maiuscolo nel catalogo di sistema.  
  
 SQL_IC_LOWER: gli identificatori in SQL non fanno distinzione tra maiuscole e minuscole e vengono archiviati in minuscolo nel catalogo di sistema.  
  
 SQL_IC_SENSITIVE: gli identificatori in SQL fanno distinzione tra maiuscole e minuscole e vengono archiviati in lettere maiuscole e minuscole nel catalogo di sistema.  
  
 SQL_IC_MIXED: gli identificatori in SQL non fanno distinzione tra maiuscole e minuscole e vengono archiviati in lettere maiuscole e minuscole nel catalogo di sistema.  
  
 Poiché gli identificatori in SQL-92 non fanno mai distinzione tra maiuscole e minuscole, un driver conforme esclusivamente a SQL-92 (qualsiasi livello) non restituirà mai l'opzione SQL_IC_SENSITIVE come supportata.  
  
 SQL_IDENTIFIER_QUOTE_CHAR (ODBC 1.0)  
 Stringa di caratteri utilizzata come delimitatore iniziale e finale di un identificatore tra virgolette (delimitato) nelle istruzioni SQL. Gli identificatori passati come argomenti alle funzioni ODBC non devono essere racchiusi tra virgolette. Se l'origine dati non supporta gli identificatori tra virgolette, viene restituito uno spazio vuoto.  
  
 Questa stringa di caratteri può essere utilizzata anche per citare gli argomenti della funzione di catalogo quando l'attributo di connessione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE.  
  
 Poiché il carattere di virgoletta identificatore in SQL-92 è la virgoletta doppia ("), un driver conforme esclusivamente a SQL-92 restituirà sempre il carattere virgolette doppie.  
  
 SQL_INDEX_KEYWORDS(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le parole chiave nell'istruzione CREATE INDEX supportate dal driver:  
  
 SQL_IK_NONE : nessuna delle parole chiave è supportata.  
  
 SQL_IK_ASC: è supportata la parola chiave ASC.  
  
 SQL_IK_DESC: è supportata la parola chiave DESC.  
  
 SQL_IK_ALL: sono supportate tutte le parole chiave.  
  
 Per verificare se l'istruzione CREATE INDEX è supportata, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_DLL_INDEX.  
  
 SQL_INFO_SCHEMA_VIEWS(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le visualizzazioni nel INFORMATION_SCHEMA supportate dal driver. Le visualizzazioni in e il contenuto di INFORMATION_SCHEMA sono definiti in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale questa funzionalità deve essere supportata viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali visualizzazioni sono supportate:The following bitmasks are used to determine which views are supported:  
  
 SQL_ISV_ASSERTIONS: identifica le asserzioni del catalogo di proprietà di un determinato utente. (Livello completo)  
  
 SQL_ISV_CHARACTER_SETS: identifica i set di caratteri del catalogo a cui può accedere un determinato utente. (livello intermedio)  
  
 SQL_ISV_CHECK_CONSTRAINTS: identifica i vincoli CHECK di proprietà di un determinato utente. (livello intermedio)  
  
 SQL_ISV_COLLATIONS: identifica le regole di confronto dei caratteri per il catalogo a cui può accedere un determinato utente. (Livello completo)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE: identifica le colonne per il catalogo che dipendono dai domini definiti nel catalogo e sono di proprietà di un determinato utente. (livello intermedio)  
  
 SQL_ISV_COLUMN_PRIVILEGES: identifica i privilegi sulle colonne di tabelle persistenti disponibili o concesse da un determinato utente. (livello di transizione FIPS)  
  
 SQL_ISV_COLUMNS: identifica le colonne di tabelle persistenti a cui può accedere un determinato utente. (livello di transizione FIPS)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE: analogamente alla visualizzazione CONSTRAINT_TABLE_USAGE, vengono identificate le colonne per i vari vincoli di proprietà di un determinato utente. (livello intermedio)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE: identifica le tabelle utilizzate dai vincoli (referenziali, univoci e asserzioni) e di proprietà di un determinato utente. (livello intermedio)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS: identifica i vincoli di dominio (dei domini nel catalogo) a cui può accedere un determinato utente. (livello intermedio)  
  
 SQL_ISV_DOMAINS: identifica i domini definiti in un catalogo a cui l'utente può accedere. (livello intermedio)  
  
 SQL_ISV_KEY_COLUMN_USAGE: identifica le colonne definite nel catalogo vincolate come chiavi da un determinato utente. (livello intermedio)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS: identifica i vincoli referenziali di proprietà di un determinato utente. (livello intermedio)  
  
 SQL_ISV_SCHEMATA: identifica gli schemi di proprietà di un determinato utente. (livello intermedio)  
  
 SQL_ISV_SQL_LANGUAGES: identifica i livelli di conformità SQL, le opzioni e i dialetti supportati dall'implementazione SQL. (livello intermedio)  
  
 SQL_ISV_TABLE_CONSTRAINTS: identifica i vincoli di tabella di proprietà di un determinato utente. (livello intermedio)  
  
 SQL_ISV_TABLE_PRIVILEGES: identifica i privilegi per le tabelle persistenti disponibili o concessi da un determinato utente. (livello di transizione FIPS)  
  
 SQL_ISV_TABLES: identifica le tabelle permanenti definite in un catalogo a cui può accedere un determinato utente. (livello di transizione FIPS)  
  
 SQL_ISV_TRANSLATIONS: identifica le traduzioni dei caratteri per il catalogo a cui può accedere un determinato utente. (Livello completo)  
  
 SQL_ISV_USAGE_PRIVILEGES: identifica i privilegi USAGE per gli oggetti del catalogo disponibili o di proprietà di un determinato utente. (livello di transizione FIPS)  
  
 SQL_ISV_VIEW_COLUMN_USAGE: identifica le colonne da cui dipendono le visualizzazioni del catalogo di proprietà di un determinato utente. (livello intermedio)  
  
 SQL_ISV_VIEW_TABLE_USAGE: identifica le tabelle da cui dipendono le viste del catalogo di proprietà di un determinato utente. (livello intermedio)  
  
 SQL_ISV_VIEWS: identifica le tabelle visualizzate definite in questo catalogo a cui può accedere un determinato utente. (livello di transizione FIPS)  
  
 SQL_INSERT_STATEMENT(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che indica il supporto per le istruzioni **INSERT:An** SQLUINTEGER bitmask that indicates support for INSERT statements:  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_INTEGRITY(ODBC 1.0)  
 Una stringa di caratteri: "Y" se l'origine dati supporta la funzionalità di miglioramento dell'integrità; "N" in caso contrario.  
  
 Questo *InfoType* è stato rinominato per ODBC 3.0 dal SQL_ODBC_SQL_OPT_IEF *InfoType* di ODBC 2.0.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1 (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore keyset supportati dal driver. Questa maschera di bit contiene il primo sottoinsieme di attributi; per il secondo sottoinsieme, vedere SQL_KEYSET_CURSOR_ATTRIBUTES2.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali attributi sono supportati:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Per le descrizioni di queste maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e sostituire "cursore basato su keyset" per "cursore dinamico" nelle descrizioni).  
  
 Un driver di livello conforme SQL-92 intermedio in genere restituisce le opzioni SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE come supportato, perché il driver supporta i cursori scorrevoli tramite l'istruzione SQL FETCH incorporata. Poiché questo non determina direttamente il supporto SQL sottostante, tuttavia, cursori scorrevoli potrebbero non essere supportati, anche per un driver di livello conforme SQL-92 intermedio.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore keyset supportati dal driver. Questa maschera di bit contiene il secondo sottoinsieme di attributi; per il primo sottoinsieme, vedere SQL_KEYSET_CURSOR_ATTRIBUTES1.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali attributi sono supportati:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 Per le descrizioni di queste maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e sostituire "cursore basato su keyset" per "cursore dinamico" nelle descrizioni).  
  
 SQL_KEYWORDS(ODBC 2.0)  
 Stringa di caratteri che contiene un elenco delimitato da virgole di tutte le parole chiave specifiche dell'origine dati. Questo elenco non contiene parole chiave specifiche di ODBC o parole chiave utilizzate sia dall'origine dati che da ODBC. Questo elenco rappresenta tutte le parole chiave riservate; le applicazioni interoperabili non devono utilizzare queste parole nei nomi degli oggetti.  
  
 Per un elenco delle parole chiave ODBC, vedere [Parole chiave riservate](../../../odbc/reference/appendixes/reserved-keywords.md) [nell'Appendice C: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Il **valore #define** SQL_ODBC_KEYWORDS contiene un elenco delimitato da virgole di parole chiave ODBC.  
  
 Appendice C: Grammatica SQL  
  
 SQL_LIKE_ESCAPE_CLAUSE (ODBC 2.0)  
 Una stringa di caratteri: "Y" se l'origine dati supporta un carattere di escape per il carattere percentuale (%) e carattere di sottolineatura (_) in un predicato **LIKE** e il driver supporta la sintassi ODBC per la definizione di un carattere di escape predicato **LIKE;** "N" in caso contrario.  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS(ODBC 3.0)  
 Valore SQLUINTEGER che specifica il numero massimo di istruzioni simultanee attive in modalità asincrona che il driver può supportare in una determinata connessione. Se non esiste alcun limite specifico o il limite è sconosciuto, questo valore è zero.  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2.0)  
 Valore SQLUINTEGER che specifica la lunghezza massima (numero di caratteri esadecimali, esclusi il prefisso e il suffisso letterali restituiti da **SQLGetTypeInfo**) di un valore letterale binario in un'istruzione SQL. Ad esempio, il valore letterale binario 0xFFAA ha una lunghezza pari a 4.For example, the binary literal 0xFFAA has a length of 4. Se non è presente alcuna lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 SQL_MAX_CATALOG_NAME_LEN (ODBC 1.0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima di un nome di catalogo nell'origine dati. Se non è presente alcuna lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 Un driver FIPS Full conforme al livello restituirà almeno 128.  
  
 Questo *InfoType* è stato rinominato per ODBC 3.0 dal SQL_MAX_QUALIFIER_NAME_LEN *InfoType* di ODBC 2.0.  
  
 SQL_MAX_CHAR_LITERAL_LEN(ODBC 2.0)  
 Valore SQLUINTEGER che specifica la lunghezza massima (numero di caratteri, esclusi il prefisso e il suffisso letterali restituiti da **SQLGetTypeInfo**) di un valore letterale carattere in un'istruzione SQL. Se non è presente alcuna lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 SQL_MAX_COLUMN_NAME_LEN(ODBC 1.0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima di un nome di colonna nell'origine dati. Se non è presente alcuna lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 Un driver di livello FIPS Entry restituirà almeno 18. Un driver conforme al livello intermedio FIPS restituirà almeno 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY(ODBC 2.0)  
 Valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in una clausola **GROUP BY.** Se non esiste alcun limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Un driver di livello FIPS Entry restituirà almeno 6. Un driver conforme al livello intermedio FIPS restituirà almeno 15.  
  
 SQL_MAX_COLUMNS_IN_INDEX(ODBC 2.0)  
 Valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in un indice. Se non esiste alcun limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY(ODBC 2.0)  
 Valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in una clausola **ORDER BY.** Se non esiste alcun limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Un driver di livello FIPS Entry restituirà almeno 6. Un driver conforme al livello intermedio FIPS restituirà almeno 15.  
  
 SQL_MAX_COLUMNS_IN_SELECT(ODBC 2.0)  
 Valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in un elenco di selezione. Se non esiste alcun limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Un driver di livello FIPS Entry restituirà almeno 100. Un driver conforme al livello intermedio FIPS restituirà almeno 250.  
  
 SQL_MAX_COLUMNS_IN_TABLE(ODBC 2.0)  
 Valore SQLUSMALLINT che specifica il numero massimo di colonne consentite in una tabella. Se non esiste alcun limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Un driver di livello FIPS Entry restituirà almeno 100. Un driver conforme al livello intermedio FIPS restituirà almeno 250.  
  
 SQL_MAX_CONCURRENT_ACTIVITIES (ODBC 1.0)  
 Valore SQLUSMALLINT che specifica il numero massimo di istruzioni attive che il driver può supportare per una connessione. Un'istruzione viene definita come attiva se contiene risultati in sospeso, con il termine "risultati" che indica le righe di un'operazione **SELECT** o le righe interessate da un'operazione **INSERT**, **UPDATE**o **DELETE** (ad esempio un conteggio delle righe) o se si trova in uno stato NEED_DATA. Questo valore può riflettere una limitazione imposta dal driver o dall'origine dati. Se non esiste alcun limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Questo *InfoType* è stato rinominato per ODBC 3.0 dal SQL_ACTIVE_STATEMENTS *InfoType* di ODBC 2.0.  
  
 SQL_MAX_CURSOR_NAME_LEN (ODBC 1.0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima di un nome di cursore nell'origine dati. Se non è presente alcuna lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 Un driver di livello FIPS Entry restituirà almeno 18. Un driver conforme al livello intermedio FIPS restituirà almeno 128.  
  
 SQL_MAX_DRIVER_CONNECTIONS (ODBC 1.0)  
 Valore SQLUSMALLINT che specifica il numero massimo di connessioni attive che il driver può supportare per un ambiente. Questo valore può riflettere una limitazione imposta dal driver o dall'origine dati. Se non esiste alcun limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Questo *InfoType* è stato rinominato per ODBC 3.0 dal SQL_ACTIVE_CONNECTIONS ODBC 2.0 *InfoType.*  
  
 SQL_MAX_IDENTIFIER_LEN(ODBC 3.0)  
 Oggetto SQLUSMALLINT che indica la dimensione massima in caratteri supportata dall'origine dati per i nomi definiti dall'utente.  
  
 Un driver di livello FIPS Entry restituirà almeno 18. Un driver conforme al livello intermedio FIPS restituirà almeno 128.  
  
 SQL_MAX_INDEX_SIZE (ODBC 2.0)  
 Valore SQLUINTEGER che specifica il numero massimo di byte consentiti nei campi combinati di un indice. Se non esiste alcun limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 SQL_MAX_PROCEDURE_NAME_LEN(ODBC 1.0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima di un nome di routine nell'origine dati. Se non è presente alcuna lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 SQL_MAX_ROW_SIZE(ODBC 2.0)  
 Valore SQLUINTEGER che specifica la lunghezza massima di una singola riga in una tabella. Se non esiste alcun limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Un driver di livello FIPS Entry restituirà almeno 2.000. Un driver conforme al livello intermedio FIPS restituirà almeno 8.000.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG (ODBC 3.0)  
 Una stringa di caratteri: "Y" se la dimensione massima della riga restituita per il tipo di informazioni SQL_MAX_ROW_SIZE include la lunghezza di tutte le SQL_LONGVARCHAR e SQL_LONGVARBINARY colonne nella riga; "N" in caso contrario.  
  
 SQL_MAX_SCHEMA_NAME_LEN (ODBC 1.0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima di un nome di schema nell'origine dati. Se non è presente alcuna lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 Un driver di livello FIPS Entry restituirà almeno 18. Un driver conforme al livello intermedio FIPS restituirà almeno 128.  
  
 Questo *InfoType* è stato rinominato per ODBC 3.0 dal SQL_MAX_OWNER_NAME_LEN ODBC 2.0 *InfoType.*  
  
 SQL_MAX_STATEMENT_LEN(ODBC 2.0)  
 Valore SQLUINTEGER che specifica la lunghezza massima (numero di caratteri, inclusi gli spazi vuoti) di un'istruzione SQL. Se non è presente alcuna lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 SQL_MAX_TABLE_NAME_LEN (ODBC 1.0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima di un nome di tabella nell'origine dati. Se non è presente alcuna lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 Un driver di livello FIPS Entry restituirà almeno 18. Un driver conforme al livello intermedio FIPS restituirà almeno 128.  
  
 SQL_MAX_TABLES_IN_SELECT(ODBC 2.0)  
 Valore SQLUSMALLINT che specifica il numero massimo di tabelle consentite nella clausola **FROM** di un'istruzione **SELECT.** Se non esiste alcun limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 Un driver di livello FIPS Entry restituirà almeno 15. Un driver conforme al livello intermedio FIPS ne restituirà almeno 50.  
  
 SQL_MAX_USER_NAME_LEN(ODBC 2.0)  
 Valore SQLUSMALLINT che specifica la lunghezza massima di un nome utente nell'origine dati. Se non è presente alcuna lunghezza massima o la lunghezza è sconosciuta, questo valore è impostato su zero.  
  
 SQL_MULT_RESULT_SETS(ODBC 1.0)  
 Una stringa di caratteri: "Y" se l'origine dati supporta più set di risultati, "N" in caso contrario.  
  
 Per ulteriori informazioni su più set di risultati, vedere [Risultati multipli](../../../odbc/reference/develop-app/multiple-results.md).  
  
 SQL_MULTIPLE_ACTIVE_TXN(ODBC 1.0)  
 Una stringa di caratteri: "Y" se il driver supporta più di una transazione attiva contemporaneamente, "N" se solo una transazione può essere attiva in qualsiasi momento.  
  
 Le informazioni restituite per questo tipo di informazioni non sono valide nel caso di transazioni distribuite.  
  
 SQL_NEED_LONG_DATA_LEN(ODBC 2.0)  
 Una stringa di caratteri: "Y" se l'origine dati richiede la lunghezza di un valore di dati long (il tipo di dati è SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo di dati specifico dell'origine dati long) prima che tale valore venga inviato all'origine dati, "N" in caso contrario. Per ulteriori informazioni, vedere [Funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 SQL_NON_NULLABLE_COLUMNS(ODBC 1.0)  
 Valore SQLUSMALLINT che specifica se l'origine dati supporta NOT NULL nelle colonne:  
  
 SQL_NNC_NULL: tutte le colonne devono essere nullable.  
  
 SQL_NNC_NON_NULL: le colonne non possono essere nullable. L'origine dati supporta il vincolo di colonna **NOT NULL** nelle istruzioni **CREATE TABLE.**  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION(ODBC 2.0)  
 Valore SQLUSMALLINT che specifica dove vengono ordinati i valori NUL in un set di risultati:  
  
 SQL_NC_END: i valori NUL vengono ordinati alla fine del set di risultati, indipendentemente dalle parole chiave ASC o DESC.  
  
 SQL_NC_HIGH: i valori NUL vengono ordinati all'estremità superiore del set di risultati, a seconda delle parole chiave ASC o DESC.  
  
 SQL_NC_LOW: i valori NUL vengono ordinati nella parte inferiore del set di risultati, a seconda delle parole chiave ASC o DESC.  
  
 SQL_NC_START: i valori NUL vengono ordinati all'inizio del set di risultati, indipendentemente dalle parole chiave ASC o DESC.  
  
 SQL_NUMERIC_FUNCTIONS(ODBC 1.0)  
 Nota: il tipo di informazioni è stato introdotto in ODBC 1.0; ogni maschera di bit è etichettata con la versione in cui è stata introdotta.  
  
 Maschera di bit SQLUINTEGER che enumera le funzioni numeriche scalari supportate dal driver e dall'origine dati associata.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare le funzioni numeriche supportate:The following bitmasks are used to determine which numeric functions are supported:  
  
 SQL_FN_NUM_ABS (ODBC 1.0)SQL_FN_NUM_ACOS (ODBC 1.0 SQL_FN_NUM_DEGREES)SQL_FN_NUM_ASIN (ODBC 1.0)SQL_FN_NUM_ATAN (ODBC 1.0)SQL_FN_NUM_ATAN2 (ODBC 1.0)SQL_FN_NUM_CEILING (ODBC 1.0)SQL_FN_NUM_CEILING (ODBC 1.0)SQL_FN_NUM_COS (ODBC 1.0)SQL_FN_NUM_COT (ODBC 1.0)SQL_FN_NUM_ASIN (ODBC 2.0)SQL_FN_NUM_EXP (ODBC 1.0)SQL_FN_NUM_FLOOR (ODBC 1.0)SQL_FN_NUM_LOG (ODBC 1.0)SQL_FN_NUM_LOG10 (ODBC 2.0)SQL_FN_ NUM_MOD (ODBC 1.0)SQL_FN_NUM_PI (ODBC 1.0)SQL_FN_NUM_POWER (ODBC 2.0)SQL_FN_NUM_RADIANS (ODBC 2.0)SQL_FN_NUM_RAND (ODBC 1.0)SQL_FN_NUM_ROUND (ODBC 2.0)SQL_FN_NUM_SIGN (ODBC 1.0)SQL_FN_NUM_SIN (ODBC 1.0)SQL_FN_NUM_SQRT (ODBC 1.0)SQL_FN_NUM_TAN (ODBC 1.0)SQL_FN_NUM_TRUNCATE (ODBC 1.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE (ODBC 3.0)  
 Valore SQLUINTEGER che indica il livello dell'interfaccia *.x* ODBC 3 con cui il driver è conforme.  
  
 SQL_OIC_CORE: il livello minimo a cui tutti i driver ODBC devono essere conformi. Questo livello include elementi di interfaccia di base, ad esempio funzioni di connessione, funzioni per la preparazione e l'esecuzione di un'istruzione SQL, funzioni di metadati del set di risultati di base, funzioni di catalogo di base e così via.  
  
 SQL_OIC_LEVEL1: un livello che include la funzionalità del livello di conformità degli standard di base, oltre a cursori scorrevoli, segnalibri, aggiornamenti ed eliminazioni posizionati e così via.  
  
 SQL_OIC_LEVEL2: un livello che include la funzionalità del livello di conformità degli standard di livello 1, oltre a funzionalità avanzate come i cursori sensibili; aggiornare, eliminare e aggiornare in base ai segnalibri; supporto di stored procedure; funzioni di catalogo per le chiavi primarie ed esterne; supporto multi-catalogo; E così via.  
  
 Per ulteriori informazioni, consultate Livelli di [conformità dell'interfaccia](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 SQL_ODBC_VER(ODBC 1.0)  
 Stringa di caratteri con la versione di ODBC a cui è conforme Gestione Driver. La versione è nel formato ".".0000", dove le prime due cifre sono la versione principale e le due cifre successive sono la versione secondaria. Questo viene implementato solo in Gestione Driver.  
  
 SQL_OJ_CAPABILITIES (ODBC 2.01)  
 Maschera di bit SQLUINTEGER che enumera i tipi di outer join supportati dal driver e dall'origine dati. Le maschere di bit seguenti vengono utilizzate per determinare i tipi supportati:The following bitmasks are used to determine which types are supported:  
  
 SQL_OJ_LEFT- Sono supportati gli outer join di sinistra.  
  
 SQL_OJ_RIGHT- Sono supportati gli outer join di destra.  
  
 SQL_OJ_FULL- Sono supportati full outer join.  
  
 SQL_OJ_NESTED sono supportati gli outer join annidati.  
  
 SQL_OJ_NOT_ORDERED: i nomi di colonna nella clausola ON dell'outer join non devono essere nello stesso ordine dei rispettivi nomi di tabella nella clausola **OUTER JOIN.**  
  
 SQL_OJ_INNER - La tabella interna (la tabella destra in un left outer join o la tabella sinistra in un right outer join) può essere utilizzata anche in un inner join. Ciò non si applica ai full outer join, che non dispongono di una tabella interna.  
  
 SQL_OJ_ALL_COMPARISON_OPS: l'operatore di confronto nella clausola ON può essere uno degli operatori di confronto ODBC. Se questo bit non è impostato, solo l'operatore di confronto uguale ( ) può essere utilizzato in outer join.  
  
 Se nessuna di queste opzioni viene restituita come supportata, non è supportata alcuna clausola outer join.  
  
 Per informazioni sul supporto degli operatori di join relazionale in un'istruzione SELECT, come definito da SQL-92, vedere SQL_SQL92_RELATIONAL_JOIN_OPERATORS.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT(ODBC 2.0)  
 Una stringa di caratteri: "Y" se le colonne nella clausola **ORDER BY** devono essere nell'elenco di selezione; in caso contrario, "N".  
  
 SQL_PARAM_ARRAY_ROW_COUNTS(ODBC 3.0)  
 Oggetto SQLUINTEGER che enumera le proprietà del driver per quanto riguarda la disponibilità dei conteggi delle righe in un'esecuzione con parametri. Ha i seguenti valori:  
  
 SQL_PARC_BATCH: per ogni set di parametri sono disponibili singoli conteggi di righe. Questo è concettualmente equivalente al driver che genera un batch di istruzioni SQL, una per ogni set di parametri nella matrice. Le informazioni estese sull'errore possono essere recuperate utilizzando il campo descrittore SQL_PARAM_STATUS_PTR.  
  
 SQL_PARC_NO_BATCH: è disponibile un solo conteggio delle righe, ovvero il conteggio cumulativo delle righe risultante dall'esecuzione dell'istruzione per l'intera matrice di parametri. Questo è concettualmente equivalente a trattare l'istruzione con la matrice di parametri completa come un'unica unità atomica. Gli errori vengono gestiti come se fosse stata eseguita un'istruzione.  
  
 SQL_PARAM_ARRAY_SELECTS(ODBC 3.0)  
 Oggetto SQLUINTEGER che enumera le proprietà del driver per quanto riguarda la disponibilità di set di risultati in un'esecuzione con parametri. Ha i seguenti valori:  
  
 SQL_PAS_BATCH: è disponibile un set di risultati per ogni set di parametri. Questo è concettualmente equivalente al driver che genera un batch di istruzioni SQL, una per ogni set di parametri nella matrice.  
  
 SQL_PAS_NO_BATCH: è disponibile un solo set di risultati, che rappresenta il set di risultati cumulativo risultante dall'esecuzione dell'istruzione per l'intera matrice di parametri. Questo è concettualmente equivalente a trattare l'istruzione con la matrice di parametri completa come un'unica unità atomica.  
  
 SQL_PAS_NO_SELECT: un driver non consente l'esecuzione di un'istruzione di generazione del set di risultati con una matrice di parametri.  
  
 SQL_PROCEDURE_TERM (ODBC 1.0)  
 Una stringa di caratteri con il nome del fornitore dell'origine dati per una routine. ad esempio, "procedura di database", "stored procedure", "procedura", "pacchetto" o "query archiviata".  
  
 SQL_PROCEDURES (ODBC 1.0)  
 Una stringa di caratteri: "Y" se l'origine dati supporta le procedure e il driver supporta la sintassi di chiamata della procedura ODBC; "N" in caso contrario.  
  
 SQL_POS_OPERATIONS(ODBC 2.0)  
 Maschera di bit SQLINTEGER che enumera le operazioni di supporto in **SQLSetPos**.  
  
 Le maschere di bit seguenti vengono utilizzate con il flag per determinare quali opzioni sono supportate.  
  
 SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0) (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE(ODBC 2.0)  
 Un valore SQLUSMALLINT come segue:  
  
 SQL_IC_UPPER: gli identificatori tra virgolette in SQL non fanno distinzione tra maiuscole e minuscole e vengono archiviati in maiuscolo nel catalogo di sistema.  
  
 SQL_IC_LOWER: gli identificatori tra virgolette in SQL non fanno distinzione tra maiuscole e minuscole e vengono archiviati in minuscolo nel catalogo di sistema.  
  
 SQL_IC_SENSITIVE: gli identificatori tra virgolette in SQL fanno distinzione tra maiuscole e minuscole e vengono archiviati in lettere maiuscole e minuscole nel catalogo di sistema. In un database compatibile con SQL-92, gli identificatori tra virgolette fanno sempre distinzione tra maiuscole e minuscole.  
  
 SQL_IC_MIXED: gli identificatori tra virgolette in SQL non fanno distinzione tra maiuscole e minuscole e vengono archiviati in lettere maiuscole e minuscole nel catalogo di sistema.  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre SQL_IC_SENSITIVE.  
  
 SQL_ROW_UPDATES(ODBC 1.0)  
 Una stringa di caratteri: "Y" se un cursore basato su keyset o misto mantiene le versioni di riga o i valori per tutte le righe recuperate e pertanto può rilevare eventuali aggiornamenti apportati a una riga da qualsiasi utente dall'ultimo recupero della riga. (Questo vale solo per gli aggiornamenti, non per le eliminazioni o inserimenti.) Il driver può restituire il flag SQL_ROW_UPDATED alla matrice di stato della riga quando viene chiamato **SQLFetchScroll.** In caso contrario, "N".  
  
 SQL_SCHEMA_TERM (ODBC 1.0)  
 Una stringa di caratteri con il nome del fornitore dell'origine dati per uno schema. ad esempio, "proprietario", "ID autorizzazione" o "Schema".  
  
 La stringa di caratteri può essere restituita in lettere maiuscole, minuscole o miste.  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre "schema".  
  
 Questo *InfoType* è stato rinominato per ODBC 3.0 dal SQL_OWNER_TERM *InfoType* di ODBC 2.0.  
  
 SQL_SCHEMA_USAGE(ODBC 2.0)  
 Maschera di bit SQLUINTEGER che enumera le istruzioni in cui è possibile utilizzare gli schemi:An SQLUINTEGER bitmask enumerating the statements in which schemas can be used:  
  
 SQL_SU_DML_STATEMENTS gli schemi sono supportati in tutte le istruzioni Data Manipulation Language: **SELECT**, **INSERT**, **UPDATE**, **DELETE**e, se supportate, **SELECT FOR UPDATE** e istruzioni di aggiornamento ed eliminazione posizionate.  
  
 SQL_SU_PROCEDURE_INVOCATION: gli schemi sono supportati nell'istruzione di chiamata di routine ODBC.  
  
 SQL_SU_TABLE_DEFINITION gli schemi sono supportati in tutte le istruzioni di definizione di tabella: **CREATE TABLE**, **CREATE VIEW**, **ALTER TABLE**, DROP **TABLE**e **DROP VIEW**.  
  
 SQL_SU_INDEX_DEFINITION: gli schemi sono supportati in tutte le istruzioni di definizione dell'indice: **CREATE INDEX** e **DROP INDEX**.  
  
 SQL_SU_PRIVILEGE_DEFINITION gli schemi sono supportati in tutte le istruzioni di definizione dei privilegi: **GRANT** e **REVOKE**.  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre le opzioni di SQL_SU_DML_STATEMENTS, SQL_SU_TABLE_DEFINITION e SQL_SU_PRIVILEGE_DEFINITION, come indicato.  
  
 Questo *InfoType* è stato rinominato per ODBC 3.0 dal SQL_OWNER_USAGE ODBC 2.0 *InfoType.*  
  
 SQL_SCROLL_OPTIONS (ODBC 1.0)  
 Nota: il tipo di informazioni è stato introdotto in ODBC 1.0; ogni maschera di bit è etichettata con la versione in cui è stata introdotta.  
  
 Maschera di bit SQLUINTEGER che enumera le opzioni di scorrimento supportate per i cursori scorrevoli.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare le opzioni supportate:The following bitmasks are used to determine which options are supported:  
  
 SQL_SO_FORWARD_ONLY- Il cursore scorre solo in avanti. (ODBC 1.0)  
  
 SQL_SO_STATIC: i dati nel set di risultati sono statici. (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN: il driver salva e utilizza le chiavi per ogni riga del set di risultati. (ODBC 1.0)  
  
 SQL_SO_DYNAMIC: il driver mantiene le chiavi per ogni riga del set di righe (la dimensione del set di chiavi corrisponde alla dimensione del set di righe). (ODBC 1.0)  
  
 SQL_SO_MIXED: il driver mantiene le chiavi per ogni riga nel keyset e la dimensione del set di chiavi è maggiore della dimensione del set di righe. Il cursore è basato su keyset all'interno del keyset e dinamico all'esterno del keyset. (ODBC 1.0)  
  
 Per informazioni sui cursori scorrevoli, consultate [Cursori scorrevoli.](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
 SQL_SEARCH_PATTERN_ESCAPE(ODBC 1.0)  
 Stringa di caratteri che specifica ciò che il driver supporta come carattere di escape che consente l'uso dei metacaratteri di corrispondenza del modello di sottolineatura (_) e segno di percentuale (%) come caratteri validi nei criteri di ricerca. Questo carattere di escape si applica solo agli argomenti della funzione di catalogo che supportano le stringhe di ricerca. Se questa stringa è vuota, il driver non supporta un carattere di escape del criterio di ricerca.  
  
 Poiché questo tipo di informazioni non indica il supporto generale del carattere di escape nel predicato **LIKE,** SQL-92 non include i requisiti per questa stringa di caratteri.  
  
 Questo *InfoType* è limitato alle funzioni di catalogo. Per una descrizione dell'utilizzo del carattere di escape nelle stringhe dei criteri di ricerca, vedere [Argomenti del valore di modello](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
 SQL_SERVER_NAME(ODBC 1.0)  
 Una stringa di caratteri con il nome effettivo del server specifico dell'origine dati; utile quando il nome di un'origine dati viene utilizzato durante **SQLConnect**, **SQLDriverConnect**e **SQLBrowseConnect**.  
  
 SQL_SPECIAL_CHARACTERS(ODBC 2.0)  
 Stringa di caratteri che contiene tutti i caratteri speciali (ovvero tutti i caratteri ad eccezione di a a z, A- , da 0 a 9 e caratteri di sottolineatura) che possono essere utilizzati in un nome di identificatore, ad esempio un nome di tabella, un nome di colonna o un nome di indice, nell'origine dati. Ad esempio, """. Se un identificatore contiene uno o più di questi caratteri, l'identificatore deve essere un identificatore delimitato.  
  
 SQL_SQL_CONFORMANCE (ODBC 3.0)  
 Valore SQLUINTEGER che indica il livello di SQL-92 supportato dal driver:  
  
 SQL_SC_SQL92_ENTRY- Livello SQL-92 di livello base.  
  
 SQL_SC_FIPS127_2_TRANSITIONAL - FIPS 127-2 livello transitorio conforme.  
  
 SQL_SC_SQL92_FULL - Compatibile con SQL-92 a livello completo.  
  
 SQL_SC_ SQL92_INTERMEDIATE: compatibile SQL-92 di livello intermedio.  
  
 SQL_SQL92_DATETIME_FUNCTIONS(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le funzioni scalari datetime supportate dal driver e dall'origine dati associata, come definito in SQL-92.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali funzioni datetime sono supportate:The following bitmasks are used to determine which datetime functions are supported:  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le regole supportate per una chiave esterna in un'istruzione **DELETE,** come definito in SQL-92.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate dall'origine dati:The following bitmasks are used to determine which clauses are supported by the data source:  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 Un driver di livello conforme a FIPS Transitional restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le regole supportate per una chiave esterna in un'istruzione **UPDATE,** come definito in SQL-92.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate dall'origine dati:The following bitmasks are used to determine which clauses are supported by the data source:  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 Un driver di livello conforme allo standard SQL-92 Full restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_SQL92_GRANT(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole supportate nell'istruzione **GRANT,** come definito in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale questa funzionalità deve essere supportata viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate dall'origine dati:The following bitmasks are used to determine which clauses are supported by the data source:  
  
 SQL_SG_DELETE_TABLE (livello di ingresso)SQL_SG_INSERT_COLUMN (livello di ingresso)SQL_SG_INSERT_TABLE (livello di ingresso)SQL_SG_INSERT_TABLE (livello di ingresso) SQL_SG_REFERENCES_TABLE SQL_SG_REFERENCES_COLUMN (livello di ingresso)SQL_SG_SELECT_TABLE (livello di ingresso)SQL_SG_UPDATE_COLUMN (livello di ingresso)SQL_SG_UPDATE_TABLE (livello di ingresso) SQL_SG_USAGE_ON_DOMAIN (livello di transizione FIPS)SQL_SG_USAGE_ON_CHARACTER_SET (livello di transizione FIPS)SQL_SG_USAGE_ON_COLLATION (livello transitorio FIPS)SQL_SG_USAGE_ON_TRANSLATION (livello transitorio FIPS)SQL_SG_USAGE_ON_COLLATION (livello transitorio FIPS)SQL_SG_USAGE_ON_COLLATION (livello transitorio FIPS)SQL_SG_USAGE_ON_COLLATION (livello di transizione FIPS)SQL_SG_USAGE_ON_COLLATION (livello transitorio FIPS)SQL_SG_USAGE_ON_COLLATION (livello di transizione FIPS)SQL_SG_USAGE_ON_COLLATION (livello transitorio FIPS)SQL_SG_USAGE_ON_COLLATION (livello transitorio FIPS)SQL_SG_USAGE_ON_COLLATION (livello transitorio FIPS)SQL_SG_USAGE_ON_COLLATION (livello transitorio FIPS)SQL_SG_USAGE_ON_COLLATION (livello di transizione FIPS)SQL_SG_USAGE_ON_COLLATION (livello di transizione FIPS)SQL_SG_USAGE_ON_COLLATION (livello di transizione FIPS)SQL_SG_USAGE_ON_COLLATION (livello di transizione FIPS)SQL_SG_USAGE_ON_COLLATION (livello di transizione FIPS)SQL_SG_USAGE_ON_COLLATION (livello di transizione FIPS)SQL_SG_USAGE_ON_COLLATION (livello di transizione FIPS)SQL_SG_USAGE_ON_COLLATION (livello di livello)SQL_SG_WITH_GRANT_OPTION (livello di ingresso)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le funzioni scalari con valore numerico supportate dal driver e dall'origine dati associata, come definito in SQL-92.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare le funzioni numeriche supportate:The following bitmasks are used to determine which numeric functions are supported:  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera i predicati supportati in un'istruzione **SELECT,** come definito in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale questa funzionalità deve essere supportata viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali opzioni sono supportate dall'origine dati:The following bitmasks are used to determine which options are supported by the data source:  
  
 SQL_SP_BETWEEN (Livello di ingresso)SQL_SP_COMPARISON (livello di ingresso)SQL_SP_EXISTS (livello di ingresso)SQL_SP_IN (livello di ingresso)SQL_SP_ISNOTNULL (livello di ingresso)SQL_SP_ISNULL SQL_SP_LIKE (livello di ingresso)SQL_SP_MATCH_FULL (livello completo)SQL_SP_MATCH_PARTIAL (livello completo)SQL_SP_MATCH_UNIQUE_FULL (livello completo)SQL_SP_MATCH_UNIQUE_PARTIAL (livello completo)SQL_SP_OVERLAPS (livello di transizione FIPS)SQL_SP_QUANTIFIED_COMPARISON (livello di ingresso)SQL_SP_UNIQUE (livello di ingresso)  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera gli operatori di join relazionali supportati in un'istruzione **SELECT,** come definito in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale questa funzionalità deve essere supportata viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali opzioni sono supportate dall'origine dati:The following bitmasks are used to determine which options are supported by the data source:  
  
 SQL_SRJO_CORRESPONDING_CLAUSE (livello intermedio)SQL_SRJO_CROSS_JOIN (livello intermedio)SQL_SRJO_EXCEPT_JOIN (livello intermedio)SQL_SRJO_FULL_OUTER_JOIN (livello intermedio) SQL_SRJO_INNER_JOIN (livello transitorio FIPS)SQL_SRJO_INTERSECT_JOIN (livello intermedio)SQL_SRJO_LEFT_OUTER_JOIN (livello di transizione FIPS)SQL_SRJO_NATURAL_JOIN (livello transitorio FIPS)SQL_SRJO_RIGHT_OUTER_JOIN (livello di transizione FIPS)SQL_SRJO_UNION_JOIN (livello completo)  
  
 SQL_SRJO_INNER_JOIN indica il supporto per la sintassi **INNER JOIN,** non per la funzionalità di inner join. Il supporto per la sintassi **INNER JOIN** è FIPS TRANSITIONAL, mentre il supporto per la funzionalità di inner join è **ENTRY**.  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole supportate nell'istruzione **REVOKE,** come definito in SQL-92, supportata dall'origine dati.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale questa funzionalità deve essere supportata viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate dall'origine dati:The following bitmasks are used to determine which clauses are supported by the data source:  
  
 SQL_SR_CASCADE (livello di transizione FIPS) SQL_SR_DELETE_TABLE (livello di ingresso)SQL_SR_GRANT_OPTION_FOR (livello intermedio) SQL_SR_INSERT_COLUMN (livello intermedio)SQL_SR_INSERT_TABLE (livello di ingresso)SQL_SR_REFERENCES_COLUMN (livello di ingresso)SQL_SR_REFERENCES_TABLE (livello di ingresso)SQL_SR_RESTRICT (livello di ingresso SQL_SR_SELECT_TABLE)SQL_SR_RESTRICT (livello di ingresso)SQL_SR_UPDATE_COLUMN (livello di ingresso)SQL_SR_UPDATE_TABLE (livello di ingresso)SQL_SR_USAGE_ON_DOMAIN SQL_SR_USAGE_ON_CHARACTER_ SET (FIPS Transitional level)SQL_SR_USAGE_ON_COLLATION (livello di transizione FIPS)SQL_SR_USAGE_ON_TRANSLATION (livello di transizione FIPS)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le espressioni del costruttore del valore di riga supportate in un'istruzione **SELECT,** come definito in SQL-92. Le maschere di bit seguenti vengono utilizzate per determinare quali opzioni sono supportate dall'origine dati:The following bitmasks are used to determine which options are supported by the data source:  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le funzioni scalari di stringa supportate dal driver e dall'origine dati associata, come definito in SQL-92.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali funzioni stringa sono supportate:The following bitmasks are used to determine which string functions are supported:  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le espressioni di valore supportate, come definito in SQL-92.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale questa funzionalità deve essere supportata viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali opzioni sono supportate dall'origine dati:The following bitmasks are used to determine which options are supported by the data source:  
  
 SQL_SVE_CASE (livello intermedio)SQL_SVE_CAST (livello transitorio FIPS)SQL_SVE_COALESCE (livello intermedio)SQL_SVE_NULLIF (livello intermedio)  
  
 SQL_STANDARD_CLI_CONFORMANCE(ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera lo standard CLI o gli standard a cui è conforme il driver. Le maschere di bit seguenti vengono utilizzate per determinare i livelli con cui il driver è conforme:  
  
 SQL_SCC_XOPEN_CLI_VERSION1: il driver è conforme all'open Group CLI versione 1.  
  
 SQL_SCC_ISO92_CLI: il driver è conforme all'INTERFACCIA DI rete 92.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1 (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore statico supportati dal driver. Questa maschera di bit contiene il primo sottoinsieme di attributi; per il secondo sottoinsieme, vedere SQL_STATIC_CURSOR_ATTRIBUTES2.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali attributi sono supportati:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Per le descrizioni di queste maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e sostituire "cursore statico" per "cursore dinamico" nelle descrizioni).  
  
 Un driver di livello conforme SQL-92 intermedio in genere restituisce le opzioni SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE come supportato, perché il driver supporta i cursori scorrevoli tramite l'istruzione SQL FETCH incorporata. Poiché questo non determina direttamente il supporto SQL sottostante, tuttavia, cursori scorrevoli potrebbero non essere supportati, anche per un driver di livello conforme SQL-92 intermedio.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2 (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che descrive gli attributi di un cursore statico supportati dal driver. Questa maschera di bit contiene il secondo sottoinsieme di attributi; per il primo sottoinsieme, vedere SQL_STATIC_CURSOR_ATTRIBUTES1.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali attributi sono supportati:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 Per le descrizioni di queste maschere di bit, vedere SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (e sostituire "cursore statico" per "cursore dinamico" nelle descrizioni).  
  
 SQL_STRING_FUNCTIONS(ODBC 1.0)  
 Nota: il tipo di informazioni è stato introdotto in ODBC 1.0; ogni maschera di bit è etichettata con la versione in cui è stata introdotta.  
  
 Maschera di bit SQLUINTEGER che enumera le funzioni stringa scalari supportate dal driver e dall'origine dati associata.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali funzioni stringa sono supportate:The following bitmasks are used to determine which string functions are supported:  
  
 SQL_FN_STR_ASCII (ODBC 1.0)SQL_FN_STR_BIT_LENGTH (ODBC 3.0)SQL_FN_STR_CHAR (ODBC 1.0)SQL_FN_STR_CHAR_LENGTH (ODBC 3.0)SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0)SQL_FN_STR_CONCAT (ODBC 3.0)SQL_FN_STR_CONCAT (ODBC 1.0)SQL_FN_STR_DIFFERENCE (ODBC 1.0)SQL_FN_STR_INSERT SQL_FN_STR_DIFFERENCE (ODBC 1.0)SQL_FN_STR_LCASE (ODBC 1.0)SQL_FN_STR_LEFT (ODBC 1.0)SQL_FN_STR_LEFT (ODBC 1.0)SQL_FN_STR_LENGTH ODBC (1.0)SQL_FN_STR_LOCATE (ODBC 1.0) SQL_FN_STR_LTRIM (ODBC 1.0) 1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0) SQL_FN_STR_REPEAT (ODBC 1.0)SQL_FN_STR_REPLACE (ODBC 1.0)SQL_FN_STR_RIGHT (ODBC 1.0)SQL_FN_STR_RTRIM (ODBC 1.0)SQL_FN_STR_RTRIM (ODBC 1.0 SQL_FN_STR_SOUNDEX)SQL_FN_STR_SPACE (ODBC 2.0)SQL_FN_STR_SUBSTRING (ODBC 1.0)SQL_FN_STR_UCASE (ODBC 1.0) (ODBC 1.0)  
  
 Se un'applicazione può chiamare la funzione scalare **LOCATE** con gli argomenti *string_exp1* *, string_exp2*e *start,* il driver restituisce la maschera di bit SQL_FN_STR_LOCATE. Se un'applicazione può chiamare la funzione scalare LOCATE solo con gli argomenti *string_exp1* e *string_exp2,* il driver restituisce la maschera di bit SQL_FN_STR_LOCATE_2. I driver che supportano completamente la funzione scalare **LOCATE** restituiscono entrambe le maschere di bit.  
  
 Per altre informazioni, vedere [Funzioni stringa](../../../odbc/reference/appendixes/string-functions.md) nell'Appendice E, "Funzioni scalari".  
  
 SQL_SUBQUERIES(ODBC 2.0)  
 Maschera di bit SQLUINTEGER che enumera i predicati che supportano le sottoquery:An SQLUINTEGER bitmask enumeracing the predicates that support subqueries:  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 La maschera di bit SQL_SQ_CORRELATED_SUBQUERIES indica che tutti i predicati che supportano le sottoquery supportano sottoquery correlate.  
  
 Un driver di livello conforme all'ingresso SQL-92 restituirà sempre una maschera di bit in cui sono impostati tutti questi bit.  
  
 SQL_SYSTEM_FUNCTIONS(ODBC 1.0)  
 Maschera di bit SQLUINTEGER che enumera le funzioni di sistema scalari supportate dal driver e dall'origine dati associata.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali funzioni di sistema sono supportate:The following bitmasks are used to determine which system functions are supported:  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM(ODBC 1.0)  
 Una stringa di caratteri con il nome del fornitore dell'origine dati per una tabella. ad esempio, "tabella" o "file".  
  
 Questa stringa di caratteri può essere maiuscola, minuscola o mista.  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre "tabella".  
  
 SQL_TIMEDATE_ADD_INTERVALS(ODBC 2.0)  
 Maschera di bit SQLUINTEGER che enumera gli intervalli timestamp supportati dal driver e dall'origine dati associata per la funzione scalare TIMESTAMPADD.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali intervalli sono supportati:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Un driver di livello conforme a FIPS Transitional restituirà sempre una maschera di bit in cui sono impostati tutti questi bit.  
  
 SQL_TIMEDATE_DIFF_INTERVALS(ODBC 2.0)  
 Maschera di bit SQLUINTEGER che enumera gli intervalli timestamp supportati dal driver e dall'origine dati associata per la funzione scalare TIMESTAMPDIFF.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali intervalli sono supportati:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Un driver di livello conforme a FIPS Transitional restituirà sempre una maschera di bit in cui sono impostati tutti questi bit.  
  
 SQL_TIMEDATE_FUNCTIONS(ODBC 1.0)  
 Nota: il tipo di informazioni è stato introdotto in ODBC 1.0; ogni maschera di bit è etichettata con la versione in cui è stata introdotta.  
  
 Maschera di bit SQLUINTEGER che enumera le funzioni di data e ora scalari supportate dal driver e dall'origine dati associata.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali funzioni di data e ora sono supportate:The following bitmasks are used to determine which date and time functions are supported:  
  
 SQL_FN_TD_CURTIME SQL_FN_TD_CURDATE SQL_FN_TD_CURRENT_TIMESTAMP SQL_FN_TD_CURRENT_TIME SQL_FN_TD_CURRENT_DATE SQL_FN_TD_DAYNAME (ODBC 1.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0)SQL_FN_TD_DAYOFWEEK (ODBC 1.0)SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0)(ODBC 1.0 SQL_FN_TD_EXTRACT)SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0) SQL_FN_TD_DAYOFMONTH (ODBC 3.0) SQL_FN_TD_DAYOFMONTH (ODBC 3.0) SQL_FN_TD_DAYOFMONTH (ODBC 3.0) SQL_FN_TD_DAYOFMONTH (ODBC 3.0) SQL_FN_TD_HOUR (ODBC 3.0) (ODBC 1.0 SQL_FN_TD_MINUTE) SQL_FN_TD_HOUR (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0)SQL_FN_TD_MONTH (ODBC 1.0) (ODBC 1.0) 1.0)SQL_FN_TD_MONTHNAME (ODBC 2.0)SQL_FN_TD_NOW (ODBC 1.0)SQL_FN_TD_QUARTER (ODBC 1.0)SQL_FN_TD_SECOND (ODBC 1.0)SQL_FN_TD_TIMESTAMPADD (ODBC 2.0)SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0)SQL_FN_TD_WEEK (ODBC 1.0)SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE(ODBC 1.0)  
 Nota: il tipo di informazioni è stato introdotto in ODBC 1.0; ogni valore restituito è etichettato con la versione in cui è stato introdotto.  
  
 Valore SQLUSMALLINT che descrive il supporto delle transazioni nel driver o nell'origine dati:An SQLUSMALLINT value describing the transaction support in the driver or data source:  
  
 SQL_TC_NONE: le transazioni non supportate. (ODBC 1.0)  
  
 SQL_TC_DML le transazioni possono contenere solo istruzioni DML (Data Manipulation Language) (**SELECT**, **INSERT**, **UPDATE**, **DELETE**). Le istruzioni DDL (Data Definition Language) rilevate in una transazione causano un errore. (ODBC 1.0)  
  
 SQL_TC_DDL_COMMIT: le transazioni possono contenere solo istruzioni DML. Le istruzioni DDL (**CREATE TABLE**, **DROP INDEX**e così via) rilevate in una transazione determinano il commit della transazione. (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE: le transazioni possono contenere solo istruzioni DML. Le istruzioni DDL rilevate in una transazione vengono ignorate. (ODBC 2.0)  
  
 SQL_TC_ALL: le transazioni possono contenere istruzioni DDL e istruzioni DML in qualsiasi ordine. (ODBC 1.0)  
  
 Poiché il supporto delle transazioni è obbligatorio in SQL-92, un driver conforme SQL-92 [qualsiasi livello] non restituirà mai SQL_TC_NONE.  
  
 SQL_TXN_ISOLATION_OPTION(ODBC 1.0)  
 Maschera di bit SQLUINTEGER che enumera i livelli di isolamento delle transazioni disponibili dal driver o dall'origine dati.  
  
 Le maschere di bit seguenti vengono utilizzate con il flag per determinare le opzioni supportate:  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 Per una descrizione di questi livelli di isolamento, vedere la descrizione di SQL_DEFAULT_TXN_ISOLATION.  
  
 Per impostare il livello di isolamento della transazione, un'applicazione chiama **SQLSetConnectAttr** per impostare l'attributo SQL_ATTR_TXN_ISOLATION. Per ulteriori informazioni, vedere [Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre SQL_TXN_SERIALIZABLE come supportato. Un driver di livello conforme a FIPS Transitional restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_UNION (ODBC 2.0)  
 Maschera di bit SQLUINTEGER che enumera il supporto per la clausola **UNION:**  
  
 SQL_U_UNION: l'origine dati supporta la clausola **UNION.**  
  
 SQL_U_UNION_ALL: l'origine dati supporta la parola chiave **ALL** nella clausola **UNION.** **SQLGetInfo** restituisce SQL_U_UNION e SQL_U_UNION_ALL in questo caso.  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre entrambe queste opzioni come supportate.  
  
 SQL_USER_NAME (ODBC 1.0)  
 Una stringa di caratteri con il nome utilizzato in un determinato database, che può essere diverso dal nome di accesso.  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3.0)  
 Stringa di caratteri che indica l'anno di pubblicazione della specifica Open Group con cui la versione di Gestione driver ODBC è completamente conforme.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 Una stringa di caratteri: "Y" se l'utente può eseguire tutte le routine restituite da **SQLProcedures**; "N" se possono essere restituite procedure che l'utente non può eseguire.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 Una stringa di caratteri: "Y" se all'utente sono garantiti i privilegi **SELECT** per tutte le tabelle restituite da **SQLTables**; "N" se potrebbero essere restituite tabelle a cui l'utente non può accedere.  
  
 SQL_ACTIVE_ENVIRONMENTS(ODBC 3.0)  
 Valore SQLUSMALLINT che specifica il numero massimo di ambienti attivi che il driver può supportare. Se non esiste alcun limite specificato o il limite è sconosciuto, questo valore è impostato su zero.  
  
 SQL_AGGREGATE_FUNCTIONS(ODBC 3.0)  
 Una maschera di bit SQLUINTEGER che enumera il supporto per le funzioni di aggregazione:An SQLUINTEGER bitmask enumerating support for aggregation functions:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Un driver di livello conforme allo standard SQL-92 Entry restituirà sempre tutte queste opzioni come supportate.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **ALTER DOMAIN,** come definito in SQL-92, supportata dall'origine dati. Un driver conforme al livello completo SQL-92 restituirà sempre tutte le maschere di bit. Un valore restituito pari a "0" indica che l'istruzione **ALTER DOMAIN** non è supportata.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale questa funzionalità deve essere supportata viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT: l'aggiunta di un vincolo di dominio è supportata (livello completo)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT \<- modifica \<del dominio> impostare la clausola predefinita del dominio> è supportata (livello completo)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION: \<la clausola di definizione del nome del vincolo> è supportata per il vincolo di dominio di denominazione (livello intermedio)The type - constraint name definition clause> is supported for naming domain constraint (Intermediate level)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT: \<è supportata la clausola del vincolo di dominio di eliminazione> (livello completo)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT \<- modifica \<del dominio> eliminare la clausola predefinita del dominio> è supportata (livello completo)  
  
 I bit seguenti specificano gli attributi di vincolo supportati \<> se \<è supportato l'> vincolo di dominio aggiuntivo (il bit di SQL_AD_ADD_DOMAIN_CONSTRAINT è impostato):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (Livello completo)SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (Livello completo)SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (livello completo)SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 Maschera di bit SQLUINTEGER che enumera le clausole nell'istruzione **ALTER TABLE** supportata dall'origine dati.  
  
 Il livello di conformità SQL-92 o FIPS in corrispondenza del quale questa funzionalità deve essere supportata viene visualizzato tra parentesi accanto a ogni maschera di bit.  
  
 Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:  
  
 SQL_AT_ADD_COLUMN_COLLATION: \<è supportata la clausola di aggiunta di> di colonna, con funzionalità per specificare le regole di confronto delle colonne (livello completo) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT: \<è supportata l'aggiunta di una clausola di> di colonna, con funzionalità per specificare i valori predefiniti delle colonne (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE: \<è supportata la> di aggiunta di colonne (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT: \<è supportata l'aggiunta di una colonna> clausola, con funzionalità per specificare i vincoli di colonna (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT: \<è supportata l'aggiunta di un vincolo di tabella> la clausola (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION: \<la definizione del nome del vincolo> è supportata per la denominazione dei vincoli di colonna e di tabella (livello intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE \<- eliminare la colonna> è supportato CASCADE (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT \<- modifica \<colonna> clausola predefinita di colonna di rilascio> è supportato (livello intermedio) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT \<- colonna di rilascio> è supportato RESTRICT (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT \<- drop column> è supportato RESTRICT (livello FIPS Transitional) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT \<- modifica \<la colonna> imposta la clausola predefinita della colonna> è supportata (livello intermedio) (ODBC 3.0)  
  
 I bit seguenti specificano gli attributi del vincolo di supporto \<> se è supportata la specifica di vincoli di colonna o di tabella (il bit SQL_AT_ADD_CONSTRAINT è impostato):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (livello completo) (ODBC 3.0)SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (livello completo) (ODBC 3.0)SQL_AT_CONSTRAINT_DEFERRABLE (livello completo) (ODBC 3.0)SQL_AT_CONSTRAINT_NON_DEFERRABLE (livello completo) (ODBC 3.0)  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 Valore SQLUINTEGER che indica il livello di supporto asincrono nel driver:  
  
 SQL_AM_CONNECTION: è supportata l'esecuzione asincrona a livello di connessione. Tutti gli handle di istruzione associati a un determinato handle di connessione sono in modalità asincrona o tutti in modalità sincrona. Un handle di istruzione su una connessione non può essere in modalità asincrona mentre un altro handle di istruzione sulla stessa connessione è in modalità sincrona e viceversa.  
  
 SQL_AM_STATEMENT: è supportata l'esecuzione asincrona a livello di istruzione. Alcuni handle di istruzione associati a un handle di connessione possono essere in modalità asincrona, mentre altri handle di istruzione nella stessa connessione sono in modalità sincrona.  
  
 SQL_AM_NONE: la modalità asincrona non è supportata.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Maschera di bit SQLUINTEGER che enumera il comportamento del driver rispetto alla disponibilità dei conteggi delle righe. Le maschere di bit seguenti vengono utilizzate insieme al tipo di informazioni:  
  
 SQL_BRC_ROLLED_UP: i conteggi delle righe per le istruzioni INSERT, DELETE o UPDATE consecutive vengono raggruppati in uno. Se questo bit non è impostato, i conteggi delle righe sono disponibili per ogni istruzione.  
  
 SQL_BRC_PROCEDURES: i conteggi delle righe, se presenti, sono disponibili quando un batch viene eseguito in una stored procedure. Se i conteggi delle righe sono disponibili, è possibile eseguire il rollup o essere disponibili singolarmente, a seconda del bit SQL_BRC_ROLLED_UP.  
  
 SQL_BRC_EXPLICIT: i conteggi delle righe, se presenti, sono disponibili quando un batch viene eseguito direttamente chiamando **SQLExecute** o **SQLExecDirect**. Se i conteggi delle righe sono disponibili, è possibile eseguire il rollup o essere disponibili singolarmente, a seconda del bit SQL_BRC_ROLLED_UP.  
  
## <a name="example"></a>Esempio  
 **SQLGetInfo** restituisce elenchi di opzioni supportate come maschera di bit SQLUINTEGER in*InfoValuePtr*. La maschera di bit per ogni opzione viene utilizzata con il flag per determinare se l'opzione è supportata.  
  
 Ad esempio, un'applicazione potrebbe utilizzare il codice seguente per determinare se la funzione scalare SUBSTRING è supportata dal driver associato alla connessione.  
  
 Per un altro esempio di utilizzo di **SQLGetInfo**, vedere [Funzione SQLTables](../../../odbc/reference/syntax/sqltables-function.md).  
  
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
 Restituzione dell'impostazione di un attributo di connessioneReturning the setting of a connection attribute  
 [Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 Determinare se un driver supporta una funzioneDetermining whether a driver supports a function  
 [SQLGetFunctions Function](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 Restituzione dell'impostazione di un attributo di istruzioneReturning the setting of a statement attribute  
 [Funzione SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 Restituzione di informazioni sui tipi di dati di un'origine datiReturning information about a data source's data types  
 [Funzione SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
