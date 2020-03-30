---
title: Monitorare le prestazioni di stored procedure compilate in modo nativo
ms.custom: seo-dt-2019
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 55548cb2-77a8-4953-8b5a-f2778a4f13cf
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b1970c5953373c500f85e82281a69be1d46f1be0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "78180064"
---
# <a name="monitoring-performance-of-natively-compiled-stored-procedures"></a>Monitoraggio delle prestazioni di stored procedure compilate in modo nativo

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Questo articolo illustra come monitorare le prestazioni di stored procedure compilate in modo nativo e di altri moduli T-SQL compilati in modo nativo.  
  
## <a name="using-extended-events"></a>Utilizzo degli eventi estesi  
 Usare l'evento esteso **sp_statement_completed** per tracciare l'esecuzione di una query. Creare una sessione di eventi estesi con questo evento, applicando facoltativamente un filtro a OBJECT_ID per una stored procedure specifica compilata in modo nativo. L'evento esteso viene generato dopo l'esecuzione di ogni query. Il tempo e la durata della CPU segnalati dagli eventi estesi indicano la quantità di CPU utilizzata dalla query e il tempo di esecuzione. Una stored procedure compilata in modo nativo che utilizza un tempo di CPU elevato può presentare problemi di prestazioni.  
  
 È possibile usare**line_number**con **object_id** nell'evento esteso per esaminare la query. È possibile utilizzare la query seguente per recuperare la definizione della routine. Il numero di riga può essere utilizzato per identificare la query all'interno della definizione:  
  
```sql  
SELECT [definition]
    from sys.sql_modules
    where object_id=object_id;
```  
  
  
## <a name="using-data-management-views-and-query-store"></a>Uso di viste di Gestione dati e di Query Store
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)] supportano la raccolta delle statistiche di esecuzione per le stored procedure compilate in modo nativo, sia a livello di routine che a livello di query. La raccolta delle statistiche di esecuzione non è abilitata per impostazione predefinita a causa dell'impatto sulle prestazioni.  

Le statistiche di esecuzione si riflettono nelle viste di sistema [sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) e [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md), nonché in [Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).

## <a name="procedure-level-execution-statistics"></a>Statistiche di esecuzione a livello di routine

**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : abilitare o disabilitare la raccolta di statistiche sulle stored procedure compilate in modo nativo a livello di routine tramite [sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md).  L'istruzione seguente abilita la raccolta di statistiche di esecuzione a livello di routine per tutti i moduli T-SQL compilati in modo nativo nell'istanza corrente:
```sql
EXEC sys.sp_xtp_control_proc_exec_stats 1
```

**[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]** : abilitare o disabilitare la raccolta di statistiche sulle stored procedure compilate in modo nativo a livello di routine tramite l'opzione di [configurazione con ambito database](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)`XTP_PROCEDURE_EXECUTION_STATISTICS`. L'istruzione seguente abilita la raccolta di statistiche di esecuzione a livello di routine per tutti i moduli T-SQL compilati in modo nativo nel database corrente:
```sql
ALTER DATABASE
    SCOPED CONFIGURATION
    SET XTP_PROCEDURE_EXECUTION_STATISTICS = ON;
```

## <a name="query-level-execution-statistics"></a>Statistiche di esecuzione a livello di query

**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : abilitare o disabilitare la raccolta di statistiche sulle stored procedure compilate in modo nativo a livello di query tramite [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).  L'istruzione seguente abilita la raccolta di statistiche di esecuzione a livello di query per tutti i moduli T-SQL compilati in modo nativo nell'istanza corrente:
```sql
EXEC sys.sp_xtp_control_query_exec_stats 1
```

**[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]** : abilitare o disabilitare la raccolta di statistiche sulle stored procedure compilate in modo nativo a livello di istruzione tramite l'opzione di [configurazione con ambito database](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)`XTP_QUERY_EXECUTION_STATISTICS`. L'istruzione seguente abilita la raccolta di statistiche di esecuzione a livello di query per tutti i moduli T-SQL compilati in modo nativo nel database corrente:
```sql
ALTER DATABASE
    SCOPED CONFIGURATION
    SET XTP_QUERY_EXECUTION_STATISTICS = ON;
```

## <a name="sample-queries"></a>Query di esempio

 Dopo avere raccolto le statistiche, è possibile interrogare le statistiche di esecuzione delle stored procedure compilate in modo nativo per individuare una routine con [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) e per individuare query con [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md).  
 
  
 La query seguente restituisce i nomi delle routine e le statistiche di esecuzione per le stored procedure compilate in modo nativo nel database corrente, dopo la raccolta delle statistiche:  

```sql
SELECT
        object_id,
        object_name(object_id) as 'object name',
        cached_time,
        last_execution_time,  execution_count,
        total_worker_time,    last_worker_time,
        min_worker_time,      max_worker_time,
        total_elapsed_time,   last_elapsed_time,
        min_elapsed_time,     max_elapsed_time
    from
        sys.dm_exec_procedure_stats
    where
        database_id = db_id()
        and
        object_id in
            (
            SELECT object_id
                from sys.sql_modules
                where uses_native_compilation=1
            )
    order by
        total_worker_time desc;
```

La query seguente restituisce il testo della query nonché le statistiche di esecuzione per tutte le query nelle stored procedure compilate in modo nativo nel database corrente per il quale sono state raccolte le statistiche, ordinate in base al tempo del processo, in ordine decrescente.  

```sql
SELECT
        st.objectid,
        object_name(st.objectid) as 'object name',
        SUBSTRING(
            st.text,
            (qs.statement_start_offset/2) + 1,
            ((qs.statement_end_offset-qs.statement_start_offset)/2) + 1
            ) as 'query text',
        qs.creation_time,
        qs.last_execution_time,   qs.execution_count,
        qs.total_worker_time,     qs.last_worker_time,
        qs.min_worker_time,       qs.max_worker_time,
        qs.total_elapsed_time,    qs.last_elapsed_time,
        qs.min_elapsed_time,      qs.max_elapsed_time
    FROM
                    sys.dm_exec_query_stats qs
        cross apply sys.dm_exec_sql_text(sql_handle) st
    WHERE
        st.dbid = db_id()
        and
        st.objectid in
            (SELECT object_id
                from sys.sql_modules
                where uses_native_compilation=1
            )
    ORDER BY
        qs.total_worker_time desc;
```

## <a name="query-execution-plans"></a>Piani di esecuzione di query

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
 [Stored procedure compilate in modo nativo](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
