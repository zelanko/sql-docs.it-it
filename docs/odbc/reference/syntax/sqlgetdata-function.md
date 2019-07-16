---
title: Funzione SQLGetData | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f33d55cc8ac5dab37ce200a5a654bcb4be7cc9ad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911373"
---
# <a name="sqlgetdata-function"></a>Funzione SQLGetData
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLGetData** recupera dati per una singola colonna nel set di risultati o per un singolo parametro dopo **SQLParamData** restituisce SQL_PARAM_DATA_AVAILABLE. Può essere chiamato più volte per recuperare dati a lunghezza variabile in parti.  
  
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
 [Input] Handle di istruzione.  
  
 *Col_or_Param_Num*  
 [Input] Per il recupero dei dati della colonna, è il numero della colonna per cui restituire i dati. Colonne del set di risultati vengono numerate nell'ordine delle colonne a incremento a partire da 1. La colonna del segnalibro è il numero di colonna 0. Ciò può essere specificato solo se sono abilitati i segnalibri.  
  
 Per il recupero dei dati dei parametri, è il numero ordinale del parametro, che inizia da 1.  
  
 *TargetType*  
 [Input] L'identificatore del tipo del tipo di dati C del **TargetValuePtr* buffer. Per un elenco di tipi di dati C validi e gli identificatori di tipo, vedere la [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) sezione nell'appendice d: Tipi di dati.  
  
 Se *TargetType* è SQL_ARD_TYPE, il driver utilizza l'identificatore del tipo specificato nel campo SQL_DESC_CONCISE_TYPE del ARD. Se *TargetType* SQL_APD_TYPE, viene **SQLGetData** userà stesso tipo di dati C che è stato specificato in **SQLBindParameter**. In caso contrario, il tipo di dati C specificato nel **SQLGetData** esegue l'override specificato nel tipo di dati C **SQLBindParameter**. Se è SQL_C_DEFAULT, il driver consente di selezionare il tipo di dati C predefiniti in base al tipo di dati SQL di origine.  
  
 È anche possibile specificare un tipo di dati C esteso. Per altre informazioni, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Output] Puntatore al buffer in cui si desidera restituire i dati.  
  
 *TargetValuePtr* non può essere NULL.  
  
 *BufferLength*  
 [Input] Lunghezza di **TargetValuePtr* buffer in byte.  
  
 Il driver utilizza *BufferLength* per evitare di scrivere oltre la fine del \* *TargetValuePtr* buffer durante la restituzione di dati a lunghezza variabile, ad esempio carattere o dati binari. Si noti che il driver viene considerato il carattere di terminazione null quando la restituzione di dati di tipo carattere a \* *TargetValuePtr*. **TargetValuePtr* deve pertanto contenere spazio per il carattere di terminazione null, o il driver verrà troncare i dati.  
  
 Quando il driver restituisce i dati a lunghezza fissa, ad esempio un numero intero o una struttura di data, il driver ignora *BufferLength* e presuppone che il buffer sia sufficientemente grande da contenere i dati. È pertanto importante per l'applicazione allocare un buffer sufficiente per i dati a lunghezza fissa o il driver verrà scritto oltre la fine del buffer.  
  
 **SQLGetData** restituisce SQLSTATE HY090 (stringa di lunghezza o non valida del buffer) quando *BufferLength* è minore di 0 ma non quando *BufferLength* è 0.  
  
 *StrLen_or_IndPtr*  
 [Output] Puntatore al buffer in cui restituire il valore di lunghezza o all'indicatore. Se si tratta di un puntatore null, viene restituito alcun valore di lunghezza o all'indicatore. Restituisce un errore quando i dati recuperati sono NULL.  
  
 **SQLGetData** può restituire i valori seguenti nel buffer di lunghezza/indicatore:  
  
-   La lunghezza dei dati disponibili da restituire  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 Per altre informazioni, vedere [usando i valori di lunghezza/indicatore](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) e "Commenti" in questo argomento.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetData** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato può essere ottenuto chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetData** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Non tutti i dati per la colonna specificata, *Col_or_Param_Num*, è stato possibile recuperare in una singola chiamata alla funzione. SQL_NO_TOTAL o la lunghezza dei dati rimanenti nella colonna specificata prima della chiamata corrente al **SQLGetData** viene restituito nella \* *StrLen_or_IndPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).<br /><br /> Per altre informazioni sull'uso di più chiamate a **SQLGetData** per una singola colonna, vedere "Commenti".|  
|01S07|Troncamento frazionario.|I dati restituiti per una o più colonne è stati troncati. Per i tipi di dati numerici, la parte frazionaria del numero è stata troncata. Per ora, timestamp e tipi di dati di intervallo che contiene un componente della fase, la parte frazionaria del tempo sono stata troncata.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07006|Violazione dell'attributo del tipo di dati|Il valore di dati di una colonna nel set di risultati non può essere convertito nel tipo di dati C specificato dall'argomento *TargetType*.|  
|07009|Indice del descrittore non valido|Il valore specificato per l'argomento *Col_or_Param_Num* era pari a 0 e l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_OFF.<br /><br /> Il valore specificato per l'argomento *Col_or_Param_Num* era maggiore del numero di colonne nel set di risultati.<br /><br /> Il *Col_or_Param_Num* valore non è uguale al numero ordinale del parametro che è disponibile.<br /><br /> (DM) è stata associata la colonna specificata. Questa descrizione non è applicabile ai driver che restituiscono la maschera di bit SQL_GD_BOUND per l'opzione di SQL_GETDATA_EXTENSIONS **SQLGetInfo**.<br /><br /> (DM) il numero della colonna specificata è minore o uguale al numero della colonna associata più alta. Questa descrizione non è applicabile ai driver che restituiscono la maschera di bit SQL_GD_ANY_COLUMN per l'opzione di SQL_GETDATA_EXTENSIONS **SQLGetInfo**.<br /><br /> (DM) l'applicazione ha già chiamato **SQLGetData** per la riga corrente; il numero della colonna specificata nella chiamata corrente è inferiore al numero della colonna specificata nella chiamata precedente; e il driver non restituisce il SQL _ Maschera di bit GD_ANY_ORDER per l'opzione di SQL_GETDATA_EXTENSIONS **SQLGetInfo**.<br /><br /> (DM) di *TargetType* argomento era SQL_ARD_TYPE e il *Col_or_Param_Num* record del descrittore nel ARD non è riuscita la verifica della coerenza.<br /><br /> (DM) di *TargetType* argomento era SQL_ARD_TYPE e il valore del campo SQL_DESC_COUNT del ARD inferiore al limite *Col_or_Param_Num* argomento.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|22002|Variabile indicatore necessaria ma non fornito|*StrLen_or_IndPtr* era un puntatore null e i dati NULL è stati recuperati.|  
|22003|Valore numerico non compreso nell'intervallo|Restituzione del valore numerico (come valore numerico o stringa) per la colonna avrebbe causato la parte intera (in contrapposizione frazionari) del numero da troncare.<br /><br /> Per altre informazioni, vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato di datetime non valido|Colonna di tipo carattere nel set di risultati è stata associata a una data, ora o struttura di timestamp di C e il valore nella colonna è una data non valida, ora o timestamp, rispettivamente. Per altre informazioni, vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22012|Divisione per zero|È stato restituito un valore da un'espressione aritmetica che ha comportato la divisione per zero.|  
|22015|Overflow del campo Interval|Assegnazione da un numerico esatto o l'intervallo di tipo SQL a un tipo di intervallo C, ha causato una perdita di cifre significative nel campo iniziale.<br /><br /> Quando la restituzione di dati a un tipo di intervallo C, si è verificato alcun rappresentazione del valore del tipo SQL nel tipo di intervallo C.|  
|22018|Valore del carattere non valido per la specifica del cast|Una colonna di tipo carattere nel set di risultati restituita da un buffer di caratteri C e la colonna contiene un carattere che non ha alcuna rappresentazione nel set di caratteri del buffer.<br /><br /> Il tipo C è un valore numerico esatto o approssimativo, un valore datetime o un tipo di dati di intervallo; il tipo SQL della colonna è un tipo di dati carattere. e il valore nella colonna non è un valore letterale valido del tipo C associato.|  
|24000|Stato del cursore non valido|(DM) a cui è stata chiamata senza chiamare prima la funzione **SQLFetch** oppure **SQLFetchScroll** per posizionare il cursore sulla riga dei dati richiesti.<br /><br /> (DM) di *StatementHandle* era stato eseguito, ma è stato associato alcun set di risultati le *StatementHandle*.<br /><br /> Un cursore è stato aperto nel *StatementHandle* e **SQLFetch** oppure **SQLFetchScroll** fosse stata chiamata, ma è stato posizionato il cursore prima dell'inizio del set di risultati o dopo il fine del set di risultati.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel *MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY003|Tipo di programma non compreso nell'intervallo|(DM) dell'argomento *TargetType* non era un tipo di dati valido, SQL_C_DEFAULT, SQL_ARD_TYPE (in caso di recupero di dati della colonna) o SQL_APD_TYPE (in caso di recupero dei dati dei parametri).<br /><br /> (DM) dell'argomento *Col_or_Param_Num* era 0 e l'argomento *TargetType* non era SQL_C_BOOKMARK per un segnalibro a lunghezza fissa o SQL_C_VARBOOKMARK per un segnalibro a lunghezza variabile.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle*, quindi è stata chiamata la funzione anche in questo caso sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread e quindi la funzione è stata chiamata nuovamente nel *StatementHandle*.|  
|HY009|Utilizzo non valido del puntatore null|(DM) dell'argomento *TargetValuePtr* era un puntatore null.|  
|HY010|Errore nella sequenza della funzione|(DM) specificato *StatementHandle* non è stato eseguito. La funzione è stata chiamata senza chiamare prima il metodo **SQLExecDirect**, **SQLExecute** o una funzione di catalogo.<br /><br /> (DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLGetData** funzione è stata chiamata.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.<br /><br /> (DM) di *StatementHandle* era stato eseguito, ma è stato associato alcun set di risultati le *StatementHandle*.<br /><br /> Una chiamata a **SQLExeceute**, **SQLExecDirect**, o **SQLMoreResults** restituiti SQL_PARAM_DATA_AVAILABLE, ma **SQLGetData** è stato chiamato , invece di **SQLParamData**.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore specificato per l'argomento *BufferLength* era minore di 0.<br /><br /> Il valore specificato per l'argomento *BufferLength* era minore di 4, il *Col_or_Param_Num* argomento è stato impostato su 0 e il driver è stato un ODBC 2*x* driver.|  
|HY109|Posizione del cursore non valido|È stato posizionato il cursore (da **SQLSetPos**, **SQLFetch**, **SQLFetchScroll**, oppure **SQLBulkOperations**) su una riga che è stata eliminata o non è stato possibile recuperare.<br /><br /> Il cursore era un cursore forward-only e le dimensioni del set di righe maggiore di uno.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|L'origine dati o driver non supporta l'utilizzo della **SQLGetData** con più righe in **SQLFetchScroll**. Questa descrizione non è applicabile ai driver che restituiscono la maschera di bit SQL_GD_BLOCK per l'opzione di SQL_GETDATA_EXTENSIONS **SQLGetInfo**.<br /><br /> L'origine dati o driver non supporta la conversione specificata dalla combinazione dei *TargetType* argomento e il tipo di dati SQL della colonna corrispondente. Questo errore si applica solo quando il tipo di dati SQL della colonna è stato eseguito il mapping a un tipo di dati specifici del driver SQL.<br /><br /> Il driver supporta solo l'API ODBC 2 *. x*e l'argomento *TargetType* era una delle operazioni seguenti:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> uno dei tipi di dati di intervallo C sono elencati nella [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) nell'appendice d: Tipi di dati.<br /><br /> Il driver supporta solo le versioni ODBC precedenti alla versione 3.50 e l'argomento *TargetType* era SQL_C_GUID.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|(DM) il driver corrispondente per il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **SQLGetData** restituisce i dati in una colonna specificata. **SQLGetData** può essere chiamato solo dopo che uno o più righe recuperate dal set di risultati tramite **SQLFetch**, **SQLFetchScroll**, oppure **SQLExtendedFetch**. Se i dati a lunghezza variabile sono troppo grandi per essere restituito in una singola chiamata a **SQLGetData** (a causa di una limitazione nell'applicazione), **SQLGetData** possibile recuperarla in parti. È possibile associare alcune colonne in una riga e chiamare **SQLGetData** per altri utenti, anche se si tratta di soggetti ad alcune restrizioni. Per altre informazioni, vedere [recupero di dati Long](../../../odbc/reference/develop-app/getting-long-data.md).  
  
 Per informazioni sull'uso **SQLGetData** con i parametri di output inviati come flusso, vedere [il recupero di parametri di Output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-sqlgetdata"></a>Mediante SQLGetData  
 Se il driver non supporta le estensioni per **SQLGetData**, la funzione può restituire solo i dati per le colonne non associate con un numero maggiore di quello dell'ultima colonna associata. Inoltre, all'interno di una riga di dati, il valore della *Col_or_Param_Num* argomento in ogni chiamata a **SQLGetData** deve essere maggiore o uguale al valore di *Col_or_Param_Num*nella chiamata precedente; vale a dire i dati devono essere recuperati in base al numero di colonna crescente. Infine, se è supportata alcuna estensione, **SQLGetData** non può essere chiamato se la dimensione del set di righe è maggiore di 1.  
  
 I driver possono ridurre una di queste restrizioni. Per determinare quali restrizioni rilassa un driver, un'applicazione chiama **SQLGetInfo** con una qualsiasi delle opzioni SQL_GETDATA_EXTENSIONS seguenti:  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** può essere chiamata per restituire i valori dei parametri output. Per altre informazioni, vedere [recupero di parametri di Output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_GD_ANY_COLUMN. Se questa opzione viene restituita, **SQLGetData** può essere chiamato per tutte le colonne non associata, inclusi quelli prima che l'ultima colonna associata.  
  
-   SQL_GD_ANY_ORDER. Se questa opzione viene restituita, **SQLGetData** possono essere chiamati per colonne non associate in qualsiasi ordine.  
  
-   SQL_GD_BLOCK. Se questa opzione viene restituita dalla **SQLGetInfo** per il InfoType SQL_GETDATA_EXTENSIONS, il driver supporta le chiamate a **SQLGetData** quando le dimensioni del set di righe sono maggiore di 1 e l'applicazione può chiamare **SQLSetPos** con l'opzione SQL_POSITION per posizionare il cursore nella riga corretta prima di chiamare **SQLGetData.**  
  
-   SQL_GD_BOUND. Se questa opzione viene restituita, **SQLGetData** può essere chiamato per le colonne associate, oltre alle colonne non associate.  
  
 Esistono due eccezioni a queste restrizioni e capacità del driver a essi. Prima di tutto **SQLGetData** non dovrebbe mai essere chiamato per un cursore forward-only, quando la dimensione del set di righe è maggiore di 1. In secondo luogo, se un driver supporta segnalibri, deve sempre supportare la possibilità di chiamare **SQLGetData** per la colonna 0, anche se non consente alle applicazioni di chiamare **SQLGetData** per le altre colonne prima degli ultimi colonna associata. (Quando un'applicazione funziona con un 2 ODBC *. x* driver **SQLGetData** restituirà correttamente un segnalibro quando viene chiamato con *Col_or_Param_Num* uguale a 0 dopo una chiamata a **SQLFetch**, in quanto **SQLFetch** viene eseguito il mapping da ODBC 3*x* gestione Driver per **SQLExtendedFetch** con un  *FetchOrientation* di SQL_FETCH_NEXT, e **SQLGetData** con un *Col_or_Param_Num* pari a 0 viene eseguito il mapping da ODBC 3*x* gestione Driver per **SQLGetStmtOption** con un *fOption* di SQL_GET_BOOKMARK.)  
  
 **SQLGetData** non può essere usato per recuperare il segnalibro per una riga appena inserita chiamando **SQLBulkOperations** con l'opzione SQL_ADD, perché il cursore non è posizionato sulla riga. Un'applicazione può recuperare il segnalibro per tale riga, associare la colonna 0 prima di chiamare **SQLBulkOperations** con SQL_ADD, nel qual caso **SQLBulkOperations** restituisce il segnalibro nel buffer associato. **SQLFetchScroll** può quindi essere chiamato con SQL_FETCH_BOOKMARK per riposizionare il cursore sulla riga.  
  
 Se il *TargetType* argomento è un tipo di dati di intervallo, la precisione iniziale intervallo predefinito (2) e la precisione dei secondi di intervallo predefinito (6), come set nei campi SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION di ARD, rispettivamente, vengono usati per i dati. Se il *TargetType* argomento è un tipo di dati SQL_C_NUMERIC, la precisione predefinita (definiti dal driver) e predefinito di scalabilità (0), come impostato nei campi SQL_DESC_PRECISION e SQL_DESC_SCALE del ARD, vengono usato per i dati. Se qualsiasi precisione predefinita o la scala non è appropriata, l'applicazione deve impostare in modo esplicito il campo di descrizione appropriato da una chiamata a **SQLSetDescField** oppure **SQLSetDescRec**. È possibile impostare il campo SQL_DESC_CONCISE_TYPE SQL_C_NUMERIC e chiamare **SQLGetData** con un *TargetType* argomento di SQL_ARD_TYPE, che determina i valori di precisione e scala in campi di descrizione da utilizzare.  
  
> [!NOTE]
>  In ODBC 2 *. x*, le applicazioni impostano *TargetType* SQL_C_DATE, SQL_C_TIME o SQL_C_TIMESTAMP per indicare che \* *TargetValuePtr* è una data, ora, o struttura di timestamp. In ODBC 3 *. x*, le applicazioni impostano *TargetType* SQL_C_TYPE_DATE, SQL_C_TYPE_TIME o SQL_C_TYPE_TIMESTAMP. Gestione Driver rende mapping appropriati se necessario, a seconda della versione dell'applicazione e il driver.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>Recupero di dati a lunghezza variabile in parti  
 **SQLGetData** può essere utilizzato per recuperare i dati da una colonna che contiene dati a lunghezza variabile in parti, vale a dire, se l'identificatore del tipo di dati SQL della colonna è SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL _ WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY o un identificatore specifico del driver per un tipo a lunghezza variabile.  
  
 Per recuperare dati da una colonna in parti, l'applicazione chiama **SQLGetData** più volte in successione per la stessa colonna. Per ogni chiamata **SQLGetData** restituisce la parte successiva dei dati. È compito dell'applicazione per riunire le parti, prestando attenzione a rimuovere il carattere di terminazione null da parti intermediate di dati di tipo carattere. Se sono presenti più dati da restituire o non è stato allocato buffer insufficiente per il carattere di terminazione **SQLGetData** restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dati troncati). Quando l'ultima parte dei dati, restituisce **SQLGetData** restituisce SQL_SUCCESS. SQL_NO_TOTAL né zero può essere restituito nell'ultima chiamata valida per recuperare dati da una colonna, perché l'applicazione non avrà quindi alcun modo sapere quanta parte dei dati nel buffer dell'applicazione è valido. Se **SQLGetData** viene chiamato al termine, viene restituito SQL_NO_DATA. Per altre informazioni, vedere la sezione successiva, "Recupero dati con SQLGetData".  
  
 Segnalibri di lunghezza variabile possono essere restituiti in parti dal **SQLGetData**. Come con altri dati, una chiamata a **SQLGetData** da restituire a lunghezza variabile segnalibri nelle parti restituirà SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dati String, troncati a destra) quando sono presenti più dati da restituire. Ciò si differenzia il caso quando un segnalibro a lunghezza variabile verrà troncato mediante una chiamata a **SQLFetch** oppure **SQLFetchScroll**, che restituisce SQL_ERROR e SQLSTATE 22001 (dati String, troncati a destra).  
  
 **SQLGetData** non può essere utilizzata per restituire dati a lunghezza fissa in parti. Se **SQLGetData** viene chiamato più volte in una riga per una colonna contenente i dati a lunghezza fissa, viene restituito SQL_NO_DATA per tutte le chiamate dopo la prima.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recupero di parametri di Output inviati come flusso  
 Se un driver supporta i parametri di output inviati come flusso, un'applicazione può chiamare **SQLGetData** con un piccolo numero di volte per recuperare un valore di parametro di grandi dimensioni del buffer. Per altre informazioni sul parametro di flusso di output, vedere [recupero di parametri di Output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="retrieving-data-with-sqlgetdata"></a>Recupero dei dati con SQLGetData  
 Per restituire i dati per la colonna specificata, **SQLGetData** esegue la sequenza di passaggi seguente:  
  
1.  Se ha già restituito tutti i dati per la colonna non restituisce SQL_NO_DATA.  
  
2.  Set \* *StrLen_or_IndPtr* su SQL_NULL_DATA se i dati sono NULL. Se i dati sono NULL e *StrLen_or_IndPtr* era un puntatore null, **SQLGetData** restituisce SQLSTATE 22002 (variabile indicatore necessaria ma non specificato).  
  
     Se i dati per la colonna non NULL, **SQLGetData** procede al passaggio 3.  
  
3.  Se l'attributo di istruzione SQL_ATTR_MAX_LENGTH è impostato su un valore diverso da zero, se la colonna contiene dati carattere o binario e se **SQLGetData** non è stato precedentemente chiamato per la colonna, i dati vengono troncati su SQL_ATTR_MAX_LENGTH byte.  
  
    > [!NOTE]  
    >  L'attributo di istruzione SQL_ATTR_MAX_LENGTH è progettato per ridurre il traffico di rete. Viene in genere implementato dall'origine dati, che tronca i dati prima di restituirlo attraverso la rete. I driver e origini dati non sono necessari per supportarla. Pertanto, per garantire che i dati vengono troncati per una determinata dimensione, un'applicazione deve allocare un buffer della dimensione e specificare le dimensioni nei *BufferLength* argomento.  
  
4.  Converte i dati nel tipo specificato nel *TargetType*. I dati viene forniti la precisione predefinita e la scala per quel tipo di dati. Se *TargetType* è SQL_ARD_TYPE, i dati di tipo nel campo SQL_DESC_CONCISE_TYPE del ARD viene utilizzato. Se *TargetType* è SQL_ARD_TYPE, i dati ha precisione e scala nel SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION, e digitare il SQL_DESC_CONCISE campi SQL_DESC_SCALE di ARD, a seconda dei dati Campo tipo. Se qualsiasi precisione predefinita o la scala non è appropriata, l'applicazione deve impostare in modo esplicito il campo di descrizione appropriato da una chiamata a **SQLSetDescField** oppure **SQLSetDescRec**.  
  
5.  Se i dati è stati convertiti in un tipo di dati a lunghezza variabile, ad esempio carattere o binario **SQLGetData** controlla se la lunghezza dei dati supera *BufferLength*. Se la lunghezza dei dati di tipo carattere (incluso il carattere di terminazione null) supera *BufferLength*, **SQLGetData** tronca i dati da *BufferLength* minore della lunghezza di un carattere di terminazione null. Quindi null fa terminare con i dati. Se la lunghezza dei dati binari supera la lunghezza del buffer di dati, **SQLGetData** lo tronca a *BufferLength* byte.  
  
     Se il buffer di dati fornito è troppo piccolo per contenere il carattere di terminazione null, **SQLGetData** restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01004.  
  
     **SQLGetData** mai tronca i dati convertiti in dati a lunghezza fissa tipi; è sempre presupposto che la lunghezza di **TargetValuePtr* è la dimensione del tipo di dati.  
  
6.  Inserisce i dati convertiti (e possibilmente troncati) nella \* *TargetValuePtr*. Si noti che **SQLGetData** non possono restituire dati da una riga.  
  
7.  La lunghezza dei dati in posizioni \* *StrLen_or_IndPtr*. Se *StrLen_or_IndPtr* era un puntatore null, **SQLGetData** non restituisce la lunghezza.  
  
    -   Per dati carattere o binario, questa è la lunghezza dei dati dopo la conversione e prima del troncamento a causa dell'errore *BufferLength*. Se il driver non è possibile determinare la lunghezza dei dati dopo la conversione, come avviene, a volte con dati di tipo long, viene restituito SQL_SUCCESS_WITH_INFO e imposta la lunghezza su SQL_NO_TOTAL. (L'ultima chiamata a **SQLGetData** devono restituire sempre la lunghezza dei dati, non da zero o SQL_NO_TOTAL.) Se i dati sono stati troncati a causa di un attributo di istruzione SQL_ATTR_MAX_LENGTH, il valore di questo attributo - anziché la lunghezza effettiva - viene inserito \* *StrLen_or_IndPtr*. Questo avviene perché questo attributo è progettato per troncare i dati nel server prima della conversione, in modo che il driver non è in grado di capire quali la lunghezza effettiva è. Quando **SQLGetData** viene chiamato più volte in successione per la stessa colonna, si tratta della lunghezza dei dati disponibile all'inizio della chiamata corrente; ovvero, la lunghezza diminuisce con ogni chiamata successiva.  
  
    -   Per tutti gli altri tipi di dati, si tratta della lunghezza dei dati dopo la conversione. vale a dire, è la dimensione del tipo a cui è stati convertiti i dati.  
  
8.  Se i dati vengono troncati durante la conversione senza perdita di significato (ad esempio, il numero reale 1,234 viene troncato quando convertito all'intero 1) o perché *BufferLength* è troppo piccolo (ad esempio, la stringa "abcdef" viene inserita in un buffer a 4 byte), **SQLGetData** restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dati troncati). Se i dati vengono troncati senza perdita di significato a causa dell'attributo di istruzione, SQL_ATTR_MAX_LENGTH **SQLGetData** restituisce SQL_SUCCESS e non restituisce SQLSTATE 01004 (dati troncati).  
  
 Il contenuto del buffer di dati associati (se **SQLGetData** viene chiamato su una colonna associata) e il buffer di lunghezza/indicatore sono indefiniti se **SQLGetData** non restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
 Le chiamate successive a **SQLGetData** recupererà i dati dall'ultima colonna richiesto; offset precedenti diventano non validi. Ad esempio, quando viene eseguita la sequenza seguente:  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 la seconda chiamata a SQLGetData(icol=n) recupera i dati dall'inizio della colonna n. Un offset nei dati causati da chiamate precedenti a **SQLGetData** per la colonna non è più valida.  
  
## <a name="descriptors-and-sqlgetdata"></a>Descrittori e SQLGetData  
 **SQLGetData** non interagisce direttamente con tutti i campi del descrittore.  
  
 Se *TargetType* è SQL_ARD_TYPE, i dati di tipo nel campo SQL_DESC_CONCISE_TYPE del ARD viene utilizzato. Se *TargetType* è SQL_ARD_TYPE o SQL_C_DEFAULT, i dati ha precisione e scala nel SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION, e digitare i campi SQL_DESC_SCALE di ARD, a seconda dei dati nel campo SQL_DESC_CONCISE_TYPE.  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, un'applicazione esegue una **seleziona** istruzione per restituire un set di risultati del cliente ID, nomi e i numeri ordinati per nome, ID e il numero di telefono del cellulare. Per ogni riga di dati, viene chiamato **SQLFetch** per posizionare il cursore alla riga successiva. Viene chiamato **SQLGetData** per recuperare i dati recuperati; i buffer per i dati e il numero di byte restituito vengono specificati nella chiamata a **SQLGetData**. Infine, viene stampato nome, ID e il numero di telefono di ogni dipendente.  
  
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
|Assegnazione di archiviazione per una colonna in un set di risultati|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Esecuzione di operazioni bulk che non riguardano la posizione del cursore di blocco|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Annullare l'elaborazione di istruzione|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Esecuzione di un'istruzione SQL|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Eseguire un'istruzione SQL preparata|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Imposta il recupero di un blocco di dati o lo scorrimento di un risultato|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Il recupero di una singola riga di dati o un blocco di dati in una direzione di tipo forward-only|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|L'invio dei dati di parametro in fase di esecuzione|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Posizionando il cursore, l'aggiornamento dei dati del set di righe o l'aggiornamento o eliminazione dei dati nel set di righe|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recupero di parametri di output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
