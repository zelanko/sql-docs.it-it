---
title: Aggiungere una replica secondaria a un gruppo di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], configuring
ms.assetid: 6669dcce-85f9-495f-aadf-7f62cff4a9da
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7605f4e5fd2fd6601cf1d132b438187edeeb29fb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62792041"
---
# <a name="add-a-secondary-replica-to-an-availability-group-sql-server"></a>Aggiungere una replica secondaria a un gruppo di disponibilità (SQL Server)
  In questo argomento viene illustrato come aggiungere una replica secondaria a un gruppo di disponibilità AlwaysOn esistente utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti e restrizioni](#PrerequisitesRestrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per aggiungere una replica mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Completamento:**  [Dopo aver aggiunto una Replica secondaria](#FollowUp)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Prima di iniziare a creare il primo gruppo di disponibilità, è consigliabile leggere questa sezione.  
  
##  <a name="PrerequisitesRestrictions"></a> Prerequisiti e restrizioni  
  
-   È necessario essere connessi all'istanza del server che ospita la replica primaria.  
  
 Per altre informazioni, vedere [Prerequisiti, restrizioni e consigli per i gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
##  <a name="Security"></a> Sicurezza  
  
###  <a name="Permissions"></a> Autorizzazioni  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per aggiungere una replica**  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita la replica primaria ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Fare clic con il pulsante destro del mouse sul gruppo di disponibilità e selezionare uno dei comandi seguenti:  
  
    -   Per avviare la procedura guidata Aggiungi replica a gruppo di disponibilità, selezionare il comando **Aggiungi replica** . Per altre informazioni, vedere [Usare la procedura guidata Aggiungi replica a gruppo di disponibilità &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md).  
  
    -   In alternativa, selezionare il comando **Proprietà** per aprire la finestra di dialogo **Proprietà gruppo di disponibilità** . I passaggi per l'aggiunta di una replica in questa finestra di dialogo sono indicati di seguito:  
  
        1.  Nel riquadro **Repliche di disponibilità** della finestra di dialogo fare clic sul pulsante **Aggiungi** . Verrà creata e selezionata una replica in cui il campo Istanza del server vuoto è selezionato.  
  
        2.  Immettere il nome di un'istanza del server che soddisfa i prerequisiti per ospitare una replica di disponibilità.  
  
         Per aggiungere repliche aggiuntive, ripetere i passaggi precedenti. Dopo avere specificato le repliche, fare clic su **OK** per completare l'operazione.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 **Per aggiungere una replica**  
  
1.  Connettersi all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che ospita la replica primaria.  
  
2.  Aggiungere la nuova replica secondaria al gruppo di disponibilità utilizzando la clausola ADD REPLICA ON dell'istruzione ALTER AVAILABILITY GROUP. Le opzioni ENDPOINT_URL, AVAILABILITY_MODE e FAILOVER_MODE sono obbligatorie in una clausola ADD REPLICA ON. Le altre opzioni di replica, BACKUP_PRIORITY, SECONDARY_ROLE, PRIMARY_ROLE e SESSION_TIMEOUT, sono facoltative. Per altre informazioni, vedere [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql).  
  
     Ad esempio, nell'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] seguente viene creata una nuova replica per un gruppo di disponibilità denominato `MyAG` sull'istanza del server predefinita ospitata da `COMPUTER04`, il cui URL dell'endpoint è `TCP://COMPUTER04.Adventure-Works.com:5022'`. Questa replica supporta il failover manuale e la modalità di disponibilità con commit asincrono.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG ADD REPLICA ON 'COMPUTER04'   
       WITH (  
             ENDPOINT_URL = 'TCP://COMPUTER04.Adventure-Works.com:5022',  
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             );  
    ```  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
 **Per aggiungere una replica**  
  
1.  Spostarsi nella directory (`cd`) dell'istanza del server che ospita la replica primaria.  
  
2.  Usare il cmdlet **New-SqlAvailabilityReplica** .  
  
     Ad esempio, il seguente comando aggiunge una replica di disponibilità per un gruppo di disponibilità esistente denominato `MyAg`. Questa replica supporta il failover manuale e la modalità di disponibilità con commit asincrono. Nel ruolo secondario, questa replica supporterà le connessioni con accesso in lettura consentendo all'utente di ripartire il carico dell'elaborazione di sola lettura in questa replica.  
  
    ```  
    $agPath = "SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg"  
    $endpointURL = "TCP://PrimaryServerName.domain.com:5022"  
    $failoverMode = "Manual"  
    $availabilityMode = "AsynchronousCommit"  
    $secondaryReadMode = "AllowAllConnections"  
  
    New-SqlAvailabilityReplica -Name SecondaryServer\Instance `   
    -EndpointUrl $endpointURL `   
    -FailoverMode $failoverMode `   
    -AvailabilityMode $availabilityMode `   
    -ConnectionModeInSecondaryRole $secondaryReadMode `   
    -Path $agPath  
    ```  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Completamento: Dopo l'aggiunta di una replica secondaria  
 Per aggiungere una replica per un gruppo di disponibilità esistente, è necessario effettuare i passaggi seguenti:  
  
1.  Connettersi all'istanza del server che ospiterà la nuova replica secondaria.  
  
2.  Creare un join della nuova replica secondaria al gruppo di disponibilità. Per altre informazioni, vedere [Creare un join di una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
3.  Per ogni database nel gruppo di disponibilità, creare un database secondario nell'istanza del server che ospita la replica secondaria. Per altre informazioni, vedere [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
4.  Creare un join dei nuovi database secondari al gruppo di disponibilità. Per altre informazioni, vedere [Creare un join di un database secondario a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per gestire una replica di disponibilità**  
  
-   [Creare un join di una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Rimuovere una replica secondaria da un gruppo di disponibilità &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Modificare la modalità di disponibilità di una replica di disponibilità &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Modificare la modalità di failover di una replica di disponibilità &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Modificare il periodo di timeout della sessione per una replica di disponibilità &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
-   [Modificare il periodo di timeout della sessione per una replica di disponibilità &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)   
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Creazione e configurazione di gruppi di disponibilità &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Usare il Dashboard AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)   
 [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
  
