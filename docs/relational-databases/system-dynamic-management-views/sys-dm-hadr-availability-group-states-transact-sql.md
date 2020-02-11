---
title: sys. dm_hadr_availability_group_states (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_availability_group_states
- sys.dm_hadr_availability_group_states_TSQL
- dm_hadr_availability_group_states_TSQL
- dm_hadr_availability_group_states
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_group_states dynamic management view
ms.assetid: d18019dd-f8dc-4492-b035-b1a639369b65
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 91efefbdc28480cf2a3b3fb579dba0946dba8a2e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67900770"
---
# <a name="sysdm_hadr_availability_group_states-transact-sql"></a>sys.dm_hadr_availability_group_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni gruppo di disponibilità Always On che dispone di una replica di disponibilità nell'istanza locale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di. Ogni riga visualizza gli stati che definiscono l'integrità di un determinato gruppo di disponibilità.  
  
> [!NOTE]  
>  Per ottenere l'elenco completo di, eseguire una query sulla vista del catalogo [sys. availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identificatore univoco del gruppo di disponibilità.|  
|**primary_replica**|**varchar (128)**|Nome dell'istanza del server che ospita la replica primaria corrente.<br /><br /> Null = Non la replica primaria o impossibile comunicare con il cluster di failover WSFC.|  
|**primary_recovery_health**|**tinyint**|Indica l'integrità di recupero della replica primaria, uno di:<br /><br /> 0 = in corso<br /><br /> 1 = Online<br /><br /> NULL<br /><br /> Nelle repliche secondarie il **primary_recovery_health** colonna è null.|  
|**primary_recovery_health_desc**|**nvarchar (60)**|Descrizione di **primary_replica_health**, uno di:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**secondary_recovery_health**|**tinyint**|Indica lo stato di ripristino di una replica secondaria, uno dei seguenti:<br /><br /> 0 = in corso<br /><br /> 1 = Online<br /><br /> NULL<br /><br /> Nella replica primaria la colonna **secondary_recovery_health** è null.|  
|**secondary_recovery_health_desc**|**nvarchar (60)**|Descrizione di **secondary_recovery_health**, uno di:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**synchronization_health**|**tinyint**|Riflette un rollup del **synchronization_health** di tutte le repliche di disponibilità nel gruppo di disponibilità. Di seguito sono riportati i valori possibili e le relative descrizioni.<br /><br /> 0: non integro. Nessuna delle repliche di disponibilità dispone di un **synchronization_health** integro (2 = integro).<br /><br /> 1: parzialmente integro. Il valore relativo all'integrità di sincronizzazione di alcune repliche di disponibilità, ma non di tutte, è integro.<br /><br /> 2: integro. Il valore relativo all'integrità di sincronizzazione di ogni replica di disponibilità è integro.<br /><br /> Per informazioni sull'integrità della sincronizzazione della replica, vedere la **synchronization_health** colonna in [sys. dm_hadr_availability_replica_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md).|  
|**synchronization_health_desc**|**nvarchar (60)**|Descrizione di **synchronization_health**, uno di:<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Funzioni e DMV di Gruppi di disponibilità AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
