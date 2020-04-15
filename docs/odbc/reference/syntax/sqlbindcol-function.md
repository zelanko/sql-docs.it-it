---
title: 'Funzione SQLBindCol : Documenti Microsoft'
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
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90bb1c1aa4dbfa2614f689faa47eb0c41a6cecd6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298741"
---
# <a name="sqlbindcol-function"></a>Funzione SQLBindCol
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLBindCol** associa i buffer di dati dell'applicazione alle colonne nel set di risultati.  
  
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
 [Ingresso] Handle di istruzione.  
  
 *ColumnNumber*  
 [Ingresso] Numero della colonna del set di risultati da associare. Le colonne sono numerate in ordine crescente di colonna a partire da 0, dove la colonna 0 è la colonna del segnalibro. Se i segnalibri non vengono utilizzati, ovvero l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è impostato su SQL_UB_OFF, i numeri di colonna iniziano da 1.  
  
 *Targettype*  
 [Ingresso] Identificatore del tipo di \*dati C del buffer *TargetValuePtr.* Quando recupera dati dall'origine dati con **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**o **SQLSetPos**, il driver converte i dati in questo tipo; quando invia dati all'origine dati con **SQLBulkOperations** o **SQLSetPos**, il driver converte i dati da questo tipo. Per un elenco dei tipi di dati C validi e degli identificatori di tipo, vedere la sezione Tipi di [dati C](../../../odbc/reference/appendixes/c-data-types.md) nell'Appendice D: Tipi di dati.  
  
 Se l'argomento *TargetType* è un tipo di dati intervallo, per i dati vengono utilizzati rispettivamente la precisione di interlinea predefinita (2) e la precisione predefinita dei secondi dell'intervallo (6), come impostato nei campi SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION dell'ARD. Se l'argomento *TargetType* è SQL_C_NUMERIC, per i dati vengono utilizzate la precisione predefinita (definita dal driver) e la scala predefinita (0), come impostato nei campi SQL_DESC_PRECISION e SQL_DESC_SCALE dell'ARD. Se la precisione o la scala predefinita non è appropriata, l'applicazione deve impostare in modo esplicito il campo del descrittore appropriato tramite una chiamata a **SQLSetDescField** o **SQLSetDescRec**.  
  
 È inoltre possibile specificare un tipo di dati C esteso. Per ulteriori informazioni, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Ingresso/uscita posticipato] Puntatore al buffer di dati da associare alla colonna. **SQLFetch** e **SQLFetchScroll** restituiscono dati in questo buffer. **SQLBulkOperations** restituisce i dati in questo buffer quando *Operation* è SQL_FETCH_BY_BOOKMARK; recupera i dati da questo buffer quando *Operation* è SQL_ADD o SQL_UPDATE_BY_BOOKMARK. **SQLSetPos** restituisce i dati in questo buffer quando *Operation* è SQL_REFRESH; recupera i dati da questo buffer quando *Operation* è SQL_UPDATE.  
  
 Se *TargetValuePtr* è un puntatore null, il driver annulla l'associazione del buffer di dati per la colonna. Un'applicazione può annullare l'associazione di tutte le colonne chiamando **SQLFreeStmt** con l'opzione SQL_UNBIND. Un'applicazione può annullare l'associazione del buffer di dati per una colonna ma avere ancora un buffer di lunghezza/indicatore associato per la colonna, se il *TargetValuePtr* argomento nella chiamata a **SQLBindCol** è un puntatore null, ma il *StrLen_or_IndPtr* argomento è un valore valido.  
  
 *BufferLength*  
 [Ingresso] Lunghezza del \*buffer *TargetValuePtr* in byte.  
  
 Il driver utilizza *BufferLength* per evitare \*di scrivere oltre la fine del *TargetValuePtr* buffer quando restituisce dati a lunghezza variabile, ad esempio dati di tipo carattere o binario. Si noti che il driver conta il carattere di terminazione null quando restituisce dati di tipo carattere a \* *TargetValuePtr*. \**TargetValuePtr* deve quindi contenere spazio per il carattere di terminazione null o il driver tronca i dati.  
  
 Quando il driver restituisce dati a lunghezza fissa, ad esempio un numero intero o una struttura di data, il driver ignora *BufferLength* e presuppone che il buffer è sufficientemente grande per contenere i dati. Pertanto, è importante per l'applicazione allocare un buffer sufficientemente grande per i dati a lunghezza fissa o il driver scriverà oltre la fine del buffer.  
  
 **SQLBindCol** restituisce SQLSTATE HY090 (stringa non valida o lunghezza del buffer) quando *BufferLength* è minore di 0 ma non quando *BufferLength* è 0. Tuttavia, se *TargetType* specifica un tipo di carattere, un'applicazione non deve impostare *BufferLength* su 0, perché i driver conformi all'interfaccia della riga di comando ISO restituiscono SQLSTATE HY090 (stringa non valida o lunghezza del buffer) in questo caso.  
  
 *StrLen_or_IndPtr*  
 [Ingresso/uscita posticipato] Puntatore al buffer di lunghezza/indicatore da associare alla colonna. **SQLFetch** e **SQLFetchScroll** restituiscono un valore in questo buffer. **SQLBulkOperations** recupera un valore da questo buffer quando *Operation* è SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK. **SQLBulkOperations** restituisce un valore in questo buffer quando *Operation* è SQL_FETCH_BY_BOOKMARK. **SQLSetPos** restituisce un valore in questo buffer quando *Operation* è SQL_REFRESH; recupera un valore da questo buffer quando *Operation* è SQL_UPDATE.  
  
 **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**e **SQLSetPos** possono restituire i valori seguenti nel buffer di lunghezza/indicatore:  
  
-   La lunghezza dei dati disponibili per la restituzione  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 L'applicazione può inserire i seguenti valori nel buffer di lunghezza/indicatore per **l'utilizzo con SQLBulkOperations** o **SQLSetPos**:  
  
-   La lunghezza dei dati inviati  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   Il risultato della macro SQL_LEN_DATA_AT_EXEC  
  
-   SQL_COLUMN_IGNORE  
  
 Se il buffer dell'indicatore e il buffer di lunghezza sono buffer separati, il buffer dell'indicatore può restituire solo SQL_NULL_DATA, mentre il buffer di lunghezza può restituire tutti gli altri valori.  
  
 Per ulteriori informazioni, vedere [Funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md), [Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)e [Utilizzo dei valori di lunghezza/indicatore](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Se *StrLen_or_IndPtr* è un puntatore null, non viene utilizzato alcun valore di lunghezza o indicatore. Si tratta di un errore durante il recupero dei dati e i dati sono NULL.  
  
 Vedere [Informazioni a 64 bit ODBC](../../../odbc/reference/odbc-64-bit-information.md), se l'applicazione verrà eseguita in un sistema operativo a 64 bit.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLBindCol** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLBindCol** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07006|Violazione dell'attributo del tipo di dati con restrizioniRestricted data type attribute violation|(DM) *l'argomento ColumnNumber* era 0 e l'argomento *TargetType* non era SQL_C_BOOKMARK o SQL_C_VARBOOKMARK.|  
|07009|Indice descrittore non valido|Il valore specificato per l'argomento *NumeroColonna ha* superato il numero massimo di colonne nel set di risultati.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY003|Tipo di buffer dell'applicazione non valido|L'argomento *TargetType* non è né un tipo di dati valido né SQL_C_DEFAULT.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando **SQLBindCol** è stato chiamato.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono è stata chiamata per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore specificato per l'argomento *BufferLength* era minore di 0.<br /><br /> (DM) Il driver era un ODBC 2. *x* driver, il *ColumnNumber* argomento è stato impostato su 0 e il valore specificato per l'argomento *BufferLength* non è uguale a 4.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il driver o l'origine dati non supporta la conversione specificata dalla combinazione del *TargetType* argomento e il tipo di dati SQL specifico del driver della colonna corrispondente.<br /><br /> L'argomento *ColumnNumber* era 0 e il driver non supporta i segnalibri.<br /><br /> Il driver supporta solo ODBC 2. *x* e l'argomento *TargetType* è uno dei seguenti:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e uno qualsiasi dei tipi di dati di intervallo C elencati in [Tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) nell'Appendice D: Tipi di dati.<br /><br /> Il driver supporta solo le versioni ODBC precedenti alla 3.50 e l'argomento *TargetType* è stato SQL_C_GUID.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 **SQLBindCol** viene utilizzato per associare, o *associare,* le colonne nel set di risultati ai buffer di dati e ai buffer di lunghezza/indicatore nell'applicazione. Quando l'applicazione chiama **SQLFetch**, **SQLFetchScroll**o **SQLSetPos** per recuperare i dati, il driver restituisce i dati per le colonne associate nei buffer specificati; Per ulteriori informazioni, vedere [Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md). Quando l'applicazione chiama **SQLBulkOperations** per aggiornare o inserire una riga o **SQLSetPos** per aggiornare una riga, il driver recupera i dati per le colonne associate dai buffer specificati; Per ulteriori informazioni, vedere [Funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) o [Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md). Per ulteriori informazioni sull'associazione, vedere [Recupero di risultati (base)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 Si noti che non è necessario associare le colonne per recuperare i dati da esse. Un'applicazione può anche chiamare **SQLGetData** per recuperare i dati dalle colonne. Sebbene sia possibile associare alcune colonne in una riga e chiamare **SQLGetData** per altri, è soggetto ad alcune restrizioni. Per ulteriori informazioni, vedere [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>Associazione, annullamento dell'associazione e riassociazione delle colonneBinding, Unbinding, and Rebinding Columns  
 Una colonna può essere associata, non associata o riassociata in qualsiasi momento, anche dopo che i dati sono stati recuperati dal set di risultati. La nuova associazione ha effetto la volta successiva che viene chiamata una funzione che utilizza le associazioni. Si supponga, ad esempio, che un'applicazione associa le colonne in un set di risultati e **chiami SQLFetch**. Il driver restituisce i dati nei buffer associati. Si supponga ora che l'applicazione associa le colonne a un set di buffer diverso. Il driver non inserisce i dati per la riga appena recuperata nei buffer appena associati. Al contrario, attende fino a quando **SQLFetch** viene chiamato nuovamente e quindi inserisce i dati per la riga successiva nei buffer appena associati.  
  
> [!NOTE]  
>  L'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS deve essere sempre impostato prima di associare una colonna alla colonna 0.The statement attribute SQL_ATTR_USE_BOOKMARKS should always be set before binding a column to column 0. Questo non è obbligatorio, ma è fortemente raccomandato.  
  
## <a name="binding-columns"></a>Associazione di colonne  
 Per associare una colonna, un'applicazione chiama **SQLBindCol** e passa il numero di colonna, il tipo, l'indirizzo e la lunghezza di un buffer di dati e l'indirizzo di un buffer di lunghezza/indicatore. Per informazioni sull'utilizzo di questi indirizzi, vedere "Indirizzi del buffer" più avanti in questa sezione. Per ulteriori informazioni sull'associazione di colonne, vedere [Utilizzo di SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 L'uso di questi buffer è posticipato; vale a dire, l'applicazione li associa in **SQLBindCol** ma il driver li accede da altre funzioni, vale a dire **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**. È responsabilità dell'applicazione assicurarsi che i puntatori specificati in **SQLBindCol** rimangano validi finché l'associazione rimane attiva. Se l'applicazione consente a questi puntatori di diventare non validi, ad esempio un buffer, e quindi chiama una funzione che prevede che siano validi, le conseguenze non sono definite. Per ulteriori informazioni, consultate [Buffer posticipati.](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
 L'associazione rimane attiva fino a quando non viene sostituita da una nuova associazione, la colonna non è associata o l'istruzione viene liberata.  
  
## <a name="unbinding-columns"></a>Annullamento dell'associazione di colonneUnbinding Columns  
 Per annullare l'associazione di una singola colonna, un'applicazione chiama **SQLBindCol** con *ColumnNumber* impostato sul numero di tale colonna e *TargetValuePtr* impostato su un puntatore null. Se *ColumnNumber* fa riferimento a una colonna non associata, **SQLBindCol** restituisce ancora SQL_SUCCESS.  
  
 Per annullare l'associazione di tutte le colonne, un'applicazione chiama **SQLFreeStmt** con *fOption* impostato su SQL_UNBIND. Questa operazione può essere eseguita anche impostando il campo SQL_DESC_COUNT dell'ARD su zero.  
  
## <a name="rebinding-columns"></a>Riassociazione delle colonneRebinding Columns  
 Un'applicazione può eseguire una delle due operazioni per modificare un'associazione:An application can perform either of two operations to change a binding:  
  
-   Chiamare **SQLBindCol** per specificare una nuova associazione per una colonna già associata. Il driver sovrascrive il binding precedente con quello nuovo.  
  
-   Specificare un offset da aggiungere all'indirizzo del buffer specificato dalla chiamata di associazione a **SQLBindCol**. Per altre informazioni, vedere la sezione successiva, "Binding Offsets".  
  
## <a name="binding-offsets"></a>Offset di rilegatura  
 Un offset di associazione è un valore che viene aggiunto agli indirizzi dei buffer di dati e lunghezza/indicatore (come specificato nel *TargetValuePtr* e *StrLen_or_IndPtr* argomento) prima che vengano dereferenziati. Quando vengono utilizzati gli offset, le associazioni sono un "modello" di come vengono disposti i buffer dell'applicazione e l'applicazione può spostare questo "modello" in diverse aree di memoria modificando l'offset. Poiché lo stesso offset viene aggiunto a ogni indirizzo in ogni associazione, gli offset relativi tra i buffer per colonne diverse devono essere gli stessi all'interno di ogni set di buffer. Ciò è sempre vero quando viene utilizzata l'associazione per riga; l'applicazione deve disporre attentamente i buffer affinché questo sia true quando viene utilizzata l'associazione per colonna.  
  
 L'utilizzo di un offset di associazione ha fondamentalmente lo stesso effetto della riassociazione di una colonna chiamando **SQLBindCol**. La differenza è che una nuova chiamata a **SQLBindCol** specifica nuovi indirizzi per il buffer di dati e il buffer di lunghezza/indicatore, mentre l'utilizzo di un offset di associazione non modifica gli indirizzi ma aggiunge semplicemente un offset. L'applicazione può specificare un nuovo offset ogni volta che lo si desidera e questo offset viene sempre aggiunto agli indirizzi associati in origine. In particolare, se l'offset è impostato su 0 o se l'attributo dell'istruzione è impostato su un puntatore null, il driver utilizza gli indirizzi associati in origine.  
  
 Per specificare un offset di associazione, l'applicazione imposta l'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR sull'indirizzo di un buffer SQLINTEGER. Prima che l'applicazione chiami una funzione che utilizza le associazioni, inserisce un offset in byte in questo buffer. Per determinare l'indirizzo del buffer da utilizzare, il driver aggiunge l'offset all'indirizzo nell'associazione. La somma dell'indirizzo e dell'offset deve essere un indirizzo valido, ma l'indirizzo a cui viene aggiunto l'offset non deve essere valido. Per ulteriori informazioni sull'utilizzo degli offset di associazione, vedere "Indirizzi del buffer" più avanti in questa sezione.  
  
## <a name="binding-arrays"></a>Matrici di associazioneBinding Arrays  
 Se la dimensione del set di righe (il valore dell'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE) è maggiore di 1, l'applicazione associa matrici di buffer anziché buffer singoli. Per ulteriori informazioni, consultate [Cursori a blocchi.](../../../odbc/reference/develop-app/block-cursors.md)  
  
 L'applicazione può associare le matrici in due modi:The application can bind arrays in two ways:  
  
-   Associare una matrice a ogni colonna. Questa operazione viene definita *associazione per colonna* perché ogni struttura di dati (matrice) contiene dati per una singola colonna.  
  
-   Definire una struttura per contenere i dati per un'intera riga e associare una matrice di queste strutture. Questa operazione viene definita *associazione per riga* perché ogni struttura di dati contiene i dati per una singola riga.  
  
 Ogni matrice di buffer deve avere almeno un numero di elementi pari alla dimensione del set di righe.  
  
> [!NOTE]  
>  Un'applicazione deve verificare che l'allineamento sia valido. Per ulteriori informazioni sulle considerazioni di allineamento, vedere [Allineamento](../../../odbc/reference/develop-app/alignment.md).  
  
## <a name="column-wise-binding"></a>Associazione per colonna  
 Nell'associazione per colonna, l'applicazione associa matrici di dati e lunghezza/indicatore separate a ogni colonna.  
  
 Per utilizzare l'associazione per colonna, l'applicazione imposta innanzitutto l'attributo dell'istruzione SQL_ATTR_ROW_BIND_TYPE su SQL_BIND_BY_COLUMN. Questa è l'impostazione predefinita. Per ogni colonna da associare, l'applicazione esegue i passaggi seguenti:For each column to be bound, the application performs the following steps:  
  
1.  Alloca una matrice del buffer di dati.  
  
2.  Alloca una matrice di buffer di lunghezza/indicatore.  
  
    > [!NOTE]  
    >  Se l'applicazione scrive direttamente nei descrittori quando viene utilizzata l'associazione per colonna, è possibile utilizzare matrici separate per i dati di lunghezza e indice.  
  
3.  Chiama **SQLBindCol** con gli argomenti seguenti:  
  
    -   *TargetType* è il tipo di un singolo elemento nella matrice del buffer di dati.  
  
    -   *TargetValuePtr* è l'indirizzo della matrice del buffer di dati.  
  
    -   *BufferLength* è la dimensione di un singolo elemento nella matrice del buffer di dati. Il *BufferLength* argomento viene ignorato quando i dati sono dati a lunghezza fissa.  
  
    -   *StrLen_or_IndPtr* è l'indirizzo della matrice lunghezza/indicatore.  
  
 Per ulteriori informazioni sull'utilizzo di queste informazioni, vedere "Indirizzi del buffer" più avanti in questa sezione. Per ulteriori informazioni sull'associazione per colonna, vedere [Associazione per colonne](../../../odbc/reference/develop-app/column-wise-binding.md).  
  
## <a name="row-wise-binding"></a>Associazione per riga  
 Nell'associazione per riga, l'applicazione definisce una struttura che contiene i buffer di dati e lunghezza/indicatore per ogni colonna da associare.  
  
 Per utilizzare l'associazione per riga, l'applicazione esegue i passaggi seguenti:To use row-wise binding, the application performs the following steps:  
  
1.  Definisce una struttura per contenere una singola riga di dati (inclusi i buffer di dati e lunghezza/indicatore) e alloca una matrice di queste strutture.  
  
    > [!NOTE]  
    >  Se l'applicazione scrive direttamente nei descrittori quando viene utilizzata l'associazione per riga, è possibile utilizzare campi separati per i dati di lunghezza e indicatore.  
  
2.  Imposta l'attributo di istruzione SQL_ATTR_ROW_BIND_TYPE sulla dimensione della struttura che contiene una singola riga di dati o sulla dimensione di un'istanza di un buffer a cui verranno associate le colonne dei risultati. La lunghezza deve includere spazio per tutte le colonne associate e qualsiasi riempimento della struttura o del buffer, per assicurarsi che quando l'indirizzo di una colonna associata viene incrementato con la lunghezza specificata, il risultato punterà all'inizio della stessa colonna nella riga successiva. Quando si utilizza l'operatore *sizeof* in ANSI C, questo comportamento è garantito.  
  
3.  Chiama **SQLBindCol** con i seguenti argomenti per ogni colonna da associare:  
  
    -   *TargetType* è il tipo del membro del buffer di dati da associare alla colonna.  
  
    -   *TargetValuePtr* è l'indirizzo del membro del buffer di dati nel primo elemento della matrice.  
  
    -   *BufferLength* è la dimensione del membro del buffer di dati.  
  
    -   *StrLen_or_IndPtr* è l'indirizzo del membro length/indicator da associare.  
  
 Per ulteriori informazioni sull'utilizzo di queste informazioni, vedere "Indirizzi del buffer" più avanti in questa sezione. Per ulteriori informazioni sull'associazione per colonna, vedere [Associazione basata](../../../odbc/reference/develop-app/row-wise-binding.md)su righe .  
  
## <a name="buffer-addresses"></a>Indirizzi buffer  
 *L'indirizzo* del buffer è l'indirizzo effettivo del buffer di lunghezza/indicatore. Il driver calcola l'indirizzo del buffer appena prima di scrivere nei buffer (ad esempio durante il tempo di recupero). Viene calcolato dalla formula seguente, che utilizza gli indirizzi specificati negli argomenti *TargetValuePtr* e *StrLen_or_IndPtr,* l'offset di associazione e il numero di riga:  
  
 *Bound Address* + *Offset associazione* indirizzo associato ( ((*Numero riga* - 1) x *Dimensione elemento*)  
  
 in cui le variabili della formula sono definite come descritto nella tabella seguente.  
  
|Variabile|Descrizione|  
|--------------|-----------------|  
|*Indirizzo associato*|Per i buffer di dati, indirizzo specificato con l'argomento *TargetValuePtr* in **SQLBindCol**.<br /><br /> Per i buffer di lunghezza/indicatore, l'indirizzo specificato con l'argomento *StrLen_or_IndPtr* in **SQLBindCol**. Per ulteriori informazioni, vedere "Commenti aggiuntivi" nella sezione "Descrittori e SQLBindCol".<br /><br /> Se l'indirizzo associato è 0, non viene restituito alcun valore di dati, anche se l'indirizzo calcolato dalla formula precedente è diverso da zero.|  
|*Offset rilegatura*|Se viene utilizzata l'associazione per riga, il valore archiviato nell'indirizzo specificato con l'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR.<br /><br /> Se viene utilizzata l'associazione per colonna o se il valore dell'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR è un puntatore null, *Offset associazione* è 0.If column-wise binding is used or if the value of the SQL_ATTR_ROW_BIND_OFFSET_PTR statement attribute is a null pointer, Binding Offset is 0.|  
|*Row Number*|Numero in base 1 della riga nel set di righe. Per i recuperi a riga singola, che sono l'impostazione predefinita, questo è 1.For single-row fetches, which are the default, this is 1.|  
|*Dimensione elemento*|Dimensione di un elemento nella matrice associata.<br /><br /> Se viene utilizzata l'associazione per colonna, si tratta **di sizeof(SQLINTEGER)** per i buffer di lunghezza/indicatore. Per i buffer di dati, è il valore del *BufferLength* argomento in **SQLBindCol** se il tipo di dati è a lunghezza variabile e la dimensione del tipo di dati se il tipo di dati è a lunghezza fissa.<br /><br /> Se viene utilizzata l'associazione per riga, questo è il valore dell'attributo di istruzione SQL_ATTR_ROW_BIND_TYPE per i buffer di dati e lunghezza/indicatore.|  
  
## <a name="descriptors-and-sqlbindcol"></a>Descrittori e SQLBindCol  
 Nelle sezioni seguenti viene descritto come **SQLBindCol** interagisce con i descrittori.  
  
> [!CAUTION]  
>  La chiamata a **SQLBindCol** per un'istruzione può influire su altre istruzioni. Ciò si verifica quando l'ARD associato all'istruzione viene allocato in modo esplicito ed è anche associato ad altre istruzioni. Poiché **SQLBindCol** modifica il descrittore, le modifiche si applicano a tutte le istruzioni a cui è associato questo descrittore. Se questo non è il comportamento richiesto, l'applicazione deve dissociare questo descrittore dalle altre istruzioni prima di chiamare **SQLBindCol**.  
  
## <a name="argument-mappings"></a>Mapping di argomenti  
 Concettualmente, SQLBindCol esegue i passaggi seguenti in sequenza:Conceptually, **SQLBindCol** performs the following steps in sequence:  
  
1.  Chiama **SQLGetStmtAttr** per ottenere l'handle ARD.  
  
2.  Chiama **SQLGetDescField** per ottenere il campo SQL_DESC_COUNT di questo descrittore e se il valore *nell'argomento ColumnNumber* supera il valore di SQL_DESC_COUNT, chiama **SQLSetDescField** per aumentare il valore di SQL_DESC_COUNT a *ColumnNumber*.  
  
3.  Chiama **SQLSetDescField** più volte per assegnare valori ai seguenti campi dell'ARD:  
  
    -   Imposta SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE sul valore di *TargetType*, con la differenza che se *TargetType* è uno degli identificatori concisi di un sottotipo datetime o interval, imposta SQL_DESC_TYPE rispettivamente su SQL_DATETIME o SQL_INTERVAL; imposta SQL_DESC_CONCISE_TYPE sull'identificatore conciso; e imposta SQL_DESC_DATETIME_INTERVAL_CODE al sottocodice datetime o interval corrispondente.  
  
    -   Imposta uno o più SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_DATETIME_INTERVAL_PRECISION, a seconda *di TargetType*.  
  
    -   Imposta il campo SQL_DESC_OCTET_LENGTH sul valore di *BufferLength*.  
  
    -   Imposta il campo SQL_DESC_DATA_PTR sul valore di *TargetValue*.  
  
    -   Imposta il campo SQL_DESC_INDICATOR_PTR sul valore di *StrLen_or_Ind*. (Vedere il paragrafo seguente).)  
  
    -   Imposta il campo SQL_DESC_OCTET_LENGTH_PTR sul valore di *StrLen_or_Ind*. (Vedere il paragrafo seguente).)  
  
 La variabile a cui fa riferimento l'argomento *StrLen_or_Ind* viene utilizzata sia per le informazioni sull'indicatore che per le informazioni sulla lunghezza. Se un recupero rileva un valore null per la colonna, archivia SQL_NULL_DATA in questa variabile; in caso contrario, archivia la lunghezza dei dati in questa variabile. Il passaggio di un puntatore null come *StrLen_or_Ind* impedisce all'operazione di recupero di restituire la lunghezza dei dati, ma rende il recupero non riuscito se rileva un valore null e non ha modo di restituire SQL_NULL_DATA.  
  
 Se la chiamata a **SQLBindCol** ha esito negativo, il contenuto dei campi del descrittore che avrebbe impostato nell'ARD non sono definiti e il valore del campo SQL_DESC_COUNT dell'ARD viene invariato.  
  
## <a name="implicit-resetting-of-count-field"></a>Reimpostazione implicita del campo COUNT  
 **SQLBindCol** imposta SQL_DESC_COUNT sul valore dell'argomento *ColumnNumber* solo quando questo aumenterebbe il valore di SQL_DESC_COUNT. Se il valore nell'argomento *TargetValuePtr* è un puntatore null e il valore nell'argomento *ColumnNumber* è uguale a SQL_DESC_COUNT, ovvero quando si annulla l'associazione della colonna con limite più alto, SQL_DESC_COUNT è impostato sul numero della colonna associata più alta rimanente.  
  
## <a name="cautions-regarding-sql_default"></a>Precauzioni relative a SQL_DEFAULT  
 Per recuperare correttamente i dati della colonna, l'applicazione deve determinare correttamente la lunghezza e il punto iniziale dei dati nel buffer dell'applicazione. Quando l'applicazione specifica un *TargetType*esplicito , le idee errate dell'applicazione vengono facilmente rilevate. Tuttavia, quando l'applicazione specifica un *TargetType* di SQL_DEFAULT, **SQLBindCol** può essere applicato a una colonna di un tipo di dati diverso da quello previsto dall'applicazione, dalle modifiche ai metadati o applicando il codice a una colonna diversa. In questo caso, l'applicazione potrebbe non determinare sempre l'inizio o la lunghezza dei dati della colonna recuperata. Ciò può causare errori di dati non segnalati o violazioni della memoria.  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, un'applicazione esegue un'istruzione **SELECT** nella tabella Customers per restituire un set di risultati degli ID cliente, dei nomi e dei numeri di telefono, ordinati in base al nome. Chiama quindi **SQLBindCol** per associare le colonne di dati ai buffer locali. Infine, l'applicazione recupera ogni riga di dati con **SQLFetch** e stampa il nome, l'ID e il numero di telefono di ogni cliente.  
  
 Per altri esempi di codice, vedere [Funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [Funzione SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)e [Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 60
  
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
                  retcode = SQLBindCol(hstmt, 1, SQL_C_WCHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_WCHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_WCHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (int i=0 ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                     {
                        //replace wprintf with printf
                        //%S with %ls
                        //warning C4477: 'wprintf' : format string '%S' requires an argument of type 'char *'
                        //but variadic argument 2 has type 'SQLWCHAR *'
                        //wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                        printf("%d: %ls %ls %ls\n", i + 1, sCustID, szName, szPhone);  
                    }    
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
  
 Vedere anche [Programma ODBC di esempio](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituzione di informazioni su una colonna in un set di risultatiReturning information about a column in a result set|[Funzione SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Recupero di un blocco di dati o scorrimento di un set di risultati|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Recupero di più righe di dati|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Rilascio di buffer di colonna sull'istruzione|[Funzione SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Recupero di parte o di tutta una colonna di dati|[Funzione SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Restituzione del numero di colonne del set di risultatiReturning the number of result set columns|[Funzione SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
