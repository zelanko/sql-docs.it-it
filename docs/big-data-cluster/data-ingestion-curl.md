---
title: Usare curl per caricare i dati in HDFS | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: Usare curl per caricare i dati in HDFS nel cluster di SQL Server 2019 dei big Data.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 56bee3241427b9de9768e7bdd9e49646b51521d1
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860147"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-big-data-clusters"></a>Usare curl per caricare i dati in HDFS nel cluster di SQL Server i big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo illustra come usare **curl** per caricare dati in HDFS nel cluster di big data 2019 Server SQL (anteprima).

## <a name="obtain-the-service-external-ip"></a>Ottenere l'IP esterno del servizio

WebHDFS viene avviato quando viene completata la distribuzione e l'accesso passa attraverso Knox. Viene esposto l'endpoint Knox attraverso un servizio Kubernetes denominato **protezione di endpoint**.  Per creare l'URL WebHDFS necessari per caricare e scaricare i file, è necessario il **protezione di endpoint** indirizzo IP esterno e il nome del cluster del servizio. È possibile ottenere il **protezione di endpoint** indirizzo IP esterno del servizio eseguendo il comando seguente:

```bash
kubectl get service endpoint-security -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> Il `<cluster name>` qui è il nome del cluster fornito quando è stato eseguito `mssqlctl cluster create --name <cluster name>`.

## <a name="construct-the-url-to-access-webhdfs"></a>Creare l'URL per accedere a WebHDFS

A questo punto, è possibile costruire l'URL di accesso di WebHDFS come indicato di seguito:

`https://<endpoint-security service external IP address>:30443/gateway/default/webhdfs/v1/`

Esempio:

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>Elencare un file

File di elenco sotto **hdfs: / / / airlinedata**, usare il comando curl seguente:

```bash
curl -i -k -u root:root-password -X GET 'https://<endpoint-security IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Inserire un file locale in HDFS

Per inserire un nuovo file **test. csv** dalla directory locale alla directory airlinedata, usare il comando curl seguente (il **Content-Type** parametro è obbligatorio):

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<endpoint-security IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Creare una directory

Per creare una directory **testare** sotto `hdfs:///`, usare il comando seguente:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<endpoint-security IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere [What ' s cluster di big data di SQL Server?](big-data-cluster-overview.md).
