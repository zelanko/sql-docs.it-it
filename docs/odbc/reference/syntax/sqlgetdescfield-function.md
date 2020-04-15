---
title: Funzione SQLGetDescField . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89972d7f36b436868cc8e243b03827f095b90492
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285476"
---
# <a name="sqlgetdescfield-function"></a>Funzione SQLGetDescField
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLGetDescField** restituisce l'impostazione corrente o il valore di un singolo campo di un record del descrittore.  
  
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
 [Ingresso] Handle del descrittore.  
  
 *RecNumber*  
 [Ingresso] Indica il record del descrittore da cui l'applicazione cerca informazioni. I record del descrittore sono numerati da 0, con il numero di record 0 come record del segnalibro. Se l'argomento *FieldIdentifier* indica un campo di intestazione, *RecNumber* viene ignorato. Se *RecNumber* è minore o uguale a SQL_DESC_COUNT ma la riga non contiene dati per una colonna o un parametro, una chiamata a **SQLGetDescField** restituirà i valori predefiniti dei campi. (Per ulteriori informazioni, vedere "Inizializzazione dei campi descrittore" in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 *FieldIdentifier*  
 [Ingresso] Indica il campo del descrittore il cui valore deve essere restituito. Per ulteriori informazioni, vedere la sezione "Argomento*FieldIdentifier"* in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 *ValuePtr*  
 [Uscita] Puntatore a un buffer in cui restituire le informazioni sul descrittore. Il tipo di dati dipende dal valore di *FieldIdentifier*.  
  
 Se *ValuePtr* è di tipo integer, le applicazioni devono utilizzare un buffer di SQLULEN e inizializzare il valore su 0 prima di chiamare questa funzione come alcuni driver possono scrivere solo il 32 bit inferiore o 16 bit di un buffer e lasciare invariato il bit di ordine superiore.  
  
 Se *ValuePtr* è NULL, *StringLengthPtr* restituirà comunque il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *ValuePtr*.  
  
 *BufferLength*  
 [Ingresso] Se *FieldIdentifier* è un campo definito da ODBC e *ValuePtr* punta a una stringa \*di caratteri o a un buffer binario, questo argomento deve essere la lunghezza di *ValuePtr*. Se *FieldIdentifier* è un campo \*definito da ODBC e *ValuePtr* è un numero intero, *BufferLength* viene ignorato. Se il valore in * \*ValuePtr* è di un tipo di dati Unicode (quando si chiama **SQLGetDescFieldW**), l'argomento *BufferLength* deve essere un numero pari.  
  
 Se *FieldIdentifier* è un campo definito dal driver, l'applicazione indica la natura del campo in Gestione Driver impostando il *BufferLength* argomento. *BufferLength* può avere i seguenti valori:  
  
-   Se * \*ValuePtr* è un puntatore a una stringa di caratteri, *quindi BufferLength* è la lunghezza della stringa o SQL_NTS.  
  
-   Se * \*ValuePtr* è un puntatore a un buffer binario, l'applicazione inserisce il risultato della macro SQL_LEN_BINARY_ATTR(*length*) in *BufferLength*. In questo modo un valore negativo in *BufferLength*.  
  
-   Se * \*ValuePtr* è un puntatore a un valore diverso da una stringa di caratteri o una stringa binaria, *quindi BufferLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se * \*ValuePtr* contiene un tipo di dati a lunghezza fissa, *BufferLength* è SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_IS_USMALLINT, a seconda dei casi.  
  
 *StringLengthPtr*  
 [Uscita] Puntatore al buffer in cui restituire il numero totale di byte (escluso il numero di byte necessari per il carattere di terminazione null) disponibile per la restituzione in *, ValuePtr*.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA viene restituito se *RecNumber* è maggiore del numero corrente di record del descrittore.  
  
 SQL_NO_DATA viene restituito se *DescriptorHandle* è un handle IRD e l'istruzione è nello stato preparato o eseguito, ma non vi è alcun cursore aperto associato.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetDescField** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *Handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetDescField** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Il \*buffer *ValuePtr* non era sufficientemente grande per restituire l'intero campo del descrittore, pertanto il campo è stato troncato. La lunghezza del campo del descrittore non troncato viene restituita in :*StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07009|Indice descrittore non valido|(DM) l'argomento *RecNumber* è uguale a 0, l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARK è stato SQL_UB_OFF e l'argomento *DescriptorHandle* è un handle IRD. Questo errore può essere restituito per un descrittore allocato in modo esplicito solo se il descrittore è associato a un handle di istruzione.<br /><br /> L'argomento *FieldIdentifier* è un campo di record, l'argomento *RecNumber* è 0 e l'argomento *DescriptorHandle* è un handle IPD.<br /><br /> L'argomento *RecNumber* era minore di 0.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I007|L'istruzione associata non è preparata|*DescriptorHandle* è stato associato a un *StatementHandle* come IRD e l'handle di istruzione associato non era stato preparato o eseguito.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) *DescriptorHandle* è stato associato a un *StatementHandle* per il quale è stata chiamata una funzione in esecuzione asincrona (non questa) ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) *DescriptorHandle* è stato associato a un *StatementHandle* per il quale **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *DescriptorHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLGetDescField.This** asynchronous function was still executing when the SQLGetDescField function was called.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I021|Informazioni sul descrittore incoerenti|I campi SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE non formano un tipo SQL ODBC valido, un tipo SQL specifico del driver valido (per IPD) o un tipo ODBC C valido (per AAD o ARD).|  
|I090|Stringa o lunghezza del buffer non valida|(DM) * \*ValuePtr* era una stringa di caratteri e *BufferLength* era minore di zero.|  
|I091|Identificatore campo descrittore non valido|*FieldIdentifier* non è un campo definito da ODBC e non è un valore definito dall'implementazione.<br /><br /> *FieldIdentifier* non definito per *Il DescriptorHandle*.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) Il driver associato a *DescriptorHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Un'applicazione può chiamare **SQLGetDescField** per restituire il valore di un singolo campo di un record del descrittore. Una chiamata a **SQLGetDescField** può restituire l'impostazione di qualsiasi campo in qualsiasi tipo di descrittore, inclusi i campi di intestazione, i campi di record e i campi segnalibro. Un'applicazione può ottenere le impostazioni di più campi nello stesso descrittore o in criteri diversi, in ordine arbitrario, effettuando chiamate ripetute a **SQLGetDescField**. **SQLGetDescField** può anche essere chiamato per restituire campi descrittore definiti dal driver.  
  
 Per motivi di prestazioni, un'applicazione non deve chiamare **SQLGetDescField** per un IRD prima di eseguire un'istruzione.  
  
 Le impostazioni di più campi che descrivono il nome, il tipo di dati e l'archiviazione dei dati di colonna o parametro possono essere recuperate anche in una singola chiamata a **SQLGetDescRec**. **SQLGetStmtAttr** può essere chiamato per restituire l'impostazione di un singolo campo nell'intestazione del descrittore che è anche un attributo di istruzione. **SQLColAttribute**, **SQLDescribeCol**e **SQLDescribeParam** restituiscono campi di record o segnalibri.  
  
 Quando un'applicazione chiama **SQLGetDescField** per recuperare il valore di un campo che non è definito per un particolare tipo di descrittore, la funzione restituisce SQL_SUCCESS ma il valore restituito per il campo non è definito. Ad esempio, la chiamata di **SQLGetDescField** per il campo SQL_DESC_NAME o SQL_DESC_NULLABLE di un APD o ARD restituirà SQL_SUCCESS ma un valore non definito per il campo.  
  
 Quando un'applicazione chiama **SQLGetDescField** per recuperare il valore di un campo definito per un particolare tipo di descrittore ma che non ha alcun valore predefinito e non è stato ancora impostato, la funzione restituisce SQL_SUCCESS ma il valore restituito per il campo non è definito. Per ulteriori informazioni sull'inizializzazione dei campi descrittore e sulle descrizioni dei campi, vedere "Inizializzazione dei campi descrittore" in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Per ulteriori informazioni sui descrittori, vedere [Descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Recupero di più campi descrittoreGetting multiple descriptor fields|[Funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Impostazione di un singolo campo descrittore|[Funzione SQLSetDescFieldSQLSetDescField Function](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Impostazione di più campi descrittore|[Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
