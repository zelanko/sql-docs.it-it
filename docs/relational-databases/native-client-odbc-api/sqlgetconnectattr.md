---
title: Proprietà SQLGetConnectAttr . Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetConnectAttr function
ms.assetid: 26e4e69a-44fd-45e3-b47a-ae39184f041b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 590d47d65ab3893dbc9eefc3facd224671668378
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302151"
---
# <a name="sqlgetconnectattr"></a>SQLGetConnectAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client definisce gli attributi di connessione specifici del driver. Alcuni degli attributi sono disponibili per **SQLGetConnectAttr**e la funzione viene utilizzata per segnalare le impostazioni correnti. I valori riportati per questi attributi non sono garantiti fino a dopo che è stata stabilita una connessione o l'attributo è stato impostato utilizzando [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 In questo argomento sono elencati gli attributi di sola lettura. Per informazioni sugli [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] altri attributi di connessione specifici del driver ODBC di Native Client, vedere [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
## <a name="sql_copt_ss_connection_dead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 L'attributo SQL_COPT_SS_CONNECTION_DEAD consente di segnalare lo stato di una connessione a un server. Il driver esegue query sulla rete al fine di individuare lo stato corrente della connessione.  
  
> [!NOTE]  
>  L'attributo di connessione ODBC standard SQL_COPT_SS_CONNECTION_DEAD restituisce lo stato più recente della connessione. Tale stato potrebbe non essere quello corrente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|SQL_CD_TRUE|La connessione al server è stata persa.|  
|SQL_CD_FALSE|La connessione è aperta e disponibile per l'elaborazione di istruzioni.|  
  
## <a name="sql_copt_ss_client_connection_id"></a>SQL_COPT_SS_CLIENT_CONNECTION_ID  
 L'attributo SQL_COPT_SS_CLIENT_CONNECTION_ID consente di recuperare l'ID di connessione client che può essere utilizzato per individuare:  
  
-   Informazioni di diagnostica nel registro XEvents, se abilitato.  
  
-   Informazioni sull'errore di connessione nel buffer circolare della connessione.  
  
-   Informazioni di diagnostica nei registri di traccia di accesso ai dati, se abilitati.  
  
 Per ulteriori informazioni, vedere [Accesso alle informazioni di diagnostica nel registro eventi estesi](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
|valore|Descrizione|  
|-----------|-----------------|  
|SQL_ERROR|Connessione non riuscita.|  
|SQL_SUCCESS|Connessione attivata. L'ID di connessione client verrà trovato nel buffer di output.|  
  
## <a name="sql_copt_ss_perf_data"></a>SQL_COPT_SS_PERF_DATA  
 Tramite l'attributo SQL_COPT_SS_PERF_DATA viene restituito un puntatore a una struttura SQLPERF contenente le statistiche correnti sulle prestazioni del driver. **SQLGetConnectAttr** restituirà NULL se la registrazione delle prestazioni non è abilitata. Le statistiche nella struttura SQLPERF non vengono aggiornate in modo dinamico dal driver. Chiamare **SQLGetConnectAttr** ogni volta che è necessario aggiornare le statistiche sulle prestazioni.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|NULL|La registrazione delle prestazioni non è abilitata.|  
|Qualsiasi altro valore|Puntatore a una struttura SQLPERF.|  
  
## <a name="sql_copt_ss_perf_query"></a>SQL_COPT_SS_PERF_QUERY  
 L'attributo SQL_COPT_SS_PERF_QUERY restituisce TRUE se è abilitata la registrazione di query con esecuzione prolungata. La richiesta restituisce FALSE se la registrazione delle query non è attiva.  
  
## <a name="sql_copt_ss_user_data"></a>SQL_COPT_SS_USER_DATA  
 L'attributo SQL_COPT_SS_USER_DATA recupera il puntatore ai dati utente. I dati utente vengono archiviati nella memoria del client e registrati per singola connessione. Se il puntatore ai dati utente SQL_UD_NOTSET non è stato impostato, viene restituito un puntatore NULL.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|SQL_UD_NOTSET|Non è impostato alcun puntatore ai dati utente.|  
|Qualsiasi altro valore|Puntatore ai dati utente.|  
  
## <a name="sqlgetconnectattr-support-for-service-principal-names-spns"></a>Supporto di SQLSetConnectAttr per i nomi SPN (Service Principal Names)  
 SQLGetConnectAttr può essere utilizzato per eseguire query sul valore dei nuovi attributi di connessione SQL_COPT_SS_SERVER_SPN, SQL_COPT_SS_FAILOVER_PARTNER_SPN, SQL_COPT_SS_MUTUALLY_AUTHENTICATED e SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD. (SQLGetConnectOption può essere utilizzato anche per eseguire query su questi valori.)  
  
 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD è disponibile solo per connessioni aperte che utilizzano l'autenticazione di Windows.  
  
 Se non è stato impostato SQL_COPT_SS_SERVER_SPN o SQL_COPT_SS_FAILOVER_PARTNER, viene restituito il valore predefinito (una stringa vuota).  
  
 Per ulteriori informazioni sui nomi SPN, vedere [Nomi delle entità servizio &#40;nomi &#40;NOMI SPN&#41; in Connessioni client &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLGetConnectAttrSQLGetConnectAttr Function](https://go.microsoft.com/fwlink/?LinkId=59347)   
 [Dettagli di implementazione dell'API ODBCODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SET QUOTED_IDENTIFIER &#40;&#41;Transact-SQLSET](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [SET ANSI_NULLS &#40;transact-SQLTransact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;&#41;Transact-SQL](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
