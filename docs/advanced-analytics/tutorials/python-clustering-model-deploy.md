---
title: 'Esercitazione: Distribuire un modello in Python per categorizzare i clienti'
description: Nella quarta parte di questa serie di esercitazioni in quattro parti, verrà distribuito un modello di clustering in Python con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: eef8a0f0f11e6d9085a1685145e4c6815979470d
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199359"
---
# <a name="tutorial-deploy-a-model-in-python-to-categorize-customers-with-sql-server-machine-learning-services"></a>Esercitazione: Distribuire un modello in Python per categorizzare i clienti con SQL Server Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Nella quarta parte di questa serie di esercitazioni in quattro parti, verrà distribuito un modello di clustering, sviluppato in Python, in un database SQL utilizzando SQL Server Machine Learning Services.

Per eseguire regolarmente il clustering, quando si registrano nuovi clienti, è necessario essere in grado di chiamare lo script Python da qualsiasi app. A tale scopo, è possibile distribuire lo script Python in SQL Server inserendo lo script Python all'interno di un stored procedure SQL nel database. Poiché il modello viene eseguito nel database SQL, può essere facilmente sottoposto a training sui dati archiviati nel database.

In questa sezione verrà spostato il codice Python appena scritto in SQL Server e verrà distribuito il clustering con l'ausilio di SQL Server Machine Learning Services.

L'articolo spiega come:

> [!div class="checklist"]
> * Creare un stored procedure che genera il modello
> * Eseguire il clustering in SQL Server
> * Usare le informazioni di clustering

Nella [prima parte](python-clustering-model.md), sono stati installati i prerequisiti e il database di esempio è stato ripristinato.

Nella [seconda parte](python-clustering-model-prepare-data.md)si è appreso come preparare i dati da un database SQL per eseguire il clustering.

Nella [terza parte](python-clustering-model-build.md)si è appreso come creare ed eseguire il training di un modello di clustering K-means in Python.

## <a name="prerequisites"></a>Prerequisiti

* Nella quarta parte di questa serie di esercitazioni si presuppone che siano stati soddisfatti i prerequisiti della [**parte 1**](python-clustering-model.md)e che siano stati completati i passaggi della [**parte 2**](python-clustering-model-prepare-data.md) e della [**terza parte**](python-clustering-model-build.md).

## <a name="create-a-stored-procedure-that-generates-the-model"></a>Creare un stored procedure che genera il modello

Eseguire lo script T-SQL seguente per creare il stored procedure. La procedura ricrea i passaggi sviluppati in parti una e due di questa serie di esercitazioni:

* classifica i clienti in base alla cronologia di acquisto e di ritorno
* generare quattro cluster di clienti usando un algoritmo K-means

```sql
USE [tpcxbb_1gb]
GO

CREATE procedure [dbo].[py_generate_customer_return_clusters]
AS

BEGIN
    DECLARE

-- Input query to generate the purchase history & return metrics
     @input_query NVARCHAR(MAX) = N'
SELECT
  ss_customer_sk AS customer,
  CAST( (ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) ) AS FLOAT) AS orderRatio,
  CAST( (ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) ) AS FLOAT) AS itemsRatio,
  CAST( (ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) ) AS FLOAT) AS monetaryRatio,
  CAST( (COALESCE(returns_count, 0)) AS FLOAT) AS frequency
FROM
  (
    SELECT
      ss_customer_sk,
      -- return order ratio
      COUNT(distinct(ss_ticket_number)) AS orders_count,
      -- return ss_item_sk ratio
      COUNT(ss_item_sk) AS orders_items,
      -- return monetary amount ratio
      SUM( ss_net_paid ) AS orders_money
    FROM store_sales s
    GROUP BY ss_customer_sk
  ) orders
  LEFT OUTER JOIN
  (
    SELECT
      sr_customer_sk,
      -- return order ratio
      count(distinct(sr_ticket_number)) as returns_count,
      -- return ss_item_sk ratio
      COUNT(sr_item_sk) as returns_items,
      -- return monetary amount ratio
      SUM( sr_return_amt ) AS returns_money
    FROM store_returns
    GROUP BY sr_customer_sk
  ) returned ON ss_customer_sk=sr_customer_sk
 '

EXEC sp_execute_external_script
      @language = N'Python'
    , @script = N'

import pandas as pd
from sklearn.cluster import KMeans

#get data from input query
customer_data = my_input_data

#We concluded in step 2 in the tutorial that 4 would be a good number of clusters
n_clusters = 4

#Perform clustering
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orderRatio","itemsRatio","monetaryRatio","frequency"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
    , @input_data_1 = @input_query
    , @input_data_1_name = N'my_input_data'
             with result sets (("Customer" int, "orderRatio" float,"itemsRatio" float,"monetaryRatio" float,"frequency" float,"cluster" float));
END;
GO
```

## <a name="perform-clustering-in-sql-database"></a>Eseguire il clustering nel database SQL

Ora che è stata creata la stored procedure, eseguire lo script seguente per eseguire il clustering usando la procedura.

```sql
--Create a table to store the predictions in

DROP TABLE IF EXISTS [dbo].[py_customer_clusters];
GO

CREATE TABLE [dbo].[py_customer_clusters] (
    [Customer] [bigint] NULL
  , [OrderRatio] [float] NULL
  , [itemsRatio] [float] NULL
  , [monetaryRatio] [float] NULL
  , [frequency] [float] NULL
  , [cluster] [int] NULL
  ,
    ) ON [PRIMARY]
GO

--Execute the clustering and insert results into table
INSERT INTO py_customer_clusters
EXEC [dbo].[py_generate_customer_return_clusters];

-- Select contents of the table to verify it works
SELECT * FROM py_customer_clusters;
```

## <a name="use-the-clustering-information"></a>Usare le informazioni di clustering

Poiché la procedura di clustering è stata archiviata nel database, è possibile eseguire il clustering in modo efficiente rispetto ai dati dei clienti archiviati nello stesso database. È possibile eseguire la procedura ogni volta che i dati dei clienti vengono aggiornati e si utilizzano le informazioni aggiornate sul clustering.

Si supponga di voler inviare un messaggio di posta elettronica promozionale ai clienti nel cluster 0, il gruppo che era inattivo (è possibile vedere come i quattro cluster sono stati descritti nella [terza parte](python-clustering-model-build.md#analyze-the-results) di questa esercitazione). Il codice seguente consente di selezionare gli indirizzi di posta elettronica dei clienti nel cluster 0.

```sql
USE [tpcxbb_1gb]
--Get email addresses of customers in cluster 0 for a promotion campaign
SELECT customer.[c_email_address], customer.c_customer_sk
  FROM dbo.customer
  JOIN
  [dbo].[py_customer_clusters] as c
  ON c.Customer = customer.c_customer_sk
  WHERE c.cluster = 0
```

È possibile modificare il valore **c. cluster** per restituire gli indirizzi di posta elettronica per i clienti di altri cluster.

## <a name="clean-up-resources"></a>Pulire le risorse

Al termine di questa esercitazione, è possibile eliminare il database tpcxbb_1gb da SQL Server.

## <a name="next-steps"></a>Passaggi successivi

Nella quarta parte di questa serie di esercitazioni sono stati completati i passaggi seguenti:

* Creare un stored procedure che genera il modello
* Eseguire il clustering in SQL Server
* Usare le informazioni di clustering

Per altre informazioni sull'uso di Python in SQL Server Machine Learning Services, vedere:

* [Avvio rapido: Creazione ed esecuzione di script Python semplici con SQL Server Machine Learning Services](quickstart-python-create-script.md)
* [Altre esercitazioni su Python per SQL Server Machine Learning Services](sql-server-python-tutorials.md)
* [Installare pacchetti Python con sqlmlutils](../package-management/install-additional-python-packages-on-sql-server.md)

