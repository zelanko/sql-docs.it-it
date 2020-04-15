---
title: Funzione SQLSpecialColumns . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 826630e1d344322268a2f2638310b3a1e182de6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287171"
---
# <a name="sqlspecialcolumns-function"></a>Funzione SQLSpecialColumns
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: Open Group  
  
 **Riepilogo**  
 **SQLSpecialColumns** recupera le seguenti informazioni sulle colonne all'interno di una tabella specificata:  
  
-   Set ottimale di colonne che identifica in modo univoco una riga nella tabella.  
  
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
 [Ingresso] Handle di istruzione.  
  
 *Tipo identificatore*  
 [Ingresso] Tipo di colonna da restituire. Deve essere uno dei valori seguenti:   
  
 SQL_BEST_ROWID: restituisce la colonna o il set ottimale di colonne che, recuperando i valori dalla colonna o dalle colonne, consente di identificare in modo univoco qualsiasi riga della tabella specificata. Una colonna può essere una pseudo-colonna progettata specificamente per questo scopo (come in Oracle ROWID o Ingres TID) o la colonna o le colonne di qualsiasi indice univoco per la tabella.  
  
 SQL_ROWVER: restituisce la colonna o le colonne nella tabella specificata, se presenti, che vengono aggiornate automaticamente dall'origine dati quando qualsiasi valore nella riga viene aggiornato da qualsiasi transazione (come in SQLBase ROWID o Sybase TIMESTAMP).  
  
 *CatalogName*  
 [Ingresso] Nome del catalogo per la tabella. Se un driver supporta i cataloghi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, una stringa vuota ("") indica le tabelle che non dispongono di cataloghi. *CatalogName* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo statement SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *CatalogName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *CatalogName* è un argomento ordinario; viene trattato letteralmente, e il suo caso è significativo. Per ulteriori informazioni, vedere [Argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Ingresso] Lunghezza in caratteri di*nomeCatalogo*.  
  
 *Nome Schema*  
 [Ingresso] Nome dello schema per la tabella. Se un driver supporta gli schemi per alcune tabelle ma non per altri, ad esempio quando il driver recupera i dati da DBS diversi, una stringa vuota ("") indica le tabelle che non dispongono di schemi. *SchemaName* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *SchemaName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *SchemaName* è un argomento ordinario; viene trattato letteralmente, e il suo caso è significativo.  
  
 *NameLength2*  
 [Ingresso] Lunghezza in caratteri di :*NomeSchema*.  
  
 *Tablename*  
 [Ingresso] Nome della tabella. Questo argomento non può essere un puntatore null. *TableName* non può contenere un criterio di ricerca di stringa.  
  
 Se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, *TableName* viene considerato come un identificatore e il relativo caso non è significativo. Se è SQL_FALSE, *TableName* è un argomento ordinario; viene trattato letteralmente, e il suo caso è significativo.  
  
 *NameLength3*  
 [Ingresso] Lunghezza in caratteri di*nomeTabella*.  
  
 *Scope*  
 [Ingresso] Ambito minimo richiesto del rowid. Il valore restituito rowid può essere di ambito maggiore. I possibili valori sono i seguenti:  
  
 SQL_SCOPE_CURROW: il rowid è garantito per essere valido solo quando posizionato su tale riga. Una successiva riselezione utilizzando rowid potrebbe non restituire una riga se la riga è stata aggiornata o eliminata da un'altra transazione.  
  
 SQL_SCOPE_TRANSACTION: il rowid è garantito per essere valido per la durata della transazione corrente.  
  
 SQL_SCOPE_SESSION: il rowid è garantito per essere valido per la durata della sessione (oltre i limiti della transazione).  
  
 *Ammette i valori Null*  
 [Ingresso] Determina se restituire colonne speciali che possono avere un valore NULL. I possibili valori sono i seguenti:  
  
 SQL_NO_NULLS: escludere le colonne speciali che possono avere valori NULL. Alcuni driver non supportano SQL_NO_NULLS e questi driver restituiranno un set di risultati vuoto se è stato specificato SQL_NO_NULLS. Le applicazioni devono essere preparate per questo caso e richiedere SQL_NO_NULLS solo se è assolutamente necessario.  
  
 SQL_NULLABLE: restituisce colonne speciali anche se possono avere valori NULL.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSpecialColumns** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLSpecialColumns** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|24000|Stato del cursore non valido|Un cursore era aperto su *StatementHandle*e **SQLFetch** o **SQLFetchScroll** era stato chiamato. Questo errore viene restituito da Gestione Driver se **SQLFetch** o **SQLFetchScroll** non ha restituito SQL_NO_DATA e viene restituito dal driver se **SQLFetch** o **SQLFetchScroll** ha restituito SQL_NO_DATA.<br /><br /> Un cursore era aperto su *StatementHandle*, ma **SQLFetch** o **SQLFetchScroll** non era stato chiamato.|  
|40001|Errore di serializzazione|È stato eseguito il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*. Quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|I009|Utilizzo non valido del puntatore null|L'argomento *TableName* è un puntatore null.<br /><br /> L'attributo dell'istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE, l'argomento *CatalogName* è un puntatore null e il SQL_CATALOG_NAME *InfoType* restituisce che i nomi dei cataloghi sono supportati.<br /><br /> (DM) l'attributo dell'istruzione SQL_ATTR_METADATA_ID è stato impostato su SQL_TRUE e l'argomento *SchemaName* è un puntatore null.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione era ancora in esecuzione quando **SQLSpecialColumns** è stato chiamato.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) Il valore di uno degli argomenti di lunghezza era minore di 0 ma non uguale a SQL_NTS.<br /><br /> Il valore di uno degli argomenti di lunghezza ha superato il valore di lunghezza massima per il nome corrispondente. La lunghezza massima di ogni nome può essere ottenuta chiamando **SQLGetInfo** con i valori *InfoType:* SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN o SQL_MAX_TABLE_NAME_LEN.|  
|I097 (informazioni in stato INCUI)|Tipo di colonna non compreso nell'intervallo|(DM) È stato specificato un valore *IdentifierType* non valido.|  
|I098 (informazioni in stato IN CUI|Tipo di ambito non compreso nell'intervallo|(DM) È stato specificato un valore *Scope* non valido.|  
|I099|Tipo nullable non compreso nell'intervalloNullable type outof-ofrange|(DM) È stato specificato un valore *Nullable* non valido.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|È stato specificato un catalogo e il driver o l'origine dati non supporta i cataloghi.<br /><br /> È stato specificato uno schema e il driver o l'origine dati non supporta gli schemi.<br /><br /> La combinazione delle impostazioni correnti degli attributi di istruzione SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE non è supportata dal driver o dall'origine dati.<br /><br /> L'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_VARIABLE e l'attributo dell'istruzione SQL_ATTR_CURSOR_TYPE è stato impostato su un tipo di cursore per il quale il driver non supporta i segnalibri.|  
|HYT00|Timeout|Il periodo di timeout della query è scaduto prima che l'origine dati restituisca il set di risultati richiesto. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 Quando il *IdentifierType* argomento viene SQL_BEST_ROWID, **SQLSpecialColumns** restituisce la colonna o le colonne che identificano in modo univoco ogni riga della tabella. Queste colonne possono sempre essere utilizzate in un *elenco di selezione* o in una clausola **WHERE.** **SQLColumns**, utilizzato per restituire un'ampia gamma di informazioni sulle colonne di una tabella, non restituisce necessariamente le colonne che identificano in modo univoco ogni riga o le colonne che vengono aggiornate automaticamente quando qualsiasi valore nella riga viene aggiornato da una transazione. Ad esempio, **SQLColumns** potrebbe non restituire la pseudo-colonna Oracle ROWID. Questo è il motivo per cui **SQLSpecialColumns** viene utilizzato per restituire queste colonne. Per ulteriori informazioni, consultate [Usi dei dati del catalogo.](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
> [!NOTE]  
>  Per ulteriori informazioni sull'utilizzo generale, gli argomenti e i dati restituiti delle funzioni di catalogo ODBC, vedere Funzioni di [catalogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Se non sono presenti colonne che identificano in modo univoco ogni riga della tabella, **SQLSpecialColumns** restituisce un set di righe senza righe. una chiamata successiva a **SQLFetch** o **SQLFetchScroll** sull'istruzione restituisce SQL_NO_DATA.  
  
 Se gli argomenti *IdentifierType*, *Scope*o *Nullable* specificano caratteristiche non supportate dall'origine dati, **SQLSpecialColumns** restituisce un set di risultati vuoto.  
  
 Se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, gli argomenti *CatalogName*, *SchemaName*e *TableName* vengono considerati come identificatori, pertanto non possono essere impostati su un puntatore null in determinate situazioni. Per altre informazioni, vedere [Argomenti nelle funzioni del catalogo.](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
 **SQLSpecialColumns** restituisce i risultati come set di risultati standard, ordinati in base a SCOPE.  
  
 Le colonne seguenti sono state rinominate per ODBC *3.x*. Le modifiche del nome della colonna non influiscono sulla compatibilità con le versioni precedenti perché le applicazioni vengono associate in base al numero di colonna.  
  
|Colonna ODBC 2.0|Colonna ODBC *3.x*|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 Per determinare la lunghezza effettiva della colonna COLUMN_NAME, un'applicazione può chiamare **SQLGetInfo** con l'opzione SQL_MAX_COLUMN_NAME_LEN.  
  
 Nella tabella seguente sono elencate le colonne del set di risultati. Colonne aggiuntive oltre la colonna 8 (PSEUDO_COLUMN) possono essere definite dal driver. Un'applicazione deve ottenere l'accesso alle colonne specifiche del driver eseguendo il conto alla rovescia dalla fine del set di risultati anziché specificare una posizione ordinale esplicita. Per ulteriori informazioni, vedere [Dati restituiti da Funzioni di catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome colonna|Numero di colonna|Tipo di dati|Commenti|  
|-----------------|-------------------|---------------|--------------|  
|AMBITO (ODBC 1.0)|1|Smallint|Ambito effettivo del rowid. Contiene uno dei seguenti valori:<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> NULL viene restituito quando *IdentifierType* è SQL_ROWVER. Per una descrizione di ogni valore, vedere la descrizione *dell'ambito* in "Sintassi", più indietro in questa sezione.|  
|COLUMN_NAME (ODBC 1.0)|2|Varchar non NULL|Nome colonna. Il driver restituisce una stringa vuota per una colonna che non dispone di un nome.|  
|DATA_TYPE (ODBC 1.0)|3|Smallint non NULL|Tipo di dati SQL. Può trattarsi di un tipo di dati SQL ODBC o di un tipo di dati SQL specifico del driver. Per un elenco dei tipi di dati SQL ODBC validi, vedere [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md). Per informazioni sui tipi di dati SQL specifici del driver, vedere la documentazione del driver.|  
|TYPE_NAME (ODBC 1.0)|4|Varchar non NULL|Nome del tipo di dati dipendente dall'origine dati; ad esempio, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" o "CHAR ( ) PER BIT DATA".|  
|COLUMN_SIZE (ODBC 1.0)|5|Integer|Dimensioni della colonna nell'origine dati. Per ulteriori informazioni sulle dimensioni delle colonne, vedere [Dimensioni colonna, Cifre decimali, Lunghezza ottetto](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)di trasferimento e Dimensioni di visualizzazione .|  
|BUFFER_LENGTH (ODBC 1.0)|6|Integer|Lunghezza in byte di dati trasferiti in un'operazione **SQLGetData** o **SQLFetch** se SQL_C_DEFAULT è specificato. Per i dati numerici, questa dimensione può essere diversa da quella dei dati archiviati nell'origine dati. Questo valore è uguale alla colonna COLUMN_SIZE per i dati di tipo carattere o binario. Per ulteriori informazioni, vedere [Dimensione colonna, Cifre decimali, Lunghezza ottetto di trasferimento e Dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|Cifre decimali della colonna nell'origine dati. Viene restituito NULL per i tipi di dati in cui le cifre decimali non sono applicabili. Per ulteriori informazioni sulle cifre decimali, vedere [Dimensioni colonna, Cifre decimali, Lunghezza ottetto](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)di trasferimento e Dimensioni di visualizzazione .|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|Indica se la colonna è una pseudo-colonna, ad esempio Oracle ROWID:<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **Nota:** per la massima interoperabilità, le pseudo-colonne non devono essere racchiuse tra virgolette con il carattere di virgolette dell'identificatore restituito da **SQLGetInfo**.|  
  
 Dopo che l'applicazione recupera i valori per SQL_BEST_ROWID, l'applicazione può utilizzare questi valori per riselezionare tale riga all'interno dell'ambito definito. È garantito che l'istruzione **SELECT** non restituisca nessuna riga o una riga.  
  
 Se un'applicazione riseleziona una riga in base alla colonna o alle colonne rowid e la riga non viene trovata, l'applicazione può presupporre che la riga sia stata eliminata o che le colonne rowid siano state modificate. Non è vero il contrario: anche se il rowid non è stato modificato, le altre colonne nella riga potrebbero essere state modificate.  
  
 Le colonne restituite per il tipo di colonna SQL_BEST_ROWID sono utili per le applicazioni che devono scorrere avanti e indietro all'interno di un set di risultati per recuperare i dati più recenti da un set di righe. La colonna o le colonne del rowid sono garantite per non cambiare mentre sono posizionate su tale riga.  
  
 La colonna o le colonne del rowid possono rimanere valide anche quando il cursore non è posizionato sulla riga. l'applicazione può determinare questo controllando la colonna SCOPE nel set di risultati.  
  
 Le colonne restituite per i SQL_ROWVER del tipo di colonna sono utili per le applicazioni che richiedono la possibilità di verificare se le colonne in una determinata riga sono state aggiornate mentre la riga è stata riselezionata utilizzando rowid. Ad esempio, dopo aver riselezionato una riga utilizzando rowid, l'applicazione può confrontare i valori precedenti nelle colonne SQL_ROWVER con quelle appena recuperate. Se il valore in una colonna SQL_ROWVER è diverso dal valore precedente, l'applicazione può avvisare l'utente che i dati sullo schermo sono stati modificati.  
  
## <a name="code-example"></a>Esempio di codice  
 Per un esempio di codice di una funzione simile, vedere [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione delle colonne in una tabella o tabelleReturning the columns in a table or tables|[Funzione SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Recupero di una singola riga o di un blocco di dati in una direzione forward-only|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Recupero di un blocco di dati o scorrimento di un set di risultati|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Restituzione delle colonne di una chiave primariaReturning the columns of a primary key|[Funzione SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
