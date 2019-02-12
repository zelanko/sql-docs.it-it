---
title: sys.pdw_loader_backup_runs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 067a39c807b546bc8364bab05d0423f86407a625
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56014511"
---
# <a name="syspdwloaderbackupruns-transact-sql"></a>sys.pdw_loader_backup_runs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene informazioni sul backup in corso e completate e operazioni di ripristino nella [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]e ai backup in corso e completate, ripristino, nonché operazioni di caricamento in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Le informazioni vengono mantenute tra un riavvio di sistema e l'altro.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Identificatore univoco per un backup specifico, ripristino o esecuzione test di carico.<br /><br /> Chiave per questa visualizzazione.||  
|NAME|**nvarchar(255)**|Null per il carico. Nome facoltativo per il backup o ripristino.||  
|submit_time|**datetime**|Ora di che invio della richiesta.||  
|start_time|**datetime**|Ora di avvio dell'operazione.||  
|end_time|**datetime**|Ora dell'operazione completato, non è riuscita o è stata annullata.||  
|total_elapsed_time|**int**|Tempo totale trascorso tra l'ora corrente e start_time o tra start_time ed end_time che sono state completate, esecuzione, annullati o non riusciti.|Se total_elapsed_time supera il valore massimo per un numero intero (24,8 giorni in millisecondi), si verificherà errore materialization a causa un overflow.<br /><br /> Il valore massimo in millisecondi è equivalente a 24,8 giorni.|  
|operation_type|**nvarchar(16)**|Il tipo di carico.|'BACKUP', 'LOAD', 'RESTORE'|  
|mode|**nvarchar(16)**|La modalità di all'interno del tipo di esecuzione.|Per operation_type = **BACKUP**<br />**DIFFERENTIAL**<br />**FULL**<br /><br /> Per operation_type = **carico**<br />**APPEND**<br />**RELOAD**<br />**UPSERT**<br /><br /> Per operation_type = **ripristinare**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|Nome del database che rappresenta il contesto di questa operazione||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|ID dell'utente che richiede l'operazione.||  
|session_id|**nvarchar(32)**|ID della sessione dell'esecuzione dell'operazione.|Vedere ID_sessione [DM pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|request_id|**nvarchar(32)**|ID della richiesta di esecuzione dell'operazione. Per i carichi, si tratta della richiesta corrente o l'ultima associata a questo tipo di caricamento...|Vedere in request_id [DM pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|status|**nvarchar(16)**|Stato dell'esecuzione.|'ANNULLATO', 'COMPLETED', 'NON RIUSCITA', 'QUEUED', 'IN ESECUZIONE'|  
|Stato di avanzamento|**int**|Percentuale di completamento.|da 0 a 100|  
|comando|**nvarchar(4000)**|Testo completo del comando inviato dall'utente.|Verrà troncato se più di 4000 caratteri (da spazi).|  
|rows_processed|**bigint**|Numero di righe elaborate come parte di questa operazione.||  
|rows_rejected|**bigint**|Numero di righe rifiutate come parte di questa operazione.||  
|rows_inserted|**bigint**|Numero di righe inserite nella tabella/e di database come parte di questa operazione.||  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste del catalogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
