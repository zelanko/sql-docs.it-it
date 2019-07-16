---
title: sys.dm_pdw_component_health_active_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7378b5f4f87c2511909aef6b75c412b6043e8c71
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899554"
---
# <a name="sysdmpdwcomponenthealthactivealerts-transact-sql"></a>sys.dm_pdw_component_health_active_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Archivia gli avvisi attivi su [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] componenti.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Identificatore univoco di un [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nodo.<br /><br /> pdw_node_id, id_componente, component_instance_id, alert_id e alert_instance_id formano la chiave per questa visualizzazione.|NOT NULL|  
|component_id|**int**|L'ID del componente. Visualizzare [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, id_componente, component_instance_id, alert_id e alert_instance_id formano la chiave per questa visualizzazione.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, id_componente, component_instance_id, alert_id e alert_instance_id formano la chiave per questa visualizzazione.|NOT NULL|  
|alert_id|**int**|L'ID per il tipo di avviso. Visualizzare [sys.pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id, id_componente, component_instance_id, alert_id e alert_instance_id formano la chiave per questa visualizzazione.|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|Identifica un'istanza di un determinato avviso.<br /><br /> pdw_node_id, id_componente, component_instance_id, alert_id e alert_instance_id formano la chiave per questa visualizzazione.|NOT NULL|  
|current_value|**nvarchar(255)**|Utilizzato quando l'avviso è di tipo StatusChange. Questo è lo stato del componente corrente. Valore è NULL per gli avvisi di tipo soglia. Visualizzare [sys.pdw_health_alerts &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) per un elenco dei tipi di avviso.|NULL|  
|previous_value|**nvarchar(255)**|Utilizzato quando l'avviso è di tipo StatusChange. Questo è lo stato del componente precedente. Valore è NULL per gli avvisi di tipo soglia. Visualizzare [sys.pdw_health_alerts &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) per un elenco dei tipi di avviso.|NULL|  
|create_time|**datetime**|Quando è stato generato l'avviso di data e ora.|NOT NULL|  
  
 Per informazioni sul numero massimo di righe mantenuto da questa vista, vedere "Minimo e massimo valori" nel [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
