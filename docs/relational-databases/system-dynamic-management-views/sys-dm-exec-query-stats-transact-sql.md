---
title: sys.dm_exec_query_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_stats_TSQL
- dm_exec_query_stats
- sys.dm_exec_query_stats
- sys.dm_exec_query_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_stats dynamic management view
ms.assetid: eb7b58b8-3508-4114-97c2-d877bcb12964
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 821eaa4b7c54d8d2f449b2b071582480ac806378
ms.sourcegitcommit: 5905c29b5531cef407b119ebf5a120316ad7b713
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66429023"
---
# <a name="sysdmexecquerystats-transact-sql"></a>sys.dm_exec_query_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Restituisce dati statistici aggregati sulle prestazioni dei piani di query memorizzati nella cache in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La vista contiene una riga per ogni istruzione di query nel piano memorizzato nella cache e la durata delle righe è legata al piano stesso. Quando un piano viene rimosso dalla cache, le righe corrispondenti vengono eliminate da questa vista.  
  
> [!NOTE]
> Una query iniziale di **DM exec_query_stats** potrebbe produrre risultati non accurati se è presente un carico di lavoro attualmente in esecuzione nel server. La riesecuzione della query può garantire risultati più accurati.  
  
> [!NOTE]
> Per chiamare questo elemento dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oppure [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], usare il nome **sys.dm_pdw_nodes_exec_query_stats**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**sql_handle**|**varbinary(64)**  |È un token che identifica in modo univoco il batch o una stored procedure che fa parte della query.<br /><br /> **valore di sql_handle**, in combinazione con **statement_start_offset** e **statement_end_offset**, può essere utilizzato per recuperare il testo SQL della query chiamando il **sys.dm_exec_sql_ testo** funzione a gestione dinamica.|  
|**statement_start_offset**|**int**|Indica, in byte e a partire da 0, la posizione iniziale della query descritta dalla riga all'interno del testo del batch o dell'oggetto persistente.|  
|**statement_end_offset**|**int**|Indica, in byte e a partire da 0, la posizione finale della query descritta dalla riga all'interno del testo del batch o dell'oggetto persistente. Per le versioni precedenti [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], il valore -1 indica la fine del batch. I commenti finali non sono più inclusi.|  
|**plan_generation_num**|**bigint**|Numero di sequenza utilizzabile per distinguere le istanze dei piani dopo una ricompilazione.|  
|**plan_handle**|**varbinary(64)**|È un token che identifica in modo univoco un piano di esecuzione di query per un batch che ha eseguito e il piano risiede nella cache dei piani o attualmente in esecuzione. Questo valore può essere passato per il [DM exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) funzione a gestione dinamica per ottenere il piano di query.<br /><br /> È sempre 0x000 quando una stored procedure compilata in modo nativo esegue una query su una tabella ottimizzata per la memoria.|  
|**creation_time**|**datetime**|Ora di compilazione del piano.|  
|**last_execution_time**|**datetime**|Ora dell'ultimo avvio dell'esecuzione del piano.|  
|**execution_count**|**bigint**|Numero di esecuzioni del piano a partire dall'ultima compilazione.|  
|**total_worker_time**|**bigint**|Quantità totale di tempo di CPU, espresso in microsecondi (con precisione al millisecondo), impiegato per le esecuzioni del piano a partire dalla relativa compilazione.<br /><br /> Per le stored procedure compilate in modo nativo, il valore di **total_worker_time** non può essere accurato se più esecuzioni richiedono meno di 1 millisecondo.|  
|**last_worker_time**|**bigint**|Tempo di CPU, espresso in microsecondi (con precisione al millisecondo), impiegato per l'ultima esecuzione del piano. <sup>1</sup>|  
|**min_worker_time**|**bigint**|Tempo minimo di CPU, espresso in microsecondi (con precisione al millisecondo), mai impiegato dal piano durante una singola esecuzione. <sup>1</sup>|  
|**max_worker_time**|**bigint**|Tempo massimo di CPU, espresso in microsecondi (con precisione al millisecondo), mai impiegato dal piano durante una singola esecuzione. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|Numero totale di letture fisiche effettuate dalle esecuzioni del piano a partire dalla relativa compilazione.<br /><br /> È sempre 0 con esecuzione di query su una tabella ottimizzata per la memoria.|  
|**last_physical_reads**|**bigint**|Numero di letture fisiche eseguite durante l'ultima esecuzione del piano.<br /><br /> È sempre 0 con esecuzione di query su una tabella ottimizzata per la memoria.|  
|**min_physical_reads**|**bigint**|Numero minimo di letture fisiche effettuate dal piano durante una singola esecuzione.<br /><br /> È sempre 0 con esecuzione di query su una tabella ottimizzata per la memoria.|  
|**max_physical_reads**|**bigint**|Numero massimo di letture fisiche effettuate dal piano durante una singola esecuzione.<br /><br /> È sempre 0 con esecuzione di query su una tabella ottimizzata per la memoria.|  
|**total_logical_writes**|**bigint**|Numero totale di scritture logiche effettuate dalle esecuzioni del piano a partire dalla relativa compilazione.<br /><br /> È sempre 0 con esecuzione di query su una tabella ottimizzata per la memoria.|  
|**last_logical_writes**|**bigint**|Numero di pagine del pool di buffer diventate dirty durante durante l'ultima esecuzione completata del piano.<br /><br />Dopo che una pagina viene letta, la pagina diventa dirty solo la prima volta che viene modificato. Quando la pagina è dirty, questo numero viene incrementato. Le modifiche successive a una pagina dirty già non interessano questo numero.<br /><br />Questo numero sarà sempre 0 quando si eseguono query di una tabella con ottimizzazione per la memoria.|  
|**min_logical_writes**|**bigint**|Numero minimo di scritture logiche effettuate dal piano durante una singola esecuzione.<br /><br /> È sempre 0 con esecuzione di query su una tabella ottimizzata per la memoria.|  
|**max_logical_writes**|**bigint**|Numero massimo di scritture logiche effettuate dal piano durante una singola esecuzione.<br /><br /> È sempre 0 con esecuzione di query su una tabella ottimizzata per la memoria.|  
|**total_logical_reads**|**bigint**|Numero totale di letture logiche effettuate dalle esecuzioni del piano a partire dalla sua compilazione.<br /><br /> È sempre 0 con esecuzione di query su una tabella ottimizzata per la memoria.|  
|**last_logical_reads**|**bigint**|Numero di letture logiche effettuate durante l'ultima esecuzione del piano.<br /><br /> È sempre 0 con esecuzione di query su una tabella ottimizzata per la memoria.|  
|**min_logical_reads**|**bigint**|Numero minimo di letture logiche effettuate dal piano durante una singola esecuzione.<br /><br /> È sempre 0 con esecuzione di query su una tabella ottimizzata per la memoria.|  
|**max_logical_reads**|**bigint**|Numero massimo di letture logiche effettuate dal piano durante una singola esecuzione.<br /><br /> È sempre 0 con esecuzione di query su una tabella ottimizzata per la memoria.|  
|**total_clr_time**|**bigint**|Tempo, espresso in microsecondi (con precisione al millisecondo), utilizzati all'interno [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] oggetti common language runtime (CLR) dalle esecuzioni del piano dopo l'ultima compilazione. Gli oggetti CLR possono essere stored procedure, funzioni, trigger, tipi e aggregazioni.|  
|**last_clr_time**|**bigint**|Tempo, espresso in microsecondi (con precisione al millisecondo), impiegato dall'ultima esecuzione del piano all'interno di oggetti CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Gli oggetti CLR possono essere stored procedure, funzioni, trigger, tipi e aggregazioni.|  
|**min_clr_time**|**bigint**|Tempo minimo di CPU, espresso in microsecondi (con precisione al millisecondo), mai impiegato dal piano durante una singola esecuzione all'interno di oggetti CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Gli oggetti CLR possono essere stored procedure, funzioni, trigger, tipi e aggregazioni.|  
|**max_clr_time**|**bigint**|Tempo massimo di CPU, espresso in microsecondi (con precisione al millisecondo), mai impiegato dal piano durante una singola esecuzione all'interno di oggetti CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Gli oggetti CLR possono essere stored procedure, funzioni, trigger, tipi e aggregazioni.|  
|**total_elapsed_time**|**bigint**|Tempo totale trascorso, espresso in microsecondi (con precisione al millisecondo), per le esecuzioni completate di questo piano.|  
|**last_elapsed_time**|**bigint**|Tempo trascorso, espresso in microsecondi (con precisione al millisecondo), per le ultime esecuzioni completate di questo piano.|  
|**min_elapsed_time**|**bigint**|Tempo minimo trascorso, espresso in microsecondi (con precisione al millisecondo), per un'esecuzione completata di questo piano.|  
|**max_elapsed_time**|**bigint**|Tempo massimo trascorso, espresso in microsecondi (con precisione al millisecondo), per un'esecuzione completata di questo piano.|  
|**query_hash**|**Binary(8)**|Valore hash binario calcolato sulla query che consente di identificare query con logica analoga. È possibile utilizzare il valore hash della query per determinare l'utilizzo delle risorse aggregate per query che differiscono solo per valori letterali.|  
|**query_plan_hash**|**binary(8)**|Valore hash binario calcolato sul piano di esecuzione di query che consente di identificare piani di esecuzioni analoghi. È possibile utilizzare il valore hash del piano di query per individuare il costo cumulativo di query con piani di esecuzione analoghi.<br /><br /> È sempre 0x000 quando una stored procedure compilata in modo nativo esegue una query su una tabella ottimizzata per la memoria.|  
|**total_rows**|**bigint**|Numero totale di righe restituite dalla query. Non può essere null.<br /><br /> È sempre 0 quando una stored procedure compilata in modo nativo esegue una query su una tabella ottimizzata per la memoria.|  
|**last_rows**|**bigint**|Numero di righe restituite durante l'ultima esecuzione della query. Non può essere null.<br /><br /> È sempre 0 quando una stored procedure compilata in modo nativo esegue una query su una tabella ottimizzata per la memoria.|  
|**min_rows**|**bigint**|Numero minimo di righe che mai restituita dalla query durante l'esecuzione. Non può essere null.<br /><br /> È sempre 0 quando una stored procedure compilata in modo nativo esegue una query su una tabella ottimizzata per la memoria.|  
|**max_rows**|**bigint**|Numero massimo di righe che mai restituita dalla query durante l'esecuzione. Non può essere null.<br /><br /> È sempre 0 quando una stored procedure compilata in modo nativo esegue una query su una tabella ottimizzata per la memoria.|  
|**statement_sql_handle**|**varbinary(64)**|**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Popolato con valori non NULL solo se Query Store è attivata e raccogliere le statistiche per quel particolare query.|  
|**statement_context_id**|**bigint**|**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Popolato con valori non NULL solo se Query Store è attivata e raccogliere le statistiche per quel particolare query.|  
|**total_dop**|**bigint**|La somma totale dei gradi di parallelismo usato in questo piano dopo l'ultima compilazione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_dop**|**bigint**|Il grado di parallelismo quando questo piano di ultima esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_dop**|**bigint**|Il grado di parallelismo minimo questo piano già utilizzata durante l'esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_dop**|**bigint**|Il grado massimo di parallelismo questo piano già utilizzata durante l'esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_grant_kb**|**bigint**|La quantità totale di memoria riservata di concessione in KB questo piano ricevuto dopo l'ultima compilazione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_grant_kb**|**bigint**|La quantità di memoria riservata di concessione in KB quando questo piano di ultima esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_grant_kb**|**bigint**|La quantità minima di memoria riservata di concessione in KB questo piano mai ricevuto durante l'esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_grant_kb**|**bigint**|La quantità massima di memoria riservata di concessione in KB questo piano mai ricevuto durante l'esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_used_grant_kb**|**bigint**|La quantità totale di memoria riservata di concessione in KB questo piano usato dopo l'ultima compilazione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_used_grant_kb**|**bigint**|La quantità di concessione di memoria usata in KB quando questo piano di ultima esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_used_grant_kb**|**bigint**|Concessione della quantità minima di memoria usata in KB questo piano utilizzato durante l'esecuzione di uno. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_used_grant_kb**|**bigint**|Concessione della quantità massima di memoria usata in KB questo piano utilizzato durante l'esecuzione di uno. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_ideal_grant_kb**|**bigint**|La quantità totale di concessione di memoria ideale in KB, il piano stimato dopo l'ultima compilazione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_ideal_grant_kb**|**bigint**|Concessione della quantità di memoria ideale in KB quando questo piano di ultima esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_ideal_grant_kb**|**bigint**|Concessione della quantità minima di memoria ideale in KB, il piano stimato mai durante l'esecuzione di uno. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_ideal_grant_kb**|**bigint**|Concessione della quantità massima di memoria ideale in KB, il piano stimato mai durante un'esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_reserved_threads**|**bigint**|La somma totale dei parallelo riservato thread del piano che mai utilizzato dopo l'ultima compilazione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_reserved_threads**|**bigint**|Il numero di thread paralleli riservati quando questo piano di ultima esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_reserved_threads**|**bigint**|Il numero minimo di parallelo riservato thread del piano già utilizzato durante l'esecuzione.  Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_reserved_threads**|**bigint**|Il numero massimo di parallelo riservato thread del piano già utilizzato durante l'esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_used_threads**|**bigint**|La somma totale dei usati thread paralleli in questo piano mai utilizzato dopo l'ultima compilazione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_used_threads**|**bigint**|Il numero di thread paralleli usati quando il piano di ultima esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_used_threads**|**bigint**|Il numero minimo di thread paralleli usati questo piano è già utilizzato durante l'esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_used_threads**|**bigint**|Il numero massimo di thread paralleli usati questo piano è già utilizzato durante l'esecuzione. Sarà sempre 0 per query di una tabella con ottimizzazione per la memoria.<br /><br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_columnstore_segment_reads**|**bigint**|La somma totale dei segmenti columnstore lette dalla query. Non può essere null.<br /><br /> **Si applica a**: A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**last_columnstore_segment_reads**|**bigint**|Il numero di segmenti columnstore letto dall'ultima esecuzione della query. Non può essere null.<br /><br /> **Si applica a**: A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**min_columnstore_segment_reads**|**bigint**|Il numero minimo di mai lette dalla query durante l'esecuzione di uno dei segmenti columnstore. Non può essere null.<br /><br /> **Si applica a**: A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**max_columnstore_segment_reads**|**bigint**|Il numero massimo di segmenti columnstore mai lette dalla query durante l'esecuzione. Non può essere null.<br /><br /> **Si applica a**: A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**total_columnstore_segment_skips**|**bigint**|La somma totale dei segmenti columnstore ignorati dalla query. Non può essere null.<br /><br /> **Si applica a**: A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**last_columnstore_segment_skips**|**bigint**|Il numero di segmenti columnstore ignorati durante l'ultima esecuzione della query. Non può essere null.<br /><br /> **Si applica a**: A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**min_columnstore_segment_skips**|**bigint**|Il numero minimo di mai ignorate dalla query durante l'esecuzione di uno dei segmenti columnstore. Non può essere null.<br /><br /> **Si applica a**: A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**max_columnstore_segment_skips**|**bigint**|Il numero massimo di segmenti columnstore mai ignorate dalla query durante l'esecuzione. Non può essere null.<br /><br /> **Si applica a**: A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|
|**total_spills**|**bigint**|Il numero totale di pagine ha distribuito tramite l'esecuzione della query dopo l'ultima compilazione.<br /><br /> **Si applica a**: A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**last_spills**|**bigint**|Il numero di pagine ha distribuito l'ora dell'ultima che esecuzione della query.<br /><br /> **Si applica a**: A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**min_spills**|**bigint**|Il numero minimo di pagine in cui questa query è sempre stati distribuiti durante una singola esecuzione.<br /><br /> **Si applica a**: A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**max_spills**|**bigint**|Il numero massimo di pagine in cui questa query è sempre stati distribuiti durante una singola esecuzione.<br /><br /> **Si applica a**: A partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**pdw_node_id**|**int**|L'identificatore per il nodo in questa distribuzione.<br /><br /> **Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]| 
|**total_page_server_reads**|**bigint**|Numero totale di letture di server remoto pagine effettuate dalle esecuzioni del piano dopo l'ultima compilazione.<br /><br /> **Si applica a:** Azure SQL DB su scala molto vasta |  
|**last_page_server_reads**|**bigint**|Numero di letture di pagina remota server eseguita l'ultima volta che il piano è stato eseguito.<br /><br /> **Si applica a:** Azure SQL DB su scala molto vasta |  
|**min_page_server_reads**|**bigint**|Numero minimo di server remoto pagina legge che questo piano effettuate durante una singola esecuzione.<br /><br /> **Si applica a:** Azure SQL DB su scala molto vasta |  
|**max_page_server_reads**|**bigint**|Numero massimo di server remoto pagina legge che questo piano effettuate durante una singola esecuzione.<br /><br /> **Si applica a:** Azure SQL DB su scala molto vasta |  
> [!NOTE]
> <sup>1</sup> per le stored procedure compilate in modo nativo quando la raccolta delle statistiche è abilitata, tempo del processo viene raccolto in millisecondi. Se la query viene eseguita in meno di un millisecondo, il valore sarà 0.  
  
## <a name="permissions"></a>Permissions  

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], è necessario il `VIEW DATABASE STATE` autorizzazione nel database.   
   
## <a name="remarks"></a>Note  
 Le statistiche nella vista vengono aggiornate quando viene completata una query.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-finding-the-top-n-queries"></a>A. Ricerca delle prime n query  
 Nell'esempio seguente vengono restituite informazioni sulle prime cinque query classificate in base al tempo medio della CPU. Nell'esempio le query vengono aggregate in base al relativo valore hash del piano, in modo da raggruppare le query logicamente equivalenti in base all'utilizzo di risorse cumulativo.  
  
```sql  
SELECT TOP 5 query_stats.query_hash AS "Query Hash",   
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",  
    MIN(query_stats.statement_text) AS "Statement Text"  
FROM   
    (SELECT QS.*,   
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,  
    ((CASE statement_end_offset   
        WHEN -1 THEN DATALENGTH(ST.text)  
        ELSE QS.statement_end_offset END   
            - QS.statement_start_offset)/2) + 1) AS statement_text  
     FROM sys.dm_exec_query_stats AS QS  
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats  
GROUP BY query_stats.query_hash  
ORDER BY 2 DESC;  
```  
  
### <a name="b-returning-row-count-aggregates-for-a-query"></a>B. Restituzione di aggregazioni relative al conteggio delle righe per una query  
 Nell'esempio seguente vengono restituite le informazioni di aggregazione relative al conteggio delle righe (totale righe, numero minimo righe, numero massimo righe e ultime righe) per le query.  
  
```sql  
SELECT qs.execution_count,  
    SUBSTRING(qt.text,qs.statement_start_offset/2 +1,   
                 (CASE WHEN qs.statement_end_offset = -1   
                       THEN LEN(CONVERT(nvarchar(max), qt.text)) * 2   
                       ELSE qs.statement_end_offset end -  
                            qs.statement_start_offset  
                 )/2  
             ) AS query_text,   
     qt.dbid, dbname= DB_NAME (qt.dbid), qt.objectid,   
     qs.total_rows, qs.last_rows, qs.min_rows, qs.max_rows  
FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS qt   
WHERE qt.text like '%SELECT%'   
ORDER BY qs.execution_count DESC;  
```  
  
## <a name="see-also"></a>Vedere anche  
[Funzioni e viste a gestione dinamica relative all'esecuzione &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)    
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)    
[sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)     
[sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)     
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  


