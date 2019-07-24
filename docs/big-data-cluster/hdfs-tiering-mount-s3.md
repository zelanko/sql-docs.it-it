---
title: Montare S3 per la suddivisione in livelli HDFS
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come configurare la suddivisione in livelli di HDFS per montare un file system S3 esterno in HDFS in un cluster SQL Server 2019 Big Data (anteprima).
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 28c80d6076f07c8a4f1605149f4b5c730c8349a1
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419334"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>Come montare S3 per la suddivisione in livelli di HDFS in un cluster Big Data

Le sezioni seguenti forniscono un esempio di come configurare la suddivisione in livelli di HDFS con un'origine dati di archiviazione S3.

## <a name="prerequisites"></a>Prerequisiti

- [Cluster Big Data distribuito](deployment-guidance.md)
- [Strumenti per Big Data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**
- Creare e caricare dati in un bucket S3 
  - Caricare file con estensione CSV o parquet nel bucket S3. Si tratta dei dati HDFS esterni che verranno montati in HDFS nel cluster Big Data.

## <a name="access-keys"></a>Chiavi di accesso

### <a name="set-environment-variable-for-access-key-credentials"></a>Imposta la variabile di ambiente per le credenziali della chiave di accesso

Aprire un prompt dei comandi in un computer client in grado di accedere al cluster Big Data. Impostare una variabile di ambiente usando il formato seguente. Si noti che le credenziali devono trovarsi in un elenco delimitato da virgole. Il comando ' set ' viene usato in Windows. Se si usa Linux, usare invece ' export '.

   ```text
    set MOUNT_CREDENTIALS=fs.s3a.access.key=<Access Key ID of the key>,
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > Per altre informazioni su come creare chiavi di accesso S3, vedere [chiavi di accesso S3](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys).

## <a id="mount"></a>Montare la risorsa di archiviazione HDFS remota

Ora che è stato preparato un file di credenziali con le chiavi di accesso, è possibile avviare il montaggio. La procedura seguente consente di montare l'archiviazione HDFS remota in S3 nell'archiviazione HDFS locale del cluster Big Data.

1. Usare **kubectl** per trovare l'indirizzo IP per il servizio endpoint **controller-SVC-external** nel cluster Big Data. Cercare **External-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Accedere con **azdata** usando l'indirizzo IP esterno dell'endpoint del controller con il nome utente e la password del cluster:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
   
1. Impostare la variabile di ambiente MOUNT_CREDENTIALS seguendo le istruzioni riportate sopra

1. Montare la risorsa di archiviazione HDFS remota in Azure usando **azdata BDC storage-pool Mount create**. Sostituire i valori segnaposto prima di eseguire il comando seguente:

   ```bash
   azdata bdc storage-pool mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > Il comando Mount create è asincrono. A questo punto, non è presente alcun messaggio che indica se il montaggio è riuscito. Per verificare lo stato dei montaggi, vedere la sezione relativa allo [stato](#status) .

Se montata correttamente, dovrebbe essere possibile eseguire una query sui dati di HDFS ed eseguire processi Spark su di essa. Verrà visualizzato in HDFS per il cluster Big Data nel percorso specificato da `--mount-path`.

## <a id="status"></a>Ottenere lo stato dei montaggi

Per elencare lo stato di tutti i montaggi nel cluster Big Data, usare il comando seguente:

```bash
azdata bdc storage-pool mount status
```

Per elencare lo stato di un montaggio in un percorso specifico in HDFS, usare il comando seguente:

```bash
azdata bdc storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>Aggiornare un montaggio

Nell'esempio seguente viene aggiornato il montaggio.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a>Elimina il montaggio

Per eliminare il montaggio, usare il comando **azdata BDC storage-pool Mount Delete** e specificare il percorso di montaggio in HDFS:

```bash
azdata bdc storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster SQL Server 2019 Big Data, vedere [che cosa sono i cluster SQL Server 2019 Big Data?](big-data-cluster-overview.md).
