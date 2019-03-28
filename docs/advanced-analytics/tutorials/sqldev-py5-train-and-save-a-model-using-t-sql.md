---
title: Eseguire il training e salvataggio di un modello Python con T-SQL - SQL Server Machine Learning
description: Esercitazione su Python che illustrano come eseguire il training e salvataggio di un modello tramite Transact-SQL in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2e0505cf847a091a5650b392aab56f486cee16aa
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511248"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>Eseguire il training e salvataggio di un modello Python con T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo fa parte di un'esercitazione [analitica di Python nel database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md). 

In questo passaggio descrive come eseguire il training di un modello di machine learning usando i pacchetti Python **scikit-informazioni** e **revoscalepy**. Queste librerie di Python sono già installate con SQL Server Machine Learning Services.

Caricare i moduli e chiamare le funzioni necessarie per creare e il training del modello tramite una stored procedure SQL Server. Il modello richiede le funzionalità dei dati che è progettato nelle lezioni precedenti. Infine, si salva il modello con training per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella.
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Suddividere i dati di esempio in set di training e set di testing

1. Creare una stored procedure denominata **PyTrainTestSplit** per dividere i dati nella tabella nyctaxi_sample in due parti: nyctaxi_sample_training e nyctaxi_sample_testing. 

    Questa stored procedure deve essere già creata per l'utente, ma è possibile eseguire il codice seguente per crearla:

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainTestSplit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. Per dividere i dati mediante una suddivisione personalizzata, eseguire la stored procedure e digitare un numero intero che rappresenta la percentuale di dati allocati al set di training. Ad esempio, l'istruzione seguente allocherà il 60% dei dati al set di training.

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>Compilare un modello di regressione logistica

Dopo che i dati sono stati preparati, è possibile usarlo per addestrare un modello. Eseguire questa operazione chiamando una stored procedure che esegue codice Python, accettando come input della tabella di dati di training. Per questa esercitazione, creare due modelli, entrambi i modelli di classificazione binaria:

+ La stored procedure **PyTrainScikit** crea un modello di stima suggerimento utilizzando il **scikit-informazioni su** pacchetto.
+ La stored procedure **TrainTipPredictionModelRxPy** crea un modello di stima suggerimento utilizzando il **revoscalepy** pacchetto.

Ogni stored procedure utilizza i dati di input dall'utente per creare e addestrare un modello di regressione logistica. Viene eseguito il wrapping di tutto il codice Python nelle stored procedure di sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Per renderne più semplice ripetere il training del modello su nuovi dati, eseguire il wrapping della chiamata a sp_execute_exernal_script in un'altra stored procedure e passare i nuovi dati di training come un parametro. In questa sezione illustrerà tale processo.

### <a name="pytrainscikit"></a>PyTrainScikit

1.  Nelle [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], aprire una nuova **Query** finestra ed eseguire l'istruzione seguente per creare la stored procedure **PyTrainScikit**.  La stored procedure contiene una definizione dei dati di input, quindi non è necessario fornire una query di input.

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainScikit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainScikit] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from sklearn.linear_model import LogisticRegression
    
    ##Create SciKit-Learn logistic regression model
    X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
    y = numpy.ravel(InputDataSet[["tipped"]])
    
    SKLalgo = LogisticRegression()
    logitObj = SKLalgo.fit(X, y)
    
    ##Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

2. Eseguire il comando seguente istruzioni SQL per inserire il modello con training nella tabella città di New York\_taxi_models.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    L'elaborazione dei dati e l'adattamento del modello potrebbe richiedere un paio di minuti. I messaggi che sarebbero inoltrati di Python **stdout** flusso vengono visualizzati nel **messaggi** finestra di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Ad esempio:

    *Messaggi STDOUT dallo script esterno:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. Aprire la tabella *città di New York\_taxi_models*. È possibile notare che è stata aggiunta una riga nuova contenente il modello serializzato nella colonna _model_.

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

Questa stored procedure utilizza la nuova **revoscalepy** pacchetto, ovvero un nuovo pacchetto per Python. Contiene gli oggetti, la trasformazione e algoritmi simili a quelli forniti per il linguaggio R **RevoScaleR** pacchetto. 

Usando **revoscalepy**, è possibile creare contesti di calcolo remoti, spostare i dati tra contesti di calcolo, trasformare i dati e Training modelli predittivi usando algoritmi più diffusi, ad esempio la regressione logistica e lineare, alberi delle decisioni, e altre. Per altre informazioni, vedere [modulo revoscalepy in SQL Server](../python/ref-py-revoscalepy.md) e [revoscalepy di riferimento alle funzioni](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

1. Nelle [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], aprire una nuova **Query** finestra ed eseguire l'istruzione seguente per creare la stored procedure _TrainTipPredictionModelRxPy_.  Poiché la stored procedure include già una definizione dei dati di input, non è necessario fornire una query di input.

    ```sql
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from revoscalepy.functions.RxLogit import rx_logit
    
    ## Create a logistic regression model using rx_logit function from revoscalepy package
    logitObj = rx_logit("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

    Questa stored procedure esegue i passaggi seguenti come parte del training del modello:

    - La query SELECT si applica la funzione scalare personalizzata _fnCalculateDistance_ per calcolare la distanza diretta tra le posizioni e fine della corsa. I risultati della query vengono archiviati nella variabile di input Python predefinito, `InputDataset`.
    - La variabile binaria _tipped_ viene utilizzato come il *label* o colonna dei risultati il modello si adatta usando queste colonne di funzionalità: _passenger_count_, _trip_ distanza_, _trip_time_in_secs_, e _direct_distance_.
    - Il modello con Training viene serializzato e archiviato nella variabile Python `logitObj`. Aggiungendo la parola chiave T-SQL OUTPUT, è possibile aggiungere la variabile come output della stored procedure. Nel passaggio successivo, tale variabile viene usata per inserire il codice binario del modello in una tabella di database _nyc_taxi_models_. Questo meccanismo permette semplice archiviare e riutilizzare i modelli.

2. Eseguire la stored procedure come indicato di seguito per inserire il modello con training **revoscalepy** modello nella tabella *nyc_taxi_models*.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    L'elaborazione dei dati e l'adattamento del modello potrebbe richiedere qualche minuto. I messaggi che sarebbero inoltrati di Python **stdout** flusso vengono visualizzati nel **messaggi** finestra di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Esempio:

    *Messaggi STDOUT dallo script esterno:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. Aprire la tabella *nyc_taxi_models*. È possibile notare che è stata aggiunta una riga nuova contenente il modello serializzato nella colonna _model_.

    *revoscalepy_model* *0x8003637265766F7363616c....*

Nel passaggio successivo, si usano i modelli con training per creare stime.

## <a name="next-step"></a>Passaggio successivo

[Eseguire le stime usando Python incorporato in una stored procedure](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Passaggio precedente

[Creare funzionalità di dati mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)
