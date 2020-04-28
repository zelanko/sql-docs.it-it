---
title: Panoramica del backup (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server], backing up data
- backups [SQL Server]
- database backups [SQL Server]
- backup types [SQL Server]
- data backups [SQL Server]
- backing up tables [SQL Server]
- database restores [SQL Server], backups
- backing up [SQL Server], about backing up
- restoring [SQL Server], backup types
- backups [SQL Server], about
- backups [SQL Server], table-level backups unsupported
ms.assetid: 09a6e0c2-d8fd-453f-9aac-4ff24a97dc1f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bf284ffce044e0efa1f855e0e504a1f92dc7e3da
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "70175991"
---
# <a name="backup-overview-sql-server"></a>Backup Overview (SQL Server)
  In questo argomento viene presentato il componente di backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'esecuzione dei backup del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è essenziale per la protezione dei dati. In questa discussione vengono analizzati i tipi di backup e le relative restrizioni. In questo argomento vengono inoltre presentati i dispositivi e i supporti di backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Contenuto dell'argomento**  
  
-   [Componenti e concetti](#TermsAndDefinitions)  
  
-   [Compressione dei backup](#BackupCompression)  
  
-   [Restrizioni relative alle operazioni di backup in SQL Server](#Restrictions)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="components-and-concepts"></a><a name="TermsAndDefinitions"></a>Componenti e concetti  
 eseguire il backup  
 Operazione di copia di dati o record di log da un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dal relativo log delle transazioni in un dispositivo di backup, ad esempio un disco, per creare un backup dei dati o del log.  
  
 backup  
 Copia dei dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzabile per il recupero e il ripristino dei dati in seguito a errori. Un backup dei dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene creato al livello di un database o di uno o più dei relativi file o filegroup. Non è possibile creare backup a livello di tabella. Per utilizzare il modello di recupero con registrazione completa, oltre al backup dei dati è necessario creare backup del log delle transazioni.  
  
 [modello di recupero](recovery-models-sql-server.md)  
 Proprietà del database che controlla la manutenzione del log delle transazioni su un database. Sono tre i modelli di recupero disponibili: con registrazione minima, con registrazione completa e con registrazione minima delle operazioni bulk. Il modello di recupero del database ne determina i requisiti di backup e di ripristino.  
  
 [restore](restore-and-recovery-overview-sql-server.md)  
 Processo multifase che copia tutti i dati e le pagine di log da un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un database specificato ed esegue il rollforward di tutte le transazioni registrate nel backup applicando le modifiche registrate in modo da aggiornare i dati.  
  
 **Tipi di backup**  
  
 [backup di sola copia](copy-only-backups-sql-server.md)  
 Backup per utilizzo speciale indipendente dalla sequenza di backup convenzionali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 backup dei dati  
 Backup dei dati in un database completo (backup del database), database parziale (backup parziale) o set di file di dati o di filegroup (backup di file).  
  
 [backup del database](full-database-backups-sql-server.md)  
 Backup di un database. I backup completi del database rappresentano l'intero database al momento del completamento del backup. I backup differenziali del database contengono solo le modifiche apportate al database a partire dal backup del database più recente.  
  
 [backup differenziale](full-database-backups-sql-server.md)  
 Backup dei dati basato sull'ultimo backup completo di un database completo o parziale o di un set di file di dati o filegroup ( *base differenziale*) che contiene solo gli extent di dati modificati rispetto alla base differenziale.  
  
 Un backup parziale differenziale registra solo gli extent di dati che sono stati modificati nei filegroup dopo il backup parziale precedente, denominato base del backup differenziale.  
  
 backup completo  
 Backup dei dati che include tutti i dati in un database specifico o in un set di filegroup o file, oltre a una parte di log sufficiente al recupero di tali dati.  
  
 [backup di log](transaction-log-backups-sql-server.md)  
 Backup dei log delle transazioni che include tutti i record di log di cui non è stato eseguito il backup in un backup di log precedente. (modello di recupero con registrazione completa)  
  
 [backup di file](full-file-backups-sql-server.md)  
 Backup di uno o più file o filegroup di database.  
  
 [backup parziale](partial-backups-sql-server.md)  
 Contiene dati provenienti solo da una parte dei filegroup in un database, compresi i dati del filegroup primario, di ogni filegroup con accesso di lettura/scrittura e di eventuali file di sola lettura specificati opzionalmente.  
  
 **Termini e definizioni relativi ai supporti di backup**  
  
 [dispositivo di backup](backup-devices-sql-server.md)  
 Dispositivo nastro o disco in cui vengono scritti i backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e da cui è possibile eseguirne il ripristino. I backup di SQL Server possono anche essere scritti in un servizio Archiviazione BLOB di Azure e viene usato il formato **URL** per specificare la destinazione e il nome del file di backup. Per altre informazioni, vedere [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 [supporti di backup](media-sets-media-families-and-backup-sets-sql-server.md)  
 Uno o più nastri o file del disco in cui sono stati scritti uno o più backup.  
  
 [set di backup](media-sets-media-families-and-backup-sets-sql-server.md)  
 Contenuto di backup aggiunto a un set di supporti da un'operazione di backup completata.  
  
 [gruppo di supporti](media-sets-media-families-and-backup-sets-sql-server.md)  
 Backup creati su un singolo dispositivo senza mirroring o su un set di dispositivi con mirroring in un set di supporti  
  
 [set di supporti](media-sets-media-families-and-backup-sets-sql-server.md)  
 Raccolta ordinata di supporti di backup, nastri o file su disco, su cui una o più operazioni di backup hanno eseguito la scrittura usando un tipo e un numero fisso di dispositivi di backup.  
  
 [set di supporti con mirroring](mirrored-backup-media-sets-sql-server.md)  
 Più copie (copie mirror) di un set di supporti.  
  
##  <a name="backup-compression"></a><a name="BackupCompression"></a>Compressione dei backup  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e versioni successive. I backup compressi possono essere ripristinati in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive. Per altre informazioni, vedere [Compressione backup &#40;SQL Server&#41;](backup-compression-sql-server.md).  
  
##  <a name="restrictions-on-backup-operations-in-sql-server"></a><a name="Restrictions"></a>Limitazioni relative alle operazioni di backup in SQL Server  
 Il backup può verificarsi mentre il database è online e in uso. Si applicano tuttavia le restrizioni seguenti.  
  
### <a name="offline-data-cannot-be-backed-up"></a>Non è possibile eseguire il backup dei dati offline  
 Se si fa riferimento in modo implicito o esplicito a dati offline, l'operazione di backup ha esito negativo. Alcuni esempi comuni sono i seguenti:  
  
-   Si richiede un backup completo del database, ma un filegroup del database è offline. Poiché tutti i filegroup vengono inclusi implicitamente in un backup completo del database, questa operazione ha esito negativo.  
  
     Per eseguire un backup del database, è possibile utilizzare un backup del file e specificare solo i filegroup online.  
  
-   Viene richiesto un backup parziale, ma un filegroup di lettura/scrittura è offline. Dato che tutti i filegroup di lettura/scrittura sono necessari per un backup parziale, l'operazione non riesce.  
  
-   Si richiede un backup di file specifici, ma uno di tali file non è online. L'operazione ha esito negativo. Per eseguire il backup dei file online, è possibile escludere il file offline dall'elenco dei file e ripetere l'operazione.  
  
 In genere, un backup del log riesce anche se uno o più file di dati non sono disponibili. Tuttavia, se uno o più file contengono modifiche con registrazione minima delle operazioni bulk apportate nel modello di recupero con registrazione minima delle operazioni bulk, è necessario che tutti i file siano online perché il backup riesca.  
  
### <a name="concurrency-restrictions-during-backup"></a>Restrizioni di concorrenza durante il backup  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza un processo di backup online per consentire un backup del database mentre questo è in uso. Durante un backup, è possibile eseguire la maggior parte delle operazioni, ad esempio istruzioni INSERT, UPDATE o DELETE. Tuttavia, se si tenta di avviare un'operazione di backup durante la creazione o l'eliminazione di un file di database, l'operazione verrà rimandata fino al completamento dell'operazione di creazione o di eliminazione, oppure verrà annullata a causa di un timeout.  
  
 Le operazioni che non possono essere eseguite durante un backup del database o del log delle transazioni sono le seguenti:  
  
-   Operazioni di gestione dei file, ad esempio l'istruzione ALTER DATABASE con l'opzione ADD FILE o REMOVE FILE.  
  
-   Compattazione di database o file, incluse operazioni di compattazione automatica.  
  
-   Se durante l'esecuzione di un'operazione di backup si tenta di creare o eliminare un file di database, l'operazione di creazione o eliminazione non riuscirà.  
  
 Se un'operazione di backup si sovrappone a un'operazione di gestione di file o di compattazione, si verifica un conflitto. Indipendentemente dall'operazione in conflitto avviata per prima, la seconda operazione attende il timeout del blocco impostato dalla prima operazione. Il periodo di timeout è controllato da un'impostazione di timeout della sessione. Se il blocco viene rilasciato durante il periodo di timeout, la seconda operazione continua. Se il periodo di timeout scade, la seconda operazione non viene eseguita.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
 **Per utilizzare i dispositivi di backup e i supporti di backup**  
  
-   [Definire un dispositivo di backup logico per un file su disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definizione di un dispositivo di backup logico per un'unità nastro &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Specificare un disco o un nastro come destinazione di backup &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Eliminare un dispositivo di backup &#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
-   [Impostazione della data di scadenza di un backup &#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Visualizzare i file di dati e i file di log in un set di backup &#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Ripristinare un backup da un dispositivo &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
-   [Esercitazione: Backup e ripristino di SQL Server nel servizio di archiviazione BLOB di Azure](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
 **Per creare un backup**  
  
> [!NOTE]  
>  Per eseguire backup parziali o di sola copia è necessario usare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) rispettivamente con l'opzione PARTIAL o COPY_ONLY.  
  
-   [Creazione di un backup completo del database &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [Backup di file e filegroup &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [Creare un backup differenziale del database &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [Esecuzione del backup del log delle transazioni quando il database è danneggiato &#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [Abilitare o disabilitare il checksum di backup durante il backup o il ripristino &#40;SQL Server&#41;](enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [Specifica se un'operazione di backup o ripristino viene arrestata o prosegue in seguito a un errore &#40;SQL Server&#41;](specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
-   [Utilizzo di Resource Governor per limitare l'utilizzo della CPU da parte della compressione dei backup &#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [Esercitazione: Backup e ripristino di SQL Server nel servizio di archiviazione BLOB di Azure](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Backup e ripristino di database di SQL Server](back-up-and-restore-of-sql-server-databases.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [Piani di manutenzione](../maintenance-plans/maintenance-plans.md)   
 [Log delle transazioni &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [Modelli di recupero &#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  
