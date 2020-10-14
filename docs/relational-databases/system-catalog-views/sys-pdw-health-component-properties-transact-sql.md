---
description: sys.pdw_health_component_properties (Transact-SQL)
title: sys.pdw_health_component_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 966c544a42ea97ed6f7233bba1a57979a87ba5ac
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036996"
---
# <a name="syspdw_health_component_properties-transact-sql"></a>sys.pdw_health_component_properties (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Archivia le proprietà che descrivono un dispositivo. Alcune proprietà mostrano lo stato del dispositivo e alcune proprietà descrivono il dispositivo stesso.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificatore univoco della proprietà di un componente.<br /><br /> property_id e component_id formano la chiave per questa visualizzazione.|NOT NULL|  
|component_id|**int**|ID del componente. Vedere [sys.pdw_health_components &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> property_id e component_id formano la chiave per questa visualizzazione.|NOT NULL|  
|property_name|**nvarchar(255)**|Nome della proprietà.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nome della proprietà definito dal produttore.|NOT NULL|  
|is_key|**bit**|Determina se l'istanza del dispositivo è univoca o non univoca.|NOT NULL<br /><br /> 0-l'istanza del dispositivo è univoca.<br /><br /> 1-l'istanza del dispositivo non è univoca.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di Azure Synapse Analytics e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
