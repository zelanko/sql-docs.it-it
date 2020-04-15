---
title: 'Funzione SQLDescribeParam : Documenti Microsoft'
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be6d076ca121923a4b6769c7dad5269c3fd642ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301161"
---
# <a name="sqldescribeparam-function"></a>Funzione SQLDescribeParam
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLDescribeParam** restituisce la descrizione di un indicatore di parametro associato a un'istruzione SQL preparata. Queste informazioni sono disponibili anche nei campi dell'IPD.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
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
 [Ingresso] Handle di istruzione.  
  
 *NumeroParametro*  
 [Ingresso] Numero di marcatore di parametro ordinato in sequenza in ordine crescente dei parametri, a partire da 1.  
  
 *DataTypePtr*  
 [Uscita] Puntatore a un buffer in cui restituire il tipo di dati SQL del parametro. Questo valore viene letto dal campo SQL_DESC_CONCISE_TYPE record dell'IPD. Questo sarà uno dei valori nella sezione [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) dell'Appendice D: Tipi di dati o un tipo di dati SQL specifico del driver.  
  
 In ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME o SQL_TYPE_TIMESTAMP verranno restituiti in * \*DataTypePtr* rispettivamente per i dati di data, ora o timestamp; in ODBC 2. *x*, SQL_DATE, SQL_TIME o SQL_TIMESTAMP verranno restituiti. Gestione Driver esegue i mapping necessari quando un ODBC 2. *l'applicazione x* funziona con un'applicazione ODBC 3. *x* o quando un ODBC 3. *l'applicazione x* funziona con un'applicazione ODBC 2. *driver x.*  
  
 Quando *ColumnNumber* è uguale a 0 (per una colonna di segnalibro), viene restituito SQL_BINARY in * \*DataTypePtr* per i segnalibri di lunghezza variabile. (SQL_INTEGER viene restituito se i segnalibri vengono utilizzati da un ODBC 3. *x* che utilizza un'applicazione ODBC 2. *x* o da un ODBC 2. *x* che utilizza un'applicazione ODBC 3. *x* driver.)  
  
 Per altre informazioni, vedere [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) nell'Appendice D: tipi di dati. Per informazioni sui tipi di dati SQL specifici del driver, vedere la documentazione del driver.  
  
 *ParameterSizePtr*  
 [Uscita] Puntatore a un buffer in cui restituire la dimensione, in caratteri, della colonna o dell'espressione dell'indicatore di parametro corrispondente come definito dall'origine dati. Per ulteriori informazioni sulle dimensioni delle colonne, vedere [Dimensioni colonna, Cifre decimali, Lunghezza ottetto di trasferimento e Dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *DecimalDigitsPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero di cifre decimali della colonna o dell'espressione del parametro corrispondente come definito dall'origine dati. Per ulteriori informazioni sulle cifre decimali, vedere [Dimensioni colonna, Cifre decimali, Lunghezza ottetto di trasferimento e Dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *NullablePtrNullablePtr*  
 [Uscita] Puntatore a un buffer in cui restituire un valore che indica se il parametro consente valori NULL. Questo valore viene letto dal campo SQL_DESC_NULLABLE dell'IPD. I tipi validi sono:  
  
-   SQL_NO_NULLS: il parametro non consente valori NULL (questo è il valore predefinito).  
  
-   SQL_NULLABLE: il parametro consente valori NULL.  
  
-   SQL_NULLABLE_UNKNOWN: il driver non è in grado di determinare se il parametro consente valori NULL.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLDescribeParam** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLDescribeParam** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07009|Indice descrittore non valido|(DM) il valore specificato per l'argomento *NumeroParametro* è minore di 1.<br /><br /> Il valore specificato per l'argomento *NumeroParametro* è maggiore del numero di parametri nell'istruzione SQL associata.<br /><br /> Il marcatore di parametro faceva parte di un'istruzione non DML.<br /><br /> L'indicatore di parametro faceva parte di un elenco **SELECT.**|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|21S01|L'elenco di valori di inserimento non corrisponde all'elenco di colonne|Il numero di parametri nell'istruzione **INSERT** non corrisponde al numero di colonne nella tabella indicata nell'istruzione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*. Quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) la funzione è stata chiamata prima di chiamare **SQLPrepare** o **SQLExecDirect** per *StatementHandle*.<br /><br /> (DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLDescribeParam.**<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 Gli indicatori di parametro sono numerati in ordine crescente di parametri, a partire da 1, nell'ordine in cui appaiono nell'istruzione SQL.  
  
 **SQLDescribeParam** non restituisce il tipo (input, input/output o output) di un parametro in un'istruzione SQL. Ad eccezione delle chiamate alle routine, tutti i parametri nelle istruzioni SQL sono parametri di input. Per determinare il tipo di ogni parametro in una chiamata a una routine, un'applicazione chiama **SQLProcedureColumns**.  
  
 Per ulteriori informazioni, vedere [Descrizione dei parametri](../../../odbc/reference/develop-app/describing-parameters.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente viene richiesto all'utente di un'istruzione SQL e quindi prepara tale istruzione. Successivamente, chiama **SQLNumParams** per determinare se l'istruzione contiene parametri. Se l'istruzione contiene parametri, chiama **SQLDescribeParam** per descrivere tali parametri e **SQLBindParameter** per associarli. Infine, richiede all'utente i valori di tutti i parametri e quindi esegue l'istruzione.  
  
```cpp  
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
|Associazione di un buffer a un parametro|[Pagina relativa alla funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparazione di un'istruzione per l'esecuzione|[Pagina relativa alla funzione SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
