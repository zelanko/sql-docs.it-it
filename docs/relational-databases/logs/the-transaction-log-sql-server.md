---
title: Log delle transazioni (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], about
- databases [SQL Server], transaction logs
- logs [SQL Server], transaction logs
ms.assetid: d7be5ac5-4c8e-4d0a-b114-939eb97dac4d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cd975ed830f9a0b705e516707d550697fbf34325
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287805"
---
# <a name="the-transaction-log-sql-server"></a>Log delle transazioni (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Ogni database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include un log delle transazioni in cui vengono registrate tutte le transazioni e le modifiche apportate dalle transazioni stesse al database.
  
Il log delle transazioni è un componente fondamentale del database. Se si verifica un errore di sistema, è necessario tale registro per ripristinare uno stato coerente del database. 

Per informazioni sull'architettura e sui meccanismi interni del log delle transazioni, vedere la [Guida sull'architettura e gestione del log delle transazioni di SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).

> [!WARNING] 
> Evitare di eliminare o spostare questo file di registro se non si conoscono a fondo le implicazioni di questa operazione. 

> [!TIP]
> I checkpoint rappresentano i punti ottimali noti da cui avviare l'applicazione dei log delle transazioni durante il ripristino del database. Per altre informazioni, vedere [Checkpoint di database (SQL Server)](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
## <a name="operations-supported-by-the-transaction-log"></a>Operazioni supportate dal log delle transazioni  
 Il log delle transazioni supporta le operazioni seguenti:  
  
-   Recupero di singole transazioni.  
-   Recupero di tutte le transazioni incomplete all'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 
-   Rollforward di una pagina, file, filegroup o database ripristinato fino al punto in cui si è verificato l'errore.  
-   Supporto della replica transazionale.  
-   Supporto delle soluzioni di ripristino di emergenza e disponibilità elevata: [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], mirroring del database e log shipping.

### <a name="individual-transaction-recovery"></a>Recupero di singole transazioni
Se un'applicazione esegue un'istruzione `ROLLBACK` oppure se [!INCLUDE[ssde_md](../../includes/ssde_md.md)] rileva un errore quale la perdita della comunicazione con un client, vengono usati i record del log per eseguire il rollback delle modifiche apportate da una transazione incompleta. 

### <a name="recovery-of-all-incomplete-transactions-when-ssnoversion-is-started"></a>Recupero di tutte le transazioni incomplete all'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
Se si verifica un errore in un server, è possibile che alcune modifiche ai database non siano state scritte dalla cache del buffer ai file di dati e che transazioni incomplete abbiano apportato modifiche al file di dati. All'avvio di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vengono recuperati i singoli database. Viene quindi eseguito il roll forward di tutte le modifiche registrate nel log che potrebbero non essere state scritte nei file di dati. A questo punto, per salvaguardare l'integrità del database, viene eseguito il rollback di tutte le transazioni incomplete rilevate nel log delle transazioni. Per altre informazioni, vedere [Panoramica del ripristino e del recupero (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery).

### <a name="rolling-a-restored-database-file-filegroup-or-page-forward-to-the-point-of-failure"></a>Rollforward di una pagina, un file, un filegroup o un database ripristinato fino al punto in cui si è verificato l'errore
Dopo un errore hardware o del disco che interessa i file del database, è possibile ripristinare il database fino al punto in cui si è verificato l'errore. Questo metodo prevede innanzitutto il ripristino dell'ultimo backup completo del database e dell'ultimo backup differenziale del database e quindi il ripristino della sequenza successiva dei backup del log delle transazioni fino al momento in cui si è verificato l'errore. 

Durante il ripristino di ogni backup del log, il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] riapplica tutte le modifiche registrate nel log per eseguire il roll forward di tutte le transazioni. Dopo il ripristino dell'ultimo backup del log, il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] usa le informazioni disponibili nel log per eseguire il rollback di tutte le transazioni non ancora completate al momento dell'esecuzione di tale backup. Per altre informazioni, vedere [Panoramica del ripristino e del recupero (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery).

### <a name="supporting-transactional-replication"></a>Supporto della replica transazionale
L'agente di lettura log esegue il monitoraggio del log delle transazioni di tutti i database configurati per la replica transazionale e copia le transazioni contrassegnate per la replica dal log delle transazioni al database di distribuzione. Per altre informazioni, vedere [Funzionamento della replica transazionale](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms151706(v=sql.105)).

### <a name="supporting-high-availability-and-disaster-recovery-solutions"></a>Supporto delle soluzioni di disponibilità elevata e ripristino di emergenza
Le soluzioni con server di standby, [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], mirroring del database e log shipping dipendono in modo significativo da log delle transazioni. 

In uno scenario **[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]** ogni aggiornamento apportato a un database (la replica primaria) viene immediatamente riprodotto in copie complete distinte del database (le repliche secondarie). La replica primaria invia immediatamente ogni record di log alle repliche secondarie. In questo modo, i record di log in ingresso vengono applicati ai database del gruppo di disponibilità, con una costante operazione di roll forward. Per altre informazioni, vedere [Istanze del cluster di failover AlwaysOn](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).

In uno **scenario di log shipping** il server primario invia il log delle transazioni attivo del database primario a una o più destinazioni. I singoli server secondari ripristinano il log nei relativi database secondari locali. Per altre informazioni, vedere [Informazioni sul log shipping](../../database-engine/log-shipping/about-log-shipping-sql-server.md). 

In uno **scenario di mirroring del database** tutti gli aggiornamenti di un database (del database principale) vengono immediatamente riprodotti in una copia distinta e completa del database, il database mirror. L'istanza del server principale invia immediatamente i singoli record di log all'istanza del server mirror, che applica i record ricevuti nel database mirror, eseguendone continuamente il roll forward. Per altre informazioni, vedere [Mirroring del database](../../database-engine/database-mirroring/database-mirroring-sql-server.md).

##  <a name="Characteristics"></a>Caratteristiche del log delle transazioni
Caratteristiche del log delle transazioni di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]: 
-  Il log delle transazioni viene implementato come file o set di file distinto nel database. La cache del log viene gestita separatamente dalla cache buffer per le pagine di dati e, pertanto, produce codice semplice, rapido e affidabile in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Per altre informazioni, vedere [Architettura fisica del log delle transazioni](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).

-  Il formato dei record e delle pagine del log non deve essere necessariamente conforme al formato delle pagine di dati.

-  Il log delle transazioni può essere implementato in diversi file, definiti in modo da espandersi automaticamente tramite l'impostazione del valore `FILEGROWTH` per il log. In questo modo è possibile ridurre le probabilità che si esaurisca lo spazio nel log delle transazioni e, nel contempo, alleggerire l'overhead amministrativo. Per altre informazioni, vedere [Opzioni per file e filegroup ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).

-  Il meccanismo che permette di riutilizzare lo spazio nei file di log è rapido e produce effetti minimi sulla velocità effettiva delle transazioni.

Per informazioni sull'architettura e sui meccanismi interni del log delle transazioni, vedere la [Guida sull'architettura e gestione del log delle transazioni di SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).

##  <a name="Truncation"></a> Troncamento del log delle transazioni  
Il troncamento del log libera spazio nel file di log per consentirne il riutilizzo da parte del log delle transazioni. È necessario troncare periodicamente il log delle transazioni per evitare il riempimento dello spazio allocato. Numerosi fattori possono posticipare il troncamento del log, pertanto è importante monitorare la dimensione del log. Ad alcune operazioni può essere applicata la registrazione minima per ridurre l'impatto sulle dimensioni del log delle transazioni.  
 
Il troncamento del log elimina i [file di log virtuali (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) inattivi dal log delle transazioni logico di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], liberando spazio nel log logico riusabile dal log delle transazioni fisico. Se un log delle transazioni non viene mai troncato, le sue dimensioni aumenteranno fino a occupare tutto lo spazio su disco allocato ai file di log fisici.  
  
Per evitare l'esaurimento dello spazio, il troncamento si verifica automaticamente dopo gli eventi riportati di seguito, a meno che l'operazione non sia stata posticipata per qualche motivo:  
  
- Nel modello di recupero con registrazione minima, dopo un checkpoint.  
- Nel modello di recupero con registrazione completa o nel modello di recupero con registrazione minima delle operazioni bulk, se si è verificato un checkpoint dal backup precedente, il troncamento si verifica dopo un backup del log (a meno che non si tratti di un backup del log di sola copia).  
  
 Per altre informazioni, vedere [Fattori che possono posticipare il troncamento del log](#FactorsThatDelayTruncation) più avanti in questo argomento.  
  
> [!NOTE]
> Il troncamento del log non riduce le dimensioni del file di log fisico. Per ridurre la dimensione fisica di un file di log fisico, è necessario ridurre il file di log. Per informazioni sulla compattazione del file di log fisico, vedere [Gestire le dimensioni del file di log delle transazioni](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md).  
> Tenere tuttavia presenti i [fattori che possono posticipare il troncamento del log](#FactorsThatDelayTruncation). Se dopo una compattazione del log è di nuovo necessario lo spazio di archiviazione, il log delle transazioni torna a crescere e durante tale crescita origina un overhead delle prestazioni.
  
##  <a name="FactorsThatDelayTruncation"></a> Factors that can delay log truncation  
 Quando i record del log rimangono attivi per molto tempo il troncamento viene posticipato e il log delle transazioni potrebbe riempirsi, come già accennato in precedenza.  
  
> [!IMPORTANT]
> Per informazioni su come agire quando il log delle transazioni è completo, vedere [Troubleshoot a Full Transaction Log &#40;SQL Server Error 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md).  
  
 Il troncamento del log può essere posticipato da diversi fattori. Per individuare l'eventuale condizione che impedisce il troncamento del log, eseguire una query sulle colonne **log_reuse_wait** e **log_reuse_wait_desc** della vista del catalogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md). Nella tabella seguente vengono descritti i valori di queste colonne.  
  
|Valore di log_reuse_wait|Valore di log_reuse_wait_desc|Descrizione|  
|----------------------------|----------------------------------|-----------------|  
|0|NOTHING|Attualmente sono disponibili uno o più [file di log virtuali (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) riusabili.|  
|1|CHECKPOINT|Non si è verificato alcun checkpoint dall'ultimo troncamento del log oppure l'inizio del log non è stato ancora spostato oltre un [file di log virtuale (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch). (Tutti i modelli di recupero)<br /><br /> Si tratta di una motivazione comune per il posticipo del troncamento del log. Per altre informazioni, vedere [Checkpoint di database &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).|  
|2|LOG_BACKUP|È necessario eseguire un backup del log prima del troncamento del log delle transazioni. (Solo modelli di recupero con registrazione completa e con registrazione minima delle operazioni bulk)<br /><br /> Quando il backup del log successivo viene completato, parte dello spazio del log potrebbe divenire riutilizzabile.|  
|3|ACTIVE_BACKUP_OR_RESTORE|È in esecuzione un processo di backup o ripristino dei dati (tutti i modelli di recupero).<br /><br /> Se il troncamento del log è impedito da un backup dei dati, l'annullamento del backup può risolvere il problema immediato.|  
|4|ACTIVE_TRANSACTION|Una transazione è attiva (tutti i modelli di recupero):<br /><br /> Una transazione con esecuzione prolungata potrebbe esistere all'inizio del backup del log. In questo caso, per liberare lo spazio potrebbe essere necessario un altro backup del log. Si noti che le transazioni con esecuzione prolungata impediscono il troncamento del log in tutti i modelli di recupero, incluso il modello di recupero con registrazione minima in cui il log delle transazioni viene generalmente troncato a ogni checkpoint automatico.<br /><br /> Viene posticipata una transazione. Una *transazione posticipata* è una transazione attiva ed efficace il cui ritorno allo stato precedente è bloccato a causa di alcune risorse non disponibili. Per informazioni sulle cause delle transazioni posticipate e su come modificarne lo stato, vedere [Transazioni posticipate &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).<br /> <br /> Anche le transazioni con esecuzione prolungata potrebbero riempire il log delle transazioni di tempdb. Tempdb viene usato in modo implicito dalle transazioni utente per gli oggetti interni, ad esempio tabelle di lavoro per l'ordinamento, file di lavoro per l'hashing, tabelle di lavoro di cursori e controllo delle versioni delle righe. Anche se la transazione utente include solo la lettura dei dati (query `SELECT`), durante le transazioni utente possono essere creati e usati oggetti interni. In questo modo, il log delle transazioni di tempdb potrebbe riempirsi.|  
|5|DATABASE_MIRRORING|Il mirroring del database è sospeso o in modalità a prestazioni elevate, il database mirror è notevolmente in ritardo rispetto al database principale. (Solo modello di recupero con registrazione completa)<br /><br /> Per altre informazioni, vedere [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|6|REPLICA|Durante le repliche transazionali, le transazioni significative per le pubblicazioni non sono ancora state recapitate al database di distribuzione. (Solo modello di recupero con registrazione completa)<br /><br /> Per informazioni sulla replica transazionale, vedere [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md).|  
|7|DATABASE_SNAPSHOT_CREATION|Viene creato uno snapshot del database. (Tutti i modelli di recupero)<br /><br /> Si tratta di una motivazione comune, e generalmente di breve durata, per il posticipo del troncamento del log.|  
|8|LOG_SCAN|È in corso un'analisi del log. (Tutti i modelli di recupero)<br /><br /> Si tratta di una motivazione comune, e generalmente di breve durata, per il posticipo del troncamento del log.|  
|9|AVAILABILITY_REPLICA|Una replica secondaria di un gruppo di disponibilità applica i record del log delle transazioni del database a un database secondario corrispondente. (Modello di recupero con registrazione completa)<br /><br /> Per altre informazioni, vedere [Panoramica di Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|10|-|Solo per uso interno|  
|11|-|Solo per uso interno|  
|12|-|Solo per uso interno|  
|13|OLDEST_PAGE|Se un database è configurato per l'uso dei checkpoint indiretti, la pagina meno recente del database potrebbe essere meno recente del [numero di sequenza del file di log (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) del checkpoint. In questo caso, la pagina meno recente può causare il posticipo del troncamento del log. (Tutti i modelli di recupero)<br /><br /> Per informazioni sui checkpoint indiretti, vedere [Database Checkpoints &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).|  
|14|OTHER_TRANSIENT|Questo valore non è attualmente utilizzato.|  
|16|XTP_CHECKPOINT|È necessario eseguire un checkpoint di OLTP in memoria. Per le tabelle ottimizzate per la memoria, viene effettuato un checkpoint automatico quando la dimensione del file di log delle transazioni supera 1,5 GB dopo l'ultimo checkpoint (include sia le tabelle basate su disco che quelle con ottimizzazione per la memoria)<br /> Per altre informazioni, vedere [Operazione su checkpoint per le tabelle con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/checkpoint-operation-for-memory-optimized-tables.md) e [processo di registrazione e Checkpoint per le tabelle con ottimizzazione per la memoria] (https://blogs.msdn.microsoft.com/sqlcat/2016/05/20/logging-and-checkpoint-process-for-memory-optimized-tables-2/)
  
##  <a name="MinimallyLogged"></a> Operazioni per cui è possibile eseguire la registrazione minima  
La*registrazione minima* implica la registrazione nel log delle transazioni delle sole informazioni necessarie per il recupero della transazione stesse senza il supporto del recupero temporizzato. In questo argomento vengono identificate le operazioni con registrazione minima nel [modello di recupero](../backup-restore/recovery-models-sql-server.md) con registrazione minima delle operazioni bulk nonché nel modello di recupero con registrazione minima, ad eccezione dei momenti in cui è in esecuzione un backup.  
  
> [!NOTE]
> La registrazione minima non è supportata dalle tabelle ottimizzate per la memoria.  
  
> [!NOTE]
> In base al [modello di recupero](../backup-restore/recovery-models-sql-server.md)con registrazione completa tutte le operazioni bulk vengono registrate per intero. È tuttavia possibile ridurre al minimo la registrazione per un set di operazioni bulk passando temporaneamente il database al modello di recupero con registrazione minima delle operazioni bulk per le operazioni bulk. La registrazione minima è più efficiente della registrazione completa e riduce la possibilità che un'operazione bulk su larga scala esaurisca lo spazio disponibile per il log delle transazioni durante una transazione bulk. Se tuttavia il database viene danneggiato o perso durante la registrazione minima, non è possibile recuperarlo fino al punto di errore.  
  
 Per le operazioni seguenti, con registrazione completa nel modello di recupero con registrazione completa, è prevista la registrazione minima nel modello di recupero con registrazione minima e in quello con registrazione minima delle operazioni bulk:  
  
-   Operazioni di importazione in blocco ([bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e [INSERT... SELECT](../../t-sql/statements/insert-transact-sql.md)). Per ulteriori informazioni sui casi in cui viene eseguita la registrazione minima di un'importazione bulk in una tabella, vedere [Prerequisites for Minimal Logging in Bulk Import](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
Quando la replica transazionale è abilitata, le operazioni `BULK INSERT` vengono registrate completamente, anche nel modello di recupero con registrazione minima delle operazioni bulk.  
  
-   Operazioni [SELECT INTO](../../t-sql/queries/select-into-clause-transact-sql.md).  
  
Quando la replica transazionale è abilitata, le operazioni `SELECT INTO` vengono registrate completamente, anche nel modello di recupero con registrazione minima delle operazioni bulk.  
  
-   Aggiornamenti parziali a tipi di dati di valori di grandi dimensioni eseguiti mediante la clausola `.WRITE` nell'istruzione [UPDATE](../../t-sql/queries/update-transact-sql.md) quando si inseriscono o si aggiungono nuovi dati. Si noti che la registrazione minima non viene utilizzata per l'aggiornamento di valori esistenti. Per altre informazioni sui tipi di dati per valori di grandi dimensioni, vedere [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
-   Istruzioni[WRITETEXT](../../t-sql/queries/writetext-transact-sql.md) e [UPDATETEXT](../../t-sql/queries/updatetext-transact-sql.md) durante l'inserimento o l'aggiunta di nuovi dati nelle colonne con tipo di dati **text**, **ntext**, e **image** . Si noti che la registrazione minima non viene utilizzata per l'aggiornamento di valori esistenti.  
  
    > [!WARNING]
    > Le istruzioni `WRITETEXT` e `UPDATETEXT` sono **deprecate**, evitare di usarle nelle nuove applicazioni.  
  
-   Se il database viene impostato sul modello di recupero con registrazione minima o con registrazione delle operazioni bulk, verrà eseguita la registrazione minima di alcune operazioni DDL sugli indici indipendentemente dal fatto che l'operazione venga eseguita online o offline. Le operazioni sugli indici con registrazione minima sono le seguenti:  
  
    -   Operazioni[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) (incluse le viste indicizzate).  
  
    -   Operazioni[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) REBUILD o DBCC DBREINDEX.  
  
        > [!WARNING]
        > L'istruzione `DBCC DBREINDEX` è **deprecata**: evitare di usarla nelle nuove applicazioni.  
  
    -   Ricompilazione del nuovo heap [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) (se pertinente). Durante un'operazione `DROP INDEX` per la deallocazione delle pagine di un indice viene eseguita **sempre** la registrazione completa.
  
##  <a name="RelatedTasks"></a> Related tasks  
**Gestione del log delle transazioni**  
  
-   [Gestione delle dimensioni del file di log delle transazioni](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)  
  
-   [Risolvere i problemi relativi a un log delle transazioni completo &#40;Errore di SQL Server 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
**Backup del log delle transazioni (modello di recupero con registrazione completa)**  
  
-   [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  

-   [Eseguire il backup del log delle transazioni quando il database è danneggiato (SQL Server)](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)

**Ripristino del log delle transazioni (modello di recupero con registrazione completa)**  
  
-   [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
[Architettura e gestione del log delle transazioni di SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)   
[Controllo della durabilità delle transazioni](../../relational-databases/logs/control-transaction-durability.md)   
[Prerequisiti per la registrazione minima nell'importazione bulk](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
[Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)     
[Panoramica del ripristino e del recupero (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery)      
[Checkpoint di database &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
[Visualizzare o modificare le proprietà di un database](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)   
[Modelli di recupero &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
[Backup di log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)    
[sys.dm_db_log_info & #40; Transact-SQL & #41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)  
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)    
  
  
