---
title: sys.dm_pdw_os_event_logs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 44a24b12c284cf253838bc1c2252e4081b8efe98
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657235"
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contiene informazioni riguardanti l'evento di Windows diverso accede in nodi diversi.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Nodo di Appliance che proviene questo log.<br /><br /> pdw_node_id e nome_registro formano la chiave per questa visualizzazione.||  
|log_name|**nvarchar(255)**|Nome registro eventi di Windows.<br /><br /> pdw_node_id e nome_registro formano la chiave per questa visualizzazione.||  
|log_source|**nvarchar(255)**|Nome di origine del registro eventi di Windows.||  
|event_id|**int**|ID dell'evento. Non deve essere univoco.||  
|event_type|**nvarchar(255)**|Tipo dell'evento, che identifica la gravità.|'Information', 'Warning', 'Error'|  
|event_message|**nvarchar(4000)**|Dettagli dell'evento.||  
|generate_time|**datetime**|Ora di che creazione dell'evento.||  
|write_time|**datetime**|Ora che dell'evento è stato effettivamente scritti nel log.||  
  
 Per informazioni sul numero massimo di righe mantenuto da questa vista, vedere la sezione di metadati nel [limiti di capacità](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) argomento. 
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
