---
title: TRACES (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- traces
- sys.traces_TSQL
- sys.traces
- traces_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.traces catalog view
ms.assetid: 4a03be22-b7da-4e2a-97ff-94bed890a620
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 147c080df688ff02d133e725b1ac310439a68eb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126683"
---
# <a name="systraces-transact-sql"></a>sys.traces (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **TRACES** vista del catalogo contiene le tracce correnti in esecuzione nel sistema. In questa vista è da intendersi come una sostituzione per il **fn_trace_getinfo** (funzione).  
  
 Per un elenco completo degli eventi di traccia supportati, vedere [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] In alternativa, utilizzare le viste del catalogo di Eventi estesi.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID della traccia.|  
|**status**|**int**|Stato della traccia:<br /><br /> 0 = arrestato<br /><br /> 1 = in esecuzione|  
|**path**|**nvarchar(260)**|Percorso del file di traccia. Il valore è Null quando la traccia è una traccia di un set di righe.|  
|**max_size**|**bigint**|Dimensioni massime in megabyte (MB) per il file di traccia. Il valore è Null quando la traccia è una traccia di un set di righe.|  
|**stop_time**|**datetime**|Ora di arresto dell'esecuzione della traccia.|  
|**max_files**|**int**|Numero massimo di file di rollover. Il valore è Null se il numero massimo non è impostato.|  
|**is_rowset**|**bit**|1 = traccia di un set di righe.|  
|**is_rollover**|**bit**|1 = l'opzione di rollover è abilitata.|  
|**is_shutdown**|**bit**|1 = l'opzione di chiusura è abilitata.|  
|**is_default**|**bit**|1 = traccia predefinita.|  
|**buffer_count**|**int**|Numero di buffer in memoria utilizzati dalla traccia.|  
|**buffer_size**|**int**|Dimensioni di ogni buffer (KB).|  
|**file_position**|**bigint**|Ultimo percorso del file di traccia. Il valore è Null quando la traccia è una traccia di un set di righe.|  
|**reader_spid**|**int**|ID sessione del lettore di traccia del set di righe. Il valore è Null quando la traccia è una traccia di un file.|  
|**start_time**|**datetime**|Ora di inizio della traccia.|  
|**last_event_time**|**datetime**|Ora di generazione dell'ultimo evento.|  
|**event_count**|**bigint**|Numero totale di eventi generati.|  
|**dropped_event_count**|**int**|Numero totale di eventi eliminati.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.trace_categories &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [sys.trace_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [sys.trace_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [sys.trace_event_bindings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [sys.trace_subclass_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
