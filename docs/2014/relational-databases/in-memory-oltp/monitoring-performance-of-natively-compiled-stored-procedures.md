---
title: Monitoraggio delle prestazioni di stored procedure compilate in modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 55548cb2-77a8-4953-8b5a-f2778a4f13cf
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9b8d6f35f8dedeb4539dc8299ca32f6566beb03f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161959"
---
# <a name="monitoring-performance-of-natively-compiled-stored-procedures"></a>Monitoraggio delle prestazioni di stored procedure compilate in modo nativo
  In questo argomento viene illustrato come è possibile monitorare le prestazioni di stored procedure compilate in modo nativo  
  
## <a name="using-extended-events"></a>Utilizzo degli eventi estesi  
 Utilizzare l'evento esteso `sp_statement_completed` per tracciare l'esecuzione di una query. Creare una sessione di eventi estesi con questo evento, applicando facoltativamente un filtro a OBJECT_ID per una stored procedure compilata in modo nativo. L'evento esteso viene generato dopo l'esecuzione di ogni query. Il tempo e la durata della CPU segnalati dagli eventi estesi indicano la quantità di CPU utilizzata dalla query e il tempo di esecuzione. Una stored procedure compilata in modo nativo che utilizza un tempo di CPU elevato può presentare problemi di prestazioni.  
  
 È possibile utilizzare `line_number` e `object_id` nell'evento esteso per esaminare la query. È possibile utilizzare la query seguente per recuperare la definizione della routine. Il numero di riga può essere utilizzato per identificare la query all'interno della definizione:  
  
```sql  
select [definition] from sys.sql_modules where object_id=object_id  
```  
  
 Per altre informazioni sul `sp_statement_completed` evento esteso, vedere [come recuperare l'istruzione che ha causato un evento](https://blogs.msdn.com/b/extended_events/archive/2010/05/07/making-a-statement-how-to-retrieve-the-t-sql-statement-that-caused-an-event.aspx).  
  
## <a name="using-data-management-views"></a>Utilizzo delle viste di gestione dati  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta la raccolta delle statistiche di esecuzione per le stored procedure compilate in modo nativo, sia a livello di routine sia a livello di query. La raccolta delle statistiche di esecuzione non è abilitata per impostazione predefinita a causa dell'impatto sulle prestazioni.  
  
 Per abilitare e disabilitare la raccolta di statistiche sulle stored procedure compilate in modo nativo, usare [sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql).  
  
 Quando la raccolta delle statistiche è abilitata con [sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql), è possibile usare [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql) per monitorare le prestazioni di una stored procedure compilata in modo nativo.  
  
 Quando la raccolta delle statistiche è abilitata con [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql), è possibile usare [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql) per monitorare le prestazioni di una stored procedure compilata in modo nativo.  
  
 All'inizio dell'operazione di raccolta, abilitare la raccolta delle statistiche. Eseguire quindi la stored procedure compilata in modo nativo. Alla fine dell'operazione di raccolta, disabilitare la raccolta delle statistiche. Analizzare quindi le statistiche di esecuzione restituite dalle viste a gestione dinamica.  
  
 Dopo avere raccolto le statistiche, è possibile interrogare le statistiche di esecuzione delle stored procedure compilate in modo nativo per individuare una routine con [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql) e per individuare query con [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql).  
  
> [!NOTE]  
>  Quando la raccolta delle statistiche è abilitata, per le stored procedure compilate in modo nativo il tempo del processo viene raccolto in millisecondi. Se la query viene eseguita in meno di un millisecondo, il valore sarà 0. Per le stored procedure compilate in modo nativo, il valore di **total_worker_time** non può essere accurato se più esecuzioni richiedono meno di 1 millisecondo.  
  
 La query seguente restituisce i nomi delle routine e le statistiche di esecuzione per le stored procedure compilate in modo nativo nel database corrente, dopo la raccolta delle statistiche:  
  
```sql  
select object_id,  
       object_name(object_id) as 'object name',  
       cached_time,  
       last_execution_time,  
       execution_count,  
       total_worker_time,  
       last_worker_time,  
       min_worker_time,  
       max_worker_time,  
       total_elapsed_time,  
       last_elapsed_time,  
       min_elapsed_time,  
       max_elapsed_time   
from sys.dm_exec_procedure_stats  
where database_id=db_id() and object_id in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by total_worker_time desc  
```  
  
 La query seguente restituisce il testo della query nonché le statistiche di esecuzione per tutte le query nelle stored procedure compilate in modo nativo nel database corrente per il quale sono state raccolte le statistiche, ordinate in base al tempo del processo, in ordine decrescente.  
  
```sql  
select st.objectid,   
       object_name(st.objectid) as 'object name',   
       SUBSTRING(st.text, (qs.statement_start_offset/2) + 1, ((qs.statement_end_offset-qs.statement_start_offset)/2) + 1) as 'query text',   
       qs.creation_time,  
       qs.last_execution_time,  
       qs.execution_count,  
       qs.total_worker_time,  
       qs.last_worker_time,  
       qs.min_worker_time,  
       qs.max_worker_time,  
       qs.total_elapsed_time,  
       qs.last_elapsed_time,  
       qs.min_elapsed_time,  
       qs.max_elapsed_time  
from sys.dm_exec_query_stats qs cross apply sys.dm_exec_sql_text(sql_handle) st  
where  st.dbid=db_id() and st.objectid in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by qs.total_worker_time desc  
```  
  
 Le stored procedure compilate in modo nativo supportano SHOWPLAN_XML (piano di esecuzione stimato). Il piano di esecuzione stimato può essere utilizzato per esaminare il piano di query al fine di rilevare eventuali problemi relativi a piani non validi. I motivi comuni per i piani non validi sono:  
  
-   Le statistiche non sono state aggiornate prima della creazione della routine.  
  
-   Indici mancanti  
  
 Showplan XML viene ottenuto mediante l'esecuzione dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)]seguente:  
  
```sql  
SET SHOWPLAN_XML ON  
GO  
EXEC my_proc   
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 In alternativa, in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]selezionare il nome della routine e fare clic su **Visualizza piano di esecuzione stimato**.  
  
 Nel piano di esecuzione stimato per le stored procedure compilate in modo nativo vengono illustrati gli operatori e le espressioni delle query per le query nella routine. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] non supporta tutti gli attributi di SHOWPLAN_XML per le stored procedure compilate in modo nativo. Ad esempio, gli attributi correlati ai costi di Query Optimizer non fanno parte di SHOWPLAN_XML per la routine.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure compilate in modo nativo](natively-compiled-stored-procedures.md)  
  
  
