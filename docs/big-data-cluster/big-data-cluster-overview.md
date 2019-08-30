---
title: Che cosa sono i cluster di Big Data?
titleSuffix: SQL Server Big Data Clusters
description: Scopri di [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] più su (anteprima) eseguibili in Kubernetes e fornisci opzioni di scalabilità orizzontale per i dati relazionali e HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c75005c35e743a87ff742352946c4fdde5fcf0b8
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153657"
---
# <a name="what-are-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Che cosa [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]sono?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

A partire [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]da [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] , è possibile distribuire cluster scalabili di contenitori SQL Server, Spark e HDFS in esecuzione in Kubernetes. Questi componenti vengono eseguiti in modo affiancato per permettere la lettura, la scrittura e l'elaborazione di Big Data da Transact-SQL o Spark, in modo da combinare e analizzare facilmente i dati relazionali di alto valore con volumi elevati di Big Data.

Per altre informazioni sulle nuove funzionalità e sui problemi noti per l'ultima versione, vedere le [note sulla versione](release-notes-big-data-cluster.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>Scenari

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]fornire flessibilità nella modalità di interazione con il Big Data. È possibile eseguire query su origini dati esterne, archiviare Big Data in HDFS gestito da SQL Server o eseguire query sui dati da più origini dati esterne tramite il cluster. È quindi possibile usare i dati per intelligenza artificiale, Machine Learning e altre attività di analisi. Le sezioni seguenti forniscono altre informazioni su questi scenari.

### <a name="data-virtualization"></a>Virtualizzazione dei dati

Sfruttando [SQL Server polibase](../relational-databases/polybase/polybase-guide.md), [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] è in grado di eseguire query sulle origini dati esterne senza dover eseguire lo spostamenti o la copia dei dati. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] introduce nuovi connettori alle origini dati.

![Virtualizzazione dei dati](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data lake

Un cluster Big Data di SQL Server include un *pool di archiviazione* HDFS scalabile. Questo pool può essere usato per archiviare Big Data, potenzialmente inseriti da più origini esterne. Una volta archiviati i Big Data in HDFS nel cluster Big Data, è possibile analizzare ed eseguire query sui dati e combinarli con i dati relazionali.

![Data lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>Data mart con scalabilità orizzontale

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]fornire risorse di calcolo e archiviazione con scalabilità orizzontale per migliorare le prestazioni di analisi dei dati. È possibile inserire e distribuire dati provenienti da diverse origini tra più nodi di *pool dati* come cache per ulteriori analisi.

![Data mart](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>Intelligenza artificiale e Machine Learning integrati

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]abilitare le attività di intelligenza artificiale e di machine learning sui dati archiviati nei pool di archiviazione HDFS e nei pool di dati. È anche possibile usare Spark nonché strumenti di intelligenza artificiale predefiniti in SQL Server, tramite R, Python, Scala o Java.

![Intelligenza artificiale e Machine Learning](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>Gestione e monitoraggio

La gestione e il monitoraggio vengono forniti tramite una combinazione di strumenti da riga di comando, API, portali e viste a gestione dinamica.

È possibile usare Azure Data Studio per eseguire un'ampia gamma di attività sul cluster Big Data. Tutto questo viene reso possibile dalla nuova **estensione di SQL Server 2019 (anteprima)** . L'estensione offre quanto segue:

- Frammenti predefiniti per attività di gestione comuni.
- Possibilità di esplorare HDFS, caricare file, visualizzare file in anteprima e creare directory.
- Possibilità di creare, aprire ed eseguire notebook compatibili con Jupyter.
- Procedura guidata di virtualizzazione dei dati per semplificare la creazione di origini dati esterne.

## <a id="architecture"></a> Architettura

Un cluster Big Data di SQL Server è un cluster di contenitori Linux orchestrati da [Kubernetes](https://kubernetes.io/docs/concepts/).

### <a name="kubernetes-concepts"></a>Concetti relativi a Kubernetes

Kubernetes è un agente di orchestrazione di contenitori open source, che può ridimensionare le distribuzioni di contenitori in base alle esigenze. La tabella seguente definisce alcuni importanti termini di Kubernetes:

|||
|:--|:--|
| **Cluster** | Un cluster Kubernetes è un set di computer, noti come nodi. Un nodo controlla il cluster e viene designato come nodo master, mentre i nodi rimanenti sono nodi di lavoro. Il nodo master Kubernetes è responsabile della distribuzione del lavoro tra i nodi di lavoro e del monitoraggio dell'integrità del cluster. |
| **Node** | Un nodo esegue applicazioni in contenitori. Può essere un computer fisico o una macchina virtuale. Un cluster Kubernetes può contenere una combinazione di nodi computer fisico e macchina virtuale. |
| **Pod** | Un pod è l'unità di distribuzione atomica di Kubernetes. Un pod è un gruppo logico di uno o più contenitori, nonché delle risorse associate, necessari per eseguire un'applicazione. Ogni pod viene eseguito in un nodo e un nodo può eseguire uno o più pod. Il nodo master Kubernetes assegna automaticamente pod a nodi nel cluster. |
| &nbsp; ||

In [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], Kubernetes è responsabile dello stato [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]di; Kubernetes compila e configura i nodi del cluster, assegna i pod ai nodi e monitora l'integrità del cluster.

### <a name="big-data-clusters-architecture"></a>Architettura dei cluster Big Data

Il diagramma seguente mostra i componenti di un cluster Big Data per SQL Server.

![Panoramica dell'architettura](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a> Controller

Il controller fornisce la gestione e la sicurezza per il cluster. Contiene il servizio cntrol, l'archivio di configurazione e altri servizi a livello di cluster, tra cui Kibana, Grafana ed Elasticsearch.

### <a id="computeplane"></a> Pool di calcolo

Il pool di calcolo fornisce risorse di calcolo al cluster. Contiene nodi che eseguono SQL Server in pod Linux. I Pod nel pool di calcolo sono divisi in *istanze di calcolo SQL* per attività di elaborazione specifiche. 

### <a id="dataplane"></a> Pool di dati

Il pool di dati viene usato per il salvataggio permanente e la memorizzazione nella cache dei dati. Il pool di dati è costituito da uno o più pod che eseguono SQL Server in Linux. Viene usato per inserire dati da query SQL o processi Spark. I data mart del cluster Big Data di SQL Server vengono salvati in modo permanente nel pool di dati. 

### <a name="storage-pool"></a>Pool di archiviazione

Il pool di archiviazione è formato da pod del pool di archiviazione costituiti da SQL Server in Linux, Spark, and HDFS. Tutti i nodi di archiviazione in un cluster Big Data di SQL Server sono membri di un cluster HDFS.

> [!TIP]
> Per informazioni dettagliate sull'architettura e sull'installazione dei cluster Big Data, vedere [Workshop: [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Architettura](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)Microsoft.

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]è disponibile per la prima volta come anteprima pubblica limitata tramite il programma di adozione anticipata SQL Server 2019. Per richiedere l'accesso, eseguire la registrazione [qui](https://aka.ms/eapsignup), specificando l'interesse a provare i cluster Big Data. Microsoft valuterà tutte le richieste e risponderà non appena possibile.
