---
title: sys. dm_os_child_instances (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_child_instances
- sys.dm_os_child_instances_TSQL
- dm_os_child_instances
- dm_os_child_instances_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server state information [SQL Server]
- sys.dm_os_child_instances dynamic management view
- monitoring server health
ms.assetid: 1bef3074-0ccc-48fa-8f3d-14f3d99df86b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 59a58348f5428f568f40d28b4e83bc6bc040647c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67900239"
---
# <a name="sysdm_os_child_instances-transact-sql"></a>sys.dm_os_child_instances (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni istanza utente creata dall'istanza del server padre.  
  
> **IMPORTANTE** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Le informazioni restituite da **sys. dm_os_child_instances** possono essere utilizzate per determinare lo stato di ogni istanza utente (heart_beat) e per ottenere il nome della pipe (instance_pipe_name) che può essere utilizzato per creare una connessione all'istanza utente [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] utilizzando o sqlcmd. È possibile connettersi a un'istanza utente solo dopo che è stata avviata da un processo esterno, ad esempio un'applicazione client. Gli strumenti di gestione di SQL non possono avviare un'istanza utente.  
  
> **Nota:** Le istanze utente sono una funzionalità [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)] di.  
> 
> **Nota** Per chiamare questo oggetto [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] da [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]o, usare il nome **sys. dm_pdw_nodes_os_child_instances**.  
  
|Colonna|Tipo di dati|Descrizione|  
|------------|---------------|-----------------|  
|**owning_principal_name**|**nvarchar(256)**|Nome dell'utente per cui è stata creata l'istanza utente.|  
|owning_principal_sid|nvarchar(256)|ID di sicurezza (SID) dell'entità proprietaria dell'istanza utente. Questo valore corrisponde al SID di Windows.|  
|owning_principal_sid_binary|varbinary(85)|Versione binaria del SID dell'utente proprietario dell'istanza utente|  
|**instance_name**|**nvarchar(128)**|Nome dell'istanza utente.|  
|**instance_pipe_name**|**nvarchar(260)**|Quando si crea un'istanza utente viene creata anche una named pipe a cui possono connettersi le applicazioni. Questo nome può essere utilizzato in una stringa di connessione per connettersi all'istanza utente.|  
|**os_process_id**|**Int**|ID del processo di Windows per l'istanza utente.|  
|**os_process_creation_date**|**DateTime**|Data e ora dell'ultimo avvio di questo processo dell'istanza utente.|  
|**heart_beat**|**nvarchar (5)**|Stato corrente dell'istanza utente, ovvero ALIVE o DEAD.|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificatore del nodo su cui si trova questa distribuzione.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="remarks"></a>Osservazioni  
 Per ulteriori informazioni sulla vista a gestione dinamica, vedere [funzioni e viste a gestione dinamica &#40;&#41;Transact-SQL](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedi anche  
 [Istanze utente per non amministratori](https://msdn.microsoft.com/85385aae-10fb-4f8b-9eeb-cce2ee7da019)  
  
  



