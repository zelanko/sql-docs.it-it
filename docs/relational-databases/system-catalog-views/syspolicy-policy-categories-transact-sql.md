---
title: syspolicy_policy_categories (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_categories
- syspolicy_policy_categories_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_groups view
ms.assetid: 65f080c7-771f-4cf6-a7a0-88882c637f8d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: af9086ba9de7d9c61bcedecd4331e7e0e77d6489
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68121116"
---
# <a name="syspolicy_policy_categories-transact-sql"></a>syspolicy_policy_categories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza una riga per ogni categoria di criteri della gestione basata su criteri nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando è presente un numero elevato di criteri, le categorie ne semplificano l'organizzazione. Nella tabella seguente vengono descritte le colonne contenute nella vista syspolicy_policy_groups.  
 
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|policy_category_id|**int**|Identificatore della categoria di criteri.|  
|name|**sysname**|Nome della categoria di criteri.|  
|mandate_database_subscriptions|**bit**|Indica se la categoria di criteri si applica a tutti i database in un'istanza senza una sottoscrizione esplicita (1) o se la categoria di criteri deve essere applicata a un database tramite una sottoscrizione esplicita (0).|  
  
## <a name="remarks"></a>Osservazioni  
 Consente di visualizzare un elenco di gruppi di criteri di gestione basata su criteri.  
  
## <a name="permissions"></a>Autorizzazioni  
 È necessaria l'appartenenza al ruolo PolicyAdministratorRole nel database msdb.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione di server tramite la gestione basata su criteri](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Viste della gestione basata su criteri &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
