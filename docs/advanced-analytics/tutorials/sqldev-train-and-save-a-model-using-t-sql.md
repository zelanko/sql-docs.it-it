---
title: 'Lezione 3 training e salvataggio di un modello usando R e T-SQL: SQL Server Machine Learning'
description: Esercitazione che illustra come eseguire il training, serializzare e salvare un modello R con SQL Server stored procedure e funzioni T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f3abe58aac4d5920e64337f63a40dc8f87fb12d9
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645110"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>Lezione 3: Eseguire il training e salvataggio di un modello usando T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo fa parte di un'esercitazione per sviluppatori SQL su come usare R in SQL Server.

In questa lezione si apprenderà come eseguire il training di un modello di machine learning tramite R. Si sarà il training del modello usando le funzionalità di dati creato nella lezione precedente e quindi salvare il modello con Training in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella. In questo caso, i pacchetti R sono già installati insieme [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], in modo che tutto ciò che può essere eseguita da SQL.

## <a name="create-the-stored-procedure"></a>Creare la stored procedure

Quando si chiama R da T-SQL, si utilizza la stored procedure di sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Tuttavia, per i processi che si ripete spesso, ad esempio un modello di ripetizione del training è più semplice incapsulare la chiamata a sp_execute_exernal_script in un'altra stored procedure.

1. Nelle [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], aprire una nuova **Query** finestra.

2. Eseguire l'istruzione seguente per creare la stored procedure **RxTrainLogitModel**. Questa stored procedure definisce i dati di input e Usa **rxLogit** da RevoScaleR per creare un modello di regressione logistica.

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

    - Per garantire che alcuni dati rimarranno per testare il modello, il 70% dei dati vengono selezionate casualmente tra la tabella di dati dei taxi per il training.

    - La query SELECT usa la funzione scalare personalizzata *fnCalculateDistance* per calcolare la distanza diretta tra la posizione di salita e discesa dei passeggeri. i risultati della query vengono archiviati nella variabile di input R predefinita `InputDataset`.
  
    - Lo script R chiama il **rxLogit** funzione, vale a dire una delle funzioni R avanzate incluse con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], per creare il modello di regressione logistica.
  
        La variabile binaria _tipped_ viene usata come *etichetta* o come colonna dei risultati. Il modello si adatta usando le colonne delle funzionalità seguenti:  _passenger_count_, _trip_distance_, _trip_time_in_secs_e _direct_distance_.
  
    - Il modello con training, salvato nella variabile R `logitObj`viene serializzato e restituito come parametro di output.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>Eseguire il training e distribuire il modello R tramite stored procedure

Poiché la stored procedure include già una definizione dei dati di input, non è necessario fornire una query di input.

1. Per eseguire il training e distribuire il modello R, chiamare la stored procedure e la inserisce nella tabella di database _nyc_taxi_models_, in modo che è possibile usarlo per stime future:

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. Guarda il **messaggi** finestra di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per i messaggi che sarebbero inoltrati di R **stdout** flusso, ad esempio questo messaggio: 

    "Messaggi STDOUT dallo script esterno: Righe lette: 1193025, totale righe elaborate: 1193025, tempo di blocco totale: 0.093 secondi"

    È anche possibile visualizzare messaggi specifici per la singola funzione, `rxLogit`, visualizzare le variabili e le metriche generate come parte della creazione del modello di test.

3.  Quando l'istruzione è stata completata, aprire la tabella *nyc_taxi_models*. L'elaborazione dei dati e l'adattamento del modello potrebbe richiedere qualche minuto.

    È possibile visualizzare una nuova riga è stato aggiunto, che contiene il modello serializzato nella colonna _model_ e il nome del modello **RxTrainLogit_model** nella colonna _nome_.

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

Nel passaggio successivo si userà il modello con training per generare stime.

## <a name="next-lesson"></a>Lezione successiva

[Lezione 4: Stimare i possibili risultati usando un modello R in una stored procedure](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Lezione precedente

[Lezione 2: Creare funzionalità di dati usando funzioni R e T-SQL](..//tutorials/sqldev-create-data-features-using-t-sql.md)

