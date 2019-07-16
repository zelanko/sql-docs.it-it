---
title: managed_backup.sp_backup_config_basic (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_basic_TSQL
- sp_backup_config_basic
- managed_backup.sp_backup_config_basic
- managed_backup.sp_backup_config_basic_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_basic
- sp_backup_config_basic
ms.assetid: 3ad73051-ae9a-4e41-a889-166146e5508f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d09fa38377910c2960b43eb6534dba4546538b4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942112"
---
# <a name="managedbackupspbackupconfigbasic-transact-sql"></a>managed_backup.sp_backup_config_basic (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Consente di configurare il [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] impostazioni di base per un database specifico o per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Questa procedura può essere chiamata su una proprio per creare una configurazione di backup gestita di base. Tuttavia, se si prevede di aggiungere funzionalità avanzate o una pianificazione personalizzata, prima di tutto configurare tali impostazioni mediante [managed_backup. sp_backup_config_advanced &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) e [managed_backup.sp_ backup_config_schedule &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) prima di abilitare il backup gestito con questa procedura.  
   
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="Arguments"></a> Argomenti  
 @enable_backup  
 Abilitare o disabilitare il [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per il database specificato. Il @enable_backup viene **BIT**. Parametro obbligatorio quando si configurano [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per la prima istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si modifica un'esistente [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configurazione, questo parametro è facoltativo. In tal caso, i valori di configurazione non è specificati mantengono i valori esistenti.  
  
 @database_name  
 Il nome del database per l'abilitazione del backup gestito in un database specifico.  
  
 @container_url  
 URL che indica la posizione del backup. Quando si @credential_name è NULL, questo URL è un URL di firma di accesso condiviso in un contenitore blob in archiviazione di Azure e i backup usano la nuova funzionalità di backup in blocco blob. Per altre informazioni, esaminare [Understanding SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/). Quando si @credential_name è specificato, questo è un URL di account di archiviazione e i backup usano l'obsoleta funzionalità di backup in pagina blob.  
  
> [!NOTE]  
>  Per questo parametro è supportato solo un URL di firma di accesso condiviso in questo momento.  
  
 @retention_days  
 Periodo di conservazione dei file di backup espresso in giorni. Il @storage_url è INT. Si tratta di un parametro obbligatorio quando si configurano [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per la prima volta nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Durante la modifica di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configurazione, questo parametro è facoltativo. Se non specificato, vengono mantenuti i valori di configurazione esistenti.  
  
 @credential_name  
 Nome delle credenziali SQL utilizzate per l'autenticazione per l'account di archiviazione di Windows Azure. @credentail_name viene **SYSNAME**. Quando specificato, il backup viene archiviato in un blob di pagine. Se questo parametro è NULL, il backup verrà archiviato come blob in blocchi. Backup in blob di pagine è deprecato, pertanto è preferibile utilizzare la nuova funzionalità backup di blob di blocco. Quando utilizzato per modificare la configurazione di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], questo parametro è facoltativo. Se non specificato, vengono mantenuti i valori di configurazione esistente.  
  
> [!WARNING]
>  Il **@credential_name** parametro non è supportato in questo momento. È supportato solo backup in blob in blocchi, che richiede questo parametro deve essere NULL.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **db_backupoperator** ruolo del database con **ALTER ANY CREDENTIAL** autorizzazioni, e **EXECUTE** autorizzazioni sul **sp_delete BackupHistory** stored procedure.  
  
## <a name="examples"></a>Esempi  
 È possibile creare il contenitore dell'account di archiviazione sia l'URL di firma di accesso condiviso usando i comandi di Azure PowerShell più recenti. Nell'esempio seguente crea un nuovo contenitore, mycontainer, nell'account di archiviazione mystorageaccount e quindi Ottiene un URL di firma di accesso condiviso per tale con autorizzazioni complete.  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 L'esempio seguente abilita [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per l'istanza di SQL Server cui viene eseguito, imposta i criteri di conservazione su 30 giorni, imposta la destinazione a un contenitore denominato "mycontainer" in un account di archiviazione denominato 'mystorageaccount'.  
  
```Transact-SQL 
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=1  
                ,@container_url = 'https://mystorageaccount.blob.core.windows.net/mycontainer'  
                ,@retention_days=30;   
GO  
  
```
  
 Nell'esempio seguente viene disabilitato [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per l'istanza di SQL Server sui cui è in esecuzione.  
  
```Transact-SQL  
Use msdb;  
Go  
EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=0;  
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
