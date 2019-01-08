---
title: Modificare una traccia esistente (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], modifying
- modifying traces
ms.assetid: 8792b43f-2510-44e3-9239-e73ad8227b89
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 56d4f7d922c0c229b1e2126f93611670adf7c702
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591845"
---
# <a name="modify-an-existing-trace-transact-sql"></a>Modificare una traccia esistente (Transact-SQL)
  In questo argomento viene descritto come utilizzare stored procedure per modificare una traccia esistente.  
  
### <a name="to-modify-an-existing-trace"></a>Per modificare una traccia esistente  
  
1.  Se la traccia è già in esecuzione, eseguire **sp_trace_setstatus** specificando **@status = 0** per arrestarla.  
  
2.  Per modificare eventi di traccia, eseguire **sp_trace_setevent** usando i parametri per specificare le modifiche. Nell'ordine i parametri sono i seguenti:  
  
    -   **@traceid** (ID traccia)  
  
    -   **@eventid** (ID evento)  
  
    -   **@columnid** (ID colonna)  
  
    -   **@on** (ON)  
  
     Quando si modifica il parametro **@on** , tenere presente l'interazione con il parametro **@columnid** :  
  
    |ON|ID colonna|Risultato|  
    |--------|---------------|------------|  
    |ON (**1**)|NULL|L'evento viene abilitato. Tutte le colonne vengono cancellate.|  
    ||NOT NULL|La colonna viene abilitata per l'evento specificato.|  
    |OFF (**0**)|NULL|L'evento viene disabilitato. Tutte le colonne vengono cancellate.|  
    ||NOT NULL|La colonna viene disabilitata per l'evento specificato.|  
  
> [!IMPORTANT]
>  A differenza delle normali stored procedure, parametri di tutte le [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] stored procedure (<strong>sp_trace _*xx*</strong>) sono rigidamente tipizzati e non supportano la conversione di tipo automatica dei dati. Se tali parametri non vengono chiamati con i tipi di dati corretti per i parametri di input, come indicato nella descrizione dell'argomento, la stored procedure restituisce un errore.  

## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [Stored procedure di SQL Server Profiler &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
