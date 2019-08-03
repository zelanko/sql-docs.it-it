---
title: sp_add_agent_parameter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_add_agent_parameter_TSQL
- sp_add_agent_parameter
helpviewer_keywords:
- sp_add_agent_parameter
ms.assetid: 055f4765-0574-47c3-bf7d-6ef6e9bd8b34
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c1aafa1736ff626f7b0bea9bea8753ae2c509ac4
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770956"
---
# <a name="spaddagentparameter-transact-sql"></a>sp_add_agent_parameter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Aggiunge un nuovo parametro e il relativo valore a un profilo agente. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_agent_parameter [ @profile_id = ] profile_id  
        , [ @parameter_name = ] 'parameter_name'   
        , [ @parameter_value = ] 'parameter_value'   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @profile_id = ] profile_id`ID del profilo dalla tabella **MSagent_profiles** nel database **msdb** . *profile_id* è di **tipo int**e non prevede alcun valore predefinito.  
  
 Per individuare il tipo di agente rappresentato da questo *profile_id* , trovare il *profile_id* nella [tabella &#40;Transact-SQL&#41; MSagent_profiles](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) e prendere nota del valore del campo *agent_type* . Sono disponibili i valori seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|agente snapshot|  
|**2**|Agente di lettura log|  
|**3**|Agente di distribuzione|  
|**4**|Agente di merge|  
|**9**|Agente di lettura coda|  
  
`[ @parameter_name = ] 'parameter_name'`Nome del parametro. *parameter_name* è di **tipo sysname**e non prevede alcun valore predefinito. Per un elenco dei parametri già definiti nei profili di sistema, vedere [profili degli agenti di replica](../../relational-databases/replication/agents/replication-agent-profiles.md). Per un elenco completo dei parametri validi per ogni agente, vedere gli argomenti seguenti:  
  
-   [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [Agente lettura log repliche](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [Agente merge repliche](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Agente di lettura coda repliche](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
`[ @parameter_value = ] 'parameter_value'`Valore da assegnare al parametro. *parameter_value* è di **tipo nvarchar (255)** e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_add_agent_parameter** viene utilizzata per la replica snapshot, la replica transazionale e la replica di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_add_agent_parameter**.  
  
## <a name="see-also"></a>Vedere anche  
 [Usare i profili agenti di replica](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Profili degli agenti di replica](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_change_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
