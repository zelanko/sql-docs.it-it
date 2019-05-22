---
title: Eseguire query sui dati HDFS nel pool di archiviazione
titleSuffix: SQL Server big data clusters
description: Questa esercitazione illustra come eseguire query sui dati HDFS in un cluster di big data di SQL Server 2019 (anteprima). Creare una tabella esterna dei dati nel pool di archiviazione e quindi eseguire una query.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: e43480c27ea865e827ec9a7325b55474935a21c1
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994135"
---
# <a name="tutorial-query-hdfs-in-a-sql-server-big-data-cluster"></a>Esercitazione: Query di HDFS in un cluster di big data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questa esercitazione illustra come eseguire query sui dati HDFS in un cluster di big data di SQL Server 2019 (anteprima).

In questa esercitazione, apprenderà come:

> [!div class="checklist"]
> * Creare una tabella esterna che punta ai dati HDFS in un cluster di big data.
> * Aggiungere i dati con dati di valore elevato nell'istanza master.

> [!TIP]
> Se si preferisce, è possibile scaricare ed eseguire uno script per i comandi in questa esercitazione. Per istruzioni, vedere la [esempi di dati di virtualizzazione](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization) su GitHub.

## <a id="prereqs"></a> Prerequisiti

- [Strumenti dei big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
- [Caricare i dati di esempio in cluster i big Data](tutorial-load-sample-data.md)

## <a name="create-an-external-table-to-hdfs"></a>Creare una tabella esterna in HDFS

Il pool di archiviazione contiene i dati clickstream web in un file CSV archiviato in HDFS. Utilizzare la procedura seguente per definire una tabella esterna che può accedere ai dati in tale file.

1. In Azure Data Studio, connettersi all'istanza master di SQL Server del cluster di big data. Per altre informazioni, vedere [connettersi all'istanza master di SQL Server](connect-to-big-data-cluster.md#master).

1. Fare doppio clic sulla connessione nel **server** finestra per visualizzare il dashboard di server per l'istanza master di SQL Server. Selezionare **nuova Query**.

   ![Query di istanza master di SQL Server](./media/tutorial-query-hdfs-storage-pool/sql-server-master-instance-query.png)

1. Eseguire il comando Transact-SQL seguente per modificare il contesto per il **Sales** database nell'istanza master.

   ```sql
   USE Sales
   GO
   ```

1. Definire il formato del file CSV da leggere da HDFS. Premere F5 per eseguire l'istruzione.

   ```sql
   CREATE EXTERNAL FILE FORMAT csv_file
   WITH (
       FORMAT_TYPE = DELIMITEDTEXT,
       FORMAT_OPTIONS(
           FIELD_TERMINATOR = ',',
           STRING_DELIMITER = '"',
           FIRST_ROW = 2,
           USE_TYPE_DEFAULT = TRUE)
   );
   ```

1. Se non esiste già, creare un'origine dati esterna al pool di archiviazione.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   BEGIN
     CREATE EXTERNAL DATA SOURCE SqlStoragePool
     WITH (LOCATION = 'sqlhdfs://controller-svc:8080/default');
   END
   ```

1. Creare una tabella esterna in grado di leggere il `/clickstream_data` dal pool di archiviazione. Il **SqlStoragePool** è accessibile dall'istanza master di un cluster di big data.

   ```sql
   CREATE EXTERNAL TABLE [web_clickstreams_hdfs]
   ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
   WITH
   (
       DATA_SOURCE = SqlStoragePool,
       LOCATION = '/clickstream_data',
       FILE_FORMAT = csv_file
   );
   GO
   ```

## <a name="query-the-data"></a>Eseguire query sui dati

Eseguire la query seguente per aggiungere i dati HDFS nel `web_clickstream_hdfs` tabella esterna con i dati relazionali locale `Sales` database.

```sql
SELECT  
    wcs_user_sk,
    SUM( CASE WHEN i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
    SUM( CASE WHEN i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
    SUM( CASE WHEN i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
    SUM( CASE WHEN i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
    SUM( CASE WHEN i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
    SUM( CASE WHEN i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
    SUM( CASE WHEN i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
    SUM( CASE WHEN i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
    SUM( CASE WHEN i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
    SUM( CASE WHEN i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
  FROM [dbo].[web_clickstreams_hdfs]
  INNER JOIN item it ON (wcs_item_sk = i_item_sk
                        AND wcs_user_sk IS NOT NULL)
GROUP BY  wcs_user_sk;
GO
```

## <a name="clean-up"></a>Pulizia

Usare il comando seguente per rimuovere la tabella esterna usata in questa esercitazione.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_hdfs];
GO
```

## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per informazioni su come eseguire una query Oracle da un cluster di big data.
> [!div class="nextstepaction"]
> [Eseguire query sui dati esterni in Oracle](tutorial-query-oracle.md)
