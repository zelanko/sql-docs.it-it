---
title: Abilitare il backup gestito di SQL Server in Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 870d1b5d1a7bedb0d758be7eef4cb3f7b2e0106c
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527084"
---
# <a name="enable-sql-server-managed-backup-to-microsoft-azure"></a>Abilitare il backup gestito di SQL Server in Microsoft Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questo argomento descrive come abilitare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con le impostazioni predefinite a livello di database e di istanza. Viene descritta anche la procedura per abilitare le notifiche tramite posta elettronica e monitorare l'attività di backup.  
  
 In questa esercitazione viene usato Azure PowerShell. Prima di iniziare l'esercitazione, [scaricare e installare Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).  
  
> [!IMPORTANT]  
>  Per abilitare anche le opzioni avanzate o usare una pianificazione personalizzata, configurare tali impostazioni prima di abilitare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Per altre informazioni, vedere [Configurare le opzioni avanzate per il backup gestito di SQL Server in Microsoft Azure](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="enable-and-configure-includesssmartbackupincludesss-smartbackup-mdmd-with-default-settings"></a>Abilitare e configurare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con le impostazioni predefinite  
  
#### <a name="create-the-azure-blob-container"></a>Creare il contenitore BLOB di Azure  
  
1.  **Iscriversi ad Azure:** se si dispone già di una sottoscrizione di Azure, andare al passaggio successivo. In caso contrario, è possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/) oppure esaminare le [opzioni per l'acquisto](https://azure.microsoft.com/pricing/purchase-options/).  
  
2.  **Creare un account di archiviazione di Azure**: se si dispone già di un account di archiviazione, andare al passaggio successivo. In caso contrario, è possibile usare il [portale di gestione di Azure](https://manage.windowsazure.com/) o Azure PowerShell per creare l'account di archiviazione. Il comando `New-AzureStorageAccount` seguente crea un account di archiviazione denominato `managedbackupstorage` nell'area Stati Uniti orientali.  
  
    ```powershell  
    New-AzureStorageAccount -StorageAccountName "managedbackupstorage" -Location "EAST US"  
    ```  
  
     Per altre informazioni sugli account di archiviazione, vedere [Informazioni sugli account di archiviazione di Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/).  
  
3.  **Creare un contenitore BLOB per i file di backup:** è possibile creare un contenitore BLOB nel portale di gestione di Azure o con Azure PowerShell. Il comando `New-AzureStorageContainer` seguente crea un contenitore BLOB denominato `backupcontainer` nell'account di archiviazione `managedbackupstorage` .  
  
    ```powershell  
    $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey (Get-AzureStorageKey -StorageAccountName managedbackupstorage).Primary  
    New-AzureStorageContainer -Name backupcontainer -Context $context  
    ```  
  
4.  **Generare una firma di accesso condiviso:** per accedere al contenitore, è necessario creare una firma di accesso condiviso. Questa operazione può essere eseguita in alcuni strumenti, tramite codice e con Azure PowerShell. Il comando `New-AzureStorageContainerSASToken` seguente crea un token della firma di accesso condiviso per il contenitore BLOB `backupcontainer` che scade entro un anno.  
  
  ```powershell  
  $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey (Get-AzureStorageKey -StorageAccountName managedbackupstorage).Primary   
  New-AzureStorageContainerSASToken -Name backupcontainer -Permission rwdl -ExpiryTime (Get-Date).AddYears(1) -FullUri -Context $context  
  ```  

Per Azure usare il comando seguente:
  ```powershell
  Connect-AzAccount
  Set-AzContext -SubscriptionId "YOURSUBSCRIPTIONID"
  $StorageAccountKey = (Get-AzStorageAccountKey -ResourceGroupName YOURRESOURCEGROUPFORTHESTORAGE -Name managedbackupstorage)[0].Value
  $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey $StorageAccountKey 
  New-AzureStorageContainerSASToken -Name backupcontainer -Permission rwdl -ExpiryTime (Get-Date).AddYears(1) -FullUri -Context $context
  ```  
  
L'output per questo comando conterrà sia l'URL del contenitore e che il token della firma di accesso condiviso. Di seguito è riportato un esempio:  
  
  `https://managedbackupstorage.blob.core.windows.net/backupcontainer?sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl`
  
Nell'esempio precedente separare l'URL del contenitore dal token della firma di accesso condiviso in corrispondenza del punto interrogativo (escludendo il punto interrogativo). Ad esempio, l'output precedente corrisponde ai due valori seguenti.  
  
|||  
|-|-|  
|**URL contenitore:**|https://managedbackupstorage.blob.core.windows.net/backupcontainer|  
|**Token della firma di accesso condiviso:**|sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl|  
|||
  
Registrare l'URL del contenitore e la firma di accesso condiviso per usarli per la creazione di una credenziale SQL. Per altre informazioni sulla firma di accesso condiviso, vedere [Firme di accesso condiviso, parte 1: informazioni sul modello di firma di accesso condiviso](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/).  
  
#### <a name="enable-includesssmartbackupincludesss-smartbackup-mdmd"></a>Abilita [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
1.  **Creare credenziali SQL per l'URL di firma di accesso condiviso:** usare il token di firma di accesso condiviso per creare credenziali SQL per l'URL del contenitore BLOB. In SQL Server Management Studio usare la query Transact-SQL seguente per creare la credenziale per l'URL del contenitore BLOB in base all'esempio seguente:  
  
    ```sql  
    CREATE CREDENTIAL [https://managedbackupstorage.blob.core.windows.net/backupcontainer]   
    WITH IDENTITY = 'Shared Access Signature',  
    SECRET = 'sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl'  
    ```  
  
2.  **Assicurarsi che il servizio SQL Server Agent sia avviato e in esecuzione:** se non è in esecuzione, avviare SQL Server Agent.  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] è necessaria l'esecuzione di SQL Server Agent nell'istanza per poter eseguire le operazioni di backup.  Per assicurarsi che le operazioni in questione vengano eseguite regolarmente, è possibile impostare l'esecuzione automatica di SQL Server Agent.  
  
3.  **Determinare il periodo di conservazione:** determinare il periodo di memorizzazione per i file di backup. Il periodo di memorizzazione viene specificato in giorni in un intervallo compreso tra 1 e 30.  
  
4.  **Abilitare e configurare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:** avviare SQL Server Management Studio e connettersi all'istanza di SQL Server di destinazione. Nella finestra Query eseguire l'istruzione seguente dopo aver modificato i valori per il nome del database, l'URL del contenitore e il periodo di memorizzazione in base alle esigenze:  
  
    > [!IMPORTANT]  
    >  Per abilitare il backup gestito a livello di istanza, specificare `NULL` per il parametro `database_name` .  
  
    ```sql  
    Use msdb;  
    GO  
    EXEC msdb.managed_backup.sp_backup_config_basic   
     @enable_backup = 1,   
     @database_name = 'yourdatabasename',  
     @container_url = 'https://managedbackupstorage.blob.core.windows.net/backupcontainer',   
     @retention_days = 30  
    GO  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ora è abilitato nel database specificato. L'inizio delle operazioni di backup nel database può richiedere fino a 15 minuti.  
  
5.  **Esaminare la configurazione predefinita degli eventi estesi:** esaminare le impostazioni degli eventi estesi eseguendo l'istruzione transact-SQL seguente.  
  
    ```  
    SELECT * FROM msdb.managed_backup.fn_get_current_xevent_settings()  
    ```  
  
     Verificare che gli eventi dei canali amministrativo, operativo e analitico siano abilitati per impostazione predefinita e che non possano essere disabilitati. Questa verifica dovrebbe essere sufficiente per monitorare gli eventi per i quali è richiesto un intervento manuale.  È possibile abilitare eventi di debug, ma nei canali di debug sono inclusi eventi informativi e di debug utilizzati dal [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per rilevare eventuali problemi e risolverli.  
  
6.  **Abilitare e configurare notifiche per lo stato di integrità** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] contiene una stored procedure che consente di creare un processo dell'agente per inviare notifiche tramite posta elettronica di errori o avvisi che potrebbero richiedere attenzione. Nei passaggi seguenti viene illustrato il processo per abilitare e configurare le notifiche tramite posta elettronica:  
  
    1.  Configurare Posta elettronica database se non è già abilitato nell'istanza. Per altre informazioni, vedere [Configurare Posta elettronica database](../../relational-databases/database-mail/configure-database-mail.md).  
  
    2.  Configurare la notifica di SQL Server Agent per l'uso di Posta elettronica database. Per altre informazioni, vedere [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  **Abilitare le notifiche di posta elettronica per ricevere avvisi ed errori di backup:** Nella finestra di query eseguire le istruzioni Transact-SQL seguenti:  
  
        ```  
        EXEC msdb.managed_backup.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
  
        ```  
  
7.  **Visualizzare i file di backup nell'account di archiviazione di Microsoft Azure:** connettersi all'account di archiviazione da SQL Server Management Studio o dal portale di gestione di Azure. Verranno visualizzati gli eventuali file di backup disponibili nel contenitore specificato. Potrebbe essere visualizzato un backup del database e del log entro 5 minuti dall'abilitazione del [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per il database.  
  
8.  **Monitorare lo stato di integrità:**  è possibile eseguire il monitoraggio attraverso notifiche tramite posta elettronica configurate in precedenza o monitorare attivamente gli eventi registrati. Di seguito sono riportate alcune istruzioni Transact-SQL di esempio utilizzate per visualizzare gli eventi:  
  
    ```sql  
    --  view all admin events  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```sql  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```sql  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
    ```
  
 I passaggi descritti in questa sezione riguardano in modo specifico la configurazione del [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per la prima volta nel database. È possibile modificare le configurazioni esistenti usando le stesse stored procedure di sistema e specificare nuovi valori.  
  
## <a name="see-also"></a>Vedere anche  
 [Backup gestito di SQL Server in Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  