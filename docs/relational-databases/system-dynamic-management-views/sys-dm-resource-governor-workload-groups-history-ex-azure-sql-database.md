---
title: Sys.dm_resource_governor_workload_groups_history_ex (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_workload_groups_history_ex_TSQL
- sys.dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_resource_governor_workload_groups_history_ex dynamic management view
author: joesackmsft
ms.author: josack
manager: craigg
ms.openlocfilehash: 1a2123c3da5945fb42184631e43fe27d83972375
ms.sourcegitcommit: 32dce314bb66c03043a93ccf6e972af455349377
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2019
ms.locfileid: "66744019"
---
# <a name="sysdmresourcegovernorworkloadgroupshistoryex-azure-sql-database"></a>sys.dm_resource_governor_workload_groups_history_ex (database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Snapshot restituisce intervalli di 15 secondi per ultimi 30 minuti di resource pool stats per un Database SQL di Azure.
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**pool_id**| INT |ID del pool di risorse. Non ammette i valori Null.|
|**group_id**| INT |ID del gruppo del carico di lavoro. Non ammette i valori Null.|
|**name**| nvarchar(256) |Nome del gruppo del carico di lavoro. Non ammette i valori Null.|
|**snapshot_time**| datetime |Data e ora dello snapshot di statistiche gruppo di risorse creato.|
|**duration_ms**| INT |Intervallo di tempo tra snapshot corrente e quella precedente.|
|**active_worker_count**| INT |Ruoli di lavoro totali nello snapshot corrente.|
|**active_request_count**| INT |Conteggio corrente richieste. Non ammette i valori Null.|
|**active_session_count**| INT |Totale sessioni attive nello snapshot corrente.|
|**total_request_count**| BIGINT |Conteggio cumulativo delle richieste completate nel gruppo del carico di lavoro. Non ammette i valori Null.|
|**delta_request_count**| INT |Conteggio delle richieste completate nel gruppo di carico di lavoro dall'ultimo snapshot. Non ammette i valori Null.|
|**total_cpu_usage_ms**| BIGINT |Utilizzo cumulativo della CPU, in millisecondi, da parte di questo gruppo del carico di lavoro. Non ammette i valori Null.|
|**delta_cpu_usage_ms**| INT |Utilizzo della CPU in millisecondi, dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_cpu_usage_preemptive_ms**| INT |Le chiamate a win32 preemptive disciplinano dal gruppo di risorse della CPU SQL, dall'ultimo snapshot.|
|**delta_reads_reduced_memgrant_count**| INT |Il conteggio delle concessioni di memoria che ha raggiunto il limite di dimensioni massimo per la query dall'ultimo snapshot. Non ammette i valori Null.|
|**reads_throttled**| INT |Numero totale di operazioni di lettura limitate.|
|**delta_reads_queued**| INT |Il totale di lettura accodati dall'ultimo snapshot. Ammette i valori Null. Null se il gruppo di risorse non è governato per il / o.|
|**delta_reads_issued**| INT |Il totale di lettura dall'ultimo snapshot. Ammette i valori Null. Null se il gruppo di risorse non è governato per il / o.|
|**delta_reads_completed**| INT |Il totale di lettura completati dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_read_bytes**| BIGINT |Il numero totale di byte letti dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_read_stall_ms**| INT |Tempo totale (in millisecondi) tra l'arrivo dei / o lettura e completamento dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_read_stall_queued_ms**| INT |Tempo totale (in millisecondi) tra lettura arrivi dei / o e il problema dall'ultimo snapshot. Ammette i valori Null. Null se il gruppo di risorse non è governato per il / o. Delta_read_stall_queued_ms diverso da zero indica che sono interessato da gruppo di risorse i/o.|
|**delta_writes_queued**| INT |Il totale di scrittura accodati dall'ultimo snapshot. Ammette i valori Null. Null se il gruppo di risorse non è governato per il / o.|
|**delta_writes_issued**| INT |Il totale di scrittura generati dall'ultimo snapshot. Ammette i valori Null. Null se il gruppo di risorse non è governato per il / o.|
|**delta_writes_completed**| INT |Totale scrittura completati dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_writes_bytes**| BIGINT |Numero totale di byte scritti dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_write_stall_ms**| INT |Tempo totale (in millisecondi) tra l'arrivo dei / o di scrittura e completamento dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_background_writes**| INT |I numero totale di scritture eseguite dalle attività in background dall'ultimo snapshot.|
|**delta_background_write_bytes**| BIGINT |Le dimensioni del numero totale di scrittura eseguite dalle attività in background dall'ultimo snapshot, in byte.|
|**delta_log_bytes_used**| BIGINT |Utilizzata dall'ultimo snapshot in byte del log.|
|**delta_log_temp_db_bytes_used**| BIGINT |Log di tempdb utilizzato dall'ultimo snapshot in byte.|
|**delta_query_optimizations**| BIGINT |Numero di ottimizzazioni di query in questo gruppo di carico di lavoro dall'ultimo snapshot. Non ammette i valori Null.|
|**delta_suboptimal_plan_generations**| BIGINT |Numero di generazioni di piani non ottimali che si sono verificati in questo gruppo di carico di lavoro a causa di un utilizzo elevato di memoria dall'ultimo snapshot. Non ammette i valori Null.
|**max_memory_grant_kb**| BIGINT |Concessione di memoria massima per il gruppo di nell'articolo.|
|**max_request_cpu_msec**| BIGINT |Limite massimo di utilizzo della CPU, in millisecondi, per una singola richiesta. Non ammette i valori Null.|
|**max_concurrent_request**| INT |Impostazione corrente per il numero massimo di richieste simultanee. Non ammette i valori Null.|
|**max_io**| INT |Limite massimo dei / o per il gruppo.|
|**max_global_io**| INT |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.
|**max_queued_io**| INT |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.|
|**max_log_rate_kb**| BIGINT |Frequenza massima del log (kg-byte / sec) a livello di gruppo di risorse.|
|**max_session**| INT |Limite di sessioni per il gruppo.|
|**max_worker**| INT |Limite per il gruppo di lavoro.|
|||

## <a name="permissions"></a>Permissions

In questa vista richiede l'autorizzazione VIEW SERVER STATE.

## <a name="remarks"></a>Note

Gli utenti possono accedere a questa vista a gestione dinamica per il monitoraggio quasi in tempo reale di consumo di risorse per il pool di carico di lavoro utente nonché pool interno del sistema dell'istanza di Database SQL di Azure.

> [!IMPORTANT]
> La maggior parte dei dati rilevati da questa DMV è destinato all'utilizzo interno ed è soggetta a modifiche.

## <a name="examples"></a>Esempi

L'esempio seguente restituisce i dati di velocità massima del log e l'utilizzo in ogni snapshot dal pool di utenti:

```sql
SELECT snapshot_time,
       name,
       max_log_rate_kb,
       delta_log_bytes_used
FROM sys.dm_resource_governor_workload_groups_history_ex
WHERE name LIKE 'User%'
ORDER BY snapshot_time DESC;
```

## <a name="see-also"></a>Vedere anche

- [Governance delle velocità di log di traduzione](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Limiti delle risorse DTU del pool elastico](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [Limiti delle risorse vCore del pool elastico](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
