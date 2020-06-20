---
title: Configurare l'accesso in sola lettura in una replica di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 22387419-22c4-43fa-851c-5fecec4b049b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ab13081396aff46d193c1b0449d6b93042ee60d6
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936959"
---
# <a name="configure-read-only-access-on-an-availability-replica-sql-server"></a>Configurare l'accesso in sola lettura in una replica di disponibilità (SQL Server)
  Per impostazione predefinita, gli accessi in lettura e scrittura e l'accesso con finalità di lettura sono entrambi consentiti alla replica primaria, ma alle repliche secondarie non sono consentite connessioni di un gruppo di disponibilità AlwaysOn. In questo argomento viene illustrato come configurare l'accesso alla connessione su una replica di disponibilità di un gruppo di disponibilità AlwaysOn in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell.  
  
 Per informazioni sulle implicazioni dell'abilitazione dell'accesso di sola lettura per una replica secondaria e per un'introduzione all'accesso alla connessione, vedere [Informazioni sull'accesso alla connessione client per le repliche di disponibilità &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md) e [Repliche secondarie attive: Repliche secondarie leggibili &#40;Gruppi di disponibilità AlwaysOn&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites-and-restrictions"></a><a name="Prerequisites"></a> Prerequisiti e restrizioni  
  
-   Per configurare un accesso alla connessione diverso, è necessario essere connessi all'istanza del server che ospita la replica primaria.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
  
|Attività|Autorizzazioni|  
|----------|-----------------|  
|Per configurare le repliche durante la creazione di un gruppo di disponibilità|Sono necessarie l'appartenenza al ruolo predefinito del server **sysadmin** e l'autorizzazione server CREATE AVAILABILITY GROUP oppure l'autorizzazione ALTER ANY AVAILABILITY GROUP o CONTROL SERVER.|  
|Per modificare una replica di disponibilità|È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.|  
  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per configurare l'accesso su una replica di disponibilità**  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita la replica primaria ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Fare clic sul gruppo di disponibilità di cui si desidera modificare la replica.  
  
4.  Fare clic con il pulsante destro del mouse sulla replica di disponibilità e scegliere **Proprietà**.  
  
5.  Nella finestra di dialogo **Proprietà replica di disponibilità** è possibile modificare l'accesso alla connessione per il ruolo primario e per il ruolo secondario, come segue:  
  
    -   Per il ruolo secondario, selezionare un nuovo valore dall'elenco a discesa **Secondario leggibile** , come segue:  
  
         **No**  
         Non sono consentite connessioni utente ai database secondari di questa replica. I database non sono disponibili per l'accesso in lettura. Si tratta dell'impostazione predefinita.  
  
         **Solo finalità di lettura**  
         Sono consentite solo connessioni in sola lettura ai database secondari di questa replica. Il database o i database secondari sono tutti disponibili per l'accesso in lettura.  
  
         **Sì**  
         Sono consentite tutte le connessioni ai database secondari di questa replica, ma solo per l'accesso in lettura. Il database o i database secondari sono tutti disponibili per l'accesso in lettura.  
  
    -   Per il ruolo primario, selezionare un nuovo valore dall'elenco a discesa **Connessioni nel ruolo primario** , come segue:  
  
         **Consenti tutte le connessioni**  
         Sono consentite tutte le connessioni ai database nella replica primaria. Si tratta dell'impostazione predefinita.  
  
         **Consenti connessioni in lettura/scrittura**  
         Se la proprietà Finalità dell'applicazione è impostata su **Lettura/Scrittura** o se tale proprietà non è impostata, la connessione è consentita. Non sono consentite le connessioni in cui la proprietà di connessione Finalità dell'applicazione è impostata su **Sola lettura** . In questo modo è possibile impedire la connessione, per errore, di un carico di lavoro con finalità di lettura alla replica primaria da parte dei clienti. Per altre informazioni sulla proprietà di connessione Finalità dell'applicazione, vedere [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per configurare l'accesso su una replica di disponibilità**  
  
> [!NOTE]  
>  Per un esempio di questa procedura, vedere [Esempio (Transact-SQL)](#TsqlExample)più avanti in questa sezione.  
  
1.  Connettersi all'istanza del server che ospita la replica primaria.  
  
2.  Se si specifica una replica per un nuovo gruppo di disponibilità, usare l'istruzione [create Availability Group](/sql/t-sql/statements/create-availability-group-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] . Se si aggiunge o si modifica una replica di un gruppo di disponibilità esistente, utilizzare l'istruzione [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Per configurare l'accesso alla connessione per il ruolo secondario, nella clausola ADD REPLICA o MODIFY REPLICA WITH specificare l'opzione SECONDARY_ROLE, come segue:  
  
         SECONDARY_ROLE **(** ALLOW_CONNECTIONS **=** { NO | READ_ONLY | ALL } **)**  
  
         dove  
  
         NO  
         Non sono consentite connessioni dirette ai database secondari di questa replica. I database non sono disponibili per l'accesso in lettura. Si tratta dell'impostazione predefinita.  
  
         READ_ONLY  
         Sono consentite solo connessioni in sola lettura ai database secondari di questa replica. Il database o i database secondari sono tutti disponibili per l'accesso in lettura.  
  
         ALL  
         Sono consentite tutte le connessioni ai database secondari di questa replica, ma solo per l'accesso in lettura. Il database o i database secondari sono tutti disponibili per l'accesso in lettura.  
  
3.  Per configurare l'accesso alla connessione per il ruolo primario, nella clausola ADD REPLICA o MODIFY REPLICA WITH specificare l'opzione PRIMARY_ROLE, come segue:  
  
     PRIMARY_ROLE **(** ALLOW_CONNECTIONS **=** { READ_WRITE | ALL } **)**  
  
     dove  
  
     READ_WRITE  
     Non sono consentite le connessioni in cui la proprietà di connessione Finalità dell'applicazione è impostata su **ReadOnly** .  Se la proprietà Finalità dell'applicazione è impostata su **Lettura/Scrittura** o se tale proprietà non è impostata, la connessione è consentita. Per altre informazioni sulla proprietà di connessione Finalità dell'applicazione, vedere [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
     ALL  
     Sono consentite tutte le connessioni ai database nella replica primaria. Si tratta dell'impostazione predefinita.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Esempio (Transact-SQL)  
 L'esempio seguente aggiunge una replica secondaria a un gruppo di disponibilità denominato *AG2*. Un'istanza del server autonoma, *COMPUTER03\HADR_INSTANCE*, viene specificata per ospitare la nuova replica di disponibilità. Questa replica è configurata per consentire unicamente le connessioni in lettura e scrittura per il ruolo primario e le connessioni con finalità di lettura per il ruolo secondario.  
  
```sql
ALTER AVAILABILITY GROUP AG2   
   ADD REPLICA ON   
      'COMPUTER03\HADR_INSTANCE' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:7022',  
         PRIMARY_ROLE ( ALLOW_CONNECTIONS = READ_WRITE ),  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY )  
         );   
GO  
```  
  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Utilizzo di PowerShell  

### <a name="to-configure-access-on-an-availability-replica"></a>Per configurare l'accesso su una replica di disponibilità
  
> [!NOTE]  
>  Per un esempio di codice, vedere gli esempi di PowerShell più avanti in questa sezione.  
  
1.  Spostarsi nella directory (`cd`) dell'istanza del server che ospita la replica primaria.  
  
2.  Quando si aggiunge una replica di disponibilità a un gruppo di disponibilità, utilizzare il cmdlet `New-SqlAvailabilityReplica`. Quando si modifica una replica di disponibilità esistente, utilizzare il cmdlet `Set-SqlAvailabilityReplica`. I parametri pertinenti sono i seguenti:  
  
    -   Per configurare l'accesso alla connessione per il ruolo secondario, specificare il `ConnectionModeInSecondaryRole` parametro *secondary_role_keyword* , dove *secondary_role_keyword* è uguale a uno dei valori seguenti:  
  
         `AllowNoConnections`  
         Non è consentita alcuna connessione diretta ai database nella replica secondaria e i database non sono disponibili per l'accesso in lettura. Si tratta dell'impostazione predefinita.  
  
         `AllowReadIntentConnectionsOnly`  
         Sono consentite solo connessioni ai database nella replica secondaria in cui la proprietà Finalità dell'applicazione è impostata su **Sola lettura**. Per altre informazioni su questa proprietà, vedere [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
         `AllowAllConnections`  
         Sono consentite tutte le connessioni ai database nella replica secondaria per l'accesso in sola lettura.  
  
    -   Per configurare l'accesso alla connessione per il ruolo primario, specificare `ConnectionModeInPrimaryRole` *primary_role_keyword*, dove *primary_role_keyword* è uguale a uno dei valori seguenti:  
  
         `AllowReadWriteConnections`  
         Non sono consentite le connessioni in cui la proprietà di connessione Finalità dell'applicazione è impostata su ReadOnly. Se la proprietà Finalità dell'applicazione è impostata su ReadWrite o se tale proprietà non è impostata, la connessione è consentita. Per altre informazioni sulla proprietà di connessione Finalità dell'applicazione, vedere [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
         `AllowAllConnections`  
         Sono consentite tutte le connessioni ai database nella replica primaria. Si tratta dell'impostazione predefinita.  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
Per configurare e usare il provider di SQL Server PowerShell, vedere [provider di SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md).
  
Nell'esempio seguente vengono impostati i parametri `ConnectionModeInSecondaryRole` e `ConnectionModeInPrimaryRole` su `AllowAllConnections`.  
  
```powershell
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  

Set-SqlAvailabilityReplica -ConnectionModeInSecondaryRole "AllowAllConnections" `
 -InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ConnectionModeInPrimaryRole "AllowAllConnections" `
-InputObject $primaryReplica
```  

##  <a name="follow-up-after-configuring-read-only-access-for-an-availability-replica"></a><a name="FollowUp"></a>Completamento: dopo la configurazione dell'accesso in sola lettura per una replica di disponibilità  
 **Accesso in sola lettura a una replica secondaria leggibile.**  
  
-   Quando si usa l'utilità [bcp](../../../tools/bcp-utility.md) o l' [utilità sqlcmd](../../../tools/sqlcmd-utility.md), è possibile specificare l'accesso in sola lettura a qualsiasi replica secondaria abilitata per l'accesso in sola lettura specificando l' `-K ReadOnly` opzione.  
  
-   Per consentire alle applicazioni client di connettersi a repliche secondarie leggibili:  
  
    ||Prerequisito|Collegamento|  
    |-|------------------|----------|  
    |![Casella](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Assicurarsi che nel gruppo di disponibilità sia presente un listener.|[Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
    |![Casella](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Configurare il routing di sola lettura per il gruppo di disponibilità.|[Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)|  
  
 **Fattori che potrebbero influire su trigger e processi dopo un failover**  
  
 Se sono presenti trigger e processi che avranno esito negativo se vengono eseguiti su una replica secondaria non leggibile o su un database secondario leggibile, è necessario generare script per trigger e processi per effettuare una verifica su una replicato specifica per determinare se il database è un database primario o un database secondario leggibile. Per ottenere queste informazioni, usare la funzione [DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql) per restituire la proprietà **Updatability** del database. Per identificare un database di sola lettura, specificare il valore READ_ONLY come indicato di seguito:  
  
```  
DATABASEPROPERTYEX([db name],'Updatability') = N'READ_ONLY'  
```  
  
 Per identificare un database di lettura/scrittura, specificare il valore READ_WRITE.  
  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Contenuto correlato  
  
-   [AlwaysOn: Value Proposition of Readable Secondary (AlwaysOn: Proposta di valore di Secondario leggibile)](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-value-proposition-of-readable-secondary)  
  
-   [AlwaysOn: Why there are two options to enable a secondary replica for read workload? (AlwaysOn: Perché ci sono due opzioni per abilitare una replica secondaria per il carico di lavoro di lettura?)](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-why-there-are-two-options-to-enable-a-secondary-replica-for-read-workload)  
  
-   [Always On: impostazione della replica secondaria leggibile](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-setting-up-readable-seconary-replica)  
  
-   [AlwaysOn: I just enabled Readable Secondary but my query is blocked? (AlwaysOn: Ho appena abilitato Secondario leggibile ma la query rimane bloccata?)](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-i-just-enabled-readable-secondary-but-my-query-is-blocked)  
  
-   [AlwaysOn: Making latest statistics available on Readable Secondary, Read-Only database and Database Snapshot (AlwaysOn: Rendere disponibili le statistiche più recenti in Secondario leggibile, nel database di sola lettura e nello snapshot del database)](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-making-latest-statistics-available-on-readable-secondary-read-only-database-and-database-snapshot)  
  
-   [AlwaysOn: Challenges with statistics on ReadOnly database, Database Snapshot and Secondary Replica (AlwaysOn: Statistiche relative al database di sola lettura, allo snapshot del database e alla replica secondaria)](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-challenges-with-statistics-on-readonly-database-database-snapshot-and-secondary-replica)  
  
-   [AlwaysOn: Impact on the primary workload when you run reporting workload on the secondary replica (AlwaysOn: Impatto sul carico di lavoro primario quando viene eseguito il carico di lavoro di report nella replica secondaria)](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-impact-on-the-primary-workload-when-you-run-reporting-workload-on-the-secondary-replica)  
  
-   [AlwaysOn: Impact of mapping reporting workload on Readable Secondary to Snapshot Isolation (AlwaysOn: Impatto del mapping del carico di lavoro di report in Secondario leggibile all'isolamento dello snapshot)](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-impact-of-mapping-reporting-workload-on-readable-secondary-to-snapshot-isolation)  
  
-   [AlwaysOn: Minimizing blocking of REDO thread when running reporting workload on Secondary Replica (AlwaysOn: Riduzione al minimo del blocco del thread REDO durante l'esecuzione del carico di lavoro di report nella replica secondaria)](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-minimizing-blocking-of-redo-thread-when-running-reporting-workload-on-secondary-replica)  
  
-   [AlwaysOn: Readable Secondary and data latency (AlwaysOn: Secondario leggibile e latenza dei dati)](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-readable-secondary-and-data-latency)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Repliche secondarie attive: repliche secondarie leggibili &#40;Gruppi di disponibilità AlwaysOn&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)  
 [Informazioni sull'accesso alla connessione client per le repliche di disponibilità &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)  
