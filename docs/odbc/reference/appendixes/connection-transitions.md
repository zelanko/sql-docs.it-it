---
title: Transizioni di connessione Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 225f8517a78f8e9d4d765163649da174d72e490c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284771"
---
# <a name="connection-transitions"></a>Transizioni di connessione
Le connessioni ODBC hanno i seguenti stati.  
  
|State|Descrizione|  
|-----------|-----------------|  
|C0|Ambiente non allocato, connessione non allocata|  
|C1|Ambiente allocato, connessione non allocata|  
|C2|Ambiente allocato, connessione allocata|  
|C3|La funzione di connessione richiede dati|  
|C4|Connessione connessa|  
|C5|Connessione collegata, istruzione allocata|  
|C6|Connessione connessa, transazione in corso. È possibile che una connessione sia nello stato C6 senza istruzioni allocate nella connessione. Si supponga, ad esempio, che la connessione sia in modalità di commit manuale e sia in stato C4. Se un'istruzione viene allocata, eseguita (avvio di una transazione) e quindi liberata, la transazione rimane attiva ma non sono presenti istruzioni sulla connessione.|  
  
 Nelle tabelle seguenti viene illustrato come ogni funzione ODBC influisce sullo stato della connessione.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> Niente Env.|C1 Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1[1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH) [2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH) [3]|(IH)|(08003)|(08003)|C5|--[5]|--[5]|  
|(IH) [4]|(IH)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 [2] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC.  
  
 [3] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_STMT.  
  
 Questa riga mostra le transizioni quando *HandleType* era SQL_HANDLE_DESC.  
  
 [5] La chiamata a **SQLAllocHandle** con *OutputHandlePtr* che punta a un handle valido sovrascrive tale handle indipendentemente dal contenuto precedente di tale handle e potrebbe causare problemi per i driver ODBC. Programmazione dell'applicazione ODBC non è corretta per chiamare **SQLAllocHandle** due volte con la stessa variabile di applicazione definita per * \*OutputHandlePtr* senza chiamare **SQLFreeHandle** per liberare l'handle prima di riallocherlo. La sovrascrittura degli handle ODBC in questo modo può causare un comportamento o errori incoerenti da parte dei driver ODBC.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C3 [d] C4 [s]|-- [d] C2 [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--[1] C5[2]|  
  
 [1] La connessione era in modalità manuale-commit.  
  
 [2] La connessione era in modalità auto-commit.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges e SQLTables  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] La connessione era in modalità autocommit o l'origine dati non ha avviato una transazione.  
  
 [2] La connessione era in modalità di commit manuale e l'origine dati ha iniziato una transazione.  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc, SQLGetDescField, SQLGetDescRec, SQLSetDescField e SQLSetDescRec  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|--[1]|--|--|  
  
 [1] In questo stato, gli unici descrittori disponibili per l'applicazione sono esplicitamente assegnati descrittori.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>Sqldisconnect  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4 s -- n[f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|--[3]|--[3]|--[3]|--|--|--[4] o ([5], [6], e [8]) C4[5] e [7] C5[5], [6] e [9]|  
|(IH) [2]|(IH)|(08003)|(08003)|--|--|C5|  
  
 [1] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 [2] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC.  
  
 [3] Poiché la connessione non è in uno stato connesso, non viene influenzata dalla transazione.  
  
 [4] Il commit o il rollback non è riuscito nella connessione. In questo caso, la funzione restituisce SQL_ERROR.  
  
 [5] Il commit o rollback ha avuto esito positivo sulla connessione. La funzione restituisce SQL_ERROR se il commit o il rollback non è riuscito su un'altra connessione o se la funzione restituisce SQL_SUCCESS se il commit o il rollback ha avuto esito positivo su tutte le connessioni.  
  
 [6] C'era almeno un'istruzione assegnata sulla connessione.  
  
 [7] Non c'erano dichiarazioni allocate sulla connessione.  
  
 [8] La connessione disponeva di almeno un'istruzione per la quale era presente un cursore aperto e l'origine dati mantiene i cursori quando viene eseguito il commit o il rollback delle transazioni, a seconda dell'applicazione di *Completion SQL_COMMITType* o di SQL_ROLLBACK). Per ulteriori informazioni, vedere gli attributi SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR in [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 [9] Se la connessione aveva istruzioni per le quali erano presenti cursori aperti, i cursori non venivano mantenuti quando fu eseguito il commit o il rollback della transazione.  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect e SQLExecute  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2] C6[3]|--|  
  
 [1] La connessione era in modalità autocommit e l'istruzione eseguita non era una *specifica* del *cursore* (ad esempio un'istruzione SELECT); o la connessione era in modalità di commit manuale e l'istruzione eseguita non ha avviato una transazione.  
  
 [2] La connessione era in modalità autocommit e l'istruzione eseguita era una *specifica* del *cursore* (ad esempio un'istruzione SELECT).  
  
 [3] La connessione era in modalità di commit manuale e l'origine dati ha iniziato una transazione.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH) [2]|(IH)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH) [3]|(IH)|(IH)|(IH)|(IH)|C4[5] --[6]|--[7] C4[5] e [8] C5[6] e [8]|  
|(IH) [4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 [2] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC.  
  
 [3] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_STMT.  
  
 Questa riga mostra le transizioni quando *HandleType* era SQL_HANDLE_DESC.  
  
 [5] C'era solo una dichiarazione allocata sulla connessione.  
  
 [6] C'erano più dichiarazioni allocate sulla connessione.  
  
 [7] La connessione era in modalità manuale-commit.  
  
 [8] La connessione era in modalità auto-commit.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|(IH)|(IH)|(IH)|(IH)|--|C5[3] --[4]|  
|(IH) [2]|(IH)|(IH)|(IH)|(IH)|--|--|  
  
 [1] Questa riga mostra le transazioni quando l'argomento *Option* è SQL_CLOSE.  
  
 [2] Questa riga mostra le transazioni quando l'argomento *Option* è SQL_UNBIND o SQL_RESET_PARAMS.  
  
 [3] La connessione era in modalità auto-commit e nessun cursore era aperto su alcuna istruzione tranne questa.  
  
 [4] La connessione era in modalità di commit manuale, oppure era in modalità di commit automatico e un cursore era aperto su almeno un'altra istruzione.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|--[1] 08003[2]|HY010 (Informazioni in stati incomMIino in|--|--|--|  
  
 [1] L'argomento *Attributo* è stato SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE o SQL_ATTR_TRACEFILE oppure è stato impostato un valore per l'attributo di connessione.  
  
 [2] L'argomento *Attributo* non era SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE o SQL_ATTR_TRACEFILE e non era stato impostato un valore per l'attributo di connessione.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|--|--|--|--|--|--|  
|(IH) [2]|(IH)|--|--|--|--|--|  
|(IH) [3]|(IH)|(IH)|(IH)|(IH)|--|--|  
|(IH) [4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 [2] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC.  
  
 [3] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_STMT.  
  
 Questa riga mostra le transizioni quando *HandleType* era SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr (Informazioni in lingua inglese)  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|HY010 (Informazioni in stati incomMIino in|HY010 (Informazioni in stati incomMIino in|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|--[1] 08003[2]|08003|--|--|--|  
  
 [1] L'argomento *InfoType* è stato SQL_ODBC_VER.  
  
 [2] L'argomento *InfoType* non è stato SQL_ODBC_VER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--[3] C5[1]|  
  
 [1] La connessione era in modalità di commit automatico e la chiamata a **SQLMoreResults** non ha inizializzato l'elaborazione di un set di risultati di una specifica del cursore.  
  
 [2] La connessione era in modalità di commit automatico e la chiamata a **SQLMoreResults** ha inizializzato l'elaborazione di un set di risultati di una specifica di cursore.  
  
 [3] La connessione era in modalità manuale-commit.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] La connessione era in modalità autocommit o l'origine dati non ha avviato una transazione.  
  
 [2] La connessione era in modalità di commit manuale e l'origine dati ha iniziato una transazione.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|--[1] 08003[2]|HY010 (Informazioni in stati incomMIino in|--[3] 08002[4] hy011[5]|--[3] 08002[4] hy011[5]|--[3] e [6] C5[8] 08002[4] HY011[5] o [7]|  
  
 [1] L'argomento *Attributo* non era SQL_ATTR_TRANSLATE_LIB o SQL_ATTR_TRANSLATE_OPTION.  
  
 [2] L'argomento *Attributo* è stato SQL_ATTR_TRANSLATE_LIB o SQL_ATTR_TRANSLATE_OPTION.  
  
 [3] L'argomento *Attributo* non era SQL_ATTR_ODBC_CURSORS o SQL_ATTR_PACKET_SIZE.  
  
 [4] L'argomento *Attributo* è stato SQL_ATTR_ODBC_CURSORS.  
  
 [5] L'argomento *Attributo* è stato SQL_ATTR_PACKET_SIZE.  
  
 [6] L'argomento *Attributo* non era SQL_ATTR_AUTOCOMMIT, o l'argomento *Attributo* era SQL_ATTR_AUTOCOMMIT e l'impostazione di questo attributo non ha eseguito il commit della transazione.  
  
 [7] L'argomento *Attributo* è stato SQL_ATTR_TXN_ISOLATION.  
  
 [8] L'argomento *Attributo* è stato SQL_ATTR_AUTOCOMMIT e l'impostazione di questo attributo ha eseguito il commit della transazione.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>Tutte le altre funzioni ODBC  
  
|C0<br /><br /> Niente Env.|C1<br /><br /> Non allocato|C2<br /><br /> Allocato|C3<br /><br /> Dati di necessità|C4<br /><br /> Connesso|C5<br /><br /> .|C6<br /><br /> Transazione|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--|
