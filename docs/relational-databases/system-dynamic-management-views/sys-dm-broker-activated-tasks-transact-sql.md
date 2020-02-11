---
title: sys. dm_broker_activated_tasks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_activated_tasks
- sys.dm_broker_activated_tasks_TSQL
- dm_broker_activated_tasks
- dm_broker_activated_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_activated_tasks dynamic management view
ms.assetid: 17e6f87f-8f56-489d-9aed-216afc8ef310
author: stevestein
ms.author: sstein
ms.openlocfilehash: f80ec78e37707058a354a03bb2605a38abdfa803
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68099196"
---
# <a name="sysdm_broker_activated_tasks-transact-sql"></a>sys.dm_broker_activated_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni stored procedure attivata da Service Broker.  
 

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**spid**|**int**|ID della sessione della stored procedure attivata. Ammette valori Null.|  
|**database_id**|**smallint**|ID del database nel quale è stata definita la coda. Ammette valori Null.|  
|**queue_id**|**int**|ID dell'oggetto della coda per il quale è stata attivata la stored procedure. Ammette valori Null.|  
|**procedure_name**|**nvarchar (650)**|Nome della stored procedure attivata. Ammette valori Null.|  
|**execute_as**|**int**|ID dell'utente in base al quale viene eseguita la stored procedure. Ammette valori Null.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="physical-joins"></a>Join fisici  
 ![Join per sys.dm_broker_activated_tasks](../../relational-databases/system-dynamic-management-views/media/join-dm-broker-activated-tasks-1.gif "Join per sys.dm_broker_activated_tasks")  
  
## <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
|Da|A|Relazione|  
|----------|--------|------------------|  
|dm_broker_activated_tasks.spid|dm_exec_sessions.session_id|Uno-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica correlate Service Broker &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

