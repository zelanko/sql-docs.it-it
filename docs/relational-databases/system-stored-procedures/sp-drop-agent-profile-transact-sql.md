---
description: sp_drop_agent_profile (Transact-SQL)
title: sp_drop_agent_profile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_drop_agent_profile
- sp_drop_agent_profile_TSQL
helpviewer_keywords:
- sp_drop_agent_profile
ms.assetid: b884f9ef-ae89-4cbc-a917-532c3ff6ed41
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d69f685fce04f3a4355fae3dab31900cde4a1c56
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474333"
---
# <a name="sp_drop_agent_profile-transact-sql"></a>sp_drop_agent_profile (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Elimina un profilo dalla tabella **MSagent_profiles** . Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_drop_agent_profile [ @profile_id = ] profile_id  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @profile_id = ] profile_id` ID del profilo da eliminare. *profile_id* è di **tipo int**e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_drop_agent_profile** viene utilizzato in tutti i tipi di replica.  
  
 Anche i parametri del profilo specificato vengono eliminati dalla tabella **MSagent_parameters** .  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_drop_agent_profile**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_agent_profile &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
