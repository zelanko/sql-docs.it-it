---
description: sys. dm_pdw_os_event_logs (Transact-SQL)
title: sys. dm_pdw_os_event_logs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 11e33ec6a9ca52ed2ca5b67906fc710922df26e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474736"
---
# <a name="sysdm_pdw_os_event_logs-transact-sql"></a>sys. dm_pdw_os_event_logs (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Include informazioni sui diversi registri eventi di Windows nei diversi nodi.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Nodo del dispositivo da cui è presente il log.<br /><br /> pdw_node_id e log_name formano la chiave per questa visualizzazione.||  
|log_name|**nvarchar(255)**|Nome del registro eventi di Windows.<br /><br /> pdw_node_id e log_name formano la chiave per questa visualizzazione.||  
|log_source|**nvarchar(255)**|Nome dell'origine del registro eventi di Windows.||  
|event_id|**int**|ID dell'evento. Non univoco.||  
|event_type|**nvarchar(255)**|Tipo dell'evento, che identifica la gravità.|' Information ',' Warning ',' Error '|  
|event_message|**nvarchar(4000)**|Dettagli dell'evento.||  
|generate_time|**datetime**|Ora di creazione dell'evento.||  
|write_time|**datetime**|Ora in cui l'evento è stato scritto nel log.||  
  
 Per informazioni sul numero massimo di righe mantenute da questa visualizzazione, vedere la sezione metadati nell'argomento [limiti di capacità](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) . 
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel data warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
