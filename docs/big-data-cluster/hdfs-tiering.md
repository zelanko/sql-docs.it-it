---
title: Configurare la suddivisione in livelli di HDFS
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come configurare la suddivisione in livelli per montare un file system di archivio Azure Data Lake esterni in HDFS in un cluster di big data (anteprima) di SQL Server 2019 HDFS.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
manager: jroth
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 823e24b4ec78996140fa3f17cef9c1e56365a3f7
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728741"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>Configurare la suddivisione in livelli nel cluster di big data di SQL Server HDFS

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

La suddivisione in livelli di HDFS offre la possibilità di montaggio esterni, compatibile con HDFS file system HDFS. Questo articolo illustra come configurare HDFS la suddivisione in livelli per i cluster di big data di SQL Server 2019 (anteprima). A questo punto, Supportiamo la connessione a Azure Data Lake Storage Gen2 e Amazon S3. 

## <a name="hdfs-tiering-overview"></a>Cenni preliminari sulla suddivisione in livelli di HDFS

Con la suddivisione in livelli, le applicazioni possono accedere con facilità i dati in un'ampia gamma di archivi esterni come se i dati risiedono in al sistema HDFS locale. Il montaggio è un'operazione di metadati, in cui viene copiato i metadati che descrive lo spazio dei nomi per il sistema di file esterno per il sistema HDFS locale. Questi metadati includono informazioni sulle directory esterne e i file con le autorizzazioni e gli ACL. I dati corrispondenti sono solo copiati su richiesta, quando si accede ai dati stessi attraverso, ad esempio una query. I dati di sistema di file esterno sono ora accessibile dal cluster di big data di SQL Server. È possibile eseguire Spark processi e le query SQL in merito ai dati nello stesso modo che è necessario eseguirli su eventuali dati locali archiviati in HDFS nel cluster.

### <a name="caching"></a>Memorizzazione nella cache
Attualmente, per impostazione predefinita, 1% dello spazio di archiviazione HDFS totale verrà riservato per la memorizzazione nella cache dei dati montati. La memorizzazione nella cache è un'impostazione globale nei punti di montaggio.

> [!NOTE]
> La suddivisione in livelli di HDFS è una funzionalità sviluppata da Microsoft e una versione precedente di esso è stata rilasciata come parte della distribuzione di Apache Hadoop 3.1. Per altre informazioni, vedere [ https://issues.apache.org/jira/browse/HDFS-9806 ](https://issues.apache.org/jira/browse/HDFS-9806) per informazioni dettagliate.

Le sezioni seguenti forniscono un esempio di come configurare la suddivisione in livelli con un'origine dati di Azure Data Lake Storage Gen2 HDFS.

## <a name="prerequisites"></a>Prerequisiti

- [Cluster di big data distribuita](deployment-guidance.md)
- [Strumenti dei big Data](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a name="mounting-instructions"></a>Istruzioni sul montaggio

Supportiamo la connessione a Azure Data Lake Storage Gen2 e Amazon S3. Istruzioni su come montare contro questi tipi di archiviazione sono disponibili negli articoli seguenti:

- [Come Azure Data Lake Store montaggio Gen2 per HDFS la suddivisione in livelli in un cluster di big data](hdfs-tiering-mount-adlsgen2.md)
- [Come montare S3 per HDFS la suddivisione in livelli in un cluster di big data](hdfs-tiering-mount-s3.md)

## <a id="issues"></a> Problemi noti e limitazioni

Quando si usa HDFS la suddivisione in livelli nel cluster di big data di SQL Server nell'elenco seguente offre i problemi noti e sulle limitazioni attuali:

- Se il montaggio è bloccato in un `CREATING` sullo stato per un lungo periodo di tempo, molto probabilmente non è riuscito. In questo caso, annullare il comando ed eliminare il montaggio, se necessario. Verificare che i parametri e le credenziali siano corrette prima di riprovare.

- Impossibile creare punti di montaggio di directory esistenti.

- Impossibile creare punti di montaggio all'interno di punti di montaggio esistente.

- Se uno dei predecessori del punto di montaggio non esiste, verrà creati con le autorizzazioni impostate come predefinite per r-xr-xr-x (555).

- La creazione di montaggio può richiedere tempo a seconda del numero e dimensioni dei file in cui vengono montati. Durante questo processo, i file sotto il montaggio non sono visibili agli utenti. Mentre viene creato il montaggio, tutti i file verranno aggiunti a un percorso temporaneo, che per impostazione predefinita `/_temporary/_mounts/<mount-location>`.

- Il comando di creazione di montaggio è asincrono. Dopo il comando viene eseguito, lo stato di montaggio può essere controllato per comprendere lo stato del montaggio.

- Quando si crea il montaggio, utilizzato per l'argomento **-percorso di montaggio** è essenzialmente un identificatore univoco del montaggio. La stessa stringa (tra cui "/" alla fine, se presente) deve essere usata nei comandi successivi.

- I punti di montaggio sono di sola lettura. Non è possibile creare alcuna directory o file in un montaggio.

- Si sconsiglia di directory di montaggio e i file che possono cambiare. Dopo aver creato il montaggio, eventuali modifiche o aggiornamenti alla sede remota non si rifletteranno nel montaggio in HDFS. Se vengono apportate modifiche nella posizione remota, è possibile eliminare e ricreare il montaggio in modo da riflettere lo stato aggiornato.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di SQL Server 2019 dei big data, vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).
