---
title: Backup in Windows Azure gestito di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: afa01165-39e0-4efe-ac0e-664edb8599fd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b4071bee5e13f415be90328bb7ff0b55ff91087c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877130"
---
# <a name="sql-server-managed--backup-to-windows-azure"></a>Backup gestito di SQL Server in Windows Azure
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] consente di gestire e automatizzare i backup di SQL Server nel servizio di archiviazione BLOB di Windows Azure. La strategia di backup utilizzata da [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] è basata sul periodo di memorizzazione e sul carico di lavoro della transazione nel database. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] supporta il ripristino temporizzato per il periodo di memorizzazione specificato.   
[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] può essere abilitato a livello di database o a livello di istanza per gestire tutti i database nell'istanza di SQL Server. SQL Server può essere eseguito in locale o in ambienti ospitati come la macchina virtuale di Windows Azure. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] è consigliato per SQL Server in esecuzione su macchine virtuali di Azure.  
  
## <a name="benefits-of-automating-sql-server-backup-using-includesssmartbackupincludesss-smartbackup-mdmd"></a>Vantaggi dell'automatizzazione del backup di SQL Server tramite [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
-   Per l'automatizzazione di backup per più database sono attualmente richiesti lo sviluppo di una strategia di backup, la scrittura di codice personalizzato e la pianificazione di backup. Utilizzando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] è necessario fornire solo le impostazioni del periodo di memorizzazione e il percorso di archiviazione. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] Pianifica, esegue e gestisce i backup.  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] può essere configurato a livello di database o con le impostazioni predefinite per un'istanza di SQL Server. L'automatizzazione del backup tramite [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] offre i vantaggi seguenti:  
  
    -   Configurando le impostazioni predefinite a livello di istanza, è possibile applicare queste impostazioni a qualsiasi database creato successivamente, eliminando di conseguenza il rischio di mancata esecuzione di backup di nuovi database e di perdita di dati.  
  
    -   Abilitando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] e impostando il periodo di memorizzazione a livello di database è possibile ignorare le impostazioni predefinite configurate a livello di istanza. In questo modo si dispone di un controllo più dettagliato sulla recuperabilità di un database specifico.  
  
-   Con [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] non è necessario specificare il tipo o la frequenza dei backup di un database.  Si specifica il periodo di memorizzazione e [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] determina il tipo e la frequenza di backup per un database vengono archiviati i backup nel servizio di archiviazione Blob di Windows Azure. Per altre informazioni sui set di criteri che [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per creare la strategia di backup, vedere la [componenti e concetti](#Concepts) in questo argomento.  
  
-   Se configurato per utilizzare la crittografia, viene incrementato il livello di sicurezza dei dati di backup. Per altre informazioni, vedere [crittografia dei Backup](backup-encryption.md)  
  
 Per altre informazioni sui vantaggi dell'uso dell'archiviazione Blob di Windows Azure per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i backup, vedere [SQL Server Backup and Restore with Windows Azure Blob Storage Service](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
## <a name="terms-and-definitions"></a>Termini e definizioni  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
 Funzionalità di SQL Server tramite cui il backup di database viene automatizzato e i backup vengono gestiti in base al periodo di memorizzazione.  
  
 Periodo di memorizzazione  
 Periodo di memorizzazione usato da [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per determinare quali file di backup devono essere mantenuti nella risorsa di archiviazione per recuperare un database fino a una data e ora specifiche comprese nell'intervallo di tempo specificato.  I valori supportati sono compresi nell'intervallo 1-30 giorni.  
  
 Catena di log  
 Una sequenza continua di backup del log è denominata catena di log. Una catena di log ha inizio con un backup completo del database.  
  
##  <a name="Concepts"></a> I requisiti, concetti e componenti  
  
  
###  <a name="Security"></a> Autorizzazioni  
 Transact-SQL è l'interfaccia principale utilizzata per configurare e monitorare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. In generale, stored procedure, eseguire la configurazione **db_backupoperator** ruolo del database con **ALTER ANY CREDENTIAL** autorizzazioni, e `EXECUTE` le autorizzazioni per **sp_delete BackupHistory** stored procedure è necessaria.  Per le stored procedure e le funzioni utilizzate per esaminare le informazioni sono in genere richieste rispettivamente le autorizzazioni `Execute` per la stored procedure e `Select` per la funzione.  
  
###  <a name="Prereqs"></a> Prerequisiti  
 **Prerequisiti**  
  
 **Servizio di archiviazione di Microsoft Azure** viene usato da [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per archiviare i file di backup.    I concetti, struttura e i requisiti per la creazione di un account di archiviazione di Azure è illustrato dettagliatamente nel [Introduzione a Key Components and Concepts](sql-server-backup-to-url.md#intorkeyconcepts) sezione il **Backup di SQL Server nell'URL** argomento.  
  
 **Credenziali SQL** viene usato per archiviare le informazioni necessarie per autenticare l'account di archiviazione Windows Azure. Tramite l'oggetto relativo alle credenziali SQL vengono archiviati il nome dell'account e le informazioni sulla chiave di accesso. Per altre informazioni, vedere la [Introduzione a Key Components and Concepts](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) sezione il **Backup di SQL Server nell'URL** argomento. Per una procedura dettagliata su come creare una credenziale SQL per archiviare le informazioni di autenticazione di archiviazione di Microsoft Azure, vedere [lezione 2: Creare una credenziale di SQL Server](../../tutorials/lesson-2-create-a-sql-server-credential.md).  
  
###  <a name="Concepts_Components"></a> Concetti e componenti chiave  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] è una funzionalità tramite cui vengono gestite le operazioni di backup. Archivia i metadati nel **msdb** i backup del log dei processi di sistema di database e viene utilizzato per scrivere completo del database e delle transazioni.  
  
#### <a name="components"></a>Componenti  
 Transact-SQL è l'interfaccia principale per interagire con [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Le stored procedure di sistema vengono utilizzate per l'abilitazione, la configurazione e il monitoraggio di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Le funzioni di sistema vengono utilizzate per recuperare le informazioni sui file di backup, i valori dei parametri e le impostazioni di configurazione esistenti. Gli eventi estesi vengono utilizzati per esporre errori e avvisi. I meccanismi di avviso sono abilitati tramite i processi di SQL Agent e la gestione basata su criteri di SQL Server. Di seguito sono riportati un elenco di oggetti e una descrizione della relativa funzionalità rispetto a [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 Per configurare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]sono disponibili anche i cmdlet di PowerShell. SQL Server Management Studio supporta il ripristino dei backup creati da [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] tramite l'attività **Ripristina database** .  
  
|||  
|-|-|  
|Oggetto di sistema|Descrizione|  
|**MSDB**|Vengono archiviati i metadati e la cronologia di backup di tutti i backup creati da [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|[smart_admin.set_db_backup &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/dn451013(v=sql.120).aspx)|Stored procedure di sistema per abilitare e configurare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per un database.|  
|[smart_admin.set_instance_backup &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/dn451009(v=sql.120).aspx)|Stored procedure per abilitare e configurare le impostazioni predefinite di sistema [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per l'istanza di SQL Server.|  
|[smart_admin.sp_ backup_master_switch &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql)|Stored procedure di sistema per sospendere e riprendere [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|[smart_admin.sp_set_parameter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql)|Stored procedure di sistema per abilitare e configurare il monitoraggio di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Esempi: abilitazione di eventi estesi, impostazioni della posta elettronica per le notifiche.|  
|[smart_admin.sp_backup_on_demand &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)|Stored procedure che viene usata per eseguire un backup ad hoc per un database abilitato per l'uso di sistema [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] senza interruzione della catena di log.|  
|[smart_admin.fn_backup_db_config &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-backup-db-config-transact-sql)|Funzione di sistema che restituisce l'attuale [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] valori di configurazione e lo stato per un database o per tutti i database nell'istanza.|  
|[smart_admin.fn_is_master_switch_on &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-is-master-switch-on-transact-sql)|Funzione di sistema tramite cui viene restituito lo stato del parametro master.|  
|[smart_admin.sp_get_backup_diagnostics &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-get-backup-diagnostics-transact-sql)|Stored procedure di sistema utilizzata per restituire gli eventi registrati dagli eventi estesi.|  
|[smart_admin.fn_get_parameter &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql)|Funzione di sistema tramite cui vengono restituiti i valori correnti delle impostazioni di sistema di backup, ad esempio le impostazioni di monitoraggio e di posta elettronica per gli avvisi.|  
|[smart_admin.fn_available_backups &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql)|Stored procedure utilizzata per recuperare i backup disponibili per un determinato database o per tutti i database in un'istanza.|  
|[smart_admin.fn_get_current_xevent_settings &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql)|Funzione di sistema tramite cui vengono restituite le impostazioni correnti degli eventi estesi.|  
|[smart_admin.fn_get_health_status &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-health-status-transact-sql)|Funzione di sistema tramite cui vengono restituiti i conteggi aggregati di errori registrati dagli eventi estesi per un periodo specificato.|  
|[Monitorare il backup gestito di SQL Server in Windows Azure](sql-server-managed-backup-to-microsoft-azure.md)|Eventi estesi per il monitoraggio, la notifica tramite posta elettronica di errori e avvisi e la gestione basata su criteri di SQL Server per [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
  
#### <a name="backup-strategy"></a>Strategia di backup  
 **Strategia di backup utilizzata da [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:**  
  
 Il tipo di backup pianificato e la frequenza di backup vengono stabiliti in base al carico di lavoro del database. Le impostazioni del periodo di memorizzazione vengono utilizzate per determinare la durata di conservazione di un file di backup nell'archiviazione e la possibilità di recupero del database fino a una temporizzazione entro il periodo di memorizzazione.  
  
 **Convenzioni di denominazione dei File e contenitori di backup:**  
  
 Tramite [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] viene assegnato un nome al contenitore di archiviazione Windows Azure utilizzando il nome dell'istanza di SQL Server per tutti i database ad eccezione dei database di disponibilità.  Per i database di disponibilità viene utilizzato il GUID del gruppo di disponibilità per assegnare un nome al contenitore di archiviazione Windows Azure.  
  
 Il file di backup per database di disponibilità non vengono denominate usando la convenzione seguente: Il nome viene creato usando i primi 40 caratteri del nome del database, il GUID del database senza il '-' e il timestamp. Il carattere di sottolineatura viene inserito tra i segmenti come separatore. Per il backup completo viene utilizzata l'estensione di file **BAK** , mentre per i backup del log viene utilizzata **LOG** . Per i database del gruppo di disponibilità, oltre alla convenzione di denominazione file descritta in precedenza, viene aggiunto il GUID del database del gruppo di disponibilità dopo i 40 caratteri del nome del database. Il valore GUID del database del gruppo di disponibilità è il valore per group_database_id in sys.databases.  
  
 **Backup completo del Database:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pianifica un backup completo del database se una delle operazioni seguenti è vera.  
  
-   Un database è abilitato da [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per la prima volta o quando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] viene abilitato con le impostazioni predefinite a livello di istanza.  
  
-   L'aumento delle dimensioni del log dopo l'ultimo backup completo del database è uguale o maggiore di 1 GB.  
  
-   È passato l'intervallo di tempo massimo di una settimana dall'ultimo backup completo del database.  
  
-   La catena di log è stata interrotta. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] vengono eseguiti controlli periodici per determinare se la catena di log è intatta confrontando il primo e l'ultimo LSN dei file di backup. Se si verifica un'interruzione nella catena di log per qualsiasi motivo, tramite [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] viene pianificato un backup completo del database. Nella maggior parte dei casi le interruzioni della catena di log sono dovute probabilmente a un comando di backup eseguito tramite Transact-SQL o mediante l'attività di backup in SQL Server Management Studio.  Tra gli altri scenari comuni sono incluse l'eliminazione accidentale dei file di log di backup o la sovrascrittura accidentale dei backup.  
  
 **Backup del Log delle transazioni:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pianifica un backup del log se una delle seguenti condizioni:  
  
-   Non sono disponibili cronologie di backup del log. Questa situazione si verifica in genere quando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] viene abilitato per la prima volta.  
  
-   Lo spazio del log delle transazioni utilizzato è pari ad almeno 5 MB.  
  
-   È stato raggiunto l'intervallo di tempo massimo di 2 ore dall'ultimo backup del log.  
  
-   Ogni volta che il backup del log delle transazioni è in ritardo rispetto a un backup completo del database. L'obiettivo è quello di anticipare la catena di log rispetto al backup completo.  
  
#### <a name="retention-period-settings"></a>Impostazioni del periodo di memorizzazione  
 Quando si abilita il backup è necessario impostare il periodo di conservazione in giorni: Il valore minimo è 1 giorno e il valore massimo è 30 giorni.  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] basato sulle impostazioni del periodo di memorizzazione viene valutata la possibilità di eseguire un recupero fino a una data e ora specifiche in un tempo specificato, per determinare quali file di backup mantenere e quali invece eliminare. L'oggetto backup_finish_date del backup viene utilizzato per determinare e far corrispondere il tempo specificato in base alle impostazioni del periodo di memorizzazione.  
  
#### <a name="important-considerations"></a>Importanti considerazioni  
 Vi sono alcune considerazioni importanti per comprendere il relativo impatto sulle operazioni di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Tali considerazioni sono elencate di seguito:  
  
-   Per un database, se è in esecuzione un processo di backup completo del database esistente, tramite [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] si attende il completamento del processo corrente prima di eseguire un altro backup completo dello stesso database. Analogamente, solo un backup del log delle transazioni può essere in esecuzione in un determinato momento. Tuttavia, un backup completo del database e un backup del log delle transazioni possono essere eseguiti contemporaneamente. Gli errori vengono registrati come eventi estesi.  
  
-   Se sono pianificati più di 10 backup completi del database simultanei, viene generato un avviso tramite il canale di debug di eventi estesi. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] viene quindi gestita una coda di priorità per i database rimanenti di cui deve essere eseguito un backup fino alla pianificazione e al completamento di tutti i backup.  
  
###  <a name="support_limits"></a> Limitazioni del supporto  
 Di seguito sono riportate alcune limitazioni specifiche di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] Agent supporta solo backup del database: Completo e backup del Log.  L'automazione di backup di file non è supportata.  
  
-   Le operazioni di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] sono supportate attualmente tramite Transact-SQL. Il monitoraggio e la risoluzione dei problemi possono essere eseguiti utilizzando gli eventi estesi. Il supporto SMO e PowerShell è limitato alla configurazione delle impostazioni predefinite del periodo di memorizzazione e di archiviazione per un'istanza di SQL Server e al monitoraggio dello stato di backup e dell'integrità complessiva in base a criteri di gestione basata su criteri di SQL Server.  
  
-   I database di sistema non sono supportati.  
  
-   Il servizio di archiviazione BLOB Windows Azure è l'unica opzione di archiviazione di backup supportata. I backup su disco o su nastro non sono supportati.  
  
-   Attualmente, le dimensioni di file massime consentite per un BLOB di pagine nel servizio di archiviazione Windows Azure sono pari a 1 TB. Pertanto l'uso di file di backup maggiori di 1 TB avrà esito negativo. Per evitare questa situazione, in caso di database di grandi dimensioni è consigliabile utilizzare la compressione e verificare le dimensioni del file di backup prima di configurare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. È possibile eseguire tale verifica effettuando il backup in un disco locale o effettuando il backup manualmente nel servizio di archiviazione Windows Azure mediante l'istruzione Transact-SQL `BACKUP TO URL`. Per altre informazioni, vedere [SQL Server Backup to URL](sql-server-backup-to-url.md).  
  
-   Modelli di recupero: Sono supportati solo database impostati sul modello con registrazione completo o con registrazione minima delle operazioni Bulk.  I database impostati sul modello di recupero con registrazione minima non sono supportati.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] può presentare alcune limitazioni se configurato con altre tecnologie che supportano il backup, la disponibilità elevata o il ripristino di emergenza. Per altre informazioni, vedere [SQL Server Managed Backup to Windows Azure: Interoperabilità e coesistenza](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
|||  
|-|-|  
|**Descrizioni delle attività**|**Argomento**|  
|Attività di base come configurare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per un database, o configurare le impostazioni predefinite a livello di istanza, disabilitare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] a livello di database o di istanza, sospendere e riavviare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|[Backup gestito di SQL Server in Windows Azure - Impostazioni di archiviazione e di memorizzazione](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)|  
|**Esercitazione:** Istruzioni dettagliate per la configurazione e monitoraggio [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|[Configurazione del backup gestito di SQL Server in Windows Azure](enable-sql-server-managed-backup-to-microsoft-azure.md)|  
|**Esercitazione:** Istruzioni dettagliate per la configurazione e monitoraggio [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per i database nel gruppo di disponibilità.|[Configurazione del backup gestito di SQL Server in Windows Azure per i gruppi di disponibilità](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)|  
|Strumenti, concetti e attività correlati al monitoraggio di [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|[Monitorare il backup gestito di SQL Server in Windows Azure](sql-server-managed-backup-to-microsoft-azure.md)|  
|Strumenti e passaggi per risolvere i problemi relativi a [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|[Risoluzione dei problemi relativi al backup gestito di SQL Server in Windows Azure](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Backup e ripristino di SQL Server nel servizio Archiviazione BLOB di Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [Backup SQL Server nell'URL](sql-server-backup-to-url.md)   
 [SQL Server Managed Backup in Windows Azure: Interoperabilità e coesistenza](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)   
 [Risoluzione dei problemi relativi al backup gestito di SQL Server in Windows Azure](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)  
  
  
