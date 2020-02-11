---
title: Aggiungere un database a un gruppo di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 2a54eef8-9e8e-4e04-909c-6970112d55cc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dda5ac5b2f569c8438439ec77da33fde3a385fa0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72782896"
---
# <a name="add-a-database-to-an-availability-group-sql-server"></a>Aggiungere un database a un gruppo di disponibilità (SQL Server)
  In questo argomento viene illustrato come aggiungere un database a un gruppo di disponibilità AlwaysOn utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti e restrizioni](#Prerequisites)  
  
     [Autorizzazioni](#Permissions)  
  
-   **Per aggiungere un database a un gruppo di disponibilità utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti e restrizioni  
  
-   È necessario essere connessi all'istanza del server che ospita la replica primaria.  
  
-   È necessario che il database risieda nell'istanza del server che ospita la replica primaria e sia conforme ai prerequisiti e alle restrizioni per i database di disponibilità. Per ulteriori informazioni, vedere [prerequisiti, restrizioni e consigli per Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Security"></a> Sicurezza  
  
###  <a name="Permissions"></a> Autorizzazioni  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
 **Per aggiungere un database a un gruppo di disponibilità**  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita la replica primaria ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Fare clic con il pulsante destro del mouse sul gruppo di disponibilità e selezionare uno dei comandi seguenti:  
  
    -   Per avviare la procedura guidata Aggiungi database a gruppo di disponibilità, selezionare il comando **Aggiungi database** . Per altre informazioni, vedere [Usare la procedura guidata Aggiungi database a gruppo di disponibilità &#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
    -   Per aggiungere uno o più database specificandoli nella finestra di dialogo **Proprietà gruppo di disponibilità** , selezionare il comando **Proprietà** . Di seguito sono indicati i passaggi per l'aggiunta di un database:  
  
        1.  Nel riquadro **Database di disponibilità** fare clic sul pulsante **Aggiungi** . Viene creato e selezionato un campo del database vuoto.  
  
        2.  Immettere il nome di un database che soddisfi i prerequisiti dei database di disponibilità.  
  
         Per aggiungere un altro database, ripetere i passaggi precedenti. Dopo avere specificato i database, fare clic su **OK** per completare l'operazione.  
  
         Dopo avere utilizzato la finestra di dialogo **Proprietà gruppo di disponibilità** per aggiungere un database a un gruppo di disponibilità, è necessario configurare il database secondario corrispondente su ogni istanza del server che ospita una replica secondaria. Per altre informazioni, vedere [Avviare lo spostamento dati su un database secondario AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
 **Per aggiungere un database a un gruppo di disponibilità**  
  
1.  Connettersi all'istanza del server che ospita la replica primaria.  
  
2.  Utilizzare l'istruzione [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) , come indicato di seguito:  
  
     ALTER AVAILABILITY GROUP *nome_gruppo* ADD DATABASE *nome_database* [,...*n*]  
  
     dove *nome_gruppo* è il nome del gruppo di disponibilità e *nome_database* è il nome di un database da aggiungere al gruppo.  
  
     Nell'esempio seguente viene aggiunto il database *MyDb3* al gruppo di disponibilità *MyAG* .  
  
    ```  
    -- Connect to the server instance that hosts the primary replica.  
    -- Add an existing database to the availability group.  
    ALTER AVAILABILITY GROUP MyAG ADD DATABASE MyDb3;  
    GO  
    ```  
  
3.  Dopo avere aggiunto un database a un gruppo di disponibilità, è necessario configurare il database secondario corrispondente su ogni istanza del server che ospita una replica secondaria. Per altre informazioni, vedere [Avviare lo spostamento dati su un database secondario AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
##  <a name="PowerShellProcedure"></a> Con PowerShell  
 **Per aggiungere un database a un gruppo di disponibilità**  
  
1.  Spostarsi nella directory (`cd`) dell'istanza del server che ospita la replica primaria.  
  
2.  Utilizzare il cmdlet `Add-SqlAvailabilityDatabase` .  
  
     Ad esempio, con il comando seguente viene aggiunto il database secondario `MyDd` al gruppo di disponibilità `MyAG` la cui replica primaria è ospitata da `PrimaryServer\InstanceName`.  
  
    ```powershell
    Add-SqlAvailabilityDatabase `   
     -Path SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `   
     -Database "MyDb"  
    ```  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
3.  Dopo avere aggiunto un database a un gruppo di disponibilità, è necessario configurare il database secondario corrispondente su ogni istanza del server che ospita una replica secondaria. Per altre informazioni, vedere [Avviare lo spostamento dati su un database secondario AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
 Per configurare e usare il provider di SQL Server PowerShell, vedere [provider di SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md).

 Nel seguente esempio si illustra il processo completo di preparazione di un database secondario da un database nell'istanza del server che ospita la replica primaria di un gruppo di disponibilità, aggiungendo il database a un gruppo di disponibilità (come database primario), quindi creando un join del database secondario al gruppo di disponibilità. Nell'esempio si esegue innanzitutto il backup del database e del relativo log delle transazioni. Successivamente si ripristinano i backup del database e del log nelle istanze del server che ospitano una replica secondaria.  
  
 Nell'esempio viene chiamato due volte `Add-SqlAvailabilityDatabase`, la prima volta nella replica primaria per aggiungere il database al gruppo di disponibilità, successivamente nella replica secondaria per creare un join del database secondario in quella replica al gruppo di disponibilità. Se si dispone di più di una replica secondaria, ripristinare e creare un join del database secondario in ognuna di esse.  
  
```powershell
$DatabaseBackupFile = "\\share\backups\MyDatabase.bak"  
$LogBackupFile = "\\share\backups\MyDatabase.trn"  
$MyAgPrimaryPath = "SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg"  
$MyAgSecondaryPath = "SQLSERVER:\SQL\SecondaryServer\InstanceName\AvailabilityGroups\MyAg"  
  
Backup-SqlDatabase -Database "MyDatabase" -BackupFile $DatabaseBackupFile -ServerInstance "PrimaryServer\InstanceName"  
Backup-SqlDatabase -Database "MyDatabase" -BackupFile $LogBackupFile -ServerInstance "PrimaryServer\InstanceName" -BackupAction 'Log'  
  
Restore-SqlDatabase -Database "MyDatabase" -BackupFile $DatabaseBackupFile -ServerInstance "SecondaryServer\InstanceName" -NoRecovery  
Restore-SqlDatabase -Database "MyDatabase" -BackupFile $LogBackupFile -ServerInstance "SecondaryServer\InstanceName" -RestoreAction 'Log' -NoRecovery  
  
Add-SqlAvailabilityDatabase -Path $MyAgPrimaryPath -Database "MyDatabase"  
Add-SqlAvailabilityDatabase -Path $MyAgSecondaryPath -Database "MyDatabase"
```  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Creazione e configurazione di gruppi di disponibilità &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Usare il dashboard AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)   
 [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
