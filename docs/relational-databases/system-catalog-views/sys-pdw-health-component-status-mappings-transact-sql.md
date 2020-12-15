---
description: sys.pdw_health_component_status_mappings (Transact-SQL)
title: sys.pdw_health_component_status_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: d0d5bfea5d43315fed6b74f8767cea6cb89904a9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466942"
---
# <a name="syspdw_health_component_status_mappings-transact-sql"></a>sys.pdw_health_component_status_mappings (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Definisce il mapping tra gli [!INCLUDE[ssDW](../../includes/ssdw-md.md)] stati dei componenti e i nomi dei componenti definiti dal produttore.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificatore univoco della proprietà.<br /><br /> property_id, component_id e physical_name formano la chiave per questa visualizzazione.|NOT NULL|  
|component_id|**int**|ID del componente. Vedere [sys.pdw_health_components &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> property_id, component_id e physical_name formano la chiave per questa visualizzazione.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nome della proprietà definito dal produttore.<br /><br /> property_id, component_id e physical_name formano la chiave per questa visualizzazione.|NOT NULL|  
|logical_name|**nvarchar(255)**|Nome della proprietà definito da [!INCLUDE[ssDW](../../includes/ssdw-md.md)] .|NOT NULL<br /><br /> 0-l'istanza del dispositivo è univoca.<br /><br /> 1-l'istanza del dispositivo non è univoca.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di Azure Synapse Analytics e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
