---
title: Montare ADLS Gen2 per la suddivisione in livelli HDFS
titleSuffix: How to mount ADLS Gen2
description: Questo articolo illustra come configurare la suddivisione in livelli per montare un file system di archivio Azure Data Lake esterni in HDFS in un cluster di big data (anteprima) di SQL Server 2019 HDFS.
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9f5d1ce4724f95b511272bb4df8d41ee0df75d90
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993967"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>Come Azure Data Lake Store montaggio Gen2 per HDFS la suddivisione in livelli in un cluster di big data

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

## <a name="credentials-for-mounting"></a>Credenziali per il montaggio

## <a name="use-oauth-credentials-to-mount"></a>Usare le credenziali OAuth per montare

Per usare le credenziali OAuth per montare, è necessario seguire i passaggi seguenti:

1. Andare alla [portale di Azure](https://portal.azure.com)
1. Passare a "servizi" nel riquadro di spostamento a sinistra e registrare il su "Azure Active Directory"
1. Con "Registrazioni per l'App" nel menu di scelta, creare una "applicazione Web e seguire la procedura guidata. **Ricordare il nome creato in questa fase**. È necessario aggiungere questo nome al tuo account Azure Data Lake Store come un utente autorizzato.
1. Dopo aver creato l'applicazione web, passare a "chiavi" in "impostazioni" per l'app.
1. Selezionare che una durata della chiave e fare clic su Salva. **Salvare la chiave generata.**
1.  Tornare alla pagina di registrazioni per l'App e fare clic sul pulsante "Endpoint" nella parte superiore. **Annotare l'URL "Endpoint di Token"**
1. Si avranno ora le operazioni seguenti annotate per OAuth:

    - il "ID applicazione" dell'App Web creato in precedenza nel passaggio 3
    - La chiave che appena generata nel passaggio 5
    - L'endpoint token nel passaggio 6

### <a name="adding-the-service-principal-to-your-adls-account"></a>Aggiunta l'entità servizio all'Account Azure Data Lake Store

1. Passare nuovamente al portale e aprire l'account Azure Data Lake Store e selezionare il controllo di accesso (IAM) nel menu a sinistra.
1. Selezionare "Aggiungi un'assegnazione di ruolo" e cercare il nome creato nel passaggio 3 in precedenza (si noti che non viene visualizzato nell'elenco, ma sarà disponibile se si cerca per il nome completo).
1. A questo punto aggiungere il ruolo di "Archiviazione Blob collaboratore ai dati (anteprima)".

Attendere circa 5-10 minuti prima di usare le credenziali per il montaggio

### <a name="create-credential-file"></a>Creare file delle credenziali

Aprire un prompt dei comandi in un computer client che possa accedere al cluster di big data.

Creare un file locale denominato **filename.creds** che contiene le credenziali dell'account Azure Data Lake Storage Gen2 usando il formato seguente:

   ```text
    fs.azure.account.auth.type=OAuth
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above]
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above]
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>Usare le chiavi di accesso per montare

È anche possibile montare usando chiavi di accesso che è possibile ottenere per l'account Azure Data Lake Store nel portale di Azure.

 > [!TIP]
   > Per altre informazioni su come trovare la chiave di accesso (`<storage-account-access-key>`) per l'account di archiviazione, vedere [visualizzare e copiare le chiavi di accesso](https://docs.microsoft.com/azure/storage/common/storage-account-manage?#view-and-copy-access-keys).

### <a name="create-credential-file"></a>Creare file delle credenziali

1. Aprire un prompt dei comandi in un computer client che possa accedere al cluster di big data.

1. Creare un file locale denominato **filename.creds** che contiene le credenziali dell'account Azure Data Lake Storage Gen2 usando il formato seguente:

   ```text
   fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a> Montare l'archiviazione HDFS remoto

Ora che è stato creato un file di credenziali con le chiavi di accesso o tramite OAuth, è possibile avviare il montaggio. I passaggi seguenti montare l'archiviazione HDFS remoto in Azure Data Lake per l'archiviazione HDFS locale del cluster di big data.

1. Uso **kubectl** per trovare l'indirizzo IP dell'endpoint **controller-svc-external** servizio nel cluster di big data. Cercare il **External-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-cluster-name>
   ```

1. Accedi con **mssqlctl** usando l'indirizzo IP esterno dell'endpoint del controller con il nome utente del cluster e la password:

   ```bash
   mssqlctl login -e https://<IP-of-controller-svc-external>:30080/
   ```

1. Montare l'archiviazione HDFS remoto in Azure usando **istallazione del pool di archiviazione cluster mssqlctl creare**. Prima di eseguire il comando seguente, sostituire i valori segnaposto:

   ```bash
   mssqlctl cluster storage-pool mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name> --credential-file <path-to-adls-credentials>/file.creds
   ```

   > [!NOTE]
   > Il montaggio di creare il comando è asincrona. A questo punto, non vi è alcun messaggio che indica se il montaggio ha avuto esito positivo. Vedere le [stato](#status) sezione per controllare lo stato dei punti di montaggio.

Se è stato montato, sarà possibile eseguire query sui dati HDFS ed eseguire i processi di Spark su di esso. Verrà visualizzata in HDFS per il cluster di big data nel percorso specificato dal `--mount-path`.

## <a id="status"></a> Ottenere lo stato dei punti di montaggio

Per elencare lo stato di tutti i punti di montaggio del cluster di big data, usare il comando seguente:

```bash
mssqlctl cluster storage-pool mount status
```

Per elencare lo stato di un montaggio in un percorso specifico in HDFS, usare il comando seguente:

```bash
mssqlctl cluster storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> Eliminare il montaggio

Per eliminare il montaggio, usare il **mssqlctl cluster pool di archiviazione montaggio delete** comando e specificare il percorso di montaggio in HDFS:

```bash
mssqlctl cluster storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di SQL Server 2019 dei big data, vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).
