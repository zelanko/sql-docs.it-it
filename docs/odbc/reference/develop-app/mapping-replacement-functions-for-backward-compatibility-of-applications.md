---
title: Mapping di funzioni di sostituzione per la compatibilità delle applicazioni - ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping replacement functions [ODBC]
- upgrading applications [ODBC], mapping replacement functions
- compatibility [ODBC], mapping replacement functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], mapping replacement functions
- application upgrades [ODBC], mapping replacement functions
- backward compatibility [ODBC], mapping replacement functions
ms.assetid: f5e6d9da-76ef-42cb-b3f5-f640857df732
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45cec32e818eab1ec5586196eadef998b8f988ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036395"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>Mapping di funzioni di sostituzione per la compatibilità con le versioni precedenti delle applicazioni
Un database ODBC *3.x* applicazione funziona tramite ODBC *3.x* gestione Driver funzionerà con un database ODBC *2.x* driver fino a quando non nuove funzionalità vengono usati. Entrambi duplicati funzionalità e modifiche del comportamento, tuttavia, hanno effetto che ODBC *3.x* funzionamento dell'applicazione in un database ODBC *2.x* driver. Quando si lavora con un database ODBC *2.x* driver, gestione Driver ODBC seguenti esegue il mapping *3.x* funzioni, che sono sostituiti ODBC uno o più *2.x* funzioni, nel ODBC corrispondente *2.x* funzioni.  
  
|ODBC *3.x* (funzione)|ODBC *2.x* (funzione)|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**, **SQLAllocConnect**, o **SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**, **SQLFreeConnect**, o **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] altre azioni potrebbero anche essere eseguite, a seconda dell'attributo richiesto.  
  
## <a name="sqlallochandle"></a>Funzione SQLAllocHandle  
 Gestione Driver esegue il mapping a **SQLAllocEnv**, **SQLAllocConnect**, o **SQLAllocStmt**, nel modo appropriato. La chiamata seguente a **SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 verrà generato in Gestione Driver eseguire le operazioni seguenti (concettuale, nessun controllo degli errori) mapping:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 Gestione Driver esegue il mapping a **SQLSetPos**. La chiamata seguente a **SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 comporterà la sequenza di passaggi seguente:  
  
1.  Se l'argomento dell'operazione corrisponde SQL_ADD, the Driver Manager chiamerà **SQLSetPos** come indicato di seguito:  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  Se l'argomento dell'operazione non è SQL_ADD, il driver restituisce SQLSTATE HY092 (identificatore di attributo/opzione non valida).  
  
3.  Se l'applicazione tenta di modificare il SQL_ATTR_ROW_STATUS_PTR tra le chiamate a **SQLFetch** oppure **SQLFetchScroll** e **SQLBulkOperations**, gestione Driver verrà Restituisce SQLSTATE HY011 (attributo non può essere impostato a questo punto).  
  
4.  Se l'argomento dell'operazione è SQL_ADD, l'applicazione deve chiamare **SQLBindCol** per associare i dati da inserire. Non può chiamare **SQLSetDescField** oppure **SQLSetDescRec** per associare i dati da inserire.  
  
5.  Se l'argomento dell'operazione è SQL_ADD e il numero di righe da inserire non è quello utilizzato per le dimensioni del set di righe correnti **SQLSetStmtAttr** deve essere chiamato per impostare l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe da inserito prima di chiamare **SQLBulkOperations**. Per ripristinare le dimensioni del set di righe precedente, l'applicazione deve impostare l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE prima **SQLFetch**, **SQLFetchScroll**, o **SQLSetPos**viene chiamato.  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 Gestione Driver esegue il mapping a **SQLColAttributes**. La chiamata seguente a **SQLColAttribute**:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 comporterà la sequenza di passaggi seguente:  
  
1.  Se *FieldIdentifier* è uno dei seguenti:  
  
     SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH, SQL_DESC_OCTET_LENGTH, SQL_DESC_UNNAMED, SQL_DESC_BASE_COLUMN_NAME, SQL_DESC_LITERAL_PREFIX, SQL_DESC_LITERAL_SUFFIX, or SQL_DESC_LOCAL_TYPE_NAME  
  
     Gestione Driver restituisce SQL_ERROR con SQLSTATE HY091 (identificatore del campo del descrittore non valido). Si applica alcuna regola ulteriormente in questa sezione.  
  
2.  Gestione Driver viene eseguito il mapping SQL_COLUMN_COUNT, SQL_COLUMN_NAME o SQL_COLUMN_NULLABLE SQL_DESC_COUNT, SQL_DESC_NAME o SQL_DESC_NULLABLE, rispettivamente. (Un database ODBC *2.x* driver devono solo supportare SQL_COLUMN_COUNT, SQL_COLUMN_NAME e SQL_COLUMN_NULLABLE, non SQL_DESC_COUNT, SQL_DESC_NAME e SQL_DESC_NULLABLE.) La chiamata a SQLColAttribute è mappata a:  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  Tutti gli altri *FieldIdentifier* valori vengono passati al driver, con **SQLColAttribute** mappato al **SQLColAttributes** come illustrato in precedenza.  
  
4.  Se *BufferLength* è minore di 0, la gestione Driver restituisce SQL_ERROR con SQLSTATE HY090 (stringa di lunghezza o non valida del buffer). Si applica alcuna regola ulteriormente in questa sezione.  
  
5.  Se *FieldIdentifier* è SQL_DESC_CONCISE_TYPE e il tipo restituito è un tipo di dati datetime conciso, le mappe di gestione Driver la restituzione di valori per i codici di date, time e timestamp.  
  
6.  Gestione Driver esegue i controlli necessari per verificare se SQLSTATE HY010 (errore di sequenza di funzioni) deve essere generato. Se, pertanto, gestione Driver restituisce SQL_ERROR e SQLSTATE HY010 (funzione di errore nella sequenza). Si applica alcuna regola ulteriormente in questa sezione.  
  
## <a name="sqlendtran"></a>SQLEndTran  
 Gestione Driver esegue il mapping a **SQLTransact**. La chiamata seguente a **SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 verrà generato in Gestione Driver eseguire le operazioni seguenti (concettuale, nessun controllo degli errori) mapping:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 Gestione Driver esegue il mapping a **SQLExtendedFetch** con un *FetchOrientation* argomento di SQL_FETCH_NEXT. La chiamata seguente a **SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 comporterà la chiamata di gestione Driver **SQLExtendedFetch**, come indicato di seguito:  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 In questa chiamata, il *pcRow* argomento è impostato su quello che l'applicazione imposta l'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR affinché tramite una chiamata a **SQLSetStmtAttr**.  
  
> [!NOTE]  
>  Quando l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROW_STATUS_PTR affinché punti a una matrice di stato, gestione Driver memorizza nella cache il puntatore del mouse. *RowStatusArray* può essere uguale a un puntatore null.  
  
 Se il driver non supporta **SQLExtendedFetch** e viene caricata la libreria di cursori, gestione Driver Usa la libreria di cursori **SQLExtendedFetch** per eseguire il mapping **SQLFetch** a **SQLExtendedFetch**. Se il driver non supporta **SQLExtendedFetch** e la libreria di cursori non è caricata, gestione Driver passa la chiamata a **SQLFetch** tramite il driver. Se l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROW_STATUS_PTR, gestione Driver garantisce che la matrice viene popolata. Se l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROWS_FETCHED_PTR, gestione Driver questo campo impostato su 1.  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 Gestione Driver esegue il mapping a **SQLExtendedFetch**. La chiamata seguente a **SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 comporterà la sequenza di passaggi seguente:  
  
1.  Quando l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROW_STATUS_PTR (che imposta il campo SQL_DESC_ARRAY_STATUS_PTR nell'implementazione) in modo che punti a una matrice di stato, gestione Driver memorizza nella cache puntatore ' this '. Si supponga che sia questo puntatore *RowStatusArray*; in caso contrario, let *RowStatusArray* essere uguale a un puntatore null. Se il *RowStatusArray* argomento è impostato su un puntatore null, gestione Driver genera una matrice di stato delle righe.  
  
2.  Se *FetchOrientation* non fa parte di SQL_FETCH_NEXT, SQL_FETCH_PRIOR, SQL_FETCH_ABSOLUTE, SQL_FETCH_RELATIVE, SQL_FETCH_FIRST, SQL_FETCH_LAST o impostato su SQL_FETCH_BOOKMARK, gestione Driver restituisce SQL_ERROR con SQLSTATE HY106 (tipo compreso nell'intervallo di recupero). Si applica alcuna regola ulteriormente in questa sezione.  
  
3.  Caso:  
  
-   Se *FetchOrientation* è uguale a SQL_FETCH_BOOKMARK, quindi:  
  
    -   Se **SQLSetStmtAttr** è stato chiamato in precedenza per impostare il valore di SQL_ATTR_FETCH_BOOKMARK_PTR, quindi consentire *Bmk* essere il valore ottenuto da dereferenziazione del puntatore SQL_DESC_FETCH_BOOKMARK_PTR.  
  
    -   In caso contrario, restituirà SQL_ERROR con SQLSTATE HY111 (valore di segnalibro non valido). Si applica alcuna regola ulteriormente in questa sezione.  
  
     Chiama gestione Driver **SQLExtendedFetch**, come indicato di seguito:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   In caso contrario, viene chiamato gestione Driver **SQLExtendedFetch**, come indicato di seguito:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     Queste chiamate, il *pcRow* argomento è impostato su quello che l'applicazione imposta l'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR affinché tramite una chiamata a **SQLSetStmtAttr**.  
  
-   SQL_ATTR_ROW_ARRAY_SIZE è mappata a SQL_ROWSET_SIZE.  
  
-   Se *rc* è diverso da SQL_SUCCESS o SQL_SUCCESS_WITH_INFO e, se *FetchOrientation* è uguale a SQL_FETCH_BOOKMARK e *FetchOffset* è diverso da 0, quindi il Driver Manager registra un avviso, il valore SQLSTATE 01S10 (tenta di recuperare da un offset di segnalibro, offset valore ignorato,) e viene restituito SQL_SUCCESS_WITH_INFO.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 Gestione Driver esegue il mapping a **SQLFreeEnv**, **SQLFreeConnect**, o **SQLFreeStmt** come appropriato. La chiamata seguente a **SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 verrà generato in Gestione Driver eseguire le operazioni seguenti (concettuale, nessun controllo degli errori) mapping:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 Gestione Driver esegue il mapping a **SQLGetConnectOption**. La chiamata seguente a **SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 comporterà la sequenza di passaggi seguente:  
  
1.  Se *attributo* non è un attributo di istruzione o di connessione definiti dal driver e non è un attributo definito in ODBC *2.x*, gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (attributo non valido / Identificatore di opzione). Si applica alcuna regola ulteriormente in questa sezione.  
  
2.  Se *attributo* è uguale a SQL_ATTR_AUTO_IPD o SQL_ATTR_METADATA_ID, la gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (identificatore di attributo/opzione non valida).  
  
3.  Il Driver di gestione esegue i controlli necessari per verificare se SQLSTATE 08003 (connessione non aperta) o SQLSTATE HY010 (errore di sequenza di funzioni) deve essere generato. In questo caso, gestione Driver restituisce SQL_ERROR e viene inviato il messaggio di errore appropriato. Si applica alcuna regola ulteriormente in questa sezione.  
  
4.  Le chiamate di gestione Driver **SQLGetConnectOption** come indicato di seguito:  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     Si noti che il *BufferLength* e *StringLengthPtr* vengono ignorati.  
  
## <a name="sqlgetdata"></a>SQLGetData  
 Quando un'applicazione ODBC *3.x* funziona con un database ODBC *2.x* driver chiama **SQLGetData** con il *ColumnNumber* argomento uguale a 0, il ODBC *3.x* Driver Manager esegue il mapping a una chiamata a **SQLGetStmtOption** con il *opzione* attributo impostato su SQL_GET_BOOKMARK.  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 Gestione Driver esegue il mapping a **SQLGetStmtOption**. La chiamata seguente a **SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 comporterà la sequenza di passaggi seguente:  
  
1.  Se *attributo* non è un attributo di istruzione o di connessione definiti dal driver e non è un attributo definito in ODBC *2.x*, gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (attributo non valido / Identificatore di opzione). Si applica alcuna regola ulteriormente in questa sezione.  
  
2.  Se *attributo* è uno dei seguenti:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     Gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (identificatore di attributo/opzione non valida). Si applica alcuna regola ulteriormente in questa sezione.  
  
3.  Gestione Driver esegue i controlli necessari per verificare se SQLSTATE HY010 (errore di sequenza di funzioni) deve essere generato. Se, pertanto, gestione Driver restituisce SQL_ERROR e SQLSTATE HY010 (funzione di errore nella sequenza). Si applica alcuna regola ulteriormente in questa sezione.  
  
4.  Se *attributo* è uguale a SQL_ATTR_ROWS_FETCHED_PTR, gestione Driver restituisce un puntatore alla variabile di gestione Driver interna *linea d'aria*, che è usato o verrà usato in una chiamata a  **SQLExtendedFetch**. Si applica alcuna regola ulteriormente in questa sezione.  
  
5.  Se *attributo* è uguale a SQL_DESC_FETCH_BOOKMARK_PTR, gestione Driver restituisce il puntatore appropriato che è memorizzato nella cache durante una chiamata a **SQLSetStmtAttr**.  
  
6.  Se *attributo* è uguale a vengono impostati SQL_ATTR_ROW_STATUS_PTR, gestione Driver restituisce il puntatore appropriato che è memorizzato nella cache durante una chiamata a **SQLSetStmtAttr**.  
  
7.  Le chiamate di gestione Driver **SQLGetStmtOption** come indicato di seguito:  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     in cui *hstmt*, *fOption*, e *il parametro pvParam* verrà impostato su valori di *StatementHandle*, *attributo*, e *ValuePtr*, rispettivamente. Il *BufferLength* e *StringLengthPtr* vengono ignorati.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 Gestione Driver esegue il mapping a **SQLSetConnectOption**. La chiamata seguente a **SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 comporterà la sequenza di passaggi seguente:  
  
1.  Se *attributo* non è un attributo di istruzione o di connessione definiti dal driver e non è un attributo definito in ODBC *2.x*, gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (attributo non valido / Identificatore di opzione). Si applica alcuna regola ulteriormente in questa sezione.  
  
2.  Se *attributo* è uguale a SQL_ATTR_AUTO_IPD, la gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (identificatore di attributo/opzione non valida).  
  
3.  Gestione Driver esegue i controlli necessari per verificare se SQLSTATE 08003 (connessione non aperta) o SQLSTATE HY010 necessità (errore di sequenza di funzioni) da generare. Se uno di questi errori deve essere generato, gestione Driver restituisce SQL_ERROR e viene inviato il messaggio di errore appropriato. Si applica alcuna regola ulteriormente in questa sezione.  
  
4.  Le chiamate di gestione Driver **SQLSetConnectOption** come indicato di seguito:  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     in cui *hdbc*, *fOption*, e *vParam* verrà impostato su valori di *ConnectionHandle*, *attributo*, e *ValuePtr*, rispettivamente. *StringLengthPtr* viene ignorato.  
  
> [!NOTE]  
>  La possibilità di impostare gli attributi di istruzione per il livello di connessione è stata deprecata. Gli attributi di istruzione non è possibile impostare a livello di connessione da un database ODBC *3.x* dell'applicazione.  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 Gestione Driver esegue il mapping a **SQLSetStmtOption**. La chiamata seguente a **SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 comporterà la sequenza di passaggi seguente:  
  
1.  Se *attributo* non è un attributo di istruzione o di connessione definiti dal driver e non è un attributo definito in ODBC *2.x*, gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (attributo non valido / Identificatore di opzione). Si applica alcuna regola ulteriormente in questa sezione.  
  
2.  Se *attributo* è uno dei seguenti:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     Gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (identificatore di attributo/opzione non valida). Si applica alcuna regola ulteriormente in questa sezione.  
  
3.  Gestione Driver esegue i controlli necessari per verificare se SQLSTATE HY010 necessità (errore di sequenza di funzioni) da generare. Se, pertanto, gestione Driver restituisce SQL_ERROR e SQLSTATE HY010 (funzione di errore nella sequenza). Si applica alcuna regola ulteriormente in questa sezione.  
  
4.  Se *attributo* è uguale a SQL_ATTR_PARAMSET_SIZE oppure SQL_ATTR_PARAMS_PROCESSED_PTR, vedere la sezione "Mapping per la gestione delle matrici di parametri," più avanti in questo argomento. Si applica alcuna regola ulteriormente in questa sezione.  
  
5.  Se *attributo* è uguale a SQL_ATTR_ROWS_FETCHED_PTR, il puntatore di valore per usarlo con le cache di gestione Driver **SQLFetchScroll**.  
  
6.  Se *attributo* è uguale a vengono impostati SQL_ATTR_ROW_STATUS_PTR, il puntatore di valore per usarlo con le cache di gestione Driver **SQLFetchScroll** oppure **SQLSetPos**. Si applica alcuna regola ulteriormente in questa sezione.  
  
7.  Se *attributo* è uguale a SQL_ATTR_FETCH_BOOKMARK_PTR, le cache di gestione Driver *ValuePtr* e userà il valore memorizzato nella cache più avanti in una chiamata a **SQLFetchScroll**. Si applica alcuna regola ulteriormente in questa sezione.  
  
8.  Le chiamate di gestione Driver **SQLSetStmtOption** come indicato di seguito:  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     in cui *hstmt*, *fOption*, e *vParam* verrà impostato su valori di *StatementHandle*, *attributo*, e *ValuePtr*, rispettivamente. Il *StringLength* argomento verrà ignorato.  
  
     Se un database ODBC *2.x* driver supporta le opzioni dell'istruzione di stringhe di caratteri, specifici del driver, un database ODBC *3.x* applicazione deve chiamare **SQLSetStmtOption** per impostare tali opzioni.  
  
## <a name="mappings-for-handling-parameter-arrays"></a>Mapping per la gestione delle matrici di parametri  
 Quando l'applicazione chiama:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 le chiamate di gestione Driver:  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 Gestione Driver, in un secondo momento, restituisce un puntatore a questa variabile quando l'applicazione chiama **SQLGetStmtAttr** recuperare SQL_ATTR_PARAMS_PROCESSED_PTR. Gestione Driver non è possibile modificare questa variabile interna finché non viene restituito l'handle di istruzione allo stato preparato o allocato.  
  
 Un database ODBC *3.x* applicazione può chiamare **SQLGetStmtAttr** per ottenere il valore di SQL_ATTR_PARAMS_PROCESSED_PTR anche se non è esplicitamente impostato il campo SQL_DESC_ARRAY_SIZE in APD. Questa situazione può verificarsi, ad esempio, se l'applicazione dispone di una routine generica che verifica la presenza di "riga" corrente "dei parametri in fase di elaborazione quando **SQLExecute** restituisce SQL_NEED_DATA. Questa routine viene richiamata o meno il SQL_DESC_ARRAY_SIZE è 1 o maggiore di 1. Per questo motivo, sarà necessario definire questa variabile interna o meno l'applicazione ha chiamato gestione Driver **SQLSetStmtAttr** per impostare il campo SQL_DESC_ARRAY_SIZE in APD. Se SQL_DESC_ARRAY_SIZE non è stato impostato, deve assicurarsi che questa variabile contiene il valore 1 prima della restituzione da Gestione Driver **SQLExecDirect** oppure **SQLExecute**.  
  
## <a name="error-handling"></a>Gestione degli errori  
 In ODBC *3.x*, la chiamata **SQLFetch** oppure **SQLFetchScroll** popola la SQL_DESC_ARRAY_STATUS_PTR nell'implementazione e il campo SQL_DIAG_ROW_NUMBER di una determinata diagnostica record contiene il numero di riga nel set di righe che si riferisce il record a. In questo modo l'applicazione può correlare un messaggio di errore con una posizione di riga specificato.  
  
 Un database ODBC *2.x* driver sarà in grado di fornire questa funzionalità. Tuttavia, fornirà demarcazione di errore con SQLSTATE 01S01 (errore nella riga). Un database ODBC *3.x* applicazione che usa **SQLFetch** oppure **SQLFetchScroll** nel corso su un database ODBC *2.x* deve essere a conoscenza del driver Questo fatto. Si noti inoltre che tale applicazione sarà in grado di chiamare **SQLGetDiagField** per ottenere il campo SQL_DIAG_ROW_NUMBER comunque. Un database ODBC *3.x* funziona con un database ODBC *2.x* driver sarà in grado di chiamare **SQLGetDiagField** solo con un *DiagIdentifier* argomento di SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_RETURNCODE o SQL_DIAG_SQLSTATE. ODBC *3.x* Driver Manager conserva la struttura di dati di diagnostica quando si lavora con un database ODBC *2.x* driver, ma ODBC *2.x* driver restituisce solo questi quattro campi.  
  
 Quando un'applicazione ODBC *2.x* applicazione funziona con un database ODBC *2.x* driver, se un'operazione può provocare più errori deve essere restituito da Gestione Driver, diversi errori possono essere restituiti da ODBC *3.x* Driver Manager piuttosto che da ODBC *2.x* gestione Driver.  
  
## <a name="mappings-for-bookmark-operations"></a>Mapping per le operazioni di segnalibro  
 ODBC *3.x* Driver Manager esegue i mapping seguenti quando un'applicazione ODBC *3.x* applicazione funziona con un database ODBC *2.x* driver esegue operazioni di segnalibro.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 Quando un'applicazione ODBC *3.x* funziona con un database ODBC *2.x* driver chiama **SQLBindCol** da associare alla colonna 0 con *fCType* uguale a SQL_C_ VARBOOKMARK, ODBC *3.x* Driver Manager verifica se il *BufferLength* argomento è minore di 4 o superiore a 4 e in caso affermativo, restituisce SQLSTATE HY090 (stringa non valido o buffer lunghezza). Se il *BufferLength* argomento è uguale a 4, le chiamate di gestione Driver **SQLBindCol** nel driver, dopo aver sostituito *fCType* con SQL_C_BOOKMARK.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Quando un'applicazione ODBC *3.x* funziona con un database ODBC *2.x* driver chiama **SQLColAttribute** con il *ColumnNumber* argomento impostato su 0, Gestione Driver restituisce il *FieldIdentifier* valori elencati nella tabella seguente.  
  
|*FieldIdentifier*|Value|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|"" (stringa vuota)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|Lo stesso valore restituito da **SQLNumResultCols**|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|  
|SQL_DESC_DISPLAY_SIZE|8|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|  
|SQL_DESC_LABEL|"" (stringa vuota)|  
|SQL_DESC_LENGTH|0|  
|SQL_DESC_LITERAL_PREFIX|"" (stringa vuota)|  
|SQL_DESC_LITERAL_SUFFIX|"" (stringa vuota)|  
|SQL_DESC_LOCAL_TYPE_NAME|"" (stringa vuota)|  
|SQL_DESC_NAME|"" (stringa vuota)|  
|SQL_DESC_NULLABLE|SQL_NO_NULLS|  
|SQL_DESC_OCTET_LENGTH|4|  
|SQL_DESC_PRECISION|4|  
|SQL_DESC_SCALE|0|  
|SQL_DESC_SCHEMA_NAME|"" (stringa vuota)|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|  
|SQL_DESC_TABLE_NAME|"" (stringa vuota)|  
|SQL_DESC_TYPE|SQL_BINARY|  
|SQL_DESC_TYPE_NAME|"" (stringa vuota)|  
|SQL_DESC_UNNAMED|SQL_UNNAMED|  
|SQL_DESC_UNSIGNED|SQL_FALSE|  
|SQL_DESC_UPDATEABLE|SQL_ATTR_READ_ONLY|  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 Quando un'applicazione ODBC *3.x* funziona con un database ODBC *2.x* driver chiama **SQLDescribeCol** con il *ColumnNumber* argomento impostato su 0, Gestione Driver restituisce i valori elencati nella tabella seguente.  
  
|Buffer|Value|  
|------------|-----------|  
|ColumnName|"" (stringa vuota)|  
|*NameLengthPtr|0|  
|\* DataTypePtr|SQL_BINARY|  
|\* ColumnSizePtr|4|  
|\* DecimalDigitsPtr|0|  
|*NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 Quando un'applicazione ODBC *3.x* funziona con un database ODBC *2.x* driver effettua la chiamata seguente al **SQLGetData** per recuperare un segnalibro:  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 la chiamata viene mappata a **SQLGetStmtOption** con un *fOption* di SQL_GET_BOOKMARK, come indicato di seguito:  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 in cui *hstmt* e *il parametro pvParam* vengono impostati sui valori nelle *StatementHandle* e *TargetValuePtr*, rispettivamente. Il segnalibro viene restituito nel buffer a cui fa riferimento il *il parametro pvParam* (*TargetValuePtr*) argomento. Il valore nel buffer a cui fa riferimento il *StrLen_or_IndPtr* argomento nella chiamata a **SQLGetData** è impostato su 4.  
  
 Questo mapping è necessario tenere conto per il caso in cui **SQLFetch** è stato chiamato prima della chiamata a **SQLGetData** e ODBC *2.x* driver non supportava **SQLExtendedFetch**. In questo caso **SQLFetch** potrebbe essere passato tramite ODBC *2.x* driver, in cui il recupero di case di segnalibro non è supportato.  
  
 **SQLGetData** non può essere chiamato più volte in un database ODBC *2.x* driver per recuperare un segnalibro in parti, pertanto la chiamata **SQLGetData** con le *BufferLength* argomento impostato su un valore inferiore a 4 e il *ColumnNumber* argomento impostato su 0 restituiranno SQLSTATE HY090 (stringa di lunghezza o non valida del buffer). **SQLGetData** , tuttavia, può essere chiamato più volte per recuperare lo stesso segnalibro.  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 Quando un'applicazione ODBC *3.x* funziona con un database ODBC *2.x* driver chiama **SQLSetStmtAttr** per impostare il SQL_ATTR_USE_BOOKMARKS attributo SQL_UB_VARIABLE, il Driver Manager imposta l'attributo SQL_UB_ON in ODBC sottostante *2.x* driver.
