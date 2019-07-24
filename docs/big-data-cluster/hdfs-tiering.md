---
title: Configurare la suddivisione in livelli HDFS
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come configurare la suddivisione in livelli di HDFS per montare un file system di Azure Data Lake Storage esterno in HDFS in un cluster Big Data SQL Server 2019 (anteprima).
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 17eedf9f0797a0adb5eda6ca8ee090fc762e1491
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419382"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>Configurare la suddivisione in livelli di HDFS nei cluster SQL Server Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

La suddivisione in livelli di HDFS offre la possibilità di montare file system esterni compatibili con HDFS in HDFS. Questo articolo illustra come configurare la suddivisione in livelli di HDFS per SQL Server cluster 2019 Big Data (anteprima). A questo punto, è supportata la connessione a Azure Data Lake Storage Gen2 e Amazon S3. 

## <a name="hdfs-tiering-overview"></a>Panoramica sulla suddivisione in livelli HDFS

Con la suddivisione in livelli, le applicazioni possono accedere facilmente ai dati in un'ampia gamma di archivi esterni come se i dati risiedano nella HDFS locale. Il montaggio è un'operazione di metadati, in cui i metadati che descrivono lo spazio dei nomi nel file system esterno vengono copiati nel HDFS locale. Questi metadati includono informazioni sulle directory e i file esterni insieme alle relative autorizzazioni e ACL. I dati corrispondenti vengono copiati su richiesta solo quando si accede ai dati, ad esempio una query. È ora possibile accedere ai dati del file System esterno dal cluster SQL Server Big Data. È possibile eseguire processi Spark e query SQL su questi dati nello stesso modo in cui vengono eseguiti nei dati locali archiviati in HDFS nel cluster.

### <a name="caching"></a>Memorizzazione nella cache
Attualmente, per impostazione predefinita, l'1% dello spazio di archiviazione HDFS totale sarà riservato per la memorizzazione nella cache dei dati montati. La memorizzazione nella cache è un'impostazione globale tra i montaggi.

> [!NOTE]
> La suddivisione in livelli di HDFS è una funzionalità sviluppata da Microsoft e una versione precedente è stata rilasciata come parte della distribuzione di Apache Hadoop 3,1. Per ulteriori informazioni, vedere [https://issues.apache.org/jira/browse/HDFS-9806](https://issues.apache.org/jira/browse/HDFS-9806) per informazioni dettagliate.

Le sezioni seguenti forniscono un esempio di come configurare la suddivisione in livelli di HDFS con un'origine dati Azure Data Lake Storage Gen2.

## <a name="refresh"></a>Aggiorna

La suddivisione in livelli di HDFS supporta l'aggiornamento. Aggiornare un montaggio esistente per l'ultimo snapshot dei dati remoti.

## <a name="prerequisites"></a>Prerequisiti

- [Cluster Big Data distribuito](deployment-guidance.md)
- [Strumenti per Big Data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="mounting-instructions"></a>Istruzioni di montaggio

È supportata la connessione a Azure Data Lake Storage Gen2 e Amazon S3. Le istruzioni su come eseguire il montaggio in questi tipi di archiviazione sono disponibili negli articoli seguenti:

- [Come montare ADLS Gen2 per la suddivisione in livelli di HDFS in un cluster Big Data](hdfs-tiering-mount-adlsgen2.md)
- [Come montare S3 per la suddivisione in livelli di HDFS in un cluster Big Data](hdfs-tiering-mount-s3.md)

## <a id="issues"></a>Problemi noti e limitazioni

L'elenco seguente fornisce problemi noti e limitazioni correnti quando si usa la suddivisione in livelli di HDFS in SQL Server Big Data cluster:

- Se il montaggio è bloccato in uno `CREATING` stato da molto tempo, è molto probabile che abbia esito negativo. In questa situazione, annullare il comando ed eliminare il montaggio se necessario. Verificare che i parametri e le credenziali siano corretti prima di riprovare.

- Non è possibile creare montaggi nelle directory esistenti.

- Non è possibile creare montaggi nei montaggi esistenti.

- Se uno dei predecessori del punto di montaggio non esiste, verranno creati con le autorizzazioni assegnate per impostazione predefinita a r-xr-xr-x (555).

- La creazione del montaggio può richiedere del tempo in base al numero e alle dimensioni dei file montati. Durante questo processo, i file nel montaggio non sono visibili agli utenti. Durante la creazione del montaggio, tutti i file verranno aggiunti a un percorso temporaneo, il cui valore predefinito `/_temporary/_mounts/<mount-location>`è.

- Il comando di creazione montaggio è asincrono. Dopo l'esecuzione del comando, è possibile controllare lo stato di montaggio per comprendere lo stato del montaggio.

- Quando si crea il montaggio, l'argomento usato per **--Mount-Path** è essenzialmente un identificatore univoco del montaggio. La stessa stringa (incluso "/" alla fine se presente) deve essere utilizzata nei comandi successivi.

- I montaggi sono di sola lettura. Non è possibile creare directory o file in un montaggio.

- Non è consigliabile installare Directory e file che possono cambiare. Dopo la creazione del montaggio, eventuali modifiche o aggiornamenti della posizione remota non verranno riflesse nel montaggio in HDFS. Se si verificano modifiche nella posizione remota, è possibile scegliere di eliminare e ricreare il montaggio per riflettere lo stato aggiornato.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster SQL Server 2019 Big Data, vedere [che cosa sono i cluster SQL Server 2019 Big Data?](big-data-cluster-overview.md).
