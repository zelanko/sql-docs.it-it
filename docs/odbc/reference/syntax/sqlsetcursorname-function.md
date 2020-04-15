---
title: Funzione SQLSetCursorName . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a3bcd07a39401d49be04d141e50c671179efb16
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287341"
---
# <a name="sqlsetcursorname-function"></a>Funzione SQLSetCursorName
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLSetCursorName** associa un nome di cursore a un'istruzione attiva. Se un'applicazione non chiama **SQLSetCursorName**, il driver genera i nomi dei cursori in base alle esigenze per l'elaborazione dell'istruzione SQL.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *CursorName (Nome Cursore)*  
 [Ingresso] Nome del cursore. Per un'elaborazione efficiente, il nome del cursore non deve includere spazi iniziali o finali nel nome del cursore e se il nome del cursore include un identificatore delimitato, il delimitatore deve essere posizionato come primo carattere nel nome del cursore.  
  
 *NameLength*  
 [Ingresso] Lunghezza in caratteri di*nomecursore*.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSetCursorName** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *Handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLSetCursorName** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Il nome del cursore ha superato il limite massimo, pertanto è stato utilizzato solo il numero massimo di caratteri consentito.|  
|24000|Stato del cursore non valido|L'istruzione corrispondente a *StatementHandle* era già in uno stato eseguito o posizionato con il cursore.|  
|34000|Nome di cursore non valido|Il nome del cursore specificato in *, CursorName* non era valido perché ha superato la lunghezza massima definita dal driver o ha iniziato con "SQLCUR" o "SQL_CUR".|  
|3C000|Nome cursore duplicato|Il nome del cursore specificato in *, CursorName* esiste già.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I009|Utilizzo non valido del puntatore null|(DM) l'argomento *CursorName* era un puntatore null.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione aynchronous era ancora in esecuzione quando è stata chiamata la funzione **SQLSetCursorName.**<br /><br /> (DM) una funzione in esecuzione in modo asincrono è stata chiamata per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) l'argomento *NameLength* era minore di 0 ma non uguale a SQL_NTS.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 I nomi dei cursori vengono utilizzati solo nelle istruzioni di aggiornamento ed eliminazione posizionate (ad esempio, **UPDATE** _nome tabella_ ... **WHERE CURRENT OF** _nome-cursore_). Per ulteriori informazioni, vedere [Istruzioni di aggiornamento e eliminazione posizionate](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Se l'applicazione non chiama **SQLSetCursorName** per definire un nome di cursore, all'esecuzione di un'istruzione di query il driver genera un nome che inizia con le lettere SQL_CUR e non supera i 18 caratteri di lunghezza.  
  
 Tutti i nomi di cursore all'interno della connessione devono essere univoci. La lunghezza massima di un nome di cursore è definita dal driver. Per garantire la massima interoperabilità, è consigliabile che le applicazioni limitino i nomi dei cursori a non più di 18 caratteri. In ODBC 3 *.x*, se il nome di un cursore è un identificatore tra virgolette, viene considerato in modo con distinzione tra maiuscole e minuscole e può contenere caratteri che la sintassi di SQL non consente o tratterebbe in modo speciale, ad esempio spazi vuoti o parole chiave riservate. Se il nome di un cursore deve essere considerato in modo con distinzione tra maiuscole e minuscole, deve essere passato come identificatore tra virgolette.  
  
 Un nome di cursore impostato in modo esplicito o implicito rimane impostato fino a quando non viene eliminata l'istruzione a cui è associato, utilizzando **SQLFreeHandle**. **SQLSetCursorName** può essere chiamato per rinominare un cursore in un'istruzione, purché il cursore si trova in uno stato allocato o preparato.  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente un'applicazione utilizza **SQLSetCursorName** per impostare un nome di cursore per un'istruzione. Viene quindi utilizzata tale istruzione per recuperare i risultati dalla tabella CUSTOMERS. Infine, esegue un aggiornamento posizionato per modificare il numero di telefono di John Smith. Si noti che l'applicazione utilizza handle di istruzione diversi per le istruzioni **SELECT** e **UPDATE.**  
  
 Per un altro esempio di codice, vedere [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp  
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
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Restituzione del nome di un cursore|[Funzione SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Impostazione delle opzioni di scorrimento del cursore|[Funzione SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
