---
title: Funzione SQLGetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescRec
helpviewer_keywords:
- SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c27b16d8b72e289f66a051cb2710004f72309599
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103793"
---
# <a name="sqlgetdescrec-function"></a>Funzione SQLGetDescRec
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLGetDescRec** restituisce le impostazioni correnti o i valori di più campi di un record del descrittore. I campi restituiti descrivono il nome, tipo di dati e archiviazione dei dati di colonna o parametro.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLGetDescRec(  
      SQLHDESC        DescriptorHandle,  
      SQLSMALLINT     RecNumber,  
      SQLCHAR *       Name,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLSMALLINT *   TypePtr,  
      SQLSMALLINT *   SubTypePtr,  
      SQLLEN *        LengthPtr,  
      SQLSMALLINT *   PrecisionPtr,  
      SQLSMALLINT *   ScalePtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *DescriptorHandle*  
 [Input] Handle descrittore.  
  
 *RecNumber*  
 [Input] Indica se il record del descrittore da cui l'applicazione cerca le informazioni. Record del descrittore sono numerati da 1, con il numero di record 0 come il record di segnalibro. Il *RecNumber* argomento deve essere minore o uguale al valore di SQL_DESC_COUNT. Se *RecNumber* è minore o uguale a SQL_DESC_COUNT ma la riga non contiene dati per una colonna o parametro, una chiamata a **SQLGetDescRec** restituirà i valori predefiniti dei campi. (Per altre informazioni, vedere "Inizializzazione di campi di descrizione" nella [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *Name*  
 [Output] Un puntatore a un buffer in cui restituire il campo SQL_DESC_NAME per il record del descrittore.  
  
 Se *Name* sia impostato su NULL *StringLengthPtr* continuerà a restituire il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui punta  *Nome*.  
  
 *BufferLength*  
 [Input] Lunghezza di **nome* buffer, in caratteri.  
  
 *StringLengthPtr*  
 [Output] Un puntatore a un buffer in cui restituire il numero di caratteri di dati disponibili per restituire il \* *nome* buffer, escluso il carattere di terminazione null. Se il numero di caratteri è maggiore o uguale a *BufferLength*, i dati in \* *Name* verranno troncati alla *BufferLength* meno la lunghezza di un carattere di terminazione null ed è con terminazione null dal driver.  
  
 *TypePtr*  
 [Output] Un puntatore a un buffer in cui restituire il valore del campo SQL_DESC_TYPE per il record del descrittore.  
  
 *SubTypePtr*  
 [Output] Per i record il cui tipo è SQL_DATETIME o SQL_INTERVAL, questo è un puntatore a un buffer in cui restituire il valore del campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *LengthPtr*  
 [Output] Un puntatore a un buffer in cui restituire il valore del campo SQL_DESC_OCTET_LENGTH per il record del descrittore.  
  
 *PrecisionPtr*  
 [Output] Un puntatore a un buffer in cui restituire il valore del campo SQL_DESC_PRECISION per il record del descrittore.  
  
 *ScalePtr*  
 [Output] Un puntatore a un buffer in cui restituire il valore del campo SQL_DESC_SCALE per il record del descrittore.  
  
 *NullablePtr*  
 [Output] Un puntatore a un buffer in cui restituire il valore del campo SQL_DESC_NULLABLE per il record del descrittore.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
 Se non viene restituito SQL_NO_DATA *RecNumber* è maggiore del numero corrente di record del descrittore.  
  
 Se non viene restituito SQL_NO_DATA *DescriptorHandle* è un handle IRD e l'istruzione si trova nello stato preparato o eseguito, ma si è verificato alcun cursore aperto è associato.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetDescRec** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_DESC e un *gestiscono* dei *DescriptorHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLGetDescRec** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Il buffer \* *nome* non era sufficientemente grande per restituire il campo di descrizione intero. Pertanto, il campo è stato troncato. Viene restituita la lunghezza del campo del descrittore non troncato **StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07009|Indice del descrittore non valido|Il *FieldIdentifier* l'argomento è un campo di record, il *RecNumber* argomento è stato impostato su 0 e il *DescriptorHandle* argomento era un handle IPD.<br /><br /> (DM) di *RecNumber* argomento è stato impostato su 0 e l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stata impostata su SQL_UB_OFF e il *DescriptorHandle* argomento era un handle IRD.<br /><br /> Il *RecNumber* argomento era minore di 0.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver non è riuscito ad allocare la memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY007|L'istruzione associata non è pronto|*DescriptorHandle* era associato un IRD e l'handle di istruzione associata non è stato nello stato preparato o eseguito.|  
|HY010|Errore nella sequenza della funzione|(DM) *DescriptorHandle* è stato associato un *StatementHandle* per i quali è stata chiamata una funzione di esecuzione asincrona (non presente uno) ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) *DescriptorHandle* è stato associato un *StatementHandle* per il quale **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.<br /><br /> (DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *DescriptorHandle*. Questa funzione asincrona era ancora in esecuzione quando **SQLGetDescRec** è stato chiamato.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associati *DescriptorHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Un'applicazione può chiamare **SQLGetDescRec** per recuperare i valori dei campi del descrittore seguenti per una singola colonna o un parametro:  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (per i record il cui tipo è SQL_DATETIME o SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** non recuperare i valori per i campi di intestazione.  
  
 Un'applicazione può impedire la restituzione dell'impostazione del campo impostando l'argomento che corrisponde al campo a un puntatore null.  
  
 Quando un'applicazione chiama **SQLGetDescRec** per recuperare il valore di un campo che non è definito per un tipo di descrittore particolare, la funzione restituisce SQL_SUCCESS, ma il valore restituito per il campo è definito. Ad esempio, chiamando **SQLGetDescRec** per il campo SQL_DESC_NAME o SQL_DESC_NULLABLE di un APD o ARD restituisce SQL_SUCCESS, ma un valore indefinito per il campo.  
  
 Quando un'applicazione chiama **SQLGetDescRec** per recuperare il valore di un campo definito per un tipo di descrittore particolare ma che non dispone di alcun valore predefinito e non è stato ancora impostato, la funzione restituisce SQL_SUCCESS, ma il valore restituito per il campo è definito. Per altre informazioni, vedere "Inizializzazione di campi di descrizione" nella [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 I valori dei campi possono essere recuperati anche singolarmente mediante una chiamata a **SQLGetDescField**. Per una descrizione dei campi in un'intestazione di descrittore o record, vedere [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Per altre informazioni sui descrittori, vedere [descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di una colonna|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Un parametro di associazione|[Funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Recupero di un campo di descrizione|[Funzione SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|L'impostazione di più campi di descrizione|[Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
