---
title: Funzione SQLGetFunctions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetFunctions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetFunctions
helpviewer_keywords:
- SQLGetFunctions function [ODBC]
ms.assetid: 0451d2f9-0f4f-46ba-b252-670956a52183
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86f888955e6188cd7f90e54f39eeef3723dcfbe8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897722"
---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions Function
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLGetFunctions** restituisce informazioni sul fatto che un driver supporta la funzione ODBC specifica. Questa funzione è implementata in Gestione Driver. può inoltre essere implementata nel driver. Se un driver implementa **SQLGetFunctions**, gestione Driver chiama la funzione nel driver. In caso contrario, esegue la funzione stessa.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *ConnectionHandle*  
 [Input] Handle di connessione.  
  
 *FunctionId*  
 [Input] Oggetto **#define** valore che identifica la funzione ODBC di interesse; **SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS**. **SQL_API_ODBC3_ALL_FUNCTIONS** viene usato da un'applicazione ODBC 3 *. x* dell'applicazione per determinare il supporto di ODBC 3*x* e le funzioni precedenti. **SQL_API_ALL_FUNCTIONS** viene usato da un'API ODBC 2 *. x* dell'applicazione per determinare il supporto di ODBC 2*x* e le funzioni precedenti.  
  
 Per un elenco degli **#define** valori che identificano le funzioni ODBC, vedere le tabelle in "Commenti".  
  
 *SupportedPtr*  
 [Output]  Se *FunctionId* identifica una funzione ODBC singola *SupportedPtr* punta a un singolo SQLUSMALLINT valore SQL_TRUE se la funzione specificata è supportata dal driver e SQL_FALSE se non è è supportato.  
  
 Se *FunctionId* SQL_API_ODBC3_ALL_FUNCTIONS, viene *SupportedPtr* punta a una matrice SQLSMALLINT con un numero di elementi uguali a SQL_API_ODBC3_ALL_FUNCTIONS_SIZE. Questa matrice viene considerata da Gestione Driver come bitmap che può essere utilizzata per determinare se un'applicazione ODBC 3 bit 4.000*x* o funzione earlier è supportato. La macro SQL_FUNC_EXISTS viene chiamata per determinare il supporto di funzione. (Vedere "Commenti".) Un'applicazione ODBC 3 *. x* applicazione può chiamare **SQLGetFunctions** con SQL_API_ODBC3_ALL_FUNCTIONS su entrambi un'applicazione ODBC 3*x* o ODBC 2*x* autista.  
  
 Se *FunctionId* SQL_API_ALL_FUNCTIONS, viene *SupportedPtr* punta a una matrice SQLUSMALLINT di 100 elementi. La matrice è indicizzata dai **#define** i valori utilizzati dalla *FunctionId* per identificare ogni funzione ODBC; alcuni elementi della matrice sono riservate per usi futuri e inutilizzate. Un elemento è SQL_TRUE se identifica un'ODBC 2*x* o funzione earlier supportate dal driver. Se identifica una funzione ODBC non supportata dal driver o non identifica una funzione ODBC è SQL_FALSE.  
  
 Le matrici restituite **SupportedPtr* usano l'indicizzazione in base zero.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetFunctions** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_DBC e un *gestiscono* dei *ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetFunctions** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------|-----|-----------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) **SQLGetFunctions** è stato chiamato prima **SQLConnect**, **SQLBrowseConnect**, oppure **SQLDriverConnect**.<br /><br /> (DM) **SQLBrowseConnect** è stato chiamato per il *ConnectionHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima **SQLBrowseConnect** restituito SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *ConnectionHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY095|Tipo di funzione non compreso nell'intervallo|(DM) non valido *FunctionId* valore specificato.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
  
## <a name="comments"></a>Commenti  
 **SQLGetFunctions** restituisce sempre che **SQLGetFunctions**, **SQLDataSources**, e **SQLDrivers** sono supportati. Ciò avviene perché queste funzioni vengono implementate in Gestione Driver. Gestione Driver assocerà una funzione ANSI per la funzione Unicode corrispondente se la funzione Unicode esiste e verrà eseguito il mapping una funzione Unicode per la funzione ANSI corrispondente se esiste la funzione ANSI. Per informazioni su come usano le applicazioni **SQLGetFunctions**, vedere [livelli di conformità di interfaccia](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 Di seguito è riportato un elenco di valori validi per *FunctionId* per le funzioni conformi a livello di conformità agli standard ISO 92:  
  
|FunctionId valore|FunctionId valore|  
|----------|----------|  
|SQL_API_SQLALLOCHANDLE|SQL_API_SQLGETDESCFIELD|  
|SQL_API_SQLBINDCOL|SQL_API_SQLGETDESCREC|  
|SQL_API_SQLCANCEL|SQL_API_SQLGETDIAGFIELD|  
|SQL_API_SQLCLOSECURSOR|SQL_API_SQLGETDIAGREC|  
|SQL_API_SQLCOLATTRIBUTE|SQL_API_SQLGETENVATTR|  
|SQL_API_SQLCONNECT|SQL_API_SQLGETFUNCTIONS|  
|SQL_API_SQLCOPYDESC|SQL_API_SQLGETINFO|  
|SQL_API_SQLDATASOURCES|SQL_API_SQLGETSTMTATTR|  
|SQL_API_SQLDESCRIBECOL|SQL_API_SQLGETTYPEINFO|  
|SQL_API_SQLDISCONNECT|SQL_API_SQLNUMRESULTCOLS|  
|SQL_API_SQLDRIVERS|SQL_API_SQLPARAMDATA|  
|SQL_API_SQLENDTRAN|SQL_API_SQLPREPARE|  
|SQL_API_SQLEXECDIRECT|SQL_API_SQLPUTDATA|  
|SQL_API_SQLEXECUTE|SQL_API_SQLROWCOUNT|  
|SQL_API_SQLFETCH|SQL_API_SQLSETCONNECTATTR|  
|SQL_API_SQLFETCHSCROLL|SQL_API_SQLSETCURSORNAME|  
|SQL_API_SQLFREEHANDLE|SQL_API_SQLSETDESCFIELD|  
|SQL_API_SQLFREESTMT|SQL_API_SQLSETDESCREC|  
|SQL_API_SQLGETCONNECTATTR|SQL_API_SQLSETENVATTR|  
|SQL_API_SQLGETCURSORNAME|SQL_API_SQLSETSTMTATTR|  
|SQL_API_SQLGETDATA| |  
  
 Di seguito è riportato un elenco di valori validi per *FunctionId* per le funzioni conformi al livello di conformità agli standard Open Group:  
  
|FunctionId valore|FunctionId valore|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 Di seguito è riportato un elenco di valori validi per *FunctionId* per le funzioni conformi a livello di conformità agli standard di ODBC.  
  
|FunctionId valore|FunctionId valore|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS[1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] quando si lavora con un 2 ODBC *. x* driver **SQLBulkOperations** verranno restituiti come supportato solo se entrambe le operazioni seguenti sono vere: ODBC 2 *. x* driver supporta  **SQLSetPos**, e il tipo di informazioni SQL_POS_OPERATIONS restituisce il bit SQL_POS_ADD come set.  
  
 Di seguito è riportato un elenco di valori validi per *FunctionId* per le funzioni introdotte in ODBC 3.8 o versioni successive:  
  
|FunctionId valore|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle** verranno restituiti come supportato solo se il driver supporta entrambi **SQLCancel** e **SQLCancelHandle**. Se **SQLCancel** è supportata ma **SQLCancelHandle** non lo è, l'applicazione potrà ancora chiamare **SQLCancelHandle** su un handle di istruzione, perché ne verrà eseguito il mapping a  **SQLCancel**.  
  
## <a name="sqlfuncexists-macro"></a>SQL_FUNC_EXISTS (macro)  
 Il SQL_FUNC_EXISTS (*SupportedPtr*, *FunctionID*) macro viene usata per determinare il supporto di ODBC 3*x* o le funzioni precedenti dopo **SQLGetFunctions**  è stato chiamato con un *FunctionId* argomento di SQL_API_ODBC3_ALL_FUNCTIONS. L'applicazione chiama SQL_FUNC_EXISTS con il *SupportedPtr* argomento impostato sulle *SupportedPtr* passato *SQLGetFunctions*e con il  *FunctionID* argomento impostato il **#define** per la funzione. SQL_FUNC_EXISTS restituisce SQL_TRUE se la funzione è supportata e SQL_FALSE in caso contrario.  
  
> [!NOTE]
>  Quando si lavora con un 2 ODBC *. x* driver ODBC 3 *. x* restituisce SQL_TRUE per gestione Driver **SQLAllocHandle** e **SQLFreeHandle**perché **SQLAllocHandle** viene eseguito il mapping a **SQLAllocEnv**, **SQLAllocConnect**, o **SQLAllocStmt**, e in quanto **SQLFreeHandle** viene eseguito il mapping al **SQLFreeEnv**, **SQLFreeConnect**, oppure **SQLFreeStmt**. **SQLAllocHandle** oppure **SQLFreeHandle** con un *HandleType* argomento di SQL_HANDLE_DESC non è supportato, tuttavia, anche se SQL_TRUE viene restituito per le funzioni, perché non esiste alcun ODBC 2*x* funzione per eseguire il mapping in questo caso.  
  
## <a name="code-example"></a>Esempio di codice  
 I tre esempi seguenti mostrano come un'applicazione usa **SQLGetFunctions** per determinare se un driver supporta **SQLTables**, **SQLColumns**, e  **SQLStatistics**. Se il driver non supporta queste funzioni, l'applicazione si disconnette dal driver. Il primo esempio viene chiamato **SQLGetFunctions** una volta per ogni funzione.  
  
```cpp  
SQLUSMALLINT TablesExists, ColumnsExists, StatisticsExists;  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
  
retcodeTables = SQLGetFunctions(hdbc, SQL_API_SQLTABLES, &TablesExists);  
retcodeColumns = SQLGetFunctions(hdbc, SQL_API_SQLCOLUMNS, &ColumnsExists);  
retcodeStatistics = SQLGetFunctions(hdbc, SQL_API_SQLSTATISTICS, &StatisticsExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (retcodeTables == SQL_SUCCESS && TablesExists == SQL_TRUE &&   
retcodeColumns == SQL_SUCCESS && ColumnsExists == SQL_TRUE &&   
retcodeStatistics == SQL_SUCCESS && StatisticsExists == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 Nel secondo esempio, chiama un'applicazione di ODBC 3.x **SQLGetFunctions** e lo passa una matrice in cui **SQLGetFunctions** restituisce informazioni su tutti i ODBC 3.x e le funzioni precedenti.  
  
```cpp  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[SQL_API_ODBC3_ALL_FUNCTIONS_SIZE];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ODBC3_ALL_FUNCTIONS, fExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (reccode == SQL_SUCCESS &&   
SQL_FUNC_EXISTS(fExists, SQL_API_SQLTABLES) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLCOLUMNS) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLSTATISTICS) == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 Il terzo esempio è un'applicazione ODBC 2.x chiama **SQLGetFunctions** e lo passa una matrice di 100 elementi in cui **SQLGetFunctions** restituisce informazioni su tutti i ODBC 2.x e le funzioni precedenti.  
  
```cpp  
#define FUNCTIONS 100  
  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[FUNCTIONS];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ALL_FUNCTIONS, fExists);  
  
/* SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver. */  
if (retcode == SQL_SUCCESS &&   
fExists[SQL_API_SQLTABLES] == SQL_TRUE &&  
   fExists[SQL_API_SQLCOLUMNS] == SQL_TRUE &&  
   fExists[SQL_API_SQLSTATISTICS] == SQL_TRUE)   
{  
  
   /* Continue with application */  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituisce l'impostazione di un attributo di connessione|[Funzione SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Restituzione di informazioni su un'origine dati o driver|[Funzione SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Restituisce l'impostazione di un attributo di istruzione|[Funzione SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
