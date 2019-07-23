---
title: Novità di SQL Server 2019 | Microsoft Docs
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b5c44145644b2846a2450a4da25a9e06b0f1f43c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984713"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>Novità di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] si basa sulle versioni precedenti per sviluppare SQL Server come piattaforma che offre una scelta di linguaggi di sviluppo, tipi di dati, sistemi operativi ed elaborazione locale o nel cloud. Questo articolo riepiloga le novità di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Questo articolo riepiloga le funzionalità di ogni versione, con i collegamenti ad altre informazioni per ognuna. La sezione [Dettagli](#details) include i dettagli tecnici delle funzionalità che potrebbero non essere disponibili nella documentazione di base. Le altre sezioni di questo articolo offrono informazioni dettagliate su tutte le funzionalità rilasciate per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Per altre informazioni e problemi noti, vedere le [Note sulla versione di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-ver15-release-notes.md).

**Usare gli [strumenti più recenti](#tools) per un'esperienza ottimale con [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].**

## <a name="ctp-31-june-2019"></a>CTP 3.1 giugno 2019

Community Technology Preview (CTP) 3.1 è la versione pubblica più recente di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Questa versione include miglioramenti delle versioni CTP precedenti per la correzione di bug, il miglioramento della sicurezza e l'ottimizzazione delle prestazioni.

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

Per funzionalità specifiche escluse dal supporto, vedere le [note sulla versione](sql-server-ver15-release-notes.md).

In [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.1 sono state anche aggiunte o migliorate le funzionalità seguenti.

### <a name="big-data-clusters"></a>Cluster di Big Data

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Modifiche dei comandi `mssqlctl` | I comandi `mssqlctl cluster` sono stati rinominati `mssqlctl bdc`. Per altre informazioni, vedere le [`mssqlctl`informazioni di riferimento](../big-data-cluster/reference-mssqlctl.md). |
|Nuovi comandi di stato per `mssqlsctl`|Per `mssqlctl` sono stati aggiunti nuovi comandi a integrazione dei comandi di monitoraggio esistenti. Questi sostituiscono il portale di amministrazione cluster, che è stato rimosso in questa versione.|
| Pool di calcolo di Spark | È possibile creare nodi aggiuntivi per incrementare la potenza di calcolo di Spark senza dover aumentare le prestazioni dell'archiviazione. È inoltre possibile avviare i nodi del pool di archiviazione che non vengono usati per Spark. Spark e l'archiviazione sono separati. Per altre informazioni, vedere [Configurare l'archiviazione senza Spark](../big-data-cluster/deployment-custom-configuration.md#sparkstorage). |
| Connettore Spark MSSQL | Supporto per la lettura/scrittura nelle tabelle esterne del pool di dati. Nelle versioni precedenti era supportata solo la lettura/scrittura nelle tabelle dell'istanza MASTER. Per altre informazioni, vedere [Come leggere e scrivere in SQL Server da Spark usando il connettore Spark MSSQL](../big-data-cluster/spark-mssql-connector.md). |
| Machine Learning tramite MLeap | [Eseguire il training di un modello di Machine Learning MLeap in Spark e assegnargli un punteggio in SQL Server tramite l'estensione per il linguaggio Java](../big-data-cluster/spark-create-machine-learning-model.md). |
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motore di database

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Indicizzare le colonne crittografate|Creare indici sulle colonne crittografate usando la crittografia casuale e le chiavi abilitate per l'enclave, per migliorare le prestazioni delle query avanzate (in cui vengono usati `LIKE` e operatori di confronto). Vedere [Always Encrypted con enclave sicuri](../relational-databases/security/encryption/always-encrypted-enclaves.md).
|Impostare i valori `MIN` e `MAX` per la memoria del server al momento dell'installazione |Durante l'installazione è possibile impostare i valori per la memoria del server. Usare i valori predefiniti, i valori consigliati calcolati oppure specificare manualmente i valori personalizzati dopo aver scelto l'opzione **Consigliato** [Opzioni di configurazione del server Server Memory](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually).
|Nuova funzione grafo: `SHORTEST_PATH` | Usare `SHORTEST_PATH` all'interno di `MATCH` per trovare il percorso più breve tra due nodi in un grafo o eseguire attraversamenti di lunghezza arbitraria.|
|Tabelle delle partizioni e indici per i database a grafo|I dati di tabelle e indici partizionati vengono divisi in unità distribuibili tra più filegroup in un database a grafo. |
|Nuova opzione per gli indici: `OPTIMIZE_FOR_SEQUENTIAL_KEY`|Attiva un'ottimizzazione all'interno del motore di database che contribuisce a migliorare la velocità effettiva per gli inserimenti nell'indice con un elevato grado di concorrenza. Questa opzione è destinata agli indici che sono soggetti a conflitti di inserimento dell'ultima pagina, che generalmente si verificano con gli indici con una chiave sequenziale, come una colonna Identity, una sequenza o una colonna di data/ora. Per altre informazioni, vedere [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys).|
| &nbsp; | &nbsp; |

### <a name="sql-server-on-linux"></a>SQL Server in Linux

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
| Miglioramenti di tempdb | Per impostazione predefinita, una nuova installazione di SQL Server in Linux crea più file di dati tempdb in base al numero di core logici (con un massimo di 8 file di dati). Questo non vale per gli aggiornamenti sul posto di una versione principale o secondaria. Ogni file tempdb è di 8 MB, con un aumento automatico di 64 MB. Questo comportamento è simile all'installazione predefinita di SQL Server in Windows. |
| &nbsp; | &nbsp; |

## <a name="ctp-30-may-2019"></a>CTP 3.0 maggio 2019

### <a name="big-data-clusters"></a>Cluster di Big Data

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Aggiornamenti di **mssqlctl** | Numerosi [aggiornamenti di comandi e parametri](../big-data-cluster/reference-mssqlctl.md) **mssqlctl** tra cui un aggiornamento al comando **mssqlctl login**, che ora ha come destinazione il nome utente e l'endpoint del controller. |
| Miglioramenti all'archiviazione | Supporto per configurazioni di archiviazione diverse per log e dati. È stato anche ridotto il numero di attestazioni di volume permanente per un cluster di Big Data. |
| Più istanze del pool di calcolo | Supporto per più istanze del pool di calcolo. |
| Nuove funzionalità e comportamento del pool | Il pool di calcolo viene ora usato per impostazione predefinita per le operazioni del pool di dati e del pool di archiviazione solo nella distribuzione **ROUND_ROBIN**. Il pool di dati ora può usare un nuovo tipo di distribuzione **REPLICATED**, il che significa che gli stessi dati sono presenti in tutte le istanze del pool di dati. |
| Miglioramenti alle tabelle esterne | Le tabelle esterne del tipo origine dati HADOOP ora supportano la lettura di righe con dimensioni fino a 1 MB. Le tabelle esterne (ODBC, pool di archiviazione, pool di dati) ora supportano righe larghe quanto una tabella di SQL Server. |
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motore di database

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Estensioni del linguaggio di SQL Server - [Estensione per il linguaggio Java](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)|[Microsoft Extensibility SDK per Java per Microsoft SQL Server](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) è ora open source e [disponibile su GitHub](https://github.com/microsoft/sql-server-language-extensions).|
|Registrare i linguaggi esterni|La nuova DDL, `CREATE EXTERNAL LANGUAGE`, registra i linguaggi esterni, come ad esempio Java, in SQL Server. Vedere [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md). |
|Altri tipi di dati supportati per Java|Vedere [Java data types](../language-extensions/how-to/java-to-sql-data-types.md) (Tipi di dati Java).|
|Criteri di acquisizione personalizzati per Query Store|Una volta abilitate, le configurazioni aggiuntive di Query Store sono disponibili in una nuova impostazione di criteri di acquisizione di Query Store, per ottimizzare la raccolta dei dati in un server specifico. Per altre informazioni, vedere [Opzioni ALTER DATABASE SET](../t-sql/statements/alter-database-transact-sql-set-options.md).|
|Il [database in memoria](../relational-databases/in-memory-database.md) aggiunge una nuova sintassi DDL per controllare il pool di buffer ibrido. <sup>2</sup>|Il [pool di buffer ibrido](../database-engine/configure-windows/hybrid-buffer-pool.md) consente di accedere direttamente alle pagine di database che si trovano in un dispositivo con memoria persistente, qualora sia necessario.|
|Aggiunta di una nuova funzionalità relativa ai database in memoria, metadati tempdb ottimizzati per la memoria.|Vedere [Metadati tempdb ottimizzati per la memoria](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata)|
|Codifica dei caratteri UTF-8 per supporto server collegati. |[Regole di confronto e supporto Unicode](../relational-databases/collations/collation-and-unicode-support.md) |
|Nome delle regole di confronto BIN2_UTF8 modificato in Latin1_General_100_BIN2_UTF8. |[Regole di confronto e supporto Unicode](../relational-databases/collations/collation-and-unicode-support.md) |
|Il programma di installazione di SQL Server include le raccomandazioni MaxDOP che seguono le linee guida documentate. |[Configurare l'opzione di configurazione del server max degree of parallelism](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)|
|`sys.dm_exec_query_plan_stats` restituisce più informazioni sul grado di parallelismo e concessione di memoria per i piani di query. |[sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)<sup>1</sup>|
| &nbsp; | &nbsp; |

><sup>1</sup> Questa funzionalità richiede il consenso esplicito per abilitarla è necessario il [flag di traccia](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451.
>
><sup>2</sup> Non è più necessario un flag di traccia per abilitare il pool di buffer ibrido.

### [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] supporta i database dell'istanza gestita del database SQL di Azure.| Ospitare [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] in un'istanza gestita. Vedere [[!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]Installazione e configurazione](../master-data-services/master-data-services-installation-and-configuration.md#SetUpWeb).
| &nbsp; | &nbsp; |

### <a name="analysis-services"></a>Analysis Services

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Supporto query MDX per modelli tabulari con i gruppi di calcolo. |In questa versione viene rimosso il limite precedente nei [gruppi di calcolo](#calc-ctp24). |
|Formattazione dinamica delle misure con i gruppi di calcolo. |Questa funzionalità consente di modificare in modo condizionale le stringhe di formato per le misure con i [gruppi di calcolo](#calc-ctp24). Ad esempio, con la conversione di valuta una misura può essere visualizzata usando formati di valuta diversi.|
| &nbsp; | &nbsp; |

## <a name="ctp-25-april-2019"></a>CTP 2.5, aprile 2019

### <a name="big-data-clusters"></a>Cluster di Big Data

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Profili di distribuzione | Per le distribuzioni di cluster di Big Data, usare i [file JSON di configurazione della distribuzione](../big-data-cluster/deployment-guidance.md#configfile), predefiniti o personalizzati, invece delle variabili di ambiente. |
| Distribuzioni richieste | `mssqlctl cluster create` ora richiede di specificare le eventuali impostazioni necessarie per le distribuzioni predefinite. |
| Modifiche dei nomi di endpoint di servizio e pod | Per altre informazioni, vedere le [note sulla versione di cluster di Big Data](../big-data-cluster/release-notes-big-data-cluster.md). |
| Miglioramenti di **mssqlctl** | Usare **mssqlctl** per [elencare gli endpoint esterni](../big-data-cluster/deployment-guidance.md#endpoints) e controllare la versione di **mssqlctl** con il parametro `--version`. |
| Eseguire l'installazione offline | [Istruzioni per le distribuzioni offline di cluster di Big Data](../big-data-cluster/deploy-offline.md). |
| Miglioramenti della suddivisione in livelli HDFS | Suddivisione in livelli HDFS rispetto all'archiviazione Amazon S3. Supporto di OAuth per ADLS Gen2. Funzionalità di memorizzazione nella cache per prestazioni più elevate. Per altre informazioni, vedere [Suddivisione in livelli HSDFS](../big-data-cluster/hdfs-tiering.md) |
| Connettore tra Spark e SQL Server | [Leggere e scrivere in SQL Server da Spark usando il connettore JDBC MSSQL](../big-data-cluster/spark-mssql-connector.md) |
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motore di database

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| PolyBase in Linux. | [Installare PolyBase](../relational-databases/polybase/polybase-linux-setup.md) in Linux per i connettori non Hadoop.<br/><br/>[Mapping dei tipi di PolyBase](../relational-databases/polybase/polybase-type-mapping.md). |
| Nuovo SDK in linguaggio Java per SQL Server. | Semplifica lo sviluppo di applicazioni Java eseguibili da SQL Server. Vedere [Novità - Machine Learning Services di SQL Server](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md). |
| L'ambito dei piani disponibili in DMF `sys.dm_exec_query_plan_stats` è stato ampliato. |Vedere [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)<sup>1</sup>|
| Nuova configurazione con ambito database di `LAST_QUERY_PLAN_STATS` per abilitare `sys.dm_exec_query_plan_stats`. |Vedere [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)|
| Nuovi identificatori SRID (Spatial Reference Identifier). |[Australian GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) offre dati più stabili e accurati, più strettamente allineati ai sistemi di posizionamento globale. I nuovi identificatori SRID sono:<br/><br/> - 7843 - 2D geografico<br/> - 7844 - 3D geografico <br/><br/>La vista [sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) contiene le definizioni dei nuovi identificatori SRID. |
| &nbsp; | &nbsp; |

><sup>1</sup> Questa funzionalità richiede il consenso esplicito e per abilitarla è necessario il [flag di traccia](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451 o l'impostazione su ON della configurazione con ambito database di `LAST_QUERY_PLAN_STATS`.

## <a name="ctp-24-march-2019"></a>CTP 2.4, marzo 2019

### <a name="big-data-clusters"></a>Cluster di Big Data

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Materiale sussidiario sul supporto della GPU per l'esecuzione di Deep Learning con TensorFlow in Spark. | [Distribuire un cluster di Big Data con il supporto della GPU ed eseguire TensorFlow](../big-data-cluster/spark-gpu-tensorflow.md). |
| Le origini dati **SqlDataPool** e **SqlStoragePool** non vengono più create per impostazione predefinita. | Se necessario, crearle manualmente. Vedere i [problemi noti](../big-data-cluster/release-notes-big-data-cluster.md#externaltablesctp24). |
| Supporto di `INSERT INTO SELECT` per il pool di dati. | Per un esempio, vedere [Esercitazione: Ingest data into a SQL Server data pool with Transact-SQL](../big-data-cluster/tutorial-data-pool-ingest-sql.md) (Inserire dati in un pool di dati di SQL Server con Transact-SQL). |
| Opzioni `FORCE SCALEOUTEXECUTION` e `DISABLE SCALEOUTEXECUTION`. | Vedere le [note sulla versione dei cluster di Big Data](../big-data-cluster/release-notes-big-data-cluster.md#whats-new).|
| Aggiornamento delle raccomandazioni sulla distribuzione del servizio Azure Kubernetes. | Quando si valutano i cluster di Big Data nel servizio Azure Kubernetes, è ora consigliabile usare un singolo nodo di dimensioni **Standard_L8s**. |
| Aggiornamento del runtime Spark a Spark 2.4. | |
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motore di database

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Il messaggio di errore di troncamento include per impostazione predefinita i nomi di tabelle e colonne e il valore troncato.|[VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation)|
|La nuova funzione a gestione dinamica `sys.dm_exec_query_plan_stats` restituisce l'equivalente dell'ultimo piano di esecuzione effettivo noto per la maggior parte delle query. |[sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)<sup>1</sup>|
|Il nuovo evento esteso `query_post_execution_plan_profile` raccoglie l'equivalente di un piano di esecuzione effettivo in base alla profilatura leggera, a differenza di `query_post_execution_showplan` che usa la profilatura standard. |[Infrastruttura di profilatura query](../relational-databases/performance/query-profiling-infrastructure.md)|
|Analisi Transparent Data Encryption (TDE) con possibilità di sospensione e ripresa.|[Analisi Transparent Data Encryption (TDE) con possibilità di sospensione e ripresa](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)|
| &nbsp; | &nbsp; |

><sup>1</sup> Questa funzionalità richiede il consenso esplicito per abilitarla è necessario il [flag di traccia](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451.

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Relazioni molti-a-molti nei modelli tabulari.|[Relazioni molti-a-molti nei modelli tabulari](#many-to-many-ctp24)|
|Impostazioni delle proprietà per la governance delle risorse.|[Impostazioni delle proprietà per la governance delle risorse](#property-ctp24)|
| &nbsp; | &nbsp; |

## <a name="ctp-23-february-2019"></a>CTP 2.3, febbraio 2019

### <a name="big-data-clusters"></a>Cluster di Big Data

| Nuova funzionalità o aggiornamento | Dettagli |
| :---------- | :------ |
| Inviare processi Spark nei cluster di Big Data in IntelliJ. | [Inviare processi Spark nei cluster di Big Data di SQL Server in IntelliJ](../big-data-cluster/spark-submit-job-intellij-tool-plugin.md) |
| Interfaccia della riga di comando comune per la distribuzione di applicazioni e la gestione di cluster. | [Come distribuire un'app in un cluster di Big Data di SQL Server 2019 (anteprima)](../big-data-cluster/big-data-cluster-create-apps.md) |
| Estensione di VS Code per distribuire applicazioni in un cluster di Big Data. | [Come usare VS Code per distribuire applicazioni nei cluster di Big Data di SQL Server](../big-data-cluster/app-deployment-extension.md) |
| Modifiche apportate all'utilizzo dei comandi dello strumento **mssqlctl**. | Per informazioni più dettagliate, vedere i [problemi noti di mssqlctl](../big-data-cluster/release-notes-big-data-cluster.md#mssqlctlctp23). |
| Usare Sparklyr in cluster di Big Data. | [Usare Sparklyr in cluster di Big Data di SQL Server 2019](../big-data-cluster/sparklyr-from-RStudio.md) |
| Montare un'archiviazione esterna compatibile con Hadoop Distributed File System (HDFS) in un cluster Big Data con la **suddivisione in livelli HDFS**. | Vedere [Suddivisione in livelli HDFS](../big-data-cluster/hdfs-tiering.md). |
| Nuova esperienza di connessione unificata per l'istanza master di SQL Server e il gateway HDFS/Spark. | Vedere [Istanza master di SQL Server e gateway HDFS/Spark](../big-data-cluster/connect-to-big-data-cluster.md). |
| L'eliminazione di un cluster con **mssqlctl cluster delete** rimuove ora solo gli oggetti dello spazio dei nomi che fanno parte del cluster di Big Data. | Lo spazio dei nomi non viene eliminato. Nelle versioni precedenti, invece, questo comando elimina l'intero spazio dei nomi. |
| I nomi degli endpoint di _sicurezza_ sono stati cambiati e consolidati. | **service-security-lb** e **service-security-nodeport** sono stati consolidati nell'endpoint **endpoint-security**. |
| I nomi degli endpoint _proxy_ sono stati cambiati e consolidati. | **service-proxy-lb** e **service-proxy-nodeport** sono stati consolidati nell'endpoint **endpoint-service-proxy**. |
| I nomi degli endpoint di _controller_ sono stati cambiati e consolidati. | **service-mssql-controller-lb** e **service-mssql-controller-nodeport** sono stati consolidati nell'endpoint **endpoint-controller**. |
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motore di database

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Il recupero del database accelerato può essere abilitato per ogni singolo database.| [Recupero del database accelerato](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr)|
|Supporto dell'uso forzato del piano di Query Store per cursori statici e fast forward.|[Supporto dell'uso forzato del piano per cursori statici e fast forward](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23) |
|Riduzione delle ricompilazioni per carichi di lavoro che usano tabelle temporanee in più ambiti. |[Riduzione delle ricompilazioni per i carichi di lavoro](../relational-databases/tables/tables.md#ctp23) |
|Scalabilità migliorata per il checkpoint indiretto. |[Scalabilità migliorata per il checkpoint indiretto](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23)|
|Aggiunta del supporto per l'uso della codifica dei caratteri UTF-8 con le regole di confronto BIN2 (`UTF8_BIN2`). |[Regole di confronto e supporto Unicode](../relational-databases/collations/collation-and-unicode-support.md) |
|Definire azioni di eliminazione propagate su un vincolo ad arco in a database a grafo. |[Vincoli di arco](../relational-databases/tables/graph-edge-constraints.md) |
|Abilitare o disabilitare `LIGHTWEIGHT_QUERY_PROFILING` con la nuova configurazione con ambito database. |[`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp) |
| &nbsp; | &nbsp; |

### <a name="tools"></a>Strumenti

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Azure Data Studio supporta Azure Active Directory. |[Azure Data Studio](../azure-data-studio/what-is.md) |
|L'interfaccia utente di visualizzazione di Notebooks è stata spostata nella memoria centrale di Azure Data Studio. |[Come gestire i notebook in Azure Data Studio](../big-data-cluster/notebooks-how-to-manage.md) |
|Aggiunta una nuova procedura guidata per creare origini dati esterne da Hadoop Distributed File System (HDFS) a cluster Big Data di SQL Server. | [Strumenti](#tools-ctp23)|
|Interfaccia utente di visualizzazione di Notebooks. | [Strumenti](#tools-ctp23) |
|Aggiunte nuove API Notebooks.| [Strumenti](#tools-ctp23) |
|Aggiunto il comando "Reinstall Notebook dependencies" (Reinstalla dipendenze Notebooks) per assistenza durante gli aggiornamenti dei pacchetti Python. | [Strumenti](#tools-ctp23) |
|Avvio di Azure Data Studio da SSMS.| [Strumenti](#tools-ctp23) |
| &nbsp; | &nbsp; |

### <a name="analysis-services"></a>Analysis Services

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Gruppi di calcolo in modelli tabulari.| [Gruppi di calcolo in modelli tabulari](#calc-ctp24) |
| &nbsp; | &nbsp; |

## <a name="ctp-22-december-2018"></a>CTP 2.2, dicembre 2018

### <a name="big-data-clusters"></a>Cluster di Big Data

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Usare SparkR da Azure Data Studio in un cluster Big Data. | |
|Distribuire app Python e R.|[Distribuire applicazioni con mssqlctl](../big-data-cluster/big-data-cluster-create-apps.md) |
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motore di database

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Aggiunta del supporto per l'uso della codifica dei caratteri UTF-8 con la replica di SQL Server. |[Regole di confronto e supporto Unicode](../relational-databases/collations/collation-and-unicode-support.md#ctp23) |
| &nbsp; | &nbsp; |


### <a name="sql-server-on-linux"></a>SQL Server in Linux

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Gruppo di disponibilità AlwaysOn in contenitori Docker con Kubernetes. |[Gruppi di disponibilità Always On per i contenitori](../linux/sql-server-ag-kubernetes.md) |
| &nbsp; | &nbsp; |

## <a name="ctp-21-november-2018"></a>CTP 2.1, novembre 2018

### <a name="database-engine"></a>Motore di database

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Aggiunta del supporto per la selezione delle regole di confronto UTF-8 come impostazione predefinita durante l'installazione di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. |[Regole di confronto e supporto Unicode](../relational-databases/collations/collation-and-unicode-support.md#ctp23) |
|L'inlining di funzioni definite dall'utente scalari trasforma automaticamente tali funzioni in espressioni relazionali e le incorpora nella query SQL chiamante. |[Inlining di funzioni definite dall'utente scalari](../relational-databases/user-defined-functions/scalar-udf-inlining.md) |
|La colonna `command` della vista a gestione dinamica `sys.dm_exec_requests` mostra `SELECT (STATMAN)` se un'operazione `SELECT` è in attesa del completamento di un'operazione di aggiornamento delle statistiche sincrona prima di continuare l'esecuzione di query. | [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) |
|Il nuovo tipo di attesa `WAIT_ON_SYNC_STATISTICS_REFRESH` viene esposto nella vista a gestione dinamica `sys.dm_os_wait_stats`. Mostra il tempo accumulato a livello di istanza dedicato alle operazioni di aggiornamento delle statistiche sincrone.|[`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) |
|Il pool di buffer ibrido è una nuova funzionalità del motore di database di SQL Server con la quale le pagine del database che si trovano in file di database posizionati in un dispositivo di memoria persistente (PMEM) saranno accessibili direttamente quando necessario.|[Pool di buffer ibrido](../database-engine/configure-windows/hybrid-buffer-pool.md) |
|Usare alias di tabelle o viste derivate nelle query corrispondenti ai grafi |[Vincoli di arco dei grafi](../relational-databases/tables/graph-edge-constraints.md) |
| &nbsp; | &nbsp; |

### <a name="sql-server-on-linux"></a>SQL Server in Linux

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Nuovo registro contenitori per SQL Server. |[Introduzione ai contenitori di SQL Server in Docker](../linux/quickstart-install-connect-docker.md) |
| &nbsp; | &nbsp; |

### <a name="tools"></a>Strumenti

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|[Azure Data Studio](../azure-data-studio/what-is.md) supporta la connessione e la gestione di cluster di Big Data di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. | |
| &nbsp; | &nbsp; |

## <a name="ctp-20-october-2018"></a>CTP 2.0, ottobre 2018

### <a name="big-data-clusters"></a>Cluster di Big Data

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Distribuire un cluster Big Data con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e contenitori Spark Linux in Kubernetes. | |
|Accedere ai Big Data da Hadoop Distributed File System (HDFS). | |
|Eseguire analisi avanzata e Machine Learning con Spark. | |
|Usare lo streaming Spark per i dati dei pool di dati SQL. | |
|Eseguire volumi Query che offrono un'esperienza di tipo notebook in **Azure Data Studio**.|[Ingegneria dei dati](../azure-data-studio/what-is.md#data-engineering)|
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motore di database

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|È stata aggiunto il livello **COMPATIBILITY_LEVEL 150** del database. |[Livello di compatibilità ALTER DATABASE (Transact-SQL)](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) |
|Creazione di indici online ripristinabili.|[CREATE INDEX (Transact-SQL)](../t-sql/statements/create-index-transact-sql.md#resumable-indexes) |
|Feedback delle concessioni di memoria in modalità riga. |[Feedback delle concessioni di memoria in modalità riga](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback) |
|Approssimazione di `COUNT DISTINCT`.|[Elaborazione delle query approssimativa](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing)|
|Modalità batch per rowstore.|[Modalità batch per rowstore](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore) |
|Compilazione posticipata delle variabili di tabella.|[Compilazione posticipata delle variabili di tabella](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation) |
|Estensione per il linguaggio Java.|[Estensione per il linguaggio Java](../advanced-analytics/java/extension-java.md) |
|È possibile unire i dati grafo correnti da tabelle nodi o tabelle archi a nuovi dati usando i predicati `MATCH` nell'istruzione `MERGE`. | |
|Vincoli di arco.|[Vincoli di arco dei grafi](../relational-databases/tables/graph-edge-constraints.md) |
|Impostazione predefinita con ambito database per operazioni DDL online e ripristinabili.| |
|I gruppi di disponibilità supportano fino a 5 repliche secondarie sincrone.|[Gruppi di disponibilità](../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) |
|Reindirizzamento della connessione in lettura/scrittura da replica da secondaria a primaria|[Reindirizzamento della connessione in lettura/scrittura da replica secondaria a primaria - Gruppi di disponibilità AlwaysOn](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md) |
|Individuazione e classificazione dei dati SQL.| [Individuazione e classificazione dei dati SQL](../relational-databases/security/sql-data-discovery-and-classification.md) |
|Supporto esteso per i dispositivi con memoria persistente.|[Pool di buffer ibrido](../database-engine/configure-windows/hybrid-buffer-pool.md) |
|Supporto delle statistiche columnstore in `DBCC CLONEDATABASE`|[BLOB di statistiche per gli indici columnstore](../t-sql/database-console-commands/dbcc-clonedatabase-transact-sql.md#ctp23)|
|In `sp_estimate_data_compression_savings` sono stati introdotti `COLUMNSTORE` e `COLUMNSTORE_ARCHIVE`.|[Considerazioni sugli indici columnstore](../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md#considerations-for-columnstore-indexes)|
|Servizi di Machine Learning supportati nel cluster di failover di Windows Server. |[Novità - Machine Learning Services di SQL Server](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)|
|Supporto di Machine Learning per la modellazione basata su partizioni.|[Novità - Machine Learning Services di SQL Server](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md) |
|Infrastruttura leggera di profilatura query abilitata per impostazione predefinita |[Infrastruttura di profilatura delle statistiche di esecuzione query lightweight v3](../relational-databases/performance/query-profiling-infrastructure.md#lightweight-query-execution-statistics-profiling-infrastructure-v3) |
|Nuovi connettori PolyBase per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata e MongoDB. |[Che cos'è PolyBase?](../relational-databases/polybase/polybase-guide.md) |
|`sys.dm_db_page_info(database_id, file_id, page_id, mode)` restituisce informazioni su una pagina di un database. |[sys.dm_db_page_info (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)|
|Always Encrypted con enclave sicuri. |[Always Encrypted con enclave sicuri](../relational-databases/security/encryption/always-encrypted-enclaves.md) |
|Compilare e ricompilare gli indici columnstore cluster online. |[Eseguire operazioni online sugli indici](../relational-databases/indexes/perform-index-operations-online.md) |
| &nbsp; | &nbsp; |

### <a name="sql-server-on-linux"></a>SQL Server in Linux

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Supporto della replica |[Replica di SQL Server in Linux](../linux/sql-server-linux-replication.md)
|Supporto di Microsoft Distributed Transaction Coordinator (MSDTC) |[Come configurare MSDTC in Linux](../linux/sql-server-linux-configure-msdtc.md) |
|Supporto OpenLDAP per provider AD di terze parti |[Esercitazione: Usare l'autenticazione di Azure Active Directory con SQL Server in Linux](../linux/sql-server-linux-active-directory-authentication.md) |
|Machine Learning in Linux |[Configurare Machine Learning in Linux](../linux/sql-server-linux-setup-machine-learning.md) |
| &nbsp; | &nbsp; |

### <a name="master-data-services"></a>Master Data Services

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|il portale Master Data Services (MDS) non è più dipendente da Silverlight.| Tutti i componenti Silverlight precedenti sono stati sostituiti con controlli HTML.|
| &nbsp; | &nbsp; |

### <a name="security"></a>Security

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Gestione dei certificati in Gestione configurazione SQL Server|[Gestione dei certificati (Gestione configurazione SQL Server)](../database-engine/configure-windows/manage-certificates.md)
| &nbsp; | &nbsp; |

### <a name="tools"></a>Strumenti

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|[Azure Data Studio](../azure-data-studio/what-is.md) supporta la connessione e la gestione di cluster di Big Data di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. |[Informazioni su Azure Data Studio](../azure-data-studio/what-is.md)|
|Supporto di scenari che usano il cluster di Big Data di SQL Server. |[Estensione di SQL Server 2019 (anteprima)](../azure-data-studio/sql-server-2019-extension.md)|
|[**SQL Server Management Studio (SSMS) 18.0 (anteprima)** ](../ssms/sql-server-management-studio-ssms.md): Supporta [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].| |
|Supporto di Always Encrypted con enclave sicuri. |[Always Encrypted con enclave sicuri](../relational-databases/security/encryption/always-encrypted-enclaves.md)|
| &nbsp; | &nbsp; |


## <a name="other-services"></a>Altri servizi

In CTP 2.4 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] non introduce nuove funzionalità per i servizi seguenti:

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS)

## <a name="details"></a>Dettagli

### <a id="bigdatacluster"></a>Cluster Big Data

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] I [cluster Big Data](../big-data-cluster/big-data-cluster-overview.md) rendono disponibili nuovi scenari come i seguenti:

- [Supporto della GPU per l'esecuzione di Deep Learning con TensorFlow in Spark](../big-data-cluster/spark-gpu-tensorflow.md). (CTP 2.4)
- Aggiornamento del runtime Spark a Spark 2.4. (CTP 2.4)
- Supporto di `INSERT INTO SELECT` per il pool di dati (CTP 2.4)
- Clausola dell'opzione `FORCE SCALEOUTEXECUTION` e `DISABLE SCALEOUTEXECUTION` per le query di tabella esterna. (CTP 2.4)
- [Inviare processi Spark nei cluster Big Data di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] in IntelliJ](../big-data-cluster/spark-submit-job-intellij-tool-plugin.md). (CTP 2.3)
- [Esperienza di distribuzione e gestione di applicazioni](../big-data-cluster/big-data-cluster-create-apps.md) per diverse app con dati correlati, inclusa l'operatività di modelli di Machine Learning che usano R e Python, l'esecuzione di processi SQL Server Integration Services (SSIS) e così via. (CTP 2.3)
- [Usare Sparklyr in cluster Big Data di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](../big-data-cluster/sparklyr-from-RStudio.md). (CTP 2.3)
- Montare un'archiviazione esterna compatibile con Hadoop Distributed File System (HDFS) in un cluster Big Data con la [suddivisione in livelli HDFS](../big-data-cluster/hdfs-tiering.md). (CTP 2.3)
- Usare SparkR da Azure Data Studio in un cluster Big Data. (CTP 2.2)
- [Distribuire app Python e R](../big-data-cluster/big-data-cluster-create-apps.md). (CTP 2.2)
- Distribuire un cluster Big Data con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e contenitori Spark Linux in Kubernetes. (CTP 2.0)
- Accedere ai Big Data da Hadoop Distributed File System (HDFS). (CTP 2.0)
- Eseguire analisi avanzata e Machine Learning con Spark. (CTP 2.0)
- Usare lo streaming Spark per i dati dei pool di dati SQL. (CTP 2.0)
- Eseguire volumi Query che offrono un'esperienza di tipo notebook in [**Azure Data Studio**](../sql-operations-studio/what-is.md). (CTP 2.0)
 
[!INCLUDE [Big data clusters preview](../includes/big-data-cluster-preview-note.md)]

### Motore di database <a id="databaseengine"></a>

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduce o migliora le nuove funzionalità seguenti per [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)].

#### <a name="new-querypostexecutionplanprofile-extended-event-ctp-24"></a>Nuovo evento esteso query_post_execution_plan_profile (CTP 2.4)

Il nuovo evento esteso `query_post_execution_plan_profile` raccoglie l'equivalente di un piano di esecuzione effettivo in base alla profilatura leggera, a differenza di `query_post_execution_showplan` che usa la profilatura standard. Per altre informazioni, vedere [Infrastruttura di profilatura delle query](../relational-databases/performance/query-profiling-infrastructure.md).

##### <a name="example-1---extended-event-session-using-standard-profiling"></a>Esempio 1 - Sessione Evento esteso con profilatura standard

```sql
CREATE EVENT SESSION [QueryPlanOld] ON SERVER 
ADD EVENT sqlserver.query_post_execution_showplan(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename = N'C:\Temp\QueryPlanStd.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

##### <a name="example-2---extended-event-session-using-lightweight-profiling"></a>Esempio 2 - Sessione Evento esteso con profilatura leggera

```sql
CREATE EVENT SESSION [QueryPlanLWP] ON SERVER 
ADD EVENT sqlserver.query_post_execution_plan_profile(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename=N'C:\Temp\QueryPlanLWP.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

#### <a name="new-dmf-sysdmexecqueryplanstats-ctp-24"></a>Nuova funzione a gestione dinamica sys.dm_exec_query_plan_stats (CTP 2.4) 

La nuova funzione a gestione dinamica `sys.dm_exec_query_plan_stats` restituisce l'equivalente dell'ultimo piano di esecuzione effettivo noto per la maggior parte delle query, in base alla profilatura leggera. Per altre informazioni, vedere [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md) e [Infrastruttura di profilatura delle query](../relational-databases/performance/query-profiling-infrastructure.md). Vedere come esempio lo script seguente:

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

Questa funzione prevede il consenso esplicito e richiede l'abilitazione del [flag di traccia](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451.

#### <a name="transparent-data-encryption-tde-scan---suspend-and-resume-ctp-24"></a>Analisi Transparent Data Encryption (TDE) con possibilità di sospensione e ripresa (CTP 2.4)

Per abilitare [Transparent Data Encryption (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md) in un database, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] deve eseguire un'analisi della crittografia che legge ogni pagina dei file di dati nel pool di buffer e quindi riscrive le pagine crittografate su disco. Per offrire all'utente maggior controllo sull'analisi della crittografia, [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] include la sintassi per sospendere l'analisi TDE quando il carico di lavoro nel sistema è pesante o durante gli orari strategici per l'azienda e di riprenderla in un momento successivo.

Per sospendere l'analisi della crittografia TDE, usare la sintassi seguente:

```sql
ALTER DATABASE <db_name> SET ENCRYPTION SUSPEND;
```

Per riprendere l'analisi della crittografia TDE, usare la sintassi seguente:

```sql
ALTER DATABASE <db_name> SET ENCRYPTION RESUME;
```

Per visualizzare lo stato corrente dell'analisi della crittografia, `encryption_scan_state` è stato aggiunta alla DMV `sys.dm_database_encryption_keys`. È anche disponibile una nuova colonna denominata `encryption_scan_modify_date` che conterrà la data e l'ora dell'ultima modifica dello stato dell'analisi della crittografia. Si noti anche che se l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] viene riavviata mentre l'analisi della crittografia è sospesa, verrà registrato un messaggio nel log degli errori all'avvio che indica la presenza di un'analisi esistente sospesa.

#### <a name="accelerated-database-recovery-ctp-23"></a>Recupero del database accelerato (CTP 2.3)

Il [recupero del database accelerato](/azure/sql-database/sql-database-accelerated-database-recovery/) migliora considerevolmente la disponibilità del database, in particolare in presenza di transazioni a esecuzione prolungata, riprogettando il processo di recupero del motore di database di SQL Server. Il [recupero del database](../relational-databases/logs/the-transaction-log-sql-server.md?#recovery-of-all-incomplete-transactions-when--is-started) è il processo che SQL Server usa per avviare ogni database in uno stato coerente a livello di transazioni o in uno stato normale. Un database in cui è abilitato il recupero del database accelerato completa l'operazione di recupero in modo considerevolmente più veloce dopo un failover o una chiusura non normale. In CTP 2.3 il recupero del database accelerato può essere abilitato per ogni database usando la sintassi seguente:

```sql
ALTER DATABASE <db_name> SET ACCELERATED_DATABASE_RECOVERY = {ON | OFF}
```

> [!NOTE]
> Questa sintassi non è necessaria per sfruttare i vantaggi di questa funzionalità nel database SQL di Azure in cui la funzionalità viene [abilitata su richiesta durante l'anteprima pubblica](/azure/sql-database/sql-database-accelerated-database-recovery). Dopo l'abilitazione, la funzionalità è attiva per impostazione predefinita.

In caso di database critici con possibili transazioni di grandi dimensioni, provare a usare questa funzionalità durante l'anteprima. Inviare commenti al [team di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](<https://aka.ms/sqlfeedback>).

#### <a name="query-store-plan-forcing-support-for-fast-forward-and-static-cursors-ctp-23"></a>Uso forzato del piano di Query Store per cursori statici e fast forward (CTP 2.3)

Query Store ora supporta la possibilità di forzare i piani di esecuzione query per i cursori T-SQL e API statici e fast forward. L'uso forzato è ora supportato tramite `sp_query_store_force_plan` o tramite i report di Query Store in SQL Server Management Studio.

#### <a name="reduced-recompilations-for-workloads-using-temporary-tables-across-multiple-scopes-ctp-23"></a>Riduzione delle ricompilazioni per carichi di lavoro che usano tabelle temporanee in più ambiti (CTP 2.3)

Prima di questa funzionalità, quando si faceva riferimento a una tabella temporanea con un'istruzione DML (`SELECT`, `INSERT`, `UPDATE`, `DELETE`), se la tabella temporanea era stata creata da un batch di ambito esterno, l'istruzione DML veniva ricompilata ogni volta che veniva eseguita. Grazie a questo miglioramento, SQL Server esegue semplici controlli aggiuntivi per evitare ricompilazioni non necessarie:

- Controlla se il modulo di ambito esterno usato per creare la tabella temporanea in fase di compilazione è uguale a quello usato per le esecuzioni consecutive. 
- Tiene traccia di eventuali modifiche di Data Definition Language (DDL) apportate alla compilazione iniziale e le confronta con le operazioni DDL per le esecuzioni consecutive. 

Il risultato finale è la riduzione di ricompilazioni estranee e di overhead della CPU.

#### <a name="improved-indirect-checkpoint-scalability-ctp-23"></a>Scalabilità migliorata per il checkpoint indiretto (CTP 2.3)

Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gli utenti possono riscontrare errori con l'utilità di pianificazione che non cede il controllo quando il database genera un numero elevato di pagine dirty, ad esempio tempdb. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduce una scalabilità migliorata per il checkpoint indiretto che consente di evitare questi errori nei database che hanno un carico di lavoro di UPDATE/INSERT eccessivo.

#### <a name="utf-8-support-ctp-23"></a>Supporto UTF-8 (CTP 2.3)

Supporto completo per la codifica dei caratteri di grande diffusione UTF-8 come codifica di importazione o esportazione o come regola di confronto di livello database o colonna per i dati di testo. La codifica UTF-8 è consentita nei tipi di dati `CHAR` e `VARCHAR` ed è abilitata quando si crea o si modifica la regola di confronto di un oggetto convertendola in una regola di confronto con il suffisso `UTF8`. 

Ad esempio da `LATIN1_GENERAL_100_CI_AS_SC` a `LATIN1_GENERAL_100_CI_AS_SC_UTF8`. UTF-8 è disponibile solo per le regole di confronto di Windows che supportano i caratteri supplementari. Questa funzionalità è stata introdotta in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. `NCHAR` e `NVARCHAR` consentono solo la codifica UTF-16 e rimangono invariati.

A seconda del set di caratteri in uso, questa funzionalità può offrire importanti risparmi di risorse di archiviazione. Se ad esempio si cambia il tipo di dati di una colonna esistente con stringhe ASCII (Latin) da `NCHAR(10)` in `CHAR(10)` usando una regola di confronto con supporto UTF-8, i requisiti di archiviazione vengono ridotti del 50%. Questa riduzione deriva dal fatto che `NCHAR(10)` richiede 20 byte per l'archiviazione, mentre `CHAR(10)` richiede solo 10 byte per la stessa stringa Unicode.

Per altre informazioni, vedere [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).

**CTP 2.1** Aggiunge il supporto per la selezione delle regole di confronto UTF-8 come impostazione predefinita durante l'installazione di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

**CTP 2.2** Aggiunge il supporto per l'uso della codifica dei caratteri UTF-8 con la replica di SQL Server.

**CTP 2.3** Aggiunge il supporto per l'uso della codifica dei caratteri UTF-8 con le regole di confronto BIN2 (UTF8_BIN2).

#### <a name="scalar-udf-inlining-ctp-21"></a>Inlining di funzioni definite dall'utente scalari (CTP 2.1)

L'inlining di funzioni definite dall'utente scalari trasforma automaticamente le funzioni definite dall'utente (UDF) scalari in espressioni relazionali e le incorpora nella query SQL chiamante, migliorando così le prestazioni dei carichi di lavoro che usano funzioni definite dall'utente scalari. L'inlining di funzioni definite dall'utente scalari facilita l'ottimizzazione basata sui costi delle operazioni all'interno di funzioni definite dall'utente e genera piani efficienti orientati ai set e paralleli, invece di piani di esecuzione seriali, inefficienti e iterativi. Questa funzionalità è abilitata per impostazione predefinita nel livello di compatibilità del database 150.

Per altre informazioni, vedere [Inlining di funzioni definite dall'utente scalari](../relational-databases/user-defined-functions/scalar-udf-inlining.md).

#### <a name="a-nametruncation-truncation-error-message-improved-to-include-table-and-column-names-and-truncated-value-ctp-21"></a><a name="truncation" />Messaggio di errore di troncamento migliorato in modo da includere i nomi di tabelle e colonne e il valore troncato (CTP 2.1)

Il messaggio di errore con ID 8152 `String or binary data would be truncated` è familiare a molti sviluppatori e amministratori di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che sviluppano e gestiscono carichi di lavoro di spostamento dei dati. Questo errore viene generato durante il trasferimento di dati tra un'origine e una destinazione con schemi diversi quando l'origine dati è troppo grande per adattarsi al tipo di dati di destinazione. Questo messaggio di errore può richiedere molto tempo per la risoluzione. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduce un nuovo messaggio di errore più specifico (2628) per questo scenario:  

`String or binary data would be truncated in table '%.*ls', column '%.*ls'. Truncated value: '%.*ls'.`

Il nuovo messaggio di errore 2628 fornisce altre informazioni di contesto per il problema di troncamento dei dati, semplificando il processo di risoluzione dei problemi. 

**CTP 2.1 e CTP 2.2** Si tratta di un messaggio di errore che prevede il consenso esplicito e richiede l'abilitazione del [flag di traccia](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460.

**CTP 2.4** Il messaggio di errore 2628 diventa il messaggio di troncamento predefinito e sostituisce il messaggio di errore 8152 nel livello di compatibilità del database 150. È stata introdotta una nuova configurazione con ambito database `VERBOSE_TRUNCATION_WARNINGS` per passare dal messaggio di errore 2628 al messaggio di errore 8152 e viceversa quando il livello di compatibilità del database è 150. Per altre informazioni, vedere [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).
Per il livello di compatibilità del database 140 o inferiore, il 2628 rimane un messaggio di errore che prevede il consenso esplicito e richiede l'abilitazione del [flag di traccia](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460.

#### <a name="improved-diagnostic-data-for-stats-blocking-ctp-21"></a>Dati di diagnostica migliorati per il blocco delle statistiche (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] offre dati di diagnostica migliorati per le query con esecuzione prolungata in attesa di operazioni di aggiornamento delle statistiche sincrone. La colonna `command` della vista a gestione dinamica `sys.dm_exec_requests` mostra `SELECT (STATMAN)` se un'operazione `SELECT` è in attesa del completamento di un'operazione di aggiornamento delle statistiche sincrona prima di continuare l'esecuzione di query. Inoltre, viene esposto il nuovo tipo di attesa `WAIT_ON_SYNC_STATISTICS_REFRESH` nella vista a gestione dinamica `sys.dm_os_wait_stats`. Mostra il tempo accumulato a livello di istanza dedicato alle operazioni di aggiornamento delle statistiche sincrone.

#### <a name="hybrid-buffer-pool-ctp-21"></a>Pool di buffer ibrido (CTP 2.1)

Il pool di buffer ibrido è una nuova funzionalità del motore di database di SQL Server con la quale le pagine del database che si trovano in file di database posizionati in un dispositivo di memoria persistente (PMEM) saranno accessibili direttamente quando necessario. Dato che i dispositivi PMEM offrono una latenza molto bassa per l'accesso ai dati, il motore può evitare di creare una copia dei dati in un'area di "pagine pulite" del pool di buffer e semplicemente accedere alla pagina direttamente nel dispositivo PMEM. L'accesso viene eseguito tramite I/O mappato alla memoria, come appropriato per il riconoscimento. Ciò offre vantaggi a livello di prestazioni grazie alla possibilità di evitare la creazione di una copia della pagina nella DRAM e di evitare che lo stack di I/O del sistema operativo acceda alla pagina in uno spazio di archiviazione permanente. Questa funzionalità è disponibile sia in SQL Server in Windows che in SQL Server in Linux.

Per altre informazioni, vedere [Pool di buffer ibrido](../database-engine/configure-windows/hybrid-buffer-pool.md)

#### <a name="static-data-masking-ctp-21"></a>Mascheramento dei dati statico (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduce il mascheramento dei dati statico. È possibile usare il mascheramento dei dati statico per purificare i dati sensibili in copie di database di SQL Server. Il mascheramento dei dati statico consente di creare una copia purificata dei database in cui tutte le informazioni sensibili vengono modificate in modo che la copia diventi condivisibile con gli utenti non di produzione. Il mascheramento dei dati statico può essere usato per scopi di sviluppo, test, analisi e creazione di report aziendali, conformità, risoluzione dei problemi e in qualsiasi altro scenario in cui i dati specifici non possono essere copiati in ambienti diversi.

Il mascheramento dei dati statico opera a livello di colonna. Selezionare le colonne da mascherare e per ogni colonna selezionata, specificare una funzione di mascheramento. Il mascheramento dei dati statico copia il database e quindi applica le funzioni di mascheramento specificate nelle colonne.

##### <a name="static-data-masking-vs-dynamic-data-masking"></a>Mascheramento dei dati statico e mascheramento dei dati dinamico

Il mascheramento dei dati è il processo di applicazione di una maschera a un database per nascondere le informazioni sensibili del database e sostituirle con nuovi dati o dati ripuliti. Microsoft offre due opzioni di mascheramento, ovvero il mascheramento dei dati statico e il mascheramento dei dati dinamico. Il mascheramento dei dati dinamico è stato introdotto in [!INCLUDE[ssSQL16](../includes/sssql16-md.md)]. Nella tabella seguente vengono messe a confronto questi due soluzioni:

|Mascheramento dei dati statico |Mascheramento dati dinamici|
|:----|:----|
|Applicato a una copia del database <br/><br/>I dati originali non sono recuperabili<br/><br/>Il mascheramento avviene a livello di archiviazione<br/><br/>Tutti gli utenti hanno accesso agli stessi dati mascherati<br/><br/>Pensato per l'accesso continuo a livello di team|Applicato al database originale<br/><br/>I dati originali rimangono intatti<br/><br/>Il mascheramento avviene in tempo reale in fase di query<br/><br/>Il mascheramento varia in base alle autorizzazioni dell'utente <br/><br/>Pensato per l'accesso puntuale da parte di utenti specifici|

#### <a name="database-compatibility-level-ctp-20"></a>Livello di compatibilità del database (CTP 2.0)

È stata aggiunto il livello **COMPATIBILITY_LEVEL 150** del database. Per attivarlo per un database utente specifico, eseguire:

   ```sql
   ALTER DATABASE database_name SET COMPATIBILITY_LEVEL =  150;
   ```

#### <a name="resumable-online-index-create-ctp-20"></a>Creazione di indici online ripristinabili (CTP 2.0)

Con la **creazione di indici online ripristinabili** un'operazione di creazione indice può essere sospesa e ripresa in seguito dal punto in cui è stata interrotta, anziché riavviarla dall'inizio.

La creazione di indici online ripristinabili supporta gli scenari seguenti:
- Ripristino di un'operazione di creazione indice dopo un errore di creazione indice, ad esempio in seguito a un failover del database o all'esaurimento dello spazio su disco.
- Sospensione temporanea di un'operazione di creazione indice e ripresa in un secondo momento, per consentire di liberare temporaneamente risorse di sistema in base alle esigenze e quindi riprendere l'esecuzione.
- Creazione di indici di grandi dimensioni senza usare grandi quantità spazio di registro, senza un'esecuzione prolungata che blocca altre attività di manutenzione e con la possibilità di troncare il log.

In caso di un errore di creazione indice, senza questa funzionalità la creazione indice online va eseguita di nuovo e l'operazione deve essere riavviata dall'inizio.

In questa versione, la funzionalità ripristinabile viene estesa con l'aggiunta di questa funzionalità alla [ricompilazione dell'indice online ripristinabile](http://azure.microsoft.com/blog/modernize-index-maintenance-with-resumable-online-index-rebuild/), già disponibile.

È anche possibile impostare questa funzionalità come valore predefinito per un database specifico usando l'[impostazione predefinita con ambito database per le operazioni DDL online e ripristinabili](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

Per altre informazioni, vedere [Creazione di indici online ripristinabili](../t-sql/statements/create-index-transact-sql.md#resumable-indexes).

#### <a name="build-and-rebuild-clustered-columnstore-indexes-online-ctp-20"></a>Compilare e ricompilare gli indici columnstore cluster online (CTP 2.0)

È possibile convertire le tabelle rowstore al formato columnstore. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] la creazione di indici columnstore cluster (CCI) era un processo offline la cui esecuzione richiedeva la sospensione di tutte le modifiche. Con [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] e [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] è possibile creare o ricreare indici columnstore cluster online. Il carico di lavoro non viene bloccato e tutte le modifiche apportate ai dati sottostanti vengono aggiunte in modo trasparente nella tabella columnstore di destinazione. Di seguito sono elencati alcuni esempi di nuove istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] che è possibile usare:

  ```sql
  CREATE CLUSTERED COLUMNSTORE INDEX cci
    ON <tableName>
    WITH (ONLINE = ON);
  ```

  ```sql
  ALTER INDEX cci
    ON <tableName>
    REBUILD WITH (ONLINE = ON);
  ```

#### <a name="always-encrypted-with-secure-enclaves-ctp-20"></a>Always Encrypted con enclave sicuri (CTP 2.0)

Espansione di Always Encrypted con crittografia sul posto e calcoli avanzati. Le espansioni provengono dall'abilitazione di calcoli sui dati di testo non crittografato all'interno di un enclave sicuro sul lato server.

Le operazioni di crittografia includono la crittografia delle colonne e la rotazione delle chiavi di crittografia della colonna. Queste operazioni possono ora essere trasmesse usando [!INCLUDE[tsql](../includes/tsql-md.md)] e non richiedono lo spostamento dei dati fuori dal database. Gli enclave sicuri rendono disponibile Always Encrypted per una vasta gamma di scenari, che dispongono di entrambi i requisiti seguenti:  

- L'esigenza di proteggere i dati sensibili da utenti con privilegi elevati ma non provvisti delle autorizzazioni necessarie, quali amministratori di database, amministratori di sistema, operatori cloud o istanze di malware.
- L'esigenza di supportare calcoli avanzati sui dati protetti all'interno del sistema di database.

Per informazioni dettagliate, vedere [Always Encrypted con enclave sicuri](../relational-databases/security/encryption/always-encrypted-enclaves.md).

> [!NOTE]
> Always Encrypted con enclave sicuri è disponibile solo nel sistema operativo Windows.

#### <a name="intelligent-query-processing-ctp-20"></a>Elaborazione di query intelligenti (CTP 2.0)

- Il **feedback delle concessioni di memoria in modalità riga** estende la funzionalità di feedback delle concessioni di memoria, adattando le dimensioni delle concessioni di memoria introdotte in [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] sia per gli operatori in modalità batch che per quelli in modalità riga. Per una condizione di concessione di memoria di dimensioni eccessive, se la memoria concessa supera di oltre due volte la quantità di memoria realmente usata, il feedback delle concessioni di memoria ricalcola la concessione. Le esecuzioni consecutive richiederanno quindi una quantità di memoria inferiore. Per le concessioni di memoria di dimensioni insufficienti che generano distribuzioni su disco, il feedback delle concessioni di memoria attiva il ricalcolo della concessione di memoria. Le esecuzioni consecutive richiederanno quindi una quantità di memoria superiore. Questa funzionalità è abilitata per impostazione predefinita nel livello di compatibilità del database 150.

- **Approximate COUNT DISTINCT** restituisce il numero approssimativo di valori univoci non Null in un gruppo. Questa funzione è progettata per l'uso in scenari Big Data. È ottimizzata per le query in cui sono vere tutte le condizioni seguenti:
   - Accede a set di dati costituiti da milioni di righe.
   - Definisce l'aggregazione di una o più colonne con un numero elevato di valori distinti.
   - La velocità di risposta è più importante della precisione assoluta.
      - `APPROX_COUNT_DISTINCT` restituisce i risultati con un'approssimazione alla risposta precisa pari al 2%.
      - La risposta approssimata viene restituita in una frazione minima del tempo necessario per la risposta esatta.

- La **modalità batch per rowstore** non richiede più un indice columnstore per l'elaborazione di una query in modalità batch. La modalità batch consente agli operatori di query di funzionare su un set di righe, anziché su una sola riga alla volta. Questa funzionalità è abilitata per impostazione predefinita nel livello di compatibilità del database 150. La modalità batch migliora la velocità delle query che accedono a tabelle rowstore quando sono soddisfatte le condizioni seguenti:
   - La query usa operatori analitici, ad esempio operatori di join o di aggregazione.
   - La query implica un numero di righe non inferiore a 100.000.
   - La query è associata alla CPU anziché all'input/output di dati.
   - La creazione e l'uso di un indice columnstore può comportare uno degli svantaggi seguenti:
      - Aggiunge un sovraccarico eccessivo alla query.
      - Non è implementabile perché l'applicazione dipende da una funzionalità non ancora supportata con gli indici columnstore.

- **La compilazione posticipata delle variabili di tabella** migliora la qualità del piano e le prestazioni generali per le query che fanno riferimento a variabili di tabella. Durante l'ottimizzazione e la compilazione iniziale, questa funzionalità propagherà le stime della cardinalità basate sui conteggi effettivi delle righe di variabili di tabella. Queste informazioni accurate sui conteggi di righe verranno usate per l'ottimizzazione delle operazioni del piano downstream. Questa funzionalità è abilitata per impostazione predefinita nel livello di compatibilità del database 150.

Per usare la funzionalità di elaborazione di query intelligenti impostare l'opzione del database `COMPATIBILITY_LEVEL = 150`.

#### <a id="programmability"></a> Estensioni di programmabilità per il linguaggio Java (CTP 2.0)

- **Estensione per il linguaggio Java (anteprima)** : usare l'estensione per il linguaggio Java per eseguire codice Java in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. In [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] questa estensione viene installata quando si aggiunge la funzionalità "Machine Learning Services (in-database)" all'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

#### <a id="sqlgraph"></a> Funzionalità grafo SQL (CTP 2.3)

- **Usare alias di tabelle o viste derivate nelle query corrispondenti ai grafi (CTP 2.1)** Le query per grafi nell'anteprima di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] supportano l'uso di alias di tabelle e viste derivate nella sintassi di `MATCH`. Per usare questi alias in `MATCH`, le viste e tabelle derivate devono essere create su un set di tabelle nodi o un set di tabelle archi, usando l'operatore `UNION ALL`. Le tabelle nodi o le tabelle archi possono o meno avere filtri applicati. La possibilità di usare alias di tabelle o viste derivate nelle query `MATCH` può essere molto utile in scenari in cui si intende eseguire query su entità eterogenee o connessioni eterogenee tra due o più entità nel grafo.

- **Il supporto delle corrispondenze in `MERGE` DML (CTP 2.0)** consente di specificare relazioni grafo in un'unica istruzione anziché in istruzioni `INSERT`, `UPDATE` o `DELETE` separate. È possibile unire i dati grafo correnti da tabelle nodi o tabelle archi a nuovi dati usando i predicati `MATCH` nell'istruzione `MERGE`. Questa funzionalità abilita gli scenari `UPSERT` nelle tabelle bordi. Ora gli utenti possono usare un'istruzione merge singola per inserire un nuovo bordo o aggiornarne uno esistente tra due nodi.

- Sono stati introdotti i **vincoli di arco (CTP 2.0)** per le tabelle archi nel grafo SQL. Le tabelle bordi possono connettere qualsiasi nodo a qualsiasi altro nodo del database. Con l'introduzione di vincoli di bordo, è ora possibile applicare determinate restrizioni a questo comportamento. Il nuovo vincolo `CONNECTION` consente di specificare il tipo di nodi ai quali può connettersi una tabella bordi nello schema. 

  **(CTP 2.3)**  Estendendo ancora di più questa funzionalità, è possibile definire azioni di eliminazione propagata in un vincolo di arco. È possibile definire le azioni eseguite dal motore di database quando un utente elimina i nodi che un arco specifico connette.

#### <a name="database-scoped-default-setting-for-online-and-resumable-ddl-operations-ctp-20"></a>Impostazione predefinita con ambito database per operazioni DDL online e ripristinabili (CTP 2.0)

- L'**impostazione predefinita con ambito database per operazioni DDL online e ripristinabili** supporta un'impostazione di funzionamento predefinita per le operazioni indice `ONLINE` e `RESUMABLE` a livello del database, anziché definire tali opzioni per ogni singola istruzione DDL dell'indice, quali le operazioni di creazione o ricompilazione dell'indice.

- Impostare questi valori predefiniti usando le opzioni di configurazione con ambito database `ELEVATE_ONLINE` e `ELEVATE_RESUMABLE`. Entrambe le opzioni fanno sì che il motore del database imposti automaticamente le operazioni dell'indice supportate per l'esecuzione online o ripristinabili. È possibile abilitare i comportamenti seguenti tramite queste opzioni:

  - L'opzione `FAIL_UNSUPPORTED` autorizza tutte le operazioni sugli indici online o ripristinabili e non consente le operazioni sugli indici online o ripristinabili non supportate.
  - L'opzione `WHEN_SUPPPORTED` consente le operazioni online o ripristinabili supportate ed esegue le operazioni sugli indici non supportate non in linea o in modo non ripristinabile.
  - L'opzione `OFF` supporta il comportamento corrente di esecuzione di tutte le operazioni sugli indici come offline e non ripristinabili, salvo diversa indicazione esplicita nell'istruzione DDL.

Per eseguire l'override dell'impostazione predefinita, includere l'opzione `ONLINE` o l'opzione `RESUMABLE` nei comandi di creazione e ricompilazione dell'indice. 

Senza questa funzionalità è necessario specificare le opzioni online e ripristinabili direttamente nell'istruzione DDL dell'indice, ad esempio nell'istruzione di creazione e ricompilazione dell'indice.

Per altre informazioni sulle operazioni ripristinabili, vedere [Creazione di indici online ripristinabili](https://azure.microsoft.com/blog/resumable-online-index-create-is-in-public-preview-for-azure-sql-db/).

#### <a id="ha"></a>Gruppi di disponibilità Always On - Più repliche sincrone (CTP 2.0)

- **Fino a cinque repliche sincrone**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] aumenta il numero massimo di repliche sincrone fino a 5. Il numero massimo era 3 in [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. È possibile configurare questo gruppo di cinque repliche per il failover automatico all'interno del gruppo. Sono presenti una replica primaria e 4 repliche secondarie sincrone.

- **Reindirizzamento della connessione di replica da secondaria a primaria**: consente di orientare le connessioni dell'applicazione client alla replica primaria, indipendentemente dal server di destinazione specificato nella stringa di connessione. Questa funzionalità consente il reindirizzamento della connessione senza un listener. Usare il reindirizzamento della connessione di replica da secondaria a primaria se si verificano le condizioni seguenti:

  - La tecnologia cluster non offre una funzionalità listener.
  - È implementata una configurazione con più subnet in cui il reindirizzamento diventa complesso.
  - Scenari di scalabilità in lettura o ripristino di emergenza in cui il tipo di cluster è `NONE`.

Per informazioni dettagliate, vedere [Secondary to primary replica read/write connection redirection (Always On Availability Groups)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md) (Reindirizzamento connessione in lettura/scrittura dalla replica secondaria alla primaria (Gruppi di disponibilità AlwaysOn)).

#### <a name="data-discovery-and-classification-ctp-20"></a>Individuazione e classificazione dei dati (CTP 2.0)

Funzionalità avanzate di individuazione e classificazione dei dati incorporate a livello nativo in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La classificazione e l'assegnazione di etichette ai dati più sensibili offre i vantaggi seguenti:
- Contribuisce a soddisfare i requisiti in materia di privacy e di conformità alle normative.
- Supporta scenari di sicurezza quali il monitoraggio (controllo) e gli avvisi in caso di accesso anomalo ai dati sensibili.
- Semplifica l'identificazione della posizione dei dati sensibili nell'organizzazione, in modo che gli amministratori possano adottare le misure necessarie per la protezione del database.

Per altre informazioni, vedere [Individuazione dati e classificazione SQL](../relational-databases/security/sql-data-discovery-and-classification.md).

Anche il [controllo](../relational-databases/security/auditing/sql-server-audit-database-engine.md) è stato migliorato e il log di controllo ora include un nuovo campo denominato `data_sensitivity_information`, che registra le classificazioni (etichette punteggio) di riservatezza dei dati effettivi restituiti dalla query. Per dettagli ed esempi vedere [ADD SENSITIVITY CLASSIFICATION](../t-sql/statements/add-sensitivity-classification-transact-sql.md).

>[!NOTE]
>Non sono state apportate modifiche alle modalità di abilitazione del controllo. È stato aggiunto ai record di controllo un nuovo campo `data_sensitivity_information`, che registra le classificazioni (etichette punteggio) di riservatezza dei dati effettivi restituiti dalla query. Vedere [Controllo dell'accesso ai dati sensibili](/azure/sql-database/sql-database-data-discovery-and-classification/#subheading-3).

#### <a name="expanded-support-for-persistent-memory-devices-ctp-20"></a>Supporto esteso per i dispositivi con memoria persistente (CTP 2.0)

Qualsiasi file [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] inserito in un dispositivo con memoria persistente può ora essere eseguito in modalità *con riconoscimento*. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] accede direttamente al dispositivo, ignorando lo stack di archiviazione del sistema operativo e usando operazioni memcpy efficienti. Questa modalità migliora le prestazioni poiché consente input/output a bassa latenza su tali dispositivi.
    - Esempi di file [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] includono:
        - File di database
        - File di log delle transazioni
        - File del checkpoint OLTP in memoria
    - La memoria persistente è anche detta memoria della classe di archiviazione.
    - La memoria persistente è talvolta denominata in modo informale *pmem* in siti Web non Microsoft.

> [!NOTE]
> Per questa versione di anteprima il riconoscimento dei file nei dispositivi con memoria persistente è disponibile solo per Linux. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Windows supporta i dispositivi con memoria persistente a partire da [!INCLUDE[ssSQL15](../includes/sssql15-md.md)].

#### <a name="support-for-columnstore-statistics-in-dbcc-clonedatabase-ctp-20"></a>Supporto delle statistiche columnstore in DBCC CLONEDATABASE (CTP 2.0)

`DBCC CLONEDATABASE` crea una copia di un database con il solo schema, che include tutti gli elementi necessari per la risoluzione dei problemi di prestazioni delle query senza copiare i dati. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] il comando non copiava le statistiche necessarie per rilevare con precisione i problemi delle query dell'indice columnstore e per acquisire queste informazioni erano necessari passaggi manuali. In [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] ora `DBCC CLONEDATABASE` acquisisce automaticamente i BLOB di statistiche per gli indici columnstore. Di conseguenza non sono necessari passaggi manuali.

#### <a name="new-options-added-to-spestimatedatacompressionsavings-ctp-20"></a>Nuove opzioni aggiunte a sp_estimate_data_compression_savings (CTP 2.0)

`sp_estimate_data_compression_savings` restituisce le dimensioni correnti degli oggetti richiesti e stima le dimensioni dell'oggetto per lo stato di compressione richiesto. Questa procedura supporta attualmente tre opzioni: `NONE`, `ROW` e `PAGE`. `COLUMNSTORE_ARCHIVE` introduce due nuove opzioni: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] e `COLUMNSTORE`. Le nuove opzioni consentono di stimare il risparmio di spazio ottenibile con la creazione di un indice columnstore sulla tabella usando la compressione del columnstore standard o archivio.

#### <a id="ml"></a> Cluster di failover di SQL Server Machine Learning Services e modellazione basata sulle partizioni (CTP 2.0)

- **Modellazione basata sulle partizioni**: elabora gli script esterni per le singole partizioni dei dati usando i nuovi parametri aggiunti a `sp_execute_external_script`. Questa funzionalità supporta il training di molti modelli di dimensioni ridotte (un modello per ogni partizione dei dati) invece del training di un solo modello di grandi dimensioni.

- **Cluster di failover di Windows Server**: è possibile configurare la disponibilità elevata per Machine Learning Services in un cluster di failover di Windows Server.

Per informazioni dettagliate, vedere [What's new in SQL Server Machine Learning Services](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md) (Novità di SQL Server Machine Learning Services).

#### <a name="lightweight-query-profiling-infrastructure-enabled-by-default-ctp-20"></a>Infrastruttura leggera di profilatura query abilitata per impostazione predefinita (CTP 2.0)

L'infrastruttura leggera di profilatura query (LWP) restituisce dati sulle prestazioni delle query in modo più efficiente rispetto ai meccanismi di profilatura standard. Ora la profilatura leggera è abilitata per impostazione predefinita. È stata introdotta in [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. La profilatura leggera offre un meccanismo per la raccolta di statistiche sull'esecuzione query con un sovraccarico previsto pari al 2% della capacità della CPU, rispetto a un sovraccarico che può raggiungere il 75% della capacità della CPU per il meccanismo di profilatura query standard. Nelle versioni precedenti, questa funzionalità era OFF per impostazione predefinita. Gli amministratori di database potevano abilitarla con il [flag di traccia 7412](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). 

Per altre informazioni sulla profilatura leggera, vedere [Infrastruttura di profilatura query](../relational-databases/performance/query-profiling-infrastructure.md).

**CTP 2.3** Viene introdotta una nuova configurazione con ambito database `LIGHTWEIGHT_QUERY_PROFILING` per abilitare o disabilitare l'infrastruttura di profilatura delle query leggera.

#### <a id="polybase"></a>Nuovi connettori PolyBase

- **Nuovi connettori per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata e MongoDB**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] presentazione di nuovi connettori a dati esterni per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata e MongoDB.

#### <a name="new-sysdmdbpageinfo-system-function-returns-page-information-ctp-20"></a>La nuova funzione di sistema sys.dm_db_page_info restituisce informazioni sulla pagina (CTP 2.0)

`sys.dm_db_page_info(database_id, file_id, page_id, mode)` restituisce informazioni su una pagina di un database. La funzione restituisce una riga che contiene le informazioni di intestazione della pagina, tra cui `object_id`, `index_id` e `partition_id`. Questa funzione sostituisce l'uso di `DBCC PAGE` nella maggior parte dei casi. 

Per facilitare la risoluzione dei problemi associati alle attese correlate alla pagina è stata anche aggiunta a `sys.dm_exec_requests` e `sys.sysprocesses` la nuova colonna page_resource. La nuova colonna consente di unire `sys.dm_db_page_info` a queste viste tramite un'altra nuova funzione di sistema: `sys.fn_PageResCracker`. Vedere come esempio lo script seguente:

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d 
  CROSS APPLY sys.fn_PageResCracker(d.page_resource) AS r
  CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id,'DETAILED')
    AS page_info;
```

### <a id="sqllinux"></a> SQL Server in Linux

- **Gruppo di disponibilità AlwaysOn in contenitori Docker con Kubernetes (CTP 2.2)** : Kubernetes può orchestrare i contenitori che eseguono istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per restituire un set di database a disponibilità elevata con Gruppi di disponibilità Always On di SQL Server. Un operatore Kubernetes distribuisce un elemento StatefulSet che include un contenitore con **mssql-server** e un monitoraggio di integrità.

- **Nuovo Registro Container (CTP 2.1)** : tutte le immagini del contenitore per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] e per [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] si trovano ora nel Registro Container Microsoft. Il Registro Container Microsoft è il registro contenitori ufficiale per la distribuzione di contenitori prodotto Microsoft. Ora vengono anche pubblicate le immagini certificate basate su RHEL.

  - Registro Container Microsoft: `mcr.microsoft.com/mssql/server:vNext-CTP2.0`
  - Immagini del contenitore certificate basate su RHEL: `mcr.microsoft.com/mssql/rhel/server:vNext-CTP2.0`

- **Supporto della replica (CTP 2.0)** : [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] supporta la replica di SQL Server in Linux. Una macchina virtuale Linux con SQL Agent può essere un'entità di pubblicazione, di distribuzione o un sottoscrittore. 

  Creare i seguenti tipi di pubblicazioni:
  - Transazionale
  - Snapshot
  - Merge

  Configurare la replica [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] oppure usare le [stored procedure di replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

- **Supporto per Microsoft Distributed Transaction Coordinator (MSDTC) (CTP 2.0)** : [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] in Linux supporta Microsoft Distributed Transaction Coordinator (MSDTC). Per informazioni dettagliate, vedere [Come configurare Microsoft Distributed Transaction Coordinator (MSDTC) in Linux](../linux/sql-server-linux-configure-msdtc.md).

- **Supporto OpenLDAP per provider AD di terze parti (CTP 2.0)** : [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] in Linux è supportato OpenLDAP, che consente ai fornitori di terze parti di accedere a Active Directory.

- **Machine Learning in Linux (CTP 2.0)** : [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Machine Learning Services (In-Database) è ora supportato in Linux. Il supporto include la stored procedure `sp_execute_external_script`. Per istruzioni su come installare Machine Learning Services in Linux, vedere [Installare [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]Machine Learning Services (R, Python, Java) in Linux](../linux/sql-server-linux-setup-machine-learning.md).

### <a id="mds"></a> Master Data Services 

- **Controlli Silverlight sostituiti con HTML (CTP 2.0)** : il portale Master Data Services (MDS) non è più dipendente da Silverlight. Tutti i componenti Silverlight precedenti sono stati sostituiti con controlli HTML.

### <a id="security"></a>Security

- **Gestione certificati in Gestione configurazione SQL Server (CTP 2.0)** : i certificati SSL/TLS sono usati in modo estensivo per proteggere l'accesso alle istanze di SQL Server. La gestione dei certificati è ora integrata in Gestione configurazione SQL Server e questo semplifica varie attività comuni, ad esempio:

  - Visualizzazione e convalida di certificati installati in un'istanza [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 
  - Visualizzazione di certificati prossimi alla scadenza.
  - Distribuzione di certificati tra computer appartenenti a gruppi di disponibilità AlwaysOn (dal nodo che contiene la replica primaria).
  - Distribuzione di certificati tra computer appartenenti a un'istanza del cluster di failover (dal nodo attivo).

  > [!NOTE]
  > L'utente deve avere autorizzazioni amministratore per tutti i nodi del cluster.

### <a id="tools"></a>Strumenti

- [**Azure Data Studio**](../azure-data-studio/what-is.md): rilasciato in precedenza con il nome di anteprima di SQL Operations Studio, Azure Data Studio è uno strumento desktop leggero, moderno, open source e multipiattaforma per le attività più comuni di sviluppo e amministrazione di dati. Con Azure Data Studio e l'[estensione di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](../azure-data-studio/sql-server-2019-extension.md) è possibile connettersi a SQL Server in locale e nel cloud in Windows, macOS e Linux. Con Azure Data Studio è possibile:

<a name = "tools-ctp23"></a>

  - È ora incluso il supporto per AAD. (CTP 2.3)
  - L'interfaccia utente di visualizzazione di Notebooks è stata spostata nella memoria centrale di Azure Data Studio. (CTP 2.3)
  - Aggiunta una nuova procedura guidata per creare origini dati esterne da Hadoop Distributed File System (HDFS) a cluster Big Data di SQL Server. (CTP 2.3)
  - Interfaccia utente di visualizzazione di Notebooks. (CTP 2.3)
  - Aggiunte nuove API Notebooks. (CTP 2.3)
  - Aggiunto il comando "Reinstall Notebook dependencies" (Reinstalla dipendenze Notebooks) per assistenza durante gli aggiornamenti dei pacchetti Python. (CTP 2.3)
  - Connettersi e gestire i cluster Big Data di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. (CTP 2.1)
  - Modificare ed eseguire query in un ambiente di sviluppo moderno, con esecuzione rapida di Intellisense, frammenti di codice e integrazione del controllo codice sorgente. (CTP 2.0) 
  - Visualizzare rapidamente i dati con la funzionalità predefinita di creazione grafici dai set di risultati. (CTP 2.0)
  - Creare dashboard personalizzati per i server e i database mediante widget personalizzabili. (CTP 2.0)  
  - Gestire facilmente l'ambiente nel suo complesso, grazie al terminale incorporato. (CTP 2.0)
  - Analizzare i dati con un'esperienza di tipo notebook integrata basata su Jupyter. (CTP 2.0)
  - Migliorare l'esperienza con estensioni e temi personalizzati. (CTP 2.0)
  - Esplorare le risorse di Azure con un browser incorporato degli abbonamenti e delle risorse. (CTP 2.0)
  - Supporta gli scenari che usano il cluster Big Data di SQL Server. (CTP 2.0)
  
  > [!TIP]
  > Per i miglioramenti più recenti ad Azure Data Studio, vedere le [Note sulla versione per Azure Data Studio](../azure-data-studio/release-notes-azure-data-studio.md).

- [**SQL Server Management Studio (SSMS) 18.0 (anteprima)** ](../ssms/sql-server-management-studio-ssms.md): Supporta [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

  - Avvio di Azure Data Studio da SSMS. (CTP 2.3)
  - Supporto di Always Encrypted con enclave sicuri. (CTP 2.0)
  - File di download di dimensioni più piccole. (CTP 2.0)
  - Ora basato su Visual Studio 2017 Isolated Shell. (CTP 2.0)
  - Per l'elenco completo, vedere il [log delle modifiche SSMS](../ssms/release-notes-ssms.md). (CTP 2.0)

- [**Modulo SQL Server PowerShell**](http://www.powershellgallery.com/packages/SqlServer/21.1.18080): Il modulo SQL Server PowerShell consente agli sviluppatori e amministratori di SQL Server, nonché ai professionisti di Business Intelligence di automatizzare la distribuzione del database e l'amministrazione del server.

  - Aggiornamento da 21.0 a 21.1 per supportare SMO v150.
  - Aggiornato il provider di SQL Server (SQLRegistration) per visualizzare i gruppi AS/IS/RS.
  - Corretto il problema nel cmdlet `New-SqlAvailabilityGroup` quando la destinazione è SQL Server 2014.
  - Aggiunto il parametro `–LoadBalancedReadOnlyRoutingList` a `Set-SqlAvailabilityReplica` e `New-SqlAvailabilityReplica`.
  - Aggiornato il cmdlet `AnalysisService` per usare l'accesso memorizzato nella cache di `Login-AzureAsAccount` per Azure Analysis Services.

### <a id="ssas"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Analysis Services (SSAS) 

#### <a name="many-to-many-ctp24"></a>Relazioni molti-a-molti nei modelli tabulari (CTP 2.4)

Questa funzionalità consente le relazioni molti-a-molti tra le tabelle in cui entrambe le colonne non sono univoche. È possibile definire una relazione tra una tabella delle dimensioni e una tabella dei fatti con una granularità maggiore rispetto alla colonna chiave delle dimensioni. Questo evita di dover normalizzare le tabelle delle dimensioni e può migliorare l'esperienza utente poiché il modello risultante ha un numero minore di tabelle con colonne raggruppate logicamente. In questa versione CTP 2.4 le relazioni molti-a-molti sono funzionalità solo motore. 

Le relazioni molti-a-molti richiedono modelli con livello di compatibilità 1470 che è attualmente supportato solo in [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.3 e versioni successive. Per questa versione CTP 2.4, è possibile creare relazioni molti-a-molti tramite l'API Modello a oggetti tabulare, TMSL (Tabular Model Scripting Language) e l'editor di modelli tabulari open source. Il supporto in SQL Server Data Tools verrà incluso in una versione futura. Seguirà documentazione. Informazioni aggiuntive per questa e altre funzionalità CTP rilasciate saranno disponibili nel blog di Analysis Services.

#### <a name="property-ctp24"></a>Impostazioni di memoria per la governance delle risorse (CTP 2.4)

Le impostazioni di memoria descritte di seguito sono già disponibili in Azure Analysis Services. A partire dalla versione CTP 2.4, sono ora supportate anche da Analysis Services di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. 

- **Memory\QueryMemoryLimit**: questa proprietà di memoria consente di limitare gli spooling di memoria creati dalle query DAX inviate al modello. 
- **DbpropMsmdRequestMemoryLimit**: questa proprietà XMLA consente di eseguire l'override del valore della proprietà del server Memory\QueryMemoryLimit per una connessione.
- **OLAP\Query\RowsetSerializationLimit**: questa proprietà del server limita il numero di righe restituite in un set di righe, proteggendo le risorse del server da un utilizzo esteso dell'esportazione di dati. Questa proprietà si applica alle query DAX e MDX.

Queste proprietà possono essere impostate usando la versione più recente di SQL Server Management Studio (SSMS). Informazioni aggiuntive per questa funzionalità saranno disponibili nel blog di Analysis Services.

#### <a name="calc-ctp24"></a>Gruppi di calcolo in modelli tabulari (CTP 2.3) 

I gruppi di calcolo consentono di risolvere un problema comune nei modelli complessi in cui si può assistere a una proliferazione di misure con gli stessi calcoli, ad esempio la funzionalità di Business Intelligence per le gerarchie temporali. I gruppi di calcolo vengono visualizzati nei client di creazione report sotto forma di tabella con una singola colonna. Ogni valore nella colonna rappresenta un calcolo riutilizzabile o un elemento di calcolo che può essere applicato a qualsiasi misura.  

Un gruppo di calcolo può avere qualsiasi numero di elementi di calcolo. Ogni elemento di calcolo è definito da un'espressione DAX. Sono state introdotte tre nuove funzioni DAX per poter usare i gruppi di calcolo: 

- `SELECTEDMEASURE()`: restituisce un riferimento alla misura attualmente nel contesto.  

- `SELECTEDMEASURENAME()`: restituisce una stringa contenente il nome della misura attualmente nel contesto.  

- `ISSELECTEDMEASURE(M1, M2, …)`: restituisce un valore booleano che indica se la misura attualmente nel contesto è una di quelle specificate come argomento.

Oltre alle nuove funzioni DAX, vengono introdotte due nuove DMV:

- `TMSCHEMA_CALCULATION_GROUPS`  
- `TMSCHEMA_CALCULATION_ITEMS`  

##### <a name="limitations-in-this-release"></a>Limitazioni in questa versione:

- La funzione `ALLSELECTED DAX` non è ancora supportata.
- La funzionalità Sicurezza a livello di riga definita nella tabella del gruppo di calcolo non è ancora supportata.
- La funzionalità Sicurezza a livello di oggetto definita nella tabella del gruppo di calcolo non è ancora supportata.
- Le espressioni DetailsRows che fanno riferimento agli elementi di calcolo non sono ancora supportate.
- La dimensione MDX non è ancora supportata.

##### <a name="known-issues-in-this-release"></a>Problemi noti di questa versione:

- La presenza di gruppi di calcolo in un modello potrebbe fare in modo che le misure restituiscano tipi di dati Variant che possono causare errori di aggiornamento per le colonne calcolate e le tabelle che fanno riferimento alle misure.

##### <a name="compatibility-level"></a>Livello di compatibilità

I gruppi di calcolo richiedono modelli con livello di compatibilità 1470 che è attualmente supportato solo in [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.3 e versioni successive. Attualmente è possibile creare gruppi di calcolo tramite l'API del Modello a oggetti tabulare, TMSL (Tabular Model Scripting Language) e l'editor di modelli tabulari open source. Il supporto in SQL Server Data Tools verrà incluso in una versione futura. Seguirà documentazione. Informazioni aggiuntive per questa e altre funzionalità CTP rilasciate saranno disponibili nel blog di Analysis Services.

## <a name="see-also"></a>Vedere anche

- [`SqlServer` Modulo PowerShell](https://www.powershellgallery.com/packages/Sqlserver)
- [Documentazione di SQL Server PowerShell](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>Passaggi successivi

- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Note sulla versione](sql-server-ver15-release-notes.md).

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]: white paper tecnico](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />Pubblicato in settembre 2018. Si applica a Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0 per Windows, Linux e i contenitori Docker.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
