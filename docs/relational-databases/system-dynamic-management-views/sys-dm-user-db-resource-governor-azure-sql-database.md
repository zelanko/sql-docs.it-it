---
title: Sys.dm_user_db_resource_governance (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: eebc22fa4f17680b843f195777d7cc5f4b2835ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090454"
---
# <a name="sysdmuserdbresourcegovernance-transact-sql"></a>Sys.dm_user_db_resource_governance (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Restituisce le impostazioni di configurazione e la capacità per un database SQL di Azure di governance delle risorse.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_id**|int|ID del database, univoco all'interno di un server di Database SQL di Azure.|
|**logical_database_guid**|uniqueidentifier|Logica guid per il database utente e rimane attraverso il ciclo di vita di un database utente.  Rinominare o l'impostazione di un database in un altro SLO non modificherà il GUID. |
|**physical_database_guid**|uniqueidentifier|Guid fisico per un database utente che rimane attraverso il ciclo di vita dell'istanza fisica del database utente. Impostazione a un SLO diversi causerà questa colonna da modificare.|
|**server_name**|nvarchar|Nome del server logico.|
|**database_name**|nvarchar|Nome logico del database.|
|**slo_name**|nvarchar|Servizio obiettivo generazione e a livello hardware.|
|**dtu_limit**|int|Limite DTU del database (NULL per vCore).|
|**cpu_limit**|int|limite di vCore del database (NULL per i database DTU).|
|**min_cpu**|tinyint|Percentuale minima della CPU che può essere utilizzato dal carico di lavoro utente.|
|**max_cpu**|tinyint|Percentuale CPU massima che può essere utilizzato dal carico di lavoro utente.|
|**cap_cpu**|tinyint|Limite di percentuale di CPU per i gruppi di carico di lavoro.|
|**min_cores**|smallint|Numero di CPU usata da SQL.|
|**max_dop**|smallint|Massimo grado parallelismo usato dal carico di lavoro utente.|
|**min_memory**|int|Percentuale di memoria minima che può essere utilizzato dal carico di lavoro utente.|
|**max_memory**|int|Percentuale massima di memoria che può essere utilizzato dal carico di lavoro utente.|
|**max_sessions**|int|Limite di sessione per il gruppo di utenti.|
|**max_memory_grant**|int|Concessione di memoria massima per ogni query nel carico di lavoro utente, in percentuale.|
|**max_db_memory**|int|Max buffer pool memoria limite di utilizzo per il carico di lavoro di database utente|
|**govern_background_io**|bit|Indica se le scritture in background vengono addebitate al gruppo di utenti.|
|**min_db_max_size_in_mb**|bigint|Dimensioni file massime minimo dei database, in MB.|
|**max_db_max_size_in_mb**|bigint|Massimo numero massimo file di database, in MB.|
|**default_db_max_size_in_mb**|bigint|Impostazione predefinita dimensioni massime del database file, in MB.|
|**db_file_growth_in_mb**|bigint|Aumento delle dimensioni predefinite del file di database di azure, in MB.|
|**initial_db_file_size_in_mb**|bigint|Dimensioni predefinite del database file, in MB.|
|**log_size_in_mb**|bigint|Dimensioni predefinite, in MB.|
|**instance_cap_cpu**|int|Limite di utilizzo della CPU a livello di istanza.|
|**instance_max_log_rate**|bigint|Generazione del registro limite di frequenza a livello di istanza, in byte al secondo.|
|**instance_max_worker_threads**|int|Limite di thread di lavoro a livello di istanza.|
|**replica_type**|int|Tipo di replica, dove 0 è primario, e 1 è secondaria.|
|**max_transaction_size**|bigint|Spazio del log massima usato da qualsiasi transazione, in KB.|
|**checkpoint_rate_mbps**|int|Punto di controllo della larghezza di banda, in Mbps.|
|**checkpoint_rate_io**|int|I/o frequenza di checkpoint in IOs al secondo.|
|**last_updated_date_utc**|datetime|Data e ora dell'ultima modifica dell'impostazione o riconfigurazione.|
|**primary_group_id**|int|ID del gruppo di carico di lavoro utente primario.|
|**primary_group_max_workers**|int|Limite di ruolo di lavoro a livello di gruppo del carico di lavoro utente primario.|
|**primary_min_log_rate**|bigint|Frequenza di registrazione minimo (byte / sec) a livello di gruppo del carico di lavoro utente primario.|
|**primary_max_log_rate**|bigint|Frequenza massima del log (byte / sec) a livello di gruppo del carico di lavoro utente primario.|
|**primary_group_min_io**|int|/ O minimo a livello di gruppo del carico di lavoro utente primario.|
|**primary_group_max_io**|int|Numero massimo operazioni i/o a livello di gruppo del carico di lavoro utente primario.|
|**primary_group_min_cpu**|float|Percentuale minima della CPU limitare a livello di gruppo del carico di lavoro utente primario.|
|**primary_group_max_cpu**|float|Percentuale CPU massima limitare a livello di gruppo del carico di lavoro utente primario.|
|**primary_log_commit_fee**|int|Log frequenza governance commit tariffa a livello di gruppo del carico di lavoro utente primario.|
|**primary_pool_max_workers**|int|Limite di ruolo di lavoro a livello di pool utente primario.
|**pool_max_io**|int|Limite massimo dei / o a livello di pool utente primario.|
|**govern_db_memory_in_resource_pool**|bit|Indica se le dimensioni massime del pool di buffer vengano regolata a livello di pool di risorse. In genere impostata per i database all'interno dei pool elastici.|
|**volume_local_iops**|int|IOs per ogni cap secondo per volume locale (ad esempio c:, d:.).|
|**volume_managed_xstore_iops**|int|IOs per ogni secondo limite di utilizzo per l'account di archiviazione remoti.|
|**volume_external_xstore_iops**|int|IOs per ogni cap secondo account di archiviazione remoti usati da dati di telemetria e i backup di database SQL di Azure.|
|**volume_type_local_iops**|int|IOs per ogni secondo limite di utilizzo per tutti i volumi locali.|
|**volume_type_managed_xstore_iops**|int|IOs per ogni secondo limite di utilizzo per tutti gli account di archiviazione remota utilizzata dall'istanza.|
|**volume_type_external_xstore_iops**|int|IOs per ogni secondo limite di utilizzo per tutti gli account di archiviazione remoti usati da backup di database SQL di Azure e i dati di telemetria per l'istanza.|
|**volume_pfs_iops**|int|IOs per ogni secondo limite di utilizzo per archiviazione premium di file.|
|**volume_type_pfs_iops**|int|IOs per ogni secondo limite di utilizzo per tutta l'archiviazione premium file utilizzato dall'istanza.|
|||

## <a name="permissions"></a>Permissions

Questa vista richiede l'autorizzazione VIEW DATABASE STATE.

## <a name="remarks"></a>Note

Gli utenti possono accedere a questa vista a gestione dinamica per la configurazione di governance delle risorse e le impostazioni di capacità per un database SQL di Azure. 

> [!IMPORTANT]
> La maggior parte dei dati rilevati da questa DMV è destinato all'utilizzo interno ed è soggetta a modifiche.

## <a name="examples"></a>Esempi

L'esempio seguente restituisce l'istanza massima velocità dati di log ordinati in base al nome del database all'interno del server di database per un database singolo o in pool.

```
SELECT database_name,
       primary_max_log_rate
FROM sys.dm_user_db_resource_governance
ORDER BY database_name DESC;  
```

## <a name="see-also"></a>Vedere anche

- [Governance delle velocità di log delle transazioni](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Limiti delle risorse DTU di database singolo](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [Limiti delle risorse di Vcore per database singolo](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
