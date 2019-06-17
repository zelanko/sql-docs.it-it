---
title: MSSQLSERVER_10519 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3bb5075ef33ced9cac22a6c92d9068907ca2ec01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048607"
---
# <a name="mssqlserver10519"></a>MSSQLSERVER_10519
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10519|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|Testo del messaggio|Impossibile creare la guida di piano '%.\*ls' perché gli hint specificati in **@hints** non possono essere applicati all'istruzione specificata da **@stmt** o **@statement_start_offset** . Verificare che gli hint possano essere applicati all'istruzione.|  
  
## <a name="explanation"></a>Spiegazione  
Gli hint specificati in **@hints** non possono essere applicati all'istruzione specificata da **@stmt** o **@statement_start_offset** .  
  
## <a name="user-action"></a>Azione dell'utente  
Specificare hint che possono essere applicati all'istruzione.  
  
## <a name="see-also"></a>Vedere anche  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guide di piano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
