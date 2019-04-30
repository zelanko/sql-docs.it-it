---
title: Funzione SQLGetConnectAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectAttr
helpviewer_keywords:
- SQLGetConnectAttr function [ODBC]
ms.assetid: 2cb4ffa8-19d3-4664-8c2f-6682cdcc3f33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a24ccf58a1cd0f6d0f4fb2fd32dbee79feb896b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259637"
---
# <a name="sqlgetconnectattr-function"></a>Funzione SQLSetConnectAttr
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLGetConnectAttr** restituisce l'impostazione corrente di un attributo di connessione.  
  
> [!NOTE]
>  Per altre informazioni su cosa the Driver Manager esegue il mapping a questa funzione quando un'applicazione ODBC 3 *. x* applicazione funziona con un'API ODBC 2 *. x* driver, vedere [Mapping di funzioni di sostituzione per Aut Compatibilità delle applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLGetConnectAttr(  
     SQLHDBC        ConnectionHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *ConnectionHandle*  
 [Input] Handle di connessione.  
  
 *Attribute*  
 [Input] Attributo da recuperare.  
  
 *ValuePtr*  
 [Output] Puntatore alla memoria in cui restituire il valore corrente dell'attributo specificato da *attributo*. Per gli attributi di tipo integer, alcuni driver può scrivere solo inferiore a 32 o a 16 bit di un buffer e lasciare invariato il bit di ordine superiore. Di conseguenza, le applicazioni devono usare un buffer di SQLULEN ed inizializzare il valore su 0 prima di chiamare questa funzione.  
  
 Se *ValuePtr* sia impostato su NULL *StringLengthPtr* continuerà a restituire il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui punta  *ValuePtr*.  
  
 *BufferLength*  
 [Input] Se *attributo* è un attributo definito da ODBC e *ValuePtr* punta a una stringa di caratteri o un buffer binario, la lunghezza di questo argomento deve essere \* *ValuePtr*. Se *attributo* è un attributo definito da ODBC e \* *ValuePtr* è un intero *BufferLength* viene ignorato. Se il valore in  *\*ValuePtr* è una stringa Unicode (quando si chiama **SQLGetConnectAttrW**), il *BufferLength* argomento deve essere un numero pari.  
  
 Se *attributo* è un attributo definito dal driver, l'applicazione indica la natura dell'attributo da Gestione Driver impostando il *BufferLength* argomento. *BufferLength* può avere i valori seguenti:  
  
-   Se  *\*ValuePtr* è un puntatore a una stringa di caratteri *BufferLength* è la lunghezza della stringa.  
  
-   Se  *\*ValuePtr* è un puntatore a un buffer binario, le posizioni dell'applicazione il risultato del SQL_LEN_BINARY_ATTR (*lunghezza*) macro in *BufferLength*. Un valore negativo in questo modo vengono inserite *BufferLength*.  
  
-   Se  *\*ValuePtr* è un puntatore a un valore diverso da una stringa di caratteri o stringa binaria *BufferLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se  *\*ValuePtr* contiene un tipo di dati a lunghezza fissa *BufferLength* è SQL_IS_INTEGER o SQL_IS_UINTEGER, come appropriato.  
  
 *StringLengthPtr*  
 [Output] Un puntatore a un buffer in cui restituire il numero totale di byte (escluso il carattere di terminazione null) disponibili per restituire \* *ValuePtr*. Se \* *ValuePtr* è un puntatore null, non viene restituita alcuna lunghezza. Se il valore dell'attributo è una stringa di caratteri e il numero di byte disponibili da restituire è maggiore *BufferLength* meno la lunghezza del carattere di terminazione null, i dati in  *\*ValuePtr*verrà troncato *BufferLength* meno la lunghezza del carattere di terminazione null ed è con terminazione null dal driver.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetConnectAttr** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti dalla struttura di dati di diagnostica chiamando **SQLGetDiagRec** con un *HandleType* SQL_HANDLE_DBC e una *gestiscono* dei *ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLGetConnectAttr** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver . Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|I dati restituiti nella \* *ValuePtr* sono stati troncati per essere *BufferLength* meno la lunghezza di un carattere di terminazione null. Viene restituita la lunghezza del valore della stringa non troncato **StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08003|Connessione non aperta|(DM) un' *attributo* valore che è necessaria una connessione aperta è stata specificata.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito dalla struttura di dati di diagnostica tramite l'argomento *MessageText* nelle **SQLGetDiagField** descrive l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver non è riuscito ad allocare memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) **SQLBrowseConnect** è stato chiamato per il *ConnectionHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima **SQLBrowseConnect** restituito SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *ConnectionHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM)  *\*ValuePtr* è una stringa di caratteri e BufferLength era minore di zero ma non è uguale a SQL_NTS.|  
|HY092|Identificatore di attributo/opzione non è valido|Il valore specificato per l'argomento *attributo* non è valido per la versione di ODBC supportati dal driver.|  
|HY114|Driver non supporta l'esecuzione della funzione asincrona a livello di connessione|(DM) un'applicazione ha tentato di attivare l'esecuzione di funzione asincrona con SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE per un driver che non supporta le operazioni di connessione asincrona.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|Il valore specificato per l'argomento *attributo* era un attributo di connessione ODBC valido per la versione di ODBC supportati dal driver, ma non era supportata dal driver.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|(DM) il driver corrispondente per il *ConnectionHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Per informazioni generali sugli attributi di connessione, vedere [attributi di connessione](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Per un elenco di attributi che è possibile impostare, vedere [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md). Si noti che, se *attributo* specifica un attributo che restituisce una stringa *ValuePtr* deve essere un puntatore a un buffer per la stringa. La lunghezza massima della stringa restituita, incluso il carattere di terminazione null, saranno *BufferLength* byte.  
  
 A seconda dell'attributo, un'applicazione non è necessario stabilire una connessione prima di chiamare **SQLGetConnectAttr**. Tuttavia, se **SQLGetConnectAttr** viene chiamato e l'attributo specificato non è un valore predefinito e non è stato impostato da una chiamata precedente a **SQLSetConnectAttr**, **SQLGetConnectAttr**verrà restituito SQL_NO_DATA.  
  
 Se *attributo* rappresenti sql_attr TRACEFILE, traccia sql_attr *ConnectionHandle* non deve essere valido, e **SQLGetConnectAttr** non restituirà SQL_ERROR o SQL _ INVALID_HANDLE se *ConnectionHandle* non è valido. Questi attributi si applicano a tutte le connessioni. **SQLGetConnectAttr** restituirà SQL_ERROR o SQL_INVALID_HANDLE se un altro argomento non è valido.  
  
 Anche se un'applicazione può impostare gli attributi di istruzione usando **SQLSetConnectAttr**, un'applicazione non è possibile usare **SQLGetConnectAttr** per recuperare l'attributo di istruzione valori; deve chiamare  **SQLGetStmtAttr** per recuperare l'impostazione degli attributi di istruzione.  
  
 Attributi di connessione SQL_ATTR_AUTO_IPD sia SQL_ATTR_CONNECTION_DEAD possono essere restituiti da una chiamata a **SQLGetConnectAttr** ma non può essere impostata da una chiamata a **SQLSetConnectAttr**.  
  
> [!NOTE]  
>  Non è disponibile alcun supporto asincrono per **SQLGetConnectAttr**. Quando si implementa **SQLGetConnectAttr**, un driver può migliorare le prestazioni riducendo al minimo il numero di volte in cui vengono inviati o richiesti dal server.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituisce l'impostazione di un attributo di istruzione|[Funzione SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Impostare un attributo di connessione|[Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|L'impostazione di un attributo di ambiente|[Funzione SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|L'impostazione di un attributo di istruzione|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
