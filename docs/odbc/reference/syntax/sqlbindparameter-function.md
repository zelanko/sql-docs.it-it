---
title: Funzione SQLBindParameter . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02f50862bcfb0295c7f098afc6856c91e0249f66
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301361"
---
# <a name="sqlbindparameter-function"></a>Pagina relativa alla funzione SQLBindParameter

**Conformità**  
 Versione introdotta: ODBC 2.0 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLBindParameter** associa un buffer a un marcatore di parametro in un'istruzione SQL. **SQLBindParameter** supporta l'associazione a un tipo di dati Unicode C, anche se il driver sottostante non supporta i dati Unicode.SQLBindParameter supports binding to a Unicode C data type, even if the underlying driver does not support Unicode data.  
  
> [!NOTE]  
>  Questa funzione sostituisce la funzione ODBC 1.0 **SQLSetParam**. Per ulteriori informazioni, vedere "Commenti".  
  
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
 [Ingresso] Handle di istruzione.  
  
 *NumeroParametro*  
 [Ingresso] Numero di parametro, ordinato in sequenza nell'ordine crescente dei parametri, a partire da 1.  
  
 *InputOutputType*  
 [Ingresso] Tipo del parametro. Per ulteriori informazioni, vedere *"Argomento InputOutputType"* in "Commenti".  
  
 *Valuetype*  
 [Ingresso] Tipo di dati C del parametro. Per ulteriori informazioni, vedere "Argomento*ValueType"* in "Commenti".  
  
 *Parametertype*  
 [Ingresso] Tipo di dati SQL del parametro. Per ulteriori informazioni, vedere "Argomento*ParameterType"* in "Commenti".  
  
 *ColumnSize*  
 [Ingresso] Dimensione della colonna o dell'espressione dell'indicatore di parametro corrispondente. Per ulteriori informazioni, vedere "Argomento*ColumnSize"* in "Commenti".  
  
 Se l'applicazione verrà eseguita in un sistema operativo Windows a 64 bit, vedere [Informazioni a 64 bit ODBC](../../../odbc/reference/odbc-64-bit-information.md).  
  
 *DecimalDigits*  
 [Ingresso] Cifre decimali della colonna o dell'espressione del marcatore di parametro corrispondente. Per ulteriori informazioni sulle dimensioni delle colonne, vedere [Dimensioni colonna, Cifre decimali, Lunghezza ottetto di trasferimento e Dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *ParameterValuePtr*  
 [Ingresso posticipato] Puntatore a un buffer per i dati del parametro. Per ulteriori informazioni, vedere "Argomento*ParameterValuePtr"* in "Commenti".  
  
 *BufferLength*  
 [Ingresso/Uscita] Lunghezza del buffer *ParameterValuePtr* in byte. Per ulteriori informazioni, vedere "Argomento*BufferLength"* in "Commenti".  
  
 Vedere [Informazioni a 64 bit ODBC](../../../odbc/reference/odbc-64-bit-information.md), se l'applicazione verrà eseguita in un sistema operativo a 64 bit.  
  
 *StrLen_or_IndPtr*  
 [Ingresso posticipato] Puntatore a un buffer per la lunghezza del parametro. Per ulteriori informazioni, vedere *"argomento StrLen_or_IndPtr"* in "Commenti".  
  
## <a name="returns"></a>Valori di codice restituiti

 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica

 Quando **SQLBindParameter** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLBindParameter** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  

|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07006|Violazione dell'attributo del tipo di dati con restrizioniRestricted data type attribute violation|Il tipo di dati identificato dall'argomento *ValueType* non può essere convertito nel tipo di dati identificato dall'argomento *ParameterType.* Si noti che questo errore può essere restituito da **SQLExecDirect**, **SQLExecute**o **SQLPutData** in fase di esecuzione, anziché da **SQLBindParameter**.|  
|07009|Indice descrittore non valido|(DM) il valore specificato per l'argomento *NumeroParametro* è minore di 1.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY003|Tipo di buffer dell'applicazione non valido|Il valore specificato dall'argomento *ValueType* non è un tipo di dati C valido o un SQL_C_DEFAULT.|  
|HY004|Tipo di dati SQL non valido|Il valore specificato per l'argomento *ParameterType* non è né un identificatore del tipo di dati SQL ODBC valido né un identificatore del tipo di dati SQL specifico del driver supportato dal driver.|  
|I009|Valore argomento non valido|(DM) l'argomento *ParameterValuePtr* era un puntatore null, l'argomento *StrLen_or_IndPtr* un puntatore null e l'argomento *InputOutputType* non è SQL_PARAM_OUTPUT.<br /><br /> (DM) SQL_PARAM_OUTPUT, in cui l'argomento *ParameterValuePtr* era un puntatore null, il tipo C era char o binario e BufferLength (*cbValueMax*) era maggiore di 0.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando **SQLBindParameter** è stato chiamato.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono è stata chiamata per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I021|Informazioni sul descrittore incoerenti|Le informazioni sul descrittore controllate durante una verifica di coerenza non erano coerenti. Vedere la sezione "Controlli di coerenza" in **SQLSetDescField.**<br /><br /> Il valore specificato per l'argomento *DecimalDigits* non è compreso nell'intervallo di valori supportati dall'origine dati per una colonna del tipo di dati SQL specificato dall'argomento *ParameterType.*|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore in *BufferLength* era minore di 0. Vedere la descrizione del campo SQL_DESC_DATA_PTR in **SQLSetDescField**.|  
|I104|Precisione o valore di scala non valido|Il valore specificato per l'argomento *ColumnSize* o *DecimalDigits* non è compreso nell'intervallo di valori supportati dall'origine dati per una colonna del tipo di dati SQL specificato dall'argomento *ParameterType.*|  
|HY105|Tipo di parametro non valido|(DM) il valore specificato per l'argomento *InputOutputType* non valido. (Vedere "Commenti").")|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il driver o l'origine dati non supporta la conversione specificata dalla combinazione del valore specificato per l'argomento *ValueType* e del valore specifico del driver specificato per l'argomento *ParameterType*.<br /><br /> Il valore specificato per l'argomento *ParameterType* è un identificatore di tipo di dati SQL ODBC valido per la versione di ODBC supportata dal driver, ma non è supportato dal driver o dall'origine dati.<br /><br /> Il driver supporta solo ODBC 2. *x* e l'argomento *ValueType* è uno dei seguenti:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e tutti i tipi di dati di intervallo C elencati in [Tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) nell'Appendice D: Tipi di dati.<br /><br /> Il driver supporta solo le versioni ODBC precedenti alla 3.50 e l'argomento *ValueType* è stato SQL_C_GUID.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti

 Un'applicazione chiama **SQLBindParameter** per associare ogni indicatore di parametro in un'istruzione SQL. Le associazioni rimangono attive fino a quando l'applicazione chiama nuovamente **SQLBindParameter,** chiama **SQLFreeStmt** con l'opzione SQL_RESET_PARAMS o **chiama SQLSetDescField** per impostare il campo di intestazione SQL_DESC_COUNT di APD su 0.  
  
 Per ulteriori informazioni sui parametri, vedere [Parametri dell'istruzione](../../../odbc/reference/develop-app/statement-parameters.md). Per altre informazioni sui tipi di dati dei parametri e sugli indicatori di parametro, vedere Tipi di [dati](../../../odbc/reference/appendixes/parameter-data-types.md) dei parametri e Indicatori di [parametro](../../../odbc/reference/appendixes/parameter-markers.md) nell'Appendice C: Grammatica SQL.  
  
## <a name="parameternumber-argument"></a>Argomento ParameterNumber  
 Se *ParameterNumber* nella chiamata a **SQLBindParameter** è maggiore del valore di SQL_DESC_COUNT, **SQLSetDescField** viene chiamato per aumentare il valore di SQL_DESC_COUNT a *ParameterNumber*.  
  
## <a name="inputoutputtype-argument"></a>Argomento InputOutputType  
 L'argomento *InputOutputType* specifica il tipo del parametro. Questo argomento imposta il campo SQL_DESC_PARAMETER_TYPE dell'IPD. Tutti i parametri nelle istruzioni SQL che non chiamano procedure, ad esempio le istruzioni **INSERT,** sono *input , parametri*. I parametri nelle chiamate di routine possono essere parametri di input, input/output o output. Un'applicazione chiama **SQLProcedureColumns** per determinare il tipo di un parametro in una chiamata di routine; i parametri il cui tipo non può essere determinato vengono considerati parametri di input.  
  
 L'argomento *InputOutputType* è rappresentato da uno dei valori seguenti:  
  
-   SQL_PARAM_INPUT. Il parametro contrassegna un parametro in un'istruzione SQL che non chiama una routine, ad esempio un'istruzione **INSERT,** o contrassegna un parametro di input in una routine. Ad esempio, i parametri in **INSERT INTO Employee VALUES (?, ?, ?)** sono parametri di input, mentre i parametri in , che richiedono la chiamata **AddEmp (?, ?, ?)** possono essere, ma non necessariamente, parametri di input.  
  
     Quando viene eseguita l'istruzione, il driver invia i dati per il parametro all'origine dati; il \*buffer *ParameterValuePtr* deve contenere un valore di input valido oppure il buffer*di StrLen_or_IndPtr* deve contenere SQL_NULL_DATA, SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC.  
  
     Se un'applicazione non è in grado di determinare il tipo di un parametro in una chiamata di routine, imposta *InputOutputType* su SQL_PARAM_INPUT; se l'origine dati restituisce un valore per il parametro, il driver lo elimina.  
  
-   SQL_PARAM_INPUT_OUTPUT. Il parametro contrassegna un parametro di input/output in una routine. Ad esempio, il parametro in **,call GetEmpDept(?)** è un parametro di input/output che accetta il nome di un dipendente e restituisce il nome del reparto del dipendente.  
  
     Quando viene eseguita l'istruzione, il driver invia i dati per il parametro all'origine dati; il \*buffer *ParameterValuePtr* deve contenere un \*valore di input valido oppure il buffer *StrLen_or_IndPtr* deve contenere SQL_NULL_DATA, SQL_DATA_AT_EXEC o il risultato della SQL_LEN_DATA_AT_EXEC macro. Dopo l'esecuzione dell'istruzione, il driver restituisce i dati per il parametro all'applicazione; Se l'origine dati non restituisce un valore per un parametro di input/output, il driver imposta il buffer*di StrLen_or_IndPtr di StrLen_or_IndPtr* su SQL_NULL_DATA.  
  
    > [!NOTE]  
    >  Quando un'applicazione ODBC 1.0 chiama **SQLSetParam** in un driver ODBC 2.0, Gestione Driver converte questo in una chiamata a **SQLBindParameter** in cui il *InputOutputType* argomento è impostato su SQL_PARAM_INPUT_OUTPUT.  
  
-   SQL_PARAM_OUTPUT. Il parametro contrassegna il valore restituito di una routine o di un parametro di output in una routine; in entrambi i casi, questi sono noti come parametri di *output*. Ad esempio, il parametro in **, call GetNextEmpID è** un parametro di output che restituisce l'ID dipendente successivo.  
  
     Dopo l'esecuzione dell'istruzione, il driver restituisce i dati per il parametro all'applicazione, a meno che gli argomenti di *StrLen_or_IndPtr* e *ParameterValuePtr* non siano entrambi puntatori null, nel qual caso il driver elimina il valore di output. Se l'origine dati non restituisce un valore per un parametro di output, il driver imposta il buffer*di StrLen_or_IndPtr* di tipo StrLen_or_IndPtr su SQL_NULL_DATA.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. Indica che un parametro di input/output deve essere trasmesso. **SQLGetData** può leggere i valori dei parametri nelle parti. *BufferLength* viene ignorato perché la lunghezza del buffer verrà determinata in base alla chiamata di **SQLGetData**. Il valore del buffer *StrLen_or_IndPtr* deve contenere SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC. Un parametro deve essere associato come parametro DAE (Data-at-Execution) all'input se verrà trasmesso all'output. *ParameterValuePtr* può essere qualsiasi valore di puntatore non null che verrà restituito da **SQLParamData** come token definito dall'utente il cui valore è stato passato con *ParameterValuePtr* sia per l'input che per l'output. Per ulteriori informazioni, vedere Recupero di parametri di [output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_PARAM_OUTPUT_STREAM. Uguale a SQL_PARAM_INPUT_OUTPUT_STREAM, per un parametro di output. **StrLen_or_IndPtr* viene ignorato al momento dell'input.  
  
 Nella tabella seguente sono elencate le diverse combinazioni di *InputOutputType* e*StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|Risultato|Commento su ParameterValuePtr|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC(*len*) o SQL_DATA_AT_EXEC|Ingresso nelle parti|*ParameterValuePtr* può essere qualsiasi valore di puntatore che verrà restituito da **SQLParamData** come token definito dall'utente il cui valore è stato passato con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT|Non SQL_LEN_DATA_AT_EXEC(*len*) o SQL_DATA_AT_EXEC|Buffer associato all'input|*ParameterValuePtr* è l'indirizzo del buffer di input.|  
|SQL_PARAM_OUTPUT|Ignorato all'input.|Buffer associato di output|*ParameterValuePtr* è l'indirizzo del buffer di output.|  
|SQL_PARAM_OUTPUT_STREAM|Ignorato all'input.|Uscita in streaming|*ParameterValuePtr* può essere qualsiasi valore del puntatore, che verrà restituito da **SQLParamData** come token definito dall'utente il cui valore è stato passato con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC(*len*) o SQL_DATA_AT_EXEC|Ingresso nelle parti e buffer associato di output|*ParameterValuePtr* è l'indirizzo del buffer di output, che verrà restituito anche da **SQLParamData** come token definito dall'utente il cui valore è stato passato con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|Non SQL_LEN_DATA_AT_EXEC(*len*) o SQL_DATA_AT_EXEC|Buffer associato all'input e buffer associato all'output|*ParameterValuePtr* è l'indirizzo del buffer di input/output condiviso.|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC(*len*) o SQL_DATA_AT_EXEC|Ingresso nelle parti e output in streaming|*ParameterValuePtr* può essere qualsiasi valore di puntatore non null, che verrà restituito da **SQLParamData** come token definito dall'utente il cui valore è stato passato con *ParameterValuePtr* sia per l'input che per l'output.|  
  
> [!NOTE]  
>  Il driver deve decidere quali tipi SQL sono consentiti quando un'applicazione associa un parametro di output o input-output come trasmesso in streaming. Gestione driver non genererà un errore per un tipo SQL non valido.  
  
## <a name="valuetype-argument"></a>Argomento ValueType

 Il *ValueType* argomento specifica il tipo di dati C del parametro. Questo argomento imposta i campi SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE dell'APD. Deve essere uno dei valori nella sezione Tipi di [dati C](../../../odbc/reference/appendixes/c-data-types.md) dell'Appendice D: Tipi di dati.  
  
 Se l'argomento *ValueType* è uno dei tipi di dati intervallo, il campo SQL_DESC_TYPE del record *ParameterNumber* di APD è impostato su SQL_INTERVAL, il campo SQL_DESC_CONCISE_TYPE dell'oggetto APD è impostato sul tipo di dati intervallo conciso e il campo SQL_DESC_DATETIME_INTERVAL_CODE del record *NumeroParametro* viene impostato su un sottocodice per il tipo di dati intervallo specifico. (Vedere [l'Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).) Per i dati vengono utilizzati rispettivamente la precisione dei secondi di intervallo predefinita (2) e la precisione predefinita dei secondi di intervallo (6), impostati nei campi SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION dell'APD. Se la precisione predefinita non è appropriata, l'applicazione deve impostare in modo esplicito il campo del descrittore tramite una chiamata a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Se l'argomento *ValueType* è uno dei tipi di dati datetime, il campo SQL_DESC_TYPE del record *ParameterNumber* dell'APD è impostato su SQL_DATETIME, il campo SQL_DESC_CONCISE_TYPE del record *ParameterNumber* dell'APD è impostato sul tipo di dati datetime C conciso e il campo SQL_DESC_DATETIME_INTERVAL_CODE del record *ParameterNumber* è impostato su un sottocodice per il tipo di dati datetime specifico. (Vedere [l'Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Se l'argomento *ValueType* è un tipo di dati SQL_C_NUMERIC, per i dati vengono utilizzati la precisione predefinita (definita dal driver) e la scala predefinita (0), come impostato nei campi SQL_DESC_PRECISION e SQL_DESC_SCALE dell'APD. Se la precisione o la scala predefinita non è appropriata, l'applicazione deve impostare in modo esplicito il campo del descrittore da una chiamata a **SQLSetDescField** o **SQLSetDescRec**.  
  
 SQL_C_DEFAULT specifica che il valore del parametro deve essere trasferito dal tipo di dati C predefinito per il tipo di dati SQL specificato con *ParameterType*.  
  
 È inoltre possibile specificare un tipo di dati C esteso. Per ulteriori informazioni, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 Per ulteriori informazioni, vedere Tipi di [dati C predefiniti](../../../odbc/reference/appendixes/default-c-data-types.md), Conversione di dati da C a tipi di dati [SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)e [Conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) nell'appendice D: tipi di dati .  
  
## <a name="parametertype-argument"></a>Argomento ParameterType

 Deve essere uno dei valori elencati nella sezione [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) dell'Appendice D: Tipi di dati oppure deve essere un valore specifico del driver. Questo argomento imposta i campi SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE dell'IPD.  
  
 Se l'argomento *ParameterType* è uno degli identificatori datetime, il campo SQL_DESC_TYPE dell'IPD è impostato su SQL_DATETIME, il campo SQL_DESC_CONCISE_TYPE dell'IPD viene impostato sul tipo di dati SQL datetime conciso e il campo SQL_DESC_DATETIME_INTERVAL_CODE è impostato sul valore del sottocodice datetime appropriato.  
  
 Se *ParameterType* è uno degli identificatori di intervallo, il campo SQL_DESC_TYPE dell'IPD è impostato su SQL_INTERVAL, il campo SQL_DESC_CONCISE_TYPE dell'IPD viene impostato sul tipo di dati intervallo SQL conciso e il campo SQL_DESC_DATETIME_INTERVAL_CODE dell'IPD viene impostato sul sottocodice di intervallo appropriato. Il campo SQL_DESC_DATETIME_INTERVAL_PRECISION dell'IPD viene impostato sulla precisione dell'interlinea dell'intervallo e il campo SQL_DESC_PRECISION viene impostato sulla precisione dei secondi dell'intervallo, se applicabile. Se il valore predefinito di SQL_DESC_DATETIME_INTERVAL_PRECISION o SQL_DESC_PRECISION non è appropriato, l'applicazione deve impostarlo in modo esplicito chiamando **SQLSetDescField**. Per ulteriori informazioni su uno di questi campi, vedere [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Se l'argomento *ValueType* è un tipo di dati SQL_NUMERIC, per i dati vengono utilizzati la precisione predefinita (definita dal driver) e la scala predefinita (0), impostata nei campi SQL_DESC_PRECISION e SQL_DESC_SCALE dell'IPD. Se la precisione o la scala predefinita non è appropriata, l'applicazione deve impostare in modo esplicito il campo del descrittore da una chiamata a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Per informazioni sulla modalità di conversione dei dati, vedere [Conversione di dati da C a tipi](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) di dati SQL e Conversione di dati da SQL a tipi di dati [C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) nell'appendice D: tipi di dati.  
  
## <a name="columnsize-argument"></a>Argomento ColumnSize

 *L'argomento ColumnSize* specifica la dimensione della colonna o dell'espressione che corrisponde all'indicatore di parametro, la lunghezza dei dati o entrambi. Questo argomento imposta campi diversi dell'IPD, a seconda del tipo di dati SQL (argomento *ParameterType).* Le regole seguenti si applicano a questo mapping:The following rules apply to this mapping:  
  
-   Se *ParameterType* è SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY o uno dei tipi di dati datetime o interval SQL concisi, il campo SQL_DESC_LENGTH dell'IPD viene impostato sul valore di *ColumnSize*. Per ulteriori informazioni, vedere la sezione [Dimensioni colonna, cifre decimali, Lunghezza ottetto](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) di trasferimento e Dimensioni di visualizzazione nell'Appendice D: Tipi di dati.  
  
-   Se *ParameterType* è SQL_DECIMAL, SQL_NUMERIC, SQL_FLOAT, SQL_REAL o SQL_DOUBLE, il campo SQL_DESC_PRECISION dell'IPD viene impostato sul valore di *ColumnSize*.  
  
-   Per altri tipi di dati, il *ColumnSize* argomento viene ignorato.  
  
 Per ulteriori informazioni, vedere "Passaggio di valori di parametro" e SQL_DATA_AT_EXEC in "*argomento di StrLen_or_IndPtr".*  
  
## <a name="decimaldigits-argument"></a>Argomento DecimalDigits

 Se *ParameterType* è SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND SQL_INTERVAL_HOUR_TO_SECOND o SQL_INTERVAL_MINUTE_TO_SECOND, il campo SQL_DESC_PRECISION dell'IPD viene impostato su *DecimalDigits*. Se *ParameterType* è SQL_NUMERIC o SQL_DECIMAL, il campo SQL_DESC_SCALE dell'IPD viene impostato su *DecimalDigits*. Per tutti gli altri tipi di dati, il *DecimalDigits* argomento viene ignorato.  
  
## <a name="parametervalueptr-argument"></a>Argomento ParameterValuePtr

 L'argomento *ParameterValuePtr* punta a un buffer che, quando viene chiamato **SQLExecute** o **SQLExecDirect,** contiene i dati effettivi per il parametro. I dati devono essere nel formato specificato dall'argomento *ValueType.* Questo argomento imposta il campo SQL_DESC_DATA_PTR dell'APD. Un'applicazione può impostare il *ParameterValuePtr* argomento a un puntatore null, purché * \*StrLen_or_IndPtr* è SQL_NULL_DATA o SQL_DATA_AT_EXEC. (Questo vale solo per i parametri di input o di input/output.)  
  
 Se \* *StrLen_or_IndPtr* è il risultato della macro o SQL_DATA_AT_EXEC SQL_LEN_DATA_AT_EXEC(*length),* *ParameterValuePtr* è un valore di puntatore definito dall'applicazione associato al parametro. Viene restituito all'applicazione tramite **SQLParamData**. Ad esempio, *ParameterValuePtr* potrebbe essere un token diverso da zero, ad esempio un numero di parametro, un puntatore ai dati o un puntatore a una struttura utilizzata dall'applicazione per associare i parametri di input. Si noti tuttavia che se il parametro è un parametro di input/output, *ParameterValuePtr* deve essere un puntatore a un buffer in cui verrà archiviato il valore di output. Se il valore nell'attributo di istruzione SQL_ATTR_PARAMSET_SIZE è maggiore di 1, l'applicazione può utilizzare il valore a cui fa riferimento l'attributo di istruzione SQL_ATTR_PARAMS_PROCESSED_PTR con il *ParameterValuePtr* argomento. Ad esempio, *ParameterValuePtr* potrebbe puntare a una matrice di valori e l'applicazione potrebbe utilizzare il valore a cui fa riferimento SQL_ATTR_PARAMS_PROCESSED_PTR per recuperare il valore corretto dalla matrice. Per ulteriori informazioni, vedere "Passaggio di valori di parametro" più avanti in questa sezione.  
  
 Se il *InputOutputType* argomento è SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT, *ParameterValuePtr* punta a un buffer in cui il driver restituisce il valore di output. Se la procedura restituisce uno \*o più set di risultati, non è garantito che venga impostato il buffer *ParameterValuePtr* fino a quando non sono stati elaborati tutti i set di risultati/conteggi delle righe. Se il buffer non viene impostato fino al completamento dell'elaborazione, i parametri di output e i valori restituiti non sono disponibili fino a quando **SQLMoreResults** non restituisce SQL_NO_DATA. La chiamata a **SQLCloseCursor** o **SQLFreeStmt** con un'opzione di SQL_CLOSE causerà l'eliminazione di questi valori.  
  
 Se il valore nell'attributo dell'istruzione SQL_ATTR_PARAMSET_SIZE è maggiore di 1, *ParameterValuePtr* punta a una matrice. Una singola istruzione SQL elabora la matrice completa di valori di input per un parametro di input o input/output e restituisce una matrice di valori di output per un parametro di input/output o di output.  
  
## <a name="bufferlength-argument"></a>Argomento BufferLength

 Per i dati C di tipo carattere e \*binario, il *BufferLength* argomento specifica la lunghezza del *ParameterValuePtr* buffer (se si tratta di un singolo elemento) o la lunghezza di un elemento nel \* *ParameterValuePtr* matrice (se il valore nel SQL_ATTR_PARAMSET_SIZE attributo di istruzione è maggiore di 1). Questo argomento imposta il campo record SQL_DESC_OCTET_LENGTH dell'APD. Se l'applicazione specifica più valori, *BufferLength* viene utilizzato per determinare la posizione dei valori nella matrice*ParameterValuePtr,* sia nell'input che nell'output. Per i parametri di input/output e di output, viene utilizzato per determinare se troncare i dati C di tipo carattere e binario nell'output:For input/output and output parameters, it is used to determine whether to truncate character and binary C data on output:  
  
-   Per i dati di tipo carattere C, se il numero di byte \*disponibili per la restituzione è maggiore o uguale a *BufferLength*, i dati in *ParameterValuePtr* vengono troncati a *BufferLength* meno la lunghezza di un carattere di terminazione null e vengono terminati con null dal driver.  
  
-   Per i dati Binari C, se il numero di byte disponibili \*per la restituzione è maggiore di *BufferLength*, i dati in *ParameterValuePtr* vengono troncati a *BufferLength* byte.  
  
 Per tutti gli altri tipi di dati C, il *BufferLength* argomento viene ignorato. La lunghezza \*del buffer *ParameterValuePtr* (se si tratta di un singolo \*elemento) o la lunghezza di un elemento nella matrice *ParameterValuePtr* (se l'applicazione chiama **SQLSetStmtAttr** con un argomento *Attribute* di SQL_ATTR_PARAMSET_SIZE per specificare più valori per ogni parametro) si presuppone che sia la lunghezza del tipo di dati C.  
  
 Per l'output trasmesso o i parametri di input/output trasmessi, l'argomento *BufferLength* viene ignorato perché la lunghezza del buffer è specificata in **SQLGetData**.  
  
> [!NOTE]  
>  Quando un'applicazione ODBC 1.0 chiama **SQLSetParam** in un ODBC 3. *x* driver, Gestione Driver converte questo in una chiamata a **SQLBindParameter** in cui il *BufferLength* argomento è sempre SQL_SETPARAM_VALUE_MAX. Poiché Gestione Driver restituisce un errore se un ODBC 3. *x* application imposta *BufferLength* su SQL_SETPARAM_VALUE_MAX, odbc 3. *x* driver può utilizzare questo per determinare quando viene chiamato da un'applicazione ODBC 1.0.  
  
> [!NOTE]  
>  In **SQLSetParam**, il modo in cui un'applicazione specifica la lunghezza del buffer*di ParametrValuePtr* in modo che il driver possa restituire dati binari o di tipo carattere e il modo in cui un'applicazione invia una matrice di valori di parametri binari o di caratteri al driver è definito dal driver.  
  
## <a name="strlen_or_indptr-argument"></a>Argomento StrLen_or_IndPtr

 Il *StrLen_or_IndPtr* argomento punta a un buffer che, quando **sqlExecute** o **SQLExecDirect** viene chiamato, contiene uno dei seguenti. Questo argomento imposta i campi SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR record dei puntatori ai parametri dell'applicazione.  
  
-   La lunghezza del valore del parametro archiviato in *: ParameterValuePtr*. Questo viene ignorato, ad eccezione dei dati C di tipo carattere o binario.  
  
-   SQL_NTS. Il valore del parametro è una stringa con terminazione null.  
  
-   SQL_NULL_DATA. Il valore del parametro è NULL.  
  
-   SQL_DEFAULT_PARAM. Una routine consiste nell'utilizzare il valore predefinito di un parametro, anziché un valore recuperato dall'applicazione. Questo valore è valido solo in una routine chiamata nella sintassi canonica ODBC e quindi solo se l'argomento *InputOutputType* è SQL_PARAM_INPUT, SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_INPUT_OUTPUT_STREAM. Quando \* *StrLen_or_IndPtr* è SQL_DEFAULT_PARAM, gli argomenti *ValueType*, *ParameterType*, *ColumnSize*, *DecimalDigits*, *BufferLength*e *ParameterValuePtr* vengono ignorati per i parametri di input e vengono utilizzati solo per definire il valore del parametro di output per i parametri di input/output.  
  
-   Risultato della macro SQL_LEN_DATA_AT_EXEC(*length*). I dati per il parametro verranno inviati con **SQLPutData**. Se l'argomento *ParameterType* è SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo di dati long, specifico dell'origine dati e il driver restituisce "Y" per il tipo di informazioni SQL_NEED_LONG_DATA_LEN in **SQLGetInfo**, *length* è il numero di byte di dati da inviare per il parametro; in caso contrario, *length* deve essere un valore non negativo e viene ignorato. Per ulteriori informazioni, vedere "Passaggio di valori di parametro" più avanti in questa sezione.  
  
     Ad esempio, per specificare che 10.000 byte di dati verranno inviati con **SQLPutData** in una o più chiamate, per un parametro SQL_LONGVARCHAR, un'applicazione imposta*StrLen_or_IndPtr su* SQL_LEN_DATA_AT_EXEC(10000).  
  
-   SQL_DATA_AT_EXEC. I dati per il parametro verranno inviati con **SQLPutData**. Questo valore viene utilizzato dalle applicazioni ODBC 1.0 quando chiamano ODBC 3. *x* driver. Per ulteriori informazioni, vedere "Passaggio di valori di parametro" più avanti in questa sezione.  
  
 Se *StrLen_or_IndPtr* è un puntatore null, il driver presuppone che tutti i valori dei parametri di input non siano NULL e che i dati di tipo carattere e binario siano con terminazione null. Se *InputOutputType* è SQL_PARAM_OUTPUT o SQL_PARAM_OUTPUT_STREAM e *ParameterValuePtr* e *StrLen_or_IndPtr* sono entrambi puntatori null, il driver elimina il valore di output.  
  
> [!NOTE]  
>  Gli sviluppatori di applicazioni sono fortemente sconsigliati di specificare un puntatore null per *StrLen_or_IndPtr* quando il tipo di dati del parametro è SQL_C_BINARY. Per assicurarsi che un driver non tronca in modo imprevisto SQL_C_BINARY dati, *StrLen_or_IndPtr* deve contenere un puntatore a un valore di lunghezza valido.  
  
 Se l'argomento *InputOutputType* è SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_OUTPUT_STREAM, *StrLen_or_IndPtr* punta a un buffer in \*cui il driver restituisce SQL_NULL_DATA, non è possibile determinare il numero di byte disponibili da restituire in *ParameterValuePtr* (escluso il byte di terminazione null dei dati di tipo carattere) o SQL_NO_TOTAL (se non è possibile determinare il numero di byte disponibili per la restituzione). Se la procedura restituisce uno o più set di risultati, non è garantito che venga impostato il buffer*di StrLen_or_IndPtr* finché non sono stati recuperati tutti i risultati.  
  
 Se il valore nell'attributo di istruzione SQL_ATTR_PARAMSET_SIZE è maggiore di 1, *StrLen_or_IndPtr* punta a una matrice di valori SQLLEN. Questi possono essere uno qualsiasi dei valori elencati in precedenza in questa sezione e vengono elaborati con una singola istruzione SQL.  
  
## <a name="passing-parameter-values"></a>Passaggio di valori di parametroPassing Parameter Values

 Un'applicazione può passare il valore \*per un parametro nel buffer *ParameterValuePtr* o con una o più chiamate a **SQLPutData**. I parametri i cui dati vengono passati con **SQLPutData** sono noti come parametri *data-at-execution.* Questi vengono in genere utilizzati per inviare dati per SQL_LONGVARBINARY e SQL_LONGVARCHAR parametri e possono essere combinati con altri parametri.  
  
 Per passare i valori dei parametri, un'applicazione esegue la sequenza di passaggi seguente:To pass parameter values, an application performs the following sequence of steps:  
  
1.  Chiama **SQLBindParameter** per ogni parametro per associare i buffer per il valore del parametro (*argomento ParameterValuePtr)* e lunghezza/indicatore *(StrLen_or_IndPtr* argomento). Per i parametri data-at-execution, *ParameterValuePtr* è un valore del puntatore definito dall'applicazione, ad esempio un numero di parametro o un puntatore ai dati. Il valore verrà restituito in un secondo momento e può essere utilizzato per identificare il parametro.  
  
2.  Inserisce i valori per i \*parametri di input e di input/output nei buffer di*StrLen_or_IndPtr* *ParameterValuePtr* e :  
  
    -   Per i parametri normali, l'applicazione \*inserisce il valore del parametro nel buffer *ParameterValuePtr* e la lunghezza di tale valore nel buffer*StrLen_or_IndPtr.* Per ulteriori informazioni, vedere [Impostazione dei valori](../../../odbc/reference/develop-app/setting-parameter-values.md)dei parametri .  
  
    -   Per i parametri data-at-execution, l'applicazione inserisce il risultato della macro SQL_LEN_DATA_AT_EXEC(*length*) (quando si chiama un driver ODBC 2.0) nel buffer*StrLen_or_IndPtr* .  
  
3.  Chiama **SQLExecute** o **SQLExecDirect** per eseguire l'istruzione SQL.  
  
    -   Se non sono presenti parametri data-at-execution, il processo è completo.  
  
    -   Se sono presenti parametri data-at-execution, la funzione restituisce SQL_NEED_DATA.  
  
4.  Chiama **SQLParamData** per recuperare il valore definito dall'applicazione specificato nell'argomento *ParameterValuePtr* di **SQLBindParameter** per il primo parametro data-at-execution da elaborare. **SQLParamData** restituisce SQL_NEED_DATA.  
  
    > [!NOTE]  
    >  Sebbene i parametri data-at-execution siano simili alle colonne data-at-execution, il valore restituito da **SQLParamData** è diverso per ognuno di essi. I parametri Data-at-execution sono parametri in un'istruzione SQL per la quale verranno inviati dati con **SQLPutData** quando l'istruzione viene eseguita con **SQLExecDirect** o **SQLExecute**. Sono associati a **SQLBindParameter**. Il valore restituito da **SQLParamData** è un valore di puntatore passato a **SQLBindParameter** nell'argomento *ParameterValuePtr.* Le colonne Data-at-execution sono colonne in un set di righe per le quali verranno inviati dati con **SQLPutData** quando una riga viene aggiornata o aggiunta con **SQLBulkOperations** o con **SQLSetPos**. Sono associati a **SQLBindCol**. Il valore restituito da **SQLParamData** è l'indirizzo della riga nel buffer*TargetValuePtr* (impostato da una chiamata a **SQLBindCol**) in fase di elaborazione.  
  
5.  Chiama **SQLPutData** una o più volte per inviare i dati per il parametro. È necessaria più di una chiamata se \*il valore dei dati è maggiore del buffer *ParameterValuePtr* specificato in **SQLPutData**; più chiamate a **SQLPutData** per lo stesso parametro sono consentite solo quando si inviano dati di tipo carattere C a una colonna con un tipo di dati carattere, binario o specifico dell'origine dati o quando si inviano dati C binari a una colonna con un tipo di dati carattere, binario o specifico dell'origine dati.  
  
6.  Chiama nuovamente **SQLParamData** per segnalare che tutti i dati sono stati inviati per il parametro.  
  
    -   Se sono presenti più parametri data-at-execution, **SQLParamData** restituisce SQL_NEED_DATA e il valore definito dall'applicazione per il successivo parametro data-at-execution da elaborare. L'applicazione ripete i passaggi 4 e 5.  
  
    -   Se non sono presenti altri parametri data-at-execution, il processo è completo. Se l'istruzione è stata eseguita correttamente, **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; se l'esecuzione non è riuscita, restituisce SQL_ERROR. A questo punto, **SQLParamData** può restituire qualsiasi SQLSTATE che può essere restituito dalla funzione utilizzata per eseguire l'istruzione (**SQLExecDirect** o **SQLExecute**).  
  
         I valori di output per qualsiasi parametro \*di input/output o output sono disponibili nei buffer *ParameterValuePtr* e*StrLen_or_IndPtr* dopo che l'applicazione recupera tutti i set di risultati generati dall'istruzione.  
  
 La chiamata a **SQLExecute** o **SQLExecDirect** inserisce l'istruzione in uno stato SQL_NEED_DATA. A questo punto, l'applicazione può chiamare solo **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**o **SQLPutData** con l'istruzione o l'handle di *connessione* associato all'istruzione . Se chiama qualsiasi altra funzione con l'istruzione o la connessione associata all'istruzione, la funzione restituisce SQLSTATE HY010 (errore di sequenza di funzione). L'istruzione lascia lo stato SQL_NEED_DATA quando **SQLParamData** o **SQLPutData** restituisce un errore, **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO o l'istruzione viene annullata.  
  
 Se l'applicazione chiama **SQLCancel** mentre il driver richiede ancora dati per i parametri data-at-execution, il driver annulla l'esecuzione dell'istruzione; l'applicazione può quindi chiamare nuovamente **SQLExecute** o **SQLExecDirect.**  
  
## <a name="retrieving-streamed-output-parameters"></a>Recupero di parametri di output trasmessiRetrieving Streamed Output Parameters

 Quando un'applicazione imposta *InputOutputType* su SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_OUTPUT_STREAM, il valore del parametro di output deve essere recuperato da una o più chiamate a **SQLGetData**. Quando il driver dispone di un valore di parametro di output trasmesso da restituire all'applicazione, restituirà SQL_PARAM_DATA_AVAILABLE in risposta a una chiamata alle funzioni seguenti: **SQLMoreResults**, **SQLExecute**e **SQLExecDirect**. Un'applicazione chiama **SQLParamData** per determinare quale valore di parametro è disponibile.  
  
 Per ulteriori informazioni sui parametri di output SQL_PARAM_DATA_AVAILABLE e trasmessi, vedere Recupero di parametri di [output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-arrays-of-parameters"></a>Uso delle matrici di parametri

 Quando un'applicazione prepara un'istruzione con indicatori di parametro e passa una matrice di parametri, è possibile eseguire questa operazione in due modi diversi. Un modo è che il driver si basi sulle funzionalità di elaborazione della matrice del back-end, nel qual caso l'intera istruzione con la matrice di parametri viene considerata come un'unità atomica. Oracle è un esempio di origine dati che supporta le funzionalità di elaborazione di matrici. Un altro modo per implementare questa funzionalità è per il driver per generare un batch di istruzioni SQL, un'istruzione SQL per ogni set di parametri nella matrice di parametri ed eseguire il batch. Le matrici di parametri non possono essere utilizzate con un'istruzione **UPDATE WHERE CURRENT OF.**  
  
 Quando viene elaborata una matrice di parametri, è possibile eseguire il rollup di singoli set di risultati/conteggi di righe (uno per ogni set di parametri) oppure il rollup dei conteggi di set di risultati/righe in uno. L'opzione SQL_PARAM_ARRAY_ROW_COUNTS in **SQLGetInfo** indica se i conteggi delle righe sono disponibili per ogni set di parametri (SQL_PARC_BATCH) o se è disponibile un solo conteggio delle righe (SQL_PARC_NO_BATCH).  
  
 L'opzione SQL_PARAM_ARRAY_SELECTS in **SQLGetInfo** indica se un set di risultati è disponibile per ogni set di parametri (SQL_PAS_BATCH) o per un solo set di risultati (SQL_PAS_NO_BATCH). Se il driver non consente l'esecuzione di un'istruzione di generazione del set di risultati con una matrice di parametri, SQL_PARAM_ARRAY_SELECTS restituisce SQL_PAS_NO_SELECT.  
  
 Per ulteriori informazioni, vedere [Funzione SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 Per supportare matrici di parametri, l'attributo di istruzione SQL_ATTR_PARAMSET_SIZE viene impostato per specificare il numero di valori per ogni parametro. Se il campo è maggiore di 1, i campi SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR dell'APD devono puntare a matrici. La cardinalità di ogni matrice è uguale al valore di SQL_ATTR_PARAMSET_SIZE.  
  
 Il campo SQL_DESC_ROWS_PROCESSED_PTR di APD punta a un buffer che contiene il numero di set di parametri che sono stati elaborati, inclusi i set di errori. Durante l'elaborazione di ogni set di parametri, il driver archivia un nuovo valore nel buffer. Se si tratta di un puntatore null, non verrà restituito alcun numero. Quando vengono utilizzate matrici di parametri, il valore a cui fa riferimento il campo SQL_DESC_ROWS_PROCESSED_PTR di APD viene popolato anche se SQL_ERROR viene restituito dalla funzione di impostazione. Se viene restituito SQL_NEED_DATA, il valore a cui fa riferimento il campo SQL_DESC_ROWS_PROCESSED_PTR dell'Oggetto APD viene impostato sul set di parametri in fase di elaborazione.  
  
 Ciò che si verifica quando viene associata una matrice di parametri e **un'istruzione UPDATE WHERE CURRENT OF** è definita dal driver.  
  
## <a name="column-wise-parameter-binding"></a>Associazione di parametri wise a colonneColumn-Wise Parameter Binding

 Nell'associazione per colonna, l'applicazione associa matrici separate di parametro e lunghezza/indicatore a ogni parametro.  
  
 Per utilizzare l'associazione per colonna, l'applicazione imposta innanzitutto l'attributo dell'istruzione SQL_ATTR_PARAM_BIND_TYPE su SQL_PARAM_BIND_BY_COLUMN. Questa è l'impostazione predefinita. Per ogni colonna da associare, l'applicazione esegue i passaggi seguenti:For each column to be bound, the application performs the following steps:  
  
1.  Alloca una matrice di buffer di parametri.  
  
2.  Alloca una matrice di buffer di lunghezza/indicatore.  
  
    > [!NOTE]  
    >  Se l'applicazione scrive direttamente nei descrittori quando viene utilizzata l'associazione per colonna, è possibile utilizzare matrici separate per i dati di lunghezza e indice.  
  
3.  Chiama **SQLBindParameter** con gli argomenti seguenti:  
  
    -   *ValueType* è il tipo C di un singolo elemento nella matrice di buffer di parametri.  
  
    -   *ParameterType* è il tipo SQL del parametro.  
  
    -   *ParameterValuePtr* è l'indirizzo della matrice di buffer di parametri.  
  
    -   *BufferLength* è la dimensione di un singolo elemento nella matrice del buffer di parametri. Il *BufferLength* argomento viene ignorato quando i dati sono dati a lunghezza fissa.  
  
    -   *StrLen_or_IndPtr* è l'indirizzo della matrice lunghezza/indicatore.  
  
 Per ulteriori informazioni sull'utilizzo di queste informazioni, vedere "Argomento ParameterValuePtr" in "Commenti" più avanti in questa sezione. Per ulteriori informazioni sull'associazione per colonna dei parametri, vedere [Associazione di matrici di parametri](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="row-wise-parameter-binding"></a>Associazione di parametri row-WiseRow-Wise Parameter Binding

 Nell'associazione per riga, l'applicazione definisce una struttura che contiene i buffer di parametro e lunghezza/indicatore per ogni parametro da associare.  
  
 Per utilizzare l'associazione per riga, l'applicazione esegue i passaggi seguenti:To use row-wise binding, the application performs the following steps:  
  
1.  Definisce una struttura per contenere un singolo set di parametri (inclusi i buffer di parametri e lunghezza/indicatore) e alloca una matrice di queste strutture.  
  
    > [!NOTE]  
    >  Se l'applicazione scrive direttamente nei descrittori quando viene utilizzata l'associazione per riga, è possibile utilizzare campi separati per i dati di lunghezza e indicatore.  
  
2.  Imposta l'attributo di istruzione SQL_ATTR_PARAM_BIND_TYPE sulla dimensione della struttura che contiene un singolo set di parametri o sulla dimensione di un'istanza di un buffer a cui verranno associati i parametri. La lunghezza deve includere spazio per tutti i parametri associati e qualsiasi riempimento della struttura o del buffer, per assicurarsi che quando l'indirizzo di un parametro associato viene incrementato con la lunghezza specificata, il risultato punterà all'inizio dello stesso parametro nella riga successiva. Quando si utilizza l'operatore *sizeof* in ANSI C, questo comportamento è garantito.  
  
3.  Chiama SQLBindParameter con i seguenti argomenti per ogni parametro da associare:Calls **SQLBindParameter** with the following arguments for each parameter to be bound:  
  
    -   *ValueType* è il tipo del membro del buffer di parametri da associare alla colonna.  
  
    -   *ParameterType* è il tipo SQL del parametro.  
  
    -   *ParameterValuePtr* è l'indirizzo del membro del buffer di parametri nel primo elemento della matrice.  
  
    -   *BufferLength* è la dimensione del membro del buffer di parametro.  
  
    -   *StrLen_or_IndPtr* è l'indirizzo del membro length/indicator da associare.  
  
 Per ulteriori informazioni sull'utilizzo di queste informazioni, vedere "Argomento*ParameterValuePtr"* più avanti in questa sezione. Per ulteriori informazioni sull'associazione per riga dei parametri, vedere [Le matrici di parametri di associazione](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="error-information"></a>Informazioni sull'errore

 Se un driver non implementa matrici di parametri come batch (l'opzione SQL_PARAM_ARRAY_ROW_COUNTS è uguale a SQL_PARC_NO_BATCH), le situazioni di errore vengono gestite come se fosse stata eseguita un'istruzione. Se il driver implementa matrici di parametri come batch, un'applicazione può utilizzare il campo di intestazione SQL_DESC_ARRAY_STATUS_PTR dell'IPD per determinare quale parametro di un'istruzione SQL o quale parametro in una matrice di parametri ha causato **SQLExecDirect** o **SQLExecute** per restituire un errore. Questo campo contiene informazioni sullo stato per ogni riga di valori di parametro. Se il campo indica che si è verificato un errore, i campi nella struttura dei dati di diagnostica indicheranno il numero di riga e di parametro del parametro non riuscito. Il numero di elementi nella matrice sarà definito dal campo di intestazione SQL_DESC_ARRAY_SIZE nell'aPD, che può essere impostato dall'attributo di istruzione SQL_ATTR_PARAMSET_SIZE.  
  
> [!NOTE]  
>  Il campo di intestazione SQL_DESC_ARRAY_STATUS_PTR nell'Oggetto PD viene utilizzato per ignorare i parametri. Per ulteriori informazioni su come ignorare i parametri, vedere la sezione successiva, "Ignorare un set di parametri".  
  
 Quando **SQLExecute** o **SQLExecDirect** restituisce SQL_ERROR, gli elementi della matrice a cui fa riferimento il campo SQL_DESC_ARRAY_STATUS_PTR nell'IPD conterranno SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, SQL_PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED o SQL_PARAM_DIAG_UNAVAILABLE.  
  
 Per ogni elemento in questa matrice, la struttura dei dati di diagnostica contiene uno o più record di stato. Il campo SQL_DIAG_ROW_NUMBER della struttura indica il numero di riga dei valori di parametro che ha causato l'errore. Se è possibile determinare il parametro specifico in una riga di parametri che ha causato l'errore, il numero di parametro verrà immesso nel campo SQL_DIAG_COLUMN_NUMBER.  
  
 SQL_PARAM_UNUSED viene immesso quando un parametro non è stato utilizzato perché si è verificato un errore in un parametro precedente che ha costretto l'interruzione di **SQLExecute** o **SQLExecDirect.** Ad esempio, se sono presenti 50 parametri e si è verificato un errore durante l'esecuzione del quarantesimo set di parametri che ha causato l'interruzione di **SQLExecute** o **SQLExecDirect,** SQL_PARAM_UNUSED viene immessa nella matrice di stato per i parametri da 41 a 50.  
  
 SQL_PARAM_DIAG_UNAVAILABLE viene immessa quando il driver considera le matrici di parametri come un'unità monolitica, pertanto non genera questo singolo livello di informazioni sull'errore del singolo parametro.  
  
 Alcuni errori nell'elaborazione di un singolo set di parametri causano l'interruzione dell'elaborazione dei set di parametri successivi nella matrice. Altri errori non influiscono sull'elaborazione dei parametri successivi. Gli errori che interromperanno l'elaborazione è definito dal driver. Se l'elaborazione non viene interrotta, tutti i parametri nella matrice vengono elaborati, SQL_SUCCESS_WITH_INFO viene restituito come risultato dell'errore e il buffer definito da SQL_ATTR_PARAMS_PROCESSED_PTR è impostato sul numero totale di set di parametri elaborati (come definito dall'attributo di istruzione SQL_ATTR_PARAMSET_SIZE), che include i set di errori.  
  
> [!CAUTION]  
>  Comportamento ODBC quando si verifica un errore nell'elaborazione di una matrice di parametri è diverso in ODBC 3. *x* rispetto a ODBC 2. *x*. In ODBC 2. *x*, la funzione ha restituito SQL_ERROR e l'elaborazione è cessata. Il buffer a cui fa riferimento l'argomento *pirow* di **SQLParamOptions** contiene il numero della riga di errore. In ODBC 3. *x*, la funzione restituisce SQL_SUCCESS_WITH_INFO e l'elaborazione può arrestarsi o continuare. Se continua, il buffer specificato da SQL_ATTR_PARAMS_PROCESSED_PTR verrà impostato sul valore di tutti i parametri elaborati, inclusi quelli che hanno generato un errore. Questa modifica nel comportamento può causare problemi per le applicazioni esistenti.  
  
 Quando **SQLExecute** o **SQLExecDirect** restituisce prima di completare l'elaborazione di tutti i set di parametri in una matrice di parametri, ad esempio quando viene restituito SQL_ERROR o SQL_NEED_DATA, la matrice di stato contiene gli stati per i parametri che sono già stati elaborati. La posizione a cui fa riferimento il campo SQL_DESC_ROWS_PROCESSED_PTR nell'IPD contiene il numero di riga nella matrice di parametri che ha causato il SQL_ERROR o SQL_NEED_DATA codice di errore. Quando una matrice di parametri viene inviata a un'istruzione SELECT, la disponibilità dei valori della matrice di stato è definita dal driver; possono essere disponibili dopo l'esecuzione dell'istruzione o il recupero dei set di risultati.  
  
## <a name="ignoring-a-set-of-parameters"></a>Ignorare un set di parametri

 Il campo SQL_DESC_ARRAY_STATUS_PTR di APD (come impostato dall'attributo statement SQL_ATTR_PARAM_STATUS_PTR) può essere utilizzato per indicare che un set di parametri associati in un'istruzione SQL deve essere ignorato. Per indicare al driver di ignorare uno o più set di parametri durante l'esecuzione, un'applicazione deve attenersi alla seguente procedura:  
  
1.  Chiamare **SQLSetDescField** per impostare il campo di intestazione SQL_DESC_ARRAY_STATUS_PTR di APD in modo che punti a una matrice di valori SQLUSMALLINT per contenere le informazioni sullo stato. Questo campo può essere impostato anche chiamando **SQLSetStmtAttr** con un *attributo* di SQL_ATTR_PARAM_OPERATION_PTR, che consente a un'applicazione di impostare il campo senza ottenere un handle di descrittore.  
  
2.  Impostare ogni elemento della matrice definita dal campo SQL_DESC_ARRAY_STATUS_PTR dell'APD su uno dei due valori seguenti:  
  
    -   SQL_PARAM_IGNORE, per indicare che la riga è esclusa dall'esecuzione dell'istruzione.  
  
    -   SQL_PARAM_PROCEED, per indicare che la riga è inclusa nell'esecuzione dell'istruzione.  
  
3.  Chiamare **SQLExecDirect** o **SQLExecute** per eseguire l'istruzione preparata.  
  
 Le seguenti regole si applicano alla matrice definita dal campo SQL_DESC_ARRAY_STATUS_PTR dell'APD:  
  
-   Il puntatore è impostato su null per impostazione predefinita.  
  
-   Se il puntatore è null, vengono utilizzati tutti i set di parametri, come se tutti gli elementi fossero impostati su SQL_ROW_PROCEED.  
  
-   L'impostazione di un elemento su SQL_PARAM_PROCEED non garantisce che l'operazione utilizzerà quel particolare set di parametri.  
  
-   SQL_PARAM_PROCEED è definito come 0 nel file di intestazione.  
  
 Un'applicazione può impostare il campo SQL_DESC_ARRAY_STATUS_PTR nell'oggetto PD in modo che punti alla stessa matrice a cui punta il campo SQL_DESC_ARRAY_STATUS_PTR nell'IRD. Ciò è utile quando si associano parametri ai dati di riga. I parametri possono quindi essere ignorati in base allo stato dei dati della riga. Oltre a SQL_PARAM_IGNORE, i codici seguenti fanno sì che un parametro in un'istruzione SQL venga ignorato: SQL_ROW_DELETED, SQL_ROW_UPDATED e SQL_ROW_ERROR. Oltre a SQL_PARAM_PROCEED, i codici seguenti determinano un'istruzione SQL: SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO e SQL_ROW_ADDED.  
  
## <a name="rebinding-parameters"></a>Riassociazione dei parametriRebinding Parameters

 Un'applicazione può eseguire una delle due operazioni per modificare un'associazione:An application can perform either of two operations to change a binding:  
  
-   Chiamare **SQLBindParameter** per specificare una nuova associazione per una colonna già associata. Il driver sovrascrive il binding precedente con quello nuovo.  
  
-   Specificare un offset da aggiungere all'indirizzo del buffer specificato dalla chiamata di associazione a **SQLBindParameter.** Per ulteriori informazioni, vedere la sezione successiva, "Riassociazione con offset".  
  
## <a name="rebinding-with-offsets"></a>Riassociazione con offset

 La riassociazione dei parametri è particolarmente utile quando un'applicazione dispone di un'impostazione dell'area del buffer che può contenere molti parametri, ma una chiamata a **SQLExecDirect** o **SQLExecute** utilizza solo alcuni dei parametri. Lo spazio rimanente nell'area del buffer può essere utilizzato per il set di parametri successivo modificando l'associazione esistente mediante un offset.  
  
 Il campo di intestazione SQL_DESC_BIND_OFFSET_PTR nell'APD punta all'offset di associazione. Se il campo non è null, il driver dereferenzia il puntatore e, se nessuno dei valori nei campi SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR è un puntatore null, aggiunge il valore dereferenziato ai campi nei record del descrittore in fase di esecuzione. I nuovi valori del puntatore vengono utilizzati quando vengono eseguite le istruzioni SQL. L'offset rimane valido dopo la riassociazione. Poiché SQL_DESC_BIND_OFFSET_PTR è un puntatore all'offset anziché l'offset stesso, un'applicazione può modificare direttamente l'offset, senza dover chiamare [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) o [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) per modificare il campo del descrittore. Il puntatore è impostato su null per impostazione predefinita. Il campo SQL_DESC_BIND_OFFSET_PTR dell'ARD può essere impostato da una chiamata a [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) o da una chiamata a [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)con un *attributo fAttribute* di SQL_ATTR_PARAM_BIND_OFFSET_PTR.  
  
 L'offset di associazione viene sempre aggiunto direttamente ai valori nei campi SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR. Se l'offset viene modificato in un valore diverso, il nuovo valore viene comunque aggiunto direttamente al valore in ogni campo del descrittore. Il nuovo offset non viene aggiunto alla somma del valore del campo e degli eventuali offset precedenti.  
  
## <a name="descriptors"></a>Descrittori

 La modalità di associazione di un parametro è determinata dai campi degli ADD e degli IPD. Gli argomenti in **SQLBindParameter** vengono utilizzati per impostare i campi del descrittore. I campi possono essere impostati anche dalle funzioni **SQLSetDescField,** anche se **SQLBindParameter** è più efficiente da utilizzare perché l'applicazione non deve ottenere un handle del descrittore per chiamare **SQLBindParameter**.  
  
> [!CAUTION]  
>  La chiamata a **SQLBindParameter** per un'istruzione può influire su altre istruzioni. Ciò si verifica quando l'ARD associato all'istruzione viene allocato in modo esplicito ed è anche associato ad altre istruzioni. Poiché **SQLBindParameter** modifica i campi dell'oggetto APD, le modifiche si applicano a tutte le istruzioni a cui è associato questo descrittore. Se questo non è il comportamento richiesto, l'applicazione deve dissociare questo descrittore dalle altre istruzioni prima di chiamare **SQLBindParameter**.  
  
 Concettualmente, SQLBindParameter esegue i passaggi seguenti in sequenza:Conceptually, **SQLBindParameter** performs the following steps in sequence:  
  
1.  Chiama [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) per ottenere l'handle APD.  
  
2.  Chiama [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) per ottenere il campo SQL_DESC_COUNT di APD e se il valore dell'argomento *ColumnNumber* supera il valore di SQL_DESC_COUNT, chiama **SQLSetDescField** per aumentare il valore di SQL_DESC_COUNT a *ColumnNumber*.  
  
3.  Chiama [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) più volte per assegnare valori ai seguenti campi di APD:  
  
    -   Imposta SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE sul valore di *ValueType*, con except if *valueType* è uno degli identificatori concisi di un sottotipo datetime o interval, imposta SQL_DESC_TYPE rispettivamente su SQL_DATETIME o SQL_INTERVAL, imposta SQL_DESC_CONCISE_TYPE sull'identificatore conciso e imposta SQL_DESC_DATETIME_INTERVAL_CODE al sottocodice datetime o interval corrispondente.  
  
    -   Imposta il campo SQL_DESC_OCTET_LENGTH sul valore di *BufferLength*.  
  
    -   Imposta il campo SQL_DESC_DATA_PTR sul valore di *ParameterValue*.  
  
    -   Imposta il campo SQL_DESC_OCTET_LENGTH_PTR sul valore di *StrLen_or_Ind*.  
  
    -   Imposta il campo SQL_DESC_INDICATOR_PTR anche sul valore di *StrLen_or_Ind*.  
  
     Il *parametro StrLen_or_Ind* consente di specificare sia le informazioni sull'indicatore che la lunghezza del valore del parametro.  
  
4.  Chiama [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) per ottenere l'handle IPD.  
  
5.  Chiama [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) per ottenere il campo SQL_DESC_COUNT dell'IPD e se il valore dell'argomento *ColumnNumber* supera il valore di SQL_DESC_COUNT, chiama **SQLSetDescField** per aumentare il valore di SQL_DESC_COUNT a *ColumnNumber*.  
  
6.  Chiama [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) più volte per assegnare valori ai seguenti campi dell'IPD:  
  
    -   Imposta SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE sul valore di *ParameterType*, con except se *ParameterType* è uno degli identificatori concisi di un sottotipo datetime o interval, imposta SQL_DESC_TYPE rispettivamente su SQL_DATETIME o SQL_INTERVAL, imposta SQL_DESC_CONCISE_TYPE all'identificatore conciso e SQL_DESC_DATETIME_INTERVAL_CODE al sottocodice datetime o interval corrispondente.  
  
    -   Imposta uno o più SQL_DESC_LENGTH, SQL_DESC_PRECISION e SQL_DESC_DATETIME_INTERVAL_PRECISION, a seconda dei valori appropriati per *TipoParametro*.  
  
    -   Imposta SQL_DESC_SCALE sul valore di *DecimalDigits*.  
  
 Se la chiamata a **SQLBindParameter** ha esito negativo, il contenuto dei campi del descrittore che sarebbe stato impostato in APD non sono definiti e il campo SQL_DESC_COUNT di APD è invariato. Inoltre, i campi SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_TYPE del record appropriato nell'IPD non sono definiti e il campo SQL_DESC_COUNT dell'IPD è invariato.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>Conversione di chiamate da e verso SQLSetParamConversion of Calls to and from SQLSetParam

 Quando un'applicazione ODBC 1.0 chiama **SQLSetParam** in un ODBC 3. *x* driver, ODBC 3. *x* Gestione driver esegue il mapping della chiamata come illustrato nella tabella seguente.  
  
|Chiamata tramite applicazione ODBC 1.0|Chiamata a ODBC 3. *x* driver|  
|----------------------------------|-------------------------------|  
|SQLSetParam( StatementHandle, ParameterNumber, ValueType, ParameterType, LengthPrecision, ParameterScale, ParameterValuePtr, StrLen_or_IndPtr);|SQLBindParameter( StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, *ColumnSize*, *DecimalDigits*, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, un'applicazione prepara un'istruzione SQL per inserire dati nella tabella ORDERS. Per ogni parametro nell'istruzione, l'applicazione chiama **SQLBindParameter** per specificare il tipo di dati C ODBC e il tipo di dati SQL del parametro e per associare un buffer a ogni parametro. Per ogni riga di dati, l'applicazione assegna i valori dei dati a ogni parametro e chiama **SQLExecute** per eseguire l'istruzione.  
  
 Nell'esempio seguente si presuppone la creazione di un'origine dati ODBC denominata Northwind associata al database Northwind.  
  
 Per altri esempi di codice, vedere [Funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [Funzione SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md), [Funzione SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)e [Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
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

 Nell'esempio seguente, un'applicazione esegue una stored procedure di SQL Server utilizzando un parametro denominato.  
  
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
|Restituzione di informazioni su un parametro in un'istruzioneReturning information about a parameter in a statement|[Funzione SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Rilascio dei buffer di parametri sull'istruzione|[Funzione SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Restituzione del numero di parametri dell'istruzione|[Funzione SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|Restituzione del parametro successivo per l'invio dei dati per|[Funzione SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Specifica di più valori di parametro|[Funzione SQLParamOptions](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|Invio dei dati dei parametri in fase di esecuzioneSending parameter data at execution time|[Funzione SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Vedere anche

 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recupero di parametri di output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
