---
title: Backup di SQL Server nell'URL | Microsoft Docs
ms.custom: ''
ms.date: 01/25/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 11be89e9-ff2a-4a94-ab5d-27d8edf9167d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d3911ab34a01b2da971aa602df37c8c559ed6390
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62920742"
---
# <a name="sql-server-backup-to-url"></a>Backup di SQL Server nell'URL
  In questo argomento vengono introdotti i concetti, i requisiti e i componenti necessari per utilizzare il servizio di archiviazione BLOB di Windows Azure come destinazione di backup. La funzionalità di backup e ripristino è uguale o simile a quella delle opzioni DISK e TAPE, con alcune differenze. Nell'argomento sono descritte le differenze e le eccezioni rilevanti e sono inclusi alcuni esempi di codice.  
  
## <a name="requirements-components-and-concepts"></a>Requisiti, componenti e concetti  
 **Contenuto della sezione:**  
  
-   [Sicurezza](#security)  
  
-   [Introduzione ai componenti e ai concetti chiave](#intorkeyconcepts)  
  
-   [Windows Azure Blob Storage Service](#Blob)  
  
-   [Componenti di SQL Server](#sqlserver)  
  
-   [Limitazioni](#limitations)  
  
-   [Supporto per le istruzioni di backup/ripristino](#Support)  
  
-   [Utilizzo dell'attività di backup in SQL Server Management Studio](sql-server-backup-to-url.md#BackupTaskSSMS)  
  
-   [Backup di SQL Server nell'URL tramite la Creazione guidata piano di manutenzione](sql-server-backup-to-url.md#MaintenanceWiz)  
  
-   [Ripristino dal servizio di archiviazione Windows Azure mediante SQL Server Management Studio](sql-server-backup-to-url.md#RestoreSSMS)  
  
###  <a name="security"></a> Sicurezza  
 Di seguito sono riportati requisiti e considerazioni sulla sicurezza a cui attenersi per l'esecuzione del backup nei servizi di archiviazione BLOB di Windows Azure o del ripristino da questi servizi.  
  
-   Quando si crea un contenitore per il servizio di archiviazione BLOB di Windows Azure, è consigliabile impostare l'accesso su **privato**. In questo modo si limita l'accesso agli utenti o account in grado di fornire le informazioni necessarie per l'autenticazione per l'account di Windows Azure.  
  
    > [!IMPORTANT]  
    >  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene richiesto che il nome dell'account di Windows Azure e l'autenticazione delle chiavi di accesso siano archiviati in credenziali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Queste informazioni vengono utilizzate per l'autenticazione dell'account di Windows Azure quando vengono eseguite operazioni di backup o ripristino.  
  
-   All'account utente usato per eseguire i comandi BACKUP o RESTORE deve essere associato il ruolo del database **db_backup operator** con autorizzazioni **Modifica qualsiasi credenziale** .  
  
###  <a name="intorkeyconcepts"></a> Introduzione ai componenti e ai concetti chiave  
 Nelle due sezioni seguenti vengono illustrati il servizio di archiviazione BLOB di Windows Azure e i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzati durante l'esecuzione del backup nel servizio di archiviazione BLOB di Windows Azure o del ripristino dallo stesso. È importante comprendere i componenti e la relativa interazione per eseguire il backup nel servizio di archiviazione BLOB di Windows Azure o il ripristino dallo stesso.  
  
 La creazione di un account di Windows Azure è il primo passaggio di questo processo. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Usa il **nome account di archiviazione Windows Azure** e il relativo **chiave di accesso** i valori per autenticare, scrivere e leggere BLOB nel servizio di archiviazione. Le credenziali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tramite cui vengono archiviate queste informazioni di autenticazione, vengono utilizzate durante le operazioni di backup o ripristino. Per una procedura dettagliata completa della creazione di un account di archiviazione e dell'esecuzione di un ripristino semplice, vedere l' [esercitazione per l'uso del servizio di archiviazione di Microsoft Azure per il backup e il ripristino di SQL Server](https://go.microsoft.com/fwlink/?LinkId=271615).  
  
 ![mapping di account di archiviazione alle credenziali sql](../../tutorials/media/backuptocloud-storage-credential-mapping.gif "mapping account di archiviazione alle credenziali sql")  
  
###  <a name="Blob"></a> Windows Azure Blob Storage Service  
 **Account di archiviazione:** l'account di archiviazione è il punto di partenza per tutti i servizi di archiviazione. Per accedere al servizio di archiviazione BLOB di Windows Azure, creare innanzitutto un account di archiviazione di Windows Azure. Il valore di **storage account name** e delle corrispondenti proprietà **access key** è necessario per eseguire l'autenticazione per il servizio di archiviazione BLOB di Windows Azure e i relativi componenti.  
  
 **Contenitore:** Un contenitore fornisce un raggruppamento di un set di BLOB e può archiviare un numero illimitato di BLOB. Per scrivere un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel servizio BLOB di Windows Azure, è necessario aver creato almeno il contenitore radice.  
  
 **BLOB:** file di qualsiasi tipo e dimensioni. Esistono due tipi di BLOB che è possibile archiviare nel servizio di archiviazione BLOB di Windows Azure: BLOB in blocchi e di pagine. Nel backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il tipo di BLOB utilizzato è quello di pagine. I BLOB sono indirizzabili usando il formato di URL seguente: https://\<account di archiviazione >.blob.core.windows.net/\<contenitore > /\<blob >  
  
 ![Archiviazione BLOB di Azure](../../database-engine/media/backuptocloud-blobarchitecture.gif "Archiviazione BLOB di Azure")  
  
 Per ulteriori informazioni sul servizio di archiviazione BLOB di Windows Azure, vedere la pagina relativa alla [modalità di utilizzo del servizio di archiviazione BLOB di Windows Azure](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)  
  
 Per ulteriori informazioni sui BLOB di pagine, vedere la pagina [Informazioni sui Blob in blocchi e sui Blob di pagine](https://msdn.microsoft.com/library/windowsazure/ee691964.aspx)  
  
###  <a name="sqlserver"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Components  
 **URL:** un URL specifica un URI (Uniform Resource Identifier) in un file di backup univoco. L'URL viene utilizzato per specificare il percorso e il nome del file di backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In questa implementazione, l'unico URL valido è quello che punta a un BLOB di pagine di un account di archiviazione di Windows Azure. L'URL deve puntare a un BLOB effettivo, non solo a un contenitore. Se il BLOB non è disponibile, viene creato. Se un Blob esistente viene specificato, BACKUP ha esito negativo, a meno che non è specificata l'opzione "WITH FORMAT".  
  
> [!WARNING]  
>  Se si sceglie di copiare e caricare un file di backup nel servizio di archiviazione BLOB di Windows Azure, utilizzare i BLOB di pagine come opzione di archiviazione. I ripristini dai BLOB in blocchi non sono supportati. Il ripristino da un BLOB in blocchi non viene completato e viene visualizzato un errore.  
  
 Questo è un valore URL di esempio: http[s]://ACCOUNTNAME.Blob.Core.Windows.NET/\<contenitore > /\<nomefile >. Anche se non richiesto, è consigliabile utilizzare HTTPS.  
  
 **Credenziale:** una credenziale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un oggetto usato per archiviare le informazioni di autenticazione necessarie per la connessione a una risorsa all'esterno di SQL Server.  In questo caso, nei processi di backup e ripristino di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le credenziali vengono utilizzate per l'autenticazione per il servizio di archiviazione BLOB di Windows Azure. Nelle credenziali vengono archiviati il nome dell'account di archiviazione e i relativi valori della **chiave di accesso** . Una volta create, le credenziali devono essere specificate nell'opzione WITH CREDENTIAL durante l'esecuzione delle istruzioni BACKUP/RESTORE. Per ulteriori informazioni sulla modalità di visualizzazione, copia o rigenerazione dell'account di archiviazione **access keys**, vedere la pagina relativa alle [chiavi di accesso dell'account di archiviazione](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx).  
  
 Per istruzioni dettagliate sulla creazione di credenziali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere l'esempio [Create a Credential](#credential) più avanti in questo argomento.  
  
 Per informazioni generali sulle credenziali, vedere la pagina [Credenziali](../security/authentication-access/credentials-database-engine.md)  
  
 Per informazioni o altri esempi in cui vengono utilizzate le credenziali, vedere [Creazione di un proxy di SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md).  
  
###  <a name="limitations"></a> Limitazioni  
  
-   Il backup in Archiviazione Premium non è supportato.  
  
-   Le dimensioni massime di backup supportate sono 1 TB.  
  
-   È possibile eseguire istruzioni di backup o ripristino tramite TSQL, SMO o cmdlet di PowerShell. L'esecuzione di un backup nel servizio di archiviazione BLOB di Windows Azure o di un ripristino dallo stesso tramite il Backup o ripristino guidato di SQL Server Management Studio non è attualmente abilitata.  
  
-   La creazione di un nome di dispositivo logico non è supportata. Di conseguenza, non è supportata neanche l'aggiunta di un URL come dispositivo di backup tramite sp_dumpdevice o SQL Server Management Studio.  
  
-   L'accodamento ai BLOB di backup esistenti non è supportato. I backup in un BLOB esistente possono solo essere sovrascritti tramite l'opzione WITH FORMAT.  
  
-   Il backup in più BLOB effettuato con una singola operazione non è supportato. Ad esempio, se si esegue l'operazione riportata di seguito viene restituito un errore:  
  
    ```  
    BACKUP DATABASE AdventureWorks2012   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_1.bak'   
       URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_2.bak'   
          WITH CREDENTIAL = 'mycredential'   
         ,STATS = 5;  
    GO  
  
    ```  
  
-   La specifica delle dimensioni del blocco con `BACKUP` non è supportata.  
  
-   La specifica di `MAXTRANSFERSIZE` non è supportata.  
  
-   La specifica delle opzioni del set di backup, `RETAINDAYS` e `EXPIREDATE`, non è supportata.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è previsto un limite massimo di 259 caratteri per il nome di un dispositivo di backup. BACKUP TO URL utilizza 36 caratteri per gli elementi necessari usati per specificare l'URL (https://.blob.core.windows.net//.bak) lasciando 223 caratteri per i nomi dell'account, del contenitore e del BLOB.  
  
###  <a name="Support"></a> Supporto per le istruzioni di backup/ripristino  
  
|||||  
|-|-|-|-|  
|Istruzione di backup/ripristino|Supportato|Eccezioni|Commenti|  
|BACKUP|???|BLOCKSIZE e MAXTRANSFERSIZE non sono supportate.|Richiede la specifica di WITH CREDENTIAL|  
|RESTORE|???||Richiede la specifica di WITH CREDENTIAL|  
|RESTORE FILELISTONLY|???||Richiede la specifica di WITH CREDENTIAL|  
|RESTORE HEADERONLY|???||Richiede la specifica di WITH CREDENTIAL|  
|RESTORE LABELONLY|???||Richiede la specifica di WITH CREDENTIAL|  
|RESTORE VERIFYONLY|???||Richiede la specifica di WITH CREDENTIAL|  
|RESTORE REWINDONLY|???|||  
  
 Per la sintassi e informazioni generali sulle istruzioni di backup, vedere [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
 Per la sintassi e informazioni generali sulle istruzioni di ripristino, vedere [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
### <a name="support-for-backup-arguments"></a>Supporto per gli argomenti dell'istruzione BACKUP  
  
|||||  
|-|-|-|-|  
|Argomento|Supportato|Eccezione|Commenti|  
|DATABASE|???|||  
|LOG|???|||  
||  
|TO (URL)|???|Diversamente da DISK e TAPE, l'URL non supporta la specifica o la creazione di un nome logico.|Questo argomento viene utilizzato per specificare il percorso URL del file di backup.|  
|MIRROR TO|???|||  
|**OPZIONI WITH:**||||  
|CREDENTIAL|???||WITH CREDENTIAL è supportata solo quando si utilizza l'opzione BACKUP TO URL per eseguire il backup nel servizio di archiviazione BLOB di Windows Azure.|  
|DIFFERENTIAL|???|||  
|COPY_ONLY|???|||  
|COMPRESSION&#124;NO_COMPRESSION|???|||  
|DESCRIPTION|???|||  
|NAME|???|||  
|EXPIREDATE &#124; RETAINDAYS|???|||  
|NOINIT &#124; INIT|???||Se utilizzata, questa opzione è ignorata.<br /><br /> L'accodamento ai BLOB non è consentito. Per sovrascrivere un backup, utilizzare l'argomento FORMAT.|  
|NOSKIP &#124; SKIP|???|||  
|NOFORMAT &#124; FORMAT|???||Se utilizzata, questa opzione è ignorata.<br /><br /> Un backup eseguito in un BLOB esistente non viene completato a meno che non venga specificato WITH FORMAT. Il BLOB esistente viene sovrascritto quando viene specificato WITH FORMAT.|  
|MEDIADESCRIPTION|???|||  
|MEDIANAME|???|||  
|BLOCKSIZE|???|||  
|BUFFERCOUNT|???|||  
|MAXTRANSFERSIZE|???|||  
|NO_CHECKSUM &#124; CHECKSUM|???|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|???|||  
|STATS|???|||  
|REWIND &#124; NOREWIND|???|||  
|UNLOAD &#124; NOUNLOAD|???|||  
|NORECOVERY &#124; STANDBY|???|||  
|NO_TRUNCATE|???|||  
  
 Per altre informazioni sugli argomenti di backup, vedere [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
### <a name="support-for-restore-arguments"></a>Supporto per gli argomenti dell'istruzione RESTORE  
  
|||||  
|-|-|-|-|  
|Argomento|Supportato|Eccezioni|Commenti|  
|DATABASE|???|||  
|LOG|???|||  
|FROM (URL)|???||L'argomento FROM URL viene utilizzato per specificare il percorso URL del file di backup.|  
|**WITH Options:**||||  
|CREDENTIAL|???||WITH CREDENTIAL è supportata solo quando si utilizza l'opzione RESTORE FROM URL per eseguire il ripristino dal servizio di archiviazione BLOB di Windows Azure.|  
|PARTIAL|???|||  
|RECOVERY &#124; NORECOVERY &#124; STANDBY|???|||  
|LOADHISTORY|???|||  
|MOVE|???|||  
|REPLACE|???|||  
|RESTART|???|||  
|RESTRICTED_USER|???|||  
|FILE|???|||  
|PASSWORD|???|||  
|MEDIANAME|???|||  
|MEDIAPASSWORD|???|||  
|BLOCKSIZE|???|||  
|BUFFERCOUNT|???|||  
|MAXTRANSFERSIZE|???|||  
|CHECKSUM &#124; NO_CHECKSUM|???|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|???|||  
|FILESTREAM|???|||  
|STATS|???|||  
|REWIND &#124; NOREWIND|???|||  
|UNLOAD &#124; NOUNLOAD|???|||  
|KEEP_REPLICATION|???|||  
|KEEP_CDC|???|||  
|ENABLE_BROKER &#124; ERROR_BROKER_CONVERSATIONS &#124; NEW_BROKER|???|||  
|STOPAT &#124; STOPATMARK &#124; STOPBEFOREMARK|???|||  
  
 Per altre informazioni sugli argomenti di ripristino, vedere [Argomenti dell'istruzione RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql).  
  
##  <a name="BackupTaskSSMS"></a> Utilizzo dell'attività di Backup in SQL Server Management Studio  
 L'attività di backup in SQL Server Management Studio è stata migliorata per includere l'URL come una delle opzioni di destinazione e altri oggetti di supporto necessari per eseguire il backup nel servizio di archiviazione Windows Azure come le credenziali SQL.  
  
 Nei passaggi seguenti vengono descritte le modifiche apportate all'attività Backup database per consentire il backup nel servizio di archiviazione Windows Azure:  
  
1.  Avviare SQL Server Management Studio e connettersi all'istanza di SQL Server.  Selezionare un database che si desidera eseguire il backup e fare clic con il pulsante destro sul **attività**e selezionare **eseguire il backup..** . Verrà visualizzata la finestra di dialogo backup Database.  
  
2.  Nella pagina Generale utilizzare l'opzione **URL** per creare un backup nel servizio di archiviazione Windows Azure. Quando si seleziona questa opzione, nella pagina verranno abilitate altre opzioni:  
  
    1.  **Nome file:** nome del file di backup.  
  
    2.  **Credenziali SQL:** È possibile specificare le credenziali di SQL Server esistenti, o crearne uno nuovo facendo clic sui **Create** accanto alla casella credenziali SQL.  
  
        > [!IMPORTANT]  
        >  La finestra di dialogo visualizzata quando si fa clic su **Crea** richiede un certificato di gestione o il profilo di pubblicazione per la sottoscrizione. SQL Server supporta attualmente la versione del profilo di pubblicazione 2.0. Per scaricare la versione supportata del profilo di pubblicazione, vedere [Download del profilo di pubblicazione 2.0](https://go.microsoft.com/fwlink/?LinkId=396421).  
        >   
        >  Se non si dispone dell'accesso al certificato di gestione o al profilo di pubblicazione, è possibile creare le credenziali di SQL specificando il nome dell'account di archiviazione e le informazioni sulla chiave di accesso tramite Transact-SQL o SQL Server Management Studio. Vedere il codice di esempio nella sezione [Creare credenziali](#credential) per creare le credenziali tramite Transact-SQL. In alternativa, utilizzando SQL Server Management Studio, dall'istanza del motore di database, fare clic con il pulsante destro del mouse su **Sicurezza**, scegliere **Nuovo**e selezionare **Credenziale**. Specificare il nome dell'account di archiviazione per **Identity** e la chiave di accesso nel campo **Password** .  
  
    3.  **Contenitore di archiviazione di Azure:** Il nome del contenitore di archiviazione di Azure per archiviare i file di backup.  
  
    4.  **Prefisso URL** Viene compilato automaticamente utilizzando le informazioni specificate nei campi descritti nei passaggi precedenti. Se si modifica questo valore manualmente, assicurarsi che corrisponda alle altre informazioni fornite in precedenza. Se ad esempio si modifica l'URL di archiviazione, assicurarsi che le credenziali SQL siano impostate per l'autenticazione dello stesso account di archiviazione.  
  
 Quando si seleziona un URL come destinazione, alcune opzioni nella pagina **Opzioni supporti** vengono disabilitate.  Negli argomenti seguenti vengono fornite ulteriori informazioni sulla finestra di dialogo Backup database:  
  
 [Backup database &#40;pagina Generale&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
 [Back Up Database &#40;pagina Opzioni supporti&#41;](back-up-database-media-options-page.md)  
  
 [Backup database &#40;pagina Opzioni di backup&#41;](back-up-database-backup-options-page.md)  
  
 [Creare le credenziali - Eseguire l'autenticazione nel servizio di archiviazione Azure](create-credential-authenticate-to-azure-storage.md)  
  
##  <a name="MaintenanceWiz"></a> Backup di SQL Server nell'URL tramite la Creazione guidata piano di manutenzione  
 Analogamente all'attività di backup descritta in precedenza, la Creazione guidata piano di manutenzione in SQL Server Management Studio è stata migliorata per includere l' **URL** come una delle opzioni di destinazione e altri oggetti di supporto necessari per eseguire il backup nel servizio di archiviazione Windows Azure come le credenziali SQL. Per altre informazioni, vedere la sezione **Definire attività di backup** in [Using Maintenance Plan Wizard](../maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure).  
  
##  <a name="RestoreSSMS"></a> Il ripristino da archiviazione di Windows Azure mediante SQL Server Management Studio  
 Se si ripristina un database, l' **URL** viene incluso come dispositivo da cui eseguire il ripristino. Nei passaggi seguenti vengono descritte le modifiche effettuate all'attività di ripristino per consentire il ripristino dal servizio di archiviazione Windows Azure:  
  
1.  Quando si seleziona **Dispositivi** nella pagina **Generale** dell'attività di ripristino in SQL Server Management Studio, viene visualizzata la finestra di dialogo **Seleziona dispositivi di backup** che include **URL** come tipo di supporti di backup.  
  
2.  Quando si seleziona **URL** e si fa clic su **Aggiungi**, viene visualizzata la finestra di dialogo **Connessione a Servizio di archiviazione Windows Azure** . Specificare le informazioni sulle credenziali SQL per l'autenticazione nel servizio di archiviazione Windows Azure.  
  
3.  SQL Server viene quindi connesso al servizio di archiviazione Windows Azure utilizzando le informazioni sulle credenziali SQL fornite e viene visualizzata la finestra di dialogo **Individua file di backup in Windows Azure** . In questa pagina vengono visualizzati i file di backup che si trovano nello spazio di archiviazione. Selezionare il file che si desidera ripristinare, quindi fare clic su **OK**. Viene visualizzata la finestra di dialogo **Seleziona dispositivi di backup** . Se si fa clic su **OK** in questa finestra di dialogo, viene visualizzata di nuovo la finestra di dialogo principale **Ripristina** in cui sarà possibile completare il ripristino.  Per ulteriori informazioni, vedere gli argomenti seguenti:  
  
     [Ripristina database &#40;pagina Generale&#41;](restore-database-general-page.md)  
  
     [Ripristina database &#40;pagina File&#41;](restore-database-files-page.md)  
  
     [Ripristina database &#40;pagina Opzioni&#41;](restore-database-options-page.md)  
  
##  <a name="Examples"></a> Esempi di codice  
 In questa sezione sono disponibili gli esempi riportati di seguito.  
  
-   [Creare credenziali](#credential)  
  
-   [Backup di un database completo](#complete)  
  
-   [Backup del database e del log](#databaselog)  
  
-   [Creazione di un backup completo del file del filegroup primario](#filebackup)  
  
-   [Creazione di un backup differenziale dei filegroup primari](#differential)  
  
-   [Ripristino di un database e spostamento dei file](#restoredbwithmove)  
  
-   [Ripristino temporizzato tramite STOPAT](#PITR)  
  
###  <a name="credential"></a> Creare credenziali  
 Nell'esempio seguente vengono create le credenziali in cui sono contenute le informazioni di autenticazione per l'archiviazione di Windows Azure.  
  
1.  **Tsql**  
  
    ```  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL mycredential WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key>' ;  
  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
    string secret = "<storage access key>";  
  
    // Create a Credential  
    string credentialName = "mycredential";  
    Credential credential = new Credential(server, credentialName);  
    credential.Create(identity, secret);  
    ```  
  
3.  **PowerShell**  
  
    ```  
    # create variables  
    $storageAccount = "mystorageaccount"  
    $storageKey = "<storage access key>"  
    $secureString = convertto-securestring $storageKey  -asplaintext -force  
    $credentialName = "mycredential"  
  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # Create a credential  
     New-SqlCredential -Name $credentialName -Path $srvpath -Identity $storageAccount -Secret $secureString  
  
    ```  
  
###  <a name="complete"></a> Backup di un database completo  
 Nell'esempio riportato di seguito viene eseguito il backup del database AdventureWorks2012 nel servizio di archiviazione BLOB di Windows Azure.  
  
1.  **Tsql**  
  
    ```  
    BACKUP DATABASE AdventureWorks2012   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'   
          WITH CREDENTIAL = 'mycredential'   
         ,COMPRESSION  
         ,STATS = 5;  
    GO  
  
    ```  
  
1.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backup.Devices.AddDevice(url, DeviceType.Url);  
    backup.SqlBackup(server);  
    ```  
  
2.  **PowerShell**  
  
    ```  
    # create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"   
    # for default instance, the $srvpath varilable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to SQL Server Instance  
    CD $srvPath   
    $backupFile = $backupUrlContainer + "AdventureWorks2012" +  ".bak"  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On  
  
    ```  
  
###  <a name="databaselog"></a> Backup del database e log  
 Nell'esempio riportato di seguito viene eseguito il backup del database di esempio AdventureWorks2012 per il quale viene utilizzato, per impostazione predefinita, il modello di recupero con registrazione minima. Per consentire il backup del log, il database AdventureWorks2012 viene modificato per l'utilizzo del modello di recupero con registrazione completa. Nell'esempio viene quindi creato un backup completo del database nel BLOB di Windows Azure e, dopo un periodo dedicato alle attività di aggiornamento, viene eseguito il backup del log. In questo esempio viene creato il nome di un file di backup con un indicatore datetime.  
  
1.  **Tsql**  
  
    ```  
    -- To permit log backups, before the full database backup, modify the database   
    -- to use the full recovery model.  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks2012  
       SET RECOVERY FULL;  
    GO  
  
    -- Back up the full AdventureWorks2012 database.  
           -- First create a file name for the backup file with DateTime stamp  
  
    DECLARE @Full_Filename AS VARCHAR (300);  
    SET @Full_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Full_'+   
    REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.bak';   
    --Back up Adventureworks2012 database  
  
    BACKUP DATABASE AdventureWorks2012  
    TO URL =  @Full_Filename  
    WITH CREDENTIAL = 'mycredential';  
    ,COMPRESSION  
    GO  
    -- Back up the AdventureWorks2012 log.  
    DECLARE @Log_Filename AS VARCHAR (300);  
    SET @Log_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Log_'+   
    REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
    BACKUP LOG AdventureWorks2012  
     TO URL = @Log_Filename  
    WITH CREDENTIAL = 'mycredential'  
    ,COMPRESSION;  
    GO  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url for data backup  
    string urlDataBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}_Data-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Database to Url  
    Backup backupData = new Backup();  
    backupData.CredentialName = credentialName;  
    backupData.Database = dbName;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backupData.Devices.AddDevice(urlDataBackup, DeviceType.Url);  
    backupData.SqlBackup(server);  
  
    // Generate Unique Url for data backup  
    string urlLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}_Log-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Database Log to Url  
    Backup backupLog = new Backup();  
    backupLog.CredentialName = credentialName;  
    backupLog.Database = dbName;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backupLog.Devices.AddDevice(urlLogBackup, DeviceType.Url);  
    backupLog.Action = BackupActionType.Log;  
    backupLog.SqlBackup(server);  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to theSQL Server Instance  
  
    CD $srvPath   
    #Create a unique file name for the full database backup  
    $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    #Backup Database to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Database    
  
    #Create a unique file name for log backup  
  
    $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
    #Backup Log to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Log  
  
    ```  
  
###  <a name="filebackup"></a> Creazione di un backup completo del file del filegroup primario  
 Nell'esempio seguente viene creato un backup di file completo del filegroup primario.  
  
1.  **Tsql**  
  
    ```  
    --Back up the files in Primary:  
    BACKUP DATABASE AdventureWorks2012  
       FILEGROUP = 'Primary'  
       TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012files.bck'  
       WITH CREDENTIAL = 'mycredential'  
       ,COMPRESSION;  
    GO  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bck",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Action = BackupActionType.Files;  
    backup.DatabaseFileGroups.Add("PRIMARY");  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backup.Devices.AddDevice(url, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to the SQL Server Instance  
  
    CD $srvPath   
    #Create a unique file name for the file backup  
    $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bck"  
  
    #Backup Primary File Group to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Files -DatabaseFileGroup Primary  
  
    ```  
  
###  <a name="differential"></a> Creazione di un backup differenziale del file del filegroup primario  
 Nell'esempio seguente viene creato un backup di file differenziale del filegroup primario.  
  
1.  **Tsql**  
  
    ```  
    --Back up the files in Primary:  
    BACKUP DATABASE AdventureWorks2012  
       FILEGROUP = 'Primary'  
       TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012filesdiff.bck'  
       WITH   
          CREDENTIAL = 'mycredential'  
          ,COMPRESSION  
      ,DIFFERENTIAL;  
    GO  
  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Action = BackupActionType.Files;  
    backup.DatabaseFileGroups.Add("PRIMARY");  
    backup.Incremental = true;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backup.Devices.AddDevice(url, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to SQL Server Instance  
  
    CD $srvPath   
  
    #create a unique file name for the full backup  
    $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    #Create a differential backup of the primary filegroup  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Files -DatabaseFileGroup Primary -Incremental  
  
    ```  
  
###  <a name="restoredbwithmove"></a> Ripristinare un database e spostare i file  
 Per ripristinare un backup completo del database e spostare il database ripristinato nella directory C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data, attenersi ai passaggi riportati di seguito.  
  
1.  **Tsql**  
  
    ```  
    -- Backup the tail of the log first  
  
    DECLARE @Log_Filename AS VARCHAR (300);  
    SET @Log_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Log_'+   
    REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
    BACKUP LOG AdventureWorks2012  
     TO URL = @Log_Filename  
    WITH CREDENTIAL = 'mycredential'  
    ,NORECOVERY;  
    GO  
  
    RESTORE DATABASE AdventureWorks2012 FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'  
    WITH CREDENTIAL = 'mycredential'  
    ,MOVE 'AdventureWorks2012_data' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf'  
    ,MOVE 'AdventureWorks2012_log' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf'  
    ,STATS = 5  
  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string urlBackupData = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-Data{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    // Generate Unique Url for tail log backup  
    string urlTailLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-TailLog{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Tail Log to Url  
    Backup backupTailLog = new Backup();  
    backupTailLog.CredentialName = credentialName;  
    backupTailLog.Database = dbName;  
    backupTailLog.Action = BackupActionType.Log;  
    backupTailLog.NoRecovery = true;  
    backupTailLog.Devices.AddDevice(urlTailLogBackup, DeviceType.Url);  
    backupTailLog.SqlBackup(server);  
  
    // Restore a database and move files  
    string newDataFilePath = server.MasterDBLogPath  + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".mdf";  
    string newLogFilePath = server.MasterDBLogPath  + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".ldf";  
  
    Restore restore = new Restore();  
    restore.CredentialName = credentialName;  
    restore.Database = dbName;  
    restore.ReplaceDatabase = true;  
    restore.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    restore.RelocateFiles.Add(new RelocateFile(dbName, newDataFilePath));  
    restore.RelocateFiles.Add(new RelocateFile(dbName+ "_Log", newLogFilePath));  
    restore.SqlRestore(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTNACENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to SQL Server Instance   
  
    CD $srvPath   
  
    #create a unique file name for the full backup  
    $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    # Full database backup to URL  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupdbFile  -SqlCredential $credentialName -CompressionOption On      
  
    #Create a unique file name for the tail log backup  
    $backuplogFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
    #Backup tail log to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName  -BackupAction Log -NoRecovery    
  
    # Restore Database and move files  
  
    $newDataFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile ("AdventureWorks_Data","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf")  
    $newLogFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile("AdventureWorks_Log","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf")  
  
    Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backupdbFile -RelocateFile @($newDataFilePath,$newLogFilePath)  
  
    ```  
  
###  <a name="PITR"></a> Ripristino temporizzato tramite STOPAT  
 Nell'esempio seguente viene ripristinato lo stato di un database in un momento preciso e viene illustrata un'operazione di ripristino.  
  
1.  **Tsql**  
  
    ```  
    RESTORE DATABASE AdventureWorks FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'   
    WITH   
     CREDENTIAL = 'mycredential'  
    ,MOVE 'AdventureWorks2012_data' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf'  
    ,Move 'AdventureWorks2012_log' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf'  
    ,NORECOVERY  
    --,REPLACE  
    ,STATS = 5;  
    GO   
  
    RESTORE LOG AdventureWorks FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.trn'   
    WITH CREDENTIAL = 'mycredential'  
    ,RECOVERY   
    ,STOPAT = 'Oct 23, 2012 5:00 PM'   
    GO  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string urlBackupData = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-Data{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    // Generate Unique Url for Tail Log backup  
    string urlTailLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-TailLog{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Tail Log to Url  
    Backup backupTailLog = new Backup();  
    backupTailLog.CredentialName = credentialName;  
    backupTailLog.Database = dbName;  
    backupTailLog.Action = BackupActionType.Log;  
    backupTailLog.NoRecovery = true;  
    backupTailLog.Devices.AddDevice(urlTailLogBackup, DeviceType.Url);  
    backupTailLog.SqlBackup(server);  
  
    // Restore a database and move files  
    string newDataFilePath = server.MasterDBLogPath + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".mdf";  
    string newLogFilePath = server.MasterDBLogPath + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".ldf";  
  
    Restore restore = new Restore();  
    restore.CredentialName = credentialName;  
    restore.Database = dbName;  
    restore.ReplaceDatabase = true;  
    restore.NoRecovery = true;  
    restore.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    restore.RelocateFiles.Add(new RelocateFile(dbName, newDataFilePath));  
    restore.RelocateFiles.Add(new RelocateFile(dbName + "_Log", newLogFilePath));  
    restore.SqlRestore(server);  
  
    // Restore transaction Log with stop at   
    Restore restoreLog = new Restore();  
    restoreLog.CredentialName = credentialName;  
    restoreLog.Database = dbName;  
    restoreLog.Action = RestoreActionType.Log;  
    restoreLog.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    restoreLog.ToPointInTime = DateTime.Now.ToString();   
    restoreLog.SqlRestore(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # Navigate to SQL Server Instance Directory  
  
    CD $srvPath   
  
    #create a unique file name for the full backup  
    $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    # Full database backup to URL  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupdbFile  -SqlCredential $credentialName -CompressionOption On     
  
    #Create a unique file name for the tail log backup  
    $backuplogFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
    #Backup tail log to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName  -BackupAction Log -NoRecovery     
  
    # Restore Database and move files  
  
    $newDataFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile ("AdventureWorks_Data","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf")  
    $newLogFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile("AdventureWorks_Log","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf")  
  
    Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backupdbFile -RelocateFile @($newDataFilePath,$newLogFilePath) -NoRecovery    
  
    # Restore Transaction log with Stop At:  
    Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backuplogFile  -ToPointInTime (Get-Date).ToString()  
  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure consigliate e risoluzione dei problemi per il backup di SQL Server nell'URL](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [Backup e ripristino di database di sistema &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [Esercitazione: Backup e ripristino di SQL Server nel servizio di archiviazione BLOB di Windows Azure](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
  
