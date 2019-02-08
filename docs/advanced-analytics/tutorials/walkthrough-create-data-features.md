---
title: 'Creare funzionalità di dati usando funzioni R e SQL Server: SQL Server Machine Learning'
description: Esercitazione che illustra come creare funzioni di dati usando funzioni di SQL Server per l'analitica nel database.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 527f88ed14adc0140cbca179177e85670f72cafd
ms.sourcegitcommit: afc0c3e46a5fec6759fe3616e2d4ba10196c06d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2019
ms.locfileid: "55890012"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>Creare funzionalità di dati con R e SQL Server (procedura dettagliata)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Il data engineering è un'area importante dell'apprendimento automatico. I dati richiedono spesso trasformazione prima di usarlo per la modellazione predittiva. Se i dati non dispongono delle funzionalità necessarie, è possibile crearle da valori esistenti.

Per questa attività di modellazione, anziché usare i valori raw di latitudine e longitudine dei punti di inizio e fine della corsa si vuole avere la distanza in miglia tra le due posizioni. Per creare questa funzionalità, per calcolare la distanza lineare diretta tra due punti, utilizzando il [formula dell'emisenoverso](https://en.wikipedia.org/wiki/Haversine_formula).

In questo passaggio altre due metodi diversi per la creazione di una funzionalità dai dati:

> [!div class="checklist"]
> * Usando una funzione R personalizzata
> * Usando una funzione personalizzata T-SQL in [!INCLUDE[tsql](../../includes/tsql-md.md)]

L'obiettivo consiste nel creare una nuova [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] set di dati che includono le colonne originali oltre la nuova funzionalità numerica *direct_distance*.

## <a name="prerequisites"></a>Prerequisiti

Questo passaggio si presuppone una sessione di R in corso in base a quello precedente in questa procedura dettagliata. Usa connessione dati e stringhe di origine oggetti creati in tali passaggi. Gli strumenti e i pacchetti seguenti vengono utilizzati per eseguire lo script.

+ Rgui.exe per eseguire i comandi di R
+ Management Studio per eseguire T-SQL

## <a name="featurization-using-r"></a>Definizione delle funzionalità con R

Il linguaggio R è noto per le ricche e variate librerie statistiche, ma potrebbe essere ancora necessario creare trasformazioni di dati personalizzate.

Prima di tutto, eseguiamo la stessa operazione i modo R gli utenti sono abituati a: ottenere i dati al computer portatile, e quindi eseguire una funzione R personalizzata *ComputeDist*, che calcola la distanza lineare tra due punti specificati mediante i valori di latitudine e longitudine.

1. Tenere presente che l'oggetto origine dati creata in precedenza ottiene solo le prime 1000 righe. Pertanto, è importante definire una query che recupera tutti i dati.

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. Creare un nuovo oggetto origine dati usando la query.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) può richiedere una query costituita da una query valida, fornita come argomento per il _sqlQuery_ parametro o il nome di un oggetto tabella, fornito come il _tabella_ parametro.
    
    - Se si desidera i dati di esempio da una tabella, è necessario usare il _sqlQuery_ parametro, definire i parametri di campionamento usando la clausola TABLESAMPLE T-SQL e impostare le _rowBuffering_ argomento su FALSE.

3. Eseguire il codice seguente per creare la funzione R personalizzata. ComputeDist accetta due coppie di valori di latitudine e longitudine e calcola la distanza lineare tra di esse, restituendo la distanza in miglia.

    ```R
    env <- new.env();
    env$ComputeDist <- function(pickup_long, pickup_lat, dropoff_long, dropoff_lat){
      R <- 6371/1.609344 #radius in mile
      delta_lat <- dropoff_lat - pickup_lat
      delta_long <- dropoff_long - pickup_long
      degrees_to_radians = pi/180.0
      a1 <- sin(delta_lat/2*degrees_to_radians)
      a2 <- as.numeric(a1)^2
      a3 <- cos(pickup_lat*degrees_to_radians)
      a4 <- cos(dropoff_lat*degrees_to_radians)
      a5 <- sin(delta_long/2*degrees_to_radians)
      a6 <- as.numeric(a5)^2
      a <- a2+a3*a4*a6
      c <- 2*atan2(sqrt(a),sqrt(1-a))
      d <- R*c
      return (d)
    }
    ```
  
    + La prima riga definisce un nuovo ambiente. In R un ambiente può essere usato per incapsulare gli spazi dei nomi in pacchetti e strutture simili. È possibile usare la funzione `search()` per visualizzare gli ambienti nell'area di lavoro. Per visualizzare gli oggetti in un ambiente specifico, digitare `ls(<envname>)`.
    + Le righe che iniziano con `$env.ComputeDist` contengono il codice di definizione della formula dell'emisenoverso, che calcola la *distanza ortodromica* tra due punti su una sfera.

4. Dopo aver definito la funzione, si applica a dati per creare una nuova colonna di funzioni *direct_distance*. ma prima di eseguire la trasformazione, modificare il contesto di calcolo in locale.

    ```R
    rxSetComputeContext("local");
    ```

5. Chiamare il [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) per ottenere la funzionalità di progettazione dei dati e applicare il `env$ComputeDist` funzione per i dati in memoria.

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureDataSource,
    transforms = list(direct_distance=ComputeDist(pickup_longitude,pickup_latitude, dropoff_longitude, dropoff_latitude),
    tipped = "tipped", fare_amount = "fare_amount", passenger_count = "passenger_count",
    trip_time_in_secs = "trip_time_in_secs",  trip_distance="trip_distance",
    pickup_datetime = "pickup_datetime",  dropoff_datetime = "dropoff_datetime"),
    transformEnvir = env,
    rowsPerRead=500,
    reportProgress = 3);
  
    used.time <- proc.time() - start.time;
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""));
    ```

    + La funzione rxDataStep supporta vari metodi per la modifica dei dati nella posizione originale. Per altre informazioni, vedere questo articolo:  [Trasformazione e subset dei dati in R Microsft](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    Tuttavia, un paio di punti la pena notare riguardanti rxDataStep: 
    
    In altre origini dati, è possibile usare gli argomenti *varsToKeep* e *varsToDrop*, ma non sono supportati per le origini dati di SQL Server. Pertanto, in questo esempio è stato utilizzato il _trasforma_ argomento per specificare le colonne pass-through e le colonne trasformate. Inoltre, quando in esecuzione in un Server SQL di calcolo contesto, il _inData_ argomento può accettare solo un'origine dati SQL Server.

    Il codice precedente può inoltre generare un messaggio di avviso quando viene eseguito più grandi set di dati. Quando il numero di righe volte il numero delle colonne viene creato supera un valore impostato (il valore predefinito è 3,000,000) rxDataStep restituisce un avviso e verrà troncato il numero di righe nel frame di dati restituiti. Per rimuovere l'avviso, è possibile modificare il _maxRowsByCols_ argomento nella funzione rxDataStep. Tuttavia, se _maxRowsByCols_ è troppo grande, potrebbero verificarsi problemi durante il caricamento del frame di dati in memoria.

7. Facoltativamente, è possibile chiamare [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) per controllare lo schema dell'origine dati trasformati.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Definizione delle funzionalità con Transact-SQL

In questo esercizio, informazioni su come eseguire la stessa attività usando le funzioni SQL invece di funzioni R personalizzate. 

Passare a [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) o un altro editor di query per eseguire lo script T-SQL.

1. Usare una funzione SQL, denominata *fnCalculateDistance*. La funzione deve essere già esistente nel database NYCTaxi_Sample. In Esplora oggetti, verificare che la funzione esiste passando questo percorso: I database > NYCTaxi_Sample > programmabilità > funzioni > funzioni a valori scalari > dbo.fnCalculateDistance.

    Se la funzione non esiste, usare SQL Server Management Studio per generare la funzione nel database NYCTaxi_Sample.

    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function calculates the direct distance between two geographical coordinates.
    RETURNS
    AS
    BEGIN
      DECLARE @distance decimal(28, 10)
      -- Convert to radians
      SET @Lat1 = @Lat1 / 57.2958
      SET @Long1 = @Long1 / 57.2958
      SET @Lat2 = @Lat2 / 57.2958
      SET @Long2 = @Long2 / 57.2958
      -- Calculate distance
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
      --Convert to miles
      IF @distance <> 0
      BEGIN
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
      END
      RETURN @distance
    END
    ```

2. In Management Studio in una nuova finestra query, eseguire il comando seguente [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione da qualsiasi applicazione che supporta [!INCLUDE[tsql](../../includes/tsql-md.md)] per visualizzare l'effetto della funzione.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. Per inserire valori direttamente in una nuova tabella (è necessario prima crearlo), è possibile aggiungere un **INTO** clausola che specifica il nome della tabella.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. È anche possibile chiamare la funzione SQL dal codice R. Tornare a Rgui e archiviare la query di definizione delle funzionalità SQL in una variabile R.

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > Questa query è stata modificata per ottenere un campione di dati, per rendere più rapida di questa procedura dettagliata più piccolo. È possibile rimuovere la clausola TABLESAMPLE se si desidera ottenere tutti i dati. Tuttavia, a seconda dell'ambiente, potrebbe non essere possibile caricare il set completo di dati in R, causando un errore.
  
5. Usare le righe di codice seguenti per chiamare la funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] dall'ambiente R e applicarla ai dati definiti in *featureEngineeringQuery*.
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  Ora che viene creata la nuova funzionalità, chiamare **rxGetVarsInfo** per creare un riepilogo dei dati nella tabella delle funzionalità.
  
    ```R
    rxGetVarInfo(data = featureDataSource)
    ```

    **Risultati**

    ```R
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: numeric
    Var 4: trip_time_in_secs, Type: numeric
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: direct_distance, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: pickup_longitude, Type: numeric
    Var 11: dropoff_latitude, Type: numeric
    Var 12: dropoff_longitude, Type: numeric
    ```

    > [!NOTE]
    > In alcuni casi, potrebbe essere visualizzato un errore simile alla seguente: *È stata negata l'autorizzazione EXECUTE per l'oggetto 'fnCalculateDistance'* in questo caso, assicurarsi che l'account di accesso in uso disponga delle autorizzazioni per eseguire gli script e creare oggetti nel database, non solo nell'istanza.
    > Controllare lo schema per l'oggetto, fnCalculateDistance. Se l'oggetto è stato creato dal proprietario del database e l'account di accesso a cui appartiene il ruolo db_datareader, è necessario fornire l'account di accesso autorizzazioni esplicite per eseguire lo script.

## <a name="comparing-r-functions-and-sql-functions"></a>Confronto tra funzioni R e funzioni SQL

Tenere presente questo frammento di codice utilizzato per sincronizzare il codice R?

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

È possibile provare l'utilizzo con l'esempio di funzione personalizzata di SQL per visualizzare il tempo la trasformazione di dati necessario quando si chiama una funzione SQL. Inoltre, provare a passare i contesti di calcolo con rxSetComputeContext e confrontare gli intervalli di tempo.

I tempi possono variare in modo significativo, a seconda della velocità della rete e alla configurazione hardware. Nelle configurazioni di cui è stato testato, il [!INCLUDE[tsql](../../includes/tsql-md.md)] approccio alla funzione è stata più veloce rispetto all'uso di una funzione R personalizzata. Pertanto, è stato usato il [!INCLUDE[tsql](../../includes/tsql-md.md)] funzione per i calcoli in passaggi successivi.

> [!TIP]
> Molto spesso, progettazione di funzionalità con [!INCLUDE[tsql](../../includes/tsql-md.md)] risulterà più veloce rispetto a R. Ad esempio, T-SQL include windowing veloce e le funzioni di rango che possono essere applicate ai calcoli di analisi scientifica dei dati comuni, ad esempio medie mobili in sequenza e *n*-riquadri. Scegliere il metodo più efficace in base ai dati e all'attività eseguita.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Compilare un modello R e salvare in SQL](walkthrough-build-and-save-the-model.md)

