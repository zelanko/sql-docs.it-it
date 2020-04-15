---
title: 'Proprietà SQLNativeSql : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLNativeSql
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLNativeSql
helpviewer_keywords:
- SQLNativeSql function [ODBC]
ms.assetid: b8efc247-27ab-4a00-92b6-1400785783fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9666bc767affb3b6bb624c416614079193d4b921
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304722"
---
# <a name="sqlnativesql-function"></a>Funzione SQLNativeSql
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLNativeSql** restituisce la stringa SQL come modificata dal driver. **SQLNativeSql** non esegue l'istruzione SQL.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLNativeSql(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      InStatementText,  
     SQLINTEGER     TextLength1,  
     SQLCHAR *      OutStatementText,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   TextLength2Ptr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *ConnectionHandle*  
 [Input] Handle di connessione.  
  
 *InStatementText (Testo InStatementText)*  
 [Ingresso] Stringa di testo SQL da tradurre.  
  
 *TestoLength1*  
 [Ingresso] Lunghezza in caratteri della stringa di testo*InStatementText.*  
  
 *Testo D'uscita*  
 [Uscita] Puntatore a un buffer in cui restituire la stringa SQL tradotta.  
  
 Se *OutStatementText* è NULL, *TextLength2Ptr* restituirà comunque il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *OutStatementText*.  
  
 *BufferLength*  
 [Ingresso] Numero di caratteri \*nel buffer *OutStatementText.* Se il valore restituito in * \*InStatementText* è una stringa Unicode (quando si chiama **SQLNativeSqlW**), l'argomento *BufferLength* deve essere un numero pari.  
  
 *TextLength2Ptr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di caratteri \*(esclusa la terminazione null) disponibili per la restituzione in *OutStatementText*. Se il numero di caratteri disponibili per la restituzione è maggiore \*o uguale a *BufferLength*, la stringa SQL tradotta in *OutStatementText* verrà troncata a *BufferLength* meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLNativeSql** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_DBC e un *handle* di *ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLNativeSql** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Il \*buffer *OutStatementText* non era sufficientemente grande per restituire l'intera stringa SQL, pertanto la stringa SQL è stata troncata. La lunghezza della stringa SQL non troncata viene restituita in*TextLength2Ptr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08003|Connessione non aperta|*ConnectionHandle* non era in uno stato connesso.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|22007|Formato datetime non valido|**InStatementText* contiene una clausola di escape con un valore di data, ora o timestamp non valido.|  
|24000|Stato del cursore non valido|Il cursore a cui si fa riferimento nell'istruzione è stato posizionato prima dell'inizio del set di risultati o dopo la fine del set di risultati. Questo errore potrebbe non essere restituito da un driver con un'implementazione nativa del cursore DBMS.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I009|Utilizzo non valido del puntatore null|(DM) -*InStatementText* era un puntatore null.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) una funzione in esecuzione in modo asincrono è stata chiamata per il *ConnectionHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) l'argomento *TextLength1* era minore di 0, ma non uguale a SQL_NTS.|  
|||(DM) l'argomento *BufferLength* era minore di 0 e l'argomento *OutStatementText* non era un puntatore null.|  
|I109|Posizione del cursore non valida|La riga corrente del cursore era stata eliminata o non era stata recuperata. Questo errore potrebbe non essere restituito da un driver con un'implementazione nativa del cursore DBMS.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) Il driver associato a *ConnectionHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Di seguito sono riportati esempi di ciò che **SQLNativeSql** potrebbe restituire per la stringa SQL di input seguente contenente la funzione scalare CONVERT. Si supponga che la colonna empid è di tipo INTEGER nell'origine dati:  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Un driver per Microsoft SQL Server potrebbe restituire la stringa SQL tradotta seguente:A driver for Microsoft SQL Server might return the following translated SQL string:  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 Un driver per ORACLE Server potrebbe restituire la seguente stringa SQL tradotta:  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Un driver per Ingres potrebbe restituire la stringa SQL tradotta seguente:A driver for Ingres might return the following translated SQL string:  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 Per ulteriori informazioni, consultate [Esecuzione diretta](../../../odbc/reference/develop-app/direct-execution-odbc.md) ed [esecuzione preparata](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
 No.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
