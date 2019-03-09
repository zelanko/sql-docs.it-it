---
title: Funzione SQLBindParameter | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindParameter
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc566c7cfd86e76df5389e56b7465dcd04b76f51
ms.sourcegitcommit: 3c4bb35163286da70c2d669a3f84fb6a8145022c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2019
ms.locfileid: "57683641"
---
# <a name="sqlbindparameter-function"></a>Pagina relativa alla funzione SQLBindParameter

**Conformità**  
 Versione introdotta: Conformità agli standard 2.0 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLBindParameter** associa un buffer a un marcatore di parametro in un'istruzione SQL. **SQLBindParameter** supporta l'associazione a un tipo di dati Unicode C, anche se il driver sottostante non supporta i dati Unicode.  
  
> [!NOTE]  
>  Questa funzione sostituisce la funzione ODBC 1.0 **SQLSetParam**. Per altre informazioni, vedere "Commenti".  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
SQLRETURN SQLBindParameter(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT     InputOutputType,  
      SQLSMALLINT     ValueType,  
      SQLSMALLINT     ParameterType,  
      SQLULEN         ColumnSize,  
      SQLSMALLINT     DecimalDigits,  
      SQLPOINTER      ParameterValuePtr,  
      SQLLEN          BufferLength,  
      SQLLEN *        StrLen_or_IndPtr);  
```
  
## <a name="arguments"></a>Argomenti

 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *ParameterNumber*  
 [Input] Numero di parametro, ordinati in sequenza in ordine crescente dei parametri, a partire da 1.  
  
 *InputOutputType*  
 [Input] Il tipo del parametro. Per altre informazioni, vedere "*InputOutputType* argomento" in "Commenti".  
  
 *ValueType*  
 [Input] Il tipo di dati C del parametro. Per altre informazioni, vedere "*ValueType* argomento" in "Commenti".  
  
 *ParameterType*  
 [Input] Il tipo di dati SQL del parametro. Per altre informazioni, vedere "*ParameterType* argomento" in "Commenti".  
  
 *ColumnSize*  
 [Input] Le dimensioni della colonna o espressione del marcatore di parametro corrispondente. Per altre informazioni, vedere "*ColumnSize* argomento" in "Commenti".  
  
 Se l'applicazione verrà eseguita in un sistema operativo di Windows a 64 bit, vedere [le informazioni ODBC 64-Bit](../../../odbc/reference/odbc-64-bit-information.md).  
  
 *DecimalDigits*  
 [Input] Le cifre decimali della colonna o espressione del marcatore di parametro corrispondente. Per altre informazioni sulle dimensioni di colonna, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *ParameterValuePtr*  
 [Input posticipata] Un puntatore a un buffer per i dati del parametro. Per altre informazioni, vedere "*ParameterValuePtr* argomento" in "Commenti".  
  
 *BufferLength*  
 [Input/Output] Lunghezza del *ParameterValuePtr* buffer in byte. Per altre informazioni, vedere "*BufferLength* argomento" in "Commenti".  
  
 Visualizzare [le informazioni ODBC 64-Bit](../../../odbc/reference/odbc-64-bit-information.md), se l'applicazione verrà eseguita in un sistema operativo a 64 bit.  
  
 *StrLen_or_IndPtr*  
 [Input posticipata] Un puntatore a un buffer per la lunghezza del parametro. Per altre informazioni, vedere "*StrLen_or_IndPtr* argomento" in "Commenti".  
  
## <a name="returns"></a>Valori di codice restituiti

 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica

 Quando **SQLBindParameter** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLBindParameter** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  

|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07006|Violazione dell'attributo del tipo di dati|Il tipo di dati identificato dal *ValueType* argomento non può essere convertito nel tipo di dati identificato dalle *ParameterType* argomento. Si noti che questo errore potrebbe essere restituito da **SQLExecDirect**, **SQLExecute**, o **SQLPutData** in fase di esecuzione, anziché mediante **SQLBindParameter**.|  
|07009|Indice del descrittore non valido|(DM) il valore specificato per l'argomento *ParameterNumber* era minore di 1.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel **MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver non è riuscito ad allocare memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY003|Tipo di buffer dell'applicazione non valido|Il valore specificato dall'argomento *ValueType* non era un SQL_C_DEFAULT o un tipo di dati C valido.|  
|HY004|Tipo di dati SQL non valido|Il valore specificato per l'argomento *ParameterType* era un identificatore di tipo di dati SQL ODBC valido né un identificatore di tipo dati SQL specifico del driver supportata dal driver.|  
|HY009|Valore dell'argomento non valido|(DM) dell'argomento *ParameterValuePtr* era un puntatore null, l'argomento *StrLen_or_IndPtr* era un puntatore null e l'argomento *InputOutputType* non era SQL_PARAM_ OUTPUT.<br /><br /> SQL_PARAM_OUTPUT (DM), in cui l'argomento *ParameterValuePtr* era un puntatore null, il tipo C è char o binary e il BufferLength (*cbValueMax*) è maggiore di 0.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando **SQLBindParameter** è stato chiamato.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione la *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY021|Informazioni descrittore incoerenti.|Le informazioni del descrittore controllate durante una verifica coerenza non erano coerente. (Vedere la sezione "Le verifiche coerenza" nella **SQLSetDescField**.)<br /><br /> Il valore specificato per l'argomento *DecimalDigits* non rientra nell'intervallo dei valori supportati dall'origine dati per una colonna del tipo di dati SQL specificata per il *ParameterType* argomento.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore in *BufferLength* era minore di 0. (Vedere la descrizione del campo SQL_DESC_DATA_PTR **SQLSetDescField**.)|  
|HY104|Valore di precisione o scala non valido|Il valore specificato per l'argomento *ColumnSize* oppure *DecimalDigits* non rientra nell'intervallo dei valori supportati dall'origine dati per una colonna del tipo di dati SQL specificato da di  *ParameterType* argomento.|  
|HY105|Tipo di parametro non valido|(DM) il valore specificato per l'argomento *InputOutputType* non è valido. (Vedere "Commenti".)|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|L'origine dati o driver non supporta la conversione specificata dalla combinazione del valore specificato per l'argomento *ValueType* e il valore specifico del driver specificato per l'argomento *ParameterType*.<br /><br /> Il valore specificato per l'argomento *ParameterType* era un identificatore di tipo di dati SQL ODBC valido per la versione di ODBC supportati dal driver, ma non era supportata dall'origine dati o driver.<br /><br /> Il driver supporta solo l'API ODBC 2. *x* e l'argomento *ValueType* era una delle operazioni seguenti:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> tutti i tipi di dati di intervallo C sono elencati nella [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) nell'appendice d: Tipi di dati.<br /><br /> Il driver supporta solo le versioni ODBC precedenti alla versione 3.50 e l'argomento *ValueType* era SQL_C_GUID.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti

 Un'applicazione chiama **SQLBindParameter** associare ogni marcatore di parametro in un'istruzione SQL. Binding rimangono valide fino a quando l'applicazione chiama **SQLBindParameter** anche in questo caso, chiama **SQLFreeStmt** con l'opzione SQL_RESET_PARAMS o chiamate **SQLSetDescField** a impostare il campo di intestazione SQL_DESC_COUNT di APD su 0.  
  
 Per altre informazioni sui parametri, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md). Per altre informazioni sui tipi di dati di parametro e marcatori di parametro, vedere [tipi di dati di parametro](../../../odbc/reference/appendixes/parameter-data-types.md) e [marcatori di parametro](../../../odbc/reference/appendixes/parameter-markers.md) nell'appendice c: Grammatica SQL.  
  
## <a name="parameternumber-argument"></a>Argomento ParameterNumber  
 Se *ParameterNumber* nella chiamata a **SQLBindParameter** è maggiore del valore di, SQL_DESC_COUNT **SQLSetDescField** viene chiamato per aumentare il valore di SQL_DESC_ Per CONTARE *ParameterNumber*.  
  
## <a name="inputoutputtype-argument"></a>Argomento InputOutputType  
 Il *InputOutputType* argomento specifica il tipo del parametro. Questo argomento consente di impostare il campo SQL_DESC_PARAMETER_TYPE dell'IPD. Tutti i parametri nelle istruzioni SQL che non chiamano le procedure, ad esempio **inserire** , le istruzioni sono *input * * parametri*. I parametri nelle chiamate a procedure possono essere di input, input/output o i parametri di output. (Un'applicazione chiama **SQLProcedureColumns** per determinare il tipo di un parametro in una chiamata di procedura; il cui tipo non è possibile determinare i parametri sono considerati parametri di input.)  
  
 Il *InputOutputType* degli argomenti è uno dei valori seguenti:  
  
-   SQL_PARAM_INPUT. Il parametro contrassegna un parametro in un'istruzione SQL che non chiama una stored procedure, ad esempio un **Inserisci** istruzione oppure contrassegna un parametro di input in una procedura. Ad esempio, i parametri in **INSERT INTO VALUES dipendente (?,?,?)**  sono parametri di input, mentre i parametri in **{chiamare AddEmp (?,?,?)}**  può essere, ma non necessariamente, i parametri di input.  
  
     Quando viene eseguita l'istruzione, il driver invia dati per il parametro dell'origine dati. il \* *ParameterValuePtr* buffer deve contenere un valore di input valido, o il **StrLen_or_IndPtr* buffer deve contenere SQL_NULL_DATA, SQL_DATA_AT_EXEC o il risultato del SQL_LEN_DATA_AT Macro Exec.  
  
     Se un'applicazione non è possibile determinare il tipo di un parametro in una chiamata di routine, imposta *InputOutputType* da SQL_PARAM_INPUT; se l'origine dati restituisce un valore per il parametro, il driver Ignora.  
  
-   SQL_PARAM_INPUT_OUTPUT. Il parametro contrassegna un parametro di input/output in una procedura. Ad esempio, il parametro in **{chiamare GetEmpDept(?)}**  è un parametro di input/output che accetta un nome di dipendente e restituisce il nome del reparto del dipendente.  
  
     Quando viene eseguita l'istruzione, il driver invia dati per il parametro dell'origine dati. il \* *ParameterValuePtr* buffer deve contenere un valore di input valido, oppure il \* *StrLen_or_IndPtr* buffer deve contenere SQL_NULL_DATA, SQL_DATA_AT_EXEC o il risultato di la macro SQL_LEN_DATA_AT_EXEC. Dopo l'istruzione viene eseguita, il driver restituisce i dati per il parametro all'applicazione. Se l'origine dati non restituisce un valore per un parametro di input/output, il driver imposta il **StrLen_or_IndPtr* buffer su SQL_NULL_DATA.  
  
    > [!NOTE]  
    >  Quando un'applicazione ODBC 1.0 chiama **SQLSetParam** in un driver ODBC 2.0, gestione Driver convertirà tale evento in una chiamata a **SQLBindParameter** in cui il *InputOutputType* argomento è impostato su SQL_PARAM_INPUT_OUTPUT.  
  
-   SQL_PARAM_OUTPUT. Il parametro contrassegna il valore restituito di una routine o un parametro di output in una routine. in entrambi i casi, si parla *parametri di output*. Ad esempio, il parametro nel **{? = chiamare GetNextEmpID}** è un parametro di output che restituisce il successivo ID del dipendente.  
  
     Dopo l'istruzione viene eseguita, il driver restituisce i dati per il parametro all'applicazione, a meno che il *ParameterValuePtr* e *StrLen_or_IndPtr* gli argomenti sono entrambi puntatori null, nel qual caso il driver ignora il valore di output. Se l'origine dati non restituisce un valore per un parametro di output, il driver imposta il **StrLen_or_IndPtr* buffer su SQL_NULL_DATA.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. Indica che un parametro di input/output deve essere trasmessa. **SQLGetData** può leggere i valori dei parametri in parti. *BufferLength* viene ignorato perché verrà determinata la lunghezza del buffer in corrispondenza della chiamata di **SQLGetData**. Il valore della *StrLen_or_IndPtr* buffer deve contenere SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC. Un parametro deve essere associato come un parametro data-at-execution (. DAE) nell'input se viene trasmesso all'output. *ParameterValuePtr* può essere qualsiasi valore del puntatore non null restituirà **SQLParamData** come definito dall'utente del token il cui valore è stato superato con *ParameterValuePtr* per sia di input e output. Per altre informazioni, vedere [recupero di parametri di Output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_PARAM_OUTPUT_STREAM. Uguale a SQL_PARAM_INPUT_OUTPUT_STREAM, per un parametro di output. **StrLen_or_IndPtr* viene ignorato nell'input.  
  
 La tabella seguente elenca diverse combinazioni di *InputOutputType* e **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|Risultato|Tenere presente su ParameterValuePtr|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Input in parti|*ParameterValuePtr* può essere qualsiasi valore del puntatore che restituirà **SQLParamData** come definito dall'utente del token il cui valore è stato superato con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT|Non SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Associare buffer di input|*ParameterValuePtr* è l'indirizzo del buffer di input.|  
|SQL_PARAM_OUTPUT|Ignorato nell'input.|Buffer con binding di output|*ParameterValuePtr* è l'indirizzo del buffer di output.|  
|SQL_PARAM_OUTPUT_STREAM|Ignorato nell'input.|Flusso di output|*ParameterValuePtr* può essere qualsiasi valore di puntatore, restituirà **SQLParamData** come definito dall'utente del token il cui valore è stato superato con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Input in parti e buffer di output associato|*ParameterValuePtr* è l'indirizzo del buffer di output, che saranno restituiti anche dal **SQLParamData** come definito dall'utente del token il cui valore è stato superato con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|Non SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Input per il buffer associato e buffer di output associato|*ParameterValuePtr* è l'indirizzo del buffer di input/output condivisi.|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Input in parti e flusso di output|*ParameterValuePtr* può essere qualsiasi valore di puntatore non null, che restituirà **SQLParamData** come definito dall'utente del token il cui valore è stato superato con *ParameterValuePtr* per sia di input e di output.|  
  
> [!NOTE]  
>  Il driver necessario decidere quali tipi SQL sono consentiti quando un'applicazione si associa un output o un parametro di input / output come state trasmesse. Gestione driver non genererà un errore per un tipo SQL non valido.  
  
## <a name="valuetype-argument"></a>Argomento ValueType

 Il *ValueType* argomento specifica il tipo di dati C del parametro. Questo argomento imposta i campi SQL_DESC_TYPE SQL_DESC_CONCISE_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE di APD. Deve essere uno dei valori di [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) sezione dell'appendice d: Tipi di dati.  
  
 Se il *ValueType* degli argomenti è uno dei tipi di dati di intervallo, il campo SQL_DESC_TYPE delle *ParameterNumber* record di APD è impostata su SQL_INTERVAL, il campo SQL_DESC_CONCISE_TYPE di APD è impostato su il tipo di dati di intervallo concisa e il campo SQL_DESC_DATETIME_INTERVAL_CODE del *ParameterNumber* record è impostata su un codice secondario per il tipo di dati di intervallo specifico. (Vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).) L'intervallo predefinito iniziali precisione (2) e la precisione dei secondi di intervallo predefinito (6), come set di campi SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION di APD, rispettivamente, vengono usati per i dati. Se entrambi precisione predefinita non è appropriata, l'applicazione deve impostare in modo esplicito il campo di descrizione da una chiamata a **SQLSetDescField** oppure **SQLSetDescRec**.  
  
 Se il *ValueType* degli argomenti è uno dei tipi di dati Data/ora, il campo SQL_DESC_TYPE delle *ParameterNumber* record di APD è impostato su SQL_DATETIME, il campo SQL_DESC_CONCISE_TYPE del *ParameterNumber* record di APD è impostato il tipo di dati datetime concisa C e il campo SQL_DESC_DATETIME_INTERVAL_CODE del *ParameterNumber* record è impostata su un codice secondario per la data e ora specifica tipo di dati. (Vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Se il *ValueType* argomento è un tipo di dati SQL_C_NUMERIC la precisione predefinita (che è definito dal driver) e la scala predefinita (0), come set di campi SQL_DESC_PRECISION e SQL_DESC_SCALE di APD, vengono usati per i dati. Se la precisione predefinita o la scala non è appropriata, l'applicazione deve impostare in modo esplicito il campo di descrizione da una chiamata a **SQLSetDescField** oppure **SQLSetDescRec**.  
  
 SQL_C_DEFAULT specifica che il valore del parametro da trasferire dal tipo di dati C predefiniti per il tipo di dati SQL specificato con *ParameterType*.  
  
 È anche possibile specificare un tipo di dati C esteso. Per altre informazioni, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 Per altre informazioni, vedere [tipi di dati C predefiniti](../../../odbc/reference/appendixes/default-c-data-types.md), [convertendo i dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md), e [convertendo i dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) nell'appendice d: Tipi di dati.  
  
## <a name="parametertype-argument"></a>Argomento ParameterType

 Deve trattarsi di uno dei valori elencati nella [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) sezione dell'appendice d: Tipi di dati, oppure deve essere un valore specifico del driver. Questo argomento consente di impostare i campi SQL_DESC_TYPE SQL_DESC_CONCISE_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE dell'IPD.  
  
 Se il *ParameterType* argomento è uno degli identificatori di data/ora, il campo SQL_DESC_TYPE dell'IPD è impostato su SQL_DATETIME, il campo SQL_DESC_CONCISE_TYPE dell'IPD è impostato per il tipo di dati SQL di data/ora concisa e il SQL_DESC_ Campo DATETIME_INTERVAL_CODE è impostato sul valore sottocodice datetime appropriato.  
  
 Se *ParameterType* è uno degli identificatori intervallo, il campo SQL_DESC_TYPE dell'IPD è impostato su SQL_INTERVAL, il campo SQL_DESC_CONCISE_TYPE dell'IPD è impostato per il tipo di dati di intervallo SQL conciso e il SQL_DESC_DATETIME_ Campo INTERVAL_CODE dell'IPD è impostato per il codice secondario dell'intervallo di tempo appropriato. Il campo SQL_DESC_DATETIME_INTERVAL_PRECISION dell'IPD è impostato per l'intervallo di precisione iniziale e il campo SQL_DESC_PRECISION è impostato per la precisione dei secondi di intervallo, se applicabile. Se il valore predefinito di SQL_DESC_DATETIME_INTERVAL_PRECISION o SQL_DESC_PRECISION non è appropriato, l'applicazione deve impostarlo in modo esplicito chiamando **SQLSetDescField**. Per altre informazioni sui set di questi campi, vedere [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Se il *ValueType* argomento è un tipo di dati SQL_NUMERIC, la precisione predefinita (che è definito dal driver) e la scala predefinita (0), come set di campi di SQL_DESC_PRECISION e SQL_DESC_SCALE dell'IPD, vengono usati per i dati. Se la precisione predefinita o la scala non è appropriata, l'applicazione deve impostare in modo esplicito il campo di descrizione da una chiamata a **SQLSetDescField** oppure **SQLSetDescRec**.  
  
 Per informazioni sulla modalità di conversione dei dati, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) e [convertendo i dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) nell'appendice d: Tipi di dati.  
  
## <a name="columnsize-argument"></a>ColumnSize argomento

 Il *ColumnSize* argomento specifica le dimensioni della colonna o espressione che corrisponde al marcatore di parametro, la lunghezza di tali dati o entrambi. Questo argomento consente di impostare diversi campi dell'IPD, a seconda del tipo di dati SQL (il *ParameterType* argomento). Per questo mapping si applicano le regole seguenti:  
  
-   Se *ParameterType* è SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY, o uno dei concisa SQL datetime o intervallo di tipi di dati, il campo SQL_DESC_LENGTH dell'IPD è impostato sul valore del  *ColumnSize*. (Per altre informazioni, vedere la [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) sezione nell'appendice d: Tipi di dati.)  
  
-   Se *ParameterType* è SQL_DECIMAL, SQL_NUMERIC, SQL_FLOAT, SQL_REAL o SQL_DOUBLE, il campo SQL_DESC_PRECISION dell'IPD è impostato sul valore di *ColumnSize*.  
  
-   Per altri tipi di dati, il *ColumnSize* argomento verrà ignorato.  
  
 Per altre informazioni, vedere "Passaggio di valori di parametro" e SQL_DATA_AT_EXEC in "*StrLen_or_IndPtr* argomento."  
  
## <a name="decimaldigits-argument"></a>Argomento DecimalDigits

 Se *ParameterType* è SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND o SQL_INTERVAL_MINUTE_TO_SECOND, viene impostato il campo SQL_DESC_PRECISION dell'IPD per *DecimalDigits*. Se *ParameterType* rappresenti SQL_NUMERIC SQL_DECIMAL, il campo SQL_DESC_SCALE dell'IPD è impostato su *DecimalDigits*. Per tutti gli altri tipi di dati, il *DecimalDigits* argomento verrà ignorato.  
  
## <a name="parametervalueptr-argument"></a>Argomento ParameterValuePtr

 Il *ParameterValuePtr* argomento punta a un buffer che, quando **SQLExecute** oppure **SQLExecDirect** viene chiamato, contiene i dati effettivi per il parametro. I dati devono essere nel formato specificato per il *ValueType* argomento. Questo argomento consente di impostare il campo SQL_DESC_DATA_PTR di APD. Un'applicazione può impostare il *ParameterValuePtr* argomento a un puntatore null, purché  *\*StrLen_or_IndPtr* è SQL_NULL_DATA o SQL_DATA_AT_EXEC. (Si applica solo a parametri input o di input/output).  
  
 Se \* *StrLen_or_IndPtr* è il risultato di SQL_LEN_DATA_AT_EXEC (*lunghezza*) (macro) o SQL_DATA_AT_EXEC, quindi *ParameterValuePtr* è un valore di puntatore definiti dall'applicazione che è associato il parametro. Viene restituito all'applicazione tramite **SQLParamData**. Ad esempio, *ParameterValuePtr* potrebbe essere un token diverso da zero, ad esempio un numero di parametro, un puntatore ai dati o un puntatore a una struttura che l'applicazione utilizzata per associare i parametri di input. Tuttavia, si noti che se il parametro è un parametro di input/output *ParameterValuePtr* deve essere un puntatore a un buffer in cui verrà archiviato il valore di output. Se il valore dell'attributo di istruzione SQL_ATTR_PARAMSET_SIZE è maggiore di 1, l'applicazione può usare il valore a cui punta l'attributo di istruzione SQL_ATTR_PARAMS_PROCESSED_PTR in combinazione con il *ParameterValuePtr* discussione. Ad esempio, *ParameterValuePtr* potrebbe puntare a una matrice di valori e l'applicazione può usare il valore a cui punta SQL_ATTR_PARAMS_PROCESSED_PTR per recuperare il valore corretto dalla matrice. Per altre informazioni, vedere "passaggio di valori dei parametri" più avanti in questa sezione.  
  
 Se il *InputOutputType* l'argomento è, SQL_PARAM_OUTPUT o SQL_PARAM_INPUT_OUTPUT *ParameterValuePtr* punta a un buffer in cui il driver restituisce il valore di output. Se la procedura restituisce uno o più set di risultati, il \* *ParameterValuePtr* buffer non è garantito a essere impostata fino a quando non sono stati elaborati tutti i conteggi di riga/set di risultati. Se il buffer non è impostato fino a quando non sarà stata completata, i parametri di output e valori restituiti non sono disponibili finché **SQLMoreResults** restituisce SQL_NO_DATA. La chiamata **SQLCloseCursor** oppure **SQLFreeStmt** con un'opzione di SQL_CLOSE causerà questi valori verranno ignorati.  
  
 Se è maggiore di 1, il valore dell'attributo di istruzione SQL_ATTR_PARAMSET_SIZE *ParameterValuePtr* punta a una matrice. Una singola istruzione SQL elabora la matrice completa dei valori di input per un parametro di input o input/output e restituisce una matrice di valori di output per un input/output o parametro di output.  
  
## <a name="bufferlength-argument"></a>Argomento BufferLength

 Per i caratteri e i dati binari C, il *BufferLength* argomento specifica la lunghezza del \* *ParameterValuePtr* buffer (se si tratta di un elemento singolo) o la lunghezza di un elemento nel \* *ParameterValuePtr* matrice (se il valore dell'attributo di istruzione SQL_ATTR_PARAMSET_SIZE è maggiore di 1). Questo argomento consente di impostare campo del record SQL_DESC_OCTET_LENGTH di APD. Se l'applicazione consente di specificare più valori, *BufferLength* viene usato per determinare la posizione dei valori nel **ParameterValuePtr* matrice, input e output. Per i parametri di input/output e outpui, viene utilizzato per determinare se troncare carattere e i dati binari di C nell'output:  
  
-   Per i dati di caratteri C, se il numero di byte disponibili da restituire è maggiore o uguale a *BufferLength*, i dati in \* *ParameterValuePtr* viene troncato a  *BufferLength* meno la lunghezza di un carattere di terminazione null ed è con terminazione null dal driver.  
  
-   Per i dati binari di C, se è maggiore del numero di byte disponibili per restituire *BufferLength*, i dati in \* *ParameterValuePtr* viene troncato a *BufferLength*byte.  
  
 Per tutti gli altri tipi di dati C, il *BufferLength* argomento verrà ignorato. La lunghezza del \* *ParameterValuePtr* buffer (se si tratta di un elemento singolo) o la lunghezza di un elemento nel \* *ParameterValuePtr* matrice (se l'applicazione chiama  **SQLSetStmtAttr** con un *attributo* argomento di SQL_ATTR_PARAMSET_SIZE per specificare più valori per ogni parametro) si presuppone che sia la lunghezza del tipo di dati C.  
  
 Flusso di output o trasmessi i parametri di input/output, il *BufferLength* verrà ignorato perché la lunghezza del buffer è stata specificata **SQLGetData**.  
  
> [!NOTE]  
>  Quando un'applicazione ODBC 1.0 chiama **SQLSetParam** in un'applicazione ODBC 3. *x* driver, gestione Driver convertirà tale evento in una chiamata a **SQLBindParameter** in cui il *BufferLength* argomento è sempre SQL_SETPARAM_VALUE_MAX. Poiché gestione Driver restituisce un errore se un'applicazione ODBC 3. *x* applicazione imposta *BufferLength* a SQL_SETPARAM_VALUE_MAX, un'applicazione ODBC 3. *x* driver può utilizzare per determinare quando viene chiamato da un'applicazione ODBC 1.0.  
  
> [!NOTE]  
>  Nella **SQLSetParam**, il modo in cui un'applicazione specifica la lunghezza di **ParameterValuePtr* memorizzare nel buffer in modo che il driver può restituire carattere o dati binari e il modo in cui un'applicazione invia un Matrice di caratteri o valori di parametro binario al driver, vengono definiti dal driver.  
  
## <a name="strlenorindptr-argument"></a>Argomento StrLen_or_IndPtr

 Il *StrLen_or_IndPtr* argomento punta a un buffer che, quando **SQLExecute** oppure **SQLExecDirect** viene chiamato, contiene uno dei valori seguenti. (Questo argomento consente di impostare i campi di record SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR degli indicatori di misura parametro application.)  
  
-   La lunghezza del valore del parametro archiviato in **ParameterValuePtr*. Viene ignorata eccetto character o binary di C.  
  
-   SQL_NTS. Il valore del parametro è una stringa con terminazione null.  
  
-   SQL_NULL_DATA. Il valore del parametro è NULL.  
  
-   SQL_DEFAULT_PARAM. Una procedura consiste nell'usare il valore predefinito di un parametro, anziché un valore recuperato dall'applicazione. Questo valore è valido solo in una routine denominata sintassi canonica ODBC e quindi solo se il *InputOutputType* argomento è SQL_PARAM_INPUT o SQL_PARAM_INPUT_OUTPUT SQL_PARAM_INPUT_OUTPUT_STREAM. Quando \* *StrLen_or_IndPtr* è SQL_DEFAULT_PARAM, il *ValueType*, *ParameterType*, *ColumnSize*,  *DecimalDigits*, *BufferLength*, e *ParameterValuePtr* argomenti vengono ignorati per i parametri di input e vengono usati solo per definire il valore del parametro di output per l'input / i parametri di output.  
  
-   Il risultato della finestra di SQL_LEN_DATA_AT_EXEC (*lunghezza*) (macro). Verranno inviati con i dati per il parametro **SQLPutData**. Se il *ParameterType* argomento SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo long, tipo di dati specifici dell'origine dati e il driver restituisce "Y" per il tipo di informazioni SQL_NEED_LONG_DATA_LEN in **SQLGetInfo**, *lunghezza* è il numero di byte di dati da inviare per il parametro; in caso contrario, *lunghezza* deve essere un valore non negativo e viene ignorato. Per altre informazioni, vedere "Passaggio di valori di parametro," più avanti in questa sezione.  
  
     Ad esempio, per specificare che 10.000 byte di dati verranno inviati con **SQLPutData** nelle chiamate a uno o più, per un parametro SQL_LONGVARCHAR, un'applicazione imposta **StrLen_or_IndPtr* su SQL_LEN_DATA_AT_EXEC ( 10000).  
  
-   SQL_DATA_AT_EXEC. Verranno inviati con i dati per il parametro **SQLPutData**. Questo valore viene utilizzato dalle applicazioni ODBC 1.0 quando chiamano ODBC 3. *x* driver. Per altre informazioni, vedere "Passaggio di valori di parametro," più avanti in questa sezione.  
  
 Se *StrLen_or_IndPtr* è un puntatore null, il driver presuppone che tutti i valori di parametro di input sono diversi da NULL e che i dati character e binary sono con terminazione null. Se *InputOutputType* è SQL_PARAM_OUTPUT o SQL_PARAM_OUTPUT_STREAM e *ParameterValuePtr* e *StrLen_or_IndPtr* sono entrambi puntatori null, le variabili Discard driver il valore di output.  
  
> [!NOTE]  
>  Sono fortemente sconsigliati dall'impostazione di un puntatore null per gli sviluppatori di applicazioni *StrLen_or_IndPtr* quando il tipo di dati del parametro è SQL_C_BINARY. Per assicurarsi che un driver non tronca inaspettatamente dati SQL_C_BINARY *StrLen_or_IndPtr* deve contenere un puntatore a un valore di lunghezza valida.  
  
 Se il *InputOutputType* argomento è SQL_PARAM_OUTPUT_STREAM, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_INPUT_OUTPUT *StrLen_or_IndPtr* punta a un buffer in cui il il driver restituisce SQL_NULL_DATA, il numero di byte disponibili per restituire \* *ParameterValuePtr* (escluso il byte di terminazione null di dati di tipo carattere,) o SQL_NO_TOTAL (se il numero di byte disponibili per return non può essere determinato). Se la procedura restituisce uno o più set di risultati, i **StrLen_or_IndPtr* buffer non è garantito a essere impostata fino a quando non sono stati recuperati tutti i risultati.  
  
 Se è maggiore di 1, il valore dell'attributo di istruzione SQL_ATTR_PARAMSET_SIZE *StrLen_or_IndPtr* punta a una matrice di valori SQLLEN. Questi può essere uno dei valori elencati in precedenza in questa sezione e vengono elaborati con un'unica istruzione SQL.  
  
## <a name="passing-parameter-values"></a>Passaggio di valori di parametro

 Un'applicazione può passare il valore per un parametro sia nel \* *ParameterValuePtr* buffer o con uno o più chiamate a **SQLPutData**. Parametri i cui dati vengono passati con **SQLPutData** sono detti *data-at-execution* parametri. Questi sono in genere usati per inviare dati per i parametri SQL_LONGVARBINARY e SQL_LONGVARCHAR e può essere combinati con altri parametri.  
  
 Per passare i valori dei parametri, un'applicazione esegue la sequenza di passaggi seguente:  
  
1.  Le chiamate **SQLBindParameter** per ogni parametro da associare i buffer per il valore del parametro (*ParameterValuePtr* argomento) e lunghezza/indicatore (*StrLen_or_IndPtr* argomento). Per i parametri data-at-execution *ParameterValuePtr* è un valore di puntatore definiti dall'applicazione, ad esempio un numero di parametro o un puntatore ai dati. Il valore verrà restituito in un secondo momento e può essere utilizzato per identificare il parametro.  
  
2.  Inserisce i valori per i parametri di input, input/output nel \* *ParameterValuePtr* e **StrLen_or_IndPtr* buffer:  
  
    -   Per i parametri normali, l'applicazione inserisce il valore del parametro nel \* *ParameterValuePtr* buffer e la lunghezza di tale valore nel **StrLen_or_IndPtr* buffer. Per altre informazioni, vedere [i valori dei parametri impostazione](../../../odbc/reference/develop-app/setting-parameter-values.md).  
  
    -   Per i parametri data-at-execution, l'applicazione inserisce il risultato della finestra di SQL_LEN_DATA_AT_EXEC (*lunghezza*) (macro) (quando si chiama un driver ODBC 2.0) nella **StrLen_or_IndPtr* buffer.  
  
3.  Le chiamate **SQLExecute** oppure **SQLExecDirect** per eseguire l'istruzione SQL.  
  
    -   Se non sono presenti parametri data-at-execution, il processo è stato completato.  
  
    -   Se sono presenti parametri data-at-execution, la funzione restituisce SQL_NEED_DATA.  
  
4.  Le chiamate **SQLParamData** per recuperare il valore definito dall'applicazione specificato nel *ParameterValuePtr* argomento del **SQLBindParameter** per la prima parametro data-at-execution da elaborare. **SQLParamData** restituisce SQL_NEED_DATA.  
  
    > [!NOTE]  
    >  Anche se i parametri data-at-execution sono simili alle colonne data-at-execution, il valore restituito da **SQLParamData** è diverso per ognuno. I parametri data-at-execution sono parametri in un'istruzione SQL per il quale i dati verranno inviati con **SQLPutData** quando viene eseguita l'istruzione con **SQLExecDirect** o **SQLExecute**. Sono associate con **SQLBindParameter**. Il valore restituito da **SQLParamData** viene passato un valore del puntatore al **SQLBindParameter** nel *ParameterValuePtr* argomento. Le colonne data-at-execution sono colonne in un set di righe per cui i dati verranno inviati con **SQLPutData** quando viene aggiornata o aggiunto con una riga **SQLBulkOperations** o aggiornate con **SQLSetPos**. Sono associate con **SQLBindCol**. Il valore restituito da **SQLParamData** è l'indirizzo della riga di **TargetValuePtr* buffer (impostata da una chiamata a **SQLBindCol**) che viene elaborata.  
  
5.  Le chiamate **SQLPutData** uno o più volte per inviare i dati per il parametro. Più di una chiamata è necessario se il valore dei dati è maggiore di \* *ParameterValuePtr* specificato nel buffer **SQLPutData**; più chiamate al metodo **SQLPutData**per lo stesso parametro sono consentiti solo quando si inviano dati di tipo carattere C a una colonna con un tipo di carattere, binary o dati specifici dell'origine dati o per l'invio di dati C binari a una colonna con un carattere, binario, o del tipo di dati specifici dell'origine dati.  
  
6.  Le chiamate **SQLParamData** nuovamente per segnalare che tutti i dati sono stati inviati per il parametro.  
  
    -   Se sono presenti più parametri data-at-execution, **SQLParamData** restituisce SQL_NEED_DATA e il valore definito dall'applicazione per il parametro data-at-execution successivo da elaborare. L'applicazione si ripete i passaggi 4 e 5.  
  
    -   Se sono presenti parametri data-at-execution non sono più, il processo è stato completato. Se l'istruzione è stata eseguita correttamente, **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; se l'esecuzione non riesce, viene restituito SQL_ERROR. A questo punto **SQLParamData** può restituire qualsiasi valore SQLSTATE che può essere restituiti dalla funzione che viene usata per eseguire l'istruzione (**SQLExecDirect** oppure **SQLExecute**).  
  
         I valori di output per i parametri di input/output o di output sono disponibili nel \* *ParameterValuePtr* e **StrLen_or_IndPtr* memorizza nel buffer dopo l'applicazione recupera tutti i set di risultati generato dall'istruzione.  
  
 La chiamata **SQLExecute** oppure **SQLExecDirect** inserisce l'istruzione in uno stato SQL_NEED_DATA. A questo punto, l'applicazione può chiamare solo **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**, o **SQLPutData** con l'istruzione o il *handle di connessione* associate all'istruzione. Se chiama qualsiasi altra funzione con l'istruzione o la connessione associata all'istruzione, la funzione restituisce SQLSTATE HY010 (funzione di errore nella sequenza). Lascia l'istruzione di SQL_NEED_DATA stato quando **SQLParamData** oppure **SQLPutData** restituisce un errore **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, o l'istruzione viene annullata.  
  
 Se l'applicazione chiama **SQLCancel** mentre il driver deve comunque i dati per i parametri data-at-execution, il driver Annulla l'esecuzione dell'istruzione, l'applicazione può quindi chiamare **SQLExecute** o **SQLExecDirect** nuovamente.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recupero di parametri di Output inviati come flusso

 Quando un'applicazione imposta *InputOutputType* SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_OUTPUT_STREAM, il valore del parametro di output deve essere recuperato da una o più chiamate a **SQLGetData**. Quando il driver ha un valore di parametro di output inviati come flusso da restituire all'applicazione, verrà restituito SQL_PARAM_DATA_AVAILABLE in risposta a una chiamata alle funzioni seguenti: **SQLMoreResults**, **SQLExecute**, e **SQLExecDirect**. Un'applicazione chiama **SQLParamData** per determinare quale valore del parametro è disponibile.  
  
 Per altre informazioni sui parametri di output inviati come flusso e SQL_PARAM_DATA_AVAILABLE, vedere [recupero di parametri di Output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-arrays-of-parameters"></a>Uso delle matrici di parametri

 Quando un'applicazione viene preparata un'istruzione con marcatori di parametro e passa una matrice di parametri, esistono due modi diversi, che questo può essere eseguito. Un modo consiste perché il driver si basano sulle funzionalità di elaborazione di matrici dei back-end, in cui l'intera istruzione con la matrice di parametri di case viene trattato come un'unica unità atomica. Oracle è un esempio di un'origine dati che supporta le funzionalità di elaborazione di matrice. Un altro modo per implementare questa funzionalità è per il driver genera un batch di istruzioni SQL, una sola istruzione SQL per ogni set di parametri nella matrice del parametro, ed eseguire il batch. Matrici di parametri non possono essere usate con un **WHERE CURRENT OF di aggiornamento** istruzione.  
  
 Quando viene elaborata una matrice di parametri, i conteggi di riga/set di risultati singolo (uno per ogni set di parametri) possono essere disponibili o i conteggi di righe/set di risultati possono essere eseguiti in un unico. Opzione il SQL_PARAM_ARRAY_ROW_COUNTS **SQLGetInfo** indica se sono disponibili per ogni set di parametri (SQL_PARC_BATCH) i conteggi delle righe o conteggio delle righe solo uno è disponibile (SQL_PARC_NO_BATCH).  
  
 Opzione il SQL_PARAM_ARRAY_SELECTS **SQLGetInfo** indica se un set di risultati è disponibile per ogni set di parametri (SQL_PAS_BATCH) o solo un set di risultati è disponibile (SQL_PAS_NO_BATCH). Se il driver non supporta un'istruzione di generazione di set di risultati deve essere eseguito con una matrice di parametri, SQL_PARAM_ARRAY_SELECTS restituisce SQL_PAS_NO_SELECT.  
  
 Per altre informazioni, vedere [funzione SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 Per supportare le matrici di parametri, specificare il numero di valori per ogni parametro è impostato l'attributo di istruzione SQL_ATTR_PARAMSET_SIZE. Se il campo è maggiore di 1, i campi SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR di APD devono puntare alle matrici. La cardinalità di ogni matrice è uguale al valore di SQL_ATTR_PARAMSET_SIZE.  
  
 Il campo SQL_DESC_ROWS_PROCESSED_PTR di APD punta a un buffer che contiene il numero di set di parametri che sono stati elaborati, compresi i set di errore. Mentre viene elaborato ogni set di parametri, il driver archivia un nuovo valore nel buffer. Non verrà restituito alcun numero se si tratta di un puntatore null. Quando si utilizzano matrici di parametri, il valore a cui punta il campo SQL_DESC_ROWS_PROCESSED_PTR di APD viene popolato anche se viene restituito SQL_ERROR dalla funzione di impostazione. Se viene restituito SQL_NEED_DATA, il valore a cui punta il campo SQL_DESC_ROWS_PROCESSED_PTR di APD è impostato per il set di parametri in fase di elaborazione.  
  
 Che cosa si verifica quando è associata una matrice di parametri e un **WHERE CURRENT OF di aggiornamento** istruzione è definito dal driver.  
  
## <a name="column-wise-parameter-binding"></a>L'associazione di parametri

 Nell'associazione per colonna, l'applicazione associa il parametro separato e le matrici di lunghezza/indicatore a ogni parametro.  
  
 Per utilizzare l'associazione, l'applicazione imposta innanzitutto l'attributo di istruzione SQL_ATTR_PARAM_BIND_TYPE su SQL_PARAM_BIND_BY_COLUMN. (Questo è il valore predefinito). Per ogni colonna deve essere associato, l'applicazione esegue i passaggi seguenti:  
  
1.  Alloca una matrice di buffer di parametri.  
  
2.  Alloca una matrice di buffer di lunghezza/indicatore.  
  
    > [!NOTE]  
    >  Se l'applicazione scrive direttamente i descrittori quando viene utilizzata l'associazione per colonna, matrici distinte è utilizzabile per i dati di lunghezza e indicatore.  
  
3.  Le chiamate **SQLBindParameter** con gli argomenti seguenti:  
  
    -   *ValueType* è il tipo C di un singolo elemento nella matrice di buffer del parametro.  
  
    -   *ParameterType* è il tipo SQL del parametro.  
  
    -   *ParameterValuePtr* è l'indirizzo della matrice di buffer del parametro.  
  
    -   *BufferLength* è la dimensione di un singolo elemento nella matrice di buffer del parametro. Il *BufferLength* argomento viene ignorato quando i dati sono dati a lunghezza fissa.  
  
    -   *StrLen_or_IndPtr* è l'indirizzo della matrice di lunghezza/indicatore.  
  
 Per altre informazioni sull'utilizzo di queste informazioni, vedere "ParameterValuePtr argomento" in "Commenti", più avanti in questa sezione. Per altre informazioni sull'associazione per colonna di parametri, vedere [matrici di parametri di associazione](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="row-wise-parameter-binding"></a>L'associazione dei parametri

 Nell'associazione per riga, l'applicazione definisce una struttura che contiene i parametri e lunghezza/indicatore buffer per ogni parametro deve essere associato.  
  
 Per usare l'associazione per riga, l'applicazione esegue i passaggi seguenti:  
  
1.  Definisce una struttura per contenere un singolo set di parametri (inclusi i buffer di lunghezza/indicatore sia parametro) e alloca una matrice di queste strutture.  
  
    > [!NOTE]  
    >  Se l'applicazione scrive direttamente i descrittori quando viene utilizzata l'associazione per riga, è possono utilizzare campi separati per i dati di lunghezza e indicatore.  
  
2.  Imposta l'attributo di istruzione SQL_ATTR_PARAM_BIND_TYPE sulla dimensione della struttura che contiene un singolo set di parametri o alle dimensioni di un'istanza di un buffer in cui verranno associati i parametri. La lunghezza deve includere lo spazio per tutti i parametri associati ed eventuale riempimento della struttura o del buffer, per assicurarsi che quando l'indirizzo di un parametro associato viene incrementato con la lunghezza specificata, il risultato punterà all'inizio del parametro stesso nel riga successiva. Quando si usa la *sizeof* operatore in ANSI C, questo comportamento è garantito.  
  
3.  Le chiamate **SQLBindParameter** con gli argomenti seguenti per ogni parametro deve essere associato:  
  
    -   *ValueType* è il tipo del membro buffer del parametro da associare alla colonna.  
  
    -   *ParameterType* è il tipo SQL del parametro.  
  
    -   *ParameterValuePtr* è l'indirizzo del membro nel primo elemento della matrice buffer parametro.  
  
    -   *BufferLength* è la dimensione del membro di buffer del parametro.  
  
    -   *StrLen_or_IndPtr* è l'indirizzo del membro lunghezza/indicatore da associare.  
  
 Per altre informazioni sull'utilizzo di queste informazioni, vedere "*ParameterValuePtr* argomento," più avanti in questa sezione. Per altre informazioni sull'associazione per riga di parametri, vedere la [matrici di parametri di associazione](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="error-information"></a>Informazioni sull'errore

 Se un driver non implementa le matrici di parametri come batch (l'opzione SQL_PARAM_ARRAY_ROW_COUNTS è uguale a SQL_PARC_NO_BATCH), situazioni di errore vengono gestiti come se venisse eseguita un'istruzione. Se il driver implementa le matrici di parametri come batch, un'applicazione può usare il campo di intestazione SQL_DESC_ARRAY_STATUS_PTR dell'IPD per determinare quale parametro di un'istruzione SQL o ha causato il parametro in una matrice di parametri  **SQLExecDirect** oppure **SQLExecute** per restituire un errore. Questo campo contiene informazioni sullo stato per ogni riga di valori di parametro. Se il campo indica che si è verificato un errore, i campi nella struttura di dati di diagnostica indicherà il numero di riga e di parametro del parametro che non è riuscita. Verrà definito il numero di elementi nella matrice dal campo di intestazione SQL_DESC_ARRAY_SIZE in APD, che può essere impostato dall'attributo SQL_ATTR_PARAMSET_SIZE istruzione.  
  
> [!NOTE]  
>  Il campo di intestazione SQL_DESC_ARRAY_STATUS_PTR in APD viene utilizzato per ignorare i parametri. Per altre informazioni su come ignorare i parametri, vedere la sezione successiva, "Verrà ignorato un Set di parametri".  
  
 Quando **SQLExecute** oppure **SQLExecDirect** restituisce SQL_ERROR, gli elementi nella matrice a cui punta il campo SQL_DESC_ARRAY_STATUS_PTR in IPD conterrà SQL _ SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, PARAM_SUCCESS_WITH_INFO SQL_PARAM_UNUSED o SQL_PARAM_DIAG_UNAVAILABLE.  
  
 Per ogni elemento nella matrice, la struttura di dati di diagnostica contiene uno o più record di stato. Il campo SQL_DIAG_ROW_NUMBER della struttura indica il numero di riga dei valori di parametro che ha causato l'errore. Se è possibile determinare il parametro specifico in una riga di parametri che ha causato l'errore, il numero di parametro verrà immesso nel campo SQL_DIAG_COLUMN_NUMBER.  
  
 SQL_PARAM_UNUSED viene immesso quando un parametro non è stato utilizzato perché si è verificato un errore in un parametro precedente che imposto **SQLExecute** oppure **SQLExecDirect** da interrompere. Ad esempio, se sono presenti 50 parametri e un errore durante l'esecuzione il set di parametri che ha causato fortieth **SQLExecute** o **SQLExecDirect** per interrompere, quindi SQL_PARAM_UNUSED immesso di Matrice di stato per i parametri di 41 e 50.  
  
 SQL_PARAM_DIAG_UNAVAILABLE viene immesso quando il driver considera le matrici di parametri come unità monolitico, in modo che non genera questo livello di singolo parametro di informazioni sull'errore.  
  
 Alcuni errori durante l'elaborazione di un singolo set di parametri causano l'elaborazione dei set di parametri successivi nella matrice da arrestare. Altri errori non influenzano l'elaborazione dei parametri successivi. Quali errori interromperà l'elaborazione viene definito dal driver. Se l'elaborazione non è stata arrestata, vengono elaborati tutti i parametri nella matrice, viene restituito SQL_SUCCESS_WITH_INFO come risultato l'errore e il buffer definito da SQL_ATTR_PARAMS_PROCESSED_PTR viene impostato per il numero totale di set di parametri elaborati (come definito per il Attributo di istruzione SQL_ATTR_PARAMSET_SIZE), che include set di errore.  
  
> [!CAUTION]  
>  Comportamento ODBC quando si verifica un errore durante l'elaborazione di una matrice di parametri è diverso in ODBC 3. *x* da quella di ODBC 2. *x*. In ODBC 2. *x*, la funzione ha restituito SQL_ERROR e l'elaborazione non siano più state. Il buffer a cui fa riferimento il *pirow* argomento di **SQLParamOptions** contiene il numero della riga di errore. In ODBC 3. *x*, la funzione restituisce SQL_SUCCESS_WITH_INFO e l'elaborazione di maggio sia arrestato o continuare. Se il problema persiste, il buffer specificato da SQL_ATTR_PARAMS_PROCESSED_PTR imposterà sul valore di tutti i parametri elaborati, inclusi quelli che hanno generato un errore. Questa modifica nel comportamento può causare problemi per le applicazioni esistenti.  
  
 Quando **SQLExecute** oppure **SQLExecDirect** restituisce prima di completare l'elaborazione di tutti i set di parametri in una matrice di parametri, ad esempio quando viene restituito SQL_ERROR o SQL_NEED_DATA, contiene la matrice di stato stati per i parametri che sono già stati elaborati. Il percorso a cui punta il campo SQL_DESC_ROWS_PROCESSED_PTR in IPD contiene il numero di riga nella matrice del parametro che ha causato il codice di errore SQL_ERROR o SQL_NEED_DATA. Quando una matrice di parametri viene inviata a un'istruzione SELECT, la disponibilità di matrice di valori di stato è definito dal driver; che potrebbero essere disponibili dopo l'istruzione è stata eseguita o come risultato vengono recuperati i set.  
  
## <a name="ignoring-a-set-of-parameters"></a>Ignorando un Set di parametri

 Il campo SQL_DESC_ARRAY_STATUS_PTR di APD (come impostato nell'attributo di istruzione SQL_ATTR_PARAM_STATUS_PTR) può essere utilizzato per indicare che un set di parametri associati in un'istruzione SQL deve essere ignorato. Per impostare il driver per ignorare uno o più set di parametri durante l'esecuzione, un'applicazione deve seguire questi passaggi:  
  
1.  Chiamare **SQLSetDescField** per impostare il campo di intestazione SQL_DESC_ARRAY_STATUS_PTR di APD in modo che punti a una matrice di valori SQLUSMALLINT per contenere le informazioni sullo stato. Questo campo può essere impostato anche chiamando **SQLSetStmtAttr** con un *attributo* di SQL_ATTR_PARAM_OPERATION_PTR, che consente a un'applicazione impostare il campo senza ottenere un handle di descrittore.  
  
2.  Impostare ogni elemento della matrice definita nel campo SQL_DESC_ARRAY_STATUS_PTR di APD su uno dei due valori:  
  
    -   SQL_PARAM_IGNORE, per indicare che la riga è stata esclusa dall'esecuzione dell'istruzione.  
  
    -   SQL_PARAM_PROCEED, per indicare che la riga è inclusa nell'esecuzione dell'istruzione.  
  
3.  Chiamare **SQLExecDirect** oppure **SQLExecute** per eseguire l'istruzione preparata.  
  
 Le regole seguenti si applicano alla matrice definita nel campo SQL_DESC_ARRAY_STATUS_PTR di APD:  
  
-   Il puntatore viene impostato su null per impostazione predefinita.  
  
-   Se il puntatore è null, vengono utilizzati tutti i set di parametri, come se tutti gli elementi impostati per SQL_ROW_PROCEED.  
  
-   L'impostazione di un elemento a SQL_PARAM_PROCEED non garantisce che l'operazione utilizzerà quel particolare set di parametri.  
  
-   SQL_PARAM_PROCEED è definito come 0 nel file di intestazione.  
  
 Un'applicazione può impostare SQL_DESC_ARRAY_STATUS_PTR campo in APD in modo che punti allo stesso array come puntato dal campo SQL_DESC_ARRAY_STATUS_PTR nell'implementazione. Ciò è utile quando si associano parametri per i dati di riga. I parametri possono quindi essere ignorati in base allo stato della riga di dati. Oltre a SQL_PARAM_IGNORE, i codici seguenti causano un parametro in un'istruzione SQL da ignorare: SQL_ROW_DELETED SQL_ROW_UPDATED e SQL_ROW_ERROR. Oltre a SQL_PARAM_PROCEED, i codici seguenti causano un'istruzione SQL continuare: SQL_ROW_SUCCESS SQL_ROW_SUCCESS_WITH_INFO e SQL_ROW_ADDED.  
  
## <a name="rebinding-parameters"></a>Riassociazione di parametri

 Un'applicazione può eseguire una delle due operazioni per modificare un'associazione:  
  
-   Chiamare **SQLBindParameter** per specificare un nuovo binding per una colonna in cui è già associato. Il driver sovrascrive il binding precedente con quello nuovo.  
  
-   Specificare un offset da aggiungere per l'indirizzo del buffer specificato dalla chiamata all'associazione **SQLBindParameter**. Per altre informazioni, vedere la sezione successiva, "Riassociazione con offset".  
  
## <a name="rebinding-with-offsets"></a>Riassociazione con offset

 La riassociazione dei parametri è particolarmente utile quando un'applicazione ha una configurazione di area del buffer che può contenere numerosi parametri ma una chiamata a **SQLExecDirect** oppure **SQLExecute** Usa solo alcuni dei parametri. Lo spazio rimanente nell'area del buffer è utilizzabile per il successivo set di parametri modificando il binding esistente da un offset.  
  
 Il campo di intestazione SQL_DESC_BIND_OFFSET_PTR in APD punta all'offset di associazione. Se il campo è diverso da null, il driver Dereferenzia il puntatore e, se nessuno dei valori nei campi SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR è un puntatore null, aggiunge il valore dereferenziato a tali campi del descrittore record in fase di esecuzione. I nuovi valori di puntatore vengono utilizzati quando vengono eseguite le istruzioni SQL. L'offset resta valido dopo la riassociazione. Poiché SQL_DESC_BIND_OFFSET_PTR è un puntatore per l'offset anziché la differenza di se stesso, un'applicazione modificabili offset direttamente, senza necessità di chiamare [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) oppure [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) a modificare il campo di descrizione. Il puntatore viene impostato su null per impostazione predefinita. Il campo SQL_DESC_BIND_OFFSET_PTR del ARD può essere impostato da una chiamata a [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) o da una chiamata a [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)con un *fAttribute* di SQL_ATTR_PARAM_BIND_ OFFSET_PTR.  
  
 L'offset di associazione è sempre stato aggiunto direttamente i valori nei campi SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR. Se l'offset viene modificato in un valore diverso, il nuovo valore viene ancora aggiunto direttamente al valore in ogni campo del descrittore. Nuovo offset non viene aggiunta alla somma di tutti gli offset precedenti e il valore del campo.  
  
## <a name="descriptors"></a>Descrittori

 Modo in cui è associato un parametro è determinato dai campi della Apd e gli IDP. Gli argomenti **SQLBindParameter** vengono usate per impostare i campi di descrizione. I campi possono essere impostati anche **SQLSetDescField** funzioni, sebbene **SQLBindParameter** è più efficiente l'utilizzo in quanto l'applicazione non è necessario ottenere un handle descrittore per chiamare **SQLBindParameter**.  
  
> [!CAUTION]  
>  La chiamata **SQLBindParameter** per un'unica istruzione può influire sulle altre istruzioni. Ciò si verifica quando il ARD associate all'istruzione viene allocato in modo esplicito ed è anche associato con le altre istruzioni. In quanto **SQLBindParameter** modifica campi del APD, le modifiche verranno applicate a tutte le istruzioni a cui è associato questo descrittore. Se questo non è il comportamento richiesto, l'applicazione deve annullare l'associazione di questo descrittore da altre istruzioni prima di chiamare **SQLBindParameter**.  
  
 Concettualmente **SQLBindParameter** esegue i passaggi seguenti in sequenza:  
  
1.  Le chiamate [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) per ottenere l'handle APD.  
  
2.  Le chiamate [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) ottenere campo SQL_DESC_COUNT dell'APD e se il valore delle *ColumnNumber* argomento supera il valore di SQL_DESC_COUNT, chiamate **SQLSetDescField**aumentare il valore di SQL_DESC_COUNT al *ColumnNumber*.  
  
3.  Le chiamate [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) più volte per assegnare valori ai campi di APD seguenti:  
  
    -   Imposta il valore di SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE *ValueType*, ad eccezione del fatto che se *ValueType* è uno degli identificatori concisi di un sottotipo di datetime o intervallo, imposta SQL_DESC_TYPE SQL _ Data/ora o SQL_INTERVAL, rispettivamente, imposta SQL_DESC_CONCISE_TYPE all'identificatore concisa e imposta SQL_DESC_DATETIME_INTERVAL_CODE datetime corrispondente o il codice secondario dell'intervallo.  
  
    -   Imposta sul valore del campo SQL_DESC_OCTET_LENGTH *BufferLength*.  
  
    -   Imposta sul valore del campo SQL_DESC_DATA_PTR *ParameterValue*.  
  
    -   Imposta sul valore del campo SQL_DESC_OCTET_LENGTH_PTR *StrLen_or_Ind*.  
  
    -   Imposta il campo SQL_DESC_INDICATOR_PTR anche al valore di *StrLen_or_Ind*.  
  
     Il *StrLen_or_Ind* parametro specifica le informazioni sugli indicatori sia la lunghezza del valore del parametro.  
  
4.  Le chiamate [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) per ottenere l'handle IPD.  
  
5.  Le chiamate [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) ottenere campo SQL_DESC_COUNT dell'IPD e se il valore delle *ColumnNumber* argomento supera il valore di SQL_DESC_COUNT, chiamate **SQLSetDescField**aumentare il valore di SQL_DESC_COUNT al *ColumnNumber*.  
  
6.  Le chiamate [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) più volte per assegnare valori ai campi seguenti dell'IPD:  
  
    -   Imposta il valore di SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE *ParameterType*, ad eccezione del fatto che se *ParameterType* è uno degli identificatori concisi di un sottotipo di datetime o intervallo, imposta SQL_DESC_TYPE SQL_DATETIME o SQL_INTERVAL, rispettivamente, imposta SQL_DESC_CONCISE_TYPE l'identificatore conciso, e i set SQL_DESC_DATETIME_INTERVAL_CODE alla data/ora corrispondente o sottocodice intervallo.  
  
    -   Imposta come appropriato per uno o più dei SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION e SQL_DESC_LENGTH *ParameterType*.  
  
    -   Imposta il valore di SQL_DESC_SCALE *DecimalDigits*.  
  
 Se la chiamata a **SQLBindParameter** ha esito negativo, il contenuto dei campi di descrizione che sarebbe impostato in APD sono definiti e il campo SQL_DESC_COUNT di APD rimane invariato. Inoltre, i campi SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_TYPE del record appropriati in IPD sono definiti e il campo SQL_DESC_COUNT dell'IPD rimane invariato.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>Conversione delle chiamate da e verso SQLSetParam

 Quando un'applicazione ODBC 1.0 chiama **SQLSetParam** in un'applicazione ODBC 3. *x* driver ODBC 3. *x* gestione Driver esegue il mapping di chiamata, come illustrato nella tabella seguente.  
  
|Chiamata dall'applicazione ODBC 1.0|Chiamate ODBC 3. *x* driver|  
|----------------------------------|-------------------------------|  
|SQLSetParam(      StatementHandle,      ParameterNumber,      ValueType,      ParameterType,      LengthPrecision,      ParameterScale,      ParameterValuePtr,      StrLen_or_IndPtr);|SQLBindParameter (StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType *ColumnSize*, *DecimalDigits*, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX,      StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, un'applicazione viene preparata un'istruzione SQL per inserire dati nella tabella ORDERS. Per ogni parametro nell'istruzione, l'applicazione chiama **SQLBindParameter** per specificare il tipo di dati C ODBC e il tipo di dati SQL del parametro e per associare un buffer per ogni parametro. Per ogni riga di dati, l'applicazione assegna i valori dei dati per ogni parametro e chiama **SQLExecute** per eseguire l'istruzione.  
  
 L'esempio seguente si presuppone la presenza di un'origine dati ODBC nel computer denominato Northwind che viene associato al database Northwind.  
  
 Per altri esempi di codice, vedere [funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [funzione SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md), [funzione SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), e [SQLSetPos funzione](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp
// SQLBindParameter_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define EMPLOYEE_ID_LEN 10  
  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLSMALLINT sCustID;  
  
SQLCHAR szEmployeeID[EMPLOYEE_ID_LEN];  
SQL_DATE_STRUCT dsOrderDate;  
SQLINTEGER cbCustID = 0, cbOrderDate = 0, cbEmployeeID = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, EMPLOYEE_ID_LEN, 0, szEmployeeID, 0, &cbEmployeeID);  
   retcode = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sCustID, 0, &cbCustID);  
   retcode = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TIMESTAMP, sizeof(dsOrderDate), 0, &dsOrderDate, 0, &cbOrderDate);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"INSERT INTO Orders(CustomerID, EmployeeID, OrderDate) VALUES (?, ?, ?)", SQL_NTS);  
  
   strcpy_s((char*)szEmployeeID, _countof(szEmployeeID), "BERGS");  
   sCustID = 5;  
   dsOrderDate.year = 2006;  
   dsOrderDate.month = 3;  
   dsOrderDate.day = 17;  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="code-example"></a>Esempio di codice

 Nell'esempio seguente, un'applicazione esegue una stored procedure SQL Server usando un parametro denominato.  
  
```cpp
// SQLBindParameter_Function_2.cpp  
// compile with: ODBC32.lib  
// sample assumes the following stored procedure:  
// use northwind  
// DROP PROCEDURE SQLBindParameter  
// GO  
//   
// CREATE PROCEDURE SQLBindParameter @quote int  
// AS  
// delete from orders where OrderID >= @quote  
// GO  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
SQLHDESC hIpd = NULL;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLCHAR szQuote[50] = "100084";  
SQLINTEGER cbValue = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"{call SQLBindParameter(?)}", SQL_NTS);  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 50, 0, szQuote, 0, &cbValue);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
   retcode = SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituzione di informazioni su un parametro in un'istruzione|[Funzione SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Esecuzione di un'istruzione SQL|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Il buffer di parametri nell'istruzione di rilascio|[Funzione SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Restituzione del numero di parametri dell'istruzione|[Funzione SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|Restituisce il parametro successivo per l'invio di dati|[Funzione SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Specifica di più valori di parametro|[Funzione SQLParamOptions](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|L'invio dei dati di parametro in fase di esecuzione|[Funzione SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Vedere anche

 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recupero di parametri di output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
