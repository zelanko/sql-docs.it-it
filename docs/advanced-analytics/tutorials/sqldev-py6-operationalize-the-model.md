---
title: Stimare i possibili risultati usando i modelli Python - SQL Server Machine Learning
description: Esercitazione che illustra come rendere operativi script PYthon incorporato in SQL Server stored procedure con funzioni di T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: e5f88beb2c429091fcea8ce66e4defa291e718d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961842"
---
# <a name="run-predictions-using-python-embedded-in-a-stored-procedure"></a>Eseguire le stime usando Python incorporato in una stored procedure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo fa parte di un'esercitazione [analitica di Python nel database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md). 

In questo passaggio viene illustrato come *rendere operativo* i modelli che è stato eseguito il training e salvato nel passaggio precedente.

In questo scenario, messa in funzione significa sulla distribuzione del modello nell'ambiente di produzione per l'assegnazione dei punteggi. L'integrazione con SQL Server rende questa piuttosto semplice, poiché è possibile incorporare codice Python in una stored procedure. Per ottenere le stime dal modello basato su nuovi input, è sufficiente chiamare la stored procedure da un'applicazione e passare i nuovi dati.

In questa lezione illustra due metodi per la creazione di stime basate su un modello Python: assegnazione dei punteggi e di una riga di punteggio batch.

- **Assegnazione dei punteggi batch:** Per fornire più righe di dati di input, passare una query di selezione come argomento alla stored procedure. Il risultato è una tabella di osservazioni corrispondenti ai case di input.
- **Assegnazione dei punteggi singoli:** Passare un set di valori dei singoli parametri come input.  La stored procedure restituisce una singola riga o un singolo valore.

Tutto il codice di Python necessario per il punteggio viene fornito come parte delle stored procedure.

## <a name="batch-scoring"></a>Punteggio batch

Le prime due stored procedure illustrano la sintassi di base per il wrapping di una chiamata di stima di Python in una stored procedure. Entrambe le stored procedure è necessaria una tabella di dati come input.

- Il nome del modello esatto da usare viene fornito come parametro di input per la stored procedure. La stored procedure consente di caricare il modello serializzato dalla tabella di database `nyc_taxi_models`.table, tramite l'istruzione SELECT nella stored procedure.
- Il modello serializzato è archiviato nella variabile Python `mod` per un'ulteriore elaborazione con Python.
- I nuovi casi devono essere calcolato il punteggio vengono ottenuti con la [!INCLUDE[tsql](../../includes/tsql-md.md)] query specificata nel `@input_data_1`. Man mano che vengono letti i dati della query, le righe vengono salvate nel frame di dati predefinito `InputDataSet`.
- Sia stored procedure usano le funzioni da `sklearn` per calcolare una metrica di accuratezza, AUC (area sotto curva). Se si specifica anche l'etichetta di destinazione può essere generata solo la metrica di accuratezza, ad esempio area sottesa alla curva (il _tipped_ colonna). Le stime non sono necessario l'etichetta di destinazione (variabile `y`), ma non il calcolo delle metriche di accuratezza.

    Pertanto, se non si dispone di etichette di destinazione per i dati a cui assegnare un punteggio, è possibile modificare la stored procedure per rimuovere i calcoli area sottesa alla curva e restituire solo le probabilità di suggerimento dalle funzionalità (variabile `X` nella stored procedure).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

Istruzioni Rrun T-SQL seguente per creare le stored procedure. Questa stored procedure richiede un modello di base di scikit-informazioni su pacchetto, perché Usa le funzioni specifiche per tale pacchetto:

+ Il frame di dati che contiene gli input viene passato per il `predict_proba` funzioni del modello di regressione logistica `mod`. Il `predict_proba` funzione (`probArray = mod.predict_proba(X)`) restituisce una **float** che rappresenta la probabilità che verrà concessa una Mancia (di qualsiasi importo).

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

Questa stored procedure Usa gli stessi input e crea lo stesso tipo dei punteggi come stored procedure precedente, ma usa le funzioni dal **revoscalepy** pacchetto fornito con SQL Server machine Learning Services.

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

## <a name="run-batch-scoring-using-a-select-query"></a>Eseguire l'assegnazione del punteggio batch utilizzando una query SELECT

Le stored procedure **PredictTipSciKitPy** e **PredictTipRxPy** richiede due parametri di input: 

- La query che recupera i dati per l'assegnazione dei punteggi
- Il nome di un modello con training

Passando gli argomenti per la stored procedure, è possibile selezionare un particolare modello o modificare i dati utilizzati per l'assegnazione dei punteggi.

1. Usare la **scikit-informazioni** del modello per l'assegnazione dei punteggi, chiamare la stored procedure **PredictTipSciKitPy**, passando il nome del modello e stringa di query come input.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    La stored procedure restituisce la probabilità stimate per ciascuna corsa che è stato passato come parte della query di input. 
    
    Se si usa SSMS (SQL Server Management Studio) per l'esecuzione di query, le probabilità vengono visualizzati come una tabella nel **risultati** riquadro. Il **messaggi** riquadro restituisce le metriche di accuratezza (area sottesa alla curva o, area under curve) con un valore di circa 0,56.

2. Usare la **revoscalepy** del modello per l'assegnazione dei punteggi, chiamare la stored procedure **PredictTipRxPy**, passando il nome del modello e stringa di query come input.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>Singola riga e di assegnazione dei punteggi

In alcuni casi, invece di assegnazione punteggio batch, si potrebbe decidere di passare in un singolo case, il recupero di valori da un'applicazione e la restituzione di un singolo risultato basato su tali valori. Ad esempio, è possibile impostare un foglio di lavoro Excel, l'applicazione web o report per chiamare la stored procedure e passare a esso gli input digitati o selezionati dagli utenti.

In questa sezione si apprenderà come creare le stime singole chiamando due stored procedure:

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy) è destinato a riga singola assegnazione del punteggio utilizzando il scikit-informazioni su modello.
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy) è destinato a riga singola assegnazione del punteggio utilizzando il modello revoscalepy.
+ Se ancora stato eseguito il training di un modello ancora, tornare alla [passaggio 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)!

Entrambe accettano modelli come input una serie di valori singoli, ad esempio il numero di passeggeri, distanza della corsa e così via. Una funzione con valori di tabella, `fnEngineerFeatures`, viene usato per convertire i valori di latitudine e longitudine dagli input a una nuova funzionalità, distanza diretta. [Lezione 4](sqldev-py4-create-data-features-using-t-sql.md) contiene una descrizione di questa funzione con valori di tabella.

Entrambe le stored procedure creano un punteggio in base al modello di Python.

> [!NOTE]
> 
> È importante fornire tutte le funzionalità di input richieste dal modello Python quando si chiama la stored procedure da un'applicazione esterna. Per evitare errori, è necessario eseguire il cast o convertire i dati di input in un tipo di dati di Python, oltre alla convalida tipo di dati e lunghezza dei dati.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

È opportuno esaminare il codice della stored procedure che esegue l'assegnazione del punteggio utilizzando il **scikit-informazioni su** modello.

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

La stored procedure seguente esegue l'assegnazione del punteggio utilizzando il **revoscalepy** modello.

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

### <a name="generate-scores-from-models"></a>Generare punteggi da modelli

Dopo aver create le stored procedure, è facile generare un punteggio in base a dei modelli. Aprire una nuova **Query** finestra e digitare o incollare i parametri per ognuna delle colonne di funzionalità. I sette necessari sono i valori per queste colonne di funzionalità, nell'ordine:
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. Per generare una stima utilizzando la **revoscalepy** modello, eseguita l'istruzione seguente:
  
    ```sql
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. Per generare un punteggio tramite il **scikit-informazioni su** modello, eseguita l'istruzione seguente:

    ```sql
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

L'output di entrambe le procedure è la probabilità di un suggerimento in corso a pagamento per una corsa in taxi con i parametri specificati o funzionalità.

## <a name="conclusions"></a>Conclusioni

In questa esercitazione si è appreso come usare il codice Python incorporato nelle stored procedure. L'integrazione con [!INCLUDE[tsql](../../includes/tsql-md.md)] rende molto più semplice per distribuire i modelli di Python per la stima e incorporare ripetizione del training del modello come parte di un flusso di lavoro dei dati aziendali.

## <a name="previous-step"></a>Passaggio precedente

[Eseguire il training e salvataggio di un modello Python](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>Vedere anche

[Estensione di Python in SQL Server](../concepts/extension-python.md)
