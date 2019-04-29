---
title: Procedure consigliate e risoluzione dei problemi per il backup di SQL Server nell'URL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f54ae14c13d58c75da0ddd6eb69a9d9d7527991f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877093"
---
# <a name="sql-server-backup-to-url-best-practices-and-troubleshooting"></a>Procedure consigliate e risoluzione dei problemi per il backup di SQL Server nell'URL
  In questo argomento sono inclusi i suggerimenti per la risoluzione dei problemi e le procedure consigliate relativi al backup e ripristino di SQL Server nel servizio BLOB di Windows Azure.  
  
 Per ulteriori informazioni sull'utilizzo del servizio di archiviazione BLOB di Windows Azure per le operazioni di backup e ripristino di SQL Server, vedere:  
  
-   [Backup e ripristino di SQL Server con il servizio di Archiviazione BLOB di Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [Esercitazione: Backup e ripristino di SQL Server nel servizio di archiviazione BLOB di Windows Azure](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="managing-backups"></a>Gestione dei backup  
 Nell'elenco seguente sono inclusi i consigli generali sulla gestione dei backup:  
  
-   Per evitare la sovrascrittura accidentale dei BLOB, è consigliabile l'utilizzo di un nome file univoco per ogni backup.  
  
-   Quando si crea un contenitore, è consigliabile impostare il livello di accesso su **privato**, in modo che solo gli utenti o account che possono fornire le informazioni di autenticazione richieste possano leggere o scrivere i BLOB nel contenitore.  
  
-   Per i database di SQL Server in un'istanza di SQL Server in esecuzione in una macchina virtuale di Windows Azure, utilizzare un account di archiviazione nella stessa area della macchina virtuale per evitare i costi di trasferimento dei dati tra le aree. L'utilizzo della stessa area garantisce anche prestazioni ottimali per le operazioni di backup e ripristino.  
  
-   Un'attività di backup non completata correttamente può generare un file di backup non valido. Sono consigliate l'identificazione periodica dei backup non completati e l'eliminazione dei file BLOB. Per altre informazioni, vedere [Eliminazione dei file BLOB di backup con lease attivi](deleting-backup-blob-files-with-active-leases.md)  
  
-   L'utilizzo dell'opzione `WITH COMPRESSION` durante il backup consente di ridurre i costi di archiviazione e quelli delle transazioni di archiviazione. Inoltre, tramite questa opzione è possibile diminuire il tempo necessario per completare il processo di backup.  
  
## <a name="handling-large-files"></a>Gestione di file di grandi dimensioni  
  
-   Nell'operazione di backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono utilizzati più thread per ottimizzare il trasferimento dei dati ai servizi di archiviazione BLOB di Windows Azure.  Le prestazioni, tuttavia, dipendono da vari fattori, ad esempio la larghezza di banda del fornitore di software indipendente e le dimensioni del database. Se si intende eseguire il backup di database o filegroup di grandi dimensioni da un database di SQL Server locale, si consiglia di eseguire innanzitutto alcuni test della velocità effettiva. [Del archiviazione di Azure contratto di servizio](https://go.microsoft.com/fwlink/?LinkId=271619) hanno tempi di elaborazione massimi per i blob che è possibile prendere in considerazione.  
  
-   L'uso dell'opzione `WITH COMPRESSION` come consigliato nella sezione **Gestione dei backup** è molto importante quando si esegue il backup di file di grandi dimensioni.  
  
## <a name="troubleshooting-backup-to-or-restore-from-url"></a>Risoluzione dei problemi di backup nell'URL e di ripristino dallo stesso  
 Di seguito sono elencate alcune modalità rapide per la risoluzione di errori durante l'esecuzione del backup nel servizio di archiviazione BLOB di Windows Azure o del ripristino dallo stesso.  
  
 Per evitare errori a causa di limitazioni o le opzioni non supportate, esaminare l'elenco delle limitazioni e supporto per BACKUP e ripristino di informazioni di comandi nel [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Windows Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) articolo.  
  
 **Errori di autenticazione:**  
  
-   WITH CREDENTIAL è una nuova opzione ed è necessaria per le operazioni di backup nel servizio di archiviazione BLOB di Windows Azure e di ripristino dallo stesso. Di seguito sono riportati i possibili errori correlati alle credenziali:  
  
     Le credenziali specificate nel comando `BACKUP` o `RESTORE` non esistono. Per evitare questo problema, è possibile includere istruzioni T-SQL per creare le credenziali qualora non siano presenti nell'istruzione di backup. Di seguito è riportato un esempio pratico:  
  
    ```  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key> ;  
  
    ```  
  
-   Le credenziali esistono, ma all'account di accesso utilizzato per eseguire il comando di backup non sono associate autorizzazioni per accedere alle credenziali. Usare un account di accesso nel ruolo **db_backupoperator** con autorizzazioni **Modifica qualsiasi credenziale** .  
  
-   Verificare il nome dell'account di archiviazione e i valori di chiave. Le informazioni archiviate nelle credenziali devono corrispondere ai valori delle proprietà dell'account di archiviazione di Windows Azure utilizzati nelle operazioni di backup e ripristino.  
  
 **Errori di backup:**  
  
-   L'esecuzione di backup paralleli nello stesso BLOB comporta il mancato completamento di uno dei backup con conseguente errore **Inizializzazione non riuscita** .  
  
-   Utilizzare i log degli errori seguenti per facilitare la risoluzione degli errori di backup:  
  
    -   Impostare il flag di traccia 3051 per abilitare la registrazione in un log degli errori specifico con il formato seguente in:  
  
         BackupToUrl-\<nomeist>-\<nomedb>-azione-\<PID.log Dove \<azione> è uno dei valori seguenti:  
  
        -   `DB`  
  
        -   `FILELISTONLY`  
  
        -   `LABELONLY`  
  
        -   `HEADERONLY`  
  
        -   `VERIFYONLY`  
  
    -   È anche possibile trovare informazioni esaminando il registro eventi di Windows - registri in applicazioni con il nome "SQLBackupToUrl".  
  
-   Quando si esegue il ripristino da un backup compresso, è possibile che venga visualizzato l'errore seguente:  
  
    -   **Si è verificata un'eccezione SqlException 3284. Gravità: 16, stato: 5**  
        **Il contrassegno di file del messaggio nel dispositivo 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak' non è allineato. Eseguire nuovamente l'istruzione Restore con le stesse dimensioni di blocco usata per creare il set di backup: '65536' potrebbe essere un valore possibile.**  
  
         Per risolvere il problema, eseguire nuovamente l'istruzione `BACKUP` con il valore `BLOCKSIZE = 65536` specificato.  
  
-   Errore durante il backup a causa di BLOB con lease attivi: l'attività di backup non completata può generare BLOB con lease attivi.  
  
     Se si tenta di nuovo un'istruzione di backup, quest'ultimo potrebbe non essere completato e potrebbe essere visualizzato un errore simile al seguente:  
  
     **Il backup nell'URL ha ricevuto un'eccezione dall'endpoint remoto. Messaggio eccezione: Errore del server remoto: Qui (412) attualmente sono attivo un lease sul blob e nessun ID lease è stato specificato nella richiesta**.  
  
     Se un'istruzione RESTORE viene tentata in un file BLOB di backup con un lease attivo, l'operazione di ripristino non viene completata e viene visualizzato un errore simile al seguente:  
  
     **Messaggio eccezione: Errore del server remoto: (409) Conflict..**  
  
     Quando si verifica un errore di questo tipo, i file BLOB devono essere eliminati. Per altre informazioni su questo scenario e su come risolvere il problema, vedere [Eliminazione dei file BLOB di backup con lease attivi](deleting-backup-blob-files-with-active-leases.md)  
  
## <a name="proxy-errors"></a>Errori del proxy  
 Se si utilizzano server proxy per accedere a Internet, è possibile che si verifichino i problemi indicati di seguito:  
  
 **Limitazione della connessione da parte dei server proxy**  
  
 Nei server proxy possono essere presenti impostazioni che limitano il numero di connessioni al minuto. Il backup su URL è un processo multithread e pertanto può superare il limite. In questo caso, il server proxy termina la connessione. Per risolvere il problema, modificare le impostazioni del proxy in modo che non venga utilizzato in SQL Server.   Di seguito sono riportati alcuni esempi di tipi o messaggi di errore visualizzati nel log degli errori:  
  
-   Scrivere su "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak" non è riuscita: Backup su URL ha ricevuto un'eccezione dall'endpoint remoto. Messaggio eccezione: Impossibile leggere i dati dalla connessione del trasporto: La connessione è stata chiusa.  
  
-   Si è verificato un errore di I/O irreversibile nel file "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Impossibile recuperare l'errore dall'endpoint remoto.  
  
     Messaggio 3013, livello 16, stato 1, riga 2  
  
     Interruzione anomala di BACKUP DATABASE in corso.  
  
-   Backupiorequest:: Reportioerror: errore di scrittura nel dispositivo di backup http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak'. Errore del sistema operativo: Il backup nell'URL ha ricevuto un'eccezione dall'endpoint remoto. Messaggio eccezione: Impossibile leggere i dati dalla connessione del trasporto: La connessione è stata chiusa.  
  
 Se si abilita la registrazione dettagliata mediante il flag di traccia 3051, è inoltre possibile che nei log venga visualizzato il messaggio seguente:  
  
 Codice di stato HTTP 502. Messaggio di stato HTTP: errore del proxy (Il numero di richieste HTTP al minuto supera il limite configurato. Contattare l'amministratore di ISA Server).  )  
  
 **Impostazioni proxy predefinite non rilevate:**  
  
 Talvolta le impostazioni predefinite non vengono rilevate, causando errori di autenticazione del proxy come quello indicato di seguito:*Errore di I/O irreversibile nel file "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Il backup all'URL ha ricevuto un'eccezione dall'endpoint remoto. Messaggio eccezione: Errore del server remoto: (407)*  **Richiesta autenticazione proxy**.  
  
 Per risolvere il problema, creare un file di configurazione che consenta al processo di backup su URL di utilizzare le impostazioni predefinite del proxy effettuando i passaggi indicati di seguito.  
  
1.  Creare un file di configurazione denominato BackuptoURL.exe.config con il seguente codice XML:  
  
    ```  
    <?xml version ="1.0"?>  
    <configuration>   
                    <system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    </system.net>  
    </configuration>  
  
    ```  
  
2.  Inserire il file di configurazione nella cartella Binn dell'istanza di SQL Server. Ad esempio, se SQL Server è installato nell'unità C del computer, inserire il file di configurazione: *C:\Program Files\Microsoft SQL Server\MSSQL12. \<InstanceName > \MSSQL\Binn*.  
  
## <a name="troubleshooting-sql-server-managed-backup-to-windows-azure"></a>Risoluzione dei problemi relativi al backup gestito di SQL Server in Windows Azure  
 Poiché Backup gestito di SQL Server è compilato in Backup nell'URL, i suggerimenti per la risoluzione di problemi descritti nelle sezioni precedenti vengono applicati ai database o alle istanze tramite Backup gestito di SQL Server.  Informazioni sulla risoluzione dei problemi di SQL Server Managed Backup to Windows Azure sono descritto dettagliatamente [risoluzione dei problemi di SQL Server Managed Backup to Windows Azure](sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristino da backup archiviati in Windows Azure](restoring-from-backups-stored-in-microsoft-azure.md)  
  
  
