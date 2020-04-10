---
title: Pool di connessioni compatibile con il driver nel driver ODBC per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 455ab165-8e4d-4df9-a1d7-2b532bfd55d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f93f7f5a000016af3c20af08d9eb318851da8c48
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928304"
---
# <a name="driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server"></a>Pool di connessioni compatibile con il driver nel driver ODBC per SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Il driver ODBC per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta il [pool di connessioni compatibile con il driver](https://msdn.microsoft.com/library/hh405031(VS.85).aspx). In questo argomento vengono descritti i miglioramenti apportati al pool di connessioni compatibile con il driver in Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows:  
  
-   Indipendentemente dalle proprietà delle connessioni, le connessioni che usano `SQLDriverConnect` vengono inserite in un pool separato rispetto alle connessioni che usano `SQLConnect`.
- Quando si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e il pool di connessioni compatibile con il driver, il driver non usa il contesto di sicurezza dell'utente di Windows per il thread corrente per separare le connessioni nel pool. Ovvero, se le connessioni hanno parametri equivalenti negli scenari di rappresentazione di Windows con l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e usano le stesse credenziali dell'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per connettersi al back-end, diversi utenti di Windows possono potenzialmente usare lo stesso pool di connessioni. Quando si usa l'autenticazione di Windows e il pool di connessioni compatibile con il driver, il driver usa il contesto di sicurezza dell'utente corrente di Windows per separare le connessioni nel pool. Ovvero, per gli scenari di rappresentazione di Windows, diversi utenti di Windows non condividono le connessioni anche se le connessioni usano gli stessi parametri.
- Quando si usa Azure Active Directory e il pool di connessioni compatibile con il driver, il driver usa anche il valore di autenticazione per determinare l'appartenenza al pool di connessioni.
  
-   Il pool di connessioni compatibile con il driver impedisce la restituzione di una connessione non valida dal pool.  
  
-   Il pool di connessioni compatibile con il driver riconosce gli attributi di connessione specifici del driver. Pertanto, se una connessione usa `SQL_COPT_SS_APPLICATION_INTENT` impostato su sola lettura, tale connessione ottiene il proprio pool di connessioni.
-   Impostando l'attributo `SQL_COPT_SS_ACCESS_TOKEN` viene creato un pool di connessioni separatamente. 
  
Se uno dei seguenti ID dell'attributo di connessione o delle seguenti parole chiave della stringa di connessione differisce tra la stringa di connessione e la stringa di connessione in pool, il driver usa una connessione in pool. Tuttavia, le prestazioni sono migliori se tutti gli ID dell'attributo di connessione o tutte le parole chiave della stringa di connessione corrispondono. (Per abbinare una connessione a una connessione in pool, il driver reimposta l'attributo.) Le prestazioni diminuiscono perché la reimpostazione dei parametri seguenti rende necessaria una chiamata di rete aggiuntiva.  
  
-    Se due o più dei seguenti attributi o delle seguenti parole chiave della connessione differiscono, non verrà usata una connessione in pool.  
  
  - `Language`  
  - `QuoteId`  
  - `SQL_ATTR_TXN_ISOLATION` 
  - `SQL_COPT_SS_QUOTED_IDENT`  
  
-   Se è presente una differenza in una qualsiasi delle seguenti parole chiave tra la stringa di connessione e una stringa di connessione in pool, non verrà usata una connessione in pool.  
  
    |Parola chiave|Driver ODBC 13|Driver ODBC 11|
    |-|-|-|
    |`Address`|Sì|Sì|
    |`AnsiNPW`|Sì|Sì|
    |`App`|Sì|Sì|
    |`ApplicationIntent`|Sì|Sì|  
    |`Authentication`|Sì|No|
    |`ColumnEncryption`|Sì|No|
    |`Database`|Sì|Sì|
    |`Encrypt`|Sì|Sì|  
    |`Failover_Partner`|Sì|Sì|
    |`FailoverPartnerSPN`|Sì|Sì|
    |`MARS_Connection`|Sì|Sì|
    |`Network`|Sì|Sì|
    |`PWD`|Sì|Sì|
    |`Server`|Sì|Sì|
    |`ServerSPN`|Sì|Sì|
    |`TransparentNetworkIPResolution`|Sì|Sì|
    |`Trusted_Connection`|Sì|Sì|
    |`TrustServerCertificate`|Sì|Sì|
    |`UID`|Sì|Sì|
    |`WSID`|Sì|Sì|
    
- Se è presente una differenza in uno qualsiasi dei seguenti attributi di connessione tra la stringa di connessione e una stringa di connessione in pool, non verrà usata una connessione in pool.  
  
    |Attributo|Driver ODBC 13|Driver ODBC 11|  
    |-|-|-|  
    |`SQL_ATTR_CURRENT_CATALOG`|Sì|Sì|
    |`SQL_ATTR_PACKET_SIZE`|Sì|Sì|
    |`SQL_COPT_SS_ANSI_NPW`|Sì|Sì|
    |`SQL_COPT_SS_ACCESS_TOKEN`|Sì|No|
    |`SQL_COPT_SS_AUTHENTICATION`|Sì|No|
    |`SQL_COPT_SS_ATTACHDBFILENAME`|Sì|Sì|
    |`SQL_COPT_SS_BCP`|Sì|Sì|
    |`SQL_COPT_SS_COLUMN_ENCRYPTION`|Sì|No|
    |`SQL_COPT_SS_CONCAT_NULL`|Sì|Sì|
    |`SQL_COPT_SS_ENCRYPT`|Sì|Sì|
    |`SQL_COPT_SS_FAILOVER_PARTNER`|Sì|Sì|
    |`SQL_COPT_SS_FAILOVER_PARTNER_SPN`|Sì|Sì|
    |`SQL_COPT_SS_INTEGRATED_SECURITY`|Sì|Sì|
    |`SQL_COPT_SS_MARS_ENABLED`|Sì|Sì|
    |`SQL_COPT_SS_OLDPWD`|Sì|Sì|
    |`SQL_COPT_SS_SERVER_SPN`|Sì|Sì|
    |`SQL_COPT_SS_TRUST_SERVER_CERTIFICATE`|Sì|Sì|
    |`SSPROP_AUTH_REPL_SERVER_NAME`|Sì|Sì|
    |`SQL_COPT_SS_TNIR`|Sì|No|
 
-   Il driver può ripristinare e modificare le seguenti parole chiave e i seguenti attributi di connessione senza effettuare una chiamata di rete aggiuntiva. Il driver reimposta i parametri seguenti per assicurarsi che la connessione non contenga informazioni non corrette.  
  
     Queste parole chiave della connessione non vengono prese in considerazione quando Gestione driver tenta di abbinare la connessione a una connessione in pool. (Anche modificando uno di questi parametri, una connessione esistente può essere riusata. Il driver reimposterà le opzioni in base alla necessità.) Questi attributi possono essere reimpostati sul lato client senza effettuare una chiamata di rete aggiuntiva.  
  
    |Parola chiave|Driver ODBC 13|Driver ODBC 11|  
    |-|-|-|  
    |`AutoTranslate`|Sì|Sì|
    |`Description`|Sì|Sì|
    |`MultisubnetFailover`|Sì|Sì|  
    |`QueryLog_On`|Sì|Sì|
    |`QueryLogFile`|Sì|Sì|
    |`QueryLogTime`|Sì|Sì|
    |`Regional`|Sì|Sì|
    |`StatsLog_On`|Sì|Sì|
    |`StatsLogFile`|  Sì|Sì|
  
     Modificando uno dei seguenti attributi di connessione, sarà comunque possibile riusare una connessione esistente.  Il driver reimposterà il valore in base alla necessità. Il driver può reimpostare questi attributi nel client senza effettuare una chiamata di rete aggiuntiva.  
  
    |Attributo|Driver ODBC 13|Driver ODBC 11|  
    |-|-|-|  
    |Tutti gli attributi di istruzione|Sì|Sì|
    |`SQL_ATTR_AUTOCOMMIT`|Sì|Sì|
    |`SQL_ATTR_CONNECTION_TIMEOUT`|  Sì|Sì|
    |`SQL_ATTR_DISCONNECT_BEHAVIOR SQL_ATTR_CONNECTION_TIMEOUT`|Sì|Sì|
    |`SQL_ATTR_LOGIN_TIMEOUT`|Sì|Sì|
    |`SQL_ATTR_ODBC_CURSORS`|  Sì|Sì|
    |`SQL_COPT_SS_PERF_DATA`|Sì|Sì|
    |`SQL_COPT_SS_PERF_DATA_LOG`|Sì|Sì|
    |`SQL_COPT_SS_PERF_DATA_LOG_NOW`| Sì|Sì| 
    |`SQL_COPT_SS_PERF_QUERY`|Sì|Sì|
    |`SQL_COPT_SS_PERF_QUERY_INTERVAL`|Sì|Sì|
    |`SQL_COPT_SS_PERF_QUERY_LOG`|  Sì|Sì|
    |`SQL_COPT_SS_PRESERVE_CURSORS`|Sì|Sì|
    |`SQL_COPT_SS_TRANSLATE`|Sì|Sì|
    |`SQL_COPT_SS_USER_DATA`|  Sì|Sì|
    |`SQL_COPT_SS_WARN_ON_CP_ERROR`|Sì|Sì|  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft ODBC Driver for SQL Server in Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
