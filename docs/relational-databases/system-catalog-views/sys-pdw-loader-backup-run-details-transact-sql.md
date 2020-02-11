---
title: sys. pdw_loader_backup_run_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: dead5962987f7fb132f21bb4e3517f7cc9249601
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127654"
---
# <a name="syspdw_loader_backup_run_details-transact-sql"></a>sys. pdw_loader_backup_run_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene ulteriori informazioni dettagliate, oltre alle informazioni contenute in [sys. pdw_loader_backup_runs &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md), sulle operazioni di backup e ripristino in corso e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] completate in e sulle operazioni di backup, ripristino e caricamento in corso [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]e completate in. Le informazioni vengono mantenute tra un riavvio di sistema e l'altro.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Identificatore univoco per l'esecuzione di un backup o un ripristino specifico.<br /><br /> run_id e pdw_node_id formano la chiave per questa visualizzazione.||  
|pdw_node_id|**int**|Identificatore univoco di un nodo Appliance per il quale questo record include i dettagli.<br /><br /> run_id e pdw_node_id formano la chiave per questa visualizzazione.|Vedere node_id in [sys. dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|status|**nvarchar (16)**|Stato corrente dell'esecuzione.|' CANCELLED ',' COMPLETED ',' FAILED ',' QUEUED ',' RUNNING '|  
|start_time|**datetime**|Ora di inizio dell'operazione su questo nodo specifico.||  
|end_time|**datetime**|Ora in cui l'operazione è terminata in questo nodo specifico, se disponibile.||  
|total_elapsed_time|**int**|Tempo totale in cui l'operazione è stata eseguita in questo nodo specifico.|Se total_elapsed_time supera il valore massimo per un numero intero (24,8 giorni in millisecondi), si verificherà un errore di materializzazione causato da un overflow.<br /><br /> Il valore massimo in millisecondi equivale a 24,8 giorni.|  
|progress|**int**|Stato dell'operazione espressa come percentuale.|Da 0 a 100|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel data warehouse viste del catalogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
