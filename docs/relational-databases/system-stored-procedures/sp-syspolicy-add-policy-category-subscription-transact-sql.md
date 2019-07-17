---
title: sp_syspolicy_add_policy_category_subscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_add_policy_category_subscription
- sp_syspolicy_add_policy_category_subscription_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_add_policy_category_subscription
ms.assetid: 4284f550-9a3f-4726-8181-15e407fbf08f
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 795a806b1b945407a2db947f6037c435efe68b56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010507"
---
# <a name="spsyspolicyaddpolicycategorysubscription-transact-sql"></a>sp_syspolicy_add_policy_category_subscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge una sottoscrizione di categoria di criteri al database specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syspolicy_add_policy_category_subscription [ @target_type = ] 'target_type'  
    , [ @target_object = ] 'target_object'  
    , [ @policy_category = ] 'policy_category'  
    [ , [ @policy_category_subscription_id = ] policy_category_subscription_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @target_type = ] 'target_type'` È il tipo di destinazione della sottoscrizione di categoria. *target_type* viene **sysname**è obbligatorio e deve essere impostata su 'DATABASE'.  
  
`[ @target_object = ] 'target_object'` È il nome del database in cui viene eseguita la sottoscrizione alla categoria. *target_object* viene **sysname**ed è obbligatorio.  
  
`[ @policy_category = ] 'policy_category'` È il nome della categoria di criteri da sottoscrivere. *policy_category* viene **sysname**ed è obbligatorio.  
  
 Per ottenere valori per *policy_category*, eseguire query sulla vista di sistema syspolicy_policy_categories.  
  
`[ @policy_category_subscription_id = ] policy_category_subscription_id` È l'identificatore per la sottoscrizione di categoria. *policy_category_subscription_id* viene **int**e viene restituito come OUTPUT.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 È necessario eseguire sp_syspolicy_add_policy_category_subscription nel contesto del database di sistema msdb.  
  
 Se si specifica una categoria di criteri non esistente, verrà creata una nuova categoria di criteri e la sottoscrizione sarà obbligatoria per tutti i database all'esecuzione della stored procedure. Se la sottoscrizione obbligatoria per la nuova categoria viene successivamente cancellata, la sottoscrizione sarà valida solo per il database specificato come *target_object*. Per altre informazioni sulla modifica dell'impostazione di una sottoscrizione obbligatoria, vedere [sp_syspolicy_update_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Questa stored procedure viene eseguita nel contesto del proprietario corrente della stessa.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene configurata la sottoscrizione di una categoria di criteri denominata 'Table Naming Policies' da parte del database specificato.  
  
```  
EXEC msdb.dbo.sp_syspolicy_add_policy_category_subscription @target_type = N'DATABASE'  
, @target_object = N'AdventureWorks2012'  
, @policy_category = N'Table Naming Policies';  
  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure della gestione basata su criteri &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_update_policy_category_subscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-subscription-transact-sql.md)   
 [sp_syspolicy_unsubscribe_from_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql.md)  
  
  
