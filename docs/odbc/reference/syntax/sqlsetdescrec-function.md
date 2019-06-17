---
title: Funzione SQLSetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescRec
helpviewer_keywords:
- SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f76974a17fc12c4a72623c133586690c81269d06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536280"
---
# <a name="sqlsetdescrec-function"></a>Funzione SQLSetDescRec
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 Il **SQLSetDescRec** funzione imposta più campi di descrizione che interessano il tipo di dati e buffer associato a una colonna o parametro dati.  
  
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
 [Input] Handle descrittore. Questo non deve essere un handle IRD.  
  
 *RecNumber*  
 [Input] Indica se il record del descrittore che contiene i campi da impostare. Record del descrittore sono numerati da 0, con il numero di record 0 come il record di segnalibro. Questo argomento deve essere uguale o maggiore di 0. Se *RecNumber* è maggiore del valore di SQL_DESC_COUNT, modificato il valore di SQL_DESC_COUNTis *RecNumber*.  
  
 *Tipo*  
 [Input] Il valore su cui impostare il campo SQL_DESC_TYPE per il record del descrittore.  
  
 *SubType*  
 [Input] Per i record il cui tipo è SQL_DATETIME o SQL_INTERVAL, questo è il valore su cui impostare il campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *Lunghezza*  
 [Input] Il valore su cui impostare il campo SQL_DESC_OCTET_LENGTH per il record del descrittore.  
  
 *Precisione*  
 [Input] Il valore su cui impostare il campo SQL_DESC_PRECISION per il record del descrittore.  
  
 *Scala*  
 [Input] Il valore su cui impostare il campo SQL_DESC_SCALE per il record del descrittore.  
  
 *DataPtr*  
 [Posticipata Input o Output] Il valore su cui impostare il campo SQL_DESC_DATA_PTR per il record del descrittore. *DataPtr* può essere impostato su un puntatore null.  
  
 Il *DataPtr* argomento può essere impostato su un puntatore null per impostare il campo SQL_DESC_DATA_PTR a un puntatore null. Se l'handle nel *DescriptorHandle* argomento è associato un ARD, rimuove il binding della colonna.  
  
 *StringLengthPtr*  
 [Posticipata Input o Output] Il valore su cui impostare il campo SQL_DESC_OCTET_LENGTH_PTR per il record del descrittore. *StringLengthPtr* può essere impostata su un puntatore null per impostare il campo SQL_DESC_OCTET_LENGTH_PTR su un puntatore null.  
  
 *IndicatorPtr*  
 [Posticipata Input o Output] Il valore su cui impostare il campo SQL_DESC_INDICATOR_PTR per il record del descrittore. *IndicatorPtr* può essere impostata su un puntatore null per impostare il campo SQL_DESC_INDICATOR_PTR su un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSetDescRec** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_DESC e un *gestiscono* dei *DescriptorHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLSetDescRec** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07009|Indice del descrittore non valido|Il *RecNumber* argomento è stato impostato su 0 e il *DescriptorHandle* definiti a un handle IPD.<br /><br /> Il *RecNumber* argomento era minore di 0.<br /><br /> Il *RecNumber* l'argomento è maggiore del numero massimo di colonne o parametri in grado di supportare l'origine dati, e il *DescriptorHandle* argomento era un APD, IPD o ARD.<br /><br /> Il *RecNumber* l'argomento è uguale a 0 e il *DescriptorHandle* argomento definito un APD allocati in modo implicito. (Questo errore non viene eseguito con un descrittore applicazione allocati in modo esplicito perché non è possibile sapere se un descrittore applicazione allocati in modo esplicito è un APD o ARD fino alla fase di esecuzione.)|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) di *DescriptorHandle* è stato associato un *StatementHandle* per i quali è stata chiamata una funzione di esecuzione asincrona (non presente uno) ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* con cui il *DescriptorHandle* è stato associato e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.<br /><br /> (DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *DescriptorHandle*. Questa funzione aynchronous era ancora in esecuzione quando il **SQLSetDescRec** funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per uno degli handle di istruzione associati il *DescriptorHandle* SQL_PARAM_DATA_AVAILABLE restituito. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY016|Non è possibile modificare un descrittore delle righe di implementazione|Il *DescriptorHandle* argomento è stato associato a un'implementazione.|  
|HY021|Informazioni descrittore incoerenti.|Il *tipo* campo o qualsiasi altro campo associato al campo SQL_DESC_TYPE nel descrittore di, è non stata valide o coerenti.<br /><br /> Le informazioni sul descrittore controllati durante una verifica coerenza non era coerente. (Vedere "Le verifiche coerenza," più avanti in questa sezione).|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il driver è stato un ODBC 2 *. x* driver, il descrittore è un ARD, il *ColumnNumber* argomento è stato impostato su 0 e il valore specificato per l'argomento *BufferLength* era non è uguale a 4.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *DescriptorHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Un'applicazione può chiamare **SQLSetDescRec** per impostare i campi seguenti per una singola colonna o un parametro:  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (per i record il cui tipo è SQL_DATETIME o SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  Se una chiamata a **SQLSetDescRec** ha esito negativo, il contenuto del record del descrittore identificato dalle *RecNumber* argomento non sono definiti.  
  
 Quando si associa una colonna o parametro, **SQLSetDescRec** consente di modificare più campi che interessano l'associazione senza chiamare **SQLBindCol** oppure **SQLBindParameter** o eseguire più chiamate a **SQLSetDescField**. **SQLSetDescRec** può impostare i campi per un descrittore non è attualmente associato a un'istruzione. Si noti che **SQLBindParameter** imposta più campi **SQLSetDescRec**, impostare campi su un APD sia un IPD in un'unica chiamata e non richiede un handle di descrittore.  
  
> [!NOTE]  
>  L'attributo di istruzione SQL_ATTR_USE_BOOKMARKS deve sempre essere impostata prima di chiamare **SQLSetDescRec** con un *RecNumber* argomento 0 per impostare i campi di segnalibro. Sebbene non sia obbligatorio, è consigliabile.  
  
## <a name="consistency-checks"></a>Verifiche di coerenza  
 Verifica di coerenza viene eseguita automaticamente dal driver ogni volta che un'applicazione imposta il campo SQL_DESC_DATA_PTR di un APD, ARD o IPD. Se non è coerente con gli altri campi, uno dei campi **SQLSetDescRec** restituiranno SQLSTATE HY021 (informazioni sul descrittore inconsistenti).  
  
 Ogni volta che un'applicazione imposta il campo SQL_DESC_DATA_PTR di un APD, ARD o IPD, il driver verificherà che il valore del campo SQL_DESC_TYPE e i valori applicabili a tale campo SQL_DESC_TYPE siano validi e coerenti. Questa verifica viene sempre eseguita quando **SQLBindParameter** oppure **SQLBindCol** viene chiamato o quando **SQLSetDescRec** viene chiamato per un APD, ARD o IPD. Questa coerenza include i controlli seguenti in campi di descrizione:  
  
-   Il campo SQL_DESC_TYPE deve essere valido ODBC C o tipi SQL o un tipo SQL specifiche del driver. Il campo SQL_DESC_CONCISE_TYPE deve essere uno dei tipi di dati ODBC C o SQL validi o un tipo SQL o C specifiche del driver, inclusi i tipi di data/ora e intervallo concisi.  
  
-   Se il campo di record SQL_DESC_TYPE è SQL_DATETIME o SQL_INTERVAL, il campo SQL_DESC_DATETIME_INTERVAL_CODE deve essere uno dei codici di intervallo o data/ora valido. (Vedere la descrizione del campo SQL_DESC_DATETIME_INTERVAL_CODE [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
-   Se il campo SQL_DESC_TYPE indica un tipo numerico, vengono verificati i campi di SQL_DESC_PRECISION e SQL_DESC_SCALE sia valido.  
  
-   Se il campo SQL_DESC_CONCISE_TYPE è un tipo di dati di ora o timestamp, un intervallo di tipo con un componente di secondi, o uno dei tipi di dati di intervallo con un componente della fase, viene verificato il campo SQL_DESC_PRECISION sia una precisione in secondi valido.  
  
-   Se il SQL_DESC_CONCISE_TYPE è un tipo di dati di intervallo, il campo SQL_DESC_DATETIME_INTERVAL_PRECISION viene verificato che sia un valore di precisione iniziale intervallo valido.  
  
 Il campo SQL_DESC_DATA_PTR di un IPD non è in genere impostato; Tuttavia, un'applicazione può farlo per forzare un controllo di consistenza dei campi IPD. Impossibile eseguire una verifica coerenza su un'implementazione. Il valore impostato per il campo SQL_DESC_DATA_PTR dell'IPD non viene effettivamente archiviato e non può essere recuperato da una chiamata a **SQLGetDescField** oppure **SQLGetDescRec**; l'impostazione viene eseguita solo per forzare il verifica della coerenza.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di una colonna|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Un parametro di associazione|[Funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Recupero di un campo del descrittore single|[Funzione SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Recupero di più campi di descrizione|[Funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configurazione dei campi del descrittore single|[Funzione SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
