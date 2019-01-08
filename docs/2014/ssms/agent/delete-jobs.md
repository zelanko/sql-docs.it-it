---
title: Eliminare processi | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf22e5cdac4d178fe41d3040afe7056f28375603
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52751234"
---
# <a name="delete-jobs"></a>Eliminare processi
  Un processo è una serie specificata di operazioni eseguite in sequenza tramite SQL Server Agent. Per impostazione predefinita, i processi non vengono eliminati al termine dell'esecuzione. È possibile eliminare uno o più processi di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, indipendentemente dall'esito positivo o negativo del processo. È inoltre possibile configurare [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per eliminare automaticamente determinati processi in caso di esito positivo, esito negativo o completamento.  
  
 Per impostazione predefinita, i membri del **sysadmin** ruolo predefinito del server possono eseguire il [sp_delete_job &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql) stored procedure per eliminare un processo di sistema. Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](sql-server-agent-fixed-database-roles.md).  
  
 I membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_delete_job** per l'eliminazione di qualsiasi processo. Se un utente non è un membro del ruolo predefinito del server **sysadmin** , può eliminare solo i processi di sua proprietà.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|||  
|-|-|  
|**Descrizione**|**Argomento**|  
|Informazioni su come eliminare uno o più processi di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Eliminare uno o più processi](delete-one-or-more-jobs.md)|  
|Informazioni su come configurare [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per eliminare automaticamente determinati processi in caso di esito positivo, esito negativo o completamento.|[Automatically Delete a Job](automatically-delete-a-job.md)|  
  
  
