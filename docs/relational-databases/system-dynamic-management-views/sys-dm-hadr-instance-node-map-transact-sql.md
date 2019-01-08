---
title: sys.dm_hadr_instance_node_map (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sys.dm_hadr_instance_node_map_TSQL
- sys.sys.dm_hadr_instance_node_map
- sys.dm_hadr_instance_node_map_TSQL
- sys.dm_hadr_instance_node_map
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.sys.dm_hadr_instance_node_map dynamic management view
ms.assetid: ccfaf62c-9f87-43cf-a5e7-8942e91dd041
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e857682f5bb03256b129521840f8969e797e1a5f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535743"
---
# <a name="sysdmhadrinstancenodemap-transact-sql"></a>sys.dm_hadr_instance_node_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Per ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospita una replica di disponibilità che appartiene al gruppo di disponibilità Always On, restituisce il nome del nodo Windows Server Failover Clustering (WSFC) che ospita l'istanza del server. Questa DMV offre i seguenti utilizzi:  
  
-   Questa DMV è utile per il rilevamento di un gruppo di disponibilità con più repliche di disponibilità ospitate nello stesso nodo WSFC. Si tratta di una configurazione non supportata che si potrebbe verificare dopo un failover dell'istanza del cluster di failover se il gruppo di disponibilità non è stato correttamente configurato. Per altre informazioni, vedere [Clustering di failover e gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md).  
  
-   Quando più istanze di SQL Server sono ospitate nello stesso nodo WSFC, tramite la DLL della risorsa viene utilizzata questa DMV per determinare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui connettersi.  
   
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**ag_resource_id**|**nvarchar(256)**|ID univoco del gruppo di disponibilità come una risorsa nel cluster WSFC.|  
|**instance_name**|**nvarchar(256)**|Nome -*server*/*istanza*-di un'istanza del server che ospita una replica del gruppo di disponibilità.|  
|**node_name**|**nvarchar(256)**|Nome del nodo del cluster WSCF.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e DMV di Gruppi di disponibilità AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Viste del catalogo dei gruppi di disponibilità AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Gruppi di disponibilità AlwaysOn di &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
