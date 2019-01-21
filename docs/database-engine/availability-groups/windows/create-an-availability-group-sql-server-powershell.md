---
title: Creare un gruppo di disponibilità con PowerShell
description: Procedura per la creazione di un gruppo disponibilità Always On con PowerShell.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: bc69a7df-20fa-41e1-9301-11317c5270d2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 57330040f7fc5ba1fdd48278b69a46bcf7eaee46
ms.sourcegitcommit: 170c275ece5969ff0c8c413987c4f2062459db21
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/11/2019
ms.locfileid: "54226548"
---
# <a name="create-an-always-on-availability-group-using-powershell"></a>Creare un gruppo di disponibilità Always On con PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento si illustra come usare i cmdlet di PowerShell per creare e configurare un gruppo di disponibilità AlwaysOn usando PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Un *gruppo di disponibilità* permette di definire un set di database utente di cui sarà eseguito il failover come unità singola e un set di partner di failover, noti come *repliche di disponibilità*, che supportano il failover.  
  
> [!NOTE]  
>  Per un'introduzione ai gruppi di disponibilità, vedere [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti, restrizioni e raccomandazioni](#PrerequisitesRestrictions)  
  
     [Sicurezza](#Security)  
  
     [Riepilogo delle attività e cmdlet di PowerShell corrispondenti](#SummaryPSStatements)  
  
     [Per impostare e usare il provider PowerShell per SQL Server](#PsProviderLinks)  
  
-   **Per creare e configurare un gruppo di disponibilità usando:**  [Uso di PowerShell per creare e configurare un gruppo di disponibilità](#PowerShellProcedure)  
  
-   **Esempi:**  [Uso di PowerShell per creare un gruppo di disponibilità](#ExampleConfigureGroup)  
  
-   [Attività correlate](#RelatedTasks)  
  
-   [Contenuto correlato](#RelatedContent)  
  
> [!NOTE]  
>  In alternativa all'uso dei cmdlet di PowerShell, è possibile usare la procedura guidata Crea gruppo di disponibilità o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Per altre informazioni, vedere [Usare la finestra di dialogo Nuovo gruppo di disponibilità &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md) o [Creare un gruppo di disponibilità &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md).  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
 Prima di iniziare a creare il primo gruppo di disponibilità, è consigliabile leggere questa sezione.  
  
###  <a name="PrerequisitesRestrictions"></a> Prerequisiti, restrizioni e raccomandazioni  
  
-   Prima di creare un gruppo di disponibilità, verificare che le istanze host di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] si trovino ognuna in un nodo WSCF (Windows Server Failover Clustering) diverso di un singolo cluster di failover WSFC. Inoltre, verificare che le istanze del server abbiano soddisfatto gli altri prerequisiti dell'istanza del server, che tutti gli altri requisiti di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] siano soddisfatti e che si tengano presenti i consigli. Per altre informazioni, si consiglia di leggere [Prerequisiti, restrizioni e raccomandazioni per i gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Sono necessarie l'appartenenza al ruolo predefinito del server **sysadmin** e l'autorizzazione server CREATE AVAILABILITY GROUP oppure l'autorizzazione ALTER ANY AVAILABILITY GROUP o CONTROL SERVER.  
  
###  <a name="SummaryPSStatements"></a> Riepilogo delle attività e cmdlet di PowerShell corrispondenti  
 Nella tabella seguente sono elencate le attività di base necessarie per la configurazione di un gruppo di disponibilità e sono indicate le attività supportate dai cmdlet di PowerShell. È necessario eseguire le attività [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] nell'ordine con cui sono elencate nella tabella.  
  
|Attività|Cmdlet di PowerShell (se disponibile) o istruzione Transact-SQL|Posizione in cui eseguire l'attività **&#42;**|  
|----------|--------------------------------------------------------------------|---------------------------------|  
|Creare un endpoint del mirroring del database (una volta per ogni istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] )|**New-SqlHadrEndPoint**|Eseguire in ogni istanza del server in cui non è presente l'endpoint del mirroring del database.<br /><br /> Nota: Per modificare un endpoint del mirroring del database esistente, usare **Set-SqlHadrEndpoint**.|  
|Creare un gruppo di disponibilità|Usare innanzitutto il cmdlet **New-SqlAvailabilityReplica** con il parametro **-AsTemplate** per creare un oggetto della replica di disponibilità in memoria per ognuna delle due repliche di disponibilità da includere nel gruppo di disponibilità.<br /><br /> Creare quindi il gruppo di disponibilità tramite il cmdlet **New-SqlAvailabilityGroup** e facendo riferimento agli oggetti replica di disponibilità.|Eseguire nell'istanza del server che dovrà ospitare la replica primaria iniziale.|  
|Creare un join della replica secondaria al gruppo di disponibilità|**Join-SqlAvailabilityGroup**|Eseguire in ogni istanza del server in cui è ospitata una replica secondaria.|  
|Preparare il database secondario|**Backup-SqlDatabase** e **Restore-SqlDatabase**|Creare i backup nell'istanza del server in cui è ospitata la replica primaria.<br /><br /> Ripristinare i backup in ogni istanza del server in cui è ospitata una replica secondaria, usando il parametro di ripristino **NoRecovery** . Se i percorsi di file differiscono tra i computer in cui sono ospitate la replica primaria e la replica secondaria di destinazione, usare anche il parametro di ripristino **RelocateFile** .|  
|Avviare la sincronizzazione dei dati creando un join di ogni database secondario al gruppo di disponibilità|**Add-SqlAvailabilityDatabase**|Eseguire in ogni istanza del server in cui è ospitata una replica secondaria.|  
  
 \*Per eseguire un'attività specifica, impostare la directory (**cd**) sull'istanza o sulle istanze del server indicate.  
  
###  <a name="PsProviderLinks"></a> Per impostare e usare il provider PowerShell per SQL Server  
  
-   [Provider PowerShell per SQL Server](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Visualizzazione della Guida di SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell per creare e configurare un gruppo di disponibilità  
  
> [!NOTE]  
>  Per visualizzare la sintassi e un esempio di un cmdlet specifico, usare il cmdlet **Get-Help** nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
1.  Spostarsi nella directory (**cd**) dell'istanza del server che deve ospitare la replica primaria.  
  
2.  Creare un oggetto replica di disponibilità in memoria per la replica primaria.  
  
3.  Creare un oggetto replica di disponibilità in memoria per ognuna delle repliche secondarie.  
  
4.  Creare il gruppo di disponibilità.  
  
    > [!NOTE]  
    >  La lunghezza massima consentita per il nome del gruppo di disponibilità è 128 caratteri.  
  
5.  Creare un join della nuova replica secondaria al gruppo di disponibilità. Per altre informazioni, vedere [Creare un join di una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
6.  Per ogni database nel gruppo di disponibilità, creare un database secondario ripristinando i backup recenti del database primario, usando RESTORE WITH NORECOVERY.  
  
7.  Creare un join di ogni nuovo database secondario al gruppo di disponibilità. Per altre informazioni, vedere [Creare un join di una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
8.  Facoltativamente, usare il comando **dir** di Windows per verificare il contenuto del nuovo gruppo di disponibilità.  
  
> [!NOTE]  
>  Se gli account del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] delle istanze del server sono eseguiti con account utente di dominio diversi, in ogni istanza del server creare un account di accesso per l'altra istanza del server e concedere a questo account l'autorizzazione CONNECT per l'endpoint del mirroring del database locale.  
  
##  <a name="ExampleConfigureGroup"></a> Esempio: Uso di PowerShell per creare un gruppo di disponibilità  
 Nell'esempio di PowerShell seguente si crea e si configura un gruppo di disponibilità semplice denominato `MyAG` con due repliche di disponibilità e un database di disponibilità. Esempio:  
  
1.  Viene eseguito il backup di `MyDatabase` e del relativo log delle transazioni.  
  
2.  Ripristina `MyDatabase` e il relativo log delle transazioni, usando l'opzione **-NoRecovery** .  
  
3.  Viene creata una rappresentazione in memoria della replica primaria, che sarà ospitata dall'istanza locale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (denominata `PrimaryComputer\Instance`).  
  
4.  Viene creata una rappresentazione in memoria della replica secondaria, che sarà ospitata da un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (denominata `SecondaryComputer\Instance`).  
  
5.  Viene creato un nuovo gruppo di disponibilità denominato `MyAG`.  
  
6.  Viene creato un join della replica secondaria al gruppo di disponibilità.  
  
7.  Viene creato un join del database secondario al gruppo di disponibilità.  
  
```  
# Backup my database and its log on the primary  
Backup-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.bak" `  
    -ServerInstance "PrimaryComputer\Instance"  
  
Backup-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.log" `  
    -ServerInstance "PrimaryComputer\Instance" `  
    -BackupAction Log   
  
# Restore the database and log on the secondary (using NO RECOVERY)  
Restore-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.bak" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -NoRecovery  
  
Restore-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.log" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -RestoreAction Log `  
    -NoRecovery  
  
# Create an in-memory representation of the primary replica.  
$primaryReplica = New-SqlAvailabilityReplica `  
    -Name "PrimaryComputer\Instance" `  
    -EndpointURL "TCP://PrimaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create an in-memory representation of the secondary replica.  
$secondaryReplica = New-SqlAvailabilityReplica `  
    -Name "SecondaryComputer\Instance" `  
    -EndpointURL "TCP://SecondaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create the availability group  
New-SqlAvailabilityGroup `  
    -Name "MyAG" `  
    -Path "SQLSERVER:\SQL\PrimaryComputer\Instance" `  
    -AvailabilityReplica @($primaryReplica,$secondaryReplica) `  
    -Database "MyDatabase"  
  
# Join the secondary replica to the availability group.  
Join-SqlAvailabilityGroup -Path "SQLSERVER:\SQL\SecondaryComputer\Instance" -Name "MyAG"  
  
# Join the secondary database to the availability group.  
Add-SqlAvailabilityDatabase -Path "SQLSERVER:\SQL\SecondaryComputer\Instance\AvailabilityGroups\MyAG" -Database "MyDatabase"  
```  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per configurare un'istanza del server per i gruppi di disponibilità AlwaysOn**  
  
-   [Abilitare e disabilitare la funzionalità Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [Creare un endpoint del mirroring del database per i gruppi di disponibilità AlwaysOn &#40;SQL Server PowerShell&#41;](~/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
 **Per configurare le proprietà della replica e del gruppo di disponibilità**  
  
-   [Modificare la modalità di disponibilità di una replica di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Modificare la modalità di failover di una replica di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurare i criteri di failover flessibili per controllare le condizioni per il failover automatico &#40;Gruppi di disponibilità AlwaysOn&#41;](~/database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
-   [Specifica dell'URL dell'endpoint quando si aggiunge o si modifica una replica di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Configurare il backup su repliche di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Modificare il periodo di timeout della sessione per una replica di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **Per completare la configurazione del gruppo di disponibilità**  
  
-   [Creare un join di una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Creare un join di un database secondario a un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **Modalità alternative di creazione di un gruppo di disponibilità**  
  
-   [Usare la Creazione guidata Gruppo di disponibilità &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Utilizzare la finestra di dialogo Nuovo gruppo di disponibilità &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Creare un gruppo di disponibilità &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
 **Per risolvere i problemi relativi alla configurazione di Gruppi di disponibilità AlwaysOn**  
  
-   [Risolvere i problemi relativi alla configurazione dei gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Risolvere i problemi relativi a una operazione di aggiunta file non riuscita &#40;Gruppi di disponibilità AlwaysOn&#41;](~/database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   **Blog:**  
  
     [Serie di informazioni su Always On - HADRON: Uso del pool di lavoro per database abilitati HADRON](https://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [Pagina relativa alla configurazione di AlwaysOn con SQL Server PowerShell](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/03/configuring-alwayson-with-sql-server-powershell/)  
  
     [SQL Server Always On Team Blogs (Blog del team di SQL Server Always On): blog ufficiale del team di SQL Server Always On](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [Pagina relativa ai blog del Servizio Supporto Tecnico Clienti per gli ingegneri di SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Video:**  
  
     [Microsoft SQL Server Code-Named "Denali" Always On Series,Part 1: Introducing the Next Generation High Availability Solution](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302) (Serie Always On in Microsoft SQL Server nome in codice "Denali", parte 1: Introduzione alla soluzione a disponibilità elevata di nuova generazione)  
  
     [Microsoft SQL Server Code-Named "Denali" Always On Series,Part 2: Building a Mission-Critical High Availability Solution Using Always On](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404) (Serie Always On in Microsoft SQL Server nome in codice "Denali", parte 2: Creazione di una soluzione cruciale a disponibilità elevata con Always On)  
  
-   **White paper:**  
  
     [Microsoft SQL Server Always On Solutions Guide for High Availability and Disaster Recovery (Guida alle soluzioni AlwaysOn di Microsoft SQL Server per la disponibilità elevata e il ripristino di emergenza)](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Pagina relativa ai white paper Microsoft per SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Pagina relativa ai white paper del team di consulenza clienti di SQL Server](https://sqlcat.com/)  
  
## <a name="see-also"></a>Vedere anche  
 [Endpoint del mirroring del database &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  







