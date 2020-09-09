---
description: sys. dm_pdw_query_stats_xe (Transact-SQL)
title: sys. dm_pdw_query_stats_xe (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d551241-db35-4958-b60f-55e996f95c1f
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 13b09ebe66a759d0c57161c99cfb16864be1b094
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89530351"
---
# <a name="sysdm_pdw_query_stats_xe-transact-sql"></a>sys. dm_pdw_query_stats_xe (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Questa DMV è deprecata e verrà rimossa in una versione futura. In questa versione, restituisce 0 righe.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|event|**nvarchar(60)**|Chiave per questa visualizzazione.||  
|event_id|**nvarchar (36)**|||  
|create_time|**datetime**|||  
|session_id|**int**|ID della sessione.|Vedere session_id in [sys. dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|cpu|**int**|||  
|reads|**int**|Numero di letture logiche dall'inizio dell'evento.||  
|writes|**int**|Numero di scritture logiche dall'inizio dell'evento.||  
|sql_text|**nvarchar(4000)**|||  
|client_app_name|**nvarchar(255)**|||  
|tsql_stack|**nvarchar(255)**|||  
|pdw_node_id|**int**|Nodo in cui è in esecuzione questa istanza XEvent.|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel data warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
