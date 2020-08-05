---
title: sys.database_service_objectives
titleSuffix: Azure SQL Database
ms.date: 03/21/2018
ms.service: sql-database
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.topic: conceptual
keywords:
- pool elastico
- pool elastico, gestione
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
author: CarlRabeler
ms.author: carlrab
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: e6ee5d0f6a2b26dc10c901297097b99338ba9091
ms.sourcegitcommit: bc10ec0be5ddfc5f0bc220a9ac36c77dd6b80f1d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2020
ms.locfileid: "87544374"
---
# <a name="sysdatabase_service_objectives-azure-sql-database"></a>sys.database_service_objectives (database SQL di Azure)
[!INCLUDE [asdb-asdbmi-asa](../../includes/applies-to-version/asdb-asdbmi-asa.md)]

Restituisce l'edizione (livello di servizio), l'obiettivo di servizio (piano tariffario) e il nome del pool elastico, se presente, per un database SQL di Azure o un Azure SQL Data Warehouse. Se si è connessi al database master in un server di database SQL di Azure, restituisce informazioni su tutti i database. Per Azure SQL Data Warehouse, è necessario essere connessi al database master.  
  
  
 Per informazioni sui prezzi, vedere [Opzioni e prestazioni del database SQL: prezzi del database SQL](https://azure.microsoft.com/pricing/details/sql-database/) e [prezzi SQL data warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).  
  
 Per modificare le impostazioni del servizio, vedere [ALTER database (database SQL di Azure)](../../t-sql/statements/alter-database-azure-sql-database.md) e [alter database (Azure SQL Data Warehouse)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest).  
  
 La vista sys. database_service_objectives contiene le colonne seguenti.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|database_id|int|ID del database, univoco all'interno di un'istanza del server di database SQL di Azure. Joinable con [sys. databases &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|edition|sysname|Livello di servizio per il database o data warehouse: **Basic**, **standard**, **Premium** o **data warehouse**.|  
|service_objective|sysname|Piano tariffario del database. Se il database si trova in un pool elastico, restituisce **ElasticPool**.<br /><br /> Il livello **Basic** restituisce **Basic**.<br /><br /> Il **database singolo in un livello di servizio standard** restituisce uno dei seguenti: S0, S1, S2, S3, S4, S6, S7, S9 o S12.<br /><br /> Il **database singolo in un livello Premium** restituisce quanto segue: P1, P2, P4, P6, P11 o P15.<br /><br /> **SQL data warehouse** restituisce DW100 tramite DW30000c.<br /><br /> Per informazioni dettagliate, vedere [database singoli](/azure/sql-database/sql-database-dtu-resource-limits-single-databases/), [pool elastici](/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools/), [data warehouse](/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu/)|  
|elastic_pool_name|sysname|Nome del [pool elastico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) a cui appartiene il database. Restituisce **null** se il database è un database singolo o un data warehouse.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede l'autorizzazione **dbManager** per il database master.  A livello di database, l'utente deve essere l'autore o il proprietario.  
  
## <a name="examples"></a>Esempi  
 Questo esempio può essere eseguito nel database master o nei database utente del database SQL di Azure. La query restituisce le informazioni sul nome, il servizio e il livello di prestazioni dei database.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
