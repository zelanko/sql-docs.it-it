---
title: resource_governor_workload_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_workload_groups
- resource_governor_workload_groups_TSQL
- sys.resource_governor_workload_groups_TSQL
- resource_governor_workload_groups
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_workload_groups catalog view
ms.assetid: 619ba4b7-868f-4784-b527-ec1dfd703c4f
author: stevestein
ms.author: sstein
ms.openlocfilehash: d0f80d9ba8f5b5a1e81949d0fb2ea4b1d9bca59d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904436"
---
# <a name="sysresourcegovernorworkloadgroups-transact-sql"></a>sys.resource_governor_workload_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce la configurazione memorizzata del gruppo del carico di lavoro in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ogni gruppo del carico di lavoro può essere sottoscritto a un unico pool di risorse.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|group_id|**int**|ID univoco del gruppo del carico di lavoro. Non ammette i valori Null.|  
|name|**sysname**|Nome del gruppo del carico di lavoro. Non ammette i valori Null.|  
|importance|**sysname**|**Nota:** Importanza si applica solo ai gruppi del carico di lavoro nel pool di risorse stesso.<br /><br /> L'importanza relativa di una richiesta in questo gruppo del carico di lavoro. L'importanza è compresa fra le seguenti, MEDIUM è l'impostazione predefinita: LOW, MEDIUM, ELEVATE.<br /><br /> Non ammette i valori Null.|  
|request_max_memory_grant_percent|**int**|Massima concessione di memoria, espressa in percentuale, per una singola richiesta. Il valore predefinito è 25. Non ammette i valori Null.<br /><br /> **Nota:** Se questa impostazione è superiore al 50%, le query di grandi dimensioni verranno eseguite una alla volta. Pertanto, durante l'esecuzione della query c'è maggiore rischio di ricevere un errore di memoria insufficiente.|  
|request_max_cpu_time_sec|**int**|Limite massimo di utilizzo della CPU, in secondi, per un'unica richiesta. Il valore predefinito, 0, non specifica alcun limite. Non ammette i valori Null.<br /><br /> **Nota:** Per altre informazioni, vedere [Classe di evento CPU Threshold Exceeded](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).|  
|request_memory_grant_timeout_sec|**int**|Timeout di concessione di memoria, in secondi, per una singola richiesta. Il valore predefinito, 0 utilizza un calcolo interno basato sul costo della query. Non ammette i valori Null.|  
|max_dop|**int**|Massimo grado di parallelismo per il gruppo del carico di lavoro. Il valore predefinito, 0, utilizza le impostazioni globali. Non ammette i valori Null.<br /><br /> **Nodo:** Questa impostazione ignorerà l'opzione di query **maxdop**.|  
|group_max_requests|**int**|Numero massimo di richieste concorrenti. Il valore predefinito, 0, non specifica alcun limite. Non ammette i valori Null.|  
|pool_id|**int**|ID del pool di risorse utilizzato dal gruppo del carico di lavoro.|  
|external_pool_id|**int**|**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID del pool di risorse esterno che utilizza questo gruppo di carico di lavoro.|  
  
## <a name="remarks"></a>Note  
 La vista del catalogo visualizza i metadati memorizzati. Per visualizzare la configurazione in memoria, usare la vista a gestione dinamica corrispondente [DM resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md).  
  
 La configurazione archiviata e in memoria può essere diversa se è stata modificata la configurazione di Resource Governor senza applicare l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'autorizzazione VIEW ANY DEFINITION per visualizzare i contenuti e l'autorizzazione CONTROL SERVER per modificarli.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Viste del catalogo di Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)  
  
  
