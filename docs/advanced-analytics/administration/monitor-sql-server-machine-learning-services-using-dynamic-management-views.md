---
title: Monitorare l'esecuzione di script R e Python mediante le viste a gestione dinamica (DMV)
description: Usare le viste a gestione dinamica (DMV) per monitorare l'esecuzione di script esterni R e Python in SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 70c409af4e8cbca3d4005f54a0772a0fd4917381
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345218"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>Monitorare SQL Server Machine Learning Services mediante le viste a gestione dinamica (DMV)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Usare le viste a gestione dinamica (DMV) per monitorare l'esecuzione di script esterni (R e Python), le risorse usate, diagnosticare i problemi e ottimizzare le prestazioni in SQL Server Machine Learning Services.

In questo articolo si troveranno i DMV specifici per SQL Server Machine Learning Services. Sono inoltre disponibili query di esempio che mostrano:

+ Impostazioni e opzioni di configurazione per Machine Learning
+ Sessioni attive che eseguono script R o Python esterni
+ Statistiche di esecuzione per il runtime esterno per R e Python
+ Contatori delle prestazioni per gli script esterni
+ Utilizzo della memoria per il sistema operativo, SQL Server e i pool di risorse esterne
+ Configurazione della memoria per SQL Server e pool di risorse esterne
+ Resource Governor pool di risorse, inclusi i pool di risorse esterni
+ Pacchetti installati per R e Python

Per informazioni più generali su DMV, vedere [viste a gestione dinamica del sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).

> [!TIP]
> È anche possibile usare i report personalizzati per monitorare SQL Server Machine Learning Services. Per altre informazioni, vedere [monitorare l'apprendimento automatico usando report personalizzati in Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="dynamic-management-views"></a>DMV

Per il monitoraggio dei carichi di lavoro di Machine Learning in SQL Server, è possibile usare le viste a gestione dinamica seguenti. Per eseguire una query su DMV, `VIEW SERVER STATE` è necessaria l'autorizzazione per l'istanza di.

| Vista a gestione dinamica | type | Descrizione |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | Esecuzione | Restituisce una riga per ogni account di lavoro attivo che esegue uno script esterno. |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | Esecuzione | Restituisce una riga per ogni tipo di richiesta di script esterni. |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | Esecuzione | Restituisce una riga per contatore delle prestazioni gestito dal server. Se si usa la condizione `WHERE object_name LIKE '%External Scripts%'`di ricerca, è possibile usare queste informazioni per vedere il numero di script eseguiti, gli script eseguiti con la modalità di autenticazione o il numero di chiamate R o Python eseguite nell'istanza complessiva. |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | Resource Governor | Restituisce informazioni sullo stato corrente del pool di risorse esterne in Resource Governor, la configurazione corrente dei pool di risorse e le statistiche del pool di risorse. |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | Resource Governor | Restituisce le informazioni di affinità della CPU relative alla configurazione corrente del pool di risorse esterne in Resource Governor. Restituisce una riga per utilità di pianificazione in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], dove è stato eseguito il mapping di ogni utilità di pianificazione a un singolo processore. Utilizzare questa vista per eseguire il monitoraggio delle condizioni di un'utilità di pianificazione oppure per identificare eventuali attività sfuggite al controllo. |

Per informazioni sul monitoraggio [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] di istanze, vedere [viste del catalogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) e viste a [gestione dinamica correlate Resource Governor](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).

## <a name="settings-and-configuration"></a>Impostazioni e configurazione

Visualizzare l'impostazione di installazione Machine Learning Services e le opzioni di configurazione.

![Output delle impostazioni e della query di configurazione](media/dmv-settings-and-configuration.png "Output delle impostazioni e della query di configurazione")

Eseguire la query seguente per ottenere questo output. Per ulteriori informazioni sulle viste e sulle funzioni utilizzate, vedere [sys. dm _server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md), [sys.](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)Configurations e [ServerProperty](../../t-sql/functions/serverproperty-transact-sql.md).

```sql
SELECT CAST(SERVERPROPERTY('IsAdvancedAnalyticsInstalled') AS INT) AS IsMLServicesInstalled
    , CAST(value_in_use AS INT) AS ExternalScriptsEnabled
    , COALESCE(SIGN(SUSER_ID(CONCAT (
                    CAST(SERVERPROPERTY('MachineName') AS NVARCHAR(128))
                    , '\SQLRUserGroup'
                    , CAST(serverproperty('InstanceName') AS NVARCHAR(128))
                    ))), 0) AS ImpliedAuthenticationEnabled
    , COALESCE((
            SELECT CAST(r.value_data AS INT)
            FROM sys.dm_server_registry AS r
            WHERE r.registry_key LIKE 'HKLM\Software\Microsoft\Microsoft SQL Server\%\SuperSocketNetLib\Tcp'
            AND r.value_name = 'Enabled'
            ), - 1) AS IsTcpEnabled
FROM sys.configurations
WHERE name = 'external scripts enabled';
```

La query restituisce le colonne seguenti:

| Colonna | Descrizione |
|--------|-------------|
| IsMLServicesInstalled | Restituisce 1 se per l'istanza è installato SQL Server Machine Learning Services. In caso contrario, restituisce 0. |
| ExternalScriptsEnabled | Restituisce 1 se gli script esterni sono abilitati per l'istanza. In caso contrario, restituisce 0. |
| ImpliedAuthenticationEnabled | Restituisce 1 se è abilitata l'autenticazione implicita. In caso contrario, restituisce 0. La configurazione per l'autenticazione implicita viene verificata verificando l'esistenza di un account di accesso per SQLRUserGroup. |
| IsTcpEnabled | Restituisce 1 se il protocollo TCP/IP è abilitato per l'istanza di. In caso contrario, restituisce 0. Per ulteriori informazioni, vedere la pagina relativa alla [configurazione predefinita del protocollo di rete SQL Server](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md). |

## <a name="active-sessions"></a>Sessioni attive

Visualizzare le sessioni attive che eseguono script esterni.

![Output della query delle impostazioni attive](media/dmv-active-sessions.png "Output della query delle impostazioni attive")

Eseguire la query seguente per ottenere questo output. Per ulteriori informazioni sulle viste a gestione dinamica utilizzate, vedere [sys. dm _exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md), [sys. dm _external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)e [sys. dm _exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md).

```sql
SELECT r.session_id, r.blocking_session_id, r.status, DB_NAME(s.database_id) AS database_name
    , s.login_name, r.wait_time, r.wait_type, r.last_wait_type, r.total_elapsed_time, r.cpu_time
    , r.reads, r.logical_reads, r.writes, er.language, er.degree_of_parallelism, er.external_user_name
FROM sys.dm_exec_requests AS r
INNER JOIN sys.dm_external_script_requests AS er
ON r.external_script_request_id = er.external_script_request_id
INNER JOIN sys.dm_exec_sessions AS s
ON s.session_id = r.session_id;
```

La query restituisce le colonne seguenti:

| Colonna | Descrizione |
|--------|-------------|
| session_id | Identifica la sessione associata a ogni connessione principale attiva. |
| blocking_session_id | ID della sessione che sta bloccando la richiesta. Se questa colonna è NULL, la richiesta non è bloccata oppure non sono disponibili o identificabili informazioni di sessione per la sessione da cui è bloccata. |
| status | Stato della richiesta. |
| database_name | Nome del database corrente per ogni sessione. |
| login_name | SQL Server nome di accesso in cui è attualmente in esecuzione la sessione. |
| wait_time | Se la richiesta è momentaneamente bloccata, in questa colonna viene restituita la durata dell'attesa corrente espressa in millisecondi. Non ammette i valori Null. |
| wait_type | Se la richiesta è momentaneamente bloccata, in questa colonna viene restituito il tipo di attesa. Per informazioni sui tipi di attese, vedere [sys. dm _os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). |
| last_wait_type | Se la richiesta è stata precedentemente bloccata, questa colonna restituisce il tipo dell'ultima attesa. |
| total_elapsed_time | Tempo totale, in millisecondi, trascorso dall'arrivo della richiesta. |
| cpu_time | Tempo della CPU utilizzato dalla richiesta, espresso in millisecondi. |
| reads | Numero di letture effettuate dalla richiesta. |
| logical_reads | Numero di letture logiche effettuate dalla richiesta. |
| writes | Numero di scritture effettuate dalla richiesta. |
| language | Parola chiave che rappresenta un linguaggio di scripting supportato. |
| degree_of_parallelism | Numero che indica il numero di processi paralleli che sono stati creati. Questo valore potrebbe essere diverso dal numero di processi paralleli che sono stati richiesti. |
| external_user_name | Account di lavoro di Windows con cui è stato eseguito lo script. |

## <a name="execution-statistics"></a>Statistiche di esecuzione

Visualizzare le statistiche di esecuzione per il runtime esterno per R e Python. Sono attualmente disponibili solo le statistiche delle funzioni del pacchetto RevoScaleR, revoscalepy o microsoftml.

![Output della query statistiche di esecuzione](media/dmv-execution-statistics.png "Output della query statistiche di esecuzione")

Eseguire la query seguente per ottenere questo output. Per ulteriori informazioni sulla vista a gestione dinamica utilizzata, vedere [sys. dm _external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). La query restituisce solo le funzioni che sono state eseguite più di una volta.

```sql
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

La query restituisce le colonne seguenti:

| Colonna | Descrizione |
|--------|-------------|
| language | Nome del linguaggio di script esterni registrato. |
| counter_name | Nome di una funzione di script esterni registrata. |
| counter_value | Numero totale di istanze chiamate dalla funzione di script esterni registrata nel server. Questo valore è cumulativo, parte dall'ora di installazione della funzionalità nell'istanza e non può essere reimpostato. |

## <a name="performance-counters"></a>Contatori delle prestazioni

Consente di visualizzare i contatori delle prestazioni correlati all'esecuzione di script esterni.

![Output della query dei contatori delle prestazioni](media/dmv-performance-counters.png "Output della query dei contatori delle prestazioni")

Eseguire la query seguente per ottenere questo output. Per ulteriori informazioni sulla vista a gestione dinamica utilizzata, vedere [sys. dm _os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md).

```sql
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**sys. dm _os_performance_counters** restituisce i contatori delle prestazioni seguenti per gli script esterni:

| Contatore | Descrizione |
|---------|-------------|
| Total Executions | Numero di processi esterni avviati da chiamate locali o remote. |
| Parallel Executions | Numero di volte in cui uno script includeva la _@parallel_ specifica e che [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] era in grado di generare e utilizzare un piano di query parallelo. |
| Streaming Executions | Numero di volte in cui è stata richiamata la funzionalità di streaming. |
| SQL CC Executions | Numero di script esterni eseguiti in cui è stata creata un'istanza remota della chiamata e SQL Server è stato usato come contesto di calcolo. |
| Implied Auth. Logins | Numero di volte in cui è stata effettuata una chiamata di loopback ODBC utilizzando l'autenticazione implicita. ovvero, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ha eseguito la chiamata per conto dell'utente che ha inviato la richiesta di script. |
| Total Execution Time (ms) | Tempo trascorso tra la chiamata e il completamento della chiamata. |
| Execution Errors | Numero di volte in cui gli script hanno segnalato errori. Questo conteggio non include errori di R o Python. |

## <a name="memory-usage"></a>Utilizzo memoria

Visualizzare le informazioni sulla memoria usata dal sistema operativo, SQL Server e i pool esterni.

![Output della query sull'utilizzo della memoria](media/dmv-memory-usage.png "Output della query sull'utilizzo della memoria")

Eseguire la query seguente per ottenere questo output. Per ulteriori informazioni sulle viste a gestione dinamica utilizzate, vedere [sys. dm _resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) e [sys. dm _os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md).

```sql
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

La query restituisce le colonne seguenti:

| Colonna | Descrizione |
|--------|-------------|
| physical_memory_kb | Quantità totale di memoria fisica nel computer. |
| committed_kb | Memoria di cui è stato eseguito il commit in kilobyte (KB) nel gestore della memoria. Non include la memoria riservata nel gestore della memoria. |
| external_pool_peak_memory_kb | Somma della quantità massima di memoria utilizzata, in kilobyte, per tutti i pool di risorse esterni. |

## <a name="memory-configuration"></a>Configurazione della memoria

Visualizzare informazioni sulla configurazione della memoria massima in percentuale di SQL Server e pool di risorse esterne. Se SQL Server è in esecuzione con il valore `max server memory (MB)`predefinito, viene considerato come 100% della memoria del sistema operativo.

![Output dalla query di configurazione della memoria](media/dmv-memory-configuration.png "Output dalla query di configurazione della memoria")

Eseguire la query seguente per ottenere questo output. Per ulteriori informazioni sulle viste utilizzate, vedere [sys.](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) Configurations e [sys. dm _resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

```sql
SELECT 'SQL Server' AS name
    , CASE CAST(c.value AS BIGINT)
        WHEN 2147483647 THEN 100
        ELSE (SELECT CAST(c.value AS BIGINT) / (physical_memory_kb / 1024.0) * 100 FROM sys.dm_os_sys_info)
        END AS max_memory_percent
FROM sys.configurations AS c
WHERE c.name LIKE 'max server memory (MB)'
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name, ep.max_memory_percent
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

La query restituisce le colonne seguenti:

| Colonna | Descrizione |
|--------|-------------|
| name | Nome del pool di risorse esterno o SQL Server. |
| max_memory_percent | Quantità massima di memoria che può essere utilizzata da SQL Server o dal pool di risorse esterne. |

## <a name="resource-pools"></a>Pool di risorse

In [SQL Server Resource Governor](../../relational-databases/resource-governor/resource-governor.md), un [pool di risorse](../../relational-databases/resource-governor/resource-governor-resource-pool.md) rappresenta un subset delle risorse fisiche di un'istanza di. È possibile specificare limiti sulla quantità di CPU, i/o fisico e memoria che le richieste dell'applicazione in ingresso, inclusa l'esecuzione di script esterni, possono usare nel pool di risorse. Consente di visualizzare i pool di risorse utilizzati per SQL Server e gli script esterni.

![Output dalla query dei pool di risorse](media/dmv-resource-pools.png "Output dalla query dei pool di risorse")

Eseguire la query seguente per ottenere questo output. Per ulteriori informazioni sulle viste a gestione dinamica utilizzate, vedere [sys. dm _resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) e [sys. dm _resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

```sql
SELECT CONCAT ('SQL Server - ', p.name) AS pool_name
    , p.total_cpu_usage_ms, p.read_io_completed_total, p.write_io_completed_total
FROM sys.dm_resource_governor_resource_pools AS p
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name
    , ep.total_cpu_user_ms, ep.read_io_count, ep.write_io_count
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

La query restituisce le colonne seguenti:

| Colonna | Descrizione |
|--------|-------------|
| pool_name | Nome del pool di risorse. I pool di risorse SQL Server sono preceduti da `SQL Server` e i pool di risorse esterne sono preceduti da. `External Pool`
| total_cpu_usage_hours | Utilizzo cumulativo della CPU in millisecondi dal momento in cui sono state reimpostate le statistiche di Resource Govenor. |
| read_io_completed_total | Il totale degli I/O di lettura completati dalla reimpostazione delle statistiche di Resource Govenor. |
| write_io_completed_total | Il totale degli I/O di scrittura completati dalla reimpostazione delle statistiche di Resource Govenor. |

## <a name="installed-packages"></a>Pacchetti installati

È possibile visualizzare i pacchetti R e Python installati in SQL Server Machine Learning Services eseguendo uno script R o Python che li restituisce.

### <a name="installed-packages-for-r"></a>Pacchetti installati per R

Visualizzare i pacchetti R installati in SQL Server Machine Learning Services.

![Output dei pacchetti installati per la query R](media/dmv-installed-packages-r.png "Output dei pacchetti installati per la query R")

Eseguire la query seguente per ottenere questo output. La query usa uno script R per determinare i pacchetti R installati con SQL Server.

```sql
EXEC sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

Le colonne restituite sono:

| Colonna | Descrizione |
|--------|-------------|
| Pacchetto | Nome del pacchetto installato. |
| Version | Versione del pacchetto. |
| Dipende da | Elenca i pacchetti da cui dipende il pacchetto installato. |
| Licenza | Licenza per il pacchetto installato. |
| LibPath | Directory in cui è possibile trovare il pacchetto. |

### <a name="installed-packages-for-python"></a>Pacchetti installati per Python

Visualizzare i pacchetti Python installati in SQL Server Machine Learning Services.

![Output della query sui pacchetti installati per Python](media/dmv-installed-packages-python.png "Output della query sui pacchetti installati per Python")

Eseguire la query seguente per ottenere questo output. La query usa uno script Python per determinare i pacchetti Python installati con SQL Server.

```sql
EXEC sp_execute_external_script @language = N'Python'
, @script = N'
import pip
OutputDataSet = pandas.DataFrame([(i.key, i.version, i.location) for i in pip.get_installed_distributions()])'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

Le colonne restituite sono:

| Colonna | Descrizione |
|--------|-------------|
| Pacchetto | Nome del pacchetto installato. |
| Version | Versione del pacchetto. |
| Location | Directory in cui è possibile trovare il pacchetto. |

## <a name="next-steps"></a>Passaggi successivi

+ [Gestione e monitoraggio delle soluzioni di apprendimento automatico](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
+ [Eventi estesi per Machine Learning](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)
+ [Viste a gestione dinamica relative a Resource Governor](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [Viste a gestione dinamica di sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [Monitorare Machine Learning usando report personalizzati in Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)