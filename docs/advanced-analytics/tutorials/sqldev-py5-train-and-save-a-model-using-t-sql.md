---
title: Eseguire il training e salvare un modello Python usando T-SQL
description: Esercitazione su Python che illustra come eseguire il training e il salvataggio di un modello usando Transact-SQL in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 470d7be0e1777d029f406e183aad644359c82f13
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005998"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>Eseguire il training e salvare un modello Python usando T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo fa parte di un'esercitazione [relativa all'analisi Python nel database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md). 

In questo passaggio si apprenderà come eseguire il training di un modello di apprendimento automatico usando i pacchetti Python **Scikit-learn** e **revoscalepy**. Queste librerie Python sono già installate con SQL Server Machine Learning Services.

I moduli vengono caricati e vengono chiamate le funzioni necessarie per creare ed eseguire il training del modello utilizzando un SQL Server stored procedure. Il modello richiede le funzionalità dei dati progettate nelle lezioni precedenti. Infine, si salva il modello sottoposto a training in una tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Suddividere i dati di esempio in set di training e di testing

1. Creare una stored procedure denominata **PyTrainTestSplit** per dividere i dati nella tabella nyctaxi_sample in due parti: nyctaxi_sample_training e nyctaxi_sample_testing. 

    Questa stored procedure dovrebbe essere già stata creata, ma è possibile eseguire il codice seguente per crearla:

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

2. Per dividere i dati utilizzando una suddivisione personalizzata, eseguire il stored procedure e digitare un numero intero che rappresenta la percentuale di dati allocati al set di training. L'istruzione seguente, ad esempio, alloca il 60% dei dati al set di training.

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>Creazione di un modello di regressione logistica

Dopo aver preparato i dati, è possibile usarli per eseguire il training di un modello. A tale scopo, chiamare un stored procedure che esegue un codice Python, accettando come input la tabella dati di training. Per questa esercitazione vengono creati due modelli di classificazione binaria:

+ Il stored procedure **PyTrainScikit** crea un modello di stima delle mance usando il pacchetto **Scikit-learn** .
+ Il stored procedure **TrainTipPredictionModelRxPy** crea un modello di stima delle mance usando il pacchetto **revoscalepy** .

Ogni stored procedure usa i dati di input forniti per creare ed eseguire il training di un modello di regressione logistica. Tutto il codice Python viene incluso nel stored procedure di sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Per semplificare la ripetizione del training del modello sui nuovi dati, è necessario eseguire il wrapping della chiamata a sp_execute_external_script in un altro stored procedure e passare i nuovi dati di training come parametro. In questa sezione viene illustrato il processo.

### <a name="pytrainscikit"></a>PyTrainScikit

1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] aprire una nuova finestra di **query** ed eseguire l'istruzione seguente per creare il stored procedure **PyTrainScikit**.  Il stored procedure contiene una definizione dei dati di input, pertanto non è necessario fornire una query di input.

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

2. Eseguire le istruzioni SQL seguenti per inserire il modello sottoposto a training nella tabella NYC @ no__t-0taxi_models.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    L'elaborazione dei dati e l'adattamento del modello potrebbero richiedere alcuni minuti. I messaggi inviati tramite pipe al flusso **stdout** di Python vengono visualizzati nella finestra **messaggi** di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Esempio:

    *Messaggi stdout dallo script esterno:* 
  *c:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. Aprire la tabella *NYC @ no__t-1taxi_models*. È possibile notare che è stata aggiunta una riga nuova contenente il modello serializzato nella colonna _model_.

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

Questo stored procedure usa il nuovo pacchetto **revoscalepy** , che è un nuovo pacchetto per Python. Contiene oggetti, trasformazione e algoritmi simili a quelli forniti per il pacchetto **RevoScaleR** del linguaggio R. 

Con **revoscalepy**è possibile creare contesti di calcolo remoti, spostare i dati tra contesti di calcolo, trasformare i dati e eseguire il training di modelli predittivi usando gli algoritmi più diffusi, ad esempio la regressione logistica e lineare, gli alberi delle decisioni e altro ancora. Per ulteriori informazioni, vedere il [modulo revoscalepy nella Guida di riferimento alle funzioni SQL Server](../python/ref-py-revoscalepy.md) e [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

1. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] aprire una nuova finestra di **query** ed eseguire l'istruzione seguente per creare il stored procedure _TrainTipPredictionModelRxPy_.  Poiché il stored procedure include già una definizione dei dati di input, non è necessario fornire una query di input.

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

    Questo stored procedure esegue i passaggi seguenti come parte del training del modello:

    - La query SELECT applica la funzione scalare personalizzata _fnCalculateDistance_ per calcolare la distanza diretta tra i percorsi di selezione e di rilascio. I risultati della query vengono archiviati nella variabile di input Python predefinita, `InputDataset`.
    - La variabile binaria _tipped_ viene usata come *etichetta* o colonna risultato e il modello è adatto usando le colonne di funzionalità seguenti: _passenger_count_, _trip_distance_, _trip_time_in_secs_e _direct_distance_.
    - Il modello sottoposto a training viene serializzato e archiviato nella variabile Python `logitObj`. Aggiungendo l'OUTPUT della parola chiave T-SQL, è possibile aggiungere la variabile come output del stored procedure. Nel passaggio successivo, tale variabile viene utilizzata per inserire il codice binario del modello in una tabella di database _nyc_taxi_models_. Questo meccanismo semplifica l'archiviazione e il riutilizzo dei modelli.

2. Eseguire il stored procedure come indicato di seguito per inserire il modello **revoscalepy** sottoposto a training nella tabella *nyc_taxi_models*.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    L'elaborazione dei dati e l'adattamento del modello potrebbero richiedere alcuni minuti. I messaggi inviati tramite pipe al flusso **stdout** di Python vengono visualizzati nella finestra **messaggi** di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Esempio:

    *Messaggi stdout dallo script esterno:* 
  *c:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. Aprire la tabella *nyc_taxi_models*. È possibile notare che è stata aggiunta una riga nuova contenente il modello serializzato nella colonna _model_.

    *revoscalepy_model* *0x8003637265766F7363616c....*

Nel passaggio successivo si useranno i modelli sottoposti a training per creare stime.

## <a name="next-step"></a>Passaggio successivo

[Eseguire stime con Python incorporato in una stored procedure](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Passaggio precedente

[Creare funzionalità di dati mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)
