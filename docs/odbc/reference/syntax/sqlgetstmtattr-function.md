---
title: SqlGetStmtAttr (funzione) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89e7c75b412a6358806017102915989a8370dd43
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303305"
---
# <a name="sqlgetstmtattr-function"></a>Funzione SQLGetStmtAttr
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLGetStmtAttr** restituisce l'impostazione corrente di un attributo di istruzione.  
  
> [!NOTE]  
>  Per ulteriori informazioni su ciò che Gestione Driver esegue il mapping di questa funzione a quando un ODBC 3. *l'applicazione x* funziona con un'applicazione ODBC 2. *x,* vedere Mapping delle funzioni di sostituzione per la [compatibilità con le applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)con le versioni precedenti.  
  
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
 [Ingresso] Handle di istruzione.  
  
 *Attributo*  
 [Ingresso] Attributo da recuperare.  
  
 *ValuePtr*  
 [Uscita] Puntatore a un buffer in cui restituire il valore dell'attributo specificato in *Attributo*.  
  
 Se *ValuePtr* è NULL, *StringLengthPtr* restituirà comunque il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *ValuePtr*.  
  
 *BufferLength*  
 [Ingresso] Se *Attribute* è un attributo definito da ODBC e *ValuePtr* punta a una \*stringa di caratteri o a un buffer binario, questo argomento deve essere la lunghezza di *ValuePtr*. Se *Attributo* è un \*attributo definito da ODBC e *ValuePtr* è un numero intero, *BufferLength* viene ignorato. Se il valore restituito in * \*ValuePtr* è una stringa Unicode (quando si chiama **SQLGetStmtAttrW**), l'argomento *BufferLength* deve essere un numero pari.  
  
 Se *Attribute* è un attributo definito dal driver, l'applicazione indica la natura dell'attributo a Gestione Driver impostando il *BufferLength* argomento. *BufferLength* può avere i seguenti valori:  
  
-   Se * \*ValuePtr* è un puntatore a una stringa di caratteri, *quindi BufferLength* è la lunghezza della stringa o SQL_NTS.  
  
-   Se * \*ValuePtr* è un puntatore a un buffer binario, l'applicazione inserisce il risultato della macro SQL_LEN_BINARY_ATTR(*length*) in *BufferLength*. In questo modo un valore negativo in *BufferLength*.  
  
-   Se * \*ValuePtr* è un puntatore a un valore diverso da una stringa di caratteri o una stringa binaria, *quindi BufferLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se * \*ValuePtr* contiene un tipo di dati a lunghezza fissa, *BufferLength* è SQL_IS_INTEGER o SQL_IS_UINTEGER, a seconda dei casi.  
  
 *StringLengthPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di byte (escluso il carattere di terminazione null) disponibile per la restituzione in * \*ValuePtr*. Se *ValuePtr* è un puntatore null, non viene restituita alcuna lunghezza. Se il valore dell'attributo è una stringa di caratteri e il numero di byte disponibili da restituire è maggiore o uguale a *BufferLength*, i dati in * \*ValuePtr* vengono troncati a *BufferLength* meno la lunghezza di un carattere di terminazione null e sono terminati con null dal driver.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetStmtAttr** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *Handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetStmtAttr** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|I dati restituiti in * \*ValuePtr* sono stati troncati per essere *BufferLength* meno la lunghezza di un carattere di terminazione null. La lunghezza del valore di stringa non troncato viene restituita in *, StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|24000|Stato del cursore non valido|L'argomento *Attributo* è stato SQL_ATTR_ROW_NUMBER e il cursore non era aperto oppure il cursore è stato posizionato prima dell'inizio del set di risultati o dopo la fine del set di risultati.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nell'argomento *MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLGetStmtAttr.**<br /><br /> (DM) una funzione in esecuzione in modo asincrono è stata chiamata per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|*(DM) \*ValuePtr* è una stringa di caratteri e BufferLength era minore di zero, ma non uguale a SQL_NTS.|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo/opzione non valido|Il valore specificato per l'argomento *attributo* non è valido per la versione di ODBC supportata dal driver.|  
|I109|Posizione del cursore non valida|L'argomento *Attribute* è stato SQL_ATTR_ROW_NUMBER e la riga è stata eliminata o non è stato possibile recuperarla.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il valore specificato per l'argomento *attributo* è un attributo di istruzione ODBC valido per la versione di ODBC supportata dal driver, ma non è supportato dal driver.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver corrispondente a *StatementHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Per informazioni generali sugli attributi dell'istruzione, vedere [Attributi dell'istruzione](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Una chiamata a **SQLGetStmtAttr** restituisce in * \*ValuePtr* il valore dell'attributo dell'istruzione specificato *nell'attributo .* Tale valore può essere un valore SQLULEN o una stringa di caratteri con terminazione null. Se il valore è un valore SQLULEN, alcuni driver possono scrivere solo il 32 bit inferiore o 16 bit di un buffer e lasciare invariato il bit di ordine superiore. Pertanto, le applicazioni devono utilizzare un buffer di SQLULEN e inizializzare il valore su 0 prima di chiamare questa funzione. Inoltre, gli argomenti *BufferLength* e *StringLengthPtr* non vengono utilizzati. Se il valore è una stringa con terminazione null, l'applicazione specifica la lunghezza massima di tale stringa nel *BufferLength* argomento e il driver restituisce la lunghezza di tale stringa nel * \*Buffer StringLengthPtr.*  
  
 Per consentire alle applicazioni che chiamano **SQLGetStmtAttr di** utilizzare con ODBC 2. *x* drivers, una chiamata a **SQLGetStmtAttr** viene mappata in Gestione Driver a **SQLGetStmtOption**.  
  
 Gli attributi dell'istruzione seguenti sono di sola lettura, pertanto possono essere recuperati da **SQLGetStmtAttr**, ma non impostati da **SQLSetStmtAttr**:  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 Per un elenco degli attributi che è possibile impostare e recuperare, vedere [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituzione dell'impostazione di un attributo di connessioneReturning the setting of a connection attribute|[Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Impostazione di un attributo di connessione|[Pagina relativa alla funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Impostazione di un attributo di istruzioneSetting a statement attribute|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
