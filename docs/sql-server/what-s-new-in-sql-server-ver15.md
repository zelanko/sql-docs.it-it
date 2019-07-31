---
title: Novità di SQL Server 2019 | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d988fc9dfc126bef79d94ca0867128085069456e
ms.sourcegitcommit: 63c6f3758aaacb8b72462c2002282d3582460e0b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68495444"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>Novità di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] si basa sulle versioni precedenti per sviluppare SQL Server come piattaforma che offre una scelta di linguaggi di sviluppo, tipi di dati, sistemi operativi ed elaborazione locale o nel cloud.

Questo articolo riepiloga le nuove funzionalità e i miglioramenti per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Per altre informazioni e problemi noti, vedere le [Note sulla versione di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-ver15-release-notes.md).

**Usare gli [strumenti più recenti](what-s-new-in-sql-server-ver15-prerelease.md#tools) per un'esperienza ottimale con [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].**

## <a name="ctp-32-july-2019"></a>CTP 3.2 luglio 2019

Community Technology Preview (CTP) 3.2 è la versione pubblica più recente di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Questa versione include miglioramenti delle versioni CTP precedenti per la correzione di bug, il miglioramento della sicurezza e l'ottimizzazione delle prestazioni. Per un elenco delle funzionalità introdotte o migliorate in ognuna delle versioni CTP precedenti a [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2, vedere [Archivio degli annunci per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP](what-s-new-in-sql-server-ver15-prerelease.md).

### <a name="new-in-big-data-clusters"></a>Novità per i cluster Big Data

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Anteprima pubblica |Prima della versione CTP 3.2, il cluster Big Data di SQL Server era disponibile per gli early adopter registrati. Questa versione consente a chiunque di sperimentare le funzionalità dei cluster Big Data di SQL Server. <br/><br/> Vedere [Introduzione ai cluster Big Data di SQL Server](../big-data-cluster/deploy-get-started.md).|
|`azdata` |CTP 3.2 introduce `azdata`, un'utilità da riga di comando scritta in Python che consente agli amministratori del cluster di avviare e gestire il cluster Big Data tramite le API REST. `azdata` sostituisce `mssqlctl`. Vedere [Installare `azdata`](../big-data-cluster/deploy-install-azdata.md). |
|PolyBase |I nomi delle colonne della tabella esterna vengono ora usati per eseguire query su origini dati SQL Server, Oracle, Teradata, MongoDB e ODBC. Nelle versioni CTP precedenti, le colonne venivano associate solo in base al numero ordinale nella destinazione e i nomi di colonna nella definizione della tabella esterna non venivano usati.|
|Aggiornamento della suddivisione in livelli HDFS |Introduzione della funzionalità di aggiornamento per la suddivisione in livelli HDFS, in modo che sia possibile aggiornare un montaggio esistente per l'ultimo snapshot dei dati remoti. Vedere [Suddivisione in livelli HDFS](../big-data-cluster/hdfs-tiering.md) |
|Risoluzione dei problemi basata su notebook |CTP 3.2 introduce notebook Jupyter per semplificare la [distribuzione](../big-data-cluster/deploy-notebooks.md) e l'[individuazione, la diagnosi e la risoluzione dei problemi](../big-data-cluster/manage-notebooks.md) per i componenti in un cluster Big Data di SQL Server. |
| &nbsp; | &nbsp; |

### <a name="new-in-analysis-services"></a>Novità di Analysis Services

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---| 
| Impostazione di governance per gli aggiornamenti della cache di Power BI.  | Il servizio Power BI memorizza nella cache i dati dei riquadri del dashboard e i dati del report per il caricamento iniziale del report Live Connect, causando un numero eccessivo di query della cache inviate a SSAS e in casi estremi il sovraccarico del server. In questa versione è stata introdotta la proprietà **ClientCacheRefreshPolicy**. Questa proprietà consente di eseguire l'override di questo comportamento a livello di server. Per altre informazioni, vedere [Proprietà generali](../analysis-services/server-properties/general-properties.md). |
| Collegamento online  | Questa funzionalità offre la possibilità di collegare un modello tabulare come operazione online. Il collegamento online può essere usato per la sincronizzazione di repliche di sola lettura negli ambienti con scalabilità orizzontale delle query locali. Per altre informazioni, vedere [Collegamento online](what-s-new-in-sql-server-ver15-prerelease.md#online-attach-ctp32) in Dettagli. |
| &nbsp; | &nbsp; |

### <a name="new-in-language-extensions"></a>Novità per le estensioni del linguaggio

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Nuovo runtime Java predefinito  | SQL Server ora include il supporto di Zulu Embedded per Java di Azul System in tutto il prodotto. Per altre informazioni, vedere [Free supported Java in SQL Server 2019 is now available](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/) (È ora disponibile il supporto gratuito di Java in SQL Server 2019). |

### <a name="new-in-sql-server-on-linux"></a>Novità per SQL Server in Linux

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Supporto di Change Data Capture (CDC) | Change Data Capture (CDC) è ora supportato in Linux per SQL Server 2019. |

## <a name="includesql-server-2019includessssqlv15-mdmd-features-by-component"></a>Funzionalità di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] per componente

Nelle sezioni seguenti vengono illustrati i nuovi componenti e le funzionalità migliorate nelle versioni precedenti di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## <a name="big-data-clusters"></a>Cluster di Big Data

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Soluzione Big Data scalabile | [Distribuire cluster scalabili](../big-data-cluster/deploy-get-started.md) di contenitori SQL Server, Spark e HDFS in esecuzione in Kubernetes <br/><br/> Leggere, scrivere ed elaborare Big Data da Transact-SQL o Spark<br/><br/> Combinare e analizzare con facilità dati relazionali di alto valore con volumi elevati di Big Data<br/><br/>Eseguire query su origini dati esterne<br/><br/>Archiviare Big Data in HDFS gestito da SQL Server<br/><br/>Eseguire query sui dati da più origini dati esterne tramite il cluster<br/><br/> Usare i dati per intelligenza artificiale, Machine Learning e altre attività di analisi<br/><br/> Distribuire ed eseguire applicazioni in cluster Big Data <br/>|
| &nbsp; | &nbsp; |

Per altri dettagli, vedere [Che cosa sono i cluster Big Data di SQL Server](../big-data-cluster/big-data-cluster-overview.md)

L'[archivio degli annunci per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] (CTP)](what-s-new-in-sql-server-ver15-prerelease.md) contiene un elenco delle funzionalità annunciate e modificate per tutte le versioni CTP precedenti di questa funzionalità.

## <a name="database-engine"></a>Motore di database

### <a name="security"></a>Security

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Limitazioni delle funzionalità| Evitare che alcune forme di SQL injection causino la divulgazione di informazioni sul database, anche quando l'attacco SQL injection riesce. Vedere [Limitazioni delle funzionalità](../relational-databases/security/feature-restrictions.md)|
|Indicizzare le colonne crittografate|Creare indici sulle colonne crittografate usando la crittografia casuale e le chiavi abilitate per l'enclave, per migliorare le prestazioni delle query avanzate (in cui vengono usati `LIKE` e operatori di confronto). Vedere [Always Encrypted con enclave sicuri](../relational-databases/security/encryption/always-encrypted-enclaves.md).
|Sospendere e riprendere l'analisi iniziale per Transparent Data Encryption (TDE)|Vedere [Analisi Transparent Data Encryption (TDE) con possibilità di sospensione e ripresa](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)|
|Gestione dei certificati in Gestione configurazione SQL Server|Vedere [Gestione dei certificati (Gestione configurazione SQL Server)](../database-engine/configure-windows/manage-certificates.md)
| &nbsp; | &nbsp; |


### <a name="graph"></a>Grafico

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Azioni di eliminazione propagate su un vincolo di arco |Definire azioni di eliminazione propagate su un vincolo ad arco in a database a grafo. Vedere [Vincoli di arco](../relational-databases/tables/graph-edge-constraints.md). |
|Nuova funzione grafo: `SHORTEST_PATH` | Usare `SHORTEST_PATH` all'interno di `MATCH` per trovare il percorso più breve tra due nodi in un grafo o eseguire attraversamenti di lunghezza arbitraria.|
|Partizionare tabelle e indici| I dati di tabelle e indici partizionati vengono divisi in unità distribuibili tra più filegroup in un database a grafo. |
|Usare alias di tabelle o viste derivate nelle query corrispondenti ai grafi |Vedere [Vincoli di arco dei grafi](../relational-databases/tables/graph-edge-constraints.md). |
| &nbsp; | &nbsp; |

### <a name="indexes"></a>Indici

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|Attiva un'ottimizzazione all'interno del motore di database che contribuisce a migliorare la velocità effettiva per gli inserimenti nell'indice con un elevato grado di concorrenza. Questa opzione è destinata agli indici che sono soggetti a conflitti di inserimento dell'ultima pagina, che generalmente si verificano con gli indici con una chiave sequenziale, come una colonna Identity, una sequenza o una colonna di data/ora. Per altre informazioni, vedere [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys).|
|Compilare e ricompilare gli indici columnstore cluster online | Vedere [Eseguire operazioni online sugli indici](../relational-databases/indexes/perform-index-operations-online.md). |
| &nbsp; | &nbsp; |

### <a name="in-memory-databases"></a>Database in memoria

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Controllo DDL per il pool di buffer ibrido |Il [pool di buffer ibrido](../database-engine/configure-windows/hybrid-buffer-pool.md) consente di accedere direttamente alle pagine di database che si trovano in un dispositivo con memoria persistente, qualora sia necessario.|
|Metadati tempdb ottimizzati per la memoria|Vedere [Metadati tempdb ottimizzati per la memoria](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata)|
| &nbsp; | &nbsp; |

### <a name="linked-servers"></a>Server collegati

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Codifica dei caratteri UTF-8 per supporto server collegati. |[Regole di confronto e supporto Unicode](../relational-databases/collations/collation-and-unicode-support.md) |
| &nbsp; | &nbsp; |

### <a name="polybase"></a>PolyBase

| Nuova funzionalità o aggiornamento | Dettagli | PolyBase | I nomi delle colonne della tabella esterna vengono ora usati per eseguire query in origini dati SQL Server, Oracle, Teradata, MongoDB e ODBC. | | &nbsp; | &nbsp; |

### <a name="collation"></a>Regole di confronto

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Supporta la codifica di caratteri UTF-8 |Abilitato per le regole di confronto BIN2 (`Latin1_General_100_BIN2_UTF8`). Vedere [Regole di confronto e supporto Unicode](../relational-databases/collations/collation-and-unicode-support.md). |
|Selezionare le regole di confronto UTF-8 come impostazione predefinita durante l'installazione | Vedere [Regole di confronto e supporto Unicode](../relational-databases/collations/collation-and-unicode-support.md#ctp23). |
| &nbsp; | &nbsp; |

### <a name="server-settings"></a>Impostazioni del server

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Impostare i valori `MIN` e `MAX` per la memoria del server al momento dell'installazione |Durante l'installazione è possibile impostare i valori per la memoria del server. Usare i valori predefiniti, i valori consigliati calcolati oppure specificare manualmente i valori personalizzati dopo aver scelto l'opzione **Consigliato** [Opzioni di configurazione del server Server Memory](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually).|
|Il programma di installazione di SQL Server abilita le impostazioni MAXDOP |Le nuove raccomandazioni seguono le linee guida documentate. [Configurare l'opzione di configurazione del server max degree of parallelism](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)|
|Pool di buffer ibrido| Nuova funzionalità del motore di database di SQL Server con la quale le pagine del database che si trovano in file di database posizionati in un dispositivo di memoria persistente (PMEM) saranno accessibili direttamente quando necessario. Vedere [Pool di buffer ibrido](../database-engine/configure-windows/hybrid-buffer-pool.md).|
| &nbsp; | &nbsp; |

### <a name="performance-monitoring"></a>Monitoraggio delle prestazioni

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Inlining di funzioni definite dall'utente scalari |Trasforma automaticamente le funzioni definite dall'utente scalari in espressioni relazionali e le incorpora nella query SQL chiamante. Vedere [Inlining di funzioni definite dall'utente scalari](../relational-databases/user-defined-functions/scalar-udf-inlining.md). |
| `sys.dm_exec_requests` colonna `command` | Mostra `SELECT (STATMAN)` se un'operazione `SELECT` è in attesa del completamento di un'operazione di aggiornamento delle statistiche sincrona prima di continuare l'esecuzione di query. Vedere [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | Nuovo tipo di attesa nella DMV `sys.dm_os_wait_stats`. Mostra il tempo accumulato a livello di istanza dedicato alle operazioni di aggiornamento delle statistiche sincrone. Vedere [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|
|Criteri di acquisizione personalizzati per Query Store|Una volta abilitate, le configurazioni aggiuntive di Query Store sono disponibili in una nuova impostazione di criteri di acquisizione di Query Store, per ottimizzare la raccolta dei dati in un server specifico. Per altre informazioni, vedere [Opzioni ALTER DATABASE SET](../t-sql/statements/alter-database-transact-sql-set-options.md).|
|`sys.dm_exec_query_plan_stats` |La nuova funzione a gestione dinamica restituisce l'equivalente dell'ultimo piano di esecuzione effettivo noto per la maggior parte delle query. Vedere [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md).|
|`LAST_QUERY_PLAN_STATS` | Nuova configurazione con ambito database per abilitare `sys.dm_exec_query_plan_stats`. Vedere [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|`LIGHTWEIGHT_QUERY_PROFILING`|Nuova configurazione con ambito database. Vedere [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp). |
|`query_post_execution_plan_profile` | L'evento esteso raccoglie l'equivalente di un piano di esecuzione effettivo in base alla profilatura leggera, a differenza di `query_post_execution_showplan` che usa la profilatura standard. Vedere [Infrastruttura di profilatura query](../relational-databases/performance/query-profiling-infrastructure.md).|
|Feedback delle concessioni di memoria in modalità riga. |[Feedback delle concessioni di memoria in modalità riga](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback) |
|Compilazione posticipata delle variabili di tabella.|[Compilazione posticipata delle variabili di tabella](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation) |
|Approssimazione di `COUNT DISTINCT`.|[Elaborazione delle query approssimativa](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing)|
|Modalità batch per rowstore.|[Modalità batch per rowstore](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore) |

### <a name="language-extensions"></a>Estensioni del linguaggio

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Nuovo SDK del linguaggio Java | Semplifica lo sviluppo di applicazioni Java eseguibili da SQL Server. Vedere [Novità - Machine Learning Services di SQL Server](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md). |
|Estensioni del linguaggio di SQL Server - [Estensione per il linguaggio Java](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)|[Microsoft Extensibility SDK per Java per Microsoft SQL Server](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) è ora open source e [disponibile in GitHub](https://github.com/microsoft/sql-server-language-extensions).|
|Registrare i linguaggi esterni|La nuova DDL, `CREATE EXTERNAL LANGUAGE`, registra i linguaggi esterni, come ad esempio Java, in SQL Server. Vedere [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md). |
|Supporto per i tipi di dati Java|Vedere [Java data types](../language-extensions/how-to/java-to-sql-data-types.md) (Tipi di dati Java).|

### <a name="spatial"></a>Spaziale

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Nuovi identificatori SRID (Spatial Reference Identifier) |[Australian GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) offre dati più stabili e accurati, più strettamente allineati ai sistemi di posizionamento globale. I nuovi identificatori SRID sono:<br/><br/> - 7843 - 2D geografico<br/> - 7844 - 3D geografico <br/><br/>La vista [sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) contiene le definizioni dei nuovi identificatori SRID. |
| &nbsp; | &nbsp; |

### <a name="performance"></a>Prestazioni

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Recupero del database accelerato | Abilitare il recupero accelerato del database per ogni database. Vedere [Recupero del database accelerato](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr).|
|Uso forzato di cursori statici e fast forward | Supporto dell'uso forzato del piano di Query Store per cursori statici e fast forward. Vedere [Supporto dell'uso forzato del piano per cursori fast forward e statici](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23).|
|Riduzione delle ricompilazioni per i carichi di lavoro| Migliora l'utilizzo di tabelle temporanee in più ambiti. Vedere [Riduzione delle ricompilazioni per i carichi di lavoro](../relational-databases/tables/tables.md#ctp23) |
|Scalabilità per il checkpoint indiretto |Vedere [Scalabilità migliorata per il checkpoint indiretto](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23).|
| &nbsp; | &nbsp; |

### <a name="availability-groups"></a>Gruppi di disponibilità

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Fino a cinque repliche sincrone|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] aumenta il numero massimo di repliche sincrone fino a 5. Il numero massimo era 3 in [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. È possibile configurare questo gruppo di cinque repliche per il failover automatico all'interno del gruppo. Sono presenti una replica primaria e 4 repliche secondarie sincrone.|
|Reindirizzamento della connessione di replica da secondaria a primaria| consente di orientare le connessioni dell'applicazione client alla replica primaria, indipendentemente dal server di destinazione specificato nella stringa di connessione. Per informazioni dettagliate, vedere [Secondary to primary replica read/write connection redirection (Always On Availability Groups)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md) (Reindirizzamento connessione in lettura/scrittura dalla replica secondaria alla primaria (Gruppi di disponibilità AlwaysOn)).|
| &nbsp; | &nbsp; |

### <a name="error-messages"></a>Messaggi di errore

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Avvisi di troncamento dettagliati | Il messaggio di errore di troncamento include per impostazione predefinita i nomi di tabelle e colonne e il valore troncato. Vedere [VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation).|
| &nbsp; | &nbsp; |

## <a name="sql-server-on-linux"></a>SQL Server in Linux

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Nuovo registro contenitori|[Introduzione ai contenitori di SQL Server in Docker](../linux/quickstart-install-connect-docker.md) |
|Gruppo di disponibilità AlwaysOn in contenitori Docker con Kubernetes |[Gruppi di disponibilità Always On per i contenitori](../linux/sql-server-ag-kubernetes.md) |
|Supporto della replica |[Replica di SQL Server in Linux](../linux/sql-server-linux-replication.md)
|Supporto di Microsoft Distributed Transaction Coordinator (MSDTC) |[Come configurare MSDTC in Linux](../linux/sql-server-linux-configure-msdtc.md) |
|Supporto OpenLDAP per provider AD di terze parti |[Esercitazione: Usare l'autenticazione di Azure Active Directory con SQL Server in Linux](../linux/sql-server-linux-active-directory-authentication.md) |
|Machine Learning in Linux |[Configurare Machine Learning in Linux](../linux/sql-server-linux-setup-machine-learning.md) |
|Miglioramenti di tempdb | Per impostazione predefinita, una nuova installazione di SQL Server in Linux crea più file di dati tempdb in base al numero di core logici (con un massimo di 8 file di dati). Questo non vale per gli aggiornamenti sul posto di una versione principale o secondaria. Ogni file tempdb è di 8 MB, con un aumento automatico di 64 MB. Questo comportamento è simile all'installazione predefinita di SQL Server in Windows. |
| PolyBase in Linux | [Installare PolyBase](../relational-databases/polybase/polybase-linux-setup.md) in Linux per i connettori non Hadoop.<br/><br/>[Mapping dei tipi di PolyBase](../relational-databases/polybase/polybase-type-mapping.md). |
| &nbsp; | &nbsp; |

## <a id="ml"></a> SQL Server Machine Learning Services

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Modellazione basata sulle partizioni|elabora gli script esterni per le singole partizioni dei dati usando i nuovi parametri aggiunti a `sp_execute_external_script`. Questa funzionalità supporta il training di molti modelli di dimensioni ridotte (un modello per ogni partizione dei dati) invece del training di un solo modello di grandi dimensioni. Vedere [Creare modelli basati sulla partizione](../advanced-analytics/tutorials/r-tutorial-create-models-per-partition.md)|
|Cluster di failover di Windows Server| è possibile configurare la disponibilità elevata per Machine Learning Services in un cluster di failover di Windows Server.|
| &nbsp; | &nbsp; |

## [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Supporta i database dell'istanza gestita del database SQL di Azure.| Ospitare [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] in un'istanza gestita. Vedere [[!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]Installazione e configurazione](../master-data-services/master-data-services-installation-and-configuration.md#SetUpWeb).|
|Nuovi controlli HTML| I controlli HTML sostituiscono tutti i componenti di Silverlight precedenti. La dipendenza da Silverlight è stata rimossa.|
| &nbsp; | &nbsp; |

## <a name="analysis-services"></a>Analysis Services

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Gruppi di calcolo in modelli tabulari| [Gruppi di calcolo in modelli tabulari](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24) |
|Supporto di query MDX per modelli tabulari con i gruppi di calcolo | Vedere [Gruppi di calcolo](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). |
|Formattazione dinamica delle misure con i gruppi di calcolo |Questa funzionalità consente di modificare in modo condizionale le stringhe di formato per le misure con i [gruppi di calcolo](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). Ad esempio, con la conversione di valuta una misura può essere visualizzata usando formati di valuta diversi.|
|Relazioni molti-a-molti nei modelli tabulari|[Relazioni molti-a-molti nei modelli tabulari](what-s-new-in-sql-server-ver15-prerelease.md#many-to-many-ctp24)|
|Impostazioni delle proprietà per la governance delle risorse|[Impostazioni delle proprietà per la governance delle risorse](what-s-new-in-sql-server-ver15-prerelease.md#property-ctp24)|
| &nbsp; | &nbsp; |

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

Per funzionalità specifiche escluse dal supporto, vedere le [note sulla versione](sql-server-ver15-release-notes.md).

In [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2 sono state anche aggiunte o migliorate le funzionalità seguenti.

## <a name="see-also"></a>Vedere anche

- [`SqlServer` Modulo PowerShell](https://www.powershellgallery.com/packages/Sqlserver)
- [Documentazione di SQL Server PowerShell](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>Passaggi successivi

- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Note sulla versione](sql-server-ver15-release-notes.md).

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]: white paper tecnico](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />Pubblicato in settembre 2018. Si applica a Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0 per Windows, Linux e i contenitori Docker.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
