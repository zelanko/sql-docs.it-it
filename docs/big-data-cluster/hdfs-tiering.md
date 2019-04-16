---
title: Configurare la suddivisione in livelli di HDFS
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come configurare la suddivisione in livelli per montare un file system di archivio Azure Data Lake esterni in HDFS in un cluster di big data (anteprima) di SQL Server 2019 HDFS.
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 32648829c64143b4f31a5d27479bbc3d28076fa2
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582424"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>Configurare la suddivisione in livelli nel cluster di big data di SQL Server HDFS

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

La suddivisione in livelli di HDFS offre la possibilità di montaggio esterni, compatibile con HDFS file system HDFS. Questo articolo illustra come configurare HDFS la suddivisione in livelli per i cluster di big data di SQL Server 2019 (anteprima). A questo punto, CTP 2.4 supporta solo la connessione a Azure Data Lake Storage Gen2, che è l'obiettivo di questo articolo.

## <a name="hdfs-tiering-overview"></a>Cenni preliminari sulla suddivisione in livelli di HDFS

Con la suddivisione in livelli, le applicazioni possono accedere con facilità i dati in un'ampia gamma di archivi esterni come se i dati risiedono in HDFS. Il montaggio è un'operazione di metadati, in cui i metadati che descrivono lo spazio dei nomi nel file esterno system viene copiato in HDFS. Questi metadati includono informazioni sulle directory esterne e i file con le autorizzazioni e gli ACL. I dati corrispondenti sono solo copiati su richiesta, quando si accede ai dati stessi. I dati di sistema di file esterno sono ora accessibile dal cluster di big data di SQL Server. È possibile eseguire Spark processi e le query SQL in merito ai dati nello stesso modo che è necessario eseguirli su eventuali dati locali archiviati in HDFS nel cluster.

> [!NOTE]
> La suddivisione in livelli di HDFS è una funzionalità sviluppata da Microsoft e una versione precedente di esso è stata rilasciata come parte della distribuzione di Apache Hadoop 3.1. Per altre informazioni, vedere [ https://issues.apache.org/jira/browse/HDFS-9806 ](https://issues.apache.org/jira/browse/HDFS-9806) per informazioni dettagliate.

Le sezioni seguenti forniscono un esempio di come configurare la suddivisione in livelli con un'origine dati di Azure Data Lake Storage Gen2 HDFS.

## <a name="prerequisites"></a>Prerequisiti

- [Cluster di big data distribuita](deployment-guidance.md)
- [Strumenti dei big Data](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a id="load"></a> Caricare i dati in archiviazione di Azure Data Lake

La sezione seguente descrive come configurare Azure Data Lake archiviazione Gen2 per testare la suddivisione in livelli di HDFS. Se si dispone già di dati archiviati in archiviazione di Azure Data Lake, è possibile ignorare questa sezione per usare i propri dati.

1. [Creare un account di archiviazione con funzionalità di Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. [Creare un contenitore blob](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) nell'account di archiviazione per i dati esterni.

1. Caricare un file CSV o Parquet nel contenitore. Si tratta dei dati HDFS esterni che verranno montati in HDFS nel cluster di big data.

## <a id="mount"></a> Montare l'archiviazione HDFS remoto

I passaggi seguenti montare l'archiviazione HDFS remoto in Azure Data Lake nella risorsa di archiviazione HDFS locale del cluster di big data.

1. Aprire un prompt dei comandi in un computer client che possa accedere al cluster di big data.

1. Creare un file locale denominato **files.creds** che contiene le credenziali dell'account Azure Data Lake Storage Gen2 usando il formato seguente:

   ```text
   fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

   > [!TIP]
   > Per altre informazioni su come trovare la chiave di accesso (`<storage-account-access-key>`) per l'account di archiviazione, vedere [visualizzare e copiare le chiavi di accesso](https://docs.microsoft.com/azure/storage/common/storage-account-manage?#view-and-copy-access-keys).

1. Uso **kubectl** per trovare l'indirizzo IP per il **endpoint-servizio-proxy** servizio nel cluster di big data. Cercare il **External-IP**.

   ```bash
   kubectl get svc endpoint-service-proxy -n <your-cluster-name>
   ```

1. Accedi con **mssqlctl** usando l'endpoint proxy del servizio con il nome utente del cluster e la password:

   ```bash
   mssqlctl login -e https://<IP-of-endpoint-service-proxy>:30777/ -u <username> -p <password>
   ```

1. Montare l'archiviazione HDFS remoto in Azure usando **montare archiviazione mssqlctl creare**. Prima di eseguire il comando seguente, sostituire i valori segnaposto:

   ```bash
   mssqlctl storage mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name> --credential-file <path-to-adls-credentials>/file.creds
   ```

   > [!NOTE]
   > Il montaggio di creare il comando è asincrona. A questo punto, non vi è alcun messaggio che indica se il montaggio ha avuto esito positivo. Vedere le [stato](#status) sezione per controllare lo stato dei punti di montaggio.

Se è stato montato, sarà possibile eseguire query sui dati HDFS ed eseguire i processi di Spark su di esso. Verrà visualizzata in HDFS per il cluster di big data nel percorso specificato dal `--local-path`.

## <a id="status"></a> Ottenere lo stato dei punti di montaggio

Per elencare lo stato di tutti i punti di montaggio del cluster di big data, usare il comando seguente:

```bash
mssqlctl storage mount status
```

Per elencare lo stato di un montaggio in un percorso specifico in HDFS, usare il comando seguente:

```bash
mssqlctl storage mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> Eliminare il montaggio

Per eliminare il montaggio, usare il **mssqlctl archiviazione montaggio delete** comando e specificare il percorso di montaggio in HDFS:

```bash
mssqlctl storage mount delete --mount-path <mount-path-in-hdfs>
```

## <a id="issues"></a> Problemi noti e limitazioni

Quando si usa HDFS la suddivisione in livelli nel cluster di big data di SQL Server nell'elenco seguente offre i problemi noti e sulle limitazioni attuali:

- Se le dimensioni della directory esterno in cui vengono montati sono maggiore della capacità del cluster, il montaggio ha esito negativo.

- Se il montaggio è bloccato in un `CREATING` sullo stato per un lungo periodo di tempo, molto probabilmente non è riuscito. In questo caso, annullare il comando ed eliminare il montaggio, se necessario. Verificare che i parametri e le credenziali siano corrette prima di riprovare.

- Impossibile creare punti di montaggio di directory esistenti.

- Impossibile creare punti di montaggio all'interno di punti di montaggio esistente.

- Se uno dei predecessori del punto di montaggio non esiste, verrà creati con le autorizzazioni impostate come predefinite per r-xr-xr-x (555).

- La creazione di montaggio può richiedere tempo a seconda del numero e dimensioni dei file in cui vengono montati. Durante questo processo, i file sotto il montaggio non sono visibili agli utenti. Mentre viene creato il montaggio, tutti i file verranno aggiunti a un percorso temporaneo, che per impostazione predefinita `/_temporary/_mounts/<mount-location>`.

- Il comando di creazione di montaggio è asincrono. Dopo il comando viene eseguito, lo stato di montaggio può essere controllato per comprendere lo stato del montaggio.

- Quando si crea il montaggio, utilizzato per l'argomento **-local-path** è essenzialmente un identificatore univoco del montaggio. La stessa stringa (tra cui "/" alla fine, se presente) deve essere usata nei comandi successivi.

- I punti di montaggio sono di sola lettura. Non è possibile creare alcuna directory o file in un montaggio.

- Si sconsiglia di directory di montaggio e i file che possono cambiare. Dopo aver creato il montaggio, eventuali modifiche o aggiornamenti alla sede remota non si rifletteranno nel montaggio in HDFS. Se vengono apportate modifiche nella posizione remota, è possibile eliminare e ricreare il montaggio in modo da riflettere lo stato aggiornato.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di SQL Server 2019 dei big data, vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).
