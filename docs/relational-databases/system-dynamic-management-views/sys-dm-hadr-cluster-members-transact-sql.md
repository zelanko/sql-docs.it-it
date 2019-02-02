---
title: Sys.dm_hadr_cluster_members (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster_members_TSQL
- sys.dm_hadr_cluster_members
- dm_hadr_cluster_members_TSQL
- dm_hadr_cluster_members
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_members catalog view
ms.assetid: feb20b3a-8835-41d3-9a1c-91d3117bc170
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e19451a24d35e63fa84a17d409d19b5c9b02ccc3
ms.sourcegitcommit: 7c052fc969d0f2c99ad574f99076dc1200d118c3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2019
ms.locfileid: "55570724"
---
# <a name="sysdmhadrclustermembers-transact-sql"></a>sys.dm_hadr_cluster_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Se il nodo WSFC che ospita un'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abilitata per [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] dispone di quorum WSFC, restituisce una riga per ogni membro che costituisce il quorum e lo stato di ognuno di essi. Inclusi tutti i nodi del cluster (restituiti con il tipo CLUSTER_ENUM_NODE dal **Clusterenum** funzione) e il disco o la condivisione file di controllo, se presente. La riga restituita per un determinato membro contiene informazioni sullo stato di quel membro. Ad esempio, per un cluster con cinque nodi con quorum di maggioranza dei nodi in cui un nodo è inattivo, se **sys.dm_hadr_cluster_members** viene eseguita una query da un'istanza del server che è abilitato per [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] che risiede in un nodo quorum **sys.dm_hadr_cluster_members** riflette lo stato del nodo inattivo come "NODE_DOWN".  
  
 Se il nodo WSFC non dispone di quorum, non viene restituita alcuna riga.  
  
 Utilizzare questa DMV per rispondere alle domande seguenti:  
  
-   Quali nodi sono attualmente in esecuzione nel cluster WSFC?  
  
-   Quanti errori può ancora tollerare il cluster WSFC prima di perdere il quorum in uno scenario con nodi di maggioranza?  

 > [!TIP]
 > A partire da [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], questa vista a gestione dinamica supporta Cluster di istanze di Failover AlwaysOn oltre ai gruppi di disponibilità AlwaysOn.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|Nome del membro che può essere un nome computer, una lettera di unità o un percorso di condivisione file.|  
|**member_type**|**tinyint**|Tipo di membro, uno di:<br /><br /> 0 = Nodo WSFC<br /><br /> 1 = Disco di controllo<br /><br /> 2 = Condivisione file di controllo<br /><br /> 3 = cloud di controllo|  
|**member_type_desc**|**nvarchar(50)**|Descrizione della **member_type**, uno di:<br /><br /> CLUSTER_NODE<br /><br /> DISK_WITNESS<br /><br /> FILE_SHARE_WITNESS<br /><br /> CLOUD_WITNESS|  
|**member_state**|**tinyint**|Stato del membro, uno di:<br /><br /> 0 = Offline<br /><br /> 1 = Online|  
|**member_state_desc**|**nvarchar(60)**|Descrizione della **member_state**, uno di:<br /><br /> UP<br /><br /> VERSO IL BASSO|  
|**number_of_quorum_votes**|**tinyint**|Numero di voti quorum che possiede questo membro del quorum. Per Nessuna maggioranza: Quorum solo disco, il valore predefinito è 0. Per altri tipi di quorum, il valore predefinito è 1.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="examples"></a>Esempi  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e DMV di Gruppi di disponibilità AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Viste del catalogo dei gruppi di disponibilità AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
