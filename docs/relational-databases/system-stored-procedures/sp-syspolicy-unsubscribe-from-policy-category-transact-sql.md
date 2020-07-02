---
title: sp_syspolicy_unsubscribe_from_policy_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_unsubscribe_from_policy_category_TSQL
- sp_syspolicy_unsubscribe_from_policy_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_unsubscribe_from_policy_category
ms.assetid: 47abab63-e605-40e8-a54e-2241e2e01afd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d606cbca53810eaa9e19153e5de8b821391b2659
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752774"
---
# <a name="sp_syspolicy_unsubscribe_from_policy_category-transact-sql"></a>sp_syspolicy_unsubscribe_from_policy_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Elimina una sottoscrizione di categoria di criteri per il database corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syspolicy_unsubscribe_from_policy_category [ @policy_category = ] 'policy_category'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @policy_category = ] 'policy_category'`Nome della sottoscrizione di categoria di criteri che si desidera eliminare. *policy_category* è di **tipo sysname**ed è obbligatorio.  
  
 Per ottenere i valori per *policy_category*, eseguire una query sulla vista di sistema msdb.dbo.syspolicy_policy_categories.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 È necessario eseguire sp_syspolicy_unsubscribe_from_policy_category nel contesto del database in cui si desidera rimuovere la sottoscrizione di categoria di criteri.  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede l'appartenenza al ruolo predefinito del database db_owner.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminata una sottoscrizione della categoria di criteri 'Finance' del database specificato.  
  
```  
USE <database_name>;  
  
EXEC sys.sp_syspolicy_unsubscribe_from_policy_category @policy_category = N'Finance';  
  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la gestione basata su criteri &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_subscribe_to_policy_category &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-syspolicy-subscribe-to-policy-category-transact-sql.md)  
  
  
