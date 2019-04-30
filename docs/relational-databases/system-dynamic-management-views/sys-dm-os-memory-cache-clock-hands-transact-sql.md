---
title: sys.dm_os_memory_cache_clock_hands (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_clock_hands_TSQL
- dm_os_memory_cache_clock_hands
- dm_os_memory_cache_clock_hands_TSQL
- sys.dm_os_memory_cache_clock_hands
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_clock_hands dynamic management view
ms.assetid: 0660eddc-691c-425f-9d43-71151d644de7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b39f40a36a9b9a639b8b6c90f6a6a37f7a32a4e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63047184"
---
# <a name="sysdmosmemorycacheclockhands-transact-sql"></a>sys.dm_os_memory_cache_clock_hands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce lo stato di ogni indicatore per un orologio della cache.  
  
> [!NOTE]  
>  Per chiamare questo elemento dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oppure [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], usare il nome **sys.dm_pdw_nodes_os_memory_cache_clock_hands**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|Indirizzo della cache associata all'orologio. Non ammette i valori Null.|  
|**name**|**nvarchar(256)**|Nome della cache. Non ammette i valori Null.|  
|**type**|**nvarchar(60)**|Tipo di archivio di cache. Possono essere presenti diverse cache dello stesso tipo. Non ammette i valori Null.|  
|**clock_hand**|**nvarchar(60)**|Tipo di indicatore. I possibili valori sono i seguenti:<br /><br /> External<br /><br /> Interno<br /><br /> Non ammette i valori Null.|  
|**clock_status**|**nvarchar(60)**|Stato dell'orologio. I possibili valori sono i seguenti:<br /><br /> Sospeso<br /><br /> In esecuzione<br /><br /> Non ammette i valori Null.|  
|**rounds_count**|**bigint**|Numero di operazioni eseguite nella cache per rimuovere le voci. Non ammette i valori Null.|  
|**removed_all_rounds_count**|**bigint**|Numero di voci rimosse da tutte le operazioni. Non ammette i valori Null.|  
|**updated_last_round_count**|**bigint**|Numero di voci aggiornate durante l'ultima operazione. Non ammette i valori Null.|  
|**removed_last_round_count**|**bigint**|Numero di voci rimosse durante l'ultima operazione. Non ammette i valori Null.|  
|**last_tick_time**|**bigint**|Ora, espressa in millisecondi, in cui l'indicatore dell'orologio si è spostata per l'ultima volta. Non ammette i valori Null.|  
|**round_start_time**|**bigint**|Ora, espressa in millisecondi, dell'operazione precedente. Non ammette i valori Null.|  
|**last_round_start_time**|**bigint**|Tempo totale, espresso in millisecondi, impiegato dall'orologio per completare il ciclo precedente. Non ammette i valori Null.|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo in questa distribuzione.|  
  
## <a name="permissions"></a>Permissions  

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], è necessario il `VIEW DATABASE STATE` autorizzazione nel database.   
  
## <a name="remarks"></a>Note  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le informazioni vengono archiviate in memoria in una struttura denominata cache in memoria. Le informazioni archiviate nella cache possono essere dati, voci di indice, piani di procedure compilati e un'ampia gamma di altri tipi di informazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per evitare la nuova creazione delle informazioni, queste vengono mantenute nella cache in memoria per il maggior tempo possibile e vengono in genere rimosse quando risultano obsolete oppure quando è necessario spazio di memoria per nuove informazioni. Il processo di rimozione delle informazioni meno recenti è denominato operazione della memoria. L'operazione della memoria è un'attività frequente, ma non continua. Un algoritmo di orologio controlla l'operazione nella cache in memoria. Ogni orologio può controllare diverse operazioni della memoria tramite indicatori. L'indicatore dell'orologio della cache in memoria rappresenta la posizione corrente di uno degli indicatori di un'operazione della memoria.  

## <a name="see-also"></a>Vedere anche  
 [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)    
 [sys.dm_os_memory_cache_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md)
  

