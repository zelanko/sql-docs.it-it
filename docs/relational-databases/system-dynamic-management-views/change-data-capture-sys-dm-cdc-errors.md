---
title: sys.dm_cdc_errors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cdc_errors_TSQL
- dm_cdc_errors
- sys.dm_cdc_errors
- sys.dm_cdc_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cdc_errors dynamic management view
- change data capture [SQL Server], error reporting
ms.assetid: 898f2d76-9e63-45ef-94da-8034e86004ab
author: stevestein
ms.author: sstein
ms.openlocfilehash: 506dae205356504c76d47ffe324b82f9f34665f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017998"
---
# <a name="change-data-capture---sysdmcdcerrors"></a>Change Data Capture - DM cdc_errors
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni errore rilevato durante la sessione di analisi dei log di acquisizione dei dati delle modifiche.  
 
 
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID della sessione.<br /><br /> 0 = l'errore non si è verificato all'interno di una sessione di analisi dei log.|  
|**phase_number**|**int**|Numero che indica la fase in cui si trovava la sessione quando si è verificato l'errore. Per una descrizione di ogni fase, vedere [DM cdc_log_scan_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md).|  
|**entry_time**|**datetime**|Data e ora di registrazione dell'errore. Questo valore corrisponde al timestamp nel log degli errori di SQL.|  
|**error_number**|**int**|ID del messaggio di errore.|  
|**error_severity**|**int**|Livello di gravità del messaggio, compreso tra 1 e 25.|  
|**error_state**|**int**|Numero di contesto dell'errore.|  
|**error_message**|**nvarchar(1024)**|Testo del messaggio di errore.|  
|**start_lsn**|**nvarchar(23)**|Valore LSN iniziale delle righe in elaborazione quando si è verificato l'errore.<br /><br /> 0 = l'errore non si è verificato all'interno di una sessione di analisi dei log.|  
|**begin_lsn**|**nvarchar(23)**|Valore LSN iniziale della transazione in elaborazione quando si è verificato l'errore.<br /><br /> 0 = l'errore non si è verificato all'interno di una sessione di analisi dei log.|  
|**sequence_value**|**nvarchar(23)**|Valore LSN delle righe in elaborazione quando si è verificato l'errore.<br /><br /> 0 = l'errore non si è verificato all'interno di una sessione di analisi dei log.|  
  
## <a name="remarks"></a>Note  
 **cdc_errors** contiene informazioni sull'errore per alle 32 sessioni precedenti.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW DATABASE STATE per eseguire query di **DM cdc_errors** vista a gestione dinamica. Per altre informazioni sulle autorizzazioni sulle viste a gestione dinamica, vedere [funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_cdc_log_scan_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)   
 [sys.dm_repl_traninfo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-repl-traninfo-transact-sql.md)  
  
  

