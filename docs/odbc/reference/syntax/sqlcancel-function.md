---
title: Funzione SQLCancel | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4ad701efe914780a74bba3b8f0530b4881d7709
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537625"
---
# <a name="sqlcancel-function"></a>Funzione SQLCancel
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLCancel** Annulla l'elaborazione in un'istruzione.  
  
 Per annullare l'elaborazione in un'istruzione o di connessione, usare [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLCancel** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLCancel** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) nell'argomento  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLCancel** funzione è stata chiamata.<br /><br /> (DM) annullare l'operazione non riuscita perché un'operazione asincrona è in esecuzione su un handle di connessione che è associato *StatementHandle*.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY018|Richiesta di annullamento. il server ha rifiutato|Il server ha rifiutato la richiesta di annullamento.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 **SQLCancel** può annullare i seguenti tipi di elaborazione in un'istruzione:  
  
-   Una funzione in esecuzione in modalità asincrona dell'istruzione.  
  
-   Una funzione in un'istruzione che necessita di dati.  
  
-   Una funzione che esegue l'istruzione in un altro thread.  
  
 In ODBC 2. *x*, se un'applicazione chiama **SQLCancel** quando non si è fatta alcuna elaborazione nell'istruzione **SQLCancel** ha lo stesso effetto **SQLFreeStmt** con l'opzione di SQL_CLOSE. Questo comportamento viene definito solo per motivi di completezza e le applicazioni devono chiamare **SQLFreeStmt** oppure **SQLCloseCursor** per chiudere i cursori.  
  
 Quando **SQLCancel** viene chiamato per annullare una funzione in esecuzione in modo asincrono in un'istruzione o una funzione in un'istruzione che vengono cancellati esigenze di dati, i record di diagnostica registrati mediante la funzione viene annullata, e **SQLCancel**  invia il proprio record di diagnostica; quando **SQLCancel** viene chiamato per annullare una funzione in esecuzione in un'istruzione in un altro thread, tuttavia, non cancella la diagnostica dei record annullata (funzione) e non non registrare i propri record di diagnostica.  
  
## <a name="canceling-asynchronous-processing"></a>Annullare l'elaborazione asincrona  
 Dopo avere un'applicazione chiama una funzione in modo asincrono, chiama la funzione più volte per determinare se ha terminato l'elaborazione. Se la funzione è in corso l'elaborazione, verrà restituito SQL_STILL_EXECUTING. Se la funzione ha completato l'elaborazione, viene restituito un codice diverso.  
  
 Dopo ogni chiamata alla funzione che restituisce SQL_STILL_EXECUTING, un'applicazione può chiamare **SQLCancel** per annullare la funzione. Se la richiesta di annullamento ha esito positivo, il driver restituisce SQL_SUCCESS. Questo messaggio non indica che la funzione è stata effettivamente annullata; indica che è stata elaborata la richiesta di annullamento. Quando o se la funzione viene annullata in realtà è dipendente dal driver e dipende dall'origine dati. L'applicazione deve continuare a chiamare la funzione originale fino a quando il codice restituito non SQL_STILL_EXECUTING. Se la funzione è stata annullata correttamente, il codice restituito è SQL_ERROR e SQLSTATE HY008 (operazione annullata). Se la funzione è stata completata la normale elaborazione, il codice restituito è SQL_SUCCESS o SQL_SUCCESS_WITH_INFO se la funzione ha esito positivo o SQL_ERROR e un valore SQLSTATE di diverso da HY008 (operazione annullata) se la funzione ha esito negativo.  
  
> [!NOTE]  
>  In ODBC 3.5, una chiamata a **SQLCancel** quando è in corso effettuata alcuna elaborazione nell'istruzione non viene considerata **SQLFreeStmt** con l'opzione di SQL_CLOSE, ma ha non è affatto alcun effetto. Per chiudere un cursore, un'applicazione deve chiamare **SQLCloseCursor**, non **SQLCancel**.  
  
 Per altre informazioni sull'elaborazione asincrona, vedere [esecuzione asincrona](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).  
  
## <a name="canceling-functions-that-need-data"></a>Annullamento di funzioni che richiedono i dati  
 Dopo aver **SQLExecute** oppure **SQLExecDirect** restituisce SQL_NEED_DATA e prima dell'invio dei dati per tutti i parametri data-at-execution, un'applicazione può chiamare **SQLCancel** Per annullare l'esecuzione dell'istruzione. Dopo l'istruzione è stata annullata, l'applicazione può chiamare **SQLExecute** oppure **SQLExecDirect** nuovamente. Per altre informazioni, vedere [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Dopo aver **SQLBulkOperations** oppure **SQLSetPos** restituisce SQL_NEED_DATA e prima dell'invio dei dati per tutte le colonne data-at-execution, un'applicazione può chiamare **SQLCancel** Per annullare l'operazione. Dopo l'operazione è stata annullata, l'applicazione può chiamare **SQLBulkOperations** oppure **SQLSetPos** anche in questo caso, l'annullamento non influisce sullo stato del cursore o la posizione corrente del cursore. Per altre informazioni, vedere [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) oppure [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="canceling-functions-executing-on-another-thread"></a>Annullamento di funzioni in esecuzione su un altro Thread  
 In un'applicazione multithread, l'applicazione può annullare una funzione che è in esecuzione in un altro thread. Per annullare la funzione, l'applicazione chiama **SQLCancel** con lo stesso handle di istruzione a quella usata dalla funzione di destinazione, ma in un thread diverso. Modalità con cui annullare la funzione dipende dal driver e il sistema operativo. Come annullare una funzione che esegue in modo asincrono, il codice restituito del **SQLCancel** indica solo se il driver di elaborata la richiesta correttamente. Può essere restituita solo SQL_SUCCESS o SQL_ERROR. viene restituita alcuna informazione di diagnostica. Se la funzione originale è stata annullata, viene restituito SQL_ERROR e SQLSTATE HY008 (operazione annullata).  
  
 Se un'istruzione SQL viene eseguita quando **SQLCancel** viene chiamato su un altro thread per annullare l'esecuzione di istruzione, è possibile che l'esecuzione abbia esito positivo e restituito SQL_SUCCESS durante l'operazione di annullamento anche ha esito positivo. In questo caso, gestione Driver presuppone che il cursore aperto per l'esecuzione dell'istruzione viene chiuso per l'annullamento, pertanto l'applicazione non saranno in grado di usare il cursore.  
  
 Per altre informazioni sul threading, vedere [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a un parametro|[Funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Esecuzione bulk insert o operazioni di aggiornamento|[Funzione SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Annulla una funzione in esecuzione in modo asincrono in un handle di connessione, anche per le funzionalità di **SQLCancel**.|[Funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Esecuzione di un'istruzione SQL|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Rilascio di un handle di istruzione|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Recupero di un campo di un record di diagnostica o un campo dell'intestazione di diagnostica|[Funzione SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|Recupero di più campi di una struttura di dati di diagnostica|[Funzione SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|Restituisce il parametro successivo per l'invio di dati|[Funzione SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|L'invio dei dati di parametro in fase di esecuzione|[Funzione SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Posizionando il cursore in un set di righe, l'aggiornamento dei dati del set di righe o l'aggiornamento o eliminazione dei dati nel set di risultati|[Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
