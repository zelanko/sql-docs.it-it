---
title: Funzione SQLCopyDesc . Documenti Microsoft
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef1fa5b319e8d72d5b70e6f2010e493eec6f844a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301228"
---
# <a name="sqlcopydesc-function"></a>Funzione SQLCopyDesc
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLCopyDesc** copia le informazioni sul descrittore da un handle di descrittore a un altro.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>Argomenti  
 *SourceDescHandle*  
 [Ingresso] Handle del descrittore di origine.  
  
 *TargetDescHandle*  
 [Ingresso] Handle del descrittore di destinazione. L'argomento *TargetDescHandle* può essere un handle per un descrittore dell'applicazione o un IPD. *TargetDescHandle* non può essere impostato su un handle di un IRD o **SQLCopyDesc** restituirà SQLSTATE HY016 (Impossibile modificare un descrittore di riga di implementazione).  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLCopyDesc** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_DESC e un *handle* di *TargetDescHandle*. Se nella chiamata è stato passato un *sourceDescHandle* non valido, verrà restituito SQL_INVALID_HANDLE ma non verrà restituito alcun SQLSTATE. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLCopyDesc** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
 Quando viene restituito un errore, la chiamata a **SQLCopyDesc** viene immediatamente interrotta e il contenuto dei campi nel *descrittore TargetDescHandle* non è definito.  
  
 Poiché **SQLCopyDesc** può essere implementato chiamando **SQLGetDescField** e **SQLSetDescField**, **SQLCopyDesc** può restituire SQLTEs restituiti da **SQLGetDescField** o **SQLSetDescField**.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I007|L'istruzione associata non è preparata|*SourceDescHandle* è stato associato a un IRD e l'handle di istruzione associato non si trovava nello stato preparato o eseguito.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) L'handle del descrittore in *SourceDescHandle* o *TargetDescHandle* è stato associato a un *StatementHandle* per il quale è stata chiamata una funzione in esecuzione asincrona (non questa) ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) l'handle del descrittore in *SourceDescHandle* o *TargetDescHandle* è stato associato a un *StatementHandle* per il quale **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.<br /><br /> (DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *SourceDescHandle* o *TargetDescHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione **SQLCopyDesc.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per uno degli handle di istruzione associati a *SourceDescHandle* o *TargetDescHandle* e ha restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY016 (informazioni in inglese)|Impossibile modificare un descrittore di riga di implementazione|*TargetDescHandle* è stato associato a un IRD.|  
|I021|Informazioni sul descrittore incoerenti|Le informazioni sul descrittore controllate durante una verifica di coerenza non erano coerenti. Per ulteriori informazioni, vedere "Controlli di coerenza" in **SQLSetDescField**.|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo/opzione non valido|La chiamata a **SQLCopyDesc** ha richiesto una chiamata a **SQLSetDescField**, ma * \*ValuePtr* non è valido per l'argomento *FieldIdentifier* in *TargetDescHandle*.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato *a SourceDescHandle* o *TargetDescHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Una chiamata a **SQLCopyDesc** copia i campi dell'handle del descrittore di origine nell'handle del descrittore di destinazione. I campi possono essere copiati solo in un descrittore dell'applicazione o in un IPD, ma non in un IRD. I campi possono essere copiati da un'applicazione o da un descrittore di implementazione.  
  
 I campi possono essere copiati da un IRD solo se l'handle dell'istruzione è nello stato preparato o eseguito. in caso contrario, la funzione restituisce SQLSTATE HY007 (istruzione associated non è preparata).  
  
 I campi possono essere copiati da un IPD indipendentemente dal fatto che un'istruzione sia stata preparata o meno. Se è stata preparata un'istruzione SQL con parametri dinamici e il popolamento automatico dell'IPD è supportato e abilitato, l'IPD viene popolato dal driver. Quando **SQLCopyDesc** viene chiamato con IPD come *SourceDescHandle*, i campi popolati vengono copiati. Se l'IPD non viene popolato dal driver, viene copiato il contenuto dei campi originariamente nell'IPD.  
  
 Tutti i campi del descrittore, ad eccezione di SQL_DESC_ALLOC_TYPE (che specifica se l'handle del descrittore è stato allocato automaticamente o in modo esplicito), vengono copiati, indipendentemente dal fatto che il campo sia definito o meno per il descrittore di destinazione. I campi copiati sovrascrivono i campi esistenti.  
  
 Il driver copia tutti i campi del descrittore se gli argomenti *SourceDescHandle* e *TargetDescHandle* sono associati allo stesso driver, anche se i driver si trovano su due connessioni o ambienti diversi. Se gli argomenti *SourceDescHandle* e *TargetDescHandle* sono associati a driver diversi, Gestione Driver copia i campi definiti da ODBC, ma non copia campi o campi definiti dal driver non definiti da ODBC per il tipo di descrittore.  
  
 La chiamata a **SQLCopyDesc** viene interrotta immediatamente se si verifica un errore.  
  
 Quando il campo SQL_DESC_DATA_PTR viene copiato, viene eseguita una verifica di coerenza sul descrittore di destinazione. Se la verifica di coerenza ha esito negativo, SQLSTATE HY021 (informazioni sul descrittore incoerenti) viene restituito e la chiamata a **SQLCopyDesc** viene immediatamente interrotta. Per ulteriori informazioni sulle verifiche di coerenza, vedere "Controlli di coerenza" in [Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 Gli handle di descrittore possono essere copiati tra le connessioni anche se le connessioni si trovano in ambienti diversi. Se Gestione Driver rileva che gli handle di origine e descrittore di destinazione non appartengono alla stessa connessione e le due connessioni appartengono a driver separati, implementa **SQLCopyDesc** eseguendo una copia campo per campo utilizzando **SQLGetDescField** e **SQLSetDescField**.  
  
 Quando **SQLCopyDesc** viene chiamato con un *SourceDescHandle* su un driver e un *TargetDescHandle* su un altro driver, la coda di errore di *SourceDescHandle* viene cancellata. Ciò si verifica perché **SQLCopyDesc** in questo caso viene implementato da chiamate a **SQLGetDescField** e **SQLSetDescField**.  
  
> [!NOTE]  
>  Un'applicazione potrebbe essere in grado di associare un handle di descrittore allocato in modo esplicito a un *statementHandle*, anziché chiamare **SQLCopyDesc** per copiare i campi da un descrittore a un altro. Un descrittore allocato in modo esplicito può essere associato a un altro *StatementHandle* nello stesso *Oggetto ConnectionHandle* impostando l'attributo di istruzione SQL_ATTR_APP_ROW_DESC o SQL_ATTR_APP_PARAM_DESC sull'handle del descrittore allocato in modo esplicito. Al termine, NON è necessario chiamare **SQLCopyDesc** per copiare i valori dei campi del descrittore da un descrittore a un altro. Un handle descrittore non può essere associato a un *StatementHandle* in un altro *Oggetto ConnectionHandle*, tuttavia; per utilizzare gli stessi valori dei campi del descrittore su *StatementHandles* su *ConnectionHandles*diversi , **SQLCopyDesc** deve essere chiamato.  
  
 Per una descrizione dei campi in un record di descrittore, vedere [Funzione SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Per ulteriori informazioni sui descrittori, vedere [Descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="copying-rows-between-tables"></a>Copia di righe tra tabelle  
 Un'applicazione può copiare i dati da una tabella a un'altra senza copiare i dati a livello di applicazione. A tale scopo, l'applicazione associa gli stessi buffer di dati e le stesse informazioni sul descrittore a un'istruzione che recupera i dati e l'istruzione che inserisce i dati in una copia. Questa operazione può essere eseguita condividendo un descrittore dell'applicazione (associando un descrittore allocato in modo esplicito come ARD a un'istruzione e APD in un'altra) o utilizzando **SQLCopyDesc** per copiare le associazioni tra ARD e APD delle due istruzioni. Se le istruzioni si trovano su connessioni diverse, è necessario utilizzare **SQLCopyDesc.** Inoltre, **SQLCopyDesc** deve essere chiamato per copiare le associazioni tra l'IRD e l'IPD delle due istruzioni. Quando si copiano tra istruzioni sulla stessa connessione, il SQL_ACTIVE_STATEMENTS tipo di informazioni restituito dal driver per una chiamata a **SQLGetInfo** deve essere maggiore di 1 affinché questa operazione abbia esito positivo. (Questo non è il caso quando si copia tra le connessioni.)  
  
### <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, le operazioni di descrittore vengono utilizzate per copiare i campi della tabella PartsSource nella tabella PartsCopy. Il contenuto della tabella PartsSource viene recuperato nei buffer del set di righe in *hstmt0*. Questi valori vengono utilizzati come parametri di un'istruzione INSERT in *hstmt1* per popolare le colonne della tabella PartsCopy. A tale scopo, i campi dell'IRD di *hstmt0* vengono copiati nei campi dell'IPD di *hstmt1*e i campi dell'ARD di *hstmt0* vengono copiati nei campi dell'APD di *hstmt1*. Utilizzare **SQLSetDescField** per impostare l'attributo SQL_DESC_PARAMETER_TYPE dell'IPD su SQL_PARAM_INPUT quando si copiano campi IRD da un'istruzione con parametri di output in campi IPD che devono essere parametri di input.  
  
```cpp  
#define ROWS 100  
#define DESC_LEN 50  
#define SQL_SUCCEEDED(rc) (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO)  
  
// Template for a row  
typedef struct {  
   SQLINTEGER   sPartID;  
   SQLINTEGER   cbPartID;  
   SQLUCHAR     szDescription[DESC_LENGTH];  
   SQLINTEGER   cbDescription;  
   REAL         sPrice;  
   SQLINTEGER   cbPrice;  
} PartsSource;  
  
PartsSource    rget[ROWS];          // rowset buffer  
SQLUSMALLINT   sts_ptr[ROWS];       // status pointer  
SQLHSTMT       hstmt0, hstmt1;  
SQLHDESC       hArd0, hIrd0, hApd1, hIpd1;  
  
// ARD and IRD of hstmt0  
SQLGetStmtAttr(hstmt0, SQL_ATTR_APP_ROW_DESC, &hArd0, 0, NULL);  
SQLGetStmtAttr(hstmt0, SQL_ATTR_IMP_ROW_DESC, &hIrd0, 0, NULL);  
  
// APD and IPD of hstmt1  
SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_PARAM_DESC, &hApd1, 0, NULL);  
SQLGetStmtAttr(hstmt1, SQL_ATTR_IMP_PARAM_DESC, &hIpd1, 0, NULL);  
  
// Use row-wise binding on hstmt0 to fetch rows  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER) sizeof(PartsSource), 0);  
  
// Set rowset size for hstmt0  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
  
// Execute a select statement  
SQLExecDirect(hstmt0, "SELECT PARTID, DESCRIPTION, PRICE FROM PARTS ORDER BY 3, 1, 2"",  
               SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt0, 1, SQL_C_SLONG, rget[0].sPartID, 0,   
   &rget[0].cbPartID);  
SQLBindCol(hstmt0, 2, SQL_C_CHAR, &rget[0].szDescription, DESC_LEN,   
   &rget[0].cbDescription);  
SQLBindCol(hstmt0, 3, SQL_C_FLOAT, rget[0].sPrice,   
   0, &rget[0].cbPrice);  
  
// Perform parameter bindings on hstmt1.   
SQLCopyDesc(hArd0, hApd1);  
SQLCopyDesc(hIrd0, hIpd1);  
  
// Set the array status pointer of IRD  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_STATUS_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the ARRAY_STATUS_PTR field of APD to be the same  
// as that in IRD.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_PARAM_OPERATION_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the hIpd1 records as input parameters  
rc = SQLSetDescField(hIpd1, 1, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 2, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 3, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
  
// Prepare an insert statement on hstmt1. PartsCopy is a copy of  
// PartsSource  
SQLPrepare(hstmt1, "INSERT INTO PARTS_COPY VALUES (?, ?, ?)", SQL_NTS);  
  
// In a loop, fetch a rowset, and copy the fetched rowset to PARTS_COPY  
  
rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
while (SQL_SUCCEEDED(rc)) {  
  
   // After the call to SQLFetchScroll, the status array has row   
   // statuses. This array is used as input status in the APD  
   // and hence determines which elements of the rowset buffer  
   // are inserted.  
   SQLExecute(hstmt1);  
  
   rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
} // while  
```  
  
### <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Recupero di più campi descrittoreGetting multiple descriptor fields|[Funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Impostazione di un singolo campo descrittore|[Funzione SQLSetDescFieldSQLSetDescField Function](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Impostazione di più campi descrittore|[Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
