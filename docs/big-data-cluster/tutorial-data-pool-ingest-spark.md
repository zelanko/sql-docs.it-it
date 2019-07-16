---
title: Inserire i dati con i processi Spark
titleSuffix: SQL Server big data clusters
description: Questa esercitazione illustra come inserire dati nel pool di dati di un cluster di big data 2019 Server SQL (anteprima) con i processi Spark in Azure Data Studio.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 06/26/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6d0ea6d4fb7a3aea9788c089ad68cb3bf523837f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957812"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>Esercitazione: Inserire dati in un pool di dati di SQL Server con i processi Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questa esercitazione illustra come usare processi di Spark per caricare i dati di [pool di dati](concept-data-pool.md) di un cluster di big data di SQL Server 2019 (anteprima). 

In questa esercitazione si imparerà a:

> [!div class="checklist"]
> * Creare una tabella esterna nel pool di dati.
> * Creare un processo Spark per caricare i dati da HDFS.
> * Query sui risultati della tabella esterna.

> [!TIP]
> Se si preferisce, è possibile scaricare ed eseguire uno script per i comandi in questa esercitazione. Per istruzioni, vedere la [dati pool esempi](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) su GitHub.

## <a id="prereqs"></a> Prerequisiti

- [Strumenti dei big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
- [Caricare i dati di esempio in cluster i big Data](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>Creare una tabella esterna nel pool di dati

La procedura seguente crea una tabella esterna nel pool di dati denominato **web_clickstreams_spark_results**. Questa tabella è quindi utilizzabile come un percorso per l'inserimento di dati nel cluster di big data.

1. In Azure Data Studio, connettersi all'istanza master di SQL Server del cluster di big data. Per altre informazioni, vedere [connettersi all'istanza master di SQL Server](connect-to-big-data-cluster.md#master).

1. Fare doppio clic sulla connessione nel **server** finestra per visualizzare il dashboard di server per l'istanza master di SQL Server. Selezionare **nuova Query**.

   ![Query di istanza master di SQL Server](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. Creare un'origine dati esterna al pool di dati se non esiste già.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. Creare una tabella esterna denominata **web_clickstreams_spark_results** nel pool di dati.

   ```sql
   USE Sales
   GO
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstreams_spark_results')
      CREATE EXTERNAL TABLE [web_clickstreams_spark_results]
      ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. Nella versione CTP 3.1, la creazione di pool di dati è asincrona, ma non è possibile determinare quando viene completato ancora. Attendere due minuti per assicurarsi che il pool di dati viene creato prima di continuare.

## <a name="start-a-spark-streaming-job"></a>Avviare un processo di streaming Spark

Il passaggio successivo consiste nel creare un processo che carica i dati clickstream web dal pool di archiviazione (distribuito Hadoop HDFS) di streaming Spark nella tabella esterna che è stato creato nel pool di dati.

1. In Azure Data Studio, connettersi all'istanza master del cluster di big data. Per altre informazioni, vedere [connettersi a un cluster di big data](connect-to-big-data-cluster.md).

1. Fare doppio clic sulla connessione di gateway HDFS/Spark nel **server** finestra. Quindi selezionare **nuovo processo Spark**.

   ![Nuovo processo Spark](media/tutorial-data-pool-ingest-spark/hdfs-new-spark-job.png)

1. Nel **nuovo processo** finestra, immettere un nome nella **il nome del processo** campo.

1. Nel **File con estensione Jar / all'anno precedente** elenco a discesa, selezionare **HDFS**. Quindi immettere il percorso del file jar seguenti:

   ```text
   /jar/mssql-spark-lib-assembly-1.0.jar
   ```

1. Nel **classe principale** immettere `FileStreaming`.

1. Nel **argomenti** immettere il testo seguente, specificando la password per l'istanza master di SQL Server nel `<your_password>` segnaposto. 

   ```text
   --server mssql-master-pool-0.service-master-pool --port 1433 --user sa --password <your_password> --database sales --table web_clickstreams_spark_results --source_dir hdfs:///clickstream_data --input_format csv --enable_checkpoint false --timeout 380000
   ```

   La tabella seguente descrive ciascun argomento:

   | Argomento | Descrizione |
   |---|---|
   | nome del server | Uso di SQL Server per la lettura lo schema della tabella |
   | Numero di porta | Porta SQL Server è in ascolto (valore predefinito 1433) |
   | userName | Nome utente di accesso di SQL Server |
   | password | Password di accesso di SQL Server |
   | nome del database | Database di destinazione |
   | nome della tabella esterna | Tabella da utilizzare per ottenere risultati |
   | Directory di origine per lo streaming | Questo deve essere un URI completo, ad esempio "hdfs: / / / clickstream_data" |
   | formato di input | Ciò può essere "csv", ". parquet" o "json" |
   | Abilita checkpoint | true o false |
   | timeout | tempo di esecuzione del processo per espresso in millisecondi prima di uscire |

1. Premere **Submit** per inviare il processo.

   ![Invio di processi Spark](media/tutorial-data-pool-ingest-spark/spark-new-job-settings.png)

## <a name="query-the-data"></a>Eseguire query sui dati

I passaggi seguenti mostrano che il processo di streaming Spark caricato i dati da HDFS in pool di dati.

1. Prima dell'esecuzione di query i dati acquisiti, esaminare l'output della cronologia di attività per verificare che il processo completato.

   ![Cronologia dei processi Spark](media/tutorial-data-pool-ingest-spark/spark-task-history.png)

1. Tornare alla finestra di query SQL Server istanza master aperta all'inizio di questa esercitazione.

1. Eseguire la query seguente per esaminare i dati acquisiti.

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```

## <a name="clean-up"></a>Eseguire la pulizia

Usare il comando seguente per rimuovere gli oggetti di database creati in questa esercitazione.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come eseguire un notebook di esempio in Azure Data Studio:
> [!div class="nextstepaction"]
> [Eseguire un notebook di esempio](tutorial-notebook-spark.md)
