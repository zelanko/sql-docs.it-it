---
title: sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governor
- sys.resource_governor_TSQL
- resource_governor
- resource_governor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 130c4f9c38e5eb7ee47d31377a224c5b602b5b35
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412943"
---
# <a name="sysdmresourcegovernorresourcepoolshistoryex-transact-sql"></a>sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Snapshot restituisce intervalli di 15 secondi per ultimi 30 minuti di resource pool stats per un Database SQL di Azure.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**pool_id**|INT|ID del pool di risorse. Non ammette i valori Null.
|**name**|sysname|Nome del pool di risorse. Non ammette i valori Null.|
|**snapshot_time**|datetime2|Valore DateTime dello snapshot resource pool stats creato|
|**duration_ms**|INT|Intervallo di tempo tra snapshot corrente e quella precedente|
|**statistics_start_time**|datetime2|Ora di reimpostazione delle statistiche per questo pool. Non ammette i valori Null.|
|**active_session_count**|INT|Totale sessioni attive nello snapshot corrente|
|**active_worker_count**|INT|Ruoli di lavoro totali nello snapshot corrente|
|**delta_cpu_usage_ms**|INT|Utilizzo della CPU in millisecondi, dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_cpu_usage_preemptive_ms**|INT|Le chiamate a win32 preemptive disciplinano dal gruppo di risorse della CPU SQL, dall'ultimo snapshot|
|**used_data_space_kb**|BIGINT|Spazio totale usato nei database utente associati al pool di utenti|
|**allocated_disk_space_kb**|BIGINT|Dimensioni dei database utente a file di dati totali in associato con pool di utenti|
|**target_memory_kb**|BIGINT|Quantità di memoria di destinazione, in kilobyte, che il pool di risorse sta cercando di ottenere. Si basa sulle impostazioni correnti e sullo stato del server. Non ammette i valori Null.|
|**used_memory_kb**|BIGINT|Quantità di memoria utilizzata, in kilobyte, per il pool di risorse. Non ammette i valori Null.|
|**cache_memory_kb**|BIGINT|Utilizzo corrente della memoria cache totale in kilobyte. Non ammette i valori Null.|
|**compile_memory_kb**|BIGINT|Utilizzo corrente della memoria prelevata totale in kilobyte (KB). La maggioranza dell'utilizzo avviene per la compilazione e l'ottimizzazione, ma può includere anche altri utenti della memoria. Non ammette i valori Null.|
|**active_memgrant_count**|BIGINT|Il conteggio corrente delle concessioni di memoria. Non ammette i valori Null.|
|**active_memgrant_kb**|BIGINT|La somma, in kilobyte (KB), delle concessioni correnti di memoria. Non ammette i valori Null.|
|**used_memgrant_kb**|BIGINT|Il totale corrente della memoria usata (prelevata) dalle concessioni di memoria. Non ammette i valori Null.|
|**delta_memgrant_timeout_count**|INT|conteggio di memoria concedere i timeout nel pool di risorse in questo periodo. Non ammette i valori Null.|
|**delta_memgrant_waiter_count**|INT|Il conteggio delle query attualmente in sospeso nelle concessioni di memoria. Non ammette i valori Null.|
|**delta_out_of_memory_count**|INT|Il numero delle allocazioni di memoria non riuscite nel pool dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_read_io_queued**|INT|Il totale di lettura accodati dall'ultimo snapshot. Ammette i valori Null. Null se il pool di risorse non è governato per l'I/O.|
|**delta_read_io_issued**|INT|Il totale di lettura dall'ultimo snapshot. Ammette i valori Null. Null se il pool di risorse non è governato per l'I/O.|
|**delta_read_io_completed**|INT|Il totale di lettura completati dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_read_io_throttled**|INT|Il totale di lettura limitati rispetto allo snapshot. Ammette i valori Null. Null se il pool di risorse non è governato per l'I/O.|
|**delta_read_bytes**|BIGINT|Il numero totale di byte letti dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_read_io_stall_ms**|INT|Tempo totale (in millisecondi) tra l'arrivo dei / o lettura e completamento dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_read_io_stall_queued_ms**|INT|Tempo totale (in millisecondi) tra lettura arrivi dei / o e il problema dall'ultimo snapshot. Ammette i valori Null. Null se il pool di risorse non è governato per l'I/O. Delta_read_io_stall_queued_ms diverso da zero indica che sono interessato da gruppo di risorse i/o.|
|**delta_write_io_queued**|INT|Il totale di scrittura accodati dall'ultimo snapshot. Ammette i valori Null. Null se il pool di risorse non è governato per l'I/O.|
|**delta_write_io_issued**|INT|Il totale di scrittura generati dall'ultimo snapshot. Ammette i valori Null. Null se il pool di risorse non è governato per l'I/O.|
|**delta_write_io_completed**|INT|Totale scrittura completati dall'ultimo snapshot. Non ammette i valori Null|
|**delta_write_io_throttled**|INT|L'operazione di scrittura totale IOs limitate dall'ultimo snapshot. Non ammette i valori Null|
|**delta_write_bytes**|BIGINT|Numero totale di byte scritti dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_write_io_stall_ms**|INT|Tempo totale (in millisecondi) tra l'arrivo dei / o di scrittura e completamento dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_write_io_stall_queued_ms**|INT|Tempo totale (in millisecondi) tra l'arrivo dei / o di scrittura e problema dall'ultimo snapshot. Ammette i valori Null. Null se il pool di risorse non è governato per l'I/O.|
|**delta_io_issue_delay_ms**|INT|Tempo totale (in millisecondi) tra la generazione pianificata e quella effettiva dei / o dall'ultimo snapshot. Ammette i valori Null. Null se il pool di risorse non è governato per l'I/O.|
|**max_iops_per_volume**|INT|Numero massimo dei / o al secondo (IOPS) per ogni impostazione del volume del disco per questo Pool. Ammette i valori Null. Null se il pool di risorse non è governato per l'I/O.|
|**max_memory_kb**|BIGINT|Quantità massima di memoria, in kilobyte, disponibile per il pool di risorse. Si basa sulle impostazioni correnti e sullo stato del server. Non ammette i valori Null.
|**max_log_rate_kb**|BIGINT|Frequenza massima del log (kg-byte / sec) a livello di pool di risorse.|
|**max_data_space_kb**|BIGINT|Impostazione per questo pool elastico nel kilobyte del limite di archiviazione massima del pool elastico.|
|**max_session**|INT|Limite di sessioni per pool|
|**max_worker**|INT|Limite di ruolo di lavoro per il pool|
|**min_cpu_percent**|INT|Configurazione corrente della larghezza di banda media garantita della CPU per tutte le richieste nel pool di risorse, in caso di contesa di CPU. Non ammette i valori Null.|
|**max_cpu_percent**|INT|Configurazione corrente per la larghezza di banda media massima della CPU concessa per tutte le richieste nel pool di risorse, in caso di contesa di CPU. Non ammette i valori Null.|
|**cap_cpu_percent**|INT|Limite di utilizzo massimo della larghezza di banda della CPU concesso per tutte le richieste nel pool di risorse. Limita il livello massimo della larghezza di banda della CPU al livello specificato. L'intervallo consentito per il valore è compreso tra 1 e 100. Non ammette i valori Null.|
|**min_vcores**|Decimal(5,2)|Configurazione corrente della larghezza di banda media garantita della CPU per tutte le richieste nel pool di risorse, in caso di contesa di CPU.  Nelle unità di Vcore|
|**max_vcores**|Decimal(5,2)|Configurazione corrente per la larghezza di banda media massima della CPU concessa per tutte le richieste nel pool di risorse, in caso di contesa di CPU.  Nell'unità del numero di Vcore|
|**cap_vcores**|Decimal(5,2)|Limite di utilizzo massimo della larghezza di banda della CPU concesso per tutte le richieste nel pool di risorse.  Nell'unità sul numero di Vcore|
|**instance_cpu_count**|INT|Numero di CPU configurata per l'istanza|
|**instance_cpu_percent|Decimal(5,2)|Percentuale CPU configurate per l'istanza|
|**instance_vcores**|Decimal(5,2)|Numero di Vcore configurati per l'istanza|
|**delta_log_bytes_used**|Decimal(5,2)|Generazione di log totali (in byte) a livello di pool dall'ultimo snapshot|
|**avg_login_rate_percent**|Decimal(5,2)|Numero di account di accesso dall'ultimo snapshot, confrontato con limite di account di accesso|
|**delta_vcores_used**|Decimal(5,2)|Utilizzo in numero di Vcore dall'ultimo snapshot del calcolo.|
|**cap_vcores_used_percent**|Decimal(5,2)|Utilizzo di calcolo medio in percentuale del limite del pool.|
|**instance_vcores_used_percent**|Decimal(5,2)|Utilizzo di calcolo medio in percentuale del limite dell'istanza SQL.|
|**avg_data_io_percent**|Decimal(5,2)|Utilizzo dei / o medio espresso in percentuale sulla base del limite del pool.|
|**avg_log_write_percent**|Decimal(5,2)|Medio scrittura utilizzo delle risorse in percentuale del limite del pool.|
|**avg_storage_percent**|Decimal(5,2)|Utilizzo di spazio di archiviazione medio espresso in percentuale del limite di archiviazione del pool.|
|**avg_allocated_storage_percent**|Decimal(5,2)|La percentuale di dati spazio allocato per tutti i database nel pool elastico. Questa è la percentuale di spazio per i dati allocato alla dimensione massima dei dati per il pool elastico. Per altre informazioni, vedere: Gestione dello spazio file nel database SQL|
|**max_worker_percent**|Decimal(5,2)|Massimi ruoli di lavoro simultanei (richieste) espresso in percentuale sulla base del limite del pool.|
|**max_session_percent**|Decimal(5,2)|Numero massimo di sessioni simultaneo espresso in percentuale sulla base del limite del pool.|
|||

## <a name="permissions"></a>Permissions

In questa vista richiede l'autorizzazione VIEW SERVER STATE.

## <a name="remarks"></a>Note

Gli utenti possono accedere a questa vista a gestione dinamica per il monitoraggio quasi in tempo reale di consumo di risorse per il pool di carico di lavoro utente nonché pool interno del sistema dell'istanza di Database SQL di Azure.

> [!IMPORTANT]
> La maggior parte dei dati rilevati da questa DMV è destinato all'utilizzo interno ed è soggetta a modifiche.

## <a name="examples"></a>Esempi

L'esempio seguente restituisce i dati di velocità massima del log e l'utilizzo in ogni snapshot dal pool di utenti  

```sql
select snapshot_time, name, max_log_rate_kb, delta_log_bytes_used from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

L'esempio seguente restituisce informazioni simili come Sys. elastic_pool_resource_stats senza la necessità di connettersi al database Master logico

```sql
select snapshot_time, name, cap_vcores_used_percent,
  avg_data_io_percent,  
  avg_log_write_percent,
  avg_storage_percent,
  avg_allocated_storage_percent,
  max_data_space_kb,
  max_worker_percent,
  max_session_percent
    from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

## <a name="see-also"></a>Vedere anche

- [Governance delle velocità di log di traduzione](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Limiti delle risorse DTU del pool elastico](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [Limiti delle risorse vCore del pool elastico](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
