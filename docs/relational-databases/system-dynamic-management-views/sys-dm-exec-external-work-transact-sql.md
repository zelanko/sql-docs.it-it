---
title: sys.dm_exec_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
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
ms.openlocfilehash: 049bf084381adaa0bf7e817eb7ae3bdb24feb118
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097749"
---
# <a name="sysdmexecexternalwork-transact-sql"></a>sys.dm_exec_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Restituisce informazioni sul carico di lavoro per ogni ruolo di lavoro, in ogni nodo di calcolo.  
  
 Eseguire una query sys.dm_exec_external_work per identificare le operazioni attivate per comunicare con l'origine dati esterna (ad esempio Hadoop o esterno di SQL Server).  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|Identificatore univoco per la query PolyBase associata.|Visualizzare *request_ID* nelle [exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|La richiesta è in esecuzione il thread di lavoro.|Visualizzare *step_index* nelle [exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|dms_step_index|**int**|Passaggio nel piano di servizio migrazione del database in esecuzione il thread di lavoro.|Visualizzare [sys.dm_exec_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md).|  
|compute_node_id|**int**|Il nodo ruolo di lavoro è in corso.|Visualizzare [DM exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|type|**nvarchar(60)**|Il tipo di lavoro esterno.|'File suddivisione'|  
|work_id|**int**|ID della suddivisione effettiva.|Maggiore o uguale a 0.|  
|input_name|**nvarchar(4000)**|Nome dell'input da leggere|Nome del file quando si usano Hadoop.|  
|read_location|**bigint**|Offset o leggere la posizione.|Offset del file da leggere.|  
|bytes_processed|**bigint**|Numero totale di byte elaborati dal thread di lavoro.|Maggiore o uguale a 0.|  
|length|**bigint**|Lunghezza della divisione o del blocco HDFS in caso di Hadoop|Definibili dall'utente. Il valore predefinito è 64M|  
|status|**nvarchar(32)**|Stato del ruolo di lavoro|In sospeso, l'elaborazione, operazione eseguita, non è riuscita, interrotto|  
|start_time|**datetime**|Inizio del lavoro||  
|end_time|**datetime**|Fine del lavoro||  
|total_elapsed_time|**int**|Tempo totale espresso in millisecondi||  
  
## <a name="see-also"></a>Vedere anche  
 [PolyBase con DMV di risoluzione dei problemi](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative ai database &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
