---
title: Funzione SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLParamData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLParamData
helpviewer_keywords:
- SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0d92abe17128bff382d4b291fa9d20fe5c4fa77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536634"
---
# <a name="sqlparamdata-function"></a>Funzione SQLParamData
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLParamData** viene usata in combinazione con **SQLPutData** per specificare i dati di parametro in fase di esecuzione di istruzione e con **SQLGetData** per recuperare i dati dei parametri di output inviati come flusso.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *ValuePtrPtr*  
 [Output] Puntatore a un buffer in cui restituire l'indirizzo del *ParameterValuePtr* specificato nel buffer **SQLBindParameter** (per i dati dei parametri) o l'indirizzo del *TargetValuePtr* specificato nel buffer **SQLBindCol** (per dati di colonna), quanto contenuto nel campo del record del descrittore SQL_DESC_DATA_PTR.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE, or SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLParamData** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLParamData** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07006|Violazione dell'attributo del tipo di dati|Il valore di dati identificato dal *ValueType* argomento nella **SQLBindParameter** per non è stato possibile convertire il parametro associato al tipo di dati identificato dal *ParameterType*nell'argomento **SQLBindParameter**.<br /><br /> Il valore di dati restituito per un parametro di associazione come SQL_PARAM_OUTPUT o SQL_PARAM_INPUT_OUTPUT non è stato possibile convertire il tipo di dati identificato dal *ValueType* nell'argomento **SQLBindParameter**.<br /><br /> (Se non è stato possibile convertire i valori dei dati per una o più righe, ma una o più righe sono state restituite correttamente, questa funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|22026|Lunghezza dei dati non corrispondente.|Il tipo di informazioni SQL_NEED_LONG_DATA_LEN nel **SQLGetInfo** è "Y", e meno dati è stati inviati per un parametro long (tipo di dati era SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo di dati specifici dell'origine dati di tipo long) superiore a quello specificato con il *StrLen_or_IndPtr* nell'argomento **SQLBindParameter**.<br /><br /> Il tipo di informazioni SQL_NEED_LONG_DATA_LEN nel **SQLGetInfo** è "Y", e meno dati è stati inviati per una colonna long (tipo di dati era SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo di dati specifici dell'origine dati di tipo long) rispetto a quello indicato di corrispondente a una colonna in una riga di dati che è stato aggiunto o aggiornati con buffer di lunghezza **SQLBulkOperations** o aggiornate con **SQLSetPos**.|  
|40001|Errore di serializzazione.|Il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver non è riuscito ad allocare memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. È stata chiamata la funzione e prima esecuzione, completata **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle*; quindi la funzione è stata chiamata nuovamente in il *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) la chiamata di funzione precedente non era una chiamata a **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, oppure **SQLSetPos** in cui il restituire codice era SQL_NEED_DATA o la chiamata di funzione precedente è stata una chiamata a **SQLPutData**.<br /><br /> La chiamata di funzione precedente è stata una chiamata a **SQLParamData**.<br /><br /> (DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLParamData** funzione è stata chiamata.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il *StatementHandle* e restituito SQL_NEED_DATA. **SQLCancel** è stato chiamato prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|(DM) il driver corrispondente per il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
 Se **SQLParamData** viene chiamato durante l'invio di dati per un parametro in un'istruzione SQL, può restituire qualsiasi valore SQLSTATE che può essere restituiti dalla funzione chiamata per eseguire l'istruzione (**SQLExecute** o**SQLExecDirect**). Se viene chiamato durante l'invio di dati per una colonna aggiornati o aggiunti con **SQLBulkOperations** o che venga aggiornato con **SQLSetPos**, può restituire qualsiasi valore SQLSTATE che può essere restituiti da  **SQLBulkOperations** oppure **SQLSetPos**.  
  
## <a name="comments"></a>Commenti  
 **SQLParamData** può essere chiamato per fornire i dati di data-at-execution per due usi: dati di parametro che verranno usati in una chiamata a **SQLExecute** oppure **SQLExecDirect**, o dati della colonna che verrà usata quando una riga viene aggiornata o aggiunto da una chiamata a **SQLBulkOperations** o aggiornato da una chiamata a **SQLSetPos**. In fase di esecuzione **SQLParamData** restituisce all'applicazione un indicatore di dati che il driver richiede.  
  
 Quando un'applicazione chiama **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos**, il driver restituisce SQL_NEED_ DATI se necessita di dati data-at-execution. Un'applicazione chiama quindi **SQLParamData** per determinare i dati da inviare. Se il driver richiede dati di parametro, il driver restituisce il  *\*ValuePtrPtr* output il valore che l'applicazione inserita nel buffer di set di righe del buffer. L'applicazione può usare questo valore per determinare a quali dati di parametro, il driver richiede. Se il driver richiede dati della colonna, il driver restituisce il  *\*ValuePtrPtr* memorizzare nel buffer l'indirizzo a cui la colonna era associata in origine, come indicato di seguito:  
  
 *Indirizzo associato* + *associazione Offset* + ((*il numero di riga* - 1) x *dimensione dell'elemento*)  
  
 le variabili in cui vengono definite come indicato nella tabella seguente.  
  
|Variabile|Descrizione|  
|--------------|-----------------|  
|*Associare l'indirizzo*|L'indirizzo specificato con il *TargetValuePtr* nell'argomento **SQLBindCol**.|  
|*Offset di associazione*|Il valore archiviato in corrispondenza dell'indirizzo specificato con l'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR.|  
|*Numero di riga*|Il numero di riga nel set di righe in base 1. Per operazioni di recupero riga singola, ovvero l'impostazione predefinita, questo è 1.|  
|*Dimensione dell'elemento*|Il valore dell'attributo dell'istruzione SQL_ATTR_ROW_BIND_TYPE i buffer di dati e lunghezza/indicatore.|  
  
 Anche restituito SQL_NEED_DATA, che è un indicatore per l'applicazione che deve chiamare **SQLPutData** per inviare i dati.  
  
 L'applicazione chiama **SQLPutData** tutte le volte in base alle esigenze per inviare i dati di data-at-execution per la colonna o parametro. Dopo l'invio di tutti i dati per la colonna o parametro, l'applicazione chiama **SQLParamData** nuovamente. Se **SQLParamData** anche in questo caso viene restituito SQL_NEED_DATA, i dati devono essere inviati per un altro parametro o della colonna. Pertanto, anche in questo caso l'applicazione chiama **SQLPutData**. Se tutti i dati di data-at-execution è stato inviato per tutti i parametri o colonne, quindi **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, il valore nella  *\*ValuePtrPtr* è definito, e può essere eseguita l'istruzione SQL o il **SQLBulkOperations** oppure **SQLSetPos** chiamata può essere elaborata.  
  
 Se **SQLParamData** fornisce i dati di parametro per una ricerca istruzione update o delete che non influiscono su tutte le righe nell'origine dati, la chiamata a **SQLParamData** restituisce SQL_NO_DATA.  
  
 Per altre informazioni sui dati di parametro come data-at-execution sono passate in fase di esecuzione di istruzione, vedere "Passaggio di valori di parametro" nella [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [l'invio di dati Long](../../../odbc/reference/develop-app/sending-long-data.md). Per altre informazioni sui dati della colonna come data-at-execution sono state aggiornate o aggiunto, vedere la sezione "Uso SQLSetPos" nella [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Esecuzione di operazioni Bulk aggiornamenti mediante segnalibri" in [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), e [dati di tipo Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
 **SQLParamData** può essere chiamato per recuperare i parametri di output inviati come flusso. Quando **SQLMoreResults**, **SQLExecute**, **SQLGetData**, oppure **SQLExecDirect** restituisce SQL_PARAM_DATA_AVAILABLE, chiama **SQLParamData** per determinare quale parametro ha un valore disponibile. Per altre informazioni sui parametri di output inviati come flusso e SQL_PARAM_DATA_AVAILABLE, vedere [recupero di parametri di Output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Visualizzare [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a un parametro|[Funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di informazioni su un parametro in un'istruzione|[Funzione SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Esecuzione di un'istruzione SQL|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|L'invio dei dati di parametro in fase di esecuzione|[Funzione SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recupero di parametri di output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
