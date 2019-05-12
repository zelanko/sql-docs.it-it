---
title: Funzione SQLGetCursorName | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33e2d1f4630228d4c59487c2a5f9de891e87ece5
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537373"
---
# <a name="sqlgetcursorname-function"></a>Funzione SQLGetCursorName
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLGetCursorName** restituisce il nome di cursore associato a un'istruzione specificata.  
  
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
 [Input] Handle di istruzione.  
  
 *Nomecursore*  
 [Output] Puntatore a un buffer in cui restituire il nome del cursore.  
  
 Se *Nomecursore* sia impostato su NULL *NameLengthPtr* continuerà a restituire il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui fa riferimento *Nomecursore*.  
  
 *BufferLength*  
 [Input] Lunghezza di \* *Nomecursore*, in caratteri. Se il valore in  *\*Nomecursore* è una stringa Unicode (quando si chiama **SQLGetCursorNameW**), il *BufferLength* argomento deve essere un numero pari.  
  
 *NameLengthPtr*  
 [Output] Puntatore alla memoria in cui si desidera restituire il numero totale di caratteri (escluso il carattere di terminazione null) disponibili per restituire \* *Nomecursore*. Se il numero di caratteri disponibili da restituire è maggiore o uguale a *BufferLength*, il nome del cursore nelle \* *Nomecursore* viene troncato a *BufferLength*meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetCursorName** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato può essere ottenuto chiamando **SQLGetDiagRec** con un *HandleType*SQL_HANDLE_STMT e una *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetCursorName** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Il buffer \* *Nomecursore* non sia abbastanza grande per restituire il nome del cursore intero, in modo che il nome del cursore è stato troncato. Viene restituita la lunghezza del nome del cursore non troncato **NameLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLGetCursorName** funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione la *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY015|Nessun nome di cursore disponibile.|(DM) il driver è stato un ODBC 2 *. x* driver, si è verificato alcun cursore aperto nell'istruzione e con era stato impostato alcun nome di cursore **SQLSetCursorName**.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore specificato nell'argomento *BufferLength* era minore di 0.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Nomi dei cursori vengono utilizzati solo per gli aggiornamenti posizionati ed eliminare le istruzioni (ad esempio, **aggiornare** _nome-tabella_ ... **WHERE CURRENT OF** _-nome del cursore_). Per altre informazioni, vedere [istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Se l'applicazione non chiama **SQLSetCursorName** per definire un nome di cursore, il driver genera un nome. Questo nome inizia con le lettere SQL_CUR.  
  
> [!NOTE]
>  In ODBC 2 *. x*, quando si è verificato alcun cursore aperto e nessun nome era stato impostato da una chiamata a **SQLSetCursorName**, una chiamata a **SQLGetCursorName** restituito SQLSTATE HY015 (Nessun nome di cursore disponibile). In ODBC 3 *. x*, questo non è più true; indipendentemente dal fatto che quando **SQLGetCursorName** viene chiamato, il driver restituisce il nome del cursore.  
  
 **SQLGetCursorName** restituisce il nome di un cursore o meno il nome è stato creato in modo esplicito o implicito. Se un nome di cursore viene generato in modo implicito **SQLSetCursorName** non viene chiamato. **SQLSetCursorName** può essere chiamato per rinominare un cursore su un'istruzione fino a quando il cursore si trova in uno stato allocato o preparato.  
  
 Rimane impostato fino a un nome di cursore che viene impostato in modo esplicito o implicito il *StatementHandle* con cui è associato viene eliminato, usando **SQLFreeHandle** con un *HandleType* SQL_HANDLE_STMT.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Esecuzione di un'istruzione SQL|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparazione di un'istruzione per l'esecuzione|[Funzione SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Impostazione di un nome di cursore|[Funzione SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
