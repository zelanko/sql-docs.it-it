---
title: Funzione SQLGetData . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetData
helpviewer_keywords:
- SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac11505b8e47dae8df53af27c64a7ee6372b3f28
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285507"
---
# <a name="sqlgetdata-function"></a>Funzione SQLGetData
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLGetData** recupera i dati per una singola colonna nel set di risultati o per un singolo parametro dopo **che SQLParamData** restituisce SQL_PARAM_DATA_AVAILABLE. Può essere chiamato più volte per recuperare dati a lunghezza variabile in parti.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLGetData(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   Col_or_Param_Num,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *Col_or_Param_Num*  
 [Ingresso] Per il recupero dei dati della colonna, è il numero della colonna per la quale restituire i dati. Le colonne del set di risultati sono numerate in ordine crescente a partire da 1.Result set columns are numbered in increasing column order starting at 1. La colonna del segnalibro è il numero di colonna 0; può essere specificato solo se i segnalibri sono abilitati.  
  
 Per il recupero dei dati del parametro, è l'ordinale del parametro, che inizia da 1.  
  
 *Targettype*  
 [Ingresso] Identificatore del tipo di dati C del buffer*di TargetValuePtr.* Per un elenco dei tipi di dati C validi e degli identificatori di tipo, vedere la sezione Tipi di [dati C](../../../odbc/reference/appendixes/c-data-types.md) nell'Appendice D: Tipi di dati.  
  
 Se *TargetType* è SQL_ARD_TYPE, il driver utilizza l'identificatore di tipo specificato nel campo SQL_DESC_CONCISE_TYPE dell'ARD. Se *TargetType* è SQL_APD_TYPE, **SQLGetData** utilizzerà lo stesso tipo di dati C specificato in **SQLBindParameter**. In caso contrario, il tipo di dati C specificato in **SQLGetData** esegue l'override del tipo di dati C specificato in **SQLBindParameter**. Se è SQL_C_DEFAULT, il driver seleziona il tipo di dati C predefinito in base al tipo di dati SQL dell'origine.  
  
 È inoltre possibile specificare un tipo di dati C esteso. Per ulteriori informazioni, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Uscita] Puntatore al buffer in cui restituire i dati.  
  
 *TargetValuePtr* non può essere NULL.  
  
 *BufferLength*  
 [Ingresso] Lunghezza del buffer*TargetValuePtr* in byte.  
  
 Il driver utilizza *BufferLength* per evitare \*di scrivere oltre la fine del *TargetValuePtr* buffer durante la restituzione di dati a lunghezza variabile, ad esempio dati di tipo carattere o binario. Si noti che il driver conta il carattere di terminazione null quando si restituiscono dati di tipo carattere a \* *TargetValuePtr*. **TargetValuePtr* deve quindi contenere spazio per il carattere di terminazione null oppure il driver tronca i dati.  
  
 Quando il driver restituisce dati a lunghezza fissa, ad esempio un numero intero o una struttura di data, il driver ignora *BufferLength* e presuppone che il buffer è sufficientemente grande per contenere i dati. È quindi importante che l'applicazione allochi un buffer sufficientemente grande per i dati a lunghezza fissa o che il driver scriva oltre la fine del buffer.  
  
 **SQLGetData** restituisce SQLSTATE HY090 (stringa non valida o lunghezza del buffer) quando *BufferLength* è minore di 0 ma non quando *BufferLength* è 0.  
  
 *StrLen_or_IndPtr*  
 [Uscita] Puntatore al buffer in cui restituire il valore della lunghezza o dell'indicatore. Se si tratta di un puntatore null, non viene restituito alcun valore di lunghezza o indicatore. Restituisce un errore quando i dati recuperati sono NULL.  
  
 **SQLGetData** può restituire i valori seguenti nel buffer di lunghezza/indicatore:SQLGetData can return the following values in the length/indicator buffer:  
  
-   La lunghezza dei dati disponibili per la restituzione  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 Per ulteriori informazioni, vedere [Utilizzo di valori di lunghezza/indicatore](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) e "Commenti" in questo argomento.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetData** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetData** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Non tutti i dati per la colonna specificata, *Col_or_Param_Num*, possono essere recuperati in una singola chiamata alla funzione. SQL_NO_TOTAL o la lunghezza dei dati rimanenti nella colonna specificata prima della \*chiamata corrente a **SQLGetData** viene restituita in *StrLen_or_IndPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)<br /><br /> Per altre informazioni sull'uso di più chiamate a **SQLGetData** per una singola colonna, vedere "Commenti".|  
|01S07 (intito)|Troncamento frazionario|I dati restituiti per una o più colonne sono stati troncati. Per i tipi di dati numerici, la parte frazionaria del numero è stata troncata. Per i tipi di dati time, timestamp e interval contenenti un componente time, la parte frazionaria dell'ora è stata troncata.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07006|Violazione dell'attributo del tipo di dati con restrizioniRestricted data type attribute violation|Il valore dei dati di una colonna nel set di risultati non può essere convertito nel tipo di dati C specificato dall'argomento *TargetType*.|  
|07009|Indice descrittore non valido|Il valore specificato per l'argomento *Col_or_Param_Num* è 0 e l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_OFF.<br /><br /> Il valore specificato per l'argomento *Col_or_Param_Num* è maggiore del numero di colonne nel set di risultati.<br /><br /> Il *valore Col_or_Param_Num* non è uguale all'ordinale del parametro disponibile.<br /><br /> (DM) La colonna specificata è stata associata. Questa descrizione non si applica ai driver che restituiscono la maschera di bit SQL_GD_BOUND per l'opzione SQL_GETDATA_EXTENSIONS in **SQLGetInfo**.<br /><br /> (DM) Il numero della colonna specificata è minore o uguale al numero della colonna più alta. Questa descrizione non si applica ai driver che restituiscono la maschera di bit SQL_GD_ANY_COLUMN per l'opzione SQL_GETDATA_EXTENSIONS in **SQLGetInfo**.<br /><br /> (DM) L'applicazione ha già chiamato **SQLGetData** per la riga corrente; il numero della colonna specificata nella chiamata corrente è minore del numero della colonna specificata nella chiamata precedente; e il driver non restituisce la maschera di bit SQL_GD_ANY_ORDER per l'opzione SQL_GETDATA_EXTENSIONS in **SQLGetInfo**.<br /><br /> (DM) l'argomento *TargetType* è stato SQL_ARD_TYPE e il record del descrittore *di Col_or_Param_Num* nell'ARD non ha superato la verifica di coerenza.<br /><br /> (DM) l'argomento *TargetType* è stato SQL_ARD_TYPE e il valore nel campo SQL_DESC_COUNT dell'ARD era minore dell'argomento *Col_or_Param_Num.*|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|22002|Variabile indicatore richiesta ma non fornita|*StrLen_or_IndPtr* era un puntatore null ed è stato recuperato dati NULL.|  
|22003|Valore numerico non compreso nell'intervallo|La restituzione del valore numerico (come numerico o stringa) per la colonna avrebbe causato il troncamento dell'intera parte (anziché frazionaria) del numero.<br /><br /> Per ulteriori informazioni, vedere [Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato datetime non valido|La colonna di caratteri nel set di risultati è stata associata a una struttura di data, ora o timestamp C e il valore nella colonna era rispettivamente una data, un'ora o un timestamp non valido. Per ulteriori informazioni, vedere [Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22012|Divisione per zero|È stato restituito un valore da un'espressione aritmetica che ha restituito la divisione per zero.|  
|22015|Overflow campo intervallo|L'assegnazione da un tipo SQL esatto numero o intervallo a un tipo di intervallo C ha causato una perdita di cifre significative nel campo iniziale.<br /><br /> Quando si restituiscono dati a un tipo di intervallo C, non è stata eseguito alcuna rappresentazione del valore del tipo SQL nel tipo di intervallo C.|  
|22018|Valore di carattere non valido per la specifica del cast|Una colonna di caratteri nel set di risultati è stata restituita a un buffer di caratteri C e la colonna contiene un carattere per il quale non era presente alcuna rappresentazione nel set di caratteri del buffer.<br /><br /> Il tipo C era un numero esatto o approssimativo, un datetime o un tipo di dati interval; il tipo SQL della colonna era un tipo di dati carattere; e il valore nella colonna non è un valore letterale valido del tipo C associato.|  
|24000|Stato del cursore non valido|(DM) la funzione è stata chiamata senza prima chiamare **SQLFetch** o **SQLFetchScroll** per posizionare il cursore sulla riga di dati necessari.<br /><br /> (DM) *StatementHandle* era in uno stato eseguito, ma a *StatementHandle*non era associato alcun set di risultati .<br /><br /> Un cursore era aperto su *StatementHandle* e **SQLFetch** o **SQLFetchScroll** era stato chiamato, ma il cursore è stato posizionato prima dell'inizio del set di risultati o dopo la fine del set di risultati.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer *MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY003|Tipo di programma fuori intervallo|(DM) l'argomento *TargetType* non è un tipo di dati valido, SQL_C_DEFAULT, SQL_ARD_TYPE (in caso di recupero dei dati della colonna) o SQL_APD_TYPE (in caso di recupero dei dati del parametro).<br /><br /> (DM) l'argomento *Col_or_Param_Num* era 0 e l'argomento *TargetType* non è stato SQL_C_BOOKMARK per un segnalibro a lunghezza fissa o SQL_C_VARBOOKMARK per un segnalibro di lunghezza variabile.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*, quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread, quindi la funzione è stata chiamata nuovamente su *StatementHandle*.|  
|I009|Utilizzo non valido del puntatore null|(DM) l'argomento *TargetValuePtr* era un puntatore null.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) *L'oggetto statementHandle* specificato non era in uno stato eseguito. La funzione è stata chiamata senza prima chiamare **SQLExecDirect**, **SQLExecute** o una funzione di catalogo.<br /><br /> (DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLGetData.This** asynchronous function was still executing when the SQLGetData function was called.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) *StatementHandle* era in uno stato eseguito, ma a *StatementHandle*non era associato alcun set di risultati .<br /><br /> Una chiamata a **SQLExeceute**, **SQLExecDirect**o **SQLMoreResults** ha restituito SQL_PARAM_DATA_AVAILABLE, ma è stato chiamato **SQLGetData,** anziché **SQLParamData**.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore specificato per l'argomento *BufferLength* è minore di 0.<br /><br /> Il valore specificato per l'argomento *BufferLength* era minore di 4, l'argomento *Col_or_Param_Num* è stato impostato su 0 e il driver era un driver *.x* ODBC 2.|  
|I109|Posizione del cursore non valida|Il cursore è stato posizionato (da **SQLSetPos**, **SQLFetch**, **SQLFetchScroll**o **SQLBulkOperations**) su una riga che era stata eliminata o non poteva essere recuperata.<br /><br /> Il cursore era un cursore forward-only e la dimensione del set di righe era maggiore di uno.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il driver o l'origine dati non supporta l'utilizzo di **SQLGetData** con più righe in **SQLFetchScroll**. Questa descrizione non si applica ai driver che restituiscono la maschera di bit SQL_GD_BLOCK per l'opzione SQL_GETDATA_EXTENSIONS in **SQLGetInfo**.<br /><br /> Il driver o l'origine dati non supporta la conversione specificata dalla combinazione di *TargetType* argomento e il tipo di dati SQL della colonna corrispondente. Questo errore si applica solo quando il tipo di dati SQL della colonna è stato mappato a un tipo di dati SQL specifico del driver.<br /><br /> Il driver supporta solo ODBC 2 *.x*e l'argomento *TargetType* è uno dei seguenti:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e uno qualsiasi dei tipi di dati di intervallo C elencati in [Tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) nell'Appendice D: Tipi di dati.<br /><br /> Il driver supporta solo le versioni ODBC precedenti alla 3.50 e l'argomento *TargetType* è stato SQL_C_GUID.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver corrispondente a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **SQLGetData** restituisce i dati in una colonna specificata. **SQLGetData** può essere chiamato solo dopo che una o più righe sono state recuperate dal set di risultati da **SQLFetch**, **SQLFetchScroll**o **SQLExtendedFetch .** Se i dati a lunghezza variabile sono troppo grandi per essere restituiti in una singola chiamata a **SQLGetData** (a causa di una limitazione nell'applicazione), **SQLGetData** può recuperarlo in parti. È possibile associare alcune colonne in una riga e chiamare **SQLGetData** per altri, anche se questo è soggetto ad alcune restrizioni. Per ulteriori informazioni, vedere [Recupero di dati lunghi](../../../odbc/reference/develop-app/getting-long-data.md).  
  
 Per informazioni **sull'utilizzo di SQLGetData** con parametri di output trasmessi, vedere Recupero di parametri di [output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-sqlgetdata"></a>Utilizzo di SQLGetDataUsing SQLGetData  
 Se il driver non supporta le estensioni di **SQLGetData**, la funzione può restituire dati solo per le colonne non associate con un numero maggiore di quello dell'ultima colonna associata. Inoltre, all'interno di una riga di dati, il valore *dell'argomento Col_or_Param_Num* in ogni chiamata a **SQLGetData** deve essere maggiore o uguale al valore di *Col_or_Param_Num* nella chiamata precedente; vale a dire, i dati devono essere recuperati in ordine crescente di numero di colonna. Infine, se non sono supportate estensioni, SQLGetData non può essere chiamato se la dimensione del set di righe è maggiore di 1.Finally, if no extensions are supported, **SQLGetData** cannot be called if the rowset size is greater than 1.  
  
 I conducenti possono rilassare una qualsiasi di queste restrizioni. Per determinare quali restrizioni si allenta un driver, un'applicazione chiama **SQLGetInfo** con una delle seguenti opzioni di SQL_GETDATA_EXTENSIONS:  
  
-   SQL_GD_OUTPUT_PARAMS **SQLGetData** può essere chiamato per restituire i valori dei parametri di output. Per ulteriori informazioni, vedere Recupero di parametri di [output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_GD_ANY_COLUMN. Se viene restituita questa opzione, **SQLGetData** può essere chiamato per qualsiasi colonna non associata, inclusi quelli prima dell'ultima colonna associata.  
  
-   SQL_GD_ANY_ORDER. Se viene restituita questa opzione, **SQLGetData** può essere chiamato per le colonne non associate in qualsiasi ordine.  
  
-   SQL_GD_BLOCK. Se questa opzione viene restituita da **SQLGetInfo** per l'SQL_GETDATA_EXTENSIONS InfoType, il driver supporta le chiamate a **SQLGetData** quando la dimensione del set di righe è maggiore di 1 e l'applicazione può chiamare **SQLSetPos** con l'opzione SQL_POSITION per posizionare il cursore sulla riga corretta prima di chiamare **SQLGetData.**  
  
-   SQL_GD_BOUND. Se viene restituita questa opzione, **SQLGetData** può essere chiamato per le colonne associate e le colonne non associate.  
  
 Ci sono due eccezioni a queste restrizioni e la capacità di un conducente di rilassarli. In primo luogo, SQLGetData non deve mai essere chiamato per un cursore forward-only quando la dimensione del set di righe è maggiore di 1.First, **SQLGetData** should never be called for a forward-only cursor when the rowset size is greater than 1. In secondo luogo, se un driver supporta i segnalibri, deve sempre supportare la possibilità di chiamare **SQLGetData** per la colonna 0, anche se non consente alle applicazioni di chiamare **SQLGetData** per altre colonne prima dell'ultima colonna associata. (Quando un'applicazione utilizza un driver *.x* ODBC 2, **SQLGetData** restituirà correttamente un segnalibro quando viene chiamato con *Col_or_Param_Num* uguale a 0 dopo una chiamata a **SQLFetch**, poiché **SQLFetch** viene mappato da Gestione driver ODBC 3 *.x* a **SQLExtendedFetch** con un *FetchOrientation* di SQL_FETCH_NEXT e **SQLGetData** con un *Col_or_Param_Num* di 0 è mappato da Gestione Driver ODBC 3 *.x* a **SQLGetStmtOption** con un *fOption* di SQL_GET_BOOKMARK.)  
  
 **Impossibile utilizzare SQLGetData** per recuperare il segnalibro per una riga appena inserita chiamando **SQLBulkOperations** con l'opzione SQL_ADD, perché il cursore non è posizionato sulla riga. Un'applicazione può recuperare il segnalibro per tale riga associando la colonna 0 prima di chiamare **SQLBulkOperations** con SQL_ADD, nel qual caso **SQLBulkOperations** restituisce il segnalibro nel buffer associato. **SQLFetchScroll** può quindi essere chiamato con SQL_FETCH_BOOKMARK per riposizionare il cursore su tale riga.  
  
 Se l'argomento *TargetType* è un tipo di dati intervallo, per i dati vengono utilizzati rispettivamente la precisione di interlinea predefinita (2) e la precisione predefinita dei secondi dell'intervallo (6), come impostato nei campi SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION dell'ARD. Se l'argomento *TargetType* è un tipo di dati SQL_C_NUMERIC, per i dati vengono utilizzati la precisione predefinita (definita dal driver) e la scala predefinita (0), come impostato nei campi SQL_DESC_PRECISION e SQL_DESC_SCALE dell'ARD. Se la precisione o la scala predefinita non è appropriata, l'applicazione deve impostare in modo esplicito il campo del descrittore appropriato tramite una chiamata a **SQLSetDescField** o **SQLSetDescRec**. Può impostare il campo SQL_DESC_CONCISE_TYPE su SQL_C_NUMERIC e chiamare **SQLGetData** con un *TargetType* argomento di SQL_ARD_TYPE, che causerà i valori di precisione e scala nei campi del descrittore da utilizzare.  
  
> [!NOTE]
>  In ODBC 2 *.x*, le applicazioni impostano *TargetType* su SQL_C_DATE, SQL_C_TIME o SQL_C_TIMESTAMP per indicare che \* *TargetValuePtr* è una struttura di data, ora o timestamp. In ODBC 3 *.x*, le applicazioni impostano *TargetType* su SQL_C_TYPE_DATE, SQL_C_TYPE_TIME o SQL_C_TYPE_TIMESTAMP. Gestione Driver esegue i mapping appropriati, se necessario, in base alla versione dell'applicazione e del driver.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>Recupero di dati a lunghezza variabile nelle partiRetrieving Variable-Length Data in Parts  
 **SQLGetData** può essere utilizzato per recuperare dati da una colonna che contiene dati di lunghezza variabile in parti, ovvero quando l'identificatore del tipo di dati SQL della colonna è SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL_WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY o un identificatore specifico del driver per un tipo a lunghezza variabile.  
  
 Per recuperare dati da una colonna in parti, l'applicazione chiama **SQLGetData** più volte in successione per la stessa colonna. A ogni chiamata, **SQLGetData** restituisce la parte successiva dei dati. Spetta all'applicazione riassemblare le parti, avendo cura di rimuovere il carattere di terminazione null dalle parti intermedie dei dati di tipo carattere. Se sono presenti più dati da restituire o non è stato allocato un buffer sufficiente per il carattere di terminazione, **SQLGetData** restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dati troncati). Quando restituisce l'ultima parte dei dati, **SQLGetData** restituisce SQL_SUCCESS. Né SQL_NO_TOTAL né zero possono essere restituiti nell'ultima chiamata valida per recuperare dati da una colonna, perché l'applicazione non avrebbe quindi modo di conoscere la quantità di dati nel buffer dell'applicazione è valida. Se **SQLGetData** viene chiamato dopo questo, restituisce SQL_NO_DATA. Per altre informazioni, vedere la sezione successiva, "Recupero di dati con SQLGetData".  
  
 I segnalibri di lunghezza variabile possono essere restituiti in parti da **SQLGetData**. Come con altri dati, una chiamata a **SQLGetData** per restituire segnalibri di lunghezza variabile in parti restituirà SQLSTATE 01004 (dati stringa, troncati a destra) e SQL_SUCCESS_WITH_INFO quando sono presenti più dati da restituire. Questo è diverso dal caso in cui un segnalibro di lunghezza variabile viene troncato da una chiamata a **SQLFetch** o **SQLFetchScroll**, che restituisce SQL_ERROR e SQLSTATE 22001 (dati String troncati a destra).  
  
 **Impossibile utilizzare SQLGetData** per restituire dati a lunghezza fissa nelle parti. Se **SQLGetData** viene chiamato più volte in una riga per una colonna contenente dati a lunghezza fissa, restituisce SQL_NO_DATA per tutte le chiamate dopo la prima.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recupero di parametri di output trasmessiRetrieving Streamed Output Parameters  
 Se un driver supporta i parametri di output trasmessi, un'applicazione può chiamare **SQLGetData** con un piccolo buffer più volte per recuperare un valore di parametro di grandi dimensioni. Per ulteriori informazioni sul parametro di output trasmesso, vedere Recupero di parametri di [output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="retrieving-data-with-sqlgetdata"></a>Recupero dei dati con SQLGetDataRetrieving Data with SQLGetData  
 Per restituire i dati per la colonna specificata, **SQLGetData** esegue la sequenza di passaggi seguente:  
  
1.  Restituisce SQL_NO_DATA se ha già restituito tutti i dati per la colonna.  
  
2.  Imposta \* *StrLen_or_IndPtr* su SQL_NULL_DATA se i dati sono NULL. Se i dati sono NULL e *StrLen_or_IndPtr* è un puntatore null, **SQLGetData** restituisce SQLSTATE 22002 (variabile indicatore richiesta ma non fornita).  
  
     Se i dati per la colonna non sono NULL, SQLGetData procede al passaggio 3.If the data for the column is not NULL, **SQLGetData** proceeds to step 3.  
  
3.  Se l'attributo dell'istruzione SQL_ATTR_MAX_LENGTH è impostato su un valore diverso da zero, se la colonna contiene dati binari o di tipo carattere e se **SQLGetData** non è stato chiamato in precedenza per la colonna, i dati vengono troncati a SQL_ATTR_MAX_LENGTH byte.  
  
    > [!NOTE]  
    >  L'attributo dell'istruzione SQL_ATTR_MAX_LENGTH ha lo scopo di ridurre il traffico di rete. In genere viene implementato dall'origine dati, che tronca i dati prima di restituirla attraverso la rete. I driver e le origini dati non sono necessari per supportarlo. Pertanto, per garantire che i dati vengano troncati a una dimensione specifica, un'applicazione deve allocare un buffer di tale dimensione e specificare la dimensione nel *BufferLength* argomento.  
  
4.  Converte i dati nel tipo specificato in *TargetType*. Ai dati vengono assegnate la precisione e la scala predefinite per quel tipo di dati. Se *TargetType* è SQL_ARD_TYPE, viene utilizzato il tipo di dati nel campo SQL_DESC_CONCISE_TYPE dell'ARD. Se *TargetType* è SQL_ARD_TYPE, ai dati viene assegnata la precisione e la scala nei campi SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION e SQL_DESC_SCALE dell'ARD, a seconda del tipo di dati nel campo SQL_DESC_CONCISE_TYPE. Se la precisione o la scala predefinita non è appropriata, l'applicazione deve impostare in modo esplicito il campo del descrittore appropriato tramite una chiamata a **SQLSetDescField** o **SQLSetDescRec**.  
  
5.  Se i dati sono stati convertiti in un tipo di dati a lunghezza variabile, ad esempio carattere o binario, **SQLGetData** controlla se la lunghezza dei dati supera *BufferLength*. Se la lunghezza dei dati di tipo carattere (incluso il carattere di terminazione null) supera *BufferLength*, **SQLGetData** tronca i dati in *BufferLength* meno la lunghezza di un carattere di terminazione null. Quindi null-termina i dati. Se la lunghezza dei dati binari supera la lunghezza del buffer di dati, **SQLGetData** tronca a *BufferLength* byte.  
  
     Se il buffer di dati fornito è troppo piccolo per contenere il carattere di terminazione null, **SQLGetData** restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01004.  
  
     **SQLGetData** non tronca mai i dati convertiti in tipi di dati a lunghezza fissa. si presuppone sempre che la lunghezza di*TargetValuePtr* è la dimensione del tipo di dati.  
  
6.  Inserisce i dati convertiti (ed eventualmente troncati) in \* *TargetValuePtr*. Si noti che **SQLGetData** non può restituire dati fuori linea.  
  
7.  Inserisce la lunghezza \*dei dati in *StrLen_or_IndPtr*. Se *StrLen_or_IndPtr* è un puntatore null, **SQLGetData** non restituisce la lunghezza.  
  
    -   Per i dati di tipo carattere o binario, si tratta della lunghezza dei dati dopo la conversione e prima del troncamento a causa di *BufferLength*. Se il driver non è in grado di determinare la lunghezza dei dati dopo la conversione, come talvolta accade con i dati long, restituisce SQL_SUCCESS_WITH_INFO e imposta la lunghezza su SQL_NO_TOTAL. L'ultima chiamata a **SQLGetData** deve sempre restituire la lunghezza dei dati, non zero o SQL_NO_TOTAL. Se i dati sono stati troncati a causa dell'attributo di istruzione SQL_ATTR_MAX_LENGTH, \*il valore di questo attributo, anziché la lunghezza effettiva, viene inserito in *StrLen_or_IndPtr*. Questo perché questo attributo è progettato per troncare i dati sul server prima della conversione, quindi il driver non ha modo di capire qual è la lunghezza effettiva. Quando **SQLGetData** viene chiamato più volte in successione per la stessa colonna, questa è la lunghezza dei dati disponibili all'inizio della chiamata corrente; vale a dire, la lunghezza diminuisce con ogni chiamata successiva.  
  
    -   Per tutti gli altri tipi di dati, questa è la lunghezza dei dati dopo la conversione; ovvero, è la dimensione del tipo in cui sono stati convertiti i dati.  
  
8.  Se i dati vengono troncati senza perdita di significato durante la conversione (ad esempio, il numero reale 1.234 viene troncato quando viene convertito nel numero intero 1) o perché *BufferLength* è troppo piccolo (ad esempio, la stringa "abcdef" viene inserita in un buffer a 4 byte), **SQLGetData** restituisce SQLSTATE 01004 (dati troncati) e SQL_SUCCESS_WITH_INFO. Se i dati vengono troncati senza perdita di significato a causa dell'attributo dell'istruzione SQL_ATTR_MAX_LENGTH, **SQLGetData** restituisce SQL_SUCCESS e non restituisce SQLSTATE 01004 (dati troncati).  
  
 Il contenuto del buffer di dati associato (se **SQLGetData** viene chiamato su una colonna associata) e il buffer di lunghezza/indicatore non sono definiti se **SQLGetData** non restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
 Le chiamate successive a **SQLGetData** recupereranno i dati dall'ultima colonna richiesta. gli offset precedenti diventano non validi. Ad esempio, quando viene eseguita la sequenza seguente:  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 la seconda chiamata a SQLGetData(icol) recupera i dati dall'inizio della colonna n. Qualsiasi offset nei dati a causa di chiamate precedenti a **SQLGetData** per la colonna non è più valido.  
  
## <a name="descriptors-and-sqlgetdata"></a>Descrittori e SQLGetData  
 **SQLGetData** non interagisce direttamente con i campi del descrittore.  
  
 Se *TargetType* è SQL_ARD_TYPE, viene utilizzato il tipo di dati nel campo SQL_DESC_CONCISE_TYPE dell'ARD. Se *TargetType* è SQL_ARD_TYPE o SQL_C_DEFAULT, ai dati viene assegnata la precisione e la scala nei campi SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION e SQL_DESC_SCALE dell'ARD, a seconda del tipo di dati nel campo SQL_DESC_CONCISE_TYPE.  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente un'applicazione esegue un'istruzione **SELECT** per restituire un set di risultati degli ID cliente, dei nomi e dei numeri di telefono ordinati per nome, ID e numero di telefono. Per ogni riga di dati, chiama **SQLFetch** per posizionare il cursore alla riga successiva. Chiama **SQLGetData** per recuperare i dati recuperati; i buffer per i dati e il numero di byte restituito vengono specificati nella chiamata a **SQLGetData**. Infine, stampa il nome, l'ID e il numero di telefono di ogni dipendente.  
  
```cpp  
#define NAME_LEN 50  
#define PHONE_LEN 50  
  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   sCustID, cbName, cbAge, cbBirthday;  
SQLRETURN    retcode;  
SQLHSTMT     hstmt;  
  
retcode = SQLExecDirect(hstmt,  
   "SELECT CUSTID, NAME, PHONE FROM CUSTOMERS ORDER BY 2, 1, 3",  
   SQL_NTS);  
  
if (retcode == SQL_SUCCESS) {  
   while (TRUE) {  
      retcode = SQLFetch(hstmt);  
      if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO) {  
         show_error();  
      }  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
         /* Get data for columns 1, 2, and 3 */  
  
         SQLGetData(hstmt, 1, SQL_C_ULONG, &sCustID, 0, &cbCustID);  
         SQLGetData(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
         SQLGetData(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN,  
            &cbPhone);  
  
         /* Print the row of data */  
  
         fprintf(out, "%-5d %-*s %*s", sCustID, NAME_LEN-1, szName,   
            PHONE_LEN-1, szPhone);  
      } else {  
         break;  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Assegnazione dell'archiviazione per una colonna in un set di risultatiAssigning storage for a column in a result set|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Esecuzione di operazioni bulk non correlate alla posizione del cursore a blocchiPerforming bulk operations that do not relate to the block cursor position|[Sqlbulkoperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Recupero di un blocco di dati o scorrimento di un set di risultati|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Recupero di una singola riga di dati o di un blocco di dati in una direzione forward-only|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Invio dei dati dei parametri in fase di esecuzioneSending parameter data at execution time|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Posizionamento del cursore, aggiornamento dei dati nel set di righe o aggiornamento o eliminazione di dati nel set di righe|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recupero di parametri di output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
