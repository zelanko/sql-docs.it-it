---
title: sys.dm_os_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dec718bfea5748db1baa4bb5d9be8c01b85ace26
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013067"
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Un componente interno denominato SQLOS crea le strutture di nodi che imitano la località del processore hardware. Queste strutture possono essere modificate usando [soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md) creare layout di nodo personalizzati.  

> [!NOTE]
> A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] userà automaticamente soft-NUMA per determinate configurazioni di hardware. Per altre informazioni, vedere [Soft-NUMA automatica](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa).
  
Nella tabella seguente sono incluse informazioni su questi nodi.  
  
> [!NOTE]
> Chiamare questa DMV dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oppure [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], usare il nome **sys.dm_pdw_nodes_os_nodes**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|ID del nodo.|  
|node_state_desc|**nvarchar(256)**|Descrizione dello stato del nodo. I valori sono visualizzati con i valori reciprocamente esclusivi all'inizio, seguiti dai valori combinabili. Ad esempio:<br /> Online, Thread Resources Low, Lazy Preemptive<br /><br />Esistono quattro valori node_state_desc reciprocamente esclusivi. Vengono elencate di seguito con le relative descrizioni.<br /><ul><li>ONLINE: Il nodo è online<li>OFFLINE: Il nodo è offline<li>IDLE: Nodo non dispone di alcuna richiesta di lavoro in sospeso ed entrato in uno stato di inattività.<li>IDLE_READY: Nodo non ha richieste di lavoro in sospeso ed è pronto per lo stato inattivo.</li></ul><br />Esistono tre valori node_state_desc combinabili, elencati di seguito con le relative descrizioni.<br /><ul><li>DAC: Questo nodo è riservato per il [connessione amministrativa dedicata](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).<li>THREAD_RESOURCES_LOW: È possibile creare nessun nuovo thread in questo nodo a causa di una condizione di memoria insufficiente.<li>AGGIUNTA A CALDO: Indica i nodi sono stati aggiunti in risposta a un caldo eventi della CPU.</li></ul>|  
|memory_object_address|**varbinary(8)**|Indirizzo dell'oggetto memoria associato al nodo. Vi è una relazione a [DM os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).memory_object_address.|  
|memory_clerk_address|**varbinary(8)**|Indirizzo del clerk di memoria associato al nodo. Vi è una relazione a [DM os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).memory_clerk_address.|  
|io_completion_worker_address|**varbinary(8)**|Indirizzo del thread di lavoro assegnato al completamento I/O per il nodo. Vi è una relazione a [DM os_workers](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).worker_address.|  
|memory_node_id|**smallint**|ID del nodo di memoria al quale questo nodo appartiene. Relazione molti-a-uno con [sys.dm_os_memory_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md).memory_node_id.|  
|cpu_affinity_mask|**bigint**|Bitmap che identifica le CPU alle quali questo nodo è associato.|  
|online_scheduler_count|**smallint**|Numero di utilità di pianificazione online gestite da questo nodo.|  
|idle_scheduler_count|**smallint**|Numero di utilità di pianificazione online che non dispongono di thread di lavoro attivi.|  
|active_worker_count|**int**|Numero di thread di lavoro attivi su tutte le utilità di pianificazione gestite da questo nodo.|  
|avg_load_balance|**int**|Media del numero di attività per utilità di pianificazione su questo nodo.|  
|timer_task_affinity_mask|**bigint**|Bitmap che identifica le utilità di pianificazione che possono avere attività di timer assegnate.|  
|permanent_task_affinity_mask|**bigint**|Bitmap che identifica le utilità di pianificazione che possono avere attività permanenti assegnate.|  
|resource_monitor_state|**bit**|A ogni nodo viene assegnato un monitoraggio risorse. Il monitoraggio risorse può essere in esecuzione o inattivo. Il valore 1 indica che è in esecuzione, il valore 0 indica che è inattivo.|  
|online_scheduler_mask|**bigint**|Identifica la maschera di affinità del processo per questo nodo.|  
|processor_group|**smallint**|Identifica il gruppo di processori per questo nodo.|  
|cpu_count |**int** |Numero di CPU disponibili per questo nodo. |
|pdw_node_id|**int**|L'identificatore per il nodo in questa distribuzione.<br /><br /> **Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permissions

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], è necessario il `VIEW DATABASE STATE` autorizzazione nel database.   

## <a name="see-also"></a>Vedere anche    
 [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
