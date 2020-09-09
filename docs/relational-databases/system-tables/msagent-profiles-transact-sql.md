---
description: MSagent_profiles (Transact-SQL)
title: MSagent_profiles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagent_profiles
- MSagent_profiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_profiles system table
ms.assetid: 4ab1b2ae-b6d9-42b7-9b31-98547dbb7f99
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2f9b44e872ef5175d07a679c330b7662ff9e5bf6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540911"
---
# <a name="msagent_profiles-transact-sql"></a>MSagent_profiles (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSagent_profiles** contiene una riga per ogni profilo di agente di replica definito. Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|ID del profilo.|  
|**profile_name**|**sysname**|Nome di profilo univoco per il tipo di agente.|  
|**agent_type**|**int**|Tipo di agente:<br /><br /> **1** = agente di snapshot<br /><br /> **2** = agente di lettura log<br /><br /> **3** = agente di distribuzione<br /><br /> **4** = agente di merge<br /><br /> **9** = agente di lettura coda|  
|**type**|**int**|Tipo di profilo:<br /><br /> **0** = sistema**1** = personalizzato|  
|**description**|**nvarchar (3000)**|Descrizione del profilo.|  
|**def_profile**|**bit**|Indica se il profilo corrisponde al profilo predefinito per il tipo di agente specificato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
