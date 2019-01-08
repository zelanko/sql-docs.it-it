---
title: Funzione SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e769949c8c57bbec56055c58c9002494fc6d37be
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211990"
---
# <a name="sqlsetpos-function"></a>Funzione SQLSetPos
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLSetPos** imposta la posizione del cursore in un set di righe e consente a un'applicazione per aggiornare i dati nel set di righe o aggiornare o eliminare dati nel set di risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *RowNumber*  
 [Input] Posizione della riga nel set di righe su cui eseguire l'operazione specificata con il *operazione* argomento. Se *RowNumber* è 0, l'operazione viene applicata a ogni riga nel set di righe.  
  
 Per altre informazioni, vedere "Commenti".  
  
 *Operazione*  
 [Input] Operazione da eseguire:  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  Il valore SQL_ADD per il *operazione* argomento è stato deprecato per ODBC 3*x*. ODBC 3. *x* i driver necessari per supportare SQL_ADD per garantire la compatibilità con le versioni precedenti. Questa funzionalità è stata sostituita da una chiamata a **SQLBulkOperations** con un *operazione* di SQL_ADD. Quando un'applicazione ODBC 3. *x* applicazione funziona con un'API ODBC 2. *x* driver, Driver Manager esegue il mapping di una chiamata a **SQLBulkOperations** con un *operazione* di SQL_ADD a **SQLSetPos** con un  *Operazione* di SQL_ADD.  
  
 Per altre informazioni, vedere "Commenti".  
  
 *LockType*  
 [Input] Specifica la modalità di bloccare la riga dopo l'operazione specificata nella *operazione* argomento.  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 Per altre informazioni, vedere "Commenti".  
  
 **Restituisce**  
  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSetPos** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLSetPos** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
 Per tutti questi SQLSTATEs che può restituire SQL_SUCCESS_WITH_INFO o SQL_ERROR (eccetto SQLSTATEs 01xxx), viene restituito SQL_SUCCESS_WITH_INFO se si verifica un errore in uno o più, ma non tutte, le righe di un'operazione con più righe e viene restituito SQL_ERROR se si verifica un errore in un riga singola operazione.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01001|Conflitto dell'operazione del cursore|Il *operazione* argomento era SQL_DELETE o SQL_UPDATE e più righe oppure nessuna riga sono stati eliminati o aggiornati. (Per altre informazioni sugli aggiornamenti per più di una riga, vedere la descrizione del SQL_ATTR_SIMULATE_CURSOR *attributo* nelle **SQLSetStmtAttr**.) (Funzione restituisce SQL_SUCCESS_WITH_INFO).<br /><br /> Il *operazione* argomento era SQL_DELETE o SQL_UPDATE e l'operazione non riuscita a causa della concorrenza ottimistica. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Troncamento a destra dei dati stringa|Il *operazione* argomento era SQL_REFRESH e stringa o dati binari restituiti per una o più colonne con un tipo di dati SQL_C_CHAR o SQL_C_BINARY ha comportato il troncamento del carattere non vuote o dati binari non NULL.|  
|01S01|Errore nella riga|Il *RowNumber* argomento era 0, e si è verificato un errore in una o più righe durante l'operazione specificata con il *operazione* argomento.<br /><br /> (SQL_SUCCESS_WITH_INFO viene restituita se si verifica un errore in uno o più, ma non tutte, le righe di un'operazione con più righe e viene restituito SQL_ERROR se si verifica un errore in un'operazione singola riga).<br /><br /> (Questo valore SQLSTATE restituito solo quando **SQLSetPos** viene chiamato dopo **SQLExtendedFetch**, se il driver è un'API ODBC 2. *x* driver e la libreria di cursori non viene utilizzato.)|  
|01S07|Troncamento frazionario.|Il *operazione* argomento era SQL_REFRESH, il tipo di dati del buffer dell'applicazione non era SQL_C_CHAR o SQL_C_BINARY e i dati restituiti al buffer dell'applicazione per una o più colonne è stati troncati. Per i tipi di dati numerici, la parte frazionaria del numero è stata troncata. Per ora, timestamp e tipi di dati di intervallo che contiene un componente della fase, la parte frazionaria del tempo sono stata troncata.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07006|Violazione dell'attributo del tipo di dati|Non è possibile convertire il valore di dati di una colonna nel set di risultati per il tipo di dati specificato dallo *TargetType* nella chiamata a **SQLBindCol**.|  
|07009|Indice del descrittore non valido|L'argomento *operazione* era SQL_REFRESH o SQL_UPDATE e una colonna è stata associata con un numero di colonne maggiore del numero di colonne nel set di risultati.|  
|21S02|Livello di tabella derivata corrisponde a elenco di colonne|L'argomento *operazione* era SQL_UPDATE e sono stati alcuna colonna aggiornabile perché tutte le colonne erano sia non associata di sola lettura, o il valore nel buffer di lunghezza/indicatore associato era SQL_COLUMN_IGNORE.|  
|22001|Dati di tipo stringa, troncamento a destra|Il *operazione* argomento era SQL_UPDATE e l'assegnazione di un carattere o un valore binario a una colonna ha comportato il troncamento di valore non blank (per i caratteri) o caratteri diverso da null (per i dati binari) o byte.|  
|22003|Valore numerico non compreso nell'intervallo|L'argomento *operazione* era SQL_UPDATE e l'assegnazione di un valore numerico a una colonna nel set di risultati ha causato la parte intera (in contrapposizione frazionari) del numero da troncare.<br /><br /> L'argomento *operazione* era SQL_REFRESH e restituendo il valore numerico per uno o più colonne associate avrebbe causato una perdita di cifre significative.|  
|22007|Formato di datetime non valido|L'argomento *operazione* era SQL_UPDATE e l'assegnazione di un valore date o timestamp a una colonna nel set di risultati ha causato l'anno, mese o campo giorno sia compreso nell'intervallo.<br /><br /> L'argomento *operazione* era SQL_REFRESH e restituzione del valore date o timestamp per una o più colonne associate avrebbe causato l'anno, mese o campo giorno sia compreso nell'intervallo.|  
|22008|Overflow del campo Data/ora|Il *operazione* argomento era SQL_UPDATE e le prestazioni di data/ora aritmetica sui dati inviati a una colonna nel set di risultati ha comportato un campo datetime (anno, mese, giorno, ora, minuto o secondo campo) dei risultati all'esterno nell'intervallo consentito di valori per il campo o non valide in base alle regole di naturale del calendario gregoriano per valori DateTime.<br /><br /> Il *operazione* argomento era SQL_REFRESH e le prestazioni di data/ora aritmetica sui dati recuperati dal set di risultati ha comportato un campo datetime (anno, mese, giorno, ora, minuto o secondo campo) dei risultati all'esterno nell'intervallo consentito di valori per il campo o non valide in base alle regole di naturale del calendario gregoriano per valori DateTime.|  
|22015|Overflow del campo Interval|Il *operazione* argomento era SQL_UPDATE e l'assegnazione di un valore numerico esatto o il tipo di intervallo C per un intervallo di tipo di dati SQL ha causato una perdita di cifre significative.<br /><br /> Il *operazione* argomento era SQL_UPDATE; quando si assegna a un intervallo di tipo SQL, si è verificato alcuna rappresentazione del valore di tipo C in un intervallo di tipo SQL.<br /><br /> Il *operazione* argomento era SQL_REFRESH e assegnazione da un numerico esatto o l'intervallo di tipo SQL a un tipo di intervallo C ha causato una perdita di cifre significative nel campo iniziale.<br /><br /> Il *operazione* argomento era SQL _ Aggiorna, quando si assegna a un tipo di intervallo C, non era alcuna rappresentazione del valore del tipo SQL nel tipo di intervallo C.|  
|22018|Valore del carattere non valido per la specifica del cast|Il *operazione* argomento era SQL_REFRESH; il tipo C è un valore numerico esatto o approssimativo, un valore datetime o un tipo di dati di intervallo; il tipo SQL della colonna è un tipo di dati carattere; e il valore nella colonna non è un valore letterale valido di tipo C associato.<br /><br /> L'argomento *operazione* era SQL_UPDATE; il tipo SQL è un valore numerico esatto o approssimativo, un valore datetime o un tipo di dati di intervallo; il tipo C è stata SQL_C_CHAR; e il valore nella colonna non è un valore letterale valido del tipo SQL associato.|  
|23000|Violazione di vincolo di integrità|L'argomento *operazione* era SQL_DELETE o SQL_UPDATE ed è stato violato un vincolo di integrità.|  
|24000|Stato del cursore non valido|Il *StatementHandle* era stato eseguito, ma è stato associato alcun set di risultati le *StatementHandle*.<br /><br /> (DM) un cursore è stato aperto nel *StatementHandle*, ma **SQLFetch** oppure **SQLFetchScroll** non fosse stata chiamata.<br /><br /> Un cursore è stato aperto nel *StatementHandle*, e **SQLFetch** oppure **SQLFetchScroll** fosse stata chiamata, ma è stato posizionato il cursore prima dell'inizio del set di risultati o dopo fine del set di risultati.<br /><br /> L'argomento *operazione* era SQL_DELETE, SQL_REFRESH o SQL_UPDATE e il cursore era posizionato prima dell'inizio del set di risultati o dopo la fine del set di risultati.|  
|40001|Errore di serializzazione.|Il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|42000|La sintassi o violazione di accesso|Il driver è stato in grado di bloccare la riga in base alle necessità per eseguire l'operazione richiesta nell'argomento *operazione*.<br /><br /> Il driver è stato in grado di bloccare la riga come richiesto nell'argomento *LockType*.|  
|44000|Violazione della clausola WITH CHECK OPTION|Il *operazione* argomento era SQL_UPDATE e l'aggiornamento è stato eseguito in una tabella visualizzata o una tabella derivata della tabella visualizzata che è stato creato specificando **WITH CHECK OPTION**, in modo che una o più righe interessati dall'aggiornamento non sarà presente nella tabella visualizzata.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle*, quindi è stata chiamata la funzione anche in questo caso sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione SQLSetPos.<br /><br /> (DM) specificato *StatementHandle* non è stato eseguito. La funzione è stata chiamata senza chiamare prima il metodo **SQLExecDirect**, **SQLExecute**, o una funzione di catalogo.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.<br /><br /> (DM) il driver è stato un ODBC 2. *x* driver, e **SQLSetPos** è stato chiamato per un *StatementHandle* dopo **SQLFetch** è stato chiamato.|  
|HY011|Impossibile impostare l'attributo adesso|(DM) il driver è stato un ODBC 2. *x* driver; i SQL_ATTR_ROW_STATUS_PTR attributo dell'istruzione è stata impostata; quindi **SQLSetPos** è stato chiamato prima **SQLFetch**, **SQLFetchScroll**, oppure **SQLExtendedFetch** è stato chiamato.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|Il *operazione* argomento era SQL_UPDATE, un valore di dati non è un puntatore null e il valore di lunghezza di colonna non è 0, SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NULL_DATA, o minore o uguale a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Il *operazione* argomento era SQL_UPDATE; un valore di dati non era un puntatore null; è stato il tipo di dati C SQL_C_BINARY o SQL_C_CHAR; e il valore di lunghezza della colonna era minore di 0 ma non uguali a SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE , SQL_NTS o SQL_NULL_DATA, o minore o uguale a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Il valore in un buffer di lunghezza/indicatore stato SQL_DATA_AT_EXEC; il tipo SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo di dati specifici dell'origine dati di tipo long; e il tipo di informazioni SQL_NEED_LONG_DATA_LEN presente **SQLGetInfo** è "Y".|  
|HY092|Identificatore di attributo non valido|(DM) il valore specificato per il *operazione* argomento non è valido.<br /><br /> (DM) il valore specificato per il *LockType* argomento non è valido.<br /><br /> Il *operazione* argomento era SQL_UPDATE o SQL_DELETE e l'attributo di istruzione SQL_ATTR_CONCURRENCY SQL_ATTR_CONCUR_READ_ONLY.|  
|HY107|Valore di riga non compreso nell'intervallo|Il valore specificato per l'argomento *RowNumber* era maggiore del numero di righe nel set di righe.|  
|HY109|Posizione del cursore non valido|Il cursore associato con il *StatementHandle* è stata definita come forward-only, in modo che il cursore non può essere posizionato all'interno del set di righe. Vedere la descrizione per l'attributo SQL_ATTR_CURSOR_TYPE **SQLSetStmtAttr**.<br /><br /> Il *operazione* argomento era SQL_UPDATE, SQL_DELETE o SQL_REFRESH e la riga identificata dalle *RowNumber* argomento è stato eliminato o non era stata recuperata.<br /><br /> (DM) di *RowNumber* argomento era 0 e il *operazione* argomento era SQL_POSITION.<br /><br /> **SQLSetPos** è stato chiamato dopo **SQLBulkOperations** è stato chiamato e prima **SQLFetchScroll** oppure **SQLFetch** è stato chiamato.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|L'origine dati o driver non supporta l'operazione richiesta nel *operazione* argomento o il *LockType* argomento.|  
|HYT00|Timeout|Il periodo di timeout query scaduto prima che l'origine dati ha restituito il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr** con un *attributo* di SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
  
> [!CAUTION]
>  Per informazioni sull'istruzione dichiara che **SQLSetPos** possono essere chiamati in e che cosa deve fare per garantire la compatibilità con l'API ODBC 2 *. x* applicazioni, vedere [cursori rettangolari, cursori scorrevoli, e Compatibilità con le versioni precedenti](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md).  
  
## <a name="rownumber-argument"></a>Argomento RowNumber  
 Il *RowNumber* argomento specifica il numero della riga nel set di righe su cui eseguire l'operazione specificata per il *operazione* argomento. Se *RowNumber* è 0, l'operazione viene applicata a ogni riga nel set di righe. *RowNumber* deve essere un valore compreso tra 0 e il numero di righe nel set di righe.  
  
> [!NOTE]  
>  Nel linguaggio C, le matrici sono basate su 0 e il *RowNumber* argomento è basato su 1. Ad esempio, per aggiornare la quinta riga del set di righe, un'applicazione modifica i set di righe i buffer in corrispondenza dell'indice di matrice 4 ma specifica un *RowNumber* pari a 5.  
  
 Tutte le operazioni di posizionare il cursore sulla riga specificata da *RowNumber*. Le operazioni seguenti richiedono una posizione del cursore:  
  
-   Aggiornamento posizionato ed eliminare le istruzioni.  
  
-   Le chiamate a **SQLGetData**.  
  
-   Le chiamate a **SQLSetPos** con le opzioni SQL_DELETE e SQL_REFRESH SQL_UPDATE.  
  
 Ad esempio, se *RowNumber* è 2 per una chiamata a **SQLSetPos** con un *operazione* di SQL_DELETE, il cursore viene posizionato nella seconda riga del set di righe e tale riga viene eliminata. La voce nell'implementazione riga stato matrice (a cui fa riferimento l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR) per la seconda riga viene modificata per SQL_ROW_DELETED.  
  
 Un'applicazione può specificare una posizione del cursore quando si chiama **SQLSetPos**. In genere, viene chiamato **SQLSetPos** con l'operazione SQL_POSITION o SQL_REFRESH per posizionare il cursore prima dell'esecuzione di un oggetto posizionato l'aggiornamento o istruzione delete o chiamando **SQLGetData**.  
  
## <a name="operation-argument"></a>Argomento dell'operazione  
 Il *operazione* argomento supporta le operazioni seguenti. Per determinare quali opzioni sono supportate da un'origine dati, un'applicazione chiama **SQLGetInfo** con SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 oppure SQL_STATIC_ Tipo di informazioni CURSOR_ATTRIBUTES1 (a seconda del tipo di cursore).  
  
|*Operazione*<br /><br /> argomento|Operazione|  
|------------------------------|---------------|  
|SQL_POSITION|Il driver posiziona il cursore sulla riga specificata da *RowNumber*.<br /><br /> Il contenuto della matrice di stato di riga a cui punta l'attributo di istruzione SQL_ATTR_ROW_OPERATION_PTR viene ignorato per il SQL_POSITION *operazione*.|  
|SQL_REFRESH|Il driver posiziona il cursore sulla riga specificata da *RowNumber* e aggiorna i dati nei buffer di set di righe per tale riga. Per altre informazioni sul modo in cui il driver restituisce i dati nei buffer di set di righe, vedere le descrizioni di associazione per riga e colonna **SQLBindCol**.<br /><br /> **SQLSetPos** con un *operazione* di SQL_REFRESH Aggiorna lo stato e il contenuto delle righe nel set di righe recuperate corrente. Ciò include l'aggiornamento i segnalibri. Poiché i dati nei buffer vengano aggiornati ma non refetched, l'appartenenza del set di righe è stato risolto. Questo comportamento è diverso dall'aggiornamento eseguita da una chiamata a **SQLFetchScroll** con un *FetchOrientation* di SQL_FETCH_RELATIVE e un *RowNumber* uguale a 0, che recupera nuovamente il set di righe dal risultato impostato in modo che possa visualizzare i dati aggiunti e rimuovere i dati eliminati se tali operazioni sono supportate dal driver e il cursore.<br /><br /> Un aggiornamento con esito positivo **SQLSetPos** non modificherà lo stato riga SQL_ROW_DELETED. Le righe eliminate nel set di righe continueranno a essere contrassegnato come eliminato finché il successivo recupero. Le righe verranno scomparire nel successivo recupero, se il cursore supporta la compressione (in cui una successiva **SQLFetch** oppure **SQLFetchScroll** non restituisce le righe eliminate).<br /><br /> Aggiungere le righe non vengono visualizzati quando un aggiornamento con **SQLSetPos** viene eseguita. Questo comportamento è diverso da **SQLFetchScroll** con un *FetchType* di SQL_FETCH_RELATIVE e un *RowNumber* uguale a 0, che consente inoltre di aggiornare il set di righe corrente ma Mostra i record aggiunti o comprimere i record eliminati se queste operazioni sono supportate dal cursore.<br /><br /> Un aggiornamento con esito positivo **SQLSetPos** modificherà lo stato riga SQL_ROW_ADDED a SQL_ROW_SUCCESS (se è presente la matrice di stato di riga).<br /><br /> Un aggiornamento con esito positivo **SQLSetPos** modificherà lo stato riga SQL_ROW_UPDATED al nuovo stato della riga (se è presente la matrice di stato di riga).<br /><br /> Se si verifica un errore un **SQLSetPos** operazione su una riga, lo stato di riga è impostato su SQL_ROW_ERROR (se è presente la matrice di stato di riga).<br /><br /> Per un cursore aperto con un attributo di istruzione SQL_ATTR_CONCURRENCY di SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, un aggiornamento con **SQLSetPos** potrebbe aggiornare i valori di concorrenza ottimistica utilizzati dall'origine dati per rilevare che il riga è stata modificata. In questo caso, le versioni delle righe o valori utilizzati per garantire concorrenza dei cursori vengono aggiornati ogni volta che i buffer di righe vengono aggiornati dal server. Ciò si verifica per ogni riga che viene aggiornato.<br /><br /> Il contenuto della matrice di stato di riga a cui punta l'attributo di istruzione SQL_ATTR_ROW_OPERATION_PTR viene ignorato per il SQL_REFRESH *operazione*.|  
|SQL_UPDATE|Il driver posiziona il cursore sulla riga specificata da *RowNumber* e aggiorni la riga sottostante dei dati con i valori nei buffer di set di righe (la *TargetValuePtr* argomento in  **SQLBindCol**). Recupera le lunghezze dei dati dai buffer di lunghezza/indicatore (il *StrLen_or_IndPtr* nell'argomento **SQLBindCol**). Se la lunghezza di qualsiasi colonna è SQL_COLUMN_IGNORE, la colonna non viene aggiornata. Dopo aver aggiornato la riga, il driver viene modificato l'elemento corrispondente della matrice di stato di riga SQL_ROW_UPDATED o SQL_ROW_SUCCESS_WITH_INFO (se è presente la matrice di stato di riga).<br /><br /> È definito dal driver che cos'è il comportamento se **SQLSetPos** con un *operazione* argomento di SQL_UPDATE viene chiamato su un cursore che include le colonne duplicate. Il driver può restituire un valore SQLSTATE definiti dal driver, può aggiornare la prima colonna visualizzata nel set di risultati o eseguire altri comportamenti definiti dal driver.<br /><br /> La matrice di operazione riga a cui punta l'attributo di istruzione SQL_ATTR_ROW_OPERATION_PTR può essere utilizzata per indicare che una riga nel set di righe corrente deve essere ignorata durante un aggiornamento bulk. Per altre informazioni, vedere "Matrici di stato e di operazione" più avanti in questo riferimento alle funzioni.|  
|SQL_DELETE|Il driver posiziona il cursore sulla riga specificata da *RowNumber* ed elimina la riga di dati sottostante. L'elemento corrispondente della matrice di stato di riga vengono modificate in SQL_ROW_DELETED. Dopo la riga è stata eliminata, seguenti non sono validi per la riga: posizionato update e delete (istruzioni), le chiamate a **SQLGetData**e le chiamate a **SQLSetPos** con *operazione* impostato su un valore qualsiasi eccetto SQL_POSITION. Per i driver che supportano la compressione, la riga viene eliminata dalla posizione del cursore quando nuovi dati vengono recuperati dall'origine dati.<br /><br /> Indica se la riga rimane visibile varia a seconda del tipo di cursore. Ad esempio, le righe eliminate sono visibili ai cursori statici e gestito da keyset, ma non per i cursori dinamici.<br /><br /> La matrice di operazione riga a cui punta l'attributo di istruzione SQL_ATTR_ROW_OPERATION_PTR può essere utilizzata per indicare che una riga nel set di righe corrente deve essere ignorata durante un'operazione di eliminazione bulk. Per altre informazioni, vedere "Matrici di stato e di operazione" più avanti in questo riferimento alle funzioni.|  
  
## <a name="locktype-argument"></a>Argomento di tipo di blocco  
 Il *LockType* argomento fornisce un modo per controllare la concorrenza delle applicazioni. Nella maggior parte dei casi, origini dati che supportano i livelli di concorrenza e le transazioni supporterà solo il valore SQL_LOCK_NO_CHANGE del *LockType* argomento. Il *LockType* argomento in genere viene usato solo per il supporto basato su file.  
  
 Il *LockType* argomento specifica lo stato di blocco di riga dopo **SQLSetPos** è stata eseguita. Se il driver è in grado di bloccare la riga per eseguire l'operazione richiesta o per soddisfare le *LockType* argomento, restituisce SQL_ERROR e SQLSTATE 42000 (sintassi o violazione di accesso).  
  
 Anche se il *LockType* specificati argomenti per una singola istruzione, il blocco riconosce gli stessi privilegi per tutte le istruzioni per la connessione. In particolare, un blocco is acquisito da un'unica istruzione in una connessione può essere sbloccato mediante un'istruzione diversa nella stessa connessione.  
  
 Una riga bloccata tramite **SQLSetPos** resta bloccato finché l'applicazione chiama **SQLSetPos** per la riga con *LockType* impostata SQL_LOCK_UNLOCK o finché l'applicazione le chiamate **SQLFreeHandle** per l'istruzione o **SQLFreeStmt** con l'opzione di SQL_CLOSE. Per un driver che supporta le transazioni, una riga bloccata tramite **SQLSetPos** viene sbloccata quando l'applicazione chiama **SQLEndTran** per eseguire il commit o rollback della transazione sulla connessione (se un cursore è chiuso Quando viene eseguito il commit o rollback, come indicato dai tipi di informazioni SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR restituiti da una transazione **SQLGetInfo**).  
  
 Il *LockType* argomento supporta i seguenti tipi di blocchi. Per determinare quali blocchi sono supportati da un'origine dati, un'applicazione chiama **SQLGetInfo** con SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 oppure SQL_STATIC_ Tipo di informazioni CURSOR_ATTRIBUTES1 (a seconda del tipo di cursore).  
  
|*LockType* argomento|Tipo di blocco|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|L'origine dati o driver garantisce che la riga è lo stesso stato bloccato o sbloccato come accadeva prima **SQLSetPos** è stato chiamato. Questo valore di *LockType* consente a origini dati che non supportano il blocco a livello di riga esplicite per l'uso di qualsiasi blocco viene richiesto dai livelli di isolamento delle transazioni e concorrenza correnti.|  
|SQL_LOCK_EXCLUSIVE|L'origine dati o driver Blocca esclusivamente la riga. Un'istruzione su una connessione diversa o in un'altra applicazione non è utilizzabile per acquisire tutti i blocchi sulla riga.|  
|SQL_LOCK_UNLOCK|L'origine dati o driver Sblocca la riga.|  
  
 Se un driver supporta SQL_LOCK_EXCLUSIVE ma SQL_LOCK_UNLOCK, una riga bloccata rimarrà bloccata finché non si verifica una delle chiamate di funzione descritte nel paragrafo precedente.  
  
 Se un driver supporta SQL_LOCK_EXCLUSIVE ma SQL_LOCK_UNLOCK, una riga bloccata rimarrà bloccata finché l'applicazione chiama **SQLFreeHandle** per l'istruzione o **SQLFreeStmt** con l'opzione di SQL_CLOSE. Se il driver supporta le transazioni e chiude il cursore dopo il commit o il rollback della transazione, l'applicazione chiama **SQLEndTran**.  
  
 Per le operazioni update e delete **SQLSetPos**, l'applicazione usa le *LockType* argomento come indicato di seguito:  
  
-   Per garantire che una riga non cambia dopo che sono stati recuperati, un'applicazione chiama **SQLSetPos** con *operazione* impostato su SQL_REFRESH e *LockType* impostato su SQL_LOCK_ ESCLUSIVO.  
  
-   Se l'applicazione imposta *LockType* a SQL_LOCK_NO_CHANGE, il driver garantisce che un'operazione update o delete avrà esito positivo solo se l'applicazione specificata SQL_CONCUR_LOCK per l'attributo di istruzione SQL_ATTR_CONCURRENCY.  
  
-   Se l'applicazione specifica SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES per l'attributo di istruzione SQL_ATTR_CONCURRENCY, il driver confronta le versioni delle righe o valori e rifiuta l'operazione, la riga è stato modificato dopo l'applicazione recuperato la riga.  
  
-   Se l'applicazione specifica SQL_CONCUR_READ_ONLY per l'attributo di istruzione SQL_ATTR_CONCURRENCY, il driver rifiuta qualsiasi aggiornamento o eliminazione.  
  
 Per altre informazioni relative all'attributo di istruzione SQL_ATTR_CONCURRENCY, vedere [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="status-and-operation-arrays"></a>Lo stato e le matrici di operazione  
 Le matrici di stato e l'operazione seguente vengono utilizzate quando si chiama **SQLSetPos**:  
  
-   Matrice di stato di riga (come a cui fa riferimento il campo SQL_DESC_ARRAY_STATUS_PTR nell'implementazione e l'attributo di istruzione SQL_ATTR_ROW_STATUS_ARRAY) contiene i valori di stato per ogni riga di dati nel set di righe. Il driver imposta i valori di stato di questa matrice dopo una chiamata a **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, oppure **SQLSetPos** . Questa matrice a cui punta l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR.  
  
-   Matrice di operazione di riga (come a cui fa riferimento nel campo SQL_DESC_ARRAY_STATUS_PTR nel ARD e l'attributo di istruzione SQL_ATTR_ROW_OPERATION_ARRAY) contiene un valore per ogni riga nel set di righe che indica se una chiamata a **SQLSetPos**per un'operazione bulk viene ignorata o eseguita. Ogni elemento nella matrice è impostato su SQL_ROW_PROCEED (predefinito) o SQL_ROW_IGNORE. Questa matrice a cui punta l'attributo di istruzione SQL_ATTR_ROW_OPERATION_PTR.  
  
 Il numero di elementi nelle matrici di stato e l'operazione sia uguale al numero di righe nel set di righe (come definito nell'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE).  
  
 Per informazioni sulla matrice di stato di riga, vedere [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md). Per informazioni sulla matrice di operazione di riga, vedere "Verrà ignorato un riga in un'operazione in blocco," più avanti in questa sezione.  
  
## <a name="using-sqlsetpos"></a>Con SQLSetPos  
 Prima di un'applicazione chiama **SQLSetPos**, è necessario eseguire la sequenza di passaggi seguente:  
  
1.  Se l'applicazione chiamerà **SQLSetPos** con *operazione* impostato su SQL_UPDATE, chiamata **SQLBindCol** (oppure **SQLSetDescRec**) per ogni colonna per specificare il tipo di dati e associare i buffer di dati e sulla lunghezza della colonna.  
  
2.  Se l'applicazione chiamerà **SQLSetPos** con *operazione* impostato su SQL_DELETE o SQL_UPDATE, chiamata **SQLColAttribute** per assicurarsi che le colonne per essere eliminata o aggiornata possono essere aggiornate.  
  
3.  Chiamare **SQLExecDirect**, **SQLExecute**, o una funzione di catalogo per creare un set di risultati.  
  
4.  Chiamare **SQLFetch** oppure **SQLFetchScroll** per recuperare i dati.  
  
 Per altre informazioni sull'uso **SQLSetPos**, vedere [aggiornamento dei dati con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
## <a name="deleting-data-using-sqlsetpos"></a>Eliminazione di dati con SQLSetPos  
 Per eliminare i dati con **SQLSetPos**, un'applicazione chiama **SQLSetPos** con *RowNumber* impostato sul numero della riga da eliminare e *operazione*impostato su SQL_DELETE.  
  
 Dopo aver eliminati i dati, il driver modifica il valore nella matrice di stato riga di implementazione per la riga appropriata in SQL_ROW_DELETED (o SQL_ROW_ERROR).  
  
## <a name="updating-data-using-sqlsetpos"></a>L'aggiornamento dei dati con SQLSetPos  
 Un'applicazione può passare il valore per una colonna nel buffer di dati associati o con uno o più chiamate a **SQLPutData**. Le colonne i cui dati vengono passati con **SQLPutData** sono detti *data-at-execution* *colonne*. Queste vengono comunemente usate per inviare i dati per le colonne SQL_LONGVARBINARY e SQL_LONGVARCHAR e può essere combinate con altre colonne.  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>Per aggiornare i dati con SQLSetPos, un'applicazione:  
  
1.  I valori decimali nei buffer di dati e lunghezza/indicatore associato **SQLBindCol**:  
  
    -   Per le colonne normali, l'applicazione inserisce il nuovo valore della colonna nel  *\*TargetValuePtr* buffer e la lunghezza di tale valore nel  *\*StrLen_or_IndPtr* buffer. Se la riga non deve essere aggiornata, l'applicazione inserisce SQL_ROW_IGNORE nell'elemento di tale riga della matrice di operazione di riga.  
  
    -   Per le colonne data-at-execution, l'applicazione inserisce un valore definito dall'applicazione, ad esempio il numero di colonna, nella  *\*TargetValuePtr* buffer. Il valore può essere utilizzato in un secondo momento per identificare la colonna.  
  
         L'applicazione inserisce il risultato della finestra di SQL_LEN_DATA_AT_EXEC (*lunghezza*) (macro) nel **StrLen_or_IndPtr* buffer. Se il tipo di dati SQL della colonna è SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo di dati specifici dell'origine dati di tipo long e il driver restituisce "Y" per il tipo di informazioni SQL_NEED_LONG_DATA_LEN **SQLGetInfo**, *lunghezza*  è il numero di byte di dati da inviare per il parametro; in caso contrario, deve essere un valore non negativo e viene ignorato.  
  
2.  Le chiamate **SQLSetPos** con il *operazione* argomento impostato su SQL_UPDATE per aggiornare la riga di dati.  
  
    -   Se non sono disponibili colonne data-at-execution, il processo è stato completato.  
  
    -   Se sono presenti colonne data-at-execution, la funzione restituisce SQL_NEED_DATA e procede al passaggio 3.  
  
3.  Le chiamate **SQLParamData** per recuperare l'indirizzo delle  *\*TargetValuePtr* buffer per la prima colonna data-at-execution da elaborare. **SQLParamData** restituisce SQL_NEED_DATA. L'applicazione recupera il valore definito dall'applicazione il  *\*TargetValuePtr* buffer.  
  
    > [!NOTE]  
    >  Anche se i parametri data-at-execution sono analoghi alle colonne data-at-execution, il valore restituito da **SQLParamData** è diverso per ognuno.  
  
    > [!NOTE]  
    >  I parametri data-at-execution sono parametri in un'istruzione SQL per il quale i dati verranno inviati con **SQLPutData** quando viene eseguita l'istruzione con **SQLExecDirect** o **SQLExecute**. Sono associate con **SQLBindParameter** oppure tramite l'impostazione con descrittori **SQLSetDescRec**. Il valore restituito da **SQLParamData** viene passato a un valore a 32 bit **SQLBindParameter** nel *ParameterValuePtr* argomento.  
  
    > [!NOTE]  
    >  Le colonne data-at-execution sono colonne in un set di righe per cui i dati verranno inviati con **SQLPutData** quando viene aggiornata una riga con **SQLSetPos**. Sono associate con **SQLBindCol**. Il valore restituito da **SQLParamData** è l'indirizzo della riga di **TargetValuePtr* buffer in fase di elaborazione.  
  
4.  Le chiamate **SQLPutData** uno o più volte per inviare i dati per la colonna. È necessario più di una chiamata se tutti i valori di dati non possono essere restituiti nel  *\*TargetValuePtr* specificato nel buffer **SQLPutData**; più chiamate al metodo **SQLPutData** per la stessa colonna sono consentiti solo quando si inviano dati di tipo carattere C a una colonna con un tipo di carattere, binary o dati specifici dell'origine dati o per l'invio di dati C binari a una colonna con un carattere, binario, o del tipo di dati specifici dell'origine dati.  
  
5.  Le chiamate **SQLParamData** nuovamente per segnalare che tutti i dati sono stati inviati per la colonna.  
  
    -   Se sono presenti altre colonne data-at-execution **SQLParamData** restituisce SQL_NEED_DATA e l'indirizzo del *TargetValuePtr* buffer per la colonna data-at-execution successiva da elaborare. L'applicazione si ripete i passaggi 4 e 5.  
  
    -   Se sono presenti colonne data-at-execution non sono più, il processo è stato completato. Se è stata eseguita correttamente, l'istruzione **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; se l'esecuzione non riesce, viene restituito SQL_ERROR. A questo punto **SQLParamData** può restituire qualsiasi valore SQLSTATE che può essere restituito da **SQLSetPos**.  
  
 Se i dati sono stati aggiornati, il driver modifica il valore nella matrice di stato riga di implementazione per la riga appropriata in SQL_ROW_UPDATED.  
  
 Se l'operazione sia annullata o si verifica un errore **SQLParamData** oppure **SQLPutData**dopo **SQLSetPos** restituisce SQL_NEED_DATA e prima che i dati vengono inviati per tutti le colonne data-at-execution, l'applicazione può chiamare solo **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions** , **SQLParamData**, o **SQLPutData** per l'istruzione o la connessione associata all'istruzione. Se chiama qualsiasi altra funzione per l'istruzione o la connessione associata all'istruzione, la funzione restituisce SQL_ERROR e SQLSTATE HY010 (funzione di errore nella sequenza).  
  
 Se l'applicazione chiama **SQLCancel** mentre il driver deve comunque i dati per le colonne data-at-execution, il driver Annulla l'operazione. L'applicazione può quindi chiamare **SQLSetPos** anche in questo caso, l'annullamento non influisce sullo stato del cursore o la posizione corrente del cursore.  
  
 Quando l'elenco SELECT della specifica di query associata al cursore contiene più di un riferimento alla stessa colonna, se viene generato un errore o il driver ignora i riferimenti duplicati ed esegue le operazioni richieste è definito dal driver.  
  
## <a name="performing-bulk-operations"></a>Esecuzione di operazioni Bulk  
 Se il *RowNumber* l'argomento è 0, il driver esegue l'operazione specificata nel *operazione* argomento per ogni riga nel set di righe con valore SQL_ROW_PROCEED nel relativo campo nell'operazione di riga matrice a cui punta attributo dell'istruzione SQL_ATTR_ROW_OPERATION_PTR. Si tratta di un valore valido di *RowNumber* argomento per un' *operazione* argomento di SQL_DELETE, SQL_REFRESH, o SQL_UPDATE, ma non SQL_POSITION. **SQLSetPos** con un *operazione* di SQL_POSITION e un *RowNumber* uguale a 0 restituiranno SQLSTATE HY109 (posizione del cursore non valido).  
  
 Se si verifica un errore che riguarda l'intero set di righe, ad esempio SQLSTATE HYT00 (Timeout scaduto), il driver restituisce SQL_ERROR e i codici SQLSTATE appropriati. Il contenuto del buffer di set di righe non è definito e la posizione del cursore viene modificata.  
  
 Se si verifica un errore che si riferisce a una singola riga, il driver:  
  
-   Imposta l'elemento per la riga nella matrice di stato di riga a cui punta l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR a SQL_ROW_ERROR.  
  
-   Invia uno o più SQLSTATEs aggiuntive per l'errore nella coda degli errori e imposta il campo SQL_DIAG_ROW_NUMBER nella struttura di dati di diagnostica.  
  
 Dopo avere elaborato l'errore o avviso, se il driver viene completata l'operazione per le righe rimanenti nel set di righe, viene restituito SQL_SUCCESS_WITH_INFO. Di conseguenza, per ogni riga che ha restituito un errore, nella coda degli errori contiene zero o più SQLSTATEs aggiuntive. Se il driver arresta l'operazione dopo che è stato elaborato l'errore o avviso, viene restituito SQL_ERROR.  
  
 Se il driver restituisce eventuali avvisi, quali SQLSTATE 01004 (dati troncati), restituisce gli avvisi che si applicano all'intero set di righe o alle righe sconosciute nel set di righe prima di restituire le informazioni sull'errore che si applica a righe specifiche. Restituisce gli avvisi per le righe specifiche insieme a qualsiasi altra informazione di errore su tali righe.  
  
 Se *RowNumber* è uguale a 0 e *operazione* è SQL_UPDATE, SQL_REFRESH o SQL_DELETE, il numero delle righe che **SQLSetPos** opera d'a cui punta l'attributo Attributo di istruzione _FETCHED_PTR.  
  
 Se *RowNumber* è uguale a 0 e *operazione* è SQL_DELETE, SQL_REFRESH o SQL_UPDATE, la riga corrente dopo l'operazione è quello utilizzato per la riga corrente prima dell'operazione.  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>Verrà ignorata una riga in un'operazione Bulk  
 La matrice di operazione riga può essere utilizzata per indicare che una riga nel set di righe corrente deve essere ignorata durante un'operazione bulk utilizzando **SQLSetPos**. Per impostare il driver per ignorare una o più righe durante un'operazione bulk, un'applicazione deve eseguire la procedura seguente:  
  
1.  Chiamare **SQLSetStmtAttr** per impostare l'attributo di istruzione SQL_ATTR_ROW_OPERATION_PTR in modo che punti a una matrice di SQLUSMALLINTs. Questo campo può essere impostato anche chiamando **SQLSetDescField** per impostare il campo di intestazione SQL_DESC_ARRAY_STATUS_PTR di ARD, il quale richiede che un'applicazione ottiene l'handle descrittore.  
  
2.  Impostare ogni elemento della matrice operazione riga a uno dei due valori:  
  
    -   SQL_ROW_IGNORE, per indicare che la riga è stata esclusa per l'operazione bulk.  
  
    -   SQL_ROW_PROCEED, per indicare che la riga è incluso nell'operazione di massa. Si tratta del valore predefinito.  
  
3.  Chiamare **SQLSetPos** per eseguire l'operazione bulk.  
  
 Le regole seguenti si applicano alla matrice operazione riga:  
  
-   SQL_ROW_IGNORE e SQL_ROW_PROCEED interessano solo le operazioni bulk usando **SQLSetPos** con un *operazione* di SQL_DELETE o SQL_UPDATE. Le chiamate a non influiscano **SQLSetPos** con un *operazione* di SQL_REFRESH o SQL_POSITION.  
  
-   Il puntatore viene impostato su null per impostazione predefinita.  
  
-   Se il puntatore è null, tutte le righe vengono aggiornate come se tutti gli elementi impostati per SQL_ROW_PROCEED.  
  
-   L'impostazione di un elemento a SQL_ROW_PROCEED non garantisce che l'operazione si verificherà in tale riga specifica. Ad esempio, se una determinata riga nel set di righe con lo stato di SQL_ROW_ERROR, il driver non sia in grado di aggiornare tale riga indipendentemente dal fatto che l'applicazione specificata SQL_ROW_PROCEED. Un'applicazione deve controllare sempre la matrice di stato di riga per verificare se l'operazione ha avuto esito positivo.  
  
-   SQL_ROW_PROCEED è definito come 0 nel file di intestazione. Un'applicazione può inizializzare la matrice di operazione riga su 0 per poter elaborare tutte le righe.  
  
-   Se il numero di elementi "n" nella matrice di operazione riga è impostato su SQL_ROW_IGNORE e **SQLSetPos** viene chiamato per eseguire un aggiornamento bulk o operazione di eliminazione, l'ennesima riga nel set di righe rimarrà invariato dopo la chiamata a **SQLSetPos**.  
  
-   Un'applicazione deve impostare automaticamente una colonna di sola lettura a SQL_ROW_IGNORE.  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>Ignorare una colonna in un'operazione Bulk  
 Per evitare un'elaborazione diagnostica generata da tentativi aggiornamenti a una o più colonne di sola lettura, un'applicazione può impostare il valore nel buffer di lunghezza/indicatore associato al SQL_COLUMN_IGNORE. Per altre informazioni, vedere [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, un'applicazione consente all'utente di individuare la tabella ORDERS e aggiornare lo stato dell'ordine. Il cursore è gestito da keyset con una dimensione di set di righe di 20 e Usa il controllo della concorrenza ottimistica confronto tra le versioni di riga. Dopo ogni set di righe viene recuperato, l'applicazione lo stampa e consente all'utente di selezionare e aggiornare lo stato di un ordine. L'applicazione utilizza **SQLSetPos** per posizionare il cursore nella riga selezionata ed esegue un aggiornamento posizionato della riga. La gestione degli errori è omessa per maggiore chiarezza.  
  
```  
#define ROWS 20  
#define STATUS_LEN 6  
  
SQLCHAR        szStatus[ROWS][STATUS_LEN], szReply[3];  
SQLINTEGER     cbStatus[ROWS], cbOrderID;  
SQLUSMALLINT   rgfRowStatus[ROWS];  
SQLUINTEGER    sOrderID, crow = ROWS, irow;  
SQLHSTMT       hstmtS, hstmtU;  
  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CONCURRENCY, (SQLPOINTER) SQL_CONCUR_ROWVER, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER) SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_STATUS_PTR, (SQLPOINTER) rgfRowStatus, 0);  
SQLSetCursorName(hstmtS, "C1", SQL_NTS);  
SQLExecDirect(hstmtS, "SELECT ORDERID, STATUS FROM ORDERS ", SQL_NTS);  
  
SQLBindCol(hstmtS, 1, SQL_C_ULONG, &sOrderID, 0, &cbOrderID);  
SQLBindCol(hstmtS, 2, SQL_C_CHAR, szStatus, STATUS_LEN, &cbStatus);  
  
while ((retcode == SQLFetchScroll(hstmtS, SQL_FETCH_NEXT, 0)) != SQL_ERROR) {  
   if (retcode == SQL_NO_DATA_FOUND)  
      break;  
   for (irow = 0; irow < crow; irow++) {  
      if (rgfRowStatus[irow] != SQL_ROW_DELETED)  
         printf("%2d %5d %*s\n", irow+1, sOrderID, NAME_LEN-1, szStatus[irow]);  
   }  
   while (TRUE) {  
      printf("\nRow number to update?");  
      gets_s(szReply, 3);  
      irow = atoi(szReply);  
      if (irow > 0 && irow <= crow) {  
         printf("\nNew status?");  
         gets_s(szStatus[irow-1], (ROWS * STATUS_LEN));  
         SQLSetPos(hstmtS, irow, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
         SQLPrepare(hstmtU,  
          "UPDATE ORDERS SET STATUS=? WHERE CURRENT OF C1", SQL_NTS);  
         SQLBindParameter(hstmtU, 1, SQL_PARAM_INPUT,  
            SQL_C_CHAR, SQL_CHAR,  
            STATUS_LEN, 0, szStatus[irow], 0, NULL);  
         SQLExecute(hstmtU);  
      } else if (irow == 0) {  
         break;  
      }  
   }  
}  
```  
  
 Per altri esempi, vedere [istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) e [aggiornare righe nel set di righe con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultati|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Esecuzione di operazioni bulk che non riguardano la posizione del cursore di blocco|[Funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Imposta il recupero di un blocco di dati o lo scorrimento di un risultato|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Recupero di un singolo campo di un descrittore|[Funzione SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Recupero di più campi di un descrittore|[Funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|L'impostazione di un singolo campo di un descrittore|[Funzione SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|L'impostazione di più campi di un descrittore|[Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|L'impostazione di un attributo di istruzione|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
