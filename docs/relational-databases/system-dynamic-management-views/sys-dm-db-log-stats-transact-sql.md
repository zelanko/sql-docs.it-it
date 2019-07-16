---
title: sys.dm_db_log_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_log_stats_TSQL
- sys.dm_db_log_stats
- sys.dm_db_log_stats_TSQL
- dm_db_log_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_stats dynamic management function
ms.assetid: ''
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b23eea391c7de1f02eacec7f8c8625211dfeea3d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004831"
---
# <a name="sysdmdblogstats-transact-sql"></a>sys.dm_db_log_stats (Transact-SQL)   
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Restituisce attributi a livello di riepiloghi e informazioni sui file di log delle transazioni di database. Usare queste informazioni per il monitoraggio e diagnostica dell'integrità del log delle transazioni.   
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>Argomenti  

*database_id* | NULL | **Predefinito**

ID del database. `database_id` è `int`. Gli input validi sono il numero di ID di un database, `NULL`, o `DEFAULT`. Il valore predefinito è `NULL`. `NULL` e `DEFAULT` sono valori equivalenti nel contesto del database corrente.  
La funzione predefinita [DB_ID](../../t-sql/functions/db-id-transact-sql.md) può essere specificato. Quando si usa `DB_ID` senza specificare un nome di database, il livello di compatibilità del database corrente deve essere maggiore o uguale a 90.

  
## <a name="tables-returned"></a>Tabelle restituite  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |ID database |  
|recovery_model |**nvarchar(60)**   |   Modello di recupero del database. I valori possibili includono: <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   Inizio corrente [sequenza numero di log (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) nel log delle transazioni.|  
|log_end_lsn    |**nvarchar(24)**   |   [sequenza numero di log (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) dell'ultimo record di log nel log delle transazioni.|  
|current_vlf_sequence_number    |**bigint** |   Corrente [file di log virtuale (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) numero di sequenza durante la fase di esecuzione.|  
|current_vlf_size_mb    |**float**  |   Corrente [file di log virtuale (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) dimensione in MB.|   
|total_vlf_count    |**bigint** |   Numero totale di [file di log virtuali (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) nel log delle transazioni. |  
|total_log_size_mb  |**float**  |   Dimensioni del log delle transazioni totale in MB. |  
|active_vlf_count   |**bigint** |   Numero totale di attivo [file di log virtuali (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) nel log delle transazioni.|  
|active_log_size_mb |**float**  |   Dimensioni log delle transazioni attivo totale in MB.|  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   Motivo di arresto del troncamento di log. Il valore è uguale a `log_reuse_wait_desc` della colonna della `sys.databases`.  (Per ulteriori informazioni sul significato di questi valori, vedere [Log delle transazioni](../../relational-databases/logs/the-transaction-log-sql-server.md)). <br />I valori possibili includono: <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />REPLICATION<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />ALTRO TEMPORANEO |  
|log_backup_time    |**datetime**   |   Transaction log ora ultimo backup.|   
|log_backup_lsn |**nvarchar(24)**   |   Ultimo backup del log delle transazioni [sequenza numero di log (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|   
|log_since_last_log_backup_mb   |**float**  |   Dimensione del log in MB dall'ultimo backup del log delle transazioni [sequenza numero di log (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|log_checkpoint_lsn |**nvarchar(24)**   |   Ultimo checkpoint [sequenza numero di log (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|log_since_last_checkpoint_mb   |**float**  |   Dimensione del log in MB dall'ultimo checkpoint [sequenza numero di log (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|log_recovery_lsn   |**nvarchar(24)**   |   Recupero [sequenza numero di log (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) del database. Se `log_recovery_lsn` si verifica prima del LSN, checkpoint `log_recovery_lsn` è la transazione attiva meno recente LSN, in caso contrario `log_recovery_lsn` è del LSN checkpoint.|  
|log_recovery_size_mb   |**float**  |   Dimensione del log in MB dal recupero del log [sequenza numero di log (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).|  
|recovery_vlf_count |**bigint** |   Numero totale di [file di log virtuali (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) da recuperare, se si è verificato il riavvio del server o del failover. |  


## <a name="remarks"></a>Note
Quando si esegue `sys.dm_db_log_stats` su un database che partecipa a un gruppo di disponibilità come replica secondaria, verrà restituito solo un subset dei campi descritti in precedenza.  Attualmente, solo `database_id`, `recovery_model`, e `log_backup_time` verrà restituito se viene eseguita in un database secondario.   

## <a name="permissions"></a>Permissions  
Richiede il `VIEW DATABASE STATE` autorizzazione nel database.   
  
## <a name="examples"></a>Esempi  

### <a name="a-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-high-number-of-vlfs"></a>R. Determinare i database in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza con un numero elevato di file di log virtuali   
La query seguente restituisce i database con più di 100 file di log virtuali nei file di log. Un numero elevato di file di log virtuali può influire sull'ora di avvio, ripristino e ripristino di database.

```sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-transaction-log-backups-older-than-4-hours"></a>B. Determinare i database in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza con i backup del log delle transazioni anteriori a 4 ore   
La query seguente identifica le ultime volte in backup log per i database nell'istanza.

```sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>Vedere anche  
[Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Viste a gestione dinamica relative ai database &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info & #40; Transact-SQL & #41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
  
