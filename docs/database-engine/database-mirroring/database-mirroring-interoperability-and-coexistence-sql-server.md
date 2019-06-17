---
title: 'Mirroring del database: Interoperabilità e coesistenza (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: d7de380dda9f76f82269177282888038bf73a928
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801273"
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>Mirroring del database: interoperabilità e coesistenza (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile utilizzare il mirroring del database con i componenti e le funzionalità seguenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [Istanze del cluster di failover Always On (Clustering di failover SQL Server)](../../database-engine/database-mirroring/database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [Change Data Capture (e rilevamento delle modifiche)](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [Snapshot di database](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
-   [Cataloghi full-text](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [Log shipping](../../database-engine/database-mirroring/database-mirroring-and-log-shipping-sql-server.md)  
  
-   [Replica](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)  
  
 Il mirroring del database non consente di interoperare con gli elementi seguenti:  
  
-   Transazioni tra database e transazioni distribuite  
  
     Per altre informazioni sui motivi per cui queste transazioni non sono supportate, vedere [Transazioni tra database non supportate per il mirroring del database o i gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
