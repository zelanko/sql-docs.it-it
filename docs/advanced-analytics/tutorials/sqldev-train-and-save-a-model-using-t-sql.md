---
title: Lezione 3 eseguire il training e il salvataggio di un modello usando R e T-SQL
description: Esercitazione che illustra come eseguire il training, la serializzazione e il salvataggio di un modello R usando SQL Server stored procedure e funzioni T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0825d99aee2639d28e95dfcaf79e1a8e915bf25a
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470539"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>Lezione 3: Eseguire il training e salvare un modello usando T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo fa parte di un'esercitazione per sviluppatori SQL sull'uso di R in SQL Server.

In questa lezione verrà illustrato come eseguire il training di un modello di apprendimento automatico usando R. Verrà eseguito il training del modello utilizzando le funzionalità dei dati create nella lezione precedente, quindi il modello sottoposto a training viene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] salvato in una tabella. In questo caso, i pacchetti R sono già installati con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], quindi è possibile eseguire tutte le operazioni da SQL.

## <a name="create-the-stored-procedure"></a>Creare il stored procedure

Quando si chiama R da T-SQL, si usa il stored procedure di sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Tuttavia, per i processi ripetuti spesso, ad esempio la ripetizione del training di un modello, è più semplice incapsulare la chiamata a sp_execute_exernal_script in un altro stored procedure.

1. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]aprire una nuova finestra **query** .

2. Eseguire l'istruzione seguente per creare il stored procedure **RxTrainLogitModel**. Questo stored procedure definisce i dati di input e USA **rxLogit** da RevoScaleR per creare un modello di regressione logistica.

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

    - Per assicurarsi che alcuni dati vengano lasciati a test del modello, il 70% dei dati viene selezionato in modo casuale dalla tabella dei dati del taxi a scopo di training.

    - La query SELECT usa la funzione scalare personalizzata *fnCalculateDistance* per calcolare la distanza diretta tra la posizione di salita e discesa dei passeggeri. I risultati della query vengono archiviati nella variabile `InputDataset`di input R predefinita.
  
    - Lo script r chiama la funzione **rxLogit** , che è una delle funzioni R avanzate incluse in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], per creare il modello di regressione logistica.
  
        La variabile binaria _tipped_ viene usata come *etichetta* o come colonna dei risultati. Il modello si adatta usando le colonne delle funzionalità seguenti:  _passenger_count_, _trip_distance_, _trip_time_in_secs_e _direct_distance_.
  
    - Il modello sottoposto a training, salvato nella `logitObj`variabile R, viene serializzato e restituito come parametro di output.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>Eseguire il training e distribuire il modello R usando il stored procedure

Poiché il stored procedure include già una definizione dei dati di input, non è necessario fornire una query di input.

1. Per eseguire il training e distribuire il modello R, chiamare il stored procedure e inserirlo nella tabella di database _nyc_taxi_models_, in modo da poterlo usare per le stime future:

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. Osservare la finestra **messaggi** di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per i messaggi che verrebbero inviati al flusso **stdout** di R, come questo messaggio: 

    "Messaggi STDOUT dallo script esterno: Righe lette: 1193025, totale righe elaborate: 1193025, tempo totale blocco: 0,093 secondi "

    È anche possibile visualizzare messaggi specifici per la singola funzione, `rxLogit`, che visualizza le variabili e le metriche di test generate come parte della creazione del modello.

3.  Al termine dell'istruzione, aprire la tabella *nyc_taxi_models*. L'elaborazione dei dati e l'adattamento del modello potrebbero richiedere alcuni minuti.

    È possibile notare che è stata aggiunta una nuova riga che contiene il modello serializzato nel _modello_ di colonna e il nome del modello **RxTrainLogit_model** nel _nome_della colonna.

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

Nel passaggio successivo verrà usato il modello sottoposto a training per generare stime.

## <a name="next-lesson"></a>Lezione successiva

[Lezione 4: Stimare potenziali risultati usando un modello R in un stored procedure](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Lezione precedente

[Lezione 2: Creare funzionalità di dati usando funzioni R e T-SQL](..//tutorials/sqldev-create-data-features-using-t-sql.md)

