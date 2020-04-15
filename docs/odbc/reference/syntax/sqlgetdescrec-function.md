---
title: SqlGetDescRec (funzione) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 87d7b971b379f19f8451e924932a5e699e9b9983
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285486"
---
# <a name="sqlgetdescrec-function"></a>Funzione SQLGetDescRec
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLGetDescRec** restituisce le impostazioni o i valori correnti di più campi di un record del descrittore. I campi restituiti descrivono il nome, il tipo di dati e l'archiviazione dei dati di colonna o parametro.  
  
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
 [Ingresso] Handle del descrittore.  
  
 *RecNumber*  
 [Ingresso] Indica il record del descrittore da cui l'applicazione cerca informazioni. I record del descrittore sono numerati a partire da 1, con il numero di record 0 come record del segnalibro. L'argomento *RecNumber* deve essere minore o uguale al valore di SQL_DESC_COUNT. Se *RecNumber* è minore o uguale a SQL_DESC_COUNT ma la riga non contiene dati per una colonna o un parametro, una chiamata a **SQLGetDescRec** restituirà i valori predefiniti dei campi. (Per ulteriori informazioni, vedere "Inizializzazione dei campi descrittore" in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 *Nome*  
 [Uscita] Puntatore a un buffer in cui restituire il campo SQL_DESC_NAME per il record del descrittore.  
  
 Se *Name* è NULL, *StringLengthPtr* restituirà comunque il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *Name*.  
  
 *BufferLength*  
 [Ingresso] Lunghezza del buffer*dei* nomi, in caratteri.  
  
 *StringLengthPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero di \*caratteri disponibili da restituire nel buffer *Name,* escluso il carattere di terminazione null. Se il numero di caratteri è maggiore o uguale a *BufferLength*, i dati in \* *Name* vengono troncati a *BufferLength* meno la lunghezza di un carattere di terminazione null e vengono terminati con null dal driver.  
  
 *TypePtr*  
 [Uscita] Puntatore a un buffer in cui restituire il valore del campo SQL_DESC_TYPE per il record del descrittore.  
  
 *SubTypePtr*  
 [Uscita] Per i record il cui tipo è SQL_DATETIME o SQL_INTERVAL, si tratta di un puntatore a un buffer in cui restituire il valore del campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *LengthPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il valore del campo SQL_DESC_OCTET_LENGTH per il record del descrittore.  
  
 *PrecisionePtr*  
 [Uscita] Puntatore a un buffer in cui restituire il valore del campo SQL_DESC_PRECISION per il record del descrittore.  
  
 *ScalePtr*  
 [Uscita] Puntatore a un buffer in cui restituire il valore del campo SQL_DESC_SCALE per il record del descrittore.  
  
 *NullablePtrNullablePtr*  
 [Uscita] Puntatore a un buffer in cui restituire il valore del campo SQL_DESC_NULLABLE per il record del descrittore.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA viene restituito se *RecNumber* è maggiore del numero corrente di record del descrittore.  
  
 SQL_NO_DATA viene restituito se *DescriptorHandle* è un handle IRD e l'istruzione è nello stato preparato o eseguito, ma non vi è alcun cursore aperto associato.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetDescRec** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_DESC e un *Handle* di *DescriptorHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLGetDescRec** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Il \* *buffer Name* non era sufficientemente grande per restituire l'intero campo del descrittore. Pertanto, il campo è stato troncato. La lunghezza del campo del descrittore non troncato viene restituita in :*StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07009|Indice descrittore non valido|L'argomento *FieldIdentifier* è un campo di record, l'argomento *RecNumber* è stato impostato su 0 e l'argomento *DescriptorHandle* è un handle IPD.<br /><br /> (DM) l'argomento *RecNumber* è stato impostato su 0 e l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_OFF e l'argomento *DescriptorHandle* è un handle IRD.<br /><br /> L'argomento *RecNumber* era minore di 0.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I007|L'istruzione associata non è preparata|*DescriptorHandle* è stato associato a un IRD e l'handle di istruzione associato non era nello stato preparato o eseguito.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) *DescriptorHandle* è stato associato a un *StatementHandle* per il quale è stata chiamata una funzione in esecuzione asincrona (non questa) ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) *DescriptorHandle* è stato associato a un *StatementHandle* per il quale **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *DescriptorHandle*. Questa funzione asincrona era ancora in esecuzione quando **SQLGetDescRec** è stato chiamato.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) Il driver associato a *DescriptorHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Un'applicazione può chiamare **SQLGetDescRec** per recuperare i valori dei seguenti campi descrittore per una singola colonna o parametro:  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (per i record il cui tipo è SQL_DATETIME o SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** non recupera i valori per i campi di intestazione.  
  
 Un'applicazione può impedire la restituzione dell'impostazione di un campo impostando l'argomento che corrisponde al campo su un puntatore null.  
  
 Quando un'applicazione chiama **SQLGetDescRec** per recuperare il valore di un campo che non è definito per un particolare tipo di descrittore, la funzione restituisce SQL_SUCCESS ma il valore restituito per il campo non è definito. Ad esempio, la chiamata di **SQLGetDescRec** per il campo SQL_DESC_NAME o SQL_DESC_NULLABLE di un APD o ARD restituirà SQL_SUCCESS ma un valore non definito per il campo.  
  
 Quando un'applicazione chiama **SQLGetDescRec** per recuperare il valore di un campo definito per un particolare tipo di descrittore ma che non ha alcun valore predefinito e non è stato ancora impostato, la funzione restituisce SQL_SUCCESS ma il valore restituito per il campo non è definito. Per ulteriori informazioni, vedere "Inizializzazione dei campi descrittore" in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 I valori dei campi possono anche essere recuperati singolarmente da una chiamata a **SQLGetDescField**. Per una descrizione dei campi in un record di descrittore, vedere [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Per ulteriori informazioni sui descrittori, vedere [Descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di una colonna|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Associazione di un parametro|[Pagina relativa alla funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Ottenere un campo descrittoreGetting a descriptor field|[Funzione SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Impostazione di più campi descrittore|[Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
