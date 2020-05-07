---
title: Creare modelli basati su partizioni in R
description: Informazioni sulle modalità di modellazione, training e utilizzo di dati partizionati creati dinamicamente quando si usano le funzionalità di modellazione basata su partizioni di SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/30/2020
ms.topic: tutorial
ms.author: davidph
author: dphansen
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 997896520a72f7803e656a42d2e38ebc6bf59d3d
ms.sourcegitcommit: d3e7c06fe989135f70d97f5ec6613fad4d62b145
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82619664"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>Esercitazione: Creare modelli basati su partizioni in R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In SQL Server 2019 la modellazione basata su partizioni è la possibilità di eseguire la creazione e il training di modelli su dati partizionati. Per i dati stratificati che possono essere segmentati naturalmente in un determinato schema di classificazione, ad esempio aree geografiche, data e ora, età o sesso, è possibile eseguire script sull'intero set di dati, con la possibilità di eseguire le operazioni di modellazione, training e assegnazione di punteggi su partizioni che rimangono intatte nel corso di tutte queste operazioni. 

La modellazione basata su partizioni viene abilitata tramite due nuovi parametri in [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql):

+ **input_data_1_partition_by_columns**, che specifica la colonna da usare per la partizione.
+ **input_data_1_order_by_columns**, che specifica la colonna da usare per l'ordinamento. 

In questa esercitazione si apprenderà la modellazione basata su partizioni usando i dati dell'esempio classico relativo ai taxi di New York City e uno script R. La colonna di partizione è relativa al metodo di pagamento.

> [!div class="checklist"]
> * Le partizioni sono basate sui tipi di pagamento (5).
> * Eseguire la creazione e il training dei modelli in ogni partizione e archiviare gli oggetti nel database.
> * Stimare la probabilità della mancia per ogni modello di partizione, usando i dati di esempio riservati a tale scopo.

## <a name="prerequisites"></a>Prerequisiti
 
Per completare l'esercitazione è necessario quanto segue:

+ Risorse di sistema sufficienti. Il set di dati è grande e le operazioni di training richiedono un elevato utilizzo delle risorse. Se possibile, usare un sistema con almeno 8 GB di RAM. In alternativa, è possibile usare set di dati più piccoli per aggirare i vincoli di risorse. Le istruzioni per la riduzione del set di dati sono fornite inline. 

+ Uno strumento per l'esecuzione di query T-SQL, ad esempio [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

+ [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak), che è possibile [scaricare e ripristinare](demo-data-nyctaxi-in-sql.md) nell'istanza del motore di database locale. Le dimensioni del file sono di circa 90 MB.

+ Istanza del motore di database di SQL Server 2019, con Machine Learning Services e integrazione di R.

+ Nell'esercitazione viene usata la [connessione loopback per SQL Server da uno script R su ODBC](../connect/loopback-connection.md]. È quindi necessario [creare un account di accesso per SQLRUserGroup](../security/create-a-login-for-sqlrusergroup.md).

Controllare la versione eseguendo **`SELECT @@Version`** come query T-SQL in uno strumento di query.

Controllare la disponibilità dei pacchetti R restituendo un elenco ben formattato di tutti i pacchetti R attualmente installati con l'istanza del motore di database:

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

## <a name="connect-to-the-database"></a>Stabilire la connessione al database

Avviare Management Studio e connettersi all'istanza del motore di database. In Esplora oggetti verificare che sia presente il [database NYCTaxi_Sample](demo-data-nyctaxi-in-sql.md). 

## <a name="create-calculatedistance"></a>Creare CalculateDistance

Il database demo include una funzione scalare per il calcolo della distanza, ma la stored procedure funziona meglio con una funzione con valori di tabella. Eseguire lo script seguente per creare la funzione **CalculateDistance** usata nel [passaggio di training](#training-step) più avanti.

Per verificare che la funzione sia stata creata, controllare in \Programmazione\Funzioni\Funzioni con valori di tabella nel database **NYCTaxi_Sample** in Esplora oggetti.

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

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>Definire una procedura per la creazione e il training di modelli per partizione

Questa esercitazione esegue il wrapping dello script R in una stored procedure. In questo passaggio si crea una stored procedure che usa R per creare un set di dati di input, si compila un modello di classificazione per la stima dei risultati relativi alle mance e quindi si archivia il modello nel database.

Tra i parametri di input usati in questo script sono presenti **input_data_1_partition_by_columns** e **input_data_1_order_by_columns**. Come spiegato in precedenza, questi parametri rappresentano il meccanismo in base al quale viene eseguita la modellazione partizionata. I parametri vengono passati come input a [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) per elaborare le partizioni, con lo script esterno eseguito una volta per ogni partizione. 

Per questa stored procedure, [usare il parallelismo](#parallel) per tempi di completamento più rapidi.

Dopo aver eseguito questo script, verrà visualizzato **train_rxLogIt_per_partition** in \Programmazione\Stored procedure nel database **NYCTaxi_Sample** in Esplora oggetti. Verrà visualizzata anche una nuova tabella usata per l'archiviazione dei modelli: **dbo.nyctaxi_models**.

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

Si noti che gli input di [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) includono `@parallel=1`, che consente di abilitare l'elaborazione parallela. A differenza delle versioni precedenti, in SQL Server 2019 l'impostazione di `@parallel=1` fornisce un hint più forte per Query Optimizer, rendendo l'esecuzione parallela un risultato molto più probabile.

Per impostazione predefinita, Query Optimizer tende a usare `@parallel=1` per le tabelle con più di 256 righe, ma è possibile gestire questo comportamento in modo esplicito impostando `@parallel=1`, come illustrato in questo script.

> [!Tip]
> Per i carichi di lavoro di training, è possibile usare `@parallel` con qualsiasi script di training arbitrario, anche quelli che usano algoritmi non Microsoft Rx. In genere, solo gli algoritmi RevoScaleR (con il prefisso rx) offrono il parallelismo negli scenari di training in SQL Server. Con il nuovo parametro, tuttavia, è possibile parallelizzare uno script che chiama funzioni, incluse le funzioni R open source, non progettate in modo specifico con tale funzionalità. Ciò è possibile perché le partizioni presentano affinità a thread specifici, quindi tutte le operazioni chiamate in uno script vengono eseguite in base alle singole partizioni, nell'oggetto `thread.`<a name="training-step"></a>

## <a name="run-the-procedure-and-train-the-model"></a>Eseguire la procedura e il training del modello

In questa sezione lo script esegue il training del modello creato e salvato nel passaggio precedente. Gli esempi seguenti illustrano due approcci al training del modello: l'uso di un intero set di dati o di dati parziali. 

Questo passaggio può richiedere un po' di tempo. Il training richiede un elevato utilizzo di risorse di calcolo e di conseguenza per il completamento sono necessari parecchi minuti. Se le risorse di sistema, in particolare la memoria, non sono sufficienti per il carico, usare un subset dei dati. Il secondo esempio fornisce la sintassi.

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
> Se si eseguono altri carichi di lavoro, è possibile aggiungere `OPTION(MAXDOP 2)` all'istruzione SELECT se si vuole limitare l'elaborazione delle query a soli 2 core.

## <a name="check-results"></a>Controllare i risultati

Il risultato nella tabella dei modelli deve essere costituito da cinque modelli diversi, basati su cinque partizioni segmentate in base ai cinque tipi di pagamento. I modelli si trovano nell'origine dati **ml_models**.

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>Definire una procedura per la stima dei risultati

È possibile usare gli stessi parametri per l'assegnazione dei punteggi. L'esempio seguente contiene uno script R che assegna un punteggio usando il modello corretto per la partizione attualmente in fase di elaborazione.

Come in precedenza, creare un stored procedure per eseguire il wrapping del codice R.

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

## <a name="view-predictions"></a>Visualizzare le stime

Poiché le stime sono archiviate, è possibile eseguire una query semplice per restituire un set di risultati.

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stata usata la stored procedure [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) per eseguire l'iterazione delle operazioni sui dati partizionati. Per un'analisi più approfondita delle chiamate di script esterni nelle stored procedure e dell'uso di funzioni RevoScaleR, continuare con l'esercitazione seguente.

> [!div class="nextstepaction"]
> [Procedura dettagliata per R e SQL Server](walkthrough-data-science-end-to-end-walkthrough.md)

