---
title: SqlSetDescRec (funzione) Documenti Microsoft
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescRec
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescRec
helpviewer_keywords:
- SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b29879ff7635d6eb7d5a0f7489ff3994758d4a35
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299531"
---
# <a name="sqlsetdescrec-function"></a>Funzione SQLSetDescRec
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 La funzione **SQLSetDescRec** imposta più campi descrittore che influiscono sul tipo di dati e sul buffer associati a dati di colonna o di parametro.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLSetDescRec(  
      SQLHDESC      DescriptorHandle,  
      SQLSMALLINT   RecNumber,  
      SQLSMALLINT   Type,  
      SQLSMALLINT   SubType,  
      SQLLEN        Length,  
      SQLSMALLINT   Precision,  
      SQLSMALLINT   Scale,  
      SQLPOINTER    DataPtr,  
      SQLLEN *      StringLengthPtr,  
      SQLLEN *      IndicatorPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *DescriptorHandle*  
 [Ingresso] Handle del descrittore. Non deve trattarsi di un handle IRD.  
  
 *RecNumber*  
 [Ingresso] Indica il record del descrittore che contiene i campi da impostare. I record del descrittore sono numerati da 0, con il numero di record 0 come record del segnalibro. Questo argomento deve essere uguale o maggiore di 0. Se *RecNumber* è maggiore del valore di SQL_DESC_COUNT, SQL_DESC_COUNTis modificato nel valore di *RecNumber*.  
  
 *Tipo*  
 [Ingresso] Valore su cui impostare il campo SQL_DESC_TYPE per il record del descrittore.  
  
 *Sottotipo*  
 [Ingresso] Per i record il cui tipo è SQL_DATETIME o SQL_INTERVAL, questo è il valore su cui impostare il campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *Lunghezza*  
 [Ingresso] Valore su cui impostare il campo SQL_DESC_OCTET_LENGTH per il record del descrittore.  
  
 *Precisione*  
 [Ingresso] Valore su cui impostare il campo SQL_DESC_PRECISION per il record del descrittore.  
  
 *Scalabilità*  
 [Ingresso] Valore su cui impostare il campo SQL_DESC_SCALE per il record del descrittore.  
  
 *DataPtr*  
 [Ingresso o uscita posticipati] Valore su cui impostare il campo SQL_DESC_DATA_PTR per il record del descrittore. *DataPtr* può essere impostato su un puntatore null.  
  
 L'argomento *DataPtr* può essere impostato su un puntatore null per impostare il campo SQL_DESC_DATA_PTR su un puntatore null. Se l'handle nel *DescriptorHandle* argomento è associato a un ARD, questo disassocia la colonna.  
  
 *StringLengthPtr*  
 [Ingresso o uscita posticipati] Valore su cui impostare il campo SQL_DESC_OCTET_LENGTH_PTR per il record del descrittore. *StringLengthPtr* può essere impostato su un puntatore null per impostare il campo SQL_DESC_OCTET_LENGTH_PTR su un puntatore null.  
  
 *IndicatorPtr*  
 [Ingresso o uscita posticipati] Valore su cui impostare il campo SQL_DESC_INDICATOR_PTR per il record del descrittore. *IndicatorPtr* può essere impostato su un puntatore null per impostare il campo SQL_DESC_INDICATOR_PTR su un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSetDescRec** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_DESC e un *Handle* di *DescriptorHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLSetDescRec** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07009|Indice descrittore non valido|L'argomento *RecNumber* è stato impostato su 0 e *DescriptorHandle* fa riferimento a un handle IPD.<br /><br /> L'argomento *RecNumber* era minore di 0.<br /><br /> L'argomento *RecNumber* è maggiore del numero massimo di colonne o parametri che l'origine dati può supportare e l'argomento *DescriptorHandle* è Un APD, UN IPD o ard.<br /><br /> L'argomento *RecNumber* è uguale a 0 e l'argomento *DescriptorHandle* fa riferimento a un APD allocato in modo implicito. Questo errore non si verifica con un descrittore di applicazione allocato in modo esplicito perché non è noto se un descrittore di applicazione allocato in modo esplicito è un APD o ARD fino all'ora di esecuzione.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) *il DescriptorHandle* è stato associato a un *StatementHandle* per il quale è stata chiamata una funzione in esecuzione asincrona (non questa) ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per il *StatementHandle* a cui *l'oggetto DescriptorHandle* è stato associato e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *DescriptorHandle*. Questa funzione ayncronous era ancora in esecuzione quando è stata chiamata la funzione **SQLSetDescRec.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per uno degli handle di istruzione associati a *DescriptorHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY016 (informazioni in inglese)|Impossibile modificare un descrittore di riga di implementazione|L'argomento *DescriptorHandle* è stato associato a un IRD.|  
|I021|Informazioni sul descrittore incoerenti|Il campo *Tipo* o qualsiasi altro campo associato al campo SQL_DESC_TYPE nel descrittore non è valido o coerente.<br /><br /> Le informazioni sul descrittore controllate durante una verifica di coerenza non erano coerenti. (Vedere "Controlli di coerenza", più avanti in questa sezione.)|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il driver era un driver ODBC *2.x,* il descrittore era un ARD, il *ColumnNumber* argomento è stato impostato su 0 e il valore specificato per l'argomento *BufferLength* non è uguale a 4.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) Il driver associato a *DescriptorHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Un'applicazione può chiamare SQLSetDescRec per impostare i campi seguenti per una singola colonna o parametro:An application can call **SQLSetDescRec** to set the following fields for a single column or parameter:  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (per i record il cui tipo è SQL_DATETIME o SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  Se una chiamata a **SQLSetDescRec** ha esito negativo, il contenuto del record del descrittore identificato dal *RecNumber* argomento non è definito.  
  
 Quando si associa una colonna o un parametro, **SQLSetDescRec** consente di modificare più campi che influiscono sull'associazione senza chiamare **SQLBindCol** o **SQLBindParameter** o effettuare più chiamate a **SQLSetDescField**. **SQLSetDescRec** può impostare campi su un descrittore non attualmente associato a un'istruzione. Si noti che **SQLBindParameter** imposta più campi di **SQLSetDescRec**, può impostare i campi su un APD e un IPD in una chiamata e non richiede un handle di descrittore.  
  
> [!NOTE]  
>  L'attributo di istruzione SQL_ATTR_USE_BOOKMARKS deve essere sempre impostato prima di chiamare **SQLSetDescRec** con un *Argomento RecNumber* pari a 0 per impostare i campi segnalibro. Anche se questo non è obbligatorio, è fortemente raccomandato.  
  
## <a name="consistency-checks"></a>Controlli di coerenza  
 Una verifica di coerenza viene eseguita automaticamente dal driver ogni volta che un'applicazione imposta il campo SQL_DESC_DATA_PTR di un APD, ARD o IPD. Se uno dei campi non è coerente con altri campi, **SQLSetDescRec** restituirà SQLSTATE HY021 (informazioni sul descrittore incoerenti).  
  
 Ogni volta che un'applicazione imposta il campo SQL_DESC_DATA_PTR di un APD, ARD o IPD, il driver verifica che il valore del campo SQL_DESC_TYPE e i valori applicabili a tale campo SQL_DESC_TYPE siano validi e coerenti. Questo controllo viene sempre eseguito quando **SQLBindParameter** o **SQLBindCol** viene chiamato o quando **SQLSetDescRec** viene chiamato per un APD, ARD o IPD. Questa verifica di coerenza include i seguenti controlli sui campi descrittore:  
  
-   Il campo SQL_DESC_TYPE deve essere uno dei tipi C o SQL ODBC validi o un tipo SQL specifico del driver. Il campo SQL_DESC_CONCISE_TYPE deve essere uno dei tipi C o SQL ODBC validi o un tipo C o SQL specifico del driver, inclusi i tipi di intervallo e ora concisi.  
  
-   Se il campo SQL_DESC_TYPE record è SQL_DATETIME o SQL_INTERVAL, il campo SQL_DESC_DATETIME_INTERVAL_CODE deve essere uno dei codici di data/ora o di intervallo validi. Vedere la descrizione del campo SQL_DESC_DATETIME_INTERVAL_CODE in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
-   Se il campo SQL_DESC_TYPE indica un tipo numerico, i campi SQL_DESC_PRECISION e SQL_DESC_SCALE vengono considerati validi.  
  
-   Se il campo SQL_DESC_CONCISE_TYPE è un tipo di dati ora o timestamp, un tipo di intervallo con un componente secondi o uno dei tipi di dati intervallo con un componente time, il campo SQL_DESC_PRECISION viene verificato come una precisione valida dei secondi.  
  
-   Se il SQL_DESC_CONCISE_TYPE è un tipo di dati intervallo, il campo SQL_DESC_DATETIME_INTERVAL_PRECISION viene verificato come un valore di precisione interlinea intervallo valido.  
  
 Il campo SQL_DESC_DATA_PTR di un IPD non è normalmente impostato; tuttavia, un'applicazione può farlo per forzare una verifica di coerenza dei campi IPD. Non è possibile eseguire una verifica di coerenza su un IRD. Il valore su cui è impostato il campo SQL_DESC_DATA_PTR dell'IPD non è effettivamente archiviato e non può essere recuperato da una chiamata a **SQLGetDescField** o **SQLGetDescRec;** l'impostazione viene effettuata solo per forzare la verifica della coerenza.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di una colonna|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Associazione di un parametro|[Pagina relativa alla funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Ottenere un singolo campo descrittoreGetting a single descriptor field|[Funzione SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Recupero di più campi descrittoreGetting multiple descriptor fields|[Funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Impostazione di campi a descrittore singolo|[Funzione SQLSetDescFieldSQLSetDescField Function](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
