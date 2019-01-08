---
title: Monitorare l'esecuzione di script R e Python usando viste a gestione dinamica (DMV) - SQL Server Machine Learning
description: Usare le viste a gestione dinamica (DMV) per monitorare l'esecuzione di script esterni di R e Python in SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0d07288bccc641f67644a37cd027e093fc3967c8
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645550"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>Il monitoraggio usando viste a gestione dinamica (DMV) di SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Utilizzare viste a gestione dinamica (DMV) per monitorare l'esecuzione di external script R e Python, risorse usate, diagnosticare i problemi e ottimizzare le prestazioni in SQL Server Machine Learning Services.

In questo articolo, sono disponibili le viste a gestione dinamica che sono specifici per SQL Server Machine Learning Services. Troverai anche query di esempio che mostra:

+ Le impostazioni e opzioni di configurazione per machine learning
+ Sessioni attive in esecuzione gli script R o Python esterni
+ Statistiche di esecuzione per il runtime esterno per R e Python
+ Contatori delle prestazioni per gli script esterni
+ Utilizzo della memoria per il sistema operativo, SQL Server e pool di risorse esterne
+ Configurazione della memoria per SQL Server e pool di risorse esterne
+ Pool di risorse, tra cui pool di risorse esterne
+ Pacchetti installati per R e Python

Per informazioni più generali sulle DMV, vedere [viste a gestione dinamica del sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).

> [!TIP]
> È anche possibile usare i report personalizzati per monitorare SQL Server Machine Learning Services. Per altre informazioni, vedere [monitorare machine learning usando i report personalizzati in Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="dynamic-management-views"></a>DMV

Le seguenti viste a gestione dinamica consente il monitoraggio di carichi di lavoro di machine learning in SQL Server. Per eseguire una query DMV, è necessario `VIEW SERVER STATE` l'autorizzazione per l'istanza.

| Vista a gestione dinamica | Tipo | Descrizione |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | Esecuzione | Restituisce una riga per ogni account di lavoro attivo che esegue uno script esterno. |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | Esecuzione | Restituisce una riga per ogni tipo di richiesta di script esterni. |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | Esecuzione | Restituisce una riga per contatore delle prestazioni gestito dal server. Se si usa la condizione di ricerca `WHERE object_name LIKE '%External Scripts%'`, è possibile usare queste informazioni per visualizzare quanti script sono stati eseguiti, che gli script sono stati eseguiti usando la modalità di autenticazione o quante R o chiamate di Python rilasciate nell'istanza complessivamente. |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | Resource Governor | Restituisce informazioni sullo stato corrente del pool risorse esterne di Resource Governor, la configurazione corrente del pool di risorse e le statistiche del pool di risorse. |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | Resource Governor | Restituisce informazioni di affinità della CPU sulla configurazione del pool di risorse esterne corrente in Resource Governor. Restituisce una riga per utilità di pianificazione in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], dove è stato eseguito il mapping di ogni utilità di pianificazione a un singolo processore. Utilizzare questa vista per eseguire il monitoraggio delle condizioni di un'utilità di pianificazione oppure per identificare eventuali attività sfuggite al controllo. |

Per informazioni sul monitoraggio [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] istanze, vedere [le viste del catalogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) e [Resource Governor correlati viste a gestione dinamica](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).

## <a name="settings-and-configuration"></a>Le impostazioni e configurazione

Visualizzare le opzioni di impostazione e configurazione di installazione servizi di Machine Learning.

![Query di configurazione dalle impostazioni di output](media/dmv-settings-and-configuration.png "query configurazione dalle impostazioni di Output")

Eseguire la query seguente per ottenere questo output. Per altre informazioni sulle viste e funzioni utilizzate, vedere [sys.dm_server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md), [Sys. Configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md), e [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md).

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

| colonna | Descrizione |
|--------|-------------|
| IsMLServicesInstalled | Restituisce 1 se è installato Servizi di SQL Server Machine Learning per l'istanza. In caso contrario, restituisce 0. |
| ExternalScriptsEnabled | Restituisce 1 se gli script esterni è abilitata per l'istanza. In caso contrario, restituisce 0. |
| ImpliedAuthenticationEnabled | Restituisce 1 se l'autenticazione implicita è abilitata. In caso contrario, restituisce 0. La configurazione per l'autenticazione implicita viene controllata tramite la verifica l'esistenza di un account di accesso per SQLRUserGroup. |
| IsTcpEnabled | Restituisce 1 se il protocollo TCP/IP è abilitato per l'istanza. In caso contrario, restituisce 0. Per altre informazioni, vedere [predefiniti SQL rete configurazione dei protocolli Server](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md). |

## <a name="active-sessions"></a>Sessioni attive

Visualizzare le sessioni attive in esecuzione di script esterni.

![L'output dalla query impostazioni attive](media/dmv-active-sessions.png "Output dalla query impostazioni attive")

Eseguire la query seguente per ottenere questo output. Per altre informazioni su viste a gestione dinamica utilizzati, vedere [exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md), [DM external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md), e [Sys. dm _](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md).

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

| colonna | Descrizione |
|--------|-------------|
| session_id | Identifica la sessione associata a ogni connessione principale attiva. |
| blocking_session_id | ID della sessione che sta bloccando la richiesta. Se questa colonna è NULL, la richiesta non è bloccata oppure non sono disponibili o identificabili informazioni di sessione per la sessione da cui è bloccata. |
| status | Stato della richiesta. |
| database_name | Nome del database corrente per ogni sessione. |
| login_name | Nome account di accesso di SQL Server in cui la sessione è attualmente in esecuzione. |
| wait_time | Se la richiesta è momentaneamente bloccata, in questa colonna viene restituita la durata dell'attesa corrente espressa in millisecondi. Non ammette i valori Null. |
| wait_type | Se la richiesta è momentaneamente bloccata, in questa colonna viene restituito il tipo di attesa. Per informazioni sui tipi di attese, vedere [DM os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). |
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

Visualizzare le statistiche di esecuzione per il runtime esterno per R e Python. Solo le statistiche di RevoScaleR o revoscalepy funzioni del pacchetto microsoftml sono attualmente disponibili.

![Output della query di statistiche di esecuzione](media/dmv-execution-statistics.png "Output dalla query di statistiche di esecuzione")

Eseguire la query seguente per ottenere questo output. Per ulteriori informazioni sulla vista a gestione dinamica utilizzata, vedere [DM external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). La query restituisce solo le funzioni che sono state eseguite più volte.

```sql
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

La query restituisce le colonne seguenti:

| colonna | Descrizione |
|--------|-------------|
| language | Nome del linguaggio di script esterni registrato. |
| counter_name | Nome di una funzione di script esterni registrata. |
| counter_value | Numero totale di istanze chiamate dalla funzione di script esterni registrata nel server. Questo valore è cumulativo, parte dall'ora di installazione della funzionalità nell'istanza e non può essere reimpostato. |

## <a name="performance-counters"></a>Contatori delle prestazioni

Visualizzare i contatori delle prestazioni relativi all'esecuzione di script esterni.

![Output dall'esecuzione di query dei contatori](media/dmv-performance-counters.png "Output dalle prestazioni di query dei contatori")

Eseguire la query seguente per ottenere questo output. Per ulteriori informazioni sulla vista a gestione dinamica utilizzata, vedere [DM os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md).

```sql
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**DM os_performance_counters** restituisce i seguenti contatori delle prestazioni per gli script esterni:

| Contatore | Descrizione |
|---------|-------------|
| Total Executions | Numero di processi esterni avviati da chiamate locali o remote. |
| Parallel Executions | Numero di volte in cui uno script ha incluso il _@parallel_ specifica e che [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] è stato in grado di generare e usare un piano di query parallele. |
| Streaming Executions | Numero di volte in cui la funzionalità di flusso è stata richiamata. |
| SQL CC Executions | Numero di script esterni eseguiti in cui la chiamata è stata creata un'istanza remota e SQL Server è stato usato come contesto di calcolo. |
| Implied Auth. Logins | Numero di volte in cui è stata effettuata una chiamata di loopback ODBC usando l'autenticazione implicita. vale a dire il [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] eseguito la chiamata per conto dell'utente che invia la richiesta di script. |
| Total Execution Time (ms) | Tempo trascorso tra la chiamata e il completamento della chiamata. |
| Execution Errors | Numero di volte in cui gli script hanno segnalato errori. Questo numero non include gli errori di R o Python. |

## <a name="memory-usage"></a>Utilizzo della memoria

Visualizzare le informazioni sulla quantità di memoria utilizzata dal sistema operativo, SQL Server e i pool esterni.

![Output della query di utilizzo memoria](media/dmv-memory-usage.png "Output dalla query di utilizzo di memoria")

Eseguire la query seguente per ottenere questo output. Per altre informazioni su viste a gestione dinamica utilizzati, vedere [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) e [DM os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md).

```sql
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

La query restituisce le colonne seguenti:

| colonna | Descrizione |
|--------|-------------|
| physical_memory_kb | La quantità totale di memoria fisica nel computer. |
| committed_kb | La memoria vincolata in kilobyte (KB) nel gestore della memoria. Non include la memoria riservata nel gestore della memoria. |
| external_pool_peak_memory_kb | La somma del la quantità massima di memoria utilizzata, in kilobyte, per tutti i pool di risorse esterne. |

## <a name="memory-configuration"></a>Configurazione della memoria

Visualizzare le informazioni sulla configurazione massima di memoria, espresso in percentuale di SQL Server e pool di risorse esterne. Se SQL Server è in esecuzione con il valore predefinito di `max server memory (MB)`, viene considerato 100% della memoria del sistema operativo.

![Output della query di configurazione della memoria](media/dmv-memory-configuration.png "Output dalla query di configurazione di memoria")

Eseguire la query seguente per ottenere questo output. Per altre informazioni sulle viste usati, vedere [Sys. Configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) e [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

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

| colonna | Descrizione |
|--------|-------------|
| NAME | Nome del pool di risorse esterne o SQL Server. |
| max_memory_percent | Memoria massima che è possibile usare SQL Server o il pool di risorse esterne. |

## <a name="resource-pools"></a>Pool di risorse

Nelle [SQL Server Resource Governor](../../relational-databases/resource-governor/resource-governor.md), un [pool di risorse](../../relational-databases/resource-governor/resource-governor-resource-pool.md) rappresenta un subset delle risorse fisiche di un'istanza. È possibile specificare limiti sulla quantità di CPU, i/o fisico e memoria che le richieste dell'applicazione in ingresso, compresa l'esecuzione di script esterni, è possono usare all'interno del pool di risorse. Visualizzare i pool di risorse usati per SQL Server e gli script esterni.

![Output dalla risorsa di pool di query](media/dmv-resource-pools.png "Output dalla risorsa di pool di query")

Eseguire la query seguente per ottenere questo output. Per altre informazioni su viste a gestione dinamica utilizzati, vedere [DM resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) e [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

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

| colonna | Descrizione |
|--------|-------------|
| pool_name | Nome del pool di risorse. I pool di risorse di SQL Server sono preceduti `SQL Server` e sono caratterizzate dal pool di risorse esterne `External Pool`.
| total_cpu_usage_hours | L'utilizzo cumulativo della CPU in millisecondi dal momento che sono state reimpostate le statistiche di Resource Govenor. |
| read_io_completed_total | Il totale degli I/O di lettura completati dalla reimpostazione delle statistiche di Resource Govenor. |
| write_io_completed_total | Il totale degli I/O di scrittura completati dalla reimpostazione delle statistiche di Resource Govenor. |

## <a name="installed-packages"></a>Pacchetti installati

È possibile per visualizzare i pacchetti R e Python che vengono installati in SQL Server Machine Learning Services eseguendo uno script R o Python che esegua l'output di questi.

### <a name="installed-packages-for-r"></a>I pacchetti installati per R

Visualizzare i pacchetti R installati in SQL Server Machine Learning Services.

![Output di pacchetti installati per la query di R](media/dmv-installed-packages-r.png "Output i pacchetti installati per la query di R")

Eseguire la query seguente per ottenere questo output. La query utilizzi uno script R per determinare i pacchetti R installati con SQL Server.

```sql
EXEC sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

Le colonne restituite sono:

| colonna | Descrizione |
|--------|-------------|
| Pacchetto | Nome del pacchetto installato. |
| Versione | Versione del pacchetto. |
| Dipende da | Elenca i pacchetti che dipende dal pacchetto installato. |
| Licenza | Licenza per il pacchetto installato. |
| LibPath | Directory in cui è possibile trovare il pacchetto. |

### <a name="installed-packages-for-python"></a>I pacchetti installati per Python

Visualizzare i pacchetti di Python installati in servizi di SQL Server Machine Learning.

![Output di pacchetti installati per la query di Python](media/dmv-installed-packages-python.png "Output i pacchetti installati per la query di Python")

Eseguire la query seguente per ottenere questo output. La query utilizza uno script Python per determinare i pacchetti di Python installati con SQL Server.

```sql
EXEC sp_execute_external_script @language = N'Python'
, @script = N'
import pip
OutputDataSet = pandas.DataFrame([(i.key, i.version, i.location) for i in pip.get_installed_distributions()])'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

Le colonne restituite sono:

| colonna | Descrizione |
|--------|-------------|
| Pacchetto | Nome del pacchetto installato. |
| Versione | Versione del pacchetto. |
| Località | Directory in cui è possibile trovare il pacchetto. |

## <a name="next-steps"></a>Passaggi successivi

+ [Gestione e monitoraggio delle soluzioni di apprendimento automatico](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
+ [Eventi estesi per machine learning](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)
+ [Viste a gestione dinamica relative a Resource Governor](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [Viste a gestione dinamica del sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [Monitorare machine learning usando i report personalizzati in Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)