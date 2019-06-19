---
title: Usare sparklyr da RStudio
titleSuffix: SQL Server big data clusters
description: Connettersi al cluster di big data usando sparklyr da RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 04/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8004146499bd8b17c7705f7558de075dfece5813
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65994172"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>Usare sparklyr nel cluster di big data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr fornisce un'interfaccia R per Apache Spark. Sparklyr è una diffusa specifica per gli sviluppatori di R per usare Spark. Questo articolo descrive come usare sparklyr in un cluster di big data di SQL Server 2019 (anteprima) usando RStudio.

## <a name="prerequisites"></a>Prerequisiti

- [Distribuire un cluster di big data di SQL Server 2019](quickstart-big-data-cluster-deploy.md).

### <a name="install-rstudio-desktop"></a>Installare RStudio Desktop

Installare e configurare **RStudio Desktop** con i passaggi seguenti:

1. Se si esegue in un client di Windows [scaricare e installare R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4).

1. [Scaricare e installare RStudio Desktop](https://www.rstudio.com/products/rstudio/download/).

1. Al termine dell'installazione, eseguire i comandi seguenti all'interno di RStudio Desktop per installare i pacchetti richiesti:

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>Connettersi a Spark in un cluster di big data

Per connettersi da un client per il cluster di big data usando Livy e il gateway HDFS/Spark, è possibile usare sparklyr. 

In RStudio, creare uno script R e connettersi a Spark come nell'esempio seguente:

> [!TIP]
> Per il `<USERNAME>` e `<PASSWORD>` valori, usare il nome utente (come radice) e la password impostati durante la distribuzione di cluster di big data. Per il `<IP>` e `<PORT>` valori, vedere la documentazione relativa [la connessione a un cluster di big data](connect-to-big-data-cluster.md).

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "<username>", password = "<password>")

httr::set_config(httr::config(ssl_verifypeer = 0L, ssl_verifyhost = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>Eseguire query sparklyr

Dopo la connessione a Spark, è possibile eseguire sparklyr. Nell'esempio seguente esegue una query sul set di dati iris tramite sparklyr:

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>Calcoli R distribuiti

Una funzionalità di sparklyr è la possibilità [distribuiscono i calcoli R](https://spark.rstudio.com/guides/distributed-r/) con [spark_apply](https://spark.rstudio.com/reference/spark_apply/).

Poiché i cluster di big data usano connessioni Livy, è necessario impostare `packages = FALSE` nella chiamata a **spark_apply**. Per altre informazioni, vedere la [sezione Livy](https://spark.rstudio.com/guides/distributed-r/#livy) della documentazione sparklyr sui calcoli R distribuiti. Con questa impostazione, è possibile usare solo i pacchetti R che sono già installati nel cluster Spark nel codice R passato a **spark_apply**. L'esempio seguente illustra questa funzionalità:

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data, vedere [quali sono i cluster di SQL Server 2019 dei big data](big-data-cluster-overview.md).
