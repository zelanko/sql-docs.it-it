---
title: Usare sparklyr da RStudio
titleSuffix: SQL Server big data clusters
description: Connettersi al cluster di big data usando sparklyr da RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 30b8ddccd01c0e8d9a4eac34f2f504b0d8971af6
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860192"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>Usare Sparklyr nel cluster di big data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr fornisce un'interfaccia R per Apache Spark. Sparklyr è il modo preferenziale per gli sviluppatori di R per usare Spark. Questo articolo descrive come usare sparklyr in un cluster di big data di SQL Server 2019 (anteprima) usando RStudio.

## <a name="prerequisites"></a>Prerequisiti

- [Distribuire un cluster di big data di SQL Server 2019](quickstart-big-data-cluster-deploy.md).
- [Installare RStudio](https://www.rstudio.com/)

## <a name="connect-to-spark-in-ss19-big-data-cluster"></a>Connettersi a spark in cluster SS19 Big Data

In RStudio creare un RScript e connettersi a Spark come indicato di seguito. Connette i cluster di big data di Spark tramite Livy, che può essere raggiunto con i [gateway HDFS/Spark](connect-to-big-data-cluster.md#hdfs). Per l'autenticazione, usare il nome utente e la password impostati durante la distribuzione.

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "***root***", password = "****")

httr::set_config(httr::config(ssl_verifypeer = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>Eseguire query sparklyr

Dopo la connessione a Spark, è possibile eseguire sparklyr. Nell'esempio seguente esegue una query sul set di dati iris tramite sparklyr:

``` r
copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data, vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).