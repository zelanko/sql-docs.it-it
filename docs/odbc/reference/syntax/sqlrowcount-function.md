---
title: Funzione SQLRowCount . Documenti Microsoft
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2cbca03e7c3e381b803196a1bf7bb227ebeea03b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293371"
---
# <a name="sqlrowcount-function"></a>SQLRowCount Function
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLRowCount** restituisce il numero di righe interessate da **un'istruzione UPDATE**, **INSERT**o **DELETE;** un'operazione di SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK in **SQLBulkOperations**; o un'operazione di SQL_UPDATE o SQL_DELETE in **SQLSetPos**.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *RowCountPtr*  
 [Uscita] Punta a un buffer in cui restituire un conteggio delle righe. Per le istruzioni **UPDATE**, **INSERT**e **DELETE,** per le operazioni SQL_ADD, SQL_UPDATE_BY_BOOKMARK e SQL_DELETE_BY_BOOKMARK in **SQLBulkOperations**e per le operazioni SQL_UPDATE o SQL_DELETE in **SQLSetPos**, il valore restituito in*RowCountPtr* è il numero di righe interessate dalla richiesta o -1 se il numero di righe interessate non è disponibile.  
  
 Quando viene chiamato **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, **SQLSetPos o SQLMoreResults** , il campo SQL_DIAG_ROW_COUNT della struttura dei dati di diagnostica viene impostato sul conteggio delle righe e il conteggio delle righe viene memorizzato nella cache in modo dipendente dall'implementazione. **SQLRowCount** restituisce il valore del conteggio delle righe memorizzato nella cache. Il valore del conteggio delle righe memorizzato nella cache è valido finché l'handle dell'istruzione non viene impostato sullo stato preparato o allocato, l'istruzione viene rieseguita o viene chiamato **SQLCloseCursor.** Si noti che se una funzione è stata chiamata dopo l'impostazione del campo SQL_DIAG_ROW_COUNT, il valore restituito da **SQLRowCount** potrebbe essere diverso dal valore nel campo SQL_DIAG_ROW_COUNT perché il campo SQL_DIAG_ROW_COUNT viene reimpostato su 0 da qualsiasi chiamata di funzione.  
  
 Per altre istruzioni e funzioni, il driver può \*definire il valore restituito in *RowCountPtr*. Ad esempio, alcune origini dati potrebbero essere in grado di restituire il numero di righe restituite da un'istruzione **SELECT** o da una funzione di catalogo prima di recuperare le righe.  
  
> [!NOTE]  
>  Molte origini dati non possono restituire il numero di righe in un set di risultati prima di recuperarle. per la massima interoperabilità, le applicazioni non devono basarsi su questo comportamento.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLRowCount** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLRowCount** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLRowCount.This** asynchronous function was still executing when the SQLRowCount function was called.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) la funzione è stata chiamata prima di chiamare **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** per *StatementHandle*.<br /><br /> (DM) una funzione in esecuzione in modo asincrono è stata chiamata per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Se l'ultima istruzione SQL eseguita sull'handle dell'istruzione non è stata un'istruzione **UPDATE**, **INSERT**o **DELETE** oppure se l'argomento *Operation* nella precedente chiamata a **SQLBulkOperations** non era SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK oppure se l'argomento *Operation* nella precedente chiamata a **SQLSetPos** non era SQL_UPDATE o SQL_DELETE, il valore di*RowCountPtr* è definito dal driver. Per ulteriori informazioni, vedere [Determinazione del numero di righe interessate](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
