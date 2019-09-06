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
ms.openlocfilehash: 92cbea99941b6e9378c4400ae0b563d462c34f27
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70152028"
---
# <a name="managed_backupsp_backup_config_basic-transact-sql"></a>managed_backup.sp_backup_config_basic (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura le [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] impostazioni di base per un database specifico o per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Questa procedura può essere chiamata autonomamente per creare una configurazione di backup gestito di base. Tuttavia, se si prevede di aggiungere funzionalità avanzate o una pianificazione personalizzata, configurare prima tali impostazioni usando [managed_backup. sp_backup_config_advanced &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) e [managed_backup. sp_backup_config_schedule &#40; Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) prima di abilitare il backup gestito con questa procedura.  
   
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="Arguments"></a> Argomenti  
 @enable_backup  
 Abilitare o disabilitare il [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per il database specificato. È @enable_backup di **bit**. Parametro obbligatorio quando si [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configura per la prima istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di. Se si modifica una configurazione esistente [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] , questo parametro è facoltativo. In tal caso, i valori di configurazione non specificati mantengono i valori esistenti.  
  
 @database_name  
 Nome del database per l'abilitazione del backup gestito in un database specifico.  
  
 @container_url  
 URL che indica la posizione del backup. Quando @credential_name è null, questo URL è un URL di firma di accesso condiviso (SAS) a un contenitore BLOB in archiviazione di Azure e i backup usano il nuovo backup per bloccare la funzionalità BLOB. Per altre informazioni, vedere [informazioni sulla firma di accesso condiviso](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/). Quando @credential_name si specifica, si tratta di un URL dell'account di archiviazione e i backup usano la funzionalità di backup deprecato per i BLOB di pagine.  
  
> [!NOTE]  
>  Al momento è supportato solo un URL di firma di accesso condiviso per questo parametro.  
  
 @retention_days  
 Periodo di conservazione dei file di backup espresso in giorni. È @storage_url di tipo int. Si tratta di un parametro obbligatorio quando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] si configura per la prima volta nell'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di. Quando si modifica [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] la configurazione, questo parametro è facoltativo. Se non specificato, vengono mantenuti i valori di configurazione esistenti.  
  
 @credential_name  
 Nome delle credenziali SQL usate per l'autenticazione nell'account di archiviazione di Azure. @credentail_nameè di **tipo sysname**. Quando specificato, il backup viene archiviato in un BLOB di pagine. Se questo parametro è NULL, il backup verrà archiviato come BLOB in blocchi. Il backup nel BLOB di pagine è deprecato, quindi è preferibile usare la nuova funzionalità di backup dei BLOB in blocchi. Quando utilizzato per modificare la configurazione di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], questo parametro è facoltativo. Se non è specificato, vengono conservati i valori di configurazione esistenti.  
  
> [!WARNING]
>  Il **@credential_name** parametro non è supportato in questo momento. È supportato solo il backup in un BLOB in blocchi, che richiede che il parametro sia NULL.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo del database **db_backupoperator** , con autorizzazioni **ALTER ANY CREDENTIAL** e autorizzazioni **Execute** su **sp_delete_backuphistory** stored procedure.  
  
## <a name="examples"></a>Esempi  
 È possibile creare il contenitore dell'account di archiviazione e l'URL della firma di accesso condiviso usando i comandi di Azure PowerShell più recenti. Nell'esempio seguente viene creato un nuovo contenitore, contenitore, nell'account di archiviazione mystorageaccount, quindi viene ottenuto un URL di firma di accesso condiviso con autorizzazioni complete.  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 Nell'esempio seguente viene [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] abilitato per l'istanza di SQL Server in cui viene eseguita, imposta i criteri di conservazione su 30 giorni, imposta la destinazione su un contenitore denominato ' contenitore ' in un account di archiviazione denominato ' mystorageaccount '.  
  
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
  
  
