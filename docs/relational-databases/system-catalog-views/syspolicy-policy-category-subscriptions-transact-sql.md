---
description: syspolicy_policy_category_subscriptions (Transact-SQL)
title: syspolicy_policy_category_subscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_category_subscriptions_TSQL
- syspolicy_policy_category_subscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_group_subscriptions view
ms.assetid: b3b3a7d7-0b78-46c0-9755-045f7a5692b9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 99f95e323b88f6932a1f3af0ed3cf72d9bed964c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460511"
---
# <a name="syspolicy_policy_category_subscriptions-transact-sql"></a>syspolicy_policy_category_subscriptions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Visualizza una riga per ogni sottoscrizione di gestione basata su criteri nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ogni riga descrive una coppia di categoria di criteri e destinazione. Nella tabella seguente vengono descritte le colonne contenute nella vista syspolicy_policy_group_subscriptions.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|policy_category_subscription_id|**int**|Identificatore del record.|  
|target_type|**sysname**|Tipo dell'oggetto di database di destinazione della sottoscrizione.|  
|target_object|**sysname**|Nome dell'oggetto di destinazione.|  
|policy_category_id|**int**|ID della categoria di criteri applicata alla destinazione.|  
  
## <a name="remarks"></a>Osservazioni  
 In questa vista vengono visualizzate le destinazioni che hanno sottoscritto le categorie di criteri.  
  
## <a name="permissions"></a>Autorizzazioni  
 È necessaria l'appartenenza al ruolo PolicyAdministratorRole nel database msdb.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare i server tramite la gestione basata su criteri](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Viste di Gestione basata su criteri &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
