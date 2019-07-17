---
title: Funzione SQLGetDescField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdf2990056c297d217248543812e347b61d3486d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103808"
---
# <a name="sqlgetdescfield-function"></a>Funzione SQLGetDescField
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLGetDescField** restituisce un valore di un singolo campo di un record del descrittore o l'impostazione corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *DescriptorHandle*  
 [Input] Handle descrittore.  
  
 *RecNumber*  
 [Input] Indica se il record del descrittore da cui l'applicazione cerca le informazioni. Record del descrittore sono numerati da 0, con il numero di record 0 come il record di segnalibro. Se il *FieldIdentifier* l'argomento indica un campo di intestazione *RecNumber* viene ignorato. Se *RecNumber* è minore o uguale a SQL_DESC_COUNT ma la riga non contiene dati per una colonna o parametro, una chiamata a **SQLGetDescField** restituirà i valori predefiniti dei campi. (Per altre informazioni, vedere "Inizializzazione di campi di descrizione" nella [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *FieldIdentifier*  
 [Input] Indica il campo del descrittore il cui valore deve essere restituita. Per altre informazioni, vedere la "*FieldIdentifier* argomento" sezione [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 *ValuePtr*  
 [Output] Puntatore a un buffer in cui si desidera restituire le informazioni del descrittore. Il tipo di dati dipende dal valore della *FieldIdentifier*.  
  
 Se *ValuePtr* è di tipo integer, le applicazioni devono utilizzare un buffer di SQLULEN e inizializzare il valore su 0 prima di chiamare questa funzione come alcuni driver può solo scrivere l'inferiore a 32 bit o 16 bit di un buffer e lasciare il bit di ordine superiore non viene modificato.  
  
 Se *ValuePtr* sia impostato su NULL *StringLengthPtr* continuerà a restituire il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui punta  *ValuePtr*.  
  
 *BufferLength*  
 [Input] Se *FieldIdentifier* è un campo definite da ODBC e *ValuePtr* punta a una stringa di caratteri o un buffer binario, la lunghezza di questo argomento deve essere \* *ValuePtr*. Se *FieldIdentifier* è un campo definite da ODBC e \* *ValuePtr* è un intero *BufferLength* viene ignorato. Se il valore in  *\*ValuePtr* è un tipo di dati Unicode (quando si chiama **SQLGetDescFieldW**), il *BufferLength* argomento deve essere un numero pari.  
  
 Se *FieldIdentifier* è un campo definito dal driver, l'applicazione indica la natura del campo da Gestione Driver impostando il *BufferLength* argomento. *BufferLength* può avere i valori seguenti:  
  
-   Se  *\*ValuePtr* è un puntatore a una stringa di caratteri, quindi *BufferLength* è la lunghezza della stringa o SQL_NTS.  
  
-   Se  *\*ValuePtr* è un puntatore a un buffer binario, quindi l'applicazione inserisce il risultato del SQL_LEN_BINARY_ATTR (*lunghezza*) macro in *BufferLength*. Un valore negativo in questo modo vengono inserite *BufferLength*.  
  
-   Se  *\*ValuePtr* è un puntatore a un valore diverso da una stringa di caratteri o stringa binaria, quindi *BufferLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se  *\*ValuePtr* è contiene un tipo di dati a lunghezza fissa, quindi *BufferLength* è SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_IS_USMALLINT, come appropriato.  
  
 *StringLengthPtr*  
 [Output] Puntatore al buffer in cui restituire il numero totale di byte (escluso il numero di byte necessari per il carattere di terminazione null) disponibile da restituire in **ValuePtr*.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
 Se non viene restituito SQL_NO_DATA *RecNumber* è maggiore del numero corrente di record del descrittore.  
  
 Se non viene restituito SQL_NO_DATA *DescriptorHandle* è un handle IRD e l'istruzione si trova nello stato preparato o eseguito, ma si è verificato alcun cursore aperto è associato.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetDescField** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetDescField** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Il buffer \* *ValuePtr* non era sufficientemente grande per restituire il campo di descrizione intero, in modo che il campo è stato troncato. Viene restituita la lunghezza del campo del descrittore non troncato **StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07009|Indice del descrittore non valido|(DM) di *RecNumber* l'argomento è uguale a 0, l'attributo di istruzione SQL_ATTR_USE_BOOKMARK era SQL_UB_OFF e il *DescriptorHandle* argomento era un handle IRD. (Questo errore può essere restituito per un descrittore allocato in modo esplicito solo se il descrittore è associato a un handle di istruzione.)<br /><br /> Il *FieldIdentifier* l'argomento è un campo di record, il *RecNumber* argomento era 0 e il *DescriptorHandle* argomento era un handle IPD.<br /><br /> Il *RecNumber* argomento era minore di 0.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver non è riuscito ad allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY007|L'istruzione associata non è pronto|*DescriptorHandle* è stato associato un *StatementHandle* come un IRD e l'istruzione associata handle aveva non è stato preparato o eseguito.|  
|HY010|Errore nella sequenza della funzione|(DM) *DescriptorHandle* è stato associato un *StatementHandle* per i quali è stata chiamata una funzione di esecuzione asincrona (non presente uno) ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) *DescriptorHandle* è stato associato un *StatementHandle* per il quale **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.<br /><br /> (DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *DescriptorHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLGetDescField** funzione è stata chiamata.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY021|Informazioni descrittore incoerenti.|I campi SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE non formano un tipo SQL ODBC valido, un tipo SQL specifiche del driver valido (per gli IDP) o un tipo di dati ODBC C valido (ad o ARDs Apd).|  
|HY090|Lunghezza della stringa o buffer non valido|(DM)  *\*ValuePtr* è una stringa di caratteri, e *BufferLength* era minore di zero.|  
|HY091|Identificatore del campo del descrittore non valido|*FieldIdentifier* non era un campo definite da ODBC e non è un valore definito dall'implementazione.<br /><br /> *FieldIdentifier* non è stato definito per il *DescriptorHandle*.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *DescriptorHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Un'applicazione può chiamare **SQLGetDescField** per restituire il valore di un singolo campo di un record del descrittore. Una chiamata a **SQLGetDescField** può restituire l'impostazione di un campo in qualsiasi tipo di descrittore, inclusi i campi di intestazione, i campi di record e campi di segnalibro. Un'applicazione può ottenere le impostazioni di più campi nei descrittori di uguali o diversi, in ordine arbitrario, eseguendo chiamate ripetute a **SQLGetDescField**. **SQLGetDescField** può anche essere chiamata per restituire i campi di descrizione definito dal driver.  
  
 Per motivi di prestazioni, un'applicazione non deve chiamare **SQLGetDescField** per un'implementazione prima di eseguire un'istruzione.  
  
 Le impostazioni di più campi che descrivono il nome, tipo di dati e archiviazione dei dati di colonna o del parametro possono essere recuperate anche in una singola chiamata a **SQLGetDescRec**. **SQLGetStmtAttr** può essere chiamata per restituire l'impostazione di un singolo campo nell'intestazione del descrittore che è anche un attributo di istruzione. **SQLColAttribute**, **SQLDescribeCol**, e **SQLDescribeParam** restituire i campi di record o un segnalibro.  
  
 Quando un'applicazione chiama **SQLGetDescField** per recuperare il valore di un campo che non è definito per un tipo di descrittore particolare, la funzione restituisce SQL_SUCCESS, ma il valore restituito per il campo è definito. Ad esempio, chiamando **SQLGetDescField** per il campo SQL_DESC_NAME o SQL_DESC_NULLABLE di un APD o ARD restituisce SQL_SUCCESS, ma un valore indefinito per il campo.  
  
 Quando un'applicazione chiama **SQLGetDescField** per recuperare il valore di un campo definito per un tipo di descrittore particolare ma che non dispone di alcun valore predefinito e non è stato ancora impostato, la funzione restituisce SQL_SUCCESS, ma il valore restituito per il campo è definito. Per altre informazioni sull'inizializzazione di campi di descrizione e le descrizioni dei campi, vedere "Inizializzazione di campi di descrizione" nella [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Per altre informazioni su descrittori, vedere [descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Recupero di più campi di descrizione|[Funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Impostazione di un campo del descrittore single|[Funzione SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|L'impostazione di più campi di descrizione|[Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
