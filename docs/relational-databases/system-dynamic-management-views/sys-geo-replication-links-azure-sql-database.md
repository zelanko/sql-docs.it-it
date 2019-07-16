---
title: Sys. geo_replication_links (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_links_TSQL
- dm_geo_replication_links
- sys.dm_geo_replication_links
- sys.dm_geo_replication_links_TSQL
helpviewer_keywords:
- sys.dm_geo_replication_links dynamic management view
- dm_geo_replication_links dynamic management view
ms.assetid: 58911798-1d60-4f28-87ab-2def2bfc3de7
author: mashamsft
ms.author: mathoma
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 6e768f447cd53321861eae91bbe40e2e34ad12f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043156"
---
# <a name="sysgeoreplicationlinks-azure-sql-database"></a>sys.geo_replication_links (database SQL di Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contiene una riga per ogni collegamento di replica tra i database primari e secondari in una relazione di replica geografica. La vista risiede nel database master logico.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID del database corrente nella vista sys. Databases.|  
|start_date|**datetimeoffset**|Ora UTC in un Data Center a livello di area del Database SQL quando è stata avviata la replica di database|  
|modify_date|**datetimeoffset**|Ora UTC in Database di SQL Data Center regionale di quando è stata completata la replica geografica del database. Il nuovo database è sincronizzato con il database primario a partire da questo momento. .|  
|link_guid|**uniqueidentifier**|ID univoco del collegamento di replica geografica.|  
|partner_server|**sysname**|Nome del server di Database SQL che contiene il database con replica geografica.|  
|partner_database|**sysname**|Nome del database con replica geografica nel server di Database SQL collegato.|  
|replication_state|**tinyint**|Lo stato della replica geografica per questo database, uno di:.<br /><br /> 0 = in sospeso. La creazione del database secondario attivo è pianificata ma i passaggi necessari per la preparazione non sono ancora stati completati.<br /><br /> 1 = Seeding. La destinazione di replica geografica è in fase di seeding, ma i due database non ancora sincronizzati. Fino al completamento del seeding non è possibile connettersi al database secondario. Rimozione di database secondario dal server primario verrà annullata l'operazione di seeding.<br /><br /> 2 = recupero. Il database secondario è in uno stato transazionale coerente e sempre sincronizzato con il database primario.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|role|**tinyint**|Ruolo replica geografica, uno di:<br /><br /> 0 = database primario. Il database_id fa riferimento al database primario nella relazione di replica geografica.<br /><br /> 1 = database secondario.  Il database_id fa riferimento al database primario nella relazione di replica geografica.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|Tipo secondario, uno di:<br /><br /> 0 = No. Il database secondario non accessibile fino al failover.<br /><br /> 1 = sola lettura. Il database secondario è accessibile solo per le connessioni client con ApplicationIntent = ReadOnly.<br /><br /> 2 = Tutte. Il database secondario è accessibile da qualsiasi connessione client.|  
|DESC secondary_allow_connections|**nvarchar(256)**|No<br /><br /> Tutti<br /><br /> Sola lettura|  
  
## <a name="permissions"></a>Permissions

In questa vista è disponibile solo nel **master** database all'account di accesso dell'entità a livello di server.  
  
## <a name="example"></a>Esempio

Mostra tutti i database con collegamenti di replica geografica.  

```sql
SELECT
     database_id  
   , start_date  
   , partner_server  
   , partner_database  
   , replication_state  
   , role_desc  
   , secondary_allow_connections_desc
FROM sys.geo_replication_links;  
```

## <a name="see-also"></a>Vedere anche

 [ALTER DATABASE (database SQL di Azure)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [DM geo_replication_link_status &#40;Database SQL di Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [DM operation_status &#40;Database SQL di Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
