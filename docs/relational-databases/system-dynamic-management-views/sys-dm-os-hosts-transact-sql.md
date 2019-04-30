---
title: sys.dm_os_hosts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_hosts_TSQL
- dm_os_hosts
- dm_os_hosts_TSQL
- sys.dm_os_hosts
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_hosts dynamic management view
ms.assetid: a313ff3b-1fe9-421e-b94b-cea19c43b0e5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43083d569ca8f06571ce52445b2a2d9c2bb6178e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63047855"
---
# <a name="sysdmoshosts-transact-sql"></a>sys.dm_os_hosts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce tutti gli host registrati in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa vista restituisce inoltre le risorse utilizzate da tali host.  
  
> [!NOTE]  
>  Per chiamare questo elemento dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oppure [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], usare il nome **sys.dm_pdw_nodes_os_hosts**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**host_address**|**varbinary(8)**|Indirizzo di memoria interna dell'oggetto host.|  
|**type**|**nvarchar(60)**|Tipo di componente hosted. Ad esempio,<br /><br /> SOSHOST_CLIENTID_SERVERSNI= Interfaccia di SQL Server Native<br /><br /> SOSHOST_CLIENTID_SQLOLEDB = Provider OLE DB di SQL Server Native Client<br /><br /> SOSHOST_CLIENTID_MSDART = Esecuzione Microsoft Data Access|  
|**name**|**nvarchar(32)**|Nome dell'host.|  
|**enqueued_tasks_count**|**int**|Numero totale di attività inserite nelle code di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dall'host.|  
|**active_tasks_count**|**int**|Numero di attività in esecuzione inserite nelle code dall'host.|  
|**completed_ios_count**|**int**|Numero totale di I/O eseguiti e completati tramite l'host.|  
|**completed_ios_in_bytes**|**bigint**|Numero totale di byte degli I/O eseguiti tramite l'host.|  
|**active_ios_count**|**int**|Numero totale di richieste di I/O relative all'host in attesa di essere completate.|  
|**default_memory_clerk_address**|**varbinary(8)**|Indirizzo di memoria dell'oggetto clerk di memoria associato all'host. Per altre informazioni, vedere [DM os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo in questa distribuzione.|  
  
## <a name="permissions"></a>Permissions

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], è necessario il `VIEW DATABASE STATE` autorizzazione nel database.   

## <a name="remarks"></a>Note  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente ai componenti, ad esempio un provider OLE DB, che non fanno parte del file eseguibile di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di allocare memoria e partecipare a una pianificazione in modalità non preemptive. Tali componenti sono ospitati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e tutte le risorse allocate da tali componenti vengono rilevate. L'hosting consente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di tenere traccia delle risorse utilizzate dai componenti esterni al file eseguibile di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
|From|Per|Relazione|  
|----------|--------|------------------|  
|sys.dm_os_hosts. default_memory_clerk_address|sys.dm_os_memory_clerks. memory_clerk_address|Uno-a-uno|  
|sys.dm_os_hosts. host_address|sys.dm_os_memory_clerks. host_address|Uno-a-uno|  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene determinata la quantità totale di memoria di cui un componente hosted ha eseguito il commit.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
```  
SELECT h.type, SUM(mc.pages_kb) AS commited_memory  
FROM sys.dm_os_memory_clerks AS mc   
INNER JOIN sys.dm_os_hosts AS h   
    ON mc.memory_clerk_address = h.default_memory_clerk_address  
GROUP BY h.type;  
```  
  
## <a name="see-also"></a>Vedere anche  

 [sys.dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


