---
title: Configurare la suddivisione in livelli HDFS
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come configurare la suddivisione in livelli HDFS per montare un file system di Azure Data Lake Storage esterno in HDFS in un'istanza di [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 673b3eed760af4b36c494e2dd45cdfc8ed8e8dc8
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706052"
---
# <a name="configure-hdfs-tiering-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Configurare la suddivisione in livelli HDFS in [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

La suddivisione in livelli HDFS offre la possibilità di montare in HDFS un file system esterno compatibile con HDFS. Questo articolo illustra come configurare la suddivisione in livelli HDFS per i cluster Big Data di SQL Server. Al momento, è supportata la connessione ad Azure Data Lake Storage Gen2 e Amazon S3. 

## <a name="hdfs-tiering-overview"></a>Panoramica della suddivisione in livelli HDFS

Con la suddivisione in livelli, le applicazioni possono accedere facilmente ai dati in un'ampia gamma di archivi esterni come se i dati si trovassero in HDFS in locale. Il montaggio è un'operazione sui metadati, in cui i metadati che descrivono lo spazio dei nomi nel file system esterno vengono copiati in HDFS in locale. Questi metadati includono informazioni sulle directory e sui file esterni insieme ai relativi elenchi di controllo di accesso e autorizzazioni. I dati corrispondenti vengono copiati solo su richiesta quando si accede ai dati, ad esempio con una query. È ora possibile accedere ai dati del file system esterno dal cluster Big Data di SQL Server. È possibile eseguire processi Spark e query SQL su questi dati nello stesso modo in cui si eseguono sui dati locali archiviati in HDFS nel cluster.

### <a name="caching"></a>Memorizzazione nella cache
Attualmente, per impostazione predefinita, l'1% dello spazio di archiviazione HDFS totale viene riservato per la memorizzazione nella cache dei dati montati. La memorizzazione nella cache è un'impostazione globale per tutti i montaggi.

> [!NOTE]
> La suddivisione in livelli HDFS è una funzionalità sviluppata da Microsoft e una sua versione precedente è stata rilasciata come parte della distribuzione di Apache Hadoop 3.1. Per altre informazioni, vedere [https://issues.apache.org/jira/browse/HDFS-9806](https://issues.apache.org/jira/browse/HDFS-9806).

Le sezioni seguenti forniscono un esempio di come configurare la suddivisione in livelli HDFS con un'origine dati Azure Data Lake Storage Gen2.

## <a name="refresh"></a>Aggiorna

La suddivisione in livelli HDFS supporta l'aggiornamento. Aggiornare un montaggio esistente per ottenere lo snapshot più recente dei dati remoti.

## <a name="prerequisites"></a>Prerequisites

- [Cluster Big Data distribuito](deployment-guidance.md)
- [Strumenti per Big Data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="mounting-instructions"></a>Istruzioni per il montaggio

È supportata la connessione ad Azure Data Lake Storage Gen2 e Amazon S3. Le istruzioni su come eseguire il montaggio in questi tipi di archiviazione sono disponibili negli articoli seguenti:

- [Come montare ADLS Gen2 per la suddivisione in livelli HDFS in un cluster Big Data](hdfs-tiering-mount-adlsgen2.md)
- [Come montare S3 per la suddivisione in livelli HDFS in un cluster Big Data](hdfs-tiering-mount-s3.md)

## <a id="issues"></a> Problemi noti e limitazioni

L'elenco seguente illustra i problemi noti e le attuali limitazioni quando si usa la suddivisione in livelli HDFS in [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]:

- Se il montaggio rimane bloccato in uno stato `CREATING` per molto tempo, è molto probabile che abbia avuto esito negativo. In questo caso, annullare il comando ed eliminare il montaggio, se necessario. Verificare che i parametri e le credenziali siano corretti prima di riprovare.

- I montaggi non possono essere creati nelle directory esistenti.

- I montaggi non possono essere creati all'interno di montaggi esistenti.

- Se uno dei predecessori del punto di montaggio non esiste, verrà creato con autorizzazioni predefinite r-xr-xr-x (555).

- La creazione del montaggio può richiedere del tempo, in base al numero e alle dimensioni dei file montati. Durante questo processo, i file nel montaggio non sono visibili agli utenti. Durante la creazione del montaggio, tutti i file verranno aggiunti a un percorso temporaneo, il cui valore predefinito è `/_temporary/_mounts/<mount-location>`.

- Il comando di creazione del montaggio è asincrono. Dopo l'esecuzione del comando, è possibile controllare lo stato di montaggio.

- Quando si crea il montaggio, l'argomento usato per **--mount-path** è essenzialmente un identificatore univoco del montaggio. La stessa stringa (inclusa la barra "/" alla fine, se presente) deve essere usata nei comandi successivi.

- I montaggi sono di sola lettura. Non è possibile creare directory o file in un montaggio.

- Non è consigliabile montare directory e file che possono cambiare. Dopo la creazione del montaggio, eventuali modifiche o aggiornamenti della posizione remota non verranno riflessi nel montaggio in HDFS. In caso di modifiche nella posizione remota, è possibile scegliere di eliminare e ricreare il montaggio per riflettere lo stato aggiornato.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
