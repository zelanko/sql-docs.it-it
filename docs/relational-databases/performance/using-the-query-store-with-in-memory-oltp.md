---
title: Uso dell'archivio query con OLTP in memoria | Microsoft Docs
description: Informazioni su come SQL Server Query Store consente di monitorare le prestazioni del codice compilato in modo nativo per i carichi di lavoro che eseguono OLTP in memoria.
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, in-memory
ms.assetid: aae5ae6d-7c90-4661-a1c5-df704319888a
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e21d436502329d7df0682e661de3548377af397d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469162"
---
# <a name="using-the-query-store-with-in-memory-oltp"></a>Uso di Archivio query con OLTP in-memoria
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Archivio query consente di monitorare le prestazioni del codice compilato in modo nativo per i carichi di lavoro che eseguono OLTP in memoria.  
Le statistiche di compilazione e runtime vengono raccolte ed esposte nello stesso modo valido per i carichi di lavoro basati su disco.   
Quando si esegue la migrazione a OLTP in memoria, è possibile continuare a usare le viste di Archivio query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oltre agli script personalizzati sviluppati per carichi di lavoro basati su disco prima della migrazione. In questo modo si tutelano gli investimenti effettuati per l'apprendimento della tecnologia di Archivio query perché queste conoscenze diventano utilizzabili a livello generale per la risoluzione dei problemi di tutti i tipi di carichi di lavoro.  
Per informazioni generali sull'uso di Archivio query, vedere [Monitoraggio delle prestazioni con Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
 L'uso di Archivio query con OLTP in memoria non richiede la configurazione di alcuna funzionalità aggiuntiva. Dopo averlo abilitato nel database, funzionerà per tutti i tipi di carico di lavoro.   
Esistono tuttavia alcuni aspetti specifici di cui gli utenti dovranno tenere conto durante l'uso di Archivio query con OLTP in memoria:  
  
-   Quando Archivio query è abilitato, vengono raccolte per impostazione predefinita statistiche relative a query, piani e tempi di compilazione. La raccolta delle statistiche di runtime non è tuttavia attivata, a meno che non venga abilitata in modo esplicito con [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).  
  
-   Quando si imposta *\@new_collection_value* su 0, Archivio query arresta la raccolta delle statistiche di runtime per la procedura interessata o per l'intera istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Il valore configurato con [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) non è persistente. Verificare di controllare e configurare nuovamente la raccolta delle statistiche dopo il riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Come nel caso della normale raccolta di statistiche sulle query, le prestazioni posso risultare ridotte quando si usa Archivio query per tenere traccia dell'esecuzione del carico di lavoro. Si consiglia di valutare la possibilità di abilitare la raccolta delle statistiche solo per un subset importante di stored procedure compilate in modo nativo.  
  
-   Le query e i piani vengono acquisiti e archiviati nella prima compilazione nativa e aggiornati per ogni ricompilazione.  
  
-   Se Archivio query viene abilitato o il suo contenuto viene cancellato dopo la compilazione di tutte le stored procedure native, è necessario ricompilarle manualmente per fare in modo che vengano acquisite da Archivio query. Lo stesso vale in caso di rimozione manuale delle query tramite [sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md) o [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md). Usare [sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) per forzare la ricompilazione delle procedure.  
  
-   Archivio query sfrutta i meccanismi di generazione dei piani di OLTP in memoria per acquisire il piano di esecuzione della query durante la compilazione. Il piano archiviato è equivalente, dal punto di vista semantico, a quello che si otterrebbe usando `SET SHOWPLAN_XML ON` con una sola differenza: i piani in Archivio query sono sempre suddivisi e archiviati per ogni singola istruzione.  
    
-   Quando si esegue Archivio query in un database con un carico di lavoro misto, è quindi possibile usare il campo **is_natively_compiled** da [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) per trovare rapidamente i piani di query generati dalla compilazione di codice nativo.  
  
-   La modalità di acquisizione di Archivio query (parametro *QUERY_CAPTURE_MODE* nell'istruzione **ALTER TABLE** ) non influisce sulle query da moduli compilati in modo nativo, perché vengono sempre acquisite indipendentemente dal valore configurato. Ciò vale anche per l'impostazione `QUERY_CAPTURE_MODE = NONE`.  
  
-   La durata della compilazione della query acquisita da Archivio query include solo tempo dedicato all'ottimizzazione della query, prima della generazione del codice nativo. Più precisamente, non include il tempo per la compilazione del codice C e la generazione delle strutture interne necessarie per la generazione del codice C.  
  
-   Le metriche delle concessioni di memoria in [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md) non vengono popolate per le query compilate in modo nativo e i valori sono sempre pari a 0. Le colonne per le concessioni di memoria sono: avg_query_max_used_memory, last_query_max_used_memory, min_query_max_used_memory, max_query_max_used_memory e stdev_query_max_used_memory.  
  
## <a name="enabling-and-using-query-store-with-in-memory-oltp"></a>Abilitazione e uso di Archivio query con OLTP in-memoria  
 Il semplice esempio seguente è una dimostrazione dell'uso di Archivio query con OLTP in memoria in uno scenario utente end-to-end. In questo esempio si presuppone che un database (`MemoryOLTP`) sia abilitato per OLTP in memoria.  
    Per altri dettagli sui prerequisiti per le tabelle ottimizzate per la memoria, vedere [Creazione di una tabella ottimizzata per la memoria e di una stored procedure compilata in modo nativo](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
```  
USE MemoryOLTP;  
GO  
  
-- Create a simple memory-optimized table   
CREATE TABLE dbo.Ord  
   (OrdNo INTEGER not null PRIMARY KEY NONCLUSTERED,   
    OrdDate DATETIME not null,   
    CustCode NVARCHAR(5) not null)   
WITH (MEMORY_OPTIMIZED=ON);  
GO  
  
-- Enable Query Store before native module compilation  
ALTER DATABASE MemoryOLTP SET QUERY_STORE = ON;  
GO  
  
-- Create natively compiled stored procedure  
CREATE PROCEDURE dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS   
    BEGIN ATOMIC WITH  
    (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'English')  
  
    DECLARE @OrdDate DATETIME = GETDATE();  
    INSERT INTO dbo.Ord (OrdNo, CustCode, OrdDate)   
        VALUES (@OrdNo, @CustCode, @OrdDate);  
END;  
GO  
  
-- Enable runtime stats collection for queries from dbo.OrderInsert stored procedure  
DECLARE @db_id INT = DB_ID()  
DECLARE @proc_id INT = OBJECT_ID('dbo.OrderInsert');  
DECLARE @collection_enabled BIT;  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
    @database_id = @db_id, @xtp_object_id = @proc_id;  
  
-- Check the state of the collection flag  
EXEC sp_xtp_control_query_exec_stats @database_id = @db_id,   
    @xtp_object_id = @proc_id,   
    @old_collection_value= @collection_enabled output;  
SELECT @collection_enabled AS 'collection status';  
  
-- Execute natively compiled workload  
EXEC dbo.OrderInsert 1, 'A';  
EXEC dbo.OrderInsert 2, 'B';  
EXEC dbo.OrderInsert 3, 'C';  
EXEC dbo.OrderInsert 4, 'D';  
EXEC dbo.OrderInsert 5, 'E';  
  
-- Check Query Store Data  
-- Compile time data  
SELECT q.query_id, plan_id, object_id, query_hash, p.query_plan,  
    p.initial_compile_start_time, p.last_compile_start_time,   
    p.last_execution_time, p.avg_compile_duration,  
    p.last_force_failure_reason, p.force_failure_count  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
  
-- Get runtime stats  
-- Check count_executions field to verify that runtime statistics   
-- have been collected by the Query Store  
SELECT q.query_id, p.plan_id, object_id, rsi.start_time, rsi.end_time,    
    p.last_force_failure_reason, p.force_failure_count, rs.*  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rs.runtime_stats_interval_id = rsi.runtime_stats_interval_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio delle prestazioni tramite Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Creazione di una tabella con ottimizzazione per la memoria e di una stored procedure compilata in modo nativo](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)   
 [Procedure consigliate per l'archivio query](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [Stored procedure di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Viste del catalogo di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
