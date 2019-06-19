---
title: 'Mirroring del database: Interoperabilità e coesistenza (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2f38e7bac91c4d65e9c6209d693a598466096069
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62807307"
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>Mirroring del database: interoperabilità e coesistenza (SQL Server)
  È possibile utilizzare il mirroring del database con i componenti e le funzionalità seguenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [Istanze del Cluster di Failover AlwaysOn (SQL Server Failover Clustering)](database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [Change Data Capture (e rilevamento delle modifiche)](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [Snapshot di database](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
-   [Cataloghi full-text](database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [Log shipping](database-mirroring-and-log-shipping-sql-server.md)  
  
-   [Replica](database-mirroring-and-replication-sql-server.md)  
  
 Il mirroring del database non consente di interoperare con gli elementi seguenti:  
  
-   Transazioni tra database e transazioni distribuite  
  
     Per altre informazioni sui motivi per cui queste transazioni non sono supportate, vedere [Transazioni tra database non supportate per il mirroring del database o i gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Mirroring del database &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
