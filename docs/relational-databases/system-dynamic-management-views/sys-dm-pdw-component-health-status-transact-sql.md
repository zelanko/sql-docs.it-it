---
description: sys. dm_pdw_component_health_status (Transact-SQL)
title: sys. dm_pdw_component_health_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 68cc3f7a-693c-4d5d-a76b-455352af8d7f
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 755ccebc287d001b6cd2aa3a2989444d510102a5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89531018"
---
# <a name="sysdm_pdw_component_health_status-transact-sql"></a>sys. dm_pdw_component_health_status (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Include informazioni sull'integrità corrente dei componenti dell'appliance.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**||Non NULL|  
|component_id|INT|ID del componente. Vedere [sys. pdw_health_components &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, component_id, property_id e component_instance_id formano la chiave per questa visualizzazione.|Non NULL|  
|property_id|**int**|ID della proprietà. Vedere [sys. pdw_health_component_properties &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md).|NOT NULL|  
|component_instance_id|**nvarchar(255)**|Identifica un'istanza di un componente. Ad esempio, un'istanza di una CPU può essere identificata da component_instance_id =' CPU1'.<br /><br /> pdw_node_id, component_id, property_id e component_instance_id formano la chiave per questa visualizzazione.|NOT NULL|  
|property_value|**nvarchar(255)**|Valore della proprietà corrente.|NULL|  
|update_time|**datetime**|Data e ora dell'ultimo aggiornamento della metrica.|NOT NULL|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel data warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
