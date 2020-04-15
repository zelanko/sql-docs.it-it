---
title: 'Funzione SQLStatistics : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2a5ef0b0e54e17a2dc091a98efc972fa608ef15
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302945"
---
# <a name="sqlstatistics-function"></a>Funzione SQLStatistics
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLStatistics** recupera un elenco di statistiche su una singola tabella e gli indici associati alla tabella. Il driver restituisce le informazioni come set di risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *CatalogName*  
 [Ingresso] Nome del catalogo. Se un driver supporta i cataloghi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, una stringa vuota ("") indica le tabelle che non dispongono di cataloghi. *CatalogName* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo statement SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *CatalogName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *CatalogName* è un argomento ordinario; viene trattato letteralmente, e il suo caso è significativo. Per ulteriori informazioni, vedere [Argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Ingresso] Lunghezza in caratteri di*nomeCatalogo*.  
  
 *Nome Schema*  
 [Ingresso] Nome dello schema. Se un driver supporta gli schemi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, una stringa vuota ("") indica le tabelle che non dispongono di schemi. *SchemaName* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *SchemaName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *SchemaName* è un argomento ordinario; viene trattato letteralmente, e il suo caso è significativo.  
  
 *NameLength2*  
 [Ingresso] Lunghezza in caratteri di :*NomeSchema*.  
  
 *Tablename*  
 [Ingresso] Nome della tabella. Questo argomento non può essere un puntatore null. *SchemaName* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *TableName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *TableName* è un argomento ordinario; viene trattato letteralmente, e il suo caso è significativo.  
  
 *NameLength3*  
 [Ingresso] Lunghezza in caratteri di*nomeTabella*.  
  
 *Unico*  
 [Ingresso] Tipo di indice: SQL_INDEX_UNIQUE o SQL_INDEX_ALL.  
  
 *Riservato*  
 [Ingresso] Indica l'importanza delle colonne CARDINALITY e PAGES nel set di risultati. Le opzioni seguenti influiscono solo sulla restituzione delle colonne CARDINALITY e PAGES; le informazioni sull'indice vengono restituite anche se CARDINALITY e PAGES non vengono restituite.  
  
 SQL_ENSURE richiede che il driver recuperi incondizionatamente le statistiche. I driver conformi solo allo standard Open Group e che non supportano le estensioni ODBC non saranno in grado di supportare SQL_ENSURE.  
  
 SQL_QUICK richiede che il driver recuperi CARDINALITY e PAGES solo se sono prontamente disponibili dal server. In tal caso, il driver non garantisce che i valori siano aggiornati. Le applicazioni scritte nello standard Open Group otterranno sempre SQL_QUICK comportamento dai driver conformi a ODBC *3.x.*  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLStatistics** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLStatistics** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|24000|Stato del cursore non valido|Un cursore era aperto su *StatementHandle*e **SQLFetch** o **SQLFetchScroll** era stato chiamato. Questo errore viene restituito da Gestione Driver se **SQLFetch** o **SQLFetchScroll** non ha restituito SQL_NO_DATA e viene restituito dal driver se **SQLFetch** o **SQLFetchScroll** ha restituito SQL_NO_DATA.<br /><br /> Un cursore era aperto su *StatementHandle*, ma **SQLFetch** o **SQLFetchScroll** non era stato chiamato.|  
|40001|Errore di serializzazione|È stato eseguito il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*, quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|I009|Utilizzo non valido del puntatore null|L'argomento *TableName* è un puntatore null.<br /><br /> L'attributo dell'istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE, l'argomento *CatalogName* è un puntatore null e il SQL_CATALOG_NAME *InfoType* restituisce che i nomi dei cataloghi sono supportati.<br /><br /> (DM) l'attributo dell'istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE e l'argomento *SchemaName* è un puntatore null.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLStatistics.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore di uno degli argomenti della lunghezza del nome è minore di 0 ma non uguale a SQL_NTS.<br /><br /> Il valore di uno degli argomenti di lunghezza del nome ha superato il valore di lunghezza massima per il nome corrispondente.|  
|I100|Tipo di opzione di unicità non compresa nell'intervallo|(DM) È stato specificato un valore *Unique* non valido.|  
|HY101|Tipo di opzione Di accuratezza fuori intervallo|(DM) È stato specificato un valore *riservato* non valido.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|È stato specificato un catalogo e il driver o l'origine dati non supporta i cataloghi.<br /><br /> È stato specificato uno schema e il driver o l'origine dati non supporta gli schemi.<br /><br /> La combinazione delle impostazioni correnti degli attributi di istruzione SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE non è supportata dal driver o dall'origine dati.<br /><br /> L'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_VARIABLE e l'attributo dell'istruzione SQL_ATTR_CURSOR_TYPE è stato impostato su un tipo di cursore per il quale il driver non supporta i segnalibri.|  
|HYT00|Timeout|Il periodo di timeout della query è scaduto prima che l'origine dati restituisca il set di risultati richiesto. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **SQLStatistics** restituisce informazioni su una singola tabella come set di risultati standard, ordinate per NON_UNIQUE, TYPE, INDEX_QUALIFIER, INDEX_NAME e ORDINAL_POSITION. Il set di risultati combina le informazioni statistiche (nelle colonne CARDINALITY e PAGES del set di risultati) per la tabella con le informazioni su ogni indice. Per informazioni sull'utilizzo di queste informazioni, vedere [Utilizzi dei dati del catalogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Per determinare le lunghezze effettive delle colonne TABLE_CAT, TABLE_SCHEM, TABLE_NAME e COLUMN_NAME, un'applicazione può chiamare **SQLGetInfo** con le opzioni SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
> [!NOTE]  
>  Per ulteriori informazioni sull'utilizzo generale, gli argomenti e i dati restituiti delle funzioni di catalogo ODBC, vedere Funzioni di [catalogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Le colonne seguenti sono state rinominate per ODBC *3.x*. Le modifiche del nome della colonna non influiscono sulla compatibilità con le versioni precedenti perché le applicazioni vengono associate in base al numero di colonna.  
  
|Colonna ODBC 2.0|Colonna ODBC *3.x*|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 Nella tabella seguente sono elencate le colonne del set di risultati. Colonne aggiuntive oltre la colonna 13 (FILTER_CONDITION) possono essere definite dal driver. Un'applicazione deve ottenere l'accesso alle colonne specifiche del driver eseguendo il conto alla rovescia dalla fine del set di risultati anziché specificare una posizione ordinale esplicita. Per ulteriori informazioni, vedere [Dati restituiti da Funzioni di catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome colonna|Numero di colonna|Tipo di dati|Commenti|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nome del catalogo della tabella a cui si applica la statistica o l'indice; NULL se non applicabile all'origine dati. Se un driver supporta i cataloghi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, restituisce una stringa vuota ("") per le tabelle che non dispongono di cataloghi.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome dello schema della tabella a cui si applica la statistica o l'indice; NULL se non applicabile all'origine dati. Se un driver supporta gli schemi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, restituisce una stringa vuota ("") per le tabelle che non dispongono di schemi.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar non NULL|Nome della tabella a cui si applica la statistica o l'indice.|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|Indica se l'indice non consente valori duplicati:<br /><br /> SQL_TRUE se i valori di indice possono essere non univoci.<br /><br /> SQL_FALSE se i valori di indice devono essere univoci.<br /><br /> Se TYPE è SQL_TABLE_STAT, viene restituito NULL.|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|Identificatore utilizzato per qualificare il nome dell'indice eseguendo un **INDEX DROP**; Se un qualificatore di indice non è supportato dall'origine dati o se TYPE è SQL_TABLE_STAT, viene restituito NULL. Se in questa colonna viene restituito un valore diverso da null, è necessario utilizzarlo per qualificare il nome dell'indice in un'istruzione **DROP INDEX.** in caso contrario, il TABLE_SCHEM deve essere utilizzato per qualificare il nome dell'indice.|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|Nome dell'indice; Se TYPE è SQL_TABLE_STAT, viene restituito NULL.|  
|TIPO (ODBC 1.0)|7|Smallint non NULL|Tipo di informazioni restituite:<br /><br /> SQL_TABLE_STAT indica una statistica per la tabella (nella colonna CARDINALITY o PAGES).<br /><br /> SQL_INDEX_BTREE indica un indice B-Tree.<br /><br /> SQL_INDEX_CLUSTERED indica un indice cluster.<br /><br /> SQL_INDEX_CONTENT indica un indice di contenuto.<br /><br /> SQL_INDEX_HASHED indica un indice con hash.<br /><br /> SQL_INDEX_OTHER indica un altro tipo di indice.|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|Numero di sequenza di colonne nell'indice (a partire da 1); Se TYPE è SQL_TABLE_STAT, viene restituito NULL.|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|Nome colonna. Se la colonna è basata su un'espressione, ad esempio SALARY e BENEFITS, viene restituita l'espressione; Se non è possibile determinare l'espressione, viene restituita una stringa vuota. Se TYPE è SQL_TABLE_STAT, viene restituito NULL.|  
|ASC_OR_DESC (ODBC 1.0)|10|Char(1)|Sequenza di ordinamento per la colonna: "A" per l'ascendente; "D" per la discesa; Null viene restituito se la sequenza di ordinamento delle colonne non è supportata dall'origine dati o se TYPE è SQL_TABLE_STAT.|  
|CARDINALITÀ (ODBC 1.0)|11|Integer|Cardinalità della tabella o dell'indice; numero di righe nella tabella se TYPE è SQL_TABLE_STAT; numero di valori univoci nell'indice se TYPE non è SQL_TABLE_STAT; Se il valore non è disponibile dall'origine dati, viene restituito NULL.|  
|PAGES (ODBC 1.0)|12|Integer|Numero di pagine utilizzate per archiviare l'indice o la tabella; numero di pagine per la tabella se TYPE è SQL_TABLE_STAT; numero di pagine per l'indice se TYPE non è SQL_TABLE_STAT; Viene restituito NULL se il valore non è disponibile dall'origine dati o se non è applicabile all'origine dati.|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|Se l'indice è un indice filtrato, questa è la condizione di filtro, ad esempio SALARY > 30000; se non è possibile determinare la condizione di filtro, si tratta di una stringa vuota.<br /><br /> NULL se l'indice non è un indice filtrato, non è possibile determinare se l'indice è un indice filtrato o TYPE è SQL_TABLE_STAT.|  
  
 Se la riga nel set di risultati corrisponde a una tabella, il driver imposta TYPE su SQL_TABLE_STAT e imposta NON_UNIQUE, INDEX_QUALIFIER, INDEX_NAME, ORDINAL_POSITION COLUMN_NAME, COLUMN_NAME e ASC_OR_DESC su NULL. Se CARDINALITY o PAGES non sono disponibili dall'origine dati, il driver le imposta su NULL.  
  
## <a name="code-example"></a>Esempio di codice  
 Per un esempio di codice di una funzione simile, vedere [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Recupero di una singola riga o di un blocco di dati in una direzione forward-only.|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Recupero di un blocco di dati o scorrimento di un set di risultati|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Restituzione delle colonne di chiavi esterne|[Funzione SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|Restituzione delle colonne di una chiave primariaReturning the columns of a primary key|[Funzione SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
