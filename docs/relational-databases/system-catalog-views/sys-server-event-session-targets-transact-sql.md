---
title: sys. server_event_session_targets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_session_targets_TSQL
- sys.server_event_session_targets_TSQL
- sys.server_event_session_targets
- server_event_session_targets
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_targets catalog view
- xe
ms.assetid: dda4879d-57ae-4267-b410-1ef5c37404c7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ac4e6a7bb6f850c2bec6ae8bcbf0b21bb5d3ed39
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85664707"
---
# <a name="sysserver_event_session_targets-transact-sql"></a>sys.server_event_session_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Restituisce una riga per ogni destinazione di evento per una sessione eventi.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|ID della sessione dell'evento. Non ammette i valori Null.|  
|target_id|**int**|ID della destinazione. L'ID è univoco all'interno dell'oggetto della sessione dell'evento. Non ammette i valori Null.|  
|name|**sysname**|Nome della destinazione dell'evento. Non ammette i valori Null.|  
|Pacchetto|**sysname**|Nome del pacchetto dell'evento contenente la destinazione dell'evento. Non ammette i valori Null.|  
|module|**sysname**|Nome del modulo contenente la destinazione dell'evento. Non ammette i valori Null.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="remarks"></a>Osservazioni  
 Questa vista ha le cardinalità della relazione seguenti.  
  
||||  
|-|-|-|  
|From|A|Relazione|  
|sys.server_event_session_targets.event_session_id|sys. server_event_sessions. event_session_id|Molti-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Viste del catalogo degli eventi estesi &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Eventi estesi](../../relational-databases/extended-events/extended-events.md)  
  
  
