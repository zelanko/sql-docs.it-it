---
title: Funzione SQLGetConnectAttr . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6076f14ff0c33fec38b99e9c43b8a688970a7a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285631"
---
# <a name="sqlgetconnectattr-function"></a>Funzione SQLSetConnectAttr
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLGetConnectAttr** restituisce l'impostazione corrente di un attributo di connessione.  
  
> [!NOTE]
>  Per ulteriori informazioni su ciò che Gestione Driver esegue il mapping di questa funzione a quando un'applicazione ODBC 3 *.x* utilizza un driver *.x* ODBC 2, vedere Mapping di funzioni di sostituzione per la [compatibilità con](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)le versioni precedenti delle applicazioni .  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
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
  
 *Attributo*  
 [Ingresso] Attributo da recuperare.  
  
 *ValuePtr*  
 [Uscita] Puntatore alla memoria in cui restituire il valore corrente dell'attributo specificato da *Attribute*. Per gli attributi di tipo Integer, alcuni driver possono scrivere solo il 32 bit inferiore o 16 bit di un buffer e lasciare invariato il bit di ordine superiore. Pertanto, le applicazioni devono utilizzare un buffer di SQLULEN e inizializzare il valore su 0 prima di chiamare questa funzione.  
  
 Se *ValuePtr* è NULL, *StringLengthPtr* restituirà comunque il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *ValuePtr*.  
  
 *BufferLength*  
 [Ingresso] Se *Attribute* è un attributo definito da ODBC e *ValuePtr* punta a una \*stringa di caratteri o a un buffer binario, questo argomento deve essere la lunghezza di *ValuePtr*. Se *Attributo* è un \*attributo definito da ODBC e *ValuePtr* è un numero intero, *BufferLength* viene ignorato. Se il valore in * \*ValuePtr* è una stringa Unicode (quando si chiama **SQLGetConnectAttrW**), l'argomento *BufferLength* deve essere un numero pari.  
  
 Se *Attribute* è un attributo definito dal driver, l'applicazione indica la natura dell'attributo a Gestione Driver impostando il *BufferLength* argomento. *BufferLength* può avere i seguenti valori:  
  
-   Se * \*ValuePtr* è un puntatore a una stringa di caratteri, *BufferLength* è la lunghezza della stringa.  
  
-   Se * \*ValuePtr* è un puntatore a un buffer binario, l'applicazione inserisce il risultato della macro SQL_LEN_BINARY_ATTR(*length*) in *BufferLength*. In questo modo un valore negativo in *BufferLength*.  
  
-   Se * \*ValuePtr* è un puntatore a un valore diverso da una stringa di caratteri o una stringa binaria, *BufferLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se * \*ValuePtr* contiene un tipo di dati a lunghezza fissa, *BufferLength* è SQL_IS_INTEGER o SQL_IS_UINTEGER, a seconda dei casi.  
  
 *StringLengthPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di byte (escluso il carattere di terminazione null) disponibile per la restituzione in \* *ValuePtr*. Se \* *ValuePtr* è un puntatore null, non viene restituita alcuna lunghezza. Se il valore dell'attributo è una stringa di caratteri e il numero di byte disponibili per la restituzione è maggiore di *BufferLength* meno la lunghezza del carattere di terminazione null, i dati in * \*ValuePtr* vengono troncati a *BufferLength* meno la lunghezza del carattere di terminazione null e viene terminato con null dal driver.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetConnectAttr** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato dalla struttura dei dati di diagnostica chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_DBC e un *handle* di *ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLGetConnectAttr** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|I dati restituiti in \* *ValuePtr* sono stati troncati per essere *BufferLength* meno la lunghezza di un carattere di terminazione null. La lunghezza del valore di stringa non troncato viene restituita in *, StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08003|Connessione non aperta|(DM) è stato specificato un valore *di attributo* che richiedeva una connessione aperta.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito dalla struttura dei dati di diagnostica dall'argomento *MessageText* in **SQLGetDiagField** descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) **SQLBrowseConnect** è stato chiamato per il *ConnectionHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima che **SQLBrowseConnect** restituisse SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *ConnectionHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) * \*ValuePtr* è una stringa di caratteri e BufferLength era minore di zero ma non uguale a SQL_NTS.|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo/opzione non valido|Il valore specificato per l'argomento *attributo* non è valido per la versione di ODBC supportata dal driver.|  
|HY114|Il driver non supporta l'esecuzione di funzioni asincrone a livello di connessioneDriver does not support connection-level asynchronous function execution|(DM) Un'applicazione ha tentato di abilitare l'esecuzione asincrona di funzioni con SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE per un driver che non supporta le operazioni di connessione asincrone.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il valore specificato per l'argomento *attributo* è un attributo di connessione ODBC valido per la versione di ODBC supportata dal driver, ma non è supportato dal driver.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver che corrisponde a *ConnectionHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Per informazioni generali sugli attributi di connessione, vedere Attributi di [connessione](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Per un elenco degli attributi che è possibile impostare, vedere [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md). Si noti che se *Attribute* specifica un attributo che restituisce una stringa, *ValuePtr* deve essere un puntatore a un buffer per la stringa. La lunghezza massima della stringa restituita, incluso il carattere di terminazione null, sarà *BufferLength* byte.  
  
 A seconda dell'attributo, un'applicazione non deve stabilire una connessione prima di chiamare **SQLGetConnectAttr**. Tuttavia, se **SQLGetConnectAttr** viene chiamato e l'attributo specificato non dispone di un valore predefinito e non è stato impostato da una precedente chiamata a **SQLSetConnectAttr**, **SQLGetConnectAttr** restituirà SQL_NO_DATA.  
  
 Se *Attribute* è SQL_ATTR_ TRACE o SQL_ATTR_ TRACEFILE, *ConnectionHandle* non deve essere valido e **SQLGetConnectAttr** non restituirà SQL_ERROR o SQL_INVALID_HANDLE se *ConnectionHandle* non è valido. Questi attributi si applicano a tutte le connessioni. **SQLGetConnectAttr** restituirà SQL_ERROR o SQL_INVALID_HANDLE se un altro argomento non è valido.  
  
 Sebbene un'applicazione possa impostare attributi di istruzione utilizzando **SQLSetConnectAttr**, un'applicazione non può utilizzare **SQLGetConnectAttr** per recuperare i valori degli attributi dell'istruzione. deve chiamare **SQLGetStmtAttr** per recuperare l'impostazione degli attributi dell'istruzione.  
  
 Gli attributi di connessione SQL_ATTR_AUTO_IPD e SQL_ATTR_CONNECTION_DEAD possono essere restituiti da una chiamata a **SQLGetConnectAttr,** ma non possono essere impostati da una chiamata a **SQLSetConnectAttr**.  
  
> [!NOTE]  
>  Non è disponibile alcun supporto asincrono per **SQLGetConnectAttr**. Quando si implementa **SQLGetConnectAttr**, un driver può migliorare le prestazioni riducendo al minimo il numero di volte in cui le informazioni vengono inviate o richieste dal server.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituzione dell'impostazione di un attributo di istruzioneReturning the setting of a statement attribute|[Funzione SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Impostazione di un attributo di connessione|[Pagina relativa alla funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Impostazione di un attributo di ambiente|[Funzione SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Impostazione di un attributo di istruzioneSetting a statement attribute|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
