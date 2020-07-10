---
title: sys. dm_pdw_dms_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f87d950f4fe876e6b04e1df1f529d22126058113
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197124"
---
# <a name="sysdm_pdw_dms_external_work-transact-sql"></a>sys. dm_pdw_dms_external_work (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]vista di sistema che include informazioni su tutti i passaggi del servizio di spostamento dei dati (DMS) per le operazioni esterne.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Query che sta utilizzando il thread di lavoro DMS.<br /><br /> request_id, step_index e dms_step_index formano la chiave per questa visualizzazione.|Uguale a request_id in [sys. dm_pdw_exec_requests &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Passaggio della query che richiama questo thread di lavoro DMS.<br /><br /> request_id, step_index e dms_step_index formano la chiave per questa visualizzazione.|Uguale a step_index in [sys. dm_pdw_request_steps &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Passaggio corrente del piano DMS.<br /><br /> request_id, step_index e dms_step_index formano la chiave per questa visualizzazione.|Uguale a dms___step_index in [sys. dm_pdw_dms_workers &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md).|  
|pdw_node_id|**int**|Nodo che esegue il ruolo di lavoro DMS.|Uguale a node_id in [sys. dm_pdw_nodes &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|tipo|**nvarchar(60)**|Tipo di operazione esterna eseguita dal nodo.<br /><br /> Il FILE SPLIT è un'operazione eseguita su un file Hadoop esterno che è stato suddiviso in più piccole cadute.|' FILE SPLIT '|  
|work_id|**int**|ID divisione del file.|Maggiore o uguale a 0.<br /><br /> Univoco per ogni nodo di calcolo.|  
|input_name|**nvarchar(60)**|Nome della stringa per l'input da leggere.|Per un file Hadoop, si tratta del nome del file Hadoop.|  
|read_location|**bigint**|Offset della posizione di lettura.||  
|estimated_bytes_processed|**bigint**|Numero di byte elaborati dal thread di lavoro.|Maggiore o uguale a 0.|  
|length|**bigint**|Numero di byte nella suddivisione del file.<br /><br /> Per Hadoop, si tratta della dimensione del blocco HDFS.|Definito dall'utente. Il valore predefinito è 64 MB.|  
|status|**nvarchar(32)**|Stato del ruolo di lavoro.|In sospeso, elaborazione, completato, non riuscito, interrotto|  
|start_time|**datetime**|Ora di inizio dell'esecuzione del thread di lavoro.|Maggiore o uguale all'ora di inizio del passaggio della query a cui appartiene il ruolo di lavoro. Vedere [sys. dm_pdw_request_steps &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Ora in cui l'esecuzione è terminata, non riuscita o è stata annullata.|NULL per i ruoli di lavoro in corso o in coda. In caso contrario, maggiore di start_time.|  
|total_elapsed_time|**int**|Tempo totale impiegato per l'esecuzione, in millisecondi.|Maggiore o uguale a 0.<br /><br /> Se total_elapsed_time supera il valore massimo per un numero intero, total_elapsed_time continuerà a essere il valore massimo. Questa condizione genererà l'avviso "è stato superato il valore massimo".<br /><br /> Il valore massimo in millisecondi equivale a 24,8 giorni.|  
  
 Per informazioni sul numero massimo di righe mantenute da questa visualizzazione, vedere la sezione metadati nell'argomento [limiti di capacità](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) .
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
