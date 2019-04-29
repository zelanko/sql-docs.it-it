---
title: Cosa&#39;s (motore di Database) | Microsoft Docs
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
ms.openlocfilehash: 0650d15ece36593139ae804f6535315eacbf9294
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843441"
---
# <a name="what39s-new-database-engine"></a>Cosa&#39;s (motore di Database)
  In quest'ultima versione di [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] sono stati apportati miglioramenti e introdotte nuove funzionalità per offrire ulteriori opportunità a progettisti, sviluppatori e amministratori che progettano, sviluppano e gestiscono sistemi di archiviazione dati e anche per migliorare la loro produttività. Di seguito sono indicate le aree del [!INCLUDE[ssDE](../includes/ssde-md.md)] in cui sono stati apportati miglioramenti.  
  
##  <a name="Feature"></a> Miglioramenti di funzionalità del motore di database  
  
###  <a name="MemoryOpt"></a> Tabelle ottimizzate per la memoria  
 OLTP in memoria è un motore di database ottimizzato per la memoria integrato nel motore di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. OLTP in memoria è ottimizzato per OLP. Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
 
  
###  <a name="DataFiles"></a> File di dati SQL Server in Microsoft Azure  
 [File di dati di SQL Server in Windows Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md) Abilita il supporto nativo per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] file archiviati come BLOB di Windows Azure del database. Questa funzionalità consente di creare un database in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in esecuzione in locale o in una macchina virtuale in Windows Azure con un percorso di archiviazione dedicato per i dati nel servizio di archiviazione BLOB di Windows Azure.  
  
  
###  <a name="AzureVM"></a> Ospitare un Database SQL Server in una finestra di macchina virtuale di Azure  
 Usare la [distribuire un Database di SQL Server a una macchina virtuale di Windows Azure](https://msdn.microsoft.com/library/dn195938\(v=sql.120\).aspx) guidata consente di ospitare un database da un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in una macchina virtuale di Windows Azure.  
  
  
###  <a name="Backup"></a> Backup e ripristino migliorate  
 In [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] sono incluse le seguenti funzionalità avanzate per il backup e ripristino di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   **Backup di SQL Server nell'URL**  
  
     Il backup di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nell'URL è stato introdotto in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP1 CU2 e supportato solo da [!INCLUDE[tsql](../includes/tsql-md.md)], PowerShell e SMO. In [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] è possibile utilizzare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per il backup nel servizio di archiviazione BLOB di Windows Azure o per il ripristino da questo servizio. La nuova opzione è disponibile sia per le attività di backup sia per i piani di manutenzione. Per altre informazioni, vedere [con attività di Backup in SQL Server Management Studio](../relational-databases/backup-restore/sql-server-backup-to-url.md#BackupTaskSSMS), [SQL Server Backup in URL Using Maintenance Plan Wizard](../relational-databases/backup-restore/sql-server-backup-to-url.md#MaintenanceWiz), e [il ripristino da archiviazione di Azure tramite SQL Server Management Studio](../relational-databases/backup-restore/sql-server-backup-to-url.md#RestoreSSMS).  
  
-   **Backup gestito di SQL Server in Windows Azure**  
  
     Basato sul backup di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nell'URL, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è un servizio fornito da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per gestire e pianificare i backup del database e del log. In questa versione è supportato solo il backup nel servizio di archiviazione Windows Azure. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] può essere configurato sia a livello di database sia a livello di istanza consentendo il controllo granulare a livello di database e l'automazione a livello di istanza. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] può essere configurata nella [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] istanze in esecuzione in locale e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] istanze in esecuzione in macchine virtuali di Azure. È consigliato per le istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in esecuzione in Macchine virtuali di Windows Azure. Per altre informazioni, vedere [SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
-   **Crittografia per backup**  
  
     È ora possibile scegliere di crittografare il file di backup durante l'operazione di backup.  La crittografia per backup supporta vari algoritmi di crittografia, tra cui AES 128, AES 192, AES 256 e Triple DES. È necessario utilizzare un certificato o una chiave asimmetrica per eseguire la crittografia durante il backup. Per altre informazioni, vedere [Crittografia dei backup](../relational-databases/backup-restore/backup-encryption.md).  
  
  
###  <a name="CE"></a> Nuovo Design per la stima della cardinalità  
 La logica di stima della cardinalità, denominata strumento di stima della cardinalità, è stata riprogettata in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] per migliorare la qualità dei piani di query e, di conseguenza, per ottimizzare le prestazioni delle query. Nel nuovo strumento di stima della cardinalità sono incorporati presupposti e algoritmi maggiormente adatti ai i carichi di lavoro di data warehouse e alle soluzioni OLTP più recenti. Lo strumento è basato sulla ricerca approfondita della stima della cardinalità sui carichi di lavoro più recenti e sulle conoscenze relative al miglioramento della stima della cardinalità di SQL Server acquisite nel corso degli ultimi 15 anni. I commenti e i suggerimenti dei clienti indicano che sebbene la maggior parte delle query registrerà un miglioramento o rimarrà invariata a seguito della modifica, una percentuale minima potrebbe registrare una regressione rispetto allo strumento di stima della cardinalità precedente. Per indicazioni per il test e ottimizzazione delle prestazioni, vedere [stima di cardinalità &#40;SQL Server&#41;](../relational-databases/performance/cardinality-estimation-sql-server.md).  
   
  
###  <a name="Durability"></a> Durabilità ritardata  
 In [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] è stata introdotta la possibilità di ridurre la latenza designando alcune o tutte le transazioni come durevoli posticipate. Tramite una transazione durevole posticipata viene restituito il controllo al client prima che il record del log delle transazioni venga scritto nel disco. La durabilità può essere controllata a livello di database, di COMMIT o a livello di blocco atomico.  
  
 Per altre informazioni, vedere l'argomento [controllo della durabilità delle transazioni](../relational-databases/logs/control-transaction-durability.md).  
  
  
###  <a name="AlwaysOn"></a> Miglioramenti AlwaysOn  
 In [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] sono stati apportati i seguenti miglioramenti per le istanze del cluster di failover AlwaysOn e i Gruppi di disponibilità AlwaysOn:  
  
-   La procedura guidata Aggiungi replica Azure semplifica la creazione di soluzioni ibride per i Gruppi di disponibilità AlwaysOn. Per altre informazioni, vedere [utilizzare la procedura guidata Aggiungi Replica Azure &#40;SQL Server&#41;](availability-groups/windows/use-the-add-azure-replica-wizard-sql-server.md).  
  
-   Il numero massimo di repliche secondarie è passato da 4 a 8.  
  
-   Quando vengono disconnesse dalla replica primaria o durante la perdita di quorum del cluster, le repliche secondarie leggibili rimangono ora disponibili per i carichi di lavoro di lettura.  
  
-   Le istanze del cluster di failover possono ora utilizzare i volumi condivisi cluster come dischi condivisi cluster. Per altre informazioni, vedere [Cluster di istanze di Failover AlwaysOn](../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
-   Una nuova funzione di sistema [Sys. fn_hadr_is_primary_replica](/sql/relational-databases/system-functions/sys-fn-hadr-is-primary-replica-transact-sql)e una nuova DMV [sys.dm_io_cluster_valid_path_names](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql), è disponibile.  
  
-   Le DMV seguenti sono state migliorate e ora vengono restituite informazioni di infrastruttura di classificazione file: [hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql), [sys.dm_hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql), e [DM hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql).  
  
  
###  <a name="OIR"></a> Indicizzazione e cambio della partizione  
 Le singole partizioni di tabelle partizionate possono ora essere ricompilate. Per altre informazioni, vedere [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
   
  
###  <a name="Lock"></a> Gestione della priorità di blocco delle operazioni Online  
 L'opzione `ONLINE = ON` contiene ora un'opzione `WAIT_AT_LOW_PRIORITY` che consente di specificare l'intervallo di attesa dei blocchi necessari per un processo di ricompilazione. L'opzione `WAIT_AT_LOW_PRIORITY` consente inoltre di configurare la fine dei processi di blocco correlati a tale istruzione di ricompilazione. Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql) e [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql). Risoluzione dei problemi relativi a informazioni sui nuovi tipi di stato di blocco è disponibile nel [DM tran_locks &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql) e [DM os_wait_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql).  
 
  
###  <a name="CCI"></a> Indici columnstore  
 Per gli indici columnstore sono disponibili le seguenti nuove funzionalità:  
  
-   **Indici columnstore cluster**  
  
     Usare un indice columnstore cluster per migliorare le prestazioni di compressione dei dati e delle query per i carichi di lavoro di data warehousing che eseguono principalmente caricamenti bulk e query di sola lettura. Poiché l'indice columnstore cluster è aggiornabile, il carico di lavoro può eseguire molte operazioni di inserimento, aggiornamento ed eliminazione. Per altre informazioni, vedere [descrizione degli indici Columnstore](../relational-databases/indexes/columnstore-indexes-described.md) e [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md).  
  
-   **SHOWPLAN**  
  
     SHOWPLAN consente di visualizzare informazioni sugli indici columnstore. Il **Actualexecutionmode** e **ActualExecutionMode** proprietà sono possibili due valori: **Batch** oppure **riga**.  Il **archiviazione** proprietà è possibili due valori: **RowStore** e **ColumnStore**.  
  
-   **Compressione dell'archivio dati**  
  
     ALTER INDEX ... REBUILD include una nuova opzione di compressione di dati COLUMNSTORE_ARCHIVE che comprime ulteriormente le partizioni specificate di un indice columnstore. Può essere utilizzata per l'archiviazione o in altre situazioni in cui sono richieste dimensioni di archiviazione dati inferiori ed è possibile concedere più tempo per l'archiviazione e il recupero. Per altre informazioni, vedere [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
   
  
###  <a name="Buffer"></a> Estensione del Pool di buffer  
 Il [Buffer Pool Extension](configure-windows/buffer-pool-extension.md) consente l'integrazione di unità SSD (unità SSD) come estensione volatile memory (NvRAM) per il [!INCLUDE[ssDE](../includes/ssde-md.md)] pool per migliorare significativamente la velocità effettiva dei / o di buffer.  
   
  
###  <a name="Stats"></a> Statistiche incrementali  
 CREATE STATISTICS e le istruzioni statistiche correlate permettono ora di creare statistiche per partizione utilizzando l'opzione INCREMENTAL. Le istruzioni correlate consentono o creano report di statistiche incrementali. La sintassi interessata include UPDATE STATISTICS, sp_createstats, CREATE INDEX, ALTER INDEX, ALTER DATABASE SET opzioni, DATABASEPROPERTYEX, sys. Databases e Sys. Stats. Per altre informazioni, vedere [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
  
###  <a name="RG"></a> Miglioramenti di Resource Governor per il controllo dei / o fisico  
 Resource Governor consente di specificare i limiti sulla quantità di CPU, I/O fisico e memoria che possono essere utilizzati dalle richieste dell'applicazione in ingresso in un pool di risorse. In [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] è possibile utilizzare le nuove impostazioni MIN_IOPS_PER_VOLUME e MAX_IOPS_PER_VOLUME per controllare gli I/O fisici per i thread di utente per un determinato pool di risorse. Per altre informazioni, vedere [Pool di risorse di Resource Governor](../relational-databases/resource-governor/resource-governor-resource-pool.md) e [crea POOL di risorse &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql).  
  
 Tramite l'impostazione MAX_OUTSTANDING_IO_PER_VOLUME di ALTER RESOURCE GOVENOR vengono impostate le operazioni di I/O in sospeso massime per ogni volume di disco. Questa impostazione può essere utilizzata per ottimizzare la governance delle risorse di I/O rispetto alle caratteristiche di I/O di un volume di disco e per limitare il numero di I/O emessi al limite dell'istanza di SQL Server. Per altre informazioni, vedere [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql).  
  
  
###  <a name="OnlineEvent"></a> Classe di evento online Index Operation  
 Il report di stato per la classe di evento operazione sugli indici online presenta ora due nuove colonne di dati: **PartitionId** e **PartitionNumber**. Per altre informazioni, vedere [Progress Report: Classe di evento online Index Operation](../relational-databases/event-classes/progress-report-online-index-operation-event-class.md).  
  
  
###  <a name="Compat"></a> Livello di compatibilità del database  
 Il livello di compatibilità 90 non è valido in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. Per altre informazioni, vedere [livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
##  <a name="TSQL"></a> Miglioramenti di Transact-SQL  
  
### <a name="inline-specification-of-clustered-and-nonclustered"></a>Specifica inline di CLUSTERED e NONCLUSTERED  
 La specifica inline degli indici `CLUSTERED` e `NONCLUSTERED` è ora consentita per le tabelle basate su disco. La creazione di una tabella con indici inline equivale a rilasciare una tabella create seguita dalle istruzioni `CREATE INDEX` corrispondenti. Le condizioni di filtro e le colonne incluse non sono supportate con gli indici inline.  
  
### <a name="select--into"></a>SELEZIONA... INTO  
 L'istruzione `SELECT ... INTO` è stata migliorata e ora può essere eseguita in parallelo. Il livello di compatibilità del database deve essere impostato almeno su 110.  
  
### <a name="includetsqlincludestsql-mdmd-enhancements-for-in-memory-oltp"></a>Miglioramenti a [!INCLUDE[tsql](../includes/tsql-md.md)] per OLTP in memoria  
 Per informazioni sul [!INCLUDE[tsql](../includes/tsql-md.md)] modifiche per supportare OLTP In memoria, vedere [supporto Transact-SQL per OLTP In memoria](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md).  
  
  
##  <a name="SystemTable"></a> Miglioramenti alle viste di sistema  
  
### <a name="sysxmlindexes"></a>sys.xml_indexes  
 [Sys. xml_indexes &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-xml-indexes-transact-sql) include 3 nuove colonne: `xml_index_type`, `xml_index_type_description`, e `path_id`.  
  
### <a name="sysdmexecqueryprofiles"></a>sys.dm_exec_query_profiles  
 [DM exec_query_profiles &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql) consente di monitorare lo stato di avanzamento query in tempo reale mentre una query è in esecuzione.  
  
### <a name="syscolumnstorerowgroups"></a>sys.column_store_row_groups  
 [column_store_row_groups &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql) fornisce informazioni sull'indice columnstore cluster in base a ogni segmento che aiutano l'amministratore a prendere decisioni di gestione di sistema.  
  
### <a name="sysdatabases"></a>sys.databases  
 [Sys. Databases &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) include 3 nuove colonne: `is_auto_create_stats_incremental_on`, `is_query_store_on`, e `resource_pool_id`.  
  
### <a name="system-view-enhancements-for-in-memory-oltp"></a>Miglioramenti alle viste di sistema per OLTP in memoria  
 Per informazioni sui miglioramenti alle viste di sistema per supportare OLTP In memoria, vedere [viste di sistema, Stored procedure, viste a gestione dinamica e i tipi di attesa per OLTP In memoria](../../2014/database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md).  
   
  
##  <a name="Security"></a> Miglioramenti della sicurezza  
  
### <a name="connect-any-database-permission"></a>Autorizzazione CONNECT ANY DATABASE  
 Nuova autorizzazione a livello di server. Concedere l'autorizzazione **CONNECT ANY DATABASE** a un account di accesso che deve connettersi a tutti i database attualmente esistenti e ai nuovi database che potrebbero essere creati in futuro. Non concede alcuna autorizzazione nei database oltre la connessione. Associ **SELECT ALL USER SECURABLES** oppure `VIEW SERVER STATE` per consentire un processo di controllo visualizzare tutti i dati o tutti gli stati di database nell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
### <a name="impersonate-any-login-permission"></a>Autorizzazione IMPERSONATE ANY LOGIN  
 Nuova autorizzazione a livello di server. Quando viene concessa, consente a un processo di livello intermedio di rappresentare l'account dei client a cui ci si connette, quando si connette ai database. Quando viene negata, è possibile che a un account di accesso con privilegi elevati venga impedito di rappresentare altri account di accesso. Ad esempio, è possibile che a un account di accesso con autorizzazione **CONTROL SERVER** venga impedito di rappresentare altri account di accesso.  
  
### <a name="select-all-user-securables-permission"></a>Autorizzazioni SELECT ALL USER SECURABLES  
 Nuova autorizzazione a livello di server. Quando viene concessa, un account di accesso, ad esempio un revisore, può visualizzare i dati in tutti i database a cui l'utente può connettersi.  
  
  
##  <a name="Deployment"></a> Miglioramenti della distribuzione  
### <a name="azure-vm"></a>Macchina virtuale di Azure
[Distribuire un Database di SQL Server a una macchina virtuale di Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) consente la distribuzione di un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] database a una VM Windows Azure.  

### <a name="refs"></a>ReFS
È ora supportata la distribuzione di database in ReFS.   
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
   
