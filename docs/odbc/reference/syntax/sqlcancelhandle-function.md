---
title: Funzione SQLCancelHandle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 655c3c76794b170b113442b14ae75cf977ac024c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253177"
---
# <a name="sqlcancelhandle-function"></a>Funzione SQLCancelHandle
**Conformità**  
 Versione introdotta: ODBC 3.8  
  
 Conformità agli standard: None  
  
 È previsto che la maggior parte dei driver ODBC 3.8 (e versioni successive) implementerà questa funzione. Se un driver non, una chiamata a **SQLCancelHandle** con una connessione da gestire nel *gestire* parametro restituirà SQL_ERROR con SQLSTATE di IM001 e messaggio ' Driver non supporta questa funzione ' una chiamata per **SQLCancelHandle** con un'istruzione come handle di *gestire* parametro verrà mappato a una chiamata a **SQLCancel** da Gestione Driver e possono essere elaborati se il driver implementa **SQLCancel**. Un'applicazione può utilizzare **SQLGetFunctions** per determinare se un driver supporta **SQLCancelHandle**.  
  
 **Riepilogo**  
 **SQLCancelHandle** Annulla l'elaborazione di una connessione o l'istruzione. Gestione Driver esegue il mapping di una chiamata a **SQLCancelHandle** a una chiamata a **SQLCancel** quando *HandleType* è SQL_HANDLE_STMT.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>Argomenti  
 *HandleType*  
 [Input] Tipo di handle in cui l'elaborazione cacel. I valori validi sono SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
 *Handle*  
 [Input] Il punto di controllo quale annullare l'elaborazione.  
  
 Se *gestiscono* non è un handle valido del tipo specificato da *HandleType*, **SQLCancelHandle** non restituisca SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLCancelHandle** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un'istruzione gestiscono *gestiscono* o una *HandleType* SQL_HANDLE_DBC e un handle di connessione *gestire*.  
  
 Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLCancelHandle** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) nell'argomento  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|Una funzione in modo asincrono in esecuzione, correlato alla istruzione è stata chiamata per uno degli handle di istruzione associati con la *gestiscono*, e *HandleType* è stato impostato su SQL_HANDLE_DBC. La funzione asincrona era ancora in esecuzione quando **SQLCancelHandle** è stato chiamato.<br /><br /> (DM) di *HandleType* argomento era SQL_HANDLE_STMT; una funzione in modo asincrono in esecuzione è stata chiamata nell'handle di connessione associata; e la funzione era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per uno degli handle di istruzione associati il *gestire* e *HandleType* è stato impostato su SQL_HANDLE_DBC e restituiti SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> **SQLBrowseConnect** è stato chiamato per *ConnectionHandle*e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima di completare il processo di esplorazione.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY092|Identificatore di attributo/opzione non è valido|*HandleType* è stato impostato su SQL_HANDLE_ENV o SQL_HANDLE_DESC.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *gestire* non supporta la funzione.|  
  
 Se **SQLCancelHandle** viene chiamato con *HandleType* impostato su SQL_HANDLE_STMT, può restituire qualsiasi valore SQLSTATE che può essere restituiti dalla funzione **SQLCancel**.  
  
## <a name="comments"></a>Commenti  
 Questa funzione è simile a **SQLCancel** ma potrebbe richiedere alcuni handle di istruzione o una connessione come parametro anziché solo un handle di istruzione. Gestione Driver esegue il mapping di una chiamata a **SQLCancelHandle** a una chiamata a **SQLCancel** quando *HandleType* è SQL_HANDLE_STMT. Ciò consente alle applicazioni di utilizzare **SQLCancelHandle** per annullare le operazioni di istruzione, anche se il driver non implementa **SQLCancelHandle**.  
  
 Per altre informazioni sull'annullamento in corso un'operazione di istruzione, vedere [funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md).  
  
 Se non sono presenti operazioni in corso sul *gestiscono* la chiamata a **SQLCancelHandle** non ha alcun effetto.  
  
 **SQLCancelHandle** su una connessione handle può annullare i tipi di elaborazione seguenti:  
  
-   Una funzione in esecuzione in modalità asincrona sulla connessione.  
  
-   Una funzione in esecuzione nell'handle di connessione in un altro thread.  
  
 Quando **SQLCancelHandle** viene chiamato per annullare una funzione che esegue in modo asincrono in una connessione, i record di diagnostica inseriti dai **SQLCancelHandle** vengono accodati a quelli restituiti dall'operazione in corso annullato. **SQLCancelHandle** non restituisce i record di diagnostica, tuttavia, quando si annulla una funzione in esecuzione su una connessione in un altro thread.  
  
 Usando **SQLCancelHandle** annullare **SQLEndTran** eventualmente la connessione in stato sospeso. Per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  Per informazioni su come usare **SQLCancelHandle** in un'applicazione che verrà distribuita in un sistema operativo Windows precedente a Windows 7, vedere [matrice di compatibilità](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>Annullare l'elaborazione asincrona correlati alla connessione  
 Se una funzione restituisce SQL_STILL_EXECUTING, un'applicazione può chiamare **SQLCancelHandle** per annullare l'operazione. Se ha esito positivo, la richiesta di annullamento **SQLCancelHandle** restituisce SQL_SUCCESS. Ciò non significa che la funzione originale è stata annullata; indica che è stata elaborata la richiesta di annullamento. Il driver e origine dati determinano quando o se l'operazione è annullata. L'applicazione deve continuare a chiamare la funzione originale fino a quando il codice restituito non SQL_STILL_EXECUTING. Se la funzione originale è stata annullata, il codice restituito è SQL_ERROR e SQLSTATE HY008 (operazione annullata). Se la funzione originale è stata completata la normale elaborazione (non è stato annullato), il codice restituito è SQL_SUCCESS o SQL_SUCCESS_WITH_INFO o SQL_ERROR e un valore SQLSTATE di diverso da HY008 (operazione annullata), se la funzione originale non è riuscita.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>Annullamento di funzioni in esecuzione su un altro Thread  
 In un'applicazione multithread, l'applicazione può annullare un'operazione che è in esecuzione in un altro thread. Per annullare l'operazione, l'applicazione chiama **SQLCancelHandle** con l'handle utilizzato dalla funzione, ma in un thread diverso. Il driver e del sistema operativo determinano la modalità con cui l'operazione viene annullata. Il **SQLCancelHandle** restituire codice indica se il driver di elaborata la richiesta, restituendo SQL_SUCCESS o SQL_ERROR (viene restituita alcuna informazione di diagnostica). Se l'elaborazione della funzione originale è annullata, la funzione originale restituisce SQL_ERROR e SQLSTATE HY008 (operazione annullata).  
  
 Se una funzione viene eseguita quando **SQLCancelHandle** viene chiamato su un altro thread per annullare la funzione, è possibile che la funzione abbia esito positivo e restituisce SQL_SUCCESS, l'annullamento per rendere effettive. Una chiamata a **SQLCancelHandle** non ha alcun effetto se l'operazione è stata completata prima **SQLCancelHandle** è stato in grado di annullare l'operazione.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Annullamento di una funzione in esecuzione in modalità asincrona su un handle di istruzione, annullamento di una funzione in un'istruzione che necessita di dati o l'annullamento di una funzione in esecuzione in un'istruzione in un altro thread.|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Esecuzione asincrona (metodo di polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
