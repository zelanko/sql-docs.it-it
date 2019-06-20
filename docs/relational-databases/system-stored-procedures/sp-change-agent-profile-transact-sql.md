---
title: sp_change_agent_profile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_agent_profile
- sp_change_agent_profile_TSQL
helpviewer_keywords:
- sp_change_agent_profile
ms.assetid: e73acf8d-0be8-4197-ba11-fe798d0e2820
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ee80fbdac31d58cdb4b4b4b60c61be01670ad65a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62993880"
---
# <a name="spchangeagentprofile-transact-sql"></a>sp_change_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifiche di un parametro di un profilo dell'agente di replica archiviato nella [MSagent_profiles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) tabella. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_change_agent_profile [ @profile_id = ] profile_id   
        , [ @property = ] 'property'   
        , [ @value = ] 'value'   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @profile_id = ] profile_id` È l'ID del profilo. *profile_id* viene **int**, non prevede alcun valore predefinito.  
  
`[ @property = ] 'property'` È il nome della proprietà. *proprietà* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @value = ] 'value'` È il nuovo valore della proprietà. *valore* viene **nvarchar(3000)** , non prevede alcun valore predefinito.  
  
 Nella tabella seguente vengono descritte le proprietà del profilo che è possibile modificare.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**description**|Descrizione del profilo.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_change_agent_profile** viene utilizzata in tutti i tipi di replica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_change_agent_profile**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
