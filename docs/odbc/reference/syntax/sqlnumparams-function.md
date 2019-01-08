---
title: Funzione SQLNumParams | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLNumParams
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLNumParams
helpviewer_keywords:
- SQLNumParams function [ODBC]
ms.assetid: dbf2da44-253b-4094-bd6b-29bafc23c7a3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7df49e572b910bee5627b8cb2d14f067c314a3f
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53205300"
---
# <a name="sqlnumparams-function"></a>Funzione SQLNumParams
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLNumParams** restituisce il numero di parametri in un'istruzione SQL.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLNumParams(  
     SQLHSTMT        StatementHandle,  
     SQLSMALLINT *   ParameterCountPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *ParameterCountPtr*  
 [Output] Puntatore a un buffer in cui restituire il numero di parametri nell'istruzione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLNumParams** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLNumParams** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. Il **SQLNumParams** funzione è stata chiamata e, prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** veniva chiamato sul *StatementHandle* ; la **SQLNumParams** funzione è stata chiamata quindi nuovamente sul *StatementHandle*.<br /><br /> OR, il **SQLNumParams** funzione è stata chiamata e, prima esecuzione, completata **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle*  da un thread diverso in un'applicazione multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata prima di chiamare la funzione **SQLPrepare** oppure **SQLExecDirect** per il *StatementHandle*.<br /><br /> (DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLNumParams** funzione è stata chiamata.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **SQLNumParams** può essere chiamato solo dopo aver **SQLPrepare** è stato chiamato.  
  
 Se l'istruzione associata *StatementHandle* non contiene parametri, **SQLNumParams** imposta **ParameterCountPtr* su 0.  
  
 Il numero di parametri restituiti da **SQLNumParams** è lo stesso valore del campo SQL_DESC_COUNT dell'IPD.  
  
 Per altre informazioni, vedere [che descrive i parametri](../../../odbc/reference/develop-app/describing-parameters.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a un parametro|[Funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Restituzione di informazioni su un parametro in un'istruzione|[Funzione SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
