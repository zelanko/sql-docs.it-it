---
title: Creare un backup completo del database (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c43fbe12b8449fb231ee9a2f479ff17ac0281493
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530753"
---
# <a name="create-a-full-database-backup-sql-server"></a>Creazione di un backup completo del database (SQL Server)
  In questo argomento viene descritto come creare un backup completo del database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o PowerShell.  
  
> [!NOTE]  
>  Per informazioni sul backup di SQL Server nel servizio di archiviazione BLOB di Windows Azure, vedere [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Windows Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un database completo di backup, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Non è possibile utilizzare l'istruzione BACKUP in una transazione esplicita o implicita.  
  
-   I backup creati nella versione più recente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non possono essere ripristinati nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Per altre informazioni, vedere [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md).  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Poiché le dimensioni del database aumentano, i backup completi del database richiedono più tempo e più spazio di archiviazione. Per un database di grandi dimensioni può pertanto essere utile integrare un backup completo del database con una serie di *backup database differenziali*. Per altre informazioni, vedere [Backup differenziali &#40;SQL Server&#41;](differential-backups-sql-server.md).  
  
-   È possibile stimare la dimensione di un backup del database completo tramite la stored procedure di sistema [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) .  
  
-   Per impostazione predefinita, per ogni operazione di backup eseguita in modo corretto viene aggiunta una voce al log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e al registro eventi di sistema. Se il backup del log viene eseguito di frequente, questi messaggi possono aumentare rapidamente, provocando la creazione di log degli errori di dimensioni elevate e rendendo difficile l'individuazione di altri messaggi. In questi casi è possibile eliminare tali voci di log utilizzando il flag di traccia 3226 se nessuno degli script dipende da esse. Per altre informazioni, vedere [Flag di traccia &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).  
  
###  <a name="Security"></a> Sicurezza  
 TRUSTWORTHY è impostato su OFF in un backup del database. Per informazioni su come impostare TRUSTWORTHY su ON, vedere [Opzioni ALTER DATABASE SET &#40; Transact-SQL &#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
 A partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], le opzioni `PASSWORD` e `MEDIAPASSWORD` non sono più disponibili per la creazione di backup. È possibile ripristinare backup creati con password.  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni BACKUP DATABASE e BACKUP LOG vengono assegnate per impostazione predefinita ai membri del ruolo predefinito del server **sysadmin** e dei ruoli predefiniti del database **db_owner** e **db_backupoperator** .  
  
 Eventuali problemi correlati alla proprietà e alle autorizzazioni sul file fisico del dispositivo di backup possono interferire con l'operazione di backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia possibile leggere e scrivere sul dispositivo e che l'account utilizzato per eseguire il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponga delle autorizzazioni di scrittura. Le autorizzazioni di accesso ai file, tuttavia, non vengono controllate dalla stored procedure [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)che aggiunge una voce per un dispositivo di backup nelle tabelle di sistema. Di conseguenza, i problemi relativi all'accesso e alla proprietà del file fisico del dispositivo di backup potrebbero emergere solo in fase di accesso alla risorsa fisica durante un tentativo di backup o ripristino.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
> [!NOTE]  
>  Quando si specifica un'attività di backup usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è possibile generare lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](/sql/t-sql/statements/backup-transact-sql) corrispondente facendo clic sul pulsante **Script** e selezionando una destinazione per lo script.  
  
#### <a name="to-back-up-a-database"></a>Per eseguire il backup di un database  
  
1.  Dopo aver stabilito la connessione all'istanza appropriata del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in Esplora oggetti fare clic sul nome del server per espandere l'albero del server.  
  
2.  Espandere **Database**e, a seconda del database, selezionare un database utente o espandere **Database di sistema** e selezionare un database di sistema.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **Attività**e fare clic su **Backup**. Verrà visualizzata la finestra di dialogo **Backup database** .  
  
4.  Nel `Database` casella di riepilogo, verificare il nome del database. È possibile selezionare facoltativamente un database diverso nell'elenco.  
  
5.  È possibile eseguire il backup di un database per qualsiasi modello di recupero (**FULL**, **BULK_LOGGED**o **SIMPLE**).  
  
6.  Nella casella di riepilogo **Tipo di backup** selezionare **Completo**.  
  
     Si noti che dopo aver eseguito un backup completo, è possibile creare un backup differenziale del database. Per altre informazioni, vedere [Creare un backup differenziale del database &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md).  
  
7.  Facoltativamente, è possibile selezionare **Backup di sola copia** per creare un backup di sola copia. Un *backup di sola copia* è un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indipendente dalla sequenza di backup convenzionali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Backup di sola copia &#40;SQL Server&#41;](copy-only-backups-sql-server.md).  
  
    > [!NOTE]  
    >  Quando si seleziona l'opzione **Differenziale** , non è possibile creare un backup di sola copia.  
  
8.  Per la **componente di Backup**, fare clic su `Database`.  
  
9. Accettare il nome predefinito del set di backup indicato nella casella di testo **Nome** oppure immettere un nome diverso per il set di backup.  
  
10. Facoltativamente, immettere una descrizione del set di backup nella casella di testo **Descrizione** .  
  
11. Scegliere il tipo di destinazione di backup facendo clic su **Disco**, **Nastro** o **URL**. Per selezionare i percorsi per un massimo di 64 unità disco o nastro contenenti un singolo set di supporti, fare clic su **Aggiungi**. I percorsi selezionati vengono visualizzati nella casella di riepilogo **Backup su** .  
  
     Per rimuovere una destinazione di backup, selezionarla e fare clic su **Rimuovi**. Per visualizzare il contenuto di una destinazione di backup, selezionarla e fare clic su **Contenuto**.  
  
12. Per visualizzare o selezionare le opzioni dei supporti, fare clic su **Opzioni supporti** nel riquadro **Selezione pagina** .  
  
13. Selezionare un'opzione **Sovrascrivi supporti** facendo clic su una delle opzioni seguenti:  
  
    -   **Esegui backup nel set di supporti esistente**  
  
         Per questa opzione, fare clic su **Accoda al set di backup esistente** o **Sovrascrivi tutti i set di backup esistenti**. Per altre informazioni, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Selezionare facoltativamente l'opzione **Controlla nome set di supporti e scadenza set di backup** per impostare la verifica della data e dell'ora di scadenza del set di supporti e del set di backup durante l'operazione di backup.  
  
         Immettere facoltativamente un nome nella casella di testo **Nome set di supporti** . Se non si specifica un nome, verrà creato un set di supporti con nome vuoto. Se si specifica un nome per il set di supporti, il supporto (nastro o disco) verrà controllato per verificare che il nome effettivo corrisponda al nome specificato.  
  
        > [!IMPORTANT]  
        >  Questa opzione è disabilitata se è stato selezionato **URL** come destinazione di backup nella pagina **Generale** . Per altre informazioni, vedere [Backup database &#40;pagina Opzioni di backup &#41;](back-up-database-media-options-page.md)  
        >   
        >  Se si intende utilizzare la crittografia, non selezionare questa opzione. Se si seleziona questa opzione, le opzioni di crittografia nella pagina **Opzioni di backup** saranno disabilitate. La crittografia non è supportata quando si esegue un accodamento al set di backup esistenti.  
  
    -   **Esegui backup in un nuovo set di supporti e cancella tutti i set di backup esistenti**  
  
         Per questa opzione, immettere un nome nella casella di testo **Nome nuovo set di supporti** e, facoltativamente, aggiungere una descrizione per il set di supporti nella casella di testo **Descrizione nuovo set di supporti** .  
  
        > [!IMPORTANT]  
        >  Questa opzione è disabilitata se è stato selezionato **URL** nella pagina **Generale** . Queste azioni non sono supportate durante l'esecuzione del backup nel Servizio di archiviazione Windows Azure.  
  
14. Nella sezione **Affidabilità** è possibile selezionare facoltativamente:  
  
    -   **Verifica backup al termine**.  
  
    -   **Esegui checksum prima della scrittura nei supporti**e, facoltativamente, **Continua in caso di errori checksum**. Per informazioni sui checksum, vedere [Possibili errori relativi ai supporti durante il backup e il ripristino &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md).  
  
15. Se si esegue il backup su un'unità nastro (come specificato nella sezione **Destinazione** della pagina **Generale**) l'opzione **Scarica nastro al termine del backup** sarà attiva. Se si seleziona questa opzione, verrà inoltre attivata l'opzione **Riavvolgi il nastro prima di scaricarlo** .  
  
    > [!NOTE]  
    >  Le opzioni presenti nella sezione **Log delle transazioni** sono attive solo in caso di backup di un log delle transazioni (come specificato nella sezione **Tipo backup** della pagina **Generale** ).  
  
16. Per visualizzare o selezionare le opzioni di backup, fare clic su **Opzioni di backup** nel riquadro **Selezione pagina** .  
  
17. Specificare quando il set di backup scadrà e potrà essere sovrascritto senza ignorare esplicitamente la verifica dei dati relativi alla scadenza:  
  
    -   Per impostare una scadenza specifica per il set di backup, fare clic su **Dopo** (opzione predefinita) e immettere il numero di giorni dopo la creazione del set trascorsi i quali il set scadrà. È possibile impostare un valore compreso nell'intervallo da 0 a 99999 giorni. L'impostazione del valore 0 giorni indica che il set di backup non ha scadenza.  
  
         Il valore predefinito viene impostato nell'opzione **Periodo di memorizzazione predefinito supporti di backup (giorni)** della finestra di dialogo **Proprietà server** (pagina delle impostazioni del database). Per accedere alla pagina, fare clic con il pulsante destro del mouse sul nome del server in Esplora oggetti e scegliere Proprietà, quindi selezionare la pagina **Impostazioni database** .  
  
    -   Per impostare una data di scadenza specifica per il set di backup, fare clic su **Il**e immettere la data di scadenza del set.  
  
         Per altre informazioni sulle date di scadenza dei backup, vedere [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
18. [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] e versioni successive supporta la [compressione dei backup](backup-compression-sql-server.md). Per impostazione predefinita, la compressione di un backup dipende dal valore dell'opzione di configurazione del server **Valore predefinito di compressione backup**. Tuttavia, indipendentemente dall'impostazione predefinita a livello di server corrente, è possibile comprimere un backup selezionando **Comprimi backup**ed è possibile impedire la compressione selezionando **Non comprimere il backup**.  
  
     **Per visualizzare o modificare l'impostazione predefinita corrente della compressione dei backup**  
  
    -   [Visualizzare o configurare l'opzione di configurazione del server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
19. Specificare se utilizzare la crittografia per il backup. Selezionare un algoritmo di crittografia da utilizzare per il passaggio di crittografia e specificare un certificato o una chiave asimmetrica da un elenco di chiavi asimmetriche o di certificati esistenti. La crittografia è supportata in SQL Server 2014 o versioni successive. Per altre informazioni sulle opzioni di crittografia, vedere [Backup database &#40;pagina Opzioni di backup &#41;](back-up-database-backup-options-page.md).  
  
> [!NOTE]  
>  In alternativa, è possibile creare i backup di database tramite Creazione guidata piano di manutenzione.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-full-database-backup"></a>Per creare un backup completo del database  
  
1.  Per creare backup completo del database, eseguire l'istruzione BACKUP DATABASE specificando:  
  
    -   Il nome del database di cui eseguire il backup.  
  
    -   Il dispositivo di backup in cui archiviare il backup completo del database.  
  
     La sintassi di base dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] per un backup completo del database è la seguente:  
  
     BACKUP DATABASE *database*  
  
     TO *dispositivo_backup* [ **,**...*n* ]  
  
     [ WITH *con_opzioni* [ **,**...*o* ] ];  
  
    |Opzione|Descrizione|  
    |------------|-----------------|  
    |*database*|Corrisponde al database di cui eseguire il backup.|  
    |*dispositivo_backup* [ **,**...*n* ]|Specifica un elenco di dispositivi di backup da 1 a 64 da utilizzare per l'operazione di backup. È possibile specificare un dispositivo di backup fisico oppure un dispositivo di backup logico corrispondente se è già stata definito. Per specificare un dispositivo di backup fisico, utilizzare l'opzione DISK o TAPE:<br /><br /> { DISK &#124; TAPE } **=**_nome_dispositivo_backup_fisico_<br /><br /> Per altre informazioni, vedere [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md).|  
    |WITH *con_opzioni* [ **,**...*o* ]|Facoltativamente, specifica una o più opzioni aggiuntive, *o*. Per informazioni su alcune opzioni WITH di base, vedere il passaggio 2.|  
  
2.  Facoltativamente, specificare uno o più opzioni WITH. Alcune opzioni WITH di base sono descritte di seguito. Per informazioni su tutte le opzioni WITH, vedere [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
    -   Opzioni WITH del set di backup di base:  
  
         { COMPRESSION | NO_COMPRESSION }  
         Solo in [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] e versioni successive, specifica se la [compressione backup](backup-compression-sql-server.md) è eseguita su questo backup, ignorando l'impostazione predefinita a livello di server.  
  
         ENCRYPTION (ALGORITHM,  SERVER CERTIFICATE |ASYMMETRIC KEY)  
         Solo in SQL Server 2014 o versioni successive specificare l'algoritmo di crittografia da utilizzare e il certificato o la chiave asimmetrica da utilizzare per proteggere la crittografia.  
  
         DESCRIPTION **=** { **'*`text`*'** | **@**_text_variable_ }  
         Specifica il testo in formato libero che descrive il set di backup. La stringa può essere composta da un massimo di 255 caratteri.  
  
         NAME **=** { *nome_set_backup* | **@**_variabile_nome_set_backup_ }  
         Specifica il nome del set di backup. I nomi possono essere composti da un massimo di 128 caratteri. Se si omette NAME, al set di backup non viene assegnato alcun nome specifico.  
  
    -   Opzioni WITH del set di backup di base:  
  
         Per impostazione predefinita, BACKUP accoda il backup a un set di supporti esistente, conservando i set di backup esistenti. E possibile specificarlo in modo esplicito utilizzando l'opzione NOINIT. Per informazioni sull'accodamento a set di backup esistenti, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
         In alternativa, utilizzare l'opzione FORMAT per formattare i supporti di backup:  
  
         FORMAT [ **,** MEDIANAME**=** { *nome_supporto* | **@**_variabile_nome_supporto_ } ] [ **,** MEDIADESCRIPTION **=** { *testo* | **@**_variabile_testo_ } ]  
         Utilizzare la clausola FORMAT, se i supporti vengono utilizzati per la prima volta o si desiderano sovrascrivere tutti i dati esistenti. Facoltativamente, assegnare al nuovo supporto un nome e una descrizione.  
  
        > [!IMPORTANT]  
        >  Utilizzare la clausola FORMAT dell'istruzione BACKUP con estrema cautela, in quanto entrambe comportano la cancellazione di eventuali backup archiviati in precedenza nei supporti di backup.  
  
###  <a name="TsqlExample"></a> Esempi (Transact-SQL)  
  
#### <a name="a-backing-up-to-a-disk-device"></a>A. Esecuzione del backup su un dispositivo disco  
 Nell'esempio riportato di seguito viene eseguito il backup su disco del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] completo, utilizzando `FORMAT` per creare un nuovo set di supporti.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="b-backing-up-to-a-tape-device"></a>B. Esecuzione del backup su un dispositivo nastro  
 Nell'esempio seguente viene eseguito il backup completo su nastro del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], accodandolo ai backup precedenti.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="c-backing-up-to-a-logical-tape-device"></a>C. Esecuzione del backup su un dispositivo nastro logico  
 Nell'esempio seguente viene creato in un dispositivo di backup logico per un'unità nastro. Nell'esempio viene quindi eseguito il backup completo del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] su quel dispositivo.  
  
```sql  
-- Create a logical backup device,   
-- AdventureWorks2012_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'AdventureWorks2012_Bak_Tape', '\\.\tape0'; USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO AdventureWorks2012_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'AdventureWorks2012_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
  
1.  Utilizzare il cmdlet `Backup-SqlDatabase`. Per indicare in modo esplicito che si tratta di un backup completo del database, specificare il **- BackupAction** parametro con il valore predefinito, `Database`. Questo parametro è facoltativo per i backup completi di database.  
  
     L'esempio seguente consente di creare un backup di database completo del database di `MyDB` nel percorso di backup predefinito dell'istanza del server `Computer\Instance`. Facoltativamente, in questo esempio viene specificato `-BackupAction Database`.  
  
    ```  
    --Enter this command at the PowerShell command prompt, C:\PS>  
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
    ```  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Eseguire il backup di un database (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [Creare un backup differenziale del database &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [Ripristinare un Backup del Database &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Ripristinare un backup del database nel modello di recupero con registrazione minima &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Ripristinare un database fino al punto di errore nel modello di recupero con registrazione completa &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Ripristinare un database in una nuova posizione &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
-   [Utilizzare la Creazione guidata piano di manutenzione](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Backup di log delle transazioni &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Eseguire il backup di database &#40;pagina Generale&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [Eseguire il backup di database &#40;pagina Opzioni di backup&#41;](back-up-database-backup-options-page.md)   
 [Backup differenziali &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [Backup completo del database &#40;SQL Server&#41;](full-database-backups-sql-server.md)  
  
  
