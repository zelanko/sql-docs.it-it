---
title: Transizioni di istruzioni Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55f82e275bfd5bff12544b35a1370cdb31495320
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302852"
---
# <a name="statement-transitions"></a>Transizioni di istruzione
Le istruzioni ODBC hanno i seguenti stati.  
  
|State|Descrizione|  
|-----------|-----------------|  
|S0|Istruzione non allocata. (Lo stato della connessione deve essere C4, C5 o C6. Per ulteriori informazioni, vedere [Transizioni di connessione](../../../odbc/reference/appendixes/connection-transitions.md).)|  
|S1|Istruzione allocata.|  
|S2|Dichiarazione preparata. Non verrà creato alcun set di risultati.|  
|S3|Dichiarazione preparata. Verrà creato un set di risultati (eventualmente vuoto).|  
|S4|Istruzione eseguita e non è stato creato alcun set di risultati.|  
|S5|Istruzione eseguita ed è stato creato un set di risultati (eventualmente vuoto). Il cursore è aperto e posizionato prima della prima riga del set di risultati.|  
|S6|Cursore posizionato con **SQLFetch** o **SQLFetchScroll**.|  
|S7|Cursore posizionato con **SQLExtendedFetch**.|  
|S8 (in questo)|La funzione richiede dati. **SQLParamData** non è stato chiamato.|  
|S9|La funzione richiede dati. **SQLPutData** non è stato chiamato.|  
|S10|La funzione richiede dati. **SQLPutData** è stato chiamato.|  
|S11 (in modo s11)|Ancora in esecuzione. Un'istruzione viene lasciata in questo stato dopo che una funzione che viene eseguita in modo asincrono restituisce SQL_STILL_EXECUTING. Un'istruzione si trova temporaneamente in questo stato mentre è in esecuzione qualsiasi funzione che accetta un handle di istruzione. La residenza temporanea nello stato S11 non viene visualizzata in alcuna tabella di stato ad eccezione della tabella di stato per **SQLCancel**. Mentre un'istruzione è temporaneamente nello stato S11, la funzione può essere annullata chiamando **SQLCancel** da un altro thread.|  
|S12|Esecuzione asincrona annullata. In S12, un'applicazione deve chiamare la funzione annullata fino a quando non restituisce un valore diverso da SQL_STILL_EXECUTING. La funzione è stata annullata correttamente solo se la funzione restituisce SQL_ERROR e SQLSTATE HY008 (Operazione annullata). Se restituisce qualsiasi altro valore, ad esempio SQL_SUCCESS, l'operazione di annullamento non è riuscita e la funzione eseguita normalmente.|  
  
 Gli stati S2 e S3 sono noti come stati preparati, gli stati da S5 a S7 come stati del cursore, gli stati da S8 a S10 come stati di dati necessari e gli stati S11 e S12 come stati asincroni. In ognuno di questi gruppi, le transizioni vengono visualizzate separatamente solo quando sono diverse per ogni stato del gruppo; nella maggior parte dei casi, le transizioni per ogni stato in ogni gruppo sono le stesse.  
  
 Nelle tabelle seguenti viene illustrato come ogni funzione ODBC influisce sullo stato dell'istruzione.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1[3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 [2] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC.  
  
 [3] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_STMT.  
  
 Questa riga mostra le transizioni quando *HandleType* era SQL_HANDLE_DESC.  
  
 [5] La chiamata a **SQLAllocHandle** con *OutputHandlePtr* che punta a un handle valido sovrascrive tale handle indipendentemente dal contenuto precedente per tale handle e potrebbe causare problemi per i driver ODBC. Programmazione dell'applicazione ODBC non è corretta per chiamare **SQLAllocHandle** due volte con la stessa variabile di applicazione definita per * \*OutputHandlePtr* senza chiamare **SQLFreeHandle** per liberare l'handle prima di riallocherlo. La sovrascrittura degli handle ODBC in questo modo potrebbe causare un comportamento o errori incoerenti da parte dei driver ODBC.  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect, SQLConnect e SQLDriverConnect  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>Sqlbulkoperations  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|24000|Vedi la tabella seguente|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations (Cursor States)  
  
|S5<br /><br /> Aperto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|-- [s] S8 [d] S11 [x]|-- [s] S8 [d] S11 [x]|HY010 (Informazioni in stati incomMIino in|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|S1[1] S2 [nr] e [2] S3 [r]e [2] S5[3] e [5] S6([3] o [4]) e [6] S7[4] e [7]|Vedi la tabella seguente|  
  
 [1] **SQLExecDirect** ha restituito SQL_NEED_DATA.  
  
 [2] **SQLExecute** ha restituito SQL_NEED_DATA.  
  
 [3] **SQLBulkOperations** ha restituito SQL_NEED_DATA.  
  
 [4] **SQLSetPos** ha restituito SQL_NEED_DATA.  
  
 [5] **SQLFetch**, **SQLFetchScroll**o **SQLExtendedFetch** non erano stati chiamati.  
  
 [6] **SQLFetch** o **SQLFetchScroll** era stato chiamato.  
  
 [7] **SQLExtendedFetch** era stato chiamato.  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel (stati asincroni)  
  
|S11 (in modo s11)<br /><br /> Ancora in esecuzione|S12<br /><br /> Asynch annullato|  
|-----------------------------|-----------------------------|  
|NS[1] S12[2]|S12|  
  
 [1] L'istruzione era temporaneamente nello stato S11 mentre era in esecuzione una funzione. **SQLCancel** è stato chiamato da un thread diverso.  
  
 [2] L'istruzione era nello stato S11 perché una funzione chiamata ha restituito in modo asincrono SQL_STILL_EXECUTING.  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|24000|24000|24000|S1 [np] S3 [p]|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010 (Informazioni in stati incomMIino in|Vedi la tabella seguente|24000|-- [s] S11 [x]|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute (Prepared States)  
  
|S2<br /><br /> Nessun risultato|S3<br /><br /> Risultati|  
|-----------------------|--------------------|  
|--[1] 07005[2]|-- [s] S11 x|  
  
 [1] *FieldIdentifier* è stato SQL_DESC_COUNT.  
  
 [2] *FieldIdentifier* non è stato SQL_DESC_COUNT.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges e SQLTables  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] e [1] S5 [s] e [1] S11 [x] e [1] 24000[2]|Vedi la tabella seguente|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 o|  
  
 [1] Il risultato corrente è l'ultimo o unico risultato, o non ci sono risultati correnti. Per ulteriori informazioni su più risultati, vedere [Risultati multipli](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2] Il risultato corrente non è l'ultimo risultato.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges e SQLTables (Stati cursore)  
  
|S5<br /><br /> Aperto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [1] Questo errore viene restituito da Gestione Driver se **SQLFetch** o **SQLFetchScroll** non ha restituito SQL_NO_DATA e viene restituito dal driver se **SQLFetch** o **SQLFetchScroll** ha restituito SQL_NO_DATA.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc (informazioni in lingua inglese)  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010 (Informazioni in stati incomMIino in|NS [c] e [3] HY010 [o] o [4]|  
|IH[2]|HY010 (Informazioni in stati incomMIino in|Vedi la tabella seguente|24000|-- [s] S11 x|HY010 (Informazioni in stati incomMIino in|NS [c] e [3] HY010 [o] o [4]|  
  
 [1] Questa riga mostra le transizioni quando l'argomento *SourceDescHandle* era un ARD, un APD o un IPD.  
  
 [2] Questa riga mostra le transizioni quando l'argomento *SourceDescHandle* era un IRD.  
  
 [3] Gli argomenti *SourceDescHandle* e *TargetDescHandle* erano gli stessi della funzione **SQLCopyDesc** in esecuzione in modo asincrono.  
  
 [4] L'argomento *SourceDescHandle* o l'argomento *TargetDescHandle* (o entrambi) erano diversi rispetto alla funzione **SQLCopyDesc** in esecuzione in modo asincrono.  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (Prepared States)  
  
|S2<br /><br /> Nessun risultato|S3<br /><br /> Risultati|  
|-----------------------|--------------------|  
|24000[1]|-- [s] S11 [x]|  
  
 [1] Questa riga mostra le transizioni quando l'argomento *SourceDescHandle* era un IRD.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010 (Informazioni in stati incomMIino in|Vedi la tabella seguente|24000|-- [s] S11 [x]|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (Stati preparati)  
  
|S2<br /><br /> Nessun risultato|S3<br /><br /> Risultati|  
|-----------------------|--------------------|  
|07005|-- [s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010 (Informazioni in stati incomMIino in|-- [s] S11 [x]|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>Sqldisconnect  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0[1]|S0[1]|S0[1]|S0[1]|(HY010)|(HY010)|  
  
 [1] La chiamata a **SQLDisconnect** libera tutte le istruzioni associate alla connessione. Inoltre, restituisce lo stato della connessione a C2; lo stato della connessione deve essere C4 prima che lo stato dell'istruzione sia S0.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--[2] o S1[1]|--[3] S1 [np] e ([1] o [2]) S1 [p] e [1] S2 [p] e [2]|--[3] S1 [np] e ([1] o [2]) S1 [p] e [1] S3 [p] e [2]|(HY010)|(HY010)|  
  
 [1] L'argomento *CompletionType* è SQL_COMMIT e **SQLGetInfo** restituisce SQL_CB_DELETE per il tipo di informazioni SQL_CURSOR_COMMIT_BEHAVIOR oppure l'argomento *CompletionType* è SQL_ROLLBACK e **SQLGetInfo** restituisce SQL_CB_DELETE per il tipo di informazioni SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [2] L'argomento *CompletionType* è SQL_COMMIT e **SQLGetInfo** restituisce SQL_CB_CLOSE per il tipo di informazioni SQL_CURSOR_COMMIT_BEHAVIOR oppure l'argomento *CompletionType* è SQL_ROLLBACK e **SQLGetInfo** restituisce SQL_CB_CLOSE per il tipo di informazioni SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [3] L'argomento *CompletionType* è SQL_COMMIT e **SQLGetInfo** restituisce SQL_CB_PRESERVE per il tipo di informazioni SQL_CURSOR_COMMIT_BEHAVIOR oppure l'argomento *CompletionType* è SQL_ROLLBACK e **SQLGetInfo** restituisce SQL_CB_PRESERVE per il tipo di informazioni SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S4 [s] e [nr] S5 [s] e [r] S8 [d] S11 [x]|-- [e] e [1] S1 [e] e [2] S4 [s] e [nr] S5 [s] e [r] S8 [d] S11 [x]|-- [e], [1], e [3] S1 [e], [2], e [3] S4 [s], [nr] e [3] S5 [s], [r], e [3] S8 [d] e [3] S11 [x] e [3] 24000 [4]|Vedi la tabella seguente|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 [o]|  
  
 [1] L'errore è stato restituito da Gestione driver.  
  
 [2] L'errore non è stato restituito da Gestione driver.  
  
 [3] Il risultato corrente è l'ultimo o unico risultato, o non ci sono risultati correnti. Per ulteriori informazioni su più risultati, vedere [Risultati multipli](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4] Il risultato attuale non è l'ultimo risultato.  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (stati cursore)  
  
|S5<br /><br /> Aperto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] Questo errore viene restituito da Gestione Driver se **SQLFetch** o **SQLFetchScroll** non ha restituito SQL_NO_DATA e viene restituito dal driver se **SQLFetch** o **SQLFetchScroll** ha restituito SQL_NO_DATA.  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|Vedi la tabella seguente|S2 [e], p e [1] S4 [s], [p], [nr] e [1] S5 [s], [p], [r] e [1] S8 [d], [p] e [1] S11 [x], [p] e [1] 24000 [p] e [2] HY010 [np]|Vedere la tabella degli stati cursore|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 [o]|  
  
 [1] Il risultato corrente è l'ultimo o unico risultato, o non ci sono risultati correnti. Per ulteriori informazioni su più risultati, vedere [Risultati multipli](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2] Il risultato corrente non è l'ultimo risultato.  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute (Stati preparati)  
  
|S2<br /><br /> Nessun risultato|S3<br /><br /> Risultati|  
|-----------------------|--------------------|  
|S4 [s] S8 [d] S11 [x]|S5 [s] S8 [d] S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute (stati cursore)  
  
|S5<br /><br /> Aperto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p], [1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [1] Questo errore viene restituito da Gestione Driver se **SQLFetch** o **SQLFetchScroll** non ha restituito SQL_NO_DATA e viene restituito dal driver se **SQLFetch** o **SQLFetchScroll** ha restituito SQL_NO_DATA.  
  
## <a name="sqlextendedfetch"></a>Sqlextendedfetch  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|S1010 (informazioni in stato in questo stato del sistema)|S1010 (informazioni in stato in questo stato del sistema)|24000|Vedi la tabella seguente|S1010 (informazioni in stato in questo stato del sistema)|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch (Cursor States)  
  
|S5<br /><br /> Aperto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] o [nf] S11 [x]|S1010 (informazioni in stato in questo stato del sistema)|-- [s] o [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch e SQLFetchScroll  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|24000|Vedi la tabella seguente|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch e SQLFetchScroll (stati cursore)  
  
|S5<br /><br /> Aperto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] o [nf] S11 [x]|-- [s] o [nf] S11 [x]|HY010 (Informazioni in stati incomMIino in|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|  
|IH [2]|S0|S0|S0|S0|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] Questa riga mostra le transizioni quando *HandleType* era SQL_HANDLE_ENV o SQL_HANDLE_DBC.  
  
 [2] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_STMT.  
  
 [3] Questa riga mostra le transizioni quando *HandleType* era SQL_HANDLE_DESC e il descrittore è stato allocato in modo esplicito.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 [np] S2 [p]|S1 [np] S3 [p]|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|  
|IH [2]|--|--|--|--|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|  
  
 [1] Questa riga mostra le transizioni quando *Option* era SQL_CLOSE.  
  
 [2] Questa riga mostra le transizioni quando *Option* è stata SQL_UNBIND o SQL_RESET_PARAMS. Se l'argomento *Option* è stato SQL_DROP e il driver sottostante è un driver ODBC 3 *.x,* Gestione Driver esegue il mapping di questo a una chiamata a **SQLFreeHandle** con *HandleType* impostato su SQL_HANDLE_STMT. Per ulteriori informazioni, vedere la tabella di transizione per [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|24000|Vedi la tabella seguente|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (Cursor States)  
  
|S5<br /><br /> Aperto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-- [s] o [nf] S11 [x] 24000 [b] HY109 [i]|-- [s] o [nf] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField e SQLGetDescRec  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|-- [1] o [2] HY010 [3]|Vedi la tabella seguente|-- [1] o [2] 24000 [3]|-- [1], [2] o [3] S11 [3] e [x]|HY010 (Informazioni in stati incomMIino in|NS [c] o [4] HY010 [o] e [5]|  
  
 [1] L'argomento *DescriptorHandle* era un APD o ARD.  
  
 [2] L'argomento *DescriptorHandle* era un IPD.  
  
 [3] L'argomento *DescriptorHandle* era un IRD.  
  
 [4] L'argomento *DescriptorHandle* era uguale all'argomento *DescriptorHandle* nella funzione **SQLGetDescField** o **SQLGetDescRec** in esecuzione in modo asincrono.  
  
 [5] L'argomento *DescriptorHandle* era diverso dall'argomento *DescriptorHandle* nella funzione **SQLGetDescField** o **SQLGetDescRec** in esecuzione in modo asincrono.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField e SQLGetDescRec (Stati preparati)  
  
|S2<br /><br /> Nessun risultato|S3<br /><br /> Risultati|  
|-----------------------|--------------------|  
|--[1], [2] o [3] S11[2] e [x]|--[1], [2] o [3] S11 [x]|  
  
 [1] L'argomento *DescriptorHandle* era un APD o ARD.  
  
 [2] L'argomento *DescriptorHandle* era un IPD.  
  
 [3] L'argomento *DescriptorHandle* era un IRD. Si noti che queste funzioni restituiscono sempre SQL_NO_DATA nello stato S2 quando *DescriptorHandle* era un IRD.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH[2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_DESC.  
  
 [2] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_STMT.  
  
 [3] **SQLGetDiagField** restituisce sempre un errore in questo stato quando *DiagIdentifier* è SQL_DIAG_ROW_COUNT.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr (Informazioni in lingua inglese)  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|Vedi la tabella seguente|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|  
  
 [1] L'attributo di istruzione non è stato SQL_ATTR_ROW_NUMBER.  
  
 [2] L'attributo di istruzione è stato SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (Stati cursore)  
  
|S5<br /><br /> Aperto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|--[1] o ([v] e [2]) 24000 [b] e [2] HY109 [i] e [2]|-- [i] o ([v] e [2]) 24000 [b] e [2] HY109[1] e [2]|  
  
 [1] L'argomento *Attributo* non era SQL_ATTR_ROW_NUMBER.  
  
 [2] L'argomento *Attributo* è stato SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|--[1]|--[1]|-- [s] e [2] S1 [nf], [np] e S2 [nf], [p] e [4] S5 [s] e [3] S11 [x]|S1 [nf], [np] e [4] S3 [nf], [p] e [4] S4 [s] e [2] S5 [s] e [3] S11 [x]|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 [o]|  
  
 [1] La funzione restituisce sempre SQL_NO_DATA in questo stato.  
  
 [2] Il risultato successivo è un conteggio delle righe.  
  
 [3] Il risultato successivo è un set di risultati.  
  
 [4] Il risultato attuale è l'ultimo risultato.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010 (Informazioni in stati incomMIino in|-- [s] S11 [x]|-- [s] S11 [x]|-- [s] S11 [x]|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010 (Informazioni in stati incomMIino in|-- [s] S11 [x]|-- [s] S11 [x]|-- [s] S11 [x]|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|Vedi la tabella seguente|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData (Need Data States)  
  
|S8 (in questo)<br /><br /> Dati di necessità|S9<br /><br /> Deve mettere|S10<br /><br /> Può mettere|  
|----------------------|---------------------|---------------------|  
|S1 [e] e [1] S2 [e], [nr] e [2] S3 [e], [r] e [2] S5 [e] e [4] S6 [e] e [5] S7 [e] e [3] S9 [d] S11 [x]|HY010 (Informazioni in stati incomMIino in|S1 [e] e [1] S2 [e], [nr] e [2] S3 [e], [r], e [2] S4 [s], [nr], e ([1] o [2]) S5 [s], [r] e ([1] o [2]) S5 ([s] o [e]) e [4] S6 ([s] o [e]) e [5] S7 ([s] o [e]) e [3] S9 [d] S1 [x] x1 x1|  
  
 [1] **SQLExecDirect** ha restituito SQL_NEED_DATA.  
  
 [2] **SQLExecute** ha restituito SQL_NEED_DATA.  
  
 [3] **SQLSetPos** era stato chiamato dallo stato S7 e ha restituito SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** era stato chiamato dallo stato S5 e ha restituito SQL_NEED_DATA.  
  
 [5] **SQLSetPos** o **SQLBulkOperations** era stato chiamato dallo stato S6 e restituito SQL_NEED_DATA.  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S2 [s] e [nr] S3 [s] e [r] S11 [x]|-- [s] o ([e] e [1]) S1 [e] e [2] S11 [x]|S1 [e] e [3] S2 [s], [nr] e S3 [s], [r] e [3] S11 [x] e [3] 24000[4]|Vedi la tabella seguente|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 [o]|  
  
 [1] La preparazione non riesce per un motivo diverso dalla convalida dell'istruzione (il SQLSTATE era HY009 [Valore argomento non valido] o HY090 [Stringa non valida o lunghezza del buffer]).  
  
 [2] La preparazione non riesce durante la convalida dell'istruzione (il SQLSTATE non era HY009 [Valore argomento non valido] o HY090 [Stringa non valida o lunghezza del buffer]).  
  
 [3] Il risultato corrente è l'ultimo o unico risultato, o non ci sono risultati correnti. Per ulteriori informazioni su più risultati, vedere [Risultati multipli](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4] Il risultato attuale non è l'ultimo risultato.  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare (stati cursore)  
  
|S5<br /><br /> Aperto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|Vedi la tabella seguente|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData (Need Data States)  
  
|S8 (in questo)<br /><br /> Dati di necessità|S9<br /><br /> Deve mettere|S10<br /><br /> Può mettere|  
|----------------------|---------------------|---------------------|  
|HY010 (Informazioni in stati incomMIino in|S1 [e] e [1] S2 [e], [nr] e [2] S3 [e], [r] e [2] S5 [e] e [4] S6 [e] e [5] S7 [e] e [3] S10 [s] S11 [x]|-- [s] S1 [e] e [1] S2 [e], [nr], e [2] S3 [e], [r], e S5 [e] e S6 [e] e [5] S7 [e] e [3] S11 [x] HY011[6]|  
  
 [1] **SQLExecDirect** ha restituito SQL_NEED_DATA.  
  
 [2] **SQLExecute** ha restituito SQL_NEED_DATA.  
  
 [3] **SQLSetPos** era stato chiamato dallo stato S7 e ha restituito SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** era stato chiamato dallo stato S5 e ha restituito SQL_NEED_DATA.  
  
 [5] **SQLSetPos** o **SQLBulkOperations** era stato chiamato dallo stato S6 e restituito SQL_NEED_DATA.  
  
 [6] Una o più chiamate a **SQLPutData** per un singolo parametro restituito SQL_SUCCESS, quindi è stata effettuata una chiamata a **SQLPutData** per lo stesso parametro con *StrLen_or_Ind* impostato su SQL_NULL_DATA.  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|  
  
 [1] Questa riga mostra le transizioni quando *Attribute* era un attributo di connessione. Per le transizioni quando *Attribute* era un attributo di istruzione, vedere la tabella di transizione delle istruzioni per **SQLSetStmtAttr**.  
  
 [2] L'argomento *Attributo* non era SQL_ATTR_CURRENT_CATALOG.  
  
 [3] L'argomento *Attributo* è stato SQL_ATTR_CURRENT_CATALOG.  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName (Nome cursore)  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|24000|24000|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField e SQLSetDescRec  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|  
  
 [1] Questa riga mostra le transizioni in cui l'argomento *DescriptorHandle* è un ARD, Un APD, un IPD o (per **SQLSetDescField)** un IRD quando l'argomento *FieldIdentifier* è SQL_DESC_ARRAY_STATUS_PTR o SQL_DESC_ROWS_PROCESSED_PTR. È un errore chiamare **SQLSetDescField** per un IRD quando *FieldIdentifier* è qualsiasi altro valore.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Ora di età che si addice|I01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|24000|Vedi la tabella seguente|HY010 (Informazioni in stati incomMIino in|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos (Cursor States)  
  
|S5<br /><br /> Aperto|S6<br /><br /> SQLFetch o SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-- [s] S8 [d] S11 [x] 24000 [b] HY109 [i]|-- [s] S8 [d] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> Non allocato|S1<br /><br /> Allocato|S2-S3<br /><br /> Prepared|S4<br /><br /> Eseguito|S5-S7<br /><br /> Cursore|S8-S10<br /><br /> Dati di necessità|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--[1] HY011[2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] o [1] HY011 [p] e [2]|HY010 [np] o [1] HY011 [p] e [2]|  
  
 [1] L'argomento *Attributo* non era SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE o SQL_ATTR_CURSOR_SENSITIVITY.  
  
 [2] L'argomento *Attributo* era SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE o SQL_ATTR_CURSOR_SENSITIVITY.
