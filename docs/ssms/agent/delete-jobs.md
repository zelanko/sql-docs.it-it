---
title: Eliminare processi | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 17caad6946157983d25aa3d16a05395a5aed5a80
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67687869"
---
# <a name="delete-jobs"></a>eliminare processi
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Un processo è una serie specificata di operazioni eseguite in sequenza tramite SQL Server Agent. Per impostazione predefinita, i processi non vengono eliminati al termine dell'esecuzione. È possibile eliminare uno o più processi di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, indipendentemente dall'esito positivo o negativo del processo. È inoltre possibile configurare [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per eliminare automaticamente determinati processi in caso di esito positivo, esito negativo o completamento.  
  
Per impostazione predefinita, i membri del ruolo predefinito del server **sysadmin** possono eseguire la stored procedure di sistema [sp_delete_job (Transact-SQL)](https://msdn.microsoft.com/b85db6e4-623c-41f1-9643-07e5ea38db09) per eliminare un processo. Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
I membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_delete_job** per l'eliminazione di qualsiasi processo. Se un utente non è un membro del ruolo predefinito del server **sysadmin** , può eliminare solo i processi di sua proprietà.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|||  
|-|-|  
|**Descrizione**|**Argomento**|  
|Informazioni su come eliminare uno o più processi di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Eliminare uno o più processi](../../ssms/agent/delete-one-or-more-jobs.md)|  
|Informazioni su come configurare [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per eliminare automaticamente determinati processi in caso di esito positivo, esito negativo o completamento.|[Automatically Delete a Job](../../ssms/agent/automatically-delete-a-job.md)|  
  
