---
title: Funzione SQLProcedureColumns . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d81e44b116ed6f26319d31430999a61a8a17f21
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306852"
---
# <a name="sqlprocedurecolumns-function"></a>Funzione SQLProcedureColumns
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLProcedureColumns** restituisce l'elenco dei parametri di input e output, nonché le colonne che costituiscono il set di risultati per le procedure specificate. Il driver restituisce le informazioni come set di risultati nell'istruzione specificata.  
  
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
 [Ingresso] Handle di istruzione.  
  
 *CatalogName*  
 [Ingresso] Nome del catalogo delle procedure. Se un driver supporta i cataloghi per alcune procedure ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, una stringa vuota ("") indica le procedure che non dispongono di cataloghi. *CatalogName* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo statement SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *CatalogName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *CatalogName* è un argomento ordinario; viene trattato letteralmente, e il suo caso è significativo. Per ulteriori informazioni, vedere [Argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Ingresso] Lunghezza in caratteri di*nomeCatalogo*.  
  
 *Nome Schema*  
 [Ingresso] Criterio di ricerca di stringhe per i nomi degli schemi di procedura. Se un driver supporta gli schemi per alcune procedure ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, una stringa vuota ("") indica le procedure che non dispongono di schemi.  
  
 Se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *SchemaName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *SchemaName* è un argomento di valore di modello; viene trattato letteralmente, e il suo caso è significativo.  
  
 *NameLength2*  
 [Ingresso] Lunghezza in caratteri di :*NomeSchema*.  
  
 *Nomeprocesso*  
 [Ingresso] Criterio di ricerca di stringhe per i nomi delle routine.  
  
 Se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *ProcName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *ProcName* è un argomento di valore di modello; viene trattato letteralmente, e il suo caso è significativo.  
  
 *NameLength3*  
 [Ingresso] Lunghezza in caratteri di :*NomeProc*.  
  
 *ColumnName*  
 [Ingresso] Criterio di ricerca di stringhe per i nomi delle colonne.  
  
 Se l'attributo statement SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *ColumnName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *ColumnName* è un argomento di valore di modello; viene trattato letteralmente, e il suo caso è significativo.  
  
 *NameLunghezza4*  
 [Ingresso] Lunghezza in caratteri di*nomeColonna*.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLProcedureColumns** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLProcedureColumns** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|24000|Stato del cursore non valido|Un cursore era aperto su *StatementHandle*e **SQLFetch** o **SQLFetchScroll** era stato chiamato. Questo errore viene restituito da Gestione Driver se **SQLFetch** o **SQLFetchScroll** non ha restituito SQL_NO_DATA e viene restituito dal driver se **SQLFetch** o **SQLFetchScroll** ha restituito SQL_NO_DATA.<br /><br /> Un cursore era aperto su *StatementHandle*, ma **SQLFetch** o **SQLFetchScroll** non era stato chiamato.|  
|40001|Errore di serializzazione|È stato eseguito il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLError** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*. Quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|I009|Utilizzo non valido del puntatore null|L'attributo dell'istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE, l'argomento *CatalogName* è un puntatore null e il SQL_CATALOG_NAME *InfoType* restituisce che i nomi dei cataloghi sono supportati.<br /><br /> (DM) l'attributo dell'istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE e l'argomento *SchemaName*, *ProcName*o *ColumnName* era un puntatore null.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione aynschronous era ancora in esecuzione quando è stata chiamata la funzione SQLProcedureColumns.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore di uno degli argomenti della lunghezza del nome è minore di 0 ma non uguale a SQL_NTS.<br /><br /> Il valore di uno degli argomenti di lunghezza del nome ha superato il valore di lunghezza massima per il nome di catalogo, schema, procedura o colonna corrispondente.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|È stato specificato un catalogo di procedure e il driver o l'origine dati non supporta i cataloghi.<br /><br /> È stato specificato uno schema di procedura e il driver o l'origine dati non supporta gli schemi.<br /><br /> È stato specificato un criterio di ricerca di stringa per lo schema della routine, il nome della routine o il nome della colonna e l'origine dati non supporta i criteri di ricerca per uno o più di tali argomenti.<br /><br /> La combinazione delle impostazioni correnti degli attributi di istruzione SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE non è supportata dal driver o dall'origine dati.<br /><br /> L'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_VARIABLE e l'attributo dell'istruzione SQL_ATTR_CURSOR_TYPE è stato impostato su un tipo di cursore per il quale il driver non supporta i segnalibri.|  
|HYT00|Timeout|Periodo di timeout scaduto prima che l'origine dati restituisca il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 Questa funzione viene in genere utilizzata prima dell'esecuzione dell'istruzione per recuperare informazioni sui parametri della routine e sulle colonne che costituiscono il set di risultati o i set restituiti dalla routine, se presenti. Per altre informazioni, vedere [Routine](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  **SQLProcedureColumns** potrebbe non restituire tutte le colonne utilizzate da una routine. Ad esempio, un driver potrebbe restituire solo informazioni sui parametri utilizzati da una procedura e non le colonne in un set di risultati che genera.  
  
 Gli argomenti *SchemaName*, *ProcName*e *ColumnName* accettano criteri di ricerca. Per ulteriori informazioni sui criteri di ricerca validi, vedere [Argomenti del valore del modello](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Per ulteriori informazioni sull'utilizzo generale, gli argomenti e i dati restituiti delle funzioni di catalogo ODBC, vedere Funzioni di [catalogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLProcedureColumns** restituisce i risultati come set di risultati standard, ordinati per PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME e COLUMN_TYPE. I nomi delle colonne vengono restituiti per ogni routine nell'ordine seguente: il nome del valore restituito, i nomi di ogni parametro nella chiamata di routine (nell'ordine di chiamata) e quindi i nomi di ogni colonna nel set di risultati restituito dalla procedura (in ordine di colonna).  
  
 Le applicazioni devono associare colonne specifiche del driver rispetto alla fine del set di risultati. Per ulteriori informazioni, vedere [Dati restituiti da Funzioni di catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
 Per determinare le lunghezze effettive delle colonne PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME e COLUMN_NAME, un'applicazione può chiamare **SQLGetInfo** con le opzioni SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_PROCEDURE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
 Le colonne seguenti sono state rinominate per ODBC 3. *x*. Le modifiche del nome della colonna non influiscono sulla compatibilità con le versioni precedenti perché le applicazioni vengono associate in base al numero di colonna.  
  
|Colonna ODBC 2.0|ODBC 3. *x* colonna|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|_OWNER procedura|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 Le colonne seguenti sono state aggiunte al set di risultati restituito da **SQLProcedureColumns** per ODBC 3. *x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 Nella tabella seguente sono elencate le colonne del set di risultati. Colonne aggiuntive oltre la colonna 19 (IS_NULLABLE) possono essere definite dal driver. Un'applicazione deve ottenere l'accesso alle colonne specifiche del driver eseguendo il conto alla rovescia dalla fine del set di risultati anziché specificare una posizione ordinale esplicita. Per ulteriori informazioni, vedere [Dati restituiti da Funzioni di catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome colonna|Numero di colonna|Tipo di dati|Commenti|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|Nome del catalogo delle procedure; NULL se non applicabile all'origine dati. Se un driver supporta i cataloghi per alcune procedure ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, restituisce una stringa vuota ("") per le procedure che non dispongono di cataloghi.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|Nome dello schema della procedura; NULL se non applicabile all'origine dati. Se un driver supporta gli schemi per alcune procedure ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, restituisce una stringa vuota ("") per le procedure che non dispongono di schemi.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar non NULL|Nome della procedura. Viene restituita una stringa vuota per una routine che non dispone di un nome.|  
|COLUMN_NAME (ODBC 2.0)|4|Varchar non NULL|Nome della colonna della procedura. Il driver restituisce una stringa vuota per una colonna di routine che non dispone di un nome.|  
|COLUMN_TYPE (ODBC 2.0)|5|Smallint non NULL|Definisce la colonna della procedura come parametro o colonna del set di risultati:<br /><br /> SQL_PARAM_TYPE_UNKNOWN: la colonna della routine è un parametro il cui tipo è sconosciuto. (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT: la colonna della routine è un parametro di input. (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: la colonna della routine è un parametro di input/output. (ODBC 1.0)<br /><br /> SQL_PARAM_OUTPUT: la colonna della routine è un parametro di output. (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE: la colonna della procedura è il valore restituito della procedura. (ODBC 2.0)<br /><br /> SQL_RESULT_COL: la colonna della procedura è una colonna del set di risultati. (ODBC 1.0)|  
|DATA_TYPE (ODBC 2.0)|6|Smallint non NULL|Tipo di dati SQL. Può trattarsi di un tipo di dati SQL ODBC o di un tipo di dati SQL specifico del driver. Per i tipi di dati datetime e interval, questa colonna restituisce i tipi di dati concisi (ad esempio, SQL_TYPE_TIME o SQL_INTERVAL_YEAR_TO_MONTH). Per un elenco dei tipi di dati SQL ODBC validi, vedere [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) nell'Appendice D: tipi di dati. Per informazioni sui tipi di dati SQL specifici del driver, vedere la documentazione del driver.|  
|TYPE_NAME (ODBC 2.0)|7|Varchar non NULL|Nome del tipo di dati dipendente dall'origine dati; ad esempio, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" o "CHAR ( ) PER BIT DATA".|  
|COLUMN_SIZE (ODBC 2.0)|8|Integer|Dimensioni della colonna della procedura nell'origine dati. Viene restituito NULL per i tipi di dati in cui la dimensione della colonna non è applicabile. Per ulteriori informazioni sulla precisione, vedere [dimensione della colonna, cifre decimali, lunghezza dell'ottetto](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) di trasferimento e dimensioni di visualizzazione nell'appendice D: tipi di dati.|  
|BUFFER_LENGTH (ODBC 2.0)|9|Integer|Lunghezza in byte di dati trasferiti in un'operazione **SQLGetData** o **SQLFetch** se SQL_C_DEFAULT è specificato. Per i dati numerici, questa dimensione può essere diversa da quella dei dati archiviati nell'origine dati. Per ulteriori informazioni, vedere [Dimensione colonna, Cifre decimali, Lunghezza ottetto di trasferimento e Dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)nell'Appendice D: Tipi di dati.|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|Cifre decimali della colonna della procedura nell'origine dati. Viene restituito NULL per i tipi di dati in cui le cifre decimali non sono applicabili. Per ulteriori informazioni sulle cifre decimali, vedere [Dimensione colonna, Cifre decimali, Lunghezza ottetto](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)di trasferimento e Dimensione di visualizzazione nell'Appendice D: Tipi di dati.|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|Per i tipi di dati numerici, 10 o 2.For numeric data types, either 10 or 2.<br /><br /> Se 10, i valori in COLUMN_SIZE e DECIMAL_DIGITS forniscono il numero di cifre decimali consentito per la colonna. Ad esempio, una colonna DECIMALE(12,5) restituisce un NUM_PREC_RADIX di 10, un COLUMN_SIZE pari a 12 e un DECIMAL_DIGITS di 5; una colonna FLOAT potrebbe restituire un NUM_PREC_RADIX di 10, un COLUMN_SIZE di 15 e un DECIMAL_DIGITS di NULL.<br /><br /> Se 2, i valori in COLUMN_SIZE e DECIMAL_DIGITS forniscono il numero di bit consentiti nella colonna. Ad esempio, una colonna FLOAT potrebbe restituire un NUM_PREC_RADIX di 2, un COLUMN_SIZE di 53 e un DECIMAL_DIGITS di NULL.<br /><br /> Viene restituito NULL per i tipi di dati in cui NUM_PREC_RADIX non è applicabile.|  
|NULLABLE (ODBC 2.0)|12|Smallint non NULL|Se la colonna della procedura accetta un valore NULL:<br /><br /> SQL_NO_NULLS: la colonna della procedura non accetta valori NULL.<br /><br /> SQL_NULLABLE: la colonna della procedura accetta valori NULL.<br /><br /> SQL_NULLABLE_UNKNOWN: non è noto se la colonna della procedura accetta valori NULL.|  
|OSSERVAZIONI (ODBC 2.0)|13|Varchar|Descrizione della colonna della procedura.|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|Valore predefinito della colonna.<br /><br /> Se NULL è stato specificato come valore predefinito, questa colonna è la parola NULL, non racchiusa tra virgolette. Se il valore predefinito non può essere rappresentato senza troncamento, questa colonna contiene TRUNCATED, senza virgolette singole di inclusione. Se non è stato specificato alcun valore predefinito, questa colonna è NULL.<br /><br /> Il valore di COLUMN_DEF può essere utilizzato per generare una nuova definizione di colonna, tranne quando contiene il valore TRUNCATED.|  
|SQL_DATA_TYPE (ODBC 3.0)|15|Smallint non NULL|Valore del tipo di dati SQL visualizzato nel campo SQL_DESC_TYPE del descrittore. Questa colonna è uguale alla colonna DATA_TYPE, ad eccezione dei tipi di dati datetime e interval.<br /><br /> Per i tipi di dati datetime e interval, il campo SQL_DATA_TYPE nel set di risultati restituirà SQL_INTERVAL o SQL_DATETIME e il campo SQL_DATETIME_SUB restituirà il sottocodice per il tipo di dati interval o datetime specifico. (Vedere [l'Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|Codice del sottotipo per i tipi di dati datetime e interval. Per gli altri tipi di dati in questa colonna viene restituito NULL.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|Integer|Lunghezza massima in byte di una colonna di tipo di dati binari o caratteri. Per gli tutti gli altri tipi di dati, il valore di questa colonna è NULL.|  
|ORDINAL_POSITION (ODBC 3.0)|18|Integer non NULL|Per i parametri di input e output, la posizione ordinale del parametro nella definizione della routine (in ordine crescente di parametro, a partire da 1). Per un valore restituito (se presente), viene restituito 0. Per le colonne del set di risultati, la posizione ordinale della colonna nel set di risultati, con la prima colonna nel set di risultati numero 1. Se sono presenti più set di risultati, le posizioni ordinali delle colonne vengono restituite in modo specifico del driver.|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|"NO" se la colonna non include valori NLL.<br /><br /> "YES" se la colonna può includere valori NUL.<br /><br /> Quando non è noto se i valori Null sono supportati, in questa colonna viene restituita una stringa di lunghezza zero.<br /><br /> Per determinare il supporto di valori Null vengono seguite le regole ISO. In un sistema DBMS conforme a ISO SQL non vengono restituite stringhe vuote.<br /><br /> Il valore restituito per questa colonna è diverso dal valore restituito per la colonna NULLABLE. (Vedere la descrizione della colonna NULLABLE.)|  
  
## <a name="code-example"></a>Esempio di codice  
 Vedere [Chiamate di routine](../../../odbc/reference/develop-app/procedure-calls.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Recupero di una singola riga o di un blocco di dati in una direzione forward-only|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Recupero di un blocco di dati o scorrimento di un set di risultati|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Restituzione di un elenco di procedure in un'origine datiReturning a list of procedures in a data source|[Funzione SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
