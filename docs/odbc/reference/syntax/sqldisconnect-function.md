---
title: Funzione SQLDisconnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 444e41699c1a61acb82acc419a2f23db6142f7bb
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537547"
---
# <a name="sqldisconnect-function"></a>Funzione SQLDisconnect
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLDisconnect** chiude la connessione associata a un handle di connessione specifica.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>Argomenti  
 *ConnectionHandle*  
 [Input] Handle di connessione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLDisconnect** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_DBC e un *gestiscono* dei *ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLDisconnect** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01002|Errore di disconnessione|Si è verificato un errore durante la disconnessione. Tuttavia, la disconnessione è stata completata. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08003|Connessione non aperta|(DM) la connessione specificata nell'argomento *ConnectionHandle* non è stato aperto.|  
|25000|Stato della transazione non valido|Si è verificato una transazione in corso la connessione specificata dall'argomento *ConnectionHandle*. La transazione rimane attiva.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *ConnectionHandle*. È stata chiamata la funzione, e prima che l'esecuzione di impostandolo [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) è stato chiamato sulle *ConnectionHandle*. Quindi la funzione è stata chiamata nuovamente sul *ConnectionHandle*.<br /><br /> La funzione è stata chiamata e prima di completare l'esecuzione **SQLCancelHandle** è stato chiamato sulle *ConnectionHandle* da un thread diverso in un'applicazione multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione un *StatementHandle* associati con la *ConnectionHandle* ed era ancora in esecuzione quando **SQLDisconnect** era viene chiamato.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *ConnectionHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per un *StatementHandle*  associata con il *ConnectionHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta, mentre la connessione è ancora attiva. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *ConnectionHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 Se un'applicazione chiama **SQLDisconnect** dopo **SQLBrowseConnect** restituisce SQL_NEED_DATA e prima di restituire un codice restituito diverso, il driver Annulla la connessione al processo di esplorazione e restituisce la connessione a uno stato non connesso.  
  
 Se un'applicazione chiama **SQLDisconnect** se è presente una transazione incompleta associata al punto di connessione, il driver restituisce SQLSTATE 25000 (stato di transazione non valido), che indica che la transazione rimane invariata e la connessione è aperta. È uno che non è stato eseguito il commit o rollback con una transazione incompleta **SQLEndTran**.  
  
 Se un'applicazione chiama **SQLDisconnect** prima che lo ha liberato tutte le istruzioni associate alla connessione, il driver, dopo aver correttamente si disconnette dall'origine dati, libera le istruzioni e tutti i descrittori di cui sono stato allocato in modo esplicito per la connessione. Tuttavia, se una o più delle istruzioni associate alla connessione sono ancora in esecuzione in modo asincrono, **SQLDisconnect** restituisce SQL_ERROR con il valore SQLSTATE HY010 (funzione di errore nella sequenza). È inoltre **SQLDisconnect** libererà istruzioni tutti i relativi e tutti i descrittori sono stati allocati in modo esplicito per la connessione, se la connessione è in uno stato sospeso o se **SQLDisconnect** era è stata annullata dal **SQLCancelHandle**.  
  
 Per informazioni sull'utilizzo di un'applicazione **SQLDisconnect**, vedere [disconnessione da un'origine dati o Driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="disconnecting-from-a-pooled-connection"></a>Disconnessione da una connessione in pool  
 Se il pool di connessioni è abilitato per un ambiente condiviso e un'applicazione chiama **SQLDisconnect** su una connessione in tale ambiente, viene restituita al pool di connessioni e ancora disponibile ad altri componenti tramite la connessione lo stesso ambiente condiviso.  
  
## <a name="code-example"></a>Esempio di codice  
 Visualizzare [ODBC programma di esempio](../../../odbc/reference/sample-odbc-program.md), [funzione SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), e [funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Allocazione di un handle|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Connessione a un'origine dati|[Funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|La connessione a un'origine dati tramite una finestra di dialogo o stringa di connessione|[Funzione SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|L'esecuzione di un'operazione di commit o rollback|[Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Rilascio di un handle di connessione|[Funzione SQLFreeConnect](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
