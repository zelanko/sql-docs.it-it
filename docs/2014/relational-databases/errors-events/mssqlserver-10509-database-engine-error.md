---
title: MSSQLSERVER_10509 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 566d57843eaeafe02f7620c019aa6fbccdebd300
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552396"
---
# <a name="mssqlserver_10509"></a>MSSQLSERVER_10509
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10509|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_INVALID_STMT|  
|Testo del messaggio|Impossibile creare la guida di piano '%.\*ls' perché l'istruzione specificata da `@stmt` o `@statement_start_offset` contiene un errore di sintassi o non può essere usata in una guida di piano. Specificare una singola istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] valida o una posizione di inizio valida dell'istruzione nel batch. Per ottenere una posizione di inizio valida, eseguire una query sulla colonna statement_start_offset nella funzione a gestione dinamica sys.dm_exec_query_stats.|  
  
## <a name="explanation"></a>Spiegazione  
 L'istruzione specificata da `@stmt` o `@statement_start_offset` contiene un errore di sintassi o non può essere utilizzata in una guida di piano.  
  
## <a name="user-action"></a>Azione dell'utente  
 Specificare una singola istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] valida o una posizione di inizio valida dell'istruzione nel batch. Per ottenere una posizione di inizio valida, eseguire una query sulla colonna statement_start_offset nella funzione a gestione dinamica sys.dm_exec_query_stats.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guide di piano](../performance/plan-guides.md)   
 [sys. dm_exec_query_stats &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
