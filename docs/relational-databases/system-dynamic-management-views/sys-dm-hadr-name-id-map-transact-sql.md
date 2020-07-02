---
title: sys. dm_hadr_name_id_map (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_name_id_map
- sys.dm_hadr_name_id_map_TSQL
- dm_hadr_name_id_map
- dm_hadr_name_id_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_name_id_map dynamic management view
ms.assetid: e07bb8a9-37de-4a39-a257-950d7c3ae8fb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0bf0e07bd621161a512d7096bff2949039d3ba1b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752841"
---
# <a name="sysdm_hadr_name_id_map-transact-sql"></a>sys.dm_hadr_name_id_map (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Mostra il mapping di Gruppi di disponibilità Always On che l'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stata unita a tre ID univoci: un ID gruppo di disponibilità, un ID risorsa WSFC e un ID gruppo WSFC. Lo scopo di questo mapping è gestire lo scenario in cui il gruppo/risorsa WSFC viene rinominato.  
   
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**ag_name**|**nvarchar(256)**|Nome del gruppo di disponibilità. Nome specificato dall'utente che deve essere univoco all'interno del cluster WSFC (Windows Server Failover Cluster).|  
|**ag_id**|**uniqueidentifier**|Identificatore univoco (GUID) del gruppo di disponibilità.|  
|**ag_resource_id**|**nvarchar(256)**|ID univoco del gruppo di disponibilità come una risorsa nel cluster WSFC.|  
|**ag_group_id**|**nvarchar(256)**|ID gruppo WSFC univoco del gruppo di disponibilità.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica dei gruppi di disponibilità Always On &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Always On viste del catalogo di gruppi di disponibilità &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorare i gruppi di disponibilità &#40;&#41;Transact-SQL](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
