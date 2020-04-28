---
title: sys. dm_exec_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_WORK
- DM_EXEC_EXTERNAL_WORK_TSQL
- SYS.DM_EXEC_EXTERNAL_WORK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_external_work management view
- dm_exec_external_work management view
- PolyBase,views
- PolyBase
ms.assetid: 7597d97b-1fde-4135-ac35-4af12968f300
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b0ba7eecc8e117e429f6992622d0c7bb2073f86a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74834329"
---
# <a name="sysdm_exec_external_work-transact-sql"></a>sys. dm_exec_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Restituisce informazioni sul carico di lavoro per ogni thread di lavoro in ogni nodo di calcolo.  
  
 Eseguire una query su sys. dm_exec_external_work per identificare il lavoro per comunicare con l'origine dati esterna, ad esempio Hadoop o External SQL Server.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|Identificatore univoco per la query di base associata.|Vedere *request_id* in [sys. dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|`int`|Richiesta eseguita dal thread di lavoro.|Vedere *step_index* in [sys. dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|dms_step_index|`int`|Passaggio del piano DMS eseguito dal thread di lavoro.|Vedere [sys. dm_exec_dms_workers &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md).|  
|compute_node_id|`int`|Nodo su cui è in esecuzione il ruolo di lavoro.|Vedere [sys. dm_exec_compute_nodes &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|type|`nvarchar(60)`|Tipo di lavoro esterno.|' File Split '|  
|work_id|`int`|ID della divisione effettiva.|Maggiore o uguale a 0.|  
|input_name|`nvarchar(4000)`|Nome dell'input da leggere|Nome file quando si usa Hadoop.|  
|read_location|`bigint`|Offset o percorso di lettura.|Offset del file da leggere.|  
|bytes_processed|`bigint`|Byte totali allocati per l'elaborazione dei dati da questo thread di lavoro. Questo potrebbe non rappresentare necessariamente i dati totali restituiti dalla query |Maggiore o uguale a 0.|  
|length|`bigint`|Lunghezza del blocco Split o HDFS in caso di Hadoop|Definibile dall'utente. Il valore predefinito è 64M|  
|status|`nvarchar(32)`|Stato del ruolo di lavoro|In sospeso, elaborazione, completato, non riuscito, interrotto|  
|start_time|`datetime`|Inizio del lavoro||  
|end_time|`datetime`|Fine del lavoro||  
|total_elapsed_time|`int`|Tempo totale in millisecondi||
|compute_pool_id|`int`|Identificatore univoco per il pool.|

## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi di polibase con viste a gestione dinamica](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Viste a gestione dinamica e funzioni &#40;&#41;Transact-SQL](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative ai database &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
