---
title: Funzione SQLDescribeParam | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62d61d43638c0ca6e3e43da83367dff461033463
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62982297"
---
# <a name="sqldescribeparam-function"></a>Funzione SQLDescribeParam
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLDescribeParam** restituisce la descrizione di un marcatore di parametro associato a un'istruzione SQL preparata. Queste informazioni sono disponibili anche i campi dell'IPD.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLDescribeParam(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT *   DataTypePtr,  
      SQLULEN *       ParameterSizePtr,  
      SQLSMALLINT *   DecimalDigitsPtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="argument"></a>Argomento  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *ParameterNumber*  
 [Input] Numero di marcatori di parametro ordinato in sequenza in ordine crescente dei parametri, a partire da 1.  
  
 *DataTypePtr*  
 [Output] Puntatore a un buffer in cui restituire il tipo di dati SQL del parametro. Questo valore viene letto dal campo del record SQL_DESC_CONCISE_TYPE dell'IPD. Questo sarà uno dei valori di [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) sezione dell'appendice d: Tipi di dati o un tipo di dati specifici del driver SQL.  
  
 In ODBC 3. *x*, verrà restituito SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP  *\*DataTypePtr* per data, ora o dati di tipo timestamp, rispettivamente; in ODBC 2. *x*, SQL_DATE, SQL_TIME o SQL_TIMESTAMP verranno restituiti. Gestione Driver esegue il mapping richiesto quando un ODBC 2. *x* applicazione funziona con un'applicazione ODBC 3. *x* driver o quando un'applicazione ODBC 3. *x* applicazione funziona con un'API ODBC 2. *x* driver.  
  
 Quando *ColumnNumber* è uguale a 0 (per una colonna del segnalibro), viene restituito SQL_BINARY nel  *\*DataTypePtr* per i segnalibri di lunghezza variabile. (SQL_INTEGER viene restituito se i segnalibri vengono utilizzati da un'applicazione ODBC 3. *x* funziona con un'API ODBC 2. *x* driver o da un'API ODBC 2. *x* funziona con un'applicazione ODBC 3. *x* driver.)  
  
 Per altre informazioni, vedere [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) nell'appendice d: Tipi di dati. Per informazioni sui tipi di dati specifici del driver SQL, vedere la documentazione del driver.  
  
 *ParameterSizePtr*  
 [Output] Puntatore a un buffer in cui si desidera restituire le dimensioni, in caratteri, della colonna o espressione del marcatore di parametro corrispondente come definito dall'origine dati. Per altre informazioni sulle dimensioni di colonna, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *DecimalDigitsPtr*  
 [Output] Puntatore a un buffer in cui restituire il numero di cifre decimali della colonna o un'espressione del parametro corrispondente come definito dall'origine dati. Per altre informazioni su cifre decimali, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *NullablePtr*  
 [Output] Puntatore a un buffer in cui si desidera restituire un valore che indica se il parametro ammette valori NULL. Questo valore viene letto dal campo SQL_DESC_NULLABLE dell'IPD. I tipi validi sono:  
  
-   SQL_NO_NULLS: Il parametro non consente valori NULL (questo è il valore predefinito).  
  
-   SQL_NULLABLE: Il parametro ammette valori NULL.  
  
-   SQL_NULLABLE_UNKNOWN: Il driver non è possibile determinare se il parametro ammette valori NULL.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLDescribeParam** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLDescribeParam** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07009|Indice del descrittore non valido|(DM) il valore specificato per l'argomento *ParameterNumber* è minore di 1.<br /><br /> Il valore specificato per l'argomento *ParameterNumber* era maggiore del numero di parametri nell'istruzione SQL associata.<br /><br /> Il marcatore di parametro faceva parte di un'istruzione DML non.<br /><br /> Il marcatore di parametro faceva parte di un **seleziona** elenco.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|21S01|Elenco di valori di inserimento non corrisponde elenco colonne|Il numero di parametri in di **Inserisci** istruzione non corrisponde il numero di colonne nella tabella denominata nell'istruzione.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver non è riuscito ad allocare memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle*. Quindi la funzione è stata chiamata nuovamente sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata prima di chiamare la funzione **SQLPrepare** oppure **SQLExecDirect** per il *StatementHandle*.<br /><br /> (DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLDescribeParam** funzione è stata chiamata.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 Marcatori di parametro sono numerati in ordine crescente di parametro, a partire da 1, in ordine che vengono visualizzati nell'istruzione SQL.  
  
 **SQLDescribeParam** non restituisce il tipo (input, input/output, o di output) di un parametro in un'istruzione SQL. La differenza nelle chiamate a procedure, tutti i parametri nelle istruzioni SQL sono i parametri di input. Per determinare il tipo di ogni parametro in una chiamata a una routine, un'applicazione chiama **SQLProcedureColumns**.  
  
 Per altre informazioni, vedere [che descrive i parametri](../../../odbc/reference/develop-app/describing-parameters.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente richiede l'immissione di un'istruzione SQL e li prepara tale istruzione. Successivamente, viene chiamato **SQLNumParams** per determinare se l'istruzione contiene tutti i parametri. Se l'istruzione include parametri, chiama il metodo **SQLDescribeParam** per descrivere i parametri e **SQLBindParameter** per associarli. Infine, richiede all'utente i valori di tutti i parametri e quindi viene eseguita l'istruzione.  
  
```  
SQLCHAR       Statement[100];  
SQLSMALLINT   NumParams, i, DataType, DecimalDigits, Nullable;  
SQLUINTEGER   ParamSize;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement and prepare it.  
GetSQLStatement(Statement);  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Check to see if there are any parameters. If so, process them.  
SQLNumParams(hstmt, &NumParams);  
if (NumParams) {  
   // Allocate memory for three arrays. The first holds pointers to buffers in which  
   // each parameter value will be stored in character form. The second contains the  
   // length of each buffer. The third contains the length/indicator value for each  
   // parameter.  
   SQLPOINTER * PtrArray = (SQLPOINTER *) malloc(NumParams * sizeof(SQLPOINTER));  
   SQLINTEGER * BufferLenArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
   SQLINTEGER * LenOrIndArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
  
   for (i = 0; i < NumParams; i++) {  
   // Describe the parameter.  
   SQLDescribeParam(hstmt, i + 1, &DataType, &ParamSize, &DecimalDigits, &Nullable);  
  
   // Call a helper function to allocate a buffer in which to store the parameter  
   // value in character form. The function determines the size of the buffer from  
   // the SQL data type and parameter size returned by SQLDescribeParam and returns  
   // a pointer to the buffer and the length of the buffer.  
   AllocParamBuffer(DataType, ParamSize, &PtrArray[i], &BufferLenArray[i]);  
  
   // Bind the memory to the parameter. Assume that we only have input parameters.  
   SQLBindParameter(hstmt, i + 1, SQL_PARAM_INPUT, SQL_C_CHAR, DataType, ParamSize,  
         DecimalDigits, PtrArray[i], BufferLenArray[i],  
         &LenOrIndArray[i]);  
  
   // Prompt the user for the value of the parameter and store it in the memory  
   // allocated earlier. For simplicity, this function does not check the value  
   // against the information returned by SQLDescribeParam. Instead, the driver does  
   // this when the statement is executed.  
   GetParamValue(PtrArray[i], BufferLenArray[i], &LenOrIndArray[i]);  
   }  
}  
  
// Execute the statement.  
SQLExecute(hstmt);  
  
// Process the statement further, such as retrieving results (if any) and closing the  
// cursor (if any). Code not shown.  
  
// Free the memory allocated for each parameter and the memory allocated for the arrays  
// of pointers, buffer lengths, and length/indicator values.  
for (i = 0; i < NumParams; i++) free(PtrArray[i]);  
free(PtrArray);  
free(BufferLenArray);  
free(LenOrIndArray);  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a un parametro|[Funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparazione di un'istruzione per l'esecuzione|[Funzione SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
