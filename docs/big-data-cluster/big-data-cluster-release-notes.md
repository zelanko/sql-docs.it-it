---
title: Note sulla versione
titleSuffix: SQL Server 2019 big data clusters
description: Questo articolo descrive gli ultimi aggiornamenti e problemi noti per i cluster di big data di SQL Server 2019 (anteprima).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 8c9c57e641c76f78bf66565cc8e1ce8f67323b7e
ms.sourcegitcommit: 3f19c843b38d3835d07921612f0143620eb9a0e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53709814"
---
# <a name="release-notes-for-sql-server-2019-big-data-clusters"></a>Note sulla versione per i cluster di SQL Server 2019 dei big Data

Questo articolo fornisce gli ultimi aggiornamenti e problemi noti per la versione più recente di SQL Server cluster di big data. Il tabella seguente include collegamenti per la sezione delle versioni illustrati in questo articolo.

| Versione | date |
|---|---|
| [CTP 2.2](#ctp22) | Dicembre 2018 |
| [CTP 2.1](#ctp21) | Novembre 2018 |
| [CTP 2.0](#ctp20) | Ottobre 2018 |

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp22"></a> CTP 2.2 (dicembre 2018)

Le sezioni seguenti descrivono le nuove funzionalità e problemi noti per i cluster di big data in SQL Server 2019 CTP 2.2.

### <a name="whats-in-the-ctp-22-release"></a>Che cos'è la versione CTP 2.2?

- Accedere al portale di amministrazione di cluster con `/portal` (**https://\<ip-address\>: 30777/portale**).
- Nome del servizio pool master modificata `service-master-pool-lb` e `service-master-pool-nodeport` a `endpoint-master-pool`.
- Nuova versione di **mssqlctl** e aggiornate le immagini.
- Varie correzioni di bug e miglioramenti.

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti riportano i problemi noti per i cluster di big data di SQL Server CTP 2.2.

#### <a name="deployment"></a>Distribuzione

- Aggiornamento di un cluster di dati dei big data da una versione precedente non è supportato. È necessario eseguire il backup ed eliminare qualsiasi cluster di big data esistente prima di distribuire la versione più recente. Per altre informazioni, vedere [esegue l'aggiornamento a una nuova versione](deployment-guidance.md#upgrade).

- Dopo la distribuzione nel servizio contenitore di AZURE, è possibile visualizzare i seguenti due eventi di avviso dalla distribuzione. Entrambi questi eventi sono presenti problemi noti, ma non impediscono è avere distribuito il cluster di big data nel servizio contenitore di AZURE.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- In caso di una distribuzione cluster con i big data, non viene rimosso lo spazio dei nomi associato. Ciò può comportare uno spazio dei nomi orfano sul cluster. Soluzione alternativa consiste nell'eliminare manualmente lo spazio dei nomi prima di distribuire un cluster con lo stesso nome.

#### <a name="cluster-administration-portal"></a>Portale di amministrazione cluster

Nel portale di amministrazione cluster non viene visualizzata l'endpoint per l'istanza master di SQL Server. Per trovare l'indirizzo IP e la porta per l'istanza master, usare il comando seguente **kubectl** comando:

```
kubectl get svc endpoint-master-pool -n <your-cluster-name>
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

### <a name="whats-in-the-ctp-21-release"></a>Che cos'è la versione CTP 2.1?

- [Distribuisci App Python e R](big-data-cluster-create-apps.md) in un cluster di big data.
- Nuova versione di **mssqlctl** e aggiornate le immagini. 
- Varie correzioni di bug e miglioramenti.

### <a name="known-issues"></a>Problemi noti

Le sezioni seguenti riportano i problemi noti per i cluster di big data di SQL Server in CTP 2.1.

#### <a name="deployment"></a>Distribuzione

- Aggiornamento di un cluster di dati dei big data da una versione precedente non è supportato. È necessario eseguire il backup ed eliminare qualsiasi cluster di big data esistente prima di distribuire la versione più recente. Per altre informazioni, vedere [esegue l'aggiornamento a una nuova versione](deployment-guidance.md#upgrade).

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

### <a name="whats-in-the-ctp-20-release"></a>Che cos'è la versione CTP 2.0?

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
