---
title: Procedure consigliate e risoluzione dei problemi per il backup nell'URL
description: Procedure consigliate e suggerimenti per la risoluzione dei problemi relativi al backup e al ripristino di SQL Server in archiviazione BLOB di Azure.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
author: cawrites
ms.author: chadam
ms.openlocfilehash: 4212c397c712351e951060032f6e7a2ece6a5c3f
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129037"
---
# <a name="sql-server-backup-to-url-best-practices-and-troubleshooting"></a>Procedure consigliate e risoluzione dei problemi per il backup di SQL Server nell'URL

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  In questo argomento sono inclusi i suggerimenti per la risoluzione dei problemi e le procedure consigliate relativi al backup e ripristino di SQL Server nel servizio BLOB di Azure.  
  
 Per altre informazioni sull'uso del servizio di archiviazione BLOB di Azure per le operazioni di backup e ripristino di SQL Server, vedere:  
  
-   [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [Esercitazione: Backup e ripristino di SQL Server nel servizio di archiviazione BLOB di Azure](../../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="managing-backups"></a><a name="managing-backups-mb1"></a> Gestione dei backup  
 Nell'elenco seguente sono inclusi i consigli generali sulla gestione dei backup:  
  
-   Per evitare la sovrascrittura accidentale dei BLOB, è consigliabile l'utilizzo di un nome file univoco per ogni backup.  
  
-   Quando si crea un contenitore, è consigliabile impostare il livello di accesso su **privato**, in modo che solo gli utenti o account che possono fornire le informazioni di autenticazione richieste possano leggere o scrivere i BLOB nel contenitore.  
  
-   Per i database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione in una macchina virtuale di Azure, usare un account di archiviazione nella stessa regione della macchina virtuale per evitare i costi di trasferimento dei dati tra le regioni. L'utilizzo della stessa area garantisce anche prestazioni ottimali per le operazioni di backup e ripristino.  
  
-   Un'attività di backup non completata correttamente può generare un file di backup non valido. Sono consigliate l'identificazione periodica dei backup non completati e l'eliminazione dei file BLOB. Per altre informazioni, vedere [Eliminazione dei file BLOB di backup con lease attivi](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md)  
  
-   L'utilizzo dell'opzione `WITH COMPRESSION` durante il backup consente di ridurre i costi di archiviazione e quelli delle transazioni di archiviazione. Inoltre, tramite questa opzione è possibile diminuire il tempo necessario per completare il processo di backup.  

- Impostare gli argomenti `MAXTRANSFERSIZE` e `BLOCKSIZE` come consigliato in [Backup di SQL Server nell'URL](./sql-server-backup-to-url.md).
  
## <a name="handling-large-files"></a>Gestione di file di grandi dimensioni  
  
-   Nell'operazione di backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono usati più thread per ottimizzare il trasferimento dei dati ai servizi di archiviazione BLOB di Azure.  Le prestazioni, tuttavia, dipendono da vari fattori, ad esempio la larghezza di banda del fornitore di software indipendente e le dimensioni del database. Se si intende eseguire il backup di database o filegroup di grandi dimensioni da un database di SQL Server locale, si consiglia di eseguire innanzitutto alcuni test della velocità effettiva. I [contratti di servizio della risorsa di archiviazione](https://azure.microsoft.com/support/legal/sla/storage/v1_0/) di Azure presentano tempi di elaborazione massimi per i BLOB che è possibile prendere in considerazione.  
  
-   L'uso dell'opzione `WITH COMPRESSION` come consigliato nella sezione [Gestione dei backup](#managing-backups-mb1) è molto importante quando si esegue il backup di file di grandi dimensioni.  
  
## <a name="troubleshooting-backup-to-or-restore-from-url"></a>Risoluzione dei problemi di backup nell'URL e di ripristino dallo stesso  
 Di seguito sono elencate alcune modalità rapide per la risoluzione di errori durante l'esecuzione del backup nel servizio di archiviazione BLOB di Azure o del ripristino dallo stesso.  
  
 Per evitare errori a causa di opzioni o limitazioni non supportate, esaminare l'elenco delle limitazioni e le informazioni sul supporto dei comandi BACKUP e RESTORE nell'articolo [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) .  
  
 **Errori di autenticazione:**  
  
-   `WITH CREDENTIAL` è una nuova opzione ed è necessaria per le operazioni di backup nel servizio di archiviazione BLOB di Azure e di ripristino dallo stesso. Di seguito sono riportati i possibili errori correlati alle credenziali:  
  
     Le credenziali specificate nel comando **BACKUP** o **RESTORE** non esistono. Per evitare questo problema, è possibile includere istruzioni T-SQL per creare le credenziali qualora non siano presenti nell'istruzione di backup. Di seguito è riportato un esempio pratico:  
  
    ```sql  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    , SECRET = '<storage access key>' ;  
    ```  
  
-   Le credenziali esistono, ma all'account di accesso utilizzato per eseguire il comando di backup non sono associate autorizzazioni per accedere alle credenziali. Usare un account di accesso nel ruolo **db_backupoperator** con autorizzazioni **_Modifica qualsiasi credenziale_* _.  
  
-   Verificare il nome dell'account di archiviazione e i valori di chiave. Le informazioni archiviate nelle credenziali devono corrispondere ai valori delle proprietà dell'account di archiviazione di Azure usati nelle operazioni di backup e ripristino.  
  
 _ *Errori di backup:* *  
  
-   L'esecuzione di backup paralleli nello stesso BLOB comporta il mancato completamento di uno dei backup con conseguente errore **Inizializzazione non riuscita** .  
  
-   Se si usano BLOB di pagine, ad esempio `BACKUP... TO URL... WITH CREDENTIAL`, usare i log degli errori seguenti per facilitare la risoluzione degli errori di backup:  
  
    -   Impostare il flag di traccia 3051 per abilitare la registrazione in un log degli errori specifico con il formato seguente in:  
  
        `BackupToUrl-\<instname>-\<dbname>-action-\<PID>.log` dove `\<action>` è uno dei tipi seguenti:  
  
        -   **DB**  
        -   **FILELISTONLY**  
        -   **LABELONLY**  
        -   **HEADERONLY**  
        -   **VERIFYONLY**  
  
    -   È inoltre possibile trovare informazioni nei registri denominati `SQLBackupToUrl` in Registro applicazioni di Windows - Applicazione.  

    -   Prendere in considerazione COMPRESSION, MAXTRANSFERSIZE, BLOCKSIZE e più argomenti di URL per il backup di database di grandi dimensioni.  Vedere [Backing up a VLDB to Azure Blob Storage](/archive/blogs/sqlcat/backing-up-a-vldb-to-azure-blob-storage) (Backup di un VLDB in Archiviazione BLOB di Azure)
  
        ```console
        Msg 3202, Level 16, State 1, Line 1
        Write on "https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak" failed: 1117(The request could not be performed because of an I/O device error.)
        Msg 3013, Level 16, State 1, Line 1
        BACKUP DATABASE is terminating abnormally.
        ```

        ```sql  
        BACKUP DATABASE TestDb
        TO URL = 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak',
        URL = 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_1.bak',
        URL = 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_2.bak'
        WITH COMPRESSION, MAXTRANSFERSIZE = 4194304, BLOCKSIZE = 65536;  
        ```  

-   Quando si esegue il ripristino da un backup compresso, è possibile che venga visualizzato l'errore seguente:  
  
    -   `SqlException 3284 occurred. Severity: 16 State: 5  
        Message Filemark on device 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak' is not aligned.           Reissue the Restore statement with the same block size used to create the backupset: '65536' looks like a possible value.`  
  
        Per risolvere il problema, eseguire nuovamente l'istruzione **RESTORE** con il valore **BLOCKSIZE = 65536** specificato.  
  
-   Errore durante il backup a causa di BLOB con lease attivi: l'attività di backup non completata può generare BLOB con lease attivi.  
  
     Se si tenta di nuovo un'istruzione di backup, quest'ultimo potrebbe non essere completato e potrebbe essere visualizzato un errore simile al seguente:  
  
     `Backup to URL received an exception from the remote endpoint. Exception Message: The remote server returned an error: (412) There is currently a lease on the blob and no lease ID was specified in the request.`  
  
     Se un'istruzione RESTORE viene tentata in un file BLOB di backup con un lease attivo, l'operazione di ripristino non viene completata e viene visualizzato un errore simile al seguente:  
  
     `Exception Message: The remote server returned an error: (409) Conflict..`  
  
     Quando si verifica un errore di questo tipo, i file BLOB devono essere eliminati. Per altre informazioni su questo scenario e su come risolvere il problema, vedere [Eliminazione dei file BLOB di backup con lease attivi](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md)  
  
## <a name="proxy-errors"></a>Errori del proxy  
 Se si utilizzano server proxy per accedere a Internet, è possibile che si verifichino i problemi indicati di seguito:  
  
 **Limitazione della connessione da parte dei server proxy**  
  
 Nei server proxy possono essere presenti impostazioni che limitano il numero di connessioni al minuto. Il backup su URL è un processo multithread e pertanto può superare il limite. In questo caso, il server proxy termina la connessione. Per risolvere il problema, modificare le impostazioni del proxy in modo che non venga utilizzato in SQL Server. Di seguito sono riportati alcuni esempi di tipi o messaggi di errore visualizzati nel log degli errori:  
  
```console
Write on "https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak" failed: Backup to URL received an exception from the remote endpoint. Exception Message: Unable to read data from the transport connection: The connection was closed.
```  
  
```console
A nonrecoverable I/O error occurred on file "https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Error could not be gathered from Remote Endpoint.  
  
Msg 3013, Level 16, State 1, Line 2  
  
BACKUP DATABASE is terminating abnormally.  
```

```console
BackupIoRequest::ReportIoError: write failure on backup device https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak'. Operating system error Backup to URL received an exception from the remote endpoint. Exception Message: Unable to read data from the transport connection: The connection was closed.
```  
  
Se si abilita la registrazione dettagliata mediante il flag di traccia 3051, è inoltre possibile che nei log venga visualizzato il messaggio seguente:  
  
`HTTP status code 502, HTTP Status Message Proxy Error (The number of HTTP requests per minute exceeded the configured limit. Contact your ISA Server administrator.)` 
  
 **Impostazioni proxy predefinite non rilevate:**  
  
Le impostazioni predefinite non vengono talvolta rilevate, motivo per il quale si verificano errori di autenticazione proxy, ad esempio quello riportato di seguito:
 
 `A nonrecoverable I/O error occurred on file "https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Backup to URL received an exception from the remote endpoint. Exception Message: The remote server returned an error: (407)* **Proxy Authentication Required.`  
  
Per risolvere il problema, creare un file di configurazione che consenta al processo di backup su URL di utilizzare le impostazioni predefinite del proxy effettuando i passaggi indicati di seguito.  
  
1.  Creare un file di configurazione denominato `BackuptoURL.exe.config` con il contenuto XML seguente:  
  
    ```xml  
    <?xml version ="1.0"?>  
    <configuration>   
                    <system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    </system.net>  
    </configuration>  
    ```  
  
2.  Inserire il file di configurazione nella cartella Binn dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ad esempio, se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene installato nell'unità C del computer, inserire il file di configurazione in `C:\Program Files\Microsoft SQL Server\MSSQL13.\<InstanceName>\MSSQL\Binn`.  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristino da backup archiviati in Microsoft Azure](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
[BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)
