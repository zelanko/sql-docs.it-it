---
title: sys.dm_exec_compute_node_errors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
- DM_EXEC_COMPUTE_NODE_ERRORS
- DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase
- PolyBase, views
- dm_exec_compute_node_errors
- sys.dm_exec_compute_node_errors management view
ms.assetid: 9a03c039-70e4-4974-95d8-d3fa45984ffb
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5a11a5e7090f89f4a31ffd15f8ebbce78ea395a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63013397"
---
# <a name="sysdmexeccomputenodeerrors-transact-sql"></a>sys.dm_exec_compute_node_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Nodi di calcolo di errori restituisce che si verificano in PolyBase.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar(36)**|Id numerico univoco associato all'errore.|Univoco in tutti gli errori di query nel sistema|  
|source|**nvarchar(255)**|Descrizione di processo o thread di origine||  
|type|**nvarchar(255)**|Tipo di errore.||  
|create_time|**datetime**|L'ora dell'occorrenza errore||  
|compute_node_id|**int**|Identificatore del nodo di calcolo specifico|Vedere di compute_node_id [DM exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|  
|rexecution_id|**nvarchar(36)**|Identificatore della query PolyBase, se presente.||  
|spid|**int**|Identificatore della sessione SQL Server||  
|thread_id|**int**|Identificatore numerico del thread su cui si è verificato l'errore.||  
|dettagli|nvarchar(4000)|Descrizione completa dei dettagli dell'errore.||  
  
## <a name="see-also"></a>Vedere anche  
 [PolyBase con DMV di risoluzione dei problemi](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative ai database &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
