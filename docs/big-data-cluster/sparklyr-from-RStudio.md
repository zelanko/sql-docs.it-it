---
title: Usare sparklyr da RStudio
titleSuffix: SQL Server 2019 big data clusters
description: Connettersi al cluster di Big data tramite sparklyr da RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 83980f9d08a3894b0fbf7871cf899483e06702c4
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018357"
---
# <a name="use-sparklyr-in-sql-server-2019-big-data-cluster"></a>Usare Sparklyr nel cluster di SQL Server 2019 Big data

Sparklyr fornisce un'interfaccia R per Apache Spark. Sparklyr è il modo preferenziale per gli sviluppatori di R per usare Spark. Questo articolo descrive come usare sparklyr in un cluster di big data di SQL Server 2019 (anteprima) usando RStudio.

## <a name="prerequisites"></a>Prerequisiti

- [Distribuire un cluster di big data di SQL Server 2019](quickstart-big-data-cluster-deploy.md).
- [Installare RStudio](https://www.rstudio.com/)

## <a name="connect-to-spark-in-ss19-big-data-cluster"></a>Connettersi a spark in cluster SS19 Big Data

In RStudio creare un RScript e connettersi a Spark come indicato di seguito. Cluster di Spark Big data si connette tramite Livy, che può essere raggiunto con i [gateway HDFS/Spark](connect-to-big-data-cluster.md#hdfs). Per l'autenticazione, usare il nome utente e la password impostati durante la distribuzione.

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