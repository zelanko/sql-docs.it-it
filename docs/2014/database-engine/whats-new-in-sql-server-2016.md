---
title: Novità di&#39;(motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5e51cda61bb44d1f143cab50901276b927cca73a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "70176075"
---
# <a name="what39s-new-database-engine"></a>Novità di&#39;(motore di database)
  In quest'ultima versione di [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] sono stati apportati miglioramenti e introdotte nuove funzionalità per offrire ulteriori opportunità a progettisti, sviluppatori e amministratori che progettano, sviluppano e gestiscono sistemi di archiviazione dati e anche per migliorare la loro produttività. Di seguito sono indicate le aree del [!INCLUDE[ssDE](../includes/ssde-md.md)] in cui sono stati apportati miglioramenti.  
  
##  <a name="database-engine-feature-enhancements"></a><a name="Feature"></a>Miglioramenti della funzionalità motore di database  
  
###  <a name="memory-optimized-tables"></a><a name="MemoryOpt"></a>Tabelle con ottimizzazione per la memoria  
 OLTP in memoria è un motore di database ottimizzato per la memoria integrato nel motore di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. OLTP in memoria è ottimizzato per OLP. Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
 
  
###  <a name="sql-server-data-files-in-azure"></a><a name="DataFiles"></a>SQL Server file di dati in Azure  
 [SQL Server file di dati in Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md) consente il supporto [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nativo per i file di database archiviati come BLOB di Azure. Questa funzionalità consente di creare un database in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esecuzione in locale o in una macchina virtuale in Azure con un percorso di archiviazione dedicato per i dati nell'archivio BLOB di Azure.  
  
  
###  <a name="host-a-sql-server-database-in-an-azure-virtual-machine"></a><a name="AzureVM"></a>Ospitare un database di SQL Server in una macchina virtuale di Azure  
 Usare la procedura guidata [Distribuisci un database di SQL Server in una macchina virtuale di Azure](https://msdn.microsoft.com/library/dn195938\(v=sql.120\).aspx) per ospitare un database [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da un'istanza di in una macchina virtuale di Azure.  
  
  
###  <a name="backup-and-restore-enhancements"></a><a name="Backup"></a>Miglioramenti di backup e ripristino  
 In [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] sono incluse le seguenti funzionalità avanzate per il backup e ripristino di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   **Backup di SQL Server nell'URL**  
  
     Il backup di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nell'URL è stato introdotto in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP1 CU2 e supportato solo da [!INCLUDE[tsql](../includes/tsql-md.md)], PowerShell e SMO. In [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] è possibile usare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per eseguire il backup o il ripristino dal servizio di archiviazione BLOB di Azure. La nuova opzione è disponibile sia per le attività di backup sia per i piani di manutenzione. Per altre informazioni, vedere [uso dell'attività di backup in SQL Server Management Studio](../relational-databases/backup-restore/sql-server-backup-to-url.md#BackupTaskSSMS), [SQL Server backup nell'URL tramite la creazione guidata piano di manutenzione](../relational-databases/backup-restore/sql-server-backup-to-url.md#MaintenanceWiz)e [ripristino da archiviazione di Azure con SQL Server Management Studio](../relational-databases/backup-restore/sql-server-backup-to-url.md#RestoreSSMS).  
  
-   **Backup gestito di SQL Server in Azure**  
  
     Basato sul backup di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nell'URL, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è un servizio fornito da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per gestire e pianificare i backup del database e del log. In questa versione è supportato solo il backup in archiviazione di Azure. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] può essere configurato sia a livello di database sia a livello di istanza consentendo il controllo granulare a livello di database e l'automazione a livello di istanza. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]può essere configurato in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] istanze di in esecuzione in locale [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e in istanze in esecuzione in macchine virtuali di Azure. È consigliabile per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] le istanze in esecuzione in macchine virtuali di Azure. Per altre informazioni, vedere [SQL Server backup gestito in Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
-   **Crittografia per i backup**  
  
     È ora possibile scegliere di crittografare il file di backup durante l'operazione di backup.  La crittografia per backup supporta vari algoritmi di crittografia, tra cui AES 128, AES 192, AES 256 e Triple DES. È necessario utilizzare un certificato o una chiave asimmetrica per eseguire la crittografia durante il backup. Per altre informazioni, vedere [Crittografia del backup](../relational-databases/backup-restore/backup-encryption.md).  
  
  
###  <a name="new-design-for-cardinality-estimation"></a><a name="CE"></a>Nuova progettazione per la stima della cardinalità  
 La logica di stima della cardinalità, denominata strumento di stima della cardinalità, è stata riprogettata in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] per migliorare la qualità dei piani di query e, di conseguenza, per ottimizzare le prestazioni delle query. Nel nuovo strumento di stima della cardinalità sono incorporati presupposti e algoritmi maggiormente adatti ai i carichi di lavoro di data warehouse e alle soluzioni OLTP più recenti. Lo strumento è basato sulla ricerca approfondita della stima della cardinalità sui carichi di lavoro più recenti e sulle conoscenze relative al miglioramento della stima della cardinalità di SQL Server acquisite nel corso degli ultimi 15 anni. I commenti e i suggerimenti dei clienti indicano che sebbene la maggior parte delle query registrerà un miglioramento o rimarrà invariata a seguito della modifica, una percentuale minima potrebbe registrare una regressione rispetto allo strumento di stima della cardinalità precedente. Per le indicazioni di ottimizzazione e test delle prestazioni, vedere la pagina relativa alla [stima della cardinalità &#40;SQL Server&#41;](../relational-databases/performance/cardinality-estimation-sql-server.md).  
   
  
###  <a name="delayed-durability"></a><a name="Durability"></a>Durabilità ritardata  
 In [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] è stata introdotta la possibilità di ridurre la latenza designando alcune o tutte le transazioni come durevoli posticipate. Tramite una transazione durevole posticipata viene restituito il controllo al client prima che il record del log delle transazioni venga scritto nel disco. La durabilità può essere controllata a livello di database, di COMMIT o a livello di blocco atomico.  
  
 Per ulteriori informazioni, vedere l'argomento [controllo della durabilità delle transazioni](../relational-databases/logs/control-transaction-durability.md).  
  
  
###  <a name="alwayson-enhancements"></a><a name="AlwaysOn"></a>Miglioramenti di AlwaysOn  
 In [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] sono stati apportati i seguenti miglioramenti per le istanze del cluster di failover AlwaysOn e i Gruppi di disponibilità AlwaysOn:  
  
-   La procedura guidata Aggiungi replica Azure semplifica la creazione di soluzioni ibride per i Gruppi di disponibilità AlwaysOn. Per ulteriori informazioni, vedere [utilizzare la procedura guidata Aggiungi replica Azure &#40;SQL Server&#41;](availability-groups/windows/use-the-add-azure-replica-wizard-sql-server.md).  
  
-   Il numero massimo di repliche secondarie è passato da 4 a 8.  
  
-   Quando vengono disconnesse dalla replica primaria o durante la perdita di quorum del cluster, le repliche secondarie leggibili rimangono ora disponibili per i carichi di lavoro di lettura.  
  
-   Le istanze del cluster di failover possono ora utilizzare i volumi condivisi cluster come dischi condivisi cluster. Per ulteriori informazioni, vedere [Always on istanze del cluster di failover](../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
-   È disponibile una nuova funzione di sistema, [sys. fn_hadr_is_primary_replica](/sql/relational-databases/system-functions/sys-fn-hadr-is-primary-replica-transact-sql)e una nuova DMV, [sys. dm_io_cluster_valid_path_names](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql).  
  
-   I seguenti DMV sono stati migliorati e ora restituiscono informazioni FCI: [sys. dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql), [sys. dm_hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)e [sys. dm_hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql).  
  
  
###  <a name="partition-switching-and-indexing"></a><a name="OIR"></a>Cambio di partizione e indicizzazione  
 Le singole partizioni di tabelle partizionate possono ora essere ricompilate. Per altre informazioni, vedere [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
   
  
###  <a name="managing-the-lock-priority-of-online-operations"></a><a name="Lock"></a>Gestione della priorità di blocco delle operazioni online  
 L'opzione `ONLINE = ON` contiene ora un'opzione `WAIT_AT_LOW_PRIORITY` che consente di specificare l'intervallo di attesa dei blocchi necessari per un processo di ricompilazione. L'opzione `WAIT_AT_LOW_PRIORITY` consente inoltre di configurare la fine dei processi di blocco correlati a tale istruzione di ricompilazione. Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql) e [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql). Le informazioni sulla risoluzione dei problemi relativi ai nuovi tipi di Stati di blocco sono disponibili in [sys. dm_tran_locks &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql) e [sys. dm_os_wait_stats &#40;transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql).  
 
  
###  <a name="columnstore-indexes"></a><a name="CCI"></a>Indici columnstore  
 Per gli indici columnstore sono disponibili le seguenti nuove funzionalità:  
  
-   **Indici columnstore cluster**  
  
     Usare un indice columnstore cluster per migliorare le prestazioni di compressione dei dati e delle query per i carichi di lavoro di data warehousing che eseguono principalmente caricamenti bulk e query di sola lettura. Poiché l'indice columnstore cluster è aggiornabile, il carico di lavoro può eseguire molte operazioni di inserimento, aggiornamento ed eliminazione. Per altre informazioni, vedere [indici columnstore descritti](../relational-databases/indexes/columnstore-indexes-described.md) e [uso degli indici columnstore cluster](../relational-databases/indexes/indexes.md).  
  
-   **SHOWPLAN**  
  
     SHOWPLAN consente di visualizzare informazioni sugli indici columnstore. Le proprietà **per** e **estimatedexecutionmode** hanno due valori possibili: **batch** o **Row**.  La proprietà **storage** ha due valori possibili: **RowStore** e **columnstore**.  
  
-   **Compressione dati dell'archivio**  
  
     ALTER INDEX... Rebuild include una nuova opzione di compressione dei dati COLUMNSTORE_ARCHIVE che comprime ulteriormente le partizioni specificate di un indice columnstore. Può essere utilizzata per l'archiviazione o in altre situazioni in cui sono richieste dimensioni di archiviazione dati inferiori ed è possibile concedere più tempo per l'archiviazione e il recupero. Per altre informazioni, vedere [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
   
  
###  <a name="buffer-pool-extension"></a><a name="Buffer"></a>Estensione pool di buffer  
 L' [estensione del pool di buffer](configure-windows/buffer-pool-extension.md) offre l'integrazione perfetta di unità SSD (Solid-State Drive) come estensione NvRAM (NonVolatile Random Access Memory) [!INCLUDE[ssDE](../includes/ssde-md.md)] nel pool di buffer per migliorare significativamente la velocità effettiva di I/O.  
   
  
###  <a name="incremental-statistics"></a><a name="Stats"></a>Statistiche incrementali  
 CREATE STATISTICS e le istruzioni statistiche correlate permettono ora di creare statistiche per partizione utilizzando l'opzione INCREMENTAL. Le istruzioni correlate consentono o creano report di statistiche incrementali. La sintassi interessata include UPDATE STATISTICs, sp_createstats, CREATE INDEX, ALTER INDEX, ALTER DATABASE SET options, DATABASEPROPERTYEX, sys. databases e sys. stats. Per ulteriori informazioni, vedere [create statistics &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-statistics-transact-sql).  
  
  
###  <a name="resource-governor-enhancements-for-physical-io-control"></a><a name="RG"></a>Miglioramenti di Resource Governor per il controllo di IO fisico  
 Resource Governor consente di specificare i limiti sulla quantità di CPU, I/O fisico e memoria che possono essere utilizzati dalle richieste dell'applicazione in ingresso in un pool di risorse. In [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] è possibile utilizzare le nuove impostazioni MIN_IOPS_PER_VOLUME e MAX_IOPS_PER_VOLUME per controllare gli I/O fisici per i thread di utente per un determinato pool di risorse. Per altre informazioni, vedere [Resource Governor pool di risorse](../relational-databases/resource-governor/resource-governor-resource-pool.md) e [creare un pool di risorse &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-resource-pool-transact-sql).  
  
 Tramite l'impostazione MAX_OUTSTANDING_IO_PER_VOLUME di ALTER RESOURCE GOVENOR vengono impostate le operazioni di I/O in sospeso massime per ogni volume di disco. Questa impostazione può essere utilizzata per ottimizzare la governance delle risorse di I/O rispetto alle caratteristiche di I/O di un volume di disco e per limitare il numero di I/O emessi al limite dell'istanza di SQL Server. Per altre informazioni, vedere [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql).  
  
  
###  <a name="online-index-operation-event-class"></a><a name="OnlineEvent"></a>Classe di evento online Index Operation  
 Il report sullo stato di avanzamento per la classe di evento online Index Operation dispone ora di due nuove colonne di dati: **PartitionID** e **partitionNumber**. Per ulteriori informazioni, vedere [classe di evento progress report: Online Index Operation](../relational-databases/event-classes/progress-report-online-index-operation-event-class.md).  
  
  
###  <a name="database-compatibility-level"></a><a name="Compat"></a>Livello di compatibilità del database  
 Il livello di compatibilità 90 non è valido in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. Per ulteriori informazioni, vedere [livello di compatibilità di ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
##  <a name="transact-sql-enhancements"></a><a name="TSQL"></a>Miglioramenti di Transact-SQL  
  
### <a name="inline-specification-of-clustered-and-nonclustered"></a>Specifica inline di CLUSTERED e NONCLUSTERED  
 La specifica inline degli indici `CLUSTERED` e `NONCLUSTERED` è ora consentita per le tabelle basate su disco. La creazione di una tabella con indici inline equivale a rilasciare una tabella create seguita dalle istruzioni `CREATE INDEX` corrispondenti. Le condizioni di filtro e le colonne incluse non sono supportate con gli indici inline.  
  
### <a name="select--into"></a>SELEZIONA... IN  
 L'istruzione `SELECT ... INTO` è stata migliorata e ora può essere eseguita in parallelo. Il livello di compatibilità del database deve essere impostato almeno su 110.  
  
### <a name="tsql-enhancements-for-in-memory-oltp"></a>Miglioramenti a [!INCLUDE[tsql](../includes/tsql-md.md)] per OLTP in memoria  
 Per informazioni sulle modifiche [!INCLUDE[tsql](../includes/tsql-md.md)] per il supporto di OLTP in memoria, vedere [supporto di Transact-SQL per OLTP in memoria](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md).  
  
  
##  <a name="system-view-enhancements"></a><a name="SystemTable"></a>Miglioramenti delle visualizzazioni di sistema  
  
### <a name="sysxml_indexes"></a>sys.xml_indexes  
 [sys. xml_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-xml-indexes-transact-sql) include 3 nuove colonne: `xml_index_type`, `xml_index_type_description`e `path_id`.  
  
### <a name="sysdm_exec_query_profiles"></a>sys.dm_exec_query_profiles  
 [sys. dm_exec_query_profiles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql) monitora lo stato di avanzamento delle query in tempo reale durante l'esecuzione di una query.  
  
### <a name="syscolumn_store_row_groups"></a>sys.column_store_row_groups  
 [sys. column_store_row_groups &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql) fornisce informazioni sugli indici columnstore cluster in base a ogni segmento, per consentire all'amministratore di prendere decisioni di gestione del sistema.  
  
### <a name="sysdatabases"></a>sys.databases  
 [sys. databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) include 3 nuove `is_auto_create_stats_incremental_on`colonne `is_query_store_on`:, `resource_pool_id`e.  
  
### <a name="system-view-enhancements-for-in-memory-oltp"></a>Miglioramenti alle viste di sistema per OLTP in memoria  
 Per informazioni sui miglioramenti apportati alla visualizzazione di sistema per supportare OLTP in memoria, vedere [viste di sistema, stored procedure, DMV e tipi di attesa per OLTP in memoria](../../2014/database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md).  
   
  
##  <a name="security-enhancements"></a><a name="Security"></a> Miglioramenti della sicurezza  
  
### <a name="connect-any-database-permission"></a>Autorizzazione CONNECT ANY DATABASE  
 Nuova autorizzazione a livello di server. Concedere l'autorizzazione **CONNECT ANY DATABASE** a un account di accesso che deve connettersi a tutti i database attualmente esistenti e ai nuovi database che potrebbero essere creati in futuro. Non concede alcuna autorizzazione nei database oltre la connessione. Combinare con **Seleziona tutte le entità a protezione diretta dell'utente** o `VIEW SERVER STATE` per consentire a un processo di controllo di visualizzare tutti i dati o tutti gli [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Stati del database nell'istanza di.  
  
### <a name="impersonate-any-login-permission"></a>Autorizzazione IMPERSONATE ANY LOGIN  
 Nuova autorizzazione a livello di server. Quando viene concessa, consente a un processo di livello intermedio di rappresentare l'account dei client a cui ci si connette, quando si connette ai database. Quando viene negata, è possibile che a un account di accesso con privilegi elevati venga impedito di rappresentare altri account di accesso. Ad esempio, è possibile che a un account di accesso con autorizzazione **CONTROL SERVER** venga impedito di rappresentare altri account di accesso.  
  
### <a name="select-all-user-securables-permission"></a>Autorizzazioni SELECT ALL USER SECURABLES  
 Nuova autorizzazione a livello di server. Quando viene concessa, un account di accesso, ad esempio un revisore, può visualizzare i dati in tutti i database a cui l'utente può connettersi.  
  
  
##  <a name="deployment-enhancements"></a><a name="Deployment"></a>Miglioramenti della distribuzione  
### <a name="azure-vm"></a>Macchina virtuale di Azure
[Distribuire un database di SQL Server in una macchina virtuale Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) consente la distribuzione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] di un database in una VM di Azure.  

### <a name="refs"></a>ReFS
È ora supportata la distribuzione di database su ReFS.   
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
   
