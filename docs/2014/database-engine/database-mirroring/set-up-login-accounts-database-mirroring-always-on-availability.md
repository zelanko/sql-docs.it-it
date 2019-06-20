---
title: Configurare gli account di accesso per il mirroring del Database o i gruppi di disponibilità AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- logins [SQL Server], database mirroring
ms.assetid: e9f5287b-1325-4cda-88a6-19eaaa52a652
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5fd397349bc3fa3ed7f69e9e1293415ea96fc75d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754316"
---
# <a name="set-up-login-accounts-for-database-mirroring-or-alwayson-availability-groups-sql-server"></a>Configurare gli account di accesso per il mirroring del database o i gruppi di disponibilità AlwaysOn (SQL Server)
  Affinché due istanze del server possano connettersi tra loro al punto dell' [endpoint del mirroring di database](the-database-mirroring-endpoint-sql-server.md) , è necessario che l'account di accesso di ognuna delle istanze possa accedere all'altra. e inoltre che disponga dell'autorizzazione per la connessione all'endpoint del mirroring del database dell'altra istanza.  
  
 L'impatto di questo requisito dipende dall'eventuale esecuzione delle istanze del server tramite lo stesso account utente di dominio:  
  
-   Se le istanze del server vengono eseguite con lo stesso account utente di dominio, gli account di accesso dell'utente corretti saranno disponibili automaticamente in entrambi i database **master** . Questa scelta semplifica la configurazione della sicurezza per il mirroring del database e i gruppi di disponibilità AlwaysOn.  
  
-   Se le istanze del server vengono eseguite con account utente diversi, gli account di accesso dell'utente nell'istanza del server in cui viene ospitato il server principale o la replica primaria devono essere riprodotti manualmente nell'istanza del server in cui viene ospitato il server mirror o in ogni istanza del server in cui viene ospitata una replica secondaria. Per ulteriori informazioni, vedere [Creare un account di accesso per un account diverso](#CreateLogin) e [Concedere l'autorizzazione di connessione](#GrantConnect)più avanti in questo argomento.  
  
    > [!IMPORTANT]  
    >  Per creare un ambiente più sicuro, provare a utilizzare account del dominio distinti per ogni istanza del server.  
  
##  <a name="CreateLogin"></a> Creare un account di accesso per un account diverso  
 Se due istanze del server vengono eseguite con account diversi, l'amministratore di sistema deve usare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE LOGIN per creare un accesso per l'account del servizio di avvio dell'istanza remota di ogni istanza del server. Per altre informazioni, vedere [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql).  
  
> [!IMPORTANT]  
>  Se si esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un account non di dominio, è necessario utilizzare i certificati. Per ulteriori informazioni, vedere [Utilizzare certificati per un endpoint del mirroring del database &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md).  
  
 Ad esempio, affinché l'istanza del server sqlA, eseguita con loginA, si connetta all'istanza del server sqlB, eseguita con loginB, è necessario che loginA sia presente in sqlB e che loginB sia presente in sqlA. In una sessione di mirroring del database che include un'istanza del server di controllo del mirroring (sqlC) e nella quale le tre istanze del server vengono eseguite con account di dominio diversi, è inoltre necessario creare gli account di accesso seguenti:  
  
|Istanza|Account di accesso da creare e ai quali concedere l'autorizzazione di connessione|  
|--------------------|--------------------------------------------------------------|  
|sqlA|sqlB e sqlC|  
|sqlB|sqlA e sqlC|  
|sqlC|sqlA e sqlB|  
  
> [!NOTE]  
>  Per connettersi all'account del servizio di rete, è possibile utilizzare l'account del computer anziché di un utente del dominio. Se si utilizza l'account del computer, è necessario aggiungerlo come utente nell'altra istanza del server.  
  
##  <a name="GrantConnect"></a> Concedere l'autorizzazione di connessione  
 Dopo avere creato un account di accesso in un'istanza del server, è necessario concedere a tale account l'autorizzazione a connettersi all'endpoint del mirroring del database dell'istanza del server. L'autorizzazione di connessione viene concessa dall'amministratore di sistema tramite un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] GRANT. Per altre informazioni, vedere [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Creare un account di accesso](../../relational-databases/security/authentication-access/create-a-login.md)  
  
-   [Concessione dell'accesso alla rete a un endpoint per il mirroring del database utilizzando l'autenticazione di Windows &#40;SQL Server&#41;](../database-mirroring-allow-network-access-windows-authentication.md).  
  
-   [Usare certificati per un endpoint del mirroring del database &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Endpoint del mirroring del database &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [Risolvere i problemi relativi alla configurazione del mirroring del database &#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)   
 [Risolvere i problemi di configurazione di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
