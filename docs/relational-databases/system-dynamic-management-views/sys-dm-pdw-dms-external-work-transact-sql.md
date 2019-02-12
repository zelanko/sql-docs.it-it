---
title: sys.dm_pdw_dms_external_work (Transact-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 9e79803a1c06a78f67a37a6a669af1c5ab4683f5
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56021567"
---
# <a name="sysdmpdwdmsexternalwork-transact-sql"></a>sys.dm_pdw_dms_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] vista di sistema che contiene informazioni su tutti i passaggi di Data Movement Service (DMS) per operazioni esterne.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Query che utilizza questo ruolo di lavoro del servizio migrazione del database.<br /><br /> request_id step_index e dms_step_index formano la chiave per questa visualizzazione.|Uguale a request_id nel [DM pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Passaggio della query che richiama questo ruolo di lavoro del servizio migrazione del database.<br /><br /> request_id step_index e dms_step_index formano la chiave per questa visualizzazione.|Uguale a step_index nel [DM pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Passaggio nel piano di servizio migrazione del database corrente.<br /><br /> request_id step_index e dms_step_index formano la chiave per questa visualizzazione.|Uguale a dms___step_index nel [DM pdw_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md).|  
|pdw_node_id|**int**|Nodo che esegue il ruolo di lavoro del servizio migrazione del database.|Uguale allo node_id nelle [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|Tipo|**nvarchar(60)**|Tipo di operazione esterna che questo nodo è in esecuzione.<br /><br /> FILE SPLIT è un'operazione su un file Hadoop esterno che è stata suddivisa in più si trova più piccoli.|'SPLIT FILE'|  
|work_id|**int**|Il file split ID.|Maggiore o uguale a 0.<br /><br /> Deve essere univoco per ogni nodo di calcolo.|  
|input_name|**nvarchar(60)**|Stringa del nome per l'input da leggere.|Per un file di Hadoop, si tratta del nome di file Hadoop.|  
|read_location|**bigint**|Offset della posizione di lettura.||  
|estimated_bytes_processed|**bigint**|Numero di byte elaborati dal thread di lavoro.|Maggiore o uguale a 0.|  
|length|**bigint**|Numero di byte nel file di divisione.<br /><br /> Per Hadoop, questa è la dimensione del blocco di HDFS.|Definito dall'utente. Il valore predefinito è 64 MB.|  
|status|**nvarchar(32)**|Stato del ruolo di lavoro.|In sospeso, l'elaborazione, operazione eseguita, non è riuscita, interrotto|  
|start_time|**datetime**|Ora di inizio esecuzione del thread di lavoro.|Maggiore o uguale all'ora di inizio di questo ruolo di lavoro a cui appartiene il passaggio della query. Visualizzare [DM pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Ora in cui l'esecuzione è terminata, non è riuscita o è stata annullata.|NULL per i ruoli di lavoro in corso o in coda. In caso contrario, maggiore start_time.|  
|total_elapsed_time|**int**|Tempo totale impiegato per l'esecuzione, in millisecondi.|Maggiore o uguale a 0.<br /><br /> Se total_elapsed_time supera il valore massimo per un numero intero, total_elapsed_time continuerà a essere il valore massimo. Questa condizione verrà generato l'avviso "il valore massimo è stato superato."<br /><br /> Il valore massimo in millisecondi è equivalente a 24,8 giorni.|  
  
 Per informazioni sul numero massimo di righe mantenuto da questa vista, vedere [i valori massimi vista di sistema](https://msdn.microsoft.com/5243f018-2713-45e3-9b61-39b2a57401b9).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
