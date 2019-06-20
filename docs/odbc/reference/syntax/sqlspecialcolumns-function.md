---
title: Funzione SQLSpecialColumns | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSpecialColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSpecialColumns
helpviewer_keywords:
- SQLSpecialColumns function [ODBC]
ms.assetid: bb2d9f21-bda0-4e50-a8be-f710db660034
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c49e7fd827cfd48df07e5e5a01367977504f4511
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536253"
---
# <a name="sqlspecialcolumns-function"></a>Funzione SQLSpecialColumns
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: Apri gruppo  
  
 **Riepilogo**  
 **SQLSpecialColumns** recupera le informazioni seguenti relative alle colonne all'interno di una tabella specificata:  
  
-   Il set ottimale di colonne che identifica in modo univoco una riga nella tabella.  
  
-   Colonne che vengono aggiornate automaticamente quando qualsiasi valore nella riga viene aggiornato da una transazione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLSpecialColumns(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   IdentifierType,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLSMALLINT   Scope,  
     SQLSMALLINT   Nullable);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *IdentifierType*  
 [Input] Tipo di colonna da restituire. Deve essere uno dei valori seguenti:  
  
 SQL_BEST_ROWID: Restituisce la colonna o ottimale set di colonne, tramite il recupero dei valori di colonna o colonne, consente a qualsiasi riga della tabella specificata che deve essere identificato in modo univoco. Una colonna può essere una pseudo-colonna appositamente per questo scopo (ad esempio Oracle ROWID o Ingres TID) o le colonne di un indice univoco per la tabella.  
  
 SQL_ROWVER: Restituisce le colonne della tabella specificata, se presente, che vengono aggiornate automaticamente dall'origine dati quando qualsiasi valore nella riga viene aggiornato tramite una transazione (ad esempio SQLBase ROWID o Sybase TIMESTAMP).  
  
 *CatalogName*  
 [Input] Nome del catalogo per la tabella. Se un driver supporta i cataloghi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da diversi DBMS, una stringa vuota ("") indica le tabelle che non dispone di cataloghi. *CatalogName* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *CatalogName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *CatalogName* è un normale argomento; viene considerato letteralmente e relativi case è significativa. Per altre informazioni, vedere [argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Input] Lunghezza in caratteri della **CatalogName*.  
  
 *SchemaName*  
 [Input] Nome dello schema per la tabella. Se un driver supporta gli schemi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da diversi DBMS, una stringa vuota ("") indica le tabelle che non hanno schemi. *NomeSchema* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *SchemaName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *SchemaName* è un normale argomento; viene considerato letteralmente e relativi case è significativa.  
  
 *NameLength2*  
 [Input] Lunghezza in caratteri della **SchemaName*.  
  
 *TableName*  
 [Input] Nome della tabella. Questo argomento non può essere un puntatore null. *TableName* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *TableName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *TableName* è un normale argomento; viene considerato letteralmente e relativi case è significativa.  
  
 *NameLength3*  
 [Input] Lunghezza in caratteri della **TableName*.  
  
 *Ambito*  
 [Input] Ambito minimo richiesto per ROWID. Il valore rowid restituito può essere un ambito. I possibili valori sono i seguenti:  
  
 SQL_SCOPE_CURROW: Il valore rowid è sicuramente valido solo mentre si è posizionati in tale riga. Una versione successiva selezionare nuovamente mediante rowid potrebbe non restituire una riga se la riga è stata aggiornata o eliminata da un'altra transazione.  
  
 SQL_SCOPE_TRANSACTION: Il valore rowid è garantito a essere validi per la durata della transazione corrente.  
  
 SQL_SCOPE_SESSION: Il valore rowid è garantito a essere validi per la durata della sessione (oltre i limiti delle transazioni).  
  
 *Ammette i valori Null*  
 [Input] Determina se restituire le colonne speciali che possono avere un valore NULL. I possibili valori sono i seguenti:  
  
 SQL_NO_NULLS: Escludere le colonne speciali che possono avere valori NULL. Alcuni driver non è in grado di supportare SQL_NO_NULLS e questi driver restituirà un risultato vuoto se è stato specificato SQL_NO_NULLS impostare. Le applicazioni devono prevedere in questo caso e richiesta SQL_NO_NULLS solo se assolutamente necessario.  
  
 SQL_NULLABLE: Restituisce le colonne speciali, anche se possono avere valori NULL.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSpecialColumns** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLSpecialColumns** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|24000|Stato del cursore non valido|Il cursore è stato aperto scegliere il *StatementHandle*, e **SQLFetch** oppure **SQLFetchScroll** fosse stata chiamata. Questo errore viene restituito da Gestione Driver, se **SQLFetch** oppure **SQLFetchScroll** non restituisce SQL_NO_DATA e viene restituito dal driver se **SQLFetch** oppure **SQLFetchScroll** è stato restituito SQL_NO_DATA.<br /><br /> Un cursore è stato aperto nel *StatementHandle*, ma **SQLFetch** oppure **SQLFetchScroll** non fosse stata chiamata.|  
|40001|Errore di serializzazione.|Il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle*. Quindi la funzione è stata chiamata nuovamente sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY009|Utilizzo non valido del puntatore null|Il *TableName* argomento era un puntatore null.<br /><br /> L'attributo di istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE, il *CatalogName* argomento era un puntatore null e il SQL_CATALOG_NAME *InfoType* restituisce che i nomi di catalogo sono supportati.<br /><br /> (DM) l'attributo di istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE e il *SchemaName* argomento era un puntatore null.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione era ancora in esecuzione quando **SQLSpecialColumns** è stato chiamato.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore di uno degli argomenti di lunghezza è minore di 0 ma non uguali a SQL_NTS.<br /><br /> Il valore di uno degli argomenti di lunghezza maggiore del valore di lunghezza massima consentita per il nome corrispondente. La lunghezza massima di ogni nome può essere ottenuta chiamando **SQLGetInfo** con il *InfoType* valori: SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, or SQL_MAX_TABLE_NAME_LEN.|  
|HY097|Tipo di colonna non compreso nell'intervallo|(DM) non valido *IdentifierType* valore specificato.|  
|HY098|Tipo di ambito non compreso nell'intervallo|(DM) non valido *ambito* valore specificato.|  
|HY099|Tipo che ammette valori null non compreso nell'intervallo|(DM) non valido *Nullable* valore specificato.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|È stato specificato un catalogo e del driver o origine dati non supporta cataloghi.<br /><br /> È stato specificato uno schema e del driver o origine dati non supporta gli schemi.<br /><br /> La combinazione delle impostazioni correnti degli attributi di istruzione SQL_ATTR_CURSOR_TYPE e SQL_ATTR_CONCURRENCY non era supportata dall'origine dati o driver.<br /><br /> L'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_VARIABLE e l'attributo SQL_ATTR_CURSOR_TYPE di istruzione è stata impostata su un tipo di cursore per i quali il driver non supporta i segnalibri.|  
|HYT00|Timeout|Il periodo di timeout query scaduto prima l'origine dati ha restituito il set di risultati richiesti. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 Quando la *IdentifierType* l'argomento è SQL_BEST_ROWID, **SQLSpecialColumns** restituisce le colonne che identificano in modo univoco ogni riga della tabella. Queste colonne sono sempre utilizzabili una *elenco select* oppure **in cui** clausola. **SQLColumns**, che viene utilizzato per restituire una varietà di informazioni sulle colonne di una tabella, non necessariamente restituiscono le colonne che identificano in modo univoco ogni riga o le colonne che vengono aggiornate automaticamente quando qualsiasi valore nella riga viene aggiornata da un transazione. Ad esempio, **SQLColumns** potrebbe non restituire il valore ROWID pseudo colonna Oracle. È per questo motivo **SQLSpecialColumns** viene utilizzato per restituire tali colonne. Per altre informazioni, vedere [Usa i dati del catalogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Per altre informazioni su uso generale, gli argomenti e i dati restituiti di funzioni di catalogo ODBC, vedere [funzioni di catalogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Se non sono presenti colonne che identificano in modo univoco ogni riga nella tabella **SQLSpecialColumns** restituisce un set di righe e senza righe; una chiamata successiva a **SQLFetch** o **SQLFetchScroll**nell'istruzione non restituisce SQL_NO_DATA.  
  
 Se il *IdentifierType*, *ambito*, o *Nullable* argomenti specificano le caratteristiche non supportate dall'origine dati, **SQLSpecialColumns**  restituisce un set di risultati vuoto.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, il *CatalogName*, *SchemaName*, e *TableName* argomenti sono trattati come identificatori, pertanto sono non può essere impostato su un puntatore null in determinate situazioni. (Per altre informazioni, vedere [argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).)  
  
 **SQLSpecialColumns** restituisce i risultati come un set di risultati standard, ordinato in base all'ambito.  
  
 Le colonne seguenti sono state rinominate per ODBC 3*x*. Le modifiche ai nomi di colonna non influenzano la compatibilità con le versioni precedenti poiché nelle applicazioni associati dal numero di colonna.  
  
|Colonna ODBC 2.0|ODBC 3*x* colonna|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 Per determinare la lunghezza effettiva della colonna COLUMN_NAME, un'applicazione può chiamare **SQLGetInfo** con l'opzione SQL_MAX_COLUMN_NAME_LEN.  
  
 Nella tabella seguente elenca le colonne nel set di risultati. Le colonne aggiuntive oltre la colonna 8 (PSEUDO_COLUMN) possono essere definite dal driver. Un'applicazione deve accedere a colonne specifiche del driver procede a ritroso dalla fine del set di risultati anziché specificare una posizione ordinale esplicita. Per altre informazioni, vedere [i dati restituiti dalle funzioni catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome colonna|Numero colonna|Tipo di dati|Commenti|  
|-----------------|-------------------|---------------|--------------|  
|AMBITO (ODBC 1.0)|1|Smallint|Ambito effettivo del rowid. Contiene uno dei valori seguenti:<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> Viene restituito NULL quando *IdentifierType* è SQL_ROWVER. Per una descrizione di ogni valore, vedere la descrizione della *ambito* "Sintassi", più indietro in questa sezione.|  
|COLUMN_NAME (ODBC 1.0)|2|Non NULL varchar|Nome colonna. Il driver restituisce una stringa vuota per una colonna che non dispone di un nome.|  
|DATA_TYPE (ODBC 1.0)|3|Smallint non NULL|Tipo di dati SQL. Può trattarsi di un tipo di dati SQL ODBC o un tipo di dati specifici del driver SQL. Per un elenco di tipi di dati SQL ODBC validi, vedere [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md). Per informazioni sui tipi di dati specifici del driver SQL, vedere la documentazione del driver.|  
|TYPE_NAME (ODBC 1.0)|4|Non NULL varchar|Nome del tipo di dati dipende dall'origine dati; ad esempio, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" o "() CHAR FOR BIT DATA".|  
|COLUMN_SIZE (ODBC 1.0)|5|Valore intero|Le dimensioni della colonna nell'origine dati. Per altre informazioni riguardanti le dimensioni di colonna, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|BUFFER_LENGTH (ODBC 1.0)|6|Valore intero|La lunghezza in byte dei dati trasferiti in un' **SQLGetData** oppure **SQLFetch** operazione se si specifica SQL_C_DEFAULT. Per i dati numerici, questa dimensione può essere diversa rispetto alla dimensione dei dati archiviati nell'origine dati. Questo valore è lo stesso nome di colonna COLUMN_SIZE per dati carattere o binario. Per altre informazioni, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|Le cifre decimali della colonna nell'origine dati. Viene restituito NULL per i tipi di dati in cui cifre decimali non sono applicabili. Per altre informazioni relative al cifre decimali, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|Indica se la colonna è una pseudo colonna, ad esempio Oracle ROWID:<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **Note:**  Per garantire la massima interoperabilità, Pseudocolonne non devono essere delimitate con l'identificatore del tipo di virgolette restituito da **SQLGetInfo**.|  
  
 Dopo l'applicazione recupera i valori per SQL_BEST_ROWID, l'applicazione è possibile usare questi valori per selezionare nuovamente tale riga all'interno dell'ambito definito. Il **seleziona** istruzione è garantita per restituire alcuna riga o una riga.  
  
 Se un'applicazione seleziona una riga in base al valore rowid colonna o colonne e la riga non viene trovata, l'applicazione può presupporre che la riga è stata eliminata o il valore rowid colonne sono state modificate. Non è vero il contrario: anche se il valore rowid non è stato modificato, le altre colonne nella riga potrebbero sono stati modificati.  
  
 Colonne restituite per il tipo di colonna SQL_BEST_ROWID sono utili per le applicazioni che necessitano di uno scorrimento in avanti e indietro all'interno di un set di risultati per recuperare i dati più recenti da un set di righe. Le colonne ROWID non dovrebbero modificare mentre si è posizionati in tale riga.  
  
 Le colonne ROWID restino valide anche quando il cursore non è posizionato sulla riga; l'applicazione può determinare selezionando la colonna ambito nel set di risultati.  
  
 Colonne restituite per il tipo di colonna SQL_ROWVER sono utili per le applicazioni che richiedono la possibilità di controllare se tutte le colonne in una determinata riga sono state aggiornate mentre la riga è stata venisse riselezionata mediante rowid. Ad esempio, dopo avere si riseleziona una riga mediante rowid, l'applicazione può confrontare i precedenti valori nelle colonne SQL_ROWVER a quelle appena recuperate. Se il valore in una colonna SQL_ROWVER è diverso dal valore precedente, l'applicazione può avvertire l'utente che ha modificato i dati sullo schermo.  
  
## <a name="code-example"></a>Esempio di codice  
 Per un esempio di codice di una funzione simile, vedere [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultati|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di colonne in una o più tabelle|[Funzione SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Il recupero di una singola riga o un blocco di dati in una direzione di tipo forward-only|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Imposta il recupero di un blocco di dati o lo scorrimento di un risultato|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Restituisce le colonne di una chiave primaria|[Funzione SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
