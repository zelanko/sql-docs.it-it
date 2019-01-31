---
title: DM geo_replication_link_status (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_link_status
- dm_geo_replication_link_status_TSQL
- sys.dm_geo_replication_link_status
- sys.dm_geo_replication_link_status_TSQL
helpviewer_keywords:
- dm_geo_replication_link_status dynamic management view
- sys.dm_geo_replication_link_status dynamic management view
ms.assetid: d763d679-470a-4c21-86ab-dfe98d37e9fd
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 94d5a2e924cfe4aa7625f6cfce40c5758eecb6a5
ms.sourcegitcommit: 97340deee7e17288b5eec2fa275b01128f28e1b8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/30/2019
ms.locfileid: "55421158"
---
# <a name="sysdmgeoreplicationlinkstatus-azure-sql-database"></a>sys.dm_geo_replication_link_status (database SQL di Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contiene una riga per ogni collegamento di replica tra i database primari e secondari in una relazione di replica geografica. Sono inclusi i database primari e secondari. Se esiste più di un collegamento di replica continua per un determinato database primario, questa tabella contiene una riga per ogni relazione. La vista viene creata in tutti i database, incluso il database master logico. Tuttavia, se si esegue una query su questa vista nel database master logico viene restituito un set vuoto.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|ID univoco del collegamento di replica.|  
|partner_server|**sysname**|Nome del server di Database SQL che contiene il database collegato.|  
|partner_database|**sysname**|Nome del database collegato nel server di database SQL collegato.|  
|last_replication|**datetimeoffset**|Il timestamp dell'acknowledgement dell'ultima transazione per il database secondario in base all'orologio di database primario. Questo valore è disponibile nel database primario.|  
|replication_lag_sec|**int**|Differenza di tempo in secondi tra il valore last_replication e il timestamp del commit della transazione nella replica primaria in base all'orologio di database primario.  Questo valore è disponibile nel database primario.|  
|replication_state|**tinyint**|Lo stato della replica geografica per questo database, uno di:.<br /><br /> 1 = Seeding. La destinazione di replica geografica è in fase di seeding, ma i due database non ancora sincronizzati. Fino al completamento del seeding non è possibile connettersi al database secondario. Rimozione di database secondario dal server primario verrà annullata l'operazione di seeding.<br /><br /> 2 = recupero. Il database secondario è in uno stato transazionale coerente e sempre sincronizzato con il database primario.<br /><br /> 4 = degli elementi sospesi. Non è presente una relazione di copia continua attiva. Questo stato indica in genere che la larghezza di banda disponibile per l'interlink è insufficiente per il livello di attività di transazione nel database primario. La relazione di copia continua tuttavia rimane invariata.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|ruolo|**tinyint**|Ruolo replica geografica, uno di:<br /><br /> 0 = database primario. Il database_id fa riferimento al database primario nella relazione di replica geografica.<br /><br /> 1 = database secondario.  Il database_id fa riferimento al database primario nella relazione di replica geografica.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|Tipo secondario, uno di:<br /><br /> 0 non = Nessun direct sono consentite connessioni al database secondario e il database non è disponibile per l'accesso in lettura.<br /><br /> 2 = all sono consentite connessioni ai database nella replica secondaria; ication per l'accesso di sola lettura.|  
|secondary_allow_connections_desc|**nvarchar(256)**|No<br /><br /> All|  
|last_commit|**datetimeoffset**|Ora dell'ultima transazione di commit nel database. Se recuperata nel database primario, indica l'ultima ora di commit nel database primario. Se recuperata nel database secondario, indica l'ultima ora di commit nel database secondario. Se recuperata nel database secondario quando la replica primaria del collegamento di replica è verso il basso, indica fino a quando non punto in cui il database secondario viene aggiornato rispetto.|
  
> [!NOTE]  
>  Se la relazione di replica viene terminata rimuovendo il database secondario (sezione 4.2), la riga per il database nel **DM geo_replication_link_status** visualizzazione scomparirà.  
  
## <a name="permissions"></a>Permissions  
 Eseguire una query qualsiasi account con autorizzazione view_database_state **DM geo_replication_link_status**.  
  
## <a name="example"></a>Esempio  
 Mostrare intervalli di replica e ora dell'ultima replica di database secondari.  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE &#40;Database SQL di Azure&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [Sys. geo_replication_links &#40;Database SQL di Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [DM operation_status &#40;Database SQL di Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
