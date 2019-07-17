---
title: Funzione SQLGetStmtAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetStmtAttr
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC]
ms.assetid: e321d460-e997-4527-aee6-207cf5a498e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31ddab7291807222882050233715d3ad61e25124
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061457"
---
# <a name="sqlgetstmtattr-function"></a>Funzione SQLGetStmtAttr
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLGetStmtAttr** restituisce l'impostazione corrente di un attributo di istruzione.  
  
> [!NOTE]  
>  Per altre informazioni su quali il Driver Manager esegue il mapping a questa funzione quando un'applicazione ODBC 3. *x* applicazione funziona con un'API ODBC 2. *x* driver, vedere [Mapping di funzioni di sostituzione per la compatibilità con le versioni precedenti di applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLGetStmtAttr(  
     SQLHSTMT        StatementHandle,  
     SQLINTEGER      Attribute,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *Attribute*  
 [Input] Attributo da recuperare.  
  
 *ValuePtr*  
 [Output] Puntatore a un buffer in cui restituire il valore dell'attributo specificato nel *attributo*.  
  
 Se *ValuePtr* sia impostato su NULL *StringLengthPtr* continuerà a restituire il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui punta  *ValuePtr*.  
  
 *BufferLength*  
 [Input] Se *attributo* è un attributo definito da ODBC e *ValuePtr* punta a una stringa di caratteri o un buffer binario, la lunghezza di questo argomento deve essere \* *ValuePtr*. Se *attributo* è un attributo definito da ODBC e \* *ValuePtr* è un intero *BufferLength* viene ignorato. Se il valore restituito  *\*ValuePtr* è una stringa Unicode (quando si chiama **SQLGetStmtAttrW**), il *BufferLength* argomento deve essere un numero pari.  
  
 Se *attributo* è un attributo definito dal driver, l'applicazione indica la natura dell'attributo da Gestione Driver impostando il *BufferLength* argomento. *BufferLength* può avere i valori seguenti:  
  
-   Se  *\*ValuePtr* è un puntatore a una stringa di caratteri, quindi *BufferLength* è la lunghezza della stringa o SQL_NTS.  
  
-   Se  *\*ValuePtr* è un puntatore a un buffer binario, quindi l'applicazione inserisce il risultato del SQL_LEN_BINARY_ATTR (*lunghezza*) macro in *BufferLength*. Un valore negativo in questo modo vengono inserite *BufferLength*.  
  
-   Se  *\*ValuePtr* è un puntatore a un valore diverso da una stringa di caratteri o stringa binaria, quindi *BufferLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se  *\*ValuePtr* è contiene un tipo di dati a lunghezza fissa, quindi *BufferLength* è SQL_IS_INTEGER o SQL_IS_UINTEGER, come appropriato.  
  
 *StringLengthPtr*  
 [Output] Un puntatore a un buffer in cui restituire il numero totale di byte (escluso il carattere di terminazione null) disponibili per restituire  *\*ValuePtr*. Se *ValuePtr* è un puntatore null, non viene restituita alcuna lunghezza. Se il valore dell'attributo è una stringa di caratteri e il numero di byte disponibili da restituire è maggiore o uguale a *BufferLength*, i dati in  *\*ValuePtr* viene troncato a *BufferLength* meno la lunghezza di un carattere di terminazione null ed è con terminazione null dal driver.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetStmtAttr** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetStmtAttr** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|I dati restituiti nella  *\*ValuePtr* sono stati troncati per essere *BufferLength* meno la lunghezza di un carattere di terminazione null. Viene restituita la lunghezza del valore della stringa non troncato **StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|24000|Stato del cursore non valido|L'argomento *attributo* era SQL_ATTR_ROW_NUMBER e il cursore non è stato aperto o è stato posizionato il cursore prima dell'inizio del set di risultati o dopo la fine del set di risultati.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nell'argomento *MessageText* descrive l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLGetStmtAttr** funzione è stata chiamata.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione la *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|*(DM) \*ValuePtr* è una stringa di caratteri e BufferLength era minore di zero, ma non è uguale a SQL_NTS.|  
|HY092|Identificatore di attributo/opzione non è valido|Il valore specificato per l'argomento *attributo* non è valido per la versione di ODBC supportati dal driver.|  
|HY109|Posizione del cursore non valido|Il *attributo* argomento era SQL_ATTR_ROW_NUMBER e la riga è stata eliminata o non è stato possibile recuperare.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|Il valore specificato per l'argomento *attributo* era un attributo di istruzione ODBC valido per la versione di ODBC supportati dal driver, ma non era supportata dal driver.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|(DM) il driver corrispondente per il *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Per informazioni generali sugli attributi di istruzione, vedere [attributi di istruzione](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Una chiamata a **SQLGetStmtAttr** restituisce  *\*ValuePtr* il valore di attributo specificata nell'istruzione *attributo*. Tale valore può essere un valore SQLULEN o una stringa di caratteri con terminazione null. Se il valore è un valore SQLULEN, alcuni driver può scrivere solo inferiore a 32 o a 16 bit di un buffer e lasciare invariato il bit di ordine superiore. Di conseguenza, le applicazioni devono usare un buffer di SQLULEN ed inizializzare il valore su 0 prima di chiamare questa funzione. Inoltre, il *BufferLength* e *StringLengthPtr* argomenti non vengono usati. Se il valore è una stringa con terminazione null, l'applicazione specifica la lunghezza massima di tale stringa nel *BufferLength* argomento e il driver restituisce la lunghezza della stringa nel  *\* StringLengthPtr* buffer.  
  
 Per consentire le applicazioni che chiamano **SQLGetStmtAttr** per lavorare con l'API ODBC 2. *x* driver, una chiamata a **SQLGetStmtAttr** viene eseguito il mapping a in Gestione Driver **SQLGetStmtOption**.  
  
 I seguenti attributi di istruzione sono di sola lettura, in modo che può essere recuperato tramite **SQLGetStmtAttr**, ma non impostata **SQLSetStmtAttr**:  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 Per un elenco di attributi che può essere impostata e recuperata, vedere [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituisce l'impostazione di un attributo di connessione|[Funzione SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Impostare un attributo di connessione|[Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|L'impostazione di un attributo di istruzione|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
