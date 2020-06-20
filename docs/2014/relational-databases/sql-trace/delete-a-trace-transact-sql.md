---
title: Eliminare una traccia (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b3551cff36ef6e2c2e9cc6a4d9b7056ae44cb950
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068294"
---
# <a name="delete-a-trace-transact-sql"></a>Eliminare una traccia (Transact-SQL)
  In questo argomento viene illustrata la procedura di utilizzo di stored procedure per eliminare una traccia.  
  
 Per un esempio dell'uso di stored procedure relative alla traccia, vedere [Creare una traccia &#40;Transact-SQL&#41;](create-a-trace-transact-sql.md).  
  
### <a name="to-delete-a-trace"></a>Per eliminare una traccia  
  
1.  Eseguire **sp_trace_setstatus** specificando **@status = 0** per arrestare la traccia.  
  
2.  Eseguire **sp_trace_setstatus** specificando **@status = 2** per chiudere la traccia ed eliminare le relative informazioni dal server.  
  
> [!NOTE]  
>  È necessario che la traccia venga arrestata prima di chiuderla.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [Stored procedure di SQL Server Profiler &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
