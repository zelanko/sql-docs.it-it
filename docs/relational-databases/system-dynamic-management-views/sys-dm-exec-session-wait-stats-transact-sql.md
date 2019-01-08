---
title: DM exec_session_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_session_wait_stats
- sys.dm_exec_session_wait_stats_tsql
- dm_exec_session_wait_stats
- dm_exec_session_wait_stats_tsql
helpviewer_keywords:
- sys.dm_exec_session_wait_stats
ms.assetid: df84842a-71eb-4fda-b448-5953cf9985dc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 89054576eb64a913e67bf3ae9a3f53d0c79eb48f
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206610"
---
# <a name="sysdmexecsessionwaitstats-transact-sql"></a>sys.dm_exec_session_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni su tutte le attese rilevate dai thread eseguiti per ogni sessione. È possibile utilizzare questa vista per diagnosticare problemi di prestazioni con il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sessione e anche con query e batch specifici.  Questa vista restituisce sessione le stesse informazioni che vengono aggregate per [DM os_wait_stats &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) ma fornisce il **session_id** anche numero.  
  
**Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|L'id della sessione.|  
|wait_type|**nvarchar(60)**|Nome del tipo di attesa. Per altre informazioni, vedere [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|  
|waiting_tasks_count|**bigint**|Numero di attese del tipo specificato. Questo contatore viene incrementato all'inizio di ogni attesa.|  
|wait_time_ms|**bigint**|Tempo di attesa totale, espresso in millisecondi, per il tipo di attesa specifico. Il tempo comprende signal_wait_time_ms.|  
|max_wait_time_ms|**bigint**|Tempo di attesa massimo per il tipo di attesa specifico.|  
|signal_wait_time_ms|**bigint**|Differenza tra il momento in cui è stato rilevato il thread in attesa e quello in cui è stata avviata l'esecuzione del thread.|  
  
## <a name="remarks"></a>Note  
 Questa DMV viene reimpostato le informazioni per una sessione quando viene aperta la sessione oppure quando la sessione viene reimpostata (se il pool di connessioni),  
  
 Per informazioni sui tipi di attesa, vedere [DM os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Se l'utente dispone **VIEW SERVER STATE** autorizzazione per il server, è possibile visualizzare le sessioni in esecuzione tutte nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; in caso contrario, l'utente verrà visualizzato solo nella sessione corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
 
