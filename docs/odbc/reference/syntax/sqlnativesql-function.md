---
title: Funzione SQLNativeSql | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f58d262f133fc242592e62e0bb5a4152877adf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536524"
---
# <a name="sqlnativesql-function"></a>Funzione SQLNativeSql
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ODBC  
  
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
  
 *InStatementText*  
 [Input] Stringa di testo SQL da tradurre.  
  
 *TextLength1*  
 [Input] Lunghezza in caratteri della **InStatementText* stringa di testo.  
  
 *OutStatementText*  
 [Output] Puntatore a un buffer in cui restituire la stringa SQL tradotta.  
  
 Se *OutStatementText* sia impostato su NULL *TextLength2Ptr* continuerà a restituire il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui punta *OutStatementText*.  
  
 *BufferLength*  
 [Input] Numero di caratteri nel \* *OutStatementText* buffer. Se il valore restituito  *\*InStatementText* è una stringa Unicode (quando si chiama **SQLNativeSqlW**), il *BufferLength* argomento deve essere un numero pari.  
  
 *TextLength2Ptr*  
 [Output] Puntatore a un buffer in cui restituire il numero totale di caratteri (ad eccezione di terminazione null) disponibili per restituire \* *OutStatementText*. Se il numero di caratteri disponibili da restituire è maggiore o uguale a *BufferLength*, il tradotto stringa SQL nella \* *OutStatementText* viene troncato a  *BufferLength* meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLNativeSql** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato può essere ottenuto chiamando **SQLGetDiagRec** con un *HandleType* SQL_HANDLE_DBC e un *gestiscono* dei *ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLNativeSql** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Il buffer \* *OutStatementText* non era sufficientemente grande per restituire l'intera stringa SQL, in modo che la stringa SQL è stata troncata. Viene restituita la lunghezza della stringa SQL non troncata **TextLength2Ptr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08003|Connessione non aperta|Il *ConnectionHandle* non era in uno stato connesso.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|22007|Formato di datetime non valido|**InStatementText* contenuta una clausola di escape con un valore di data, ora o timestamp non valido.|  
|24000|Stato del cursore non valido|È stato posizionato il cursore definito nell'istruzione prima dell'inizio del set di risultati o dopo la fine del set di risultati. Questo errore non può essere restituito per un driver con un'implementazione nativa di cursore DBMS.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY009|Utilizzo non valido del puntatore null|(DM) **InStatementText* era un puntatore null.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione la *ConnectionHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) dell'argomento *TextLength1* era minore di 0, ma non è uguale a SQL_NTS.|  
|||(DM) dell'argomento *BufferLength* era minore di 0 e l'argomento *OutStatementText* non era un puntatore null.|  
|HY109|Posizione del cursore non valido|La riga corrente del cursore è stata eliminata o non era stata recuperata. Questo errore non può essere restituito per un driver con un'implementazione nativa di cursore DBMS.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *ConnectionHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Di seguito sono riportati esempi di cosa **SQLNativeSql** potrebbe restituire la stringa di input seguente SQL che contiene la funzione scalare CONVERT. Si supponga che la colonna Employee!1!empID sia di tipo INTEGER nell'origine dati:  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Un driver per Microsoft SQL Server potrebbe restituire la stringa SQL tradotta seguente:  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 Un driver per ORACLE Server potrebbe restituire la stringa SQL tradotta seguente:  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Un driver per Ingres potrebbe restituire la stringa SQL tradotta seguente:  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 Per altre informazioni, vedere [esecuzione diretta](../../../odbc/reference/develop-app/direct-execution-odbc.md) e [esecuzione preparata](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
 Nessuna.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
