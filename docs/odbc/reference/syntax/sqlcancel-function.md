---
title: 'Funzione SQLCancel : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCancel
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCancel
helpviewer_keywords:
- SQLCancel function [ODBC]
ms.assetid: ac0b5972-627f-4440-8c5a-0e8da728726d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcc2afce495a1481692ba1f20162a2df5d9a9458
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301311"
---
# <a name="sqlcancel-function"></a>Funzione SQLCancel
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLCancel** annulla l'elaborazione su un'istruzione.  
  
 Per annullare l'elaborazione su una connessione o un'istruzione, utilizzare [la funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLCancel** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLCancel** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) nell'argomento * \*BufferMessaggio* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLCancel.This** asynchronous function was still executing when the SQLCancel function was called.<br /><br /> (DM) Annulla operazione non riuscita perché è in corso un'operazione asincrona su un handle di connessione associato a *StatementHandle*.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY018 (INFORMAZIONI in cui è INSTATO)|Richiesta di annullamento rifiutata dal server|Il server ha rifiutato la richiesta di annullamento.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 **SQLCancel** può annullare i seguenti tipi di elaborazione in un'istruzione:  
  
-   Funzione in esecuzione in modo asincrono sull'istruzione.  
  
-   Funzione in un'istruzione che richiede dati.  
  
-   Funzione in esecuzione sull'istruzione in un altro thread.  
  
 In ODBC 2. *x*, se un'applicazione chiama **SQLCancel** quando non viene eseguita alcuna elaborazione sull'istruzione, **SQLCancel** ha lo stesso effetto di **SQLFreeStmt** con l'opzione SQL_CLOSE; questo comportamento è definito solo per completezza e le applicazioni devono chiamare **SQLFreeStmt** o **SQLCloseCursor** per chiudere i cursori.  
  
 Quando **SQLCancel** viene chiamato per annullare una funzione in esecuzione in modo asincrono in un'istruzione o una funzione in un'istruzione che richiede dati, i record di diagnostica registrati dalla funzione da annullare vengono cancellati e **SQLCancel** registra i propri record di diagnostica; Quando **SQLCancel** viene chiamato per annullare una funzione in esecuzione su un'istruzione in un altro thread, tuttavia, non cancella i record di diagnostica della funzione in corso di annullamento e non registra i propri record di diagnostica.  
  
## <a name="canceling-asynchronous-processing"></a>Annullamento dell'elaborazione asincronaCanceling Asynchronous Processing  
 Dopo che un'applicazione chiama una funzione in modo asincrono, chiama ripetutamente la funzione per determinare se ha terminato l'elaborazione. Se la funzione è ancora in fase di elaborazione, restituisce SQL_STILL_EXECUTING. Se la funzione ha terminato l'elaborazione, restituisce un codice diverso.  
  
 Dopo qualsiasi chiamata alla funzione che restituisce SQL_STILL_EXECUTING, un'applicazione può chiamare **SQLCancel** per annullare la funzione. Se la richiesta di annullamento ha esito positivo, il driver restituisce SQL_SUCCESS. Questo messaggio non indica che la funzione è stata effettivamente annullata; indica che la richiesta di annullamento è stata elaborata. Quando o se la funzione viene effettivamente annullata dipende dal driver e dall'origine dati. L'applicazione deve continuare a chiamare la funzione originale fino a quando non viene SQL_STILL_EXECUTING il codice restituito. Se la funzione è stata annullata correttamente, il codice restituito viene SQL_ERROR e SQLSTATE HY008 (Operazione annullata). Se la funzione ha completato la normale elaborazione, il codice restituito viene SQL_SUCCESS o SQL_SUCCESS_WITH_INFO se la funzione ha avuto esito positivo o SQL_ERROR e un SQLSTATE diverso da HY008 (operazione annullata) se la funzione non è riuscita.  
  
> [!NOTE]  
>  In ODBC 3.5, una chiamata a **SQLCancel** quando non viene eseguita alcuna elaborazione sull'istruzione non viene considerata **SQLFreeStmt** con l'opzione SQL_CLOSE, ma non ha alcun effetto. Per chiudere un cursore, un'applicazione deve chiamare **SQLCloseCursor**, non **SQLCancel**.  
  
 Per ulteriori informazioni sull'elaborazione asincrona, vedere [esecuzione asincrona](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).  
  
## <a name="canceling-functions-that-need-data"></a>Annullamento delle funzioni che richiedono datiCanceling Functions that Need Data  
 Dopo **che SQLExecute** o **SQLExecDirect** restituisce SQL_NEED_DATA e prima dell'invio dei dati per tutti i parametri data-at-execution, un'applicazione può chiamare **SQLCancel** per annullare l'esecuzione dell'istruzione. Dopo che l'istruzione è stata annullata, l'applicazione può chiamare nuovamente **SQLExecute** o **SQLExecDirect.** Per ulteriori informazioni, vedere [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Dopo **SQLBulkOperations** o **SQLSetPos** restituisce SQL_NEED_DATA e prima dell'invio dei dati per tutte le colonne data-at-execution, un'applicazione può chiamare **SQLCancel** per annullare l'operazione. Dopo che l'operazione è stata annullata, l'applicazione può chiamare nuovamente **SQLBulkOperations** o **SQLSetPos;** l'annullamento non influisce sullo stato del cursore o sulla posizione corrente del cursore. Per ulteriori informazioni, vedere [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) o [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="canceling-functions-executing-on-another-thread"></a>Annullamento di funzioni in esecuzione su un altro threadCanceling Functions Executing on Another Thread  
 In un'applicazione multithread, l'applicazione può annullare una funzione in esecuzione su un altro thread. Per annullare la funzione, l'applicazione chiama **SQLCancel** con lo stesso handle di istruzione utilizzato dalla funzione di destinazione, ma in un thread diverso. La modalità di annullamento della funzione dipende dal driver e dal sistema operativo. Come nell'annullamento di una funzione in esecuzione in modo asincrono, il codice restituito di **SQLCancel** indica solo se il driver ha elaborato correttamente la richiesta. È possibile restituire solo SQL_SUCCESS o SQL_ERROR; non vengono restituite informazioni diagnostiche. Se la funzione originale viene annullata, restituisce SQL_ERROR e SQLSTATE HY008 (Operazione annullata).  
  
 Se un'istruzione SQL viene eseguita quando **SQLCancel** viene chiamato su un altro thread per annullare l'esecuzione dell'istruzione, è possibile che l'esecuzione abbia esito positivo e restituisca SQL_SUCCESS mentre anche l'annullamento ha esito positivo. In questo caso, Gestione Driver presuppone che il cursore aperto dall'esecuzione dell'istruzione viene chiuso dall'annullamento, in modo che l'applicazione non sarà in grado di utilizzare il cursore.  
  
 Per ulteriori informazioni sul threading, vedere [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a un parametro|[Pagina relativa alla funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Esecuzione di operazioni di inserimento o aggiornamento bulk|[Funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Annulla una funzione in esecuzione in modo asincrono su un handle di connessione, oltre alla funzionalità di **SQLCancel**.|[Funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberare un handle di istruzioneFreeing a statement handle|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Recupero di un campo di un record di diagnostica o di un campo dell'intestazione diagnostica|[Funzione SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|Recupero di più campi di una struttura di dati di diagnosticaObtaining multiple fields of a diagnostic data structure|[Funzione SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|Restituzione del parametro successivo per l'invio dei dati per|[Funzione SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Invio dei dati dei parametri in fase di esecuzioneSending parameter data at execution time|[Funzione SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Posizionamento del cursore in un set di righe, aggiornamento dei dati nel set di righe o aggiornamento o eliminazione di dati nel set di risultati|[Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
