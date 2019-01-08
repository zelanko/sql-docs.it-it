---
title: Funzione SQLTables | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTables
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTables
helpviewer_keywords:
- SQLTables function [ODBC]
ms.assetid: 60d5068a-7d7c-447c-acc6-f3f2cf73440c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dfe77cba535b78f387a786ddc56f65cf87172644
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53212400"
---
# <a name="sqltables-function"></a>Funzione SQLTables
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: Apri gruppo  
  
 **Riepilogo**  
 **SQLTables** restituisce l'elenco di nomi di tabella, catalogo o schema e tipi di tabella, archiviati in un'origine dati specifica. Il driver restituisce le informazioni come set di risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLTables(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      TableType,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione per recuperata i risultati.  
  
 *CatalogName*  
 [Input] Nome del catalogo. Il *CatalogName* argomento accetta i criteri di ricerca se l'attributo di ambiente SQL_ODBC_VERSION SQL_OV_ODBC3; criteri di ricerca non vengono accettate se SQL_OV_ODBC2 è impostata. Se un driver supporta i cataloghi per alcune tabelle ma non per altri, ad esempio quando un driver recupera i dati da diversi DBMS, una stringa vuota ("") indica le tabelle che non dispone di cataloghi.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *CatalogName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *CatalogName* è un argomento di valore modello; viene considerato letteralmente e relativi case è significativa. Per altre informazioni, vedere [argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Input] Lunghezza in caratteri della **CatalogName*.  
  
 *NomeSchema*  
 [Input] Criterio di ricerca di stringa per i nomi degli schemi. Se un driver supporta gli schemi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da diversi DBMS, una stringa vuota ("") indica le tabelle che non hanno schemi.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *SchemaName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *SchemaName* è un argomento di valore modello; viene considerato letteralmente e relativi case è significativa.  
  
 *NameLength2*  
 [Input] Lunghezza in caratteri della **SchemaName*.  
  
 *TableName*  
 [Input] Criterio di ricerca per i nomi delle tabelle di stringhe.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *TableName* viene considerato come un identificatore e il caso non è significativo. Se si tratta, SQL_FALSE *TableName* è un argomento di valore modello; viene considerato letteralmente e relativi case è significativa.  
  
 *NameLength3*  
 [Input] Lunghezza in caratteri della **TableName*.  
  
 *TableType*  
 [Input] Elenco dei tipi di tabella in modo che corrispondano.  
  
 Si noti che l'attributo di istruzione SQL_ATTR_METADATA_ID non ha alcun effetto durante la *TableType* argomento. *TableType* è un argomento di elenco di valore, indipendentemente dall'impostazione di SQL_ATTR_METADATA_ID.  
  
 *NameLength4*  
 [Input] Lunghezza in caratteri della **TableType*.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLTables** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLTables** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|24000|Stato del cursore non valido|Il cursore è stato aperto scegliere il *StatementHandle*, e **SQLFetch** oppure **SQLFetchScroll** fosse stata chiamata. Questo errore viene restituito da Gestione Driver, se **SQLFetch** oppure **SQLFetchScroll** non restituisce SQL_NO_DATA e viene restituito dal driver se **SQLFetch** oppure **SQLFetchScroll** è stato restituito SQL_NO_DATA.<br /><br /> Un cursore è stato aperto nel *StatementHandle*, ma **SQLFetch** oppure **SQLFetchScroll** non fosse stata chiamata.|  
|40001|Errore di serializzazione.|Il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver non è riuscito ad allocare memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle*. Quindi la funzione è stata chiamata nuovamente sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY009|Utilizzo non valido del puntatore null|L'attributo di istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE, il *CatalogName* argomento era un puntatore null e il SQL_CATALOG_NAME *InfoType* restituisce che i nomi di catalogo sono supportati.<br /><br /> (DM) l'attributo di istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE e il *SchemaName* oppure *NomeTabella* argomento era un puntatore null.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stato chiamato SQLTables.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore di uno degli argomenti di lunghezza è minore di 0 ma non uguali a SQL_NTS.<br /><br /> Il valore di uno degli argomenti di lunghezza nome superato il valore di lunghezza massima consentita per il nome corrispondente.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|È stato specificato un catalogo e del driver o origine dati non supporta cataloghi.<br /><br /> È stato specificato uno schema e del driver o origine dati non supporta gli schemi.<br /><br /> È stato specificato un criterio di ricerca di stringa per il nome del catalogo, lo schema della tabella o nome della tabella e l'origine dati non supporta criteri di ricerca per uno o più di questi argomenti.<br /><br /> La combinazione delle impostazioni correnti degli attributi di istruzione SQL_ATTR_CURSOR_TYPE e SQL_ATTR_CONCURRENCY non era supportata dall'origine dati o driver.<br /><br /> L'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_VARIABLE e l'attributo SQL_ATTR_CURSOR_TYPE di istruzione è stata impostata su un tipo di cursore per i quali il driver non supporta i segnalibri.|  
|HYT00|Timeout|Il periodo di timeout query scaduto prima l'origine dati ha restituito il set di risultati richiesti. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **SQLTables** Elenca tutte le tabelle nell'intervallo richiesto. Un utente può o non abbia privilegi selezionati da una di queste tabelle. Per verificare l'accessibilità, un'applicazione può:  
  
-   Chiamare **SQLGetInfo** e controllare il tipo di informazioni SQL_ACCESSIBLE_TABLES.  
  
-   Chiamare **SQLTablePrivileges** per verificare i privilegi per ogni tabella.  
  
 In caso contrario, l'applicazione deve essere in grado di gestire una situazione in cui l'utente seleziona una tabella per cui **seleziona** non vengono concessi i privilegi.  
  
 Il *SchemaName* e *NomeTabella* argomenti accettano criteri di ricerca. Il *CatalogName* argomento accetta i criteri di ricerca se l'attributo di ambiente SQL_ODBC_VERSION SQL_OV_ODBC3; criteri di ricerca non vengono accettate se SQL_OV_ODBC2 è impostata. Se è impostata SQL_OV_ODBC3, un'applicazione ODBC 3 *. x* driver richiederà i caratteri che con caratteri jolly nel *CatalogName* argomento usare caratteri di escape per essere considerato letteralmente. Per altre informazioni sui pattern di ricerca validi, vedere [argomenti del valore criterio](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Per altre informazioni su uso generale, gli argomenti e i dati restituiti di funzioni di catalogo ODBC, vedere [funzioni di catalogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Per supportare l'enumerazione dei cataloghi, schemi e tipi di tabella, la semantica di speciale seguente venga definita per il *CatalogName*, *SchemaName*, *TableName*e  *TableType* argomenti del **SQLTables**:  
  
-   Se *CatalogName* è SQL_ALL_CATALOGS e *SchemaName* e *TableName* sono stringhe vuote, il set di risultati contiene un elenco di cataloghi validi per l'origine dati. (Tutte le colonne ad eccezione della colonna TABLE_CAT contengono valori null).  
  
-   Se *SchemaName* è SQL_ALL_SCHEMAS e *CatalogName* e *TableName* sono stringhe vuote, il set di risultati contiene un elenco di schemi validi per l'origine dati. (Tutte le colonne ad eccezione della colonna TABLE_SCHEM contengono valori null).  
  
-   Se *TableType* è SQL_ALL_TABLE_TYPES e *CatalogName*, *SchemaName*, e *TableName* sono stringhe vuote, il set di risultati contiene un elenco dei tipi di tabella validi per l'origine dati. (Tutte le colonne ad eccezione della colonna TABLE_TYPE contengono valori null).  
  
 Se *TableType* non è una stringa vuota, deve contenere un elenco con valori delimitati da virgole per i tipi di interesse, ogni valore può essere racchiuso tra virgolette singole (') o senza virgolette, ad esempio 'TABLE', 'VIEW' o tabella, visualizzare. Un'applicazione deve specificare sempre il tipo di tabella in maiuscole. il driver deve convertire il tipo di tabella in qualsiasi caso è necessario per l'origine dati. Se l'origine dati non supporta un tipo di tabella specificato **SQLTables** non restituisce alcun risultato per quel tipo.  
  
 **SQLTables** restituisce i risultati come un set di risultati standard, ordinato in base TABLE_TYPE, TABLE_CAT, TABLE_SCHEM e TABLE_NAME. Per informazioni su come è possibile usare queste informazioni, vedere [Usa i dati del catalogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Per determinare le lunghezze delle colonne TABLE_CAT TABLE_SCHEM e TABLE_NAME effettive, un'applicazione può chiamare **SQLGetInfo** con le informazioni SQL_MAX_CATALOG_NAME_LEN SQL_MAX_SCHEMA_NAME_LEN e SQL_MAX_TABLE_NAME_LEN tipi.  
  
 Le colonne seguenti sono state rinominate per ODBC 3*x*. Le modifiche ai nomi di colonna non influenzano la compatibilità con le versioni precedenti poiché nelle applicazioni associati dal numero di colonna.  
  
|Colonna ODBC 2.0|ODBC 3*x* colonna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 Nella tabella seguente elenca le colonne nel set di risultati. Le colonne aggiuntive oltre colonna 5 (note) possono essere definite dal driver. Un'applicazione deve accedere a colonne specifiche del driver contando dalla fine del gruppo di risultati anziché che specifica la posizione ordinale esplicita verso il basso. Per altre informazioni, vedere [i dati restituiti dalle funzioni catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome colonna|Numero colonna|Tipo di dati|Commenti|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nome del catalogo; NULL se non applicabile all'origine dati. Se un driver supporta i cataloghi per alcune tabelle ma non per altri utenti, ad esempio quando i dati vengono recuperati dai diversi DBMS, restituisce una stringa vuota ("") per le tabelle che non dispone di cataloghi.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome dello schema; NULL se non applicabile all'origine dati. Se un driver supporta gli schemi per alcune tabelle ma non per altri utenti, ad esempio quando i dati vengono recuperati dai diversi DBMS, restituisce una stringa vuota ("") per le tabelle che non hanno schemi.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar|Nome della tabella.|  
|TABLE_TYPE (ODBC 1.0)|4|Varchar|Nome tipo di tabella. uno dei seguenti: "TABLE", "Visualizzazione", "Tabella di sistema", "Temporanei globali", "Locale temporanea", "ALIAS", "SINONIMI" o un nome di tipo specifiche dell'origine dati.<br /><br /> Il significato di "ALIAS" e "SINONIMI" è specifici del driver.|  
|SEZIONE OSSERVAZIONI (ODBC 1.0)|5|Varchar|Descrizione della tabella.|  
  
## <a name="example"></a>Esempio  
 Esempio di codice seguente non libera gli handle e le connessioni. Visualizzare [funzione SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) e [SQLFreeStmt-funzione](../../../odbc/reference/syntax/sqlfreestmt-function.md) per esempi di codice liberare l'handle e le istruzioni.  
  
```  
// SQLTables.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
// simple helper functions  
int MySQLSuccess(SQLRETURN rc) {  
   return (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO);  
}  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printCatalog(const struct DataBinding* catalogResult) {  
   if (catalogResult[0].StrLen_or_Ind != SQL_NULL_DATA)   
      printf("Catalog Name = %s\n", (char *)catalogResult[0].TargetValuePtr);  
}  
  
// remember to disconnect and free memory, and free statements and handles  
int main() {  
   int bufferSize = 1024, i, numCols = 5;  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   wchar_t* dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   wchar_t* userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR*)"Driver={SQL Server}", SQL_NTS, (SQLCHAR*)connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
  
   bufferSize = 1024;  
  
   // allocate memory for the binding  
   // free this memory when done  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // setup the binding (can be used even if the statement is closed by closeStatementHandle)  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   // all catalogs query  
   printf( "A list of names of all catalogs\n" );  
   retCode = SQLTables( hstmt, (SQLCHAR*)SQL_ALL_CATALOGS, SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS );  
   for ( retCode = SQLFetch(hstmt) ;  MySQLSuccess(retCode) ; retCode = SQLFetch(hstmt) )  
      printCatalog( catalogResult );  
}  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultati|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione dei privilegi per una o più colonne|[Funzione SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Restituzione di colonne in una o più tabelle|[Funzione SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Il recupero di una singola riga o un blocco di dati in una direzione di tipo forward-only|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Imposta il recupero di un blocco di dati o lo scorrimento di un risultato|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Restituzione delle statistiche delle tabelle e indici|[Funzione SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Restituzione dei privilegi per una o più tabelle|[Funzione SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
