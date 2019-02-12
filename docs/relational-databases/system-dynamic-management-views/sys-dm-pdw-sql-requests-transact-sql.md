---
title: sys.dm_pdw_sql_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 9a99d922dd8b57bb033f2a6ba13560c22c0eff6c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56030812"
---
# <a name="sysdmpdwsqlrequests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene informazioni su tutte le distribuzioni di query di SQL Server come parte di un passaggio SQL nella query.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Identificatore univoco della query a cui appartiene questa distribuzione di query SQL.<br /><br /> request_id step_index e distribution_id formano la chiave per questa visualizzazione.|Vedere in request_id [DM pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Indice del passaggio della query di di che questo tipo di distribuzione fa parte.<br /><br /> request_id step_index e distribution_id formano la chiave per questa visualizzazione.|Vedere in step_index [DM pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|pdw_node_id|**int**|Identificatore univoco del nodo in cui viene eseguita la distribuzione di query.|Vedere node_id nelle [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**int**|Identificatore univoco della distribuzione in cui viene eseguita la distribuzione di query.<br /><br /> request_id step_index e distribution_id formano la chiave per questa visualizzazione.|Vedere in distribution_id [sys.pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md). Impostare su -1 per le richieste eseguite nell'ambito del nodo, non nell'ambito della distribuzione.|  
|status|**nvarchar(32)**|Stato corrente della distribuzione di query.|In sospeso, in esecuzione, non riusciti, annullati, completato, interrotto, CancelSubmitted|  
|error_id|**nvarchar(36)**|Identificatore univoco dell'errore associato con la distribuzione di query, se presente.|Vedere in error_id [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). Se si è verificato alcun errore, impostato su NULL.|  
|start_time|**datetime**|Ora in cui query distribuzione è iniziata l'esecuzione.|Minore o uguale all'ora corrente e maggiore o uguale a start_time del passaggio della query a cui appartiene questa distribuzione delle query|  
|end_time|**datetime**|Ora in corrispondenza del quale questo tipo di distribuzione query completato l'esecuzione, è stata annullata o non è riuscita.|Maggiore o uguale all'ora di inizio o impostato su NULL se la distribuzione di query è in corso o in coda.|  
|total_elapsed_time|**int**|Rappresenta il tempo che di distribuzione delle query è in esecuzione, in millisecondi.|Maggiore o uguale a 0. Uguale al delta di start_time ed end_time che sono state completate, non è riuscita o annullata distribuzioni di query.<br /><br /> Se total_elapsed_time supera il valore massimo per un numero intero, total_elapsed_time continuerà a essere il valore massimo. Questa condizione verrà generato l'avviso "il valore massimo è stato superato."<br /><br /> Il valore massimo in millisecondi è equivalente a 24,8 giorni.|  
|row_count|**bigint**|Numero di righe modificate o lette dalla distribuzione query.|-1 per le operazioni che non cambiano o restituire dati, ad esempio CREATE TABLE e DROP TABLE.|  
|spid|**int**|Id di sessione nell'istanza di SQL Server che esegue la distribuzione delle query.||  
|comando|**nvarchar(4000)**|Testo completo del comando per la distribuzione di query.|Qualsiasi stringa di query o una richiesta valida.|  
  
 Per informazioni sul numero massimo di righe mantenuto da questa vista, vedere la sezione i valori massimi vista di sistema nel [valori minimi e massimi (SQL Server PDW)](https://msdn.microsoft.com/5243f018-2713-45e3-9b61-39b2a57401b9) argomento.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
