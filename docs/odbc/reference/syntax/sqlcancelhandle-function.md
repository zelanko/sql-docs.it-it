---
title: Funzione SQLCancelHandle . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 059ed283032feb96ca5e6b12520682ccb034752a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299666"
---
# <a name="sqlcancelhandle-function"></a>Funzione SQLCancelHandle
**Conformità**  
 Versione introdotta: ODBC 3.8  
  
 Conformità agli standard: Nessuno  
  
 Si prevede che la maggior parte dei driver ODBC 3.8 (e versioni successive) implementerà questa funzione. In caso contrario, una chiamata a **SQLCancelHandle** con un handle di connessione nel parametro *Handle* restituirà SQL_ERROR con un oggetto SQLSTATE di IM001 e il messaggio 'Driver does not support this function' Una chiamata a **SQLCancelHandle** con un handle di istruzione come parametro *Handle* verrà eseguito il mapping a una chiamata a **SQLCancel** da Gestione Driver e può essere elaborata se il driver implementa **SQLCancel**. Un'applicazione può utilizzare **SQLGetFunctions** per determinare se un driver supporta **SQLCancelHandle**.  
  
 **Riepilogo**  
 **SQLCancelHandle** annulla l'elaborazione su una connessione o un'istruzione. Gestione Driver esegue il mapping di una chiamata a **SQLCancelHandle** a una chiamata a **SQLCancel** quando *HandleType* è SQL_HANDLE_STMT.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>Argomenti  
 *HandleType*  
 [Ingresso] Tipo di maniglia su cui eseguire l'elaborazione. I valori validi sono SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
 *Handle*  
 [Ingresso] Handle in cui annullare l'elaborazione.  
  
 Se *Handle* non è un handle valido del tipo specificato da *HandleType*, **SQLCancelHandle** restituisce SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLCancelHandle** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un handle di istruzione *Handle* o un *HandleType* di SQL_HANDLE_DBC e un handle di connessione *Handle*.  
  
 Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLCancelHandle** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) nell'argomento * \*BufferMessaggio* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|È stata chiamata una funzione correlata all'istruzione in esecuzione in modo asincrono per uno degli handle di istruzione associati a *Handle*e *HandleType* è stato impostato su SQL_HANDLE_DBC. La funzione asincrona era ancora in esecuzione quando **SQLCancelHandle** è stato chiamato.<br /><br /> (DM) l'argomento *HandleType* è stato SQL_HANDLE_STMT; una funzione in esecuzione asincrona è stata chiamata sull'handle di connessione associato; e la funzione era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per uno degli handle di istruzione associati *a Handle* e *HandleType* è stato impostato su SQL_HANDLE_DBC e ha restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> **SQLBrowseConnect** è stato chiamato per *ConnectionHandle*e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima del completamento del processo di esplorazione.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo/opzione non valido|*HandleType* è stato impostato su SQL_HANDLE_ENV o SQL_HANDLE_DESC.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) Il driver associato *all'handle* non supporta la funzione.|  
  
 Se **SQLCancelHandle** viene chiamato con *HandleType* impostato su SQL_HANDLE_STMT, può restituire qualsiasi SQLSTATE che può essere restituito dalla funzione **SQLCancel**.  
  
## <a name="comments"></a>Commenti  
 Questa funzione è simile a **SQLCancel,** ma può accettare una connessione o un handle di istruzione come parametro anziché solo un handle di istruzione. Gestione Driver esegue il mapping di una chiamata a **SQLCancelHandle** a una chiamata a **SQLCancel** quando *HandleType* è SQL_HANDLE_STMT. Ciò consente alle applicazioni di utilizzare **SQLCancelHandle** per annullare le operazioni di istruzione anche se il driver non implementa **SQLCancelHandle**.  
  
 Per ulteriori informazioni sull'annullamento di un'operazione di istruzione, vedere [Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md).  
  
 Se non sono presenti operazioni in corso su *Gestire* la chiamata a **SQLCancelHandle** non ha alcun effetto.  
  
 **SQLCancelHandle** su un handle di connessione può annullare i seguenti tipi di elaborazione:  
  
-   Funzione in esecuzione in modo asincrono sulla connessione.  
  
-   Funzione in esecuzione sull'handle di connessione in un altro thread.  
  
 Quando **SQLCancelHandle** viene chiamato per annullare una funzione in esecuzione in modo asincrono in una connessione, i record di diagnostica registrati da **SQLCancelHandle** vengono aggiunti a quelli restituiti dall'operazione in fase di annullamento; **SQLCancelHandle** non restituisce record di diagnostica, tuttavia, quando si annulla una funzione in esecuzione su una connessione in un altro thread.  
  
 L'utilizzo di **SQLCancelHandle** per annullare **SQLEndTran** può mettere la connessione in stato sospeso. Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  Per informazioni su come utilizzare **SQLCancelHandle** in un'applicazione che verrà distribuita in un sistema operativo Windows precedente a Windows 7, vedere Matrice di [compatibilità](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>Annullamento dell'elaborazione asincrona correlata alla connessioneCanceling Connection-Related Asynchronous Processing  
 Se una funzione restituisce SQL_STILL_EXECUTING, un'applicazione può chiamare **SQLCancelHandle** per annullare l'operazione. Se la richiesta di annullamento ha esito positivo, **SQLCancelHandle** restituisce SQL_SUCCESS. Ciò non significa che la funzione originale è stata annullata; indica che la richiesta di annullamento è stata elaborata. Il driver e l'origine dati determinano quando o se l'operazione viene annullata. L'applicazione deve continuare a chiamare la funzione originale fino a quando non viene SQL_STILL_EXECUTING il codice restituito. Se la funzione originale è stata annullata, il codice restituito viene SQL_ERROR e SQLSTATE HY008 (Operazione annullata). Se la funzione originale ha completato l'elaborazione normale (non è stata annullata), il codice restituito viene SQL_SUCCESS o SQL_SUCCESS_WITH_INFO oppure SQL_ERROR e un SQLSTATE diverso da HY008 (operazione annullata), se la funzione originale non è riuscita.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>Annullamento di funzioni in esecuzione su un altro threadCanceling Functions Executing on Another Thread  
 In un'applicazione multithread, l'applicazione può annullare un'operazione in esecuzione su un altro thread. Per annullare l'operazione, l'applicazione chiama **SQLCancelHandle** con l'handle utilizzato dalla funzione, ma in un thread diverso. Il driver e il sistema operativo determinano la modalità di annullamento dell'operazione. Il codice restituito **SQLCancelHandle** indica se il driver ha elaborato la richiesta, restituendo SQL_SUCCESS o SQL_ERROR (non vengono restituite informazioni di diagnostica). Se l'elaborazione sulla funzione originale viene annullata, la funzione originale restituisce SQL_ERROR e SQLSTATE HY008 (Operazione annullata).  
  
 Se una funzione viene eseguita quando **SQLCancelHandle** viene chiamato su un altro thread per annullare la funzione, è possibile che la funzione abbia esito positivo e restituisca SQL_SUCCESS prima che l'annullamento abbia effetto. Una chiamata a **SQLCancelHandle** non ha alcun effetto se l'operazione è stata completata prima che **SQLCancelHandle** fosse in grado di annullare l'operazione.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Annullamento di una funzione in esecuzione in modo asincrono su un handle di istruzione, annullamento di una funzione in un'istruzione che richiede dati o annullamento di una funzione in esecuzione su un'istruzione in un altro thread.|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Esecuzione asincrona (metodo di polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
