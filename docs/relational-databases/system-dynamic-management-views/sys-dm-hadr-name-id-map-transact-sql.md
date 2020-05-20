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
ms.openlocfilehash: ef571a14c0d4679930f04ed0353231ba5a0c44aa
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827939"
---
# <a name="sysdm_hadr_name_id_map-transact-sql"></a>sys.dm_hadr_name_id_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
  
  
