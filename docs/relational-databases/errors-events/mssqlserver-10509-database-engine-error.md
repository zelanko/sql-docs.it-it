---
title: MSSQLSERVER_10509 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0cdf2c06311e703b6a07667ba41d1c853c17eb86
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305891"
---
# <a name="mssqlserver_10509"></a>MSSQLSERVER_10509
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10509|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_INVALID_STMT|  
|Testo del messaggio|Impossibile creare la guida di piano '%.\*ls' perché l'istruzione specificata da **\@stmt** o **\@statement_start_offset** contiene un errore di sintassi o non può essere usata in una guida di piano. Specificare una singola istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] valida o una posizione di inizio valida dell'istruzione nel batch. Per ottenere una posizione di inizio valida, eseguire una query sulla colonna statement_start_offset nella funzione a gestione dinamica sys.dm_exec_query_stats.|  
  
## <a name="explanation"></a>Spiegazione  
L'istruzione specificata da **\@stmt** o **\@statement_start_offset** contiene un errore di sintassi o non può essere usata in una guida di piano.  
  
## <a name="user-action"></a>Azione dell'utente  
Specificare una singola istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] valida o una posizione di inizio valida dell'istruzione nel batch. Per ottenere una posizione di inizio valida, eseguire una query sulla colonna statement_start_offset nella funzione a gestione dinamica sys.dm_exec_query_stats.  
  
## <a name="see-also"></a>Vedere anche  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guide di piano](~/relational-databases/performance/plan-guides.md)  
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
