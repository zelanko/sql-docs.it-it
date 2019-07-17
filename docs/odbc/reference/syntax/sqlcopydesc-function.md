---
title: Funzione SQLCopyDesc | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bacf438180dd6fe2823660e8275e48a2316e9efa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121437"
---
# <a name="sqlcopydesc-function"></a>Funzione SQLCopyDesc
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLCopyDesc** copia le informazioni sul descrittore da handle uno descrittore a un altro.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>Argomenti  
 *SourceDescHandle*  
 [Input] Handle descrittore di origine.  
  
 *TargetDescHandle*  
 [Input] Handle descrittore di destinazione. Il *TargetDescHandle* argomento può essere un handle a un descrittore applicazione o un IPD. *TargetDescHandle* non può essere impostata su un handle per un'implementazione, oppure **SQLCopyDesc** restituiranno SQLSTATE HY016 (non è possibile modificare un descrittore delle righe di implementazione).  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLCopyDesc** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_DESC e un *gestiscono* dei *TargetDescHandle*. Se un valore non valido *SourceDescHandle* è stato passato nella chiamata, verrà restituito SQL_INVALID_HANDLE ma non verrà restituito alcun valore SQLSTATE. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLCopyDesc** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
 Quando viene restituito un errore, la chiamata a **SQLCopyDesc** viene immediatamente interrotta e il contenuto dei campi nella *TargetDescHandle* descrittore sono definiti.  
  
 In quanto **SQLCopyDesc** può essere implementata chiamando **SQLGetDescField** e **SQLSetDescField**, **SQLCopyDesc** possono restituire SQLSTATE restituiti da **SQLGetDescField** oppure **SQLSetDescField**.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver non è riuscito ad allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY007|L'istruzione associata non è pronto|*SourceDescHandle* era associato un IRD e l'handle di istruzione associata non è stato nello stato preparato o eseguito.|  
|HY010|Errore nella sequenza della funzione|(DM) il descrittore di gestire in *SourceDescHandle* oppure *TargetDescHandle* è stato associato un *StatementHandle* per il quale un'esecuzione asincrona (not (funzione) Questo file) è stato chiamato ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) il descrittore di handle in *SourceDescHandle* oppure *TargetDescHandle* è stato associato un *StatementHandle* per il quale **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** è stato chiamato e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.<br /><br /> (DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *SourceDescHandle* oppure *TargetDescHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLCopyDesc** funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per uno degli handle di istruzione associati il *SourceDescHandle* oppure *TargetDescHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY016|Non è possibile modificare un descrittore delle righe di implementazione|*TargetDescHandle* era associato a un'implementazione.|  
|HY021|Informazioni descrittore incoerenti.|Le informazioni del descrittore controllate durante una verifica coerenza non erano coerente. Per altre informazioni, vedere "Le verifiche coerenza" nella **SQLSetDescField**.|  
|HY092|Identificatore di attributo/opzione non è valido|La chiamata a **SQLCopyDesc** richiesto una chiamata a **SQLSetDescField**, ma  *\*ValuePtr* non è valido per il *FieldIdentifier* argomenti sul *TargetDescHandle*.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *SourceDescHandle* oppure *TargetDescHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Una chiamata a **SQLCopyDesc** copie di gestire i campi del descrittore di origine per l'handle descrittore di destinazione. I campi possono essere copiati solo a un descrittore applicazione o un IPD, ma non a un'implementazione. I campi possono essere copiati da un'applicazione o un descrittore di implementazione.  
  
 I campi possono essere copiati da un'implementazione solo se l'handle di istruzione è nello stato preparato o eseguito; in caso contrario, la funzione restituisce SQLSTATE hy007 il (istruzione associata non è pronto).  
  
 I campi possono essere copiati da un IPD se è stata preparata un'istruzione. Se è stata preparata un'istruzione SQL con parametri dinamici e il popolamento automatico dell'IPD è supportato e abilitato, IPD viene popolato dal driver. Quando **SQLCopyDesc** viene chiamato con IPD come le *SourceDescHandle*, vengono copiati i campi popolati. Se il IPD non viene popolata dal driver, viene copiato il contenuto dei campi originariamente in IPD.  
  
 Tutti i campi del descrittore, tranne SQL_DESC_ALLOC_TYPE (che specifica se l'handle descrittore è stata allocata in modo esplicito o automaticamente), vengono copiati, se il campo viene definito per il descrittore di destinazione. Campi copiati sovrascrivono i campi esistenti.  
  
 Il driver consente di copiare tutti i campi del descrittore se la *SourceDescHandle* e *TargetDescHandle* argomenti associati con il driver stesso, anche se i driver sono in due diverse connessioni o ambienti. Se il *SourceDescHandle* e *TargetDescHandle* argomenti sono associati a diversi driver, gestione Driver copia i campi definite da ODBC, ma non consente di copiare i campi definiti dal driver o campi che non sono definite da ODBC per il tipo di descrittore.  
  
 La chiamata a **SQLCopyDesc** viene interrotta immediatamente se si verifica un errore.  
  
 Quando il campo SQL_DESC_DATA_PTR viene copiato, viene eseguita una verifica coerenza per il descrittore di destinazione. Se la verifica coerenza ha esito negativo, HY021 SQLSTATE restituiti (informazioni sul descrittore inconsistenti) e la chiamata a **SQLCopyDesc** viene interrotta immediatamente. Per altre informazioni sui controlli di coerenza, vedere "Le verifiche coerenza" nella [funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 Handle descrittore possono essere copiati tra le connessioni anche se le connessioni sono in ambienti diversi. Se Gestione Driver rileva che l'origine e il descrittore di destinazione gli handle non appartengono alla stessa connessione e le due connessioni appartengono per separare i driver, implementa **SQLCopyDesc** mediante l'esecuzione di un campo per campo copiare usando **SQLGetDescField** e **SQLSetDescField**.  
  
 Quando **SQLCopyDesc** viene chiamato con un *SourceDescHandle* sul driver in una e una *TargetDescHandle* sul driver in un'altra, nella coda degli errori del  *SourceDescHandle* viene cancellato. Ciò si verifica perché **SQLCopyDesc** in questo caso viene implementato da chiamate agli **SQLGetDescField** e **SQLSetDescField**.  
  
> [!NOTE]  
>  Un'applicazione potrebbe essere in grado di associare un handle di descrittore allocato in modo esplicito con una *StatementHandle*, anziché chiamare il metodo **SQLCopyDesc** per copiare i campi da un descrittore a un altro. Un descrittore allocato in modo esplicito può essere associato a un altro *StatementHandle* sullo stesso *ConnectionHandle* impostando l'istruzione SQL_ATTR_APP_ROW_DESC o SQL_ATTR_APP_PARAM_DESC attributo per l'handle di descrittore allocato in modo esplicito. Quando ciò avviene **SQLCopyDesc** non deve essere chiamato per copiare i valori dei campi del descrittore da un descrittore a altro. Un handle di descrittore non può essere associato a un *StatementHandle* in un'altra *ConnectionHandle*, tuttavia, usare gli stessi valori di campo del descrittore nel *StatementHandles*in diverse *ConnectionHandles*, **SQLCopyDesc** deve essere chiamata.  
  
 Per una descrizione dei campi in un'intestazione di descrittore o record, vedere [funzione SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Per altre informazioni su descrittori, vedere [descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="copying-rows-between-tables"></a>Copia delle righe tra le tabelle  
 Un'applicazione può copiare dati da una tabella a altra senza copiare i dati a livello di applicazione. A tale scopo, l'applicazione associa il buffer di dati stesso e le informazioni sul descrittore a un'istruzione che recupera i dati e sull'istruzione che inserisce i dati in una copia. A tale scopo a condividendo un descrittore applicazione (associazione di un descrittore allocato in modo esplicito come il ARD a una sola istruzione sia APD in un altro) o utilizzando **SQLCopyDesc** per copiare le associazioni tra il ARD e APD delle due istruzioni. Se si trovano in diverse connessioni, le istruzioni **SQLCopyDesc** deve essere utilizzato. È inoltre **SQLCopyDesc** deve essere chiamata per copiare le associazioni tra il IRD e IPD delle due istruzioni. Durante la copia tra le istruzioni sulla stessa connessione, il tipo di informazioni SQL_ACTIVE_STATEMENTS restituiti dal driver per una chiamata a **SQLGetInfo** deve essere maggiore di 1 per eseguire questa operazione. (Non il case durante la copia tra le connessioni.)  
  
### <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, descrittore operazioni vengono utilizzate per copiare i campi della tabella PartsSource nella tabella di PartsCopy. Il contenuto della tabella PartsSource venga recuperato nel buffer di righe nel *hstmt0*. Questi valori vengono usati come parametri di un'istruzione INSERT su *hstmt1* per popolare le colonne della tabella PartsCopy. A tale scopo, i campi di implementazione di *hstmt0* vengono copiati i campi dell'IPD dei *hstmt1*e i campi del ARD dei *hstmt0* vengono copiati i campi di APD di *hstmt1*. Uso **SQLSetDescField** su cui impostare SQL_DESC_PARAMETER_TYPE attributo dell'IPD SQL_PARAM_INPUT quando si copiano i campi IRD da un'istruzione con parametri di output per i campi IPD che devono essere parametri di input.  
  
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
|Recupero di più campi di descrizione|[Funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Impostazione di un campo del descrittore single|[Funzione SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|L'impostazione di più campi di descrizione|[Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
