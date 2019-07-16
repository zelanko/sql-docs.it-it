---
title: Funzione SQLProcedureColumns | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedureColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedureColumns
helpviewer_keywords:
- SQLProcedureColumns function [ODBC]
ms.assetid: 4ca37b28-a6df-465b-8988-d422d37fc025
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a5a869d38782478b69ce47656455c38c2b4645b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005746"
---
# <a name="sqlprocedurecolumns-function"></a>Funzione SQLProcedureColumns
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLProcedureColumns** restituisce l'elenco dei parametri di input e output, nonché le colonne che costituiscono il set di risultati per le procedure specificate. Il driver restituisce le informazioni come set di risultati dell'istruzione specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLProcedureColumns(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     ProcName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *CatalogName*  
 [Input] Nome del catalogo della procedura. Se un driver supporta i cataloghi per alcune procedure ma non per altri, ad esempio quando il driver recupera i dati da diversi DBMS, una stringa vuota ("") indica le procedure che non dispone di cataloghi. *CatalogName* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *CatalogName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *CatalogName* è un normale argomento; viene considerato letteralmente e relativi case è significativa. Per altre informazioni, vedere [argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Input] Lunghezza in caratteri della **CatalogName*.  
  
 *SchemaName*  
 [Input] Criterio di ricerca di stringa per i nomi dello schema di procedura. Se un driver supporta gli schemi per alcune procedure ma non per altri, ad esempio quando il driver recupera i dati da diversi DBMS, una stringa vuota ("") indica le procedure che non dispongono degli schemi.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *SchemaName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *SchemaName* è un argomento di valore modello; viene considerato letteralmente e relativi case è significativa.  
  
 *NameLength2*  
 [Input] Lunghezza in caratteri della **SchemaName*.  
  
 *ProcName*  
 [Input] Criterio di ricerca di stringa per i nomi delle procedure.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *ProcName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *ProcName* è un argomento di valore modello; viene considerato letteralmente e relativi case è significativa.  
  
 *NameLength3*  
 [Input] Lunghezza in caratteri della **ProcName*.  
  
 *ColumnName*  
 [Input] Criterio di ricerca di stringa dei nomi di colonna.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *ColumnName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *ColumnName* è un argomento di valore modello; viene considerato letteralmente e relativi case è significativa.  
  
 *NameLength4*  
 [Input] Lunghezza in caratteri della **ColumnName*.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLProcedureColumns** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* SQL_HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLProcedureColumns** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti dal Driver Gestore. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|24000|Stato del cursore non valido|Il cursore è stato aperto scegliere il *StatementHandle*, e **SQLFetch** oppure **SQLFetchScroll** fosse stata chiamata. Questo errore viene restituito da Gestione Driver, se **SQLFetch** oppure **SQLFetchScroll** non restituisce SQL_NO_DATA e viene restituito dal driver se **SQLFetch** oppure **SQLFetchScroll** è stato restituito SQL_NO_DATA.<br /><br /> Un cursore è stato aperto nel *StatementHandle*, ma **SQLFetch** oppure **SQLFetchScroll** non fosse stata chiamata.|  
|40001|Errore di serializzazione.|Il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLError** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle*. Quindi la funzione è stata chiamata nuovamente sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY009|Utilizzo non valido del puntatore null|L'attributo di istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE, il *CatalogName* argomento era un puntatore null e il SQL_CATALOG_NAME *InfoType* restituisce che i nomi di catalogo sono supportati.<br /><br /> (DM) l'attributo di istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE e il *SchemaName*, *ProcName*, o *ColumnName* argomento era un puntatore null.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione aynschronous era ancora in esecuzione quando è stata chiamata la funzione SQLProcedureColumns.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore di uno degli argomenti di lunghezza nome era minore di 0 ma non uguale a SQL_NTS.<br /><br /> Il valore di uno degli argomenti di lunghezza nome superato il valore di lunghezza massima consentita per il catalogo corrispondente, schema, procedure o nome di colonna.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|È stato specificato un catalogo di procedure e i driver o origine dati non supporta cataloghi.<br /><br /> È stato specificato uno schema di procedure e i driver o origine dati non supporta gli schemi.<br /><br /> È stato specificato un criterio di ricerca di stringa per lo schema procedura, nome della routine o nome di colonna e l'origine dati non supporta criteri di ricerca per uno o più di questi argomenti.<br /><br /> La combinazione delle impostazioni correnti degli attributi di istruzione SQL_ATTR_CURSOR_TYPE e SQL_ATTR_CONCURRENCY non era supportata dall'origine dati o driver.<br /><br /> L'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_VARIABLE e l'attributo SQL_ATTR_CURSOR_TYPE di istruzione è stata impostata su un tipo di cursore per i quali il driver non supporta i segnalibri.|  
|HYT00|Timeout|Il periodo di timeout è scaduto prima che l'origine dati ha restituito il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 Questa funzione viene in genere utilizzata prima dell'esecuzione dell'istruzione per recuperare informazioni sui parametri di procedure e le colonne che costituiscono il set di risultati o i set restituiti dalla procedura, se presente. Per altre informazioni, vedere [procedure](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  **SQLProcedureColumns** potrebbe non restituire tutte le colonne utilizzate da una procedura. Ad esempio, un driver potrebbe restituire solo le informazioni sui parametri usati da una procedura e non le colonne in un set di risultati che vengono generati.  
  
 Il *SchemaName*, *ProcName*, e *ColumnName* argomenti accettano criteri di ricerca. Per altre informazioni sui pattern di ricerca validi, vedere [argomenti del valore criterio](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Per altre informazioni su uso generale, gli argomenti e i dati restituiti di funzioni di catalogo ODBC, vedere [funzioni di catalogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLProcedureColumns** restituisce i risultati come un set di risultati standard, ordinato in base PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME e COLUMN_TYPE. Vengono restituiti i nomi di colonna per ogni procedura nell'ordine seguente: il nome del valore restituito, i nomi di ogni parametro nella chiamata di procedura (nell'ordine di chiamata) e quindi i nomi di ogni colonna nel set di risultati restituito dalla procedura (nell'ordine delle colonne).  
  
 Le applicazioni devono essere associati a colonne specifiche del driver relativa alla fine del set di risultati. Per altre informazioni, vedere [i dati restituiti dalle funzioni catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
 Per determinare la lunghezza effettiva delle colonne PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME e COLUMN_NAME, un'applicazione può chiamare **SQLGetInfo** con il SQL_MAX_ SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, PROCEDURE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN opzioni.  
  
 Le colonne seguenti sono state rinominate per ODBC 3. *x*. Le modifiche ai nomi di colonna non influenzano la compatibilità con le versioni precedenti poiché nelle applicazioni associati dal numero di colonna.  
  
|Colonna ODBC 2.0|ODBC 3. *x* colonna|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|PROCEDURE _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 Le colonne seguenti sono stati aggiunti al set di risultati restituito da **SQLProcedureColumns** per ODBC 3. *x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 Nella tabella seguente elenca le colonne nel set di risultati. Le colonne aggiuntive oltre a 19 (IS_NULLABLE) colonna possono essere definite dal driver. Un'applicazione deve accedere a colonne specifiche del driver procede a ritroso dalla fine del set di risultati anziché specificare una posizione ordinale esplicita. Per altre informazioni, vedere [i dati restituiti dalle funzioni catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome colonna|Numero colonna|Tipo di dati|Commenti|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|Nome del catalogo della procedura. NULL se non applicabile all'origine dati. Se un driver supporta i cataloghi per alcune procedure ma non per altri utenti, ad esempio quando i dati vengono recuperati dai diversi DBMS, restituisce una stringa vuota ("") per tutte le procedure che non dispone di cataloghi.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|Nome dello schema della procedura. NULL se non applicabile all'origine dati. Se un driver supporta gli schemi per alcune procedure ma non per altri utenti, ad esempio quando i dati vengono recuperati dai diversi DBMS, restituisce una stringa vuota ("") per tutte le procedure che non dispongono degli schemi.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Non NULL varchar|Nome della procedura. Per una routine che non dispone di un nome, viene restituita una stringa vuota.|  
|COLUMN_NAME (ODBC 2.0)|4|Non NULL varchar|Nome colonna della procedura. Il driver restituisce una stringa vuota per una colonna di procedure che non dispone di un nome.|  
|COLUMN_TYPE (ODBC 2.0)|5|Smallint non NULL|Definisce la colonna di procedure come parametro o una colonna del set di risultati:<br /><br /> SQL_PARAM_TYPE_UNKNOWN: Colonna della procedura è un parametro il cui tipo è sconosciuto. ODBC (1.0)<br /><br /> SQL_PARAM_INPUT: Colonna della procedura è un parametro di input. ODBC (1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: Colonna della procedura è un parametro di input/output. ODBC (1.0)<br /><br /> SQL_PARAM_OUTPUT: Colonna della procedura è un parametro di output. (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE: Colonna della procedura è il valore restituito della procedura. (ODBC 2.0)<br /><br /> SQL_RESULT_COL: Colonna della procedura è una colonna del set di risultati. ODBC (1.0)|  
|DATA_TYPE (ODBC 2.0)|6|Smallint non NULL|Tipo di dati SQL. Può trattarsi di un tipo di dati SQL ODBC o un tipo di dati specifici del driver SQL. Per i tipi di dati datetime e interval, questa colonna restituisce i tipi di dati concisa (ad esempio, SQL_TYPE_TIME o SQL_INTERVAL_YEAR_TO_MONTH). Per un elenco di tipi di dati SQL ODBC validi, vedere [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) nell'appendice d: Tipi di dati. Per informazioni sui tipi di dati specifici del driver SQL, vedere la documentazione del driver.|  
|TYPE_NAME (ODBC 2.0)|7|Non NULL varchar|Nome del tipo di dati dipende dall'origine dati; ad esempio, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" o "() CHAR FOR BIT DATA".|  
|COLUMN_SIZE (ODBC 2.0)|8|Integer|La dimensione della colonna della colonna della procedura sull'origine dati. Viene restituito NULL per i tipi di dati in cui le dimensioni di colonna non sono applicabile. Per altre informazioni riguardanti la precisione, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice d: Tipi di dati.|  
|BUFFER_LENGTH (ODBC 2.0)|9|Integer|La lunghezza in byte dei dati trasferiti in un' **SQLGetData** oppure **SQLFetch** operazione se si specifica SQL_C_DEFAULT. Per i dati numerici, questa dimensione può essere diversa rispetto alla dimensione dei dati archiviati nell'origine dati. Per altre informazioni, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), nell'appendice d: Tipi di dati.|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|Le cifre decimali della colonna della procedura sull'origine dati. Viene restituito NULL per i tipi di dati in cui cifre decimali non sono applicabile. Per altre informazioni relative al cifre decimali, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), nell'appendice d: Tipi di dati.|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|Per i tipi di dati numerici, 10 o 2.<br /><br /> Se 10, i valori di COLUMN_SIZE e DECIMAL_DIGITS assegnare il numero di cifre decimali è consentita per la colonna. Ad esempio, una colonna DECIMAL(12,5) restituirebbe un NUM_PREC_RADIX pari a 10, un valore di COLUMN_SIZE pari a 12 e un DECIMAL_DIGITS pari a 5; una colonna di tipo FLOAT potrebbe restituire un NUM_PREC_RADIX pari a 10, un valore di COLUMN_SIZE 15 e DECIMAL_DIGITS NULL.<br /><br /> Se è 2, i valori di COLUMN_SIZE e DECIMAL_DIGITS assegnare il numero di bit consentiti nella colonna. Ad esempio, una colonna di tipo FLOAT potrebbe restituire un NUM_PREC_RADIX 2, un valore di COLUMN_SIZE pari a 53 e DECIMAL_DIGITS NULL.<br /><br /> Viene restituito NULL per i tipi di dati in cui NUM_PREC_RADIX non è applicabile.|  
|NULLABLE (ODBC 2.0)|12|Smallint non NULL|Indica se la colonna di routine accetta un valore NULL:<br /><br /> SQL_NO_NULLS: Colonna della procedura non accetta valori NULL.<br /><br /> SQL_NULLABLE: Colonna della procedura accetta valori NULL.<br /><br /> SQL_NULLABLE_UNKNOWN: Non è noto se la colonna procedura accetta valori NULL.|  
|SEZIONE OSSERVAZIONI (ODBC 2.0)|13|Varchar|Descrizione della colonna della procedura.|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|Valore predefinito della colonna.<br /><br /> Se è stato specificato NULL come valore predefinito, questa colonna è la parola NULL, non è racchiuso tra virgolette. Se il valore predefinito non può essere rappresentato senza troncamento, questa colonna contiene troncata, con nessuna inclusione tra virgolette singole. Se è stato specificato alcun valore predefinito, questa colonna è NULL.<br /><br /> Il valore di COLUMN_DEF può essere utilizzato nella generazione di una nuova definizione di colonna, tranne quando contiene il valore di TRONCAMENTO.|  
|SQL_DATA_TYPE (ODBC 3.0)|15|Smallint non NULL|Il valore del tipo di dati SQL perché viene visualizzato nel campo SQL_DESC_TYPE del descrittore. Questa colonna corrisponde alla colonna DATA_TYPE, tranne i tipi di dati Data/ora e intervallo.<br /><br /> Per i tipi di dati datetime e interval, il campo SQL_DATA_TYPE nel set di risultati restituirà SQL_DATETIME o SQL_INTERVAL, e il campo SQL_DATETIME_SUB restituirà il codice secondario per il tipo di dati datetime o intervallo specifico. (Vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|Il codice di sottotipo per i tipi di dati Data/ora e intervallo. Per gli altri tipi di dati in questa colonna viene restituito NULL.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|Integer|Colonna di tipo la lunghezza massima in byte di un carattere o dati binari. Per gli tutti gli altri tipi di dati, il valore di questa colonna è NULL.|  
|ORDINAL_POSITION (ODBC 3.0)|18|Integer non NULL|Per i parametri inpui e outpui, la posizione ordinale del parametro nella definizione della stored procedure (parametro in ordine crescente in, a partire da 1). Per un valore restituito (se presente), viene restituito 0. Per le colonne di set di risultati, imposta la posizione ordinale della colonna nel risultato, con la prima colonna nel set in fase di risultati numero 1. Se sono presenti più set di risultati, le posizioni ordinali di colonna vengono restituite in modo specifico del driver.|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|"NO" se la colonna non ammette valori null.<br /><br /> "Sì" se la colonna ammette valori null.<br /><br /> Quando non è noto se i valori Null sono supportati, in questa colonna viene restituita una stringa di lunghezza zero.<br /><br /> Per determinare il supporto di valori Null vengono seguite le regole ISO. In un sistema DBMS conforme a ISO SQL non vengono restituite stringhe vuote.<br /><br /> Il valore restituito per questa colonna è diverso dal valore restituito per la colonna NULLABLE. (Vedere la descrizione della colonna che ammette valori null).|  
  
## <a name="code-example"></a>Esempio di codice  
 Visualizzare [le chiamate di procedura](../../../odbc/reference/develop-app/procedure-calls.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultati|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Il recupero di una singola riga o un blocco di dati in una direzione di tipo forward-only|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Imposta il recupero di un blocco di dati o lo scorrimento di un risultato|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Restituzione di un elenco di procedure in un'origine dati|[Funzione SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
