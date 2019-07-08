---
title: Ripristinare un database in una nuova posizione (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring databases [SQL Server], moving
- database restores [SQL Server], creating new databases
- restoring [SQL Server], with move
- restoring databases [SQL Server], creating new databases
- database backups [SQL Server], creating new database from
- backing up databases [SQL Server], creating new database from
- restoring databases [SQL Server], renaming
- database creation [SQL Server], restoring with move
ms.assetid: 4da76d61-5e11-4bee-84f5-b305240d9f42
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d05f6a469649d959e6ba68e6413ee772025a1d45
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67580327"
---
# <a name="restore-a-database-to-a-new-location-sql-server"></a>Ripristino di un database in una nuova posizione (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questo argomento illustra come ripristinare un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un nuovo percorso e facoltativamente rinominare il database, in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando SQL Server Management Studio (SSMS) o [!INCLUDE[tsql](../../includes/tsql-md.md)]. È possibile spostare un database in un nuovo percorso di directory o crearne una copia nella stessa istanza server o in una diversa.  
    
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   L'amministratore di sistema che esegue il ripristino di un backup completo del database deve essere l'unico utente collegato al database.  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   Nel modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk, prima di poter ripristinare un database, è necessario eseguire il backup del log delle transazioni attivo. Per altre informazioni, vedere [Backup di un log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md).  

-   Per ripristinare un database crittografato, è necessario poter **accedere al certificato o alla chiave asimmetrica usata per crittografare il database**. Non è possibile effettuare l'operazione di ripristino del database senza almeno uno di questi due elementi. Il certificato usato per crittografare la chiave di crittografia del database deve essere mantenuto finché è necessario il backup. Per altre informazioni, vedere [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Per altre considerazioni sullo spostamento di un database, vedere [Copiare database tramite backup e ripristino](../../relational-databases/databases/copy-databases-with-backup-and-restore.md).  
  
-   Se si ripristina un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versione successiva in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], il database viene aggiornato automaticamente. In genere, il database diventa subito disponibile. Se tuttavia un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] include indici full-text, questi vengono importati, reimpostati o ricompilati dal processo di aggiornamento, a seconda dell'impostazione della proprietà del server  **upgrade_option** . Se l'opzione di aggiornamento è impostata per l'importazione (**upgrade_option** = 2) o la ricompilazione (**upgrade_option** = 0), gli indici full-text non saranno disponibili durante l'aggiornamento. A seconda della quantità di dati indicizzati, l'importazione può richiedere diverse ore, mentre la ricompilazione può risultare dieci volte più lunga. Si noti inoltre che quando l'opzione di aggiornamento è impostata sull'importazione, gli indici full-text associati vengono ricompilati se non è disponibile un catalogo full-text. Per modificare l'impostazione della proprietà del server **upgrade_option** , usare [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md).  
  
###  <a name="Security"></a> Sicurezza  
 Per motivi di sicurezza, è consigliabile non collegare o ripristinare database da origini sconosciute o non attendibili. Tali database possono contenere codice dannoso che potrebbe eseguire codice [!INCLUDE[tsql](../../includes/tsql-md.md)] indesiderato o causare errori modificando lo schema o la struttura fisica di database. Prima di utilizzare un database da un'origine sconosciuta o non attendibile, eseguire [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) sul database in un server non di produzione ed esaminare il codice contenuto nel database, ad esempio le stored procedure o altro codice definito dall'utente.  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Se il database da ripristinare non esiste, per eseguire un'operazione RESTORE l'utente deve disporre delle autorizzazioni CREATE DATABASE. Se il database esiste, le autorizzazioni per l'istruzione RESTORE vengono assegnate per impostazione predefinita ai membri dei ruoli predefiniti del server **sysadmin** e **dbcreator** e al proprietario (**dbo**) del database.  
  
 Le autorizzazioni per l'istruzione RESTORE vengono assegnate ai ruoli in cui le informazioni sull'appartenenza sono sempre disponibili per il server. Poiché è possibile controllare l'appartenenza ai ruoli predefiniti del database solo quando il database è accessibile e non è danneggiato, condizioni che non risultano sempre vere quando si esegue un'operazione RESTORE, i membri del ruolo predefinito del database **db_owner** non dispongono delle autorizzazioni per l'istruzione RESTORE.  
  
  
## <a name="restore-a-database-to-a-new-location-optionally-rename-the-database-using-ssms"></a>Ripristinare un database in un nuovo percorso e facoltativamente rinominare il database usando SSMS 

  
1.  Connettersi all'istanza appropriata di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e quindi fare clic sul nome del server in Esplora oggetti per espandere l'albero del server.  
  
2.  Fare clic con il pulsante destro del mouse su **Database**, quindi scegliere **Ripristina database**. Verrà visualizzata la finestra di dialogo **Ripristina database** .  
  
3.  Per specificare l'origine e il percorso dei set di backup da ripristinare, nella pagina **Generale** , utilizzare la sezione **Origine** . Selezionare una delle opzioni seguenti:  
  
    -   **Database**  
  
         Selezionare il database da ripristinare dall'elenco a discesa. Nell'elenco sono inclusi solo i database di cui è stato eseguito il backup in base alla cronologia dei backup di **msdb** .  
  
    > **NOTA:** Se il backup viene eseguito da un server diverso, il server di destinazione non disporrà delle informazioni della cronologia di backup per il database specificato. In questo caso, selezionare **Dispositivo** per specificare manualmente il file o il dispositivo da ripristinare.  
  
    1.  **Dispositivo**  
  
         Fare clic sul pulsante Sfoglia ( **...** ) per aprire la finestra di dialogo **Seleziona dispositivi di backup** . Nella casella **Tipi di supporti di backup** selezionare uno dei tipi di dispositivi elencati. Per selezionare uno o più dispositivi per la casella **Supporti di backup** , fare clic su **Aggiungi**.  
  
         Dopo avere aggiunto i dispositivi desiderati nella casella di riepilogo **Dispositivi di backup** , fare clic su **OK** per tornare alla pagina **Generale** .  
  
         Nella casella di riepilogo **Origine: Dispositivo: Database** selezionare il nome del database da ripristinare.  
  
         **Nota** Questo elenco è disponibile solo se si seleziona **Dispositivo** . Saranno disponibili solo i database che dispongono di backup sul dispositivo selezionato.  
  
4.  Nella sezione **Destinazione** , la casella **Database** viene popolata automaticamente con il nome del database da ripristinare. Per modificare il nome del database, immettere il nome nuovo nella casella **Database** .  
  
5.  Nella casella **Ripristina fino a** mantenere l'impostazione predefinita **Ultimo backup eseguito** oppure fare clic su **Cronologia** per accedere alla finestra di dialogo **Cronologia di backup** e selezionare manualmente un momento specifico per arrestare l'azione di recupero. Per ulteriori informazioni sulla designazione di un momento specifico, vedere [Backup Timeline](../../relational-databases/backup-restore/backup-timeline.md) .  
  
6.  Nella griglia **Selezionare i set di backup da ripristinare** selezionare i set di backup che si desidera ripristinare. In questa griglia vengono visualizzati i backup disponibili per il percorso specificato. Per impostazione predefinita, viene suggerito un piano di recupero. Per ignorare il piano di recupero suggerito, è possibile modificare le impostazioni selezionate nella griglia. I backup che dipendono dal ripristino di un backup precedente vengono automaticamente deselezionati quando il backup precedente è deselezionato.  
  
     Per informazioni sulle colonne nella griglia **Set di backup da ripristinare**, vedere [Ripristina database&#40;(pagina Generale)&#41;](../../relational-databases/backup-restore/restore-database-general-page.md).  
  
7.  Per specificare il nuovo percorso dei file di database, selezionare la pagina **File** , quindi fare clic su **Riloca tutti i file nella cartella**. Fornire un nuovo percorso per **Cartella file di dati** e **Cartella file di log**. Per altre informazioni su questa griglia, vedere [Ripristina database&#40;(pagina File)&#41;](../../relational-databases/backup-restore/restore-database-files-page.md).  
  
8.  Se lo si desidera, regolare le opzioni nella pagina **Opzioni** . Per altre informazioni su queste opzioni, vedere [Ripristina database &#40;(pagina Opzioni)&#41;](../../relational-databases/backup-restore/restore-database-options-page.md).  

 ## <a name="restore-database-to-a-new-location-optionally-rename-the-database-using-t-sql"></a>Ripristinare un database in un nuovo percorso e facoltativamente rinominare il database usando T-SQL
 
 
1.  Facoltativamente, determinare i nomi logici e fisici dei file del set di backup che contiene il backup di database completo da ripristinare. Questa istruzione restituisce un elenco dei file di database e di log contenuti nel set di backup. La sintassi di base è la seguente:  
  
     RESTORE FILELISTONLY FROM *<dispositivo_backup>* WITH FILE = *backup_set_file_number* 
  
     Dove *backup_set_file_number* indica la posizione del backup nel set di supporti. È possibile ottenere la posizione di un set di backup utilizzando l'istruzione [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) . Per altre informazioni, vedere "Specifica di un set di backup" in [Argomenti RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
     Questa istruzione supporta inoltre alcune opzioni WITH. Per altre informazioni, vedere [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md).  
  
2.  Eseguire l'istruzione [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md) per ripristinare il backup di database completo. Per impostazione predefinita, i file di dati e di log vengono ripristinati nei percorsi originali. Per modificare il percorso di un database, utilizzare l'opzione MOVE per spostare ogni file di database e per evitare conflitti con i file esistenti.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     The basic [!INCLUDE[tsql](../../includes/tsql-md.md)] syntax for restoring the database to a new location and a new name is:  
  
     RESTORE DATABASE *new_database_name*  
  
     FROM *backup_device* [ ,...*n* ]  
  
     [ WITH  
  
     {  
  
     [ **RECOVERY** | NORECOVERY ]  
  
     [ , ] [ FILE ={ *backup_set_file_number* | @*backup_set_file_number* } ]  
  
     [ , ] MOVE '*logical_file_name_in_backup*' TO '*operating_system_file_name*' [ ,...*n* ]  
  
     }  
  
     ;  
  
    > **NOTE!** When preparing to relocate a database on a different disk, you should verify that sufficient space is available and identify any potential collisions with existing files. This involves using a [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md) statement that specifies the same MOVE parameters that you plan to use in your RESTORE DATABASE statement.  
  
     The following table describes arguments of this RESTORE statement in terms of restoring a database to a new location. For more information about these arguments, see [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
     *new_database_name*  
     The new name for the database.  
  
    >**NOTE:** If you are restoring the database to a different server instance, you can use the original database name instead of a new name.  
  
     *backup_device* [ **,**...*n* ]  
     Specifies a comma-separated list of from 1 to 64 backup devices from which the database backup is to be restored. You can specify a physical backup device, or you can specify a corresponding logical backup device, if defined. To specify a physical backup device, use the DISK or TAPE option:  
  
     { DISK | TAPE } **=**_physical_backup_device_name_  
  
     For more information, see [Backup Devices &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
     { **RECOVERY** | NORECOVERY }  
     If the database uses the full recovery model, you might need to apply transaction log backups after you restore the database. In this case, specify the NORECOVERY option.  
  
     Otherwise, use the RECOVERY option, which is the default.  
  
     FILE = { *backup_set_file_number* | @*backup_set_file_number* }  
     Identifies the backup set to be restored. For example, a *backup_set_file_number* of **1** indicates the first backup set on the backup medium and a *backup_set_file_number* of **2** indicates the second backup set. You can obtain the *backup_set_file_number* of a backup set by using the [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) statement.  
  
     When this option is not specified, the default is to use the first backup set on the backup device.  
  
     For more information, see "Specifying a Backup Set," in [RESTORE Arguments &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
     MOVE **'**_logical_file_name_in_backup_**'** TO **'**_operating_system_file_name_**'** [ **,**...*n* ]  
     Specifies that the data or log file specified by *logical_file_name_in_backup* is to be restored to the location specified by *operating_system_file_name*. Specify a MOVE statement for every logical file you want to restore from the backup set to a new location.  
  
    |Opzione|Descrizione|  
    |------------|-----------------|  
    |*logical_file_name_in_backup*|Specifica il nome logico di un file di dati o di log da includere nel set di backup. Il nome di file logico di un file di dati o di log in un set di backup corrisponde al relativo nome logico nel database al momento della creazione del set di backup.<br /><br /> <br /><br /> Nota: per ottenere un elenco dei file logici del set di backup, usare [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md).|  
    |*operating_system_file_name*|Specifica un nuovo percorso per il file indicato da *logical_file_name_in_backup*. Il file verrà ripristinato a questo percorso.<br /><br /> Facoltativamente, *operating_system_file_name* specifica un nuovo nome per il file ripristinato. Questo passaggio è necessario se si crea una copia di un database esistente nella stessa istanza del server.|  
    |*n*|Segnaposto tramite cui viene indicata la possibilità di specificare istruzioni MOVE aggiuntive.|  
  
###  <a name="TsqlExample"></a> Esempio (Transact-SQL)  
 In questo esempio viene creato un nuovo database denominato `MyAdvWorks` ripristinando un backup del database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] in cui sono inclusi due file: [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Data e [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Log. In questo database viene utilizzato il modello di recupero con registrazione minima. Il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] è già presente nell'istanza del server, pertanto i file del backup devono essere ripristinati in un nuovo percorso. L'istruzione RESTORE FILELISTONLY viene utilizzata per stabilire il numero e i nomi dei file del database da ripristinare. Il backup del database corrisponde al primo set disponibile sul dispositivo.  
  
> **NOTA:** Gli esempi di backup e di ripristino del log delle transazioni, inclusi i ripristini temporizzati, utilizzano il database `MyAdvWorks_FullRM` creato da [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] esattamente come nell'esempio seguente basato su `MyAdvWorks` . Per usare il modello di recupero con registrazione completa è tuttavia necessario modificare il database `MyAdvWorks_FullRM` risultante usando l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente: ALTER DATABASE <nome_database> SET RECOVERY FULL.  
  
```sql  
USE master;  
GO  
-- First determine the number and names of the files in the backup.  
-- AdventureWorks2012_Backup is the name of the backup device.  
RESTORE FILELISTONLY  
   FROM AdventureWorks2012_Backup;  
-- Restore the files for MyAdvWorks.  
RESTORE DATABASE MyAdvWorks  
   FROM AdventureWorks2012_Backup  
   WITH RECOVERY,  
   MOVE 'AdventureWorks2012_Data' TO 'D:\MyData\MyAdvWorks_Data.mdf',   
   MOVE 'AdventureWorks2012_Log' TO 'F:\MyLog\MyAdvWorks_Log.ldf';  
GO  
  
```  
  
 Per un esempio relativo alla creazione di un backup completo del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , vedere [Creare un backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Related tasks  
  
-   [Creazione di un backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Ripristino di un backup del database con SQL Server Management Studio](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire i metadati quando si rende disponibile un database in un'altra istanza del server &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Copiare database tramite backup e ripristino](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)  
  
  
