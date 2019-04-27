---
title: Funzione SQLSetCursorName | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetCursorName
helpviewer_keywords:
- SQLSetCursorName function [ODBC]
ms.assetid: 4e055946-12d4-4589-9891-41617a50f34e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2606f7ec05df6422135220605087b81ac7ec4f50
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62742247"
---
# <a name="sqlsetcursorname-function"></a>Funzione SQLSetCursorName
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLSetCursorName** associa un nome di cursore con un'istruzione attiva. Se un'applicazione non chiama **SQLSetCursorName**, il driver genera nomi dei cursori in base alle necessità per l'elaborazione di istruzione SQL.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *Nomecursore*  
 [Input] Nome del cursore. Elaborare con efficienza, il nome del cursore non deve includere spazi iniziali o finali nel nome del cursore e se il nome del cursore include identificatori delimitati, il delimitatore deve essere inserito come primo carattere nel nome del cursore.  
  
 *NameLength*  
 [Input] Lunghezza in caratteri della **Nomecursore*.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSetCursorName** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLSetCursorName** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Il nome del cursore ha superato il limite massimo, pertanto è stato usato solo il numero massimo consentito di caratteri.|  
|24000|Stato del cursore non valido|L'istruzione corrispondente *StatementHandle* era già stato eseguito o cursore posizionato.|  
|34000|Nome di cursore non valido|Il nome di cursore specificato in **Nomecursore* non è valido perché perché supera la lunghezza massima definita dal driver, i o "SQLCUR" o "SQL_CUR."|  
|3C000|Nome di cursore duplicato|Il nome di cursore specificato in **Nomecursore* esiste già.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY009|Utilizzo non valido del puntatore null|(DM) dell'argomento *Nomecursore* era un puntatore null.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione aynchronous era ancora in esecuzione quando il **SQLSetCursorName** funzione è stata chiamata.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione la *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) dell'argomento *lunghezzanome non* era minore di 0, ma non è uguale a SQL_NTS.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Nomi dei cursori vengono utilizzati solo per gli aggiornamenti posizionati ed eliminare le istruzioni (ad esempio, **aggiornare** _nome-tabella_ ... **WHERE CURRENT OF** _-nome del cursore_). Per altre informazioni, vedere [istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Se l'applicazione non chiama **SQLSetCursorName** per definire un nome di cursore, durante l'esecuzione di un'istruzione di query il driver genera un nome che inizia con le lettere SQL_CUR e non superare i 18 caratteri.  
  
 Tutti i nomi di cursore all'interno della connessione devono essere univoci. La lunghezza massima di un nome di cursore è definita dal driver. Per garantire la massima interoperabilità, è consigliabile che le applicazioni limitare i nomi di cursore a non più di 18 caratteri. In ODBC 3*x*, se un nome di cursore è un identificatore con virgolette, viene trattata in modo distinzione maiuscole/minuscole e può contenere caratteri che la sintassi SQL non autorizza o gestisce in modo speciale, ad esempio gli spazi vuoti o parole chiave riservate. Se un nome di cursore deve essere trattato in modo tra maiuscole e minuscole, deve essere passato come un identificatore tra virgolette.  
  
 Impostare un nome di cursore che viene impostato in modo esplicito o implicito è rimasto fino a quando non viene eliminata l'istruzione con cui è associato, usando **SQLFreeHandle**. **SQLSetCursorName** può essere chiamato per rinominare un cursore su un'istruzione fino a quando il cursore si trova in uno stato allocato o preparato.  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, un'applicazione utilizza **SQLSetCursorName** per impostare un nome di cursore per un'istruzione. Tale istruzione viene quindi utilizzato per recuperare i risultati della tabella CUSTOMERS. Infine, esegue un aggiornamento posizionato per modificare il numero di telefono di John Smith. Si noti che l'applicazione usa gli handle di istruzione diverso per il **selezionate** e **UPDATE** istruzioni.  
  
 Per un altro esempio di codice, vedere [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
#define NAME_LEN 50  
#define PHONE_LEN 10  
  
SQLHSTMT     hstmtSelect,  
SQLHSTMT     hstmtUpdate;  
SQLRETURN    retcode;  
SQLHDBC      hdbc;  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   cbName, cbPhone;  
  
/* Allocate the statements and set the cursor name. */  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtSelect);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtUpdate);  
SQLSetCursorName(hstmtSelect, "C1", SQL_NTS);  
  
/* SELECT the result set and bind its columns to local buffers. */  
  
SQLExecDirect(hstmtSelect,  
      "SELECT NAME, PHONE FROM CUSTOMERS",  
      SQL_NTS);  
SQLBindCol(hstmtSelect, 1, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
SQLBindCol(hstmtSelect, 2, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);  
  
/* Read through the result set until the cursor is */  
/* positioned on the row for John Smith. */  
  
do  
 retcode = SQLFetch(hstmtSelect);  
while ((retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) &&  
   (strcmp(szName, "Smith, John") != 0));  
  
/* Perform a positioned update of John Smith's name. */  
  
if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
   SQLExecDirect(hstmtUpdate,  
   "UPDATE EMPLOYEE SET PHONE=\"2064890154\" WHERE CURRENT OF C1",  
   SQL_NTS);  
}  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Esecuzione di un'istruzione SQL|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Restituzione di un nome di cursore|[Funzione SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|L'impostazione di scorrere le opzioni di cursore|[Funzione SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
