---
title: Montare ADLS Gen2 per la suddivisione in livelli HDFS
titleSuffix: How to mount ADLS Gen2
description: Questo articolo illustra come configurare la suddivisione in livelli di HDFS per montare un Azure Data Lake Storage esterno file system in HDFS [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]in un.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 822c10ad41232d213302e4bb5e328449d9f5f764
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652313"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>Come montare ADLS Gen2 per la suddivisione in livelli HDFS in un cluster Big Data

Le sezioni seguenti forniscono un esempio di come configurare la suddivisione in livelli HDFS con un'origine dati Azure Data Lake Storage Gen2.

## <a name="prerequisites"></a>Prerequisiti

- [Cluster Big Data distribuito](deployment-guidance.md)
- [Strumenti per Big Data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a id="load"></a> Caricare i dati in Azure Data Lake Storage

La sezione seguente descrive come configurare Azure Data Lake Storage Gen2 per testare la suddivisione in livelli HDFS. Se si hanno già dati archiviati in Azure Data Lake Storage, è possibile ignorare questa sezione per usare i propri dati.

1. [Creare un account di archiviazione con le funzionalità di Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. [Creare un contenitore BLOB](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) in questo account di archiviazione per i dati esterni.

1. Caricare un file CSV o Parquet nel contenitore. Si tratta dei dati HDFS esterni che verranno montati in HDFS nel cluster Big Data.

## <a name="credentials-for-mounting"></a>Credenziali per il montaggio

## <a name="use-oauth-credentials-to-mount"></a>Usare le credenziali OAuth per il montaggio

Per usare le credenziali OAuth per il montaggio, è necessario seguire questa procedura:

1. Passare al [portale di Azure](https://portal.azure.com)
1. Passare a "Servizi" nel riquadro di spostamento sinistro e fare clic su "Azure Active Directory"
1. Usando "Registrazioni app" nel menu creare un'applicazione Web e seguire la procedura guidata. **Tenere a mente il nome creato in questa posizione.** . Sarà necessario aggiungere questo nome all'account ADLS come utente autorizzato.
1. Una volta creata l'applicazione Web, passare a "Chiavi" in "Impostazioni" per l'app.
1. Selezionare una durata della chiave e fare clic su Salva. **Salvare la chiave generata.**
1.  Tornare alla pagina Registrazioni app e fare clic sul pulsante "Endpoint" nella parte superiore. **Annotare l'URL di "Endpoint token"**
1. A questo punto dovrebbero essere state annotate le informazioni seguenti per OAuth:

    - "ID applicazione" dell'app Web creata in precedenza nel passaggio 3
    - Chiave appena generata nel passaggio 5
    - Endpoint token del passaggio 6

### <a name="adding-the-service-principal-to-your-adls-account"></a>Aggiungere l'entità servizio all'account ADLS

1. Tornare al portale, aprire l'account ADLS e scegliere Controllo di accesso (IAM) dal menu a sinistra.
1. Selezionare "Aggiungi un'assegnazione di ruolo" e cercare il nome creato nel passaggio 3 in precedenza (si noti che non viene visualizzato nell'elenco, ma è possibile trovarlo cercando il nome completo).
1. Aggiungere ora il ruolo "Collaboratore ai dati del BLOB di archiviazione (anteprima)".

Attendere 5-10 minuti prima di usare le credenziali per il montaggio

### <a name="set-environment-variable-for-oauth-credentials"></a>Impostare la variabile di ambiente per le credenziali OAuth

Aprire un prompt dei comandi in un computer client in grado di accedere al cluster Big Data. Impostare una variabile di ambiente usando il formato seguente: Si noti che le credenziali devono essere inserite in un elenco delimitato da virgole. Il comando "set" viene usato in Windows. Se si usa Linux, usare invece "export".

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above],
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above],
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>Usare le chiavi di accesso per il montaggio

È anche possibile eseguire il montaggio usando chiavi di accesso che è possibile ottenere per l'account ADLS nel portale di Azure.

 > [!TIP]
   > Per altre informazioni su come trovare la chiave di accesso (`<storage-account-access-key>`) per l'account di archiviazione, vedere [Visualizzare la stringa di connessione e le chiavi dell'account](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string).

### <a name="set-environment-variable-for-access-key-credentials"></a>Impostare la variabile di ambiente per le credenziali della chiave di accesso

1. Aprire un prompt dei comandi in un computer client in grado di accedere al cluster Big Data.

1. Aprire un prompt dei comandi in un computer client in grado di accedere al cluster Big Data. Impostare una variabile di ambiente usando il formato seguente. Si noti che le credenziali devono essere inserite in un elenco delimitato da virgole. Il comando "set" viene usato in Windows. Se si usa Linux, usare invece "export".

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a> Montare la risorsa di archiviazione HDFS remota

Ora che è stata impostata la variabile di ambiente MOUNT_CREDENTIALS per le chiavi di accesso o tramite OAuth, è possibile iniziare il montaggio. La procedura seguente consente di montare la risorsa di archiviazione HDFS remota in Azure Data Lake nell'archiviazione HDFS locale del cluster Big Data.

1. Usare **kubectl** per trovare l'indirizzo IP per il servizio **controller-svc-external** dell'endpoint nel cluster Big Data. Cercare **External-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Accedere con **azdata** usando l'indirizzo IP esterno dell'endpoint del controller con il nome utente e la password del cluster:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
1. Impostare la variabile di ambiente MOUNT_CREDENTIALS (scorrere verso l'alto per istruzioni)

1. Montare la risorsa di archiviazione HDFS remota in Azure usando **azdata BDC HDFS Mount create**. Sostituire i valori segnaposto prima di eseguire il comando seguente:

   ```bash
   azdata bdc hdfs mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > Il comando mount create è asincrono. A questo punto, non sono presenti messaggi che indicano se il montaggio è riuscito o meno. Vedere la sezione relativa allo [stato](#status) per controllare lo stato dei montaggi.

Se il montaggio è riuscito, dovrebbe essere possibile eseguire una query sui dati di HDFS, nonché eseguire processi Spark. Il montaggio verrà visualizzato in HDFS per il cluster Big Data nel percorso specificato da `--mount-path`.

## <a id="status"></a> Ottenere lo stato dei montaggi

Per elencare lo stato di tutti i montaggi nel cluster Big Data, usare il comando seguente:

```bash
azdata bdc hdfs mount status
```

Per elencare lo stato di un montaggio in un percorso specifico in HDFS, usare il comando seguente:

```bash
azdata bdc hdfs mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>Aggiornare un montaggio

L'esempio seguente aggiorna il montaggio.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> Eliminare il montaggio

Per eliminare il montaggio, usare il comando **azdata BDC HDFS Mount Delete** e specificare il percorso di montaggio in HDFS:

```bash
azdata bdc hdfs mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], vedere [che cosa [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]sono?](big-data-cluster-overview.md).
