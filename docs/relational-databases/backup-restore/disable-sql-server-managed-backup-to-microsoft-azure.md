---
title: Disabilitare il backup gestito in Archiviazione BLOB di Azure
description: Questo articolo illustra come disabilitare o sospendere Backup gestito di SQL Server in Microsoft Azure sia a livello di database che di istanza usando Transact-SQL.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 3e02187f-363f-4e69-a82f-583953592544
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c14d2ab4c8ab3f24272b30df0de5ca9727ffb4bd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85737794"
---
# <a name="disable-sql-server-managed-backup-to-microsoft-azure"></a>Disabilitare il backup gestito di SQL Server in Microsoft Azure
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Questo argomento descrive come disabilitare o sospendere [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] a livello di database e di istanza.  
  
##  <a name="disable-ss_smartbackup-for-a-database"></a><a name="DatabaseDisable"></a> Disabilitare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per un database  
 È possibile disabilitare le impostazioni di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usando la stored procedure di sistema [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md). Il parametro *\@enable_backup* consente di abilitare e disabilitare le configurazioni di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per un database specifico. Il valore 1 abilita e il valore 0 disabilita le impostazioni di configurazione.  
  
#### <a name="to-disable-ss_smartbackup-for-a-specific-database"></a>Per disabilitare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per un database specifico:  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
```sql
EXEC msdb.managed_backup.sp_backup_config_basic  
                @database_name = 'TestDB'   
                ,@enable_backup = 0;  
GO
```

> [!NOTE]
> Potrebbe anche essere necessario impostare il parametro `@container_url` in base alla configurazione.
  
##  <a name="disable-ss_smartbackup-for-all-the-databases-on-the-instance"></a><a name="DatabaseAllDisable"></a> Disabilitare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per tutti i database dell'istanza  
 La procedura seguente viene utilizzata quando si desidera disabilitare le impostazioni di configurazione di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] da tutti i database con [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] abilitato attualmente nell'istanza.  Le impostazioni di configurazione come l'URL di archiviazione, la memorizzazione e le credenziali SQL rimarranno nei metadati ed è possibile usarle se si abilita [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per il database in un secondo momento. Se si vuole sospendere solo temporaneamente i servizi [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] , è possibile usare l'opzione master descritta nelle sezioni successive di questo argomento.  
  
#### <a name="to-disable-ss_smartbackup-for-all-the-databases"></a>Per disabilitare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per tutti i database:  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. L'esempio seguente determina se [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] è configurato a livello di istanza e tutti i database abilitati da [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] nell'istanza ed esegue la stored procedure di sistema **sp_backup_config_basic** per disabilitare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
```sql
-- Create a working table to store the database names  
Declare @DBNames TABLE  
  
       (  
             RowID int IDENTITY PRIMARY KEY  
             ,DBName varchar(500)  
  
       )  
-- Define the variables  
DECLARE @rowid int  
DECLARE @dbname varchar(500)  
DECLARE @SQL varchar(2000)  
-- Get the database names from the system function  
  
INSERT INTO @DBNames (DBName)  
  
SELECT db_name  
       FROM   
  
       msdb.managed_backup.fn_backup_db_config (NULL)  
       WHERE is_managed_backup_enabled = 1 
       AND is_dropped = 0
  
       --Select DBName from @DBNames  
  
       select @rowid = min(RowID)  
       FROM @DBNames  
  
       WHILE @rowID IS NOT NULL  
       Begin  
  
             Set @dbname = (Select DBName From @DBNames Where RowID = @rowid)  
             Begin  
             Set @SQL = 'EXEC msdb.managed_backup.sp_backup_config_basic    
                @database_name= '''+'' + @dbname+ ''+''',   
                @enable_backup=0'  
  
            EXECUTE (@SQL)  
  
             END  
             Select @rowid = min(RowID)  
             From @DBNames Where RowID > @rowid  
  
       END  
```  
  
 Per verificare le impostazioni di configurazione per tutti i database nell'istanza, utilizzare la query seguente:  
  
```sql
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_db_config (NULL);  
GO  
```  
  
##  <a name="disable-default-ss_smartbackup-settings-for-the-instance"></a><a name="InstanceDisable"></a> Disabilitare le impostazioni predefinite di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per l'istanza  
 Le impostazioni predefinite a livello di istanza vengono applicate a tutti i nuovi database creati nell'istanza in questione.  Se le impostazioni predefinite non sono più necessarie o richieste, è possibile disabilitare questa configurazione usando la stored procedure di sistema **managed_backup.sp_backup_config_basic** con il parametro *\@database_name* impostato su NULL. La disabilitazione non comporta la rimozione delle altre impostazioni di configurazione come l'URL di archiviazione, l'impostazione di memorizzazione o il nome delle credenziali SQL. Queste impostazioni verranno utilizzate se [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] viene abilitato per l'istanza in un secondo momento.  
  
#### <a name="to-disable-ss_smartbackup-default-configuration-settings"></a>Per disabilitare le impostazioni di configurazione predefinite di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] :  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```sql
    EXEC msdb.managed_backup.sp_backup_config_basic  
                    @enable_backup = 0;  
    GO
    ```  
  
##  <a name="pause-ss_smartbackup-at-the-instance-level"></a><a name="InstancePause"></a> Sospendere [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] a livello di istanza  
 In alcuni casi è possibile che sia necessario sospendere temporaneamente i servizi [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per un breve periodo.  La stored procedure di sistema **managed_backup.sp_backup_master_switch** consente di disabilitare il servizio [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] a livello di istanza.  La stessa stored procedure viene utilizzata per riprendere [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Il parametro \@state viene usato per definire se [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] deve essere disattivato o attivato.  
  
#### <a name="to-pause-ss_smartbackup-services-using-transact-sql"></a>Per sospendere i servizi [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] tramite Transact-SQL:  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
```sql
Use msdb;  
GO  
EXEC managed_backup.sp_backup_master_switch @new_state=0;  
Go
```  
  
#### <a name="to-resume-ss_smartbackup-using-transact-sql"></a>Per riprendere [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] tramite Transact-SQL  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
```sql
Use msdb;  
Go  
EXEC managed_backup.sp_backup_master_switch @new_state=1;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Abilitare il backup gestito di SQL Server in Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)  
  
  
