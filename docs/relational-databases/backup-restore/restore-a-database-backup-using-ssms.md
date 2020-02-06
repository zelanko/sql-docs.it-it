---
title: Ripristinare un backup del database tramite SSMS | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.locatebackupfileazure.f1
- sql13.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7cd893c9556b1dd45e2206ce73740e253af98ed3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "70278763"
---
# <a name="restore-a-database-backup-using-ssms"></a>Ripristinare un backup del database tramite SSMS
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In questo argomento viene descritto come ripristinare un backup completo del database tramite SQL Server Management Studio.    
       
### <a name="important"></a>Importante!    
Prima di poter ripristinare un database nel modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk, è necessario eseguire il backup del log delle transazioni attivo, noto come [parte finale del log](tail-log-backups-sql-server.md). Per altre informazioni, vedere [Backup di un log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md).  

Quando si ripristina un database da un'altra istanza, vedere le informazioni in [Gestione dei metadati quando si rende disponibile un database in un'altra istanza del server (SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).   
    
Per ripristinare un database crittografato, è necessario accedere al certificato o alla chiave asimmetrica usata per crittografare il database in questione. Non è possibile effettuare l'operazione di ripristino del database senza almeno uno di questi due elementi. È necessario mantenere il certificato usato per crittografare la chiave di crittografia del database fino al salvataggio del backup. Per altre informazioni, vedere [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).    
    
Se si ripristina un database di una versione precedente a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], il database viene aggiornato automaticamente a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Questo impedisce l'uso del database con una versione precedente di [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. Tuttavia, ciò interessa solo l'aggiornamento dei metadati e non influisce sul [livello di compatibilità del database](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md). Se il livello di compatibilità di un database utente è 100 o superiore prima dell'aggiornamento, rimane invariato dopo l'aggiornamento. Se il livello di compatibilità è 90 prima dell'aggiornamento, nel database aggiornato viene impostato su 100, ovvero sul livello di compatibilità supportato più basso in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
In genere, il database diventa subito disponibile. Tuttavia, se in un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] sono inclusi indici full-text, questi vengono importati, reimpostati o ricompilati dal processo di aggiornamento, a seconda dell'impostazione della proprietà del server **Opzione di aggiornamento full-text** . Se l'opzione di aggiornamento è impostata su **Importa** o **Ricompila**, gli indici full-text non saranno disponibili durante l'aggiornamento. A seconda della quantità di dati indicizzati, l'importazione può richiedere diverse ore, mentre la ricompilazione può risultare dieci volte più lunga.     
    
Quando l'opzione di aggiornamento è impostata su **Importa**e un catalogo full-text non è disponibile, gli indici full-text associati vengono ricompilati. Per informazioni sulla visualizzazione o sulla modifica dell'impostazione della proprietà **Opzione di aggiornamento full-text** , vedere [Gestione e monitoraggio della ricerca full-text per un'istanza del server](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).    

Per informazioni sul ripristino di SQL Server da un servizio di archiviazione BLOB di Microsoft Azure, vedere [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).

## <a name="examples"></a>Esempi
    
### <a name="a-restore-a-full-database-backup"></a>R. Ripristinare un backup del database completo   
    
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
    
2.  Fare clic con il pulsante destro del mouse su **Database** e scegliere **Ripristina database...**    
    
3.  Per specificare l'origine e il percorso dei set di backup da ripristinare, nella pagina **Generale** , utilizzare la sezione **Origine** . Selezionare una delle opzioni seguenti:    
    
    -   **Database**    
    
         Selezionare il database da ripristinare dall'elenco a discesa. Nell'elenco sono inclusi solo i database di cui è stato eseguito il backup in base alla cronologia dei backup di **msdb** .    
    
        > [!NOTE]
        > Se il backup viene eseguito da un server diverso, il server di destinazione non disporrà delle informazioni della cronologia di backup per il database specificato. In questo caso, selezionare **Dispositivo** per specificare manualmente il file o il dispositivo da ripristinare. 
    
    -   **Dispositivo**    
    
         Fare clic sul pulsante Sfoglia ( **...** ) per aprire la finestra di dialogo **Seleziona dispositivi di backup** . 
         
        -   Finestra di dialogo**Seleziona dispositivi di backup**  
        
            **Tipo di supporto di backup**  
         Selezionare un tipo di supporto dall'elenco a discesa **Tipo di supporti di backup** .  Nota: l'opzione **Nastro** viene visualizzata solo se nel computer è montata un'unità nastro, mentre l'opzione **Dispositivo di backup** viene visualizzata solo se è disponibile almeno un dispositivo di backup.

            **Aggiungere**  
            In base al tipo di supporto selezionato nell'elenco a discesa **Tipo di supporti di backup** , facendo clic su **Aggiungi** , si apre una delle finestre di dialogo seguenti. Se l'elenco nella casella di riepilogo **Supporti di backup** è pieno, il pulsante **Aggiungi** non è disponibile.

            |Tipo di supporto|Finestra di dialogo|Descrizione|    
            |----------------|----------------|-----------------|    
            |**File**|**Individua file di backup**|In questa finestra di dialogo è possibile selezionare un file locale nell'albero o specificare un file remoto utilizzandone il nome completo in formato UNC (Universal Naming Convention). Per altre informazioni, vedere [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).|    
            |**Dispositivo**|**Selezionare il dispositivo di backup**|In questa finestra di dialogo è possibile eseguire una selezione da un elenco di dispositivi di backup logici definiti sull'istanza del server.|    
            |**Nastro**|**Seleziona unità nastro**|In questa finestra di dialogo è possibile eseguire una selezione da un elenco di unità nastro fisicamente collegate al computer che esegue l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|    
            |**URL**|**Selezionare un percorso del file di backup**|In questa finestra di dialogo è possibile selezionare un contenitore di archiviazione esistente con credenziali di SQL Server o di Azure, aggiungere un nuovo contenitore di archiviazione di Azure con firma di accesso condiviso oppure creare una firma di accesso condiviso e credenziali di SQL Server per un contenitore di archiviazione esistente.  Vedere anche [Connect to a Microsoft Azure Subscription](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)(Connettersi a una sottoscrizione di Microsoft Azure)|  
         
             **Rimuovi**    
             Consente di rimuovere uno o più file, nastri o dispositivi di backup logici selezionati.    
                 
             **Sommario**    
            Consente di visualizzare il contenuto del supporto di un file, un nastro o un dispositivo di backup logico selezionato.  Questo pulsante potrebbe non funzionare se il tipo di supporto è **URL**.  

             **Supporti di backup**   
             Elenca i supporti selezionati.
    
             Dopo avere aggiunto i dispositivi desiderati nella casella di riepilogo **Dispositivi di backup** , fare clic su **OK** per tornare alla pagina **Generale** .    
    
         Nella casella di riepilogo **Origine: Dispositivo: Database** selezionare il nome del database da ripristinare.    
    
         > [!NOTE]
         > Questo elenco è disponibile solo quando l'opzione **Dispositivo** è selezionata. Saranno disponibili solo i database che dispongono di backup sul dispositivo selezionato.    
     
4.  Nella sezione **Destinazione** , la casella **Database** viene popolata automaticamente con il nome del database da ripristinare. Per modificare il nome del database, immettere il nome nuovo nella casella **Database** .    
    
5.  Nella casella **Ripristina fino a** mantenere l'impostazione predefinita **Ultimo backup eseguito** oppure fare clic su **Cronologia** per accedere alla finestra di dialogo **Cronologia di backup** e selezionare manualmente un momento specifico per arrestare l'azione di recupero. Per altre informazioni sull'indicazione di un momento specifico, vedere [Sequenza temporale di backup](../../relational-databases/backup-restore/backup-timeline.md).    
    
6.  Nella griglia **Selezionare i set di backup da ripristinare** selezionare i set di backup che si desidera ripristinare. In questa griglia vengono visualizzati i backup disponibili per il percorso specificato. Per impostazione predefinita, viene suggerito un piano di recupero. Per ignorare il piano di recupero suggerito, è possibile modificare le impostazioni selezionate nella griglia. I backup che dipendono dal ripristino di un backup precedente vengono automaticamente deselezionati quando il backup precedente è deselezionato. Per informazioni sulle colonne nella griglia **Selezionare i set di backup da ripristinare** , vedere [Ripristina database &#40;pagina Generale&#41;](../../relational-databases/backup-restore/restore-database-general-page.md).    
    
7.  Facoltativamente, fare clic su **File** nel riquadro **Seleziona una pagina** per accedere alla finestra di dialogo **File** . In questa finestra è possibile ripristinare il database in un nuovo percorso specificando una destinazione di ripristino nuova per ogni file nella griglia **Ripristina file di database come**. Per altre informazioni su questa griglia, vedere [Ripristina database&#40;(pagina File)&#41;](../../relational-databases/backup-restore/restore-database-files-page.md).    
    
8. Per visualizzare o selezionare le opzioni avanzate, nella pagina **Opzioni** del pannello **Opzioni di ripristino** è possibile selezionare una delle opzioni seguenti, in base alla situazione:    

   1. Opzioni**WITH** (non obbligatorie):    
    
     - **Sovrascrivi il database esistente (WITH REPLACE)**    
    
     - **Mantieni le impostazioni di replica (WITH KEEP_REPLICATION)**    
    
     - **Limita accesso al database ripristinato (WITH RESTRICTED_USER)**    
    
   2. Selezionare un'opzione per la casella **Stato di recupero** . Questa casella determina lo stato del database al termine dell'operazione di ripristino.    
    
     - **RESTORE WITH RECOVERY** è il comportamento predefinito che lascia il database pronto per l'utilizzo mediante il rollback delle transazioni di cui non è stato eseguito il commit. I log delle transazioni aggiuntivi non possono essere ripristinati. Selezionare questa opzione se si desidera ripristinare subito tutti i backup necessari.    
    
     - **RESTORE WITH NORECOVERY** lascia il database non operativo e non esegue il rollback delle transazioni di cui non è stato eseguito il commit. I log delle transazioni aggiuntivi possono essere ripristinati. Non è possibile utilizzare il database fino al completamento del recupero.    
    
     - **RESTORE WITH STANDBY** lascia il database in modalità di sola lettura. Annulla le transazioni di cui non è stato eseguito il commit, ma salva le azioni di rollback in un file standby in modo che gli effetti del recupero possano essere annullati.    
    
   3. **Eseguire il backup della parte finale del log prima del ripristino.** Non in tutti gli scenari di ripristino è necessario un backup della parte finale del log.  Per altre informazioni, vedere **Scenari in cui è necessario un backup della parte finale del log** in [Backup della parte finale del log (SQL Server).](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)
  
   4. Le operazioni di ripristino potrebbero non riuscire in presenza di connessioni attive al database. Selezionare l'opzione **Chiudi connessioni esistenti** per garantire che tutte le connessioni attive tra [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e il database vengano chiuse. Questa casella di controllo imposta il database sulla modalità utente singolo prima di effettuare qualsiasi operazione di ripristino e imposta il database sulla modalità multiutente al termine.    
  
   5. Selezionare **Chiedi conferma prima del ripristino di ogni backup** se si desidera ricevere una richiesta di conferma prima di ciascuna operazione di ripristino. L'operazione non è normalmente necessaria, a meno che le dimensioni del database siano elevate e si desideri monitorare lo stato dell'operazione di ripristino.    
    
Per altre informazioni su queste opzioni di ripristino, vedere [Ripristina database &#40;pagina Opzioni&#41;](../../relational-databases/backup-restore/restore-database-options-page.md).    
    
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="b-restore-an-earlier-disk-backup-over-an-existing-database"></a>B. Ripristinare un backup del disco precedente su un database esistente
Nell'esempio seguente viene ripristinato un backup del disco precedente di `Sales` e viene sovrascritto il database `Sales` esistente.

1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
2.  Fare clic con il pulsante destro del mouse su **Database** e scegliere **Ripristina database...**  
3.  Nella pagina **Generale** selezionare **Dispositivo** nella sezione **Origine** .
4.  Fare clic sul pulsante Sfoglia ( **...** ) per aprire la finestra di dialogo **Seleziona dispositivi di backup** . Fare clic su **Aggiungi** e passare al backup. Fare clic su **OK** dopo aver selezionato i file di backup su disco.
5.  Fare clic su **OK** per tornare alla pagina **Generale** .
6.  Fare clic su **Opzioni** nel riquadro **Seleziona una pagina** .
7.  Nella sezione **Opzioni di ripristino** selezionare **Sovrascrivi il database esistente (WITH REPLACE)** .

    > [!NOTE]
    > Se non si seleziona questa opzione è possibile che sia visualizzato il messaggio di errore seguente: "System.Data.SqlClient.SqlError: Il set di backup include il backup di un database diverso dal database '`Sales`' esistente. (Microsoft.SqlServer.SmoExtended)"

8.  Nella sezione **Backup della parte finale del log** deselezionare **Esegui il backup della parte finale del log prima del ripristino**.

    > [!NOTE]
    > Non in tutti gli scenari di ripristino è necessario un backup della parte finale del log. Se il punto di recupero è contenuto in un backup del log precedente, non è necessario un backup della parte finale del log. Non è inoltre necessario eseguire il backup della parte finale del log se il punto di recupero è incluso in un backup del log precedente o se si sta spostando o sostituendo (sovrascrivendo) il database e non è necessario ripristinarlo fino a un punto nel tempo dopo l'ultimo backup. Per altre informazioni, vedere [Backup della parte finale del log (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).

    Questa opzione non è disponibile per i database nel modello di recupero con registrazione minima.

9.  Nella sezione **Connessioni server** selezionare **Chiudi connessioni esistenti ai database di destinazione**.

    > [!NOTE]
    > Se non si seleziona questa opzione è possibile che sia visualizzato il messaggio di errore seguente: "System.Data.SqlClient.SqlError: Impossibile ottenere accesso esclusivo al database perché è in uso. (Microsoft.SqlServer.SmoExtended)"
    
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="c--restore-an-earlier-disk-backup-with-a-new-database-name-where-the-original-database-still-exists"></a>C.  Ripristinare un backup del disco precedente con un nome di database nuovo in cui è già esistente il database originale
Nell'esempio seguente viene ripristinato un backup del disco precedente di `Sales` e viene creato un database nuovo con il nome `SalesTest`.  Il database originale `Sales`è già esistente nel server.

1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
2.  Fare clic con il pulsante destro del mouse su **Database** e scegliere **Ripristina database...**  
3.  Nella pagina **Generale** selezionare **Dispositivo** nella sezione **Origine** .
4.  Fare clic sul pulsante Sfoglia ( **...** ) per aprire la finestra di dialogo **Seleziona dispositivi di backup** . Fare clic su **Aggiungi** e passare al backup. Fare clic su **OK** dopo aver selezionato i file di backup su disco.
5.  Fare clic su **OK** per tornare alla pagina **Generale** .
6.  Nella sezione **Destinazione** , la casella **Database** viene popolata automaticamente con il nome del database da ripristinare. Per modificare il nome del database, immettere il nome nuovo nella casella **Database** .
7.  Fare clic su **Opzioni** nel riquadro **Seleziona una pagina** .
8.  Nella sezione **Backup della parte finale del log** deselezionare "**Esegui il backup della parte finale del log prima del ripristino**".

    > [!IMPORTANT]
    > Se non si deseleziona questa opzione, il database esistente `Sales`passerà allo stato di ripristino.

9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

    > [!NOTE]
    > Se fosse visualizzato il seguente messaggio di errore:      
    > "System.Data.SqlClient.SqlError: La parte finale del log per il database "`Sales`" non è stata inclusa nel backup. Se il log contiene informazioni che non si desidera perdere, utilizzare `BACKUP LOG WITH NORECOVERY` per eseguire il backup del log. Se si desidera semplicemente sovrascrivere il contenuto del log, utilizzare la clausola `WITH REPLACE`o `WITH STOPAT` dell'istruzione `RESTORE`. (Microsoft.SqlServer.SmoExtended)".      
    > Probabilmente non è stato immesso il nuovo nome del database come descritto nel passo 6 precedente. In genere, il ripristino impedisce la sovrascrittura accidentale di un database con un altro. Se il database specificato in un'istruzione `RESTORE` esiste già nel server corrente e il GUID del gruppo di database specificato è diverso da quello registrato nel set di backup, il database non verrà ripristinato. Questa misura di sicurezza è importante.

### <a name="d--restore-earlier-disk-backups-to-a-point-in-time"></a>D.  Ripristinare i backup del disco precedenti in un momento specifico
Nell'esempio seguente viene ripristinato lo stato del database corrispondente alle ore `1:23:17 PM` del giorno `May 30, 2016` e viene illustrata un'operazione di ripristino di più backup del log. Il database attualmente non esiste nel server.

1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
2.  Fare clic con il pulsante destro del mouse su **Database** e scegliere **Ripristina database...**  
3.  Nella pagina **Generale** selezionare **Dispositivo** nella sezione **Origine** .
4.  Fare clic sul pulsante Sfoglia ( **...** ) per aprire la finestra di dialogo **Seleziona dispositivi di backup** . Fare clic su **Aggiungi** e passare al backup completo e a tutti i backup del log delle transazioni rilevanti.  Fare clic su **OK** dopo aver selezionato i file di backup su disco.
5.  Fare clic su **OK** per tornare alla pagina **Generale** .
6.  Nella sezione **Destinazione** fare clic su **Sequenza temporale** per accedere alla finestra di dialogo **Sequenza temporale di backup** e selezionare manualmente un momento in cui arrestare l'azione di recupero.
7.  Selezionare **Data e ora specifiche**.  
8.  Modificare l' **Intervallo sequenza temporale** nella casella di riepilogo a discesa **Ora** (facoltativo).  
9.  Spostare il dispositivo di scorrimento sul tempo desiderato.
10. Fare clic su **OK** per tornare alla pagina Generale.
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="e--restore-a-backup-from-the-microsoft-azure-storage-service"></a>E.  Ripristinare un backup dal servizio di archiviazione di Microsoft Azure

#### <a name="common-steps"></a>Passaggi comuni
Nei due esempi seguenti viene eseguito un ripristino di `Sales` da un backup che si trova nel servizio di archiviazione di Microsoft Azure.  Il nome dell'account di archiviazione è `mystorageaccount`, mentre  il nome del contenitore è `myfirstcontainer`.  Per essere più concisi, i primi sei passaggi sono elencati di seguito una volta sola e tutti gli esempi verranno avviati con il **passaggio 7**.
1.  In **Esplora oggetti**connettersi a un'istanza del motore di database di SQL Server e, successivamente, espanderla.
2.  Fare clic con il pulsante destro del mouse su **Database** e scegliere **Ripristina database....** .
3.  Nella pagina **Generale** selezionare **Dispositivo** nella sezione **Origine** .
4.  Fare clic sul pulsante Sfoglia (...) per aprire la finestra di dialogo **Seleziona dispositivi di backup** .    
5.  Selezionare **URL** dall'elenco a discesa **Tipo di supporti di backup:** .
6.  Fare clic su **Aggiungi** e scegliere **Selezionare un percorso del file di backup** .

#### <a name="e1---restore-a-striped-backup-over-an-existing-database-and-a-shared-access-signature-exists"></a>E1.   Ripristinare un backup con striping in un database esistente con firma di accesso condiviso esistente.
Sono stati creati criteri di accesso archiviati con diritti di lettura, scrittura ed elenco.  Per il contenitore `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`è stata creata una firma di accesso condiviso associata ai criteri di accesso archiviati.  I passaggi sono essenzialmente gli stessi se sono già esistenti credenziali di SQL Server.  Il database `Sales` non esiste attualmente nel server.  I file di backup sono `Sales_stripe1of2_20160601.bak` e `Sales_stripe2of2_20160601.bak`.  

1.  Selezionare `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` dall'elenco a discesa **Contenitore di archiviazione di Azure:** se esistono già credenziali di SQL Server, altrimenti immettere manualmente il nome del contenitore, vale a dire `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`. 
1. Digitare la firma di accesso condiviso nella casella di testo con formattazione **Firma di accesso condiviso:** .
1. Fare clic su **OK** . Si aprirà la finestra di dialogo **Trova file di backup in Microsoft Azure** .
1. Espandere **Contenitori** e scegliere `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`.
1. Tenendo premuto CTRL e selezionare i file `Sales_stripe1of2_20160601.bak` e `Sales_stripe2of2_20160601.bak`.
1. Fare clic su **OK**.
1. Fare clic su **OK** per tornare alla pagina **Generale** .
1. Fare clic su **Opzioni** nel riquadro **Seleziona una pagina** .
1. Nella sezione **Opzioni di ripristino** selezionare **Sovrascrivi il database esistente (WITH REPLACE)** .
1. Nella sezione **Backup della parte finale del log** deselezionare **Esegui il backup della parte finale del log prima del ripristino**.
1. Nella sezione **Connessioni server** selezionare **Chiudi connessioni esistenti ai database di destinazione**.
1. Fare clic su **OK**.

#### <a name="e2---a-shared-access-signature-does-not-exist"></a>E2.   Non esiste una firma di accesso condiviso
In questo esempio il database `Sales` non esiste attualmente nel server.
1. Fare clic su **Aggiungi** . Si aprirà la finestra di dialogo **Connetti a una sottoscrizione Microsoft** .  
1. Completare la finestra di dialogo **Connetti a una sottoscrizione Microsoft** e fare clic su **OK** per tornare alla finestra di dialogo **Selezionare un percorso del file di backup** .  Per altre informazioni, vedere [Connect to a Microsoft Azure Subscription](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md) (Connettersi a una sottoscrizione di Microsoft Azure).
1. Fare clic su **OK** nella finestra di dialogo **Selezionare un percorso del file di backup** . Si aprirà la finestra di dialogo **Trova file di backup in Microsoft Azure** .
1. Espandere **Contenitori** e scegliere `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`.
1. Selezionare il file e fare clic su **OK**.
1. Fare clic su **OK** per tornare alla pagina **Generale** .
1. Fare clic su **OK**.

#### <a name="f-restore-local-backup-to-microsoft-azure-storage-url"></a>F. Ripristinare un backup locale nell'archiviazione di Microsoft Azure
Il database `Sales` sarà ripristinato nel contenitore di archiviazione di Microsoft Azure `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` da un backup che si trova nel percorso `E:\MSSQL\BAK`.  Le credenziali di SQL Server per il contenitore di Azure sono già state create.  È necessario che le credenziali di SQL Server per il contenitore di destinazione siano già esistenti in quanto non è possibile crearle nell'attività di **ripristino** .  Il database `Sales` non esiste attualmente nel server.
1.  In **Esplora oggetti**connettersi a un'istanza del motore di database di SQL Server e, successivamente, espanderla.
2.  Fare clic con il pulsante destro del mouse su **Database** e scegliere **Ripristina database....** .
3.  Nella pagina **Generale** selezionare **Dispositivo** nella sezione **Origine** .
4.  Fare clic sul pulsante Sfoglia (...) per aprire la finestra di dialogo **Seleziona dispositivi di backup** .  
5.  Selezionare **File** dall'elenco a discesa **Tipo di supporti di backup:** .
6.  Fare clic su **Aggiungi** . Si aprirà la finestra di dialogo **Trova file di backup** .
7.  Scegliere `E:\MSSQL\BAK`, selezionare il file di backup e fare clic su **OK**.
8.  Fare clic su **OK** per tornare alla pagina **Generale** .
9.  Selezionare **File** nel riquadro **Seleziona una pagina** .
10. Selezionare la casella **Riloca tutti i file nella cartella**.
11. Immettere il contenitore `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`nelle caselle di testo per **Cartella file di dati:** e **Cartella file di log:** .
12. Fare clic su **OK**.

## <a name="see-also"></a>Vedere anche    
 [Backup di un log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)     
 [Creare un backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)     
 [Ripristinare un database in una nuova posizione &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)     
 [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)     
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)     
 [Ripristina database &#40;pagina Opzioni&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)     
 [Ripristina database &#40;pagina Generale&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)    
    
  
