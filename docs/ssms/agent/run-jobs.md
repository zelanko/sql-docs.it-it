---
title: Esecuzione di processi
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, manually running
- multiserver job processing [SQL Server]
- jobs [SQL Server Agent], manually running
- manual job processing [SQL Server]
ms.assetid: cd445949-dc10-42fc-8785-4db74c9723ad
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2927502310511e55cba942184d019d2151ee2069
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246460"
---
# <a name="run-jobs"></a>Esecuzione di processi
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Per gestire i processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, è possibile utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] oppure oggetti SMO ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects).  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione|Argomento|  
|-|-|  
|Viene illustrato come avviare l'esecuzione di un processo di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Start a Job](../../ssms/agent/start-a-job.md)|  
|Viene illustrato come arrestare un processo di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Stop a Job](../../ssms/agent/stop-a-job.md)|  
|Viene illustrato come disabilitare o abilitare un processo di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)|  
  
## <a name="see-also"></a>Vedere anche  
[sysdownloadlist](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)  
  
