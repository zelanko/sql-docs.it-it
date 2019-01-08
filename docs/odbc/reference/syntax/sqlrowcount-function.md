---
title: Funzione SQLRowCount | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ab7046e036a6f50f8009a481f92345d7ce12aea
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502555"
---
# <a name="sqlrowcount-function"></a>SQLRowCount Function
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLRowCount** restituisce il numero di righe interessate da un' **UPDATE**, **Inserisci**, o **eliminare** istruzione; un SQL_ADD SQL_UPDATE_BY_BOOKMARK o SQL _ Operazione DELETE_BY_BOOKMARK **SQLBulkOperations**; o in un'operazione SQL_UPDATE o SQL_DELETE **SQLSetPos**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *RowCountPtr*  
 [Output] Punta a un buffer in cui si desidera restituire un conteggio delle righe. Per la **UPDATE**, **Inserisci**, e **Elimina** istruzioni, per le operazioni SQL_ADD SQL_UPDATE_BY_BOOKMARK e SQL_DELETE_BY_BOOKMARK nel  **SQLBulkOperations**e per le operazioni SQL_UPDATE o SQL_DELETE **SQLSetPos**, il valore restituito in **RowCountPtr* è il numero di righe interessate dal richiesta oppure -1 se il numero di righe interessate non è disponibile.  
  
 Quando **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, **SQLSetPos o SQLMoreResults** viene chiamato, il SQL_DIAG_ROW_COUNT campo della struttura di dati di diagnostica è impostato per il conteggio delle righe e il conteggio delle righe viene memorizzato nella cache in modo dipendente dall'implementazione. **SQLRowCount** restituisce il valore del conteggio riga memorizzata nella cache. Il valore del conteggio riga memorizzata nella cache è valido fino a quando l'handle di istruzione viene ripristinata allo stato preparato o allocato, viene rieseguito l'istruzione, oppure **SQLCloseCursor** viene chiamato. Si noti che se una funzione è stata chiamata perché il campo SQL_DIAG_ROW_COUNT era impostato, il valore restituito da **SQLRowCount** potrebbe essere diverso dal valore nel campo SQL_DIAG_ROW_COUNT perché il campo SQL_DIAG_ROW_COUNT viene reimpostato su 0 per qualsiasi chiamata di funzione.  
  
 Per altre istruzioni e funzioni, il driver può definire il valore restituito in \* *RowCountPtr*. Ad esempio, alcune origini dati potrebbero essere in grado di restituire il numero di righe restituite da una **seleziona** istruzione o una funzione di catalogo prima di recuperare le righe.  
  
> [!NOTE]  
>  Molte origini dati non possono restituire il numero di righe in un set di risultati prima scaricarle; Per garantire la massima interoperabilità, le applicazioni non devono basarsi su questo comportamento.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLRowCount** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLRowCount** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLRowCount** funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata prima di chiamare la funzione **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** per il  *StatementHandle*.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione la *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Se l'ultima istruzione SQL eseguita nell'handle di istruzione non è un **UPDATE**, **INSERT**, o **Elimina** istruzione o se il *operazione* argomento della chiamata precedente a **SQLBulkOperations** non è stato SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK, o se il *operazione* argomento nella chiamata precedente a  **SQLSetPos** non è stata SQL_UPDATE o SQL_DELETE, il valore di **RowCountPtr* è definito dal driver. Per altre informazioni, vedere [che determina il numero di righe interessate](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Esecuzione di un'istruzione SQL|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
