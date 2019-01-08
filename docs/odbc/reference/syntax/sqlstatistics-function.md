---
title: Funzione SQLStatistics | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cd0503b9f0169a19179bcee545132279903ea10
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207550"
---
# <a name="sqlstatistics-function"></a>Funzione SQLStatistics
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLStatistics** recupera un elenco delle statistiche su una singola tabella e gli indici associati alla tabella. Il driver restituisce le informazioni come set di risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
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
 [Input] Handle di istruzione.  
  
 *CatalogName*  
 [Input] Nome del catalogo. Se un driver supporta i cataloghi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da diversi DBMS, una stringa vuota ("") indica le tabelle che non dispone di cataloghi. *CatalogName* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *CatalogName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *CatalogName* è un normale argomento; viene considerato letteralmente e relativi case è significativa. Per altre informazioni, vedere [argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Input] Lunghezza in caratteri della **CatalogName*.  
  
 *NomeSchema*  
 [Input] Nome dello schema. Se un driver supporta gli schemi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da diversi DBMS, una stringa vuota ("") indica le tabelle che non hanno schemi. *NomeSchema* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *SchemaName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *SchemaName* è un normale argomento; viene considerato letteralmente e relativi case è significativa.  
  
 *NameLength2*  
 [Input] Lunghezza in caratteri della **SchemaName*.  
  
 *TableName*  
 [Input] Nome della tabella. Questo argomento non può essere un puntatore null. *NomeSchema* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *TableName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *TableName* è un normale argomento; viene considerato letteralmente e relativi case è significativa.  
  
 *NameLength3*  
 [Input] Lunghezza in caratteri della **TableName*.  
  
 *Univoco*  
 [Input] Tipo di indice: SQL_INDEX_UNIQUE o SQL_INDEX_ALL.  
  
 *Reserved*  
 [Input] Indica l'importanza delle colonne della CARDINALITÀ e le pagine nel set di risultati. Le opzioni seguenti interessano la restituzione di sola lettura; le colonne della CARDINALITÀ e le pagine informazioni sugli indici viene restituiti anche se la CARDINALITÀ e le pagine non vengono restituite.  
  
 SQL_ENSURE richiede che il driver di recuperare in modo incondizionato le statistiche. (I driver che sono conformi solo allo standard Open Group e non sono supportate estensioni ODBC non sarà in grado di supportare SQL_ENSURE.)  
  
 SQL_QUICK richiede che il driver di recuperare la CARDINALITÀ e le pagine solo se sono immediatamente disponibili dal server. In tal caso, il driver non garantisce che i valori siano aggiornati. (Le applicazioni che vengono scritti allo standard Open Group otterranno sempre il comportamento di SQL_QUICK da ODBC 3*x*-driver conformi a.)  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLStatistics** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLStatistics** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|24000|Stato del cursore non valido|Il cursore è stato aperto scegliere il *StatementHandle*, e **SQLFetch** oppure **SQLFetchScroll** fosse stata chiamata. Questo errore viene restituito da Gestione Driver, se **SQLFetch** oppure **SQLFetchScroll** non restituisce SQL_NO_DATA e viene restituito dal driver se **SQLFetch** oppure **SQLFetchScroll** è stato restituito SQL_NO_DATA.<br /><br /> Un cursore è stato aperto nel *StatementHandle*, ma **SQLFetch** oppure **SQLFetchScroll** non fosse stata chiamata.|  
|40001|Errore di serializzazione.|Il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver non è riuscito ad allocare memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle*, quindi è stata chiamata la funzione anche in questo caso sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY009|Utilizzo non valido del puntatore null|Il *TableName* argomento era un puntatore null.<br /><br /> L'attributo di istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE, il *CatalogName* argomento era un puntatore null e il SQL_CATALOG_NAME *InfoType* restituisce che i nomi di catalogo sono supportati.<br /><br /> (DM) l'attributo di istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE e il *SchemaName* argomento era un puntatore null.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLStatistics** funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore di uno degli argomenti di lunghezza nome era minore di 0 ma non uguale a SQL_NTS.<br /><br /> Il valore di uno degli argomenti di lunghezza nome superato il valore di lunghezza massima consentita per il nome corrispondente.|  
|HY100|Tipo di opzione di univocità non compreso nell'intervallo|(DM) non valido *Unique* valore specificato.|  
|HY101|Tipo di opzione di accuratezza non compreso nell'intervallo|(DM) non valido *riservato* valore specificato.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|È stato specificato un catalogo e del driver o origine dati non supporta cataloghi.<br /><br /> È stato specificato uno schema e del driver o origine dati non supporta gli schemi.<br /><br /> La combinazione delle impostazioni correnti degli attributi di istruzione SQL_ATTR_CURSOR_TYPE e SQL_ATTR_CONCURRENCY non era supportata dall'origine dati o driver.<br /><br /> L'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_VARIABLE e l'attributo SQL_ATTR_CURSOR_TYPE di istruzione è stata impostata su un tipo di cursore per i quali il driver non supporta i segnalibri.|  
|HYT00|Timeout|Il periodo di timeout query scaduto prima l'origine dati ha restituito il set di risultati richiesti. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **SQLStatistics** restituisce informazioni su una singola tabella come set di risultati standard, ordinati in base NON_UNIQUE, tipo, INDEX_QUALIFIER, INDEX_NAME e ORDINAL_POSITION. Il set di risultati combina le informazioni statistiche (nelle colonne della CARDINALITÀ e le pagine del set di risultati) per la tabella con le informazioni su ogni indice. Per informazioni su come è possibile usare queste informazioni, vedere [Usa i dati del catalogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Per determinare la lunghezza effettiva delle colonne TABLE_CAT, TABLE_SCHEM, TABLE_NAME e COLUMN_NAME, un'applicazione può chiamare **SQLGetInfo** con SQL_MAX_CATALOG_NAME_LEN SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN, e le opzioni SQL_MAX_COLUMN_NAME_LEN.  
  
> [!NOTE]  
>  Per altre informazioni su uso generale, gli argomenti e i dati restituiti di funzioni di catalogo ODBC, vedere [funzioni di catalogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Le colonne seguenti sono state rinominate per ODBC 3*x*. Le modifiche ai nomi di colonna non influenzano la compatibilità con le versioni precedenti poiché nelle applicazioni associati dal numero di colonna.  
  
|Colonna ODBC 2.0|ODBC 3*x* colonna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 Nella tabella seguente elenca le colonne nel set di risultati. Ulteriori colonne successive alla 13 (FILTER_CONDITION) possono essere definite dal driver. Un'applicazione deve accedere a colonne specifiche del driver contando dalla fine del gruppo di risultati anziché che specifica la posizione ordinale esplicita verso il basso. Per altre informazioni, vedere [i dati restituiti dalle funzioni catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome colonna|Numero colonna|Tipo di dati|Commenti|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nome del catalogo della tabella a cui si applica l'indice o statistica; NULL se non applicabile all'origine dati. Se un driver supporta i cataloghi per alcune tabelle ma non per altri utenti, ad esempio quando i dati vengono recuperati dai diversi DBMS, restituisce una stringa vuota ("") per le tabelle che non dispone di cataloghi.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome dello schema della tabella a cui si applica l'indice o statistica; NULL se non applicabile all'origine dati. Se un driver supporta gli schemi per alcune tabelle ma non per altri utenti, ad esempio quando i dati vengono recuperati dai diversi DBMS, restituisce una stringa vuota ("") per le tabelle che non hanno schemi.|  
|TABLE_NAME (ODBC 1.0)|3|Non NULL varchar|Nome della tabella della tabella a cui si applica l'indice o statistica.|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|Indica se l'indice consente i valori duplicati:<br /><br /> SQL_TRUE se i valori di indice possono essere non univoci.<br /><br /> SQL_FALSE se i valori di indice devono essere univoci.<br /><br /> Se il tipo è SQL_TABLE_STAT, viene restituito NULL.|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|L'identificatore usato per qualificare l'indice nome operazione un **DROP INDEX**; Se un qualificatore di indice non è supportato dall'origine dati o se il tipo è SQL_TABLE_STAT, viene restituito NULL. Se in questa colonna viene restituito un valore diverso da null, deve essere utilizzato per qualificare il nome dell'indice in una **DROP INDEX** istruzione; in caso contrario, usare il TABLE_SCHEM per qualificare il nome dell'indice.|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|Nome dell'indice; Se il tipo è SQL_TABLE_STAT, viene restituito NULL.|  
|TIPO (ODBC 1.0)|7|Smallint non NULL|Tipo di informazioni da restituire:<br /><br /> SQL_TABLE_STAT indica una statistica per la tabella (nella colonna della CARDINALITÀ o pagine).<br /><br /> SQL_INDEX_BTREE indica un indice albero B.<br /><br /> SQL_INDEX_CLUSTERED indica un indice cluster.<br /><br /> SQL_INDEX_CONTENT indica un indice di contenuto.<br /><br /> SQL_INDEX_HASHED indica un indice hash.<br /><br /> SQL_INDEX_OTHER indica un altro tipo di indice.|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|Numero di sequenza di colonna nell'indice (a partire da 1); Se il tipo è SQL_TABLE_STAT, viene restituito NULL.|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|Nome colonna. Se la colonna è basata su un'espressione, ad esempio SALARY + vantaggi, viene restituita l'espressione; Se l'espressione non può essere determinato, viene restituita una stringa vuota. Se il tipo è SQL_TABLE_STAT, viene restituito NULL.|  
|ASC_OR_DESC (ODBC 1.0)|10|Char (1)|Sequenza di ordinamento per la colonna: "A" per ordine crescente; "D" per ordine decrescente; Se la sequenza di ordinamento colonne non è supportata dall'origine dati o se il tipo è SQL_TABLE_STAT, viene restituito NULL.|  
|CARDINALITÀ (ODBC 1.0)|11|Integer|Cardinalità della tabella o indice. numero di righe nella tabella se il tipo è SQL_TABLE_STAT; numero di valori univoci nell'indice se il tipo non è SQL_TABLE_STAT; Se il valore non è disponibile dall'origine dati, viene restituito NULL.|  
|PAGINE (ODBC 1.0)|12|Integer|Numero di pagine utilizzate per archiviare l'indice o tabella. numero di pagine per la tabella se il tipo è SQL_TABLE_STAT; numero di pagine per l'indice se il tipo non è SQL_TABLE_STAT; Se il valore non è disponibile dall'origine dati o se non applicabile all'origine dati, viene restituito NULL.|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|Se l'indice è un indice filtrato, questa è la condizione di filtro, ad esempio SALARY > 30000; Se non è possibile determinare la condizione di filtro, questa è una stringa vuota.<br /><br /> NULL se l'indice non è un indice filtrato, non è possibile determinare se l'indice è un indice filtrato o il tipo è SQL_TABLE_STAT.|  
  
 Se la riga nel set di risultati corrisponde a una tabella, il driver Imposta tipo su SQL_TABLE_STAT e NON_UNIQUE INDEX_QUALIFIER, INDEX_NAME, ORDINAL_POSITION, COLUMN_NAME e ASC_OR_DESC su NULL. Se la CARDINALITÀ o le pagine non sono disponibili dall'origine dati, il driver imposta su NULL.  
  
## <a name="code-example"></a>Esempio di codice  
 Per un esempio di codice di una funzione simile, vedere [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultati|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Durante il recupero di una singola riga o un blocco di dati in una direzione di tipo forward-only.|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Imposta il recupero di un blocco di dati o lo scorrimento di un risultato|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Restituisce le colonne di chiavi esterne|[Funzione SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|Restituisce le colonne di una chiave primaria|[Funzione SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
