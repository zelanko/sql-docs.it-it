---
title: sys.pdw_loader_backup_run_details (Transact-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 328d949afc548b179f26ba83f06348ccb72cbe1f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025342"
---
# <a name="syspdwloaderbackuprundetails-transact-sql"></a>sys.pdw_loader_backup_run_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene inoltre informazioni dettagliate, oltre le informazioni contenute in [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md), sul backup in corso e completate e operazioni di ripristino nella [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e su in corso completate e backup, ripristino e operazioni di caricamento in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Le informazioni vengono mantenute tra un riavvio di sistema e l'altro.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Identificatore univoco per un backup specifico o un ripristino eseguito.<br /><br /> run_id e pdw_node_id formano la chiave per questa visualizzazione.||  
|pdw_node_id|**int**|Identificatore univoco di un nodo dell'appliance per il quale questo record contiene dettagli.<br /><br /> run_id e pdw_node_id formano la chiave per questa visualizzazione.|Vedere node_id nelle [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|status|**nvarchar(16)**|Lo stato corrente dell'esecuzione.|'ANNULLATO', 'COMPLETED', 'NON RIUSCITA', 'QUEUED', 'IN ESECUZIONE'|  
|start_time|**datetime**|Ora di inizio dell'operazione su questo nodo particolare.||  
|end_time|**datetime**|Ora in corrispondenza del quale l'operazione è terminata in questo nodo particolare, se presente.||  
|total_elapsed_time|**int**|Tempo totale che l'operazione è in esecuzione su questo nodo particolare.|Se total_elapsed_time supera il valore massimo per un numero intero (24,8 giorni in millisecondi), si verificherà errore materialization a causa un overflow.<br /><br /> Il valore massimo in millisecondi è equivalente a 24,8 giorni.|  
|Stato di avanzamento|**int**|Stato di avanzamento dell'operazione espressa come percentuale.|da 0 a 100|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste del catalogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
