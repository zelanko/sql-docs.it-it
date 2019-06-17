---
title: Funzione SQLFetchScroll | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20a1580503ad141817edcf8e01772dfcc8dc39a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537362"
---
# <a name="sqlfetchscroll-function"></a>Funzione SQLFetchScroll
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLFetchScroll** recupera il set di righe specificato dei dati dal set di risultati e restituisce i dati per tutte le colonne associate. I set di righe può essere specificato in una posizione assoluta o relativa o dal segnalibro.  
  
 Quando si usa un driver ODBC 2.x, gestione Driver esegue il mapping di questa funzione per **SQLExtendedFetch**. Per altre informazioni, vedere [Mapping di funzioni di sostituzione per la compatibilità con le versioni precedenti di applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *FetchOrientation*  
 [Input]  
  
 Tipo di operazione di recupero:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 Per altre informazioni, vedere "Posizionare il cursore" nella sezione "Commenti".  
  
 *FetchOffset*  
 [Input]  
  
 Numero di riga da recuperare. L'interpretazione di questo argomento dipende dal valore della *FetchOrientation* argomento. Per altre informazioni, vedere "Posizionare il cursore" nella sezione "Commenti".  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLFetchScroll** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato può essere ottenuto chiamando **SQLGetDiagRec** con un HandleType su SQL_HANDLE_STMT e di un Handle StatementHandle. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLFetchScroll** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente. Se si verifica un errore in una singola colonna, **SQLGetDiagField** può essere chiamato con un DiagIdentifier di SQL_DIAG_COLUMN_NUMBER per determinare la colonna a cui si è verificato l'errore; e **SQLGetDiagField** può essere chiamato con un DiagIdentifier di SQL_DIAG_ROW_NUMBER per determinare la riga che contiene tale colonna.  
  
 Per tutti questi SQLSTATEs che può restituire SQL_SUCCESS_WITH_INFO o SQL_ERROR (eccetto SQLSTATEs 01xxx), viene restituito SQL_SUCCESS_WITH_INFO se si verifica un errore in uno o più, ma non tutte, le righe di un'operazione con più righe e viene restituito SQL_ERROR se si verifica un errore in un riga singola operazione.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Stringa o dati binari restituiti per una colonna ha comportato il troncamento del carattere non vuote o dati binari non NULL. Se si tratta di un valore stringa, era troncati a destra.|  
|01S01|Errore nella riga|Si è verificato un errore durante il recupero di una o più righe.<br /><br /> (Se il valore SQLSTATE restituito quando un'applicazione ODBC 3 *. x* applicazione funziona con un'API ODBC 2*x* driver, può essere ignorato.)|  
|01S06|Tentativo di recupero prima che il set di risultati restituito il primo set di righe|Il set di righe richiesto sovrappongono l'inizio del set di risultati quando FetchOrientation era SQL_FETCH_PRIOR, la posizione corrente non è compresa nella prima riga e il numero di riga corrente è minore o uguale alla dimensione del set di righe.<br /><br /> Il set di righe richiesto sovrappongono l'inizio del set di risultati quando FetchOrientation era SQL_FETCH_PRIOR, la posizione corrente è oltre la fine del set di risultati e il set di righe dimensioni superiori a dimensioni del set di risultati.<br /><br /> Il set di righe richiesto sovrappongono l'inizio del set di risultati quando FetchOrientation era SQL_FETCH_RELATIVE, FetchOffset è negativo e il valore assoluto di FetchOffset minore o uguale alla dimensione del set di righe.<br /><br /> Il set di righe richiesto sovrapposte l'inizio del set di risultati quando FetchOrientation era SQL_FETCH_ABSOLUTE, FetchOffset è negativo e il valore assoluto di FetchOffset superiore a dimensioni del set di risultati, ma minore o uguale alla dimensione del set di righe.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01S07|Troncamento frazionario.|I dati restituiti per una colonna è stati troncati. Per i tipi di dati numerici, la parte frazionaria del numero è stata troncata. Per ora, timestamp e tipi di dati di intervallo che contiene un componente della fase, la parte frazionaria del tempo sono stata troncata.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07006|Violazione dell'attributo del tipo di dati|Non è possibile convertire il valore di dati di una colonna nel set di risultati per il tipo di dati specificato dallo *TargetType* nelle **SQLBindCol**.<br /><br /> Colonna 0 è stata associata a un tipo di dati di SQL_C_BOOKMARK e l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_VARIABLE.<br /><br /> Colonna 0 è stata associata a un tipo di dati di SQL_C_VARBOOKMARK e l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS non è stato impostato su SQL_UB_VARIABLE.|  
|07009|Indice del descrittore non valido|Il driver è stato un ODBC 2 *. x* driver che non supporta **SQLExtendedFetch**, e un numero di colonna specificato nell'associazione per una colonna è 0.<br /><br /> Colonna 0 è stata associata e l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_OFF.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|22001|Stringa troncati di dati a destra|Un segnalibro a lunghezza variabile restituito per una colonna sono stato troncato.|  
|22002|Variabile indicatore necessaria ma non fornito|Dati NULL è stati recuperati in una colonna la cui proprietà *StrLen_or_IndPtr* effettui **SQLBindCol** (o SQL_DESC_INDICATOR_PTR impostato da **SQLSetDescField** o  **SQLSetDescRec**) era un puntatore null.|  
|22003|Valore numerico non compreso nell'intervallo|Restituzione del valore numerico (come valore numerico o stringa) per uno o più colonne associate avrebbe causato la parte intera (in contrapposizione frazionari) del numero da troncare.<br /><br /> Per altre informazioni, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) in [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato di datetime non valido|Una colonna di tipo carattere nel set di risultati è stata associata a una data, ora o timestamp C struttura e un valore nella colonna non è, rispettivamente, una data non valida, ora o timestamp.|  
|22012|Divisione per zero|Un valore da un'espressione aritmetica è stato restituito, ciò ha provocato la divisione per zero.|  
|22015|Overflow del campo Interval|Assegnazione da un numerico esatto o l'intervallo di tipo SQL a un tipo di intervallo C, ha causato una perdita di cifre significative nel campo iniziale.<br /><br /> Durante il recupero di dati a un tipo di intervallo C, si è verificato alcun rappresentazione del valore del tipo SQL nel tipo di intervallo C.|  
|22018|Valore del carattere non valido per la specifica del cast|Una colonna di tipo carattere nel set di risultati è stata associata a un buffer di caratteri C e la colonna contiene un carattere che non ha alcuna rappresentazione nel set di caratteri del buffer.<br /><br /> Il tipo C è un valore numerico esatto o approssimativo, un valore datetime o un tipo di dati di intervallo; il tipo SQL della colonna è un tipo di dati carattere. e il valore nella colonna non è un valore letterale valido del tipo C associato.|  
|24000|Stato del cursore non valido|Il *StatementHandle* era stato eseguito ma è stato associato alcun set di risultati le *StatementHandle*.|  
|40001|Errore di serializzazione.|La transazione in cui è stata eseguita l'operazione di recupero è stata interrotta per impedire un deadlock.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle*. Quindi la funzione è stata chiamata nuovamente sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLFetchScroll** funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) specificato *StatementHandle* non è stato eseguito. La funzione è stata chiamata senza chiamare prima il metodo **SQLExecDirect**, **SQLExecute** o una funzione di catalogo.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.<br /><br /> (DM) **SQLFetch** è stato chiamato per il *StatementHandle* dopo **SQLExtendedFetch** è stato chiamato e prima **SQLFreeStmt** con il SQL _ Opzione di chiusura è stato chiamato.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|L'attributo di istruzione SQL_ATTR_USE_BOOKMARK è stata impostata su SQL_UB_VARIABLE e colonna 0 è stata associata a un buffer di lunghezza non è uguale alla lunghezza massima per il segnalibro per questo set di risultati. (Questa lunghezza è disponibile nel campo SQL_DESC_OCTET_LENGTH di implementazione e può essere ottenuta chiamando **SQLDescribeCol**, **SQLColAttribute**, o **SQLGetDescField**.)|  
|HY106|Tipo compreso nell'intervallo di recupero|Gestione dei dispositivi) il valore specificato per l'argomento FetchOrientation non è valido.<br /><br /> (DM) FetchOrientation l'argomento è stato impostato su SQL_FETCH_BOOKMARK e l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_OFF.<br /><br /> Il valore dell'attributo SQL_ATTR_CURSOR_TYPE istruzione era SQL_CURSOR_FORWARD_ONLY e il valore dell'argomento che fetchorientation non era SQL_FETCH_NEXT.<br /><br /> Il valore dell'attributo di istruzione SQL_ATTR_CURSOR_SCROLLABLE era SQL_NONSCROLLABLE e il valore dell'argomento che fetchorientation non era SQL_FETCH_NEXT.|  
|HY107|Valore di riga non compreso nell'intervallo|Il valore specificato con l'attributo di istruzione SQL_ATTR_CURSOR_TYPE era SQL_CURSOR_KEYSET_DRIVEN, ma il valore specificato con l'attributo di istruzione SQL_ATTR_KEYSET_SIZE è maggiore di 0 e minore del valore specificato con il SQL_ATTR_ROW_ARRAY_ Attributo di istruzione di dimensioni.|  
|HY111|Valore di segnalibro non valido|L'argomento FetchOrientation era impostato su SQL_FETCH_BOOKMARK e il segnalibro a cui punta il valore dell'attributo di istruzione SQL_ATTR_FETCH_BOOKMARK_PTR non è valido o è un puntatore null.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|L'origine dati o driver non supporta la conversione specificata dalla combinazione dei *TargetType* nelle **SQLBindCol** e il tipo di dati SQL della colonna corrispondente.|  
|HYT00|Timeout|Il periodo di timeout query scaduto prima l'origine dati ha restituito il set di risultati richiesti. Il periodo di timeout viene impostato tramite SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **SQLFetchScroll** restituisce un set di righe specificato dal set di risultati. In base alla posizione assoluta o relativa o tramite segnalibro, è possibile specificare i set di righe. **SQLFetchScroll** può essere chiamato solo mentre è presente un set di risultati, vale a dire, dopo una chiamata che crea un set di risultati e prima del cursore over che set di risultati è chiuso. Se tutte le colonne sono associate, restituisce i dati in tali colonne. Se l'applicazione non è specificato un puntatore a un buffer in cui restituire il numero di righe recuperate, o una matrice di stato di riga **SQLFetchScroll** restituisce anche queste informazioni. Le chiamate a **SQLFetchScroll** possono essere combinate con le chiamate a **SQLFetch** ma ReadContentAsBase64 e ReadContentAsBinHex con chiamate a **SQLExtendedFetch**.  
  
 Per altre informazioni, vedere [cursori a blocchi usando](../../../odbc/reference/develop-app/using-block-cursors.md) e [utilizzando i cursori scorrevoli](../../../odbc/reference/develop-app/using-scrollable-cursors.md).  
  
## <a name="positioning-the-cursor"></a>Posizionando il cursore  
 Quando viene creato il set di risultati, il cursore viene posizionato prima dell'inizio del set di risultati. **SQLFetchScroll** posiziona il cursore a blocchi in base ai valori del *FetchOrientation* e *FetchOffset* argomenti come illustrato nella tabella seguente. Le regole precise per determinare l'inizio del nuovo set di righe vengono visualizzate nella sezione successiva.  
  
|FetchOrientation|Significato|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|Restituisce il successivo set di righe. Ciò equivale alla chiamata **SQLFetch**.<br /><br /> **SQLFetchScroll** ignora il valore di *FetchOffset*.|  
|SQL_FETCH_PRIOR|Restituisce il set di righe precedente.<br /><br /> **SQLFetchScroll** ignora il valore di *FetchOffset*.|  
|SQL_FETCH_RELATIVE|Restituisce il set di righe *FetchOffset* dall'inizio del set di righe corrente.|  
|SQL_FETCH_ABSOLUTE|Restituisce il set di righe a partire dalla riga *FetchOffset*.|  
|SQL_FETCH_FIRST|Restituisce il primo set di righe nel set di risultati.<br /><br /> **SQLFetchScroll** ignora il valore di *FetchOffset*.|  
|SQL_FETCH_LAST|Restituisce l'ultimo intero set di righe nel set di risultati.<br /><br /> **SQLFetchScroll** ignora il valore di *FetchOffset*.|  
|SQL_FETCH_BOOKMARK|Restituisce il set di righe FetchOffset righe dal segnalibro specificato dall'attributo istruzione SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
 I driver non sono necessari per supportare tutti gli orientamenti di recupero; un'applicazione chiama **SQLGetInfo** con un tipo di informazioni di SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (a seconda del tipo di cursore) per determinare quale operazione di recupero orientamenti supportati dal driver. L'applicazione deve esaminare le maschere SQL_CA1_NEXT, SQL_CA1_RELATIVE, SQL_CA1_ABSOLUTE e WQL_CA1_BOOKMARK in questi tipi di informazioni. Inoltre, se il cursore è forward-only e FetchOrientation non, SQL_FETCH_NEXT **SQLFetchScroll** restituisce SQLSTATE HY106 (tipo compreso nell'intervallo di recupero).  
  
 L'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE specifica il numero di righe nel set di righe. Se il set di righe recuperate dal **SQLFetchScroll** fine del set di risultati, è sovrapposto **SQLFetchScroll** restituisce un set di righe parziale. Vale a dire se S + R - 1 è maggiore di L, dove S è la riga iniziale del set di righe recuperate, R è la dimensione del set di righe e L è l'ultima riga nel set di risultati, quindi solo il primo G - S + 1 righe del set di righe sono validi. Le righe rimanenti sono vuote e con stato SQL_ROW_NOROW.  
  
 Dopo aver **SQLFetchScroll** viene restituito, la riga corrente è la prima riga del set di righe.  
  
## <a name="cursor-positioning-rules"></a>Le regole di posizionamento del cursore  
 Le sezioni seguenti descrivono le regole precise per ogni valore di FetchOrientation. Tali regole utilizzano la notazione seguente.  
  
|Notazione|Significato|  
|--------------|-------------|  
|*Prima dell'inizio*|Prima dell'inizio del set di risultati è posizionato il cursore a blocchi. Se prima dell'inizio del set di risultati, la prima riga del set di righe nuove **SQLFetchScroll** restituisce SQL_NO_DATA.|  
|*Dopo la fine*|Il cursore a blocchi viene posizionato dopo la fine del set di risultati. Se dopo la fine del set di risultati, la prima riga del set di righe nuove **SQLFetchScroll** restituisce SQL_NO_DATA.|  
|*CurrRowsetStart*|Il numero della prima riga nel set di righe corrente.|  
|*LastResultRow*|Il numero dell'ultima riga nel set di risultati.|  
|*RowsetSize*|Le dimensioni del set di righe.|  
|*FetchOffset*|Il valore della *FetchOffset* argomento.|  
|*BookmarkRow*|La riga corrispondente al segnalibro specificato dall'attributo istruzione SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
## <a name="sqlfetchnext"></a>SQL_FETCH_NEXT  
 Le regole seguenti si applicano.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*Prima dell'inizio*|1|  
|*CurrRowsetStart + RowsetSize*[1] *\<= LastResultRow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1] *> LastResultRow*|*Dopo la fine*|  
|*Dopo la fine*|*Dopo la fine*|  
  
 [1] se le dimensioni del set di righe sono stata modificata dalla chiamata precedente a recuperare le righe, questa è la dimensione del set di righe che è stata usata con la chiamata precedente.  
  
## <a name="sqlfetchprior"></a>SQL_FETCH_PRIOR  
 Le regole seguenti si applicano.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*Prima dell'inizio*|*Prima dell'inizio*|  
|*CurrRowsetStart = 1*|*Prima dell'inizio*|  
|*1 < CurrRowsetStart <= RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart - RowsetSize* <sup>[2]</sup>|  
|*Dopo la fine e LastResultRow < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*Dopo la fine LastResultRow e > = RowsetSize* <sup>[2]</sup>|*LastResultRow - RowsetSize + 1* <sup>[2].</sup>|  
  
 [1] **SQLFetchScroll** restituisce SQLSTATE 01S06 (tentativo di recupero prima che il set di risultati restituito il primo set di righe) e SQL_SUCCESS_WITH_INFO.  
  
 [2] se le dimensioni del set di righe sono stata modificata dalla chiamata precedente a recuperare le righe, questa è la nuova dimensione di set di righe.  
  
## <a name="sqlfetchrelative"></a>SQL_FETCH_RELATIVE  
 Le regole seguenti si applicano.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*(Prima di avviare e FetchOffset > 0) O (dopo la fine e FetchOffset < 0)*|*--* <sup>[1]</sup>|  
|*BeforeStart e FetchOffset < = 0*|*Prima dell'inizio*|  
|*CurrRowsetStart = 1 AND FetchOffset < 0*|*Prima dell'inizio*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; > RowsetSize* <sup>[3]</sup>|*Prima dell'inizio*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; <= RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 <= CurrRowsetStart + FetchOffset \<= LastResultRow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*Dopo la fine*|  
|*Dopo la fine FetchOffset e > = 0*|*Dopo la fine*|  
  
 [1] ***SQLFetchScroll*** restituisce set di righe dello stesso come se fosse stato chiamato con FetchOrientation impostata su SQL_FETCH_ABSOLUTE. Per altre informazioni, vedere la sezione "SQL_FETCH_ABSOLUTE".  
  
 [2] **SQLFetchScroll** restituisce SQLSTATE 01S06 (tentativo di recupero prima che il set di risultati restituito il primo set di righe) e SQL_SUCCESS_WITH_INFO.  
  
 [3] se le dimensioni del set di righe sono stata modificata dalla chiamata precedente a recuperare le righe, questa è la nuova dimensione di set di righe.  
  
## <a name="sqlfetchabsolute"></a>SQL_FETCH_ABSOLUTE  
 Le regole seguenti si applicano.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; <= LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 e &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; > RowsetSize* <sup>[2]</sup>|*Prima dell'inizio*|  
|*FetchOffset < 0 e &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; < = RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*Prima dell'inizio*|  
|*1 <= FetchOffset \<= LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*Dopo la fine*|  
  
 [1] **SQLFetchScroll** restituisce SQLSTATE 01S06 (tentativo di recupero prima che il set di risultati restituito il primo set di righe) e SQL_SUCCESS_WITH_INFO.  
  
 [2] se le dimensioni del set di righe sono stata modificata dalla chiamata precedente a recuperare le righe, questa è la nuova dimensione di set di righe.  
  
 Un recupero assoluto eseguito a fronte di un cursore dinamico non può fornire il risultato richiesto perché le posizioni di riga in un cursore dinamico sono Indeterminate. Questa operazione equivale a un'operazione di recupero prima di tutto è seguito da un'istruzione fetch relative; non è un'operazione atomica, perché è un recupero assoluto su un cursore statico.  
  
## <a name="sqlfetchfirst"></a>SQL_FETCH_FIRST  
 Le regole seguenti si applicano.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*Any*|*1*|  
  
## <a name="sqlfetchlast"></a>SQL_FETCH_LAST  
 Le regole seguenti si applicano.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> < = LastResultRow|*LastResultRow - RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] se le dimensioni del set di righe sono stata modificata dalla chiamata precedente a recuperare le righe, questa è la nuova dimensione di set di righe.  
  
## <a name="sqlfetchbookmark"></a>SQL_FETCH_BOOKMARK  
 Le regole seguenti si applicano.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*Prima dell'inizio*|  
|*1 <= BookmarkRow + FetchOffset \<= LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*Dopo la fine*|  
  
 Per informazioni sui segnalibri, vedere [segnalibri (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>Effetto dell'aggiunta, eliminazione e le righe di errore in uno spostamento del cursore  
 I cursori statici e gestito da keyset in alcuni casi rilevano righe aggiunte al risultato, impostare e rimuovere le righe eliminate dal set di risultati. Chiamando **SQLGetInfo** specificando le SQL_STATIC_CURSOR_ATTRIBUTES2 SQL_KEYSET_CURSOR_ATTRIBUTES2 opzioni ed esaminando il SQL_CA2_SENSITIVITY_ADDITIONS SQL_CA2_SENSITIVITY_DELETIONS e SQL_CA2_SENSITIVITY_ Gli aggiornamenti maschere di bit, un'applicazione determina se i cursori implementati da un driver specifico scopo. Per i driver che è possano rilevare le righe eliminate e rimuoverle, nei paragrafi seguenti vengono descritti gli effetti di questo comportamento. Per i driver in grado di rilevare le righe eliminate, ma non è possibile rimuoverli, le eliminazioni non hanno effetto sui movimenti del cursore e nei paragrafi seguenti non sono applicabili.  
  
 Se il cursore rileva righe aggiunte al set di risultati o rimuove le righe eliminate dal set di risultati, viene visualizzato come se rileva queste modifiche solo quando il recupero dei dati. Include il caso quando **SQLFetchScroll** viene chiamato con FetchOrientation impostata SQL_FETCH_RELATIVE e FetchOffset impostata su 0 per recupera di nuovo set di righe dello stesso, ma non include il caso quando viene chiamato SQLSetPos con fOption impostato su SQL _ aggiornare. Nel secondo caso, vengono aggiornati i dati nei buffer di set di righe, ma non refetched ed eliminate righe non vengono rimosse dal set di risultati. Di conseguenza, quando una riga viene eliminata dal o inserita nel set di righe corrente, il cursore non modifica i buffer di righe. Al contrario, rileva la modifica quando recupera qualsiasi set di righe incluse in precedenza la riga eliminata o include ora la riga inserita.  
  
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
  
 Quando **SQLFetchScroll** restituisce un nuovo set di righe con una posizione rispetto al set di righe corrente, vale a dire FetchOrientation è SQL_FETCH_NEXT, SQL_FETCH_PRIOR o SQL_FETCH_RELATIVE: non sono incluse le modifiche al set di righe corrente Quando si calcola la posizione iniziale del nuovo set di righe. Tuttavia, sono incluse le modifiche all'esterno di righe corrente se è in grado di rilevarli. Inoltre, quando **SQLFetchScroll** restituisce un nuovo set di righe che dispone di una posizione indipendente del set di righe corrente - FetchOrientation è SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE o impostato su SQL_FETCH_BOOKMARK -, include tutte le modifiche è in grado di rilevare, anche se sono il set di righe corrente.  
  
 Per determinare se le righe appena aggiunte sono all'interno o all'esterno di righe corrente, un set di righe parziali viene considerato per terminare in corrispondenza dell'ultima riga valida; vale a dire, l'ultima riga per cui lo stato di riga non è SQL_ROW_NOROW. Si supponga, ad esempio, il cursore si trova in grado di rilevare le righe appena aggiunte, il set di righe corrente è un set di righe parziale, l'applicazione aggiunge nuove righe e il cursore queste righe vengono aggiunte alla fine del set di risultati. Se l'applicazione chiama **SQLFetchScroll** con FetchOrientation impostata su, SQL_FETCH_NEXT **SQLFetchScroll** restituisce il set di righe a partire dalla prima riga appena aggiunta.  
  
 Si supponga, ad esempio, il set di righe corrente è costituito da righe 21 e 30, la dimensione del set di righe è 10, il cursore rimuove le righe eliminate dal set di risultati e cursore rileva righe aggiunte al set di risultati. La tabella seguente mostra le righe **SQLFetchScroll** restituisce in varie situazioni.  
  
|Cambia|Tipo di recupero|FetchOffset|Nuovo set di righe [1]|  
|------------|----------------|-----------------|---------------------|  
|Elimina riga 21|NEXT|0|31 a 40|  
|Elimina riga 31|NEXT|0|da 32 a 41|  
|Inserire la riga tra le righe 21 e 22|NEXT|0|31 a 40|  
|Inserire la riga tra le righe 30 e 31|NEXT|0|Riga inserita, 31 a 39|  
|Elimina riga 21|PRIOR|0|da 11 a 20|  
|Elimina riga 20|PRIOR|0|da 10 a 19|  
|Inserire la riga tra le righe 21 e 22|PRIOR|0|da 11 a 20|  
|Inserire la riga tra le righe di 20 e 21|PRIOR|0|riga inserita da 12 a 20,|  
|Elimina riga 21|RELATIVE|0|22 a 31<sup>[2]</sup>|  
|Elimina riga 21|RELATIVE|1|22 a 31|  
|Inserire la riga tra le righe 21 e 22|RELATIVE|0|riga inserita, 21, 22 e 29|  
|Inserire la riga tra le righe 21 e 22|RELATIVE|1|22 a 31|  
|Elimina riga 21|ABSOLUTE|21|22 a 31<sup>[2]</sup>|  
|Elimina riga 22|ABSOLUTE|21|21, 23 a 31|  
|Inserire la riga tra le righe 21 e 22|ABSOLUTE|22|Riga inserita, 22 e 29|  
  
 [1] la colonna utilizza i numeri di riga prima di tutte le righe inserite o eliminate.  
  
 [2] In questo caso, il cursore tenta di restituire le righe a partire da riga 21. Poiché riga 21 è stata eliminata, la prima riga che restituisce è riga 22.  
  
 Le righe di errore (ovvero, le righe con lo stato di SQL_ROW_ERROR) non influenzano lo spostamento del cursore. Ad esempio, se il set di righe corrente inizia con righe 11 e lo stato di riga 11 viene SQL_ROW_ERROR, chiamare **SQLFetchScroll** con FetchOrientation impostata SQL_FETCH_RELATIVE e FetchOffset è impostato su 5 restituisce il set di righe inizia con la riga 16, esattamente come verrebbe se lo stato di riga 11 è SQL_SUCCESS.  
  
## <a name="returning-data-in-bound-columns"></a>Restituzione di dati nelle colonne associate  
 **SQLFetchScroll** restituisce i dati nelle colonne associate nello stesso modo **SQLFetch**. Per altre informazioni, vedere "Restituzione di dati nelle colonne associate" nella [SQLFetch-funzione](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Se nessuna colonna è associata, **SQLFetchScroll** non restituisce dati ma consente di spostare il cursore a blocchi nella posizione specificata. Indica se i dati possono essere recuperati da colonne non associate di un cursore a blocchi con **SQLGetData** dipende dal driver. Questa funzionalità è supportata se una chiamata a **SQLGetInfo** restituisce il SQL_GD_BLOCK bit per il tipo di informazioni SQL_GETDATA_EXTENSIONS.  
  
## <a name="buffer-addresses"></a>Indirizzi di buffer  
 **SQLFetchScroll** utilizza la stessa formula per determinare l'indirizzo del buffer di dati e lunghezza/indicatore come **SQLFetch**. Per altre informazioni, vedere "Indirizzi di Buffer" nella [funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="row-status-array"></a>Matrice di stato riga  
 **SQLFetchScroll** imposta i valori nella matrice di stato di riga in modo analogo SQLFetch. Per altre informazioni, vedere "Matrice di stato di riga" nella [SQLFetch-funzione](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="rows-fetched-buffer"></a>Recuperare le righe del Buffer  
 **SQLFetchScroll** restituisce il numero di righe recuperate nel buffer di righe recuperate in modo analogo **SQLFetch**. Per altre informazioni, vedere "Buffer di recupero di righe" nella [SQLFetch-funzione](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="error-handling"></a>Gestione degli errori  
 Quando un'applicazione chiama **SQLFetchScroll** in un driver ODBC 3.x, gestione Driver chiama **SQLFetchScroll** nel driver. Quando un'applicazione chiama **SQLFetchScroll** in un driver ODBC 2.x, gestione Driver chiama SQLExtendedFetch nel driver. In quanto **SQLFetchScroll** e SQLExtendedFetch gestire gli errori in modo leggermente diverso, l'applicazione non vede il comportamento dell'errore leggermente diverse quando chiama **SQLFetchScroll** in ODBC 2.x e ODBC driver 3.x.  
  
 **SQLFetchScroll** restituisce errori e avvisi in modo analogo **SQLFetch**; per altre informazioni, vedere "Gestione degli errori" nel **SQLFetch**. **SQLExtendedFetch** restituisce errori in modo analogo **SQLFetch**, con le eccezioni seguenti:  
  
 Quando viene generato un avviso che si applica a una particolare riga nel set di righe, SQLExtendedFetch imposta la voce corrispondente nella matrice di stato di riga per SQL_ROW_SUCCESS, non SQL_ROW_SUCCESS_WITH_INFO.  
  
 Se si verificano errori in ogni riga nel set di righe, SQLExtendedFetch restituisce SQL_SUCCESS_WITH_INFO, non da SQL_ERROR.  
  
 In ogni gruppo di record di stato che si applica a una singola riga, il primo record di stato restituito da SQLExtendedFetch deve contenere SQLSTATE 01S01 (errore nella riga). **SQLFetchScroll** non restituisce il valore SQLSTATE. Se SQLExtendedFetch è in grado di restituire altri SQLSTATEs, comunque deve restituire il valore SQLSTATE.  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll e concorrenza ottimistica  
 Se un cursore utilizza la concorrenza ottimistica, vale a dire, l'attributo di istruzione SQL_ATTR_CONCURRENCY ha un valore delle SQL_CONCUR_ROWVER, SQL_CONCUR_VALUES **SQLFetchScroll** Aggiorna i valori di concorrenza ottimistica utilizzati dai dati origine per rilevare se una riga è stata modificata. Ciò si verifica ogni volta che **SQLFetchScroll** recupera un nuovo set di righe, ad esempio quando recupera nuovamente il set di righe corrente. (Viene chiamato con FetchOrientation impostata SQL_FETCH_RELATIVE e FetchOffset impostato su 0.)  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll e ODBC 2.x driver  
 Quando un'applicazione chiama **SQLFetchScroll** in un driver ODBC 2.x, gestione Driver esegue il mapping di questa chiamata a **SQLExtendedFetch**. Passa i valori seguenti per gli argomenti di **SQLExtendedFetch**.  
  
|Argomento SQLExtendedFetch|Value|  
|-------------------------------|-----------|  
|StatementHandle|In StatementHandle **SQLFetchScroll**.|  
|FetchOrientation|In FetchOrientation **SQLFetchScroll**.|  
|FetchOffset|Se FetchOrientation non è impostato su SQL_FETCH_BOOKMARK, il valore dell'argomento FetchOffset nella **SQLFetchScroll** viene usato.<br /><br /> Se impostato su SQL_FETCH_BOOKMARK FetchOrientation, viene utilizzato il valore archiviato in corrispondenza dell'indirizzo specificato dall'attributo istruzione SQL_ATTR_FETCH_BOOKMARK_PTR.|  
|RowCountPtr|L'indirizzo specificato dall'attributo SQL_ATTR_ROWS_FETCHED_PTR istruzione.|  
|RowStatusArray|L'indirizzo specificato nell'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR.|  
  
 Per altre informazioni, vedere [cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) nell'appendice g: Driver linee guida per la compatibilità con le versioni precedenti.  
  
## <a name="descriptors-and-sqlfetchscroll"></a>Descrittori e SQLFetchScroll  
 **SQLFetchScroll** interagisce con i descrittori in modo analogo **SQLFetch**. Per altre informazioni, vedere la sezione "Descrittori e SQLFetchScroll" nella [SQLFetch-funzione](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Visualizzare [associazione per colonna](../../../odbc/reference/develop-app/column-wise-binding.md), [l'associazione per riga](../../../odbc/reference/develop-app/row-wise-binding.md), [istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md), e [aggiornamento delle righe nel set di righe con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultati|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Esecuzione di operazioni bulk insert, update o operazioni di eliminazione|[Funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di informazioni relative a una colonna in un set di risultati|[Funzione SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Esecuzione di un'istruzione SQL|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Il recupero di una singola riga o un blocco di dati in una direzione di tipo forward-only|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Chiusura del cursore nell'istruzione|[Funzione SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Colonne del set di restituzione del numero di risultati|[Funzione SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Posizionando il cursore, l'aggiornamento dei dati del set di righe o l'aggiornamento o eliminazione dei dati nel set di risultati|[Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|L'impostazione di un attributo di istruzione|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
