---
title: syscollector_collection_items (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_collection_items_TSQL
- syscollector_collection_items
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_collection_items view
- add data collector view
ms.assetid: a279ecd1-a59c-4315-9f08-bf221f00a465
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c24af2de8be7656ece793c17c051ff59ae5c8fa1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730155"
---
# <a name="syscollector_collection_items-transact-sql"></a>syscollector_collection_items (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Restituisce informazioni su un elemento di un set di raccolta.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**collection_set_id**|**int**|Identifica il set di raccolta. Non ammette i valori Null.|  
|**collection_item_id**|**int**|Identifica un elemento del set di raccolta. Non ammette i valori Null.|  
|**collector_type_uid**|**uniqueidentifier**|GUID utilizzato per identificare il tipo agente di raccolta dati. Non ammette i valori Null.|  
|**nome**|**nvarchar(4000)**|Nome del set di raccolta. Ammette i valori Null.|  
|**frequenza**|**int**|La frequenza con cui i dati sono raccolti da un elemento della raccolta. Non ammette i valori Null.|  
|**parameters**|**xml**|Descrive la parametrizzazione per il tipo di agente di raccolta associato all'elemento della raccolta. Il XML Schema per questo elemento della raccolta viene convalidato con lo schema XML (XSD) archiviato nel **parameter_schema** per un tipo di agente di raccolta specifico. Ammette i valori Null. Per ulteriori informazioni, vedere [syscollector_collector_types &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md).|  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede SELECT per **dc_operator**, **dc_proxy**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure dell'agente di raccolta dati &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Viste dell'agente di raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)  
  
  
