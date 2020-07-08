---
title: sys. dm_db_rda_schema_update_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b74f408bdb2be61076d5034478dc6743259fed6a
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053647"
---
# <a name="stretch-database---sysdm_db_rda_schema_update_status"></a>Stretch Database-sys. dm_db_rda_schema_update_status
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Contiene una riga per ogni attività di aggiornamento dello schema per l'archivio dati remoto di ogni tabella abilitata per l'estensione nel database corrente. Le attività sono identificate dagli ID attività.  
  
 **dm_db_rda_schema_update_status** viene definito come ambito del contesto di database corrente. Assicurarsi di trovarsi nel contesto del database della tabella abilitata per l'estensione per la quale si desidera visualizzare lo stato di aggiornamento dello schema.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|ID della tabella abilitata per l'estensione locale di cui viene aggiornato lo schema di archiviazione dei dati remoti.|  
|**database_id**|**int**|ID del database che contiene la tabella abilitata per l'estensione locale.|  
|**task_id**|**bigint**|ID dell'attività di aggiornamento dello schema dell'archivio dati remoto.|  
|**task_type**|**int**|Tipo di attività di aggiornamento dello schema di archiviazione dati remota.|  
|**task_type_desc**|**nvarchar**|Descrizione del tipo di attività di aggiornamento dello schema di archiviazione dati remota.|  
|**task_state**|**int**|Stato dell'attività di aggiornamento dello schema di archiviazione dati remota.|  
|**task_state_des**|**nvarchar**|Descrizione dello stato dell'attività di aggiornamento dello schema di archiviazione dati remota.|  
|**start_time_utc**|**datetime**|Ora UTC in cui è stato avviato l'aggiornamento dello schema dell'archivio dati remoto.|  
|**end_time_utc**|**datetime**|Ora UTC in cui è terminato l'aggiornamento dello schema dell'archivio dati remoto.|  
|**error_number**|**int**|Se l'aggiornamento dello schema dell'archivio dati remoto ha esito negativo, il numero di errore dell'errore che si è verificato. in caso contrario, null.|  
|**error_severity**|**int**|Se l'aggiornamento dello schema dell'archivio dati remoto ha esito negativo, la gravità dell'errore che si è verificato. in caso contrario, null.|  
|**error_state**|**int**|Se l'aggiornamento dello schema dell'archivio dati remoto ha esito negativo, lo stato dell'errore che si è verificato. in caso contrario, null. Il error_state indica la condizione o la posizione in cui si è verificato l'errore.|  
  
## <a name="see-also"></a>Vedere anche  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
