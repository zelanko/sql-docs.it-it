---
title: Visualizzare una traccia salvata (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], viewing
- displaying traces
- viewing traces
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 16adeb7225df27d571e3c8ea30daa44151f3c19c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52788523"
---
# <a name="view-a-saved-trace-transact-sql"></a>Visualizzare una traccia salvata (Transact-SQL)
  In questo argomento viene illustrato l'utilizzo delle funzioni predefinite per visualizzare una traccia salvata.  
  
### <a name="to-view-a-specific-trace"></a>Per visualizzare una traccia specifica  
  
1.  Eseguire **fn_trace_getinfo** specificando l'ID della traccia su cui si vuole ottenere informazioni. Questa funzione restituisce una tabella in cui sono indicate la traccia, la proprietà della traccia e le informazioni sulla proprietà.  
  
     Richiamare la funzione nel modo seguente:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### <a name="to-view-all-existing-traces"></a>Per visualizzare tutte le tracce esistenti  
  
1.  Eseguire **fn_trace_getinfo** specificando `0` o `default`. Questa funzione restituisce una tabella in cui sono indicate tutte le tracce, le relative proprietà e le informazioni su tali proprietà.  
  
     Di seguito è illustrato come richiamare la funzione:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Per eseguire la funzione predefinita **fn_trace_getinfo**, è necessaria l'autorizzazione seguente:  
  
 ALTER TRACE nel server.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql)   
 [Visualizzare e analizzare le tracce con SQL Server Profiler](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  
