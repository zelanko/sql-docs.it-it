---
title: Backup di SQL Server nell'URL | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 11be89e9-ff2a-4a94-ab5d-27d8edf9167d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 04f8eaf855d33faf0d2eab8fde718c92f9a24906
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289229"
---
# <a name="sql-server-backup-to-url"></a>Backup di SQL Server nell'URL
  Questo argomento introduce i concetti, i requisiti e i componenti necessari per usare il servizio di archiviazione BLOB di Azure come destinazione di backup. La funzionalità di backup e ripristino è uguale o simile a quella delle opzioni DISK e TAPE, con alcune differenze. Nell'argomento sono descritte le differenze e le eccezioni rilevanti e sono inclusi alcuni esempi di codice.  
  
## <a name="requirements-components-and-concepts"></a>Requisiti, componenti e concetti  
 **Contenuto della sezione:**  
  
-   [Sicurezza](#security)  
  
-   [Introduzione ai componenti e ai concetti chiave](#intorkeyconcepts)  
  
-   [Servizio di archiviazione BLOB di Azure](#Blob)  
  
-   [Componenti di SQL Server](#sqlserver)  
  
-   [Limitazioni](#limitations)  
  
-   [Supporto per le istruzioni di backup/ripristino](#Support)  
  
-   [Utilizzo dell'attività di backup in SQL Server Management Studio](sql-server-backup-to-url.md#BackupTaskSSMS)  
  
-   [Backup di SQL Server nell'URL tramite la Creazione guidata piano di manutenzione](sql-server-backup-to-url.md#MaintenanceWiz)  
  
-   [Ripristino da Archiviazione di Azure mediante SQL Server Management Studio](sql-server-backup-to-url.md#RestoreSSMS)  
  
###  <a name="security"></a> Sicurezza  
 Di seguito sono riportati i requisiti e le considerazioni sulla sicurezza per il backup o il ripristino dai servizi di archiviazione BLOB di Azure.  
  
-   Quando si crea un contenitore per il servizio di archiviazione BLOB di Azure, è consigliabile impostare l'accesso su **privato**. In questo modo si limita l'accesso a utenti o account in grado di specificare le informazioni necessarie per l'autenticazione all'account di Azure.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]richiede l'archiviazione del nome dell'account di Azure e della chiave di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] accesso in una credenziale. Queste informazioni vengono usate per eseguire l'autenticazione all'account di Azure quando vengono eseguite operazioni di backup o ripristino.  
  
-   All'account utente usato per eseguire i comandi BACKUP o RESTORE deve essere associato il ruolo del database **db_backup operator** con autorizzazioni **Modifica qualsiasi credenziale** .  
  
###  <a name="intorkeyconcepts"></a> Introduzione ai componenti e ai concetti chiave  
 Le due sezioni seguenti introducono il servizio di archiviazione BLOB di Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i componenti usati durante il backup o il ripristino dal servizio di archiviazione BLOB di Azure. È importante comprendere i componenti e l'interazione tra di essi per eseguire un backup o il ripristino dal servizio di archiviazione BLOB di Azure.  
  
 La creazione di un account Azure è il primo passaggio per questo processo. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Usa il **nome dell'account di archiviazione di Azure** e i relativi valori della **chiave di accesso** per autenticare e scrivere e leggere i BLOB nel servizio di archiviazione. Le credenziali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tramite cui vengono archiviate queste informazioni di autenticazione, vengono utilizzate durante le operazioni di backup o ripristino. Per una procedura dettagliata completa per la creazione di un account di archiviazione e l'esecuzione di un ripristino semplice, vedere [esercitazione sull'uso del servizio di archiviazione di Azure per SQL Server backup e ripristino](https://go.microsoft.com/fwlink/?LinkId=271615).  
  
 ![Mapping dell'account di archiviazione alle credenziali SQL](../../tutorials/media/backuptocloud-storage-credential-mapping.gif "Mapping dell'account di archiviazione alle credenziali SQL")  
  
###  <a name="Blob"></a>Servizio di archiviazione BLOB di Azure  
 **Account di archiviazione:** l'account di archiviazione è il punto di partenza per tutti i servizi di archiviazione. Per accedere al servizio di archiviazione BLOB di Azure, creare prima un account di archiviazione di Azure. Il **nome dell'account di archiviazione** e le relative proprietà **chiave di accesso** sono necessari per eseguire l'autenticazione nel servizio di archiviazione BLOB di Azure e nei relativi componenti.  
  
 **Contenitore:** Un contenitore fornisce un raggruppamento di un set di BLOB e può archiviare un numero illimitato di BLOB. Per scrivere un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] backup nel servizio BLOB di Azure, è necessario che sia stato creato almeno il contenitore radice.  
  
 **BLOB:** file di qualsiasi tipo e dimensioni. Esistono due tipi di BLOB che è possibile archiviare nel servizio di archiviazione BLOB di Azure: BLOB in blocchi e di pagine. Nel backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il tipo di BLOB utilizzato è quello di pagine. I BLOB sono indirizzabili usando il formato di URL seguente\<: account di archiviazione https://\<>. blob.Core.Windows.NET/\<>/BLOB del contenitore>  
  
 ![Archiviazione BLOB di Azure](../../database-engine/media/backuptocloud-blobarchitecture.gif "Archiviazione BLOB di Azure")  
  
 Per altre informazioni sul servizio di archiviazione BLOB di Azure, vedere [come usare il servizio di archiviazione BLOB di Azure](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)  
  
 Per altre informazioni sui BLOB di pagine, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](https://msdn.microsoft.com/library/windowsazure/ee691964.aspx)  
  
###  <a name="sqlserver"></a> Componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 **URL:** un URL specifica un URI (Uniform Resource Identifier) in un file di backup univoco. L'URL viene utilizzato per specificare il percorso e il nome del file di backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In questa implementazione, l'unico URL valido è quello che punta a un BLOB di pagine in un account di archiviazione di Azure. L'URL deve puntare a un BLOB effettivo, non solo a un contenitore. Se il BLOB non è disponibile, viene creato. Se viene specificato un BLOB esistente, il BACKUP ha esito negativo, a meno che non sia stata specificata l'opzione "WITH FORMAT".  
  
> [!WARNING]  
>  Se si sceglie di copiare e caricare un file di backup nel servizio di archiviazione BLOB di Azure, usare il BLOB di pagine come opzione di archiviazione. I ripristini dai BLOB in blocchi non sono supportati. Il ripristino da un BLOB in blocchi non viene completato e viene visualizzato un errore.  
  
 Di seguito è riportato un valore URL di esempio: http [s\<]://ACCOUNTNAME.Blob.core.windows.net/\<container>/filename. bak>. Anche se non richiesto, è consigliabile utilizzare HTTPS.  
  
 **Credenziale:** una credenziale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un oggetto usato per archiviare le informazioni di autenticazione necessarie per la connessione a una risorsa all'esterno di SQL Server.  Qui, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i processi di backup e ripristino usano le credenziali per eseguire l'autenticazione nel servizio di archiviazione BLOB di Azure. Nelle credenziali vengono archiviati il nome dell'account di archiviazione e i relativi valori della **chiave di accesso** . Una volta create, le credenziali devono essere specificate nell'opzione WITH CREDENTIAL durante l'esecuzione delle istruzioni BACKUP/RESTORE. Per altre informazioni su come visualizzare, copiare o rigenerare le **access keys**dell'account di archiviazione, vedere la pagina relativa alle [chiavi di accesso dell'account di archiviazione](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx).  
  
 Per istruzioni dettagliate sulla creazione di credenziali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere l'esempio [Creare credenziali](#credential) più avanti in questo argomento.  
  
 Per informazioni generali sulle credenziali, vedere [Credenziali](../security/authentication-access/credentials-database-engine.md)  
  
 Per informazioni su altri esempi in cui vengono usate le credenziali, vedere [creare un Proxy SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md).  
  
###  <a name="limitations"></a> Limitazioni  
  
-   Il backup in Archiviazione Premium non è supportato.  
  
-   Le dimensioni massime di backup supportate sono 1 TB.  
  
-   È possibile eseguire istruzioni di backup o ripristino tramite TSQL, SMO o cmdlet di PowerShell. Il backup o il ripristino dal servizio di archiviazione BLOB di Azure tramite SQL Server Management Studio backup o ripristino guidato non è attualmente abilitato.  
  
-   La creazione di un nome di dispositivo logico non è supportata. Di conseguenza, non è supportata neanche l'aggiunta di un URL come dispositivo di backup tramite sp_dumpdevice o SQL Server Management Studio.  
  
-   L'accodamento ai BLOB di backup esistenti non è supportato. I backup in un BLOB esistente possono solo essere sovrascritti tramite l'opzione WITH FORMAT.  
  
-   Il backup in più BLOB effettuato con una singola operazione non è supportato. Ad esempio, se si esegue l'operazione riportata di seguito viene restituito un errore:  
  
    ```sql
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
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è previsto un limite massimo di 259 caratteri per il nome di un dispositivo di backup. BACKUP TO URL utilizza 36 caratteri per gli elementi necessari usati per specificare l'URL (https://.blob.core.windows.net//.bak ) lasciando 223 caratteri per i nomi dell'account, del contenitore e del BLOB.  
  
###  <a name="Support"></a> Supporto per le istruzioni di backup/ripristino  
  
|||||  
|-|-|-|-|  
|Istruzione di backup/ripristino|Supportato|Eccezioni|Commenti|  
|BACKUP|&#x2713;|BLOCKSIZE e MAXTRANSFERSIZE non sono supportate.|Richiede la specifica di WITH CREDENTIAL|  
|RESTORE|&#x2713;||Richiede la specifica di WITH CREDENTIAL|  
|RESTORE FILELISTONLY|&#x2713;||Richiede la specifica di WITH CREDENTIAL|  
|RESTORE HEADERONLY|&#x2713;||Richiede la specifica di WITH CREDENTIAL|  
|RESTORE LABELONLY|&#x2713;||Richiede la specifica di WITH CREDENTIAL|  
|RESTORE VERIFYONLY|&#x2713;||Richiede la specifica di WITH CREDENTIAL|  
|RESTORE REWINDONLY|&#x2713;|||  
  
 Per la sintassi e informazioni generali sulle istruzioni di backup, vedere [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
 Per la sintassi e informazioni generali sulle istruzioni di ripristino, vedere [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
### <a name="support-for-backup-arguments"></a>Supporto per gli argomenti dell'istruzione BACKUP  
  
|||||  
|-|-|-|-|  
|Argomento|Supportato|Eccezione|Commenti|  
|DATABASE|&#x2713;|||  
|LOG|&#x2713;|||  
||  
|TO (URL)|&#x2713;|Diversamente da DISK e TAPE, l'URL non supporta la specifica o la creazione di un nome logico.|Questo argomento viene utilizzato per specificare il percorso URL del file di backup.|  
|MIRROR TO|&#x2713;|||  
|**OPZIONI WITH:**||||  
|CREDENTIAL|&#x2713;||WITH CREDENTIAL è supportato solo quando si usa l'opzione BACKUP TO URL per eseguire il backup nel servizio di archiviazione BLOB di Azure.|  
|DIFFERENTIAL|&#x2713;|||  
|COPY_ONLY|&#x2713;|||  
|COMPRESSION&#124;NO_COMPRESSION|&#x2713;|||  
|DESCRIZIONE|&#x2713;|||  
|NAME|&#x2713;|||  
|EXPIREDATE &#124; RETAINDAYS|&#x2713;|||  
|NOINIT &#124; INIT|&#x2713;||Se utilizzata, questa opzione è ignorata.<br /><br /> L'accodamento ai BLOB non è consentito. Per sovrascrivere un backup, utilizzare l'argomento FORMAT.|  
|NOSKIP &#124; SKIP|&#x2713;|||  
|NOFORMAT &#124; FORMAT|&#x2713;||Se utilizzata, questa opzione è ignorata.<br /><br /> Un backup eseguito in un BLOB esistente non viene completato a meno che non venga specificato WITH FORMAT. Il BLOB esistente viene sovrascritto quando viene specificato WITH FORMAT.|  
|MEDIADESCRIPTION|&#x2713;|||  
|MEDIANAME|&#x2713;|||  
|BLOCKSIZE|&#x2713;|||  
|BUFFERCOUNT|&#x2713;|||  
|MAXTRANSFERSIZE|&#x2713;|||  
|NO_CHECKSUM &#124; CHECKSUM|&#x2713;|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|&#x2713;|||  
|STATS (Statistiche)|&#x2713;|||  
|REWIND &#124; NOREWIND|&#x2713;|||  
|UNLOAD &#124; NOUNLOAD|&#x2713;|||  
|NORECOVERY &#124; STANDBY|&#x2713;|||  
|NO_TRUNCATE|&#x2713;|||  
  
 Per altre informazioni sugli argomenti di backup, vedere [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
### <a name="support-for-restore-arguments"></a>Supporto per gli argomenti dell'istruzione RESTORE  
  
|||||  
|-|-|-|-|  
|Argomento|Supportato|Eccezioni|Commenti|  
|DATABASE|&#x2713;|||  
|LOG|&#x2713;|||  
|FROM (URL)|&#x2713;||L'argomento FROM URL viene utilizzato per specificare il percorso URL del file di backup.|  
|**WITH Options:**||||  
|CREDENTIAL|&#x2713;||WITH CREDENTIAL è supportato solo quando si usa l'opzione RESTOre FROM URL per eseguire il ripristino dal servizio di archiviazione BLOB di Azure.|  
|PARTIAL|&#x2713;|||  
|RECOVERY &#124; NORECOVERY &#124; STANDBY|&#x2713;|||  
|LOADHISTORY|&#x2713;|||  
|MOVE|&#x2713;|||  
|REPLACE|&#x2713;|||  
|RESTART|&#x2713;|||  
|RESTRICTED_USER|&#x2713;|||  
|FILE|&#x2713;|||  
|PASSWORD|&#x2713;|||  
|MEDIANAME|&#x2713;|||  
|MEDIAPASSWORD|&#x2713;|||  
|BLOCKSIZE|&#x2713;|||  
|BUFFERCOUNT|&#x2713;|||  
|MAXTRANSFERSIZE|&#x2713;|||  
|CHECKSUM &#124; NO_CHECKSUM|&#x2713;|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|&#x2713;|||  
|FILESTREAM|&#x2713;|||  
|STATS (Statistiche)|&#x2713;|||  
|REWIND &#124; NOREWIND|&#x2713;|||  
|UNLOAD &#124; NOUNLOAD|&#x2713;|||  
|KEEP_REPLICATION|&#x2713;|||  
|KEEP_CDC|&#x2713;|||  
|ENABLE_BROKER &#124; ERROR_BROKER_CONVERSATIONS &#124; NEW_BROKER|&#x2713;|||  
|STOPAT &#124; STOPATMARK &#124; STOPBEFOREMARK|&#x2713;|||  
  
 Per altre informazioni sugli argomenti di ripristino, vedere [Argomenti dell'istruzione RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql).  
  
##  <a name="BackupTaskSSMS"></a>Utilizzo dell'attività di backup in SQL Server Management Studio  
 L'attività di backup in SQL Server Management Studio è stata migliorata per includere l'URL come una delle opzioni di destinazione e altri oggetti di supporto necessari per eseguire il backup in archiviazione di Azure come le credenziali SQL.  
  
 I passaggi seguenti descrivono le modifiche apportate all'attività Backup database per consentire il backup in archiviazione di Azure.:  
  
1.  Avviare SQL Server Management Studio e connettersi all'istanza di SQL Server.  Selezionare un database di cui si desidera eseguire il backup e fare clic con il pulsante destro del mouse su **attività**e selezionare **backup..**. Verrà visualizzata la finestra di dialogo Backup database.  
  
2.  Nella pagina generale viene usata l'opzione **URL** per creare un backup in archiviazione di Azure. Quando si seleziona questa opzione, nella pagina verranno abilitate altre opzioni:  
  
    1.  **Nome file:** Nome del file di backup.  
  
    2.  **Credenziali SQL:** È possibile specificare una credenziale di SQL Server esistente o crearne una nuova facendo clic sul pulsante **Crea** accanto alla casella credenziali SQL.  
  
        > [!IMPORTANT]  
        >  La finestra di dialogo visualizzata quando si fa clic su **Crea** richiede un certificato di gestione o il profilo di pubblicazione per la sottoscrizione. SQL Server supporta attualmente la versione del profilo di pubblicazione 2.0. Per scaricare la versione supportata del profilo di pubblicazione, vedere [Download del profilo di pubblicazione 2.0](https://go.microsoft.com/fwlink/?LinkId=396421).  
        >   
        >  Se non si dispone dell'accesso al certificato di gestione o al profilo di pubblicazione, è possibile creare le credenziali di SQL specificando il nome dell'account di archiviazione e le informazioni sulla chiave di accesso tramite Transact-SQL o SQL Server Management Studio. Vedere il codice di esempio nella sezione [Creare credenziali](#credential) per creare le credenziali tramite Transact-SQL. In alternativa, utilizzando SQL Server Management Studio, dall'istanza del motore di database, fare clic con il pulsante destro del mouse su **Sicurezza**, scegliere **Nuovo**e selezionare **Credenziale**. Specificare il nome dell'account di archiviazione per **Identity** e la chiave di accesso nel campo **Password** .  
  
    3.  **Contenitore di archiviazione di Azure:** Nome del contenitore di archiviazione di Azure in cui archiviare i file di backup.  
  
    4.  **Prefisso URL:** Questa operazione viene compilata automaticamente utilizzando le informazioni specificate nei campi descritti nei passaggi precedenti. Se si modifica questo valore manualmente, assicurarsi che corrisponda alle altre informazioni fornite in precedenza. Se ad esempio si modifica l'URL di archiviazione, assicurarsi che le credenziali SQL siano impostate per l'autenticazione dello stesso account di archiviazione.  
  
 Quando si seleziona un URL come destinazione, alcune opzioni nella pagina **Opzioni supporti** vengono disabilitate.  Negli argomenti seguenti vengono fornite ulteriori informazioni sulla finestra di dialogo Backup database:  
  
 [Backup database &#40;pagina Generale&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
 [Back Up Database &#40;pagina Opzioni supporti&#41;](back-up-database-media-options-page.md)  
  
 [Backup database &#40;pagina Opzioni di backup&#41;](back-up-database-backup-options-page.md)  
  
 [Creare le credenziali - Eseguire l'autenticazione nel servizio di archiviazione Azure](create-credential-authenticate-to-azure-storage.md)  
  
##  <a name="MaintenanceWiz"></a> Backup di SQL Server nell'URL tramite la Creazione guidata piano di manutenzione  
 Analogamente all'attività di backup descritta in precedenza, la creazione guidata piano di manutenzione in SQL Server Management Studio è stata migliorata per includere l' **URL** come una delle opzioni di destinazione e altri oggetti di supporto necessari per eseguire il backup in archiviazione di Azure come le credenziali SQL. Per altre informazioni, vedere la sezione **Definire attività di backup** in [Using Maintenance Plan Wizard](../maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure).  
  
##  <a name="RestoreSSMS"></a>Ripristino da archiviazione di Azure tramite SQL Server Management Studio  
 Se si ripristina un database, l' **URL** viene incluso come dispositivo da cui eseguire il ripristino. Nei passaggi seguenti vengono descritte le modifiche apportate all'attività di ripristino per consentire il ripristino da archiviazione di Azure:  
  
1.  Quando si seleziona **Dispositivi** nella pagina **Generale** dell'attività di ripristino in SQL Server Management Studio, viene visualizzata la finestra di dialogo **Seleziona dispositivi di backup** che include **URL** tra i tipi di supporto per il backup.  
  
2.  Quando si seleziona **URL** e si fa clic su **Aggiungi**, viene visualizzata la finestra di dialogo **Connessione a Servizio di archiviazione Windows Azure** . Specificare le informazioni sulle credenziali SQL per l'autenticazione in archiviazione di Azure.  
  
3.  SQL Server quindi si connette ad archiviazione di Azure usando le informazioni sulle credenziali SQL fornite e apre la finestra **di dialogo Individua file di backup in Azure** . In questa pagina vengono visualizzati i file di backup che si trovano nello spazio di archiviazione. Selezionare il file che si desidera ripristinare, quindi fare clic su **OK**. Viene visualizzata di nuovo la finestra di dialogo **Seleziona dispositivi di backup** . Se si fa clic su **OK** in questa finestra di dialogo, viene visualizzata di nuovo la finestra di dialogo principale **Ripristina** in cui sarà possibile completare il ripristino.  Per ulteriori informazioni, vedere gli argomenti seguenti:  
  
     [Ripristina database &#40;pagina Generale&#41;](restore-database-general-page.md)  
  
     [Ripristina database &#40;pagina File&#41;](restore-database-files-page.md)  
  
     [Ripristina database &#40;pagina Opzioni&#41;](restore-database-options-page.md)  
  
##  <a name="Examples"></a> Esempi di codice  
 In questa sezione sono disponibili gli esempi riportati di seguito.  
  
-   [Creare credenziali](#credential)  
  
-   [Backup di un database completo](#complete)  
  
-   [Backup del database e del log](#databaselog)  
  
-   [Creazione di un backup di file completo del filegroup primario](#filebackup)  
  
-   [Creazione di un backup di file differenziale dei filegroup primari](#differential)  
  
-   [Ripristino di un database e spostamento dei file](#restoredbwithmove)  
  
-   [Ripristino temporizzato tramite STOPAT](#PITR)  
  
###  <a name="credential"></a> Creare credenziali  
 L'esempio seguente crea una credenziale che archivia le informazioni di autenticazione di archiviazione di Azure.  

   ```sql
   IF NOT EXISTS  
   (SELECT * FROM sys.credentials   
   WHERE credential_identity = 'mycredential')  
   CREATE CREDENTIAL mycredential WITH IDENTITY = 'mystorageaccount'  
   ,SECRET = '<storage access key>' ;  
   ```
  
   ```csharp
   // Connect to default sql server instance on local machine  
   Server server = new Server(".");  
   string identity = "mystorageaccount";  
   string secret = "<storage access key>";  
  
   // Create a Credential  
   string credentialName = "mycredential";  
   Credential credential = new Credential(server, credentialName);  
   credential.Create(identity, secret);  
   ```  
  
   ```powershell
   # create variables  
   $storageAccount = "mystorageaccount"  
   $storageKey = "<storage access key>"  
   $secureString = ConvertTo-SecureString $storageKey  -asplaintext -force  
   $credentialName = "mycredential"  
  
   $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
   # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
   # Create a credential  
   New-SqlCredential -Name $credentialName -Path $srvpath -Identity $storageAccount -Secret $secureString
   ```  
  
###  <a name="complete"></a>Esecuzione del backup di un database completo  
 Nell'esempio seguente viene eseguito il backup del database AdventureWorks2012 nel servizio di archiviazione BLOB di Azure.
  
   ```sql
   BACKUP DATABASE AdventureWorks2012   
   TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'   
         WITH CREDENTIAL = 'mycredential'   
         ,COMPRESSION  
         ,STATS = 5;  
   GO
   ```  
  
   ```csharp
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
  
   ```powershell
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
  
###  <a name="databaselog"></a>Backup del database e del log  
 Nell'esempio riportato di seguito viene eseguito il backup del database di esempio AdventureWorks2012 per il quale viene utilizzato, per impostazione predefinita, il modello di recupero con registrazione minima. Per consentire il backup del log, il database AdventureWorks2012 viene modificato per l'utilizzo del modello di recupero con registrazione completa. Nell'esempio viene quindi creato un backup completo del database nel BLOB di Azure e, dopo un periodo di attività di aggiornamento, viene eseguito il backup del log. In questo esempio viene creato il nome di un file di backup con un indicatore datetime.  
  
   ```sql
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
  
   ```csharp
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

   ```powershell
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
  
###  <a name="filebackup"></a>Creazione di un backup completo del filegroup primario  
 Nell'esempio seguente viene creato un backup di file completo del filegroup primario.
  
   ```sql
   --Back up the files in Primary:  
   BACKUP DATABASE AdventureWorks2012  
       FILEGROUP = 'Primary'  
       TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012files.bck'  
       WITH CREDENTIAL = 'mycredential'  
       ,COMPRESSION;  
   GO  
   ```
  
   ```csharp
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
  
   ```powershell
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
  
###  <a name="differential"></a>Creazione di un backup differenziale del filegroup primario  
 Nell'esempio seguente viene creato un backup di file differenziale del filegroup primario.  
  
   ```sql
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
  
   ```csharp
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

   ```powershell
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
  
###  <a name="restoredbwithmove"></a>Ripristinare un database e spostare i file  
 Per ripristinare un backup completo del database e spostare il database ripristinato nella directory C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data, attenersi ai passaggi riportati di seguito.
  
   ```sql
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
  
   ```csharp
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

   ```powershell
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
  
   ```sql
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
  
   ```csharp
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
  
   ```powershell
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
