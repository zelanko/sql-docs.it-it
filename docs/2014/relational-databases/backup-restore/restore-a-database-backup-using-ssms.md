---
title: Ripristinare un backup del database (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.locatebackupfileazure.f1
- sql12.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 521fc35b8ada4b1eb6c62e75fed4e1d9f99d21c4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "70154784"
---
# <a name="restore-a-database-backup-sql-server-management-studio"></a>Ripristino di un backup del database (SQL Server Management Studio)
  In questo argomento viene descritto come ripristinare un backup completo del database.  
  
> [!IMPORTANT]  
>  Nel modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk, prima di poter ripristinare un database in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è necessario effettuare il backup del log delle transazioni attivo, noto come parte finale del log. Per altre informazioni, vedere [Backup di un log delle transazioni &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md). Per ripristinare un database crittografato, è necessario poter accedere alla chiave asimmetrica o al certificato utilizzato per crittografare il database. Non è possibile effettuare l'operazione di ripristino del database senza almeno uno di questi due elementi. Di conseguenza, il certificato utilizzato per crittografare la chiave di crittografia del database deve essere conservato fino a quando il backup è necessario. Per altre informazioni, vedere [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md).  
  
 Si noti che se si ripristina un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versione successiva in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], il database viene aggiornato automaticamente. In genere, il database diventa subito disponibile. Tuttavia, se in un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] sono inclusi indici full-text, questi vengono importati, reimpostati o ricompilati dal processo di aggiornamento, a seconda dell'impostazione della proprietà del server **Opzione di aggiornamento full-text** . Se l'opzione di aggiornamento è impostata su **Importa** o **Ricompila**, gli indici full-text non saranno disponibili durante l'aggiornamento. A seconda della quantità di dati indicizzati, l'importazione può richiedere diverse ore, mentre la ricompilazione può risultare dieci volte più lunga. Si noti inoltre che, quando l'opzione di aggiornamento è impostata su **Importa**e un catalogo full-text non è disponibile, gli indici full-text associati vengono ricompilati. Per informazioni sulla visualizzazione o sulla modifica dell'impostazione della proprietà **Opzione di aggiornamento full-text** , vedere [Gestione e monitoraggio della ricerca full-text per un'istanza del server](../search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
### <a name="to-restore-a-full-database-backup"></a>Per ripristinare un backup completo del database  
  
1.  Dopo aver eseguito la connessione all'istanza appropriata del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in Esplora oggetti fare clic sul nome del server per espandere l'albero del server.  
  
2.  Espandere **Database**. A seconda del database, selezionare un database utente oppure espandere **Database di sistema**e selezionare un database di sistema.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **attività**, **Ripristina**, quindi fare clic su **database**per aprire la finestra di dialogo **Ripristina database** .  
  
4.  Per specificare l'origine e il percorso dei set di backup da ripristinare, nella pagina **Generale** , utilizzare la sezione **Origine** . Selezionare una delle opzioni seguenti:  
  
    -   **Database**  
  
         Selezionare il database da ripristinare dall'elenco a discesa. Nell'elenco sono inclusi solo i database di cui è stato eseguito il backup in base alla cronologia dei backup di **msdb** .  
  
    > [!NOTE]  
    >  Se il backup viene eseguito da un server diverso, il server di destinazione non disporrà delle informazioni della cronologia di backup per il database specificato. In questo caso, selezionare **Dispositivo** per specificare manualmente il file o il dispositivo da ripristinare.  
  
    -   **Dispositivo**  
  
         Fare clic sul pulsante Sfoglia (**..**.) per aprire la finestra di dialogo **Seleziona dispositivi di backup** . Nella casella **Tipi di supporti di backup** selezionare uno dei tipi di dispositivi elencati. Per selezionare uno o più dispositivi per la casella **Supporti di backup** , fare clic su **Aggiungi**.  
  
         Dopo avere aggiunto i dispositivi desiderati nella casella di riepilogo **Dispositivi di backup** , fare clic su **OK** per tornare alla pagina **Generale** .  
  
         Nella casella di riepilogo **Origine: Dispositivo: Database** selezionare il nome del database da ripristinare.  
  
        > [!NOTE]  
        >  Questo elenco è disponibile solo quando l'opzione **Dispositivo** è selezionata. Saranno disponibili solo i database che dispongono di backup sul dispositivo selezionato.  
  
         **Supporti di backup**  
         Selezionare il supporto per l'operazione di ripristino: **file**, **nastro**, **URL**o **dispositivo di backup**. L'opzione **Nastro** viene visualizzata solo se nel computer è montata un'unità nastro, mentre l'opzione **Dispositivo di backup** viene visualizzata solo se è disponibile almeno un dispositivo di backup.  
  
         **Percorso backup**  
         Consente di visualizzare, aggiungere o rimuovere supporti per l'operazione di ripristino. L'elenco può contenere fino a 64 file, nastri o dispositivi di backup.  
  
         **Aggiungere**  
         Aggiunge il percorso di un dispositivo di backup all'elenco dei **percorsi di backup** . A seconda del tipo di supporto selezionato nel campo supporti di **backup** , fare clic su **Aggiungi** per aprire una delle seguenti finestre di dialogo.  
  
        |Tipo di supporto|Finestra di dialogo|Descrizione|  
        |----------------|----------------|-----------------|  
        |**File**|**Individua file di backup**|In questa finestra di dialogo è possibile selezionare un file locale nell'albero o specificare un file remoto utilizzandone il nome completo in formato UNC (Universal Naming Convention). Per altre informazioni, vedere [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md).|  
        |**Dispositivo**|**Selezionare il dispositivo di backup**|In questa finestra di dialogo è possibile eseguire una selezione da un elenco di dispositivi di backup logici definiti sull'istanza del server.|  
        |**Nastro**|**Seleziona unità nastro**|In questa finestra di dialogo è possibile eseguire una selezione da un elenco di unità nastro fisicamente collegate al computer che esegue l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
        |**URL**|Verranno avviate due finestre di dialogo nell'ordine seguente:<br /><br /> 1) **connettersi ad archiviazione di Azure**<br /><br /> 2) **individuare il file di backup in Azure**|Nella finestra di dialogo **Connetti ad archiviazione di Azure** selezionare le credenziali SQL esistenti che archiviano il nome dell'account di archiviazione di Azure e le informazioni sulla chiave di accesso oppure creare nuove credenziali SQL specificando il nome dell'account di archiviazione e le informazioni sulla chiave di accesso alle archiviazione. Per altre informazioni, vedere [connettersi ad archiviazione di Azure &#40;ripristinare&#41;](connect-to-microsoft-azure-storage-restore.md).<br /><br /> Nella finestra di dialogo **Individua file di backup** è possibile selezionare un file dall'elenco di contenitori visualizzato nel frame a sinistra.|  
  
         Se l'elenco è completo, il pulsante **Aggiungi** non è disponibile.  
  
         **Rimuovi**  
         Consente di rimuovere uno o più file, nastri o dispositivi di backup logici selezionati.  
  
         **Sommario**  
         Consente di visualizzare il contenuto del supporto di un file, un nastro o un dispositivo di backup logico selezionato.  
  
5.  Nella sezione **Destinazione** , la casella **Database** viene popolata automaticamente con il nome del database da ripristinare. Per modificare il nome del database, immettere il nome nuovo nella casella **Database** .  
  
6.  Nella casella **Ripristina fino a** mantenere l'impostazione predefinita **Ultimo backup eseguito** oppure fare clic su **Cronologia** per accedere alla finestra di dialogo **Cronologia di backup** e selezionare manualmente un momento specifico per arrestare l'azione di recupero. Per altre informazioni sull'indicazione di un momento specifico, vedere [Sequenza temporale di backup](backup-timeline.md).  
  
7.  Nella griglia **Selezionare i set di backup da ripristinare** selezionare i set di backup che si desidera ripristinare. In questa griglia vengono visualizzati i backup disponibili per il percorso specificato. Per impostazione predefinita, viene suggerito un piano di recupero. Per ignorare il piano di recupero suggerito, è possibile modificare le impostazioni selezionate nella griglia. I backup che dipendono dal ripristino di un backup precedente vengono automaticamente deselezionati quando il backup precedente è deselezionato. Per informazioni sulle colonne nella griglia **Selezionare i set di backup da ripristinare** , vedere [Ripristina database &#40;pagina Generale&#41;](../../integration-services/general-page-of-integration-services-designers-options.md).  
  
8.  Facoltativamente, fare clic su **File** nel riquadro **Seleziona una pagina** per accedere alla finestra di dialogo **File** . In questa finestra è possibile ripristinare il database in un nuovo percorso specificando una destinazione di ripristino nuova per ogni file nella griglia **Ripristina file di database come**. Per altre informazioni su questa griglia, vedere [Ripristina database&#40;(pagina File)&#41;](restore-database-files-page.md).  
  
9. Per visualizzare o selezionare le opzioni avanzate, nella pagina **Opzioni** del pannello **Opzioni di ripristino** è possibile selezionare una delle opzioni seguenti, in base alla situazione:  
  
    1.  Opzioni `WITH` (non richieste):  
  
        -   **Sovrascrivi il database esistente (WITH REPLACE)**  
  
        -   **Mantieni le impostazioni di replica (WITH KEEP_REPLICATION)**  
  
        -   **Limitazione dell'accesso al database ripristinato (con RESTRICTED_USER)**  
  
    2.  Selezionare un'opzione per la casella **Stato di recupero** . Questa casella determina lo stato del database al termine dell'operazione di ripristino.  
  
        -   **RESTORE WITH RECOVERY** è il comportamento predefinito che lascia il database pronto per l'utilizzo mediante il rollback delle transazioni di cui non è stato eseguito il commit. I log delle transazioni aggiuntivi non possono essere ripristinati. Selezionare questa opzione se si desidera ripristinare subito tutti i backup necessari.  
  
        -   **RESTORE WITH NORECOVERY** lascia il database non operativo e non esegue il rollback delle transazioni di cui non è stato eseguito il commit. I log delle transazioni aggiuntivi possono essere ripristinati. Non è possibile utilizzare il database fino al completamento del recupero.  
  
        -   **RESTORE WITH STANDBY** lascia il database in modalità di sola lettura. Annulla le transazioni di cui non è stato eseguito il commit, ma salva le azioni di rollback in un file standby in modo che gli effetti del recupero possano essere annullati.  
  
    3.  **Esegui il backup della parte finale del log prima del ripristino** verrà selezionato se necessario per il punto nel tempo selezionato. Non è necessario modificare questa impostazione, ma è possibile scegliere di eseguire il backup della parte finale del log, anche se non è richiesto. Inserire il nome file in questa posizione? Se il primo set di backup nella pagina **generale** è in Azure, verrà eseguito il backup anche del log della parte finale nello stesso contenitore di archiviazione.  
  
    4.  Le operazioni di ripristino potrebbero non riuscire in presenza di connessioni attive al database. Selezionare l'opzione **Chiudi connessioni esistenti** per garantire che tutte le connessioni attive tra [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e il database vengano chiuse. Questa casella di controllo imposta il database sulla modalità utente singolo prima di effettuare qualsiasi operazione di ripristino e imposta il database sulla modalità multiutente al termine.  
  
    5.  Selezionare **Chiedi conferma prima del ripristino di ogni backup** se si desidera ricevere una richiesta di conferma prima di ciascuna operazione di ripristino. L'operazione non è normalmente necessaria, a meno che le dimensioni del database siano elevate e si desideri monitorare lo stato dell'operazione di ripristino.  
  
     Per altre informazioni su queste opzioni di ripristino, vedere [Ripristina database &#40;pagina Opzioni&#41;](restore-database-options-page.md).  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [Creazione di un backup completo del database &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)   
 [Ripristinare un database in un nuovo percorso &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)   
 [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Pagina Opzioni di ripristino &#40;database&#41;](restore-database-options-page.md)   
 [Ripristina database &#40;pagina Generale&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  
