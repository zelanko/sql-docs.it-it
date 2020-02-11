---
title: Service Broker con Gruppi di disponibilità AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Service Broker, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 881c20e5-1c99-44eb-b393-09fc5ea0f122
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fdf98d461039c5c6fb4f25c8cdf543422e5a0a2c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62788531"
---
# <a name="service-broker-with-alwayson-availability-groups-sql-server"></a>Service Broker con i gruppi di disponibilità AlwaysOn (SQL Server)
  In questo argomento sono contenute informazioni sulla configurazione di Service Broker per poter utilizzarlo con i [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 **Contenuto dell'argomento:**  
  
-   [Requisiti per un servizio in un gruppo di disponibilità per la ricezione di messaggi remoti](#ReceiveRemoteMessages)  
  
-   [Requisiti per l'invio di messaggi a un servizio remoto in un gruppo di disponibilità](#SendRemoteMessages)  
  
##  <a name="ReceiveRemoteMessages"></a>Requisiti per un servizio in un gruppo di disponibilità per la ricezione di messaggi remoti  
  
1.  **Verificare che il gruppo di disponibilità disponga di un listener.**  
  
     Per altre informazioni, vedere [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md).  
  
2.  **Verificare che l'endpoint Service Broker esista e che sia configurato correttamente.**  
  
     In ogni istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui è ospitata una replica di disponibilità per il gruppo di disponibilità, configurare l'endpoint di Service Broker come riportato di seguito:  
  
    -   Impostare LISTENER_IP su 'ALL'. Con questa impostazione vengono abilitate le connessioni in qualsiasi indirizzo IP valido associato al listener del gruppo di disponibilità.  
  
    -   Impostare la porta di Service Broker sullo stesso numero di porta in tutte le istanze del server host.  
  
        > [!TIP]  
        >  Per visualizzare il numero di porta dell'endpoint di Service Broker in un'istanza del server specifica, eseguire una query sulla colonna **port** della vista del catalogo [sys.tcp_endpoints](/sql/relational-databases/system-catalog-views/sys-tcp-endpoints-transact-sql) , dove **type_desc** = 'SERVICE_BROKER'.  
  
     Nell'esempio seguente viene creato un endpoint di Service Broker con autenticazione di Windows in cui viene utilizzata la porta predefinita di Service Broker (4022) e si è in ascolto di tutti gli indirizzi IP validi.  
  
    ```  
    CREATE ENDPOINT [SSBEndpoint]  
        STATE = STARTED  
        AS TCP  (LISTENER_PORT = 4022, LISTENER_IP = ALL )  
        FOR SERVICE_BROKER (AUTHENTICATION = WINDOWS)  
    ```  
  
     Per altre informazioni, vedere [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql).  
  
3.  **Concedere l'autorizzazione CONNECT per l'endpoint.**  
  
     Concedere l'autorizzazione CONNECT per l'endpoint di Service Broker al ruolo PUBLIC o a un account di accesso.  
  
     Nell'esempio seguente viene concessa la connessione in un endpoint di Service Broker denominato `broker_endpoint` al ruolo PUBLIC.  
  
    ```  
    GRANT CONNECT ON ENDPOINT::[broker_endpoint] TO [PUBLIC]  
    ```  
  
     Per altre informazioni, vedere [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql).  
  
4.  **Assicurarsi che msdb contenga una route AutoCreatedLocal o una route per il servizio specifico.**  
  
    > [!NOTE]  
    >  Per impostazione predefinita, tutti i database utente, incluso **msdb**, contengono la route **AutoCreatedLocal**. Questa route corrisponde a qualsiasi nome di servizio e istanza di Service Broker e, tramite essa, viene specificato che il messaggio deve essere recapitato all'interno dell'istanza corrente. **AutoCreatedLocal** ha una priorità inferiore rispetto alle route che specificano in modo esplicito un servizio specifico che comunica con un'istanza remota.  
  
     Per informazioni sulla creazione di route, vedere [Esempi di routing di Service Broker](https://msdn.microsoft.com/library/ms166090\(SQL.105\).aspx) nella versione [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] della documentazione online e [CREATE ROUTE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-route-transact-sql).  
  
##  <a name="SendRemoteMessages"></a>Requisiti per l'invio di messaggi a un servizio remoto in un gruppo di disponibilità  
  
1.  **Creare una route per il servizio di destinazione.**  
  
     Configurare la route come riportato di seguito:  
  
    -   Impostare ADDRESS sull'indirizzo IP del listener del gruppo di disponibilità in cui è ospitato il database del servizio.  
  
    -   Impostare PORT sulla porta specificata nell'endpoint di Service Broker di ogni istanza remota di SQL Server.  
  
     Nell'esempio seguente viene creata una route denominata `RouteToTargetService` per il servizio `ISBNLookupRequestService` . La route è destinata al listener del gruppo di disponibilità, `MyAgListener`, da cui viene utilizzata la porta 4022.  
  
    ```  
    CREATE ROUTE [RouteToTargetService] WITH   
    SERVICE_NAME = 'ISBNLookupRequestService',   
    ADDRESS = 'TCP://MyAgListener:4022';  
  
    ```  
  
     Per altre informazioni, vedere [CREATE ROUTE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-route-transact-sql).  
  
2.  **Assicurarsi che msdb contenga una route AutoCreatedLocal o una route per il servizio specifico.** Per altre informazioni, vedere [Requisiti necessari affinché i messaggi remoti vengano ricevuti da un servizio in un gruppo di disponibilità](#ReceiveRemoteMessages)più indietro in questo argomento.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
-   [CREARE una ROUTE &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-route-transact-sql)  
  
-   [CONCEDERE &#40;&#41;Transact-SQL](/sql/t-sql/statements/grant-transact-sql)  
  
-   [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md).  
  
-   [Creazione e configurazione di gruppi di disponibilità &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Configurare gli account di accesso per il mirroring del database o Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [SQL Server Service Broker](../../configure-windows/sql-server-service-broker.md)  
  
  
