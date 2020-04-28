---
title: Backup di file e filegroup (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up filegroups [SQL Server]
- file backups [SQL Server], how-to topics
- backing up files [SQL Server]
- backups [SQL Server], creating
- filegroups [SQL Server], backing up
ms.assetid: a0d3a567-7d8b-4cfe-a505-d197b9a51f70
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c686e5eb9bb44517aa1636dc28c972f6782f8bfe
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782752"
---
# <a name="back-up-files-and-filegroups-sql-server"></a>Backup di file e filegroup (SQL Server)
  In questo argomento viene descritto come eseguire il backup di file e filegroup in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o PowerShell. Quando a causa delle dimensioni del database e dei requisiti relativi alle prestazioni non è consigliabile eseguire un backup completo del database, è possibile creare invece un backup del file. Un *backup del file* contiene tutti i dati inclusi in uno o più file o filegroup. Per altre informazioni sul backup dei file, vedere [Backup completi del file &#40;SQL Server&#41;](full-file-backups-sql-server.md) e [Backup differenziali &#40;SQL Server&#41;](differential-backups-sql-server.md).  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per eseguire il backup di file e filegroup utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Non è possibile utilizzare l'istruzione BACKUP in una transazione esplicita o implicita.  
  
-   In base al modello di recupero con registrazione minima, è necessario creare una copia di backup contenente tutti i file di lettura/scrittura, al fine di garantire che il database possa essere ripristinato fino a un punto nel tempo coerente. Anziché specificare singolarmente ogni file o filegroup di lettura/scrittura, utilizzare l'opzione READ_WRITE_FILEGROUPS. Questa opzione consente di eseguire il backup di tutti i filegroup di lettura/scrittura del database. Un backup creato specificando READ_WRITE_FILEGROUPS è noto come *backup parziale*. Per altre informazioni, vedere [Backup parziali &#40;SQL Server&#41;](partial-backups-sql-server.md).  
  
-   Per altre informazioni sulle limitazioni e restrizioni, vedere [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md).  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Indicazioni  
  
-   Per impostazione predefinita, per ogni operazione di backup eseguita in modo corretto viene aggiunta una voce al log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e al registro eventi di sistema. Se il backup del log viene eseguito di frequente, questi messaggi possono aumentare rapidamente, provocando la creazione di log degli errori di dimensioni elevate e rendendo difficile l'individuazione di altri messaggi. In questi casi è possibile eliminare tali voci di log utilizzando il flag di traccia 3226 se nessuno degli script dipende da esse. Per altre informazioni, vedere [Flag di traccia &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni BACKUP DATABASE e BACKUP LOG vengono assegnate per impostazione predefinita ai membri del ruolo predefinito del server **sysadmin** e dei ruoli predefiniti del database **db_owner** e **db_backupoperator** .  
  
 Eventuali problemi correlati alla proprietà e alle autorizzazioni sul file fisico del dispositivo di backup possono interferire con l'operazione di backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia possibile leggere e scrivere sul dispositivo e che l'account utilizzato per eseguire il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponga delle autorizzazioni di scrittura. Le autorizzazioni di accesso ai file, tuttavia, [non](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)vengono controllate dalla stored procedure sp_addumpdevice , che aggiunge una voce per un dispositivo di backup nelle tabelle di sistema. Di conseguenza, i problemi relativi all'accesso e alla proprietà del file fisico del dispositivo di backup potrebbero emergere solo in fase di accesso alla risorsa fisica durante un tentativo di backup o ripristino.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-back-up-database-files-and-filegroups"></a>Per eseguire il backup di file e filegroup del database  
  
1.  Dopo aver effettuato la connessione all'istanza appropriata del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in Esplora oggetti fare clic sul nome del server per espanderne l'albero.  
  
2.  Espandere **Database**e, a seconda del database, selezionare un database utente o espandere **Database di sistema** e selezionare un database di sistema.  
  
3.  Fare clic con il pulsante destro del mouse sul database, selezionare **Attività**, quindi fare clic su **Esegui backup**. Verrà visualizzata la finestra di dialogo **Backup del database**.  
  
4.  Nell'elenco **Database** verificare il nome del database. È possibile selezionare facoltativamente un database diverso nell'elenco.  
  
5.  Nell'elenco **Tipo di backup** selezionare **Completo** o **Differenziale**.  
  
6.  Selezionare l'opzione **File e filegroup** in **Componente di cui eseguire il backup**.  
  
7.  Selezionare i file e i filegroup dei quali si desidera eseguire il backup nella finestra di dialogo **Seleziona file e filegroup** . È possibile selezionare uno o più file singoli oppure selezionare la casella di controllo relativa a un filegroup per selezionare automaticamente tutti i file appartenenti al filegroup.  
  
8.  Accettare il nome del set di backup predefinito suggerito nella casella di testo **Nome** o immettere un nome diverso.  
  
9. Facoltativamente, immettere una descrizione del set di backup nella casella di testo **Descrizione**.  
  
10. Specificare la scadenza del set di backup:  
  
    -   Per far scadere il set di backup dopo un numero specifico di giorni, fare clic su **Dopo** (opzione predefinita), quindi immettere il numero di giorni che devono trascorrere prima della scadenza del set. È possibile impostare un valore compreso nell'intervallo da 0 a 99999 giorni. L'impostazione del valore 0 giorni indica che il set di backup non ha scadenza.  
  
         Il valore predefinito viene impostato nell'opzione **periodo di memorizzazione predefinito supporti di backup (giorni)** della finestra di dialogo **Proprietà Server** (pagina**Impostazioni database** ). Per accedere a questa opzione, fare clic con il pulsante destro del mouse sul nome del server in Esplora oggetti, scegliere Proprietà e quindi selezionare la pagina **Impostazioni database** .  
  
    -   Per impostare il set di backup in modo che scada in una data specifica, fare clic su **Il** e immettere la data di scadenza del set.  
  
11. Fare clic su **Disco** o su **Nastro**per selezionare il tipo di destinazione del backup. Per selezionare i percorsi per un massimo di 64 unità disco o nastro contenenti un singolo set di supporti, fare clic su **Aggiungi**. I percorsi selezionati vengono visualizzati nell'elenco **Backup su** .  
  
    > [!NOTE]  
    >  Per rimuovere una destinazione di backup, selezionarla e fare clic su **Rimuovi**. Per visualizzare il contenuto di una destinazione di backup, selezionarla e fare clic su **Contenuto**.  
  
12. Per visualizzare o selezionare le opzioni avanzate, fare clic su **Opzioni** nel riquadro **Selezione pagina**.  
  
13. Selezionare un'opzione **Sovrascrivi supporti** facendo clic su uno degli elementi seguenti:  
  
    -   **Esegui backup nel set di supporti esistente**  
  
         Per questa opzione, fare clic su **Accoda al set di backup esistente** o **Sovrascrivi tutti i set di backup esistenti**. Per informazioni sul backup in un set di supporti esistente, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Selezionare facoltativamente l'opzione **Controlla nome set di supporti e scadenza set di backup** per impostare la verifica della data e dell'ora di scadenza del set di supporti e del set di backup durante l'operazione di backup.  
  
         Immettere facoltativamente un nome nella casella di testo **Nome set di supporti** . Se non si specifica un nome, verrà creato un set di supporti con nome vuoto. Se si specifica il nome di un set di supporti, viene eseguito un controllo sul supporto (nastro o disco) per verificare che il nome effettivo corrisponda al nome qui immesso.  
  
         Se non si specifica il nome del set di supporti e si seleziona la casella di controllo per il controllo del nome, in caso di esito positivo anche il nome dei supporti nei supporti risulterà vuoto.  
  
    -   **Esegui backup in un nuovo set di supporti e cancella tutti i set di backup esistenti**  
  
         Per questa opzione, immettere un nome nella casella di testo **Nome nuovo set di supporti** e, se lo si desidera, descrivere il set di supporti nella casella di testo **Descrizione nuovo set di supporti**. Per altre informazioni sulla creazione di un nuovo set di supporti, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
14. Nella sezione **affidabilità** selezionare facoltativamente:  
  
    -   **Verificare il backup al termine**dell'operazione.  
  
    -   **Esegui checksum prima della scrittura nei supporti** e, facoltativamente, **Continua su errore di checksum**. Per altre informazioni sui checksum, vedere [Possibili errori relativi ai supporti durante il backup e il ripristino &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md).  
  
15. Se si esegue il backup su un'unità nastro, come specificato nella sezione **Destinazione** della pagina **Generale** , l'opzione **Scarica nastro al termine del backup** sarà attiva. Selezionando questa opzione viene abilitata anche l'opzione **Riavvolgi il nastro prima di scaricarlo** .  
  
    > [!NOTE]  
    >  Le opzioni presenti nella sezione **Log delle transazioni** sono attive solo in caso di backup di un log delle transazioni, come specificato nella sezione **Tipo backup** nella pagina **Generale** .  
  
16. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]e versioni successive supportano la [compressione dei backup](backup-compression-sql-server.md). Per impostazione predefinita, il fatto che un backup venga o meno compresso dipende dal valore dell'opzione di configurazione del server **Compressione backup predefinita**. Tuttavia, indipendentemente dall'impostazione predefinita a livello del server corrente, è possibile comprimere un backup selezionando la casella **Comprimi backup** e impedirne la compressione selezionando la casella **Non comprimere il backup**.  
  
     **Per visualizzare l'impostazione predefinita corrente della compressione dei backup**  
  
    -   [Visualizzare o configurare l'opzione di configurazione del server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-back-up-files-and-filegroups"></a>Per eseguire il backup di file e filegroup  
  
1.  Per creare un backup del file o del filegroup, usare un'istruzione [BACKUP DATABASE <file_or_filegroup>](/sql/t-sql/statements/backup-transact-sql). In questa istruzione è necessario specificare almeno gli elementi seguenti:  
  
    -   Nome del database.  
  
    -   Una clausola FILE o FILEGROUP per ogni file o filegroup, rispettivamente.  
  
    -   Il dispositivo di backup in cui verrà scritto il backup completo.  
  
     La sintassi [!INCLUDE[tsql](../../includes/tsql-md.md)] di base per un backup del file è la seguente:  
  
     BACKUP DATABASE *database*  
  
     {FILE **=** _logical_file_name_ | Filegroup **=** _logical_filegroup_name_ } [ **,**... *f* ]  
  
     TO *dispositivo_backup* [ **,**...*n* ]  
  
     [ WITH *con_opzioni* [ **,**...*o* ] ];  
  
    |Opzione|Descrizione|  
    |------------|-----------------|  
    |*database*|Nome del database di cui viene eseguito il backup del log delle transazioni oppure il backup parziale o completo del database.|  
    |**=** _Logical_file_name_ file|Specifica il nome logico di un file da includere nel backup del file.|  
    |**=** _Logical_filegroup_name_ filegroup|Specifica il nome logico di un filegroup da includere nel backup del file. Con il modello di recupero con registrazione minima, il backup dei filegroup è consentito solo per i filegroup di sola lettura.|  
    |[ **,**...*f* ]|Segnaposto che indica che è possibile specificare più file e filegroup. Il numero di file o filegroup che possono essere specificati è illimitato.|  
    |*backup_device* [ **,**...*n* ]|Specifica un elenco di dispositivi di backup da 1 a 64 da utilizzare per l'operazione di backup. È possibile specificare un dispositivo di backup fisico oppure un dispositivo di backup logico corrispondente se è già stata definito. Per specificare un dispositivo di backup fisico, utilizzare l'opzione DISK o TAPE:<br /><br /> {DISK &#124; TAPE} **=** _physical_backup_device_name_<br /><br /> Per altre informazioni, vedere [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md).|  
    |WITH *con_opzioni* [ **,**...*o* ]|Facoltativamente, specifica una o più opzioni aggiuntive, ad esempio DIFFERENTIAL.<br /><br /> Nota: il backup differenziale del file richiede come base un backup completo del file. Per altre informazioni, vedere [Creare un backup differenziale del database &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md).|  
  
2.  Se si utilizza il modello di recupero con registrazione completa, è inoltre necessario eseguire un backup del log delle transazioni. Per utilizzare un set completo di backup del file completi per il ripristino di un database, è inoltre necessario disporre di backup dei log relativi a tutti i backup del file, dall'inizio del primo backup del file. Per altre informazioni, vedere [Backup di un log delle transazioni &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md).  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> Esempi (Transact-SQL)  
 Negli esempi seguenti viene eseguito il backup di uno o più file dei filegroup secondari del database `Sales` . Questo database utilizza il modello di recupero con registrazione completa e contiene i filegroup secondari seguenti:  
  
-   Un filegroup denominato `SalesGroup1` che include i file `SGrp1Fi1` e `SGrp1Fi2`.  
  
-   Un filegroup denominato `SalesGroup2` che include i file `SGrp2Fi1` e `SGrp2Fi2`.  
  
#### <a name="a-creating-a-file-backup-of-two-files"></a>A. Creazione di un backup del file per due file  
 Nell'esempio seguente viene creato un backup differenziale del file solo per il file `SGrp1Fi2` del filegroup `SalesGroup1` e per il file `SGrp2Fi2` del filegroup `SalesGroup2` .  
  
```sql  
--Backup the files in the SalesGroup1 secondary filegroup.  
BACKUP DATABASE Sales  
   FILE = 'SGrp1Fi2',   
   FILE = 'SGrp2Fi2'   
   TO DISK = 'G:\SQL Server Backups\Sales\SalesGroup1.bck';  
GO  
```  
  
#### <a name="b-creating-a-full-file-backup-of-the-secondary-filegroups"></a>B. Creazione di un backup completo dei filegroup secondari  
 Nell'esempio seguente viene creato un backup completo di ogni file presente in entrambi i filegroup secondari.  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck';  
GO  
```  
  
#### <a name="c-creating-a-differential-file-backup-of-the-secondary-filegroups"></a>C. Creazione di un backup differenziale dei filegroup secondari  
 Nell'esempio seguente viene creato un backup differenziale di ogni file presente in entrambi i filegroup secondari.  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck'  
   WITH   
      DIFFERENTIAL;  
GO  
```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
  
Utilizzare il cmdlet `Backup-SqlDatabase` e specificare `Files` per il valore del parametro `-BackupAction`. Inoltre, specificare uno dei parametri seguenti:  
  
    -   Per eseguire il backup di un file specifico, `-DatabaseFile`specificare il parametro *String* , dove *String* è uno o più file di database di cui eseguire il backup.  
  
    -   Per eseguire il backup di tutti i file di un determinato filegroup, `-DatabaseFileGroup`specificare il parametro *String* , dove *String* è uno o più filegroup di database di cui eseguire il backup.  
  
     Nell'esempio seguente viene creato un backup completo di ogni file presente nei filegroup secondari 'FileGroup1' e 'FileGroup2' nel database `MyDB` . I backup vengono creati nel percorso di backup predefinito dell'istanza del server `Computer\Instance`.  
  
    ```powershell
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Files -DatabaseFileGroup "FileGroup1","FileGroup2"  
    ```  
  
Per configurare e usare il provider di SQL Server PowerShell, vedere [provider di SQL Server PowerShell](../../powershell/sql-server-powershell-provider.md).
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Informazioni sulla cronologia e sull'intestazione del backup &#40;SQL Server&#41;](backup-history-and-header-information-sql-server.md)   
 [Backup database &#40;pagina generale&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [Pagina Backup database &#40;opzioni di backup&#41;](back-up-database-backup-options-page.md)   
 [Backup completi dei file &#40;SQL Server&#41;](full-file-backups-sql-server.md)   
 [Backup differenziali &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [Ripristini di file &#40;modello di recupero con versione completa&#41;](file-restores-full-recovery-model.md)   
 [Ripristini di file &#40;modello di recupero con registrazione minima&#41;](file-restores-simple-recovery-model.md)  
  
  
