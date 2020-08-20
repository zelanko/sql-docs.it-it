---
description: Salvare i risultati della traccia in un file
title: Salvare i risultati della traccia in un file | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 74f80667-62f3-4e14-bb1a-f0c2b6ef3402
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b5b60bea4633abcef041ad516aef972875884282
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455347"
---
# <a name="save-trace-results-to-a-file"></a>Salvare i risultati della traccia in un file
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  È possibile salvare i risultati della traccia in un file. Un file di traccia è un file nel quale vengono scritti i risultati della traccia. Un file di traccia può trovarsi in una directory locale (ad esempio C:\\*nomecartella*\\*nomefile.trc*) o in una directory di rete (ad esempio \\\nomecomputer\nomecondivisione\nomefile.trc).  
  
 I file di traccia consentono di:  
  
-   Riprodurre le tracce  
  
-   Controllare il funzionamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Condurre analisi sulle prestazioni  
  
-   Correlare eventi di traccia a contatori delle prestazioni per migliorare il rilevamento dei problemi  
  
-   Eseguire analisi di Ottimizzazione guidata motore di database  
  
-   Eseguire l'ottimizzazione delle query  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] salva i risultati della traccia in un file quando vengono specificati un percorso e un nome file per l'argomento **\@tracefile** della stored procedure **sp_trace_create**.  
  
> [!NOTE]  
>  Se nella stored procedure **sp_trace_create** si specifica un percorso per il salvataggio del file di traccia, è necessario che la directory sia accessibile al server. Si noti anche che se viene specificata una directory locale in **sp_trace_create**, si tratta di una directory locale nel computer server.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] consente di salvare i risultati della traccia in un file o in una tabella. Il salvataggio in una tabella offre lo stesso accesso del salvataggio in un file e in più consente l'esecuzione di query sulla tabella per la ricerca di eventi specifici.  
  
 Per altre informazioni sul salvataggio dei risultati della traccia, vedere [Salvare i risultati della traccia in una tabella &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md) e [Salvare i risultati della traccia in un file &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md).  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [Creare una traccia &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [Creare una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
