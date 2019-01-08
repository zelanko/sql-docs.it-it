---
title: sys.dm_db_xtp_checkpoint_files (Transact-SQL) | Microsoft Docs
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_files
- sys.dm_db_xtp_checkpoint_files_TSQL
- dm_db_xtp_checkpoint_files_TSQL
- sys.dm_db_xtp_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_files dynamic management view
ms.assetid: ac8e6333-7a9f-478a-b446-5602283e81c9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2c7f7f4296b3cbed025303f58cf07717db06c8e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510873"
---
# <a name="sysdmdbxtpcheckpointfiles-transact-sql"></a>sys.dm_db_xtp_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Visualizza informazioni sui file del checkpoint, incluse le dimensioni del file, la posizione fisica e l'ID transazione.  
  
> **NOTA:** Per il checkpoint corrente che non è chiusa, la colonna contenente gli stati di s`ys.dm_db_xtp_checkpoint_files` sarà UNDER CONSTRUCTION per i nuovi file. Un checkpoint viene chiuso automaticamente quando è presente l'aumento delle dimensioni del log delle transazioni sufficiente dall'ultimo checkpoint oppure se si esegue la `CHECKPOINT` comando ([CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)).  
  
 Un filegroup ottimizzato per la memoria utilizza internamente i file di solo accodamento per archiviare le righe inserite ed eliminate per le tabelle in memoria. Sono disponibili due tipi di file. Un file di dati contiene le righe inserite mentre un file differenziale contiene riferimenti alle righe eliminate. 
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] è notevolmente diverso rispetto alle versioni più recenti e viene illustrato più basso nell'argomento relativo alla [SQL Server 2014](#bkmk_2014).  
  
 Per altre informazioni, vedere [creazione e la gestione dell'archiviazione per gli oggetti ottimizzati per la memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md).  
  
##  <a name="bkmk_2016"></a> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e versioni successive  
 Nella tabella seguente vengono descritte le colonne per `sys.dm_db_xtp_checkpoint_files`, a partire **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]**.  
  
|Nome colonna|Tipo|Descrizione|  
|-----------------|----------|-----------------|  
|container_id|**int**|ID del contenitore (rappresentato come file con tipo FILESTREAM in sys.database_files) di cui fa parte il file di dati o il file differenziale. Join con file_id in [Sys. database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).|  
|container_guid|**uniqueidentifier**|GUID del contenitore, che il file radice, dati o differenziale fa parte di. Crea un join con file_guid nella tabella sys. database_files.|  
|checkpoint_file_id|**uniqueidentifier**|GUID del file del checkpoint.|  
|relative_file_path|**nvarchar(256)**|Percorso del file relativo contenitore a che è mappata.|  
|file_type|**smallint**|-1 per il livello gratuito<br /><br /> 0 per file di dati.<br /><br /> 1 per il file differenziale.<br /><br /> 2 per il file radice<br /><br /> 3 per il file di dati di grandi dimensioni|  
|file_type_desc|**nvarchar(60)**|File gratuito - All gestiti come disponibile sono disponibili per l'allocazione. File gratuiti possono variare nella dimensione in base alla esigenze previste dal sistema. La dimensione massima è di 1GB.<br /><br /> DATA - file di dati contengono righe che sono state inserite nelle tabelle ottimizzate per la memoria.<br /><br /> DELTA - file differenziali contengono i riferimenti alle righe nel file di dati che sono stati eliminati.<br /><br /> RADICE - file radice contengano metadati di sistema per gli oggetti con ottimizzazione per la memoria e compilati in modo nativo.<br /><br /> DATI di grandi dimensioni - file di grandi quantità di dati contengono valori inseriti nelle (colonne varchar e varbinary (max), nonché i segmenti di colonna che fanno parte di indici columnstore nelle tabelle ottimizzate per la memoria.|  
|internal_storage_slot|**int**|Indice del file nella matrice di archiviazione interna. NULL per la radice o per lo stato diverso da 1.|  
|checkpoint_pair_file_id|**uniqueidentifier**|I dati corrispondenti o il file differenziale. NULL per la radice.|  
|file_size_in_bytes|**bigint**|Dimensioni del file sul disco.|  
|file_size_used_in_bytes|**bigint**|Per le coppie di file del checkpoint ancora da popolare, questa colonna verrà aggiornata dopo il checkpoint successivo.|  
|logical_row_count|**bigint**|Per i dati, numero di righe inserite.<br /><br /> Delta, numero di righe eliminate dopo aver tenuto conto per la tabella di riepilogo.<br /><br /> Per la radice, NULL.|  
|state|**smallint**|0 - PRECREATI<br /><br /> 1 - IN FASE DI COSTRUZIONE<br /><br /> 2 - ACTIVE<br /><br /> 3 - MERGE TARGET<br /><br /> 8 - IN ATTESA DI TRONCAMENTO DEL LOG|  
|state_desc|**nvarchar(60)**|PRECREATED: un numero di file di checkpoint viene preallocato per ridurre al minimo o eliminare le attese di allocazione di nuovi file durante l'esecuzione delle transazioni. Questi file precreati possono variare nella dimensione, a seconda delle necessità stimate del carico di lavoro, ma non contengono dati. Si tratta di un overhead di archiviazione nei database con un filegroup MEMORY_OPTIMIZED_DATA.<br /><br /> UNDER CONSTRUCTION: questi file di checkpoint sono in fase di costruzione, ovvero che verranno popolati in base i record di log generati dal database e non fanno ancora parte di un checkpoint.<br /><br /> ACTIVE: contengono le righe inserite/eliminate dai precedenti checkpoint chiusi. Contengono il contenuto delle tabelle che area lette in memoria prima di applicare la parte attiva del log delle transazioni al riavvio del database. È probabile che le dimensioni di questi file del checkpoint da circa 2x delle dimensioni in memoria delle tabelle ottimizzate per la memoria, supponendo che l'operazione di unione è mantenersi aggiornato rispetto al carico di lavoro transazionale.<br /><br /> MERGE TARGET - la destinazione delle operazioni di unione: questi file di checkpoint archiviano le righe di dati consolidate dai file di origine identificate dai criteri di unione. Una volta installata l'operazione di unione, lo stato di MERGE TARGET diventa ACTIVE.<br /><br /> In attesa di troncamento del LOG - una volta che è stato installato l'unione e MERGE TARGET PCP fa parte del checkpoint durevole, la transizione di file checkpoint di merge source a questo stato. File in questo stato sono necessari per la correttezza operativa del database con tabelle ottimizzate per la memoria.  Ad esempio, per recuperare da un checkpoint durevole tornando indietro nel tempo.|  
|lower_bound_tsn|**bigint**|Limite inferiore della transazione nel file. null se non nello stato (1, 3).|  
|upper_bound_tsn|**bigint**|Limite superiore della transazione nel file. null se non nello stato (1, 3).|  
|begin_checkpoint_id|**bigint**|ID del punto di arresto iniziale.|  
|end_checkpoint_id|**bigint**|ID del punto di arresto finale.|  
|last_updated_checkpoint_id|**bigint**|ID dell'ultimo checkpoint che questo file aggiornato.|  
|encryption_status|**smallint**|0, 1, 2|  
|encryption_status_desc|**nvarchar(60)**|0 = &GT; UNENCRTPTED<br /><br /> 1 = &GT; CRITTOGRAFATO CON CHIAVE 1<br /><br /> 2 = &GT; CRITTOGRAFATO CON CHIAVE 2. Valido solo per i file attivi.|  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 Nella tabella seguente vengono descritte le colonne per `sys.dm_db_xtp_checkpoint_files`, per **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**.  
  
|Nome colonna|Tipo|Descrizione|  
|-----------------|----------|-----------------|  
|container_id|**int**|ID del contenitore (rappresentato come file con tipo FILESTREAM in sys.database_files) di cui fa parte il file di dati o il file differenziale. Join con file_id in [Sys. database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).|  
|container_guid|**uniqueidentifier**|GUID del contenitore di cui fa parte il file di dati o il file differenziale.|  
|checkpoint_file_id|**GUID**|ID del file di dati o differenziale.|  
|relative_file_path|**nvarchar(256)**|Percorso del file di dati o differenziale, relativo al percorso del contenitore.|  
|file_type|**tinyint**|0 per il file di dati.<br /><br /> 1 per il file differenziale.<br /><br /> NULL se la colonna contenente gli stati è impostata su 7.|  
|file_type_desc|**nvarchar(60)**|Il tipo di file: DATA_FILE, DELTA_FILE o NULL se la colonna contenente gli stati è impostata su 7.|  
|internal_storage_slot|**int**|Indice del file nella matrice di archiviazione interna. NULL se la colonna contenente gli stati è impostata su 2 o 3.|  
|checkpoint_pair_file_id|**uniqueidentifier**|File di dati o differenziale corrispondente.|  
|file_size_in_bytes|**bigint**|Dimensioni del file in uso. NULL se la colonna contenente gli stati è impostata su 5, 6 o 7.|  
|file_size_used_in_bytes|**bigint**|Dimensioni utilizzate del file in uso. NULL se la colonna contenente gli stati è impostata su 5, 6 o 7.<br /><br /> Per le coppie di file del checkpoint ancora da popolare, questa colonna verrà aggiornata dopo il checkpoint successivo.|  
|inserted_row_count|**bigint**|Numero di righe del file di dati.|  
|deleted_row_count|**bigint**|Numero di righe eliminate del file differenziale.|  
|drop_table_deleted_row_count|**bigint**|Numero di righe nei file di dati interessati dall'eliminazione di una tabella. Si applica ai file di dati quando la colonna contenente gli stati è uguale a 1.<br /><br /> Mostra i conteggi delle righe eliminate dalle tabelle eliminate. Le statistiche drop_table_deleted_row_count vengono compilate dopo il completamento del Garbage Collection in memoria delle righe delle tabelle eliminate e l'esecuzione di un checkpoint. Se si riavvia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prima che le statistiche delle tabelle eliminate vengono riflesse nella colonna, le statistiche verranno aggiornate durante il recupero. Il processo di recupero non carica le righe delle tabelle eliminate. Le statistiche delle tabelle eliminate vengono compilate durante la fase di caricamento e riportate nella colonna al termine del recupero.|  
|state|**int**|0 - PRECREATI<br /><br /> 1 - IN FASE DI COSTRUZIONE<br /><br /> 2 - ACTIVE<br /><br /> 3 - MERGE TARGET<br /><br /> 4 - MERGED SOURCE<br /><br /> 5 - OBBLIGATORIO FOR BACKUP/HA<br /><br /> 6: IN TRANSIZIONE VERSO PER LA RIMOZIONE DEFINITIVA<br /><br /> 7 - PER LA RIMOZIONE DEFINITIVA|  
|state_desc|**nvarchar(60)**|PRECREATED: un set ridotto di coppie di file dati e differenziali, noto anche come coppie di file checkpoint (CFP) viene mantenuto preallocato per ridurre o eliminare le attese di allocazione di nuovi file durante l'esecuzione delle transazioni. Hanno dimensioni intere, con file di dati di 128 MB e file differenziali di 8 MB, ma non contengono dati. Il numero di coppie di file di checkpoint è calcolato in base al numero di processori logici o utilità di pianificazione (uno per core, senza limiti) con un minimo di 8. Si tratta di un overhead di archiviazione fisso nei database con tabelle ottimizzate per la memoria.<br /><br /> UNDER CONSTRUCTION: Set di checkpoint che archiviano appena inserite ed eventualmente eliminate le righe di dati dall'ultimo checkpoint.<br /><br /> ACTIVE: contengono le righe inserite ed eliminate dai precedenti checkpoint chiusi. Queste coppie di file di checkpoint contengono tutte le righe inserite ed eliminate richieste prima dell'applicazione della parte attiva del log delle transazioni al riavvio del database. Le dimensioni di queste coppie di file di checkpoint saranno all'incirca il doppio delle dimensioni in memoria delle tabelle ottimizzate per la memoria, supponendo che l'operazione di unione sia corrente con il carico di lavoro transazionale.<br /><br /> MERGE TARGET - PCP archivia le righe di dati consolidati da CFP(s) identificate dai criteri di unione. Una volta installata l'operazione di unione, lo stato di MERGE TARGET diventa ACTIVE.<br /><br /> MERGED SOURCE: una volta l'operazione di unione è installato, il checkpoint di origine vengono contrassegnate come MERGED SOURCE. Si noti che l'analizzatore dei criteri di unione può identificare più operazioni di unione ma una coppia di file di checkpoint può partecipare solo a un'operazione di unione.<br /><br /> OBBLIGATORIO FOR BACKUP/HA: una volta installato l'unione e MERGE TARGET PCP fa parte del checkpoint durevole, l'origine dell'unione passano checkpoint a questo stato. Le coppie di file di checkpoint in questo stato sono necessarie per la correttezza operativa del database in cui sia inclusa una tabella ottimizzata per la memoria.  Ad esempio, per recuperare da un checkpoint durevole tornando indietro nel tempo. Una coppia di file di checkpoint può essere contrassegnata per il processo di Garbage Collection quando il punto di troncamento del log va oltre l'intervallo di transazioni.<br /><br /> IN TRANSITION TO TOMBSTONE: queste checkpoint non sono necessarie per il motore di OLTP In memoria e possono essere sottoposte al garbage collection. Questo stato indica che le coppie di file di checkpoint sono in attesa del thread in background per passare allo stato successivo, ovvero allo stato TOMBSTONE.<br /><br /> Per la rimozione definitiva - questi checkpoint sono in attesa di essere sottoposto a garbage collection dal garbage collector di filestream. ([sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md))|  
|lower_bound_tsn|**bigint**|Limite inferiore delle transazioni incluse nel file. Null se la colonna contenente gli stati è diversa da 2, 3 o 4.|  
|upper_bound_tsn|**bigint**|Limite superiore delle transazioni incluse nel file. Null se la colonna contenente gli stati è diversa da 2, 3 o 4.|  
|last_backup_page_count|**int**|Conteggio delle pagine logiche determinato nell'ultimo backup. Si applica quando la colonna contenente gli stati è impostata su 2, 3, 4 o 5. NULL se il conteggio delle pagine non è noto.|  
|delta_watermark_tsn|**int**|Transazione dell'ultimo checkpoint che ha scritto in questo file differenziale. Si tratta della filigrana per il file differenziale.|  
|last_checkpoint_recovery_lsn|**nvarchar(23)**|Numero di sequenza del file di log (LSN) di recupero dell'ultimo checkpoint per cui è ancora richiesto il file.|  
|tombstone_operation_lsn|**nvarchar(23)**|Il file verrà eliminato una volta che tombstone_operation_lsn non è più sincronizzato con l'LSN di troncamento del log.|  
|logical_deletion_log_block_id|**bigint**|Si applica solo alla stato 5.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione `VIEW DATABASE STATE` per il server.  
  
## <a name="use-cases"></a>Casi d'uso  
 È possibile stimare la memoria usata da OLTP In memoria come segue:  
  
```  
-- total storage used by In-Memory OLTP  
SELECT SUM (file_size_in_bytes)/(1024*1024) as file_size_in_MB  
FROM sys.dm_db_xtp_checkpoint_files  
```  
  
  
Per visualizzare i dettagli di utilizzo di spazio di archiviazione dal tipo di stato e i file di eseguire la query seguente:
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(file_size_in_bytes) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  

  
## <a name="see-also"></a>Vedere anche  
 [Memoria-con ottimizzazione per la tabella viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
