---
title: Note sulla versione
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive gli aggiornamenti più recenti e i problemi [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] noti per (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bcbc3537a6ba26dc907bf348c565939ff869ea43
ms.sourcegitcommit: da8bb7abd256b2bebee7852dc0164171eeff11be
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/14/2019
ms.locfileid: "70988100"
---
# <a name="release-notes-for-sql-server-big-data-clusters"></a>Note sulla versione per i cluster SQL Server Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo elenca gli aggiornamenti e conosce i problemi per le versioni più recenti [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]di.

## <a id="rc"></a>Versione finale candidata (agosto)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in 2019 SQL Server versione finale candidata.

### <a name="whats-new"></a>Novità

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|SQL Server Always On gruppo di disponibilità |Quando si distribuisce un cluster SQL Server Big data, è possibile configurare la distribuzione per creare un gruppo di disponibilità da fornire:<br/><br/>-Disponibilità elevata <br/><br/>-Lettura-scalabilità orizzontale <br/><br/>-Inserimento di dati con scalabilità orizzontale nel pool di dati<br/><br>Vedere [distribuire con disponibilità elevata](../big-data-cluster/deployment-high-availability.md). |
|`azdata` |Installazione semplificata per lo strumento con [installazione Manager](./deploy-install-azdata-linux-package.md)<br/><br/>[`azdata notebook`comando](./reference-azdata-notebook.md)<br/><br/>[`azdata bdc status`comando](./reference-azdata-bdc-status.md) |
|Azure Data Studio|[Scaricare la build finale candidata di Azure Data Studio](deploy-big-data-tools.md#download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc).<br/><br/>Aggiunta di notebook per la risoluzione dei problemi tramite SQL Server manuale della Guida di 2019 Jupyter.<br/><br/>Aggiunta dell'esperienza di accesso del controller.<br/><br/>Aggiunta del dashboard del controller per visualizzare gli endpoint di servizio, visualizzare lo stato di integrità del cluster e accedere ai notebook per la risoluzione dei problemi.<br/><br/>Miglioramento delle prestazioni di modifica/output delle celle notebook.|
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemi noti

* SQL Server 2019 i cluster Big Data rilasciano il numero `15.0.1900.47`di build dell'aggiornamento candidata.

* Il profilo di distribuzione "kubeadm-prod" non è supportato nei cluster SQL Server 2019 Big Data Release Candidate con il numero di build precedente. Usare invece il profilo "kubeadm-dev-test" per le distribuzioni di Kubeadm.

## <a id="ctp32"></a> CTP 3.2 (luglio)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 3.2.

### <a name="whats-new"></a>Novità

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Anteprima pubblica |Prima della versione CTP 3.2, il cluster Big Data di SQL Server era disponibile per gli early adopter registrati. Questa versione consente a chiunque di sperimentare le funzionalità dei cluster Big Data di SQL Server. <br/><br/> Vedere [Introduzione a [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](deploy-get-started.md).|
|`azdata` |La versione CTP 3.2 introduce `azdata`, un'utilità da riga di comando scritta in Python che consente agli amministratori del cluster di avviare e gestire il cluster Big Data tramite le API REST. `azdata` sostituisce `mssqlctl`. Vedere [Installare `azdata`](deploy-install-azdata.md). |
|PolyBase |I nomi delle colonne della tabella esterna vengono ora usati per eseguire query su origini dati SQL Server, Oracle, Teradata, MongoDB e ODBC. Nelle versioni CTP precedenti le colonne nell'origine dati esterna venivano associate solo in base alla posizione ordinale e i nomi specificati nella definizione EXTERNAL TABLE non venivano usati. |
|Aggiornamento della suddivisione in livelli HDFS |Introduzione della funzionalità di aggiornamento per la suddivisione in livelli HDFS, in modo che sia possibile aggiornare un montaggio esistente per l'ultimo snapshot dei dati remoti. Vedere [Suddivisione in livelli HDFS](hdfs-tiering.md) |
|Risoluzione dei problemi basata su notebook |La versione CTP 3.2 introduce notebook Jupyter che semplificano le operazioni di [distribuzione](deploy-notebooks.md), [individuazione, diagnosi e risoluzione dei problemi](manage-notebooks.md) per i componenti in un cluster Big Data di SQL Server. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni per questa versione.

#### <a name="polybase"></a>PolyBase

- Il push della clausola TOP quando il conteggio è > 1000 non è supportato in questa versione. In questi casi, tutte le righe verranno lette dall'origine dati remota. (Risolto nella versione finale candidata)

- Il push di join con percorso condiviso nelle origini dai esterne non è supportato in questa versione. Ad esempio, il push di due tabelle del pool di dati con tipo di distribuzione ROUND_ROBIN sposterà i dati nell'istanza SQL master o nell'istanza del pool di calcolo per eseguire l'operazione di join.

#### <a name="compute-pool"></a>Pool di calcolo

- La distribuzione di cluster Big Data supporta solo pool di calcolo con una istanza. (Risolto nella versione finale candidata)

#### <a name="storage-pool"></a>Pool di archiviazione

- L'esecuzione di query su file Parquet in un pool di archiviazione non supporta determinati tipi di dati.

- Non è possibile eseguire query sulle colonne padre MAP e LIST, né sulle colonne padre senza un tipo collegato. In questo caso, viene restituito un errore.

- Non è possibile eseguire query sui nodi REPEATED e potrebbero venire restituiti risultati non corretti.

## <a id="ctp31"></a> CTP 3.1 (giugno)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 3.1.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Modifiche dei comandi `mssqlctl` | I comandi `mssqlctl cluster` sono stati rinominati `mssqlctl bdc`. Per altre informazioni, vedere le [`mssqlctl`informazioni di riferimento](reference-azdata.md). |
| Nuovi comandi di stato `mssqlctl` e rimozione del portale di amministrazione dei cluster. | Il portale di amministrazione dei cluster è stato rimosso in questa versione. Sono stati aggiunti nuovi comandi di stato a `mssqlctl` che integrano i comandi di monitoraggio esistenti. |
| Pool di calcolo di Spark | È possibile creare nodi aggiuntivi per incrementare la potenza di calcolo di Spark senza dover aumentare le prestazioni dell'archiviazione. È inoltre possibile avviare i nodi del pool di archiviazione che non vengono usati per Spark. Spark e l'archiviazione sono separati. Per altre informazioni, vedere [Configurare l'archiviazione senza Spark](deployment-custom-configuration.md#sparkstorage). |
| Connettore Spark MSSQL | Supporto per la lettura/scrittura nelle tabelle esterne del pool di dati. Nelle versioni precedenti era supportata solo la lettura/scrittura nelle tabelle dell'istanza MASTER. Per altre informazioni, vedere [Come leggere e scrivere in SQL Server da Spark usando il connettore Spark MSSQL](spark-mssql-connector.md). |
| Machine Learning tramite MLeap | [Eseguire il training di un modello di Machine Learning MLeap in Spark e assegnargli un punteggio in SQL Server tramite l'estensione per il linguaggio Java](spark-create-machine-learning-model.md). |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni per questa versione.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, potrebbe venire visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file con dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche della configurazione in HDFS che comportano modifiche di hdfs-site.xml non sono supportate.

#### <a name="deployment"></a>Distribuzione

- L'aggiornamento di un cluster Big Data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster Big Data esistente (usando la versione precedente di **azdata**) prima di distribuire la versione più recente. Per altre informazioni, vedere [Eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione nel servizio Azure Kubernetes, è possibile che vengano visualizzati i due eventi di avviso seguenti della distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la corretta distribuzione del cluster Big Data nel servizio Azure Kubernetes.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Ciò potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="external-tables"></a>Tabelle esterne

- La distribuzione di cluster Big data non comporta più la creazione delle origini dati esterne **SqlDataPool** e **SqlStoragePool**. È possibile creare queste origini dati manualmente per supportare la virtualizzazione dei dati nel pool di dati e nel pool di archiviazione.

   > [!NOTE]
   > L'URI per la creazione di queste origini dati esterne è diverso per ogni versione CTP. Vedere i comandi Transact-SQL seguenti per informazioni sulla loro creazione 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, si riceve un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, potrebbe verificarsi un errore se contemporaneamente è in corso la copia del file sottostante in HDFS.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si crea una tabella esterna a Oracle che usa dati di tipo carattere, la procedura guidata di virtualizzazione di Azure Data Studio interpreta queste colonne come VARCHAR nella definizione di tabella esterna. Ciò causerà un errore nel linguaggio DDL (Data Definition Language) della tabella esterna. Modificare lo schema Oracle per usare il tipo NVARCHAR2 oppure creare manualmente istruzioni EXTERNAL TABLE e specificare NVARCHAR invece di usare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione R, Python o MLeap dall'API RESTful, si verifica il timeout della chiamata dopo 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP dei pod cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Se viene riavviato il pod master, è possibile che si verifichi un errore della sessione Spark con l'eccezione `NoRoteToHostException`. Questa situazione è causata dal mancato aggiornamento delle cache JVM con i nuovi indirizzi IP.

- Se Jupyter è già installato ed è presente un ambiente Python separato in Windows, potrebbe verificarsi un errore dei notebook Spark. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- Se in un notebook si fa clic sul comando **Aggiungi testo**, la cella di testo viene aggiunta in modalità di anteprima invece che in modalità di modifica. È possibile fare clic sull'icona di anteprima per passare alla modalità di modifica e modificare la cella.

#### <a name="security"></a>Security

- La variabile SA_PASSWORD fa parte dell'ambiente ed è individuabile (ad esempio in un file core dump). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Non si tratta di un bug ma di un passaggio di sicurezza. Per altre informazioni su come modificare SA_PASSWORD in un contenitore Linux, vedere [Cambiare la password dell'amministratore di sistema](../linux/quickstart-install-connect-docker.md#sapassword).

- I log del servizio Azure Kubernetes possono contenere la password dell'amministratore di sistema per le distribuzioni di cluster Big Data.

#### <a name="kibana-logs-dashboards"></a>Dashboard dei log di Kibana

- Tra Aris CTP 3.0 e 3.1, la versione di Kibana è stata aggiornata da 6.3.1 a 7.0.1.  Questo ha reso il browser Microsoft Edge incompatibile con Kibana. Quando si carica la versione corrente dei dashboard Kibana in Microsoft Edge, gli utenti visualizzeranno una pagina vuota. Vedere [qui]( https://www.elastic.co/support/matrix#matrix_browse) per i browser supportati per Kibana.rs 


## <a id="ctp30"></a> CTP 3.0 (maggio)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 3.0.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Aggiornamenti di **mssqlctl** | Numerosi [aggiornamenti di comandi e parametri](reference-azdata.md) **mssqlctl** tra cui un aggiornamento al comando **mssqlctl login**, che ora ha come destinazione il nome utente e l'endpoint del controller. |
| Miglioramenti all'archiviazione | Supporto per configurazioni di archiviazione diverse per log e dati. È stato anche ridotto il numero di attestazioni di volume permanente per un cluster di Big Data. |
| Più istanze del pool di calcolo | Supporto per più istanze del pool di calcolo. |
| Nuove funzionalità e comportamento del pool | Il pool di calcolo viene ora usato per impostazione predefinita per le operazioni del pool di dati e del pool di archiviazione solo nella distribuzione **ROUND_ROBIN**. Il pool di dati ora può usare un nuovo tipo di distribuzione **REPLICATED**, il che significa che gli stessi dati sono presenti in tutte le istanze del pool di dati. |
| Miglioramenti alle tabelle esterne | Le tabelle esterne del tipo origine dati HADOOP ora supportano la lettura di righe con dimensioni fino a 1 MB. Le tabelle esterne (ODBC, pool di archiviazione, pool di dati) ora supportano righe larghe quanto una tabella di SQL Server. |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni per questa versione.

#### <a name="hdfs"></a>HDFS

- Azure Data Studio restituisce un errore quando si cerca di creare una nuova cartella in HDFS. Per abilitare questa funzionalità, installare la build Insider di Azure Data Studio:
  
   - [Programma di installazione utenti Windows - **Build Insider**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Programma di installazione di sistema Windows - **Build Insider**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [File ZIP Windows - **Build Insider**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [File ZIP macOS - **Build Insider**](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [File TAR.GZ Linux - **Build Insider**](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, potrebbe venire visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file con dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche della configurazione in HDFS che comportano modifiche di hdfs-site.xml non sono supportate.

#### <a name="deployment"></a>Distribuzione

- Le procedure di distribuzione precedenti per i cluster Big Data abilitati per la GPU non sono supportate nella versione CTP 3.0. È in corso la ricerca di una procedura di distribuzione alternativa. Per il momento, è stata temporaneamente annullata la pubblicazione dell'articolo "Distribuire un cluster Big Data con il supporto della GPU ed eseguire TensorFlow", per evitare confusione.

- L'aggiornamento di un cluster Big Data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster Big Data esistente (usando la versione precedente di **azdata**) prima di distribuire la versione più recente. Per altre informazioni, vedere [Eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione nel servizio Azure Kubernetes, è possibile che vengano visualizzati i due eventi di avviso seguenti della distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la corretta distribuzione del cluster Big Data nel servizio Azure Kubernetes.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Ciò potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="external-tables"></a>Tabelle esterne

- La distribuzione di cluster Big data non comporta più la creazione delle origini dati esterne **SqlDataPool** e **SqlStoragePool**. È possibile creare queste origini dati manualmente per supportare la virtualizzazione dei dati nel pool di dati e nel pool di archiviazione.

   > [!NOTE]
   > L'URI per la creazione di queste origini dati esterne è diverso per ogni versione CTP. Vedere i comandi Transact-SQL seguenti per informazioni sulla loro creazione 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, si riceve un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, potrebbe verificarsi un errore se contemporaneamente è in corso la copia del file sottostante in HDFS.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si crea una tabella esterna a Oracle che usa dati di tipo carattere, la procedura guidata di virtualizzazione di Azure Data Studio interpreta queste colonne come VARCHAR nella definizione di tabella esterna. Ciò causerà un errore nel linguaggio DDL (Data Definition Language) della tabella esterna. Modificare lo schema Oracle per usare il tipo NVARCHAR2 oppure creare manualmente istruzioni EXTERNAL TABLE e specificare NVARCHAR invece di usare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione R, Python o MLeap dall'API RESTful, si verifica il timeout della chiamata dopo 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP dei pod cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Se viene riavviato il pod master, è possibile che si verifichi un errore della sessione Spark con l'eccezione `NoRoteToHostException`. Questa situazione è causata dal mancato aggiornamento delle cache JVM con i nuovi indirizzi IP.

- Se Jupyter è già installato ed è presente un ambiente Python separato in Windows, potrebbe verificarsi un errore dei notebook Spark. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- Se in un notebook si fa clic sul comando **Aggiungi testo**, la cella di testo viene aggiunta in modalità di anteprima invece che in modalità di modifica. È possibile fare clic sull'icona di anteprima per passare alla modalità di modifica e modificare la cella.

#### <a name="security"></a>Security

- La variabile SA_PASSWORD fa parte dell'ambiente ed è individuabile (ad esempio in un file core dump). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Non si tratta di un bug ma di un passaggio di sicurezza. Per altre informazioni su come modificare SA_PASSWORD in un contenitore Linux, vedere [Cambiare la password dell'amministratore di sistema](../linux/quickstart-install-connect-docker.md#sapassword).

- I log del servizio Azure Kubernetes possono contenere la password dell'amministratore di sistema per le distribuzioni di cluster Big Data.

## <a id="ctp25"></a> CTP 2.5 (aprile)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 2.5.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Profili di distribuzione | Per le distribuzioni di cluster di Big Data, usare i [file JSON di configurazione della distribuzione](deployment-guidance.md#configfile), predefiniti o personalizzati, invece delle variabili di ambiente. |
| Distribuzioni richieste | `azdata cluster create` ora richiede di specificare le eventuali impostazioni necessarie per le distribuzioni predefinite. |
| Modifiche dei nomi di endpoint di servizio e pod | I nomi degli endpoint esterni seguenti sono stati modificati:<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-service-proxy** => **mgmtproxy-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| Miglioramenti di **azdata** | Usare **azdata** per [elencare gli endpoint esterni](deployment-guidance.md#endpoints) e controllare la versione di **azdata** con il parametro `--version`. |
| Eseguire l'installazione offline | Istruzioni per le distribuzioni offline di cluster Big Data. |
| Miglioramenti della suddivisione in livelli HDFS | Suddivisione in livelli S3, memorizzazione nella cache del montaggio e supporto OAuth per ADLS Gen2. |
| Nuovo connettore `mssql` tra Spark e SQL Server | |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni per questa versione.

#### <a name="deployment"></a>Distribuzione

- L'aggiornamento di un cluster Big Data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster Big Data esistente (usando la versione precedente di **azdata**) prima di distribuire la versione più recente. Per altre informazioni, vedere [Eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione nel servizio Azure Kubernetes, è possibile che vengano visualizzati i due eventi di avviso seguenti della distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la corretta distribuzione del cluster Big Data nel servizio Azure Kubernetes.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Ciò potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="external-tables"></a>Tabelle esterne

- La distribuzione di cluster Big data non comporta più la creazione delle origini dati esterne **SqlDataPool** e **SqlStoragePool**. È possibile creare queste origini dati manualmente per supportare la virtualizzazione dei dati nel pool di dati e nel pool di archiviazione.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, si riceve un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, potrebbe verificarsi un errore se contemporaneamente è in corso la copia del file sottostante in HDFS.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si crea una tabella esterna a Oracle che usa dati di tipo carattere, la procedura guidata di virtualizzazione di Azure Data Studio interpreta queste colonne come VARCHAR nella definizione di tabella esterna. Ciò causerà un errore nel linguaggio DDL (Data Definition Language) della tabella esterna. Modificare lo schema Oracle per usare il tipo NVARCHAR2 oppure creare manualmente istruzioni EXTERNAL TABLE e specificare NVARCHAR invece di usare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione R, Python o MLeap dall'API RESTful, si verifica il timeout della chiamata dopo 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP dei pod cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Se viene riavviato il pod master, è possibile che si verifichi un errore della sessione Spark con l'eccezione `NoRoteToHostException`. Questa situazione è causata dal mancato aggiornamento delle cache JVM con i nuovi indirizzi IP.

- Se Jupyter è già installato ed è presente un ambiente Python separato in Windows, potrebbe verificarsi un errore dei notebook Spark. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- Se in un notebook si fa clic sul comando **Aggiungi testo**, la cella di testo viene aggiunta in modalità di anteprima invece che in modalità di modifica. È possibile fare clic sull'icona di anteprima per passare alla modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, potrebbe venire visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file con dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche della configurazione in HDFS che comportano modifiche di hdfs-site.xml non sono supportate.

#### <a name="security"></a>Security

- La variabile SA_PASSWORD fa parte dell'ambiente ed è individuabile (ad esempio in un file core dump). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Non si tratta di un bug ma di un passaggio di sicurezza. Per altre informazioni su come modificare SA_PASSWORD in un contenitore Linux, vedere [Cambiare la password dell'amministratore di sistema](../linux/quickstart-install-connect-docker.md#sapassword).

- I log del servizio Azure Kubernetes possono contenere la password dell'amministratore di sistema per le distribuzioni di cluster Big Data.

## <a id="ctp24"></a> CTP 2.4 (marzo)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 2.4.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Materiale sussidiario sul supporto della GPU per l'esecuzione di Deep Learning con TensorFlow in Spark. | [Distribuire un cluster di Big Data con il supporto della GPU ed eseguire TensorFlow](spark-gpu-tensorflow.md). |
| Le origini dati **SqlDataPool** e **SqlStoragePool** non vengono più create per impostazione predefinita. | Se necessario, crearle manualmente. Vedere i [problemi noti](#externaltablesctp24). |
| Supporto di `INSERT INTO SELECT` per il pool di dati. | Per un esempio, vedere [Esercitazione: Ingest data into a SQL Server data pool with Transact-SQL](tutorial-data-pool-ingest-sql.md) (Inserire dati in un pool di dati di SQL Server con Transact-SQL). |
| Opzioni `FORCE SCALEOUTEXECUTION` e `DISABLE SCALEOUTEXECUTION`. | Forza o disabilita l'uso del pool di calcolo per le query sulle tabelle esterne. Ad esempio `SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)`. |
| Aggiornamento delle raccomandazioni sulla distribuzione del servizio Azure Kubernetes. | Quando si valutano i cluster di Big Data nel servizio Azure Kubernetes, è ora consigliabile usare un singolo nodo di dimensioni **Standard_L8s**. |
| Aggiornamento del runtime Spark a Spark 2.4. | |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni per questa versione.

#### <a name="deployment"></a>Distribuzione

- L'aggiornamento di un cluster Big Data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster Big Data esistente (usando la versione precedente di **azdata**) prima di distribuire la versione più recente. Per altre informazioni, vedere [Eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione nel servizio Azure Kubernetes, è possibile che vengano visualizzati i due eventi di avviso seguenti della distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la corretta distribuzione del cluster Big Data nel servizio Azure Kubernetes.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Ciò potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="kubeadm-deployments"></a>Distribuzioni kubeadm

Se si usa kubeadm per distribuire Kubernetes in più computer, nel portale di amministrazione dei cluster non vengono visualizzati correttamente gli endpoint necessari per la connessione al cluster Big Data. Se si verifica questo problema, usare la soluzione alternativa seguente per individuare gli indirizzi IP dell'endpoint di servizio:

- Se ci si connette dall'interno del cluster, eseguire una query su Kubernetes per l'indirizzo IP del servizio per l'endpoint a cui si vuole connettersi. Ad esempio, il comando **kubectl** seguente consente di visualizzare l'indirizzo IP dell'istanza master di SQL Server:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Se ci si connette dall'esterno del cluster, attenersi alla procedura seguente per la connessione:

   1. Ottenere l'indirizzo IP del nodo che esegue l'istanza master di SQL Server: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`.

   1. Connettersi all'istanza master di SQL Server usando questo indirizzo IP.

   1. Eseguire una query su **cluster_endpoint_table** nel database master per altri endpoint esterni.

      Se l'operazione ha esito negativo e si verifica un timeout della connessione, è possibile che il nodo sia protetto da un firewall. In questo caso, è necessario contattare l'amministratore del cluster Kubernetes e chiedere che l'IP del nodo venga esposto esternamente. Potrebbe trattarsi di qualsiasi nodo. È quindi possibile usare l'IP e la porta corrispondente per connettersi a diversi servizi in esecuzione nel cluster. L'amministratore può ad esempio trovare questo indirizzo IP eseguendo:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a name="delete-cluster-fails"></a>Errore nell'eliminazione del cluster

Quando si cerca di eliminare un cluster con **azdata**, l'operazione ha esito negativo con l'errore seguente:

```
2019-03-26 20:38:11.0614 UTC | INFO | Deleting cluster ...
Error processing command: "TypeError"
delete_namespaced_service() takes 3 positional arguments but 4 were given
Makefile:61: recipe for target 'delete-cluster' failed
make[2]: *** [delete-cluster] Error 1
Makefile:223: recipe for target 'deploy-clean' failed
make[1]: *** [deploy-clean] Error 2
Makefile:203: recipe for target 'deploy-clean' failed
make: *** [deploy-clean] Error 2
```

Un nuovo client Python Kubernetes (versione 9.0.0) ha modificato l'API di eliminazione dello spazio dei nomi, che attualmente provoca l'interruzione di **azdata**. Ciò si verifica solo se è installato un client Python Kubernetes più recente. È possibile risolvere questo problema eliminando direttamente il cluster con **kubectl** (`kubectl delete ns <ClusterName>`) oppure è possibile installare la versione precedente usando `sudo pip install kubernetes==8.0.1`.

#### <a id="externaltablesctp24"></a> Tabelle esterne

- La distribuzione di cluster Big data non comporta più la creazione delle origini dati esterne **SqlDataPool** e **SqlStoragePool**. È possibile creare queste origini dati manualmente per supportare la virtualizzazione dei dati nel pool di dati e nel pool di archiviazione.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, si riceve un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, potrebbe verificarsi un errore se contemporaneamente è in corso la copia del file sottostante in HDFS.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si crea una tabella esterna a Oracle che usa dati di tipo carattere, la procedura guidata di virtualizzazione di Azure Data Studio interpreta queste colonne come VARCHAR nella definizione di tabella esterna. Ciò causerà un errore nel linguaggio DDL (Data Definition Language) della tabella esterna. Modificare lo schema Oracle per usare il tipo NVARCHAR2 oppure creare manualmente istruzioni EXTERNAL TABLE e specificare NVARCHAR invece di usare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione R, Python o MLeap dall'API RESTful, si verifica il timeout della chiamata dopo 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP dei pod cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Se viene riavviato il pod master, è possibile che si verifichi un errore della sessione Spark con l'eccezione `NoRoteToHostException`. Questa situazione è causata dal mancato aggiornamento delle cache JVM con i nuovi indirizzi IP.

- Se Jupyter è già installato ed è presente un ambiente Python separato in Windows, potrebbe verificarsi un errore dei notebook Spark. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- Se in un notebook si fa clic sul comando **Aggiungi testo**, la cella di testo viene aggiunta in modalità di anteprima invece che in modalità di modifica. È possibile fare clic sull'icona di anteprima per passare alla modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, potrebbe venire visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file con dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche della configurazione in HDFS che comportano modifiche di hdfs-site.xml non sono supportate.

#### <a name="security"></a>Security

- La variabile SA_PASSWORD fa parte dell'ambiente ed è individuabile (ad esempio in un file core dump). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Non si tratta di un bug ma di un passaggio di sicurezza. Per altre informazioni su come modificare SA_PASSWORD in un contenitore Linux, vedere [Cambiare la password dell'amministratore di sistema](../linux/quickstart-install-connect-docker.md#sapassword).

- I log del servizio Azure Kubernetes possono contenere la password dell'amministratore di sistema per le distribuzioni di cluster Big Data.

## <a id="ctp23"></a> CTP 2.3 (febbraio)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 2.3.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
| :---------- | :------ |
| Inviare processi Spark nei cluster di Big Data in IntelliJ. | [Inviare processi [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Spark in IntelliJ](spark-submit-job-intellij-tool-plugin.md) |
| Interfaccia della riga di comando comune per la distribuzione di applicazioni e la gestione di cluster. | [Come distribuire un'app in[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-create-apps.md) |
| Estensione di VS Code per distribuire applicazioni in un cluster di Big Data. | [Come usare VS Code per distribuire le applicazioni in[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](app-deployment-extension.md) |
| Modifiche apportate all'utilizzo dei comandi dello strumento **azdata**. | Per informazioni più dettagliate, vedere i [problemi noti di azdata](#azdatactp23). |
| Usare Sparklyr in un cluster Big Data | [Usare Sparklyr in cluster di Big Data di SQL Server 2019](sparklyr-from-RStudio.md) |
| Montare un'archiviazione esterna compatibile con Hadoop Distributed File System (HDFS) in un cluster Big Data con la **suddivisione in livelli HDFS**. | Vedere [Suddivisione in livelli HDFS](hdfs-tiering.md). |
| Nuova esperienza di connessione unificata per l'istanza master di SQL Server e il gateway HDFS/Spark. | Vedere [Istanza master di SQL Server e gateway HDFS/Spark](connect-to-big-data-cluster.md). |
| Se si elimina in cluster con **azdata cluster delete**, vengono ora eliminati solo gli oggetti dello spazio dei nomi che fanno parte del cluster Big Data. | Lo spazio dei nomi non viene eliminato. Nelle versioni precedenti, invece, questo comando elimina l'intero spazio dei nomi. |
| I nomi degli endpoint di _sicurezza_ sono stati cambiati e consolidati. | **service-security-lb** e **service-security-nodeport** sono stati consolidati nell'endpoint **endpoint-security**. |
| I nomi degli endpoint _proxy_ sono stati cambiati e consolidati. | **service-proxy-lb** e **service-proxy-nodeport** sono stati consolidati nell'endpoint **endpoint-service-proxy**. |
| I nomi degli endpoint di _controller_ sono stati cambiati e consolidati. | **service-mssql-controller-lb** e **service-mssql-controller-nodeport** sono stati consolidati nell'endpoint **endpoint-controller**. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni per questa versione.

#### <a name="deployment"></a>Distribuzione

- L'aggiornamento di un cluster Big Data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster Big Data esistente (usando la versione precedente di **azdata**) prima di distribuire la versione più recente. Per altre informazioni, vedere [Eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- La variabile di ambiente **ACCEPT_EULA** deve essere "yes" o "Yes" per accettare il contratto di licenza. Nelle versioni precedenti era possibile usare "y" e "Y", ma queste opzioni non sono più accettate e provocano un errore della distribuzione.

- Le variabili di ambiente **CLUSTER_PLATFORM** non hanno un valore predefinito come nelle versioni precedenti.

- Dopo la distribuzione nel servizio Azure Kubernetes, è possibile che vengano visualizzati i due eventi di avviso seguenti della distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la corretta distribuzione del cluster Big Data nel servizio Azure Kubernetes.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Ciò potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="kubeadm-deployments"></a>Distribuzioni kubeadm

Se si usa kubeadm per distribuire Kubernetes in più computer, nel portale di amministrazione dei cluster non vengono visualizzati correttamente gli endpoint necessari per la connessione al cluster Big Data. Se si verifica questo problema, usare la soluzione alternativa seguente per individuare gli indirizzi IP dell'endpoint di servizio:

- Se ci si connette dall'interno del cluster, eseguire una query su Kubernetes per l'indirizzo IP del servizio per l'endpoint a cui si vuole connettersi. Ad esempio, il comando **kubectl** seguente consente di visualizzare l'indirizzo IP dell'istanza master di SQL Server:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Se ci si connette dall'esterno del cluster, attenersi alla procedura seguente per la connessione:

   1. Ottenere l'indirizzo IP del nodo che esegue l'istanza master di SQL Server: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`.

   1. Connettersi all'istanza master di SQL Server usando questo indirizzo IP.

   1. Eseguire una query su **cluster_endpoint_table** nel database master per altri endpoint esterni.

      Se l'operazione ha esito negativo e si verifica un timeout della connessione, è possibile che il nodo sia protetto da un firewall. In questo caso, è necessario contattare l'amministratore del cluster Kubernetes e chiedere che l'IP del nodo venga esposto esternamente. Potrebbe trattarsi di qualsiasi nodo. È quindi possibile usare l'IP e la porta corrispondente per connettersi a diversi servizi in esecuzione nel cluster. L'amministratore può ad esempio trovare questo indirizzo IP eseguendo:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="azdatactp23"></a> azdata

- Lo strumento **azdata** è stato modificato passando da un ordinamento verbo-nome nel comando a un ordinamento nome-verbo. Ad esempio, `azdata create cluster` è ora `azdata cluster create`.

- Il parametro `--name` è ora necessario quando si crea un cluster con `azdata cluster create`.

   ```bash
   azdata cluster create --name <cluster_name>
   ```

- Per informazioni importanti sull'aggiornamento alla versione più recente dei cluster Big Data e di **azdata**, vedere [Eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

#### <a name="external-tables"></a>Tabelle esterne

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, si riceve un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, potrebbe verificarsi un errore se contemporaneamente è in corso la copia del file sottostante in HDFS.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si crea una tabella esterna a Oracle che usa dati di tipo carattere, la procedura guidata di virtualizzazione di Azure Data Studio interpreta queste colonne come VARCHAR nella definizione di tabella esterna. Ciò causerà un errore nel linguaggio DDL (Data Definition Language) della tabella esterna. Modificare lo schema Oracle per usare il tipo NVARCHAR2 oppure creare manualmente istruzioni EXTERNAL TABLE e specificare NVARCHAR invece di usare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione R, Python o MLeap dall'API RESTful, si verifica il timeout della chiamata dopo 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP dei pod cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Se viene riavviato il pod master, è possibile che si verifichi un errore della sessione Spark con l'eccezione `NoRoteToHostException`. Questa situazione è causata dal mancato aggiornamento delle cache JVM con i nuovi indirizzi IP.

- Se Jupyter è già installato ed è presente un ambiente Python separato in Windows, potrebbe verificarsi un errore dei notebook Spark. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- Se in un notebook si fa clic sul comando **Aggiungi testo**, la cella di testo viene aggiunta in modalità di anteprima invece che in modalità di modifica. È possibile fare clic sull'icona di anteprima per passare alla modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, potrebbe venire visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file con dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche della configurazione in HDFS che comportano modifiche di hdfs-site.xml non sono supportate.

#### <a name="security"></a>Security

- La variabile SA_PASSWORD fa parte dell'ambiente ed è individuabile (ad esempio in un file core dump). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Non si tratta di un bug ma di un passaggio di sicurezza. Per altre informazioni su come modificare SA_PASSWORD in un contenitore Linux, vedere [Cambiare la password dell'amministratore di sistema](../linux/quickstart-install-connect-docker.md#sapassword).

- I log del servizio Azure Kubernetes possono contenere la password dell'amministratore di sistema per le distribuzioni di cluster Big Data.

## <a id="ctp22"></a> CTP 2.2 (dicembre 2018)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 2.2.

### <a name="new-features"></a>Nuove funzionalità

- Accesso al portale di amministrazione dei cluster con `/portal` (**https://\<ip-address\>:30777/portal**).
- Nome del servizio pool master cambiato da `service-master-pool-lb` e `service-master-pool-nodeport` a `endpoint-master-pool`.
- Nuova versione di **azdata** e immagini aggiornate.
- Correzioni di bug e miglioramenti di vario tipo.

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni per questa versione.

#### <a name="deployment"></a>Distribuzione

- L'aggiornamento di un cluster Big Data da una versione precedente non è supportato. È necessario eseguire il backup e l'eliminazione di qualsiasi cluster Big Data esistente prima di distribuire la versione più recente. Per altre informazioni, vedere [Eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione nel servizio Azure Kubernetes, è possibile che vengano visualizzati i due eventi di avviso seguenti della distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la corretta distribuzione del cluster Big Data nel servizio Azure Kubernetes.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Ciò potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="cluster-administration-portal"></a>Portale di amministrazione cluster

Il portale di amministrazione dei cluster non visualizza l'endpoint per l'istanza master di SQL Server. Per trovare l'indirizzo IP e la porta dell'istanza master, usare il comando **kubectl** seguente:

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
```

#### <a name="external-tables"></a>Tabelle esterne

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, si riceve un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, potrebbe verificarsi un errore se contemporaneamente è in corso la copia del file sottostante in HDFS.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP dei pod cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Se viene riavviato il pod master, è possibile che si verifichi un errore della sessione Spark con l'eccezione `NoRoteToHostException`. Questa situazione è causata dal mancato aggiornamento delle cache JVM con i nuovi indirizzi IP.

- Se Jupyter è già installato ed è presente un ambiente Python separato in Windows, potrebbe verificarsi un errore dei notebook Spark. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- Se in un notebook si fa clic sul comando **Aggiungi testo**, la cella di testo viene aggiunta in modalità di anteprima invece che in modalità di modifica. È possibile fare clic sull'icona di anteprima per passare alla modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, potrebbe venire visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file con dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche della configurazione in HDFS che comportano modifiche di hdfs-site.xml non sono supportate.

#### <a name="security"></a>Security

- La variabile SA_PASSWORD fa parte dell'ambiente ed è individuabile (ad esempio in un file core dump). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Non si tratta di un bug ma di un passaggio di sicurezza. Per altre informazioni su come modificare SA_PASSWORD in un contenitore Linux, vedere [Cambiare la password dell'amministratore di sistema](../linux/quickstart-install-connect-docker.md#sapassword).

- I log del servizio Azure Kubernetes possono contenere la password dell'amministratore di sistema per le distribuzioni di cluster Big Data.

## <a id="ctp21"></a> CTP 2.1 (novembre 2018)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 2.1.

### <a name="new-features"></a>Nuove funzionalità

- [Distribuire app Python e R](big-data-cluster-create-apps.md) in un cluster Big Data.
- Nuova versione di **azdata** e immagini aggiornate. 
- Correzioni di bug e miglioramenti di vario tipo.

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti forniscono problemi noti per [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] nella versione CTP 2,1.

#### <a name="deployment"></a>Distribuzione

- L'aggiornamento di un cluster Big Data da una versione precedente non è supportato. È necessario eseguire il backup e l'eliminazione di qualsiasi cluster Big Data esistente prima di distribuire la versione più recente. Per altre informazioni, vedere [Eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione nel servizio Azure Kubernetes, è possibile che vengano visualizzati i due eventi di avviso seguenti della distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la corretta distribuzione del cluster Big Data nel servizio Azure Kubernetes.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Ciò potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="admin-portal"></a>Portale di amministrazione

- Quando si [crea un'app usando il comando msqlctl-ctp](big-data-cluster-create-apps.md) e la si distribuisce in un cluster Big Data di SQL Server, il portale di amministrazione dei cluster mostra i pod in cui l'applicazione è stata distribuita come "sconosciuti" nella sezione relativa al controller della parte riservata all'amministratore.

#### <a name="external-tables"></a>Tabelle esterne

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, si riceve un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, potrebbe verificarsi un errore se contemporaneamente è in corso la copia del file sottostante in HDFS.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP dei pod cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Se viene riavviato il pod master, è possibile che si verifichi un errore della sessione Spark con l'eccezione `NoRoteToHostException`. Questa situazione è causata dal mancato aggiornamento delle cache JVM con i nuovi indirizzi IP.

- Se Jupyter è già installato ed è presente un ambiente Python separato in Windows, potrebbe verificarsi un errore dei notebook Spark. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- Se in un notebook si fa clic sul comando **Aggiungi testo**, la cella di testo viene aggiunta in modalità di anteprima invece che in modalità di modifica. È possibile fare clic sull'icona di anteprima per passare alla modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, potrebbe venire visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file con dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche della configurazione in HDFS che comportano modifiche di hdfs-site.xml non sono supportate.

#### <a name="security"></a>Security

- La variabile SA_PASSWORD fa parte dell'ambiente ed è individuabile (ad esempio in un file core dump). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Non si tratta di un bug ma di un passaggio di sicurezza. Per altre informazioni su come modificare SA_PASSWORD in un contenitore Linux, vedere [Cambiare la password dell'amministratore di sistema](../linux/quickstart-install-connect-docker.md#sapassword).

- I log del servizio Azure Kubernetes possono contenere la password dell'amministratore di sistema per le distribuzioni di cluster Big Data.

## <a id="ctp20"></a> CTP 2.0 (ottobre 2018)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 2.0.

### <a name="new-features"></a>Nuove funzionalità

- Esperienza di distribuzione semplice con lo strumento di gestione azdata
- Esperienza di notebook di tipo nativo in Azure Data Studio
- Query su file HDFS tramite l'istanza di archiviazione di SQL Server
- Virtualizzazione dei dati tramite master in SQL Server, Oracle, MongoDB e HDFS
- Procedura guidata di virtualizzazione dei dati per SQL Server e Oracle in Azure Data Studio
- Servizi ML nell'istanza master
- Portale di amministrazione dei cluster che è possibile usare per il monitoraggio e la risoluzione dei problemi
- Invio di processi Spark in Azure Data Studio 
- Interfaccia utente Spark nel portale di amministrazione dei cluster
- Montaggio dei volumi nelle classi di archiviazione
- Query sui pool di dati dall'istanza master
- Visualizzazione dei piani per le query distribuite in SSMS
- Pacchetto pip per lo strumento di gestione azdata
- Motore di distribuzione predefinito tramite il servizio controller

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti forniscono problemi noti per [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] nella versione CTP 2,0.

#### <a name="deployment"></a>Distribuzione

- Se si usa il servizio Azure Kubernetes (AKS), la versione consigliata di Kubernetes è 1.10.*, che non supporta il ridimensionamento dei dischi. Assicurarsi di ridimensionare lo spazio di archiviazione di conseguenza in fase di distribuzione. Per altre informazioni su come modificare le dimensioni dello spazio di archiviazione, vedere l'articolo [Salvataggio permanente dei dati](concept-data-persistence.md). Per le distribuzioni di Kubernetes nelle macchine virtuali, la versione consigliata è 1.11.

- Dopo la distribuzione nel servizio Azure Kubernetes, è possibile che vengano visualizzati i due eventi di avviso seguenti della distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la corretta distribuzione del cluster Big Data nel servizio Azure Kubernetes.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Ciò potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="external-tables"></a>Tabelle esterne

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, si riceve un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, potrebbe verificarsi un errore se contemporaneamente è in corso la copia del file sottostante in HDFS.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP dei pod cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Se viene riavviato il pod master, è possibile che si verifichi un errore della sessione Spark con l'eccezione `NoRoteToHostException`. Questa situazione è causata dal mancato aggiornamento delle cache JVM con i nuovi indirizzi IP.

- Se Jupyter è già installato ed è presente un ambiente Python separato in Windows, potrebbe verificarsi un errore dei notebook Spark. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- Se in un notebook si fa clic sul comando **Aggiungi testo**, la cella di testo viene aggiunta in modalità di anteprima invece che in modalità di modifica. È possibile fare clic sull'icona di anteprima per passare alla modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, potrebbe venire visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file con dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche della configurazione in HDFS che comportano modifiche di hdfs-site.xml non sono supportate.

#### <a name="security"></a>Security

- La variabile SA_PASSWORD fa parte dell'ambiente ed è individuabile (ad esempio in un file core dump). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Non si tratta di un bug ma di un passaggio di sicurezza. Per altre informazioni su come modificare SA_PASSWORD in un contenitore Linux, vedere [Cambiare la password dell'amministratore di sistema](../linux/quickstart-install-connect-docker.md#sapassword).

- I log del servizio Azure Kubernetes possono contenere la password dell'amministratore di sistema per le distribuzioni di cluster Big Data.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere [che cosa [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]sono?](big-data-cluster-overview.md).
