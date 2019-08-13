---
title: Inserire dati con processi Spark
titleSuffix: SQL Server big data clusters
description: Questa esercitazione illustra come inserire dati nel pool di dati di un cluster Big Data di SQL Server 2019 (anteprima) usando processi Spark in Azure Data Studio.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 06/26/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6d0ea6d4fb7a3aea9788c089ad68cb3bf523837f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67957812"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>Esercitazione: Inserire dati in un pool di dati di SQL Server con processi Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questa esercitazione illustra come usare processi Spark per caricare dati nel [pool di dati](concept-data-pool.md) di un cluster Big Data di SQL Server 2019 (anteprima). 

In questa esercitazione verranno illustrate le procedure per:

> [!div class="checklist"]
> * Creare una tabella esterna nel pool di dati.
> * Creare un processo Spark mediante il quale caricare i dati da HDFS.
> * Eseguire una query sui risultati nella tabella esterna.

> [!TIP]
> Se si preferisce, è possibile scaricare ed eseguire uno script per i comandi descritti in questa esercitazione. Per istruzioni, vedere i [pool di dati di esempio](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) in GitHub.

## <a id="prereqs"></a> Prerequisiti

- [Strumenti per Big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
- [Caricare dati di esempio nel cluster Big Data](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>Creare una tabella esterna nel pool di dati

Questa procedura consente di creare una tabella esterna nel pool di dati denominata **web_clickstreams_spark_results**. La tabella può essere quindi usata come posizione per l'inserimento di dati nel cluster Big Data.

1. In Azure Data Studio connettersi all'istanza master di SQL Server del cluster Big Data. Per altre informazioni, vedere [Connettersi all'istanza master di SQL Server](connect-to-big-data-cluster.md#master).

1. Fare doppio clic sulla connessione nella finestra **Server** per visualizzare il dashboard del server per l'istanza master di SQL Server. Selezionare **Nuova query**.

   ![Query dell'istanza master di SQL Server](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. Creare un'origine dati esterna nel pool di dati, se non esiste già.

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
  
1. Nella versione CTP 3.1 la creazione del pool di dati è asincrona, ma non esiste alcun modo per determinare quando viene completata. Prima di continuare, attendere due minuti per avere la certezza che il pool di dati sia stato creato.

## <a name="start-a-spark-streaming-job"></a>Avviare un processo di streaming Spark

Il passaggio successivo consiste nella creazione di un processo di streaming Spark che carica dati clickstream Web dal pool di archiviazione (HDFS) nella tabella esterna creata nel pool di dati.

1. In Azure Data Studio connettersi all'istanza master del cluster Big Data. Per altre informazioni, vedere [Connettersi a un cluster Big Data](connect-to-big-data-cluster.md).

1. Fare doppio clic sulla connessione del gateway HDFS/Spark nella finestra **Server**. Selezionare quindi **New Spark Job** (Nuovo processo Spark).

   ![Nuovo processo Spark](media/tutorial-data-pool-ingest-spark/hdfs-new-spark-job.png)

1. Nella finestra **Nuovo processo** immettere un nome nel campo **Nome processo**.

1. Nell'elenco a discesa **File Jar/py** selezionare **HDFS**. Immettere quindi il seguente percorso di file JAR:

   ```text
   /jar/mssql-spark-lib-assembly-1.0.jar
   ```

1. Nel campo **Classe principale** immettere `FileStreaming`.

1. Nel campo **Argomenti** immettere il testo seguente, specificando la password per accedere all'istanza master di SQL Server nel segnaposto `<your_password>`. 

   ```text
   --server mssql-master-pool-0.service-master-pool --port 1433 --user sa --password <your_password> --database sales --table web_clickstreams_spark_results --source_dir hdfs:///clickstream_data --input_format csv --enable_checkpoint false --timeout 380000
   ```

   Nella tabella seguente viene descritto ciascun argomento:

   | Argomento | Descrizione |
   |---|---|
   | nome del server | SQL Server da usare per la lettura dello schema della tabella |
   | numero di porta | Porta su cui è in ascolto SQL Server (valore predefinito: 1433) |
   | username | Nome utente di accesso a SQL Server |
   | password | Password di accesso a SQL Server |
   | nome del database | Database di destinazione |
   | nome tabella esterna | Tabella da usare per i risultati |
   | directory di origine per lo streaming | Deve essere un URI completo, ad esempio "hdfs:///clickstream_data" |
   | formato di input | Può essere "CSV", "parquet" o "JSON" |
   | abilita checkpoint | true o false |
   | timeout | tempo di esecuzione del processo (in millisecondi) prima dell'uscita |

1. Premere **INVIO** per inviare il processo.

   ![Invio del processo Spark](media/tutorial-data-pool-ingest-spark/spark-new-job-settings.png)

## <a name="query-the-data"></a>Eseguire una query sui dati

Questa procedura dimostra che il processo di streaming Spark ha caricato i dati da HDFS nel pool di dati.

1. Prima di eseguire una query sui dati inseriti, controllare l'output della cronologia delle attività per verificare che il processo sia stato completato.

   ![Cronologia processi Spark](media/tutorial-data-pool-ingest-spark/spark-task-history.png)

1. Tornare alla finestra di query dell'istanza master di SQL Server aperta all'inizio di questa esercitazione.

1. Eseguire la query seguente per esaminare i dati inseriti.

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
