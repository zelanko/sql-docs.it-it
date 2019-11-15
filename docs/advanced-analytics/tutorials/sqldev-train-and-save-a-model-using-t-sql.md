---
title: 'Esercitazione su R + T-SQL: Eseguire il training del modello'
description: Esercitazione che illustra come eseguire il training, la serializzazione e il salvataggio di un modello R usando stored procedure di SQL Server e funzioni T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 406f8e1c60c5820f9edaaf7760b7aeed321d2611
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73724460"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>Lezione 3: Eseguire il training e il salvataggio di un modello usando T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo fa parte di un'esercitazione per sviluppatori SQL sull'uso di R in SQL Server.

In questa lezione verrà illustrato come eseguire il training di un modello di Machine Learning usando R. Si eseguirà il training del modello usando le caratteristiche dei dati create nella lezione precedente e quindi si salverà il modello sottoposto a training in una tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In questo caso, i pacchetti R sono già installati con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], quindi è possibile eseguire tutte le operazioni da SQL.

## <a name="create-the-stored-procedure"></a>Creare la stored procedure

Quando si chiama R da T-SQL, si usa la stored procedure di sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Per i processi che vengono ripetuti spesso, come la ripetizione del training di un modello, è tuttavia più semplice incapsulare la chiamata a sp_execute_exernal_script in un'altra stored procedure.

1. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] aprire una nuova finestra **Query**.

2. Eseguire l'istruzione seguente per creare la stored procedure **RxTrainLogitModel**. Questa stored procedure definisce i dati di input e usa **rxLogit** di RevoScaleR per creare un modello di regressione logistica.

    ```sql
    CREATE PROCEDURE [dbo].[RxTrainLogitModel] (@trained_model varbinary(max) OUTPUT)
    
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
        pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
        from nyctaxi_sample
        tablesample (70 percent) repeatable (98052)
    '
    
      EXEC sp_execute_external_script @language = N'R',
                                      @script = N'
    ## Create model
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
    summary(logitObj)
    
    ## Serialize model 
    trained_model <- as.raw(serialize(logitObj, NULL));
    ',
      @input_data_1 = @inquery,
      @params = N'@trained_model varbinary(max) OUTPUT',
      @trained_model = @trained_model OUTPUT; 
    END
    GO
    ```

    - Per assicurarsi che rimangano dati disponibili per testare il modello, viene selezionato in modo casuale il 70% dei dati della tabella relativa ai dati dei taxi da usare per il training.

    - La query SELECT usa la funzione scalare personalizzata *fnCalculateDistance* per calcolare la distanza diretta tra la posizione di salita e discesa dei passeggeri. I risultati della query vengono archiviati nella variabile di input R predefinita `InputDataset`.
  
    - Lo script R chiama la funzione **rxLogit**, ovvero una delle funzioni R avanzate incluse in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], per creare il modello di regressione logistica.
  
        La variabile binaria _tipped_ viene usata come *etichetta* o come colonna dei risultati. Il modello si adatta usando le colonne delle funzionalità seguenti:  _passenger_count_, _trip_distance_, _trip_time_in_secs_e _direct_distance_.
  
    - Il modello sottoposto a training salvato nella variabile R `logitObj` viene serializzato e restituito come parametro di output.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>Eseguire il training e la distribuzione del modello R usando la stored procedure

Poiché la stored procedure include già una definizione dei dati di input, non è necessario specificare una query di input.

1. Per eseguire il training e la distribuzione del modello R, chiamare la stored procedure e inserirla nella tabella di database _nyc_taxi_models_, in modo che sia possibile farne uso per stime future:

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. Esaminare la finestra **Messaggi** di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per visualizzare i messaggi che verrebbero inoltrati al flusso **stdout** di R, come il seguente: 

    "STDOUT message(s) from external script: Rows Read: 1193025, Total Rows Processed: 1193025, Total Chunk Time: 0.093 seconds"

    Possono venire visualizzati anche messaggi specifici per la singola funzione, `rxLogit`, con informazioni sulle variabili e sulle metriche di test generate come parte della creazione del modello.

3.  Dopo il completamento dell'istruzione, aprire la tabella *nyc_taxi_models*. L'elaborazione dei dati e l'adattamento del modello possono richiedere un po' di tempo.

    È possibile notare che è stata aggiunta una nuova riga nuova contenente il modello serializzato nella colonna _model_ e il nome del modello **RxTrainLogit_model** nella colonna _name_.

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

Nel passaggio successivo si userà il modello sottoposto a training per generare stime.

## <a name="next-lesson"></a>Lezione successiva

[Lezione 4: Stimare i risultati potenziali usando un modello R in una stored procedure](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Lezione precedente

[Lezione 2: Creare caratteristiche dei dati usando funzioni T-SQL e R](..//tutorials/sqldev-create-data-features-using-t-sql.md)

