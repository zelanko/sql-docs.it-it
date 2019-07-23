---
title: Visualizzare informazioni sui filtri (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: b7e52c13-8c83-47c2-8cd0-af7a49eceb5c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4fa854d5ece9dc659e5a5d30ea051cf717f20d96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126612"
---
# <a name="view-filter-information-transact-sql"></a>Visualizzare informazioni sui filtri (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene illustrata la procedura di utilizzo delle funzioni predefinite per la visualizzazione delle informazioni sui filtri di traccia.  
  
### <a name="to-view-filter-information"></a>Per visualizzare informazioni sui filtri  
  
1.  Eseguire **fn_trace_getfilterinfo** specificando l'ID della traccia per cui vuole ottenere informazioni sui filtri. La funzione restituisce una tabella con l'elenco dei filtri, le colonne cui i filtri sono applicati e i valori ai quali il filtro si applica.  
  
     Richiamare la funzione nel modo seguente:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getfilterinfo(trace_id)  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Stored procedure di SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
