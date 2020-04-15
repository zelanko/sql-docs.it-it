---
title: 'Funzione SQLSetPos : Documenti Microsoft'
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a8839f1ae540ac9e5f29e144f7f57fb754e50ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287331"
---
# <a name="sqlsetpos-function"></a>Funzione SQLSetPos
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLSetPos** imposta la posizione del cursore in un set di righe e consente a un'applicazione di aggiornare i dati nel set di righe o di aggiornare o eliminare i dati nel set di risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *Rownumber*  
 [Ingresso] Posizione della riga nel set di righe su cui eseguire l'operazione specificata con il *Operation* argomento. Se *RowNumber* è 0, l'operazione si applica a ogni riga del set di righe.  
  
 Per ulteriori informazioni, vedere "Commenti".  
  
 *Operazione*  
 [Ingresso] Operazione da eseguire:  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  Il valore SQL_ADD per l'argomento *Operation* è stato deprecato per ODBC *3.x*. I driver ODBC *3.x* dovranno supportare SQL_ADD per la compatibilità con le versioni precedenti. Questa funzionalità è stata sostituita da una chiamata a **SQLBulkOperations** con *un'operazione* di SQL_ADD. Quando un'applicazione ODBC *3.x* funziona con un driver ODBC *2.x,* Gestione Driver esegue il mapping di una chiamata a **SQLBulkOperations** con *un'operazione* di SQL_ADD a **SQLSetPos** con *un'operazione* di SQL_ADD.  
  
 Per ulteriori informazioni, vedere "Commenti".  
  
 *Locktype*  
 [Ingresso] Specifica come bloccare la riga dopo aver eseguito l'operazione specificata nell'argomento *Operation.*  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 Per ulteriori informazioni, vedere "Commenti".  
  
 **Restituisce**  
  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSetPos** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLSetPos** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
 Per tutti gli SQLSTATE che possono restituire SQL_SUCCESS_WITH_INFO o SQL_ERROR (ad eccezione di 01xxx SQLSTATEs), viene restituito SQL_SUCCESS_WITH_INFO se si verifica un errore in uno o più, ma non in tutte le righe di un'operazione multiriga, e SQL_ERROR viene restituito se si verifica un errore in un'operazione a riga singola.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01001|Conflitto di funzionamento del cursoreCursor operation conflict|*L'argomento Operation* è stato SQL_DELETE o SQL_UPDATE e non sono state eliminate o aggiornate righe o più righe. Per ulteriori informazioni sugli aggiornamenti a più righe, vedere la descrizione *dell'attributo* SQL_ATTR_SIMULATE_CURSOR in **SQLSetStmtAttr**. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)<br /><br /> L'argomento *Operation* è stato SQL_DELETE o SQL_UPDATE e l'operazione non è riuscita a causa della concorrenza ottimistica. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Troncamento a destra dei dati stringaString data right truncation|*L'argomento Operation* è stato SQL_REFRESH e i dati stringa o binari restituiti per una colonna o colonne con un tipo di dati SQL_C_CHAR o SQL_C_BINARY hanno determinato il troncamento di caratteri non vuoti o dati binari non NULL.|  
|01S01 (in questo stato di|Errore nella riga|L'argomento *RowNumber* era 0 e si è verificato un errore in una o più righe durante l'esecuzione dell'operazione specificata con l'argomento *Operation.*<br /><br /> (SQL_SUCCESS_WITH_INFO viene restituito se si verifica un errore in una o più righe, ma non tutte, di un'operazione a più righe e SQL_ERROR viene restituito se si verifica un errore in un'operazione a riga singola.)<br /><br /> (Questo SQLSTATE viene restituito solo quando **SQLSetPos** viene chiamato dopo **SQLExtendedFetch**, se il driver è un driver ODBC *2.x* e la libreria di cursori non viene utilizzata.)|  
|01S07 (intito)|Troncamento frazionario|*L'argomento Operation* è stato SQL_REFRESH, il tipo di dati del buffer dell'applicazione non è SQL_C_CHAR o SQL_C_BINARY e i dati restituiti ai buffer dell'applicazione per una o più colonne sono stati troncati. Per i tipi di dati numerici, la parte frazionaria del numero è stata troncata. Per i tipi di dati time, timestamp e interval contenenti un componente time, la parte frazionaria dell'ora è stata troncata.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07006|Violazione dell'attributo del tipo di dati con restrizioniRestricted data type attribute violation|Impossibile convertire il valore dei dati di una colonna nel set di risultati nel tipo di dati specificato da *TargetType* nella chiamata a **SQLBindCol**.|  
|07009|Indice descrittore non valido|*L'argomento Operation* è stato SQL_REFRESH o SQL_UPDATE ed è stata associata una colonna con un numero di colonna maggiore del numero di colonne nel set di risultati.|  
|21S02|Il grado della tabella derivata non corrisponde all'elenco di colonne|*L'argomento Operation* è stato SQL_UPDATE e nessuna colonna non è stata aggiornabile perché tutte le colonne erano non associate, di sola lettura o il valore nel buffer di lunghezza/indicatore associato è stato SQL_COLUMN_IGNORE.|  
|22001|Dati stringa, troncamento a destra|*L'argomento Operation* è stato SQL_UPDATE e l'assegnazione di un carattere o di un valore binario a una colonna ha generato il troncamento di caratteri non vuoti (per i caratteri) o non null (per binari) o byte.|  
|22003|Valore numerico non compreso nell'intervallo|L'argomento *Operation* è stato SQL_UPDATE e l'assegnazione di un valore numerico a una colonna nel set di risultati ha causato il troncamento dell'intera parte (anziché frazionaria).<br /><br /> L'argomento *Operation* è stato SQL_REFRESH e la restituzione del valore numerico per una o più colonne associate avrebbe causato una perdita di cifre significative.|  
|22007|Formato datetime non valido|*L'argomento Operazione* è stato SQL_UPDATE e l'assegnazione di un valore di data o timestamp a una colonna nel set di risultati ha causato il campo anno, mese o giorno non compreso nell'intervallo.<br /><br /> L'argomento *Operazione* è stato SQL_REFRESH e la restituzione del valore data o timestamp per una o più colonne associate avrebbe fatto sì che il campo anno, mese o giorno non fosse compreso nell'intervallo.|  
|22008|Overflow del campo Data/ora|*L'argomento Operation* è stato SQL_UPDATE e le prestazioni dell'aritmetica datetime sui dati inviati a una colonna nel set di risultati hanno restituito un campo datetime (anno, mese, giorno, ora, minuto o secondo campo) del risultato al di fuori dell'intervallo di valori consentito per il campo o non valido in base alle regole naturali del calendario gregoriano per datetime.<br /><br /> *L'argomento Operation* è stato SQL_REFRESH e le prestazioni dell'aritmetica datetime sui dati recuperati dal set di risultati hanno restituito un campo datetime (anno, mese, giorno, ora, minuto o secondo campo) del risultato non compreso nell'intervallo di valori consentito per il campo o non valido in base alle regole naturali del calendario gregoriano per le date time.|  
|22015|Overflow campo intervallo|*L'argomento Operation* è stato SQL_UPDATE e l'assegnazione di un tipo di dati numerico o di intervallo C esatto a un tipo di dati SQL a intervalli ha causato una perdita di cifre significative.<br /><br /> L'argomento *Operazione* è stato SQL_UPDATE; durante l'assegnazione a un tipo SQL intervallo, non è stata rappresentazione del valore del tipo C nel tipo SQL di intervallo.<br /><br /> *L'argomento Operation* è stato SQL_REFRESH e l'assegnazione da un tipo SQL esatto numerico o a intervallo a un tipo di intervallo C ha causato una perdita di cifre significative nel campo iniziale.<br /><br /> L'argomento *Operation* era SQL_ REFRESH; durante l'assegnazione a un tipo di intervallo C, non è stata rappresentazione del valore del tipo SQL nel tipo di intervallo C.|  
|22018|Valore di carattere non valido per la specifica del cast|L'argomento *Operazione* è stato SQL_REFRESH; il tipo C era un numero esatto o approssimativo, un datetime o un tipo di dati interval; il tipo SQL della colonna era un tipo di dati carattere; e il valore nella colonna non è un valore letterale valido del tipo C associato.<br /><br /> L'argomento *Operazione* era SQL_UPDATE; il tipo SQL era un numero esatto o approssimativo, un datetime o un tipo di dati interval; il tipo C è stato SQL_C_CHAR; e il valore nella colonna non è un valore letterale valido del tipo SQL associato.|  
|23000|Violazione dei vincoli di integrità|L'argomento *Operation* è stato SQL_DELETE o SQL_UPDATE e un vincolo di integrità è stato violato.|  
|24000|Stato del cursore non valido|*StatementHandle* era in uno stato eseguito, ma a *StatementHandle*non è stato associato alcun set di risultati .<br /><br /> (DM) Un cursore era aperto su *StatementHandle*, ma **SQLFetch** o **SQLFetchScroll** non era stato chiamato.<br /><br /> Un cursore era aperto su *StatementHandle*e **SQLFetch** o **SQLFetchScroll** era stato chiamato, ma il cursore è stato posizionato prima dell'inizio del set di risultati o dopo la fine del set di risultati.<br /><br /> *L'argomento Operation* è stato SQL_DELETE, SQL_REFRESH o SQL_UPDATE e il cursore è stato posizionato prima dell'inizio del set di risultati o dopo la fine del set di risultati.|  
|40001|Errore di serializzazione|È stato eseguito il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|42000|Errore di sintassi o violazione di accesso|Il driver non è stato in grado di bloccare la riga in base alle esigenze per eseguire l'operazione richiesta nell'argomento *Operation*.<br /><br /> Il driver non è riuscito a bloccare la riga come richiesto nell'argomento *LockType*.|  
|44000|Violazione della clausola WITH CHECK OPTION|*L'argomento Operazione* è stato SQL_UPDATE e l'aggiornamento è stato eseguito su una tabella visualizzata o una tabella derivata dalla tabella visualizzata creata specificando **WITH CHECK OPTION**, in modo che una o più righe interessate dall'aggiornamento non saranno più presenti nella tabella visualizzata.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*, quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione SQLSetPos.This asynchronous function was still executing when the SQLSetPos function was called.<br /><br /> (DM) *L'oggetto statementHandle* specificato non era in uno stato eseguito. La funzione è stata chiamata senza prima chiamare **SQLExecDirect**, **SQLExecute**o una funzione di catalogo.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) il driver era un driver ODBC *2.x* e **SQLSetPos** è stato chiamato per un *StatementHandle* dopo **SQLFetch** è stato chiamato.|  
|HY011|Impossibile impostare l'attributo ora|(DM) il driver era un driver ODBC *2.x;* è stato impostato l'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR; **SQLSetPos** è stato chiamato prima di **SQLFetch**, **SQLFetchScroll**o **SQLExtendedFetch** è stato chiamato.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|*L'argomento Operation* è stato SQL_UPDATE, un valore di dati è un puntatore null e il valore della lunghezza della colonna non è 0, SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NULL_DATA o minore o uguale a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> L'argomento *Operazione* è stato SQL_UPDATE; un valore di dati non era un puntatore null; il tipo di dati C è stato SQL_C_BINARY o SQL_C_CHAR; e il valore della lunghezza della colonna era minore di 0 ma non uguale a SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NTS o SQL_NULL_DATA oppure minore o uguale a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Il valore in un buffer di lunghezza/indicatore è stato SQL_DATA_AT_EXEC; il tipo SQL è SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo di dati specifico dell'origine dati long. e il tipo di informazioni SQL_NEED_LONG_DATA_LEN in **SQLGetInfo** era "Y".|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo non valido|(DM) il valore specificato per l'argomento *Operation* non è valido.<br /><br /> (DM) il valore specificato per l'argomento *LockType* non è valido.<br /><br /> *L'argomento Operation* è stato SQL_UPDATE o SQL_DELETE e l'attributo dell'istruzione SQL_ATTR_CONCURRENCY è stato SQL_ATTR_CONCUR_READ_ONLY.|  
|I107|Valore di riga non compreso nell'intervallo|Il valore specificato per l'argomento *RowNumber* è maggiore del numero di righe nel set di righe.|  
|I109|Posizione del cursore non valida|Il cursore associato a *StatementHandle* è stato definito come forward-only, pertanto non è stato possibile posizionare il cursore all'interno del set di righe. Vedere la descrizione dell'attributo SQL_ATTR_CURSOR_TYPE in **SQLSetStmtAttr**.<br /><br /> *L'argomento Operation* è stato SQL_UPDATE, SQL_DELETE o SQL_REFRESH e la riga identificata dall'argomento *RowNumber* è stata eliminata o non è stata recuperata.<br /><br /> (DM) l'argomento *RowNumber* era 0 e l'argomento *Operation* era SQL_POSITION.<br /><br /> **SQLSetPos** è stato chiamato dopo **SQLBulkOperations** è stato chiamato e prima **sqlFetchScroll** o **SQLFetch** è stato chiamato.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il driver o l'origine dati non supporta l'operazione richiesta nell'argomento *Operation* o l'argomento *LockType.*|  
|HYT00|Timeout|Il periodo di timeout della query è scaduto prima che l'origine dati restituisca il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr** con un *attributo* di SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
  
> [!CAUTION]
>  Per informazioni sull'istruzione indica che **SQLSetPos** può essere chiamato e cosa deve fare per garantire la compatibilità con le applicazioni ODBC *2.x,* vedere cursori a [blocchi, cursori scorrevoli e compatibilità con](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)le versioni precedenti .  
  
## <a name="rownumber-argument"></a>Argomento RowNumber  
 *L'argomento RowNumber* specifica il numero della riga nel set di righe su cui eseguire l'operazione specificata dall'argomento *Operation.* Se *RowNumber* è 0, l'operazione si applica a ogni riga del set di righe. *RowNumber* deve essere un valore compreso tra 0 e il numero di righe nel set di righe.  
  
> [!NOTE]  
>  Nel linguaggio C, le matrici sono in base 0 e l'argomento *RowNumber* è in base 1. Ad esempio, per aggiornare la quinta riga del set di righe, un'applicazione modifica i buffer del set di righe in corrispondenza dell'indice di matrice 4 ma specifica un *RowNumber* pari a 5.  
  
 Tutte le operazioni posizionano il cursore sulla riga specificata da *RowNumber*. Le seguenti operazioni richiedono una posizione del cursore:  
  
-   Istruzioni di aggiornamento ed eliminazione posizionate.  
  
-   Chiamate a **SQLGetData**.  
  
-   Chiamate a **SQLSetPos** con le opzioni di SQL_DELETE, SQL_REFRESH e SQL_UPDATE.  
  
 Ad esempio, se *RowNumber* è 2 per una chiamata a **SQLSetPos** con *un'operazione* di SQL_DELETE, il cursore viene posizionato sulla seconda riga del set di righe e tale riga viene eliminata. La voce nella matrice di stato della riga di implementazione (a cui fa riferimento l'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR) per la seconda riga viene modificata in SQL_ROW_DELETED.  
  
 Un'applicazione può specificare una posizione del cursore quando chiama **SQLSetPos**. In genere, chiama **SQLSetPos** con l'SQL_POSITION o SQL_REFRESH operazione per posizionare il cursore prima di eseguire un'istruzione di aggiornamento o eliminazione posizionata o la chiamata **di SQLGetData**.  
  
## <a name="operation-argument"></a>Argomento dell'operazione  
 *L'argomento Operation* supporta le operazioni seguenti. Per determinare quali opzioni sono supportate da un'origine dati, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (a seconda del tipo di cursore).  
  
|*Operazione*<br /><br /> argomento|Operazione|  
|------------------------------|---------------|  
|SQL_POSITION|Il driver posiziona il cursore sulla riga specificata da *RowNumber*.<br /><br /> Il contenuto della matrice di stato della riga a cui fa riferimento l'attributo dell'istruzione SQL_ATTR_ROW_OPERATION_PTR viene ignorato per l'SQL_POSITION *Operation*.|  
|SQL_REFRESH|Il driver posiziona il cursore sulla riga specificata da *RowNumber* e aggiorna i dati nei buffer del set di righe per tale riga. Per ulteriori informazioni sul modo in cui il driver restituisce i dati nei buffer del set di righe, vedere le descrizioni dell'associazione per riga e colonna in **SQLBindCol**.<br /><br /> **SQLSetPos** con *un'operazione* di SQL_REFRESH aggiorna lo stato e il contenuto delle righe all'interno del set di righe recuperato corrente. Ciò include l'aggiornamento dei segnalibri. Poiché i dati nei buffer vengono aggiornati ma non recuperati, l'appartenenza al set di righe è fissa. Questo è diverso dall'aggiornamento eseguito da una chiamata a **SQLFetchScroll** con un *FetchOrientation* di SQL_FETCH_RELATIVE e un *RowNumber* uguale a 0, che recupera nuovamente il set di righe dal set di risultati in modo che possa visualizzare i dati aggiunti e rimuovere i dati eliminati se tali operazioni sono supportate dal driver e il cursore.<br /><br /> Un aggiornamento riuscito con **SQLSetPos** non modificherà lo stato di riga SQL_ROW_DELETED. Le righe eliminate all'interno del set di righe continueranno a essere contrassegnate come eliminate fino al successivo recupero. Le righe scompariranno al successivo recupero se il cursore supporta la compressione (in cui un successivo **SQLFetch** o **SQLFetchScroll** non restituisce le righe eliminate).<br /><br /> Le righe aggiunte non vengono visualizzate quando viene eseguito un aggiornamento con **SQLSetPos.Added** rows do not appear when a refresh with SQLSetPos is performed. Questo comportamento è diverso da **SQLFetchScroll** con un *FetchType* di SQL_FETCH_RELATIVE e un *RowNumber* uguale a 0, che aggiorna anche il set di righe corrente, ma mostrerà i record eliminati aggiunti o comprimere i record eliminati se queste operazioni sono supportate dal cursore.<br /><br /> Un aggiornamento riuscito con **SQLSetPos** modificherà lo stato di una riga di SQL_ROW_ADDED in SQL_ROW_SUCCESS (se la matrice di stato della riga esiste).<br /><br /> Un aggiornamento riuscito con **SQLSetPos** modificherà lo stato di una riga di SQL_ROW_UPDATED al nuovo stato della riga (se la matrice di stato della riga esiste).<br /><br /> Se si verifica un errore in un'operazione **SQLSetPos** su una riga, lo stato della riga è impostato su SQL_ROW_ERROR (se la matrice di stato della riga esiste).<br /><br /> Per un cursore aperto con un attributo di istruzione SQL_ATTR_CONCURRENCY di SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, un aggiornamento con **SQLSetPos** potrebbe aggiornare i valori di concorrenza ottimistica utilizzati dall'origine dati per rilevare che la riga è stata modificata. In questo caso, le versioni di riga o i valori utilizzati per garantire la concorrenza del cursore vengono aggiornati ogni volta che i buffer del set di righe vengono aggiornati dal server. Ciò si verifica per ogni riga che viene aggiornata.<br /><br /> Il contenuto della matrice di stato della riga a cui fa riferimento l'attributo dell'istruzione SQL_ATTR_ROW_OPERATION_PTR viene ignorato per l'SQL_REFRESH *Operation*.|  
|SQL_UPDATE|Il driver posiziona il cursore sulla riga specificata da *RowNumber* e aggiorna la riga sottostante di dati con i valori nei buffer del set di righe (l'argomento *TargetValuePtr* in **SQLBindCol**). Recupera le lunghezze dei dati dai buffer di lunghezza/indicatore (l'argomento *StrLen_or_IndPtr* in **SQLBindCol**). Se la lunghezza di una colonna è SQL_COLUMN_IGNORE, la colonna non viene aggiornata. Dopo aver aggiornato la riga, il driver modifica l'elemento corrispondente della matrice di stato della riga in SQL_ROW_UPDATED o SQL_ROW_SUCCESS_WITH_INFO (se la matrice di stato della riga esiste).<br /><br /> È definito dal driver qual è il comportamento se **SQLSetPos** con un *Operation* argomento di SQL_UPDATE viene chiamato su un cursore che contiene colonne duplicate. Il driver può restituire un SQLSTATE definito dal driver, può aggiornare la prima colonna visualizzata nel set di risultati o eseguire altri comportamenti definiti dal driver.<br /><br /> La matrice di operazioni di riga a cui fa riferimento l'attributo di istruzione SQL_ATTR_ROW_OPERATION_PTR può essere utilizzata per indicare che una riga nel set di righe corrente deve essere ignorata durante un aggiornamento bulk. Per ulteriori informazioni, vedere "Matrici di stato e operazioni" più avanti in questo riferimento alla funzione.|  
|SQL_DELETE|Il driver posiziona il cursore sulla riga specificata da *RowNumber* ed elimina la riga di dati sottostante. Modifica l'elemento corrispondente della matrice di stato della riga in SQL_ROW_DELETED. Dopo l'eliminazione della riga, le istruzioni di aggiornamento ed eliminazione posizionate, le chiamate a **SQLGetData**e le chiamate a **SQLSetPos** con *Operation* impostato su un valore diverso da SQL_POSITION. Per i driver che supportano la compressione, la riga viene eliminata dal cursore quando vengono recuperati nuovi dati dall'origine dati.<br /><br /> Il fatto che la riga rimanga visibile dipende dal tipo di cursore. Ad esempio, le righe eliminate sono visibili ai cursori statici e basati su keyset ma non sono visibili ai cursori dinamici.<br /><br /> La matrice di operazioni di riga a cui fa riferimento l'attributo di istruzione SQL_ATTR_ROW_OPERATION_PTR può essere utilizzata per indicare che una riga nel set di righe corrente deve essere ignorata durante un'eliminazione bulk. Per ulteriori informazioni, vedere "Matrici di stato e operazioni" più avanti in questo riferimento alla funzione.|  
  
## <a name="locktype-argument"></a>Argomento LockType  
 Il *LockType* argomento fornisce un modo per le applicazioni per controllare la concorrenza. Nella maggior parte dei casi, le origini dati che supportano i livelli di concorrenza e le transazioni supporteranno solo il valore di SQL_LOCK_NO_CHANGE dell'argomento *LockType.* Il *LockType* argomento viene in genere utilizzato solo per il supporto basato su file.  
  
 Il *LockType* argomento specifica lo stato di blocco della riga dopo l'esecuzione di **SQLSetPos.** Se il driver non è in grado di bloccare la riga per eseguire l'operazione richiesta o per soddisfare il *LockType* argomento, restituisce SQL_ERROR e SQLSTATE 42000 (errore di sintassi o violazione di accesso).  
  
 Anche se l'argomento *LockType* viene specificato per una singola istruzione, il blocco assegna gli stessi privilegi a tutte le istruzioni sulla connessione. In particolare, un blocco acquisito da un'istruzione su una connessione può essere sbloccato da un'istruzione diversa sulla stessa connessione.  
  
 Una riga bloccata tramite **SQLSetPos** rimane bloccata fino a quando l'applicazione chiama **SQLSetPos** per la riga con *LockType* impostato su SQL_LOCK_UNLOCK o fino a quando l'applicazione chiama **SQLFreeHandle** per l'istruzione o **SQLFreeStmt** con l'opzione SQL_CLOSE. Per un driver che supporta le transazioni, una riga bloccata tramite **SQLSetPos** viene sbloccata quando l'applicazione chiama **SQLEndTran** per eseguire il commit o il rollback di una transazione nella connessione (se un cursore viene chiuso quando viene eseguito il commit o il rollback di una transazione, come indicato dai tipi di informazioni SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR restituiti da **SQLGetInfo**).  
  
 L'argomento *LockType* supporta i seguenti tipi di blocchi. Per determinare quali blocchi sono supportati da un'origine dati, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (a seconda del tipo di cursore).  
  
|*Argomento LockType*|Tipo di blocco|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|Il driver o l'origine dati assicura che la riga si trova nello stesso stato bloccato o sbloccato in cui si trovava prima della chiamata a **SQLSetPos.** Questo valore di *LockType* consente alle origini dati che non supportano il blocco esplicito a livello di riga di utilizzare qualsiasi blocco richiesto dai livelli di isolamento della concorrenza e delle transazioni correnti.|  
|SQL_LOCK_EXCLUSIVE|Il driver o l'origine dati blocca la riga in modo esclusivo. Un'istruzione su una connessione diversa o in un'applicazione diversa non può essere utilizzata per acquisire blocchi sulla riga.|  
|SQL_LOCK_UNLOCK|Il driver o l'origine dati sblocca la riga.|  
  
 Se un driver supporta SQL_LOCK_EXCLUSIVE ma non supporta SQL_LOCK_UNLOCK, una riga bloccata rimarrà bloccata fino a quando non si verifica una delle chiamate di funzione descritte nel paragrafo precedente.  
  
 Se un driver supporta SQL_LOCK_EXCLUSIVE ma non supporta SQL_LOCK_UNLOCK, una riga bloccata rimarrà bloccata fino a quando l'applicazione chiama **SQLFreeHandle** per l'istruzione o **SQLFreeStmt** con l'opzione SQL_CLOSE. Se il driver supporta le transazioni e chiude il cursore al momento del commit o del rollback della transazione, l'applicazione chiama **SQLEndTran**.  
  
 Per le operazioni di aggiornamento ed eliminazione in **SQLSetPos**, l'applicazione utilizza l'argomento *LockType* come segue:  
  
-   Per garantire che una riga non venga modificata dopo il recupero, un'applicazione chiama **SQLSetPos** con *Operation* impostato su SQL_REFRESH e *LockType* impostato su SQL_LOCK_EXCLUSIVE.  
  
-   Se l'applicazione imposta *LockType* su SQL_LOCK_NO_CHANGE, il driver garantisce che un'operazione di aggiornamento o eliminazione avrà esito positivo solo se l'applicazione specificata SQL_CONCUR_LOCK per l'attributo di istruzione SQL_ATTR_CONCURRENCY.  
  
-   Se l'applicazione specifica SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES per l'attributo di istruzione SQL_ATTR_CONCURRENCY, il driver confronta le versioni o i valori delle righe e rifiuta l'operazione se la riga è stata modificata dopo che l'applicazione ha recuperato la riga.  
  
-   Se l'applicazione specifica SQL_CONCUR_READ_ONLY per l'attributo di istruzione SQL_ATTR_CONCURRENCY, il driver rifiuta qualsiasi operazione di aggiornamento o eliminazione.  
  
 Per ulteriori informazioni sull'attributo dell'istruzione SQL_ATTR_CONCURRENCY , vedere [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="status-and-operation-arrays"></a>Matrici di stato e operazioni  
 Le seguenti matrici di stato e operazioni vengono utilizzate quando si chiama **SQLSetPos:**  
  
-   La matrice di stato della riga (a cui fa riferimento il campo SQL_DESC_ARRAY_STATUS_PTR nell'attributo IRD e l'istruzione SQL_ATTR_ROW_STATUS_ARRAY) contiene i valori di stato per ogni riga di dati nel set di righe. Il driver imposta i valori di stato in questa matrice dopo una chiamata a **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**o **SQLSetPos**. Questa matrice fa riferimento all'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR.  
  
-   La matrice di operazioni di riga (a seconda del campo SQL_DESC_ARRAY_STATUS_PTR nell'attributo ARD e SQL_ATTR_ROW_OPERATION_ARRAY statement) contiene un valore per ogni riga nel set di righe che indica se una chiamata a **SQLSetPos** per un'operazione bulk viene ignorata o eseguita. Ogni elemento della matrice è impostato su SQL_ROW_PROCEED (impostazione predefinita) o su SQL_ROW_IGNORE. Questa matrice fa riferimento all'attributo dell'istruzione SQL_ATTR_ROW_OPERATION_PTR.  
  
 Il numero di elementi nelle matrici di stato e operazione deve essere uguale al numero di righe nel set di righe (come definito dall'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE).  
  
 Per informazioni sulla matrice di stato della riga, vedere [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md). Per informazioni sulla matrice di operazioni di riga, vedere "Ignorare una riga in un'operazione in blocco" più avanti in questa sezione.  
  
## <a name="using-sqlsetpos"></a>Utilizzo di SQLSetPosUsing SQLSetPos  
 Prima che un'applicazione chiami **SQLSetPos**, è necessario eseguire la sequenza di passaggi seguente:  
  
1.  Se l'applicazione chiamerà **SQLSetPos** con *Operation* impostato su SQL_UPDATE, chiamare **SQLBindCol** (o **SQLSetDescRec**) per ogni colonna per specificare il tipo di dati e i buffer di associazione per i dati e la lunghezza della colonna.  
  
2.  Se l'applicazione chiamerà **SQLSetPos** con *Operation* impostato su SQL_DELETE o SQL_UPDATE, chiamare **SQLColAttribute** per assicurarsi che le colonne da eliminare o aggiornare siano aggiornabili.  
  
3.  Chiamare **SQLExecDirect**, **SQLExecute**o una funzione di catalogo per creare un set di risultati.  
  
4.  Chiamare **SQLFetch** o **SQLFetchScroll** per recuperare i dati.  
  
 Per ulteriori informazioni **sull'utilizzo di SQLSetPos**, vedere Aggiornamento dei dati con [SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
## <a name="deleting-data-using-sqlsetpos"></a>Eliminazione di dati tramite SQLSetPosDeleting Data Using SQLSetPos  
 Per eliminare dati con **SQLSetPos**, un'applicazione chiama **SQLSetPos** con *RowNumber* impostato sul numero della riga da eliminare e *Operazione* impostata su SQL_DELETE.  
  
 Dopo l'eliminazione dei dati, il driver modifica il valore nella matrice di stato della riga di implementazione per la riga appropriata in SQL_ROW_DELETED (o SQL_ROW_ERROR).  
  
## <a name="updating-data-using-sqlsetpos"></a>Aggiornamento dei dati tramite SQLSetPosUpdating Data Using SQLSetPos  
 Un'applicazione può passare il valore di una colonna nel buffer di dati associato o con una o più chiamate a **SQLPutData**. Le colonne i cui dati vengono passati con **SQLPutData** sono note come *colonne* *data-at-execution* . Questi vengono comunemente utilizzati per inviare dati per SQL_LONGVARBINARY e SQL_LONGVARCHAR colonne e possono essere combinati con altre colonne.  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>Per aggiornare i dati con SQLSetPos, un'applicazione:To update data with SQLSetPos, an application:  
  
1.  Inserisce i valori nei buffer di dati e di lunghezza/indicatore associati **a SQLBindCol**:  
  
    -   Per le colonne normali, l'applicazione inserisce il nuovo valore di colonna nel buffer * \*TargetValuePtr* e la lunghezza di tale valore nel buffer * \*di StrLen_or_IndPtr.* Se la riga non deve essere aggiornata, l'applicazione inserisce SQL_ROW_IGNORE nell'elemento di tale riga della matrice di operazioni di riga.  
  
    -   Per le colonne data-at-execution, l'applicazione inserisce un valore definito dall'applicazione, ad esempio il numero di colonna, nel buffer * \*TargetValuePtr.For* data-at-execution columns, the application places an application-defined value, such as the column number, in the TargetValuePtr buffer. Il valore può essere utilizzato in un secondo momento per identificare la colonna.  
  
         L'applicazione inserisce il risultato della macro SQL_LEN_DATA_AT_EXEC(*length*) nel buffer*StrLen_or_IndPtr .* Se il tipo di dati SQL della colonna è SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo di dati specifico dell'origine dati long e il driver restituisce "Y" per il tipo di informazioni SQL_NEED_LONG_DATA_LEN in **SQLGetInfo**, *length* è il numero di byte di dati da inviare per il parametro; in caso contrario, deve essere un valore non negativo e viene ignorato.  
  
2.  Chiama **SQLSetPos** con *l'argomento Operation* impostato su SQL_UPDATE per aggiornare la riga di dati.  
  
    -   Se non sono presenti colonne data-at-execution, il processo è completo.  
  
    -   Se sono presenti colonne data-at-execution, la funzione restituisce SQL_NEED_DATA e procede al passaggio 3.If there are any data-at-execution columns, the function returns SQL_NEED_DATA and proceeds to step 3.  
  
3.  Chiama **SQLParamData** per recuperare l'indirizzo del buffer * \*TargetValuePtr* per la prima colonna data-at-execution da elaborare. **SQLParamData** restituisce SQL_NEED_DATA. L'applicazione recupera il valore definito dall'applicazione dal buffer * \*TargetValuePtr.*  
  
    > [!NOTE]  
    >  Anche se i parametri data-at-execution sono simili alle colonne data-at-execution, il valore restituito da **SQLParamData** è diverso per ognuno.  
  
    > [!NOTE]  
    >  I parametri Data-at-execution sono parametri in un'istruzione SQL per la quale verranno inviati dati con **SQLPutData** quando l'istruzione viene eseguita con **SQLExecDirect** o **SQLExecute**. Sono associati a **SQLBindParameter** o impostando descrittori con **SQLSetDescRec**. Il valore restituito da **SQLParamData** è un valore a 32 bit passato a **SQLBindParameter** nell'argomento *ParameterValuePtr.*  
  
    > [!NOTE]  
    >  Le colonne Data-at-execution sono colonne in un set di righe per le quali verranno inviati dati con **SQLPutData** quando una riga viene aggiornata con **SQLSetPos**. Sono associati a **SQLBindCol**. Il valore restituito da **SQLParamData** è l'indirizzo della riga nel buffer*TargetValuePtr* che viene elaborato.  
  
4.  Chiama **SQLPutData** una o più volte per inviare i dati per la colonna. È necessaria più di una chiamata se tutti i valori dei dati non possono essere restituiti nel buffer * \*TargetValuePtr* specificato in **SQLPutData**; più chiamate a **SQLPutData** per la stessa colonna sono consentite solo quando si inviano dati di tipo carattere C a una colonna con un tipo di dati carattere, binario o specifico dell'origine dati o quando si inviano dati C binari a una colonna con un tipo di dati carattere, binario o specifico dell'origine dati.  
  
5.  Chiama nuovamente **SQLParamData** per segnalare che tutti i dati sono stati inviati per la colonna.  
  
    -   Se sono presenti più colonne data-at-execution, **SQLParamData** restituisce SQL_NEED_DATA e l'indirizzo del buffer *TargetValuePtr* per la successiva colonna data-at-execution da elaborare. L'applicazione ripete i passaggi 4 e 5.  
  
    -   Se non sono presenti altre colonne data-at-execution, il processo è completo. Se l'istruzione è stata eseguita correttamente, **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; se l'esecuzione non è riuscita, restituisce SQL_ERROR. A questo punto, **SQLParamData** può restituire qualsiasi SQLSTATE che può essere restituito da **SQLSetPos**.  
  
 Se i dati sono stati aggiornati, il driver modifica il valore nella matrice di stato della riga di implementazione per la riga appropriata in SQL_ROW_UPDATED.  
  
 Se l'operazione viene annullata o si verifica un errore in **SQLParamData** o **SQLPutData**, dopo **che SQLSetPos** restituisce SQL_NEED_DATA e prima dell'invio dei dati per tutte le colonne data-at-execution, l'applicazione può chiamare solo **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**o **SQLPutData** per l'istruzione o la connessione associata all'istruzione. Se chiama qualsiasi altra funzione per l'istruzione o la connessione associata all'istruzione, la funzione restituisce SQL_ERROR e SQLSTATE HY010 (errore di sequenza di funzione).  
  
 Se l'applicazione chiama **SQLCancel** mentre il driver richiede ancora dati per le colonne data-at-esecuzione, il driver annulla l'operazione. L'applicazione può quindi chiamare **SQLSetPos** nuovamente; l'annullamento non influisce sullo stato del cursore o sulla posizione corrente del cursore.  
  
 Quando l'elenco SELECT della specifica di query associata al cursore contiene più di un riferimento alla stessa colonna, se viene generato un errore o se il driver ignora i riferimenti duplicati ed esegue le operazioni richieste è definito dal driver.  
  
## <a name="performing-bulk-operations"></a>Esecuzione di operazioni collettivePerforming Bulk Operations  
 Se l'argomento *RowNumber* è 0, il driver esegue l'operazione specificata nell'argomento *Operation* per ogni riga del set di righe il cui valore è SQL_ROW_PROCEED nel relativo campo della matrice di operazioni di riga a cui punta SQL_ATTR_ROW_OPERATION_PTRattributo istruzione. Si tratta di un valore valido dell'argomento *RowNumber* per un argomento *Operation* di SQL_DELETE, SQL_REFRESH o SQL_UPDATE, ma non SQL_POSITION. **SQLSetPos** con *un'operazione* di SQL_POSITION e un *RowNumber* uguale a 0 restituirà SQLSTATE HY109 (posizione del cursore non valido).  
  
 Se si verifica un errore relativo all'intero set di righe, ad esempio SQLSTATE HYT00 (Timeout scaduto), il driver restituisce SQL_ERROR e l'istruzione SQLSTATE appropriata. Il contenuto dei buffer del set di righe non è definito e la posizione del cursore non è modificata.  
  
 Se si verifica un errore relativo a una singola riga, il driver:  
  
-   Imposta su SQL_ROW_ERROR l'elemento per la riga nella matrice di stato della riga a cui fa riferimento l'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR.  
  
-   Pubblica uno o più SQLSTATE aggiuntivi per l'errore nella coda degli errori e imposta il campo SQL_DIAG_ROW_NUMBER nella struttura dei dati di diagnostica.  
  
 Dopo aver elaborato l'errore o l'avviso, se il driver completa l'operazione per le righe rimanenti nel set di righe, restituisce SQL_SUCCESS_WITH_INFO. Pertanto, per ogni riga che ha restituito un errore, la coda degli errori contiene zero o più SQLSTATE aggiuntivi. Se il driver interrompe l'operazione dopo aver elaborato l'errore o l'avviso, restituisce SQL_ERROR.  
  
 Se il driver restituisce avvisi, ad esempio SQLSTATE 01004 (dati troncati), restituisce avvisi che si applicano all'intero set di righe o a righe sconosciute nel set di righe prima di restituire le informazioni sull'errore che si applicano a righe specifiche. Restituisce avvisi per righe specifiche insieme a qualsiasi altra informazione di errore su tali righe.  
  
 Se *RowNumber* è uguale a 0 e *Operation* è SQL_UPDATE, SQL_REFRESH o SQL_DELETE, il numero di righe a cui opera **SQLSetPos** fa riferimento all'attributo dell'istruzione SQL_ATTR_ROWS_FETCHED_PTR.  
  
 Se *RowNumber* è uguale a 0 e *Operation* è SQL_DELETE, SQL_REFRESH o SQL_UPDATE, la riga corrente dopo l'operazione è uguale alla riga corrente prima dell'operazione.  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>Ignorare una riga in un'operazione in blocco  
 La matrice di operazioni di riga può essere utilizzata per indicare che una riga nel set di righe corrente deve essere ignorata durante un'operazione in blocco utilizzando **SQLSetPos**. Per indicare al driver di ignorare una o più righe durante un'operazione in blocco, un'applicazione deve eseguire la procedura seguente:  
  
1.  Chiamare **SQLSetStmtAttr** per impostare l'attributo dell'istruzione SQL_ATTR_ROW_OPERATION_PTR in modo che punti a una matrice di SQLUSMALLINT. Questo campo può essere impostato anche chiamando **SQLSetDescField** per impostare il campo di intestazione SQL_DESC_ARRAY_STATUS_PTR dell'ARD, che richiede che un'applicazione ottenga l'handle del descrittore.  
  
2.  Impostare ogni elemento della matrice di operazioni di riga su uno dei due valori seguenti:  
  
    -   SQL_ROW_IGNORE, per indicare che la riga è esclusa per l'operazione in blocco.  
  
    -   SQL_ROW_PROCEED, per indicare che la riga è inclusa nell'operazione in blocco. Si tratta del valore predefinito.  
  
3.  Chiamare **SQLSetPos** per eseguire l'operazione in blocco.  
  
 Le regole seguenti si applicano alla matrice di operazioni di riga:  
  
-   SQL_ROW_IGNORE e SQL_ROW_PROCEED interessano solo le operazioni bulk **utilizzando SQLSetPos** con *un'operazione* di SQL_DELETE o SQL_UPDATE. Non influiscono sulle chiamate a **SQLSetPos** con *un'operazione* di SQL_REFRESH o SQL_POSITION.  
  
-   Il puntatore è impostato su null per impostazione predefinita.  
  
-   Se il puntatore è null, tutte le righe vengono aggiornate come se tutti gli elementi fossero impostati su SQL_ROW_PROCEED.  
  
-   L'impostazione di un elemento su SQL_ROW_PROCEED non garantisce che l'operazione verrà eseguita su quella particolare riga. Ad esempio, se una determinata riga nel set di righe ha lo stato SQL_ROW_ERROR, il driver potrebbe non essere in grado di aggiornare tale riga indipendentemente dal fatto che l'applicazione abbia specificato SQL_ROW_PROCEED. Un'applicazione deve sempre controllare la matrice di stato della riga per verificare se l'operazione è stata eseguita correttamente.  
  
-   SQL_ROW_PROCEED è definito come 0 nel file di intestazione. Un'applicazione può inizializzare la matrice di operazioni di riga su 0 per elaborare tutte le righe.  
  
-   Se il numero di elemento "n" nella matrice di operazioni di riga è impostato su SQL_ROW_IGNORE e **SQLSetPos** viene chiamato per eseguire un'operazione di aggiornamento o eliminazione in blocco, l'ennesima riga nel set di righe rimane invariata dopo la chiamata a **SQLSetPos**.  
  
-   Un'applicazione deve impostare automaticamente una colonna di sola lettura su SQL_ROW_IGNORE.  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>Ignorare una colonna in un'operazione in blocco  
 Per evitare che la diagnostica di elaborazione non necessaria generata dai tentativi di aggiornamento a una o più colonne di sola lettura, un'applicazione può impostare il valore nel buffer di lunghezza/indicatore associato su SQL_COLUMN_IGNORE. Per ulteriori informazioni, vedere [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, un'applicazione consente a un utente di esplorare la tabella ORDERS e aggiornare lo stato dell'ordine. Il cursore è basato su keyset con una dimensione del set di righe pari a 20 e utilizza il controllo della concorrenza ottimistica per confrontare le versioni di riga. Dopo il recupero di ogni set di righe, l'applicazione lo stampa e consente all'utente di selezionare e aggiornare lo stato di un ordine. L'applicazione utilizza **SQLSetPos** per posizionare il cursore sulla riga selezionata ed esegue un aggiornamento posizionato della riga. (La gestione degli errori viene omessa per maggiore chiarezza.)  
  
```cpp  
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
  
 Per altri esempi, vedere [Istruzioni di aggiornamento ed eliminazione posizionate](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) e Aggiornamento di righe nel set di righe con [SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Esecuzione di operazioni bulk non correlate alla posizione del cursore a blocchiPerforming bulk operations that do not relate to the block cursor position|[Funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Recupero di un blocco di dati o scorrimento di un set di risultati|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Ottenere un singolo campo di un descrittoreGetting a single field of a descriptor|[Funzione SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Recupero di più campi di un descrittoreGetting multiple fields of a descriptor|[Funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Impostazione di un singolo campo di un descrittore|[Funzione SQLSetDescFieldSQLSetDescField Function](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Impostazione di più campi di un descrittore|[Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Impostazione di un attributo di istruzioneSetting a statement attribute|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
