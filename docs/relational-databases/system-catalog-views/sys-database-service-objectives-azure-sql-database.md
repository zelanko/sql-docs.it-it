---
title: database_service_objectives (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 08/30/2016
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
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7a073dba8a05aa6f098bdf2b2ce1666d4cc324be
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028522"
---
# <a name="sysdatabaseserviceobjectives-azure-sql-database"></a>database_service_objectives (Database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Restituisce l'edizione (livello di servizio), l'obiettivo di servizio (piano tariffario) e nome del pool elastico, se presente, per un database SQL di Azure o Azure SQL Data Warehouse. Se connessi al database master in un server di Database SQL di Azure, restituisce informazioni su tutti i database. Per Azure SQL Data Warehouse, è necessario essere connessi al database master.  
  
  
 Per informazioni sui prezzi, vedere [opzioni del Database SQL e le prestazioni: Database SQL-prezzi](https://azure.microsoft.com/pricing/details/sql-database/) e [SQL Data Warehouse prezzi](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).  
  
 Per modificare le impostazioni del servizio, vedere [ALTER DATABASE (Database SQL di Azure)](../../t-sql/statements/alter-database-azure-sql-database.md) e [ALTER DATABASE (Azure SQL Data Warehouse)](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).  
  
 La vista database_service_objectives contiene le colonne seguenti.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|database_id|INT|ID del database, univoco all'interno di un'istanza del server di Database SQL di Azure. Sottoponibile a join con [Sys. Databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|edition|sysname|Il livello di servizio per il database o data warehouse: **Base**, **Standard**, **Premium** oppure **Data Warehouse**.|  
|service_objective|sysname|Il piano tariffario del database. Se il database è in un pool elastico, restituisce **ElasticPool**.<br /><br /> Nel **base** tier, restituisce **base**.<br /><br /> **Database singolo in un livello di servizio standard** restituisce uno dei seguenti: S0, S1, S2, S3, S4, S6, S7, S9 o S12.<br /><br /> **Database singolo in un livello premium** restituisce delle operazioni seguenti: P1, P2, P4, P6, P11 o P15.<br /><br /> **SQL Data Warehouse** restituisce DW100 tramite DW10000c.|  
|nome_pool_elastico|sysname|Il nome del [pool elastico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) a cui appartiene il database. Restituisce **NULL** se il database è un database singolo o un warehoue dati.|  
  
## <a name="permissions"></a>Permissions  
 È necessario **dbManager** autorizzazione per il database master.  A livello di database, l'utente deve essere l'autore o il proprietario.  
  
## <a name="examples"></a>Esempi  
 Questo esempio può essere eseguito nel database master o nei database utente. La query restituisce il nome del servizio e informazioni di livello delle prestazioni dei database.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
