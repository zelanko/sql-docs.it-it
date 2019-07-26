---
title: Lezione 4 stimare i potenziali risultati con i modelli R
description: Esercitazione che illustra come rendere operativo script R incorporato in SQL Server stored procedure con funzioni T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: a3bd6671ee1f48c67f58e9b1ee17772b18184bc0
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469043"
---
# <a name="lesson-4-run-predictions-using-r-embedded-in-a-stored-procedure"></a>Lezione 4: Eseguire stime usando R incorporato in una stored procedure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo fa parte di un'esercitazione per sviluppatori SQL sull'uso di R in SQL Server.

In questo passaggio si apprenderà come usare il modello con nuove osservazioni per stimare potenziali risultati. Il modello viene racchiuso in un stored procedure che può essere chiamato direttamente da altre applicazioni. Nella procedura dettagliata vengono illustrati diversi modi per eseguire il Punteggio:

- Modalità di assegnazione dei **punteggi batch**: Usare una query SELECT come input per la stored procedure. La stored procedure restituisce una tabella di osservazioni corrispondenti ai casi di input.

- Modalità di assegnazione dei **punteggi individuali**: Passare un set di singoli valori di parametro come input.  La stored procedure restituisce una singola riga o un singolo valore.

In primo luogo si prenderà in analisi il funzionamento generale della valutazione.

## <a name="basic-scoring"></a>Punteggio di base

Il stored procedure **RxPredict** illustra la sintassi di base per il wrapping di una chiamata RevoScaleR RxPredict in una stored procedure.

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

+ L'istruzione SELECT ottiene il modello serializzato dal database e archivia il modello nella variabile `mod` R per un'ulteriore elaborazione con R.

+ I nuovi casi di assegnazione dei punteggi vengono ottenuti dalla [!INCLUDE[tsql](../../includes/tsql-md.md)] query specificata in `@inquery`, il primo parametro per la stored procedure. Man mano che vengono letti i dati della query, le righe vengono salvate nel frame di dati predefinito `InputDataSet`. Questo frame di dati viene passato alla funzione [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) in [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), che genera i punteggi.
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    Poiché un data.frame può contenere una riga singola, è possibile usare lo stesso codice per la valutazione batch e la valutazione singola.
  
+ Il valore restituito dalla `rxPredict` funzione è un valore **float** che rappresenta la probabilità che il driver ottenga una mancia di qualsiasi quantità.

## <a name="batch-scoring-a-list-of-predictions"></a>Punteggio batch (un elenco di stime)

Uno scenario più comune è quello di generare stime per più osservazioni in modalità batch. In questo passaggio verrà illustrato il funzionamento del Punteggio batch.

1.  Per iniziare, ottenere un set di dati di input più piccolo da usare. Questa query crea un elenco "top 10" delle corse, con il numero di passeggeri e altre funzionalità necessarie per effettuare una stima.
  
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

2. Creare un stored procedure denominato **RxPredictBatchOutput** in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

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

3.  Fornire il testo della query in una variabile e passarlo come parametro al stored procedure:

    ```sql
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'
    
    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[RxPredictBatchOutput] @model = 'RxTrainLogit_model', @inquery = @query_string;
    ```
  
Il stored procedure restituisce una serie di valori che rappresentano la stima per ognuno dei primi 10 viaggi. Tuttavia, i viaggi più frequenti sono anche corse a singolo passeggero con una distanza relativamente breve, per cui è improbabile che il driver ottenga un suggerimento.
  

> [!TIP]
> 
> Anziché restituire solo i risultati "Sì-Tip" e "No-Tip", è possibile restituire anche il Punteggio di probabilità per la stima, quindi applicare una clausola WHERE ai valori della colonna _Score_ per suddividere in categorie il punteggio come "suggerimento" o "suggerimento improbabile", usando un valore soglia, ad esempio 0,5 o 0,7. Questo passaggio non è incluso nella stored procedure, ma la sua implementazione non sarebbe difficile.

## <a name="single-row-scoring-of-multiple-inputs"></a>Assegnazione di punteggi a riga singola di più input

In alcuni casi si desidera passare più valori di input e ottenere una singola stima in base a tali valori. Ad esempio, è possibile configurare un foglio di lavoro di Excel, un'applicazione Web o un report Reporting Services per chiamare il stored procedure e fornire input tipizzati o selezionati dagli utenti da tali applicazioni.

In questa sezione viene illustrato come creare stime singole utilizzando un stored procedure che accetta più input, ad esempio il numero di passeggeri, la distanza di corsa e così via. Il stored procedure crea un punteggio in base al modello R archiviato in precedenza.
  
Se si chiama il stored procedure da un'applicazione esterna, assicurarsi che i dati corrispondano ai requisiti del modello R. Ciò può includere la verifica che i dati di input siano sottoponibili a cast o convertibili in un tipo di dati di R o la convalida del tipo di dati e della lunghezza dei dati. 

1. Creare un stored procedure **RxPredictSingleRow**.
  
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
  
    Aprire una nuova finestra di **query** e chiamare il stored procedure, specificando i valori per ognuno dei parametri. I parametri rappresentano le colonne di funzionalità utilizzate dal modello e sono obbligatorie.

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

    In alternativa, usare questa forma più breve supportata per i [parametri di un stored procedure](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```sql
    EXEC [dbo].[RxPredictSingleRow] 'RxTrainLogit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. I risultati indicano che la probabilità di ottenere un suggerimento è bassa (zero) per le prime 10 corse, perché tutte sono viaggi a passeggero singolo su una distanza relativamente breve.

## <a name="conclusions"></a>Conclusioni

In questo modo si conclude l'esercitazione. Ora che si è appreso come incorporare il codice R nelle stored procedure, è possibile estendere queste procedure per creare modelli personalizzati. L'integrazione con [!INCLUDE[tsql](../../includes/tsql-md.md)] semplifica notevolmente la distribuzione di modelli R per le stime e l'inclusione delle ripetizioni del training dei modelli nel flusso di lavoro dei dati enterprise.

## <a name="previous-lesson"></a>Lezione precedente

[Lezione 3: Eseguire il training e salvare un modello R usando T-SQL](sqldev-train-and-save-a-model-using-t-sql.md)
