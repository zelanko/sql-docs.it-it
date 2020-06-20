---
title: Dispositivi di backup (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- tape backup devices, about tape backup devices
- backup devices [SQL Server]
- disk backup devices [SQL Server]
- database backups [SQL Server], backup devices
- logical devices [SQL Server]
- backup devices [SQL Server], about backup devices
- backing up [SQL Server], backup devices
- removable media [SQL Server]
- network shares [SQL Server]
- backups [SQL Server], backup devices
- tape backup devices
- physical devices [SQL Server]
- backing up databases [SQL Server], backup devices
- devices [SQL Server]
ms.assetid: 35a8e100-3ff2-4844-a5da-dd088c43cba4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a8abbba087679d263c00484764ecf445d6e5a006
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84959331"
---
# <a name="backup-devices-sql-server"></a>Dispositivi di backup (SQL Server)
  Durante un'operazione di backup su un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , i dati sottoposti a *backup*vengono scritti in un dispositivo di backup fisico. Tale dispositivo di backup fisico viene inizializzato quando si scrive su di esso il primo backup di un set di supporti. I backup disponibili in un set di uno o più dispositivi di backup costituiscono un singolo set di supporti.  
  
 **Contenuto dell'argomento**  
  
-   [Termini e definizioni](#TermsAndDefinitions)  
  
-   [Uso di dispositivi di backup su disco](#DiskBackups)  
  
-   [Uso di dispositivi nastro](#TapeDevices)  
  
-   [Utilizzo di un dispositivo di backup logico](#LogicalBackupDevice)  
  
-   [Set di supporti di backup con mirroring](#MirroredMediaSets)  
  
-   [Archiviazione di backup di SQL Server](#Archiving)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="terms-and-definitions"></a><a name="TermsAndDefinitions"></a>Termini e definizioni  
 disco di backup  
 Disco rigido o altro supporto di archiviazione su disco in cui sono contenuti uno o più file di backup. Un file di backup è un file normale del sistema operativo.  
  
 set di supporti  
 Raccolta ordinata di nastri, file su disco o supporti di backup in cui vengono utilizzati un tipo e un numero fisso di dispositivi di backup. Per informazioni sui set di supporti, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
 dispositivo di backup fisico  
 Unità nastro o file su disco fornito dal sistema operativo. È possibile scrivere un backup su un massimo di 64 dispositivi di backup. Se un backup richiede più dispositivi di backup, tutti devono corrispondere a un unico tipo di dispositivo, ovvero disco o nastro.  
  
 I backup di SQL Server possono essere scritti nel servizio Archiviazione BLOB di Azure oltre che su disco o nastro.  
  
##  <a name="using-disk-backup-devices"></a><a name="DiskBackups"></a>Uso di dispositivi di backup su disco  
 **Contenuto della sezione**  
  
-   [Specifica di un file di backup utilizzando il nome fisico (Transact-SQL)](#BackupFileUsingPhysicalName)  
  
-   [Impostazione del percorso di un file di backup su disco](#BackupFileDiskPath)  
  
-   [Esecuzione del backup in un file in una condivisione di rete](#NetworkShare)  
  
 Se lo spazio su disco assegnato a un file si esaurisce mentre è in corso l'aggiunta di un backup al set di supporti durante un'operazione di backup, l'operazione avrà esito negativo. Le dimensioni massime di un file di backup sono determinate dallo spazio libero su disco disponibile nel dispositivo disco. Le dimensioni appropriate per un dispositivo disco di backup dipendono pertanto dalle dimensioni dei backup eseguiti.  
  
 Un dispositivo di backup su disco può essere un semplice dispositivo disco, come un'unità ATA. In alternativa, è possibile utilizzare un'unità disco collegabile a caldo che consenta di sostituire in modo trasparente un disco vuoto a un disco pieno presente nell'unità. Un disco di backup può essere un disco locale nel server o un disco remoto, ovvero una risorsa di rete condivisa. Per informazioni sull'utilizzo di un disco remoto, vedere [Esecuzione del backup in un file in una condivisione di rete](#NetworkShare)di seguito in questo argomento.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gli strumenti di gestione consentono grande flessibilità nella gestione dei dispositivi di backup su disco, in quanto permettono di generare automaticamente un nome timestamp nel file su disco.  
  
> [!IMPORTANT]  
>  È consigliabile utilizzare come disco di backup un disco diverso da quelli in cui sono archiviati i dati di database e i log. Questa condizione è necessaria per garantire l'accesso ai backup in caso di errore del disco contenente il log o i dati.  
  
###  <a name="specifying-a-backup-file-by-using-its-physical-name-transact-sql"></a><a name="BackupFileUsingPhysicalName"></a>Specifica di un file di backup utilizzando il nome fisico (Transact-SQL)  
 La sintassi di base di [BACKUP](/sql/t-sql/statements/backup-transact-sql) per specificare un file di backup utilizzando il nome del dispositivo fisico è la seguente:  
  
 BACKUP DATABASE *database_name*  
  
 TO DISK **=** { **'** _physical_backup_device_name_ **'**  |  **@** _physical_backup_device_name_var_ }  
  
 Ad esempio:  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak';  
GO  
```  
  
 La sintassi di base per specificare un dispositivo disco fisico in un'istruzione [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) è la seguente:  
  
 RESTORE { DATABASE | LOG } *database_name*  
  
 FROM DISK **=** { **'** _physical_backup_device_name_ **'**  |  **@** _physical_backup_device_name_var_ }  
  
 Ad esempio,  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak';   
```  
  
###  <a name="specifying-the-path-of-a-disk-backup-file"></a><a name="BackupFileDiskPath"></a>Specifica del percorso di un file di backup su disco  
 Quando si specifica un file di backup, è consigliabile immetterne il percorso completo e il nome di file. Quando si esegue il backup di un file, se si specifica solo il nome del file o un percorso relativo, il file di backup viene inserito nella directory di backup predefinita. La directory di backup predefinita è C:\Programmi\Microsoft SQL Server\MSSQL.*n*\MSSQL\Backup, dove *n* rappresenta il numero dell'istanza del server. La directory di backup predefinita per l'istanza del server predefinita è pertanto C:\Programmi\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Backup.  
  
 Per evitare ambiguità, in particolare negli script, è consigliabile specificare in modo esplicito il percorso della directory di backup in ogni clausola DISK. Questa indicazione risulta tuttavia meno importante quando si utilizza l'editor di query. In questo caso infatti, se si è certi che il file di backup si trovi nella directory di backup predefinita, è possibile omettere il percorso dalla clausola DISK. Ad esempio, l'istruzione `BACKUP` seguente consente di effettuare il backup del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] nella directory di backup predefinita.  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = 'AdventureWorks2012.bak';  
GO  
```  
  
> [!NOTE]  
>  Il percorso predefinito è archiviato nella chiave del Registro di sistema **BackupDirectory** in **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.n\MSSQLServer**.  
  
###  <a name="backing-up-to-a-file-on-a-network-share"></a><a name="NetworkShare"></a>Esecuzione del backup in un file in una condivisione di rete  
 Per accedere a un file su disco remoto tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario che l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abbia accesso alla condivisione di rete e disponga delle autorizzazioni necessarie per eseguire operazioni di scrittura nella condivisione di rete durante il backup e di lettura durante il ripristino. La disponibilità delle autorizzazioni e delle unità di rete dipende dal contesto in cui viene eseguito il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Per eseguire il backup in un'unità di rete quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito in un account utente di dominio, è necessario eseguire il mapping dell'unità condivisa a un'unità di rete nella sessione in cui viene eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se si avvia Sqlservr.exe dalla riga di comando, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono rilevate tutte le unità di rete di cui è stato eseguito il mapping nella sessione di accesso.  
  
-   Quando si esegue Sqlservr.exe come servizio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito in una sessione separata che non ha alcuna relazione con la sessione di accesso. La sessione in cui viene eseguito un servizio può disporre di proprie unità di cui è stato eseguito il mapping, sebbene questo solitamente non avvenga.  
  
-   È possibile connettersi all'account del servizio di rete utilizzando l'account del computer anziché un utente di dominio. Per consentire i backup da computer specifici in un'unità condivisa, concedere l'accesso agli account dei computer. Purché il processo Sqlservr.exe che scrive il backup abbia accesso, è irrilevante che l'utente che invia il comando BACKUP abbia accesso.  
  
    > [!IMPORTANT]  
    >  Il backup dei dati in una rete può essere soggetto agli errori della rete stessa. Quando si utilizza un disco remoto, è pertanto consigliabile verificare l'operazione di backup dopo il suo completamento. Per altre informazioni, vedere [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql).  
  
#### <a name="specifying-a-universal-naming-convention-unc-name"></a>Specifica di un nome UNC (Universal Naming Convention)  
 Per specificare una condivisione di rete in un comando di backup o ripristino, è necessario utilizzare il nome UNC (Universal Naming Convention) completo del file per il dispositivo di backup. Il formato di un nome UNC è **\\\\** _NomeSistema_ **\\** _NomeCondivisione_ **\\** _Percorso_ **\\** _NomeFile_.  
  
 Ad esempio:  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = '\\BackupSystem\BackupDisk1\AW_backups\AdventureWorksData.Bak';  
GO  
```  
  
##  <a name="using-tape-devices"></a><a name="TapeDevices"></a>Uso di dispositivi nastro  
  
> [!NOTE]  
>  Il supporto per i dispositivi di backup su nastro verrà rimosso in una versione futura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata.  
  
 **Contenuto della sezione**  
  
-   [Specifica di un nastro di backup utilizzando il nome fisico (Transact-SQL)](#BackupTapeUsingPhysicalName)  
  
-   [Opzioni di BACKUP e ripristino specifiche del nastro (Transact-SQL)](#TapeOptions)  
  
-   [Gestione dei nastri aperti](#OpenTapes)  
  
 Il backup dei dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su nastro richiede che l'unità o le unità nastro siano supportate dal sistema operativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Per ogni unità nastro è inoltre opportuno utilizzare solo nastri consigliati dal produttore di tale unità. Per ulteriori informazioni sull'installazione di un'unità nastro, vedere la documentazione per il sistema operativo Windows.  
  
 Quando viene utilizzata un'unità nastro, se durante il backup un nastro viene completato, è possibile continuare su un altro nastro. Ogni nastro include un'intestazione supporto. Il primo supporto utilizzato è denominato *nastro iniziale*. Ogni nastro successivo è noto come *nastro di continuità* e dispone di un numero di sequenza del supporto maggiore rispetto al nastro precedente. In un set di supporti associato a quattro dispositivi nastro, ad esempio, sono presenti almeno quattro nastri iniziali e, se lo spazio non è sufficiente per il database, quattro serie di nastri di continuità. Quando si accoda un set di backup, è necessario montare l'ultimo nastro della serie. Se l'ultimo nastro non è montato, tramite [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene eseguita un'analisi in avanti fino alla fine del nastro montato e quindi viene richiesto di cambiare il nastro. A questo punto, montare l'ultimo nastro.  
  
 I dispositivi di backup su nastro vengono utilizzati come dispositivi disco, con le eccezioni seguenti:  
  
-   Il dispositivo nastro deve essere collegato fisicamente al computer in cui è in esecuzione un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il backup su dispositivi nastro remoti non è supportato.  
  
-   Se durante l'operazione di backup lo spazio disponibile su un dispositivo di backup su nastro si esaurisce, ma rimangono ancora dati da registrare, tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene richiesto di inserire un nuovo nastro e l'operazione di backup continua dopo il caricamento del nuovo nastro.  
  
###  <a name="specifying-a-backup-tape-by-using-its-physical-name-transact-sql"></a><a name="BackupTapeUsingPhysicalName"></a>Specifica di un nastro di backup utilizzando il nome fisico (Transact-SQL)  
 La sintassi di base di [BACKUP](/sql/t-sql/statements/backup-transact-sql) per specificare un nastro di backup utilizzando il nome di dispositivo fisico dell'unità nastro è la seguente:  
  
 BACKUP { DATABASE | LOG } *database_name*  
  
 TO TAPE **=** { **'** _physical_backup_device_name_ **'**  |  **@** _physical_backup_device_name_var_ }  
  
 Ad esempio:  
  
```  
BACKUP LOG AdventureWorks2012   
   TO TAPE = '\\.\tape0';  
GO  
```  
  
 La sintassi di base per specificare un dispositivo nastro fisico in un'istruzione [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) è la seguente:  
  
 RESTORE { DATABASE | LOG } *database_name*  
  
 FROM TAPE **=** { **'** _physical_backup_device_name_ **'**  |  **@** _physical_backup_device_name_var_ }  
  
###  <a name="tape-specific-backup-and-restore-options-transact-sql"></a><a name="TapeOptions"></a>Opzioni di BACKUP e ripristino specifiche del nastro (Transact-SQL)  
 Per facilitare la gestione dei nastri, per l'istruzione BACKUP sono disponibili le opzioni seguenti specifiche dei nastri:  
  
-   { NOUNLOAD | **UNLOAD** }  
  
     È possibile controllare se un nastro di backup viene scaricato automaticamente dall'unità nastro dopo un'operazione di backup o ripristino. UNLOAD/NOUNLOAD è un'impostazione di sessione che rimane valida per l'intera durata della sessione o finché non viene reimpostata tramite la specifica di un'impostazione alternativa.  
  
-   { **REWIND** | NOREWIND }  
  
     È possibile controllare se il nastro viene mantenuto aperto da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dopo l'operazione di backup o ripristino oppure viene rilasciato e riavvolto quando è pieno. Il comportamento predefinito prevede il riavvolgimento del nastro (REWIND).  
  
> [!NOTE]  
>  Per altre informazioni sulla sintassi e sugli argomenti di BACKUP, vedere [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql). Per altre informazioni sulla sintassi e gli argomenti di RESTORE, vedere [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql) e [Argomenti dell'istruzione RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql).  
  
###  <a name="managing-open-tapes"></a><a name="OpenTapes"></a>Gestione dei nastri aperti  
 Per visualizzare un elenco dei dispositivi nastro aperti e lo stato delle richieste di montaggio, eseguire una query nella DMV [sys.dm_io_backup_tapes](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql) . Questa vista contiene tutti i nastri aperti, inclusi i nastri in uso che risultano temporaneamente inattivi in quanto in attesa dell'operazione BACKUP o RESTORE successiva.  
  
 Se un nastro viene inavvertitamente lasciato aperto, il modo più rapido per rilasciarlo consiste nell'usare il comando seguente: RESTORE REWINDONLY FROM TAPE **=** _backup_device_name_. Per altre informazioni, vedere [RESTORE REWINDONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-rewindonly-transact-sql).  
  
## <a name="using-the-azure-blob-storage-service"></a>Uso del servizio di archiviazione BLOB di Azure  
 I backup di SQL Server possono essere scritti nel servizio Archiviazione BLOB di Azure.  Per altre informazioni su come usare il servizio di archiviazione BLOB di Azure per i backup, vedere [SQL Server backup e ripristino con il servizio di archiviazione BLOB di Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
##  <a name="using-a-logical-backup-device"></a><a name="LogicalBackupDevice"></a>Uso di un dispositivo di backup logico  
 Un *dispositivo di backup logico* è un nome facoltativo definito dall'utente tramite cui viene fatto riferimento a un dispositivo di backup fisico specifico, ovvero un file su disco o un'unità nastro. Un dispositivo di backup logico consente di utilizzare i riferimenti indiretti per fare riferimento al dispositivo di backup fisico corrispondente.  
  
 La definizione di un dispositivo di backup logico implica l'assegnazione di un nome logico a un dispositivo fisico. Ad esempio, un dispositivo logico, AdventureWorksBackups, può essere definito in modo da puntare al file Z:\SQLServerBackups\AdventureWorks2012.bak o all'unità nastro \\\\.\tape0. Nei comandi di backup e di ripristino è quindi possibile specificare come dispositivo di backup AdventureWorksBackups anziché DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak' o TAPE = '\\\\.\tape0'.  
  
 Il nome del dispositivo logico deve essere univoco tra tutti i dispositivi di backup logici nell'istanza del server. Per visualizzare i nomi dei dispositivi logici esistenti, eseguire una query nella vista del catalogo [sys.backup_devices](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql) . Questa vista contiene il nome di ogni dispositivo di backup logico, nonché una descrizione del tipo e del nome di file o del percorso fisico del dispositivo di backup fisico corrispondente.  
  
 Dopo aver definito un dispositivo di backup logico, in un comando BACKUP o RESTORE è possibile specificare il dispositivo di backup logico anziché il nome fisico del dispositivo. Ad esempio, l'istruzione seguente esegue il backup del database `AdventureWorks2012` nel dispositivo di backup logico `AdventureWorksBackups` .  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO AdventureWorksBackups;  
GO  
```  
  
> [!NOTE]  
>  In una determinata istruzione BACKUP o RESTORE, il nome del dispositivo di backup logico e il nome del dispositivo di backup fisico corrispondente sono intercambiabili.  
  
 Un vantaggio offerto dall'utilizzo di un dispositivo di backup logico è la semplicità di impiego rispetto a un percorso lungo. Un dispositivo di backup logico può essere utile se si intende scrivere una serie di backup nello stesso percorso o in un dispositivo nastro. I dispositivi di backup logici sono particolarmente utili per identificare i dispositivi di backup su nastro.  
  
 È possibile scrivere uno script di backup per l'utilizzo di un particolare dispositivo di backup logico. Ciò consente di passare a nuovi dispositivi di backup fisici senza aggiornare lo script. Tale passaggio richiede il processo seguente:  
  
1.  Eliminazione del dispositivo di backup logico originale.  
  
2.  Definizione di un nuovo dispositivo di backup logico che utilizzi il nome del dispositivo logico originale ma esegua il mapping a un dispositivo di backup fisico diverso. I dispositivi di backup logici sono particolarmente utili per identificare i dispositivi di backup su nastro.  
  
##  <a name="mirrored-backup-media-sets"></a><a name="MirroredMediaSets"></a>Set di supporti di backup con mirroring  
 Il mirroring dei set di supporti di backup riduce l'effetto di eventuali funzionamenti non corretti dei dispositivi di backup. Tali problemi possono risultare estremamente gravi, poiché i backup rappresentano l'ultima difesa contro la perdita dei dati. Con l'aumento delle dimensioni dei database, cresce il rischio che un errore di un dispositivo o di un supporto di backup impedisca il ripristino di un backup. I supporti di backup con mirroring aumentano l'affidabilità dei backup garantendo la ridondanza per il dispositivo di backup fisico. Per altre informazioni, vedere [Set di supporti di backup con mirroring &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md).  
  
> [!NOTE]  
>  I set di supporti di backup con mirroring sono supportati solo in [!INCLUDE[ssEnterpriseEd2005](../../includes/ssenterpriseed2005-md.md)] e versioni successive.  
  
##  <a name="archiving-sql-server-backups"></a><a name="Archiving"></a>Archiviazione SQL Server backup  
 È consigliabile utilizzare un'utilità di backup del file system per l'archiviazione dei backup del disco, nonché conservare gli archivi in una posizione esterna. L'utilizzo del disco consente di utilizzare la rete per scrivere i backup archiviati in un disco esterno. Il servizio Archiviazione BLOB di Azure può essere usato come opzione di archiviazione esterna.  È possibile caricare i backup su disco o scriverli direttamente nel servizio Archiviazione BLOB di Azure.  
  
 Un altro approccio comune all'archiviazione consiste nello scrivere backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un disco di backup locale, archiviarli su nastro e quindi archiviare i nastri in una posizione esterna.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
 **Per specificare un dispositivo disco (SQL Server Management Studio)**  
  
-   [Specificare un disco o un nastro come destinazione di backup &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
 **Per specificare un dispositivo nastro (SQL Server Management Studio)**  
  
-   [Specificare un disco o un nastro come destinazione di backup &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
 **Per definire un dispositivo di backup logico**  
  
-   [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)  
  
-   [Definire un dispositivo di backup logico per un file su disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definizione di un dispositivo di backup logico per un'unità nastro &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.BackupDevice> (SMO)  
  
 **Per utilizzare un dispositivo di backup logico**  
  
-   [Specificare un disco o un nastro come destinazione di backup &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Ripristinare un backup da un dispositivo &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
-   [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)  
  
-   [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
 **Per visualizzare informazioni sui dispositivi di backup**  
  
-   [Informazioni sulla cronologia e sull'intestazione del backup &#40;SQL Server&#41;](backup-history-and-header-information-sql-server.md)  
  
-   [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
 **Per eliminare un dispositivo di backup logico**  
  
-   [sp_dropdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdevice-transact-sql)  
  
-   [Eliminare un dispositivo di backup &#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Backup Device di SQL Server](../performance-monitor/sql-server-backup-device-object.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Piani di manutenzione](../maintenance-plans/maintenance-plans.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)   
 [sys.backup_devices &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql)   
 [sys.dm_io_backup_tapes &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql)   
 [Set di supporti di backup con mirroring &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md)  
  
  
