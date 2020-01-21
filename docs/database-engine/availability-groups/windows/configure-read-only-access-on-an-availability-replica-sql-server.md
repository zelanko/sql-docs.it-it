---
title: Configurare l'accesso in sola lettura su una replica secondaria di un gruppo di disponibilità
description: "Configurare la replica secondaria per consentire solo l'accesso in lettura per il gruppo di disponibilità Always On. "
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
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
ms.openlocfilehash: aaeef70fe81699d0cbb00ba3d7e5a6dfcf1b6aa7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241726"
---
# <a name="configure-read-only-access-to-a-secondary-replica-of-an-always-on-availability-group"></a>Configurare l'accesso in sola lettura su una replica secondaria di un gruppo di disponibilità Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Per impostazione predefinita, l'accesso in lettura e scrittura e l'accesso con finalità di lettura sono entrambi consentiti nella replica primaria, ma non sono consentite connessioni alle repliche secondarie di un gruppo di disponibilità AlwaysOn. Questo argomento descrive come configurare l'accesso alla connessione in una replica di disponibilità di un gruppo di disponibilità AlwaysOn in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell.  
  
 Per informazioni sulle implicazioni dell'abilitazione dell'accesso di sola lettura per una replica secondaria e per un'introduzione all'accesso alla connessione, vedere [Informazioni sull'accesso alla connessione client per le repliche di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md) e [Repliche secondarie attive: Repliche secondarie leggibili &#40;Gruppi di disponibilità AlwaysOn&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 
##  <a name="Prerequisites"></a> Prerequisiti e restrizioni  
  
-   Per configurare un accesso alla connessione diverso, è necessario essere connessi all'istanza del server che ospita la replica primaria.  
  
##  <a name="Permissions"></a> Autorizzazioni  
  
|Attività|Autorizzazioni|  
|----------|-----------------|  
|Per configurare le repliche durante la creazione di un gruppo di disponibilità|Sono necessarie l'appartenenza al ruolo predefinito del server **sysadmin** e l'autorizzazione server CREATE AVAILABILITY GROUP oppure l'autorizzazione ALTER ANY AVAILABILITY GROUP o CONTROL SERVER.|  
|Per modificare una replica di disponibilità|È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.|  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per configurare l'accesso su una replica di disponibilità**  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita la replica primaria ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità**.  
  
3.  Fare clic sul gruppo di disponibilità di cui si desidera modificare la replica.  
  
4.  Fare clic con il pulsante destro del mouse sulla replica di disponibilità e scegliere **Proprietà**.  
  
5.  Nella finestra di dialogo **Proprietà replica di disponibilità** è possibile modificare l'accesso alla connessione per il ruolo primario e per il ruolo secondario, come segue:  
  
    -   Per il ruolo secondario, selezionare un nuovo valore dall'elenco a discesa **Secondario leggibile** , come segue:  
  
         **No**  
         Non sono consentite connessioni utente ai database secondari di questa replica. I database non sono disponibili per l'accesso in lettura. Si tratta dell'impostazione predefinita.  
  
         **Solo con finalità di lettura**  
         Sono consentite solo connessioni in sola lettura ai database secondari di questa replica. Il database o i database secondari sono tutti disponibili per l'accesso in lettura.  
  
         **Sì**  
         Sono consentite tutte le connessioni ai database secondari di questa replica, ma solo per l'accesso in lettura. Il database o i database secondari sono tutti disponibili per l'accesso in lettura.  
  
    -   Per il ruolo primario, selezionare un nuovo valore dall'elenco a discesa **Connessioni nel ruolo primario** , come segue:  
  
         **Consenti tutte le connessioni**  
         Sono consentite tutte le connessioni ai database nella replica primaria. Si tratta dell'impostazione predefinita.  
  
         **Consenti connessioni in lettura/scrittura**  
         Se la proprietà Finalità dell'applicazione è impostata su **Lettura/Scrittura** o se tale proprietà non è impostata, la connessione è consentita. Non sono consentite le connessioni in cui la proprietà di connessione Finalità dell'applicazione è impostata su **Sola lettura** . In questo modo è possibile impedire la connessione, per errore, di un carico di lavoro con finalità di lettura alla replica primaria da parte dei clienti. Per altre informazioni sulla proprietà di connessione Finalità dell'applicazione, vedere [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per configurare l'accesso su una replica di disponibilità**  
  
> [!NOTE]  
>  Per un esempio di questa procedura, vedere [Esempio (Transact-SQL)](#TsqlExample)più avanti in questa sezione.  
  
1.  Connettersi all'istanza del server che ospita la replica primaria.  
  
2.  Se si specifica una replica per un nuovo gruppo di disponibilità, usare l'istruzione [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Se si aggiunge o si modifica una replica di un gruppo di disponibilità esistente, usare l'istruzione [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
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
  
###  <a name="TsqlExample"></a> Esempio (Transact-SQL)  
 L'esempio seguente aggiunge una replica secondaria a un gruppo di disponibilità denominato *AG2*. Un'istanza del server autonoma, *COMPUTER03\HADR_INSTANCE*, viene specificata per ospitare la nuova replica di disponibilità. Questa replica è configurata per consentire unicamente le connessioni in lettura e scrittura per il ruolo primario e le connessioni con finalità di lettura per il ruolo secondario.  
  
```  
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
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
 **Per configurare l'accesso su una replica di disponibilità**  
  
> [!NOTE]  
>  Per un esempio di codice, vedere [Esempio (PowerShell)](#PSExample), più avanti in questa sezione.  
  
1.  Cambiare la directory (**cd**) impostandola sull'istanza del server che ospita la replica primaria.  
  
2.  Quando si aggiunge una replica di disponibilità a un gruppo di disponibilità, usare il cmdlet **New-SqlAvailabilityReplica** . Quando si modifica una replica di disponibilità esistente, usare il cmdlet **Set-SqlAvailabilityReplica** . I parametri pertinenti sono i seguenti:  
  
    -   Per configurare l'accesso alla connessione per il ruolo secondario, specificare **ConnectionModeInSecondaryRole**_secondary_role_keyword_ , dove *secondary_role_keyword* corrisponde a uno dei valori seguenti:  
  
         **AllowNoConnections**  
         Non è consentita alcuna connessione diretta ai database nella replica secondaria e i database non sono disponibili per l'accesso in lettura. Si tratta dell'impostazione predefinita.  
  
         **AllowReadIntentConnectionsOnly**  
         Sono consentite solo connessioni ai database nella replica secondaria in cui la proprietà Finalità dell'applicazione è impostata su **Sola lettura**. Per altre informazioni su questa proprietà, vedere [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
         **AllowAllConnections**  
         Sono consentite tutte le connessioni ai database nella replica secondaria per l'accesso in sola lettura.  
  
    -   Per configurare l'accesso alla connessione per il ruolo primario, specificare **ConnectionModeInPrimaryRole**_primary_role_keyword_, dove *primary_role_keyword* corrisponde a uno dei valori seguenti:  
  
         **AllowReadWriteConnections**  
         Non sono consentite le connessioni in cui la proprietà di connessione Finalità dell'applicazione è impostata su ReadOnly. Se la proprietà Finalità dell'applicazione è impostata su ReadWrite o se tale proprietà non è impostata, la connessione è consentita. Per altre informazioni sulla proprietà di connessione Finalità dell'applicazione, vedere [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
         **AllowAllConnections**  
         Sono consentite tutte le connessioni ai database nella replica primaria. Si tratta dell'impostazione predefinita.  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, usare il cmdlet **Get-Help** nell'ambiente PowerShell di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] . Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
###  <a name="PSExample"></a> Esempio (PowerShell)  
 Nell'esempio seguente vengono impostati i parametri **ConnectionModeInSecondaryRole** e **ConnectionModeInPrimaryRole** su **AllowAllConnections**.  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
Set-SqlAvailabilityReplica -ConnectionModeInSecondaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ConnectionModeInPrimaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
  
```  
  
##  <a name="FollowUp"></a> Completamento: Dopo la configurazione dell'accesso in sola lettura per una replica di disponibilità  
 **Accesso in sola lettura a una replica secondaria leggibile.**  
  
-   Quando si usa [bcp Utility](../../../tools/bcp-utility.md) o [sqlcmd Utility](../../../tools/sqlcmd-utility.md), è possibile specificare l'accesso in sola lettura a qualsiasi replica secondaria abilitata per l'accesso in sola lettura specificando l'opzione **-K ReadOnly** .  
  
-   Per consentire alle applicazioni client di connettersi a repliche secondarie leggibili:  
  
    ||Prerequisito|Collegamento|  
    |-|------------------|----------|  
    |![Casella di controllo](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Assicurarsi che nel gruppo di disponibilità sia presente un listener.|[Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)|  
    |![Casella di controllo](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Configurare il routing di sola lettura per il gruppo di disponibilità.|[Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)|  
  
 **Fattori che potrebbero influire su trigger e processi dopo un failover**  
  
 Se sono presenti trigger e processi che avranno esito negativo se vengono eseguiti su una replica secondaria non leggibile o su un database secondario leggibile, è necessario generare script per trigger e processi per effettuare una verifica su una replicato specifica per determinare se il database è un database primario o un database secondario leggibile. Per ottenere queste informazioni, usare la funzione [DATABASEPROPERTYEX](../../../t-sql/functions/databasepropertyex-transact-sql.md) per restituire la proprietà **Updateability** del database. Per identificare un database di sola lettura, specificare il valore READ_ONLY come indicato di seguito:  
  
```  
DATABASEPROPERTYEX([db name],'UpdateAbility') = N'READ_ONLY'  
```  
  
 Per identificare un database di lettura/scrittura, specificare il valore READ_WRITE.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   [Always On: proposta di valore di Secondario leggibile](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-value-proposition-of-readable-secondary.aspx)  
  
-   [Always On: motivi per cui sono presenti due opzioni per abilitare una replica secondaria per un carico di lavoro di lettura](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-why-there-are-two-options-to-enable-a-secondary-replica-for-read-workload.aspx)  
  
-   [Always On: configurazione di una replica secondaria leggibile](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-setting-up-readable-seconary-replica.aspx)  
  
-   [Always On: motivo per cui anche se Secondario leggibile è appena stato abilitato la query rimane bloccata](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-i-just-enabled-readble-secondary-but-my-query-is-blocked.aspx)  
  
-   [Always On: come rendere disponibili le statistiche più recenti in Secondario leggibile, nel database di sola lettura e nello snapshot del database](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-making-upto-date-statistics-available-on-readable-secondary-read-only-database-and-database-snapshot.aspx)  
  
-   [Always On: problematiche riguardanti le statistiche sul database di sola lettura, sullo snapshot del database e sulla replica secondaria](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-challenges-with-statistics-on-readonly-database-database-snapshot-and-secondary-replica.aspx)  
  
-   [Always On: impatto sul carico di lavoro primario quando viene eseguito il carico di lavoro di report nella replica secondaria](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-impact-on-the-primary-workload-when-you-run-reporting-workload-on-the-secondary-replica.aspx)  
  
-   [Always On: impatto del mapping del carico di lavoro di report in Secondario leggibile all'isolamento dello snapshot](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-impact-of-mapping-reporting-workload-to-snapshot-isolation-on-readable-secondary.aspx)  
  
-   [Always On: riduzione al minimo del blocco del thread REDO quando si esegue il carico di lavoro di report nella replica secondaria](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-minimizing-blocking-of-redo-thread-when-running-reporting-workload-on-secondary-replica.aspx)  
  
-   [Always On: Secondario leggibile e latenza dei dati](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On.aspx)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Repliche secondarie attive: Repliche secondarie leggibili &#40;Gruppi di disponibilità Always On&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Informazioni sull'accesso alla connessione client per le repliche di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)  
  
  
