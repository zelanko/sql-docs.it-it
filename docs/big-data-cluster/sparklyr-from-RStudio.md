---
title: Usare sparklyr da RStudio
titleSuffix: SQL Server big data clusters
description: Connettersi a Big Data cluster usando sparklyr da RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 04/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f346fed17e4c79214a7eba43f70767fc80b98a07
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/30/2019
ms.locfileid: "67728382"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>Usare sparklyr nel cluster SQL Server Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr fornisce un'interfaccia R per Apache Spark. Sparklyr è un modo comune per gli sviluppatori R di usare Spark. Questo articolo descrive come usare sparklyr in un cluster SQL Server 2019 Big Data (anteprima) usando RStudio.

## <a name="prerequisites"></a>Prerequisiti

- [Distribuire un cluster SQL Server 2019 Big Data](quickstart-big-data-cluster-deploy.md).

### <a name="install-rstudio-desktop"></a>Installare RStudio desktop

Installare e configurare **rstudio desktop** con i passaggi seguenti:

1. Se si esegue un client Windows, [scaricare e installare R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4).

1. [Scaricare e installare rstudio desktop](https://www.rstudio.com/products/rstudio/download/).

1. Al termine dell'installazione, eseguire i comandi seguenti all'interno di RStudio desktop per installare i pacchetti necessari:

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>Connettersi a Spark in un cluster di Big Data

È possibile usare sparklyr per connettersi da un client al cluster Big Data usando Livio e il gateway HDFS/Spark. 

In RStudio creare uno script R e connettersi a Spark come nell'esempio seguente:

> [!TIP]
> Per i `<USERNAME>` valori `<PASSWORD>` e, usare il nome utente (ad esempio la radice) e la password impostati durante la distribuzione del cluster Big Data. Per i `<IP>` valori `<PORT>` e, vedere la documentazione relativa alla [connessione a un cluster Big Data](connect-to-big-data-cluster.md).

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

Dopo la connessione a Spark, è possibile eseguire sparklyr. L'esempio seguente esegue una query sul set di dati Iris usando sparklyr:

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>Calcoli R distribuiti

Una funzionalità di sparklyr è la possibilità di [distribuire calcoli R](https://spark.rstudio.com/guides/distributed-r/) con [spark_apply](https://spark.rstudio.com/reference/spark_apply/).

Poiché i cluster Big Data usano le connessioni Livio, è necessario `packages = FALSE` impostare nella chiamata a **spark_apply**. Per altre informazioni, vedere la [sezione Livio](https://spark.rstudio.com/guides/distributed-r/#livy) della documentazione di sparklyr sui calcoli R distribuiti. Con questa impostazione, è possibile usare solo i pacchetti R già installati nel cluster Spark nel codice R passato a **spark_apply**. Nell'esempio seguente viene illustrata questa funzionalità:

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster di Big Data, vedere [che cosa sono SQL Server cluster Big Data 2019](big-data-cluster-overview.md).
