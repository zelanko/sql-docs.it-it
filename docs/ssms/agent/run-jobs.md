---
description: Esecuzione di processi
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
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 6ab1b3da4bfb0d897698f5ceb0a220453a12e985
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478832"
---
# <a name="run-jobs"></a>Esecuzione di processi
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte ma non tutte le funzionalità di SQL Server Agent. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di SQL di Azure e SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Per gestire i processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, è possibile utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] oppure oggetti SMO ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects).  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione|Argomento|  
|-|-|  
|Viene illustrato come avviare l'esecuzione di un processo di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Avviare un processo](../../ssms/agent/start-a-job.md)|  
|Viene illustrato come arrestare un processo di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Stop a Job](../../ssms/agent/stop-a-job.md)|  
|Viene illustrato come disabilitare o abilitare un processo di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)|  
  
## <a name="see-also"></a>Vedere anche  
[sysdownloadlist](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)  
