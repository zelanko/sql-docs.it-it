---
title: Funzione SQLDisconnect . Documenti Microsoft
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5ea73919fbe90719d881fb43108ab1934933708
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301151"
---
# <a name="sqldisconnect-function"></a>Funzione SQLDisconnect
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLDisconnect** chiude la connessione associata a un handle di connessione specifico.  
  
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
 Quando **SQLDisconnect** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_DBC e un *handle* di *ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLDisconnect** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01002|Errore di disconnessione|Si è verificato un errore durante la disconnessione. Tuttavia, la disconnessione ha avuto esito positivo. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08003|Connessione non aperta|(DM) La connessione specificata nell'argomento *ConnectionHandle* non è stata aperta.|  
|25000|Stato della transazione non valido|Si è verificata una transazione in corso sulla connessione specificata dall'argomento *ConnectionHandle*. La transazione rimane attiva.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *ConnectionHandle*. La funzione è stata chiamata e prima dell'esecuzione della [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) è stata chiamata su *ConnectionHandle*. Quindi la funzione è stata chiamata nuovamente su *ConnectionHandle*.<br /><br /> La funzione è stata chiamata e prima del termine dell'esecuzione di **SQLCancelHandle** è stata chiamata su *ConnectionHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) una funzione in esecuzione in modo asincrono è stata chiamata per un *StatementHandle* associato il *ConnectionHandle* ed era ancora in esecuzione quando **SQLDisconnect** è stato chiamato.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *ConnectionHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per un *statementHandle* associato a *ConnectionHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta e la connessione sia ancora attiva. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) Il driver associato a *ConnectionHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 Se un'applicazione chiama **SQLDisconnect** dopo **SQLBrowseConnect** restituisce SQL_NEED_DATA e prima che restituisca un codice restituito diverso, il driver annulla il processo di esplorazione della connessione e restituisce la connessione a uno stato non connesso.  
  
 Se un'applicazione chiama **SQLDisconnect** mentre è presente una transazione incompleta associata all'handle di connessione, il driver restituisce SQLSTATE 25000 (stato della transazione non valido), che indica che la transazione è invariata e la connessione è aperta. Una transazione incompleta è una transazione di cui non è stato eseguito il commit o il rollback con **SQLEndTran**.  
  
 Se un'applicazione chiama **SQLDisconnect** prima di aver liberato tutte le istruzioni associate alla connessione, il driver, dopo la disconnessione dall'origine dati, libera tali istruzioni e tutti i descrittori che sono stati allocati in modo esplicito sulla connessione. Tuttavia, se una o più delle istruzioni associate alla connessione sono ancora in esecuzione in modo asincrono, **SQLDisconnect** restituisce SQL_ERROR con un valore SQLSTATE di HY010 (errore di sequenza di funzioni). Inoltre, **SQLDisconnect** libererà tutte le istruzioni associate e tutti i descrittori che sono stati allocati in modo esplicito nella connessione, se la connessione è in uno stato sospeso o se **SQLDisconnect** è stato annullato correttamente da **SQLCancelHandle**.  
  
 Per informazioni sull'utilizzo di **SQLDisconnect**da parte di un'applicazione, vedere [Disconnessione da un'origine dati o da un driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="disconnecting-from-a-pooled-connection"></a>Disconnessione da una connessione in pool  
 Se il pool di connessioni è abilitato per un ambiente condiviso e un'applicazione chiama **SQLDisconnect** su una connessione in tale ambiente, la connessione viene restituita al pool di connessioni ed è ancora disponibile per altri componenti che utilizzano lo stesso ambiente condiviso.  
  
## <a name="code-example"></a>Esempio di codice  
 Vedere [Programma ODBC di esempio](../../../odbc/reference/sample-odbc-program.md), Funzione [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)e Funzione [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Allocazione di una maniglia|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Connessione a un'origine dati|[Funzione SQLConnectSQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Connessione a un'origine dati tramite una stringa di connessione o una finestra di dialogoConnecting to a data source using a connection string or dialog box|[SQLDriverConnect Function](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Esecuzione di un'operazione di commit o rollbackExecuting a commit or rollback operation|[SQLEndTran Function](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Liberare un handle di connessione|[Funzione SQLFreeConnect](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
