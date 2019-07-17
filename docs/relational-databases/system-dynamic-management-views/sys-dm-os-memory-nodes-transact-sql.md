---
title: sys.dm_os_memory_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_nodes_TSQL
- sys.dm_os_memory_nodes
- sys.dm_os_memory_nodes_TSQL
- dm_os_memory_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_nodes dynamic management view
ms.assetid: bf4032fe-7db1-40e9-a62e-d69cebff4b44
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7d1be540f73a5a5e625a1f33f1c3f24e409fd307
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265758"
---
# <a name="sysdmosmemorynodes-transact-sql"></a>sys.dm_os_memory_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Le allocazioni interne a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzano il gestore della memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La differenza tra i contatori di memoria del processo di rilevamento **sys.dm_os_process_memory** e i contatori interni possono indicare l'utilizzo di memoria da componenti esterni nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] spazio di memoria.  
  
 I nodi vengono creati per nodi di memoria NUMA fisici. Questi potrebbero essere diversi dai nodi CPU in **DM os_nodes**.  
  
 Nessuna delle allocazioni eseguite direttamente tramite le routine di allocazione di memoria di Windows viene registrata. Nella tabella seguente sono fornite informazioni sulle allocazioni di memoria eseguite solo utilizzando interfacce dello strumento di gestione della memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Per chiamare questo elemento dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oppure [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], usare il nome **sys.dm_pdw_nodes_os_memory_nodes**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**memory_node_id**|**smallint**|Specifica l'ID del nodo di memoria. Correlati a **memory_node_id** dei **DM os_memory_clerks**. Non ammette i valori NULL.|  
|**virtual_address_space_reserved_kb**|**bigint**|Indica il numero di indirizzi virtuali riservati, in kilobyte (KB), di cui non è stato eseguito il commit né il mapping a pagine fisiche. Non ammette i valori NULL.|  
|**virtual_address_space_committed_kb**|**bigint**|Specifica la quantità di indirizzo virtuale, in KB, di cui è stato eseguito il commit o il mapping a pagine fisiche. Non ammette i valori NULL.|  
|**locked_page_allocations_kb**|**bigint**|Specifica la quantità di memoria fisica, in KB, bloccata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non ammette i valori NULL.|  
|**single_pages_kb**|**bigint**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Quantità di memoria riservata, in KB, allocata utilizzando l'allocatore di pagine singole da thread in esecuzione sul nodo. Questa memoria è allocata dal pool di buffer. Questo valore indica il nodo in cui si è verificata la richiesta di allocazione, non la posizione fisica in cui la richiesta di allocazione è stata soddisfatta.|  
|**pages_kb**|**bigint**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Specifica la quantità di memoria di cui è stato eseguito il commit, in KB, allocata da questo nodo NUMA dall'allocatore di pagine del gestore della memoria. Non ammette i valori NULL.|  
|**multi_pages_kb**|**bigint**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Quantità di memoria riservata, in KB, allocata utilizzando l'allocatore di più pagine da thread in esecuzione sul nodo. Questa memoria è esterna al pool di buffer. Questo valore indica il nodo in cui si sono verificate le richieste di allocazione, non la posizione fisica in cui le richieste di allocazione sono state soddisfatte.|  
|**shared_memory_reserved_kb**|**bigint**|Specifica la quantità di memoria condivisa del nodo, in KB, che è stata riservata. Non ammette i valori NULL.|  
|**shared_memory_committed_kb**|**bigint**|Specifica la quantità di memoria condivisa del nodo, in KB, di cui è stato eseguito il commit. Non ammette i valori NULL.|  
|**cpu_affinity_mask**|**bigint**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Solo per uso interno. Non ammette i valori NULL.|  
|**online_scheduler_mask**|**bigint**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Solo per uso interno. Non ammette i valori NULL.|  
|**processor_group**|**smallint**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Solo per uso interno. Non ammette i valori NULL.|  
|**foreign_committed_kb**|**bigint**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Viene specificata la quantità totale di memoria di cui è stato eseguito il commit, in KB, da altri nodi di memoria. Non ammette i valori NULL.|  
|**target_kb** |**bigint** |**Si applica a**: da [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Specifica l'obiettivo di memoria per il nodo di memoria, in KB. |   
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo in questa distribuzione.|  
  
## <a name="permissions"></a>Permissions

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, è necessario il `VIEW DATABASE STATE` autorizzazione nel database. Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard e i livelli Basic, è necessario il **amministratore del Server** o un' **amministratore di Azure Active Directory** account.   

## <a name="see-also"></a>Vedere anche  
  [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


