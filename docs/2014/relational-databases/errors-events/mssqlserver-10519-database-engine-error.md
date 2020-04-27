---
title: MSSQLSERVER_10519 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6bb9c6f7fddc9ba0d4430b42ba5472a59c29e3cf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62916236"
---
# <a name="mssqlserver_10519"></a>MSSQLSERVER_10519
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10519|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|Testo del messaggio|Impossibile creare la guida di piano '%.\*ls' perché gli hint specificati in `@hints` non possono essere applicati all'istruzione specificata da `@stmt` o `@statement_start_offset`. Verificare che gli hint possano essere applicati all'istruzione.|  
  
## <a name="explanation"></a>Spiegazione  
 Gli hint specificati in `@hints` non possono essere applicati all'istruzione specificata da `@stmt` o `@statement_start_offset`.  
  
## <a name="user-action"></a>Azione dell'utente  
 Specificare hint che possono essere applicati all'istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_create_plan_guide &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guide di piano](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
