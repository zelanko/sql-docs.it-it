---
title: Funzione SQLBindCol | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17b907be3e2641fe1dcbbb8fbd96586132e054ca
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65538069"
---
# <a name="sqlbindcol-function"></a>Funzione SQLBindCol
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLBindCol** associa i buffer dei dati dell'applicazione alle colonne nel set di risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLBindCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *ColumnNumber*  
 [Input] Numero del risultato impostato colonna da associare. Le colonne sono numerate in ordine crescente di colonna a partire da 0, in cui colonna 0 è la colonna del segnalibro. Se non vengono usati i segnalibri, vale a dire, l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è impostato su SQL_UB_OFF - numeri di colonna partono da 1.  
  
 *TargetType*  
 [Input] L'identificatore del tipo di dati C il \* *TargetValuePtr* buffer. Durante il recupero dei dati dall'origine dati con **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, oppure **SQLSetPos**, driver converte i dati per questo tipo. Quando invia i dati all'origine dati con **SQLBulkOperations** oppure **SQLSetPos**, il driver converte i dati da questo tipo. Per un elenco di tipi di dati C validi e gli identificatori di tipo, vedere la [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) sezione nell'appendice d: Tipi di dati.  
  
 Se il *TargetType* argomento è un tipo di dati di intervallo, la precisione iniziale intervallo predefinito (2) e la precisione dei secondi di intervallo predefinito (6), come set nei campi SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION di ARD, rispettivamente, vengono usati per i dati. Se il *TargetType* argomento SQL_C_NUMERIC, la precisione predefinita (definiti dal driver) e predefinito di scalabilità (0), come impostato nei campi SQL_DESC_PRECISION e SQL_DESC_SCALE del ARD, vengono usato per i dati. Se qualsiasi precisione predefinita o la scala non è appropriata, l'applicazione deve impostare in modo esplicito il campo di descrizione appropriato da una chiamata a **SQLSetDescField** oppure **SQLSetDescRec**.  
  
 È anche possibile specificare un tipo di dati C esteso. Per altre informazioni, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Input/Output differito] Puntatore al buffer di dati da associare alla colonna. **SQLFetch** e **SQLFetchScroll** restituire i dati in questo buffer. **SQLBulkOperations** restituisce i dati in questo buffer quando *operazione* è SQL_FETCH_BY_BOOKMARK; recupera dati da questo buffer quando *operazione* rappresenti SQL_UPDATE_BY_BOOKMARK SQL_ADD. **SQLSetPos** restituisce i dati in questo buffer quando *operazione* è SQL_REFRESH; recupera dati da questo buffer quando *operazione* è SQL_UPDATE.  
  
 Se *TargetValuePtr* è un puntatore null, il driver viene disassociato il buffer di dati per la colonna. Un'applicazione può annullare l'associazione di tutte le colonne chiamando **SQLFreeStmt** con l'opzione SQL_UNBIND. Un'applicazione può separare il buffer di dati per una colonna ma non è stato un buffer di lunghezza/indicatore associato per la colonna, se il *TargetValuePtr* argomento nella chiamata a **SQLBindCol** è un puntatore null, ma il *StrLen_or_IndPtr* argomento è un valore valido.  
  
 *BufferLength*  
 [Input] Lunghezza di **TargetValuePtr* buffer in byte.  
  
 Il driver utilizza *BufferLength* per evitare di scrivere oltre la fine del \* *TargetValuePtr* memorizzare nel buffer quando vengono restituiti i dati a lunghezza variabile, ad esempio carattere o dati binari. Si noti che il driver viene considerato il carattere di terminazione null quando vengono restituiti i dati di carattere per \* *TargetValuePtr*. **TargetValuePtr* deve pertanto contenere spazio per il carattere di terminazione di tipo null o il driver verrà troncare i dati.  
  
 Quando il driver restituisce i dati a lunghezza fissa, ad esempio un numero intero o una struttura di data, il driver ignora *BufferLength* e presuppone che il buffer sia sufficientemente grande da contenere i dati. Pertanto, è importante per l'applicazione allocare un buffer sufficiente per i dati a lunghezza fissa o il driver verrà scritto oltre la fine del buffer.  
  
 **SQLBindCol** restituisce SQLSTATE HY090 (stringa di lunghezza o non valida del buffer) quando *BufferLength* è minore di 0 ma non quando *BufferLength* è 0. Tuttavia, se *TargetType* specifica un tipo di carattere, un'applicazione non è consigliabile impostare *BufferLength* su 0, poiché i driver conforme a ISO CLI restituiscono SQLSTATE HY090 (stringa di lunghezza o non valida del buffer) in quanto case.  
  
 *StrLen_or_IndPtr*  
 [Input/Output differito] Puntatore al buffer di lunghezza/indicatore da associare alla colonna. **SQLFetch** e **SQLFetchScroll** restituiscono un valore di questo buffer. **SQLBulkOperations** recupera un valore da questo buffer quando *operazione* è SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK. **SQLBulkOperations** restituisce un valore in questo buffer quando *operazione* è SQL_FETCH_BY_BOOKMARK. **SQLSetPos** restituisce un valore in questo buffer quando *operazione* è SQL_REFRESH; recupera un valore da questo buffer quando *operazione* è SQL_UPDATE.  
  
 **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, e **SQLSetPos** può restituire i valori seguenti nel buffer di lunghezza/indicatore:  
  
-   La lunghezza dei dati disponibili da restituire  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 L'applicazione può inserire i valori seguenti nel buffer di lunghezza/indicatore per l'uso con **SQLBulkOperations** oppure **SQLSetPos**:  
  
-   La lunghezza dei dati inviati  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   Il risultato della macro SQL_LEN_DATA_AT_EXEC  
  
-   SQL_COLUMN_IGNORE  
  
 Se il buffer di indicatore e il buffer di lunghezza sono buffer distinti, il buffer di indicatore può restituire solo SQL_NULL_DATA, mentre il buffer di lunghezza può restituire tutti gli altri valori.  
  
 Per altre informazioni, vedere [funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md), [funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), e [usando i valori di lunghezza/indicatore](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Se *StrLen_or_IndPtr* viene usato un valore di puntatore, alcuna lunghezza o indicatore null. Si tratta di un errore durante il recupero dei dati e i dati è NULL.  
  
 Visualizzare [le informazioni ODBC 64-Bit](../../../odbc/reference/odbc-64-bit-information.md), se l'applicazione verrà eseguita in un sistema operativo a 64 bit.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLBindCol** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLBindCol** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07006|Violazione dell'attributo del tipo di dati|(DM) di *ColumnNumber* argomento era 0 e il *TargetType* argomento non è stata SQL_C_BOOKMARK o SQL_C_VARBOOKMARK.|  
|07009|Indice del descrittore non valido|Il valore specificato per l'argomento *ColumnNumber* superato il numero massimo di colonne nel set di risultati.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver non è riuscito ad allocare memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY003|Tipo di buffer dell'applicazione non valido|L'argomento *TargetType* era né un tipo di dati valido né SQL_C_DEFAULT.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando **SQLBindCol** è stato chiamato.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione la *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore specificato per l'argomento *BufferLength* era minore di 0.<br /><br /> (DM) il driver è stato un ODBC 2. *x* driver, il *ColumnNumber* argomento è stato impostato su 0 e il valore specificato per l'argomento *BufferLength* non è uguale a 4.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|L'origine dati o driver non supporta la conversione specificata dalla combinazione dei *TargetType* argomento e il tipo di dati specifici del driver SQL della colonna corrispondente.<br /><br /> L'argomento *ColumnNumber* era pari a 0 e il driver non supporta i segnalibri.<br /><br /> Il driver supporta solo l'API ODBC 2. *x* e l'argomento *TargetType* era una delle operazioni seguenti:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> uno dei tipi di dati di intervallo C sono elencati nella [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) nell'appendice d: Tipi di dati.<br /><br /> Il driver supporta solo le versioni ODBC precedenti alla versione 3.50 e l'argomento *TargetType* era SQL_C_GUID.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 **SQLBindCol** viene usato per associare, oppure *associare,* colonne nel risultato impostate per i buffer dei dati e buffer di lunghezza/indicatore nell'applicazione. Quando l'applicazione chiama **SQLFetch**, **SQLFetchScroll**, o **SQLSetPos** per recuperare i dati, il driver restituisce i dati per le colonne associate nel buffer specificato; per altre informazioni, vedere [SQLFetch-funzione](../../../odbc/reference/syntax/sqlfetch-function.md). Quando l'applicazione chiama **SQLBulkOperations** per aggiornare o inserire una riga oppure **SQLSetPos** per aggiornare una riga, il driver può recuperare i dati per le colonne associate dal buffer specificato; per altre informazioni , vedere [funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) oppure [funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md). Per altre informazioni sul binding, vedere [recupero di risultati (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 Si noti che le colonne non sono necessario essere associato a recuperare i dati da essi. Un'applicazione può anche chiamare **SQLGetData** per recuperare i dati dalle colonne. Sebbene sia possibile associare alcune colonne in una riga e chiamare **SQLGetData** per altri utenti, è soggetto ad alcune limitazioni. Per altre informazioni, vedere [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>Associazione, annullamento dell'associazione e riassociazione di colonne  
 Una colonna può essere associata, non associata o riassociata in qualunque momento, anche dopo che i dati sono stati recuperati dal set di risultati. La nuova associazione viene applicata la prossima volta che viene chiamata una funzione che utilizza le associazioni. Ad esempio, si supponga che un'applicazione associa le colonne in un set di risultati e le chiamate **SQLFetch**. Il driver restituisce i dati nei buffer associato. Ora si supponga che l'applicazione associa le colonne da un set diverso di buffer. Il driver non inserire i dati per la riga recuperata solo nei buffer appena associato. In alternativa, è in attesa fino al **SQLFetch** viene chiamato di nuovo e quindi inserisce i dati per la riga successiva nel buffer appena associato.  
  
> [!NOTE]  
>  L'attributo di istruzione SQL_ATTR_USE_BOOKMARKS deve sempre essere impostata prima di associare un valore 0 per una colonna. Questo non è obbligatorio ma è fortemente consigliato.  
  
## <a name="binding-columns"></a>Associazione di colonne  
 Per associare una colonna, un'applicazione chiama **SQLBindCol** e passa il numero di colonna, tipo, indirizzo e lunghezza di un buffer di dati e l'indirizzo di un buffer di lunghezza/indicatore. Per informazioni sull'uso di questi indirizzi, vedere "Buffer indirizzi" più avanti in questa sezione. Per altre informazioni sull'associazione delle colonne, vedere [SQLBindCol usando](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 L'utilizzo di tali buffer viene rinviata; vale a dire, l'applicazione associa nella **SQLBindCol** ma il driver accede ad essi da altre funzioni, vale a dire **SQLBulkOperations**, **SQLFetch**,  **SQLFetchScroll**, oppure **SQLSetPos**. È responsabilità dell'applicazione per assicurarsi che gli indicatori di misura specificato nel **SQLBindCol** rimangono valide fino a quando l'associazione rimane effettiva. Se l'applicazione consente a questi puntatori non saranno più validi, ad esempio, libera un buffer - e quindi chiama una funzione che prevede che siano validi, le conseguenze sono definite. Per altre informazioni, vedere [buffer con rinviata](../../../odbc/reference/develop-app/deferred-buffers.md).  
  
 L'associazione rimane effettiva fino a quando non viene sostituita da una nuova associazione, la colonna non è associata o l'istruzione viene liberata.  
  
## <a name="unbinding-columns"></a>Annullamento dell'associazione di colonne  
 Per disassociare una singola colonna, un'applicazione chiama **SQLBindCol** con *ColumnNumber* impostato sul numero di colonna e *TargetValuePtr* impostato su un puntatore null. Se *ColumnNumber* fa riferimento a una colonna non associata, **SQLBindCol** ancora restituisce SQL_SUCCESS.  
  
 Per disassociare tutte le colonne, un'applicazione chiama **SQLFreeStmt** con *fOption* impostato su SQL_UNBIND. Ciò può essere effettuata anche impostando il campo SQL_DESC_COUNT di ARD su zero.  
  
## <a name="rebinding-columns"></a>Riassociazione delle colonne  
 Un'applicazione può eseguire una delle due operazioni per modificare un'associazione:  
  
-   Chiamare **SQLBindCol** per specificare un nuovo binding per una colonna in cui è già associato. Il driver sovrascrive il binding precedente con quello nuovo.  
  
-   Specificare un offset da aggiungere per l'indirizzo del buffer specificato dalla chiamata all'associazione **SQLBindCol**. Per altre informazioni, vedere la sezione successiva, "Offset di associazione".  
  
## <a name="binding-offsets"></a>Offset di associazione  
 Un offset di associazione è un valore che viene aggiunto agli indirizzi dei buffer di dati e lunghezza/indicatore (come specificato nella *TargetValuePtr* e *StrLen_or_IndPtr* argomento) prima che essi vengono dereferenziati. Quando vengono utilizzati gli offset, le associazioni sono un "modello" della modalità di disposizione i buffer dell'applicazione e l'applicazione può passare questa "modello" a diverse aree di memoria tramite la modifica dell'offset. Poiché lo stesso offset viene aggiunto a ogni indirizzo in ogni associazione, gli offset relativi tra i buffer per colonne diverse devono corrispondere all'interno di ogni set di buffer. Ciò vale sempre quando viene utilizzata l'associazione per riga. l'applicazione con attenzione deve disporre i relativi buffer per questo oggetto essere vera quando viene utilizzata l'associazione per colonna.  
  
 Utilizzando un offset di associazione è fondamentalmente lo stesso effetto la riassociazione della colonna chiamando **SQLBindCol**. La differenza è che una nuova chiamata a **SQLBindCol** specifica nuovi indirizzi per il buffer di dati e buffer di lunghezza/indicatore, mentre l'utilizzo di un offset di associazione non modifica gli indirizzi, ma semplicemente aggiunge un offset a essi. L'applicazione può specificare un offset di nuovo ogni volta che desidera, e l'offset viene sempre aggiunto agli indirizzi di origine associati. In particolare, se l'offset viene impostato su 0 o se l'attributo di istruzione è impostata su un puntatore null, il driver utilizza gli indirizzi di origine associati.  
  
 Per specificare un offset di associazione, l'applicazione imposta l'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR all'indirizzo di un buffer SQLINTEGER. Prima che l'applicazione chiama una funzione che utilizza le associazioni, inserisce un offset in byte di questo buffer. Per determinare l'indirizzo del buffer da usare, il driver aggiunge l'offset per l'indirizzo nell'associazione. La somma dell'indirizzo e l'offset deve essere un indirizzo valido, ma l'indirizzo a cui viene aggiunta l'offset non deve essere valido. Per altre informazioni sull'utilizzo di offset di associazione, vedere "Buffer indirizzi" più avanti in questa sezione.  
  
## <a name="binding-arrays"></a>Associazione delle matrici  
 Se la dimensione di set di righe (il valore dell'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE) è maggiore di 1, l'applicazione associa le matrici di buffer anziché singolo buffer. Per altre informazioni, vedere [cursori a blocchi](../../../odbc/reference/develop-app/block-cursors.md).  
  
 L'applicazione può associare le matrici in due modi:  
  
-   Associare una matrice per ogni colonna. Ciò è detto *associazione per colonna* perché ogni struttura di data (array) contiene i dati per una singola colonna.  
  
-   Definire una struttura per contenere i dati per una riga intera e associare una matrice di queste strutture. Ciò è detto *l'associazione per riga* perché ogni struttura di dati contiene i dati per una singola riga.  
  
 Ogni matrice di buffer deve avere almeno un numero di elementi come le dimensioni del set di righe.  
  
> [!NOTE]  
>  Un'applicazione deve verificare che l'allineamento è valido. Per altre informazioni sulle considerazioni relative all'allineamento, vedere [allineamento](../../../odbc/reference/develop-app/alignment.md).  
  
## <a name="column-wise-binding"></a>Associazione per colonna  
 Nell'associazione per colonna, l'applicazione associa dati separati e le matrici di lunghezza/indicatore a ogni colonna.  
  
 Per utilizzare l'associazione, l'applicazione imposta innanzitutto l'attributo di istruzione SQL_ATTR_ROW_BIND_TYPE su SQL_BIND_BY_COLUMN. (Questo è il valore predefinito). Per ogni colonna deve essere associato, l'applicazione esegue i passaggi seguenti:  
  
1.  Alloca una matrice di buffer di dati.  
  
2.  Alloca una matrice di buffer di lunghezza/indicatore.  
  
    > [!NOTE]  
    >  Se l'applicazione scrive direttamente i descrittori quando viene utilizzata l'associazione per colonna, matrici distinte è utilizzabile per i dati di lunghezza e indicatore.  
  
3.  Le chiamate **SQLBindCol** con gli argomenti seguenti:  
  
    -   *TargetType* è il tipo di un singolo elemento nella matrice di buffer di dati.  
  
    -   *TargetValuePtr* è l'indirizzo della matrice di buffer di dati.  
  
    -   *BufferLength* è la dimensione di un singolo elemento nella matrice di buffer di dati. Il *BufferLength* argomento viene ignorato quando i dati sono dati a lunghezza fissa.  
  
    -   *StrLen_or_IndPtr* è l'indirizzo della matrice di lunghezza/indicatore.  
  
 Per altre informazioni sull'utilizzo di queste informazioni, vedere "Buffer indirizzi" più avanti in questa sezione. Per altre informazioni sull'associazione per colonna, vedere [associazione per colonna](../../../odbc/reference/develop-app/column-wise-binding.md).  
  
## <a name="row-wise-binding"></a>Associazione per riga  
 Nell'associazione per riga, l'applicazione definisce una struttura che contiene i buffer di dati e lunghezza/indicatore per ogni colonna da associare.  
  
 Per usare l'associazione per riga, l'applicazione esegue i passaggi seguenti:  
  
1.  Definisce una struttura per contenere una singola riga di dati, inclusi i buffer di lunghezza/indicatore sia i dati e consente di allocare una matrice di queste strutture.  
  
    > [!NOTE]  
    >  Se l'applicazione scrive direttamente i descrittori quando viene utilizzata l'associazione per riga, è possono utilizzare campi separati per i dati di lunghezza e indicatore.  
  
2.  Imposta l'attributo di istruzione SQL_ATTR_ROW_BIND_TYPE sulla dimensione della struttura che contiene una singola riga di dati o alle dimensioni di un'istanza di un buffer in cui verranno associate le colonne di risultati. La lunghezza deve includere lo spazio per tutte le colonne associate ed eventuale riempimento della struttura o del buffer, per assicurarsi che quando l'indirizzo di una colonna associata viene incrementato con la lunghezza specificata, il risultato punterà all'inizio della stessa colonna nella riga successiva. Quando si usa la *sizeof* operatore in ANSI C, questo comportamento è garantito.  
  
3.  Le chiamate **SQLBindCol** con gli argomenti seguenti per ogni colonna deve essere associato:  
  
    -   *TargetType* è il tipo del membro da associare alla colonna del buffer dei dati.  
  
    -   *TargetValuePtr* è l'indirizzo del membro nel primo elemento della matrice buffer dei dati.  
  
    -   *BufferLength* è la dimensione del membro dati del buffer.  
  
    -   *StrLen_or_IndPtr* è l'indirizzo del membro lunghezza/indicatore da associare.  
  
 Per altre informazioni sull'utilizzo di queste informazioni, vedere "Buffer indirizzi" più avanti in questa sezione. Per altre informazioni sull'associazione per colonna, vedere [associazione per riga](../../../odbc/reference/develop-app/row-wise-binding.md).  
  
## <a name="buffer-addresses"></a>Indirizzi di buffer  
 Il *indirizzo del buffer* è l'indirizzo effettivo del buffer di dati o di lunghezza/indicatore. Il driver calcola l'indirizzo del buffer appena prima che vengano scritte per i buffer (ad esempio durante i tempi di recupero). Viene calcolato dalla formula seguente, che usa gli indirizzi specificati nella *TargetValuePtr* e *StrLen_or_IndPtr* argomenti, l'offset di associazione e il numero di riga:  
  
 *Indirizzo associato* + *associazione Offset* + ((*il numero di riga* - 1) x *dimensione dell'elemento*)  
  
 le variabili della formula in cui vengono definite come descritto nella tabella seguente.  
  
|Variabile|Descrizione|  
|--------------|-----------------|  
|*Associare l'indirizzo*|Per i buffer dei dati, l'indirizzo specificato con il *TargetValuePtr* nell'argomento **SQLBindCol**.<br /><br /> Per i buffer di lunghezza/indicatore, l'indirizzo specificato con il *StrLen_or_IndPtr* nell'argomento **SQLBindCol**. Per altre informazioni, vedere "Commenti aggiuntivi" nella sezione "Descrittori e SQLBindCol".<br /><br /> Se l'indirizzo associato è 0, viene restituito alcun valore di dati, anche se l'indirizzo calcolato dalla formula precedente è diverso da zero.|  
|*Offset di associazione*|Se viene utilizzata l'associazione per riga, il valore archiviato in corrispondenza dell'indirizzo specificato con l'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR.<br /><br /> Se viene utilizzata l'associazione per colonna o se il valore dell'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR è un puntatore null, *associazione Offset* è 0.|  
|*Numero di riga*|Il numero di riga nel set di righe in base 1. Per operazioni di recupero riga singola, ovvero l'impostazione predefinita, questo è 1.|  
|*Dimensione dell'elemento*|Le dimensioni di un elemento di matrice associata.<br /><br /> Se viene utilizzata l'associazione per colonna, si tratta **sizeof(SQLINTEGER)** per i buffer di lunghezza/indicatore. Per i buffer dei dati, è il valore della *BufferLength* nell'argomento **SQLBindCol** se il tipo di dati è di lunghezza variabile e la dimensione del tipo di dati se il tipo di dati è a lunghezza fissa.<br /><br /> Se viene utilizzata l'associazione per riga, questo è il valore dell'attributo dell'istruzione SQL_ATTR_ROW_BIND_TYPE i buffer di dati e lunghezza/indicatore.|  
  
## <a name="descriptors-and-sqlbindcol"></a>Descrittori e SQLBindCol  
 Le sezioni seguenti descrivono come **SQLBindCol** interagisce con i descrittori.  
  
> [!CAUTION]  
>  La chiamata **SQLBindCol** per un'unica istruzione può influire sulle altre istruzioni. Ciò si verifica quando il ARD associate all'istruzione viene allocato in modo esplicito ed è anche associato con le altre istruzioni. In quanto **SQLBindCol** modifica il descrittore, le modifiche si applicano a tutte le istruzioni a cui è associato questo descrittore. Se questo non è il comportamento richiesto, l'applicazione deve annullare l'associazione di questo descrittore da altre istruzioni prima di chiamare **SQLBindCol**.  
  
## <a name="argument-mappings"></a>Mapping di argomento  
 Concettualmente **SQLBindCol** esegue i passaggi seguenti in sequenza:  
  
1.  Le chiamate **SQLGetStmtAttr** per ottenere l'handle ARD.  
  
2.  Le chiamate **SQLGetDescField** per ottenere SQL_DESC_COUNT campo del descrittore e se il valore nel *ColumnNumber* argomento supera il valore di SQL_DESC_COUNT, chiamate **SQLSetDescField**  per aumentare il valore di SQL_DESC_COUNT al *ColumnNumber*.  
  
3.  Le chiamate **SQLSetDescField** più volte per assegnare valori ai campi seguenti del ARD:  
  
    -   Imposta il valore di SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE *TargetType*, ad eccezione del fatto che se *TargetType* è uno degli identificatori concisi di un sottotipo di datetime o intervallo, imposta SQL_DESC_TYPE SQL _ Data/ora o SQL_INTERVAL, rispettivamente. Imposta SQL_DESC_CONCISE_TYPE all'identificatore concisa; e set SQL_DESC_DATETIME_INTERVAL_CODE alla data/ora corrispondente o sottocodice intervallo.  
  
    -   Imposta una o più delle SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_DATETIME_INTERVAL_PRECISION, a seconda del *TargetType*.  
  
    -   Imposta sul valore del campo SQL_DESC_OCTET_LENGTH *BufferLength*.  
  
    -   Imposta sul valore del campo SQL_DESC_DATA_PTR *valore di destinazione*.  
  
    -   Imposta sul valore del campo SQL_DESC_INDICATOR_PTR *StrLen_or_Ind*. (Vedere il paragrafo seguente).  
  
    -   Imposta sul valore del campo SQL_DESC_OCTET_LENGTH_PTR *StrLen_or_Ind*. (Vedere il paragrafo seguente).  
  
 La variabile che il *StrLen_or_Ind* argomento fa riferimento a scopo informativo sia indicatore di lunghezza. Se un'operazione di recupero rileva un valore null per la colonna, SQL_NULL_DATA archivia nella variabile; in caso contrario, archivia la lunghezza dei dati in questa variabile. Passando un puntatore null come *StrLen_or_Ind* mantiene l'operazione di recupero restituisca la lunghezza dei dati, ma rende l'operazione di recupero non riesce se rileva un valore null e non è in grado di restituire SQL_NULL_DATA.  
  
 Se la chiamata a **SQLBindCol** ha esito negativo, il contenuto dei campi di descrizione che sarebbe impostato nel ARD sono definiti e il valore del campo SQL_DESC_COUNT del ARD rimane invariato.  
  
## <a name="implicit-resetting-of-count-field"></a>La reimpostazione implicita del campo del conteggio  
 **SQLBindCol** imposta il valore di SQL_DESC_COUNT il *ColumnNumber* argomento solo quando questo aumenterebbe il valore di SQL_DESC_COUNT. Se il valore nel *TargetValuePtr* argomento è un puntatore null e il valore nel *ColumnNumber* argomento è uguale a SQL_DESC_COUNT (vale a dire, se disassociare il più alto vengono associati colonna), quindi SQL_DESC_ CONTEGGIO è impostato per il numero della colonna associata rimanente più alta.  
  
## <a name="cautions-regarding-sqldefault"></a>Cautions Regarding SQL_DEFAULT  
 Per recuperare correttamente i dati della colonna, l'applicazione deve determinare correttamente la lunghezza e il punto iniziale dei dati nel buffer dell'applicazione. Quando l'applicazione specifica esplicita *TargetType*, rilevare facilmente convinzioni erronee dell'applicazione. Tuttavia, quando l'applicazione specifica un *TargetType* di SQL_DEFAULT, **SQLBindCol** può essere applicato a una colonna di un tipo di dati diversa da quella desiderata con l'applicazione, da modifiche al i metadati o applicando il codice in una colonna diversa. L'applicazione non può in questo caso, sempre determinare l'inizio o la lunghezza dei dati della colonna recuperata. Ciò potrebbe causare errori dati illegali o violazioni della memoria.  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, un'applicazione esegue una **seleziona** istruzione sulla tabella Customers per restituire un set di risultati del cliente, ID, nomi e numeri di telefono, ordinati in base al nome. Chiama poi **SQLBindCol** per associare le colonne di dati ai buffer locale. Infine, l'applicazione recupera ciascuna riga di dati con **SQLFetch** e stampa ogni customer name, ID e il numero di telefono.  
  
 Per altri esempi di codice, vedere [funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [funzione SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md), e [SQLSetPos funzione](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 20  
  
void show_error() {  
   printf("error\n");  
}  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
   SQLWCHAR szName[NAME_LEN], szPhone[PHONE_LEN], sCustID[NAME_LEN];  
   SQLLEN cbName = 0, cbCustID = 0, cbPhone = 0;  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLWCHAR*) L"NorthWind", SQL_NTS, (SQLWCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {   
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               retcode = SQLExecDirect(hstmt, (SQLWCHAR *) L"SELECT CustomerID, ContactName, Phone FROM CUSTOMERS ORDER BY 2, 1, 3", SQL_NTS);  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
                  // Bind columns 1, 2, and 3  
                  retcode = SQLBindCol(hstmt, 1, SQL_C_CHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (i ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                        wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                     else  
                        break;  
                  }  
               }  
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLCancel(hstmt);  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 Vedere anche [programma di esempio ODBC](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituzione di informazioni relative a una colonna in un set di risultati|[Funzione SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Imposta il recupero di un blocco di dati o lo scorrimento di un risultato|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Il recupero di più righe di dati|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Il buffer delle colonne nell'istruzione di rilascio|[Funzione SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Durante il recupero o parte di una colonna di dati|[Funzione SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Colonne del set di restituzione del numero di risultati|[Funzione SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
