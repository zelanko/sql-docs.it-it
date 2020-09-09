---
description: sp_help_agent_profile (Transact-SQL)
title: sp_help_agent_profile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_profile
- sp_help_agent_profile_TSQL
helpviewer_keywords:
- sp_help_agent_profile
ms.assetid: 5637b671-4aa3-497e-9a1c-c99798a1afb4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7bcb9de7480bf0aea92f585cfece47cf09545195
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538857"
---
# <a name="sp_help_agent_profile-transact-sql"></a>sp_help_agent_profile (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Visualizza il profilo di un agente specificato. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_agent_profile [ [ @agent_type = ] agent_type ]   
    [ , [ @profile_id = ] profile_id ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @agent_type = ] agent_type` Tipo di agente. *agent_type* è di **tipo int**e il valore predefinito è **0**. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**1**|agente snapshot|  
|**2**|Agente di lettura log|  
|**3**|Agente di distribuzione|  
|**4**|Agente di merge|  
|**9**|Agente di lettura coda|  
  
`[ @profile_id = ] profile_id` ID del profilo da visualizzare. *profile_id* è di **tipo int**e il valore predefinito è **-1**, che restituisce tutti i profili nella tabella **MSagent_profiles** .  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|ID del profilo.|  
|**profile_name**|**sysname**|Nome univoco per il tipo di agente.|  
|**agent_type**|**int**|**1** = agente di snapshot<br /><br /> **2** = agente di lettura log<br /><br /> **3** = agente di distribuzione<br /><br /> **4** = agente di merge<br /><br /> **9** = agente di lettura coda|  
|**Tipo**|**int**|**0** = sistema<br /><br /> **1** = personalizzato|  
|**description**|**varchar (3000)**|Descrizione del profilo.|  
|**def_profile**|**bit**|Indica se il profilo corrisponde al profilo predefinito per il tipo di agente specificato.|  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_help_agent_profile** viene utilizzato in tutti i tipi di replica.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **replmonitor** possono eseguire **sp_help_agent_profile**.  
  
## <a name="see-also"></a>Vedere anche  
 [Usare i profili agenti di replica](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
