---
title: sp_update_agent_profile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_update_agent_profile_TSQL
- sp_update_agent_profile
helpviewer_keywords:
- sp_update_agent_profile
ms.assetid: cc81f227-0df3-4151-bb4d-4f45ea997b71
author: stevestein
ms.author: sstein
ms.openlocfilehash: 730f996a35e7ea2e31518322d710b197cf31f38b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73632821"
---
# <a name="sp_update_agent_profile-transact-sql"></a>sp_update_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiorna il profilo utilizzato da un agente di replica. La stored procedure viene eseguita nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_update_agent_profile [@agent_type=] agent_type, [ @agent_id= ] agent_id, [ @profile_id= ] profile_id  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @agent_type = ] 'agent_type'`Tipo di agente. *agent_type* è di **tipo int**e non prevede alcun valore predefinito. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**1**|Agente snapshot.|  
|**2**|Agente di lettura log.|  
|**3**|Agente di distribuzione.|  
|**4**|Agente di merge.|  
|**9**|Agente di lettura coda.|  
  
`[ @agent_id = ] 'agent_id'`ID dell'agente. *agent_id* è di **tipo int**e non prevede alcun valore predefinito.  
  
`[ @profile_id = ] 'profile_id'`ID del profilo che deve essere utilizzato dall'agente. *profile_id* è di **tipo int**e non prevede alcun valore predefinito. Per visualizzare un elenco dei profili definiti per ogni agente, utilizzare [sp_help_agent_profile &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Per ulteriori informazioni sui profili di sistema, vedere [profili degli agenti di replica](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_update_agent_profile** viene utilizzato in tutti i tipi di replica.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_update_agent_profile**.  
  
## <a name="see-also"></a>Vedere anche  
 [Profili degli agenti di replica](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
