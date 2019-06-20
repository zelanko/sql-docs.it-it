---
title: Inserire dati in un pool di dati di SQL Server
titleSuffix: SQL Server big data clusters
description: Questa esercitazione illustra come inserire dati nel pool di dati di un cluster di big data di SQL Server 2019 (anteprima).
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 44ef1a05dfe0437420b8b3a1036ed356122dcfca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66770924"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-transact-sql"></a>Esercitazione: Inserire dati in un pool di dati di SQL Server con Transact-SQL

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questa esercitazione illustra come usare Transact-SQL per caricare i dati di [pool di dati](concept-data-pool.md) di un cluster di big data di SQL Server 2019 (anteprima). Con i cluster di big data di SQL Server, i dati da una varietà di origini possono essere inseriti e distribuiti in istanze del pool di dati.

In questa esercitazione, apprenderà come:

> [!div class="checklist"]
> * Creare una tabella esterna nel pool di dati.
> * Inserire i dati clickstream web di esempio nella tabella dati del pool.
> * Unire i dati nella tabella di pool di dati con le tabelle locali.

> [!TIP]
> Se si preferisce, è possibile scaricare ed eseguire uno script per i comandi in questa esercitazione. Per istruzioni, vedere la [dati pool esempi](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) su GitHub.

## <a id="prereqs"></a> Prerequisiti

- [Strumenti dei big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
- [Caricare i dati di esempio in cluster i big Data](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>Creare una tabella esterna nel pool di dati

La procedura seguente crea una tabella esterna nel pool di dati denominato **web_clickstream_clicks_data_pool**. Questa tabella è quindi utilizzabile come un percorso per l'inserimento di dati nel cluster di big data.

1. In Azure Data Studio, connettersi all'istanza master di SQL Server del cluster di big data. Per altre informazioni, vedere [connettersi all'istanza master di SQL Server](connect-to-big-data-cluster.md#master).

1. Fare doppio clic sulla connessione nel **server** finestra per visualizzare il dashboard di server per l'istanza master di SQL Server. Selezionare **nuova Query**.

   ![Query di istanza master di SQL Server](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. Eseguire il comando Transact-SQL seguente per modificare il contesto per il **Sales** database nell'istanza master.

   ```sql
   USE Sales
   GO
   ```

1. Creare un'origine dati esterna al pool di dati se non esiste già.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc:8080/datapools/default');
   ```

1. Creare una tabella esterna denominata **web_clickstream_clicks_data_pool** nel pool di dati.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstream_clicks_data_pool')
      CREATE EXTERNAL TABLE [web_clickstream_clicks_data_pool]
      ("wcs_user_sk" BIGINT , "i_category_id" BIGINT , "clicks" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. Nella versione CTP 3.0, la creazione di pool di dati è asincrona, ma non è possibile determinare quando viene completato ancora. Attendere due minuti per assicurarsi che il pool di dati viene creato prima di continuare.

## <a name="load-data"></a>Caricamento dei dati

Le seguenti operazioni di inserimento dati clickstream web di esempio nel pool di dati utilizzando la tabella esterna creata nei passaggi precedenti.

1. Usa un' `INSERT INTO` istruzione per inserire i risultati della query nel pool di dati (la **web_clickstream_clicks_data_pool** tabella esterna).

   ```sql
   INSERT INTO web_clickstream_clicks_data_pool
   SELECT wcs_user_sk, i_category_id, COUNT_BIG(*) as clicks
     FROM sales.dbo.web_clickstreams_hdfs_parquet
   INNER JOIN sales.dbo.item it ON (wcs_item_sk = i_item_sk
                           AND wcs_user_sk IS NOT NULL)
   GROUP BY wcs_user_sk, i_category_id
   HAVING COUNT_BIG(*) > 100;
   ```

1. Esaminare i dati inseriti con due query SELECT.

   ```sql
   SELECT count(*) FROM [dbo].[web_clickstream_clicks_data_pool]
   SELECT TOP 10 * FROM [dbo].[web_clickstream_clicks_data_pool]  
   ```

## <a name="query-the-data"></a>Eseguire query sui dati

Unire i risultati della query nel pool di dati con dati locali in archiviati il **Sales** tabella.

```sql
SELECT TOP (100)
   w.wcs_user_sk,
   SUM( CASE WHEN i.i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
   SUM( CASE WHEN w.i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
   SUM( CASE WHEN w.i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
   SUM( CASE WHEN w.i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
   SUM( CASE WHEN w.i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
   SUM( CASE WHEN w.i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
   SUM( CASE WHEN w.i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
   SUM( CASE WHEN w.i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
   SUM( CASE WHEN w.i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
   SUM( CASE WHEN w.i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
FROM [dbo].[web_clickstream_clicks_data_pool] as w
INNER JOIN (SELECT DISTINCT i_category_id, i_category FROM item) as i
   ON i.i_category_id = w.i_category_id
GROUP BY w.wcs_user_sk;
```

## <a name="clean-up"></a>Pulizia

Usare il comando seguente per rimuovere gli oggetti di database creati in questa esercitazione.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstream_clicks_data_pool];
```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come inserire dati nel pool di dati con i processi di Spark:
> [!div class="nextstepaction"]
> [Inserire i dati con i processi Spark](tutorial-data-pool-ingest-spark.md)
