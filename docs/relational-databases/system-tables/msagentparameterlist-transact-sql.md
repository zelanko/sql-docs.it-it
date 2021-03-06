---
description: MSagentparameterlist (Transact-SQL)
title: MSagentparameterlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs:
- TSQL
helpviewer_keywords:
- Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b5fcded0e1ffe97578832f773e65d2d08e1c41d8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551046"
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSagentparameterlist** contiene informazioni sui parametri dell'agente di replica e viene utilizzata per specificare i parametri che possono essere impostati per un determinato tipo di agente. Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|Tipo di agente:<br /><br /> **1** = agente di snapshot.<br /><br /> **2** = agente di lettura log.<br /><br /> **3** = agente di distribuzione.<br /><br /> **4** = agente di merge.<br /><br /> **9** = agente di lettura coda.|  
|**parameter_name**|**sysname**|Nome di un parametro valido dell'agente.|  
|**default_value**|**nvarchar(4000)**|Valore predefinito del parametro dell'agente, dove NULL indica che non esiste alcun valore predefinito.|  
|**min_value**|**int**|Imposta il limite inferiore per il parametro dell'agente, dove NULL indica che non esiste alcun limite inferiore.|  
|**max_value**|**int**|Imposta il limite superiore per il parametro dell'agente, dove NULL indica che non esiste alcun limite superiore.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
