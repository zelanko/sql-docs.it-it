---
title: Montare S3 per la suddivisione in livelli HDFS
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come configurare la suddivisione in livelli di HDFS per montare un file system S3 esterno in HDFS [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]in un.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 653f9a48c03df18fc0591f7bd8060d951567c779
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652301"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>Come montare S3 per la suddivisione in livelli HDFS in un cluster Big Data

Le sezioni seguenti forniscono un esempio di come configurare la suddivisione in livelli HDFS con un'origine dati di archiviazione S3.

## <a name="prerequisites"></a>Prerequisiti

- [Cluster Big Data distribuito](deployment-guidance.md)
- [Strumenti per Big Data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**
- Creare e caricare dati in un bucket S3 
  - Caricare file CSV o Parquet nel bucket S3. Si tratta dei dati HDFS esterni che verranno montati in HDFS nel cluster Big Data.

## <a name="access-keys"></a>Chiavi di accesso

### <a name="set-environment-variable-for-access-key-credentials"></a>Impostare la variabile di ambiente per le credenziali della chiave di accesso

Aprire un prompt dei comandi in un computer client in grado di accedere al cluster Big Data. Impostare una variabile di ambiente usando il formato seguente. Si noti che le credenziali devono essere inserite in un elenco delimitato da virgole. Il comando "set" viene usato in Windows. Se si usa Linux, usare invece "export".

   ```text
    set MOUNT_CREDENTIALS=fs.s3a.access.key=<Access Key ID of the key>,
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > Per altre informazioni su come creare chiavi di accesso S3, vedere [Chiavi di accesso S3](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys).

## <a id="mount"></a> Montare la risorsa di archiviazione HDFS remota

Dopo aver preparato un file di credenziali con chiavi di accesso, è ora possibile iniziare il montaggio. La procedura seguente consente di montare la risorsa di archiviazione HDFS remota in S3 nell'archiviazione HDFS locale del cluster Big Data.

1. Usare **kubectl** per trovare l'indirizzo IP per il servizio **controller-svc-external** dell'endpoint nel cluster Big Data. Cercare **External-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Accedere con **azdata** usando l'indirizzo IP esterno dell'endpoint del controller con il nome utente e la password del cluster:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
   
1. Impostare la variabile di ambiente MOUNT_CREDENTIALS seguendo le istruzioni sopra riportate

1. Montare la risorsa di archiviazione HDFS remota in Azure usando **azdata BDC HDFS Mount create**. Sostituire i valori segnaposto prima di eseguire il comando seguente:

   ```bash
   azdata bdc hdfs mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name>
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
