---
title: Note sulla versione
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive gli aggiornamenti più recenti e i problemi noti per i cluster Big Data di SQL Server 2019 (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c0dd96d4a3227fda76921764429b4566e3e5dd28
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419309"
---
# <a name="release-notes-for-big-data-clusters-on-sql-server"></a>Note sulla versione per i cluster di Big Data in SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo elenca gli aggiornamenti e conosce i problemi per le versioni più recenti di SQL Server Big Data cluster.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp32"></a>CTP 3,2 (luglio)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 3,2.

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Anteprima pubblica |Prima della versione CTP 3,2, SQL Server cluster Big Data era disponibile per i primi utenti registrati. Questa versione consente a chiunque di sperimentare le funzionalità di SQL Server cluster di Big Data. <br/><br/> Vedere [Introduzione ai cluster SQL Server Big Data](deploy-get-started.md).|
|`azdata` |CTP 3,2 introduce `azdata` un'utilità da riga di comando scritta in Python che consente agli amministratori del cluster di avviare e gestire il cluster Big data tramite le API REST. `azdata`sostituisce `mssqlctl`. Vedere [install `azdata` ](deploy-install-azdata.md). |
|PolyBase |I nomi delle colonne della tabella esterna vengono ora usati per eseguire query su origini dati SQL Server, Oracle, Teradata, MongoDB e ODBC. |
|Aggiornamento a livelli HDFS |Introduzione della funzionalità di aggiornamento per la suddivisione in livelli di HDFS in modo che sia possibile aggiornare un montaggio esistente per l'ultimo snapshot dei dati remoti. Vedere la suddivisione in [livelli HDFS](hdfs-tiering.md) |
|Risoluzione dei problemi basata su notebook |CTP 3,2 introduce notebook Jupyter per semplificare la [distribuzione](deploy-notebooks.md) e l' [individuazione, la diagnosi e la risoluzione dei problemi](manage-notebooks.md) per i componenti in un cluster SQL Server Big Data. |
| &nbsp; | &nbsp; |

## <a id="ctp31"></a>CTP 3,1 (giugno)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 3,1.

|Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
|Anteprima pubblica |Prima della versione CTP 3,2, SQL Server cluster Big Data era disponibile per i primi utenti registrati. Questa versione consente a chiunque di sperimentare le funzionalità di SQL Server cluster di Big Data. <br/><br/> Vedere [Introduzione ai cluster SQL Server Big Data](deploy-get-started.md).|
|Risoluzione dei problemi basata su notebook.|CTP 3,2 introduce notebook Jupyter per semplificare la [distribuzione](deploy-notebooks.md)e l' [individuazione, la diagnosi e la risoluzione dei problemi](manage-notebooks.md) per i componenti in un cluster SQL Server Big Data. |
|`azdata` |CTP 3,2 introduce `azdata` un'utilità da riga di comando scritta in Python che consente agli amministratori del cluster di avviare e gestire il cluster Big data tramite le API REST. `azdata`sostituisce `mssqlctl`. Vedere [install `azdata` ](deploy-install-azdata.md). |
|Aggiornamento a livelli HDFS |Introduzione della funzionalità di aggiornamento per la suddivisione in livelli di HDFS in modo che sia possibile aggiornare un montaggio esistente per l'ultimo snapshot dei dati remoti. Vedere la suddivisione in [livelli HDFS](hdfs-tiering.md) |
| &nbsp; | &nbsp; |

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Modifiche dei comandi `mssqlctl` | I comandi `mssqlctl cluster` sono stati rinominati `mssqlctl bdc`. Per altre informazioni, vedere le [`mssqlctl`informazioni di riferimento](reference-azdata.md). |
| Nuovi `mssqlctl` comandi di stato e rimozione del portale di amministrazione del cluster. | Il portale di amministrazione del cluster è stato rimosso in questa versione. Sono stati aggiunti nuovi comandi di stato `mssqlctl` a che integrano i comandi di monitoraggio esistenti. |
| Pool di calcolo di Spark | È possibile creare nodi aggiuntivi per incrementare la potenza di calcolo di Spark senza dover aumentare le prestazioni dell'archiviazione. È inoltre possibile avviare i nodi del pool di archiviazione che non vengono usati per Spark. Spark e l'archiviazione sono separati. Per altre informazioni, vedere [Configurare l'archiviazione senza Spark](deployment-custom-configuration.md#sparkstorage). |
| Connettore Spark MSSQL | Supporto per la lettura/scrittura nelle tabelle esterne del pool di dati. Nelle versioni precedenti era supportata solo la lettura/scrittura nelle tabelle dell'istanza MASTER. Per altre informazioni, vedere [Come leggere e scrivere in SQL Server da Spark usando il connettore Spark MSSQL](spark-mssql-connector.md). |
| Machine Learning tramite MLeap | [Eseguire il training di un modello di Machine Learning MLeap in Spark e assegnargli un punteggio in SQL Server tramite l'estensione per il linguaggio Java](spark-create-machine-learning-model.md). |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni di questa versione.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, è possibile che venga visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file di dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche di configurazione apportate a HDFS che coinvolgono le modifiche di HDFS-site. XML non sono supportate.

#### <a name="deployment"></a>Distribuzione

- L'aggiornamento di un cluster di dati Big Data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster di Big Data esistente (usando la versione precedente di **azdata**) prima di distribuire la versione più recente. Per altre informazioni, vedere [eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione in AKS, è possibile che vengano visualizzati i due eventi di avviso seguenti dalla distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la distribuzione corretta del cluster Big Data su AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Questo potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="external-tables"></a>Tabelle esterne

- La distribuzione di cluster di Big data non crea più le origini dati esterne **SqlDataPool** e **SqlStoragePool** . È possibile creare queste origini dati manualmente per supportare la virtualizzazione dei dati nel pool di dati e nel pool di archiviazione.

   > [!NOTE]
   > L'URI per la creazione di queste origini dati esterne è diverso tra CTP. Per informazioni su come crearli, vedere i comandi Transact-SQL seguenti. 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, viene ricevuto un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, è possibile che venga ricevuto un errore se il file sottostante viene copiato in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si crea una tabella esterna in Oracle che usa tipi di dati di tipo carattere, la Azure Data Studio Virtualization Wizard interpreta tali colonne come VARCHAR nella definizione della tabella esterna. Ciò causerà un errore nel DDL della tabella esterna. Modificare lo schema Oracle per utilizzare il tipo NVARCHAR2 o creare istruzioni della tabella esterna manualmente e specificare NVARCHAR anziché utilizzare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione R, Python o MLeap dall'API RESTful, il timeout della chiamata si verifica in 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP POD cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Nello scenario in cui il Master-Pod viene riavviato, è possibile che la sessione `NoRoteToHostException`di Spark abbia esito negativo con. Questa situazione è causata da cache JVM che non vengono aggiornate con nuovi indirizzi IP.

- Se Jupyter è già installato e un Python separato in Windows, i notebook di Spark potrebbero avere esito negativo. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- In un notebook, se si fa clic sul comando **Aggiungi testo** , la cella di testo viene aggiunta in modalità di anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per impostare la modalità di modifica e modificare la cella.

#### <a name="security"></a>Sicurezza

- SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug ma un passaggio di sicurezza. Per ulteriori informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [Change the sa password](../linux/quickstart-install-connect-docker.md#sapassword).

- I log AKS possono contenere password SA per le distribuzioni di Big Data cluster.

#### <a name="kibana-logs-dashboards"></a>Kibana registra i dashboard

- Tra Aris CTP 3,0 e 3,1, la versione di Kibana è stata aggiornata da 6.3.1 a 7.0.1.  Questo ha reso il browser Edge incompatibile con Kibana. Quando si carica la versione corrente dei dashboard Kibana in Edge, gli utenti visualizzeranno una pagina vuota. Vedere [qui]( https://www.elastic.co/support/matrix#matrix_browse) per i browser supportati per Kibana.RS 


## <a id="ctp30"></a>CTP 3,0 (maggio)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 3,0.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Aggiornamenti di **mssqlctl** | Numerosi [aggiornamenti di comandi e parametri](reference-azdata.md) **mssqlctl** tra cui un aggiornamento al comando **mssqlctl login**, che ora ha come destinazione il nome utente e l'endpoint del controller. |
| Miglioramenti all'archiviazione | Supporto per configurazioni di archiviazione diverse per log e dati. È stato anche ridotto il numero di attestazioni di volume permanente per un cluster di Big Data. |
| Più istanze del pool di calcolo | Supporto per più istanze del pool di calcolo. |
| Nuove funzionalità e comportamento del pool | Il pool di calcolo viene ora usato per impostazione predefinita per le operazioni del pool di dati e del pool di archiviazione solo nella distribuzione **ROUND_ROBIN**. Il pool di dati ora può usare un nuovo tipo di distribuzione **REPLICATED**, il che significa che gli stessi dati sono presenti in tutte le istanze del pool di dati. |
| Miglioramenti alle tabelle esterne | Le tabelle esterne del tipo origine dati HADOOP ora supportano la lettura di righe con dimensioni fino a 1 MB. Le tabelle esterne (ODBC, pool di archiviazione, pool di dati) ora supportano righe larghe quanto una tabella di SQL Server. |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni di questa versione.

#### <a name="hdfs"></a>HDFS

- Azure Data Studio restituisce un errore quando si tenta di creare una nuova cartella in HDFS. Per abilitare questa funzionalità, installare la build Insider di Azure Data Studio:
  
   - [Programma di installazione utente Windows- **compilazione** Insider](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Programma di installazione di sistema di Windows- **compilazione** Insider](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [**Compilazione** di Windows zip-Insider](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [**compilazione** di MacOS zip-Insider](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [TAR Linux. GZ- **compilazione** Insider](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, è possibile che venga visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file di dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche di configurazione apportate a HDFS che coinvolgono le modifiche di HDFS-site. XML non sono supportate.

#### <a name="deployment"></a>Distribuzione

- Le procedure di distribuzione precedenti per i cluster di Big Data abilitati per GPU non sono supportate nella versione CTP 3,0. È in corso l'analisi di una procedura di distribuzione alternativa. Per il momento, l'articolo "distribuire un cluster Big Data con supporto GPU ed eseguire TensorFlow" è stato temporaneamente non pubblicato per evitare confusione.

- L'aggiornamento di un cluster di dati Big Data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster di Big Data esistente (usando la versione precedente di **azdata**) prima di distribuire la versione più recente. Per altre informazioni, vedere [eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione in AKS, è possibile che vengano visualizzati i due eventi di avviso seguenti dalla distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la distribuzione corretta del cluster Big Data su AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Questo potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="external-tables"></a>Tabelle esterne

- La distribuzione di cluster di Big data non crea più le origini dati esterne **SqlDataPool** e **SqlStoragePool** . È possibile creare queste origini dati manualmente per supportare la virtualizzazione dei dati nel pool di dati e nel pool di archiviazione.

   > [!NOTE]
   > L'URI per la creazione di queste origini dati esterne è diverso tra CTP. Per informazioni su come crearli, vedere i comandi Transact-SQL seguenti. 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, viene ricevuto un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, è possibile che venga ricevuto un errore se il file sottostante viene copiato in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si crea una tabella esterna in Oracle che usa tipi di dati di tipo carattere, la Azure Data Studio Virtualization Wizard interpreta tali colonne come VARCHAR nella definizione della tabella esterna. Ciò causerà un errore nel DDL della tabella esterna. Modificare lo schema Oracle per utilizzare il tipo NVARCHAR2 o creare istruzioni della tabella esterna manualmente e specificare NVARCHAR anziché utilizzare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione R, Python o MLeap dall'API RESTful, il timeout della chiamata si verifica in 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP POD cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Nello scenario in cui il Master-Pod viene riavviato, è possibile che la sessione `NoRoteToHostException`di Spark abbia esito negativo con. Questa situazione è causata da cache JVM che non vengono aggiornate con nuovi indirizzi IP.

- Se Jupyter è già installato e un Python separato in Windows, i notebook di Spark potrebbero avere esito negativo. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- In un notebook, se si fa clic sul comando **Aggiungi testo** , la cella di testo viene aggiunta in modalità di anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per impostare la modalità di modifica e modificare la cella.

#### <a name="security"></a>Sicurezza

- SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug ma un passaggio di sicurezza. Per ulteriori informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [Change the sa password](../linux/quickstart-install-connect-docker.md#sapassword).

- I log AKS possono contenere password SA per le distribuzioni di Big Data cluster.

## <a id="ctp25"></a>CTP 2,5 (aprile)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 2,5.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Profili di distribuzione | Per le distribuzioni di cluster di Big Data, usare i [file JSON di configurazione della distribuzione](deployment-guidance.md#configfile), predefiniti o personalizzati, invece delle variabili di ambiente. |
| Distribuzioni richieste | `azdata cluster create` ora richiede di specificare le eventuali impostazioni necessarie per le distribuzioni predefinite. |
| Modifiche dei nomi di endpoint di servizio e pod | I nomi degli endpoint esterni seguenti sono stati modificati:<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-service-proxy** => **mgmtproxy-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| miglioramenti di **azdata** | Usare **azdata** per [elencare gli endpoint esterni](deployment-guidance.md#endpoints) e controllare la versione di **azdata** con `--version` il parametro. |
| Eseguire l'installazione offline | Linee guida per le distribuzioni di cluster Big Data offline. |
| Miglioramenti della suddivisione in livelli HDFS | Suddivisione in livelli S3, Mount Caching e supporto OAuth per ADLS Gen2. |
| Nuovo `mssql` connettore Spark-SQL Server | |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni di questa versione.

#### <a name="deployment"></a>Distribuzione

- L'aggiornamento di un cluster di dati Big Data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster di Big Data esistente (usando la versione precedente di **azdata**) prima di distribuire la versione più recente. Per altre informazioni, vedere [eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione in AKS, è possibile che vengano visualizzati i due eventi di avviso seguenti dalla distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la distribuzione corretta del cluster Big Data su AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Questo potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="external-tables"></a>Tabelle esterne

- La distribuzione di cluster di Big data non crea più le origini dati esterne **SqlDataPool** e **SqlStoragePool** . È possibile creare queste origini dati manualmente per supportare la virtualizzazione dei dati nel pool di dati e nel pool di archiviazione.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, viene ricevuto un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, è possibile che venga ricevuto un errore se il file sottostante viene copiato in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si crea una tabella esterna in Oracle che usa tipi di dati di tipo carattere, la Azure Data Studio Virtualization Wizard interpreta tali colonne come VARCHAR nella definizione della tabella esterna. Ciò causerà un errore nel DDL della tabella esterna. Modificare lo schema Oracle per utilizzare il tipo NVARCHAR2 o creare istruzioni della tabella esterna manualmente e specificare NVARCHAR anziché utilizzare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione R, Python o MLeap dall'API RESTful, il timeout della chiamata si verifica in 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP POD cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Nello scenario in cui il Master-Pod viene riavviato, è possibile che la sessione `NoRoteToHostException`di Spark abbia esito negativo con. Questa situazione è causata da cache JVM che non vengono aggiornate con nuovi indirizzi IP.

- Se Jupyter è già installato e un Python separato in Windows, i notebook di Spark potrebbero avere esito negativo. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- In un notebook, se si fa clic sul comando **Aggiungi testo** , la cella di testo viene aggiunta in modalità di anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per impostare la modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, è possibile che venga visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file di dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche di configurazione apportate a HDFS che coinvolgono le modifiche di HDFS-site. XML non sono supportate.

#### <a name="security"></a>Sicurezza

- SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug ma un passaggio di sicurezza. Per ulteriori informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [Change the sa password](../linux/quickstart-install-connect-docker.md#sapassword).

- I log AKS possono contenere password SA per le distribuzioni di Big Data cluster.

## <a id="ctp24"></a>CTP 2,4 (marzo)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 2,4.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Materiale sussidiario sul supporto della GPU per l'esecuzione di Deep Learning con TensorFlow in Spark. | [Distribuire un cluster di Big Data con il supporto della GPU ed eseguire TensorFlow](spark-gpu-tensorflow.md). |
| Le origini dati **SqlDataPool** e **SqlStoragePool** non vengono più create per impostazione predefinita. | Se necessario, crearle manualmente. Vedere i [problemi noti](#externaltablesctp24). |
| Supporto di `INSERT INTO SELECT` per il pool di dati. | Per un esempio, vedere [Esercitazione: Ingest data into a SQL Server data pool with Transact-SQL](tutorial-data-pool-ingest-sql.md) (Inserire dati in un pool di dati di SQL Server con Transact-SQL). |
| Opzioni `FORCE SCALEOUTEXECUTION` e `DISABLE SCALEOUTEXECUTION`. | Forza o Disabilita l'utilizzo del pool di calcolo per le query su tabelle esterne. Ad esempio `SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)`. |
| Aggiornamento delle raccomandazioni sulla distribuzione del servizio Azure Kubernetes. | Quando si valutano i cluster di Big Data nel servizio Azure Kubernetes, è ora consigliabile usare un singolo nodo di dimensioni **Standard_L8s**. |
| Aggiornamento del runtime Spark a Spark 2.4. | |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni di questa versione.

#### <a name="deployment"></a>Distribuzione

- L'aggiornamento di un cluster di dati Big Data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster di Big Data esistente (usando la versione precedente di **azdata**) prima di distribuire la versione più recente. Per altre informazioni, vedere [eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione in AKS, è possibile che vengano visualizzati i due eventi di avviso seguenti dalla distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la distribuzione corretta del cluster Big Data su AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Questo potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="kubeadm-deployments"></a>distribuzioni kubeadm

Se si utilizza kubeadm per distribuire Kubernetes in più computer, nel portale di amministrazione del cluster non vengono visualizzati correttamente gli endpoint necessari per la connessione al cluster Big Data. Se si verifica questo problema, utilizzare le seguenti operazioni per individuare gli indirizzi IP dell'endpoint di servizio:

- Se ci si connette dall'interno del cluster, eseguire una query su Kubernetes per l'indirizzo IP del servizio per l'endpoint a cui si vuole connettersi. Ad esempio, il comando **kubectl** seguente consente di visualizzare l'indirizzo IP dell'istanza di SQL Server Master:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Se ci si connette dall'esterno del cluster, attenersi alla procedura seguente per connettersi:

   1. Ottenere l'indirizzo IP del nodo che esegue l'istanza di SQL Server master `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`:.

   1. Connettersi a SQL Server istanza master usando questo indirizzo IP.

   1. Eseguire una query su **cluster_endpoint_table** nel database master per altri endpoint esterni.

      Se l'operazione ha esito negativo con un timeout della connessione, è possibile che il rispettivo nodo sia firewall. In questo caso, è necessario contattare l'amministratore del cluster Kubernetes e richiedere l'IP del nodo esposto esternamente. Potrebbe trattarsi di qualsiasi nodo. È quindi possibile usare tale indirizzo IP e la porta corrispondente per connettersi a vari servizi in esecuzione nel cluster. Ad esempio, l'amministratore può trovare questo indirizzo IP eseguendo:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a name="delete-cluster-fails"></a>Eliminazione del cluster non riuscita

Quando si tenta di eliminare un cluster con **azdata**, l'operazione ha esito negativo con l'errore seguente:

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

Un nuovo client Python Kubernetes (Version 9.0.0) ha modificato l'API degli spazi dei nomi Delete, che attualmente interrompe **azdata**. Questo si verifica solo se è installato un client Kubernetes Python più recente. È possibile risolvere questo problema eliminando direttamente il cluster tramite **kubectl** (`kubectl delete ns <ClusterName>`) oppure è possibile installare la versione precedente utilizzando `sudo pip install kubernetes==8.0.1`.

#### <a id="externaltablesctp24"></a>Tabelle esterne

- La distribuzione di cluster di Big data non crea più le origini dati esterne **SqlDataPool** e **SqlStoragePool** . È possibile creare queste origini dati manualmente per supportare la virtualizzazione dei dati nel pool di dati e nel pool di archiviazione.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, viene ricevuto un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, è possibile che venga ricevuto un errore se il file sottostante viene copiato in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si crea una tabella esterna in Oracle che usa tipi di dati di tipo carattere, la Azure Data Studio Virtualization Wizard interpreta tali colonne come VARCHAR nella definizione della tabella esterna. Ciò causerà un errore nel DDL della tabella esterna. Modificare lo schema Oracle per utilizzare il tipo NVARCHAR2 o creare istruzioni della tabella esterna manualmente e specificare NVARCHAR anziché utilizzare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione R, Python o MLeap dall'API RESTful, il timeout della chiamata si verifica in 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP POD cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Nello scenario in cui il Master-Pod viene riavviato, è possibile che la sessione `NoRoteToHostException`di Spark abbia esito negativo con. Questa situazione è causata da cache JVM che non vengono aggiornate con nuovi indirizzi IP.

- Se Jupyter è già installato e un Python separato in Windows, i notebook di Spark potrebbero avere esito negativo. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- In un notebook, se si fa clic sul comando **Aggiungi testo** , la cella di testo viene aggiunta in modalità di anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per impostare la modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, è possibile che venga visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file di dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche di configurazione apportate a HDFS che coinvolgono le modifiche di HDFS-site. XML non sono supportate.

#### <a name="security"></a>Sicurezza

- SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug ma un passaggio di sicurezza. Per ulteriori informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [Change the sa password](../linux/quickstart-install-connect-docker.md#sapassword).

- I log AKS possono contenere password SA per le distribuzioni di Big Data cluster.

## <a id="ctp23"></a>CTP 2,3 (febbraio)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 2,3.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
| :---------- | :------ |
| Inviare processi Spark nei cluster di Big Data in IntelliJ. | [Inviare processi Spark nei cluster di Big Data di SQL Server in IntelliJ](spark-submit-job-intellij-tool-plugin.md) |
| Interfaccia della riga di comando comune per la distribuzione di applicazioni e la gestione di cluster. | [Come distribuire un'app in un cluster di Big Data di SQL Server 2019 (anteprima)](big-data-cluster-create-apps.md) |
| Estensione di VS Code per distribuire applicazioni in un cluster di Big Data. | [Come usare VS Code per distribuire applicazioni nei cluster di Big Data di SQL Server](app-deployment-extension.md) |
| Modifiche all'utilizzo del comando dello strumento **azdata** . | Per altri dettagli, vedere i [problemi noti relativi a azdata](#azdatactp23). |
| Usare Sparklyr in un cluster Big Data | [Usare Sparklyr in cluster di Big Data di SQL Server 2019](sparklyr-from-RStudio.md) |
| Montare un'archiviazione esterna compatibile con Hadoop Distributed File System (HDFS) in un cluster Big Data con la **suddivisione in livelli HDFS**. | Vedere [Suddivisione in livelli HDFS](hdfs-tiering.md). |
| Nuova esperienza di connessione unificata per l'istanza master di SQL Server e il gateway HDFS/Spark. | Vedere [Istanza master di SQL Server e gateway HDFS/Spark](connect-to-big-data-cluster.md). |
| Eliminando un cluster con l' **eliminazione del cluster azdata** ora vengono eliminati solo gli oggetti nello spazio dei nomi che facevano parte del cluster Big Data. | Lo spazio dei nomi non viene eliminato. Nelle versioni precedenti, invece, questo comando elimina l'intero spazio dei nomi. |
| I nomi degli endpoint di _sicurezza_ sono stati cambiati e consolidati. | **service-security-lb** e **service-security-nodeport** sono stati consolidati nell'endpoint **endpoint-security**. |
| I nomi degli endpoint _proxy_ sono stati cambiati e consolidati. | **service-proxy-lb** e **service-proxy-nodeport** sono stati consolidati nell'endpoint **endpoint-service-proxy**. |
| I nomi degli endpoint di _controller_ sono stati cambiati e consolidati. | **service-mssql-controller-lb** e **service-mssql-controller-nodeport** sono stati consolidati nell'endpoint **endpoint-controller**. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni di questa versione.

#### <a name="deployment"></a>Distribuzione

- L'aggiornamento di un cluster di dati Big Data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster di Big Data esistente (usando la versione precedente di **azdata**) prima di distribuire la versione più recente. Per altre informazioni, vedere [eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- La variabile di ambiente **ACCEPT_EULA** deve essere "Yes" o "Yes" per accettare il contratto di licenza. Le versioni precedenti consentivano "y" e "Y", ma non sono più accettate e la distribuzione avrà esito negativo.

- Le variabili di ambiente **CLUSTER_PLATFORM** non hanno un valore predefinito come nelle versioni precedenti.

- Dopo la distribuzione in AKS, è possibile che vengano visualizzati i due eventi di avviso seguenti dalla distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la distribuzione corretta del cluster Big Data su AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Questo potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="kubeadm-deployments"></a>distribuzioni kubeadm

Se si utilizza kubeadm per distribuire Kubernetes in più computer, nel portale di amministrazione del cluster non vengono visualizzati correttamente gli endpoint necessari per la connessione al cluster Big Data. Se si verifica questo problema, utilizzare le seguenti operazioni per individuare gli indirizzi IP dell'endpoint di servizio:

- Se ci si connette dall'interno del cluster, eseguire una query su Kubernetes per l'indirizzo IP del servizio per l'endpoint a cui si vuole connettersi. Ad esempio, il comando **kubectl** seguente consente di visualizzare l'indirizzo IP dell'istanza di SQL Server Master:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Se ci si connette dall'esterno del cluster, attenersi alla procedura seguente per connettersi:

   1. Ottenere l'indirizzo IP del nodo che esegue l'istanza di SQL Server master `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`:.

   1. Connettersi a SQL Server istanza master usando questo indirizzo IP.

   1. Eseguire una query su **cluster_endpoint_table** nel database master per altri endpoint esterni.

      Se l'operazione ha esito negativo con un timeout della connessione, è possibile che il rispettivo nodo sia firewall. In questo caso, è necessario contattare l'amministratore del cluster Kubernetes e richiedere l'IP del nodo esposto esternamente. Potrebbe trattarsi di qualsiasi nodo. È quindi possibile usare tale indirizzo IP e la porta corrispondente per connettersi a vari servizi in esecuzione nel cluster. Ad esempio, l'amministratore può trovare questo indirizzo IP eseguendo:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="azdatactp23"></a>azdata

- Lo strumento **azdata** è stato modificato da un ordinamento verbo-sostantivo a un ordine sostantivo-verbo. Ad esempio, `azdata create cluster` è ora `azdata cluster create`.

- Il `--name` parametro è ora necessario quando si crea un cluster `azdata cluster create`con.

   ```bash
   azdata cluster create --name <cluster_name>
   ```

- Per informazioni importanti sull'aggiornamento alla versione più recente di Big Data cluster e **azdata**, vedere [eseguire l'aggiornamento a una nuova](deployment-upgrade.md)versione.

#### <a name="external-tables"></a>Tabelle esterne

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, viene ricevuto un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, è possibile che venga ricevuto un errore se il file sottostante viene copiato in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si crea una tabella esterna in Oracle che usa tipi di dati di tipo carattere, la Azure Data Studio Virtualization Wizard interpreta tali colonne come VARCHAR nella definizione della tabella esterna. Ciò causerà un errore nel DDL della tabella esterna. Modificare lo schema Oracle per utilizzare il tipo NVARCHAR2 o creare istruzioni della tabella esterna manualmente e specificare NVARCHAR anziché utilizzare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione R, Python o MLeap dall'API RESTful, il timeout della chiamata si verifica in 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP POD cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Nello scenario in cui il Master-Pod viene riavviato, è possibile che la sessione `NoRoteToHostException`di Spark abbia esito negativo con. Questa situazione è causata da cache JVM che non vengono aggiornate con nuovi indirizzi IP.

- Se Jupyter è già installato e un Python separato in Windows, i notebook di Spark potrebbero avere esito negativo. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- In un notebook, se si fa clic sul comando **Aggiungi testo** , la cella di testo viene aggiunta in modalità di anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per impostare la modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, è possibile che venga visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file di dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche di configurazione apportate a HDFS che coinvolgono le modifiche di HDFS-site. XML non sono supportate.

#### <a name="security"></a>Sicurezza

- SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug ma un passaggio di sicurezza. Per ulteriori informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [Change the sa password](../linux/quickstart-install-connect-docker.md#sapassword).

- I log AKS possono contenere password SA per le distribuzioni di Big Data cluster.

## <a id="ctp22"></a>CTP 2,2 (dicembre 2018)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 2,2.

### <a name="new-features"></a>Nuove funzionalità

- Portale di amministrazione del cluster `/portal` a cui si accede con (**indirizzo\<\>IP HTTPS://: 30777/Portal**).
- Il nome del servizio del pool `service-master-pool-lb` master `service-master-pool-nodeport` è `endpoint-master-pool`stato modificato da e a.
- Nuova versione di **azdata** e immagini aggiornate.
- Correzioni di bug e miglioramenti diversi.

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e le limitazioni di questa versione.

#### <a name="deployment"></a>Distribuzione

- L'aggiornamento di un cluster di dati Big Data da una versione precedente non è supportato. È necessario eseguire il backup ed eliminare qualsiasi cluster di Big Data esistente prima di distribuire la versione più recente. Per altre informazioni, vedere [eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione in AKS, è possibile che vengano visualizzati i due eventi di avviso seguenti dalla distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la distribuzione corretta del cluster Big Data su AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Questo potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="cluster-administration-portal"></a>Portale di amministrazione cluster

Il portale di amministrazione del cluster non Visualizza l'endpoint per l'istanza di SQL Server master. Per trovare l'indirizzo IP e la porta per l'istanza master, usare il comando **kubectl** seguente:

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
```

#### <a name="external-tables"></a>Tabelle esterne

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, viene ricevuto un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, è possibile che venga ricevuto un errore se il file sottostante viene copiato in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP POD cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Nello scenario in cui il Master-Pod viene riavviato, è possibile che la sessione `NoRoteToHostException`di Spark abbia esito negativo con. Questa situazione è causata da cache JVM che non vengono aggiornate con nuovi indirizzi IP.

- Se Jupyter è già installato e un Python separato in Windows, i notebook di Spark potrebbero avere esito negativo. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- In un notebook, se si fa clic sul comando **Aggiungi testo** , la cella di testo viene aggiunta in modalità di anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per impostare la modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, è possibile che venga visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file di dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche di configurazione apportate a HDFS che coinvolgono le modifiche di HDFS-site. XML non sono supportate.

#### <a name="security"></a>Sicurezza

- SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug ma un passaggio di sicurezza. Per ulteriori informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [Change the sa password](../linux/quickstart-install-connect-docker.md#sapassword).

- I log AKS possono contenere password SA per le distribuzioni di Big Data cluster.

## <a id="ctp21"></a>CTP 2,1 (novembre 2018)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 2,1.

### <a name="new-features"></a>Nuove funzionalità

- [Distribuire app Python e R](big-data-cluster-create-apps.md) in un cluster Big Data.
- Nuova versione di **azdata** e immagini aggiornate. 
- Correzioni di bug e miglioramenti diversi.

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti forniscono problemi noti per i cluster SQL Server Big Data nella versione CTP 2,1.

#### <a name="deployment"></a>Distribuzione

- L'aggiornamento di un cluster di dati Big Data da una versione precedente non è supportato. È necessario eseguire il backup ed eliminare qualsiasi cluster di Big Data esistente prima di distribuire la versione più recente. Per altre informazioni, vedere [eseguire l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione in AKS, è possibile che vengano visualizzati i due eventi di avviso seguenti dalla distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la distribuzione corretta del cluster Big Data su AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Questo potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="admin-portal"></a>Portale di amministrazione

- Quando si [Crea un'app usando il comando msqlctl-CTP](big-data-cluster-create-apps.md) e la si distribuisce in un cluster SQL Server Big data, il portale di amministrazione del cluster Mostra i pod in cui l'applicazione è stata distribuita come "sconosciuta" nella sezione controller della parte admin.

#### <a name="external-tables"></a>Tabelle esterne

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, viene ricevuto un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, è possibile che venga ricevuto un errore se il file sottostante viene copiato in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP POD cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Nello scenario in cui il Master-Pod viene riavviato, è possibile che la sessione `NoRoteToHostException`di Spark abbia esito negativo con. Questa situazione è causata da cache JVM che non vengono aggiornate con nuovi indirizzi IP.

- Se Jupyter è già installato e un Python separato in Windows, i notebook di Spark potrebbero avere esito negativo. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- In un notebook, se si fa clic sul comando **Aggiungi testo** , la cella di testo viene aggiunta in modalità di anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per impostare la modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, è possibile che venga visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file di dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche di configurazione apportate a HDFS che coinvolgono le modifiche di HDFS-site. XML non sono supportate.

#### <a name="security"></a>Sicurezza

- SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug ma un passaggio di sicurezza. Per ulteriori informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [Change the sa password](../linux/quickstart-install-connect-docker.md#sapassword).

- I log AKS possono contenere password SA per le distribuzioni di Big Data cluster.

## <a id="ctp20"></a>CTP 2,0 (ottobre 2018)

Le sezioni seguenti descrivono le nuove funzionalità e i problemi noti per i cluster Big Data in SQL Server 2019 CTP 2,0.

### <a name="new-features"></a>Nuove funzionalità

- Esperienza di distribuzione semplice con lo strumento di gestione di azdata
- Esperienza notebook nativa in Azure Data Studio
- Eseguire query sui file HDFS tramite l'istanza di archiviazione di SQL Server
- Virtualizzazione dei dati tramite master per SQL Server, Oracle, MongoDB e HDFS
- Data Virtualization Wizard for SQL Server e Oracle in Azure Data Studio
- ML Services nel database master
- Portale di amministrazione cluster che è possibile utilizzare per il monitoraggio e la risoluzione dei problemi
- Invio del processo Spark in Azure Data Studio 
- Interfaccia utente di Spark nel portale di amministrazione del cluster
- Montaggio del volume in classi di archiviazione
- Query sui pool di dati del database master
- Mostrare il piano per le query distribuite in SSMS
- Pacchetto pip per lo strumento di gestione azdata
- Motore di distribuzione predefinito tramite il servizio controller

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti forniscono problemi noti per i cluster SQL Server Big Data nella versione CTP 2,0.

#### <a name="deployment"></a>Distribuzione

- Se si usa Azure Kubernetes Service (AKS), la versione consigliata di Kubernetes è 1,10. *, che non supporta il ridimensionamento del disco. È necessario assicurarsi di ridimensionare lo spazio di archiviazione di conseguenza in fase di distribuzione. Per altre informazioni su come modificare le dimensioni di archiviazione, vedere l'articolo relativo alla [persistenza dei dati](concept-data-persistence.md) . Per Kubernetes distribuite nelle macchine virtuali, la versione consigliata è 1,11.

- Dopo la distribuzione in AKS, è possibile che vengano visualizzati i due eventi di avviso seguenti dalla distribuzione. Entrambi questi eventi sono problemi noti, ma non impediscono la distribuzione corretta del cluster Big Data su AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se la distribuzione di un cluster Big Data non riesce, lo spazio dei nomi associato non viene rimosso. Questo potrebbe generare uno spazio dei nomi orfano nel cluster. Una soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="external-tables"></a>Tabelle esterne

- È possibile creare una tabella esterna del pool di dati per una tabella con tipi di colonna non supportati. Se si esegue una query sulla tabella esterna, viene ricevuto un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query su una tabella esterna del pool di archiviazione, è possibile che venga ricevuto un errore se il file sottostante viene copiato in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebook

- È possibile che gli indirizzi IP POD cambino nell'ambiente Kubernetes quando i pod vengono riavviati. Nello scenario in cui il Master-Pod viene riavviato, è possibile che la sessione `NoRoteToHostException`di Spark abbia esito negativo con. Questa situazione è causata da cache JVM che non vengono aggiornate con nuovi indirizzi IP.

- Se Jupyter è già installato e un Python separato in Windows, i notebook di Spark potrebbero avere esito negativo. Per risolvere questo problema, aggiornare Jupyter alla versione più recente.

- In un notebook, se si fa clic sul comando **Aggiungi testo** , la cella di testo viene aggiunta in modalità di anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per impostare la modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se si fa clic con il pulsante destro del mouse su un file in HDFS per visualizzarne l'anteprima, è possibile che venga visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima i file di dimensioni superiori a 30 MB in Azure Data Studio.

- Le modifiche di configurazione apportate a HDFS che coinvolgono le modifiche di HDFS-site. XML non sono supportate.

#### <a name="security"></a>Sicurezza

- SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo). È necessario reimpostare SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug ma un passaggio di sicurezza. Per ulteriori informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [Change the sa password](../linux/quickstart-install-connect-docker.md#sapassword).

- I log AKS possono contenere password SA per le distribuzioni di Big Data cluster.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster SQL Server Big Data, vedere [che cosa sono SQL Server 2019 cluster Big Data?](big-data-cluster-overview.md).
