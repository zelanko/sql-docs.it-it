---
title: Backup e ripristino di database SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], see restoring [SQL Server]
- backups [SQL Server]
- restoring databases [SQL Server]
- backup [SQL Server], see backing up [SQL Server]
- databases [SQL Server], restoring
- backing up databases [SQL Server]
- restore [SQL Server], see restoring [SQL Server]
- disaster recovery [SQL Server], see backing up [SQL Server]
- backing up [SQL Server]
- Database Engine [SQL Server], backups
- databases [SQL Server], backups
ms.assetid: 570a21b3-ad29-44a9-aa70-deb2fbd34f27
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 586a1315c2d8e73d5010964864560db0fc0012fd
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890812"
---
# <a name="back-up-and-restore-of-sql-server-databases"></a>Backup e ripristino di database SQL Server
  In questo argomento vengono descritti i vantaggi dell'esecuzione del backup dei database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e illustrati i termini di base del backup e del ripristino. Vengono inoltre presentate alcune strategie di backup e ripristino per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e alcune considerazioni relative alla sicurezza per il backup e il ripristino di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Il componente di backup e ripristino di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rappresenta uno strumento essenziale per la sicurezza e la protezione di dati di importanza critica archiviati nei database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per ridurre il rischio di perdita irreversibile dei dati, è necessario eseguire regolarmente il backup dei database per preservare le modifiche ai dati. Una strategia di backup e ripristino ben pianificata aiuta a proteggere i database dalla perdita di dati causata da vari tipi di guasti e problemi. Il test della strategia mediante il ripristino di un set di backup e il recupero del database assicura una efficace preparazione a reagire in qualsiasi emergenza.  
  
 Oltre alle risorse di archiviazione locale per l'archiviazione di backup, SQL Server supporta anche il backup e il ripristino dal servizio di archiviazione BLOB di Windows Azure. Per altre informazioni, vedere [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Windows Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  

  
##  <a name="Benefits"></a> Vantaggi  
  
-   L'esecuzione di backup dei database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , l'esecuzione di procedure di ripristino di test sui backup e l'archiviazione delle copie di backup in una posizione esterna sicura costituiscono modi validi per evitare una perdita di dati potenzialmente irreversibile.  
  
    > [!IMPORTANT]  
    >  Questo è l'unico modo per proteggere in maniera affidabile i dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Con backup validi di un database, è possibile recuperare i dati a seguito di molti tipi di guasti ed errori, quali:  
  
    -   Errori di funzionamento dei supporti.  
  
    -   Errori degli utenti, ad esempio l'eliminazione accidentale di una tabella.  
  
    -   Errori hardware, ad esempio un'unità disco danneggiata o la perdita definitiva di un server.  
  
    -   Calamità naturali o altre emergenze gravi. Tramite il backup di SQL Server nel servizio di archiviazione BLOB di Windows Azure, è possibile creare un backup esterno in un'area diversa dalla posizione locale da utilizzare in caso si venga colpiti da una calamità naturale.  
  
-   I backup di un database risultano inoltre utili per le attività di amministrazione di routine, ad esempio la copia di un database da un server a un altro, l'impostazione di [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] o del mirroring del database e l'archiviazione.  
  

  
##  <a name="TermsAndDefinitions"></a> Componenti e concetti  
 eseguire il backup  
 Operazione di copia di dati o record di log da un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dal relativo log delle transazioni in un dispositivo di backup, ad esempio un disco, per creare un backup dei dati o del log.  
  
 backup  
 Copia dei dati utilizzabile per il ripristino e il recupero in seguito a un errore. I backup di un database possono essere utilizzati anche per ripristinare una copia del database in una nuova posizione.  
  
 dispositivo di backup  
 Dispositivo disco o nastro nel quale vengono scritti i backup di SQL Server e da cui è possibile eseguirne il ripristino. I backup di SQL Server possono anche essere scritti in un servizio di archiviazione BLOB di Windows Azure e il formato **URL** viene utilizzato per specificare la destinazione e il nome del file di backup. Per altre informazioni, vedere [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Windows Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 supporti di backup  
 Uno o più nastri o file del disco in cui sono stati scritti uno o più backup.  
  
 backup dei dati  
 Backup dei dati in un database completo (backup del database), database parziale (backup parziale) o set di file di dati o di filegroup (backup di file).  
  
 backup del database  
 Backup di un database. I backup completi del database rappresentano l'intero database al momento del completamento del backup. I backup differenziali del database contengono solo le modifiche apportate al database a partire dal backup del database più recente.  
  
 backup differenziale  
 Backup dei dati basato sull'ultimo backup completo di un database completo o parziale o di un set di file di dati o di filegroup (base differenziale) che contiene solo i dati modificati rispetto a quella base.  
  
 backup completo  
 Backup dei dati che include tutti i dati in un database specifico o in un set di filegroup o file, oltre a una parte di log sufficiente al recupero di tali dati.  
  
 backup di log  
 Backup dei log delle transazioni che include tutti i record di log di cui non è stato eseguito il backup in un backup di log precedente. (modello di recupero con registrazione completa)  
  
 recuperare  
 Riportare un database a uno stato stabile e coerente.  
  
 recovery  
 Fase di avvio del database o di ripristino con recupero che porta il database in uno stato coerente a livello di transazioni.  
  
 modello di recupero  
 Proprietà del database che controlla la manutenzione del log delle transazioni su un database. Sono tre i modelli di recupero disponibili: con registrazione minima, con registrazione completa e con registrazione minima delle operazioni bulk. Il modello di recupero del database ne determina i requisiti di backup e di ripristino.  
  
 ripristino  
 Processo multifase che copia tutti i dati e le pagine di log da un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un database specificato ed esegue il rollforward di tutte le transazioni registrate nel backup applicando le modifiche registrate in modo da aggiornare i dati.  
  

  
##  <a name="BnrStrategies"></a>Introduzione alle strategie di backup e ripristino  
 Il backup e il ripristino dei dati devono essere personalizzati per uno specifico ambiente e devono funzionare con le risorse disponibili. Per un utilizzo affidabile delle funzionalità di backup e ripristino è pertanto necessaria un'apposita strategia. Una strategia ben progettata a tale scopo ottimizza la disponibilità dei dati e ne riduce al minimo la perdita, rispettando al contempo le esigenze aziendali specifiche.  
  
> [!IMPORTANT]  
>  Archiviare il database e i backup su dispositivi separati. In caso contrario, se nel dispositivo contenente il database si verifica un errore, i backup non saranno disponibili. L'archiviazione dei dati e dei backup su dispositivi separati migliora inoltre le prestazioni di I/O sia per la scrittura dei backup che per l'utilizzo in produzione del database.  
  
 Tale strategia prevede una parte relativa al backup e una parte relativa al ripristino. La parte della strategia relativa al backup definisce il tipo e la frequenza delle operazioni di backup, il tipo e la velocità dell'hardware necessario, le modalità di esecuzione di test dei backup, nonché i percorsi e le modalità di archiviazione dei relativi supporti, incluse le considerazioni relative alla sicurezza. La parte della strategia relativa al ripristino definisce il responsabile dell'esecuzione delle operazioni di ripristino e la modalità di esecuzione di tali operazioni in modo da realizzare gli obiettivi relativi alla disponibilità del database e ridurre al minimo il rischio di perdita dei dati. È consigliabile documentare le procedure di backup e ripristino e mantenerne una copia nella documentazione relativa alle procedure operative aziendali.  
  
 La progettazione di una strategia di backup e ripristino efficace richiede operazioni accurate di pianificazione, implementazione e testing. È necessario eseguire test. Una strategia di backup può essere considerata efficace solo dopo il completamento del ripristino dei backup in tutte le combinazioni incluse nella strategia. È necessario considerare una vasta gamma di fattori, tra cui:  
  
-   Obiettivi di produzione dell'organizzazione per i database, in particolar modo i requisiti relativi alla disponibilità e alla protezione dalla perdita dei dati.  
  
-   Caratteristiche di ogni database, ovvero dimensioni, tipo di utilizzo, tipo di contenuto, requisiti relativi ai dati e così via.  
  
-   Vincoli relativi alle risorse, ad esempio hardware, personale, spazio per l'archiviazione dei supporti di backup, sicurezza fisica dei supporti archiviati e così via.  
  
    > [!NOTE]  
    >  Il formato di archiviazione su disco di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è lo stesso sia negli ambienti a 64 bit sia negli ambienti a 32 bit. È pertanto possibile eseguire il backup e il ripristino tra ambienti a 32 bit e ambienti a 64 bit. Un backup creato su un'istanza del server in esecuzione in un ambiente può essere ripristinato su un'istanza del server in esecuzione nell'altro ambiente.  
  

  
### <a name="impact-of-the-recovery-model-on-backup-and-restore"></a>Impatto del modello di recupero sulle operazioni di backup e di ripristino  
 Le operazioni di backup e di ripristino si verificano nel contesto di un modello di recupero, ovvero una proprietà del database tramite la quale si controlla la modalità di gestione del log delle transazioni. Il modello di recupero di un database determina inoltre i tipi di scenari di backup e ripristino supportati per il database. In genere, in un database viene utilizzato il modello di recupero con registrazione minima o il modello di recupero con registrazione completa. Il modello di recupero con registrazione completa può essere integrato passando al modello di recupero con registrazione minima delle operazioni bulk prima delle operazioni bulk. Per un'introduzione a questi modelli di recupero e alla loro influenza sulla gestione del log delle transazioni, vedere [Log delle transazioni &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md).  
  
 Il modello di recupero migliore per un database dipende dalle esigenze aziendali. Per evitare la gestione del log delle transazioni e semplificare le operazioni di backup e ripristino, è possibile utilizzare il modello di recupero con registrazione minima. Per ridurre al minimo il rischio di perdita di dati, aumentando tuttavia il numero di operazioni amministrative, è possibile utilizzare il modello di recupero con registrazione completa. Per informazioni sull'effetto dei modelli di recupero sulle operazioni di backup e ripristino, vedere [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md).  
  
### <a name="design-the-backup-strategy"></a>Progettare la strategia di backup  
 Dopo aver selezionato un modello di recupero che soddisfa le esigenze aziendali per un determinato database, è necessario pianificare e implementare una strategia di backup corrispondente. La strategia ottimale dipende da una serie di fattori. Di seguito vengono riportati i più significativi:  
  
-   Numero di ore giornaliere per cui è necessario garantire l'accesso delle applicazioni al database.  
  
     Se è possibile prevedere un periodo di minore attività, è consigliabile pianificare i backup completi del database durante tale periodo.  
  
-   Frequenza prevista per l'esecuzione di modifiche e aggiornamenti.  
  
     Se le modifiche sono frequenti, considerare gli aspetti seguenti:  
  
    -   Nel modello di recupero con registrazione minima è consigliabile pianificare backup differenziali nei periodi intermedi tra i backup completi del database. Con un backup differenziale è possibile acquisire solo le modifiche successive all'ultimo backup completo del database.  
  
    -   Nel modello di recupero con registrazione completa è necessario pianificare backup frequenti del log. La pianificazione di backup differenziali nei periodi intermedi tra i backup completi consente di ridurre i tempi di ripristino limitando il numero di backup del log da ripristinare in seguito al ripristino dei dati.  
  
-   Ambito previsto per le modifiche, ovvero solo in parti ridotte del database o in gran parte del database.  
  
     Per un database di dimensioni estese in cui le modifiche sono concentrate in una parte dei file o dei filegroup, i backup parziali e/o i backup del file possono risultare utili. Per altre informazioni, vedere [Backup parziali &#40; SQL Server &#41;](partial-backups-sql-server.md) e [Backup dei file completo &#40; SQL Server &#41;](full-file-backups-sql-server.md).  
  
-   Quantità di spazio su disco necessaria per un backup completo del database.  
  
     Per altre informazioni, vedere [Stimare le dimensioni di un backup completo del database](#EstimateDbBuSize), più avanti in questa sezione.  
  
####  <a name="EstimateDbBuSize"></a>Stima delle dimensioni di un backup completo del database  
 Prima di implementare una strategia di backup e ripristino, stimare quanto spazio su disco verrà utilizzato da un backup del database completo. Con l'operazione di backup i dati contenuti nel database vengono copiati nel file di backup. Poiché il backup include soltanto i dati presenti nel database, ma non lo spazio inutilizzato, le dimensioni del backup risultano di solito inferiori a quelle del database originale. È possibile stimare la dimensione di un backup del database completo tramite la stored procedure di sistema **sp_spaceused**. Per altre informazioni, vedere [sp_spaceused &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql).  
  
### <a name="schedule-backups"></a>Pianificare le operazioni di backup  
 L'esecuzione di un'operazione di backup ha un effetto minimo sulle transazioni in esecuzione; è possibile quindi eseguire le operazioni di backup durante le operazioni normali. È possibile eseguire un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un effetto minimo sui carichi di lavoro di produzione.  
  
> [!NOTE]  
>  Per informazioni sulle restrizioni di concorrenza durante il backup, vedere [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md).  
  
 Dopo aver stabilito i tipi di backup necessari e la frequenza di esecuzione per ogni tipo, è consigliabile pianificare backup regolari come parte di un piano di manutenzione per il database. Per informazioni sui piani di manutenzione e su come crearli per i backup di database e di log, vedere [Use the Maintenance Plan Wizard](../maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
### <a name="test-your-backups"></a>Eseguire il test dei backup  
 Una strategia di ripristino può essere considerata efficace solo dopo l'esecuzione di test dei backup. È essenziale testare accuratamente la strategia di backup per ogni database ripristinando una copia del database in un sistema di prova. È necessario testare il ripristino di tutti i tipi di backup che si desidera utilizzare.  
  
 È consigliabile mantenere un manuale operativo per ogni database, in cui indicare la posizione dei backup, i nomi dei dispositivi di backup (se presenti) e il tempo necessario per il ripristino dei backup di prova.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
### <a name="scheduling-backup-jobs"></a>Pianificazione dei processi di backup  
  
-   [Creare un piano di manutenzione](../maintenance-plans/create-a-maintenance-plan.md)  
  
-   [Creazione di un processo](../../ssms/agent/create-a-job.md)  
  
-   [Pianificare un processo](../../ssms/agent/schedule-a-job.md)  
  
### <a name="working-with-backup-devices-and-backup-media"></a>Utilizzo dei dispositivi di backup e dei supporti di backup  
  
-   [Definizione di un dispositivo di backup logico per un file su disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definire un dispositivo di backup logico per un'unità nastro &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Specificare un disco o un nastro come destinazione di backup &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Eliminare un dispositivo di backup &#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
-   [Impostare la data di scadenza di un backup &#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Visualizzare i file di dati e i file di log in un set di backup &#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Ripristino di un backup da un dispositivo &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
### <a name="creating-backups"></a>Creazione di backup  
  
> [!NOTE]  
>  Per eseguire backup parziali o di sola copia è necessario usare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) rispettivamente con l'opzione PARTIAL o COPY_ONLY.  
  
 **Utilizzo di SQL Server Management Studio**  
  
-   [Creazione di un backup completo del database &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [Eseguire il backup di file e filegroup &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [Creare un backup differenziale del database &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
 **Utilizzo di Transact-SQL**  
  
-   [Utilizzo di Resource Governor per limitare l'utilizzo della CPU da parte della compressione dei backup &#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [Esecuzione del backup del log delle transazioni quando il database è danneggiato &#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [Abilitare o disabilitare il checksum di backup durante il backup o il ripristino &#40;SQL Server&#41;](enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [Specifica se un'operazione di backup o ripristino viene arrestata o prosegue in seguito a un errore &#40;SQL Server&#41;](specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  

  
### <a name="restoring-data-backups"></a>Ripristino di backup dei dati  
 **Utilizzo di SQL Server Management Studio**  
  
-   [Ripristinare un backup &#40;del database SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Ripristinare un database in una nuova posizione &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
-   [Ripristinare un backup differenziale del database &#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)  
  
-   [Ripristino di file e filegroup &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
 **Utilizzo di Transact-SQL**  
  
-   [Ripristinare un backup del database nel modello di recupero con registrazione minima &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Ripristinare un database al punto di errore nel modello di recupero con registrazione completa &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Ripristinare file e filegroup sovrascrivendo file esistenti &#40;SQL Server&#41;](restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Ripristinare file in un percorso nuovo &#40;SQL Server&#41;](restore-files-to-a-new-location-sql-server.md)  
  
-   [Ripristinare il database master &#40;Transact-SQL&#41;](restore-the-master-database-transact-sql.md)  
  

  
### <a name="restoring-transaction-logs-full-recovery-model"></a>Ripristino di log delle transazioni (modello di recupero con registrazione completa)  
 **Utilizzo di SQL Server Management Studio**  
  
-   [Ripristino di un database fino a una transazione contrassegnata &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
-   [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
 **Utilizzo di Transact-SQL**  
  
-   [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  

  
### <a name="additional-restore-tasks"></a>Attività di ripristino aggiuntive  
 **Utilizzo di Transact-SQL**  
  
-   [Riavviare un'operazione di ripristino interrotta &#40;Transact-SQL&#41;](restart-an-interrupted-restore-operation-transact-sql.md)  
  
-   [Recuperare un database senza ripristino dei dati &#40;Transact-SQL&#41;](recover-a-database-without-restoring-data-transact-sql.md)  
  

  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Backup e ripristino di database di Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)   
 [Backup e ripristino di indici e cataloghi full-text](../search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [Backup e ripristino di database replicati](../replication/administration/back-up-and-restore-replicated-databases.md)   
 [Log delle transazioni &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [Modelli di recupero &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
