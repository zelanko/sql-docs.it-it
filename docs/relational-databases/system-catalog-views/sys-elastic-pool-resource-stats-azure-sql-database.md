---
title: sys.elastic_pool_resource_stats
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: reference
f1_keywords:
- sys.elastic_pool_resource_stats catalog view
helpviewer_keywords:
- sys.elastic_pool_resource_stats_TSQL
- sys.elastic_pool_resource_stats
- elastic_pool_resource_stats_TSQL
- elastic_pool_resource_stats
ms.assetid: f242c1bd-3cc8-4c8b-8aaf-c79b6a8a0329
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 0712785a5af3e8cc3c606a597ba02e0075c88dd9
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843868"
---
# <a name="syselastic_pool_resource_stats-azure-sql-database"></a>sys. elastic_pool_resource_stats (database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Restituisce le statistiche di utilizzo delle risorse per tutti i pool elastici in un server di database SQL. Per ogni pool elastico è presente una riga per ogni finestra di report di 15 secondi (quattro righe al minuto). Sono inclusi CPU, i/o, log, consumo di risorse di archiviazione e utilizzo simultaneo di richieste/sessioni da parte di tutti i database nel pool. Questi dati vengono conservati per 14 giorni. 
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.|  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|Ora UTC che indica l'inizio dell'intervallo di Reporting di 15 secondi.|  
|**end_time**|**datetime2**|Ora UTC che indica la fine dell'intervallo di Reporting di 15 secondi.|  
|**elastic_pool_name**|**nvarchar(128)**|Nome del pool di database elastici.|  
|**avg_cpu_percent**|**Decimal (5, 2)**|Utilizzo medio del calcolo in percentuale del limite del pool.|  
|**avg_data_io_percent**|**Decimal (5, 2)**|Utilizzo medio di I/O in percentuale in base al limite del pool.|  
|**avg_log_write_percent**|**Decimal (5, 2)**|Utilizzo medio delle risorse di scrittura in percentuale del limite del pool.|  
|**avg_storage_percent**|**Decimal (5, 2)**|Utilizzo medio dello spazio di archiviazione in percentuale del limite di archiviazione del pool.|  
|**max_worker_percent**|**Decimal (5, 2)**|Numero massimo di ruoli di lavoro simultanei (richieste) in percentuale in base al limite del pool.|  
|**max_session_percent**|**Decimal (5, 2)**|Numero massimo di sessioni simultanee in percentuale in base al limite del pool.|  
|**elastic_pool_dtu_limit**|**int**|Impostazione del DTU del pool elastico corrente per questo pool elastico durante questo intervallo.|  
|**elastic_pool_storage_limit_mb**|**bigint**|Impostazione limite massimo corrente di archiviazione del pool elastico per questo pool elastico in megabyte durante questo intervallo.|
|**avg_allocated_storage_percent**|**Decimal (5, 2)**|Percentuale di spazio dati allocato da tutti i database nel pool elastico.  Questo è il rapporto tra lo spazio dati allocato e le dimensioni massime dei dati per il pool elastico.  Per ulteriori informazioni, vedere la pagina relativa [alla gestione dello spazio file nel database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|  
  
## <a name="remarks"></a>Osservazioni

 Questa vista è presente nel database master del server di database SQL. Per eseguire una query su **sys. elastic_pool_resource_stats**è necessario essere connessi al database master.  
  
## <a name="permissions"></a>Autorizzazioni

 È richiesta l'appartenenza al ruolo **dbmanager** .  
  
## <a name="examples"></a>Esempi

 Nell'esempio seguente vengono restituiti i dati di utilizzo delle risorse ordinati in base all'ora più recente per tutti i pool di database elastici nel server di database SQL corrente.  
  
```sql
SELECT * FROM sys.elastic_pool_resource_stats
ORDER BY end_time DESC;  
```

 Nell'esempio seguente viene calcolato il consumo di percentuale medio di DTU per un determinato pool.  

```sql
SELECT start_time, end_time,
  (SELECT Max(v)
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]
FROM sys.elastic_pool_resource_stats
WHERE elastic_pool_name = '<your pool name>'
ORDER BY end_time DESC;  
```

## <a name="see-also"></a>Vedere anche

 Aumenta [la crescita esplosiva con i database elastici](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [Creare e gestire un pool di database elastici del database SQL (anteprima)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [sys. resource_stats &#40;database&#41; SQL di Azure](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [sys. dm_db_resource_stats &#40;database SQL di Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
