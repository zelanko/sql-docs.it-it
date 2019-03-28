---
title: Esercitazione sulla creazione, training e valutazione dei modelli basati sulla partizione nel R - servizi di SQL Server Machine Learning
description: Informazioni su come modellare, eseguire il training e utilizzare dati partizionati che viene creati in modo dinamico quando si usa la funzionalità di modellazione delle minacce basato sulla partizione di machine learning di SQL Server.
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/27/2018
ms.topic: tutorial
ms.author: davidph
author: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7ccdc67413e6714c762d165a8d087b9385a3f5a4
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512168"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>Esercitazione: Creare modelli basati su partizioni in R in SQL Server
[!INCLUDE[appliesto-ssvnex-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

In SQL Server 2019, la modellazione basata sulla partizione è la possibilità di creare ed eseguire il training di modelli su dati partizionati. Per i dati stratificati che naturalmente segmenti in uno schema di classificazione specifica - ad esempio aree geografiche, data e ora, età o gender - è possibile eseguire script tramite l'intero set di dati, con la possibilità di modellare, eseguire il training e assegnare un punteggio in partizioni che non subiranno alcuna modifica in tutte queste operazioni. 

Modellazione delle minacce basato sulla partizione viene abilitata tramite due nuovi parametri sul [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql):

+ **input_data_1_partition_by_columns**, che consente di specificare una colonna di partizionamento per.
+ **input_data_1_order_by_columns** specifica quali colonne alla clausola order by. 

In questa esercitazione, illustrato modellazione basata sulla partizione usando il classici dati di esempio relativi ai taxi di NYC e lo script R. La colonna di partizione è il metodo di pagamento.

> [!div class="checklist"]
> * Le partizioni sono basate sui tipi di pagamento (5).
> * Creare e il training dei modelli in ogni partizione e archiviare gli oggetti nel database.
> * Stimare la probabilità di risultati di suggerimento su ogni modello di partizione, usando dati di esempio sono riservati a tale scopo.

## <a name="prerequisites"></a>Prerequisiti
 
Per completare questa esercitazione, è necessario quanto segue:

+ Risorse di sistema sufficienti. Il set di dati è grande e operazioni di training sono a elevato utilizzo di risorse. Se possibile, usare un sistema con almeno 8 GB di RAM. In alternativa, è possibile usare set di dati più piccoli per ovviare i limiti di risorse. Le istruzioni per ridurre il set di dati sono inline. 

+ Uno strumento per T-SQL, esecuzione della query, ad esempio [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

+ [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak), che è possibile [scaricare e ripristinare](demo-data-nyctaxi-in-sql.md) all'istanza del motore di database locale. Dimensioni del file sono di circa 90 MB.

+ SQL Server 2019 anteprima istanza motore di database, con l'integrazione di servizi di Machine Learning e R.

Controllo versione eseguendo **`SELECT @@Version`** come una query T-SQL in uno strumento di query. Output deve essere "Microsoft SQL Server (CTP 2.4) - 2019 15.0.x".

Controllo della disponibilità dei pacchetti di R, restituendo un elenco formattato in modo corretto di tutti i pacchetti R attualmente installato con l'istanza del motore di database:

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

## <a name="connect-to-the-database"></a>Connettersi al database

Avviare Management Studio e connettersi all'istanza del motore di database. In Esplora oggetti, verificare i [NYCTaxi_Sample database](demo-data-nyctaxi-in-sql.md) esiste. 

## <a name="create-calculatedistance"></a>Creare CalculateDistance

Il database di esempio include una funzione scalare per il calcolo distanza, ma il funzionamento di stored procedure migliori con una funzione con valori di tabella. Eseguire lo script seguente per creare il **CalculateDistance** le funzioni usate nel [passaggio training](#training-step) in un secondo momento.

Per verificare che la funzione è stata creata, controllare le funzioni \Programmability\Functions\Table-valued sotto il **NYCTaxi_Sample** database in Esplora oggetti.

```sql
USE NYCTaxi_sample
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[CalculateDistance] (
    @Lat1 FLOAT
    ,@Long1 FLOAT
    ,@Lat2 FLOAT
    ,@Long2 FLOAT
    )
    -- User-defined function calculates the direct distance between two geographical coordinates.
RETURNS TABLE
AS
RETURN

SELECT COALESCE(3958.75 * ATAN(SQRT(1 - POWER(t.distance, 2)) / nullif(t.distance, 0)), 0) AS direct_distance
FROM (
    VALUES (CAST((SIN(@Lat1 / 57.2958) * SIN(@Lat2 / 57.2958)) + (COS(@Lat1 / 57.2958) * COS(@Lat2 / 57.2958) * COS((@Long2 / 57.2958) - (@Long1 / 57.2958))) AS DECIMAL(28, 10)))
    ) AS t(distance)
GO
 ```

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>Definire una routine per la creazione e training dei modelli per partizione

Questa esercitazione esegue il wrapping di script R in una stored procedure. In questo passaggio si crea una stored procedure che usa R per creare un set di dati di input, creare un modello di classificazione per stimare i risultati di suggerimento e quindi archivia il modello nel database.

Tra l'input dei parametri usato da questo script, si noterà **input_data_1_partition_by_columns** e **input_data_1_order_by_columns**. Tenere presente che questi parametri sono il meccanismo mediante il quale è partizionata la modellazione si verifica. I parametri vengono passati come input per [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) per elaborare le partizioni con dello script esterno in esecuzione una sola volta per ogni partizione. 

Per questa stored procedure [utilizzare il parallelismo](#parallel) per accelerare i tempi di completamento.

Dopo aver eseguito questo script, dovrebbe **train_rxLogIt_per_partition** nelle procedure \Programmability\Stored sotto il **NYCTaxi_Sample** database in Esplora oggetti. Si dovrebbe vedere anche una nuova tabella usata per archiviare i modelli: **dbo.nyctaxi_models**.

```sql
USE NYCTaxi_Sample
GO

CREATE
    OR

ALTER PROCEDURE [dbo].[train_rxLogIt_per_partition] (@input_query NVARCHAR(max))
AS
BEGIN
    DECLARE @start DATETIME2 = SYSDATETIME()
        ,@model_generation_duration FLOAT
        ,@model VARBINARY(max)
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name();

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    # Make sure InputDataSet is not empty. In parallel mode, if one thread gets zero data, an error occurs
    if (nrow(InputDataSet) > 0) {
    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    
    # build classification model to predict a tip outcome
    duration <- system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet))[3];

    # First, serialize a model to and put it into a database table
    modelbin <- as.raw(serialize(logitObj, NULL));

    # Create the data source. To reduce data size, add rowsPerRead=500000 to cut the dataset by half.
    ds <- RxOdbcData(table="ml_models", connectionString=connStr);

    # Store the model in the database
    model_name <- paste0("nyctaxi.", InputDataSet[1,]$payment_type);
    
    rxWriteObject(ds, model_name, modelbin, version = "v1",
    keyName = "model_name", valueName = "model_object", versionName = "model_version", overwrite = TRUE, serialize = FALSE);
    } 
    
    '
        ,@input_data_1 = @input_query
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@input_data_1_order_by_columns = N'passenger_count'
        ,@parallel = 1
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS NONE
END;
GO
```

<a name="parallel"></a>

### <a name="parallel-execution"></a>Esecuzione parallela

Si noti che il [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) gli input includono  **@parallel= 1**utilizzata per abilitare l'elaborazione parallela. A differenza delle versioni precedenti, in SQL Server 2019, impostando  **@parallel= 1** fornisce un hint per la più avanzata a query optimizer, rendendo l'esecuzione parallela un risultato molto più probabile.

Per impostazione predefinita, query optimizer tende a funzionare con  **@parallelad=1** nelle tabelle che includono più di 256 righe, ma se è possibile gestire questa in modo esplicito impostando  **@parallel= 1** come illustrato in questo script.

> [!Tip]
> Per la formazione workoads, è possibile usare **@parallel** qualsiasi script di training arbitrari, anche quelli con algoritmi non-Microsoft-rx. Solo gli algoritmi di RevoScaleR (con il prefisso di rx) offrono in genere, il parallelismo in scenari di training in SQL Server. Ma con il nuovo parametro, è possibile parallelizzare uno script che chiama funzioni, tra cui funzioni R open source, non specificamente progettate con tale funzionalità. Questo procedimento funziona perché le partizioni hanno affinità a thread specifici, pertanto tutte le operazioni di chiamata in uno script eseguito su una base per ogni partizione, sul thread specificato.

<a name="training-step"></a>

## <a name="run-the-procedure-and-train-the-model"></a>Eseguire la stored procedure e il training del modello

In questa sezione, lo script esegue il training di modelli che è stato creato e salvato nel passaggio precedente. Gli esempi seguenti illustrano due approcci per il training del modello: usando un intero set di dati o una parziale dei dati. 

Prevede che questo passaggio per richiedere un po' di tempo. Il training è con calcoli complessi, richiede molti minuti. Se le risorse di sistema, in particolare della memoria, non sono sufficienti per il caricamento, utilizzare un subset dei dati. Nel secondo esempio fornisce la sintassi.

```sql
--Example 1: train on entire dataset
EXEC train_rxLogIt_per_partition N'
SELECT payment_type, tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

```sql
--Example 2: Train on 20 percent of the dataset to expedite processing.
EXEC train_rxLogIt_per_partition N'
  SELECT tipped, payment_type, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample TABLESAMPLE (20 PERCENT) REPEATABLE (98074)
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

> [!NOTE]
> Se si eseguono altri carichi di lavoro, è possibile aggiungere `OPTION(MAXDOP 2)` all'istruzione SELECT se si desidera limitare l'elaborazione di query per solo 2 core.

## <a name="check-results"></a>Risultati della verifica

Il risultato nella tabella di modelli deve essere cinque diversi modelli, basati su cinque partizioni segmentate per i tipi di cinque pagamento. I modelli hanno le **ml_models** origine dati.

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>Definire una procedura per la stima dei risultati

È possibile usare gli stessi parametri per l'assegnazione dei punteggi. L'esempio seguente include uno script R che verrà assegna un punteggio con il modello corretto per la partizione che attualmente elaborata.

Come in precedenza, creare una stored procedure per eseguire il wrapping del codice R.

```sql
USE NYCTaxi_Sample
GO

-- Stored procedure that scores per partition. 
-- Depending on the partition being processed, a model specific to that partition will be used
CREATE
    OR

ALTER PROCEDURE [dbo].[predict_per_partition]
AS
BEGIN
    DECLARE @predict_duration FLOAT
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name()
        ,@input_query NVARCHAR(max);

    SET @input_query = 'SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance, payment_type
                          FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)
                          CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d'

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    if (nrow(InputDataSet) > 0) {

    #Get the partition that is currently being processed
    current_partition <- InputDataSet[1,]$payment_type;

    #Create the SQL query to select the right model
    query_getModel <- paste0("select model_object from ml_models where model_name = ", "''", "nyctaxi.",InputDataSet[1,]$payment_type,"''", ";")
    

    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
        
    #Define data source to use for getting the model
    ds <- RxOdbcData(sqlQuery = query_getModel, connectionString = connStr)

    # Load the model
    modelbin <- rxReadObject(ds, deserialize = FALSE)
    # unserialize model
    logitObj <- unserialize(modelbin);

    # predict tipped or not based on model
    predictions <- rxPredict(logitObj, data = InputDataSet, overwrite = TRUE, type = "response", writeModelVars = TRUE
        , extraVarsToWrite = c("payment_type"));        
    OutputDataSet <- predictions
    
    } else {
        OutputDataSet <- data.frame(integer(), InputDataSet[,]);        
    }
    '
        ,@input_data_1 = @input_query
        ,@parallel = 1
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS((
                tipped_Pred INT
                ,payment_type VARCHAR(5)
                ,tipped INT
                ,passenger_count INT
                ,trip_distance FLOAT
                ,trip_time_in_secs INT
                ,direct_distance FLOAT
                ));
END;
GO
```

## <a name="create-a-table-to-store-predictions"></a>Creare una tabella per archiviare le stime

```sql
CREATE TABLE prediction_results (
    tipped_Pred INT
    ,payment_type VARCHAR(5)
    ,tipped INT
    ,passenger_count INT
    ,trip_distance FLOAT
    ,trip_time_in_secs INT
    ,direct_distance FLOAT
    );

TRUNCATE TABLE prediction_results
GO
```

## <a name="run-the-procedure-and-save-predictions"></a>Eseguire la procedura e salvare le stime

```sql
INSERT INTO prediction_results (
    tipped_Pred
    ,payment_type
    ,tipped
    ,passenger_count
    ,trip_distance
    ,trip_time_in_secs
    ,direct_distance
    )
EXECUTE [predict_per_partition]
GO
```

## <a name="view-predictions"></a>Stime di visualizzazione

Poiché le stime vengono archiviate, è possibile eseguire una query semplice per restituire un set di risultati.

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, sono state usate [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) eseguire l'iterazione di operazioni su dati partizionati. Per ingrandire esaminare chiama gli script esterni nelle stored procedure e Usa funzioni RevoScaleR, continuare con l'esercitazione seguente.

> [!div class="nextstepaction"]
> [procedura dettagliata per R e SQL Server](walkthrough-data-science-end-to-end-walkthrough.md)

<!--
## Old intro

**(Not for production workloads)**

One of the more common approaches for executing R or Python code on SQL data is providing script as an input parameter to the [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure. In this CTP release, SQL Server 2019 adds new parameters to `sp_execute_external_script` to process partitions with the external script executing once for every partition:

| Parameter | Usage |
|-----------|-------|
| **input_data_1_partition_by_columns** | Specifies which columns to partition by. |
| **input_data_1_order_by_columns** | Specifies which columns to order by.  |

Partitions are an organizational mechanism for stratified data that naturally segments into a given classification scheme. Common examples include partitioning by geographic region, by date and time, by age or gender, and so forth. Given the existence of partitioned data, you might want to execute script over the entire data set, with the ability to model, train, and score partitions that remain intact over all these operations. Calling `sp_execute_external_script` with the new parameters allows you to do just that.

You can run this operation in parallel by combining `partition_by` with `@parallel`. If the input query can be parallelized, set `@parallel=1` as part of your arguments to `sp_execute_external_script`. By default, the query optimizer operates under `@parallel=1` on tables having more than 256 rows.

When the scenario is training, one advantage is that any arbitrary training script, even those using non-Microsoft-rx algorithms, can be parallelized by also using the @parallel parameter. Typically, you would have to use RevoScaleR algorithms (with the rx prefix) to obtain parallelism in training scenarios in SQL Server. But with the new parameter, you can parallelize a script that calls functions not specifically engineered with that capability.
-->
