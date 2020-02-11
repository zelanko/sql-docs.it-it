---
title: sys. dm_os_memory_objects (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: a3d0691a82607a207a64f4a6c7ed8c937f052abc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73983082"
---
# <a name="sysdm_os_memory_objects-transact-sql"></a>sys.dm_os_memory_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Vengono restituiti gli oggetti di memoria attualmente allocati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile utilizzare **sys. dm_os_memory_objects** per analizzare l'utilizzo della memoria e identificare le possibili perdite di memoria.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**memory_object_address**|**varbinary (8)**|Indirizzo dell'oggetto memoria. Non ammette i valori Null.|  
|**parent_address**|**varbinary (8)**|Indirizzo dell'oggetto memoria padre. Ammette i valori Null.|  
|**pages_allocated_count**|**int**|**Si applica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] : [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]da a.<br /><br /> Numero di pagine allocate dall'oggetto. Non ammette i valori Null.|  
|**pages_in_bytes**|**bigint**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive.<br /><br /> Quantità di memoria in byte allocata tramite questa istanza dell'oggetto memoria. Non ammette i valori Null.|  
|**creation_options**|**int**|Solo per uso interno. Ammette i valori Null.|  
|**bytes_used**|**bigint**|Solo per uso interno. Ammette i valori Null.|  
|**tipo**|**nvarchar (60)**|Tipo di oggetto memoria.<br /><br /> Indica un componente a cui appartiene l'oggetto memoria oppure la funzione dell'oggetto memoria. Ammette i valori Null.|  
|**nome**|**varchar (128)**|Solo per uso interno. Ammette valori Null.|  
|**memory_node_id**|**smallint**|ID di un nodo di memoria utilizzato dall'oggetto memoria. Non ammette i valori Null.|  
|**creation_time**|**datetime**|Solo per uso interno. Ammette i valori Null.|  
|**max_pages_allocated_count**|**int**|**Si applica a** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] : [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]da a.<br /><br /> Numero massimo di pagine allocate dall'oggetto memoria. Non ammette i valori Null.|  
|**page_size_in_bytes**|**int**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive.<br /><br /> Dimensioni in byte delle pagine allocate dall'oggetto. Non ammette i valori Null.|  
|**max_pages_in_bytes**|**bigint**|Quantità massima di memoria utilizzata da questo oggetto memoria. Non ammette i valori Null.|  
|**page_allocator_address**|**varbinary (8)**|Indirizzo di memoria dell'allocatore di pagine. Non ammette i valori Null. Per ulteriori informazioni, vedere [sys. dm_os_memory_clerks &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**creation_stack_address**|**varbinary (8)**|Solo per uso interno. Ammette i valori Null.|  
|**sequence_num**|**int**|Solo per uso interno. Ammette i valori Null.|  
|**partition_type**|**int**|Tipo di partizione:<br /><br /> 0: oggetto memoria non partizionabile<br /><br /> 1-oggetto memoria partizionabile, attualmente non partizionato<br /><br /> 2-oggetto memoria partizionabile, partizionato per nodo NUMA. In un ambiente con un singolo nodo NUMA equivale a 1.<br /><br /> 3: oggetto memoria partizionabile, partizionato in base alla CPU.|  
|**contention_factor**|**reale**|Valore che specifica la contesa in questo oggetto di memoria, con 0 che significa nessuna contesa. Il valore viene aggiornato ogni volta che viene eseguito un numero specificato di allocazioni di memoria che riflette la contesa durante tale periodo. Si applica solo agli oggetti di memoria thread-safe.|  
|**waiting_tasks_count**|**bigint**|Numero di attese in questo oggetto memoria. Questo contatore viene incrementato ogni volta che viene allocata memoria da questo oggetto memoria. L'incremento indica il numero di attività attualmente in attesa di accesso a questo oggetto memoria. Si applica solo agli oggetti di memoria thread-safe. Si tratta di un valore del massimo sforzo senza una garanzia di correttezza.|  
|**exclusive_access_count**|**bigint**|Specifica la frequenza con cui è stato eseguito l'accesso esclusivo a questo oggetto di memoria. Si applica solo agli oggetti di memoria thread-safe.  Si tratta di un valore del massimo sforzo senza una garanzia di correttezza.|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificatore del nodo su cui si trova questa distribuzione.|  
  
 **partition_type**, **contention_factor**, **waiting_tasks_count**e **exclusive_access_count** non sono ancora implementate in [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
## <a name="permissions"></a>Autorizzazioni

In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]è richiesta `VIEW SERVER STATE` l'autorizzazione.   
Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, richiede l' `VIEW DATABASE STATE` autorizzazione nel database. Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli standard e Basic, richiede l' **amministratore del server** o un account **amministratore Azure Active Directory** .   

## <a name="remarks"></a>Osservazioni  
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
  [SQL Server viste a gestione dinamica relative al sistema operativo &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys. dm_os_memory_clerks &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)  
  
  


