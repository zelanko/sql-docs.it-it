---
title: Mappatura delle funzioni di sostituzione per la compatibilità delle applicazioni - ODBC Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b18669fe9b6edbd39859166e382ad18d1b04a99a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301091"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>Mapping di funzioni di sostituzione per la compatibilità con le versioni precedenti delle applicazioni
Un'applicazione ODBC *3.x* che utilizza Gestione driver ODBC *3.x* funzionerà con un driver ODBC *2.x* purché non vengono utilizzate nuove funzionalità. Sia la funzionalità duplicata che le modifiche comportamentali influiscono tuttavia sul funzionamento dell'applicazione ODBC *3.x* su un driver ODBC *2.x.* Quando si utilizza un driver ODBC *2.x,* Gestione Driver esegue il mapping delle seguenti funzioni ODBC *3.x,* che hanno sostituito una o più funzioni ODBC *2.x,* nelle funzioni ODBC *2.x* corrispondenti.  
  
|ODBC *3.x (funzione)*|ODBC *2.x (funzione)*|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**, **SQLAllocConnect**o **SQLAllocStmt**|  
|**Sqlbulkoperations**|**SQLSetPos**|  
|**SQLColAttribute**|**ATTRIBUTI SQLCol**|  
|**SQLEndTran**|**SQLTransact (transazione SQLTransact)**|  
|**SQLFetch**|**Sqlextendedfetch**|  
|**SQLFetchScroll**|**Sqlextendedfetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**, **SQLFreeConnect**o **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption (Opzione SQLGetConnectOption)**|  
|**SQLGetDiagRec**|**Sqlerror**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**Sqlsetconnectoption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] Potrebbero essere intraprese anche altre azioni, a seconda dell'attributo richiesto.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 Gestione Driver esegue il mapping a **SQLAllocEnv**, **SQLAllocConnect**o **SQLAllocStmt**, in base alle esigenze. La chiamata seguente a **SQLAllocHandle:**  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 si tradurrà in Gestione Driver eseguendo il seguente mapping (concettuale, nessun controllo degli errori):  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>Sqlbulkoperations  
 Gestione Driver esegue il mapping di questo a **SQLSetPos**. La chiamata seguente a **SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 si tradurrà nella seguente sequenza di passaggi:  
  
1.  Se l'argomento Operation è SQL_ADD, Gestione Driver chiama **SQLSetPos** come segue:  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  Se l'argomento Operation non è SQL_ADD, il driver restituisce SQLSTATE HY092 (identificatore di attributo/opzione non valido).  
  
3.  Se l'applicazione tenta di modificare l'SQL_ATTR_ROW_STATUS_PTR tra le chiamate a **SQLFetch** o **SQLFetchScroll** e **SQLBulkOperations**, Gestione Driver restituirà SQLSTATE HY011 (attributo non può essere impostato ora).  
  
4.  Se il Operation argomento è SQL_ADD, l'applicazione deve chiamare **SQLBindCol** per associare i dati da inserire. Non è possibile chiamare **SQLSetDescField** o **SQLSetDescRec** per associare i dati da inserire.  
  
5.  Se l'argomento Operation è SQL_ADD e il numero di righe da inserire non corrisponde alla dimensione corrente del set di righe, **sqlSetStmtAttr** deve essere chiamato per impostare l'attributo dell'istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe da inserire prima di chiamare **SQLBulkOperations**. Per ripristinare le dimensioni del set di righe precedente, l'applicazione deve impostare l'attributo dell'istruzione SQL_ATTR_ROW_ARRAY_SIZE prima che venga chiamato **SQLFetch**, **SQLFetchScroll**o **SQLSetPos** .  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 Gestione Driver esegue il mapping a **SQLColAttributes**. La chiamata seguente a **SQLColAttribute:**  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 si tradurrà nella seguente sequenza di passaggi:  
  
1.  Se *FieldIdentifier* è uno dei seguenti:  
  
     SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH, SQL_DESC_OCTET_LENGTH, SQL_DESC_UNNAMED, SQL_DESC_BASE_COLUMN_NAME, SQL_DESC_LITERAL_PREFIX, SQL_DESC_LITERAL_SUFFIX o SQL_DESC_LOCAL_TYPE_NAME  
  
     Gestione Driver restituisce SQL_ERROR con SQLSTATE HY091 (identificatore di campo descrittore non valido). Non si applicano altre regole di questa sezione.  
  
2.  Gestione Driver esegue il mapping di SQL_COLUMN_COUNT, SQL_COLUMN_NAME o SQL_COLUMN_NULLABLE rispettivamente a SQL_DESC_COUNT, SQL_DESC_NAME o SQL_DESC_NULLABLE. Un driver ODBC *2.x* deve essere supportato solo SQL_COLUMN_COUNT, SQL_COLUMN_NAME e SQL_COLUMN_NULLABLE, non SQL_DESC_COUNT, SQL_DESC_NAME e SQL_DESC_NULLABLE. La chiamata a SQLColAttribute è mappata a:The call to SQLColAttribute is mapped to:  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  Tutti gli altri valori *FieldIdentifier* vengono passati al driver, con **SQLColAttribute** mappato a **SQLColAttributes** come illustrato in precedenza.  
  
4.  Se *BufferLength* è minore di 0, Gestione Driver restituisce SQL_ERROR con SQLSTATE HY090 (stringa non valida o lunghezza del buffer). Non si applicano altre regole di questa sezione.  
  
5.  Se *FieldIdentifier* è SQL_DESC_CONCISE_TYPE e il tipo restituito è un tipo di dati datetime conciso, Gestione Driver esegue il mapping dei valori restituiti per i codici di data, ora e timestamp.  
  
6.  Gestione Driver esegue i controlli necessari per verificare se SQLSTATE HY010 (errore di sequenza di funzione) deve essere generato. In tal caso, Gestione Driver restituisce SQL_ERROR e SQLSTATE HY010 (errore di sequenza di funzione). Non si applicano altre regole di questa sezione.  
  
## <a name="sqlendtran"></a>SQLEndTran  
 Gestione Driver esegue il mapping a **SQLTransact**. La seguente chiamata a **SQLEndTran:**  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 si tradurrà in Gestione Driver eseguendo il seguente mapping (concettuale, nessun controllo degli errori):  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 Gestione Driver esegue il mapping di questo a **SQLExtendedFetch** con un *FetchOrientation* argomento di SQL_FETCH_NEXT. La seguente chiamata a **SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 verrà riportato il nome di Gestione driver che chiama **SQLExtendedFetch**, come indicato di seguito:  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 In questa chiamata, l'argomento *pcRow* viene impostato sul valore su cui l'applicazione imposta l'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR tramite una chiamata a **SQLSetStmtAttr**.  
  
> [!NOTE]  
>  Quando l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROW_STATUS_PTR in modo che punti a una matrice di stato, Gestione Driver memorizza il puntatore nella cache. *RowStatusArray* può essere uguale a un puntatore null.  
  
 Se il driver non supporta **SQLExtendedFetch** e viene caricata la libreria di cursori, Gestione Driver utilizza **SQLExtendedFetch** della libreria di cursori per eseguire il mapping di **SQLFetch** a **SQLExtendedFetch**. Se il driver non supporta **SQLExtendedFetch** e la libreria di cursori non è caricata, Gestione Driver passa la chiamata a **SQLFetch** tramite il driver. Se l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROW_STATUS_PTR, Gestione Driver garantisce che la matrice viene popolata. Se l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROWS_FETCHED_PTR, Gestione Driver imposta questo campo su 1.  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 Gestione Driver esegue il mapping di questo a **SQLExtendedFetch**. La seguente chiamata a **SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 si tradurrà nella seguente sequenza di passaggi:  
  
1.  Quando l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROW_STATUS_PTR (che imposta il campo SQL_DESC_ARRAY_STATUS_PTR nell'IRD) in modo che punti a una matrice di stato, Gestione Driver memorizza nella cache questo puntatore. Consentire a questo puntatore di essere *RowStatusArray*; in caso contrario, lasciare *RowStatusArray* essere uguale a un puntatore null. Se il *RowStatusArray* argomento è impostato su un puntatore null, Gestione Driver genera una matrice di stato di riga.  
  
2.  Se *FetchOrientation* non è SQL_FETCH_NEXT, SQL_FETCH_PRIOR, SQL_FETCH_ABSOLUTE, SQL_FETCH_RELATIVE, SQL_FETCH_FIRST, SQL_FETCH_LAST o SQL_FETCH_BOOKMARK, Gestione Driver ritorna con SQL_ERROR e SQLSTATE HY106 (Fetch tipo non compreso nell'intervallo). Non si applicano altre regole di questa sezione.  
  
3.  Maiuscole/minuscole:  
  
-   Se FetchOrientation è uguale a SQL_FETCH_BOOKMARK, allora:If *FetchOrientation* is equal, then:  
  
    -   Se **SQLSetStmtAttr** è stato chiamato in precedenza per impostare il valore di SQL_ATTR_FETCH_BOOKMARK_PTR, quindi lasciare *Bmk* essere il valore ottenuto dereferenziando il puntatore SQL_DESC_FETCH_BOOKMARK_PTR.  
  
    -   In caso contrario, restituire SQL_ERROR con SQLSTATE HY111 (valore del segnalibro non valido). Non si applicano altre regole di questa sezione.  
  
     Gestione Driver ora chiama **SQLExtendedFetch**, come segue:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   In caso contrario, Gestione Driver chiama **SQLExtendedFetch**, come segue:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     In queste chiamate, il *pcRow* argomento è impostato sul valore che l'applicazione imposta il SQL_ATTR_ROWS_FETCHED_PTR attributo di istruzione tramite una chiamata a **SQLSetStmtAttr**.  
  
-   SQL_ATTR_ROW_ARRAY_SIZE è mappato a SQL_ROWSET_SIZE.  
  
-   Se *rc* è uguale a SQL_SUCCESS o SQL_SUCCESS_WITH_INFO e se *FetchOrientation* è uguale a SQL_FETCH_BOOKMARK e *FetchOffset* non è uguale a 0, Gestione Driver invia un avviso, SQLSTATE 01S10 (tentativo di recupero da un offset del segnalibro, valore di offset ignorato) e restituisce SQL_SUCCESS_WITH_INFO.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 Gestione Driver esegue il mapping di questo a **SQLFreeEnv**, **SQLFreeConnect**o **SQLFreeStmt** in base alle esigenze. La seguente chiamata a **SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 si tradurrà in Gestione Driver eseguendo il seguente mapping (concettuale, nessun controllo degli errori):  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 Gestione Driver esegue il mapping a **SQLGetConnectOption**. La chiamata seguente a **SQLGetConnectAttr:**  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 si tradurrà nella seguente sequenza di passaggi:  
  
1.  Se *Attributo* non è un attributo di connessione o istruzione definito dal driver e non è un attributo definito in ODBC *2.x*, Gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (identificatore di attributo/opzione non valido). Non si applicano altre regole in questa sezione.  
  
2.  Se *Attributo* è uguale a SQL_ATTR_AUTO_IPD o SQL_ATTR_METADATA_ID, Gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (identificatore di attributo/opzione non valido).  
  
3.  Gestione Driver esegue i controlli necessari per verificare se SQLSTATE 08003 (connessione non aperta) o SQLSTATE HY010 (errore di sequenza di funzione) deve essere generato. In tal caso, Gestione Driver restituisce SQL_ERROR e invia il messaggio di errore appropriato. Non si applicano altre regole di questa sezione.  
  
4.  Gestione Driver chiama SQLGetConnectOption come segue:The Driver Manager calls **SQLGetConnectOption** as follows:  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     Si noti che *il BufferLength* e *StringLengthPtr* vengono ignorati.  
  
## <a name="sqlgetdata"></a>SQLGetData  
 Quando un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* chiama **SQLGetData** con il *ColumnNumber* argomento uguale a 0, il Gestore Driver ODBC *3.x* esegue il mapping di questo a una chiamata a **SQLGetStmtOption** con il *Option* attributo impostato su SQL_GET_BOOKMARK.  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 Gestione Driver esegue il mapping a **SQLGetStmtOption**. La seguente chiamata a **SQLGetStmtAttr:**  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 si tradurrà nella seguente sequenza di passaggi:  
  
1.  Se *Attributo* non è un attributo di connessione o istruzione definito dal driver e non è un attributo definito in ODBC *2.x*, Gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (identificatore di attributo/opzione non valido). Non si applicano altre regole in questa sezione.  
  
2.  Se *Attributo* è uno dei seguenti:  
  
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
  
     Gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (identificatore di attributo/opzione non valido). Non si applicano altre regole di questa sezione.  
  
3.  Gestione Driver esegue i controlli necessari per verificare se SQLSTATE HY010 (errore di sequenza di funzione) deve essere generato. In tal caso, Gestione Driver restituisce SQL_ERROR e SQLSTATE HY010 (errore di sequenza di funzione). Non si applicano altre regole di questa sezione.  
  
4.  Se *Attribute* è uguale a SQL_ATTR_ROWS_FETCHED_PTR, Gestione Driver restituisce un puntatore alla variabile interna di Gestione Driver *cRow*, che ha utilizzato o verrà utilizzato in una chiamata a **SQLExtendedFetch**. Non si applicano altre regole di questa sezione.  
  
5.  Se *Attribute* è uguale a SQL_DESC_FETCH_BOOKMARK_PTR, Gestione Driver restituisce il puntatore appropriato che aveva memorizzato nella cache durante una chiamata a **SQLSetStmtAttr**.  
  
6.  Se *Attribute* è uguale a SQL_ATTR_ROW_STATUS_PTR, Gestione Driver restituisce il puntatore appropriato che aveva memorizzato nella cache durante una chiamata a **SQLSetStmtAttr**.  
  
7.  Gestione Driver chiama **SQLGetStmtOption** come segue:  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     dove *hstmt*, *fOption*e *pvParam* verranno impostati rispettivamente sui valori di *StatementHandle*, *Attribute*e *ValuePtr*. Il *BufferLength* e *StringLengthPtr* vengono ignorati.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 Gestione Driver esegue il mapping a **SQLSetConnectOption**. La seguente chiamata a **SQLSetConnectAttr:**  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 si tradurrà nella seguente sequenza di passaggi:  
  
1.  Se *Attributo* non è un attributo di connessione o istruzione definito dal driver e non è un attributo definito in ODBC *2.x*, Gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (identificatore di attributo/opzione non valido). Non si applicano altre regole in questa sezione.  
  
2.  Se *Attributo* è uguale a SQL_ATTR_AUTO_IPD, Gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (identificatore di attributo/opzione non valido).  
  
3.  Gestione Driver esegue i controlli necessari per verificare se SQLSTATE 08003 (connessione non aperta) o SQLSTATE HY010 (errore di sequenza di funzione) devono essere generati. Se uno di questi errori deve essere generato, Gestione Driver restituisce SQL_ERROR e invia il messaggio di errore appropriato. Non si applicano altre regole di questa sezione.  
  
4.  Gestione Driver chiama **SQLSetConnectOption** come segue:  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     dove *hdbc*, *fOption*e *vParam* verranno impostati rispettivamente sui valori di *ConnectionHandle*, *Attribute*e *ValuePtr*. *StringLengthPtr* viene ignorato.  
  
> [!NOTE]  
>  La possibilità di impostare gli attributi dell'istruzione a livello di connessione è deprecata. Gli attributi dell'istruzione non devono mai essere impostati a livello di connessione da un'applicazione ODBC *3.x.*  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 Gestione Driver esegue il mapping di questo a **SQLSetStmtOption**. La seguente chiamata a **SQLSetStmtAttr:**  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 si tradurrà nella seguente sequenza di passaggi:  
  
1.  Se *Attributo* non è un attributo di connessione o istruzione definito dal driver e non è un attributo definito in ODBC *2.x*, Gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (identificatore di attributo/opzione non valido). Non si applicano altre regole in questa sezione.  
  
2.  Se *Attributo* è uno dei seguenti:  
  
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
  
     Gestione Driver restituisce SQL_ERROR con SQLSTATE HY092 (identificatore di attributo/opzione non valido). Non si applicano altre regole di questa sezione.  
  
3.  Gestione Driver esegue i controlli necessari per verificare se sqlSTATE HY010 (errore di sequenza di funzione) deve essere generato. In tal caso, Gestione Driver restituisce SQL_ERROR e SQLSTATE HY010 (errore di sequenza di funzione). Non si applicano altre regole di questa sezione.  
  
4.  Se *Attributo* è uguale a SQL_ATTR_PARAMSET_SIZE o SQL_ATTR_PARAMS_PROCESSED_PTR, vedere la sezione "Mapping per la gestione delle matrici di parametri" più avanti in questo argomento. Non si applicano altre regole di questa sezione.  
  
5.  Se *Attribute* è uguale a SQL_ATTR_ROWS_FETCHED_PTR, Gestione Driver memorizza nella cache il valore del puntatore per un utilizzo successivo con **SQLFetchScroll**.  
  
6.  Se *Attributo* è uguale a SQL_ATTR_ROW_STATUS_PTR, Gestione Driver memorizza nella cache il valore del puntatore per un utilizzo successivo con **SQLFetchScroll** o **SQLSetPos**. Non si applicano altre regole di questa sezione.  
  
7.  Se *Attribute* è uguale a SQL_ATTR_FETCH_BOOKMARK_PTR, Gestione Driver memorizza nella cache *ValuePtr* e utilizzerà il valore memorizzato nella cache in un secondo momento in una chiamata a **SQLFetchScroll**. Non si applicano altre regole di questa sezione.  
  
8.  Gestione Driver chiama **SQLSetStmtOption** come segue:  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     dove *hstmt*, *fOption*e *vParam* verranno impostati rispettivamente sui valori di *StatementHandle*, *Attribute*e *ValuePtr*. L'argomento *StringLength* viene ignorato.  
  
     Se un driver ODBC *2.x* supporta le opzioni di istruzione specifiche del driver, un'applicazione ODBC *3.x* deve chiamare **SQLSetStmtOption** per impostare tali opzioni.  
  
## <a name="mappings-for-handling-parameter-arrays"></a>Mapping per la gestione delle matrici di parametriMappings for Handling Parameter Arrays  
 Quando l'applicazione chiama:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 Gestione Driver chiama:  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 Gestione Driver in un secondo momento restituisce un puntatore a questa variabile quando l'applicazione chiama **SQLGetStmtAttr** per recuperare SQL_ATTR_PARAMS_PROCESSED_PTR. Gestione Driver non può modificare questa variabile interna fino a quando l'handle di istruzione viene restituito allo stato preparato o allocato.  
  
 Un'applicazione ODBC *3.x* può chiamare **SQLGetStmtAttr** per ottenere il valore di SQL_ATTR_PARAMS_PROCESSED_PTR anche se non ha impostato in modo esplicito il campo SQL_DESC_ARRAY_SIZE nell'oggetto APD. Questa situazione può verificarsi, ad esempio, se l'applicazione dispone di una routine generica che controlla la "riga" corrente dei parametri in fase di elaborazione quando **SQLExecute** restituisce SQL_NEED_DATA. Questa routine viene richiamata indipendentemente dal fatto che il SQL_DESC_ARRAY_SIZE sia 1 o sia maggiore di 1. A causa di questo, Gestione Driver dovrà definire questa variabile interna se l'applicazione ha chiamato **SQLSetStmtAttr** per impostare il campo SQL_DESC_ARRAY_SIZE in APD. Se non è stata impostata SQL_DESC_ARRAY_SIZE, Gestione Driver deve assicurarsi che questa variabile contenga il valore 1 prima di restituire da **SQLExecDirect** o **SQLExecute**.  
  
## <a name="error-handling"></a>Gestione degli errori  
 In ODBC *3.x*, la chiamata a **SQLFetch** o **SQLFetchScroll** popola il SQL_DESC_ARRAY_STATUS_PTR nella Classe Di RD e il campo SQL_DIAG_ROW_NUMBER di un determinato record di diagnostica contiene il numero della riga nel set di righe a cui si parte questo record. In questo modo, l'applicazione può correlare un messaggio di errore con una determinata posizione di riga.  
  
 Un driver ODBC *2.x* non sarà in grado di fornire questa funzionalità. Tuttavia, verrà fornita la demarcazione degli errori con SQLSTATE 01S01 (errore nella riga). Un'applicazione ODBC *3.x* che utilizza **SQLFetch** o **SQLFetchScroll** mentre si passa contro un driver ODBC *2.x* deve essere a conoscenza di questo fatto. Si noti inoltre che tale applicazione non sarà in grado di chiamare **SQLGetDiagField** per ottenere effettivamente il campo SQL_DIAG_ROW_NUMBER comunque. Un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* sarà in grado di chiamare **SQLGetDiagField** solo con un *DiagIdentifier* argomento di SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_RETURNCODE o SQL_DIAG_SQLSTATE. ODBC *3.x* Driver Manager mantiene la struttura dei dati di diagnostica quando si lavora con un driver ODBC *2.x,* ma il driver ODBC *2.x* restituisce solo questi quattro campi.  
  
 Quando un'applicazione ODBC *2.x* utilizza un driver ODBC *2.x,* se un'operazione può causare la restituzione di più errori da Gestione Driver, possono essere restituiti errori diversi da Gestione Driver ODBC *3.x* rispetto a Gestione driver ODBC *2.x.*  
  
## <a name="mappings-for-bookmark-operations"></a>Mapping per le operazioni sui segnalibri  
 Gestione Driver ODBC *3.x* esegue i mapping seguenti quando un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* esegue operazioni sui segnalibri.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 Quando un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* chiama **SQLBindCol** per l'associazione alla colonna 0 con *fCType* uguale a SQL_C_VARBOOKMARK, ODBC *3.x* Gestione Driver verifica se il *BufferLength* argomento è minore di 4 o maggiore di 4 e, in caso affermativo, restituisce SQLSTATE HY090 (stringa non valida o lunghezza del buffer). Se il *BufferLength* argomento è uguale a 4, Gestione Driver chiama **SQLBindCol** nel driver, dopo la sostituzione di *fCType* con SQL_C_BOOKMARK.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Quando un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* chiama **SQLColAttribute** con il *ColumnNumber* argomento impostato su 0, Gestione Driver restituisce il *FieldIdentifier* valori elencati nella tabella seguente.  
  
|*FieldIdentifier*|Valore|  
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
 Quando un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* chiama **SQLDescribeCol** con l'argomento *ColumnNumber* impostato su 0, Gestione Driver restituisce i valori elencati nella tabella seguente.  
  
|Buffer|Valore|  
|------------|-----------|  
|ColumnName|"" (stringa vuota)|  
|-NameLengthPtr|0|  
|DataTypePtr (DataTypePtr)|SQL_BINARY|  
|ColumnSizePtr (ColumnSizePtr)|4|  
|DecimalDigitsPtr (DecimalDigitsPtr)|0|  
|NullablePtr (NullablePtr)|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 Quando un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* effettua la seguente chiamata a **SQLGetData** per recuperare un segnalibro:  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 la chiamata è mappata a **SQLGetStmtOption** con un *fOption* di SQL_GET_BOOKMARK, come segue:  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 dove *hstmt* e *pvParam* sono impostati sui valori rispettivamente in *StatementHandle* e *TargetValuePtr*. Il segnalibro viene restituito nel buffer a cui punta l'argomento *pvParam* (*TargetValuePtr*). Il valore nel buffer a cui fa riferimento l'argomento *StrLen_or_IndPtr* nella chiamata a **SQLGetData** è impostato su 4.  
  
 Questo mapping è necessario per tenere conto del caso in cui **SQLFetch** è stato chiamato prima della chiamata a **SQLGetData** e il driver ODBC *2.x* non supporta **SQLExtendedFetch**. In questo caso, **SQLFetch** verrebbe passato al driver ODBC *2.x,* nel qual caso il recupero dei segnalibri non è supportato.  
  
 **Impossibile chiamare SQLGetData** più volte in un driver ODBC *2.x* per recuperare un segnalibro in parti, pertanto la chiamata di **SQLGetData** con il *BufferLength* argomento impostato su un valore minore di 4 e il *ColumnNumber* argomento impostato su 0 restituirà SQLSTATE HY090 (stringa non valida o lunghezza del buffer). **SQLGetData** può, tuttavia, essere chiamato più volte per recuperare lo stesso segnalibro.  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 Quando un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* chiama **SQLSetStmtAttr** per impostare l'attributo SQL_ATTR_USE_BOOKMARKS su SQL_UB_VARIABLE, Gestione Driver imposta l'attributo su SQL_UB_ON nel driver ODBC *2.x* sottostante.
