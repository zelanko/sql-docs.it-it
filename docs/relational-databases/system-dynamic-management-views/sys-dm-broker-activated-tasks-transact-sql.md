---
description: sys.dm_broker_activated_tasks (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e89f0caf5eb3181a59e653ca1a64f4a68ec3fbc5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544786"
---
# <a name="sysdm_broker_activated_tasks-transact-sql"></a>sys.dm_broker_activated_tasks (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
  
|Da|To|Relazione|  
|----------|--------|------------------|  
|dm_broker_activated_tasks.spid|dm_exec_sessions.session_id|Uno-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative a Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

