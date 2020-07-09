---
title: MSSQLSERVER_10535 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: abb449a55e8b30e6574d75ab5ebf72df3db994c7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781423"
---
# <a name="mssqlserver_10535"></a>MSSQLSERVER_10535
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
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
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
