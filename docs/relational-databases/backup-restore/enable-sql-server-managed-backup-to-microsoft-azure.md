---
title: Usare il backup gestito in Azure
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.description: Enable SQL Server managed backup to Azure
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e59dfd9c79090bc20a517367e0145303822d8079
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "78280888"
---
# <a name="enable-sql-server-managed-backup-to-azure"></a>Abilitare il backup gestito di SQL Server in Azure

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questo argomento descrive come abilitare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con le impostazioni predefinite a livello di database e di istanza. Viene descritta anche la procedura per abilitare le notifiche tramite posta elettronica e monitorare l'attività di backup.  
  
 In questa esercitazione viene usato Azure PowerShell. Prima di iniziare l'esercitazione, [scaricare e installare Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).  
  
> [!IMPORTANT]  
>  Per abilitare anche le opzioni avanzate o usare una pianificazione personalizzata, configurare tali impostazioni prima di abilitare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Per altre informazioni, vedere [Configurare le opzioni avanzate per il backup gestito di SQL Server in Microsoft Azure](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="create-the-azure-blob-container"></a>Creare il contenitore BLOB di Azure

Il processo richiede un account Azure. Se è già disponibile un account, procedere con il passaggio successivo. In caso contrario, è possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/) oppure esaminare le [opzioni per l'acquisto](https://azure.microsoft.com/pricing/purchase-options/).

Per altre informazioni sugli account di archiviazione, vedere [Informazioni sugli account di archiviazione di Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/). 

#### <a name="azure-cli"></a>[Interfaccia della riga di comando di Azure](#tab/azure-cli)

1. Accedere all'account Azure.

    ```azurecli-interactive
    az login
    ```
  
1. Creare un account di archiviazione di Azure. se si dispone già di un account di archiviazione, andare al passaggio successivo. Il comando seguente crea un account di archiviazione denominato `<backupStorage>` nell'area Stati Uniti orientali.  
  
    ```azurecli-interactive
    az storage account create -n <backupStorage> -l "eastus" --resource-group <resourceGroup>
    ```  
    
1. Creare un contenitore BLOB denominato `<backupContainer>` per i file di backup.
  
    ```azurecli-interactive
    $keys = az storage account keys list --account-name <backupStorage> --resource-group <resourceGroup> | ConvertFrom-Json
    az storage container create --name <backupContainer> --account-name <backupStorage> --account-key $keys[0].value 
    ```  
  
1. Generare una firma di accesso condiviso per accedere al contenitore. Il comando seguente crea un token della firma di accesso condiviso per il contenitore BLOB `<backupContainer>` con scadenza annuale.  
  
    ```azurecli-interactive 
    az storage container generate-sas --name <backupContainer> --account-name <backupStorage> --account-key $keys[0].value
    ```

#### <a name="powershell"></a>[PowerShell](#tab/azure-powershell)

1. Il comando seguente consente di accedere al proprio account Azure.

    ```azurepowershell-interactive
    Connect-AzAccount
    Set-AzContext -SubscriptionId "<subscriptionId>"
    ```
  
1. Creare un account di archiviazione di Azure. se si dispone già di un account di archiviazione, andare al passaggio successivo. Il comando seguente crea un account di archiviazione denominato `<backupStorage>` nell'area Stati Uniti orientali.  
  
    ```azurepowershell-interactive
    New-AzStorageAccount -StorageAccountName <backupStorage> -Location "EAST US" -ResourceGroupName <resourceGroup> -SkuName Standard_GRS
    ```   
  
1. Creare un contenitore BLOB denominato `<backupContainer>` per i file di backup.  
  
    ```azurepowershell-interactive
    $context = New-AzStorageContext -StorageAccountName <backupStorage> -StorageAccountKey (Get-AzStorageAccountKey -Name <backupStorage> -ResourceGroupName <resourceGroup>).Value[0]  
    New-AzStorageContainer -Name <backupContainer> -Context $context  
    ```  
  
1. Generare una firma di accesso condiviso per accedere al contenitore. Il comando seguente crea un token della firma di accesso condiviso per il contenitore BLOB `<backupContainer>` con scadenza annuale.
  
    ```azurepowershell-interactive 
    New-AzStorageContainerSASToken -Name <backupContainer> -Permission rwdl -ExpiryTime (Get-Date).AddYears(1) -FullUri -Context $context 
    ```

* * *

> [!NOTE]
> Questi passaggi possono essere eseguiti anche usando il [portale di Azure](https://portal.azure.com/).

L'output conterrà l'URL del contenitore e/o il token della firma di accesso condiviso. Di seguito è riportato un esempio:  
  
  `https://managedbackupstorage.blob.core.windows.net/backupcontainer?sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl`
  
Se l'URL è incluso, separarlo dal token della firma di accesso condiviso in corrispondenza del punto interrogativo (non includere il punto interrogativo). Ad esempio, l'output precedente corrisponde ai due valori seguenti.  
  
|||  
|-|-|  
|**URL del contenitore**|https://managedbackupstorage.blob.core.windows.net/backupcontainer|  
|**Token della firma di accesso condiviso**|sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl|  
|||
  
Registrare l'URL del contenitore e la firma di accesso condiviso per usarli per la creazione di una credenziale SQL. Per altre informazioni su SAS, vedere [Firme di accesso condiviso, parte 1: informazioni sul modello di firma di accesso condiviso](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/).  
  
## <a name="enable-managed-backup-to-azure"></a>Abilitare il backup gestito in Azure
  
1.  **Creare credenziali SQL per l'URL di firma di accesso condiviso:** usare il token di firma di accesso condiviso per creare credenziali SQL per l'URL del contenitore BLOB. In SQL Server Management Studio usare la query Transact-SQL seguente per creare la credenziale per l'URL del contenitore BLOB in base all'esempio seguente:  
  
    ```sql  
    CREATE CREDENTIAL [https://managedbackupstorage.blob.core.windows.net/backupcontainer]   
    WITH IDENTITY = 'Shared Access Signature',  
    SECRET = 'sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl'  
    ```  
  
2.  **Assicurarsi che il servizio SQL Server Agent sia avviato e in esecuzione:** se non è in esecuzione, avviare SQL Server Agent.  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] è necessaria l'esecuzione di SQL Server Agent nell'istanza per poter eseguire le operazioni di backup.  Per assicurarsi che le operazioni in questione vengano eseguite regolarmente, è possibile impostare l'esecuzione automatica di SQL Server Agent.  
  
3.  **Determinare il periodo di conservazione:** determinare il periodo di conservazione per i file di backup. Il periodo di memorizzazione viene specificato in giorni in un intervallo compreso tra 1 e 30.  
  
4.  **Abilitare e configurare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:** avviare SQL Server Management Studio e connettersi all'istanza di SQL Server di destinazione. Nella finestra Query eseguire l'istruzione seguente dopo aver modificato i valori per il nome del database, l'URL del contenitore e il periodo di memorizzazione in base alle esigenze:  
  
    > [!IMPORTANT]  
    >  Per abilitare il backup gestito a livello di istanza, specificare `NULL` per il parametro `database_name` .  
  
    ```sql  
    USE msdb;  
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
  
    ```sql
    SELECT * FROM msdb.managed_backup.fn_get_current_xevent_settings()  
    ```  
  
     Verificare che gli eventi dei canali amministrativo, operativo e analitico siano abilitati per impostazione predefinita e che non possano essere disabilitati. Questa verifica dovrebbe essere sufficiente per monitorare gli eventi per i quali è richiesto un intervento manuale.  È possibile abilitare eventi di debug, ma nei canali di debug sono inclusi eventi informativi e di debug utilizzati dal [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per rilevare eventuali problemi e risolverli.  
  
6.  **Abilitare e configurare notifiche per lo stato di integrità:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] contiene una stored procedure che consente di creare un processo dell'agente per inviare notifiche via posta elettronica di errori o avvisi che potrebbero richiedere attenzione. Nei passaggi seguenti viene illustrato il processo per abilitare e configurare le notifiche tramite posta elettronica:  
  
    1.  Configurare Posta elettronica database se non è già abilitato nell'istanza. Per altre informazioni, vedere [Configurare Posta elettronica database](../../relational-databases/database-mail/configure-database-mail.md).  
  
    2.  Configurare la notifica di SQL Server Agent per l'uso di Posta elettronica database. Per altre informazioni, vedere [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  **Abilitare le notifiche di posta elettronica per ricevere avvisi ed errori di backup:** nella finestra di query eseguire le istruzioni Transact-SQL seguenti:  
  
        ```sql
        EXEC msdb.managed_backup.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
        ```  
  
7.  **Visualizzare i file di backup nell'account di archiviazione di Azure:** connettersi all'account di archiviazione da SQL Server Management Studio o dal portale di Azure. Verranno visualizzati gli eventuali file di backup disponibili nel contenitore specificato. Potrebbe essere visualizzato un backup del database e del log entro 5 minuti dall'abilitazione del [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per il database.  
  
8.  **Monitorare lo stato di integrità:**  è possibile eseguire il monitoraggio attraverso notifiche tramite posta elettronica configurate in precedenza o monitorare attivamente gli eventi registrati. Di seguito sono riportate alcune istruzioni Transact-SQL di esempio utilizzate per visualizzare gli eventi:  
  
    ```sql  
    --  view all admin events  
    USE msdb;  
    GO  
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
    USE msdb;  
    GO  
    EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
    ```  
  
    ```sql  
    --  View all events in the current week  
    USE msdb;  
    GO  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
    ```
  
I passaggi descritti in questa sezione riguardano in modo specifico la configurazione del [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per la prima volta nel database. È possibile modificare le configurazioni esistenti usando le stesse stored procedure di sistema e specificare nuovi valori.  
  
## <a name="see-also"></a>Vedere anche  
 [Backup gestito di SQL Server in Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
