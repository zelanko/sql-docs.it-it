---
title: sys.dm_pdw_query_stats_xe (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d551241-db35-4958-b60f-55e996f95c1f
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d4ade9fe6cb13ae26823a399678e994edc69a3f8
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020662"
---
# <a name="sysdmpdwquerystatsxe-transact-sql"></a>sys.dm_pdw_query_stats_xe (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Questa DMV è deprecata e verrà rimossa in una versione futura. In questa versione, restituisce 0 righe.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|evento|**nvarchar(60)**|Chiave per questa visualizzazione.||  
|event_id|**nvarchar(36)**|||  
|create_time|**datetime**|||  
|session_id|**int**|L'id della sessione.|Vedere ID_sessione [DM pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|cpu|**int**|||  
|reads|**int**|Numero di letture logiche eseguite dopo l'avvio dell'evento.||  
|writes|**int**|Numero di scritture logiche eseguite dopo l'avvio dell'evento.||  
|sql_text|**nvarchar(4000)**|||  
|client_app_name|**nvarchar(255)**|||  
|tsql_stack|**nvarchar(255)**|||  
|pdw_node_id|**int**|Nodo su cui è in esecuzione questa istanza di Xevent.|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
