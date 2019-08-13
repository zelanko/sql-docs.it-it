---
title: Usare curl per caricare dati in HDFS | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: Usare curl per caricare dati nei sistemi HDFS dei cluster Big Data di SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aae991c6dfdade4145f1e5578273e3b6aeb83299
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958638"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-big-data-clusters"></a>Usare curl per caricare dati nei sistemi HDFS dei cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo illustra come usare **curl** per caricare dati nel sistema HDFS dei cluster Big Data di SQL Server 2019 (preview).

## <a name="obtain-the-service-external-ip"></a>Ottenere l'indirizzo IP esterno del servizio

Al termine della distribuzione viene avviato WebHDFS, a cui è possibile accedere attraverso Knox. L'endpoint Knox viene esposto tramite un servizio Kubernetes denominato **gateway-svc-external**.  Per creare l'URL WebHDFS necessario per caricare/scaricare i file, sono necessari l'indirizzo IP esterno del servizio **gateway-svc-external** e il nome del cluster Big Data. È possibile ottenere l'indirizzo IP esterno del servizio **gateway-svc-external** eseguendo il comando seguente:

```bash
kubectl get service gateway-svc-external -n <big data cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> `<big data cluster name>` è il nome del cluster specificato nel file di configurazione della distribuzione. Il nome predefinito è `mssql-cluster`.

## <a name="construct-the-url-to-access-webhdfs"></a>Costruire l'URL per accedere a WebHDFS

A questo punto, è possibile costruire l'URL per accedere a WebHDFS, come indicato di seguito:

`https://<gateway-svc-external service external IP address>:30443/gateway/default/webhdfs/v1/`

Esempio:

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>Elencare un file

Per elencare il file in **hdfs:///airlinedata**, usare il comando curl seguente:

```bash
curl -i -k -u root:root-password -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Inserire un file locale in HDFS

Per inserire un nuovo file **test. csv** dalla directory locale alla directory airlinedata, usare il comando curl seguente (il parametro **Content-Type**):

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Creare una directory

Per creare un **tes**  di directory in `hdfs:///`, usare il comando seguente:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data di SQL Server, vedere [Che cos'è un cluster Big Data di SQL Server?](big-data-cluster-overview.md).
