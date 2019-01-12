---
title: Usare curl per caricare i dati in HDFS nel cluster di SQL Server 2019 dei big Data | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 2d1f3139023f326bc230e6269478b6dbfe522361
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241972"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-2019-big-data-clusters"></a>Usare curl per caricare i dati in HDFS nel cluster di SQL Server 2019 dei big Data

Questo articolo illustra come usare **curl** per caricare dati in HDFS nel cluster di big data 2019 Server SQL (anteprima).

## <a name="obtain-the-service-external-ip"></a>Ottenere l'IP esterno del servizio

WebHDFS viene avviato quando viene completata la distribuzione e l'accesso passa attraverso Knox. Viene esposto l'endpoint Knox attraverso un servizio Kubernetes denominato (per ora) **service-sicurezza-lb**.  Per creare l'URL WebHDFS che dovrai usare CURL per caricare e scaricare file che saranno necessari i **service-sicurezza-lb** indirizzo IP esterno e il nome del cluster del servizio. È possibile ottenere l'indirizzo IP esterno del servizio servizio-sicurezza-lb eseguendo questo comando:

```bash
kubectl get service service-security-lb -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> Il `<cluster name>` di seguito è il nome del cluster fornito quando è stato eseguito mssqlctl creare cluster `<cluster name>`.

## <a name="construct-the-url-to-access-webhdfs"></a>Creare l'URL per accedere a WebHDFS

A questo punto, è possibile costruire l'URL di accesso di WebHDFS come indicato di seguito:

`https://<service-security-lb service external IP address>:30433/gateway/default/webhdfs/v1/`

Ad esempio:

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>Elencare un file

File di elenco sotto **hdfs: / / / airlinedata** usare il comando curl seguente:

```bash
curl -i -k -u root:root-password -X GET 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Inserire un file locale in HDFS

Per inserire un nuovo file **test. csv** dalla directory locale alla directory airlinedata (**Content-Type** parametro è obbligatorio) usare il comando curl seguente:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Creare una directory

Per creare una directory **testare** sotto `hdfs:///` usare il comando seguente:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere [What ' s cluster di big data di SQL Server?](big-data-cluster-overview.md).