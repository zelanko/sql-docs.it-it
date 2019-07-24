---
title: Che cosa sono i cluster Big Data?
titleSuffix: SQL Server big data clusters
description: Informazioni sui cluster SQL Server 2019 Big Data (anteprima) che vengono eseguiti in Kubernetes e offrono opzioni di scalabilità orizzontale per dati relazionali e HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0beb4ea57ba6c2591e5b2c06a7775fc2d7e8b26c
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419503"
---
# <a name="what-are-sql-server-big-data-clusters"></a>Cluster di Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

A partire [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]da, i cluster SQL Server Big Data consentono di distribuire cluster scalabili di contenitori SQL Server, Spark e HDFS in esecuzione in Kubernetes. Questi componenti vengono eseguiti side-by-side per consentire la lettura, la scrittura e l'elaborazione di Big Data da Transact-SQL o Spark, consentendo di combinare e analizzare facilmente i dati relazionali di alto valore con Big Data di volumi elevati.

Per ulteriori informazioni sulle nuove funzionalità e sui problemi noti per la versione più recente, vedere le [Note sulla versione](release-notes-big-data-cluster.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>Scenari

I cluster SQL Server Big Data offrono la flessibilità necessaria per interagire con il Big Data. È possibile eseguire query sulle origini dati esterne, archiviare Big Data in HDFS gestite da SQL Server o eseguire query sui dati da più origini dati esterne tramite il cluster. È quindi possibile usare i dati per intelligenza artificiale, Machine Learning e altre attività di analisi. Nelle sezioni seguenti vengono fornite ulteriori informazioni su questi scenari.

### <a name="data-virtualization"></a>Virtualizzazione dei dati

Sfruttando [SQL Server polibase](../relational-databases/polybase/polybase-guide.md), SQL Server i cluster Big data possono eseguire query sulle origini dati esterne senza dover trasferire o copiare i dati. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]introduce nuovi connettori per le origini dati.

![Virtualizzazione dei dati](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data Lake

Un cluster SQL Server Big Data include un pool di *archiviazione*HDFS scalabile. Questa operazione può essere usata per archiviare Big Data, potenzialmente inserite da più origini esterne. Una volta archiviato il Big Data in HDFS nel cluster Big Data, è possibile analizzare ed eseguire query sui dati e combinarli con i dati relazionali.

![Data Lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>Scalabilità orizzontale data mart

SQL Server cluster di Big Data offrono risorse di calcolo e archiviazione con scalabilità orizzontale per migliorare le prestazioni di analisi dei dati. I dati provenienti da un'ampia gamma di origini possono essere inseriti e distribuiti tra i nodi del *pool di dati* come cache per un'ulteriore analisi.

![Data Mart](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>Intelligenza artificiale integrata e Machine Learning

SQL Server cluster Big Data abilitano le attività di intelligenza artificiale e di machine learning sui dati archiviati nei pool di archiviazione HDFS e nei pool di dati. È possibile usare Spark e gli strumenti di intelligenza artificiale integrati in SQL Server, usando R, Python, scala o Java.

![Intelligenza artificiale e ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>Gestione e monitoraggio

La gestione e il monitoraggio sono forniti tramite una combinazione di strumenti da riga di comando, API, portali e viste a gestione dinamica.

È possibile usare Azure Data Studio per eseguire una serie di attività nel cluster Big Data. Questa funzionalità è abilitata dalla nuova **estensione SQL Server 2019 (anteprima)** . Questa estensione fornisce:

- Frammenti predefiniti per le attività di gestione comuni.
- Possibilità di esplorare HDFS, caricare file, visualizzare in anteprima i file e creare directory.
- Possibilità di creare, aprire ed eseguire notebook compatibili con Jupyter.
- Data Virtualization Wizard per semplificare la creazione di origini dati esterne.

## <a id="architecture"></a>Architettura

Un cluster SQL Server Big Data è un cluster di contenitori Linux orchestrati da [Kubernetes](https://kubernetes.io/docs/concepts/).

### <a name="kubernetes-concepts"></a>Concetti di Kubernetes

Kubernetes è un agente di orchestrazione di contenitori open source, che consente di ridimensionare le distribuzioni di contenitori in base alle esigenze. La tabella seguente definisce alcuni importanti termini di Kubernetes:

|||
|:--|:--|
| **Cluster** | Un cluster Kubernetes è un set di computer, noti come nodi. Un nodo controlla il cluster e viene designato come nodo master; i nodi rimanenti sono nodi di lavoro. Il Master Kubernetes è responsabile della distribuzione del lavoro tra i dipendenti e del monitoraggio dell'integrità del cluster. |
| **Node** | Un nodo esegue applicazioni incluse in contenitori. Può essere un computer fisico o una macchina virtuale. Un cluster Kubernetes può contenere una combinazione di nodi computer fisico e macchina virtuale. |
| **Pod** | Un pod è l'unità di distribuzione atomica di Kubernetes. Un pod è un gruppo logico di uno o più contenitori e risorse associate, necessari per eseguire un'applicazione. Ogni pod viene eseguito in un nodo; un nodo può eseguire uno o più POD. Il Master Kubernetes assegna automaticamente i pod ai nodi del cluster. |
| &nbsp; ||

In SQL Server cluster Big Data, Kubernetes è responsabile dello stato dei cluster di Big Data di SQL Server. Kubernetes compila e configura i nodi del cluster, assegna i pod ai nodi e monitora l'integrità del cluster.

### <a name="big-data-clusters-architecture"></a>Architettura di cluster di Big Data

Il diagramma seguente illustra i componenti di un cluster di Big Data per SQL Server.

![Panoramica dell'architettura](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a>Controller

Il controller fornisce la gestione e la sicurezza per il cluster. Contiene il servizio cntrol, l'archivio di configurazione e altri servizi a livello di cluster, ad esempio Kibana, Grafana e la ricerca elastica.

### <a id="computeplane"></a>Pool di calcolo

Il pool di calcolo fornisce risorse di calcolo al cluster. Contiene nodi che eseguono SQL Server in Linux pod. I Pod nel pool di calcolo sono divisi in *istanze di calcolo SQL* per attività di elaborazione specifiche. 

### <a id="dataplane"></a>Pool di dati

Il pool di dati viene utilizzato per la persistenza e la memorizzazione nella cache dei dati. Il pool di dati è costituito da uno o più pod in esecuzione SQL Server in Linux. Viene usato per inserire dati da query SQL o processi Spark. SQL Server i Data Mart del cluster Big Data sono salvati in permanenza nel pool di dati. 

### <a name="storage-pool"></a>Pool di archiviazione

Il pool di archiviazione è costituito da Pod del pool di archiviazione costituiti da SQL Server in Linux, Spark e HDFS. Tutti i nodi di archiviazione in un cluster SQL Server Big Data sono membri di un cluster HDFS.

> [!TIP]
> Per informazioni dettagliate sull'architettura e sull'installazione di Big Data cluster, vedere [workshop: Microsoft SQL Server architettura](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)Big Data cluster.

## <a name="next-steps"></a>Passaggi successivi

SQL Server cluster Big Data è disponibile per la prima volta come anteprima pubblica limitata tramite il programma di adozione anticipato SQL Server 2019. Per richiedere l'accesso, registrarsi [qui](https://aka.ms/eapsignup)e specificare l'interesse per provare a Big Data cluster. Microsoft effettuerà la valutazione di tutte le richieste e risponderà il prima possibile.
