---
title: sys.dm_os_memory_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_pools_TSQL
- dm_os_memory_pools
- dm_os_memory_pools_TSQL
- sys.dm_os_memory_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_pools dynamic management view
ms.assetid: 1ef053f3-c6f3-456e-82b6-26e4bd630d46
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4292c659e796a61e601296a2ac984de987526cad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899899"
---
# <a name="sysdmosmemorypools-transact-sql"></a>sys.dm_os_memory_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce una riga per ogni archivio di oggetti nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile utilizzare questa vista per monitorare l'utilizzo della memoria cache e per identificare l'errato funzionamento della memorizzazione nella cache.  
  
> [!NOTE]  
>  Per chiamare questo elemento dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oppure [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], usare il nome **sys.dm_pdw_nodes_os_memory_pools**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**memory_pool_address**|**varbinary(8)**|Indirizzo di memoria della voce che rappresenta il pool di memoria. Non ammette i valori Null.|  
|**pool_id**|**int**|ID di un pool specifico all'interno di un set di pool. Non ammette i valori Null.|  
|**type**|**nvarchar(60)**|Tipo di pool di oggetti. Non ammette i valori Null. Per altre informazioni, vedere [DM os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**name**|**nvarchar(256)**|Nome assegnato dal sistema dell'oggetto memoria. Non ammette i valori Null.|  
|**max_free_entries_count**|**bigint**|Numero massimo di voci libere che un pool può avere. Non ammette i valori Null.|  
|**free_entries_count**|**bigint**|Numero di voci libere incluse nel pool. Non ammette i valori Null.|  
|**removed_in_all_rounds_count**|**bigint**|Numero di voci rimosse dal pool dall'avvio dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non ammette i valori Null.|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo in questa distribuzione.|  
  
## <a name="permissions"></a>Permissions

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] è richiesta l'autorizzazione `VIEW DATABASE STATE` per il database.   

## <a name="remarks"></a>Note  
 I componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] talvolta utilizzano una struttura comune di pool per memorizzare nella cache tipi di dati omogenei e senza informazioni sullo stato. La struttura di pool è più semplice della struttura di cache. Tutte le voci nei pool sono considerate uguali. Internamente i pool sono clerk di memoria e possono essere utilizzati nelle stesse posizioni in cui vengono utilizzati i clerk di memoria.  
  
## <a name="see-also"></a>Vedere anche  
 
  [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


