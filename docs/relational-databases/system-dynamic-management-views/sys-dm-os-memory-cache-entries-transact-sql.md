---
title: sys.dm_os_memory_cache_entries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_cache_entries
- sys.dm_os_memory_cache_entries
- dm_os_memory_cache_entries_TSQL
- sys.dm_os_memory_cache_entries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_entries dynamic management view
ms.assetid: dd32be6b-10d1-4059-b4fd-0bf817f40d54
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2d00a5e39057f6c1410cb170095bc9c0d5f322fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63048065"
---
# <a name="sysdmosmemorycacheentries-transact-sql"></a>sys.dm_os_memory_cache_entries (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Vengono restituite informazioni su tutte le voci nelle cache di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Utilizzare questa vista per tracciare le informazioni relative alle voci della cache e agli oggetti associati. È anche possibile utilizzare la vista per ottenere le statistiche relative alle voci di cache.  
  
> [!NOTE]  
>  Per chiamare questo elemento dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oppure [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], usare il nome **sys.dm_pdw_nodes_os_memory_cache_entries**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|Indirizzo della cache. Non ammette i valori Null.|  
|**name**|**nvarchar(256)**|Nome della cache. Non ammette i valori Null.|  
|**type**|**varchar(60)**|Tipo di cache. Non ammette i valori Null.|  
|**entry_address**|**varbinary(8)**|Indirizzo del descrittore della voce di cache. Non ammette i valori Null.|  
|**entry_data_address**|**varbinary(8)**|Indirizzo dei dati utente nella voce di cache.<br /><br /> 0x00000000 = Indirizzo dei dati della voce non disponibile.<br /><br /> Non ammette i valori Null.|  
|**in_use_count**|**int**|Numero di utenti simultanei di questa voce di cache. Non ammette i valori Null.|  
|**is_dirty**|**bit**|Indica se questa voce di cache è contrassegnata per la rimozione. 1 = Contrassegnata per la rimozione. Non ammette i valori Null.|  
|**disk_ios_count**|**int**|Numero di I/O verificatisi durante la creazione di questa voce. Non ammette i valori Null.|  
|**context_switches_count**|**int**|Numero di cambi di contesto verificatisi durante la creazione di questa voce. Non ammette i valori Null.|  
|**original_cost**|**int**|Costo originale della voce. Questo valore è un'approssimazione del numero di I/O, del costo di istruzioni per la CPU e della quantità di memoria utilizzata dalla voce. Maggiore il costo, minori le possibilità che l'elemento venga rimosso dalla cache. Non ammette i valori Null.|  
|**current_cost**|**int**|Costo corrente della voce di cache. Questo valore viene aggiornato durante il processo di eliminazione delle voci. Il costo corrente viene reimpostato sul valore originale al riutilizzo della voce. Non ammette i valori Null.|  
|**memory_object_address**|**varbinary(8)**|Indirizzo dell'oggetto di memoria associato. Ammette i valori Null.|  
|**pages_allocated_count**|**bigint**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Numero di pagine da 8 KB per l'archiviazione della voce di cache. Non ammette i valori Null.|  
|**pages_kb**|**bigint**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Quantità di memoria in kilobyte (KB) utilizzata da questa voce di cache.  Non ammette i valori Null.|  
|**entry_data**|**nvarchar(2048)**|Rappresentazione serializzata della voce archiviata nella cache. Queste informazioni dipendono dall'archiviazione nella cache. Ammette i valori Null.|  
|**pool_id**|**int**|**Si applica a**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID del pool di risorse associato alla voce. Ammette i valori Null.<br /><br /> non katmai|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo in questa distribuzione.|  
  
## <a name="permissions"></a>Permissions 

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], è necessario il `VIEW DATABASE STATE` autorizzazione nel database.   

## <a name="see-also"></a>Vedere anche  
 
  [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


