---
title: Stimare potenziali risultati usando i modelli Python
description: Esercitazione che illustra come rendere operativo script PYthon incorporato in SQL Server stored procedure con funzioni T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: b04e57c45c6113d4a0404a3a338e6beba4cda813
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468594"
---
# <a name="run-predictions-using-python-embedded-in-a-stored-procedure"></a>Eseguire stime con Python incorporato in una stored procedure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo fa parte di un'esercitazione [relativa all'analisi Python nel database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md). 

In questo passaggio si apprenderà come *rendere operativo* i modelli di cui è stato eseguito il training e il salvataggio nel passaggio precedente.

In questo scenario, la messa in funzione comporta la distribuzione del modello in produzione per l'assegnazione dei punteggi. L'integrazione con SQL Server rende questa operazione abbastanza semplice, perché è possibile incorporare il codice Python in una stored procedure. Per ottenere stime dal modello in base ai nuovi input, è sufficiente chiamare il stored procedure da un'applicazione e passare i nuovi dati.

In questa lezione vengono illustrati due metodi per la creazione di stime basate su un modello Python: Punteggio batch e punteggio riga per riga.

- **Punteggio batch:** Per fornire più righe di dati di input, passare una query SELECT come argomento al stored procedure. Il risultato è una tabella di osservazioni corrispondenti ai case di input.
- **Punteggio singolo:** Passare un set di singoli valori di parametro come input.  La stored procedure restituisce una singola riga o un singolo valore.

Tutto il codice Python necessario per l'assegnazione dei punteggi viene fornito come parte delle stored procedure.

## <a name="batch-scoring"></a>Punteggio batch

Nelle prime due stored procedure viene illustrata la sintassi di base per eseguire il wrapping di una chiamata di stima Python in un stored procedure. Per entrambe le stored procedure è necessaria una tabella di dati come input.

- Il nome del modello esatto da usare viene fornito come parametro di input per il stored procedure. Il stored procedure carica il modello serializzato dal database Table `nyc_taxi_models`. Table, utilizzando l'istruzione SELECT nel stored procedure.
- Il modello serializzato viene archiviato nella variabile `mod` Python per un'ulteriore elaborazione con Python.
- I nuovi casi che devono essere classificati vengono ottenuti dalla [!INCLUDE[tsql](../../includes/tsql-md.md)] query specificata in. `@input_data_1` Man mano che vengono letti i dati della query, le righe vengono salvate nel frame di dati predefinito `InputDataSet`.
- Entrambe stored procedure usano funzioni da `sklearn` per calcolare una metrica di accuratezza, AUC (area sotto curva). È possibile generare metriche di accuratezza, ad esempio AUC, solo se si specifica anche l'etichetta di destinazione (colonna con _Tipp_ ). Per le stime non è necessaria l'etichetta di destinazione `y`(variabile), ma il calcolo della metrica di accuratezza.

    Se pertanto non si dispone di etichette di destinazione per i dati a cui assegnare un punteggio, è possibile modificare il stored procedure per rimuovere i calcoli AUC e restituire solo le probabilità di suggerimento dalle funzionalità ( `X` variabile nel stored procedure).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

Rrun le istruzioni T-SQL seguenti per creare le stored procedure. Questo stored procedure richiede un modello basato sul pacchetto Scikit-learn, perché usa funzioni specifiche del pacchetto:

+ Il frame di dati contenente gli input viene passato `predict_proba` alla funzione del `mod`modello di regressione logistica. La `predict_proba` funzione (`probArray = mod.predict_proba(X)`) restituisce un valore **float** che rappresenta la probabilità che venga assegnata una mancia (di qualsiasi quantità).

```sql
DROP PROCEDURE IF EXISTS PredictTipSciKitPy;
GO

CREATE PROCEDURE [dbo].[PredictTipSciKitPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script
  @language = N'Python',
  @script = N'
import pickle;
import numpy;
from sklearn import metrics

mod = pickle.loads(lmodel2)
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
y = numpy.ravel(InputDataSet[["tipped"]])

probArray = mod.predict_proba(X)
probList = []
for i in range(len(probArray)):
  probList.append((probArray[i])[1])

probArray = numpy.asarray(probList)
fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
aucResult = metrics.auc(fpr, tpr)
print ("AUC on testing data is: " + str(aucResult))

OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',  
  @input_data_1 = @inquery,
  @input_data_1_name = N'InputDataSet',
  @params = N'@lmodel2 varbinary(max)',
  @lmodel2 = @lmodel2
WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttiprxpy"></a>PredictTipRxPy

Questo stored procedure usa gli stessi input e crea lo stesso tipo di punteggi della stored procedure precedente, ma usa le funzioni del pacchetto **revoscalepy** fornito con SQL Server machine learning.

```sql
DROP PROCEDURE IF EXISTS PredictTipRxPy;
GO

CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script 
  @language = N'Python',
  @script = N'
import pickle;
import numpy;
from sklearn import metrics
from revoscalepy.functions.RxPredict import rx_predict;

mod = pickle.loads(lmodel2)
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
y = numpy.ravel(InputDataSet[["tipped"]])

probArray = rx_predict(mod, X)
probList = probArray["tipped_Pred"].values 

probArray = numpy.asarray(probList)
fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
aucResult = metrics.auc(fpr, tpr)
print ("AUC on testing data is: " + str(aucResult))

OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',  
  @input_data_1 = @inquery,
  @input_data_1_name = N'InputDataSet',
  @params = N'@lmodel2 varbinary(max)',
  @lmodel2 = @lmodel2
WITH RESULT SETS ((Score float));
END
GO
```

## <a name="run-batch-scoring-using-a-select-query"></a>Eseguire il Punteggio batch usando una query SELECT

Le stored procedure **PredictTipSciKitPy** e **PredictTipRxPy** richiedono due parametri di input: 

- Query che recupera i dati per l'assegnazione dei punteggi
- Nome di un modello sottoposto a training

Passando gli argomenti alla stored procedure, è possibile selezionare un determinato modello o modificare i dati usati per l'assegnazione dei punteggi.

1. Per usare il modello **Scikit-learn** per l'assegnazione dei punteggi, chiamare il stored procedure **PredictTipSciKitPy**, passando il nome del modello e la stringa di query come input.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    Il stored procedure restituisce le probabilità stimate per ogni viaggio passato come parte della query di input. 
    
    Se si utilizza SSMS (SQL Server Management Studio) per l'esecuzione di query, le probabilità verranno visualizzate come una tabella nel riquadro **risultati** . Il riquadro **messaggi** restituisce la metrica di accuratezza (AUC o area sotto la curva) con un valore pari a circa 0,56.

2. Per usare il modello **revoscalepy** per l'assegnazione dei punteggi, chiamare il stored procedure **PredictTipRxPy**, passando il nome del modello e la stringa di query come input.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>Assegnazione di punteggi a riga singola

A volte, anziché assegnare un punteggio batch, è possibile passare un singolo case, ottenere i valori da un'applicazione e restituire un singolo risultato in base a tali valori. Ad esempio, è possibile configurare un foglio di lavoro di Excel, un'applicazione Web o un report per chiamare il stored procedure e passarvi input tipizzati o selezionati dagli utenti.

In questa sezione verrà illustrato come creare stime singole chiamando due stored procedure:

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy) è progettato per l'assegnazione di punteggi a riga singola usando il modello Scikit-learn.
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy) è progettato per l'assegnazione di punteggi a riga singola usando il modello revoscalepy.
+ Se non è ancora stato eseguito il training di un modello, tornare al [passaggio 5](sqldev-py5-train-and-save-a-model-using-t-sql.md).

Entrambi i modelli accettano come input una serie di valori singoli, ad esempio il numero di passeggeri, la distanza di corsa e così via. Una funzione con valori di tabella `fnEngineerFeatures`,, viene utilizzata per convertire i valori di latitudine e Longitudine dagli input in una nuova funzionalità, ovvero la distanza diretta. La [lezione 4](sqldev-py4-create-data-features-using-t-sql.md) contiene una descrizione di questa funzione con valori di tabella.

Entrambe le stored procedure creano un punteggio basato sul modello Python.

> [!NOTE]
> 
> È importante fornire tutte le funzionalità di input richieste dal modello Python quando si chiama il stored procedure da un'applicazione esterna. Per evitare errori, potrebbe essere necessario eseguire il cast o convertire i dati di input in un tipo di dati Python, oltre a convalidare il tipo di dati e la lunghezza dei dati.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Esaminare il codice del stored procedure che esegue il punteggio usando il modello **Scikit-learn** .

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeSciKitPy;
GO

CREATE PROCEDURE [dbo].[PredictTipSingleModeSciKitPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
    '
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script 
  @language = N'Python',
  @script = N'
import pickle;
import numpy;

# Load model and unserialize
mod = pickle.loads(model)

# Get features for scoring from input data
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]

# Score data to get tip prediction probability as a list (of float)
probList = []
probList.append((mod.predict_proba(X)[0])[1])

# Create output data frame
OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',
  @input_data_1 = @inquery,
  @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
    @trip_time_in_secs int ,
    @pickup_latitude float ,
    @pickup_longitude float ,
    @dropoff_latitude float ,
    @dropoff_longitude float',
    @model = @lmodel2,
    @passenger_count =@passenger_count ,
    @trip_distance=@trip_distance,
    @trip_time_in_secs=@trip_time_in_secs,
    @pickup_latitude=@pickup_latitude,
    @pickup_longitude=@pickup_longitude,
    @dropoff_latitude=@dropoff_latitude,
    @dropoff_longitude=@dropoff_longitude
WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttipsinglemoderxpy"></a>PredictTipSingleModeRxPy

Il stored procedure seguente esegue il punteggio usando il modello **revoscalepy** .

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeRxPy;
GO

CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
  '
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script 
  @language = N'Python',
  @script = N'
import pickle;
import numpy;
from revoscalepy.functions.RxPredict import rx_predict;

# Load model and unserialize
mod = pickle.loads(model)

# Get features for scoring from input data
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]

# Score data to get tip prediction probability as a list (of float)

probArray = rx_predict(mod, X)

probList = []
probList = probArray["tipped_Pred"].values

# Create output data frame
OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',
  @input_data_1 = @inquery,
  @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
    @trip_time_in_secs int ,
    @pickup_latitude float ,
    @pickup_longitude float ,
    @dropoff_latitude float ,
    @dropoff_longitude float',
    @model = @lmodel2,
    @passenger_count =@passenger_count ,
    @trip_distance=@trip_distance,
    @trip_time_in_secs=@trip_time_in_secs,
    @pickup_latitude=@pickup_latitude,
    @pickup_longitude=@pickup_longitude,
    @dropoff_latitude=@dropoff_latitude,
    @dropoff_longitude=@dropoff_longitude
WITH RESULT SETS ((Score float));
END
GO
```

### <a name="generate-scores-from-models"></a>Genera punteggi dai modelli

Una volta create le stored procedure, è facile generare un punteggio in base a uno dei due modelli. È sufficiente aprire una nuova finestra di **query** e digitare o incollare i parametri per ogni colonna della funzionalità. I sette valori richiesti sono per queste colonne di funzionalità, in ordine:
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. Per generare una stima tramite il modello **revoscalepy** , eseguire l'istruzione seguente:
  
    ```sql
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. Per generare un punteggio usando il modello **Scikit-learn** , eseguire questa istruzione:

    ```sql
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

L'output di entrambe le procedure è la probabilità che una mancia venga pagata per il viaggio in taxi con i parametri o le funzionalità specificate.

## <a name="conclusions"></a>Conclusioni

In questa esercitazione si è appreso come usare il codice Python incorporato nelle stored procedure. L'integrazione con [!INCLUDE[tsql](../../includes/tsql-md.md)] rende molto più semplice la distribuzione di modelli Python per la stima e la ripetizione del training del modello come parte di un flusso di lavoro dei dati aziendali.

## <a name="previous-step"></a>Passaggio precedente

[Eseguire il training e salvare un modello Python](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>Vedere anche

[Estensione Python in SQL Server](../concepts/extension-python.md)
