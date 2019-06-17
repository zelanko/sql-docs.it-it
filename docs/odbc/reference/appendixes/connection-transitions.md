---
title: Transizioni di connessione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], connection
- connection transitions [ODBC]
- state transitions [ODBC], connection
ms.assetid: 6b6e1a47-4a52-41c8-bb9e-7ddeae09913e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f808460a1421a9ab4cb3a76c2810d810b9636b11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224512"
---
# <a name="connection-transitions"></a>Transizioni di connessione
Connessioni ODBC presentano gli stati seguenti.  
  
|State|Descrizione|  
|-----------|-----------------|  
|C0|Ambiente non allocato, non allocato connessione|  
|C1|Ambiente allocato, non allocato connessione|  
|C2|Ambiente di connessione allocato allocata|  
|C3|Funzione di connessione sono necessari dati|  
|C4|Connessione connessi|  
|C5|Connessione, allocate istruzione connesso|  
|C6|Connessione connessi, delle transazioni in corso. È possibile che una connessione sia nello stato C6 senza istruzioni allocate nella connessione. Si supponga, ad esempio, la connessione è in modalità di commit manuale e si trova in stato C4. Se un'istruzione viene allocata, esecuzione (avvio di una transazione) e quindi liberata, la transazione rimane attiva, ma sono presenti istruzioni per la connessione.|  
  
 Le tabelle seguenti mostrano come ogni funzione ODBC riguarda lo stato della connessione.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> Nessun Env.|C1 non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1[1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)[2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)[3]|(IH)|(08003)|(08003)|C5|--[5]|--[5]|  
|(IH)[4]|(IH)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_STMT.  
  
 [4] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DESC.  
  
 [5] chiamante **SQLAllocHandle** con *OutputHandlePtr* che punta a un handle valido sovrascrive tale handle senza tener conto per l'handle di ofthat contenuto precedente e può causare problemi per i driver ODBC. Si tratta di programmazione di applicazioni ODBC non corretta per chiamare **SQLAllocHandle** due volte alla stessa variabile di applicazione definita per  *\*OutputHandlePtr* senza chiamare  **SQLFreeHandle** per liberare l'handle prima la riallocazione. Sovrascrittura ODBC gli handle in questo modo possono causare un comportamento non coerente o errori da parte dei driver ODBC.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C3 [d] C4 [s]|-[d] C2 C4 [e] [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--[1] C5[2]|  
  
 [1] la connessione è in modalità di commit manuale.  
  
 [2] la connessione era in modalità autocommit.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges e SQLTables  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] la connessione non è in modalità autocommit o l'origine dati non è iniziato una transazione.  
  
 [2] la connessione non è in modalità di commit manuale e l'origine dati ha iniziato una transazione.  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc, SQLGetDescField, SQLGetDescRec, SQLSetDescField and SQLSetDescRec  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|--[1]|--|--|  
  
 [1] in questo stato, i descrittori soli disponibili per l'applicazione vengono allocati in modo esplicito i descrittori.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4 s -- n[f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|--[3]|--[3]|--[3]|--|--|: [4] o ([5], [6] e [8]) C4 [5] e [7] C5 [5], [6] e [9]|  
|(IH)[2]|(IH)|(08003)|(08003)|--|--|C5|  
  
 [1] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] perché la connessione non è in uno stato di connessione, è interessato dalla transazione.  
  
 [4] la connessione non riuscito il commit o rollback. La funzione restituisce SQL_ERROR in questo caso.  
  
 [5] il commit o rollback ha avuto esito positivo della connessione. La funzione restituisce SQL_ERROR se il commit o il rollback non riuscita in un'altra connessione o la funzione restituisce SQL_SUCCESS se il commit o il rollback ha avuto esito positivo su tutte le connessioni.  
  
 [6] si è verificato almeno un'istruzione allocata per la connessione.  
  
 [7] non esistevano alcun istruzioni allocate nella connessione.  
  
 [8] la connessione ha almeno una sola istruzione per il quale si era un cursore aperto, e l'origine dati consente di mantenere i cursori quando le transazioni vengono eseguito il commit o rollback, a seconda di quale si applica (a seconda che *CompletionType* era SQL _ COMMIT o SQL_ROLLBACK). Per altre informazioni, vedere gli attributi SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 [9] se la connessione ha tutte le istruzioni per il quale si sono verificati i cursori aperti, i cursori non sono stati mantenuti quando è stato eseguito il commit o il rollback della transazione.  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect e SQLExecute  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2] C6[3]|--|  
  
 [1] la connessione non è in modalità autocommit e dell'esecuzione dell'istruzione non è un *cursore* *specifica* (ad esempio, un'istruzione SELECT); o la connessione è in modalità di commit manuale e l'istruzione esecuzione non è iniziato una transazione.  
  
 [2] la connessione è in modalità autocommit e dell'esecuzione dell'istruzione è un' *cursore* *specification* (ad esempio, un'istruzione SELECT).  
  
 [3] della connessione è in modalità di commit manuale e l'origine dati ha iniziato una transazione.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH)[2]|(IH)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH)[3]|(IH)|(IH)|(IH)|(IH)|C4[5] --[6]|-C4 [7] [5] e [8] C5 [6] e [8]|  
|(IH)[4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_STMT.  
  
 [4] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DESC.  
  
 [5] si è verificato solo di un'istruzione allocata per la connessione.  
  
 [6] si sono verificati più istruzioni allocate nella connessione.  
  
 [7] la connessione è in modalità di commit manuale.  
  
 [8] la connessione era in modalità autocommit.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|(IH)|(IH)|(IH)|(IH)|--|C5[3] --[4]|  
|(IH)[2]|(IH)|(IH)|(IH)|(IH)|--|--|  
  
 [1] questa riga Mostra le transazioni quando il *opzione* argomento è SQL_CLOSE.  
  
 [2] questa riga Mostra le transazioni quando il *opzione* argomento è SQL_UNBIND o SQL_RESET_PARAMS.  
  
 [3] la connessione non è in modalità autocommit e non i cursori sono stati aperti sulle istruzioni ad eccezione di questo.  
  
 [4] la connessione è in modalità di commit manuale, o era in modalità autocommit e un cursore è stato aperto in almeno un'altra istruzione.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--|--|--|  
  
 [1] il *attributo* argomento era SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE o SQL_ATTR_TRACEFILE o fosse stato impostato un valore per l'attributo di connessione.  
  
 [2] il *attributo* argomento non era SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE o SQL_ATTR_TRACEFILE e non era stato impostato un valore per la connessione attributo.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagRec e SQLGetDiagField  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|--|--|--|--|--|--|  
|(IH)[2]|(IH)|--|--|--|--|--|  
|(IH)[3]|(IH)|(IH)|(IH)|(IH)|--|--|  
|(IH)[4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_STMT.  
  
 [4] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|08003|--|--|--|  
  
 [1] il *InfoType* argomento era SQL_ODBC_VER.  
  
 [2] il *InfoType* argomento non era SQL_ODBC_VER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--[3] C5[1]|  
  
 [1] la connessione non è in modalità autocommit e la chiamata a **SQLMoreResults** l'elaborazione di un set di risultati di una specifica del cursore non è stato inizializzato.  
  
 [2] la connessione non è in modalità autocommit e la chiamata a **SQLMoreResults** ha inizializzato l'elaborazione di un set di risultati di una specifica del cursore.  
  
 [3] della connessione è in modalità di commit manuale.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] la connessione non è in modalità autocommit o l'origine dati non è iniziato una transazione.  
  
 [2] la connessione non è in modalità di commit manuale e l'origine dati ha iniziato una transazione.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--[3] 08002[4] HY011[5]|--[3] 08002[4] HY011[5]|: [3] e [6] C5 [8] 08002 HY011 [4] [5] o [7]|  
  
 [1] il *attributo* argomento non è stata SQL_ATTR_TRANSLATE_LIB o SQL_ATTR_TRANSLATE_OPTION.  
  
 [2] il *attributo* argomento era SQL_ATTR_TRANSLATE_LIB o SQL_ATTR_TRANSLATE_OPTION.  
  
 [3] il *attributo* argomento non è stata SQL_ATTR_ODBC_CURSORS o SQL_ATTR_PACKET_SIZE.  
  
 [4] di *attributo* argomento era SQL_ATTR_ODBC_CURSORS.  
  
 [5] il *attributo* argomento era SQL_ATTR_PACKET_SIZE.  
  
 [6] al *attributo* argomento non era SQL_ATTR_AUTOCOMMIT, o il *attributo* argomento era SQL_ATTR_AUTOCOMMIT e l'impostazione di questo attributo non il commit della transazione.  
  
 [7] al *attributo* argomento era SQL_ATTR_TXN_ISOLATION.  
  
 [8] al *attributo* argomento era SQL_ATTR_AUTOCOMMIT e l'impostazione di questo attributo eseguito il commit della transazione.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>Tutte le altre funzioni ODBC  
  
|C0<br /><br /> Nessun Env.|C1<br /><br /> Non allocato|C2<br /><br /> allocato|C3<br /><br /> Dati necessari|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--|
