---
title: Sys. server_event_session_fields (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_session_fields
- server_event_session_fields_TSQL
- sys.server_event_session_fields
- sys.server_event_session_fields_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_fields catalog view
- xe
ms.assetid: 7109f9fb-8a1f-432c-92d1-6f8af3e96af1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 81d66f177c230d406fac9dae9373cf85da1837e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133216"
---
# <a name="sysservereventsessionfields-transact-sql"></a>sys.server_event_session_fields (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni colonna personalizzabile che è impostata in modo esplicito su eventi e destinazioni.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|ID della sessione dell'evento. Non ammette i valori Null.|  
|object_id|**int**|ID dell'oggetto a cui è associato il campo. Non ammette i valori Null.|  
|name|**sysname**|Nome del campo. Non ammette i valori Null.|  
|Valore|**sql_variant**|Valore del campo. Non ammette i valori Null.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="remarks"></a>Note  
 Questa vista ha le cardinalità della relazione seguenti.  
  
||||  
|-|-|-|  
|From|Per|Relazione|  
|sys.server_event_session_actions.event_session_id|Sys.server_event_sessions.event_session_id|Molti-a-uno|  
|sys.server_event_session_actions.event_id<br /><br /> sys.server_event_session_actions.object_id<br /><br /> sys.server_event_session_actions.event_session_id|sys.server_event_session_events.event_session_id<br /><br /> sys.server_event_session_events.event_id|Molti-a-uno|  
|sys.server_event_session_actions.event_session_id<br /><br /> sys.server_event_session_actions.object_id|sys.server_event_session_targets.event_session_id<br /><br /> sys.server_event_session_targets.target_id|Molti-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Viste del catalogo degli eventi estesi &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Eventi estesi](../../relational-databases/extended-events/extended-events.md)  
  
  
