---
title: 'Funzione SQLFetch : Documenti Microsoft'
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc7e2da6996d8d6b2ee66befdc90794efec5617b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285971"
---
# <a name="sqlfetch-function"></a>Funzione SQLFetch
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLFetch** recupera il set di righe successivo di dati dal set di risultati e restituisce i dati per tutte le colonne associate.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLFetch** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando la [funzione SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLFetch** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente. Se si verifica un errore in una singola colonna, [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) può essere chiamato con un *DiagIdentifier* di SQL_DIAG_COLUMN_NUMBER per determinare la colonna in cui si è verificato l'errore; e **SQLGetDiagField** può essere chiamato con un *DiagIdentifier* di SQL_DIAG_ROW_NUMBER per determinare la riga che contiene tale colonna.  
  
 Per tutti gli SQLSTATE che possono restituire SQL_SUCCESS_WITH_INFO o SQL_ERROR (ad eccezione di 01xxx SQLSTATEs), viene restituito SQL_SUCCESS_WITH_INFO se si verifica un errore in uno o più, ma non in tutte le righe di un'operazione multiriga, e SQL_ERROR viene restituito se si verifica un errore in un'operazione a riga singola.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Dati stringa o binari restituiti per una colonna hanno determinato il troncamento di caratteri non vuoti o dati binari non NULL. Se si tratta di un valore stringa, è stato troncato a destra.|  
|01S01 (in questo stato di|Errore nella riga|Si è verificato un errore durante il recupero di una o più righe.<br /><br /> (Se questo SQLSTATE viene restituito quando un'applicazione ODBC 3 *.x* utilizza un driver *.x* ODBC 2, può essere ignorato.)|  
|01S07 (intito)|Troncamento frazionario|I dati restituiti per una colonna sono stati troncati. Per i tipi di dati numerici, la parte frazionaria del numero è stata troncata. Per i tipi di dati time, timestamp e interval che contengono un componente ora, la parte frazionaria dell'ora è stata troncata.<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07006|Violazione dell'attributo del tipo di dati con restrizioniRestricted data type attribute violation|Impossibile convertire il valore dei dati di una colonna nel set di risultati nel tipo di dati specificato da *TargetType* in **SQLBindCol**.<br /><br /> La colonna 0 è stata associata a un tipo di dati SQL_C_BOOKMARK e l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_VARIABLE.<br /><br /> La colonna 0 era associata a un tipo di dati di SQL_C_VARBOOKMARK e l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS non è stato impostato su SQL_UB_VARIABLE.|  
|07009|Indice descrittore non valido|Il driver era un driver *.x* ODBC 2 che non supporta **SQLExtendedFetch**e un numero di colonna specificato nell'associazione per una colonna era 0.<br /><br /> La colonna 0 è stata associata e l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_OFF.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|22001|Dati stringa troncati a destra|Un segnalibro di lunghezza variabile restituito per una colonna è stato troncato.|  
|22002|Variabile indicatore richiesta ma non fornita|I dati NULL sono stati recuperati in una colonna il cui *StrLen_or_IndPtr* impostato da **SQLBindCol** (o SQL_DESC_INDICATOR_PTR impostato da **SQLSetDescField** o **SQLSetDescRec**) era un puntatore null.|  
|22003|Valore numerico non compreso nell'intervallo|La restituzione del valore numerico come valore numerico o stringa per una o più colonne associate avrebbe causato il troncamento dell'intera parte (anziché frazionaria).<br /><br /> Per altre informazioni, vedere [Conversione di dati da tipi](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) di dati SQL a C nell'Appendice D: tipi di dati.|  
|22007|Formato datetime non valido|Una colonna di caratteri nel set di risultati è stata associata a una data, ora o timestamp C struttura e un valore nella colonna è stato, rispettivamente, una data, ora o timestamp non valido.|  
|22012|Divisione per zero|È stato restituito un valore da un'espressione aritmetica, che ha restituito la divisione per zero.|  
|22015|Overflow campo intervallo|L'assegnazione da un tipo SQL esatto numero o intervallo a un tipo di intervallo C ha causato una perdita di cifre significative nel campo iniziale.<br /><br /> Durante il recupero dei dati in un tipo di intervallo C, non esisteva alcuna rappresentazione del valore del tipo SQL nel tipo di intervallo C.|  
|22018|Valore di carattere non valido per la specifica del cast|Una colonna di caratteri nel set di risultati è stata associata a un buffer di caratteri C e la colonna contiene un carattere per il quale non era presente alcuna rappresentazione nel set di caratteri del buffer.<br /><br /> Il tipo C era un numero esatto o approssimativo, un datetime o un tipo di dati interval; il tipo SQL della colonna era un tipo di dati carattere; e il valore nella colonna non è un valore letterale valido del tipo C associato.|  
|24000|Stato del cursore non valido|*StatementHandle* era in uno stato eseguito ma non era associato alcun set di risultati a *StatementHandle*.|  
|40001|Errore di serializzazione|La transazione in cui è stato eseguito il recupero è stata terminata per evitare deadlock.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione **SQLFetch** è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*. Quindi la funzione **SQLFetch** è stata chiamata nuovamente su *StatementHandle*.<br /><br /> In alternativa, è stata chiamata la funzione **SQLFetch** e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLFetch.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) *L'oggetto statementHandle* specificato non era in uno stato eseguito. La funzione è stata chiamata senza prima chiamare **SQLExecDirect**, **SQLExecute** o una funzione di catalogo.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) **SQLFetch** è stato chiamato per il *StatementHandle* dopo **SQLExtendedFetch** è stato chiamato e prima **di SQLFreeStmt** con il SQL_CLOSE opzione è stata chiamata.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|L'attributo dell'istruzione SQL_ATTR_USE_BOOKMARK è stato impostato su SQL_UB_VARIABLE e la colonna 0 è stata associata a un buffer la cui lunghezza non è uguale alla lunghezza massima per il segnalibro per il set di risultati. Questa lunghezza è disponibile nel campo SQL_DESC_OCTET_LENGTH dell'IRD e può essere ottenuta chiamando **SQLDescribeCol**, **SQLColAttribute**o **SQLGetDescField**.|  
|I107|Valore di riga non compreso nell'intervallo|Il valore specificato con l'attributo di istruzione SQL_ATTR_CURSOR_TYPE è stato SQL_CURSOR_KEYSET_DRIVEN, ma il valore specificato con l'attributo di istruzione SQL_ATTR_KEYSET_SIZE è maggiore di 0 e minore del valore specificato con l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il driver o l'origine dati non supporta la conversione specificata dalla combinazione di *TargetType* in **SQLBindCol** e il tipo di dati SQL della colonna corrispondente.|  
|HYT00|Timeout|Il periodo di timeout della query è scaduto prima che l'origine dati restituisca il set di risultati richiesto. Il periodo di timeout viene impostato tramite SQLSetStmtAttr SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **SQLFetch** restituisce il set di righe successivo nel set di risultati. Può essere chiamato solo mentre esiste un set di risultati, ovvero dopo una chiamata che crea un set di risultati e prima che il cursore su tale set di risultati venga chiuso. Se le colonne sono associate, vengono restituiti i dati in tali colonne. Se l'applicazione ha specificato un puntatore a una matrice di stato di riga o un buffer in cui restituire il numero di righe recuperate, **SQLFetch** restituisce anche queste informazioni. Le chiamate a **SQLFetch** possono essere mescolate con chiamate a **SQLFetchScroll,** ma non possono essere mescolate con chiamate a **SQLExtendedFetch**. Per ulteriori informazioni, vedere [Recupero di una riga di dati](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 Se un'applicazione ODBC 3 *.x* funziona con un driver *.x* ODBC 2, Gestione Driver esegue il mapping di **chiamate SQLFetch** a **SQLExtendedFetch** per un driver *.x* ODBC 2 che supporta **SQLExtendedFetch**. Se il driver *.x* ODBC 2 non supporta **SQLExtendedFetch**, Gestione Driver esegue il mapping di **chiamate SQLFetch** a **SQLFetch** nel driver ODBC 2 *.x,* che può recuperare solo una singola riga.  
  
 Per altre informazioni, vedere Cursori a [blocchi, cursori scorrevoli e compatibilità](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) con le versioni precedenti nell'appendice G: Linee guida per i driver per la compatibilità con le versioni precedenti.  
  
## <a name="positioning-the-cursor"></a>Posizionamento del cursore  
 Quando viene creato il set di risultati, il cursore viene posizionato prima dell'inizio del set di risultati. **SQLFetch** recupera il set di righe successivo. Equivale a chiamare **SQLFetchScroll** con *FetchOrientation* impostato su SQL_FETCH_NEXT. Per ulteriori informazioni sui cursori, vedere [Cursori](../../../odbc/reference/develop-app/cursors.md) e [cursori a blocchi](../../../odbc/reference/develop-app/block-cursors.md).  
  
 L'attributo SQL_ATTR_ROW_ARRAY_SIZE'istruzione specifica il numero di righe nel set di righe. Se il set di righe recuperato da **SQLFetch** si sovrappone alla fine del set di risultati, **SQLFetch** restituisce un set di righe parziale. Ovvero, se S - R - 1 è maggiore di L, dove S è la riga iniziale del set di righe da recuperare, R è la dimensione del set di righe e L è l'ultima riga nel set di risultati, solo le prime righe L - S - 1 del set di righe sono valide. Le righe rimanenti sono vuote e hanno lo stato SQL_ROW_NOROW.  
  
 Dopo la restituzione di **SQLFetch,** la riga corrente è la prima riga del set di righe.  
  
 Le regole elencate nella tabella seguente descrivono il posizionamento del cursore dopo una chiamata a **SQLFetch**, in base alle condizioni elencate nella seconda tabella di questa sezione.  
  
|Condizione|Prima riga del nuovo set di righe|  
|---------------|-----------------------------|  
|Prima dell'inizio|1|  
|*CurrRowsetStart* \< =  *LastResultRow - RowsetSize*[1]|*CurrRowsetStart* + *RowsetSize*[2]|  
|*CurrRowsetStart* > *LastResultRow - RowsetSize*[1]|Dopo la fine|  
|Dopo la fine|Dopo la fine|  
  
 [1] Se la dimensione del set di righe viene modificata tra un recupero e l'altro, si tratta della dimensione del set di righe utilizzata con il recupero precedente.  
  
 [2] Se la dimensione del set di righe viene modificata tra un recupero e l'altro, si tratta della dimensione del set di righe utilizzata con il nuovo fetch.  
  
|Notation|Significato|  
|--------------|-------------|  
|Prima dell'inizio|Il cursore di blocco viene posizionato prima dell'inizio del set di risultati. Se la prima riga del nuovo set di righe è prima dell'inizio del set di risultati, **SQLFetch** restituisce SQL_NO_DATA.|  
|Dopo la fine|Il cursore di blocco viene posizionato dopo la fine del set di risultati. Se la prima riga del nuovo set di righe è dopo la fine del set di risultati, **SQLFetch** restituisce SQL_NO_DATA.|  
|*CurrRowsetStart (Esempio di currRowsetStart)*|Numero della prima riga nel set di righe corrente.|  
|*LastResultRow*|Numero dell'ultima riga nel set di risultati.|  
|*RowsetSize (Dimensioni Set di righe)*|Dimensioni del set di righe.|  
  
 Si supponga, ad esempio, che un set di risultati abbia 100 righe e che la dimensione del set di righe sia 5.For example, suppose a result set has 100 rows and the rowset size is 5. Nella tabella seguente vengono illustrati il set di righe e il codice restituito restituito da **SQLFetch** per posizioni iniziali diverse.  
  
|Set di righe corrente|Codice restituito|Nuovo set di righe|Numero di righe recuperate|  
|--------------------|-----------------|----------------|------------------------|  
|Prima dell'inizio|SQL_SUCCESS|Da 1 a 5|5|  
|Da 1 a 5|SQL_SUCCESS|Da 6 a 10 anni|5|  
|Da 52 a 56 anni|SQL_SUCCESS|Da 57 a 61 anni|5|  
|Da 91 a 95 anni|SQL_SUCCESS|Da 96 a 100 anni|5|  
|Da 93 a 97 anni|SQL_SUCCESS|da 98 a 100. Le righe 4 e 5 della matrice di stato della riga sono impostate su SQL_ROW_NOROW.|3|  
|Da 96 a 100 anni|SQL_NO_DATA|No.|0|  
|Da 99 a 100 anni|SQL_NO_DATA|No.|0|  
|Dopo la fine|SQL_NO_DATA|No.|0|  
  
## <a name="returning-data-in-bound-columns"></a>Restituzione di dati nelle colonne associateReturning Data in Bound Columns  
 Quando **SQLFetch** restituisce ogni riga, inserisce i dati per ogni colonna associata nel buffer associato a tale colonna. Se non sono associate colonne, **SQLFetch** non restituisce dati ma sposta in avanti il cursore a blocchi. I dati possono comunque essere recuperati utilizzando **SQLGetData**. Se il cursore è un cursore a più righe, ovvero il SQL_ATTR_ROW_ARRAY_SIZE è maggiore di 1, **SQLGetData** può essere chiamato solo se viene restituito SQL_GD_BLOCK quando **SQLGetInfo** viene chiamato con un *InfoType* di SQL_GETDATA_EXTENSIONS. (Per altre informazioni, vedere [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).)  
  
 Per ogni colonna associata in una riga, SQLFetch esegue le operazioni seguenti:For each bound column in a row, **SQLFetch** does the following:  
  
1.  Imposta il buffer di lunghezza/indicatore su SQL_NULL_DATA e passa alla colonna successiva se i dati sono NULL. Se i dati sono NULL e nessun buffer di lunghezza/indicatore è stato associato, **SQLFetch** restituisce SQLSTATE 22002 (variabile indicatore richiesta ma non fornita) per la riga e procede alla riga successiva. Per informazioni su come determinare l'indirizzo del buffer di lunghezza/indicatore, vedere "Indirizzi buffer" in [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
     Se i dati per la colonna non sono NULL, **SQLFetch** procede al passaggio 2.  
  
2.  Se l'attributo dell'istruzione SQL_ATTR_MAX_LENGTH è impostato su un valore diverso da zero e la colonna contiene dati binari o di tipo carattere, i dati vengono troncati a SQL_ATTR_MAX_LENGTH byte.  
  
    > [!NOTE]  
    >  L'attributo dell'istruzione SQL_ATTR_MAX_LENGTH ha lo scopo di ridurre il traffico di rete. In genere viene implementato dall'origine dati, che tronca i dati prima di restituirla in rete. I driver e le origini dati non sono necessari per supportarlo. Pertanto, per garantire che i dati vengano troncati a una dimensione specifica, un'applicazione deve allocare un buffer di tale dimensione e specificare la dimensione nell'argomento *cbValueMax* in **SQLBindCol**.  
  
3.  Converte i dati nel tipo specificato da *TargetType* in **SQLBindCol**.  
  
4.  Se i dati sono stati convertiti in un tipo di dati a lunghezza variabile, ad esempio carattere o binario, **SQLFetch** controlla se la lunghezza dei dati supera la lunghezza del buffer di dati. Se la lunghezza dei dati di tipo carattere (incluso il carattere di terminazione null) supera la lunghezza del buffer di dati, **SQLFetch** tronca i dati alla lunghezza del buffer di dati meno la lunghezza di un carattere di terminazione null. Quindi null-termina i dati. Se la lunghezza dei dati binari supera la lunghezza del buffer di dati, **SQLFetch** tronca alla lunghezza del buffer di dati. La lunghezza del buffer di dati viene specificata con *BufferLength* in **SQLBindCol**.  
  
     **SQLFetch** non tronca mai i dati convertiti in tipi di dati a lunghezza fissa; presuppone sempre che la lunghezza del buffer di dati sia la dimensione del tipo di dati.  
  
5.  Inserisce i dati convertiti (ed eventualmente troncati) nel buffer di dati. Per informazioni su come determinare l'indirizzo del buffer di dati, vedere "Indirizzi buffer" in [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
6.  Inserisce la lunghezza dei dati nel buffer di lunghezza/indicatore. Se il puntatore dell'indicatore e il puntatore di lunghezza sono stati entrambi impostati sullo stesso buffer (come una chiamata a **SQLBindCol),** la lunghezza viene scritta nel buffer per i dati validi e SQL_NULL_DATA viene scritta nel buffer per i dati NULL. Se nessun buffer di lunghezza/indicatore è stato associato, **SQLFetch** non restituisce la lunghezza.  
  
    -   Per i dati di tipo carattere o binario, si tratta della lunghezza dei dati dopo la conversione e prima del troncamento a causa del buffer di dati troppo piccolo. Se il driver non è in grado di determinare la lunghezza dei dati dopo la conversione, come talvolta accade con i dati long, imposta la lunghezza su SQL_NO_TOTAL. Se i dati sono stati troncati a causa dell'attributo di istruzione SQL_ATTR_MAX_LENGTH, il valore di questo attributo viene inserito nel buffer di lunghezza/indicatore anziché nella lunghezza effettiva. Questo perché questo attributo è progettato per troncare i dati sul server prima della conversione, in modo che il driver non ha modo di capire qual è la lunghezza effettiva.  
  
    -   Per tutti gli altri tipi di dati, questa è la lunghezza dei dati dopo la conversione; ovvero, è la dimensione del tipo in cui sono stati convertiti i dati.  
  
     Per informazioni su come determinare l'indirizzo del buffer di lunghezza/indicatore, vedere "Indirizzi buffer" in [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
7.  Se i dati vengono troncati durante la conversione senza una perdita di cifre significative (ad esempio, il numero reale 1.234 viene troncato al numero intero 1 quando viene convertito), **SQLFetch** restituisce SQLSTATE 01S07 (troncamento frazionario) e SQL_SUCCESS_WITH_INFO. Se i dati vengono troncati perché la lunghezza del buffer di dati è troppo piccola (ad esempio, la stringa "abcdef" viene inserita in un buffer a 4 byte), **SQLFetch** restituisce SQLSTATE 01004 (dati troncati) e SQL_SUCCESS_WITH_INFO. Se i dati vengono troncati a causa dell'attributo dell'istruzione SQL_ATTR_MAX_LENGTH, **SQLFetch** restituisce SQL_SUCCESS e non restituisce SQLSTATE 01S07 (troncamento frazionario) o SQLSTATE 01004 (dati troncati). Se i dati vengono troncati durante la conversione con una perdita di cifre significative (ad esempio, se un valore di SQL_INTEGER maggiore di 100.000 sono stati convertiti in un SQL_C_TINYINT), **SQLFetch** restituisce SQLSTATE 22003 (valore numerico non compreso nell'intervallo) e SQL_ERROR (se la dimensione del set di righe è 1) o SQL_SUCCESS_WITH_INFO (se la dimensione del set di righe è maggiore di 1).  
  
 Il contenuto del buffer di dati associato e il buffer di lunghezza/indicatore non sono definiti se **SQLFetch** o **SQLFetchScroll** non restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
## <a name="row-status-array"></a>Matrice di stato riga  
 La matrice di stato della riga viene utilizzata per restituire lo stato di ogni riga nel set di righe. L'indirizzo di questa matrice viene specificato con l'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR. La matrice viene allocata dall'applicazione e deve avere tutti gli elementi specificati dall'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE. I relativi valori vengono impostati da **SQLFetch**, **SQLFetchScroll**e **SQLBulkOperations** o **SQLSetPos** (tranne quando sono stati chiamati dopo che il cursore è stato posizionato da **SQLExtendedFetch**). Se il valore dell'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR è un puntatore null, queste funzioni non restituiscono lo stato della riga.  
  
 Il contenuto del buffer della matrice di stato della riga non è definito se **SQLFetch** o **SQLFetchScroll** non restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
 I valori seguenti vengono restituiti nella matrice di stato della riga.  
  
|Valore della matrice di stato della riga|Descrizione|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|La riga è stata recuperata correttamente e non è stata modificata dall'ultimo recupero da questo set di risultati.|  
|SQL_ROW_SUCCESS_WITH_INFO|La riga è stata recuperata correttamente e non è stata modificata dall'ultimo recupero da questo set di risultati. Tuttavia, è stato restituito un avviso relativo alla riga.|  
|SQL_ROW_ERROR|Si è verificato un errore durante il recupero della riga.|  
|SQL_ROW_UPDATED[1],[2] e [3]|La riga è stata recuperata correttamente ed è stata modificata dall'ultimo recupero da questo set di risultati. Se la riga viene recuperata nuovamente da questo set di risultati o viene aggiornata da **SQLSetPos**, lo stato viene modificato nel nuovo stato della riga.|  
|SQL_ROW_DELETED[3]|La riga è stata eliminata dall'ultima volta che è stata recuperata da questo set di risultati.|  
|SQL_ROW_ADDED[4]|La riga è stata inserita da **SQLBulkOperations**. Se la riga viene recuperata nuovamente da questo set di risultati o viene aggiornata da **SQLSetPos**, il relativo stato è SQL_ROW_SUCCESS.|  
|SQL_ROW_NOROW|Il set di righe si sovrapponeva alla fine del set di risultati e non veniva restituita alcuna riga corrispondente a questo elemento della matrice di stato della riga.|  
  
 [1] Per i cursori keyset, misti e dinamici, se un valore chiave viene aggiornato, la riga di dati viene considerata eliminata e viene aggiunta una nuova riga.  
  
 [2] Alcuni driver non sono in grado di rilevare gli aggiornamenti ai dati e pertanto non possono restituire questo valore. Per determinare se un driver può rilevare gli aggiornamenti alle righe rerecuperate, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_ROW_UPDATES.  
  
 [3] **SQLFetch** può restituire questo valore solo quando è intermixed con chiamate a **SQLFetchScroll**. Ciò è dovuto al fatto che **SQLFetch** si sposta in avanti nel set di risultati e quando viene utilizzato in modo esclusivo, non recupera le righe. Poiché nessuna riga viene recuperata, **SQLFetch** non rileva le modifiche apportate alle righe recuperate in precedenza. Tuttavia, se **SQLFetchScroll** posiziona il cursore prima di qualsiasi riga recuperata in precedenza e **SQLFetch** viene utilizzato per recuperare tali righe, **SQLFetch** è in grado di rilevare eventuali modifiche a tali righe.  
  
 [4] Restituito solo da SQLBulkOperations. Non impostato da **SQLFetch** o **SQLFetchScroll.**  
  
### <a name="rows-fetched-buffer"></a>Righe recuperate Buffer  
 Le righe recuperate buffer viene utilizzato per restituire il numero di righe recuperate, incluse le righe per cui non sono stati restituiti dati perché si è verificato un errore durante il recupero. In altre parole, è il numero di righe per cui il valore nella matrice di stato della riga non è SQL_ROW_NOROW. L'indirizzo di questo buffer viene specificato con l'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR. Il buffer viene allocato dall'applicazione. Viene impostato da **SQLFetch** e **SQLFetchScroll**. Se il valore dell'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR è un puntatore null, queste funzioni non restituiscono il numero di righe recuperate. Per determinare il numero della riga corrente nel set di risultati, un'applicazione può chiamare **SQLGetStmtAttr** con l'attributo SQL_ATTR_ROW_NUMBER.  
  
 Il contenuto delle righe recuperate nel buffer non è definito se **SQLFetch** o **SQLFetchScroll** non restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, tranne quando viene restituito SQL_NO_DATA, nel qual caso il valore nelle righe recuperate buffer è impostato su 0.  
  
### <a name="error-handling"></a>Gestione degli errori  
 Gli errori e gli avvisi possono essere applicati a singole righe o all'intera funzione. Per ulteriori informazioni sui record di diagnostica, vedere [diagnostica](../../../odbc/reference/develop-app/diagnostics.md) e [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>Errori e avvisi sull'intera funzioneErrors and Warnings on the Entire Function  
 Se un errore si applica all'intera funzione, ad esempio SQLSTATE HYT00 (Timeout scaduto) o SQLSTATE 24000 (stato del cursore non valido), **SQLFetch** restituisce SQL_ERROR e SQLSTATE applicabile. Il contenuto dei buffer del set di righe non è definito e la posizione del cursore non è modificata.  
  
 Se un avviso si applica all'intera funzione, **SQLFetch** restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE applicabile. I record di stato per gli avvisi che si applicano all'intera funzione vengono restituiti prima dei record di stato che si applicano alle singole righe.  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>Errori e avvisi nelle singole righeErrors and Warnings in Individual Rows  
 Se un errore (ad esempio SQLSTATE 22012 (Divisione per zero)) o un avviso (ad esempio SQLSTATE 01004 (dati troncati)) si applica a una singola riga, **SQLFetch**esegue le operazioni seguenti:  
  
-   Imposta l'elemento corrispondente della matrice di stato della riga su SQL_ROW_ERROR per gli errori o SQL_ROW_SUCCESS_WITH_INFO per gli avvisi.  
  
-   Aggiunge zero o più record di stato che contengono SQLSTATEs per l'errore o l'avviso.  
  
-   Imposta i campi dei numeri di riga e colonna nei record di stato. Se **SQLFetch** non è in grado di determinare un numero di riga o di colonna, imposta tale numero rispettivamente su SQL_ROW_NUMBER_UNKNOWN o SQL_COLUMN_NUMBER_UNKNOWN. Se il record di stato non si applica a una determinata colonna, **SQLFetch** imposta il numero di colonna su SQL_NO_COLUMN_NUMBER.  
  
 **SQLFetch** continua a recuperare le righe fino a quando non ha recuperato tutte le righe nel set di righe. Restituisce SQL_SUCCESS_WITH_INFO a meno che non si verifichi un errore in ogni riga del set di righe (escluse le righe con stato SQL_ROW_NOROW), nel qual caso restituisce SQL_ERROR. In particolare, se la dimensione del set di righe è 1 e si verifica un errore in tale riga, **SQLFetch** restituisce SQL_ERROR.  
  
 **SQLFetch** restituisce i record di stato nell'ordine dei numeri di riga. Ovvero, restituisce tutti i record di stato per le righe sconosciute (se presenti); next restituisce tutti i record di stato per la prima riga (se presente) e quindi restituisce tutti i record di stato per la seconda riga (se presente) e così via. I record di stato per ogni riga vengono ordinati in base alle normali regole per l'ordinazione dei record di stato; Per ulteriori informazioni, vedere "Sequenza di record di stato" in [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
### <a name="descriptors-and-sqlfetch"></a>Descrittori e SQLFetch  
 Nelle sezioni seguenti viene descritto come **SQLFetch** interagisce con i descrittori.  
  
#### <a name="argument-mappings"></a>Mapping di argomenti  
 Il driver non imposta alcun campo descrittore in base agli argomenti di **SQLFetch**.  
  
#### <a name="other-descriptor-fields"></a>Altri campi descrittore  
 I seguenti campi del descrittore vengono utilizzati da **SQLFetch**.  
  
|Campo di descrizione|Desc.|Campo in|Impostare attraverso|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|Ard|intestazione|attributo SQL_ATTR_ROW_ARRAY_SIZE'istruzione|  
|SQL_DESC_ARRAY_STATUS_PTR|Ird|intestazione|SQL_ATTR_ROW_STATUS_PTR'attributo dell'istruzione|  
|SQL_DESC_BIND_OFFSET_PTR|Ard|intestazione|SQL_ATTR_ROW_BIND_OFFSET_PTR'attributo dell'istruzione|  
|SQL_DESC_BIND_TYPE|Ard|intestazione|SQL_ATTR_ROW_BIND_TYPE'attributo dell'istruzione|  
|SQL_DESC_COUNT|Ard|intestazione|*Argomento ColumnNumber* di **SQLBindCol**|  
|SQL_DESC_DATA_PTR|Ard|record|*Argomento TargetValuePtr* di **SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|Ard|record|*StrLen_or_IndPtr* argomento in **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|Ard|record|*Argomento BufferLength* in **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|Ard|record|*StrLen_or_IndPtr* argomento in **SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|Ird|intestazione|SQL_ATTR_ROWS_FETCHED_PTR'attributo dell'istruzione|  
|SQL_DESC_TYPE|Ard|record|*Argomento TargetType* in **SQLBindCol**|  
  
 Tutti i campi descrittore possono essere impostati anche tramite **SQLSetDescField**.  
  
#### <a name="separate-length-and-indicator-buffers"></a>Buffer di lunghezza e indicatori separati  
 Le applicazioni possono associare un singolo buffer o due buffer separati che possono essere utilizzati per contenere i valori di lunghezza e indicatore. Quando un'applicazione chiama **SQLBindCol**, il driver imposta i campi SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR dell'ARD sullo stesso indirizzo, che viene passato nell'argomento *StrLen_or_IndPtr.* Quando un'applicazione chiama **SQLSetDescField** o **SQLSetDescRec**, è possibile impostare questi due campi su indirizzi diversi.  
  
 **SQLFetch** determina se l'applicazione ha specificato buffer di lunghezza e indicatore separati. In questo caso, quando i dati non sono NULL, **SQLFetch** imposta il buffer dell'indicatore su 0 e restituisce la lunghezza nel buffer di lunghezza. Quando i dati sono NULL, **SQLFetch** imposta il buffer dell'indicatore su SQL_NULL_DATA e non modifica il buffer di lunghezza.  
  
### <a name="code-example"></a>Esempio di codice  
 Vedere [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)e [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md).  
  
### <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di informazioni su una colonna in un set di risultatiReturning information about a column in a result set|[Funzione SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Recupero di un blocco di dati o scorrimento di un set di risultati|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Chiusura del cursore sull'istruzione|[Funzione SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Recupero di parte o di tutta una colonna di dati|[Funzione SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Restituzione del numero di colonne del set di risultatiReturning the number of result set columns|[Funzione SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparazione di un'istruzione per l'esecuzione|[Pagina relativa alla funzione SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
