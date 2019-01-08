---
title: Configurare il routing di sola lettura per un gruppo di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- read-only routing
- Availability Groups [SQL Server], readable secondary replicas
- Availability Groups [SQL Server], read-only routing
- readable secondary replicas
- Availability Groups [SQL Server], client connectivity
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 7bd89ddd-0403-4930-a5eb-3c78718533d4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3af17b9ee12846fc89e406420fa6405cb59e0af3
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367927"
---
# <a name="configure-read-only-routing-for-an-availability-group-sql-server"></a>Configurare il routing di sola lettura per un gruppo di disponibilità (SQL Server)
  Per configurare un gruppo di disponibilità AlwaysOn in modo da supportare il routing di sola lettura in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], è possibile utilizzare [!INCLUDE[tsql](../../../includes/tsql-md.md)] o PowerShell. Con *routing di sola lettura* si intende la capacità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di instradare le richieste di connessione in sola lettura valide a una [replica secondaria leggibile](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) AlwaysOn, ovvero una replica configurata per consentire carichi di lavoro di sola lettura quando viene eseguita nel ruolo secondario. Per supportare il routing di sola lettura, il gruppo di disponibilità deve possedere un [listener del gruppo di disponibilità](../../listeners-client-connectivity-application-failover.md). I client in sola lettura devono indirizzare le richieste di connessione al listener e le stringhe di connessione del client devono specificare la finalità dell'applicazione come in sola lettura, ovvero devono essere *richieste di connessione con finalità di lettura*.  
  
> [!NOTE]
>  Per informazioni su come configurare una replica secondaria leggibile, vedere [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md).  
> 
> 
> 
> [!NOTE]
>  La configurazione del routing di sola lettura non è supportata in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  

  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   È necessario che il gruppo di disponibilità disponga di un listener del gruppo di disponibilità. Per altre informazioni, vedere [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md).  
  
-   Uno o più repliche di disponibilità devono essere configurate per accettare di sola lettura nel ruolo secondario (vale a dire, sia [repliche secondarie leggibili](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)(AlwaysOn % 20Availability % 20Groups\)MD)). Per altre informazioni, vedere [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
-   È necessario essere connessi all'istanza del server che ospita la replica primaria corrente.  
  
###  <a name="RORReplicaProperties"></a> Proprietà della replica da configurare per il supporto del routing di sola lettura  
  
-   Per ogni replica secondaria leggibile che deve supportare il routing di sola lettura, è necessario specificare un *URL di routing di sola lettura*. L'URL viene usato solo quando la replica locale viene eseguita nel ruolo secondario. L'URL di routing di sola lettura deve essere specificato per ogni singola replica in base alle esigenze. Ogni URL di routing di sola lettura viene usato per il routing delle richieste di connessione con finalità di lettura a una replica secondaria leggibile specifica. In genere, a ogni replica secondaria leggibile viene assegnato un URL di routing di sola lettura.  
  
     Per informazioni sul calcolo dell'URL di routing di sola lettura per una replica di disponibilità, vedere [Calcolo di read_only_routing_url per AlwaysOn](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx).  
  
-   Per ogni replica di disponibilità che deve supportare il routing di sola lettura quando viene eseguita come replica primaria, è necessario specificare un *elenco di routing di sola lettura*. L'elenco di routing di sola lettura viene usato solo quando la replica locale viene eseguita nel ruolo primario. L'elenco deve essere specificato per ogni singola replica in base alle esigenze. In genere, ciascun elenco di routing di sola lettura deve contenere tutti gli URL di routing di sola lettura, con l'URL della replica locale alla fine dell'elenco.  
  
    > [!NOTE]  
    >  Le richieste di connessione con finalità di lettura vengono instradate alla prima replica secondaria leggibile disponibile nell'elenco di routing di sola lettura della replica primaria corrente. Non viene eseguito alcun bilanciamento del carico.  
  
> [!NOTE]  
>  Per informazioni sui listener del gruppo di disponibilità e altre informazioni sul routing di sola lettura, vedere [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
  
|Attività|Permissions|  
|----------|-----------------|  
|Per configurare le repliche durante la creazione di un gruppo di disponibilità|Sono necessarie l'appartenenza al ruolo predefinito del server **sysadmin** e l'autorizzazione server CREATE AVAILABILITY GROUP oppure l'autorizzazione ALTER ANY AVAILABILITY GROUP o CONTROL SERVER.|  
|Per modificare una replica di disponibilità|È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.|  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 **Per configurare il routing di sola lettura**  
  
> [!NOTE]  
>  Per un esempio di codice, vedere [Esempio (Transact-SQL)](#TsqlExample), più avanti in questa sezione.  
  
1.  Connettersi all'istanza del server che ospita la replica primaria.  
  
2.  Se si specifica una replica per un nuovo gruppo di disponibilità, usare l'istruzione [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Se si aggiunge o modifica una replica per un gruppo di disponibilità esistente, usare l'istruzione [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Per configurare il routing di sola lettura per il ruolo secondario, nella clausola ADD REPLICA o MODIFY REPLICA WITH specificare l'opzione SECONDARY_ROLE, come segue:  
  
         SECONDARY_ROLE **(** READ_ONLY_ROUTING_URL **='** TCP **://*`system-address`*:*`port`*')**  
  
         I parametri dell'URL del routing di sola lettura sono i seguenti:  
  
         *system-address*  
         Stringa, ad esempio un nome di sistema, un nome di dominio completo o un indirizzo IP, che identifica in modo univoco il computer di destinazione.  
  
         *port*  
         Numero di porta utilizzato dal motore di database dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
         Esempio:   `SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433')`  
  
         In una clausola MODIFY REPLICA l'argomento ALLOW_CONNECTIONS è facoltativo se la replica è già configurata per consentire connessioni in sola lettura.  
  
         Per ulteriori informazioni, vedere [Calcolo di Read_only_routing_url per AlwaysOn](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx).  
  
    -   Per configurare il routing di sola lettura per il ruolo primario, nella clausola ADD REPLICA o MODIFY REPLICA WITH specificare l'opzione PRIMARY_ROLE, come segue:  
  
         PRIMARY_ROLE **(** READ_ONLY_ROUTING_LIST **= ('*`server`*'** [ **,**... *n* ] **))**  
  
         dove *server* identifica un'istanza del server in cui viene ospitata una replica secondaria di sola lettura nel gruppo di disponibilità.  
  
         Esempio:   `PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('Server1','Server2'))`  
  
        > [!NOTE]  
        >  È necessario impostare l'URL del routing di sola lettura prima di configurare l'elenco di routing di sola lettura.  
  
###  <a name="TsqlExample"></a> Esempio (Transact-SQL)  
 Nell'esempio seguente vengono modificate due repliche di disponibilità di un gruppo di disponibilità esistente, `AG1` , per supportare il routing di sola lettura se a una di queste repliche è attualmente assegnato il ruolo primario. Per identificare le istanze del server che ospitano la replica di disponibilità, in questo esempio vengono specificati i nomi delle istanze, `COMPUTER01` e `COMPUTER02`.  
  
```  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER02.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER02','COMPUTER01')));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER01','COMPUTER02')));  
GO  
  
```  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
 **Per configurare il routing di sola lettura**  
  
> [!NOTE]  
>  Per un esempio di codice, vedere [Esempio (PowerShell)](#PSExample), più avanti in questa sezione.  
  
1.  Impostare il valore predefinito (`cd`) sull'istanza del server che ospita la replica primaria.  
  
2.  Quando si aggiunge una replica di disponibilità a un gruppo di disponibilità, utilizzare il cmdlet `New-SqlAvailabilityReplica`. Quando si modifica una replica di disponibilità esistente, utilizzare il cmdlet `Set-SqlAvailabilityReplica`. I parametri pertinenti sono i seguenti:  
  
    -   Per configurare il routing di sola lettura per il ruolo secondario, specificare il **ReadonlyRoutingConnectionUrl "*`url`*"** parametro.  
  
         dove *url* è il nome di dominio completo (FQDN) e la porta di connettività da usare in caso di routing alla replica per le connessioni di sola lettura. Esempio:  `-ReadonlyRoutingConnectionUrl "TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024"`  
  
         Per ulteriori informazioni, vedere [Calcolo di Read_only_routing_url per AlwaysOn](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx).  
  
    -   Per configurare l'accesso alla connessione per il ruolo primario, specificare **ReadonlyRoutingList "*`server`*"** [ **,**... *n* ], dove *server* identifica un'istanza del server che ospita una replica secondaria di sola lettura nel gruppo di disponibilità. Esempio:  `-ReadOnlyRoutingList "SecondaryServer","PrimaryServer"`  
  
        > [!NOTE]  
        >  È necessario impostare l'URL del routing di sola lettura di una replica prima di configurare il relativo elenco di routing di sola lettura.  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Visualizzare la Guida di SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
###  <a name="PSExample"></a> Esempio (PowerShell)  
 Nell'esempio seguente vengono configurate la replica primaria e una replica secondaria in un gruppo di disponibilità per il routing di sola lettura. Innanzi tutto, nell'esempio viene assegnato un URL di routing di sola lettura a ciascuna replica. L'elenco di routing di sola lettura viene quindi impostato sulla replica primaria. Le connessioni la cui proprietà "ReadOnly" è impostata nella stringa di connessione verranno reindirizzate alla replica secondaria. Se la replica secondaria non è leggibile (in base all'impostazione `ConnectionModeInSecondaryRole`), la connessione verrà nuovamente indirizzata alla replica primaria.  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
$secondaryReplica = Get-Item "AvailabilityReplicas\SecondaryServer"  
  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://PrimaryServer.domain.com:1433" -InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://SecondaryServer.domain.com:1433" -InputObject $secondaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingList "SecondaryServer","PrimaryServer" -InputObject $primaryReplica  
```  
  
##  <a name="FollowUp"></a> Completamento: Dopo la configurazione del routing di sola lettura  
 Una volta configurate la replica primaria corrente e le repliche secondarie leggibili per supportare il routing di sola lettura in entrambi i ruoli, le repliche secondarie leggibili potranno ricevere richieste di connessione con finalità di lettura dai client che si connettono tramite il listener del gruppo di disponibilità.  
  
> [!TIP]  
>  Quando si usa la [utilità bcp](../../../tools/bcp-utility.md) oppure [utilità sqlcmd](../../../tools/sqlcmd-utility.md), è possibile specificare l'accesso in lettura a qualsiasi replica secondaria abilitata per l'accesso di sola lettura specificando il `-K ReadOnly` passare.  
  
###  <a name="ConnStringReqsRecs"></a> Requisiti e indicazioni per le stringhe di connessione del client  
 Per consentire a un'applicazione client di utilizzare il routing di sola lettura, è necessario che la relativa stringa di connessione soddisfi i requisiti seguenti:  
  
-   Utilizzare il protocollo TCP.  
  
-   Impostare la proprietà o l'attributo della finalità dell'applicazione su readonly.  
  
-   Fare riferimento al listener di un gruppo di disponibilità configurato per supportare il routing di sola lettura.  
  
-   Fare riferimento a un database in tale gruppo di disponibilità.  
  
 È inoltre consigliabile che le stringhe di connessione consentano il failover su più subnet, che supporta un thread client parallelo per ogni replica in ogni subnet. In questo modo di riduce al minimo il tempo di riconnessione del client dopo un failover.  
  
 La sintassi per una stringa di connessione dipende dal provider SQL Server utilizzato da un'applicazione. Nella stringa di connessione di esempio seguente per il Provider di dati .NET Framework 4.0.2 per SQL Server sono illustrate le parti di una stringa di connessione necessarie e consigliate per il funzionamento del routing di sola lettura.  
  
```  
Server=tcp:MyAgListener,1433;Database=Db1;IntegratedSecurity=SSPI;ApplicationIntent=ReadOnly;MultiSubnetFailover=True  
```  
  
 Per altre informazioni sulla finalità dell'applicazione di sola lettura e sul routing di sola lettura, vedere [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
### <a name="if-read-only-routing-is-not-working-correctly"></a>Se il routing di sola lettura non funziona correttamente  
 Per informazioni sulla risoluzione dei problemi di una configurazione di routing di sola lettura, vedere [ Routing di sola lettura non funziona correttamente è](troubleshoot-always-on-availability-groups-configuration-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per visualizzare le configurazioni del routing di sola lettura**  
  
-   [sys.availability_read_only_routing_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
  
-   [sys.availability_replicas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql) (colonna **read_only_routing_url**)  
  
 **Per configurare l'accesso alla connessione client**  
  
-   [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
 **Per utilizzare stringhe di connessione nelle applicazioni**  
  
-   [Supporto di SQL Server Native Client per il ripristino di emergenza a disponibilità elevata](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   **Blog:**  
  
     [Calcolo di read_only_routing_url per AlwaysOn](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)  
  
     [SQL Server AlwaysOn Team blog: Il Team Blog ufficiale di SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Pagina relativa ai blog del Servizio Supporto Tecnico Clienti per gli ingegneri di SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **White paper:**  
  
     [Pagina relativa ai white paper Microsoft per SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Pagina relativa ai white paper del team di consulenza clienti di SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Repliche secondarie attive: Repliche secondarie leggibili (gruppi di disponibilità AlwaysOn)](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Informazioni sull'accesso alla connessione client per le repliche di disponibilità &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)  
  
  
