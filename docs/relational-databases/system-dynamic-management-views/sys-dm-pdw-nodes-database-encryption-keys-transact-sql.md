---
title: sys. dm_pdw_nodes_database_encryption_keys (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e7fd02b2-5d7e-4816-a0af-b58ae2ac3f7a
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c319259d8997db2ff39d90b408056d03eb008782
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401644"
---
# <a name="sysdm_pdw_nodes_database_encryption_keys-transact-sql"></a>sys. dm_pdw_nodes_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Restituisce informazioni sullo stato di crittografia di un database e sulle chiavi di crittografia a esso associate. **sys. dm_pdw_nodes_database_encryption_keys** fornisce queste informazioni per ogni nodo. Per ulteriori informazioni sulla crittografia del database, vedere [Transparent Data Encryption (SQL Server PDW)](../../analytics-platform-system/transparent-data-encryption.md).  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID del database fisico in ogni nodo.|  
|encryption_state|**int**|Indica se il database in questo nodo è crittografato o non crittografato.<br /><br /> 0 = Nessuna chiave di crittografia del database presente, nessuna crittografia<br /><br /> 1 = Non crittografato<br /><br /> 2 = Crittografia in corso<br /><br /> 3 = Crittografato<br /><br /> 4 = Modifica chiave in corso<br /><br /> 5 = Decrittografia in corso<br /><br /> 6 = modifica della protezione in corso (il certificato che sta crittografando la chiave di crittografia del database è in corso di modifica).|  
|create_date|**DateTime**|Visualizza la data di creazione della chiave di crittografia.|  
|regenerate_date|**DateTime**|Visualizza la data di rigenerazione della chiave di crittografia.|  
|modify_date|**DateTime**|Visualizza la data di modifica della chiave di crittografia.|  
|set_date|**DateTime**|Visualizza la data di applicazione al database della chiave di crittografia.|  
|opened_date|**DateTime**|Mostra l'ultima apertura della chiave del database.|  
|key_algorithm|**varchar (?)**|Visualizza l'algoritmo usato per la chiave.|  
|key_length|**int**|Visualizza la lunghezza della chiave.|  
|encryptor_thumbprint|**varbin**|Mostra l'identificazione digitale della crittografia.|  
|percent_complete|**reale**|Percentuale di completamento del cambiamento di stato della crittografia del database. In assenza di un cambiamento di stato il valore sarà 0.|  
|node_id|**int**|ID numerico univoco associato al nodo.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente viene aggiunta `sys.dm_pdw_nodes_database_encryption_keys` ad altre tabelle di sistema per indicare lo stato di crittografia per ogni nodo dei database protetti da Transparent Data Encryption.  
  
```  
SELECT D.database_id AS DBIDinMaster, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName,   
keys.encryption_state  
FROM sys.dm_pdw_nodes_database_encryption_keys AS keys  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON keys.database_id = PD.database_id AND keys.pdw_node_id = PD.pdw_node_id  
JOIN sys.pdw_database_mappings AS DM  
    ON DM.physical_name = PD.physical_name  
JOIN sys.databases AS D  
    ON D.database_id = DM.database_id  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel data warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [CREAZIONE della chiave di crittografia del DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  

