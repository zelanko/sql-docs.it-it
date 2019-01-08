---
title: sys.dm_db_xtp_checkpoint_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_stats
- dm_db_xtp_checkpoint_stats_TSQL
- sys.dm_db_xtp_checkpoint_stats
- sys.dm_db_xtp_checkpoint_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_stats dynamic management view
ms.assetid: 8d0b18ca-db4d-4376-9905-3e4457727c46
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fdb255570febc6d37bef824958c15422b6fae733
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52503187"
---
# <a name="sysdmdbxtpcheckpointstats-transact-sql"></a>sys.dm_db_xtp_checkpoint_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Restituisce le statistiche relative alle operazioni checkpoint OLTP in memoria del database corrente. Se il database non include oggetti OLTP in memoria, viene restituito un set di risultati vuoto.  
  
 Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
```  
SELECT * FROM db.sys.dm_db_xtp_checkpoint_stats;  
```  
  
**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] è notevolmente diverso rispetto alle versioni più recenti e viene illustrato più basso nell'argomento relativo alla [SQL Server 2014](#bkmk_2014).**
  
## <a name="includesssql15includessssql15-mdmd-and-later"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e versioni successive  
 Nella tabella seguente vengono descritte le colonne in `sys.dm_db_xtp_checkpoint_stats`, a partire **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]**.  
  
|Nome colonna|Tipo|Descrizione|  
|-----------------|----------|-----------------|  
|last_lsn_processed|**bigint**|Ultimo LSN visualizzato dal controller.|  
|end_of_log_lsn|**Numeric(38)**|LSN di fine del log.|  
|bytes_to_end_of_log|**bigint**|Byte non elaborati dal controller, corrispondenti ai byte tra log `last_lsn_processed` e `end_of_log_lsn`.|  
|log_consumption_rate|**bigint**|Frequenza di utilizzo di log delle transazioni dal controller (in KB/sec).|  
|active_scan_time_in_ms|**bigint**|Tempo trascorso per il controller esegua l'analisi del log delle transazioni.|  
|total_wait_time_in_ms|**bigint**|Tempo di attesa cumulativo per il controller durante l'analisi non eseguita del log.|  
|waits_for_io|**bigint**|Numero di attese dei / o causati dal thread del controller log.|  
|io_wait_time_in_ms|**bigint**|Tempo cumulativo trascorso in attesa dei / o log dal thread del controller.|  
|waits_for_new_log_count|**bigint**|Numero di attese causati dal thread del controller per un nuovo registro da generare.|  
|new_log_wait_time_in_ms|**bigint**|Tempo cumulativo trascorso in attesa di un nuovo log dal thread del controller.|  
|idle_attempts_count|**bigint**|Numero di volte in cui il controller di transizione a uno stato di inattività.|  
|tx_segments_dispatched|**bigint**|Numero di segmenti visto dal controller e di spedizione i serializzatori. Segmento è una contigua parte del log che costituisce un'unità di serializzazione. Attualmente viene ridimensionato a 1MB, ma può cambiare in futuro.|  
|segment_bytes_dispatched|**bigint**|Numero totale di byte di byte inviati dal controller per i serializzatori, poiché il database riavviare.|  
|bytes_serialized|**bigint**|Numero totale di byte serializzati dal riavvio del database.|  
|serializer_user_time_in_ms|**bigint**|Tempo impiegato dai serializzatori in modalità utente.|  
|serializer_kernel_time_in_ms|**bigint**|Tempo impiegato dai serializzatori in modalità kernel.|  
|xtp_log_bytes_consumed|**bigint**|Numero totale di byte di log utilizzati dal riavvio del database.|  
|checkpoints_closed|**bigint**|Numero di checkpoint chiusi perché il database riavviare.|  
|last_closed_checkpoint_ts|**bigint**|Timestamp dell'ultimo checkpoint chiusi.|  
|hardened_recovery_lsn|**Numeric(38)**|Verrà avviato il recupero da questo LSN.|  
|hardened_root_file_guid|**uniqueidentifier**|GUID del file radice che finalizzati in seguito all'ultimo checkpoint completato.|  
|hardened_root_file_watermark|**bigint**|**Interno solo**. Fino a che punto è possibile leggere il file radice fino a (questo è un tipo internamente rilevante solo - denominato BSN).|  
|hardened_truncation_lsn|**Numeric(38)**|LSN del punto di troncamento.|  
|log_bytes_since_last_close|**bigint**|Byte dall'ultima chiusura alla fine corrente del log.|  
|time_since_last_close_in_ms|**bigint**|Tempo trascorso dall'ultima chiusura del checkpoint.|  
|current_checkpoint_id|**bigint**|Attualmente, i nuovi segmenti vengono assegnati a questo checkpoint. Il sistema di checkpoint è una pipeline. Il checkpoint corrente è quello che vengono assegnati a segmenti dal log. Dopo che è stato raggiunto un limite, il checkpoint viene rilasciato il controller e una nuova istanza creata come corrente.|  
|current_checkpoint_segment_count|**bigint**|Numero di segmenti nel checkpoint corrente.|  
|recovery_lsn_candidate|**bigint**|**Internamente solo**. Candidato per essere selezionato come recoverylsn quando current_checkpoint_id viene chiusa.|  
|outstanding_checkpoint_count|**bigint**|Numero di checkpoint nella pipeline in attesa di essere chiuso.|  
|closing_checkpoint_id|**bigint**|ID del punto di arresto di chiusura.<br /><br /> I serializzatori lavorano in parallelo, in modo che una volta effettuato terminati il checkpoint è un candidato per essere chiuso dal thread di chiusura. Ma il thread di chiusura solo possibile chiudere una alla volta e deve essere in ordine, in modo che il checkpoint di chiusura è quella che sta lavorando per il thread di chiusura.|  
|recovery_checkpoint_id|**bigint**|ID del checkpoint da utilizzare per il ripristino.|  
|recovery_checkpoint_ts|**bigint**|Timestamp del checkpoint di ripristino.|  
|bootstrap_recovery_lsn|**Numeric(38)**|LSN recupero per il bootstrap.|  
|bootstrap_root_file_guid|**uniqueidentifier**|GUID del file radice per il bootstrap.|  
|internal_error_code|**bigint**|Errore rilevato da uno qualsiasi dei controller, serializzatore, close e thread di unione.|
|bytes_of_large_data_serialized|**bigint**|La quantità di dati che è stati serializzati. |  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 Nella tabella seguente vengono descritte le colonne in `sys.dm_db_xtp_checkpoint_stats`, per **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**.  
  
|Nome colonna|Tipo|Descrizione|  
|-----------------|----------|-----------------|  
|log_to_process_in_bytes|**bigint**|Numero di byte di log tra il numero di sequenza del file di log (LSN) corrente e la fine del log del thread.|  
|total_log_blocks_processed|**bigint**|Numero complessivo di blocchi di log elaborati dall'avvio del server.|  
|total_log_records_processed|**bigint**|Numero complessivo di record di log elaborati dall'avvio del server.|  
|xtp_log_records_processed|**bigint**|Numero totale di record di log OLTP in memoria elaborati dall'avvio del server.|  
|total_wait_time_in_ms|**bigint**|Tempo di attesa cumulativo in ms.|  
|waits_for_io|**bigint**|Numero di attese per le operazioni di I/O sui log.|  
|io_wait_time_in_ms|**bigint**|Tempo cumulativo trascorso in attesa delle operazioni di I/O sui log.|  
|waits_for_new_log|**bigint**|Numero di attese per la generazione del nuovo log.|  
|new_log_wait_time_in_ms|**bigint**|Tempo cumulativo trascorso in attesa del nuovo log.|  
|log_generated_since_last_checkpoint_in_bytes|**bigint**|Quantità di log generato dall'ultimo checkpoint OLTP in memoria.|  
|ms_since_last_checkpoint|**bigint**|Quantità di tempo, in millisecondi, dall'ultimo checkpoint OLTP in memoria.|  
|checkpoint_lsn|**numerico (38)**|Numero di sequenza del file di log (LSN) di recupero associato all'ultimo checkpoint completato OLTP in memoria.|  
|current_lsn|**numerico (38)**|LSN del record del log attualmente in elaborazione.|  
|end_of_log_lsn|**numerico (38)**|LSN di fine del log.|  
|task_address|**varbinary(8)**|Indirizzo di SOS_Task. Join a sys.dm_os_tasks per ottenere ulteriori informazioni.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione `VIEW DATABASE STATE` per il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Memoria-con ottimizzazione per la tabella viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
