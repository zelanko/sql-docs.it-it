---
title: Note sulla versione
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive gli ultimi aggiornamenti e problemi noti per i cluster di big data di SQL Server 2019 (anteprima).
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1f2d7f5a1d4a966edbce3c4ad96a7b31bd604b48
ms.sourcegitcommit: f7ad034f748ebc3e5691a5e4c3eb7490e5cf3ccf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469128"
---
# <a name="release-notes-for-big-data-clusters-on-sql-server"></a>Note sulla versione per i cluster di big data in SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo elenca gli aggiornamenti e conoscere i problemi per le versioni più recenti di SQL Server cluster di big data.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp31"></a> CTP 3.1 (giugno)

Le sezioni seguenti descrivono le nuove funzionalità e problemi noti per i cluster di big data in SQL Server 2019 CTP 3.1.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| `mssqlctl` modifiche dei comandi | `mssqlctl cluster` i comandi sono stati rinominati in `mssqlctl bdc`. Per altre informazioni, vedere la [ `mssqlctl` riferimento](reference-mssqlctl.md). |
| Nuovo `mssqlctl` i comandi di stato e la rimozione del portale di amministrazione del Cluster. | Nel portale di amministrazione del Cluster è stata rimossa in questa versione. Sono stati aggiunti nuovi comandi di stato per `mssqlctl` complemento esistenti comandi di monitoraggio. |
| Pool di calcolo di Spark | Creazione di nodi aggiuntivi per aumentare la potenza di calcolo di Spark senza dover aumentare le prestazioni di archiviazione. Inoltre, è possibile avviare i nodi del pool di archiviazione che non vengono usati per Spark. Spark e l'archiviazione sono separate. Per altre informazioni, vedere [configurare l'archiviazione senza spark](deployment-custom-configuration.md#sparkstorage). |
| Connettore Spark MSSQL | Supporto per la lettura/scrittura alle tabelle esterne del pool di dati. Solo tabelle dell'istanza precedente le versioni supportate lettura/scrittura al server principale. Per altre informazioni, vedere [come leggere e scrivere in SQL Server da Spark usando il connettore Spark MSSQL](spark-mssql-connector.md). |
| Machine Learning che usano MLeap | [Eseguire il training di un modello di MLeap machine learning in Spark e assegnare un punteggio in SQL Server tramite l'estensione del linguaggio Java](spark-create-machine-learning-model.md). |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e limitazioni della versione.

#### <a name="hdfs"></a>HDFS

- Se facendo clic su un file in HDFS per visualizzarlo in anteprima, si potrebbe essere visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima file di dimensioni superiori a 30 MB in Azure Data Studio.

- Modifiche di configurazione HDFS che implicano modifiche alle hdfs-Site. XML non sono supportate.

#### <a name="deployment"></a>Distribuzione

- Aggiornamento di un cluster di dati dei big data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster di big data esistente (con la versione precedente di **mssqlctl**) prima di distribuire la versione più recente. Per altre informazioni, vedere [esegue l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione nel servizio contenitore di AZURE, è possibile visualizzare i seguenti due eventi di avviso dalla distribuzione. Entrambi questi eventi sono presenti problemi noti, ma non impediscono è avere distribuito il cluster di big data nel servizio contenitore di AZURE.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- In caso di una distribuzione cluster con i big data, non viene rimosso lo spazio dei nomi associato. Ciò può comportare uno spazio dei nomi orfano sul cluster. Soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="external-tables"></a>Tabelle esterne

- Distribuzione di cluster di big data non crea più il **SqlDataPool** e **SqlStoragePool** origini dati esterne. È possibile creare queste origini dati manualmente per supportare la virtualizzazione dei dati per il pool di dati e il pool di archiviazione.

   > [!NOTE]
   > L'URI per la creazione di queste origini dati esterne è diversa tra le versioni CTP. Vedere i comandi di Transact-SQL seguenti per informazioni su come crearli 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- È possibile creare una tabella esterna di pool di dati per una tabella che contiene i tipi di colonna non supportati. Se si esegue una query della tabella esterna, viene visualizzato un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query una tabella esterna del pool di archiviazione, è possibile ottenere un errore se vengono copiato i file sottostante in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si sta creando una tabella esterna a Oracle che usano tipi di dati carattere, la procedura guidata la virtualizzazione di Studio di Azure Data interpreta queste colonne come VARCHAR nella definizione della tabella esterna. Ciò causerà un errore nel DDL della tabella esterna. Modificare lo schema Oracle per utilizzare il tipo NVARCHAR2, oppure creare manualmente le istruzioni di tabella esterna e specificare NVARCHAR invece di usare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione di R, Python o MLeap dall'API REST, la chiamata con timeout di 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- Gli indirizzi IP del POD possono cambiare nell'ambiente di Kubernetes come riavvii POD. Nello scenario in cui i pod master viene riavviato, la sessione di Spark potrebbe non riuscire con `NoRoteToHostException`. Questo problema è causato dalla cache JVM non aggiornati con nuovo indirizzo IP indirizzi.

- Se hai Jupyter già installato e Python separato in Windows, i notebook Spark potrebbero non riuscire. Per risolvere questo problema, eseguire l'aggiornamento di Jupyter per la versione più recente.

- In un notebook, se si sceglie la **Aggiungi testo** comando, la cella di testo viene aggiunto in modalità anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per attivare/disattivare per la modalità di modifica e modificare la cella.

#### <a name="security"></a>Sicurezza

- Il SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo di alimentazione). È necessario reimpostare il SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug, ma un passaggio di sicurezza. Per altre informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [modificare la password SA](../linux/quickstart-install-connect-docker.md#sapassword).

- I log di servizio contenitore di AZURE possono contenere la password dell'amministratore di sistema per le distribuzioni cluster di big data.

## <a id="ctp30"></a> CTP 3.0 (maggio)

Le sezioni seguenti descrivono le nuove funzionalità e problemi noti per i cluster di big data in CTP 3.0 per SQL Server 2019.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Aggiornamenti di **mssqlctl** | Numerosi [aggiornamenti di comandi e parametri](../big-data-cluster/reference-mssqlctl.md) **mssqlctl** tra cui un aggiornamento al comando **mssqlctl login**, che ora ha come destinazione il nome utente e l'endpoint del controller. |
| Miglioramenti all'archiviazione | Supporto per configurazioni di archiviazione diverse per log e dati. È stato anche ridotto il numero di attestazioni di volume permanente per un cluster di Big Data. |
| Più istanze del pool di calcolo | Supporto per più istanze del pool di calcolo. |
| Nuove funzionalità e comportamento del pool | Il pool di calcolo viene ora usato per impostazione predefinita per le operazioni del pool di dati e del pool di archiviazione solo nella distribuzione **ROUND_ROBIN**. Il pool di dati ora può usare un nuovo tipo di distribuzione **REPLICATED**, il che significa che gli stessi dati sono presenti in tutte le istanze del pool di dati. |
| Miglioramenti alle tabelle esterne | Le tabelle esterne del tipo origine dati HADOOP ora supportano la lettura di righe con dimensioni fino a 1 MB. Le tabelle esterne (ODBC, pool di archiviazione, pool di dati) ora supportano righe larghe quanto una tabella di SQL Server. |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e limitazioni della versione.

#### <a name="hdfs"></a>HDFS

- Azure Data Studio restituisce un errore quando si tenta di creare una nuova cartella in HDFS. Per abilitare questa funzionalità, installare la build Insider di Studio dei dati di Azure:
  
   - [Programma di installazione di Windows utente - **build Insider**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Programma di installazione di Windows System - **build Insider**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [Windows con estensione ZIP - **build Insider**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [macOS - ZIP **build Insider**](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [Linux con estensione TAR. -GZ **build Insider**](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- Se facendo clic su un file in HDFS per visualizzarlo in anteprima, si potrebbe essere visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima file di dimensioni superiori a 30 MB in Azure Data Studio.

- Modifiche di configurazione HDFS che implicano modifiche alle hdfs-Site. XML non sono supportate.

#### <a name="deployment"></a>Distribuzione

- Le procedure di distribuzione precedenti per i cluster abilitate per GPU dei big data non sono supportate nella versione CTP 3.0. Una procedura di distribuzione alternativo è in fase di analisi. Per il momento, l'articolo "Distribuzione del cluster con supporto per GPU ed eseguire TensorFlow un big data" è stata temporaneamente non pubblicato per evitare confusione.

- Aggiornamento di un cluster di dati dei big data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster di big data esistente (con la versione precedente di **mssqlctl**) prima di distribuire la versione più recente. Per altre informazioni, vedere [esegue l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione nel servizio contenitore di AZURE, è possibile visualizzare i seguenti due eventi di avviso dalla distribuzione. Entrambi questi eventi sono presenti problemi noti, ma non impediscono è avere distribuito il cluster di big data nel servizio contenitore di AZURE.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- In caso di una distribuzione cluster con i big data, non viene rimosso lo spazio dei nomi associato. Ciò può comportare uno spazio dei nomi orfano sul cluster. Soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="external-tables"></a>Tabelle esterne

- Distribuzione di cluster di big data non crea più il **SqlDataPool** e **SqlStoragePool** origini dati esterne. È possibile creare queste origini dati manualmente per supportare la virtualizzazione dei dati per il pool di dati e il pool di archiviazione.

   > [!NOTE]
   > L'URI per la creazione di queste origini dati esterne è diversa tra le versioni CTP. Vedere i comandi di Transact-SQL seguenti per informazioni su come crearli 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- È possibile creare una tabella esterna di pool di dati per una tabella che contiene i tipi di colonna non supportati. Se si esegue una query della tabella esterna, viene visualizzato un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query una tabella esterna del pool di archiviazione, è possibile ottenere un errore se vengono copiato i file sottostante in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si sta creando una tabella esterna a Oracle che usano tipi di dati carattere, la procedura guidata la virtualizzazione di Studio di Azure Data interpreta queste colonne come VARCHAR nella definizione della tabella esterna. Ciò causerà un errore nel DDL della tabella esterna. Modificare lo schema Oracle per utilizzare il tipo NVARCHAR2, oppure creare manualmente le istruzioni di tabella esterna e specificare NVARCHAR invece di usare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione di R, Python o MLeap dall'API REST, la chiamata con timeout di 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- Gli indirizzi IP del POD possono cambiare nell'ambiente di Kubernetes come riavvii POD. Nello scenario in cui i pod master viene riavviato, la sessione di Spark potrebbe non riuscire con `NoRoteToHostException`. Questo problema è causato dalla cache JVM non aggiornati con nuovo indirizzo IP indirizzi.

- Se hai Jupyter già installato e Python separato in Windows, i notebook Spark potrebbero non riuscire. Per risolvere questo problema, eseguire l'aggiornamento di Jupyter per la versione più recente.

- In un notebook, se si sceglie la **Aggiungi testo** comando, la cella di testo viene aggiunto in modalità anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per attivare/disattivare per la modalità di modifica e modificare la cella.

#### <a name="security"></a>Sicurezza

- Il SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo di alimentazione). È necessario reimpostare il SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug, ma un passaggio di sicurezza. Per altre informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [modificare la password SA](../linux/quickstart-install-connect-docker.md#sapassword).

- I log di servizio contenitore di AZURE possono contenere la password dell'amministratore di sistema per le distribuzioni cluster di big data.

## <a id="ctp25"></a> CTP 2.5 (aprile)

Le sezioni seguenti descrivono le nuove funzionalità e problemi noti per i cluster di big data in SQL Server 2019 CTP 2.5.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Profili di distribuzione | Per le distribuzioni di cluster di Big Data, usare i [file JSON di configurazione della distribuzione](deployment-guidance.md#configfile), predefiniti o personalizzati, invece delle variabili di ambiente. |
| Distribuzioni richieste | `mssqlctl cluster create` ora richiede di specificare le eventuali impostazioni necessarie per le distribuzioni predefinite. |
| Modifiche dei nomi di endpoint di servizio e pod | I seguenti endpoint esterni sono stati modificati i nomi:<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-service-proxy** => **mgmtproxy-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| Miglioramenti di **mssqlctl** | Usare **mssqlctl** per [elencare gli endpoint esterni](deployment-guidance.md#endpoints) e controllare la versione di **mssqlctl** con il parametro `--version`. |
| Eseguire l'installazione offline | Linee guida per le distribuzioni di cluster non in linea dei big Data. |
| Miglioramenti della suddivisione in livelli HDFS | La suddivisione in livelli S3, la memorizzazione nella cache di montaggio e OAuth supporto per Azure Data Lake Store Gen2. |
| Nuovo `mssql` connettore Spark-SQL Server | |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e limitazioni della versione.

#### <a name="deployment"></a>Distribuzione

- Aggiornamento di un cluster di dati dei big data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster di big data esistente (con la versione precedente di **mssqlctl**) prima di distribuire la versione più recente. Per altre informazioni, vedere [esegue l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione nel servizio contenitore di AZURE, è possibile visualizzare i seguenti due eventi di avviso dalla distribuzione. Entrambi questi eventi sono presenti problemi noti, ma non impediscono è avere distribuito il cluster di big data nel servizio contenitore di AZURE.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- In caso di una distribuzione cluster con i big data, non viene rimosso lo spazio dei nomi associato. Ciò può comportare uno spazio dei nomi orfano sul cluster. Soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="external-tables"></a>Tabelle esterne

- Distribuzione di cluster di big data non crea più il **SqlDataPool** e **SqlStoragePool** origini dati esterne. È possibile creare queste origini dati manualmente per supportare la virtualizzazione dei dati per il pool di dati e il pool di archiviazione.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- È possibile creare una tabella esterna di pool di dati per una tabella che contiene i tipi di colonna non supportati. Se si esegue una query della tabella esterna, viene visualizzato un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query una tabella esterna del pool di archiviazione, è possibile ottenere un errore se vengono copiato i file sottostante in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si sta creando una tabella esterna a Oracle che usano tipi di dati carattere, la procedura guidata la virtualizzazione di Studio di Azure Data interpreta queste colonne come VARCHAR nella definizione della tabella esterna. Ciò causerà un errore nel DDL della tabella esterna. Modificare lo schema Oracle per utilizzare il tipo NVARCHAR2, oppure creare manualmente le istruzioni di tabella esterna e specificare NVARCHAR invece di usare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione di R, Python o MLeap dall'API REST, la chiamata con timeout di 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- Gli indirizzi IP del POD possono cambiare nell'ambiente di Kubernetes come riavvii POD. Nello scenario in cui i pod master viene riavviato, la sessione di Spark potrebbe non riuscire con `NoRoteToHostException`. Questo problema è causato dalla cache JVM non aggiornati con nuovo indirizzo IP indirizzi.

- Se hai Jupyter già installato e Python separato in Windows, i notebook Spark potrebbero non riuscire. Per risolvere questo problema, eseguire l'aggiornamento di Jupyter per la versione più recente.

- In un notebook, se si sceglie la **Aggiungi testo** comando, la cella di testo viene aggiunto in modalità anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per attivare/disattivare per la modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se facendo clic su un file in HDFS per visualizzarlo in anteprima, si potrebbe essere visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima file di dimensioni superiori a 30 MB in Azure Data Studio.

- Modifiche di configurazione HDFS che implicano modifiche alle hdfs-Site. XML non sono supportate.

#### <a name="security"></a>Sicurezza

- Il SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo di alimentazione). È necessario reimpostare il SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug, ma un passaggio di sicurezza. Per altre informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [modificare la password SA](../linux/quickstart-install-connect-docker.md#sapassword).

- I log di servizio contenitore di AZURE possono contenere la password dell'amministratore di sistema per le distribuzioni cluster di big data.

## <a id="ctp24"></a> CTP 2.4 (marzo)

Le sezioni seguenti descrivono le nuove funzionalità e problemi noti per i cluster di big data in SQL Server 2019 CTP 2.4.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
|:---|:---|
| Materiale sussidiario sul supporto della GPU per l'esecuzione di Deep Learning con TensorFlow in Spark. | [Distribuire un cluster di Big Data con il supporto della GPU ed eseguire TensorFlow](spark-gpu-tensorflow.md). |
| Le origini dati **SqlDataPool** e **SqlStoragePool** non vengono più create per impostazione predefinita. | Se necessario, crearle manualmente. Vedere i [problemi noti](#externaltablesctp24). |
| Supporto di `INSERT INTO SELECT` per il pool di dati. | Per un esempio, vedere [Esercitazione: Ingest data into a SQL Server data pool with Transact-SQL](tutorial-data-pool-ingest-sql.md) (Inserire dati in un pool di dati di SQL Server con Transact-SQL). |
| Opzioni `FORCE SCALEOUTEXECUTION` e `DISABLE SCALEOUTEXECUTION`. | Forza o disabilita l'utilizzo dell'attività di calcolo del pool per le query su tabelle esterne. Ad esempio `SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)`. |
| Aggiornamento delle raccomandazioni sulla distribuzione del servizio Azure Kubernetes. | Quando si valutano i cluster di Big Data nel servizio Azure Kubernetes, è ora consigliabile usare un singolo nodo di dimensioni **Standard_L8s**. |
| Aggiornamento del runtime Spark a Spark 2.4. | |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e limitazioni della versione.

#### <a name="deployment"></a>Distribuzione

- Aggiornamento di un cluster di dati dei big data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster di big data esistente (con la versione precedente di **mssqlctl**) prima di distribuire la versione più recente. Per altre informazioni, vedere [esegue l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione nel servizio contenitore di AZURE, è possibile visualizzare i seguenti due eventi di avviso dalla distribuzione. Entrambi questi eventi sono presenti problemi noti, ma non impediscono è avere distribuito il cluster di big data nel servizio contenitore di AZURE.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- In caso di una distribuzione cluster con i big data, non viene rimosso lo spazio dei nomi associato. Ciò può comportare uno spazio dei nomi orfano sul cluster. Soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="kubeadm-deployments"></a>distribuzioni kubeadm

Se si usa kubeadm per la distribuzione di Kubernetes in più computer, il portale di amministrazione cluster non viene visualizzato correttamente gli endpoint necessari per connettersi al cluster di big data. Se si riscontrano questo problema, usare la soluzione alternativa seguente per individuare gli indirizzi IP dell'endpoint del servizio:

- Se ci si connette da all'interno del cluster, eseguire una query per l'IP del servizio per l'endpoint che si desidera connettersi a Kubernetes. Ad esempio, il seguente **kubectl** comando Visualizza l'indirizzo IP dell'istanza master di SQL Server:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Se ci si connette dall'esterno del cluster, usare la procedura seguente per connettersi:

   1. Ottenere l'indirizzo IP del nodo che esegue l'istanza master di SQL Server: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`.

   1. Connettersi all'istanza master di SQL Server usando questo indirizzo IP.

   1. Query di **cluster_endpoint_table** nel database master per gli altri endpoint esterni.

      Se l'operazione non riesce con un timeout di connessione, è possibile che il relativo nodo è protette. In questo caso, è necessario contattare l'amministratore del cluster Kubernetes e richiedere l'indirizzo IP di nodo che viene esposto esternamente. Potrebbe trattarsi di qualsiasi nodo. È quindi possibile usare tale indirizzo IP e porta corrispondente per la connessione a vari servizi in esecuzione nel cluster. Ad esempio, l'amministratore può trovare questo indirizzo IP eseguendo:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a name="delete-cluster-fails"></a>Eliminazione del cluster non riesce

Quando si tenta di eliminare un cluster con **mssqlctl**, ha esito negativo con l'errore seguente:

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

Un nuovo client Python Kubernetes (versione 9.0.0) modificato l'eliminazione degli spazi dei nomi API, che attualmente si interrompe **mssqlctl**. Ciò si verifica solo se si dispone di un client più recente di python Kubernetes installato. È possibile risolvere questo problema eliminando direttamente il cluster usando **kubectl** (`kubectl delete ns <ClusterName>`), oppure è possibile installare la versione meno recente usando `sudo pip install kubernetes==8.0.1`.

#### <a id="externaltablesctp24"></a> Tabelle esterne

- Distribuzione di cluster di big data non crea più il **SqlDataPool** e **SqlStoragePool** origini dati esterne. È possibile creare queste origini dati manualmente per supportare la virtualizzazione dei dati per il pool di dati e il pool di archiviazione.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- È possibile creare una tabella esterna di pool di dati per una tabella che contiene i tipi di colonna non supportati. Se si esegue una query della tabella esterna, viene visualizzato un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query una tabella esterna del pool di archiviazione, è possibile ottenere un errore se vengono copiato i file sottostante in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si sta creando una tabella esterna a Oracle che usano tipi di dati carattere, la procedura guidata la virtualizzazione di Studio di Azure Data interpreta queste colonne come VARCHAR nella definizione della tabella esterna. Ciò causerà un errore nel DDL della tabella esterna. Modificare lo schema Oracle per utilizzare il tipo NVARCHAR2, oppure creare manualmente le istruzioni di tabella esterna e specificare NVARCHAR invece di usare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione di R, Python o MLeap dall'API REST, la chiamata con timeout di 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- Gli indirizzi IP del POD possono cambiare nell'ambiente di Kubernetes come riavvii POD. Nello scenario in cui i pod master viene riavviato, la sessione di Spark potrebbe non riuscire con `NoRoteToHostException`. Questo problema è causato dalla cache JVM non aggiornati con nuovo indirizzo IP indirizzi.

- Se hai Jupyter già installato e Python separato in Windows, i notebook Spark potrebbero non riuscire. Per risolvere questo problema, eseguire l'aggiornamento di Jupyter per la versione più recente.

- In un notebook, se si sceglie la **Aggiungi testo** comando, la cella di testo viene aggiunto in modalità anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per attivare/disattivare per la modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se facendo clic su un file in HDFS per visualizzarlo in anteprima, si potrebbe essere visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima file di dimensioni superiori a 30 MB in Azure Data Studio.

- Modifiche di configurazione HDFS che implicano modifiche alle hdfs-Site. XML non sono supportate.

#### <a name="security"></a>Sicurezza

- Il SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo di alimentazione). È necessario reimpostare il SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug, ma un passaggio di sicurezza. Per altre informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [modificare la password SA](../linux/quickstart-install-connect-docker.md#sapassword).

- I log di servizio contenitore di AZURE possono contenere la password dell'amministratore di sistema per le distribuzioni cluster di big data.

## <a id="ctp23"></a> CTP 2.3 (febbraio)

Le sezioni seguenti descrivono le nuove funzionalità e problemi noti per i cluster di big data in versione CTP 2.3 di SQL Server 2019.

### <a name="whats-new"></a>Novità

| Nuova funzionalità o aggiornamento | Dettagli |
| :---------- | :------ |
| Inviare processi Spark nei cluster di Big Data in IntelliJ. | [Inviare processi Spark nei cluster di Big Data di SQL Server in IntelliJ](spark-submit-job-intellij-tool-plugin.md) |
| Interfaccia della riga di comando comune per la distribuzione di applicazioni e la gestione di cluster. | [Come distribuire un'app in un cluster di Big Data di SQL Server 2019 (anteprima)](big-data-cluster-create-apps.md) |
| Estensione di VS Code per distribuire applicazioni in un cluster di Big Data. | [Come usare VS Code per distribuire applicazioni nei cluster di Big Data di SQL Server](app-deployment-extension.md) |
| Modifiche apportate all'utilizzo dei comandi dello strumento **mssqlctl**. | Per informazioni più dettagliate, vedere i [problemi noti di mssqlctl](#mssqlctlctp23). |
| Usare Sparklyr nel cluster di big data | [Usare Sparklyr in cluster di Big Data di SQL Server 2019](sparklyr-from-RStudio.md) |
| Montare un'archiviazione esterna compatibile con Hadoop Distributed File System (HDFS) in un cluster Big Data con la **suddivisione in livelli HDFS**. | Vedere [Suddivisione in livelli HDFS](hdfs-tiering.md). |
| Nuova esperienza di connessione unificata per l'istanza master di SQL Server e il gateway HDFS/Spark. | Vedere [Istanza master di SQL Server e gateway HDFS/Spark](connect-to-big-data-cluster.md). |
| L'eliminazione di un cluster con **mssqlctl cluster delete** rimuove ora solo gli oggetti dello spazio dei nomi che fanno parte del cluster di Big Data. | Lo spazio dei nomi non viene eliminato. Nelle versioni precedenti, invece, questo comando elimina l'intero spazio dei nomi. |
| I nomi degli endpoint di _sicurezza_ sono stati cambiati e consolidati. | **service-security-lb** e **service-security-nodeport** sono stati consolidati nell'endpoint **endpoint-security**. |
| I nomi degli endpoint _proxy_ sono stati cambiati e consolidati. | **service-proxy-lb** e **service-proxy-nodeport** sono stati consolidati nell'endpoint **endpoint-service-proxy**. |
| I nomi degli endpoint di _controller_ sono stati cambiati e consolidati. | **service-mssql-controller-lb** e **service-mssql-controller-nodeport** sono stati consolidati nell'endpoint **endpoint-controller**. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e limitazioni della versione.

#### <a name="deployment"></a>Distribuzione

- Aggiornamento di un cluster di dati dei big data da una versione precedente non è supportato.

   > [!IMPORTANT]
   > È necessario eseguire il backup dei dati e quindi eliminare il cluster di big data esistente (con la versione precedente di **mssqlctl**) prima di distribuire la versione più recente. Per altre informazioni, vedere [esegue l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Il **ACCEPT_EULA** variabile di ambiente deve essere "yes" o "Sì" per accettare le condizioni di licenza. Nelle versioni precedenti consentiti "y" e "Y", ma questi non vengono più accettati e causerà la distribuzione ha esito negativo.

- Il **CLUSTER_PLATFORM** le variabili di ambiente è privo di un valore predefinito come accadeva nelle versioni precedenti.

- Dopo la distribuzione nel servizio contenitore di AZURE, è possibile visualizzare i seguenti due eventi di avviso dalla distribuzione. Entrambi questi eventi sono presenti problemi noti, ma non impediscono è avere distribuito il cluster di big data nel servizio contenitore di AZURE.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- In caso di una distribuzione cluster con i big data, non viene rimosso lo spazio dei nomi associato. Ciò può comportare uno spazio dei nomi orfano sul cluster. Soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="kubeadm-deployments"></a>distribuzioni kubeadm

Se si usa kubeadm per la distribuzione di Kubernetes in più computer, il portale di amministrazione cluster non viene visualizzato correttamente gli endpoint necessari per connettersi al cluster di big data. Se si riscontrano questo problema, usare la soluzione alternativa seguente per individuare gli indirizzi IP dell'endpoint del servizio:

- Se ci si connette da all'interno del cluster, eseguire una query per l'IP del servizio per l'endpoint che si desidera connettersi a Kubernetes. Ad esempio, il seguente **kubectl** comando Visualizza l'indirizzo IP dell'istanza master di SQL Server:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Se ci si connette dall'esterno del cluster, usare la procedura seguente per connettersi:

   1. Ottenere l'indirizzo IP del nodo che esegue l'istanza master di SQL Server: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`.

   1. Connettersi all'istanza master di SQL Server usando questo indirizzo IP.

   1. Query di **cluster_endpoint_table** nel database master per gli altri endpoint esterni.

      Se l'operazione non riesce con un timeout di connessione, è possibile che il relativo nodo è protette. In questo caso, è necessario contattare l'amministratore del cluster Kubernetes e richiedere l'indirizzo IP di nodo che viene esposto esternamente. Potrebbe trattarsi di qualsiasi nodo. È quindi possibile usare tale indirizzo IP e porta corrispondente per la connessione a vari servizi in esecuzione nel cluster. Ad esempio, l'amministratore può trovare questo indirizzo IP eseguendo:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="mssqlctlctp23"></a> mssqlctl

- Il **mssqlctl** strumento modificato da un comando di verbo-sostantivo ordinamento a un ordine di verbo-sostantivo. Ad esempio, `mssqlctl create cluster` è ora `mssqlctl cluster create`.

- Il `--name` parametro è ora necessaria per la creazione di un cluster con `mssqlctl cluster create`.

   ```bash
   mssqlctl cluster create --name <cluster_name>
   ```

- Per informazioni importanti sull'aggiornamento all'ultima versione dei cluster di big data e **mssqlctl**, vedere [esegue l'aggiornamento a una nuova versione](deployment-upgrade.md).

#### <a name="external-tables"></a>Tabelle esterne

- È possibile creare una tabella esterna di pool di dati per una tabella che contiene i tipi di colonna non supportati. Se si esegue una query della tabella esterna, viene visualizzato un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query una tabella esterna del pool di archiviazione, è possibile ottenere un errore se vengono copiato i file sottostante in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se si sta creando una tabella esterna a Oracle che usano tipi di dati carattere, la procedura guidata la virtualizzazione di Studio di Azure Data interpreta queste colonne come VARCHAR nella definizione della tabella esterna. Ciò causerà un errore nel DDL della tabella esterna. Modificare lo schema Oracle per utilizzare il tipo NVARCHAR2, oppure creare manualmente le istruzioni di tabella esterna e specificare NVARCHAR invece di usare la procedura guidata.

#### <a name="application-deployment"></a>Distribuzione dell'applicazione

- Quando si chiama un'applicazione di R, Python o MLeap dall'API REST, la chiamata con timeout di 5 minuti.

#### <a name="spark-and-notebooks"></a>Spark e notebook

- Gli indirizzi IP del POD possono cambiare nell'ambiente di Kubernetes come riavvii POD. Nello scenario in cui i pod master viene riavviato, la sessione di Spark potrebbe non riuscire con `NoRoteToHostException`. Questo problema è causato dalla cache JVM non aggiornati con nuovo indirizzo IP indirizzi.

- Se hai Jupyter già installato e Python separato in Windows, i notebook Spark potrebbero non riuscire. Per risolvere questo problema, eseguire l'aggiornamento di Jupyter per la versione più recente.

- In un notebook, se si sceglie la **Aggiungi testo** comando, la cella di testo viene aggiunto in modalità anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per attivare/disattivare per la modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se facendo clic su un file in HDFS per visualizzarlo in anteprima, si potrebbe essere visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima file di dimensioni superiori a 30 MB in Azure Data Studio.

- Modifiche di configurazione HDFS che implicano modifiche alle hdfs-Site. XML non sono supportate.

#### <a name="security"></a>Sicurezza

- Il SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo di alimentazione). È necessario reimpostare il SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug, ma un passaggio di sicurezza. Per altre informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [modificare la password SA](../linux/quickstart-install-connect-docker.md#sapassword).

- I log di servizio contenitore di AZURE possono contenere la password dell'amministratore di sistema per le distribuzioni cluster di big data.

## <a id="ctp22"></a> CTP 2.2 (dicembre 2018)

Le sezioni seguenti descrivono le nuove funzionalità e problemi noti per i cluster di big data in SQL Server 2019 CTP 2.2.

### <a name="new-features"></a>Nuove funzionalità

- Accedere al portale di amministrazione di cluster con `/portal` (**https://\<ip-address\>: 30777/portale**).
- Nome del servizio pool master modificata `service-master-pool-lb` e `service-master-pool-nodeport` a `endpoint-master-pool`.
- Nuova versione di **mssqlctl** e aggiornate le immagini.
- Varie correzioni di bug e miglioramenti.

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti e limitazioni della versione.

#### <a name="deployment"></a>Distribuzione

- Aggiornamento di un cluster di dati dei big data da una versione precedente non è supportato. È necessario eseguire il backup ed eliminare qualsiasi cluster di big data esistente prima di distribuire la versione più recente. Per altre informazioni, vedere [esegue l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione nel servizio contenitore di AZURE, è possibile visualizzare i seguenti due eventi di avviso dalla distribuzione. Entrambi questi eventi sono presenti problemi noti, ma non impediscono è avere distribuito il cluster di big data nel servizio contenitore di AZURE.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- In caso di una distribuzione cluster con i big data, non viene rimosso lo spazio dei nomi associato. Ciò può comportare uno spazio dei nomi orfano sul cluster. Soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="cluster-administration-portal"></a>Portale di amministrazione cluster

Nel portale di amministrazione cluster non viene visualizzata l'endpoint per l'istanza master di SQL Server. Per trovare l'indirizzo IP e la porta per l'istanza master, usare il comando seguente **kubectl** comando:

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
```

#### <a name="external-tables"></a>Tabelle esterne

- È possibile creare una tabella esterna di pool di dati per una tabella che contiene i tipi di colonna non supportati. Se si esegue una query della tabella esterna, viene visualizzato un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query una tabella esterna del pool di archiviazione, è possibile ottenere un errore se vengono copiato i file sottostante in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebook

- Gli indirizzi IP del POD possono cambiare nell'ambiente di Kubernetes come riavvii POD. Nello scenario in cui i pod master viene riavviato, la sessione di Spark potrebbe non riuscire con `NoRoteToHostException`. Questo problema è causato dalla cache JVM non aggiornati con nuovo indirizzo IP indirizzi.

- Se hai Jupyter già installato e Python separato in Windows, i notebook Spark potrebbero non riuscire. Per risolvere questo problema, eseguire l'aggiornamento di Jupyter per la versione più recente.

- In un notebook, se si sceglie la **Aggiungi testo** comando, la cella di testo viene aggiunto in modalità anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per attivare/disattivare per la modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se facendo clic su un file in HDFS per visualizzarlo in anteprima, si potrebbe essere visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima file di dimensioni superiori a 30 MB in Azure Data Studio.

- Modifiche di configurazione HDFS che implicano modifiche alle hdfs-Site. XML non sono supportate.

#### <a name="security"></a>Sicurezza

- Il SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo di alimentazione). È necessario reimpostare il SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug, ma un passaggio di sicurezza. Per altre informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [modificare la password SA](../linux/quickstart-install-connect-docker.md#sapassword).

- I log di servizio contenitore di AZURE possono contenere la password dell'amministratore di sistema per le distribuzioni cluster di big data.

## <a id="ctp21"></a> CTP 2.1 (novembre 2018)

Le sezioni seguenti descrivono le nuove funzionalità e problemi noti per i cluster di big data in SQL Server 2019 CTP 2.1.

### <a name="new-features"></a>Nuove funzionalità

- [Distribuisci App Python e R](big-data-cluster-create-apps.md) in un cluster di big data.
- Nuova versione di **mssqlctl** e aggiornate le immagini. 
- Varie correzioni di bug e miglioramenti.

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti riportano i problemi noti per i cluster di big data di SQL Server in CTP 2.1.

#### <a name="deployment"></a>Distribuzione

- Aggiornamento di un cluster di dati dei big data da una versione precedente non è supportato. È necessario eseguire il backup ed eliminare qualsiasi cluster di big data esistente prima di distribuire la versione più recente. Per altre informazioni, vedere [esegue l'aggiornamento a una nuova versione](deployment-upgrade.md).

- Dopo la distribuzione nel servizio contenitore di AZURE, è possibile visualizzare i seguenti due eventi di avviso dalla distribuzione. Entrambi questi eventi sono presenti problemi noti, ma non impediscono è avere distribuito il cluster di big data nel servizio contenitore di AZURE.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- In caso di una distribuzione cluster con i big data, non viene rimosso lo spazio dei nomi associato. Ciò può comportare uno spazio dei nomi orfano sul cluster. Soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="admin-portal"></a>Portale di amministrazione

- Quando si [creare un'app usando il comando msqlctl ctp](big-data-cluster-create-apps.md) e distribuirla in un cluster di big data, il portale di amministrazione del Cluster Mostra i POD in cui l'applicazione è stata distribuita come "Sconosciuto" nella sezione Controller della porzione di amministrazione di SQL Server.

#### <a name="external-tables"></a>Tabelle esterne

- È possibile creare una tabella esterna di pool di dati per una tabella che contiene i tipi di colonna non supportati. Se si esegue una query della tabella esterna, viene visualizzato un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query una tabella esterna del pool di archiviazione, è possibile ottenere un errore se vengono copiato i file sottostante in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebook

- Gli indirizzi IP del POD possono cambiare nell'ambiente di Kubernetes come riavvii POD. Nello scenario in cui i pod master viene riavviato, la sessione di Spark potrebbe non riuscire con `NoRoteToHostException`. Questo problema è causato dalla cache JVM non aggiornati con nuovo indirizzo IP indirizzi.

- Se hai Jupyter già installato e Python separato in Windows, i notebook Spark potrebbero non riuscire. Per risolvere questo problema, eseguire l'aggiornamento di Jupyter per la versione più recente.

- In un notebook, se si sceglie la **Aggiungi testo** comando, la cella di testo viene aggiunto in modalità anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per attivare/disattivare per la modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se facendo clic su un file in HDFS per visualizzarlo in anteprima, si potrebbe essere visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima file di dimensioni superiori a 30 MB in Azure Data Studio.

- Modifiche di configurazione HDFS che implicano modifiche alle hdfs-Site. XML non sono supportate.

#### <a name="security"></a>Sicurezza

- Il SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo di alimentazione). È necessario reimpostare il SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug, ma un passaggio di sicurezza. Per altre informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [modificare la password SA](../linux/quickstart-install-connect-docker.md#sapassword).

- I log di servizio contenitore di AZURE possono contenere la password dell'amministratore di sistema per le distribuzioni cluster di big data.

## <a id="ctp20"></a> CTP 2.0 (ottobre 2018)

Le sezioni seguenti descrivono le nuove funzionalità e problemi noti per i cluster di big data in SQL Server 2019 CTP 2.0.

### <a name="new-features"></a>Nuove funzionalità

- Esperienza di distribuzione semplice usando lo strumento di gestione mssqlctl
- Esperienza notebook nativa in Azure Data Studio
- Eseguire query sui file HDFS tramite archiviazione istanza di SQL Server
- Virtualizzazione dei dati tramite master per SQL Server, Oracle, MongoDB e HDFS
- Procedura guidata di virtualizzazione dei dati per SQL Server e Oracle in Azure Data Studio
- Servizi di Machine Learning nel master
- Portale di amministrazione che è possibile usare per il monitoraggio e risoluzione dei problemi del cluster
- Invia processo Spark in Azure Data Studio 
- Interfaccia utente di Spark nel portale di amministrazione del cluster
- Volumi di montaggio per le classi di archiviazione
- Eseguire query sui pool di dati dal master
- Visualizza il piano di query distribuite in SQL Server Management Studio
- Pacchetto PIP per mssqlctl management tool
- Motore integrato per la distribuzione tramite il servizio controller

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti riportano i problemi noti per i cluster di big data di SQL Server nella versione CTP 2.0.

#### <a name="deployment"></a>Distribuzione

- Se si usa Azure Kubernetes Service (AKS), la versione consigliata di Kubernetes è 1.10. *, che non supporta il ridimensionamento del disco. È necessario assicurarsi di conseguenza si ridimensionano lo spazio di archiviazione in fase di distribuzione. Per altre informazioni su come regolare le dimensioni di archiviazione, vedere la [persistenza dei dati](concept-data-persistence.md) articolo. Per Kubernetes distribuito in macchine virtuali, la versione consigliata è 1.11.

- Dopo la distribuzione nel servizio contenitore di AZURE, è possibile visualizzare i seguenti due eventi di avviso dalla distribuzione. Entrambi questi eventi sono presenti problemi noti, ma non impediscono è avere distribuito il cluster di big data nel servizio contenitore di AZURE.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- In caso di una distribuzione cluster con i big data, non viene rimosso lo spazio dei nomi associato. Ciò può comportare uno spazio dei nomi orfano sul cluster. Soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="external-tables"></a>Tabelle esterne

- È possibile creare una tabella esterna di pool di dati per una tabella che contiene i tipi di colonna non supportati. Se si esegue una query della tabella esterna, viene visualizzato un messaggio simile al seguente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se si esegue una query una tabella esterna del pool di archiviazione, è possibile ottenere un errore se vengono copiato i file sottostante in HDFS nello stesso momento.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebook

- Gli indirizzi IP del POD possono cambiare nell'ambiente di Kubernetes come riavvii POD. Nello scenario in cui i pod master viene riavviato, la sessione di Spark potrebbe non riuscire con `NoRoteToHostException`. Questo problema è causato dalla cache JVM non aggiornati con nuovo indirizzo IP indirizzi.

- Se hai Jupyter già installato e Python separato in Windows, i notebook Spark potrebbero non riuscire. Per risolvere questo problema, eseguire l'aggiornamento di Jupyter per la versione più recente.

- In un notebook, se si sceglie la **Aggiungi testo** comando, la cella di testo viene aggiunto in modalità anteprima anziché in modalità di modifica. È possibile fare clic sull'icona di anteprima per attivare/disattivare per la modalità di modifica e modificare la cella.

#### <a name="hdfs"></a>HDFS

- Se facendo clic su un file in HDFS per visualizzarlo in anteprima, si potrebbe essere visualizzato l'errore seguente:

   `Error previewing file: File exceeds max size of 30MB`

   Attualmente non è possibile visualizzare in anteprima file di dimensioni superiori a 30 MB in Azure Data Studio.

- Modifiche di configurazione HDFS che implicano modifiche alle hdfs-Site. XML non sono supportate.

#### <a name="security"></a>Sicurezza

- Il SA_PASSWORD fa parte dell'ambiente e individuabile (ad esempio in un file di dump del cavo di alimentazione). È necessario reimpostare il SA_PASSWORD nell'istanza master dopo la distribuzione. Questo non è un bug, ma un passaggio di sicurezza. Per altre informazioni su come modificare il SA_PASSWORD in un contenitore Linux, vedere [modificare la password SA](../linux/quickstart-install-connect-docker.md#sapassword).

- I log di servizio contenitore di AZURE possono contenere la password dell'amministratore di sistema per le distribuzioni cluster di big data.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster dei big data a SQL Server, vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).
