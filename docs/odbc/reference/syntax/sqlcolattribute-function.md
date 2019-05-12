---
title: Funzione SQLColAttribute | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColAttribute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColAttribute
helpviewer_keywords:
- SQLColAttribute function [ODBC]
ms.assetid: 8c45c598-cb01-4789-a571-e93619a18ed9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e23b7dd9ce81f02a822bece3546bf1c604030df1
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537565"
---
# <a name="sqlcolattribute-function"></a>Funzione SQLColAttribute
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLColAttribute** restituisce informazioni sul descrittore per una colonna in un set di risultati. Informazioni sul descrittore viene restituiti come una stringa di caratteri, un valore descrittore dipendente o un valore intero.  
  
> [!NOTE]  
>  Per altre informazioni su quali il Driver Manager esegue il mapping a questa funzione quando un'applicazione ODBC 3. *x* applicazione funziona con un'API ODBC 2. *x* driver, vedere [Mapping di funzioni di sostituzione per la compatibilità con le versioni precedenti di applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLColAttribute (  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ColumnNumber,  
      SQLUSMALLINT    FieldIdentifier,  
      SQLPOINTER      CharacterAttributePtr,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLLEN *        NumericAttributePtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *ColumnNumber*  
 [Input] Il numero del record nell'implementazione da cui è necessario recuperare il valore del campo. Questo argomento corrisponde al numero di colonna di dati del risultato, ordinati in sequenza in ordine crescente di colonna, a partire da 1. Le colonne possono essere descritti in qualsiasi ordine.  
  
 Colonna 0 può essere specificato in questo argomento, ma tutti i valori tranne SQL_DESC_TYPE e SQL_DESC_OCTET_LENGTH restituiranno valori non definiti.  
  
 *FieldIdentifier*  
 [Input] L'handle descrittore. Questo handle definisce il campo di implementazione deve essere eseguita una query (ad esempio, SQL_COLUMN_TABLE_NAME).  
  
 *CharacterAttributePtr*  
 [Output] Puntatore a un buffer in cui restituire il valore nel *FieldIdentifier* campo le *ColumnNumber* riga di implementazione, se il campo è una stringa di caratteri. In caso contrario, il campo è inutilizzato.  
  
 Se *CharacterAttributePtr* sia impostato su NULL *StringLengthPtr* continuerà a restituire il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui punta *CharacterAttributePtr*.  
  
 *BufferLength*  
 [Input] Se *FieldIdentifier* è un campo definite da ODBC e *CharacterAttributePtr* punta a una stringa di caratteri o binario buffer, la lunghezza di questo argomento deve essere \*  *CharacterAttributePtr*. Se *FieldIdentifier* è un campo definite da ODBC e \* *CharacterAttribute*Ptr è un numero intero, questo campo verrà ignorato. Se il  *\*CharacterAttributePtr* è una stringa Unicode (quando si chiama **SQLColAttributeW**), il *BufferLength* argomento deve essere un numero pari. Se *FieldIdentifier* è un campo definito dal driver, l'applicazione indica la natura del campo da Gestione Driver impostando il *BufferLength* argomento. *BufferLength* può avere i valori seguenti:  
  
-   Se *CharacterAttributePtr* è un puntatore a un puntatore *BufferLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se *CharacterAttributePtr* è un puntatore a una stringa di caratteri, il *BufferLength* è la lunghezza del buffer.  
  
-   Se *CharacterAttributePtr* è un puntatore a un buffer binario, le posizioni dell'applicazione il risultato del SQL_LEN_BINARY_ATTR (*lunghezza*) (macro) in *BufferLength*. Un valore negativo in questo modo vengono inserite *BufferLength*.  
  
-   Se *CharacterAttributePtr* è un puntatore a un tipo di dati a lunghezza fissa *BufferLength* deve essere uno dei seguenti: SQL_IS_INTEGER, SQL_IS_UNINTEGER, SQL_SMALLINT, or SQLUSMALLINT.  
  
 *StringLengthPtr*  
 [Output] Puntatore a un buffer in cui restituire il numero totale di byte (escluso il byte di terminazione null per i dati di tipo carattere) disponibile da restituire in **CharacterAttributePtr*.  
  
 Per i dati di tipo carattere, se il numero di byte disponibili da restituire è maggiore o uguale a *BufferLength*, le informazioni del descrittore nel \* *CharacterAttributePtr* verranno troncati alla  *BufferLength* meno la lunghezza di un carattere di terminazione null ed è con terminazione null dal driver.  
  
 Per tutti gli altri tipi di dati, il valore di *BufferLength* viene ignorato e il driver presuppone che le dimensioni di **CharacterAttributePtr* è a 32 bit.  
  
 *NumericAttributePtr*  
 [Output] Puntatore a un buffer di integer in cui restituire il valore nel *FieldIdentifier* campo le *ColumnNumber* righe di implementazione, se il campo è un tipo di descrittore numerici, ad esempio SQL_DESC_COLUMN_LENGTH. In caso contrario, il campo è inutilizzato. Si noti che alcuni driver può scrivere solo inferiore a 32 o a 16 bit di un buffer e lasciare invariato il bit di ordine superiore. Di conseguenza, le applicazioni devono inizializzare il valore su 0 prima di chiamare questa funzione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLColAttribute** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato può essere ottenuto chiamando **SQLGetDiagRec** con un *HandleType*SQL_HANDLE_STMT e una *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLColAttribute** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Il buffer \* *CharacterAttributePtr* non era sufficientemente grande per restituire il valore di stringa intera, in modo che il valore della stringa è stato troncato. Viene restituita la lunghezza del valore della stringa non troncato **StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07005|Istruzione preparata non un *specifica di cursore.*|L'istruzione associata la *StatementHandle* non ha restituito un set di risultati e *FieldIdentifier* SQL_DESC_COUNT non è stato. Si sono verificati Nessuna colonna per descrivere.|  
|07009|Indice del descrittore non valido|(DM) il valore specificato per *ColumnNumber* era uguale a 0 e l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS SQL_UB_OFF.<br /><br /> Il valore specificato per l'argomento *ColumnNumber* era maggiore del numero di colonne nel set di risultati.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagField** dai dati di diagnostica struttura descrive l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle*. Quindi la funzione è stata chiamata nuovamente sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione aynchronous era ancora in esecuzione quando è stato chiamato SQLColAttribute.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata prima di chiamare la funzione **SQLPrepare**, **SQLExecDirect**, o una funzione di catalogo per il *StatementHandle*.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM)  *\*CharacterAttributePtr* è una stringa di caratteri, e *BufferLength* era minore di 0, ma non è uguale a SQL_NTS.|  
|HY091|Identificatore del campo del descrittore non valido|Il valore specificato per l'argomento *FieldIdentifier* non corrisponde a uno dei valori definiti e non è un valore definito dall'implementazione.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Non è in grado di driver|Il valore specificato per l'argomento *FieldIdentifier* non era supportata dal driver.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
 Se viene chiamato dopo **SQLPrepare** e prima **SQLExecute**, **SQLColAttribute** può restituire qualsiasi valore SQLSTATE che può essere restituiti da **SQLPrepare**oppure **SQLExecute**, a seconda di quando l'origine dati viene valutata l'istruzione SQL associata la *StatementHandle*.  
  
 Per motivi di prestazioni, un'applicazione non deve chiamare **SQLColAttribute** prima di eseguire un'istruzione.  
  
## <a name="comments"></a>Commenti  
 Per informazioni su come applicazioni di usano le informazioni restituite da **SQLColAttribute**, vedere [metadati dei Set di risultati](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLColAttribute** restituisce informazioni sia nella \* *NumericAttributePtr* o nella \* *CharacterAttributePtr*. Vengono restituite informazioni di integer in \* *NumericAttributePtr* come valore SQLLEN; vengono restituiti tutti gli altri formati di informazioni in \* *CharacterAttributePtr*. Quando vengono restituite informazioni \* *NumericAttributePtr*, il driver ignora *CharacterAttributePtr*, *BufferLength*, e  *StringLengthPtr*. Quando vengono restituite informazioni \* *CharacterAttributePtr*, il driver ignora *NumericAttributePtr*.  
  
 **SQLColAttribute** restituisce i valori dei campi del descrittore di implementazione. La funzione viene chiamata con un handle di istruzione anziché un handle di descrittore. I valori restituiti da **SQLColAttribute** per il *FieldIdentifier* elencate più avanti in questa sezione possono anche essere recuperati chiamando **SQLGetDescField** con di handle IRD appropriato.  
  
 Il descrittore attualmente definito campi, la versione di ODBC in cui sono state introdotte e gli argomenti in cui vengono restituite informazioni per tali sono illustrati più avanti in questa sezione; più tipi di descrittore possono essere definiti dai driver per sfruttare i vantaggi di origini dati diverse.  
  
 Un database ODBC 3. *x* driver deve restituire un valore per ognuno dei campi di descrizione. Se un campo di descrizione non viene applicata a un'origine dati o driver e se non diversamente specificato, il driver restituisce 0 in \* *StringLengthPtr* o una stringa vuota in **CharacterAttributePtr*.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ODBC 3. *x* funzione **SQLColAttribute** sostituisce il deprecate di ODBC 2. *x* funzione **SQLColAttributes**. Quando il mapping **SQLColAttributes** al **SQLColAttribute** (quando un ODBC 2. *x* applicazione funziona con un'applicazione ODBC 3. *x* driver), o mapping **SQLColAttribute** al **SQLColAttributes** (quando un'applicazione ODBC 3. *x* applicazione funziona con un'API ODBC 2. *x* driver), gestione Driver passa sia il valore di *FieldIdentifier* tramite, viene eseguito il mapping a un nuovo valore o restituisce un errore, come indicato di seguito:  
  
> [!NOTE]  
>  Il prefisso utilizzato nelle *FieldIdentifier* i valori in ODBC 3. *x* è stata modificata da tale utilizzato in ODBC 2. *x*. Il nuovo prefisso è "SQL_DESC"; il prefisso precedente era "SQL_COLUMN".  
  
-   Se il **#define** pari a ODBC 2. *x* *FieldIdentifier* equivale al **#define** pari a ODBC 3. *x* *FieldIdentifier*, il valore nella chiamata di funzione viene passato semplicemente attraverso.  
  
-   Il **#define** i valori di ODBC 2. *x* *FieldIdentifiers* SQL_COLUMN_LENGTH SQL_COLUMN_PRECISION e SQL_COLUMN_SCALE sono diversi dai **#define** valori di ODBC 3. *x* *FieldIdentifiers* SQL_DESC_SCALE, SQL_DESC_PRECISION e SQL_DESC_LENGTH. Un database ODBC 2. *x* driver necessario solo il supporto di ODBC 2. *x* valori. Un database ODBC 3. *x* driver deve supportare sia "SQL_COLUMN" e "SQL_DESC" i valori per questi tre *FieldIdentifiers*. Questi valori sono diversi perché la precisione, scala e lunghezza vengono definite in modo diverso in ODBC 3. *x* rispetto a ODBC 2. *x*. Per altre informazioni, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
-   Se il **#define** pari a ODBC 2. *x* *FieldIdentifier* è diverso dal **#define** pari a ODBC 3. *x* *FieldIdentifier*, come avviene con il numero, nome, e viene eseguito il mapping ai valori null, il valore nella chiamata di funzione per il valore corrispondente. Ad esempio, viene eseguito il mapping SQL_COLUMN_COUNT a SQL_DESC_COUNT, SQL_DESC_COUNT viene mappato a SQL_COLUMN_COUNT, a seconda della direzione del mapping.  
  
-   Se *FieldIdentifier* è un nuovo valore in ODBC 3. *x*, per cui si è verificato alcun valore corrispondente in ODBC 2. *x*, non verrà mappata quando un'applicazione ODBC 3. *x* dell'applicazione da usare in una chiamata a **SQLColAttribute** in un'API ODBC 2. *x* driver e la chiamata restituirà SQLSTATE HY091 (identificatore del campo del descrittore non valido).  
  
 Nella tabella seguente sono elencati i tipi di descrittore restituiti da **SQLColAttribute**. Il tipo per *NumericAttributePtr* valori viene **SQLLEN \*** .  
  
|*FieldIdentifier*|Informazioni<br /><br /> restituito in|Descrizione|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE se la colonna è di tipo incrementata automaticamente.<br /><br /> SQL_FALSE se la colonna non è di tipo incrementata automaticamente o non è numerica.<br /><br /> Questo campo è valido per solo colonne di tipo di dati numerici. Un'applicazione può inserire i valori in una riga che contiene una colonna a incremento automatico, ma in genere non è possibile aggiornare i valori della colonna.<br /><br /> Quando un'operazione di inserimento viene effettuata in Pro sloupec autoincrement, viene inserito un valore univoco nella colonna al momento dell'inserimento. L'incremento non è definito, ma è specifiche dell'origine dati. Un'applicazione non deve presupporre che Pro sloupec autoincrement inizia in corrispondenza di qualsiasi particolare punto o incrementi da un particolare valore.|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|Il nome di colonna di base per il risultato del set di colonne. Se non esiste un nome di colonna di base (come nel caso delle colonne che sono espressioni), questa variabile contiene una stringa vuota.<br /><br /> Queste informazioni vengono restituite dal campo del record SQL_DESC_BASE_COLUMN_NAME di implementazione, che è un campo di sola lettura.|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|Il nome della tabella di base che contiene la colonna. Se il nome della tabella di base non può essere definito o non è applicabile, questa variabile contiene una stringa vuota.<br /><br /> Queste informazioni vengono restituite dal campo del record SQL_DESC_BASE_TABLE_NAME di implementazione, che è un campo di sola lettura.|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE se la colonna viene considerata come distinzione maiuscole/minuscole per le regole di confronto e i confronti.<br /><br /> SQL_FALSE se la colonna non viene trattata come distinzione maiuscole/minuscole per le regole di confronto e i confronti o è non carattere.|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|Il catalogo della tabella che contiene la colonna. Il valore restituito è definito dall'implementazione se la colonna è un'espressione o se la colonna fa parte di una vista. Se l'origine dati non supporta cataloghi o non è possibile determinare il nome del catalogo, viene restituita una stringa vuota. Questo campo di record VARCHAR non è limitato a 128 caratteri.|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|Il tipo di dati concisa.<br /><br /> Per i tipi di dati datetime e interval, questo campo restituisce il tipo di dati concisa; ad esempio, SQL_TYPE_TIME o SQL_INTERVAL_YEAR. (Per altre informazioni, vedere [identificatori di tipo di dati e i descrittori](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) nell'appendice d: Tipi di dati.)<br /><br /> Queste informazioni vengono restituite dal campo del record SQL_DESC_CONCISE_TYPE di implementazione.|  
|SQL_DESC_COUNT  (ODBC 1.0)|*NumericAttributePtr*|Il numero di colonne disponibili nel set di risultati. Restituisce 0 se non sono disponibili colonne nel set di risultati. Il valore di *ColumnNumber* argomento verrà ignorato.<br /><br /> Queste informazioni vengono restituite dal campo di intestazione SQL_DESC_COUNT di implementazione.|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|Numero massimo di caratteri necessari per visualizzare i dati dalla colonna. Per altre informazioni sulle dimensioni di visualizzazione, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e visualizzare le dimensioni](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice d: Tipi di dati.|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE se la colonna ha una scala e precisione fisse diverso da zero che sono specifiche dell'origine dati.<br /><br /> SQL_FALSE se la colonna non ha una scala e precisione fisse diverso da zero che sono specifiche dell'origine dati.|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|L'etichetta di colonna o il titolo. Ad esempio, una colonna denominata EmpName potrebbe essere contrassegnata come nome di dipendente o potrebbe essere etichettata con un alias.<br /><br /> Se una colonna non dispone di un'etichetta, viene restituito il nome della colonna. Se la colonna è senza etichetta e senza nome, viene restituita una stringa vuota.|  
|SQL_DESC_LENGTH  (ODBC 3.0)|*NumericAttributePtr*|Un valore numerico che può essere digitare la lunghezza massima o effettivo di un carattere string o binary di dati. È la lunghezza caratteri massima per un tipo di dati a lunghezza fissa oppure la lunghezza in caratteri effettivi per un tipo di dati a lunghezza variabile. Il valore esclude sempre il byte di terminazione null che termina la stringa di caratteri.<br /><br /> Queste informazioni vengono restituite dal campo del record SQL_DESC_LENGTH di implementazione.<br /><br /> Per altre informazioni sulla lunghezza, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice d: Tipi di dati.|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|Questo campo di record VARCHAR(128) contiene uno o più caratteri che il driver riconosce come un prefisso per un valore letterale di questo tipo di dati. Questo campo contiene una stringa vuota per un tipo di dati per cui non è applicabile un prefisso letterale. Per altre informazioni, vedere [letterale prefissi e suffissi](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|Questo campo di record VARCHAR(128) contiene uno o più caratteri che il driver riconosce come un suffisso per un valore letterale di questo tipo di dati. Questo campo contiene una stringa vuota per un tipo di dati per il quale un suffisso letterale non è applicabile. Per altre informazioni, vedere [letterale prefissi e suffissi](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|Questo campo di record VARCHAR(128) contiene qualsiasi nome localizzato (native language) per il tipo di dati che potrebbe essere diverso dal nome del tipo di dati regolare. Se è presente alcun nome localizzato, viene restituita una stringa vuota. Questo campo è solo a fini di visualizzazione. Il set di caratteri della stringa dipende dalla lingua e in genere è il set di caratteri predefinito del server.|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|L'alias di colonna, se applicabile. Se non si applica l'alias di colonna, viene restituito il nome della colonna. In entrambi i casi, è impostare SQL_DESC_UNNAMED su SQL_NAMED. Se è presente alcun nome di colonna o un alias di colonna, viene restituita una stringa vuota e SQL_DESC_UNNAMED è impostato su SQL_UNNAMED.<br /><br /> Queste informazioni vengono restituite dal campo del record SQL_DESC_NAME di implementazione.|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|SQL _ ammette valori null se la colonna può contenere valori NULL. SQL_NO_NULLS se la colonna non dispone di valori NULL. o SQL_NULLABLE_UNKNOWN se non è noto se la colonna accetta valori NULL.<br /><br /> Queste informazioni vengono restituite dal campo del record SQL_DESC_NULLABLE di implementazione.|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|Se il tipo di dati nel campo SQL_DESC_TYPE è un tipo di dati numerici approssimati, questo campo SQLINTEGER contiene un valore pari a 2 perché il campo SQL_DESC_PRECISION contiene il numero di bit. Se il tipo di dati nel campo SQL_DESC_TYPE è un tipo di dati numerici esatti, questo campo contiene un valore pari a 10 perché il campo SQL_DESC_PRECISION contiene il numero di cifre decimali. Questo campo è impostato su 0 per tutti i tipi di dati non numerici.|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|La lunghezza, espressa in byte, di un tipo di dati string o binary di carattere. Carattere a lunghezza fissa o tipi binari, questa è la lunghezza effettiva in byte. Per i tipi binari o carattere a lunghezza variabile questa è la lunghezza massima in byte. Questo valore non include il carattere di terminazione null.<br /><br /> Queste informazioni vengono restituite dal campo del record SQL_DESC_OCTET_LENGTH di implementazione.<br /><br /> Per altre informazioni sulla lunghezza, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice d: Tipi di dati.|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|Un valore numerico che per un tipo di dati numerici denota la precisione applicabile. Per i dati di tipi SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, e tutti i tipi di dati di intervallo che rappresentano un intervallo di tempo, il relativo valore è la precisione applicabile del componente in frazioni.<br /><br /> Queste informazioni vengono restituite dal campo del record SQL_DESC_PRECISION di implementazione.|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|Valore numerico che rappresenta la scala applicabile per un tipo di dati numerici. Per i tipi di dati DECIMAL e NUMERIC, si tratta alla scala definita. Non è stato definito per tutti gli altri tipi di dati.<br /><br /> Queste informazioni vengono restituite dal campo del record di scalabilità di implementazione.|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|Lo schema della tabella che contiene la colonna. Il valore restituito è definito dall'implementazione se la colonna è un'espressione o se la colonna fa parte di una vista. Se l'origine dati non supporta schemi o non è possibile determinare il nome dello schema, viene restituita una stringa vuota. Questo campo di record VARCHAR non è limitato a 128 caratteri.|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|SQL_PRED_NONE se la colonna non può essere utilizzata in una clausola WHERE. (Questo è lo stesso come il valore SQL_UNSEARCHABLE in ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR se la colonna può essere utilizzata in una clausola WHERE, ma solo con il predicato LIKE. (Questo è lo stesso come il valore SQL_LIKE_ONLY in ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC se la colonna può essere utilizzata in una clausola WHERE con tutti gli operatori di confronto, ad eccezione di tipo. (Questo è lo stesso come il valore SQL_EXCEPT_LIKE in ODBC 2. *x*.)<br /><br /> SQL_PRED_SEARCHABLE se la colonna può essere utilizzata in una clausola WHERE con qualsiasi operatore di confronto.<br /><br /> Colonne di tipo SQL_PRED_CHAR in genere restituito SQL_LONGVARBINARY e SQL_LONGVARCHAR.|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|Nome della tabella che contiene la colonna. Il valore restituito è definito dall'implementazione se la colonna è un'espressione o se la colonna fa parte di una vista.<br /><br /> Se non è possibile determinare il nome della tabella, viene restituita una stringa vuota.|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|Valore numerico che specifica il tipo di dati SQL.<br /><br /> Quando *ColumnNumber* è uguale a 0, viene restituito SQL_BINARY per a lunghezza variabile segnalibri e SQL_INTEGER viene restituito per i segnalibri di lunghezza fissa.<br /><br /> Per i tipi di dati datetime e interval, questo campo restituisce il tipo di dati dettagliati: SQL_DATETIME o SQL_INTERVAL. (Per altre informazioni, vedere [identificatori di tipo di dati e i descrittori](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) nell'appendice d: Tipi di dati.<br /><br /> Queste informazioni vengono restituite dal campo del record SQL_DESC_TYPE di implementazione. **Nota:**  Per funzionare con l'API ODBC 2. *x* driver, usare invece SQL_DESC_CONCISE_TYPE.|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|Nome del tipo di dati dipende dall'origine dati; ad esempio, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" o "() CHAR FOR BIT DATA".<br /><br /> Se il tipo è sconosciuto, viene restituita una stringa vuota.|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED o SQL_UNNAMED. Se il campo SQL_DESC_NAME di implementazione contiene un alias di colonna o un nome di colonna, viene restituito SQL_NAMED. Se è presente alcun nome di colonna o alias di colonna, viene restituito SQL_UNNAMED.<br /><br /> Queste informazioni vengono restituite dal campo del record SQL_DESC_UNNAMED di implementazione.|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE se la colonna è senza segno (o non numerico).<br /><br /> SQL_FALSE se la colonna è firmata.|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|Colonna verrà indicata i valori per le costanti definite:<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE descrive quanto concerne l'aggiornabilità della colonna nel set di risultati, non la colonna nella tabella di base. L'aggiornabilità della colonna di base su cui si basa la colonna del set di risultati può essere diverso da quello in questo campo. Se una colonna è aggiornabile può basarsi sul tipo di dati, i privilegi utente e la definizione di se stesso set di risultati. Se non è chiaro se una colonna è aggiornabile, SQL_ATTR_READWRITE_UNKNOWN devono essere restituiti.|  
  
 **SQLColAttribute** è un'alternativa a estendibile **SQLDescribeCol**. **SQLDescribeCol** restituisce un set fisso di informazioni del descrittore di base 89 ANSI SQL. **SQLColAttribute** consente l'accesso per il set più completo di informazioni del descrittore disponibili nelle estensioni del fornitore di ANSI SQL-92 e DBMS.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultati|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di informazioni relative a una colonna in un set di risultati|[Funzione SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Imposta il recupero di un blocco di dati o lo scorrimento di un risultato|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Il recupero di più righe di dati|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>Esempio  
 Esempio di codice seguente non libera gli handle e le connessioni. Visualizzare [funzione SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md), [programma di esempio ODBC](../../../odbc/reference/sample-odbc-program.md), e [SQLFreeStmt-funzione](../../../odbc/reference/syntax/sqlfreestmt-function.md) per esempi di codice liberare l'handle e le istruzioni.  
  
```cpp  
// SQLColAttibute.cpp  
// compile with: user32.lib odbc32.lib  
  
#define UNICODE  
  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printStatementResult(SQLHSTMT hstmt) {  
   int bufferSize = 1024, i;  
   SQLRETURN retCode;  
   SQLSMALLINT numColumn = 0, bufferLenUsed;
   
   retCode = SQLNumResultCols(hstmt, &numColumn);  
   
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   printf( "Columns from that table:\n" );  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnLabels[i] = (SQLPOINTER)malloc( bufferSize*sizeof(char) );  
  
      retCode = SQLColAttribute(hstmt, (SQLUSMALLINT)i + 1, SQL_DESC_LABEL, columnLabels[i], (SQLSMALLINT)bufferSize, &bufferLenUsed, NULL);  
      wprintf( L"Column %d: %s\n", i, (wchar_t*)columnLabels[i] );  
   }  
  
   // allocate memory for the binding  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnData[i].TargetType = SQL_C_CHAR;  
      columnData[i].BufferLength = (bufferSize+1);  
      columnData[i].TargetValuePtr = malloc( sizeof(unsigned char)*columnData[i].BufferLength );  
   }  
  
   // setup the binding   
   for ( i = 0 ; i < numColumn ; i++ ) {  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, columnData[i].TargetType,   
         columnData[i].TargetValuePtr, columnData[i].BufferLength, &(columnData[i].StrLen_or_Ind));  
   }  
  
   printf( "Data from that table:\n" );  
   // fetch the data and print out the data  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt) ) {  
      int j;  
      for ( j = 0 ; j < numColumn ; j++ )  
         wprintf( L"%s: %hs\n", columnLabels[j], columnData[j].TargetValuePtr );  
      printf( "\n" );  
   }  
   printf( "\n" );   
}  
  
int main() {  
   int bufferSize = 1024, i, count = 1, numCols = 5;  
   wchar_t firstTableName[1024], * dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize ), * userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen, bufferLen;  
   SQLRETURN retCode;  
  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   SQLWCHAR* selectAllQuery = (SQLWCHAR *)malloc( sizeof(SQLWCHAR) * bufferSize );  
  
   // connect to database  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLCHAR *)(void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, L"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // display the database information  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferLen);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, &bufferLen);  
  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // Set up the binding. This can be used even if the statement is closed by closeStatementHandle  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   retCode = SQLTables( hstmt, (SQLWCHAR*)SQL_ALL_CATALOGS, SQL_NTS, L"", SQL_NTS, L"", SQL_NTS, L"", SQL_NTS );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   retCode = SQLTables( hstmt, dbName, SQL_NTS, userName, SQL_NTS, L"%", SQL_NTS, L"TABLE", SQL_NTS );  
  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt), ++count )  
      if ( count == 1 )  
         StringCchPrintfW( firstTableName, 1024, L"%hs", catalogResult[2].TargetValuePtr );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   wprintf( L"Select all data from the first table (%s)\n", firstTableName );  
   StringCchPrintfW( selectAllQuery, bufferSize, L"SELECT * FROM %s", firstTableName );  
  
   retCode = SQLExecDirect(hstmt, selectAllQuery, SQL_NTS);  
   printStatementResult(hstmt);  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programma di esempio ODBC](../../../odbc/reference/sample-odbc-program.md)
