---
title: Creare funzionalità di dati usando R e funzioni SQL Server
description: Esercitazione che illustra come creare funzionalità di dati usando funzioni di SQL Server per l'analisi nel database.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: a7d62004745f8b77bbc26b4d924e2e3948cf2f9e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345839"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>Creare funzionalità di dati usando R e SQL Server (procedura dettagliata)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Il data engineering è un'area importante dell'apprendimento automatico. I dati richiedono spesso la trasformazione prima di poter essere usati per la modellazione predittiva. Se i dati non dispongono delle funzionalità necessarie, è possibile crearle da valori esistenti.

Per questa attività di modellazione, anziché usare i valori raw di latitudine e longitudine dei punti di inizio e fine della corsa si vuole avere la distanza in miglia tra le due posizioni. Per creare questa funzionalità, calcolare la distanza lineare diretta tra due punti, usando la [formula haversine](https://en.wikipedia.org/wiki/Haversine_formula).

In questo passaggio vengono illustrati due metodi diversi per la creazione di una funzionalità dai dati:

> [!div class="checklist"]
> * Uso di una funzione R personalizzata
> * Uso di una funzione T-SQL personalizzata in[!INCLUDE[tsql](../../includes/tsql-md.md)]

Lo scopo è quello di creare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nuovo set di dati che includa le colonne originali più la nuova funzionalità numerica, *direct_distance*.

## <a name="prerequisites"></a>Prerequisiti

Questo passaggio presuppone una sessione R in corso in base ai passaggi precedenti di questa procedura dettagliata. Usa le stringhe di connessione e gli oggetti origine dati creati in questi passaggi. Per eseguire lo script vengono usati gli strumenti e i pacchetti seguenti.

+ Rgui. exe per l'esecuzione di comandi R
+ Management Studio per eseguire T-SQL

## <a name="featurization-using-r"></a>Conteggi con R

Il linguaggio R è noto per le ricche e variate librerie statistiche, ma potrebbe essere ancora necessario creare trasformazioni di dati personalizzate.

In primo luogo, è possibile eseguire questa operazione nel modo in cui gli utenti di R sono abituati a: ottenere i dati nel portatile e quindi eseguire una funzione R personalizzata, *ComputeDist*, che calcola la distanza lineare tra due punti specificati da valori di latitudine e longitudine.

1. Tenere presente che l'oggetto origine dati creato in precedenza ottiene solo le prime 1000 righe. Quindi, definiamo una query che ottiene tutti i dati.

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. Creare un nuovo oggetto origine dati utilizzando la query.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) può richiedere una query di selezione valida, fornita come argomento al parametro sqlQuery, oppure il nome  di un oggetto Table, fornito come parametro _Table_ .
    
    - Se si desidera campionare i dati da una tabella, è necessario utilizzare  il parametro sqlQuery, definire i parametri di campionamento utilizzando la clausola T-SQL TABLESAMPLE e impostare l'argomento _rowBuffering_ su false.

3. Eseguire il codice seguente per creare la funzione R personalizzata. ComputeDist accetta due coppie di valori di latitudine e longitudine e calcola la distanza lineare tra di essi, restituendo la distanza in miglia.

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

4. Dopo aver definito la funzione, applicarla ai dati per creare una nuova colonna di funzionalità, *direct_distance*. prima di eseguire la trasformazione, tuttavia, impostare il contesto di calcolo su local.

    ```R
    rxSetComputeContext("local");
    ```

5. Chiamare la funzione [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) per ottenere i dati di progettazione delle funzionalità e applicare `env$ComputeDist` la funzione ai dati in memoria.

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

    + La funzione rxDataStep supporta vari metodi per la modifica dei dati sul posto. Per altre informazioni, vedere questo articolo:  [Come trasformare i dati e sottosubset in Microsft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    Tuttavia, si noti un paio di punti relativi a rxDataStep: 
    
    In altre origini dati è possibile usare gli argomenti *varsToKeep* e *varsToDrop*, ma questi non sono supportati per le origini dati SQL Server. Pertanto, in questo esempio è stato usato l'argomento  Transformations per specificare sia le colonne pass-through sia le colonne trasformate. Inoltre, in caso di esecuzione in un SQL Server contesto di calcolo  , l'argomento indata può assumere solo un'origine dati SQL Server.

    Il codice precedente può inoltre generare un messaggio di avviso quando viene eseguito su set di dati più grandi. Quando il numero di righe per il numero di colonne da creare supera un valore impostato (il valore predefinito è 3 milioni), rxDataStep restituisce un avviso e il numero di righe nel frame di dati restituito verrà troncato. Per rimuovere l'avviso, è possibile modificare l'argomento _maxRowsByCols_ nella funzione rxDataStep. Tuttavia, se _maxRowsByCols_ è troppo grande, potrebbe verificarsi un problema durante il caricamento del frame di dati in memoria.

7. Facoltativamente, è possibile chiamare [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) per esaminare lo schema dell'origine dati trasformata.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Definizione delle funzionalità con Transact-SQL

In questo esercizio si apprenderà come eseguire la stessa attività usando le funzioni SQL anziché le funzioni R personalizzate. 

Passare a [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) o a un altro editor di query per eseguire lo script T-SQL.

1. Usare una funzione SQL denominata *fnCalculateDistance*. La funzione deve essere già presente nel database NYCTaxi_Sample. In Esplora oggetti verificare che la funzione esista esplorando questo percorso: I database > NYCTaxi_Sample > Programmabilità > funzioni > funzioni a valori scalari > dbo. fnCalculateDistance.

    Se la funzione non esiste, utilizzare SQL Server Management Studio per generare la funzione nel database NYCTaxi_Sample.

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

2. In Management Studio, in una nuova finestra di query, eseguire l' [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione seguente da qualsiasi applicazione che [!INCLUDE[tsql](../../includes/tsql-md.md)] supporta per verificare il funzionamento della funzione.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. Per inserire i valori direttamente in una nuova tabella (prima di tutto è necessario crearla), è possibile aggiungere una clausola **into** che specifichi il nome della tabella.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. È anche possibile chiamare la funzione SQL dal codice R. Tornare a Rgui e archiviare la query SQL conteggi in una variabile R.

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > Questa query è stata modificata per ottenere un campione di dati più piccolo, in modo da rendere più veloce questa procedura dettagliata. Se si desidera ottenere tutti i dati, è possibile rimuovere la clausola TABLESAMPLE. Tuttavia, a seconda dell'ambiente, potrebbe non essere possibile caricare il insieme alle completo in R, causando un errore.
  
5. Usare le righe di codice seguenti per chiamare la funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] dall'ambiente R e applicarla ai dati definiti in *featureEngineeringQuery*.
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  Ora che la nuova funzionalità è stata creata, chiamare **rxGetVarsInfo** per creare un riepilogo dei dati nella tabella delle funzionalità.
  
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
    > In alcuni casi, è possibile che si ottenga un errore simile al seguente: *Autorizzazione EXECUTE negata per l'oggetto ' fnCalculateDistance '* In tal caso, verificare che l'account di accesso in uso disponga delle autorizzazioni per eseguire gli script e creare oggetti nel database, non solo nell'istanza di.
    > Controllare lo schema per l'oggetto fnCalculateDistance. Se l'oggetto è stato creato dal proprietario del database e l'account di accesso appartiene al ruolo db_datareader, è necessario concedere all'account di accesso le autorizzazioni esplicite per eseguire lo script.

## <a name="comparing-r-functions-and-sql-functions"></a>Confronto tra funzioni R e funzioni SQL

Si ricordi questo frammento di codice usato per il codice R?

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

È possibile provare a usarlo con l'esempio di funzione SQL personalizzato per verificare il tempo necessario per la trasformazione dei dati quando si chiama una funzione SQL. Provare anche a cambiare i contesti di calcolo con rxSetComputeContext e confrontare le tempistiche.

I tempi potrebbero variare in modo significativo, a seconda della velocità della rete e della configurazione hardware. Nelle configurazioni testate, l'approccio [!INCLUDE[tsql](../../includes/tsql-md.md)] della funzione era più veloce rispetto all'uso di una funzione R personalizzata. Quindi, la [!INCLUDE[tsql](../../includes/tsql-md.md)] funzione per questi calcoli è stata usata nei passaggi successivi.

> [!TIP]
> Molto spesso, la progettazione delle [!INCLUDE[tsql](../../includes/tsql-md.md)] funzionalità con sarà più veloce di R. Ad esempio, T-SQL include le funzioni rapide di finestra e di rango che è possibile applicare ai calcoli di data science comuni, come le medie mobili in sequenza e *n*-riquadri. Scegliere il metodo più efficace in base ai dati e all'attività eseguita.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Compila un modello R e Salva in SQL](walkthrough-build-and-save-the-model.md)

