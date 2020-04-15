---
title: Funzione SQLParamData . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLParamData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLParamData
helpviewer_keywords:
- SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ed149e125e3231d670c6ddbd4569ff5ccee5c15
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306922"
---
# <a name="sqlparamdata-function"></a>Funzione SQLParamData
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLParamData** viene usato insieme a **SQLPutData** per fornire i dati dei parametri in fase di esecuzione dell'istruzione e con **SQLGetData** per recuperare i dati dei parametri di output trasmessi.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *ValuePtrPtr*  
 [Uscita] Puntatore a un buffer in cui restituire l'indirizzo del buffer *ParameterValuePtr* specificato in **SQLBindParameter** (per i dati di parametro) o l'indirizzo del buffer *TargetValuePtr* specificato in **SQLBindCol** (per i dati di colonna), contenuto nel campo del record descrittore di SQL_DESC_DATA_PTR.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE o SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLParamData** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLParamData** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07006|Violazione dell'attributo del tipo di dati con restrizioniRestricted data type attribute violation|Impossibile convertire il valore di dati identificato dall'argomento *ValueType* in **SQLBindParameter** per il parametro associato nel tipo di dati identificato dall'argomento *ParameterType* in **SQLBindParameter**.<br /><br /> Il valore dei dati restituito per un parametro associato come SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT non può essere convertito nel tipo di dati identificato dall'argomento *ValueType* in **SQLBindParameter**.<br /><br /> Se non è stato possibile convertire i valori dei dati per una o più righe, ma una o più righe sono state restituite correttamente, questa funzione restituisce SQL_SUCCESS_WITH_INFO.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|22026|Lunghezza dei dati non corrispondente.|Il tipo di informazioni SQL_NEED_LONG_DATA_LEN in **SQLGetInfo** era "Y" e sono stati inviati meno dati per un parametro long (il tipo di dati è stato SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo di dati specifico dell'origine dati lungo) di quello specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**.<br /><br /> Il SQL_NEED_LONG_DATA_LEN tipo di informazioni in **SQLGetInfo** era "Y" e sono stati inviati meno dati per una colonna lunga (il tipo di dati è stato SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo di dati specifico dell'origine dati lungo) di quanto è stato specificato nel buffer di lunghezza corrispondente a una colonna in una riga di dati che è stata aggiunta o aggiornata con **SQLBulkOperations** o aggiornata con **SQLSetPos**.|  
|40001|Errore di serializzazione|È stato eseguito il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*; la funzione è stata quindi chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) la chiamata di funzione precedente non era una chiamata a **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**o **SQLSetPos** in cui il codice restituito era SQL_NEED_DATA o la chiamata di funzione precedente era una chiamata a **SQLPutData**.<br /><br /> La chiamata di funzione precedente era una chiamata a **SQLParamData**.<br /><br /> (DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLParamData.**<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. **SQLCancel** è stato chiamato prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver che corrisponde a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
 Se **SQLParamData** viene chiamato durante l'invio di dati per un parametro in un'istruzione SQL, può restituire qualsiasi SQLSTATE che può essere restituito dalla funzione chiamata per eseguire l'istruzione (**SQLExecute** o **SQLExecDirect**). Se viene chiamato durante l'invio di dati per una colonna da aggiornare o aggiunta con **SQLBulkOperations** o con **SQLSetPos**, può restituire qualsiasi SQLSTATE che può essere restituito da **SQLBulkOperations** o **SQLSetPos**.  
  
## <a name="comments"></a>Commenti  
 **SQLParamData** può essere chiamato per fornire dati dati all'esecuzione per due utilizzi: dati di parametro che verranno utilizzati in una chiamata a **SQLExecute** o **SQLExecDirect**, o dati di colonna che verranno utilizzati quando una riga viene aggiornata o aggiunta da una chiamata a **SQLBulkOperations** o da una chiamata a **SQLSetPos**. In fase di esecuzione, **SQLParamData** restituisce all'applicazione un indicatore dei dati necessari al driver.  
  
 Quando un'applicazione chiama **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos**, il driver restituisce SQL_NEED_DATA se sono necessari dati data-at-execution. Un'applicazione chiama quindi **SQLParamData** per determinare quali dati inviare. Se il driver richiede dati di parametro, il driver restituisce nel buffer di output * \*ValuePtrPtr* il valore inserito dall'applicazione nel buffer del set di righe. L'applicazione può utilizzare questo valore per determinare i dati dei parametri che il driver richiede. Se il driver richiede dati di colonna, il driver restituisce nel * \*ValuePtrPtr* buffer l'indirizzo che la colonna è stata originariamente associata, come segue:  
  
 *Bound Address* + *Offset associazione* indirizzo associato ( ((*Numero riga* - 1) x *Dimensione elemento*)  
  
 in cui le variabili sono definite come indicato nella tabella seguente.  
  
|Variabile|Descrizione|  
|--------------|-----------------|  
|*Indirizzo associato*|Indirizzo specificato con l'argomento *TargetValuePtr* in **SQLBindCol**.|  
|*Offset rilegatura*|Valore archiviato in corrispondenza dell'indirizzo specificato con l'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR.|  
|*Row Number*|Numero in base 1 della riga nel set di righe. Per i recuperi a riga singola, che sono l'impostazione predefinita, questo è 1.For single-row fetches, which are the default, this is 1.|  
|*Dimensione elemento*|Valore dell'attributo di istruzione SQL_ATTR_ROW_BIND_TYPE per i buffer di dati e di lunghezza/indicatore.|  
  
 Restituisce anche SQL_NEED_DATA, che è un indicatore per l'applicazione che deve chiamare **SQLPutData** per inviare i dati.  
  
 L'applicazione chiama **SQLPutData** il numero di volte necessario per inviare i dati di data-at-execution per la colonna o il parametro. Dopo che tutti i dati sono stati inviati per la colonna o il parametro, l'applicazione chiama nuovamente **SQLParamData.After** all the data has been sent for the column or parameter, the application calls SQLParamData again. Se **SQLParamData** restituisce nuovamente SQL_NEED_DATA, i dati devono essere inviati per un altro parametro o colonna. Pertanto, l'applicazione chiama nuovamente **SQLPutData**. Se tutti i dati data-at-execution sono stati inviati per tutti i parametri o le colonne, **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il valore in * \*ValuePtrPtr* è indefinito e l'istruzione SQL può essere eseguita o la chiamata **SQLBulkOperations** o **SQLSetPos** può essere elaborata.  
  
 Se **SQLParamData** fornisce i dati dei parametri per un'istruzione di aggiornamento o eliminazione cercata che non influisce sulle righe nell'origine dati, la chiamata a **SQLParamData** restituisce SQL_NO_DATA.  
  
 Per ulteriori informazioni sul modo in cui i dati dei parametri data-at-execution vengono passati in fase di esecuzione dell'istruzione, vedere "Passaggio di valori di parametro" in [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [Invio di dati lunghi](../../../odbc/reference/develop-app/sending-long-data.md). Per ulteriori informazioni sulla modalità di aggiornamento o aggiunta dei dati delle colonne data-at-execution, vedere la sezione "Using SQLSetPos" in [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Performing Bulk Updates Using Bookmarks" in [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)e [Long Data e SQLSetPos and SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
 **SQLParamData** può essere chiamato per recuperare i parametri di output trasmessi. Quando **SQLMoreResults**, **SQLExecute**, **SQLGetData**o **SQLExecDirect** restituisce SQL_PARAM_DATA_AVAILABLE, chiamare **SQLParamData** per determinare quale parametro ha un valore disponibile. Per ulteriori informazioni sui parametri di output SQL_PARAM_DATA_AVAILABLE e trasmessi, vedere Recupero di parametri di [output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Vedere [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a un parametro|[Pagina relativa alla funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di informazioni su un parametro in un'istruzioneReturning information about a parameter in a statement|[Funzione SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Invio dei dati dei parametri in fase di esecuzioneSending parameter data at execution time|[Funzione SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recupero di parametri di output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
