---
title: Funzione SQLSetDescField . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 122d4b26d1d75811d4a8e252378ce8f81ca2c66b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299551"
---
# <a name="sqlsetdescfield-function"></a>Funzione SQLSetDescField

**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLSetDescField** imposta il valore di un singolo campo di un record descrittore.  
  
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
 [Ingresso] Handle del descrittore.  
  
 *RecNumber*  
 [Ingresso] Indica il record del descrittore contenente il campo che l'applicazione desidera impostare. I record del descrittore sono numerati da 0, con il numero di record 0 come record del segnalibro. L'argomento *RecNumber* viene ignorato per i campi di intestazione.  
  
 *FieldIdentifier*  
 [Ingresso] Indica il campo del descrittore il cui valore deve essere impostato. Per ulteriori informazioni, vedere *"Argomento FieldIdentifier"* nella sezione "Commenti".  
  
 *ValuePtr*  
 [Ingresso] Puntatore a un buffer contenente le informazioni sul descrittore o a un valore intero. Il tipo di dati dipende dal valore di *FieldIdentifier*. Se *ValuePtr* è un valore intero, può essere considerato come 8 byte (SQLLEN), 4 byte (SQLINTEGER) o 2 byte (SQLSMALLINT), a seconda del valore dell'argomento *FieldIdentifier.*  
  
 *BufferLength*  
 [Ingresso] Se *FieldIdentifier* è un campo definito da ODBC e *ValuePtr* punta a una stringa di caratteri o a un buffer binario, questo argomento deve essere la lunghezza di*ValuePtr*. Per i dati di stringa di caratteri, questo argomento deve contenere il numero di byte nella stringa.  
  
 Se *FieldIdentifier* è un campo definito da ODBC e *ValuePtr* è un numero intero, *BufferLength* viene ignorato.  
  
 Se *FieldIdentifier* è un campo definito dal driver, l'applicazione indica la natura del campo in Gestione Driver impostando il *BufferLength* argomento. *BufferLength* può avere i seguenti valori:  
  
-   Se *ValuePtr* è un puntatore a una stringa di caratteri, *quindi BufferLength* è la lunghezza della stringa o SQL_NTS.  
  
-   Se *ValuePtr* è un puntatore a un buffer binario, l'applicazione inserisce il risultato della macro SQL_LEN_BINARY_ATTR(*length*) in *BufferLength*. In questo modo un valore negativo in *BufferLength*.  
  
-   Se *ValuePtr* è un puntatore a un valore diverso da una stringa di caratteri o una stringa binaria, *quindi BufferLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se *ValuePtr* contiene un valore a lunghezza fissa, *BufferLength* è SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_IS_USMALLINT, a seconda dei casi.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSetDescField** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_DESC e un *handle* di *DescriptorHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLSetDescField** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S02 (in questo stato di|Valore dell'opzione modificato|Il driver non supportava il valore specificato in * \*ValuePtr* (se *ValuePtr* era un puntatore) o il valore in *ValuePtr* (se *ValuePtr* era un valore integer) o * \*ValuePtr* non era valido a causa delle condizioni di lavoro di implementazione, pertanto il driver ha sostituito un valore simile. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07009|Indice descrittore non valido|L'argomento *FieldIdentifier* è un campo di record, l'argomento *RecNumber* era 0 e l'argomento *DescriptorHandle* fa riferimento a un handle IPD.<br /><br /> L'argomento *RecNumber* era minore di 0 e l'argomento *DescriptorHandle* fa riferimento a un ARD o a un APD.<br /><br /> L'argomento *RecNumber* è maggiore del numero massimo di colonne o parametri che l'origine dati può supportare e l'argomento *DescriptorHandle* fa riferimento a un APD o ARD.<br /><br /> (DM) l'argomento *FieldIdentifier* è stato SQL_DESC_COUNT e * \*l'argomento ValuePtr* è minore di 0.<br /><br /> L'argomento *RecNumber* è uguale a 0 e l'argomento *DescriptorHandle* fa riferimento a un APD allocato in modo implicito. Questo errore non si verifica con un descrittore dell'applicazione allocato in modo esplicito, perché non è noto se un descrittore di applicazione allocato in modo esplicito sia un APD o ARD fino all'ora di esecuzione.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|22001|Dati stringa troncati a destra|L'argomento *FieldIdentifier* è stato SQL_DESC_NAME e l'argomento *BufferLength* è un valore maggiore di SQL_MAX_IDENTIFIER_LEN.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) *il DescriptorHandle* è stato associato a un *StatementHandle* per il quale è stata chiamata una funzione in esecuzione asincrona (non questa) ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per il *StatementHandle* a cui *l'oggetto DescriptorHandle* è stato associato e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *DescriptorHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLSetDescField.This** asynchronous function was still executing when the SQLSetDescField function was called.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per uno degli handle di istruzione associati a *DescriptorHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY016 (informazioni in inglese)|Impossibile modificare un descrittore di riga di implementazione|L'argomento *DescriptorHandle* è stato associato a un IRD e l'argomento *FieldIdentifier* non è stato SQL_DESC_ARRAY_STATUS_PTR o SQL_DESC_ROWS_PROCESSED_PTR.|  
|I021|Informazioni sul descrittore incoerenti|I campi SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE non formano un tipo SQL ODBC valido o un tipo SQL specifico del driver valido (per IPD) o un tipo ODBC C valido (per AAD o ARD).<br /><br /> Le informazioni sul descrittore controllate durante una verifica di coerenza non erano coerenti. Vedere "Controllo di coerenza" in **SQLSetDescRec**.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) * \*ValuePtr* è una stringa di caratteri e *BufferLength* è minore di zero, ma non è uguale a SQL_NTS.<br /><br /> (DM) il driver era un driver *.x* ODBC 2, il descrittore era un ARD, il *ColumnNumber* argomento è stato impostato su 0 e il valore specificato per l'argomento *BufferLength* non è uguale a 4.|  
|I091|Identificatore campo descrittore non valido|Il valore specificato per l'argomento *FieldIdentifier* non è un campo definito da ODBC e non è un valore definito dall'implementazione.<br /><br /> L'argomento *FieldIdentifier* non è valido per l'argomento *DescriptorHandle.*<br /><br /> L'argomento *FieldIdentifier* era un campo di sola lettura definito da ODBC.|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo/opzione non valido|Il valore in * \*ValuePtr* non è valido per l'argomento *FieldIdentifier.*<br /><br /> L'argomento *FieldIdentifier* è stato SQL_DESC_UNNAMED e *ValuePtr* è stato SQL_NAMED.|  
|HY105|Tipo di parametro non valido|(DM) il valore specificato per il campo SQL_DESC_PARAMETER_TYPE non è valido. (Per ulteriori informazioni, vedere la sezione *"Argomento InputOutputType"* in **SQLBindParameter**.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Novità di ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) Il driver associato a *DescriptorHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Un'applicazione può chiamare **SQLSetDescField** per impostare qualsiasi campo descrittore uno alla volta. Una chiamata a **SQLSetDescField** imposta un singolo campo in un singolo descrittore. Questa funzione può essere chiamata per impostare qualsiasi campo in qualsiasi tipo di descrittore, a condizione che il campo possa essere impostato. (Vedere la tabella più avanti in questa sezione.)  
  
> [!NOTE]  
>  Se una chiamata a **SQLSetDescField** ha esito negativo, il contenuto del record del descrittore identificato dal *RecNumber* argomento non è definito.  
  
 Altre funzioni possono essere chiamate per impostare più campi descrittore con una singola chiamata della funzione. La funzione **SQLSetDescRec** imposta una varietà di campi che influiscono sul tipo di dati e sul buffer associati a una colonna o a un parametro (i campi SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR). **SQLBindCol** o **SQLBindParameter** può essere utilizzato per creare una specifica completa per l'associazione di una colonna o parametro. Queste funzioni impostano un gruppo specifico di campi descrittore con una chiamata di funzione.  
  
 **SQLSetDescField** può essere chiamato per modificare i buffer di associazione aggiungendo un offset ai puntatori di associazione (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR o SQL_DESC_OCTET_LENGTH_PTR). In questo modo i buffer di associazione senza chiamare **SQLBindCol** o **SQLBindParameter**, che consente a un'applicazione di modificare SQL_DESC_DATA_PTR senza modificare altri campi, ad esempio SQL_DESC_DATA_TYPE.  
  
 Se un'applicazione chiama **SQLSetDescField** per impostare un campo diverso da SQL_DESC_COUNT o i campi posticipati SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR o SQL_DESC_INDICATOR_PTR, il record diventa non associato.  
  
 I campi di intestazione del descrittore vengono impostati chiamando **SQLSetDescField** con *l'identificatore FieldIdentifier*appropriato. Molti campi di intestazione sono anche attributi di istruzione, pertanto possono anche essere impostati da una chiamata a **SQLSetStmtAttr**. Ciò consente alle applicazioni di impostare un campo descrittore senza prima ottenere un handle descrittore. Quando **SQLSetDescField** viene chiamato per impostare un campo di intestazione, il *RecNumber* argomento viene ignorato.  
  
 Un *RecNumber* pari a 0 viene utilizzato per impostare i campi segnalibro.  
  
> [!NOTE]  
>  L'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS deve essere sempre impostato prima di chiamare **SQLSetDescField** per impostare i campi segnalibro. Anche se questo non è obbligatorio, è fortemente raccomandato.  
  
## <a name="sequence-of-setting-descriptor-fields"></a>Sequenza di impostazione dei campi descrittore  
 Quando si impostano i campi descrittore chiamando **SQLSetDescField**, l'applicazione deve seguire una sequenza specifica:  
  
1.  L'applicazione deve prima impostare il campo SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE o SQL_DESC_DATETIME_INTERVAL_CODE.  
  
2.  Dopo aver impostato uno di questi campi, l'applicazione può impostare un attributo di un tipo di dati e il driver imposta i campi dell'attributo del tipo di dati sui valori predefiniti appropriati per il tipo di dati. L'impostazione predefinita automatica dei campi degli attributi di tipo garantisce che il descrittore sia sempre pronto per l'uso dopo che l'applicazione ha specificato un tipo di dati. Se l'applicazione imposta in modo esplicito un attributo del tipo di dati, esegue l'override dell'attributo predefinito.  
  
3.  Dopo aver impostato uno dei campi elencati nel passaggio 1 e aver impostato gli attributi del tipo di dati, l'applicazione può impostare SQL_DESC_DATA_PTR. Ciò richiede una verifica di coerenza dei campi descrittore. Se l'applicazione modifica il tipo di dati o gli attributi dopo aver impostato il campo SQL_DESC_DATA_PTR, il driver imposta SQL_DESC_DATA_PTR su un puntatore null, annullando l'associazione del record. In questo modo l'applicazione per completare i passaggi corretti in sequenza, prima che il record del descrittore sia utilizzabile.  
  
## <a name="initialization-of-descriptor-fields"></a>Inizializzazione dei campi di descrizione  
 Quando viene allocato un descrittore, i campi nel descrittore possono essere inizializzati su un valore predefinito, possono essere inizializzati senza un valore predefinito o non definiti per il tipo di descrittore. Le tabelle seguenti indicano l'inizializzazione di ogni campo per ogni tipo di descrittore, con "D" che indica che il campo viene inizializzato con un valore predefinito e "ND" che indica che il campo viene inizializzato senza un valore predefinito. Se viene visualizzato un numero, il valore predefinito del campo è tale numero. Le tabelle indicano anche se un campo è di lettura/scrittura (R/W) o di sola lettura (R).  
  
 I campi di un IRD hanno un valore predefinito solo dopo che l'istruzione è stata preparata o eseguita e l'IRD è stato popolato, non quando l'handle o il descrittore dell'istruzione è stato allocato. Fino a quando l'IRD non è stato popolato, qualsiasi tentativo di ottenere l'accesso a un campo di un IRD restituirà un errore.  
  
 Alcuni campi descrittore sono definiti per uno o più campi descrittore, ma non per tutti, dei tipi di descrittori (ARD e ID e APP e IPD). Quando un campo non è definito per un tipo di descrittore, non è necessario per nessuna delle funzioni che utilizzano tale descrittore.  
  
 I campi accessibili da **SQLGetDescField** non possono essere necessariamente impostati da **SQLSetDescField**. I campi che possono essere impostati da **SQLSetDescField** sono elencati nelle tabelle seguenti.  
  
 L'inizializzazione dei campi di intestazione è descritta nella tabella seguente.  
  
|Nome campo intestazione|Type|L/S|Predefinito|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD: R APD: R IRD: R IPD: R|ARD: SQL_DESC_ALLOC_AUTO implicito o SQL_DESC_ALLOC_USER per esplicito<br /><br /> APD: SQL_DESC_ALLOC_AUTO implicito o SQL_DESC_ALLOC_USER per esplicito<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN (informazioni in lingua inglese)|ARD: R/W APD: R/W IRD: IPD inutilizzato: Inutilizzato|ARD:[1] APD:[1] IRD: IPD inutilizzato: Inutilizzato|  
|SQL_DESC_ARRAY_STATUS_PTR|Istruzione SQLUSMALLINT (informazioni in lingua inglese)|ARD: R/W APD: R/W IRD: R/W IPD: R/W|ARD: Null ptr APD: IRD ptr Null: Null ptr IPD: Null ptr|  
|SQL_DESC_BIND_OFFSET_PTR|Istruzione SQLLEN|ARD: R/W APD: R/W IRD: IPD inutilizzato: Inutilizzato|ARD: Null ptr APD: IRD ptr null: IPD inutilizzato: Inutilizzato|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD: R/W APD: R/W IRD: IPD inutilizzato: Inutilizzato|ARD: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD: Inutilizzato<br /><br /> IPD: Inutilizzato|  
|SQL_DESC_COUNT|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: 0 APD: 0 IRD: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN|ARD: APD inutilizzato: IRD inutilizzato: R/W IPD: R/W|ARD: APD inutilizzato: IRD inutilizzato: NULL ptr IPD: Null ptr|  
  
 [1] Questi campi sono definiti solo quando l'IPD viene popolato automaticamente dal driver. In caso contrario, non sono definiti. Se un'applicazione tenta di impostare questi campi, verrà restituito SQLSTATE HY091 (Identificatore campo descrittore non valido).  
  
 L'inizializzazione dei campi di record è come illustrato nella tabella seguente.  
  
|Nome campo record|Type|L/S|Predefinito|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD: APD inutilizzato: IRD inutilizzato: R IPD: Inutilizzato|ARD: APD inutilizzato: IRD inutilizzato: D IPD: Inutilizzato|  
|SQL_DESC_BASE_COLUMN_NAME|Proprietà SQLCHAR .|ARD: APD inutilizzato: IRD inutilizzato: R IPD: Inutilizzato|ARD: APD inutilizzato: IRD inutilizzato: D IPD: Inutilizzato|  
|SQL_DESC_BASE_TABLE_NAME|Proprietà SQLCHAR .|ARD: APD inutilizzato: IRD inutilizzato: R IPD: Inutilizzato|ARD: APD inutilizzato: IRD inutilizzato: D IPD: Inutilizzato|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD: APD inutilizzato: IRD inutilizzato: R IPD: R|ARD: APD inutilizzato: IRD inutilizzato: D IPD: D[1]|  
|SQL_DESC_CATALOG_NAME|Proprietà SQLCHAR .|ARD: APD inutilizzato: IRD inutilizzato: R IPD: Inutilizzato|ARD: APD inutilizzato: IRD inutilizzato: D IPD: Inutilizzato|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: SQL_C_ DEFAULT APD: SQL_C_ IRD DEFAULT: D IPD: ND|  
|SQL_DESC_DATA_PTR|PUNTATORE SQL|ARD: R/W APD: R/W IRD: IPD inutilizzato: Inutilizzato|ARD: Null ptr APD: IRD ptr null: IPD inutilizzato: inutilizzato[2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN (informazioni in lingua inglese)|ARD: APD inutilizzato: IRD inutilizzato: R IPD: Inutilizzato|ARD: APD inutilizzato: IRD inutilizzato: D IPD: Inutilizzato|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD: APD inutilizzato: IRD inutilizzato: R IPD: R|ARD: APD inutilizzato: IRD inutilizzato: D IPD: D[1]|  
|SQL_DESC_INDICATOR_PTR|Proprietà SQLLEN .|ARD: R/W APD: R/W IRD: IPD inutilizzato: Inutilizzato|ARD: Null ptr APD: IRD ptr null: IPD inutilizzato: Inutilizzato|  
|SQL_DESC_LABEL|Proprietà SQLCHAR .|ARD: APD inutilizzato: IRD inutilizzato: R IPD: Inutilizzato|ARD: APD inutilizzato: IRD inutilizzato: D IPD: Inutilizzato|  
|SQL_DESC_LENGTH|SQLULEN (informazioni in lingua inglese)|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|Proprietà SQLCHAR .|ARD: APD inutilizzato: IRD inutilizzato: R IPD: Inutilizzato|ARD: APD inutilizzato: IRD inutilizzato: D IPD: Inutilizzato|  
|SQL_DESC_LITERAL_SUFFIX|Proprietà SQLCHAR .|ARD: APD inutilizzato: IRD inutilizzato: R IPD: Inutilizzato|ARD: APD inutilizzato: IRD inutilizzato: D IPD: Inutilizzato|  
|SQL_DESC_LOCAL_TYPE_NAME|Proprietà SQLCHAR .|ARD: APD inutilizzato: IRD inutilizzato: R IPD: R|ARD: APD inutilizzato: IRD inutilizzato: D IPD: D[1]|  
|SQL_DESC_NAME|Proprietà SQLCHAR .|ARD: APD inutilizzato: IRD inutilizzato: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD: APD inutilizzato: IRD inutilizzato: R IPD: R|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN (informazioni in lingua inglese)|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|Proprietà SQLLEN .|ARD: R/W APD: R/W IRD: IPD inutilizzato: Inutilizzato|ARD: Null ptr APD: IRD ptr null: IPD inutilizzato: Inutilizzato|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD: APD inutilizzato: IRD inutilizzato: IPD inutilizzato: R/W|ARD: APD inutilizzato: IRD inutilizzato: IPD inutilizzato: D-SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD: Inutilizzato<br /><br /> APD: Inutilizzato<br /><br /> IRD: R<br /><br /> IPD: R|ARD: Inutilizzato<br /><br /> APD: Inutilizzato<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|Proprietà SQLCHAR .|ARD: APD inutilizzato: IRD inutilizzato: R IPD: Inutilizzato|ARD: APD inutilizzato: IRD inutilizzato: D IPD: Inutilizzato|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD: APD inutilizzato: IRD inutilizzato: R IPD: Inutilizzato|ARD: APD inutilizzato: IRD inutilizzato: D IPD: Inutilizzato|  
|SQL_DESC_TABLE_NAME|Proprietà SQLCHAR .|ARD: APD inutilizzato: IRD inutilizzato: R IPD: Inutilizzato|ARD: APD inutilizzato: IRD inutilizzato: D IPD: Inutilizzato|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
|SQL_DESC_TYPE_NAME|Proprietà SQLCHAR .|ARD: APD inutilizzato: IRD inutilizzato: R IPD: R|ARD: APD inutilizzato: IRD inutilizzato: D IPD: D[1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD: APD inutilizzato: IRD inutilizzato: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD: APD inutilizzato: IRD inutilizzato: R IPD: R|ARD: APD inutilizzato: IRD inutilizzato: D IPD: D[1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD: APD inutilizzato: IRD inutilizzato: R IPD: Inutilizzato|ARD: APD inutilizzato: IRD inutilizzato: D IPD: Inutilizzato|  
  
 [1] Questi campi sono definiti solo quando l'IPD viene popolato automaticamente dal driver. In caso contrario, non sono definiti. Se un'applicazione tenta di impostare questi campi, verrà restituito SQLSTATE HY091 (Identificatore campo descrittore non valido).  
  
 [2] Il campo SQL_DESC_DATA_PTR nell'IPD può essere impostato per forzare una verifica di coerenza. In una chiamata successiva a **SQLGetDescField** o **SQLGetDescRec**, il driver non è necessario restituire il valore su cui è stato impostato SQL_DESC_DATA_PTR.  
  
## <a name="fieldidentifier-argument"></a>Argomento FieldIdentifier  
 Il *FieldIdentifier* argomento indica il campo del descrittore da impostare. Un descrittore contiene l'intestazione del *descrittore,* costituita dai campi di intestazione descritti nella sezione successiva, "Campi intestazione" e da zero o più *record di descrittori,* costituiti dai campi di record descritti nella sezione che segue la sezione "Campi di intestazione".  
  
## <a name="header-fields"></a>Campi intestazione  
 Ogni descrittore ha un'intestazione costituita dai seguenti campi:  
  
 **SQL_DESC_ALLOC_TYPE [Tutti]**  
 Questo campo di intestazione SQLSMALLINT di sola lettura specifica se il descrittore è stato allocato automaticamente dal driver o in modo esplicito dall'applicazione. L'applicazione può ottenere, ma non modificare, questo campo. Il campo viene impostato su SQL_DESC_ALLOC_AUTO dal driver se il descrittore è stato allocato automaticamente dal driver. Viene impostato su SQL_DESC_ALLOC_USER dal driver se il descrittore è stato allocato in modo esplicito dall'applicazione.  
  
 **SQL_DESC_ARRAY_SIZE [Descrittori di applicazione]**  
 In ARD, questo campo di intestazione SQLULEN specifica il numero di righe nel set di righe. Questo è il numero di righe che devono essere restituite da una chiamata a **SQLFetch** o **SQLFetchScroll** o da utilizzare da una chiamata a **SQLBulkOperations** o **SQLSetPos**.  
  
 Negli APD, questo campo di intestazione SQLULEN specifica il numero di valori per ogni parametro.  
  
 Il valore predefinito di questo campo è 1. Se SQL_DESC_ARRAY_SIZE è maggiore di 1, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR di APD o ARD puntano a matrici. La cardinalità di ogni matrice è uguale al valore di questo campo.  
  
 Questo campo nell'ARD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_ROW_ARRAY_SIZE. Questo campo nell'oggetto APD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_PARAMSET_SIZE.  
  
 **SQL_DESC_ARRAY_STATUS_PTR [Tutti]**  
 Per ogni tipo di descrittore, questo campo di intestazione SQLUSMALLINT - punta a una matrice di valori SQLUSMALLINT. Questi array sono denominati come segue: matrice di stato della riga (IRD), matrice di stato del parametro (IPD), matrice di operazioni di riga (ARD) e matrice di operazioni di parametro (APD).  
  
 In IRD questo campo di intestazione punta a una matrice di stato di riga contenente i valori di stato dopo una chiamata a **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**. La matrice contiene un numero di elementi quanti sono le righe nel set di righe. L'applicazione deve allocare una matrice di SQLUSMALLINT e impostare questo campo in modo che punti alla matrice. Il campo è impostato su un puntatore null per impostazione predefinita. Il driver popolerà la matrice, a meno che il campo SQL_DESC_ARRAY_STATUS_PTR non sia impostato su un puntatore null, nel qual caso non vengono generati valori di stato e la matrice non viene popolata.  
  
> [!CAUTION]  
>  Il comportamento del driver non è definito se l'applicazione imposta gli elementi della matrice di stato della riga a cui punta il campo SQL_DESC_ARRAY_STATUS_PTR dell'IRD.  
  
 La matrice viene inizialmente popolata da una chiamata a **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**. Se la chiamata non ha restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il contenuto della matrice a cui fa riferimento questo campo non è definito. Gli elementi nella matrice possono contenere i seguenti valori:  
  
-   SQL_ROW_SUCCESS: la riga è stata recuperata correttamente e non è stata modificata dall'ultimo recupero.  
  
-   SQL_ROW_SUCCESS_WITH_INFO: la riga è stata recuperata correttamente e non è stata modificata dall'ultimo recupero. Tuttavia, è stato restituito un avviso relativo alla riga.  
  
-   SQL_ROW_ERROR: si è verificato un errore durante il recupero della riga.  
  
-   SQL_ROW_UPDATED: la riga è stata recuperata correttamente ed è stata aggiornata dall'ultimo recupero. Se la riga viene recuperata nuovamente, il relativo stato è SQL_ROW_SUCCESS.  
  
-   SQL_ROW_DELETED: la riga è stata eliminata dall'ultimo recupero.  
  
-   SQL_ROW_ADDED: la riga è stata inserita da **SQLBulkOperations**. Se la riga viene recuperata nuovamente, il relativo stato è SQL_ROW_SUCCESS.  
  
-   SQL_ROW_NOROW: il set di righe si sovrapponeva alla fine del set di risultati e non veniva restituita alcuna riga corrispondente a questo elemento della matrice di stato della riga.  
  
 Questo campo in IRD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_ROW_STATUS_PTR.  
  
 Il campo SQL_DESC_ARRAY_STATUS_PTR dell'IRD è valido solo dopo SQL_SUCCESS o SQL_SUCCESS_WITH_INFO è stato restituito. Se il codice restituito non è uno di questi, la posizione a cui fa riferimento SQL_DESC_ROWS_PROCESSED_PTR non è definita.  
  
 Nell'IPD questo campo di intestazione punta a una matrice di stato dei parametri contenente informazioni sullo stato per ogni set di valori di parametro dopo una chiamata a **SQLExecute** o **SQLExecDirect**. Se la chiamata a **SQLExecute** o **SQLExecDirect** non ha restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il contenuto della matrice a cui punta questo campo non è definito. L'applicazione deve allocare una matrice di SQLUSMALLINT e impostare questo campo in modo che punti alla matrice. Il driver popolerà la matrice, a meno che il campo SQL_DESC_ARRAY_STATUS_PTR non sia impostato su un puntatore null, nel qual caso non vengono generati valori di stato e la matrice non viene popolata. Gli elementi nella matrice possono contenere i seguenti valori:  
  
-   SQL_PARAM_SUCCESS: l'istruzione SQL è stata eseguita correttamente per questo set di parametri.  
  
-   SQL_PARAM_SUCCESS_WITH_INFO: l'istruzione SQL è stata eseguita correttamente per questo set di parametri. tuttavia, le informazioni di avviso sono disponibili nella struttura dei dati di diagnostica.  
  
-   SQL_PARAM_ERROR: si è verificato un errore durante l'elaborazione di questo set di parametri. Ulteriori informazioni sull'errore sono disponibili nella struttura dei dati di diagnostica.  
  
-   SQL_PARAM_UNUSED: questo set di parametri era inutilizzato, probabilmente a causa del fatto che un set di parametri precedente ha causato un errore che ha interrotto l'ulteriore elaborazione o perché SQL_PARAM_IGNORE è stato impostato per quel set di parametri nella matrice specificata dal campo SQL_DESC_ARRAY_STATUS_PTR dell'APD.  
  
-   SQL_PARAM_DIAG_UNAVAILABLE: le informazioni di diagnostica non sono disponibili. Un esempio è quando il driver considera le matrici di parametri come un'unità monolitica e pertanto non genera questo livello di informazioni sull'errore.  
  
 Questo campo nell'IPD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_PARAM_STATUS_PTR.  
  
 Nell'ARD, questo campo di intestazione punta a una matrice di valori di operazione di riga che può essere impostata dall'applicazione per indicare se questa riga deve essere ignorata per le operazioni **SQLSetPos.** Gli elementi nella matrice possono contenere i seguenti valori:  
  
-   SQL_ROW_PROCEED: la riga viene inclusa nell'operazione in blocco utilizzando **SQLSetPos**. Questa impostazione non garantisce che l'operazione verrà eseguita sulla riga. Se la riga ha lo stato SQL_ROW_ERROR nella matrice di stato della riga IRD, il driver potrebbe non essere in grado di eseguire l'operazione nella riga.)  
  
-   SQL_ROW_IGNORE: la riga viene esclusa dall'operazione in blocco utilizzando **SQLSetPos**.  
  
 Se non sono impostati elementi della matrice, tutte le righe vengono incluse nell'operazione in blocco. Se il valore nel campo SQL_DESC_ARRAY_STATUS_PTR di ARD è un puntatore null, tutte le righe vengono incluse nell'operazione in blocco; l'interpretazione è la stessa come se il puntatore puntasse a una matrice valida e tutti gli elementi della matrice sono stati SQL_ROW_PROCEED. Se un elemento nella matrice è impostato su SQL_ROW_IGNORE, il valore nella matrice di stato della riga per la riga ignorata non viene modificato.  
  
 Questo campo nell'ARD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_ROW_OPERATION_PTR.  
  
 Nell'Oggetto APD, questo campo di intestazione punta a una matrice di valori di operazione di parametro che può essere impostata dall'applicazione per indicare se questo set di parametri deve essere ignorato quando viene chiamato **SQLExecute** o **SQLExecDirect.** Gli elementi nella matrice possono contenere i seguenti valori:  
  
-   SQL_PARAM_PROCEED: il set di parametri è incluso nella chiamata **SQLExecute** o **SQLExecDirect.**  
  
-   SQL_PARAM_IGNORE: il set di parametri è escluso dalla chiamata **SQLExecute** o **SQLExecDirect.**  
  
 Se non sono impostati elementi della matrice, tutti i set di parametri nella matrice vengono utilizzati nelle chiamate **SQLExecute** o **SQLExecDirect.** Se il valore nel campo SQL_DESC_ARRAY_STATUS_PTR di APD è un puntatore null, vengono utilizzati tutti i set di parametri; l'interpretazione è la stessa come se il puntatore puntasse a una matrice valida e tutti gli elementi della matrice sono stati SQL_PARAM_PROCEED.  
  
 Questo campo nell'oggetto APD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_PARAM_OPERATION_PTR.  
  
 **SQL_DESC_BIND_OFFSET_PTR [descrittori di applicazione]**  
 Questo campo di intestazione SQLLEN: punta all'offset dell'associazione. È impostato su un puntatore null per impostazione predefinita. Se questo campo non è un puntatore null, il driver dereferenzia il puntatore e aggiunge il valore dereferenziato a ognuno dei campi posticipati che dispone di un valore non null nel record del descrittore (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR) in fase di recupero e utilizza i nuovi valori del puntatore durante l'associazione.  
  
 L'offset di associazione viene sempre aggiunto direttamente ai valori nei campi SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR. Se l'offset viene modificato in un valore diverso, il nuovo valore viene comunque aggiunto direttamente al valore in ogni campo del descrittore. Il nuovo offset non viene aggiunto al valore del campo più qualsiasi offset precedente.  
  
 Questo campo è un *campo posticipato*: non viene utilizzato al momento dell'impostazione, ma viene utilizzato in un secondo momento dal driver quando è necessario determinare gli indirizzi per i buffer di dati.  
  
 Questo campo nell'ARD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_ROW_BIND_OFFSET_PTR. Questo campo nell'ARD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_PARAM_BIND_OFFSET_PTR.  
  
 Per ulteriori informazioni, vedere la descrizione dell'associazione per riga in [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) e [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 **SQL_DESC_BIND_TYPE [descrittori di applicazioni]**  
 Questo campo di intestazione SQLUINTEGER imposta l'orientamento di associazione da utilizzare per l'associazione di colonne o parametri.  
  
 In ARDs, questo campo specifica l'orientamento di associazione quando **SQLFetchScroll** o **SQLFetch** viene chiamato sull'handle di istruzione associato.  
  
 Per selezionare l'associazione per colonna per le colonne, questo campo è impostato su SQL_BIND_BY_COLUMN (impostazione predefinita).  
  
 Questo campo nell'ARD può essere impostato anche chiamando **SQLSetStmtAttr** con il SQL_ATTR_ROW_BIND_TYPE *Attribute*.  
  
 Negli AAD questo campo specifica l'orientamento dell'associazione da utilizzare per i parametri dinamici.  
  
 Per selezionare l'associazione per colonna per i parametri, questo campo è impostato su SQL_BIND_BY_COLUMN (impostazione predefinita).  
  
 Questo campo nell'oggetto APD può essere impostato anche chiamando **SQLSetStmtAttr** con *l'attributo*SQL_ATTR_PARAM_BIND_TYPE .  
  
 **SQL_DESC_COUNT [Tutti]**  
 Questo campo di intestazione SQLSMALLINT specifica l'indice in base 1 del record con il numero più alto che contiene dati. Quando il driver imposta la struttura dei dati per il descrittore, deve anche impostare il campo SQL_DESC_COUNT per mostrare quanti record sono significativi. Quando un'applicazione alloca un'istanza di questa struttura di dati, non è necessario specificare il numero di record per cui riservare spazio. Come l'applicazione specifica il contenuto dei record, il driver esegue qualsiasi azione necessaria per garantire che l'handle descrittore fa riferimento a una struttura di dati di dimensioni adeguate.  
  
 SQL_DESC_COUNT non è un conteggio di tutte le colonne di dati associate (se il campo è in un ARD) o di tutti i parametri associati (se il campo si trova in un aPD), ma il numero del record con il numero più alto. Se la colonna o il parametro con il numero più alto non è associato, SQL_DESC_COUNT viene modificato nel numero della colonna o del parametro con il numero più alto successivo. Se una colonna o un parametro con un numero inferiore al numero della colonna con il numero più alto è non associata (chiamando **SQLBindCol** con il *TargetValuePtr* argomento impostato su un puntatore null o **SQLBindParameter** con il *ParameterValuePtr* argomento impostato su un puntatore null), SQL_DESC_COUNT non viene modificato. Se colonne o parametri aggiuntivi sono associati a numeri maggiori del record con il numero più alto che contiene dati, il driver aumenta automaticamente il valore nel campo SQL_DESC_COUNT. Se tutte le colonne non sono associate chiamando **SQLFreeStmt** con l'opzione SQL_UNBIND, i campi SQL_DESC_COUNT in ARD e IRD sono impostati su 0. Se **SQLFreeStmt** viene chiamato con l'opzione SQL_RESET_PARAMS, i campi SQL_DESC_COUNT in APD e IPD sono impostati su 0.  
  
 Il valore in SQL_DESC_COUNT può essere impostato in modo esplicito da un'applicazione chiamando **SQLSetDescField**. Se il valore in SQL_DESC_COUNT viene ridotto in modo esplicito, tutti i record con numeri maggiori del nuovo valore in SQL_DESC_COUNT vengono rimossi in modo efficace. Se il valore in SQL_DESC_COUNT è impostato in modo esplicito su 0 e il campo è in un ARD, vengono rilasciati tutti i buffer di dati ad eccezione di una colonna segnalibro associato.  
  
 Il numero di record in questo campo di un ARD non include una colonna segnalibro associato. L'unico modo per annullare l'associazione di una colonna segnalibro consiste nell'impostare il campo SQL_DESC_DATA_PTR su un puntatore null.  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [Descrittori di implementazione]**  
 In un IRD, questo \* campo di intestazione SQLULEN punta a un buffer contenente il numero di righe recuperate dopo una chiamata a **SQLFetch** o **SQLFetchScroll**o il numero di righe interessate in un'operazione bulk eseguita da una chiamata a **SQLBulkOperations** o **SQLSetPos**, incluse le righe di errore.  
  
 In un'IPD, questo campo di intestazione SQLUINTEGER punta a un buffer contenente il numero di set di parametri che sono stati elaborati, inclusi i set di errori. Se si tratta di un puntatore null, non verrà restituito alcun numero.  
  
 SQL_DESC_ROWS_PROCESSED_PTR è valido solo dopo SQL_SUCCESS o SQL_SUCCESS_WITH_INFO è stata restituita dopo una chiamata a **SQLFetch** o **SQLFetchScroll** (per un campo IRD) o **SQLExecute**, **SQLExecDirect**o **SQLParamData** (per un campo IPD). Se la chiamata che riempie il buffer a cui fa riferimento questo campo non restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il contenuto del buffer non è definito, a meno che non restituisca SQL_NO_DATA, nel qual caso il valore nel buffer è impostato su 0.  
  
 Questo campo nell'ARD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_ROWS_FETCHED_PTR. Questo campo nell'oggetto APD può essere impostato anche chiamando **SQLSetStmtAttr** con l'attributo SQL_ATTR_PARAMS_PROCESSED_PTR.  
  
 Il buffer a cui fa riferimento questo campo viene allocato dall'applicazione. Si tratta di un buffer di output posticipato impostato dal driver. È impostato su un puntatore null per impostazione predefinita.  
  
## <a name="record-fields"></a>Campi record  
 Ogni descrittore contiene uno o più record costituiti da campi che definiscono i dati di colonna o i parametri dinamici, a seconda del tipo di descrittore. Ogni record è una definizione completa di una singola colonna o parametro.  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [ICAM]**  
 Questo campo di record SQLINTEGER di sola lettura contiene SQL_TRUE se la colonna è una colonna a incremento automatico o SQL_FALSE se la colonna non è una colonna a incremento automatico. Questo campo è di sola lettura, ma la colonna di incremento automatico sottostante non è necessariamente di sola lettura.  
  
 **SQL_DESC_BASE_COLUMN_NAME [ICAM]**  
 Questo campo di sola lettura SQLCHAR - record contiene il nome della colonna di base per la colonna del set di risultati. Se non esiste un nome di colonna di base (come nel caso di colonne che sono espressioni), questa variabile contiene una stringa vuota.  
  
 **SQL_DESC_BASE_TABLE_NAME [ICAM]**  
 Questo campo di sola lettura SQLCHAR - record contiene il nome della tabella di base per la colonna del set di risultati. Se un nome di tabella di base non può essere definito o non è applicabile, questa variabile contiene una stringa vuota.  
  
 **SQL_DESC_CASE_SENSITIVE [descrittori di implementazione]**  
 Questo campo di record SQLINTEGER di sola lettura contiene SQL_TRUE se la colonna o il parametro viene considerato come maiuscole/minuscole per le regole di confronto e i confronti oppure SQL_FALSE se la colonna non viene considerata come maiuscole/minuscole per le regole di confronto e i confronti o se si tratta di una colonna non di tipo carattere.  
  
 **SQL_DESC_CATALOG_NAME [ICAM]**  
 Questo campo di sola lettura SQLCHAR - record contiene il catalogo per la tabella di base che contiene la colonna. Il valore restituito dipende dal driver se la colonna è un'espressione o se la colonna fa parte di una vista. Se l'origine dati non supporta i cataloghi o non è possibile determinare il catalogo, questa variabile contiene una stringa vuota.  
  
 **SQL_DESC_CONCISE_TYPE [Tutti]**  
 Questo campo di intestazione SQLSMALLINT specifica il tipo di dati conciso per tutti i tipi di dati, inclusi i tipi di dati datetime e interval.  
  
 I valori nei campi SQL_DESC_CONCISE_TYPE, SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE sono interdipendenti. Ogni volta che uno dei campi è impostato, anche l'altro deve essere impostato. SQL_DESC_CONCISE_TYPE può essere impostata da una chiamata a **SQLBindCol** o **SQLBindParameter**o **SQLSetDescField**. SQL_DESC_TYPE possono essere impostati da una chiamata a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Se SQL_DESC_CONCISE_TYPE è impostato su un tipo di dati conciso diverso da un tipo di dati interval o datetime, il campo SQL_DESC_TYPE viene impostato sullo stesso valore e il campo SQL_DESC_DATETIME_INTERVAL_CODE è impostato su 0.  
  
 Se SQL_DESC_CONCISE_TYPE è impostato sul tipo di dati conciso datetime o interval, il campo SQL_DESC_TYPE viene impostato sul tipo dettagliato corrispondente (SQL_DATETIME o SQL_INTERVAL) e il campo SQL_DESC_DATETIME_INTERVAL_CODE viene impostato sul sottocodice appropriato.  
  
 **SQL_DESC_DATA_PTR [Descrittori di applicazioni e IPD]**  
 Questo campo di record SQLPOINTER punta a una variabile che conterrà il valore del parametro (per Gli AAD) o il valore della colonna (per gli ARD). Questo campo è un *campo posticipato*. Non viene utilizzato al momento dell'impostazione, ma viene utilizzato in un secondo momento dal driver per recuperare i dati.  
  
 La colonna specificata dal campo SQL_DESC_DATA_PTR di ARD non è associata se il *TargetValuePtr* argomento in una chiamata a **SQLBindCol** è un puntatore null o se il campo SQL_DESC_DATA_PTR nel ARD viene impostato da una chiamata a **SQLSetDescField** o **SQLSetDescRec** a un puntatore null. Altri campi non sono interessati se il campo SQL_DESC_DATA_PTR è impostato su un puntatore null.  
  
 Se la chiamata a **SQLFetch** o **SQLFetchScroll** che riempie il buffer a cui punta questo campo non ha restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il contenuto del buffer non è definito.  
  
 Ogni volta che viene impostato il campo SQL_DESC_DATA_PTR di un APD, ARD o IPD, il driver verifica che il valore nel campo SQL_DESC_TYPE contenga uno dei tipi di dati ODBC C validi o un tipo di dati specifico del driver e che tutti gli altri campi che interessano i tipi di dati siano coerenti. La richiesta di verifica della coerenza è l'unico utilizzo del campo SQL_DESC_DATA_PTR di un IPD. In particolare, se un'applicazione imposta il campo SQL_DESC_DATA_PTR di un IPD e successivamente chiama **SQLGetDescField** su questo campo, non viene necessariamente restituito il valore che aveva impostato. Per ulteriori informazioni, vedere "Controlli di coerenza" in [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [Tutti]**  
 Questo campo di record SQLSMALLINT contiene il sottocodice per il tipo di dati datetime o interval specifico quando il campo SQL_DESC_TYPE è SQL_DATETIME o SQL_INTERVAL. Ciò vale per entrambi i tipi di dati SQL e C. Il codice è costituito dal nome del tipo di dati con "CODE" sostituito da "TYPE" o "C_TYPE" (per i tipi datetime) o "CODE" sostituito da "INTERVAL" o "C_INTERVAL" (per i tipi di intervallo).  
  
 Se SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE in un descrittore dell'applicazione sono impostati su SQL_C_DEFAULT e il descrittore non è associato a un handle di istruzione, il contenuto di SQL_DESC_DATETIME_INTERVAL_CODE non è definito.  
  
 Questo campo può essere impostato per i tipi di dati datetime elencati nella tabella seguente.  
  
|Tipi datetime|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/ SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 Questo campo può essere impostato per i tipi di dati intervallo elencati nella tabella seguente.  
  
|Tipo di intervallo|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY/SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR/SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND/SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR/SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND/SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND/SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH/SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND/SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR/SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH/SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 Per ulteriori informazioni sugli intervalli di dati e su questo campo, vedere [Identificatori e descrittori dei tipi](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)di dati .  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [Tutti]**  
 Questo campo di record SQLINTEGER contiene la precisione di interlinea dell'intervallo se il campo SQL_DESC_TYPE è SQL_INTERVAL. Quando il campo SQL_DESC_DATETIME_INTERVAL_CODE è impostato su un tipo di dati intervallo, questo campo viene impostato sulla precisione di interlinea intervallo predefinita.  
  
 **SQL_DESC_DISPLAY_SIZE [ICAM]**  
 Questo campo di record SQLINTEGER di sola lettura contiene il numero massimo di caratteri necessari per visualizzare i dati della colonna.  
  
 **SQL_DESC_FIXED_PREC_SCALE [descrittori di implementazione]**  
 Questo campo di record SQLSMALLINT di sola lettura è impostato su SQL_TRUE se la colonna è una colonna numerica esatta e ha una precisione fissa e una scala diversa oppure per SQL_FALSE se la colonna non è una colonna numerica esatta con precisione e scala fissa.  
  
 **SQL_DESC_INDICATOR_PTR [descrittori di applicazione]**  
 In ARDs, questo campo di record SQLLEN - punta alla variabile indicatore. Questa variabile contiene SQL_NULL_DATA se il valore della colonna è NULL. Per gli APD, la variabile indicatore è impostata su SQL_NULL_DATA per specificare argomenti dinamici NULL. In caso contrario, la variabile è zero (a meno che i valori in SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR sono lo stesso puntatore).  
  
 Se il campo SQL_DESC_INDICATOR_PTR in un ARD è un puntatore null, al driver viene impedito di restituire informazioni sul fatto che la colonna sia NULL o meno. Se la colonna è NULL e SQL_DESC_INDICATOR_PTR è un puntatore null, SQLSTATE 22002 (variabile indicatore richiesta ma non fornita) viene restituito quando il driver tenta di popolare il buffer dopo una chiamata a **SQLFetch** o **SQLFetchScroll**. Se la chiamata a **SQLFetch** o **SQLFetchScroll** non ha restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il contenuto del buffer non è definito.  
  
 Il campo SQL_DESC_INDICATOR_PTR determina se il campo a cui punta SQL_DESC_OCTET_LENGTH_PTR è impostato. Se il valore dei dati per una colonna è NULL, il driver imposta la variabile indicatore su SQL_NULL_DATA. Il campo a cui fa riferimento SQL_DESC_OCTET_LENGTH_PTR non viene quindi impostato. Se non viene rilevato un valore NULL durante il recupero, il buffer a cui punta SQL_DESC_INDICATOR_PTR è impostato su zero e il buffer a cui punta SQL_DESC_OCTET_LENGTH_PTR è impostato sulla lunghezza dei dati.  
  
 Se il campo SQL_DESC_INDICATOR_PTR in un APD è un puntatore null, l'applicazione non può utilizzare questo record del descrittore per specificare argomenti NULL.  
  
 Questo campo è un *campo posticipato*: non viene utilizzato al momento dell'impostazione, ma viene utilizzato in un secondo momento dal driver per indicare il supporto di valori Null (per gli AD) o per determinare il supporto di valori Null (per gli AD).  
  
 **SQL_DESC_LABEL [ICAM]**  
 Questo campo di sola lettura SQLCHAR - record contiene l'etichetta o il titolo della colonna. Se la colonna non dispone di un'etichetta, questa variabile contiene il nome della colonna. Se la colonna è senza nome e senza etichetta, questa variabile contiene una stringa vuota.  
  
 **SQL_DESC_LENGTH [Tutti]**  
 Questo campo di record SQLULEN è la lunghezza massima o effettiva di una stringa di caratteri in caratteri o di un tipo di dati binari in byte. È la lunghezza massima per un tipo di dati a lunghezza fissa o la lunghezza effettiva per un tipo di dati a lunghezza variabile. Il valore esclude sempre il carattere di terminazione null che termina la stringa di caratteri. Per i valori il cui tipo è SQL_TYPE_DATE, SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP o uno dei tipi di dati dell'intervallo SQL, questo campo contiene la lunghezza in caratteri della rappresentazione di stringa di caratteri del valore datetime o interval.  
  
 Il valore di questo campo può essere diverso dal valore di "length" come definito in ODBC 2 *.x*. Per ulteriori informazioni, vedere [Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_LITERAL_PREFIX [ICAM]**  
 Questo campo di sola lettura SQLCHAR - record contiene il carattere o i caratteri riconosciuti dal driver come prefisso per un valore letterale di questo tipo di dati. Questa variabile contiene una stringa vuota per un tipo di dati per il quale non è applicabile un prefisso letterale.  
  
 **SQL_DESC_LITERAL_SUFFIX [ICAM]**  
 Questo campo di sola lettura SQLCHAR - record contiene il carattere o i caratteri riconosciuti dal driver come suffisso per un valore letterale di questo tipo di dati. Questa variabile contiene una stringa vuota per un tipo di dati per il quale non è applicabile un suffisso letterale.  
  
 **SQL_DESC_LOCAL_TYPE_NAME [descrittori di implementazione]**  
 Questo campo di sola lettura SQLCHAR - record contiene qualsiasi nome localizzato (lingua nativa) per il tipo di dati che può essere diverso dal nome normale del tipo di dati. Se non è presente alcun nome localizzato, viene restituita una stringa vuota. Questo campo è solo a scopo di visualizzazione.  
  
 **SQL_DESC_NAME [Descrittori di implementazione]**  
 Questo campo di record SQLCHAR in un descrittore di riga contiene l'alias di colonna, se applicabile. Se l'alias di colonna non è applicabile, viene restituito il nome della colonna. In entrambi i casi, il driver imposta il campo SQL_DESC_UNNAMED su SQL_NAMED quando imposta il campo SQL_DESC_NAME. Se non è presente alcun nome di colonna o un alias di colonna, il driver restituisce una stringa vuota nel campo SQL_DESC_NAME e imposta il campo SQL_DESC_UNNAMED su SQL_UNNAMED.  
  
 Un'applicazione può impostare il campo SQL_DESC_NAME di un IPD su un nome di parametro o un alias per specificare i parametri della stored procedure in base al nome. Per ulteriori informazioni, vedere [Associazione di parametri in base al nome (parametri denominati)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md). Il campo SQL_DESC_NAME di un IRD è un campo di sola lettura. SQLSTATE HY091 (Identificatore di campo descrittore non valido) verrà restituito se un'applicazione tenta di impostarlo.  
  
 Negli IPD, questo campo non è definito se il driver non supporta i parametri denominati. Se il driver supporta i parametri denominati ed è in grado di descrivere i parametri, il nome del parametro viene restituito in questo campo.  
  
 **SQL_DESC_NULLABLE [descrittori di implementazione]**  
 Negli I/IRD, questo campo di record SQLSMALLINT di sola lettura è SQL_NULLABLE se la colonna può avere valori NULL, SQL_NO_NULLS se la colonna non dispone di valori NULL o SQL_NULLABLE_UNKNOWN se non è noto se la colonna accetta valori NULL. Questo campo riguarda la colonna del set di risultati, non la colonna di base.  
  
 Negli IPD, questo campo è sempre impostato su SQL_NULLABLE perché i parametri dinamici sono sempre nullable e non possono essere impostati da un'applicazione.  
  
 **SQL_DESC_NUM_PREC_RADIX [Tutti]**  
 Questo campo SQLINTEGER contiene un valore pari a 2 se il tipo di dati nel campo SQL_DESC_TYPE è un tipo di dati numerico approssimativo, perché il campo SQL_DESC_PRECISION contiene il numero di bit. Questo campo contiene un valore pari a 10 se il tipo di dati nel campo SQL_DESC_TYPE è un tipo di dati numerico esatto, poiché il campo SQL_DESC_PRECISION contiene il numero di cifre decimali. Questo campo è impostato su 0 per tutti i tipi di dati non numerici.  
  
 **SQL_DESC_OCTET_LENGTH [Tutti]**  
 Questo campo di record SQLLEN contiene la lunghezza, in byte, di una stringa di caratteri o di un tipo di dati binario. Per i tipi binari o di caratteri a lunghezza fissa, questa è la lunghezza effettiva in byte. Per i tipi binari o di caratteri a lunghezza variabile, questa è la lunghezza massima in byte. Questo valore esclude sempre lo spazio per il carattere di terminazione null per i descrittori di implementazione e include sempre lo spazio per il carattere di terminazione null per i descrittori dell'applicazione. Per i dati dell'applicazione, questo campo contiene la dimensione del buffer. Per gli AAD, questo campo è definito solo per i parametri di output o di input/output.  
  
 **SQL_DESC_OCTET_LENGTH_PTR [descrittori di applicazioni]**  
 Questo campo di record SQLLEN - punta a una variabile che conterrà la lunghezza totale in byte di un argomento dinamico (per i descrittori di parametro) o di un valore di colonna associato (per i descrittori di riga).  
  
 Per un APD, questo valore viene ignorato per tutti gli argomenti ad eccezione della stringa di caratteri e binario; Se questo campo punta a SQL_NTS, l'argomento dinamico deve essere con terminazione null. Per indicare che un parametro associato sarà un parametro data-at-execution, un'applicazione imposta questo campo nel record appropriato di APD su una variabile che, in fase di esecuzione, conterrà il valore SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC. Se è presente più di un campo di questo tipo, SQL_DESC_DATA_PTR può essere impostato su un valore che identifica in modo univoco il parametro per consentire all'applicazione di determinare quale parametro viene richiesto.  
  
 Se il campo OCTET_LENGTH_PTR di un ARD è un puntatore null, il driver non restituisce informazioni sulla lunghezza per la colonna. Se il campo SQL_DESC_OCTET_LENGTH_PTR di un APD è un puntatore null, il driver presuppone che le stringhe di caratteri e valori binari sono terminati con null. I valori binari non devono essere con terminazione null, ma devono avere una lunghezza per evitare il troncamento.  
  
 Se la chiamata a **SQLFetch** o **SQLFetchScroll** che riempie il buffer a cui punta questo campo non ha restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il contenuto del buffer non è definito. Questo campo è un *campo posticipato*. Non viene utilizzato al momento dell'impostazione, ma viene utilizzato in un secondo momento dal driver per determinare o indicare la lunghezza dell'ottetto dei dati.  
  
 **SQL_DESC_PARAMETER_TYPE [IPD]**  
 Questo campo di record SQLSMALLINT è impostato su SQL_PARAM_INPUT per un parametro di input, SQL_PARAM_INPUT_OUTPUT per un parametro di input/output, SQL_PARAM_OUTPUT per un parametro di output, SQL_PARAM_INPUT_OUTPUT_STREAM per un parametro in streaming di input/output o SQL_PARAM_OUTPUT_STREAM per un parametro di output trasmesso. È impostato su SQL_PARAM_INPUT per impostazione predefinita.  
  
 Per un IPD, il campo è impostato su SQL_PARAM_INPUT per impostazione predefinita se l'IPD non viene popolato automaticamente dal driver (l'attributo di istruzione SQL_ATTR_ENABLE_AUTO_IPD è SQL_FALSE). Un'applicazione deve impostare questo campo nell'IPD per i parametri che non sono parametri di input.  
  
 **SQL_DESC_PRECISION [Tutti]**  
 Questo campo di record SQLSMALLINT contiene il numero di cifre per un tipo numerico esatto, il numero di bit nella mantissa (precisione binaria) per un tipo numerico approssimativo o il numero di cifre nel componente dei secondi frazionari per il SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP o SQL_INTERVAL_SECOND tipo di dati. Questo campo non è definito per tutti gli altri tipi di dati.  
  
 Il valore in questo campo può essere diverso dal valore di "precisione" come definito in ODBC 2 *.x*. Per ulteriori informazioni, vedere [Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_ROWVER [descrittori di implementazione]**  
 Questo campo SQLSMALLINTrecord indica se una colonna viene modificata automaticamente dal sistema DBMS quando viene aggiornata una riga, ad esempio una colonna di tipo "timestamp" in SQL ServerSQL Server.This SQLSMALLINTrecord field indicates whether a column is automatically modified by the DBMS when a row is updated (for example, a column of the type "timestamp" in SQL ServerSQL Server). Il valore di questo campo di record è impostato su SQL_TRUE se la colonna è una colonna di controllo delle versioni delle righe e per SQL_FALSE in caso contrario. Questo attributo di colonna è simile alla chiamata **SQLSpecialColumns** con IdentifierType di SQL_ROWVER per determinare se una colonna viene aggiornata automaticamente.  
  
 **SQL_DESC_SCALE [Tutti]**  
 Questo campo di record SQLSMALLINT contiene la scala definita per i tipi di dati decimali e numerici. Il campo non è definito per tutti gli altri tipi di dati.  
  
 Il valore di questo campo può essere diverso dal valore di "scale" come definito in ODBC 2 *.x*. Per ulteriori informazioni, vedere [Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_SCHEMA_NAME [ICAM]**  
 Questo campo di sola lettura SQLCHAR - record contiene il nome dello schema della tabella di base che contiene la colonna. Il valore restituito dipende dal driver se la colonna è un'espressione o se la colonna fa parte di una vista. Se l'origine dati non supporta gli schemi o non è possibile determinare il nome dello schema, questa variabile contiene una stringa vuota.  
  
 **SQL_DESC_SEARCHABLE [ICAM]**  
 Questo campo di record SQLSMALLINT di sola lettura è impostato su uno dei valori seguenti:  
  
-   SQL_PRED_NONE se la colonna non può essere utilizzata in una clausola **WHERE.** (Questo è lo stesso valore SQL_UNSEARCHABLE in ODBC 2 *.x .x*.)  
  
-   SQL_PRED_CHAR se la colonna può essere utilizzata in una clausola **WHERE** ma solo con il predicato **LIKE.** (Questo è lo stesso valore SQL_LIKE_ONLY in ODBC 2 *.x*.x .)  
  
-   SQL_PRED_BASIC se la colonna può essere utilizzata in una clausola **WHERE** con tutti gli operatori di confronto ad eccezione **di LIKE**. (Questo è lo stesso valore SQL_EXCEPT_LIKE in ODBC 2 *.x*.x .)  
  
-   SQL_PRED_SEARCHABLE se la colonna può essere utilizzata in una clausola **WHERE** con qualsiasi operatore di confronto.  
  
 **SQL_DESC_TABLE_NAME [ICAM]**  
 Questo campo di sola lettura SQLCHAR - record contiene il nome della tabella di base che contiene questa colonna. Il valore restituito dipende dal driver se la colonna è un'espressione o se la colonna fa parte di una vista.  
  
 **SQL_DESC_TYPE [Tutti]**  
 Questo campo di record SQLSMALLINT specifica il tipo di dati SQL o C conciso per tutti i tipi di dati, ad eccezione dei tipi di dati datetime e interval. Per i tipi di dati datetime e interval, questo campo specifica il tipo di dati dettagliato, SQL_DATETIME o SQL_INTERVAL.  
  
 Ogni volta che questo campo contiene SQL_DATETIME o SQL_INTERVAL, il campo SQL_DESC_DATETIME_INTERVAL_CODE deve contenere il sottocodice appropriato per il tipo conciso. Per i tipi di dati datetime, SQL_DESC_TYPE contiene SQL_DATETIME e il campo SQL_DESC_DATETIME_INTERVAL_CODE contiene un sottocodice per il tipo di dati datetime specifico. Per i tipi di dati intervallo, SQL_DESC_TYPE contiene SQL_INTERVAL e il campo SQL_DESC_DATETIME_INTERVAL_CODE contiene un sottocodice per il tipo di dati intervallo specifico.  
  
 I valori nei campi SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE sono interdipendenti. Ogni volta che uno dei campi è impostato, anche l'altro deve essere impostato. SQL_DESC_TYPE possono essere impostati da una chiamata a **SQLSetDescField** o **SQLSetDescRec**. SQL_DESC_CONCISE_TYPE può essere impostata da una chiamata a **SQLBindCol** o **SQLBindParameter**o **SQLSetDescField**.  
  
 Se SQL_DESC_TYPE è impostato su un tipo di dati conciso diverso da un tipo di dati interval o datetime, il campo SQL_DESC_CONCISE_TYPE viene impostato sullo stesso valore e il campo SQL_DESC_DATETIME_INTERVAL_CODE è impostato su 0.  
  
 Se SQL_DESC_TYPE è impostato sul tipo di dati verbose datetime o interval (SQL_DATETIME o SQL_INTERVAL) e il campo SQL_DESC_DATETIME_INTERVAL_CODE è impostato sul sottocodice appropriato, il campo TYPE SQL_DESC_CONCISE viene impostato sul tipo conciso corrispondente. Se si tenta di impostare SQL_DESC_TYPE su uno dei tipi di intervallo o datetime concisi, verrà restituito SQLSTATE HY021 (informazioni sul descrittore incoerenti).  
  
 Quando il campo SQL_DESC_TYPE viene impostato da una chiamata a **SQLBindCol**, **SQLBindParameter**o **SQLSetDescField**, i campi seguenti vengono impostati sui seguenti valori predefiniti, come illustrato nella tabella seguente. I valori dei campi rimanenti dello stesso record non sono definiti.  
  
|Valore della SQL_DESC_TYPE|Altri campi impostati in modo implicito|  
|------------------------------|---------------------------------|  
|SQL_CHAR, SQL_VARCHAR, SQL_C_CHAR, SQL_C_VARCHAR|SQL_DESC_LENGTH è impostato su 1. SQL_DESC_PRECISION è impostato su 0.|  
|SQL_DATETIME|Quando SQL_DESC_DATETIME_INTERVAL_CODE è impostato su SQL_CODE_DATE o SQL_CODE_TIME, SQL_DESC_PRECISION è impostato su 0. Quando è impostato su SQL_DESC_TIMESTAMP, SQL_DESC_PRECISION è impostato su 6.|  
|SQL_DECIMAL, SQL_NUMERIC, SQL_C_NUMERIC|SQL_DESC_SCALE è impostato su 0. SQL_DESC_PRECISION è impostata sulla precisione definita dall'implementazione per il rispettivo tipo di dati.<br /><br /> Vedere [SQL to C: Numerico](../../../odbc/reference/appendixes/sql-to-c-numeric.md) per informazioni su come associare manualmente un valore di SQL_C_NUMERIC.|  
|SQL_FLOAT, SQL_C_FLOAT|SQL_DESC_PRECISION è impostata sulla precisione predefinita definita dall'implementazione per SQL_FLOAT.|  
|SQL_INTERVAL|Quando SQL_DESC_DATETIME_INTERVAL_CODE è impostata su un tipo di dati intervallo, SQL_DESC_DATETIME_INTERVAL_PRECISION è impostato su 2 (precisione di interlinea intervallo predefinita). Quando l'intervallo ha un componente secondi, SQL_DESC_PRECISION è impostata su 6 (la precisione predefinita dei secondi).|  
  
 Quando un'applicazione chiama **SQLSetDescField** per impostare i campi di un descrittore anziché **chiamare SQLSetDescRec**, l'applicazione deve prima dichiarare il tipo di dati. In caso affermativo, gli altri campi indicati nella tabella precedente vengono impostati in modo implicito. Se uno dei valori impostati in modo implicito non è accettabile, l'applicazione può quindi chiamare **SQLSetDescField** o **SQLSetDescRec** per impostare il valore inaccettabile in modo esplicito.  
  
 **SQL_DESC_TYPE_NAME [Descrittori di implementazione]**  
 Questo campo di sola lettura SQLCHAR - record contiene il nome del tipo dipendente dall'origine dati (ad esempio, "CHAR", "VARCHAR" e così via). Se il nome del tipo di dati è sconosciuto, questa variabile contiene una stringa vuota.  
  
 **SQL_DESC_UNNAMED [descrittori di implementazione]**  
 Questo campo di record SQLSMALLINT in un descrittore di riga viene impostato dal driver per SQL_NAMED o SQL_UNNAMED quando imposta il campo SQL_DESC_NAME. Se il campo SQL_DESC_NAME contiene un alias di colonna o se l'alias di colonna non è applicabile, il driver imposta il campo SQL_DESC_UNNAMED su SQL_NAMED. Se un'applicazione imposta il campo SQL_DESC_NAME di un IPD su un nome di parametro o un alias, il driver imposta il campo SQL_DESC_UNNAMED dell'IPD su SQL_NAMED. Se non è presente alcun nome di colonna o un alias di colonna, il driver imposta il campo SQL_DESC_UNNAMED su SQL_UNNAMED.  
  
 Un'applicazione può impostare il campo SQL_DESC_UNNAMED di un IPD su SQL_UNNAMED. Un driver restituisce SQLSTATE HY091 (identificatore di campo descrittore non valido) se un'applicazione tenta di impostare il campo SQL_DESC_UNNAMED di un IPD su SQL_NAMED. Il campo SQL_DESC_UNNAMED di un IRD è di sola lettura; SQLSTATE HY091 (Identificatore di campo descrittore non valido) verrà restituito se un'applicazione tenta di impostarlo.  
  
 **SQL_DESC_UNSIGNED [Descrittori di implementazione]**  
 Questo campo di record SQLSMALLINT di sola lettura è impostato su SQL_TRUE se il tipo di colonna è senza segno o non numerico oppure SQL_FALSE se il tipo di colonna è firmato.  
  
 **SQL_DESC_UPDATABLE [ICAM]**  
 Questo campo di record SQLSMALLINT di sola lettura è impostato su uno dei valori seguenti:  
  
-   SQL_ATTR_READ_ONLY se la colonna del set di risultati è di sola lettura.  
  
-   SQL_ATTR_WRITE se la colonna del set di risultati è di lettura/scrittura.  
  
-   SQL_ATTR_READWRITE_UNKNOWN se non è noto se la colonna del set di risultati è aggiornabile o meno.  
  
 SQL_DESC_UPDATABLE viene descritta l'aggiornabilità della colonna nel set di risultati, non la colonna nella tabella di base. L'aggiornabilità della colonna nella tabella di base su cui si basa questa colonna del set di risultati può essere diversa dal valore in questo campo. Se una colonna è aggiornabile può essere basata sul tipo di dati, sui privilegi utente e sulla definizione del set di risultati stesso. Se non è chiaro se una colonna è aggiornabile, SQL_ATTR_READWRITE_UNKNOWN deve essere restituito.  
  
## <a name="consistency-checks"></a>Controlli di coerenza  
 Una verifica di coerenza viene eseguita automaticamente dal driver ogni volta che un'applicazione passa un valore per il campo SQL_DESC_DATA_PTR di ARD, APD o IPD. Se uno dei campi non è coerente con altri campi, **SQLSetDescField** restituirà SQLSTATE HY021 (informazioni sul descrittore incoerenti). Per ulteriori informazioni, vedere "Verifica coerenza" in [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di una colonna|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Associazione di un parametro|[Pagina relativa alla funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Ottenere un campo descrittoreGetting a descriptor field|[Funzione SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Recupero di più campi descrittoreGetting multiple descriptor fields|[Funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Impostazione di più campi descrittore|[Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Riferimento API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)
