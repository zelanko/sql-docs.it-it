---
title: Funzione SQLFetchScroll . Documenti Microsoft
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6c65ef71f5c2cb9202ab788cac5e00357674f4a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285881"
---
# <a name="sqlfetchscroll-function"></a>Funzione SQLFetchScroll
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLFetchScroll** recupera il set di righe specificato di dati dal set di risultati e restituisce i dati per tutte le colonne associate. I set di righe possono essere specificati in una posizione assoluta o relativa o in base al segnalibro.  
  
 Quando si utilizza un driver ODBC 2.x, Gestione Driver esegue il mapping di questa funzione a **SQLExtendedFetch**. Per ulteriori informazioni, vedere Mapping delle funzioni di sostituzione per la [compatibilità con le applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)con le versioni precedenti.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *Orientamento Fetch*  
 [Ingresso]  
  
 Tipo di recupero:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 Per ulteriori informazioni, vedere "Posizionamento del cursore" nella sezione "Commenti".  
  
 *RecuperaOffset*  
 [Ingresso]  
  
 Numero della riga da recuperare. L'interpretazione di questo argomento dipende dal valore dell'argomento *FetchOrientation.* Per ulteriori informazioni, vedere "Posizionamento del cursore" nella sezione "Commenti".  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLFetchScroll** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un HandleType di SQL_HANDLE_STMT e un Handle di StatementHandle. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLFetchScroll** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente. Se si verifica un errore in una singola colonna, **SQLGetDiagField** può essere chiamato con un DiagIdentifier di SQL_DIAG_COLUMN_NUMBER per determinare la colonna in cui si è verificato l'errore; e **SQLGetDiagField** può essere chiamato con un DiagIdentifier di SQL_DIAG_ROW_NUMBER per determinare la riga contenente tale colonna.  
  
 Per tutti gli SQLSTATE che possono restituire SQL_SUCCESS_WITH_INFO o SQL_ERROR (ad eccezione di 01xxx SQLSTATEs), viene restituito SQL_SUCCESS_WITH_INFO se si verifica un errore in uno o più, ma non in tutte le righe di un'operazione multiriga, e SQL_ERROR viene restituito se si verifica un errore in un'operazione a riga singola.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Dati stringa o binari restituiti per una colonna hanno determinato il troncamento di caratteri non vuoti o dati binari non NULL. Se si tratta di un valore stringa, è stato troncato a destra.|  
|01S01 (in questo stato di|Errore nella riga|Si è verificato un errore durante il recupero di una o più righe.<br /><br /> (Se questo SQLSTATE viene restituito quando un'applicazione ODBC 3 *.x* utilizza un driver *.x* ODBC 2, può essere ignorato.)|  
|01S06 (in inglese)|Tentativo di recupero prima che il set di risultati restituisca il primo set di righe|Il set di righe richiesto si sovrapponeva all'inizio del set di risultati quando FetchOrientation era SQL_FETCH_PRIOR, la posizione corrente era oltre la prima riga e il numero della riga corrente è minore o uguale alla dimensione del set di righe.<br /><br /> Il set di righe richiesto si sovrapponeva all'inizio del set di risultati quando FetchOrientation era SQL_FETCH_PRIOR, la posizione corrente era oltre la fine del set di risultati e la dimensione del set di righe era maggiore della dimensione del set di risultati.<br /><br /> Il set di righe richiesto si sovrapponeva all'inizio del set di risultati quando FetchOrientation era SQL_FETCH_RELATIVE, FetchOffset era negativo e il valore assoluto di FetchOffset era minore o uguale alla dimensione del set di righe.<br /><br /> Il set di righe richiesto si sovrapponeva all'inizio del set di risultati quando FetchOrientation era SQL_FETCH_ABSOLUTE, FetchOffset era negativo e il valore assoluto di FetchOffset era maggiore della dimensione del set di risultati ma minore o uguale alla dimensione del set di righe.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S07 (intito)|Troncamento frazionario|I dati restituiti per una colonna sono stati troncati. Per i tipi di dati numerici, la parte frazionaria del numero è stata troncata. Per i tipi di dati time, timestamp e interval contenenti un componente time, la parte frazionaria dell'ora è stata troncata.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07006|Violazione dell'attributo del tipo di dati con restrizioniRestricted data type attribute violation|Impossibile convertire il valore dei dati di una colonna nel set di risultati nel tipo di dati specificato da *TargetType* in **SQLBindCol**.<br /><br /> La colonna 0 è stata associata a un tipo di dati SQL_C_BOOKMARK e l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_VARIABLE.<br /><br /> La colonna 0 era associata a un tipo di dati di SQL_C_VARBOOKMARK e l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS non è stato impostato su SQL_UB_VARIABLE.|  
|07009|Indice descrittore non valido|Il driver era un driver *.x* ODBC 2 che non supporta **SQLExtendedFetch**e un numero di colonna specificato nell'associazione per una colonna era 0.<br /><br /> La colonna 0 è stata associata e l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_OFF.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|22001|Dati stringa troncati a destra|Un segnalibro di lunghezza variabile restituito per una colonna è stato troncato.|  
|22002|Variabile indicatore richiesta ma non fornita|I dati NULL sono stati recuperati in una colonna il cui *StrLen_or_IndPtr* impostato da **SQLBindCol** (o SQL_DESC_INDICATOR_PTR impostato da **SQLSetDescField** o **SQLSetDescRec**) era un puntatore null.|  
|22003|Valore numerico non compreso nell'intervallo|La restituzione del valore numerico (come numerico o stringa) per una o più colonne associate avrebbe causato il troncamento dell'intera parte (anziché frazionaria) del numero.<br /><br /> Per ulteriori informazioni, vedere [Conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) [nell'Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato datetime non valido|Una colonna di caratteri nel set di risultati è stata associata a una data, ora o timestamp C struttura e un valore nella colonna è stato, rispettivamente, una data, ora o timestamp non valido.|  
|22012|Divisione per zero|È stato restituito un valore da un'espressione aritmetica, che ha restituito la divisione per zero.|  
|22015|Overflow campo intervallo|L'assegnazione da un tipo SQL esatto numero o intervallo a un tipo di intervallo C ha causato una perdita di cifre significative nel campo iniziale.<br /><br /> Durante il recupero dei dati in un tipo di intervallo C, non esisteva alcuna rappresentazione del valore del tipo SQL nel tipo di intervallo C.|  
|22018|Valore di carattere non valido per la specifica del cast|Una colonna di caratteri nel set di risultati è stata associata a un buffer di caratteri C e la colonna contiene un carattere per il quale non era presente alcuna rappresentazione nel set di caratteri del buffer.<br /><br /> Il tipo C era un numero esatto o approssimativo, un datetime o un tipo di dati interval; il tipo SQL della colonna era un tipo di dati carattere; e il valore nella colonna non è un valore letterale valido del tipo C associato.|  
|24000|Stato del cursore non valido|*StatementHandle* era in uno stato eseguito ma non era associato alcun set di risultati a *StatementHandle*.|  
|40001|Errore di serializzazione|La transazione in cui è stato eseguito il recupero è stata terminata per evitare deadlock.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*. Quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLFetchScroll.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) *L'oggetto statementHandle* specificato non era in uno stato eseguito. La funzione è stata chiamata senza prima chiamare **SQLExecDirect**, **SQLExecute** o una funzione di catalogo.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) **SQLFetch** è stato chiamato per il *StatementHandle* dopo **SQLExtendedFetch** è stato chiamato e prima **di SQLFreeStmt** con il SQL_CLOSE opzione è stata chiamata.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|L'attributo dell'istruzione SQL_ATTR_USE_BOOKMARK è stato impostato su SQL_UB_VARIABLE e la colonna 0 è stata associata a un buffer la cui lunghezza non è uguale alla lunghezza massima per il segnalibro per il set di risultati. Questa lunghezza è disponibile nel campo SQL_DESC_OCTET_LENGTH dell'IRD e può essere ottenuta chiamando **SQLDescribeCol**, **SQLColAttribute**o **SQLGetDescField**.|  
|I106|Tipo di recupero non compreso nell'intervallo|DM) Il valore specificato per l'argomento FetchOrientation non è valido.<br /><br /> (DM) l'argomento FetchOrientation è stato SQL_FETCH_BOOKMARK e l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_OFF.<br /><br /> Il valore dell'attributo di istruzione SQL_ATTR_CURSOR_TYPE è stato SQL_CURSOR_FORWARD_ONLY e il valore dell'argomento FetchOrientation non è stato SQL_FETCH_NEXT.<br /><br /> Il valore dell'attributo di istruzione SQL_ATTR_CURSOR_SCROLLABLE è stato SQL_NONSCROLLABLE e il valore dell'argomento FetchOrientation non è SQL_FETCH_NEXT.|  
|I107|Valore di riga non compreso nell'intervallo|Il valore specificato con l'attributo di istruzione SQL_ATTR_CURSOR_TYPE è stato SQL_CURSOR_KEYSET_DRIVEN, ma il valore specificato con l'attributo di istruzione SQL_ATTR_KEYSET_SIZE è maggiore di 0 e minore del valore specificato con l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE.|  
|HY111|Valore segnalibro non valido|L'argomento FetchOrientation è stato SQL_FETCH_BOOKMARK e il segnalibro a cui fa riferimento il valore nell'attributo di istruzione SQL_ATTR_FETCH_BOOKMARK_PTR non è valido o era un puntatore null.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il driver o l'origine dati non supporta la conversione specificata dalla combinazione di *TargetType* in **SQLBindCol** e il tipo di dati SQL della colonna corrispondente.|  
|HYT00|Timeout|Il periodo di timeout della query è scaduto prima che l'origine dati restituisca il set di risultati richiesto. Il periodo di timeout viene impostato tramite SQLSetStmtAttr SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **SQLFetchScroll** restituisce un set di righe specificato dal set di risultati. I set di righe possono essere specificati dalla posizione assoluta o relativa o dal segnalibro. **SQLFetchScroll** può essere chiamato solo mentre esiste un set di risultati, ovvero dopo una chiamata che crea un set di risultati e prima che il cursore su tale set di risultati venga chiuso. Se le colonne sono associate, vengono restituiti i dati in tali colonne. Se l'applicazione ha specificato un puntatore a una matrice di stato di riga o un buffer in cui restituire il numero di righe recuperate, **SQLFetchScroll** restituisce anche queste informazioni. Le chiamate a **SQLFetchScroll** possono essere mescolate con chiamate a **SQLFetch,** ma non possono essere mescolate con chiamate a **SQLExtendedFetch**.  
  
 Per ulteriori informazioni, consultate [Utilizzo dei cursori](../../../odbc/reference/develop-app/using-block-cursors.md) a blocchi e [Utilizzo dei cursori scorrevoli.](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
## <a name="positioning-the-cursor"></a>Posizionamento del cursore  
 Quando viene creato il set di risultati, il cursore viene posizionato prima dell'inizio del set di risultati. **SQLFetchScroll** posiziona il cursore di blocco in base ai valori degli argomenti *FetchOrientation* e *FetchOffset,* come illustrato nella tabella seguente. Le regole esatte per determinare l'inizio del nuovo set di righe sono illustrate nella sezione successiva.  
  
|Orientamento Fetch|Significato|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|Restituire il set di righe successivo. Equivale a chiamare **SQLFetch**.<br /><br /> **SQLFetchScroll** ignora il valore di *FetchOffset*.|  
|SQL_FETCH_PRIOR|Restituire il set di righe precedente.<br /><br /> **SQLFetchScroll** ignora il valore di *FetchOffset*.|  
|SQL_FETCH_RELATIVE|Restituire il set di righe *FetchOffset* dall'inizio del set di righe corrente.|  
|SQL_FETCH_ABSOLUTE|Restituire il set di righe a partire dalla riga *FetchOffset*.|  
|SQL_FETCH_FIRST|Restituire il primo set di righe nel set di risultati.<br /><br /> **SQLFetchScroll** ignora il valore di *FetchOffset*.|  
|SQL_FETCH_LAST|Restituisce l'ultimo set di righe completo nel set di risultati.<br /><br /> **SQLFetchScroll** ignora il valore di *FetchOffset*.|  
|SQL_FETCH_BOOKMARK|Restituisce il set di righe FetchOffset righe dal segnalibro specificato dall'attributo di istruzione SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
 I driver non sono tenuti a supportare tutti gli orientamenti di recupero; un'applicazione chiama **SQLGetInfo** con un tipo di informazioni di SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (a seconda del tipo di cursore) per determinare quali orientamenti di recupero sono supportati dal driver. L'applicazione deve esaminare le maschere di bit SQL_CA1_NEXT, SQL_CA1_RELATIVE, SQL_CA1_ABSOLUTE e WQL_CA1_BOOKMARK in questi tipi di informazioni. Inoltre, se il cursore è forward-only e FetchOrientation non è SQL_FETCH_NEXT, **SQLFetchScroll** restituisce SQLSTATE HY106 (tipo Fetch non compreso nell'intervallo).  
  
 L'attributo SQL_ATTR_ROW_ARRAY_SIZE'istruzione specifica il numero di righe nel set di righe. Se il set di righe recuperato da **SQLFetchScroll** si sovrappone alla fine del set di risultati, **SQLFetchScroll** restituisce un set di righe parziale. Ovvero, se S - R - 1 è maggiore di L, dove S è la riga iniziale del set di righe da recuperare, R è la dimensione del set di righe e L è l'ultima riga nel set di risultati, solo le prime righe L - S - 1 del set di righe sono valide. Le righe rimanenti sono vuote e hanno lo stato SQL_ROW_NOROW.  
  
 Dopo **SQLFetchScroll** restituisce, la riga corrente è la prima riga del set di righe.  
  
## <a name="cursor-positioning-rules"></a>Regole di posizionamento del cursoreCursor Positioning Rules  
 The following sections describe the exact rules for each value of FetchOrientation. Queste regole utilizzano la notazione seguente.  
  
|Notation|Significato|  
|--------------|-------------|  
|*Prima dell'inizio*|Il cursore di blocco viene posizionato prima dell'inizio del set di risultati. Se la prima riga del nuovo set di righe è prima dell'inizio del set di risultati, **SQLFetchScroll** restituisce SQL_NO_DATA.|  
|*Dopo la fine*|Il cursore di blocco viene posizionato dopo la fine del set di risultati. Se la prima riga del nuovo set di righe è dopo la fine del set di risultati, **SQLFetchScroll** restituisce SQL_NO_DATA.|  
|*CurrRowsetStart (Esempio di currRowsetStart)*|Numero della prima riga nel set di righe corrente.|  
|*LastResultRow*|Numero dell'ultima riga nel set di risultati.|  
|*RowsetSize (Dimensioni Set di righe)*|Dimensioni del set di righe.|  
|*RecuperaOffset*|Valore dell'argomento *FetchOffset.*|  
|*Riga di segnalibro*|Riga corrispondente al segnalibro specificato dall'attributo di istruzione SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
## <a name="sql_fetch_next"></a>SQL_FETCH_NEXT  
 Si applicano le seguenti regole.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*Prima dell'inizio*|1|  
|*CurrRowsetStart : RowsetSize*[1] * \<- LastResultRow*|*CurrRowsetStart : RowsetSize*[1]|  
|*CurrRowsetStart : RowsetSize*[1]*> LastResultRow*|*Dopo la fine*|  
|*Dopo la fine*|*Dopo la fine*|  
  
 [1] Se la dimensione del set di righe è stata modificata dopo la chiamata precedente per recuperare le righe, si tratta della dimensione del set di righe utilizzata con la chiamata precedente.  
  
## <a name="sql_fetch_prior"></a>SQL_FETCH_PRIOR  
 Si applicano le seguenti regole.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*Prima dell'inizio*|*Prima dell'inizio*|  
|*CurrRowsetStart - 1*|*Prima dell'inizio*|  
|*1 < <CurrRowsetStart - RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart - RowsetSize* <sup>[2]</sup>|  
|*Dopo la fine AND LastResultRow < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*Dopo la fine E LastResultRow >: RowsetSize* <sup>[2]</sup>|*LastResultRow - RowsetSize : 1* <sup>[2]</sup>|  
  
 [1] **SQLFetchScroll** restituisce SQLSTATE 01S06 (tentativo di recupero prima che il set di risultati restituisse il primo set di righe) e SQL_SUCCESS_WITH_INFO.  
  
 [2] Se la dimensione del set di righe è stata modificata dopo la chiamata precedente per recuperare le righe, si tratta della nuova dimensione del set di righe.  
  
## <a name="sql_fetch_relative"></a>SQL_FETCH_RELATIVE  
 Si applicano le seguenti regole.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*(Prima dell'avvio E > 0) OR (Dopo la fine E il < 0)*|*--*<sup>[1]</sup>|  
|*<beforeStart E FetchOffset : 0*|*Prima dell'inizio*|  
|*CurrRowsetStart - 1 E < FetchOffset 0*|*Prima dell'inizio*|  
|*CurrRowsetStart > 1 E CurrRowsetStart : FetchOffset < 1 E &#124; FetchOffset &#124; > RowsetSize* <sup>[3]</sup>|*Prima dell'inizio*|  
|*CurrRowsetStart > 1 E CurrRowsetStart : FetchOffset < 1 E &#124; FetchOffset &#124; <: RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 <: CurrRowsetStart \<, FetchOffset , LastResultRow*|*CurrRowsetStart - FetchOffset*|  
|*CurrRowsetStart - FetchOffset > LastResultRow*|*Dopo la fine*|  
|*Dopo la fine E >FetchOffset 0*|*Dopo la fine*|  
  
 [1] ***SQLFetchScroll*** restituisce lo stesso set di righe come se fosse stato chiamato con FetchOrientation impostato su SQL_FETCH_ABSOLUTE. Per ulteriori informazioni, vedere la sezione "SQL_FETCH_ABSOLUTE".  
  
 [2] **SQLFetchScroll** restituisce SQLSTATE 01S06 (Tentativo di recupero prima che il set di risultati restituisse il primo set di righe) e SQL_SUCCESS_WITH_INFO.  
  
 [3] Se la dimensione del set di righe è stata modificata dopo la chiamata precedente per recuperare le righe, si tratta della nuova dimensione del set di righe.  
  
## <a name="sql_fetch_absolute"></a>SQL_FETCH_ABSOLUTE  
 Si applicano le seguenti regole.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*FetchOffset < 0 E &#124; &#124; <FetchOffset - LastResultRow*|*LastResultRow ( ) , ) e 1*|  
|*FetchOffset < 0 E &#124; &#124; > FetchOffset LastResultRow E &#124; FetchOffset &#124; > RowsetSize* <sup>[2]</sup>|*Prima dell'inizio*|  
|*FetchOffset < 0 E &#124; FetchOffset &#124; > LastResultRow E &#124; la &#124; <FetchOffset - RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset - 0*|*Prima dell'inizio*|  
|*1 <: \<FetchOffset - LastResultRow*|*RecuperaOffset*|  
|*FetchOffset > LastResultRow*|*Dopo la fine*|  
  
 [1] **SQLFetchScroll** restituisce SQLSTATE 01S06 (tentativo di recupero prima che il set di risultati restituisse il primo set di righe) e SQL_SUCCESS_WITH_INFO.  
  
 [2] Se la dimensione del set di righe è stata modificata dopo la chiamata precedente per recuperare le righe, si tratta della nuova dimensione del set di righe.  
  
 Un recupero assoluto eseguito su un cursore dinamico non può fornire il risultato richiesto perché le posizioni delle righe in un cursore dinamico non sono determinate. Tale operazione è equivalente a un recupero prima seguito da un parente fetch; non è un'operazione atomica, come è un recupero assoluto su un cursore statico.  
  
## <a name="sql_fetch_first"></a>SQL_FETCH_FIRST  
 Si applicano le seguenti regole.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*qualsiasi*|*1*|  
  
## <a name="sql_fetch_last"></a>SQL_FETCH_LAST  
 Si applicano le seguenti regole.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*Proprietà Set di righe* <sup>[1]</sup> <- LastResultRow|*LastResultRow - RowsetSize : 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] Se la dimensione del set di righe è stata modificata dopo la chiamata precedente per recuperare le righe, si tratta della nuova dimensione del set di righe.  
  
## <a name="sql_fetch_bookmark"></a>SQL_FETCH_BOOKMARK  
 Si applicano le seguenti regole.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*< di BookmarkRow e FetchOffset 1*|*Prima dell'inizio*|  
|*1 <, BookmarkRow \<, FetchOffset , LastResultRow*|*BookmarkRow - FetchOffset*|  
|*BookmarkRow - FetchOffset > LastResultRow*|*Dopo la fine*|  
  
 Per informazioni sui segnalibri, vedere [Segnalibri (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>Effetto delle righe eliminate, aggiunte e di errore sul movimento del cursore  
 I cursori statici e basati su keyset talvolta rilevano le righe aggiunte al set di risultati e rimuovono le righe eliminate dal set di risultati. Chiamando **SQLGetInfo** con le opzioni SQL_STATIC_CURSOR_ATTRIBUTES2 e SQL_KEYSET_CURSOR_ATTRIBUTES2 e esaminando le maschere di bit SQL_CA2_SENSITIVITY_ADDITIONS, SQL_CA2_SENSITIVITY_DELETIONS e SQL_CA2_SENSITIVITY_UPDATES, un'applicazione determina se i cursori implementati da un driver specifico eseguire questa operazione. Per i driver in grado di rilevare le righe eliminate e rimuoverle, i paragrafi seguenti descrivono gli effetti di questo comportamento. Per i driver in grado di rilevare le righe eliminate ma non rimuoverle, le eliminazioni non hanno alcun effetto sui movimenti del cursore e i paragrafi seguenti non vengono applicati.  
  
 Se il cursore rileva le righe aggiunte al set di risultati o rimuove le righe eliminate dal set di risultati, viene visualizzato come se rilevasse queste modifiche solo quando recupera i dati. Ciò include il caso in cui **SQLFetchScroll** viene chiamato con FetchOrientation impostato su SQL_FETCH_RELATIVE e FetchOffset impostato su 0 per recuperare nuovamente lo stesso set di righe, ma non include il caso in cui SQLSetPos viene chiamato con fOption impostato su SQL_REFRESH. In quest'ultimo caso, i dati nei buffer del set di righe vengono aggiornati, ma non recuperati e le righe eliminate non vengono rimosse dal set di risultati. Pertanto, quando una riga viene eliminata o inserita nel set di righe corrente, il cursore non modifica i buffer del set di righe. Al contrario, rileva la modifica quando recupera qualsiasi set di righe che in precedenza includeva la riga eliminata o che ora include la riga inserita.  
  
 Ad esempio:  
  
```cpp  
// Fetch the next rowset.  
SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
// Delete third row of the rowset. Does not modify the rowset buffers.  
SQLSetPos(hstmt, 3, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
// The third row has a status of SQL_ROW_DELETED after this call.  
SQLSetPos(hstmt, 3, SQL_REFRESH, SQL_LOCK_NO_CHANGE);  
// Refetch the same rowset. The third row is removed, replaced by what  
// was previously the fourth row.  
SQLFetchScroll(hstmt, SQL_FETCH_RELATIVE, 0);  
```  
  
 Quando **SQLFetchScroll** restituisce un nuovo set di righe con una posizione relativa al set di righe corrente, ovvero FetchOrientation è SQL_FETCH_NEXT, SQL_FETCH_PRIOR o SQL_FETCH_RELATIVE, non include modifiche al set di righe corrente durante il calcolo della posizione iniziale del nuovo set di righe. Tuttavia, include le modifiche all'esterno del set di righe corrente se è in grado di rilevarle. Inoltre, quando **SQLFetchScroll** restituisce un nuovo set di righe con una posizione indipendente dal set di righe corrente, ovvero FetchOrientation è SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE o SQL_FETCH_BOOKMARK, include tutte le modifiche che è in grado di rilevare, anche se si trovano nel set di righe corrente.  
  
 Quando si determina se le righe appena aggiunte si trovano all'interno o all'esterno del set di righe corrente, un set di righe parziale viene considerato terminato all'ultima riga valida. ovvero l'ultima riga per la quale lo stato della riga non è SQL_ROW_NOROW. Si supponga, ad esempio, che il cursore sia in grado di rilevare le righe appena aggiunte, che il set di righe corrente sia un set di righe parziale, che l'applicazione aggiunga nuove righe e che il cursore aggiunga queste righe alla fine del set di risultati. Se l'applicazione chiama **SQLFetchScroll** con FetchOrientation impostato su SQL_FETCH_NEXT, **SQLFetchScroll** restituisce il set di righe a partire dalla prima riga appena aggiunta.  
  
 Si supponga, ad esempio, che il set di righe corrente comprenda le righe da 21 a 30, che la dimensione del set di righe sia 10, che il cursore rimuova le righe eliminate dal set di risultati e che il cursore rilevi le righe aggiunte al set di risultati. Nella tabella seguente vengono illustrate le righe restituite da **SQLFetchScroll** in varie situazioni.  
  
|Modifica|Tipo di recupero|RecuperaOffset|Nuovo set di righe[1]|  
|------------|----------------|-----------------|---------------------|  
|Elimina riga 21|NEXT|0|Da 31 a 40 anni|  
|Elimina riga 31|NEXT|0|Da 32 a 41 anni|  
|Inserisci riga tra le righe 21 e 22|NEXT|0|Da 31 a 40 anni|  
|Inserisci riga tra le righe 30 e 31|NEXT|0|Riga inserita, da 31 a 39|  
|Elimina riga 21|PRIOR|0|Da 11 a 20 anni|  
|Elimina riga 20|PRIOR|0|Da 10 a 19 anni|  
|Inserisci riga tra le righe 21 e 22|PRIOR|0|Da 11 a 20 anni|  
|Inserisci riga tra le righe 20 e 21|PRIOR|0|12 a 20, riga inserita|  
|Elimina riga 21|RELATIVE|0|Da 22 a 31<sup>[2]</sup>|  
|Elimina riga 21|RELATIVE|1|Da 22 a 31 anni|  
|Inserisci riga tra le righe 21 e 22|RELATIVE|0|21, riga inserita, da 22 a 29|  
|Inserisci riga tra le righe 21 e 22|RELATIVE|1|Da 22 a 31 anni|  
|Elimina riga 21|ABSOLUTE|21|Da 22 a 31<sup>[2]</sup>|  
|Riga di eliminazione 22|ABSOLUTE|21|21, 23 a 31|  
|Inserisci riga tra le righe 21 e 22|ABSOLUTE|22|Riga inserita, da 22 a 29|  
  
 [1] Questa colonna utilizza i numeri di riga prima dell'inserimento o dell'eliminazione di qualsiasi riga.  
  
 [2] In questo caso, il cursore tenta di restituire le righe che iniziano con la riga 21. Poiché la riga 21 è stata eliminata, la prima riga restituita è la riga 22.  
  
 Le righe di errore, ovvero le righe con stato SQL_ROW_ERROR, non influiscono sullo spostamento del cursore. Ad esempio, se il set di righe corrente inizia con la riga 11 e lo stato della riga 11 è SQL_ROW_ERROR, la chiamata di **SQLFetchScroll** con FetchOrientation impostato su SQL_FETCH_RELATIVE e FetchOffset impostato su 5 restituisce il set di righe a partire dalla riga 16, proprio come se lo stato per la riga 11 fosse SQL_SUCCESS.  
  
## <a name="returning-data-in-bound-columns"></a>Restituzione di dati nelle colonne associateReturning Data in Bound Columns  
 **SQLFetchScroll** restituisce i dati nelle colonne associate nello stesso modo di **SQLFetch**. Per ulteriori informazioni, vedere "Restituzione di dati in colonne associate" in [Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Se nessuna colonna è associata, **SQLFetchScroll** non restituisce dati ma sposta il cursore di blocco nella posizione specificata. Se i dati possono essere recuperati da colonne non associate di un cursore a blocchi con **SQLGetData** dipende dal driver. Questa funzionalità è supportata se una chiamata a **SQLGetInfo** restituisce il bit di SQL_GD_BLOCK per il tipo di informazioni SQL_GETDATA_EXTENSIONS.  
  
## <a name="buffer-addresses"></a>Indirizzi buffer  
 **SQLFetchScroll** utilizza la stessa formula per determinare l'indirizzo dei buffer di dati e di lunghezza/indicatore come **SQLFetch**. Per ulteriori informazioni, vedere "Indirizzi del buffer" nella [funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="row-status-array"></a>Matrice di stato riga  
 **SQLFetchScroll** imposta i valori nella matrice di stato della riga nello stesso modo di SQLFetch. Per ulteriori informazioni, vedere "Matrice di stato delle righe" nella [funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="rows-fetched-buffer"></a>Righe recuperate Buffer  
 **SQLFetchScroll** restituisce il numero di righe recuperate nel buffer delle righe recuperate nello stesso modo di **SQLFetch**. Per ulteriori informazioni, vedere "Righe recuperate nel buffer" in [Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="error-handling"></a>Gestione degli errori  
 Quando un'applicazione chiama **SQLFetchScroll** in un driver ODBC 3.x, Gestione Driver chiama **SQLFetchScroll** nel driver. Quando un'applicazione chiama **SQLFetchScroll** in un driver ODBC 2.x, Gestione Driver chiama SQLExtendedFetch nel driver. Poiché **SQLFetchScroll** e SQLExtendedFetch gestiscono gli errori in modo leggermente diverso, l'applicazione vede un comportamento di errore leggermente diverso quando chiama **SQLFetchScroll** nei driver ODBC 2.x e ODBC 3.x.  
  
 **SQLFetchScroll** restituisce errori e avvisi nello stesso modo di **SQLFetch**; Per ulteriori informazioni, vedere "Gestione degli errori" in **SQLFetch**. **SQLExtendedFetch** restituisce gli errori nello stesso modo di **SQLFetch**, con le seguenti eccezioni:  
  
 Quando si verifica un avviso che si applica a una determinata riga nel set di righe, SQLExtendedFetch imposta la voce corrispondente nella matrice di stato della riga su SQL_ROW_SUCCESS, non SQL_ROW_SUCCESS_WITH_INFO.  
  
 Se si verificano errori in ogni riga del set di righe, SQLExtendedFetch restituisce SQL_SUCCESS_WITH_INFO, non SQL_ERROR.  
  
 In ogni gruppo di record di stato che si applica a una singola riga, il primo record di stato restituito da SQLExtendedFetch deve contenere SQLSTATE 01S01 (errore nella riga); **SQLFetchScroll** non restituisce questo SQLSTATE. Se SQLExtendedFetch non è in grado di restituire SQLSTATEs aggiuntivi, deve comunque restituire questo SQLSTATE.  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll e concorrenza ottimistica  
 Se un cursore utilizza la concorrenza ottimistica, ovvero l'attributo dell'istruzione SQL_ATTR_CONCURRENCY ha un valore di SQL_CONCUR_VALUES o SQL_CONCUR_ROWVER, **SQLFetchScroll** aggiorna i valori di concorrenza ottimistica utilizzati dall'origine dati per rilevare se una riga è stata modificata. Ciò si verifica ogni volta che **SQLFetchScroll** recupera un nuovo set di righe, anche quando recupera nuovamente il set di righe corrente. Viene chiamato con FetchOrientation impostato su SQL_FETCH_RELATIVE e FetchOffset impostato su 0.  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>Driver SQLFetchScroll e ODBC 2.x  
 Quando un'applicazione chiama **SQLFetchScroll** in un driver ODBC 2.x, Gestione Driver esegue il mapping di questa chiamata a **SQLExtendedFetch**. Passa i valori seguenti per gli argomenti di **SQLExtendedFetch**.  
  
|Argomento SQLExtendedFetch|Valore|  
|-------------------------------|-----------|  
|StatementHandle|StatementHandle in **SQLFetchScroll**.|  
|Orientamento Fetch|FetchOrientation in **SQLFetchScroll**.|  
|RecuperaOffset|Se FetchOrientation non è SQL_FETCH_BOOKMARK, viene utilizzato il valore dell'argomento FetchOffset in **SQLFetchScroll.**<br /><br /> Se FetchOrientation è SQL_FETCH_BOOKMARK, viene utilizzato il valore archiviato in corrispondenza dell'indirizzo specificato dall'attributo di istruzione SQL_ATTR_FETCH_BOOKMARK_PTR.|  
|RowCountPtr|Indirizzo specificato dall'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR.|  
|RowStatusArray|Indirizzo specificato dall'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR.|  
  
 Per altre informazioni, vedere Cursori a [blocchi, cursori scorrevoli e compatibilità](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) con le versioni precedenti nell'appendice G: Linee guida per i driver per la compatibilità con le versioni precedenti.  
  
## <a name="descriptors-and-sqlfetchscroll"></a>Descrittori e SQLFetchScroll  
 **SQLFetchScroll** interagisce con i descrittori nello stesso modo di **SQLFetch**. Per ulteriori informazioni, vedere la sezione "Descrittori e SQLFetchScroll" in [Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Vedere [Associazione per colonna](../../../odbc/reference/develop-app/column-wise-binding.md), [Associazione per](../../../odbc/reference/develop-app/row-wise-binding.md)base di righe , Istruzioni di aggiornamento ed eliminazione [posizionate](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)e [Aggiornamento delle righe nel set di righe con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Esecuzione di operazioni di inserimento, aggiornamento o eliminazione bulk|[Funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di informazioni su una colonna in un set di risultatiReturning information about a column in a result set|[Funzione SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Recupero di una singola riga o di un blocco di dati in una direzione forward-only|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Chiusura del cursore sull'istruzione|[Funzione SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Restituzione del numero di colonne del set di risultatiReturning the number of result set columns|[Funzione SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Posizionamento del cursore, aggiornamento dei dati nel set di righe o aggiornamento o eliminazione di dati nel set di risultati|[Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Impostazione di un attributo di istruzioneSetting a statement attribute|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
