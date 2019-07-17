---
title: sys.dm_os_memory_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_objects
- sys.dm_os_memory_objects
- sys.dm_os_memory_objects_TSQL
- dm_os_memory_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_objects dynamic management view
ms.assetid: 5688bcf8-5da9-4ff9-960b-742b671d7096
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ca3a6a8891e74bd795f15e9a374194650e70b197
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265747"
---
# <a name="sysdmosmemoryobjects-transact-sql"></a>sys.dm_os_memory_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Vengono restituiti gli oggetti di memoria attualmente allocati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile usare **DM os_memory_objects** per analizzare il consumo di memoria e identificare possibili memoria perdite.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**memory_object_address**|**varbinary(8)**|Indirizzo dell'oggetto memoria. Non ammette i valori Null.|  
|**parent_address**|**varbinary(8)**|Indirizzo dell'oggetto memoria padre. Ammette i valori Null.|  
|**pages_allocated_count**|**int**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Numero di pagine allocate dall'oggetto. Non ammette i valori Null.|  
|**pages_in_bytes**|**bigint**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Quantità di memoria in byte allocata tramite questa istanza dell'oggetto memoria. Non ammette i valori Null.|  
|**creation_options**|**int**|Solo per uso interno. Ammette i valori Null.|  
|**bytes_used**|**bigint**|Solo per uso interno. Ammette i valori Null.|  
|**type**|**nvarchar(60)**|Tipo di oggetto memoria.<br /><br /> Indica un componente a cui appartiene l'oggetto memoria oppure la funzione dell'oggetto memoria. Ammette i valori Null.|  
|**name**|**varchar(128)**|Solo per uso interno. Ammette valori Null.|  
|**memory_node_id**|**smallint**|ID di un nodo di memoria utilizzato dall'oggetto memoria. Non ammette i valori Null.|  
|**creation_time**|**datetime**|Solo per uso interno. Ammette i valori Null.|  
|**max_pages_allocated_count**|**int**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Numero massimo di pagine allocate dall'oggetto memoria. Non ammette i valori Null.|  
|**page_size_in_bytes**|**int**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Dimensioni in byte delle pagine allocate dall'oggetto. Non ammette i valori Null.|  
|**max_pages_in_bytes**|**bigint**|Quantità massima di memoria utilizzata da questo oggetto memoria. Non ammette i valori Null.|  
|**page_allocator_address**|**varbinary(8)**|Indirizzo di memoria dell'allocatore di pagine. Non ammette i valori Null. Per altre informazioni, vedere [DM os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**creation_stack_address**|**varbinary(8)**|Solo per uso interno. Ammette i valori Null.|  
|**sequence_num**|**int**|Solo per uso interno. Ammette i valori Null.|  
|**partition_type**|**int**|Il tipo di partizione:<br /><br /> 0 - non partizionabile oggetto memoria<br /><br /> 1 - oggetto memory partizionabile, attualmente non partizionata<br /><br /> 2 - oggetto di memoria partizionabile, partizionato in base al nodo NUMA. In un ambiente con un singolo nodo NUMA ciò equivale a 1.<br /><br /> 3 - oggetto di memoria partizionabile, partizionato in base alla CPU.|  
|**contention_factor**|**real**|Un valore che specifica di contesa per l'oggetto di memoria, con 0, vale a dire senza conflitti. Il valore viene aggiornato ogni volta che un determinato numero di allocazioni di memoria sono stato apportato riflettente contesa durante il periodo specificato. Si applica solo agli oggetti memoria affidabili.|  
|**waiting_tasks_count**|**bigint**|Numero di attese su questo oggetto memoria. Questo contatore viene incrementato ogni volta che la memoria viene allocata da questo oggetto memoria. L'incremento è il numero di attività attualmente in attesa per l'accesso a questo oggetto memoria. Si applica solo agli oggetti memoria affidabili. Questo è un valore di impegno migliore senza una garanzia di correttezza.|  
|**exclusive_access_count**|**bigint**|Specifica la frequenza oggetto memoria ha effettuato l'accesso in modo esclusivo. Si applica solo agli oggetti memoria affidabili.  Questo è un valore di impegno migliore senza una garanzia di correttezza.|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo in questa distribuzione.|  
  
 **partition_type**, **contention_factor**, **waiting_tasks_count**, e **exclusive_access_count** non sono ancora disponibili [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
## <a name="permissions"></a>Permissions

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, è necessario il `VIEW DATABASE STATE` autorizzazione nel database. Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard e i livelli Basic, è necessario il **amministratore del Server** o un' **amministratore di Azure Active Directory** account.   

## <a name="remarks"></a>Note  
 Gli oggetti memoria sono heap. Le allocazioni implementate dagli oggetti sono caratterizzate da una maggiore granularità rispetto alle allocazioni implementate dai clerk di memoria. I componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzano oggetti memoria anziché clerk di memoria. Gli oggetti memoria utilizzano l'interfaccia dell'allocatore di pagine del clerk di memoria per allocare le pagine. Gli oggetti memoria non utilizzano interfacce di memoria virtuale o condivisa. In base al modello di allocazione, i componenti possono creare tipi diversi di oggetti memoria per allocare aree di dimensioni arbitrarie.  
  
 Le dimensioni di pagina tipiche di un oggetto memoria sono pari a 8 KB. Gli oggetti memoria incrementale possono tuttavia avere dimensioni di pagina da 512 byte a 8 KB.  
  
> [!NOTE]  
>  Le dimensioni di pagina non corrispondono a un'allocazione massima. Le dimensioni di pagina corrispondono invece alla granularità dell'allocazione supportata da un allocatore di pagine e implementata da un clerk di memoria. È possibile richiedere allocazioni superiori a 8 KB dagli oggetti memoria.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituita la quantità di memoria allocata per ogni tipo di oggetto memoria.  
  
```  
SELECT SUM (pages_in_bytes) as 'Bytes Used', type   
FROM sys.dm_os_memory_objects  
GROUP BY type   
ORDER BY 'Bytes Used' DESC;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
  [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)  
  
  


