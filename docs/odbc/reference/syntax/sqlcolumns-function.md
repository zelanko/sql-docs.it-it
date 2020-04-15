---
title: Funzione SQLColumns . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumns
helpviewer_keywords:
- SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36293c1f2393e9a57351fc8cd19dcc6e3338f5cc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301257"
---
# <a name="sqlcolumns-function"></a>Funzione SQLColumns
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: Open Group  
  
 **Riepilogo**  
 **SQLColumns** restituisce l'elenco dei nomi di colonna nelle tabelle specificate. Il driver restituisce queste informazioni come set di risultati *sull'oggetto specificato StatementHandle*.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLColumns(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      ColumnName,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *CatalogName*  
 [Ingresso] Nome del catalogo. Se un driver supporta i cataloghi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, una stringa vuota ("") indica le tabelle che non dispongono di cataloghi. *CatalogName* non può contenere un criterio di ricerca di stringa.  
  
> [!NOTE]  
>  Se l'attributo statement SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *CatalogName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *CatalogName* è un argomento ordinario; viene trattato letteralmente, e il suo caso è significativo. Per ulteriori informazioni, vedere [Argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Ingresso] Lunghezza in caratteri di*nomeCatalogo*.  
  
 *Nome Schema*  
 [Ingresso] Criterio di ricerca di stringhe per i nomi degli schemi. Se un driver supporta gli schemi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, una stringa vuota ("") indica le tabelle che non dispongono di schemi.  
  
> [!NOTE]  
>  Se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *SchemaName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *SchemaName* è un argomento di valore di modello; viene trattato letteralmente, e il suo caso è significativo.  
  
 *NameLength2*  
 [Ingresso] Lunghezza in caratteri di :*NomeSchema*.  
  
 *Tablename*  
 [Ingresso] Criterio di ricerca di stringhe per i nomi delle tabelle.  
  
> [!NOTE]  
>  Se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *TableName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *TableName* è un argomento di valore di modello; viene trattato letteralmente, e il suo caso è significativo.  
  
 *NameLength3*  
 [Ingresso] Lunghezza in caratteri di*nomeTabella*.  
  
 *ColumnName*  
 [Ingresso] Criterio di ricerca di stringhe per i nomi delle colonne.  
  
> [!NOTE]  
>  Se l'attributo statement SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *ColumnName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *ColumnName* è un argomento di valore di modello; viene trattato letteralmente, e il suo caso è significativo.  
  
 *NameLunghezza4*  
 [Ingresso] Lunghezza in caratteri di*nomeColonna*.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLColumns** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLColumns** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|24000|Stato del cursore non valido|Un cursore era aperto su *StatementHandle*e **SQLFetch** o **SQLFetchScroll** era stato chiamato. Questo errore viene restituito da Gestione Driver se **SQLFetch** o **SQLFetchScroll** non ha restituito SQL_NO_DATA e viene restituito dal driver se **SQLFetch** o **SQLFetchScroll** ha restituito SQL_NO_DATA.<br /><br /> Un cursore era aperto su *StatementHandle* ma **SQLFetch** o **SQLFetchScroll** non era stato chiamato.|  
|40001|Errore di serializzazione|È stato eseguito il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*. Quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|I009|Utilizzo non valido del puntatore null|L'attributo dell'istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE, l'argomento *CatalogName* è un puntatore null e il SQL_CATALOG_NAME *InfoType* restituisce che i nomi dei cataloghi sono supportati.<br /><br /> (DM) l'attributo dell'istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE e l'argomento *SchemaName*, *TableName*o *ColumnName* è un puntatore null.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLColumns.This** asynchronous function was still executing when the SQLColumns function was called.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore di uno degli argomenti della lunghezza del nome è minore di 0 ma non uguale a SQL_NTS.|  
|||Il valore di uno degli argomenti di lunghezza del nome ha superato il valore di lunghezza massima per il catalogo o il nome corrispondente. La lunghezza massima di ogni catalogo o nome può essere ottenuta chiamando **SQLGetInfo** con il *InfoType* valori. (Vedere "Commenti").")|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|È stato specificato un nome di catalogo e il driver o l'origine dati non supporta i cataloghi.<br /><br /> È stato specificato un nome di schema e il driver o l'origine dati non supporta gli schemi.<br /><br /> È stato specificato un criterio di ricerca di stringa per il nome dello schema, il nome della tabella o il nome della colonna e l'origine dati non supporta i criteri di ricerca per uno o più di tali argomenti.<br /><br /> La combinazione delle impostazioni correnti degli attributi di istruzione SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE non è supportata dal driver o dall'origine dati.<br /><br /> L'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_VARIABLE e l'attributo dell'istruzione SQL_ATTR_CURSOR_TYPE è stato impostato su un tipo di cursore per il quale il driver non supporta i segnalibri.|  
|HYT00|Timeout|Il periodo di timeout della query è scaduto prima che l'origine dati restituisca il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 Questa funzione viene in genere utilizzata prima dell'esecuzione dell'istruzione per recuperare informazioni sulle colonne per una tabella o tabelle dal catalogo dell'origine dati. **SQLColumns** può essere utilizzato per recuperare i dati per tutti i tipi di elementi restituiti da **SQLTables**. Oltre alle tabelle di base, questo può includere (ma non è limitato a) viste, sinonimi, tabelle di sistema e così via. Al contrario, le funzioni **SQLColAttribute** e **SQLDescribeCol** descrivono le colonne in un set di risultati e la funzione **SQLNumResultCols** restituisce il numero di colonne in un set di risultati. Per ulteriori informazioni, consultate [Usi dei dati del catalogo.](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
> [!NOTE]  
>  Per ulteriori informazioni sull'utilizzo generale, gli argomenti e i dati restituiti delle funzioni di catalogo ODBC, vedere Funzioni di [catalogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLColumns** restituisce i risultati come set di risultati standard, ordinati per TABLE_CAT, TABLE_SCHEM, TABLE_NAME e ORDINAL_POSITION.  
  
> [!NOTE]  
>  Quando un'applicazione funziona con un ODBC 2. *x* driver, non viene restituita alcuna colonna di ORDINAL_POSITION nel set di risultati. Di conseguenza, quando si lavora con ODBC 2. *x* driver, l'ordine delle colonne nell'elenco di colonne restituito da **SQLColumns** non è necessariamente lo stesso dell'ordine delle colonne restituite quando l'applicazione esegue un'istruzione SELECT su tutte le colonne della tabella.  
  
> [!NOTE]  
>  **SQLColumns** potrebbe non restituire tutte le colonne. Ad esempio, un driver potrebbe non restituire informazioni sulle pseudo-colonne, ad esempio Oracle ROWID.For example, a driver might not return information about pseudo-columns, such as Oracle ROWID. Le applicazioni possono utilizzare qualsiasi colonna valida, indipendentemente dal fatto che venga restituita da **SQLColumns**.  
>   
>  Alcune colonne che possono essere restituite da **SQLStatistics** non vengono restituite da **SQLColumns**. Ad esempio, **SQLColumns** non restituisce le colonne di un indice creato su un'espressione o un filtro, ad esempio SALARY , BENEFITS o DEPT , 0012.  
  
 Le lunghezze delle colonne VARCHAR non vengono visualizzate nella tabella. le lunghezze effettive dipendono dall'origine dati. Per determinare le lunghezze effettive delle colonne TABLE_CAT, TABLE_SCHEM, TABLE_NAME e COLUMN_NAME, un'applicazione può chiamare **SQLGetInfo** con le opzioni SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
 Le colonne seguenti sono state rinominate per ODBC 3. *x*. Le modifiche del nome della colonna non influiscono sulla compatibilità con le versioni precedenti perché le applicazioni vengono associate in base al numero di colonna.  
  
|Colonna ODBC 2.0|ODBC 3. *x* colonna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 Le colonne seguenti sono state aggiunte al set di risultati restituito da **SQLColumns** per ODBC 3. *x*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 Nella tabella seguente sono elencate le colonne del set di risultati. Colonne aggiuntive oltre la colonna 18 (IS_NULLABLE) possono essere definite dal driver. Un'applicazione deve ottenere l'accesso alle colonne specifiche del driver eseguendo il conto alla rovescia dalla fine del set di risultati anziché specificare una posizione ordinale esplicita. Per ulteriori informazioni, vedere [Dati restituiti da Funzioni di catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome colonna|Colonna<br /><br /> d'acquisto|Tipo di dati|Commenti|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nome del catalogo; NULL se non applicabile all'origine dati. Se un driver supporta i cataloghi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, restituisce una stringa vuota ("") per le tabelle che non dispongono di cataloghi.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome dello schema; NULL se non applicabile all'origine dati. Se un driver supporta gli schemi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, restituisce una stringa vuota ("") per le tabelle che non dispongono di schemi.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar non NULL|Nome della tabella.|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar non NULL|Nome colonna. Il driver restituisce una stringa vuota per una colonna che non dispone di un nome.|  
|DATA_TYPE (ODBC 1.0)|5|Smallint non NULL|Tipo di dati SQL. Può trattarsi di un tipo di dati SQL ODBC o di un tipo di dati SQL specifico del driver. Per i tipi di dati datetime e interval, questa colonna restituisce il tipo di dati conciso (ad esempio SQL_TYPE_DATE o SQL_INTERVAL_YEAR_TO_MONTH, anziché il tipo di dati non conciso, ad esempio SQL_DATETIME o SQL_INTERVAL). Per un elenco dei tipi di dati SQL ODBC validi, vedere [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) nell'Appendice D: tipi di dati. Per informazioni sui tipi di dati SQL specifici del driver, vedere la documentazione del driver.<br /><br /> Tipi di dati restituiti per ODBC 3. *x* e ODBC 2. *x* applicazioni possono essere diverse. Per ulteriori informazioni, vedere [Compatibilità con le versioni precedenti e conformità agli standard](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).|  
|TYPE_NAME (ODBC 1.0)|6|Varchar non NULL|Nome del tipo di dati dipendente dall'origine dati; ad esempio, "CHAR", "VARCHAR", "MONEY", "LONG VARBINAR" o "CHAR ( ) PER BIT DATA".|  
|COLUMN_SIZE (ODBC 1.0)|7|Integer|Se DATA_TYPE è SQL_CHAR o SQL_VARCHAR, questa colonna contiene la lunghezza massima in caratteri della colonna. Per i tipi di dati datetime, questo è il numero totale di caratteri necessari per visualizzare il valore quando viene convertito in caratteri. Per i tipi di dati numerici, si tratta del numero totale di cifre o del numero totale di bit consentiti nella colonna, in base alla colonna NUM_PREC_RADIX. Per i tipi di dati intervallo, questo è il numero di caratteri nella rappresentazione di caratteri del valore letterale di intervallo (come definito dalla precisione iniziale dell'intervallo, vedere [Interval Data Type Length](../../../odbc/reference/appendixes/interval-data-type-length.md) in Appendix D: Tipi di dati). Per ulteriori informazioni, vedere [Dimensione colonna, Cifre decimali, Lunghezza ottetto di trasferimento e Dimensioni](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) di visualizzazione nell'Appendice D: Tipi di dati.|  
|BUFFER_LENGTH (ODBC 1.0)|8|Integer|Lunghezza in byte di dati trasferiti in un'operazione SQLGetData, SQLFetch o SQLFetchScroll se SQL_C_DEFAULT è specificata. Per i dati numerici, questa dimensione può differire dalle dimensioni dei dati archiviati nell'origine dati. Questo valore potrebbe essere diverso da COLUMN_SIZE colonna per i dati di tipo carattere. Per ulteriori informazioni sulla lunghezza, vedere [dimensione della colonna, cifre decimali, lunghezza dell'ottetto](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) di trasferimento e dimensioni di visualizzazione nell'appendice D: tipi di dati.|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|Numero totale di cifre significative a destra del separatore decimale. Per SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP, questa colonna contiene il numero di cifre nel componente dei secondi frazionari. Per gli altri tipi di dati, si tratta delle cifre decimali della colonna nell'origine dati. Per i tipi di dati intervallo che contengono un componente ora, questa colonna contiene il numero di cifre a destra del separatore decimale (secondi frazionari). Per i tipi di dati intervallo che non contengono un componente ora, questa colonna è 0.For interval data types that do not contain a time component, this column is 0. Per ulteriori informazioni sulle cifre decimali, vedere [Dimensione colonna, Cifre decimali, Trasferimento ottetto lunghezza e Dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice D: tipi di dati. Viene restituito NULL per i tipi di dati in cui DECIMAL_DIGITS non è applicabile.|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|Per i tipi di dati numerici, 10 o 2.For numeric data types, either 10 or 2. Se è 10, i valori in COLUMN_SIZE e DECIMAL_DIGITS forniscono il numero di cifre decimali consentito per la colonna. Ad esempio, una colonna DECIMALE(12,5) restituisce un NUM_PREC_RADIX di 10, un COLUMN_SIZE pari a 12 e un DECIMAL_DIGITS di 5; una colonna FLOAT potrebbe restituire un NUM_PREC_RADIX di 10, un COLUMN_SIZE di 15 e un DECIMAL_DIGITS di NULL.<br /><br /> Se è 2, i valori in COLUMN_SIZE e DECIMAL_DIGITS forniscono il numero di bit consentiti nella colonna. Ad esempio, una colonna FLOAT potrebbe restituire un RADIX pari a 2, un COLUMN_SIZE di 53 e un DECIMAL_DIGITS NULL.<br /><br /> Viene restituito NULL per i tipi di dati in cui NUM_PREC_RADIX non è applicabile.|  
|NULLABLE (ODBC 1.0)|11|Smallint non NULL|SQL_NO_NULLS se la colonna non è in grado di includere valori NULL.<br /><br /> SQL_NULLABLE se la colonna accetta valori NULL.<br /><br /> SQL_NULLABLE_UNKNOWN se non è noto se la colonna accetta valori NULL.<br /><br /> Il valore restituito per questa colonna è diverso dal valore restituito per la colonna IS_NULLABLE. La colonna NULLABLE indica con certezza che una colonna può accettare valori NULL, ma non può indicare con certezza che una colonna non accetta valori NULL. La colonna IS_NULLABLE indica con certezza che una colonna non può accettare valori NLL, ma non può indicare con certezza che una colonna accetta valori nu(NET).|  
|OSSERVAZIONI (ODBC 1.0)|12|Varchar|Descrizione della colonna.|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|Valore predefinito della colonna. Il valore in questa colonna deve essere interpretato come stringa se è racchiuso tra virgolette.<br /><br /> Se NULL è stato specificato come valore predefinito, questa colonna è la parola NULL, non racchiusa tra virgolette. Se il valore predefinito non può essere rappresentato senza troncamento, questa colonna contiene TRUNCATED, senza racchiudere virgolette singole. Se non è stato specificato alcun valore predefinito, questa colonna è NULL.<br /><br /> Il valore di COLUMN_DEF può essere utilizzato per generare una nuova definizione di colonna, tranne quando contiene il valore TRUNCATED.|  
|SQL_DATA_TYPE (ODBC 3.0)|14|Smallint non NULL|Tipo di dati SQL, come viene visualizzato nel campo SQL_DESC_TYPE record nell'IRD. Può trattarsi di un tipo di dati SQL ODBC o di un tipo di dati SQL specifico del driver. Questa colonna è uguale alla colonna DATA_TYPE, ad eccezione dei tipi di dati datetime e interval. Questa colonna restituisce il tipo di dati non conciso (ad esempio SQL_DATETIME o SQL_INTERVAL), anziché il tipo di dati conciso (ad esempio SQL_TYPE_DATE o SQL_INTERVAL_YEAR_TO_MONTH) per i tipi di dati datetime e interval. Se questa colonna restituisce SQL_DATETIME o SQL_INTERVAL, il tipo di dati specifico può essere determinato dalla colonna SQL_DATETIME_SUB. Per un elenco dei tipi di dati SQL ODBC validi, vedere [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) nell'Appendice D: tipi di dati. Per informazioni sui tipi di dati SQL specifici del driver, vedere la documentazione del driver.<br /><br /> Tipi di dati restituiti per ODBC 3. *x* e ODBC 2. *x* applicazioni possono essere diverse. Per ulteriori informazioni, vedere [Compatibilità con le versioni precedenti e conformità agli standard](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|Codice del sottotipo per i tipi di dati datetime e interval. Per gli altri tipi di dati in questa colonna viene restituito NULL. Per ulteriori informazioni sui sottocodici datetime e interval, vedere "SQL_DESC_DATETIME_INTERVAL_CODE" in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|Integer|Lunghezza massima in byte di una colonna di tipo di dati binari o caratteri. Per gli tutti gli altri tipi di dati, il valore di questa colonna è NULL.|  
|ORDINAL_POSITION (ODBC 3.0)|17|Integer non NULL|Posizione ordinale della colonna nella tabella. La prima colonna della tabella è il numero 1.|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|"NO" se la colonna non include valori NLL.<br /><br /> "YES" se la colonna può includere valori NUL.<br /><br /> Quando non è noto se i valori Null sono supportati, in questa colonna viene restituita una stringa di lunghezza zero.<br /><br /> Per determinare il supporto di valori Null vengono seguite le regole ISO. In un sistema DBMS conforme a ISO SQL non vengono restituite stringhe vuote.<br /><br /> Il valore restituito per questa colonna è diverso dal valore restituito per la colonna NULLABLE. (Vedere la descrizione della colonna NULLABLE.)|  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, un'applicazione dichiara i buffer per il set di risultati restituito da **SQLColumns**. Chiama **SQLColumns** per restituire un set di risultati che descrive ogni colonna nella tabella EMPLOYEE. Chiama quindi **SQLBindCol** per associare le colonne nel set di risultati ai buffer. Infine, l'applicazione recupera ogni riga di dati con **SQLFetch** e la elabora.  
  
```cpp  
// SQLColumns_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
// Declare buffers for result set data  
SQLCHAR szSchema[STR_LEN];  
SQLCHAR szCatalog[STR_LEN];  
SQLCHAR szColumnName[STR_LEN];  
SQLCHAR szTableName[STR_LEN];  
SQLCHAR szTypeName[STR_LEN];  
SQLCHAR szRemarks[REM_LEN];  
SQLCHAR szColumnDefault[STR_LEN];  
SQLCHAR szIsNullable[STR_LEN];  
  
SQLINTEGER ColumnSize;  
SQLINTEGER BufferLength;  
SQLINTEGER CharOctetLength;  
SQLINTEGER OrdinalPosition;  
  
SQLSMALLINT DataType;  
SQLSMALLINT DecimalDigits;  
SQLSMALLINT NumPrecRadix;  
SQLSMALLINT Nullable;  
SQLSMALLINT SQLDataType;  
SQLSMALLINT DatetimeSubtypeCode;  
  
SQLHSTMT hstmt = NULL;  
  
// Declare buffers for bytes available to return  
SQLINTEGER cbCatalog;  
SQLINTEGER cbSchema;  
SQLINTEGER cbTableName;  
SQLINTEGER cbColumnName;  
SQLINTEGER cbDataType;  
SQLINTEGER cbTypeName;  
SQLINTEGER cbColumnSize;  
SQLLEN cbBufferLength;  
SQLINTEGER cbDecimalDigits;  
SQLINTEGER cbNumPrecRadix;  
SQLINTEGER cbNullable;  
SQLINTEGER cbRemarks;  
SQLINTEGER cbColumnDefault;  
SQLINTEGER cbSQLDataType;  
SQLINTEGER cbDatetimeSubtypeCode;  
SQLINTEGER cbCharOctetLength;  
SQLINTEGER cbOrdinalPosition;  
SQLINTEGER cbIsNullable;  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retcode = SQLColumns(hstmt, NULL, 0, NULL, 0, (SQLCHAR*)"CUSTOMERS", SQL_NTS, NULL, 0);  
  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      // Bind columns in result set to buffers  
      SQLBindCol(hstmt, 1, SQL_C_CHAR, szCatalog, STR_LEN,&cbCatalog);  
      SQLBindCol(hstmt, 2, SQL_C_CHAR, szSchema, STR_LEN, &cbSchema);  
      SQLBindCol(hstmt, 3, SQL_C_CHAR, szTableName, STR_LEN,&cbTableName);  
      SQLBindCol(hstmt, 4, SQL_C_CHAR, szColumnName, STR_LEN, &cbColumnName);  
      SQLBindCol(hstmt, 5, SQL_C_SSHORT, &DataType, 0, &cbDataType);  
      SQLBindCol(hstmt, 6, SQL_C_CHAR, szTypeName, STR_LEN, &cbTypeName);  
      SQLBindCol(hstmt, 7, SQL_C_SLONG, &ColumnSize, 0, &cbColumnSize);  
      SQLBindCol(hstmt, 8, SQL_C_SLONG, &BufferLength, 0, &cbBufferLength);  
      SQLBindCol(hstmt, 9, SQL_C_SSHORT, &DecimalDigits, 0, &cbDecimalDigits);  
      SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix, 0, &cbNumPrecRadix);  
      SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable, 0, &cbNullable);  
      SQLBindCol(hstmt, 12, SQL_C_CHAR, szRemarks, REM_LEN, &cbRemarks);  
      SQLBindCol(hstmt, 13, SQL_C_CHAR, szColumnDefault, STR_LEN, &cbColumnDefault);  
      SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType, 0, &cbSQLDataType);  
      SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode, 0, &cbDatetimeSubtypeCode);  
      SQLBindCol(hstmt, 16, SQL_C_SLONG, &CharOctetLength, 0, &cbCharOctetLength);  
      SQLBindCol(hstmt, 17, SQL_C_SLONG, &OrdinalPosition, 0, &cbOrdinalPosition);  
      SQLBindCol(hstmt, 18, SQL_C_CHAR, szIsNullable, STR_LEN, &cbIsNullable);  
  
      while (SQL_SUCCESS == retcode) {  
         retcode = SQLFetch(hstmt);  
         /*  
         if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // show_error();  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // Process fetched data  
         else  
            break;  
        */  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione dei privilegi per una o più colonne|[Funzione SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Recupero di un blocco di dati o scorrimento di un set di risultati|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Recupero di più righe di dati|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Restituzione di colonne che identificano in modo univoco una riga o colonne aggiornate automaticamente da una transazioneReturning columns that uniquely identify a row, or columns automatically updated by a transaction|[Funzione SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|Restituzione di statistiche e indici delle tabelleReturning table statistics and indexes|[Funzione SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Restituzione di un elenco di tabelle in un'origine datiReturning a list of tables in a data source|[Funzione SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
|Restituzione dei privilegi per una tabella o tabelleReturning privileges for a table or tables|[Funzione SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
