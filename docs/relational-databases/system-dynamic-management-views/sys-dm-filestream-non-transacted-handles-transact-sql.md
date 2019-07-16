---
title: Sys.dm_filestream_non_transacted_handles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_non_transacted_handles_TSQL
- dm_filestream_non_transacted_handles
- dm_filestream_non_transacted_handles_TSQL
- sys.dm_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_non_transacted_handles dynamic management view
ms.assetid: 507ec125-67dc-450a-9081-94cde5444a92
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4dda607ace977be539dbed096a3d83ac5f220ea0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950985"
---
# <a name="sysdmfilestreamnontransactedhandles-transact-sql"></a>sys.dm_filestream_non_transacted_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di visualizzare gli handle di file non transazionali aperti associati a dati di tabelle FileTable.  
  
 Questa vista contiene una riga per ogni handle di file aperto. Poiché i dati nella vista corrispondono allo stato interno in tempo reale del server, tali dati cambiano costantemente in corrispondenza dell'apertura e della chiusura degli handle. La vista non contiene informazioni cronologiche.  
  
 Per altre informazioni, vedere [Gestire le tabelle FileTable](../../relational-databases/blob/manage-filetables.md).  
  
|**Colonna**|**Tipo**|**Descrizione**|  
|----------------|--------------|---------------------|  
|database_id|int|ID del database associato all'handle.|  
|object_id|int|ID oggetto della tabella FileTable a cui è associato l'handle.|  
|handle_id|int|Identificatore di contesto dell'handle univoco. Utilizzato per il [sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md) stored procedure per terminare un handle specifico.|  
|file_object_type|int|Tipo dell'handle. Indica il livello della gerarchia rispetto al quale è stato aperto l'handle, ovvero a livello di database o a livello di elemento.|  
|file_object_type_desc|nvarchar(120)|"UNDEFINED",<br />"SERVER_ROOT",<br />"DATABASE_ROOT",<br />"TABLE_ROOT",<br />"TABLE_ITEM"|  
|correlation_process_id|varbinary(8)|Contiene un identificatore univoco per il processo da cui ha avuto origine la richiesta.|  
|correlation_thread_id|varbinary(8)|Contiene un identificatore univoco per il thread da cui ha avuto origine la richiesta.|  
|file_context|varbinary(8)|Puntatore all'oggetto file utilizzato dall'handle.|  
|state|int|Stato corrente dell'handle. Può essere attivo, chiuso o terminato.|  
|state_desc|nvarchar(120)|"ATTIVO",<br />"CLOSED",<br />"TERMINATO"|  
|current_workitem_type|int|Stato tramite cui l'handle viene attualmente elaborato.|  
|current_workitem_type_desc|nvarchar(120)|"NoSetWorkItemType",<br />"FFtPreCreateWorkitem",<br />"FFtGetPhysicalFileNameWorkitem",<br />"FFtPostCreateWorkitem",<br />"FFtPreCleanupWorkitem",<br />"FFtPostCleanupWorkitem",<br />"FFtPreCloseWorkitem",<br />"FFtQueryDirectoryWorkItem",<br />"FFtQueryInfoWorkItem",<br />"FFtQueryVolumeInfoWorkItem",<br />"FFtSetInfoWorkitem",<br />"FFtWriteCompletionWorkitem"|  
|fcb_id|bigint|ID blocco di controllo file della tabella FileTable.|  
|item_id|varbinary(892)|ID elemento per un file o una directory. Può essere null per gli handle della radice del server.|  
|is_directory|bit|Specifica che l'elemento è una directory.|  
|item_name|nvarchar(512)|Nome dell'elemento.|  
|opened_file_name|nvarchar(512)|Percorso richiesto in origine per l'apertura.|  
|database_directory_name|nvarchar(512)|Parte di opened_file_name che rappresenta il nome della directory dei database.|  
|table_directory_name|nvarchar(512)|Parte di opened_file_name che rappresenta il nome della directory delle tabelle.|  
|remaining_file_name|nvarchar(512)|Parte di opened_file_name che rappresenta il nome di directory rimanente.|  
|open_time|datetime|Data e ora in cui è stato aperto l'handle.|  
|flags|int|ShareFlagsUpdatedToFcb = 0x1<br />DeleteOnClose = 0x2<br />NewFile = 0x4<br />PostCreateDoneForNewFile = 0x8<br />StreamFileOverwritten = 0x10<br />RequestCancelled = 0x20<br />NewFileCreationRolledBack = 0x40|  
|login_id|int|ID dell'entità che ha aperto l'handle.|  
|login_name|nvarchar(512)|Nome dell'entità che ha aperto l'handle.|  
|login_sid|varbinary(85)|SID dell'entità che ha aperto l'handle.|  
|read_access|bit|Elemento aperto per l'accesso in lettura.|  
|write_access|bit|Elemento aperto per l'accesso in scrittura.|  
|delete_access|bit|Elemento aperto per l'accesso in eliminazione.|  
|share_read|bit|Elemento aperto con share_read consentito.|  
|share_write|bit|Elemento aperto con share_write consentito.|  
|share_delete|bit|Elemento aperto con share_delete consentito.|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire tabelle FileTable](../../relational-databases/blob/manage-filetables.md)  
  
  
