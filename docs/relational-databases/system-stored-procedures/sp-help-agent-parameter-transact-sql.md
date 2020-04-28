---
title: sp_help_agent_parameter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_parameter
- sp_help_agent_parameter_TSQL
helpviewer_keywords:
- sp_help_agent_parameter
ms.assetid: 8fb4a9c3-19af-4a34-8004-572729ba3d15
author: stevestein
ms.author: sstein
ms.openlocfilehash: 398e1eebbb269fa1f1507725fefff820c5174f58
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771507"
---
# <a name="sp_help_agent_parameter-transact-sql"></a>sp_help_agent_parameter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Restituisce tutti i parametri di un profilo dall'MSagent_parameters &#40;tabella di sistema [&#41;Transact-SQL](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) . Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione in cui l'agente è in esecuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_agent_parameter [ [ @profile_id = ] profile_id ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @profile_id = ] profile_id`ID del profilo dal [MSagent_parameters &#40;tabella&#41;Transact-SQL](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) . *profile_id* è di **tipo int**e il valore predefinito è **-1**, che restituisce tutti i parametri.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|ID del profilo agente.|  
|**parameter_name**|**sysname**|Nome del parametro.|  
|**value**|**nvarchar(255)**|Valore del parametro.|  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_help_agent_parameter** viene utilizzato in tutti i tipi di replica.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **replmonitor** possono eseguire **sp_help_agent_parameter**.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzare i profili degli agenti di replica](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [sp_add_agent_parameter &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_drop_agent_parameter &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
