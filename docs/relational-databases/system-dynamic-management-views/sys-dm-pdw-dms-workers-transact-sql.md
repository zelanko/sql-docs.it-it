---
title: sys.dm_pdw_dms_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 96fd36d1710a166285fecba092735c7d2495271e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62690452"
---
# <a name="sysdmpdwdmsworkers-transact-sql"></a>sys.dm_pdw_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene informazioni su tutti i ruoli di lavoro completato i passaggi di migrazione del database.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Query che fanno parte di questo ruolo di lavoro del servizio migrazione del database.<br /><br /> request_id step_index e dms_step_index formano la chiave per questa visualizzazione.|Vedere in request_id [DM pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Questo ruolo di lavoro DMS fa parte del passaggio di query.<br /><br /> request_id step_index e dms_step_index formano la chiave per questa visualizzazione.|Vedere in step_index [DM pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Passaggio nel piano di servizio migrazione del database che è in esecuzione il thread di lavoro.<br /><br /> request_id step_index e dms_step_index formano la chiave per questa visualizzazione.||  
|pdw_node_id|**int**|Nodo su cui è in esecuzione il ruolo di lavoro.|Vedere node_id nelle [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**Int**|Distribuzione che esegue il ruolo di lavoro, se presente.|Vedere in distribution_id [sys.pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md).|  
|Tipo|**nvarchar(32)**|Tipo di thread di lavoro DMS che questa voce rappresenta.|'DIRECT_CONVERTER', 'DIRECT_READER', 'FILE_READER', 'HASH_CONVERTER', 'HASH_READER', 'ROUNDROBIN_CONVERTER', 'EXPORT_READER', 'EXTERNAL_READER', 'EXTERNAL_WRITER', 'PARALLEL_COPY_READER', 'REJECT_WRITER', 'WRITER'|  
|status|**nvarchar(32)**|Stato del servizio migrazione del database.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|Velocità effettiva di lettura o scrittura nell'ultimo secondo.|Maggiore o uguale a 0. NULL se la query è stata annullata o non riuscita prima di eseguire il ruolo di lavoro.|  
|bytes_processed|**bigint**|Numero totale di byte elaborati dal thread di lavoro.|Maggiore o uguale a 0. NULL se la query è stata annullata o non riuscita prima di eseguire il ruolo di lavoro.|  
|rows_processed|**bigint**|Numero di righe lette o scritte per questo ruolo di lavoro.|Maggiore o uguale a 0. NULL se la query è stata annullata o non riuscita prima di eseguire il ruolo di lavoro.|  
|start_time|**datetime**|Ora di inizio esecuzione del thread di lavoro.|Maggiore o uguale all'ora di inizio di questo ruolo di lavoro a cui appartiene il passaggio della query. Visualizzare [DM pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Ora in cui l'esecuzione è terminata, non è riuscita o è stata annullata.|NULL per i ruoli di lavoro in corso o in coda. In caso contrario, maggiore start_time.|  
|total_elapsed_time|**int**|Tempo totale impiegato per l'esecuzione, in millisecondi.|Maggiore o uguale a 0.<br /><br /> Tempo totale trascorso dal sistema avviare o riavviare. Se total_elapsed_time supera il valore massimo per un numero intero (24,8 giorni in millisecondi), si verificherà errore materialization a causa un overflow.<br /><br /> Il valore massimo in millisecondi è equivalente a 24,8 giorni.|  
|cpu_time|**bigint**|Tempo di CPU utilizzato dal thread di lavoro, in millisecondi.|Maggiore o uguale a 0.|  
|query_time|**int**|Periodo di tempo prima che SQL inizia a restituire righe al thread, in millisecondi.|Maggiore o uguale a 0.|  
|buffers_available|**int**|Numero di buffer inutilizzate.| NULL se la query è stata annullata o non riuscita prima di eseguire il ruolo di lavoro.|  
|sql_spid|**int**|Id di sessione nell'istanza di SQL Server esegue il lavoro per questo ruolo di lavoro del servizio migrazione del database.||  
|dms_cpid|**int**|ID del thread effettivo in esecuzione.||  
|error_id|**nvarchar(36)**|Identificatore univoco dell'errore verificatosi durante l'esecuzione del thread di lavoro, se presente.|Vedere in error_id [DM pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|source_info|**nvarchar(4000)**|Per un lettore, la specifica delle tabelle di origine e delle colonne.||  
|destination_info|**nvarchar(4000)**|Per un writer, specifica di tabelle di destinazione.||  
  
 Per informazioni sul numero massimo di righe mantenuto da questa vista, vedere la sezione di metadati nel [limiti di capacità](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) argomento...  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
