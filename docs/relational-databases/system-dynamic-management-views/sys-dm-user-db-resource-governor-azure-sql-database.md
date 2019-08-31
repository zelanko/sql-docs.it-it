---
title: sys. dm _user_db_resource_governance (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governance
- sys.resource_governance_TSQL
- resource_governance
- resource_governance_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governance catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: ea07ba28efc4ac50fdeef04bb1b3643c359ead28
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176259"
---
# <a name="sysdm_user_db_resource_governance-transact-sql"></a>sys. dm _user_db_resource_governance (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Restituisce le impostazioni di capacità e configurazione della governance delle risorse per un database di database SQL di Azure.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_id**|int|ID del database, univoco all'interno di un server di database SQL di Azure.|
|**logical_database_guid**|uniqueidentifier|GUID logico per il database utente e rimane nel corso del ciclo di vita di un database utente.  Rinominare o impostare un database su un SLO diverso non modificherà il GUID. |
|**physical_database_guid**|uniqueidentifier|GUID fisico per un database utente che rimane per tutta la durata dell'istanza fisica del database utente. Se si imposta su un SLO diverso, la colonna verrà modificata.|
|**server_name**|nvarchar|Nome del server logico.|
|**database_name**|nvarchar|Nome del database logico.|
|**slo_name**|nvarchar|Obiettivo del livello di servizio e generazione di hardware.|
|**dtu_limit**|int|Limite DTU del database (NULL per vCore).|
|**cpu_limit**|int|limite vCore del database (NULL per i database DTU).|
|**min_cpu**|tinyint|Percentuale minima della CPU che può essere usata dal carico di lavoro dell'utente.|
|**max_cpu**|tinyint|Percentuale massima della CPU che può essere usata dal carico di lavoro dell'utente.|
|**cap_cpu**|tinyint|Limite della percentuale di CPU per i gruppi del carico di lavoro dell'utente.|
|**min_cores**|smallint|Numero di CPU utilizzate da SQL.|
|**max_dop**|smallint|Massimo grado di parallelismo utilizzato dal carico di lavoro dell'utente.|
|**min_memory**|int|Percentuale minima della memoria che può essere usata dal carico di lavoro dell'utente.|
|**max_memory**|int|Percentuale massima della memoria che può essere usata dal carico di lavoro dell'utente.|
|**max_sessions**|int|Limite della sessione per il gruppo utenti.|
|**max_memory_grant**|int|Concessione di memoria massima per ogni query nel carico di lavoro dell'utente, espressa in percentuale.|
|**max_db_memory**|int|Limite massimo di memoria per il pool di buffer per il carico di lavoro database utente|
|**govern_background_io**|bit|Indica se le Scritture in background vengono addebitate al gruppo di utenti.|
|**min_db_max_size_in_mb**|bigint|Dimensioni minime massime del file di database, in MB.|
|**max_db_max_size_in_mb**|bigint|Numero massimo di file di database, in MB.|
|**default_db_max_size_in_mb**|bigint|Dimensioni massime predefinite del file di database, in MB.|
|**db_file_growth_in_mb**|bigint|Aumento predefinito del file di database di Azure, in MB.|
|**initial_db_file_size_in_mb**|bigint|Dimensioni predefinite del file di database, in MB.|
|**log_size_in_mb**|bigint|Dimensioni del file di log predefinite, in MB.|
|**instance_cap_cpu**|int|Limite della CPU a livello di istanza.|
|**instance_max_log_rate**|bigint|Limite della velocità di generazione del log a livello di istanza, espresso in byte al secondo.|
|**instance_max_worker_threads**|int|Limite di thread di lavoro a livello di istanza.|
|**replica_type**|int|Tipo di replica, dove 0 è primario e 1 è secondario.|
|**max_transaction_size**|bigint|Spazio di log massimo utilizzato da qualsiasi transazione, in KB.|
|**checkpoint_rate_mbps**|int|Larghezza di banda Checkpoint, in Mbps.|
|**checkpoint_rate_io**|int|Velocità di i/o Checkpoint in IOs al secondo.|
|**last_updated_date_utc**|Datetime|Data e ora dell'Ultima modifica o riconfigurazione dell'ultima impostazione.|
|**primary_group_id**|int|ID del gruppo di carico di lavoro utente primario.|
|**primary_group_max_workers**|int|Limite di lavoro al livello del gruppo di carico di lavoro dell'utente primario.|
|**primary_min_log_rate**|bigint|Velocità minima dei log (byte al secondo) al livello del gruppo di carico di lavoro dell'utente primario.|
|**primary_max_log_rate**|bigint|Velocità massima di log (byte al secondo) al livello del gruppo di carico di lavoro dell'utente primario.|
|**primary_group_min_io**|int|I/o minimo al livello del gruppo di carico di lavoro dell'utente primario.|
|**primary_group_max_io**|int|I/o massimo al livello del gruppo di carico di lavoro dell'utente primario.|
|**primary_group_min_cpu**|float|Limite minimo di percentuale CPU al livello del gruppo di carico di lavoro dell'utente primario.|
|**primary_group_max_cpu**|float|Limite di percentuale massimo della CPU al livello del gruppo di carico di lavoro dell'utente primario.|
|**primary_log_commit_fee**|int|Tariffa di commit per la gestione della frequenza dei log al livello del gruppo di carico di lavoro utente|
|**primary_pool_max_workers**|int|Limite di lavoro a livello di pool di utenti primario.
|**pool_max_io**|int|Limite massimo di i/o a livello di pool di utenti primario.|
|**govern_db_memory_in_resource_pool**|bit|Indica se le dimensioni massime del pool di buffer sono regolate a livello del pool di risorse. Vengono in genere impostati per i database all'interno dei pool elastici.|
|**volume_local_iops**|int|Limite di IOs al secondo per il volume locale (ad esempio C:, D:).|
|**volume_managed_xstore_iops**|int|Limite di IOs al secondo per l'account di archiviazione remoto.|
|**volume_external_xstore_iops**|int|Limite di IOs al secondo per l'account di archiviazione remoto usato dai backup e dalla telemetria del database SQL di Azure.|
|**volume_type_local_iops**|int|Limite di IOs al secondo per tutti i volumi locali.|
|**volume_type_managed_xstore_iops**|int|Limite di IOs al secondo per tutti gli account di archiviazione remoti utilizzati dall'istanza.|
|**volume_type_external_xstore_iops**|int|Limite di IOs al secondo per tutti gli account di archiviazione remoti usati dai backup e dalla telemetria del database SQL di Azure per l'istanza.|
|**volume_pfs_iops**|int|Limite di IOs al secondo per archiviazione file Premium.|
|**volume_type_pfs_iops**|int|Limite di IOs al secondo per tutti i file di archiviazione Premium utilizzati dall'istanza.|
|||

## <a name="permissions"></a>Permissions

Questa vista richiede l'autorizzazione VIEW DATABASE STATE.

## <a name="remarks"></a>Note

Gli utenti possono accedere a questa DMV per la configurazione della governance delle risorse e le impostazioni di capacità per un database di database SQL di Azure. 

> [!IMPORTANT]
> La maggior parte dei dati esposti da questa DMV è destinata al consumo interno ed è soggetta a modifiche.

## <a name="examples"></a>Esempi

Nell'esempio seguente vengono restituiti i dati della frequenza di log massimi dell'istanza ordinati in base al nome del database all'interno del server di database per un database singolo o in pool.

```
SELECT database_name,
       primary_max_log_rate
FROM sys.dm_user_db_resource_governance
ORDER BY database_name DESC;  
```

## <a name="see-also"></a>Vedere anche

- [Governance della frequenza del log delle transazioni](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Limiti delle risorse DTU database singolo](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [Limiti delle risorse vCore database singolo](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
