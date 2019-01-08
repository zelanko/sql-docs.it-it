---
title: Sys.dm_xe_session_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_session_events
- sys.dm_xe_session_events_TSQL
- dm_xe_session_events
- dm_xe_session_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_session_events dynamic management view
- extended events [SQL Server], views
ms.assetid: 4f027b31-4e03-43a6-849d-1ba9d8d34ae8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c2b42eacb645f27ba44b467c842df98e8ca6944a
ms.sourcegitcommit: f46fd79fd32a894c8174a5cb246d9d34db75e5df
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/26/2018
ms.locfileid: "53785892"
---
# <a name="sysdmxesessionevents-transact-sql"></a>sys.dm_xe_session_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sugli eventi di sessione. Gli eventi sono punti di esecuzione discreti. I predicati possono essere applicati agli eventi per arrestarne la generazione se l'evento non contiene le informazioni necessarie.  
   
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|Indirizzo di memoria della sessione dell'evento. Non ammette i valori Null.|  
|event_name|**nvarchar(256)**|Nome dell'evento associato all'azione. Non ammette i valori Null.|  
|event_package_guid|**uniqueidentifier**|GUID per il pacchetto che contiene l'evento. Non ammette i valori Null.|  
|event_predicate|**nvarchar(3072)**|Rappresentazione XML dell'albero predicativo applicato all'evento. Ammette i valori Null.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
### <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
|From|Per|Relazione|  
|----------|--------|------------------|  
|sys.dm_xe_session_events.event_session_address|sys.dm_xe_sessions.address|Molti-a-uno|  
|Sys.dm_xe_session_events.event_package_guid,<br /><br /> Sys.dm_xe_session_events.EVENT_NAME|sys.dm_xe_objects.name,<br /><br /> sys.dm_xe_objects.package_guid|Molti-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

