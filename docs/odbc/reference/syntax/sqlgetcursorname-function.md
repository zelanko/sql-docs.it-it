---
title: Funzione SQLGetCursorName . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetCursorName
helpviewer_keywords:
- SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3ac65dc07897ddc789ee03b06b1bc1f71d37c3c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285549"
---
# <a name="sqlgetcursorname-function"></a>Funzione SQLGetCursorName
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLGetCursorName** restituisce il nome del cursore associato a un'istruzione specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *CursorName (Nome Cursore)*  
 [Uscita] Puntatore a un buffer in cui restituire il nome del cursore.  
  
 Se *CursorName* è NULL, *NameLengthPtr* restituirà comunque il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui punta *CursorName*.  
  
 *BufferLength*  
 [Ingresso] Lunghezza \*di *CursorName*, in caratteri. Se il valore in * \*CursorName* è una stringa Unicode (quando si chiama **SQLGetCursorNameW**), il *BufferLength* argomento deve essere un numero pari.  
  
 *NameLengthPtr*  
 [Uscita] Puntatore alla memoria in cui restituire il numero totale di caratteri (escluso il carattere di terminazione null) disponibili per la restituzione in \* *CursorName*. Se il numero di caratteri disponibili per la restituzione è \*maggiore o uguale a *BufferLength*, il nome del cursore in *CursorName* verrà troncato a *BufferLength* meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetCursorName** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *Handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetCursorName** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Il \*buffer *CursorName* non era sufficientemente grande per restituire l'intero nome del cursore, pertanto il nome del cursore è stato troncato. La lunghezza del nome del cursore non troncato viene restituita in*NameLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLGetCursorName.This** asynchronous function was still executing when the SQLGetCursorName function was called.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono è stata chiamata per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY015 (informazioni in stato INCUI)|Nessun nome cursore disponibile|(DM) il driver era un driver *.x* ODBC 2, non era presente alcun cursore aperto sull'istruzione e nessun nome di cursore era stato impostato con **SQLSetCursorName**.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore specificato nell'argomento *BufferLength* è minore di 0.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 I nomi dei cursori vengono utilizzati solo nelle istruzioni di aggiornamento ed eliminazione posizionate (ad esempio, **UPDATE** _nome tabella_ ... **WHERE CURRENT OF** _nome-cursore_). Per ulteriori informazioni, vedere [Istruzioni di aggiornamento e eliminazione posizionate](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Se l'applicazione non chiama **SQLSetCursorName** per definire un nome di cursore, il driver genera un nome. Questo nome inizia con le lettere SQL_CUR.  
  
> [!NOTE]
>  In ODBC 2 *.x*, quando non era presente alcun cursore aperto e nessun nome era stato impostato da una chiamata a **SQLSetCursorName**, una chiamata a **SQLGetCursorName** ha restituito SQLSTATE HY015 (nessun nome del cursore disponibile). In ODBC 3 *.x*, questo non è più vero; indipendentemente da quando **SQLGetCursorName** viene chiamato, il driver restituisce il nome del cursore.  
  
 **SQLGetCursorName** restituisce il nome di un cursore indipendentemente dal fatto che il nome sia stato creato in modo esplicito o implicito. Un nome di cursore viene generato in modo implicito se **SQLSetCursorName** non viene chiamato. **SQLSetCursorName** può essere chiamato per rinominare un cursore in un'istruzione, purché il cursore si trova in uno stato allocato o preparato.  
  
 Un nome di cursore impostato in modo esplicito o implicito rimane impostato fino a quando il *StatementHandle* a cui è associato viene rilasciato, utilizzando **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_STMT.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparazione di un'istruzione per l'esecuzione|[Pagina relativa alla funzione SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Impostazione del nome di un cursore|[Funzione SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
