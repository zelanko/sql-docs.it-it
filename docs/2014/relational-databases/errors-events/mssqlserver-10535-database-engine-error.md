---
title: MSSQLSERVER_10535 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 68070291c5e7f50d423b74338dc1f6baeb9c6dfa
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554116"
---
# <a name="mssqlserver_10535"></a>MSSQLSERVER_10535
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10535|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_NO_PLAN|  
|Testo del messaggio|Impossibile cerare la guida di piano '%.*ls' perché non è stato trovato alcun piano nella cache dei piani corrispondente all'handle di piani specificato. Specificare un handle di piani memorizzati nella cache. Per un elenco degli handle di piani memorizzati nella cache, eseguire una query sulla vista a gestione dinamica sys.dm_exec_query_stats.|  
  
## <a name="explanation"></a>Spiegazione  
 Non è stato trovato alcun piano nella cache dei piani corrispondente all'handle di piani specificato.  
  
## <a name="user-action"></a>Azione dell'utente  
 Specificare un handle di piani memorizzati nella cache. Per un elenco degli handle di piani memorizzati nella cache, eseguire una query sulla vista a gestione dinamica sys.dm_exec_query_stats.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_create_plan_guide_from_handle &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)  
  
  
