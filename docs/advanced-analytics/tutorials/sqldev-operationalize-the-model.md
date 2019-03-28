---
title: Lezione 4 Predict potenziali dei risultati mediante i modelli R - SQL Server Machine Learning
description: Esercitazione che illustra come rendere operativi script R incorporato in SQL Server stored procedure con funzioni di T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4e74f587177c31f55c952eb06ccb8a7e8960c93a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511588"
---
# <a name="lesson-4-run-predictions-using-r-embedded-in-a-stored-procedure"></a>Lezione 4: Eseguire le stime usando R incorporato in una stored procedure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo fa parte di un'esercitazione per sviluppatori SQL su come usare R in SQL Server.

In questo passaggio descrive come utilizzare il modello rispetto a nuove osservazioni per stimare i possibili risultati. Il modello viene eseguito il wrapping in una stored procedure che può essere chiamata direttamente da altre applicazioni. La procedura dettagliata illustra diversi modi per eseguire l'assegnazione dei punteggi:

- **Modalità di valutazione batch**: Usare una query di selezione come input per la stored procedure. La stored procedure restituisce una tabella di osservazioni corrispondenti ai casi di input.

- **Modalità di assegnazione dei punteggi singoli**: Passare un set di valori dei singoli parametri come input.  La stored procedure restituisce una singola riga o un singolo valore.

In primo luogo si prenderà in analisi il funzionamento generale della valutazione.

## <a name="basic-scoring"></a>Valutazione di base

La stored procedure **RxPredict** viene illustrata la sintassi di base per il wrapping di una chiamata rxPredict RevoScaleR in una stored procedure.

```sql
CREATE PROCEDURE [dbo].[RxPredict] (@model varchar(250), @inquery nvarchar(max))
AS 
BEGIN 

DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);  
EXEC sp_execute_external_script @language = N'R',
  @script = N' 
    mod <- unserialize(as.raw(model)); 
    print(summary(mod)) 
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE); 
    str(OutputDataSet) 
    print(OutputDataSet) 
    ', 
  @input_data_1 = @inquery, 
  @params = N'@model varbinary(max)',
  @model = @lmodel2 
  WITH RESULT SETS ((Score float));
END
GO
```

+ L'istruzione SELECT recupera il modello serializzato dal database e il modello viene archiviato nella variabile R `mod` per un'ulteriore elaborazione con R.

+ Per assegnare punteggi ai nuovi casi vengono ottenuti dal [!INCLUDE[tsql](../../includes/tsql-md.md)] specificata nella query `@inquery`, il primo parametro alla stored procedure. Man mano che vengono letti i dati della query, le righe vengono salvate nel frame di dati predefinito `InputDataSet`. Il frame di dati viene passato per il [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) funzionare in [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), che genera i punteggi.
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    Poiché un data.frame può contenere una riga singola, è possibile usare lo stesso codice per la valutazione batch e la valutazione singola.
  
+ Il valore restituito per il `rxPredict` funzione è un **float** che rappresenta la probabilità che il driver Ottiene un suggerimento di qualsiasi quantità.

## <a name="batch-scoring-a-list-of-predictions"></a>(Un elenco di stime) di assegnazione punteggio batch

Uno scenario più comune consiste nel generare stime per più osservazioni in modalità batch. In questo passaggio vediamo come funziona il punteggio batch.

1.  Iniziare recuperando un set di dati di input per lavorare con più piccolo. Questa query crea un elenco "top 10" delle corse, con il numero di passeggeri e altre funzionalità necessarie per effettuare una stima.
  
    ```sql
    SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    
    FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

    LEFT OUTER JOIN

    (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime
    WHERE b.medallion IS NULL
    ```

    **Risultati di esempio**
    
    ```sql
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

2. Creare una stored procedure denominata **RxPredictBatchOutput** in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

    ```sql
    CREATE PROCEDURE [dbo].[RxPredictBatchOutput] (@model varchar(250), @inquery nvarchar(max))
    AS
    BEGIN
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
    EXEC sp_execute_external_script 
      @language = N'R',
      @script = N'
        mod <- unserialize(as.raw(model));
        print(summary(mod))
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);
        str(OutputDataSet)
        print(OutputDataSet)
      ',
      @input_data_1 = @inquery,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

3.  Specificare il testo della query in una variabile e passarla come parametro alla stored procedure:

    ```sql
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'
    
    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[RxPredictBatchOutput] @model = 'RxTrainLogit_model', @inquery = @query_string;
    ```
  
La stored procedure restituisce una serie di valori che rappresentano la stima per ognuna delle corse primi 10. Tuttavia, le corse principali sono anche un singolo passeggero e con una distanza relativamente breve, per i quali il driver è improbabile che riceverà una Mancia.
  

> [!TIP]
> 
> Invece di restituire solo il "Mancia Sì" e i risultati di tipo "senza Mancia", è possibile restituire anche il punteggio di probabilità per la stima e quindi applicare una clausola WHERE per il _punteggio_ valori di colonna da classificare il punteggio come "Mancia probabile" o " Mancia poco probabile", usando un valore di soglia, ad esempio 0.5 o 0.7. Questo passaggio non è incluso nella stored procedure, ma la sua implementazione non sarebbe difficile.

## <a name="single-row-scoring-of-multiple-inputs"></a>Riga singola assegnazione dei punteggi di più input

Talvolta si desidera passare più valori di input e ottenere una sola stima in base a tali valori. Ad esempio, è possibile impostare backup di un foglio di lavoro di Excel, applicazione web o report di Reporting Services per chiamare la stored procedure e renda disponibili input digitati o selezionati dagli utenti da tali applicazioni.

In questa sezione descrive come creare stime singole usando una stored procedure che accetta più input, ad esempio il numero di passeggeri, distanza della corsa e così via. La stored procedure crea un punteggio in base al modello R archiviato in precedenza.
  
Se si chiama la stored procedure da un'applicazione esterna, assicurarsi che i dati soddisfino i requisiti del modello R. Ciò può includere la verifica che i dati di input siano sottoponibili a cast o convertibili in un tipo di dati di R o la convalida del tipo di dati e della lunghezza dei dati. 

1. Creare una stored procedure **RxPredictSingleRow**.
  
    ```sql
    CREATE PROCEDURE [dbo].[RxPredictSingleRow] @model varchar(50), @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
    AS
    BEGIN
    DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
    EXEC sp_execute_external_script  
      @language = N'R',
      @script = N'  
        mod <- unserialize(as.raw(model));  
        print(summary(mod));  
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
        str(OutputDataSet);
        print(OutputDataSet); 
        ',  
      @input_data_1 = @inquery,  
      @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float', @model = @lmodel2, @passenger_count =@passenger_count, @trip_distance=@trip_distance, @trip_time_in_secs=@trip_time_in_secs, @pickup_latitude=@pickup_latitude, @pickup_longitude=@pickup_longitude, @dropoff_latitude=@dropoff_latitude, @dropoff_longitude=@dropoff_longitude  
      WITH RESULT SETS ((Score float));  
    END
    ```

2. Provare la stored procedure inserendo manualmente i valori.
  
    Aprire una nuova **Query** finestra e chiamare la stored procedure, fornire valori per ognuno dei parametri. I parametri rappresentano le colonne di funzionalità utilizzate dal modello e sono necessari.

    ```sql
    EXEC [dbo].[RxPredictSingleRow] @model = 'RxTrainLogit_model',
    @passenger_count = 1,
    @trip_distance = 2.5,
    @trip_time_in_secs = 631,
    @pickup_latitude = 40.763958,
    @pickup_longitude = -73.973373,
    @dropoff_latitude =  40.782139,
    @dropoff_longitude = -73.977303
    ```

    In alternativa, usare questo formato più breve è supportato per [parametri a una stored procedure](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```sql
    EXEC [dbo].[RxPredictSingleRow] 'RxTrainLogit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. I risultati indicano che la probabilità di ricevere una Mancia è bassa (zero) in queste corse primi 10, poiché tutti sono un singolo passeggero e su una distanza relativamente breve.

## <a name="conclusions"></a>Conclusioni

In questo modo si conclude l'esercitazione. Ora che si è appreso come incorporare il codice R nelle stored procedure, è possibile estendere queste procedure consigliate per la creazione di modelli personalizzati. L'integrazione con [!INCLUDE[tsql](../../includes/tsql-md.md)] semplifica notevolmente la distribuzione di modelli R per le stime e l'inclusione delle ripetizioni del training dei modelli nel flusso di lavoro dei dati enterprise.

## <a name="previous-lesson"></a>Lezione precedente

[Lezione 3: Training e salvataggio di un modello R usando T-SQL](sqldev-train-and-save-a-model-using-t-sql.md)
