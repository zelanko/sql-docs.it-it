---
title: Funzione SQLSetDescField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescField
helpviewer_keywords:
- SQLSetDescField function [ODBC]
ms.assetid: 8c544388-fe9d-4f94-a0ac-fa0b9c9c88a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4cca223510ebb6838048e3babbf8fdcada42f87a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039745"
---
# <a name="sqlsetdescfield-function"></a>Funzione SQLSetDescField

**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLSetDescField** imposta il valore di un singolo campo di un record del descrittore.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
SQLRETURN SQLSetDescField(  
     SQLHDESC      DescriptorHandle,  
     SQLSMALLINT   RecNumber,  
     SQLSMALLINT   FieldIdentifier,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    BufferLength);  
```  
  
## <a name="arguments"></a>Argomenti  
 *DescriptorHandle*  
 [Input] Handle descrittore.  
  
 *RecNumber*  
 [Input] Indica che contiene il campo che l'applicazione tenta di impostare il record del descrittore. Record del descrittore sono numerati da 0, con il numero di record 0 come il record di segnalibro. Il *RecNumber* argomento viene ignorato per i campi di intestazione.  
  
 *FieldIdentifier*  
 [Input] Indica il campo del descrittore il cui valore deve essere impostata. Per altre informazioni, vedere "*FieldIdentifier* argomento" nella sezione "Commenti".  
  
 *ValuePtr*  
 [Input] Puntatore a un buffer contenente le informazioni del descrittore o un valore intero. Il tipo di dati dipende dal valore della *FieldIdentifier*. Se *ValuePtr* è un valore intero, può essere considerato come 8 byte (SQLLEN), 4 byte (SQLINTEGER) o 2 byte (SQLSMALLINT), in base al valore di *FieldIdentifier* argomento.  
  
 *BufferLength*  
 [Input] Se *FieldIdentifier* è un campo definite da ODBC e *ValuePtr* punta a una stringa di caratteri o binario buffer, questo argomento deve essere la lunghezza di **ValuePtr*. Per i dati di stringa di caratteri, questo argomento deve contenere il numero di byte nella stringa.  
  
 Se *FieldIdentifier* è un campo definite da ODBC e *ValuePtr* è un intero *BufferLength* viene ignorato.  
  
 Se *FieldIdentifier* è un campo definito dal driver, l'applicazione indica la natura del campo da Gestione Driver impostando il *BufferLength* argomento. *BufferLength* può avere i valori seguenti:  
  
-   Se *ValuePtr* è un puntatore a una stringa di caratteri, quindi *BufferLength* è la lunghezza della stringa o SQL_NTS.  
  
-   Se *ValuePtr* è un puntatore a un buffer binario, quindi l'applicazione inserisce il risultato del SQL_LEN_BINARY_ATTR (*lunghezza*) (macro) in *BufferLength*. Un valore negativo in questo modo vengono inserite *BufferLength*.  
  
-   Se *ValuePtr* è un puntatore a un valore diverso da una stringa di caratteri o stringa binaria, quindi *BufferLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se *ValuePtr* contiene un valore di lunghezza fissa, quindi *BufferLength* è SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_IS_USMALLINT, come appropriato.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSetDescField** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_DESC e un *gestiscono* dei *DescriptorHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLSetDescField** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01S02|Valore di opzione modificato|Il driver non supportava il valore specificato nel  *\*ValuePtr* (se *ValuePtr* era un puntatore) oppure il valore nella *ValuePtr* (se *ValuePtr*  era un valore intero), oppure  *\*ValuePtr* non è valido a causa di condizioni di lavoro di implementazione, in modo che il driver sostituito un valore simile. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07009|Indice del descrittore non valido|Il *FieldIdentifier* l'argomento è un campo di record, il *RecNumber* argomento era 0 e il *DescriptorHandle* argomento cui a un handle IPD.<br /><br /> Il *RecNumber* argomento era minore di 0 e il *DescriptorHandle* argomento definito un ARD o un APD.<br /><br /> Il *RecNumber* l'argomento è maggiore del numero massimo di colonne o parametri in grado di supportare l'origine dati, e il *DescriptorHandle* argomento definito un APD o ARD.<br /><br /> (DM) di *FieldIdentifier* argomento era SQL_DESC_COUNT, e  *\*ValuePtr* argomento era minore di 0.<br /><br /> Il *RecNumber* l'argomento è uguale a 0 e il *DescriptorHandle* argomento definito un APD allocati in modo implicito. (Questo errore si verifica con un descrittore applicazione allocati in modo esplicito, perché non è possibile sapere se un descrittore applicazione esplicito allocato è una APD o ARD fino alla fase di esecuzione.)|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|22001|Stringa troncati di dati a destra|Il *FieldIdentifier* argomento era SQL_DESC_NAME e il *BufferLength* argomento era un valore maggiore di quello SQL_MAX_IDENTIFIER_LEN.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) di *DescriptorHandle* è stato associato un *StatementHandle* per i quali è stata chiamata una funzione di esecuzione asincrona (non presente uno) ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* con cui il *DescriptorHandle* è stato associato e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.<br /><br /> (DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *DescriptorHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLSetDescField** funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per uno degli handle di istruzione associati il *DescriptorHandle* SQL_PARAM_DATA_AVAILABLE restituito. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY016|Non è possibile modificare un descrittore delle righe di implementazione|Il *DescriptorHandle* argomento è stato associato a un'implementazione e il *FieldIdentifier* argomento non è stata SQL_DESC_ARRAY_STATUS_PTR o SQL_DESC_ROWS_PROCESSED_PTR.|  
|HY021|Informazioni descrittore incoerenti.|I campi SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE non formano un tipo ODBC SQL valido o un tipo SQL specifiche del driver valido (per gli IDP) o un tipo di dati ODBC C valido (ad o ARDs Apd).<br /><br /> Le informazioni sul descrittore controllati durante una verifica coerenza non era coerente. (Vedere "Verifica coerenza" nella **SQLSetDescRec**.)|  
|HY090|Lunghezza della stringa o buffer non valido|(DM)  *\*ValuePtr* è una stringa di caratteri, e *BufferLength* era minore di zero ma non uguale a SQL_NTS.<br /><br /> (DM) il driver è stato un ODBC 2 *. x* driver, il descrittore è un ARD, il *ColumnNumber* argomento è stato impostato su 0 e il valore specificato per l'argomento *BufferLength* era non è uguale a 4.|  
|HY091|Identificatore del campo del descrittore non valido|Il valore specificato per il *FieldIdentifier* argomento non è un campo definite da ODBC e non è un valore definito dall'implementazione.<br /><br /> Il *FieldIdentifier* argomento non è valido per il *DescriptorHandle* argomento.<br /><br /> Il *FieldIdentifier* argomento era un campo di sola lettura definite da ODBC.|  
|HY092|Identificatore di attributo/opzione non è valido|Il valore in  *\*ValuePtr* non è valido per il *FieldIdentifier* argomento.<br /><br /> Il *FieldIdentifier* argomento era SQL_DESC_UNNAMED, e *ValuePtr* era SQL_NAMED.|  
|HY105|Tipo di parametro non valido|(DM) il valore specificato per il campo SQL_DESC_PARAMETER_TYPE non è valido. (Per altre informazioni, vedere la "*InputOutputType* argomento" sezione **SQLBindParameter**.)|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [What ' s New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *DescriptorHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Un'applicazione può chiamare **SQLSetDescField** impostare qualsiasi campo del descrittore uno alla volta. Una chiamata a **SQLSetDescField** imposta un singolo campo in un singolo descrittore. Questa funzione può essere chiamato per impostare i campi in qualsiasi tipo di descrittore, fornito che il campo può essere impostato. (Vedere la tabella più avanti in questa sezione).  
  
> [!NOTE]  
>  Se una chiamata a **SQLSetDescField** ha esito negativo, il contenuto del record del descrittore identificato dalle *RecNumber* argomento non sono definiti.  
  
 Altre funzioni possono essere chiamati per impostare più campi di descrizione con una singola chiamata della funzione. Il **SQLSetDescRec** funzione imposta un'ampia gamma di campi che interessano il buffer e il tipo di dati associati a una colonna o parametro (il SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL _ Campi DESC_SCALE, SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR). **SQLBindCol** oppure **SQLBindParameter** può essere utilizzata per rendere una specifica completa per l'associazione di una colonna o parametro. Queste funzioni impostano un gruppo specifico di campi di descrizione con chiamata una funzione.  
  
 **SQLSetDescField** può essere chiamato per modificare i buffer dell'associazione tramite l'aggiunta di un offset per i puntatori di associazione (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR). Questa operazione modificherà i buffer dell'associazione senza chiamare **SQLBindCol** oppure **SQLBindParameter**, che consente a un'applicazione modificare SQL_DESC_DATA_PTR senza modificare altri campi, ad esempio SQL_DESC_DATA_ digitare.  
  
 Se un'applicazione chiama **SQLSetDescField** per impostare un campo diverso da SQL_DESC_COUNT o i campi posticipati SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR o SQL_DESC_INDICATOR_PTR, diventa non associato al record.  
  
 I campi di intestazione di descrizione vengono impostati chiamando **SQLSetDescField** con l'appropriato *FieldIdentifier*. Molti campi di intestazione sono anche gli attributi di istruzione, pertanto può essere impostate inoltre mediante una chiamata a **SQLSetStmtAttr**. Ciò consente alle applicazioni di impostare un campo di descrizione senza prima ottenere un handle di descrittore. Quando **SQLSetDescField** viene chiamato per impostare un campo di intestazione, il *RecNumber* argomento verrà ignorato.  
  
 Oggetto *RecNumber* pari a 0, viene usato per impostare i campi di segnalibro.  
  
> [!NOTE]  
>  L'attributo di istruzione SQL_ATTR_USE_BOOKMARKS deve sempre essere impostata prima di chiamare **SQLSetDescField** per impostare i campi di segnalibro. Sebbene non sia obbligatorio, è consigliabile.  
  
## <a name="sequence-of-setting-descriptor-fields"></a>Sequenza di configurazione dei campi del descrittore  
 Quando si impostano i campi di descrizione chiamando **SQLSetDescField**, l'applicazione deve seguire una sequenza specifica:  
  
1.  L'applicazione prima di tutto necessario impostare il campo SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE o SQL_DESC_DATETIME_INTERVAL_CODE.  
  
2.  Dopo che è stato impostato uno di questi campi, l'applicazione può impostare un attributo di un tipo di dati e il driver imposta i campi degli attributi di tipo di dati per i valori predefiniti appropriati per il tipo di dati. La ripetizione automatica dei campi di tipo attributo assicura che il descrittore è sempre pronto per l'uso dopo l'applicazione ha specificato un tipo di dati. Se l'applicazione imposta in modo esplicito un attributo di tipo di dati, esegue l'override dell'attributo predefinito.  
  
3.  Dopo che uno dei campi elencati nel passaggio 1 è stato impostato e sono stati impostati gli attributi di tipo di dati, l'applicazione può impostare SQL_DESC_DATA_PTR. Ciò richiede una verifica di coerenza dei campi di descrizione. Se l'applicazione modifica il tipo di dati o attributi dopo aver impostato il campo SQL_DESC_DATA_PTR, il driver imposta SQL_DESC_DATA_PTR a un puntatore null, quando si separa il record. In tal modo l'applicazione per completare le procedure appropriate in sequenza, prima che il record del descrittore è utilizzabile.  
  
## <a name="initialization-of-descriptor-fields"></a>Inizializzazione dei campi di descrizione  
 Quando si alloca un descrittore, i campi del descrittore possono essere inizializzati su un valore predefinito, essere inizializzati senza un valore predefinito o essere non definito per il tipo di descrittore. Nelle tabelle seguenti indicano l'inizializzazione di ogni campo per ogni tipo di descrittore, con "D" indicante che il campo viene inizializzato con un valore predefinito e "ND" che indica che il campo viene inizializzato senza un valore predefinito. Se viene visualizzato un numero, il valore predefinito del campo è tale numero. Le tabelle indicano anche se un campo è di sola lettura (R) o lettura/scrittura (L/S).  
  
 I campi di un'implementazione hanno un valore predefinito solo dopo l'istruzione è stato preparato o eseguito e l'implementazione è stato popolato, non quando è stato allocato l'handle di istruzione o il descrittore. Fino a quando non è stato popolato il IRD, qualsiasi tentativo di ottenere l'accesso a un campo di un IRD restituirà un errore.  
  
 Alcuni campi di descrizione sono definiti per una o più, ma non tutti i tipi di descrittore (ARDs e IRDs e Apd e gli IDP). Quando un campo è definito per un tipo di descrittore, non è necessaria per tutte le funzioni che usano questo descrittore.  
  
 I campi che possano accedervi **SQLGetDescField** necessariamente non può essere impostato dal **SQLSetDescField**. I campi che possono essere impostati tramite **SQLSetDescField** sono elencati nelle tabelle seguenti.  
  
 L'inizializzazione di campi di intestazione è descritto nella tabella seguente.  
  
|Nome di campo di intestazione|type|L/S|Impostazione predefinita|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD: R APD: R IRD: R IPD: R|ARD: SQL_DESC_ALLOC_AUTO per implicite o SQL_DESC_ALLOC_USER per esplicita<br /><br /> APD: SQL_DESC_ALLOC_AUTO per implicite o SQL_DESC_ALLOC_USER per esplicita<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|ARD: R/W APD: R/W IRD: Inutilizzati IPD: Non utilizzato|ARD:[1] APD:[1] IRD: Inutilizzati IPD: Non utilizzato|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT*|ARD: R/W APD: R/W IRD: R/W IPD: L/S|ARD: Ptr APD null: Ptr null IRD: Ptr null IPD: Ptr null|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN *|ARD: R/W APD: R/W IRD: Inutilizzati IPD: Non utilizzato|ARD: Ptr APD null: Ptr null IRD: Inutilizzati IPD: Non utilizzato|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD: R/W APD: R/W IRD: Inutilizzati IPD: Non utilizzato|ARD: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD: Non utilizzato<br /><br /> IPD: Non utilizzato|  
|SQL_DESC_COUNT|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: L/S|ARD: 0 APD: 0 IRD: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN*|ARD: APD inutilizzate: Inutilizzati IRD: R/W IPD: L/S|ARD: APD inutilizzate: Inutilizzati IRD: Ptr null IPD: Ptr null|  
  
 [1] questi campi sono definiti solo quando il IPD viene popolato automaticamente dal driver. In caso contrario, non sono definite. Se un'applicazione tenta di impostare questi campi, SQLSTATE HY091 verrà restituito (identificatore del campo del descrittore non valido).  
  
 L'inizializzazione di campi del record è come illustrato nella tabella seguente.  
  
|Nome del campo di record|type|L/S|Impostazione predefinita|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: Non utilizzato|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: Non utilizzato|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR *|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: Non utilizzato|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: Non utilizzato|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR *|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: Non utilizzato|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: Non utilizzato|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: R|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: D[1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR *|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: Non utilizzato|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: Non utilizzato|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: L/S|ARD: SQL_C_ DEFAULT APD: SQL_C_ DEFAULT IRD: D IPD: ND|  
|SQL_DESC_DATA_PTR|SQLPOINTER|ARD: R/W APD: R/W IRD: Inutilizzati IPD: Non utilizzato|ARD: Ptr APD null: Ptr null IRD: Inutilizzati IPD: [2] non utilizzato|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: L/S|ARD: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD: R/W APD: R/W IRD: R IPD: L/S|ARD: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: Non utilizzato|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: Non utilizzato|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: R|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: D[1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN *|ARD: R/W APD: R/W IRD: Inutilizzati IPD: Non utilizzato|ARD: Ptr APD null: Ptr null IRD: Inutilizzati IPD: Non utilizzato|  
|SQL_DESC_LABEL|SQLCHAR *|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: Non utilizzato|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: Non utilizzato|  
|SQL_DESC_LENGTH|SQLULEN|ARD: R/W APD: R/W IRD: R IPD: L/S|ARD: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR *|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: Non utilizzato|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: Non utilizzato|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR *|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: Non utilizzato|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: Non utilizzato|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR *|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: R|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: D[1]|  
|SQL_DESC_NAME|SQLCHAR *|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: L/S|ARD: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: R|ARD: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD: R/W APD: R/W IRD: R IPD: L/S|ARD: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN|ARD: R/W APD: R/W IRD: R IPD: L/S|ARD: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN *|ARD: R/W APD: R/W IRD: Inutilizzati IPD: Non utilizzato|ARD: Ptr APD null: Ptr null IRD: Inutilizzati IPD: Non utilizzato|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD: APD inutilizzate: Inutilizzati IRD: Inutilizzati IPD: L/S|ARD: APD inutilizzate: Inutilizzati IRD: Inutilizzati IPD: D=SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: L/S|ARD: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD: Non utilizzato<br /><br /> APD: Non utilizzato<br /><br /> IRD: R<br /><br /> IPD: R|ARD: Non utilizzato<br /><br /> APD: Non utilizzato<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: L/S|ARD: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR *|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: Non utilizzato|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: Non utilizzato|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: Non utilizzato|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: Non utilizzato|  
|SQL_DESC_TABLE_NAME|SQLCHAR *|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: Non utilizzato|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: Non utilizzato|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: L/S|ARD: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
|SQL_DESC_TYPE_NAME|SQLCHAR *|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: R|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: D[1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: L/S|ARD: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: R|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: D[1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD: APD inutilizzate: Inutilizzati IRD: R IPD: Non utilizzato|ARD: APD inutilizzate: Inutilizzati IRD: D IPD: Non utilizzato|  
  
 [1] questi campi sono definiti solo quando il IPD viene popolato automaticamente dal driver. In caso contrario, non sono definite. Se un'applicazione tenta di impostare questi campi, SQLSTATE HY091 verrà restituito (identificatore del campo del descrittore non valido).  
  
 [2] per forzare un controllo di coerenza, è possibile impostare il campo SQL_DESC_DATA_PTR in IPD. In una chiamata successiva al **SQLGetDescField** oppure **SQLGetDescRec**, il driver non deve restituire il valore su cui è stato impostato SQL_DESC_DATA_PTR.  
  
## <a name="fieldidentifier-argument"></a>Argomento FieldIdentifier  
 Il *FieldIdentifier* argomento indica il campo di descrizione da impostare. Un descrittore contiene il *intestazione descrittore,* costituita da campi intestazione descritti nella sezione successiva, "Campi di intestazione" e zero o più *record del descrittore,* costituito da campi dei record descritto nella sezione seguente la sezione "Campi di intestazione".  
  
## <a name="header-fields"></a>Campi di intestazione  
 Ogni descrittore presenta un'intestazione costituita i campi seguenti:  
  
 **SQL_DESC_ALLOC_TYPE [All]**  
 Questo campo di intestazione SQLSMALLINT di sola lettura consente di specificare se il descrittore allocato automaticamente dal driver o in modo esplicito dall'applicazione. L'applicazione può ottenere, ma non modificato, questo campo. Il campo è impostato su SQL_DESC_ALLOC_AUTO dal driver, se il descrittore allocato automaticamente dal driver. È impostato per SQL_DESC_ALLOC_USER dal driver se il descrittore è stato allocato in modo esplicito dall'applicazione.  
  
 **SQL_DESC_ARRAY_SIZE [descrittori applicazione]**  
 In ARDs, questo campo di intestazione SQLULEN specifica il numero di righe nel set di righe. Questo è il numero di righe da restituire mediante una chiamata a **SQLFetch** oppure **SQLFetchScroll** o da una chiamata a deve operare **SQLBulkOperations** o **SQLSetPos** .  
  
 In Apd, questo campo di intestazione SQLULEN specifica il numero di valori per ogni parametro.  
  
 Il valore predefinito di questo campo è 1. Se è maggiore di 1 SQL_DESC_ARRAY_SIZE SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR del APD o ARD puntare alle matrici. La cardinalità di ogni matrice è uguale al valore di questo campo.  
  
 Questo campo nel ARD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_ROW_ARRAY_SIZE. Questo campo in APD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_PARAMSET_SIZE.  
  
 **SQL_DESC_ARRAY_STATUS_PTR [All]**  
 Per ogni tipo di descrittore questo SQLUSMALLINT * i punti di campo di intestazione in una matrice di valori SQLUSMALLINT. Questi array sono denominati come segue: matrice di stato (IRD), la matrice di stato parametro (IPD), riga operazione matrice (ARD) e matrice di parametri operazione (APD) di righe.  
  
 Nell'implementazione, questo campo di intestazione fa riferimento a una matrice di stato di riga contenente i valori di stato dopo una chiamata a **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, oppure **SQLSetPos**. La matrice ha tutti gli elementi poiché sono presenti righe nel set di righe. L'applicazione deve allocare una matrice di SQLUSMALLINTs e impostare questo campo in modo da puntare alla matrice. Il campo è impostato su un puntatore null per impostazione predefinita. Il driver popolerà la matrice -, a meno che il campo SQL_DESC_ARRAY_STATUS_PTR è impostato su un puntatore null, nel qual caso non vengono generati valori di stato e la matrice non viene popolata.  
  
> [!CAUTION]  
>  Driver comportamento sarà indefinito se l'applicazione imposta gli elementi della matrice di stato di riga a cui punta il campo SQL_DESC_ARRAY_STATUS_PTR di implementazione.  
  
 La matrice viene inizialmente popolata da una chiamata a **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, oppure **SQLSetPos**. Se la chiamata non restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il contenuto della matrice a cui punta questo campo è non definito. Gli elementi della matrice possono contenere i valori seguenti:  
  
-   SQL_ROW_SUCCESS: La riga è stata recuperata correttamente e non è stato modificato dopo l'ultimo recupero.  
  
-   SQL_ROW_SUCCESS_WITH_INFO: La riga è stata recuperata correttamente e non è stato modificato dopo l'ultimo recupero. Tuttavia, è stato restituito un avviso sulla riga.  
  
-   SQL_ROW_ERROR: Si è verificato un errore durante il recupero della riga.  
  
-   SQL_ROW_UPDATED: La riga è stata recuperata correttamente ed è stata aggiornata dopo l'ultimo recupero. Se la riga viene recuperata di nuovo, il relativo stato è SQL_ROW_SUCCESS.  
  
-   SQL_ROW_DELETED: La riga è stata eliminata dopo l'ultimo recupero.  
  
-   SQL_ROW_ADDED: La riga inserita da **SQLBulkOperations**. Se la riga viene recuperata di nuovo, il relativo stato è SQL_ROW_SUCCESS.  
  
-   SQL_ROW_NOROW: Il set di righe sovrapposti la fine del set di risultati, ed è stata restituita alcuna riga che corrisponde a questo elemento della matrice di stato di riga.  
  
 Questo campo nell'implementazione può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo vengono impostati SQL_ATTR_ROW_STATUS_PTR.  
  
 Il campo SQL_DESC_ARRAY_STATUS_PTR di implementazione è valido solo dopo che è stato restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO. Se il codice restituito non è uno di questi, il percorso a cui punta SQL_DESC_ROWS_PROCESSED_PTR è indefinito.  
  
 In IPD, questo campo di intestazione punta a una matrice di stato di parametri contenente informazioni sullo stato per ogni set di valori dei parametri dopo una chiamata a **SQLExecute** oppure **SQLExecDirect**. Se la chiamata a **SQLExecute** oppure **SQLExecDirect** non ha restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il contenuto della matrice a cui punta questo campo non sono definiti. L'applicazione deve allocare una matrice di SQLUSMALLINTs e impostare questo campo in modo da puntare alla matrice. Il driver popolerà la matrice -, a meno che il campo SQL_DESC_ARRAY_STATUS_PTR è impostato su un puntatore null, nel qual caso non vengono generati valori di stato e la matrice non viene popolata. Gli elementi della matrice possono contenere i valori seguenti:  
  
-   SQL_PARAM_SUCCESS: L'istruzione SQL è stata eseguita correttamente per questo set di parametri.  
  
-   SQL_PARAM_SUCCESS_WITH_INFO: L'istruzione SQL è stata eseguita correttamente per questo set di parametri. Tuttavia, le informazioni sull'avviso è disponibile nella struttura di dati di diagnostica.  
  
-   SQL_PARAM_ERROR: Si è verificato un errore nell'elaborazione di questo set di parametri. Informazioni aggiuntive sull'errore è disponibile nella struttura di dati di diagnostica.  
  
-   SQL_PARAM_UNUSED: Questo set di parametri è inutilizzato, probabilmente dovuto al fatto che alcuni set di parametri precedente ha causato un errore che ha interrotto l'ulteriore elaborazione o SQL_PARAM_IGNORE è stato impostato per tale set di parametri nella matrice specificata dal campo SQL_DESC_ARRAY_STATUS_PTR di APD.  
  
-   SQL_PARAM_DIAG_UNAVAILABLE: Informazioni di diagnostica non sono disponibile. Un esempio è quando il driver considera le matrici di parametri come un'unità monolitica e, in modo non genera questo livello di informazioni sull'errore.  
  
 Questo campo in IPD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_PARAM_STATUS_PTR.  
  
 In ARD, questo campo di intestazione punta a una matrice di operazione riga di valori che possono essere impostate tramite l'applicazione di indicare se questa riga deve essere ignorato per **SQLSetPos** operazioni. Gli elementi della matrice possono contenere i valori seguenti:  
  
-   SQL_ROW_PROCEED: La riga è incluso nell'operazione di massa usando **SQLSetPos**. (Questa impostazione non garantisce che verrà eseguita l'operazione sulla riga. Se la riga ha lo stato SQL_ROW_ERROR nella matrice di stato di riga IRD, il driver non sia in grado di eseguire l'operazione della riga.)  
  
-   SQL_ROW_IGNORE: La riga viene escluso dall'operazione bulk utilizzando **SQLSetPos**.  
  
 Se nessun elemento della matrice è impostato, tutte le righe sono inclusi nell'operazione di massa. Se il valore nel campo SQL_DESC_ARRAY_STATUS_PTR del ARD è un puntatore null, tutte le righe sono inclusi nell'operazione di massa; l'interpretazione è lo stesso come se il puntatore punta a una matrice valida e tutti gli elementi della matrice sono stati SQL_ROW_PROCEED. Se un elemento nella matrice è impostato su SQL_ROW_IGNORE, il valore nella matrice di stato di riga per la riga ignorata non viene modificato.  
  
 Questo campo nel ARD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_ROW_OPERATION_PTR.  
  
 In APD, questo campo di intestazione fa riferimento a una matrice di operazione parametro dei valori che possono essere impostate tramite l'applicazione di indicare se questo set di parametri deve essere ignorata quando **SQLExecute** o **SQLExecDirect**viene chiamato. Gli elementi della matrice possono contenere i valori seguenti:  
  
-   SQL_PARAM_PROCEED: Il set di parametri è incluso nel **SQLExecute** oppure **SQLExecDirect** chiamare.  
  
-   SQL_PARAM_IGNORE: Il set di parametri è escluso dal **SQLExecute** oppure **SQLExecDirect** chiamare.  
  
 Se nessun elemento della matrice è impostato, tutti i set di parametri nella matrice vengono utilizzati la **SQLExecute** o **SQLExecDirect** chiamate. Se il valore nel campo SQL_DESC_ARRAY_STATUS_PTR di APD è un puntatore null, vengono utilizzati tutti i set di parametri. l'interpretazione è lo stesso come se il puntatore punta a una matrice valida e tutti gli elementi della matrice sono stati SQL_PARAM_PROCEED.  
  
 Questo campo in APD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_PARAM_OPERATION_PTR.  
  
 **SQL_DESC_BIND_OFFSET_PTR [descrittori applicazione]**  
 Questo SQLLEN * punti di campo di intestazione all'offset di associazione. Si è impostato su un puntatore null per impostazione predefinita. Se questo campo non è un puntatore null, il driver Dereferenzia il puntatore e aggiunge il valore dereferenziato a ognuno dei campi posticipati che ha un valore diverso da null nel record del descrittore (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR) durante l'associazione a recuperare ora e Usa i nuovi valori di puntatore.  
  
 L'offset di associazione è sempre stato aggiunto direttamente i valori nei campi SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR. Se l'offset viene modificato in un valore diverso, il nuovo valore viene ancora aggiunto direttamente al valore in ogni campo del descrittore. Nuovo offset non viene aggiunto al valore del campo più alcun offset precedenti.  
  
 Questo campo è un *campi posticipati*: Non è utilizzato al momento è impostata, ma viene usato in un secondo momento dal driver, quando è necessario determinare gli indirizzi per i buffer dei dati.  
  
 Questo campo nel ARD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_ROW_BIND_OFFSET_PTR. Questo campo nel ARD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_PARAM_BIND_OFFSET_PTR.  
  
 Per altre informazioni, vedere la descrizione dell'associazione per riga in [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) e [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 **SQL_DESC_BIND_TYPE [descrittori applicazione]**  
 Questo campo di intestazione SQLUINTEGER imposta l'orientamento di associazione da usare per colonne o parametri di associazione.  
  
 In ARDs, questo campo specifica l'orientamento di binding quando **SQLFetchScroll** oppure **SQLFetch** viene chiamato nell'handle di istruzione associata.  
  
 Per selezionare l'associazione per colonna per le colonne, questo campo è impostato su SQL_BIND_BY_COLUMN (predefinito).  
  
 Questo campo nel ARD può essere impostato anche chiamando **SQLSetStmtAttr** con il SQL_ATTR_ROW_BIND_TYPE *attributo*.  
  
 In Apd, questo campo specifica l'orientamento di associazione da utilizzare per i parametri dinamici.  
  
 Per selezionare l'associazione per colonna per i parametri, questo campo è impostato su SQL_BIND_BY_COLUMN (predefinito).  
  
 Questo campo in APD può essere impostato anche chiamando **SQLSetStmtAttr** con il SQL_ATTR_PARAM_BIND_TYPE *attributo*.  
  
 **SQL_DESC_COUNT [All]**  
 Questo campo di intestazione SQLSMALLINT specifica l'indice in base 1 del record con numero più alto che contiene i dati. Quando il driver imposta la struttura dei dati per il descrittore, anche necessario impostare il campo SQL_DESC_COUNT per mostrare il numero di record è significativo. Quando un'applicazione alloca un'istanza di questa struttura di dati, non è necessario specificare il numero di record per riservare spazio per. Come l'applicazione specifica il contenuto dei record, il driver accetta qualsiasi azione necessaria per garantire che l'handle descrittore fa riferimento a una struttura di dati della dimensione adeguata.  
  
 SQL_DESC_COUNT non è un conteggio di tutte le colonne di dati che sono associate (se il campo è in un ARD) o di tutti i parametri di associazione (se il campo è in un APD), ma il numero di record con numero più alto. Se la colonna con numero più alto o il parametro non è associato, SQL_DESC_COUNT viene modificato il numero di colonna con numero più alto successivo o del parametro. Se una colonna o un parametro con un numero che è inferiore al numero di colonna con numero più alto non è associato (chiamando **SQLBindCol** con il *TargetValuePtr* argomento impostato a un puntatore null, ovvero **SQLBindParameter** con il *ParameterValuePtr* argomento impostato su un puntatore null), SQL_DESC_COUNT non viene modificato. Se altre colonne o parametri di associazione con un numero maggiore di record con numero più alto che contiene i dati, il driver aumenta automaticamente il valore del campo SQL_DESC_COUNT. Se tutte le colonne non sono associate chiamando **SQLFreeStmt** con l'opzione SQL_UNBIND, i campi SQL_DESC_COUNT ARD e IRD vengono impostati su 0. Se **SQLFreeStmt** viene chiamato con l'opzione SQL_RESET_PARAMS, i campi SQL_DESC_COUNT in APD e IPD vengono impostati su 0.  
  
 Il valore in SQL_DESC_COUNT può essere impostato in modo esplicito da un'applicazione chiamando **SQLSetDescField**. Se il valore in SQL_DESC_COUNT è diminuito in modo esplicito, tutti i record con un numero maggiore del valore nuovo in SQL_DESC_COUNT vengono rimossi in modo efficace. Se il valore in SQL_DESC_COUNT è impostato esplicitamente su 0 e il campo è in un ARD, vengono rilasciati tutti i buffer di dati, ad eccezione di una colonna del segnalibro associato.  
  
 Il functoid Conteggio record in questo campo di un ARD non include una colonna del segnalibro associato. L'unico modo per annullare l'associazione di una colonna del segnalibro consiste nell'impostare il campo SQL_DESC_DATA_PTR a un puntatore null.  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [descrittori di implementazione]**  
 In un'implementazione, questa SQLULEN \* intestazione campo punta a un buffer contenente il numero di righe recuperate dopo una chiamata a **SQLFetch** oppure **SQLFetchScroll**, o il numero di righe interessate in un'operazione bulk eseguito da una chiamata a **SQLBulkOperations** oppure **SQLSetPos**, tra cui le righe di errore.  
  
 In un IPD, questo SQLUINTEGER * intestazione campo punta a un buffer contenente il numero di set di parametri che sono stati elaborati, compresi i set di errore. Non verrà restituito alcun numero se si tratta di un puntatore null.  
  
 SQL_DESC_ROWS_PROCESSED_PTR è valido solo dopo che è stato restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO dopo una chiamata a **SQLFetch** oppure **SQLFetchScroll** (per un campo IRD) o **SQLExecute** , **SQLExecDirect**, o **SQLParamData** (per un campo IPD). Se la chiamata che viene riempito il buffer a cui fa riferimento questo campo non viene restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il contenuto del buffer non è definito, a meno che non viene restituito SQL_NO_DATA, nel qual caso il valore nel buffer è impostato su 0.  
  
 Questo campo nel ARD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_ROWS_FETCHED_PTR. Questo campo in APD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_PARAMS_PROCESSED_PTR.  
  
 Il buffer a cui punta questo campo viene allocato dall'applicazione. È un buffer di output posticipato che viene impostato dal driver. Si è impostato su un puntatore null per impostazione predefinita.  
  
## <a name="record-fields"></a>Campi di record  
 Ogni descrittore contiene uno o più record costituita dai campi che definiscono i dati delle colonne o parametri dinamici, a seconda del tipo di descrittore. Ogni record è una definizione completa di una singola colonna o parametro.  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 Questo campo di record SQLINTEGER di sola lettura contiene SQL_TRUE se la colonna è una colonna a incremento automatico o SQL_FALSE se la colonna non è una colonna a incremento automatico. Questo campo è di sola lettura, ma la colonna a incremento automatico sottostante non è necessariamente di sola lettura.  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 Questo SQLCHAR di sola lettura * campi di record contiene il nome di colonna di base per colonna del set di risultati. Se non esiste un nome di colonna di base (come nel caso delle colonne che sono espressioni), questa variabile contiene una stringa vuota.  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 Questo SQLCHAR di sola lettura * campi di record contiene il nome della tabella di base per colonna del set di risultati. Se un nome di tabella di base non può essere definito o non è applicabile, questa variabile contiene una stringa vuota.  
  
 **SQL_DESC_CASE_SENSITIVE [descrittori di implementazione]**  
 Questo campo di record SQLINTEGER di sola lettura contiene SQL_TRUE se la colonna o il parametro deve essere trattata come distinzione maiuscole/minuscole per le regole di confronto e i confronti o SQL_FALSE se la colonna non viene considerata come distinzione maiuscole/minuscole per le regole di confronto e i confronti o se si tratta di una non di tipo carattere colonna.  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 Questo SQLCHAR di sola lettura * campi di record contengono il catalogo per la tabella di base che contiene la colonna. Se la colonna è un'espressione o se la colonna fa parte di una vista, il valore restituito è dipendente dal driver. Se l'origine dati non supporta cataloghi o non è possibile determinare il catalogo, questa variabile contiene una stringa vuota.  
  
 **SQL_DESC_CONCISE_TYPE [All]**  
 Questo campo di intestazione SQLSMALLINT specifica il tipo di dati concisa per tutti i tipi di dati, inclusi i tipi di dati Data/ora e intervallo.  
  
 I valori nei campi SQL_DESC_CONCISE_TYPE SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE sono interdipendenti. Ogni volta che uno dei campi è impostata, l'altra deve essere impostata. SQL_DESC_CONCISE_TYPE può essere impostata da una chiamata a **SQLBindCol** oppure **SQLBindParameter**, o **SQLSetDescField**. SQL_DESC_TYPE può essere impostata da una chiamata a **SQLSetDescField** oppure **SQLSetDescRec**.  
  
 Se SQL_DESC_CONCISE_TYPE è impostata su un tipo di dati concisa diverso da un tipo di dati datetime o intervallo, il campo SQL_DESC_TYPE è impostato sullo stesso valore e il campo SQL_DESC_DATETIME_INTERVAL_CODE è impostato su 0.  
  
 Se SQL_DESC_CONCISE_TYPE è impostato per il tipo di dati datetime o intervallo conciso, il campo SQL_DESC_TYPE è impostato per il corrispondente tipo verbose (SQL_DATETIME o SQL_INTERVAL) e il campo SQL_DESC_DATETIME_INTERVAL_CODE è impostato per il codice secondario appropriato.  
  
 **SQL_DESC_DATA_PTR [descrittori dell'applicazione e gli IDP]**  
 Questo campo record SQLPOINTER punta a una variabile che conterrà il valore del parametro (per Apd) o il valore della colonna (per ARDs). Questo campo è un *campi posticipati*. Non è utilizzato al momento è impostata, ma viene utilizzato in un secondo momento dal driver per recuperare i dati.  
  
 La colonna specificata dal campo SQL_DESC_DATA_PTR del ARD è non associata, se il *TargetValuePtr* argomento nella chiamata a **SQLBindCol** è un puntatore null o se il SQL_DESC_DATA_PTR campo nel ARD è impostata un le chiamate a **SQLSetDescField** oppure **SQLSetDescRec** a un puntatore null. Se il campo SQL_DESC_DATA_PTR viene impostato su un puntatore null, gli altri campi non sono interessati.  
  
 Se la chiamata a **SQLFetch** oppure **SQLFetchScroll** che compila il buffer a cui punta questo campo non ha restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il contenuto del buffer non è definito.  
  
 Ogni volta che il campo SQL_DESC_DATA_PTR di un APD, ARD o IPD è impostato, il driver verificherà che il valore nel campo SQL_DESC_TYPE contiene i tipi di dati C ODBC validi o un tipo di dati specifici del driver, e che tutti gli altri campi che interessano i tipi di dati sono coerenti. Richiedere una verifica coerenza è l'uso solo del campo SQL_DESC_DATA_PTR di un IPD. In particolare, se un'applicazione imposta il campo SQL_DESC_DATA_PTR un IPD e le chiamate successive **SQLGetDescField** su questo campo non viene necessariamente restituito il valore che aveva impostato. Per altre informazioni, vedere "Le verifiche coerenza" nella [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [All]**  
 Questo campo SQLSMALLINT di record contiene il codice secondario per il tipo di dati datetime o intervallo specifico quando il campo SQL_DESC_TYPE è SQL_DATETIME o SQL_INTERVAL. Questo vale per i tipi di dati sia SQL che C. Il codice è costituito il nome del tipo di dati con "CODE" sostituisce "TYPE" o "C_TYPE" (per i tipi data/ora), o "CODE" sostituisce "INTERVAL" o "C_INTERVAL" (per i tipi di intervallo).  
  
 Se SQL_DESC_TYPE SQL_DESC_CONCISE_TYPE in un descrittore applicazione sono impostate su SQL_C_DEFAULT e il descrittore non è associato a un handle di istruzione, il contenuto di SQL_DESC_DATETIME_INTERVAL_CODE è definito.  
  
 Questo campo può essere impostato per i tipi di dati Data/ora elencati nella tabella seguente.  
  
|Tipi DateTime|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/ SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 Questo campo può essere impostato per i tipi di dati di intervallo elencati nella tabella seguente.  
  
|Tipo di intervallo|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY / SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR/ SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/ SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND / SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR/ SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/ SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND / SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/ SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND / SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH / SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND / SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR / SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH/ SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 Per altre informazioni su questo campo e gli intervalli di dati, vedere [identificatori di tipo di dati e i descrittori](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [All]**  
 Questo campo di record SQLINTEGER contiene l'intervallo di precisione iniziale se il campo SQL_DESC_TYPE è SQL_INTERVAL. Quando il campo SQL_DESC_DATETIME_INTERVAL_CODE è impostato su un tipo di dati di intervallo, questo campo è impostato per l'intervallo predefinito di precisione iniziale.  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 Questo campo di record SQLINTEGER di sola lettura contiene il numero massimo di caratteri necessari per visualizzare i dati dalla colonna.  
  
 **SQL_DESC_FIXED_PREC_SCALE [descrittori di implementazione]**  
 Questo campo di record SQLSMALLINT di sola lettura viene impostato su SQL_TRUE se la colonna è una colonna numerica esatta e ha precisione e scala diverso da zero, oppure a SQL_FALSE se la colonna non è una colonna numerica esatta con scala e precisione fisse.  
  
 **SQL_DESC_INDICATOR_PTR [descrittori applicazione]**  
 In ARDs, questo SQLLEN * campo punta alla variabile dell'indicatore di record. Se il valore della colonna è un valore NULL, questa variabile contiene SQL_NULL_DATA. Per Apd, la variabile indicatore è impostata su SQL_NULL_DATA per specificare gli argomenti dinamici NULL. In caso contrario, la variabile è zero (a meno che i valori in SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR sono lo stesso puntatore).  
  
 Se il campo SQL_DESC_INDICATOR_PTR un ARD è un puntatore null, il driver viene impedito di restituzione di informazioni su se la colonna è NULL o non. Se la colonna è NULL e SQL_DESC_INDICATOR_PTR è un puntatore null, SQLSTATE 22002 (variabile indicatore necessaria ma non fornito) viene restituito quando il driver tenta di popolare i buffer dopo una chiamata a **SQLFetch** o  **SQLFetchScroll**. Se la chiamata a **SQLFetch** oppure **SQLFetchScroll** non ha restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il contenuto del buffer non sono definiti.  
  
 Il campo SQL_DESC_INDICATOR_PTR determina se il campo a cui punta SQL_DESC_OCTET_LENGTH_PTR è impostato. Se il valore dei dati per una colonna è NULL, il driver imposta la variabile indicatore su SQL_NULL_DATA. Il campo a cui punta SQL_DESC_OCTET_LENGTH_PTR quindi non è impostato. Se un valore NULL non viene rilevato durante l'operazione di recupero, il buffer a cui punta SQL_DESC_INDICATOR_PTR viene impostato su zero e il buffer a cui punta SQL_DESC_OCTET_LENGTH_PTR viene impostato per la lunghezza dei dati.  
  
 Se il campo SQL_DESC_INDICATOR_PTR un APD è un puntatore null, l'applicazione non è possibile usare questo record del descrittore per specificare gli argomenti NULL.  
  
 Questo campo è un *campi posticipati*: Non è utilizzato al momento è impostata, ma viene usato in un secondo momento dal driver per indicare i valori null (per ARDs) o per determinare i valori null (per Apd).  
  
 **SQL_DESC_LABEL [IRDs]**  
 Questo SQLCHAR di sola lettura * campi di record contiene l'etichetta di colonna o il titolo. Se la colonna non ha un'etichetta, questa variabile contiene il nome della colonna. Se la colonna senza nome e senza etichetta, questa variabile contiene una stringa vuota.  
  
 **SQL_DESC_LENGTH [All]**  
 Questo campo di record SQLULEN è la lunghezza massima o effettiva di una stringa di caratteri in caratteri o un tipo di dati binari in byte. È la lunghezza massima per un tipo di dati a lunghezza fissa oppure la lunghezza effettiva per un tipo di dati a lunghezza variabile. Il valore esclude sempre il carattere di terminazione null che termina la stringa di caratteri. Per i valori il cui tipo è SQL_TYPE_DATE, SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP o uno dei tipi di dati intervallo SQL, questo campo ha la lunghezza in caratteri della rappresentazione di stringa di caratteri del valore datetime o intervallo.  
  
 Il valore in questo campo potrebbe essere diverso dal valore di "length" come definito in ODBC 2*x*. Per altre informazioni, vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 Questo SQLCHAR di sola lettura * campi di record contengano uno o più caratteri che il driver riconosce come un prefisso per un valore letterale di questo tipo di dati. Questa variabile contiene una stringa vuota per un tipo di dati per cui non è applicabile un prefisso letterale.  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 Questo SQLCHAR di sola lettura * campi di record contengano uno o più caratteri che il driver riconosce come un suffisso per un valore letterale di questo tipo di dati. Questa variabile contiene una stringa vuota per un tipo di dati per il quale un suffisso letterale non è applicabile.  
  
 **SQL_DESC_LOCAL_TYPE_NAME [descrittori di implementazione]**  
 Questo SQLCHAR di sola lettura * campi di record contiene qualsiasi nome localizzato (native language) per il tipo di dati che potrebbe essere diverso dal nome del tipo di dati regolare. Se è presente alcun nome localizzato, viene restituita una stringa vuota. Questo campo è solo a fini di visualizzazione.  
  
 **SQL_DESC_NAME [descrittori di implementazione]**  
 Questo SQLCHAR * campi di record in un descrittore riga contiene l'alias di colonna, se applicabile. Se non si applica l'alias di colonna, viene restituito il nome della colonna. In entrambi i casi, il driver imposta il campo SQL_DESC_UNNAMED su SQL_NAMED quando si imposta il campo SQL_DESC_NAME. Se è presente alcun nome di colonna o un alias di colonna, il driver restituisce una stringa vuota nel campo SQL_DESC_NAME e imposta il campo SQL_DESC_UNNAMED SQL_UNNAMED.  
  
 Un'applicazione può impostare il campo SQL_DESC_NAME di un IPD per un nome di parametro o un alias per specificare i parametri della stored procedure in base al nome. (Per altre informazioni, vedere [Binding Parameters by Name (Named Parameters)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md).) Il campo SQL_DESC_NAME di un'implementazione è un campo di sola lettura. SQLSTATE HY091 (identificatore del campo del descrittore non valido) verrà restituito se un'applicazione tenta di impostarlo.  
  
 Negli IDP, questo campo è definito se il driver non supporta parametri denominati. Se il driver supporta parametri denominati e sia in grado di descrivere i parametri, in questo campo viene restituito il nome del parametro.  
  
 **SQL_DESC_NULLABLE [descrittori di implementazione]**  
 In IRDs, questo campo di record SQLSMALLINT di sola lettura è SQL_NULLABLE se la colonna può contenere valori NULL, SQL_NO_NULLS se la colonna non ha i valori NULL o SQL_NULLABLE_UNKNOWN se non è noto se la colonna accetta valori NULL. Questo campo riguarda la colonna del set di risultati, non la colonna di base.  
  
 Negli IDP, questo campo viene sempre impostato su SQL_NULLABLE perché i parametri dinamici sono sempre nullable e non possono essere impostati da un'applicazione.  
  
 **SQL_DESC_NUM_PREC_RADIX [All]**  
 Questo campo SQLINTEGER contiene un valore pari a 2 se il tipo di dati nel campo SQL_DESC_TYPE è un tipo di dati numerici approssimati, perché il campo SQL_DESC_PRECISION contiene il numero di bit. Questo campo contiene un valore pari a 10 se il tipo di dati nel campo SQL_DESC_TYPE è un tipo di dati numerici esatti, perché il campo SQL_DESC_PRECISION contiene il numero di cifre decimali. Questo campo è impostato su 0 per tutti i tipi di dati non numerici.  
  
 **SQL_DESC_OCTET_LENGTH [All]**  
 Questo campo di record SQLLEN contiene la lunghezza, espressa in byte, di una stringa di caratteri o un tipo di dati binari. Carattere a lunghezza fissa o tipi binari, questa è la lunghezza effettiva in byte. Per i tipi binari o carattere a lunghezza variabile questa è la lunghezza massima in byte. Questo valore esclude sempre spazio per il carattere di terminazione null per i descrittori di implementazione e include sempre spazio per il carattere di terminazione null per i descrittori di applicazione. Per i dati dell'applicazione, questo campo contiene la dimensione del buffer. Per Apd, questo campo viene definito solo per i parametri di output o input/output.  
  
 **SQL_DESC_OCTET_LENGTH_PTR [descrittori applicazione]**  
 Questo SQLLEN * registrare campo punta a una variabile che conterrà la lunghezza totale in byte di un argomento dinamico (per i descrittori di parametri) o di un valore della colonna associata (per i descrittori delle righe).  
  
 Per un APD, questo valore viene ignorato per tutti gli argomenti, ad eccezione di stringa di caratteri e binari; Se questo campo fa riferimento a SQL_NTS, l'argomento dinamico deve essere con terminazione null. Per indicare che un parametro associato è un parametro data-at-execution, un'applicazione imposta questo campo nel record di APD appropriato a una variabile che, nel tempo, eseguire conterrà il valore SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC . Se è presente più di un campo, è possibile impostare SQL_DESC_DATA_PTR su un valore che identifica in modo univoco il parametro per determinare quale parametro è richiesto l'applicazione.  
  
 Se il campo OCTET_LENGTH_PTR di un ARD è un puntatore null, il driver non restituisce informazioni sulla lunghezza della colonna. Se il campo SQL_DESC_OCTET_LENGTH_PTR di un APD è un puntatore null, il driver presuppone che le stringhe di caratteri e valori binari sono con terminazione null. (I valori binari non devono essere con terminazione null ma devono avere una lunghezza per evitare il troncamento).  
  
 Se la chiamata a **SQLFetch** oppure **SQLFetchScroll** che compila il buffer a cui punta questo campo non ha restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il contenuto del buffer non è definito. Questo campo è un *campi posticipati*. Non è utilizzato al momento è impostata, ma viene utilizzato in un secondo momento dal driver per determinare o indicare la lunghezza dell'ottetto dei dati.  
  
 **SQL_DESC_PARAMETER_TYPE [IPDs]**  
 Questo campo SQLSMALLINT di record è impostato su SQL_PARAM_INPUT per un parametro di input, SQL_PARAM_INPUT_OUTPUT per un parametro di input/output SQL_PARAM_OUTPUT per un parametro di output, SQL_PARAM_INPUT_OUTPUT_STREAM per un parametro inviato nel flusso di input/output o SQL _ PARAM_OUTPUT_STREAM per un parametro di output di streaming. Si è impostato su SQL_PARAM_INPUT per impostazione predefinita.  
  
 Per un IPD, il campo è impostato su SQL_PARAM_INPUT per impostazione predefinita se IPD non viene popolato automaticamente dal driver (l'attributo di istruzione SQL_ATTR_ENABLE_AUTO_IPD è SQL_FALSE). Un'applicazione deve impostare questo campo in IPD per i parametri che non sono parametri di input.  
  
 **SQL_DESC_PRECISION [All]**  
 Questo campo SQLSMALLINT di record contiene il numero di cifre per un tipo numerico esatto, il numero di bit nella mantissa (precisione binaria) per un tipo numerico approssimato o il numero di cifre nel componente di secondi frazionari per la SQL_TYPE_TIME, rilevato SQL_C_TYPE o tipo di dati SQL_INTERVAL_SECOND. Questo campo è definito per tutti gli altri tipi di dati.  
  
 Il valore in questo campo potrebbe essere diverso dal valore di "precisione" come definito in ODBC 2*x*. Per altre informazioni, vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_ROWVER [descrittori di implementazione]**  
 Questo campo SQLSMALLINTrecord indica se una colonna viene modificata automaticamente dal sistema DBMS quando viene aggiornata una riga (ad esempio, una colonna di tipo "timestamp" in SQL Server). Il valore di questo campo di record è impostato su SQL_TRUE se la colonna è una colonna di controllo delle versioni di riga e SQL_FALSE in caso contrario. Questo attributo della colonna è simile alla chiamata **SQLSpecialColumns** con IdentifierType SQL_ROWVER per determinare se una colonna viene aggiornata automaticamente.  
  
 **SQL_DESC_SCALE [All]**  
 Questo campo SQLSMALLINT di record contiene alla scala definita per i tipi di dati decimali e numerici. Il campo è definito per tutti gli altri tipi di dati.  
  
 Il valore in questo campo può essere diverso dal valore per "scalabilità" come definito in ODBC 2*x*. Per altre informazioni, vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 Questo SQLCHAR di sola lettura * campi di record contiene il nome dello schema della tabella di base che contiene la colonna. Se la colonna è un'espressione o se la colonna fa parte di una vista, il valore restituito è dipendente dal driver. Se l'origine dati non supporta schemi o non è possibile determinare il nome dello schema, questa variabile contiene una stringa vuota.  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 Questo campo di record SQLSMALLINT di sola lettura è impostato su uno dei valori seguenti:  
  
-   SQL_PRED_NONE se la colonna non può essere utilizzata in una **in cui** clausola. (Questo è lo stesso come il valore SQL_UNSEARCHABLE in ODBC 2*x*.)  
  
-   SQL_PRED_CHAR se la colonna può essere utilizzata una **in cui** clausola ma solo con i **, ad esempio** predicato. (Questo è lo stesso come il valore SQL_LIKE_ONLY in ODBC 2*x*.)  
  
-   SQL_PRED_BASIC se la colonna può essere utilizzata una **in cui** clausola con tutti gli operatori di confronto tranne **, ad esempio**. (Questo è lo stesso come il valore SQL_EXCEPT_LIKE in ODBC 2*x*.)  
  
-   SQL_PRED_SEARCHABLE se la colonna può essere utilizzata una **in cui** clausola con qualsiasi operatore di confronto.  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 Questo SQLCHAR di sola lettura * campi di record contiene il nome della tabella di base che contiene questa colonna. Se la colonna è un'espressione o se la colonna fa parte di una vista, il valore restituito è dipendente dal driver.  
  
 **SQL_DESC_TYPE [All]**  
 Questo campo SQLSMALLINT di record specifica il tipo di dati di concisa SQL o C per tutti i tipi di dati eccetto i tipi di dati Data/ora e intervallo. Per i tipi di dati datetime e interval, questo campo specifica il tipo di dati dettagliati che è SQL_DATETIME o SQL_INTERVAL.  
  
 Ogni volta che questo campo contiene SQL_DATETIME o SQL_INTERVAL, il campo SQL_DESC_DATETIME_INTERVAL_CODE deve contenere il codice secondario appropriato per il tipo conciso. Per tipi di dati datetime SQL_DESC_TYPE contiene SQL_DATETIME e il campo SQL_DESC_DATETIME_INTERVAL_CODE contiene un codice secondario per il tipo di dati Data/ora specifica. Per i tipi di dati di intervallo, SQL_DESC_TYPE contiene SQL_INTERVAL e il campo SQL_DESC_DATETIME_INTERVAL_CODE contiene un codice secondario per il tipo di dati di intervallo specifico.  
  
 I valori nei campi SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE sono interdipendenti. Ogni volta che uno dei campi è impostata, l'altra deve essere impostata. SQL_DESC_TYPE può essere impostata da una chiamata a **SQLSetDescField** oppure **SQLSetDescRec**. SQL_DESC_CONCISE_TYPE può essere impostata da una chiamata a **SQLBindCol** oppure **SQLBindParameter**, o **SQLSetDescField**.  
  
 Se SQL_DESC_TYPE è impostato su un tipo di dati concisa diverso da un tipo di dati datetime o intervallo, il campo SQL_DESC_CONCISE_TYPE è impostato sullo stesso valore e il campo SQL_DESC_DATETIME_INTERVAL_CODE è impostato su 0.  
  
 Se SQL_DESC_TYPE è impostato su dettagliato valore datetime o tipo di dati di intervallo (SQL_DATETIME o SQL_INTERVAL) e il campo SQL_DESC_DATETIME_INTERVAL_CODE è impostato per il codice secondario appropriato, il campo tipo SQL_DESC_CONCISE è impostato per il tipo conciso corrispondente. Tentativo di impostare SQL_DESC_TYPE in uno dei tipi datetime o intervallo concisi restituiranno SQLSTATE HY021 (informazioni sul descrittore inconsistenti).  
  
 Se il campo SQL_DESC_TYPE è impostato da una chiamata a **SQLBindCol**, **SQLBindParameter**, o **SQLSetDescField**, i campi seguenti vengono impostati sui valori predefiniti seguenti, come illustrato nella tabella seguente. I valori dei campi rimanenti dello stesso record sono definiti.  
  
|Valore di SQL_DESC_TYPE|Gli altri campi impostati in modo implicito|  
|------------------------------|---------------------------------|  
|SQL_CHAR, SQL_VARCHAR, SQL_C_CHAR, SQL_C_VARCHAR|SQL_DESC_LENGTH è impostato su 1. SQL_DESC_PRECISION è impostato su 0.|  
|SQL_DATETIME|Quando SQL_DESC_DATETIME_INTERVAL_CODE è impostata su SQL_CODE_DATE o SQL_CODE_TIME, SQL_DESC_PRECISION è impostato su 0. Quando è impostata su SQL_DESC_TIMESTAMP, SQL_DESC_PRECISION è impostata su 6.|  
|SQL_DECIMAL, SQL_NUMERIC, SQL_C_NUMERIC|SQL_DESC_SCALE è impostato su 0. SQL_DESC_PRECISION è impostato per la precisione definita dall'implementazione per il tipo di dati corrispondente.<br /><br /> Vedere [SQL a c: Numerico](../../../odbc/reference/appendixes/sql-to-c-numeric.md) per informazioni su come associare manualmente un valore SQL_C_NUMERIC.|  
|SQL_FLOAT, SQL_C_FLOAT|SQL_DESC_PRECISION è impostato per la precisione definita dall'implementazione predefinita per SQL_FLOAT.|  
|SQL_INTERVAL|Quando SQL_DESC_DATETIME_INTERVAL_CODE è impostata su un tipo di dati di intervallo, SQL_DESC_DATETIME_INTERVAL_PRECISION è impostato su 2 (la precisione iniziale intervallo predefinita). Quando l'intervallo ha un componente di secondi, SQL_DESC_PRECISION è impostata su 6 (precisione secondi intervallo predefinito).|  
  
 Quando un'applicazione chiama **SQLSetDescField** per impostare i campi di un descrittore anziché chiamando **SQLSetDescRec**, l'applicazione prima di tutto necessario dichiarare il tipo di dati. In questo caso, gli altri campi indicati nella tabella precedente sono impostati in modo implicito. Se uno dei valori in modo implicito set è inaccettabile, l'applicazione può quindi chiamare **SQLSetDescField** oppure **SQLSetDescRec** impostare in modo esplicito il valore accettabile.  
  
 **Descrizione SQL_DESC_TYPE_NAME [descrittori di implementazione]**  
 Questo SQLCHAR di sola lettura * campi di record contiene il nome del tipo dipende dall'origine dati (ad esempio, "CHAR", "VARCHAR" e così via). Se il nome del tipo di dati è sconosciuto, questa variabile contiene una stringa vuota.  
  
 **SQL_DESC_UNNAMED [descrittori di implementazione]**  
 Questo campo SQLSMALLINT di record in un descrittore delle righe è impostato dal driver SQL_NAMED o SQL_UNNAMED quando si imposta il campo SQL_DESC_NAME. Se il campo SQL_DESC_NAME contiene un alias di colonna o se non si applica l'alias di colonna, il driver imposta il campo SQL_DESC_UNNAMED su SQL_NAMED. Se un'applicazione imposta il campo SQL_DESC_NAME di un IPD per un nome di parametro o un alias, il driver Imposta campo dell'IPD SQL_DESC_UNNAMED su SQL_NAMED. Se è presente alcun nome di colonna o un alias di colonna, il driver imposta il campo SQL_DESC_UNNAMED SQL_UNNAMED.  
  
 Un'applicazione può impostare il campo SQL_DESC_UNNAMED di un IPD per SQL_UNNAMED. Un driver restituisce SQLSTATE HY091 (identificatore del campo del descrittore non valido) se un'applicazione tenta di impostare campo di un IPD SQL_DESC_UNNAMED su SQL_NAMED. Il campo SQL_DESC_UNNAMED di un'implementazione è di sola lettura. SQLSTATE HY091 (identificatore del campo del descrittore non valido) verrà restituito se un'applicazione tenta di impostarlo.  
  
 **SQL_DESC_UNSIGNED [descrittori di implementazione]**  
 Questo campo di record SQLSMALLINT sola lettura è impostato su SQL_TRUE se il tipo di colonna è senza segno o non numerico o SQL_FALSE se il tipo di colonna è firmato.  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 Questo campo di record SQLSMALLINT di sola lettura è impostato su uno dei valori seguenti:  
  
-   SQL_ATTR_READ_ONLY se il set di risultati colonna è di sola lettura.  
  
-   SQL_ATTR_WRITE se il set di risultati colonna è di lettura / scrittura.  
  
-   SQL_ATTR_READWRITE_UNKNOWN se non è noto se il set di risultati colonna è aggiornabile o meno.  
  
 SQL_DESC_UPDATABLE descrive quanto concerne l'aggiornabilità della colonna nel set di risultati, non la colonna nella tabella di base. L'aggiornabilità della colonna nella tabella di base su cui si basa questa colonna del set di risultati potrebbe essere diverso dal valore in questo campo. Se una colonna è aggiornabile può basarsi sul tipo di dati, i privilegi utente e la definizione di se stesso set di risultati. Se non è chiaro se una colonna è aggiornabile, SQL_ATTR_READWRITE_UNKNOWN devono essere restituiti.  
  
## <a name="consistency-checks"></a>Verifiche di coerenza  
 Verifica di coerenza viene eseguita automaticamente dal driver ogni volta che un'applicazione passa un valore per il campo SQL_DESC_DATA_PTR del ARD, APD o IPD. Se non è coerente con gli altri campi, uno dei campi **SQLSetDescField** restituiranno SQLSTATE HY021 (informazioni sul descrittore inconsistenti). Per altre informazioni, vedere "Verifica coerenza" nella [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di una colonna|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Un parametro di associazione|[Funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Recupero di un campo di descrizione|[Funzione SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Recupero di più campi di descrizione|[Funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|L'impostazione di più campi di descrizione|[Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Riferimento API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)
