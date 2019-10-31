---
title: Distribuire un modello R per le stime in SQL Server
description: Esercitazione che illustra come distribuire un modello R su SQL Server per l'analisi nel database.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: aba6990fbed5b24d63d4ab5c16e192718aeff305
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714684"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>Distribuire il modello R e usarlo in SQL Server (procedura dettagliata)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa lezione si apprenderà come distribuire modelli R in un ambiente di produzione chiamando un modello sottoposto a training da un stored procedure. È possibile richiamare il stored procedure da R o qualsiasi linguaggio di programmazione dell'applicazione [!INCLUDE[tsql](../../includes/tsql-md.md)] che supporti ( C#ad esempio, Java, Python e così via) e usare il modello per eseguire stime sulle nuove osservazioni.

Questo articolo illustra i due modi più comuni per usare un modello per l'assegnazione dei punteggi:

> [!div class="checklist"]
> * La modalità di assegnazione dei **punteggi batch** genera più stime
> * La modalità di assegnazione dei **punteggi singoli** genera stime una alla volta

## <a name="batch-scoring"></a>Punteggio batch

Creare una stored procedure, *PredictTipBatchMode*, che genera più stime, passando una query o una tabella SQL come input. Viene restituita una tabella di risultati, che è possibile inserire direttamente in una tabella o scrivere in un file.

- Ottiene un set di dati di input come query SQL
- Chiama il modello di regressione logistica di cui è stato eseguito il training e che è stato salvato nella lezione precedente
- Consente di stimare la probabilità che il driver ottenga qualsiasi suggerimento diverso da zero

1. In Management Studio aprire una nuova finestra di query ed eseguire lo script T-SQL seguente per creare il stored procedure PredictTipBatchMode.
  
    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipBatchMode')
    DROP PROCEDURE v
    GO

    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @input nvarchar(max)
    AS
    BEGIN
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  FROM nyc_taxi_models);
      EXEC sp_execute_external_script @language = N'R',
         @script = N'
           mod <- unserialize(as.raw(model));
           print(summary(mod))
           OutputDataSet<-rxPredict(modelObject = mod,
             data = InputDataSet,
             outData = NULL,
             predVarNames = "Score", type = "response",
             writeModelVars = FALSE, overwrite = TRUE);
           str(OutputDataSet)
           print(OutputDataSet)',
      @input_data_1 = @input,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

    + Utilizzare un'istruzione SELECT per chiamare il modello archiviato da una tabella SQL. Il modello viene recuperato dalla tabella come dati **varbinary (max)** , archiviato nella variabile  _\@SQL lmodel2_e passato come parametro *mod* al sistema stored procedure [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + I dati usati come input per il punteggio vengono definiti come query SQL e archiviati come stringa nell'  _\@input_della variabile SQL. Poiché i dati vengono recuperati dal database, vengono archiviati in un frame di dati denominato *InputDataSet*, che è solo il nome predefinito per i dati di input nella procedura [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) . Se necessario, è possibile definire un altro nome di variabile utilizzando il parametro *_\@input_data_1_name_* .

    + Per generare i punteggi, il stored procedure chiama la funzione rxPredict dalla libreria **RevoScaleR** .

    + Il valore restituito *Score*è la probabilità, dato il modello, che il driver ottiene un suggerimento. Facoltativamente, è possibile applicare facilmente un filtro ai valori restituiti per categorizzare i valori restituiti nei gruppi "Tip" e "No Tip".  Una probabilità inferiore a 0,5, ad esempio, potrebbe significare che è improbabile una mancia.
  
2.  Per chiamare il stored procedure in modalità batch, è necessario definire la query necessaria come input per l'stored procedure. Di seguito è riportata la query SQL, che è possibile eseguire in SSMS per verificarne il funzionamento.

    ```sql
    SELECT TOP 10
      a.passenger_count AS passenger_count,
      a.trip_time_in_secs AS trip_time_in_secs,
      a.trip_distance AS trip_distance,
      a.dropoff_datetime AS dropoff_datetime,
      dbo.fnCalculateDistance( pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance
      FROM 
        (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude 
        FROM nyctaxi_sample)a 
      LEFT OUTER JOIN
      ( SELECT medallion, hack_license, pickup_datetime
      FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b
      ON a.medallion=b.medallion
      AND a.hack_license=b.hack_license
      AND a.pickup_datetime=b.pickup_datetime
      WHERE b.medallion is null
    ```

3. Usare questo codice R per creare la stringa di input dalla query SQL:

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @input = ", input, sep="");
    ```

4. Per eseguire il stored procedure da R, chiamare il metodo sqlQuery del pacchetto **RODBC** e usare la connessione `conn` SQL definita in precedenza:

    ```R
    sqlQuery (conn, q);
    ```

    Se viene ricevuto un errore ODBC, verificare la presenza di errori di sintassi e indicare se è presente il numero corretto di virgolette. 
    
    Se si verifica un errore di autorizzazione, verificare che l'account di accesso sia in grado di eseguire il stored procedure.

## <a name="single-row-scoring"></a>Assegnazione di punteggi a riga singola

La modalità di assegnazione dei punteggi singoli genera stime una alla volta, passando un set di singoli valori al stored procedure come input. I valori corrispondono alle funzionalità del modello, utilizzate dal modello per creare una stima, o generano un altro risultato, ad esempio un valore di probabilità. È quindi possibile restituire tale valore all'applicazione o all'utente.

Quando si chiama il modello per la stima in base alla riga, si passa un set di valori che rappresentano le funzionalità per ogni singolo case. Il stored procedure restituisce quindi una singola stima o probabilità. 

Il stored procedure *PredictTipSingleMode* illustra questo approccio. Accetta come input più parametri che rappresentano i valori delle funzionalità, ad esempio il numero di passeggeri e la distanza della corsa, punteggiano queste funzionalità usando il modello R archiviato e restituisce la probabilità del suggerimento.

1. Eseguire l'istruzione Transact-SQL seguente per creare la stored procedure.

    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipSingleMode')
    DROP PROCEDURE v
    GO

    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0,
    @trip_distance float = 0,
    @trip_time_in_secs int = 0,
    @pickup_latitude float = 0,
    @pickup_longitude float = 0,
    @dropoff_latitude float = 0,
    @dropoff_longitude float = 0
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs, @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)'
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);

      EXEC sp_execute_external_script @language = N'R',  @script = N'
            mod <- unserialize(as.raw(model));
            print(summary(mod))
            OutputDataSet<-rxPredict(
              modelObject = mod,
              data = InputDataSet,
              outData = NULL,
              predVarNames = "Score",
              type = "response",
              writeModelVars = FALSE,
              overwrite = TRUE);
            str(OutputDataSet)
            print(OutputDataSet)
            ',
      @input_data_1 = @inquery,
      @params = N'
      -- passthrough columns
      @model varbinary(max) ,
      @passenger_count int ,
      @trip_distance float ,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      -- mapped variables
      @model = @lmodel2 ,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance ,
      @trip_time_in_secs=@trip_time_in_secs ,
      @pickup_latitude=@pickup_latitude ,
      @pickup_longitude=@pickup_longitude ,
      @dropoff_latitude=@dropoff_latitude ,
      @dropoff_longitude=@dropoff_longitude
      WITH RESULT SETS ((Score float));
    END
    ```

2. In SQL Server Management Studio, è possibile utilizzare la [!INCLUDE[tsql](../../includes/tsql-md.md)] procedura **Exec** (o **Execute**) per chiamare il stored procedure e passargli gli input necessari. Provare ad esempio a eseguire questa istruzione in Management Studio:

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    I valori passati qui sono, rispettivamente, per le variabili _numero passeggeri\__ , _trip_distance_, _tempo\_\_di viaggio in\_secondi_, _latitudine\_di ritiro_, _Longitudine\__ di prelievo, _Latitudine abbandono\__ e _Longitudine abbandono\__ .

3. Per eseguire la stessa chiamata dal codice R, è sufficiente definire una variabile R contenente l'intera chiamata di stored procedure, come questa:

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    I valori passati qui sono, rispettivamente, per le variabili _numero passeggeri\__ , _distanza corsa\__ , _tempo\_\_di viaggio in\_secondi_, _pickup\_ Latitudine_, _\_prelievo Longitudine_, _latitudine\_abbandono_e _Longitudine\_abbandono_.

4. Chiamare `sqlQuery` (dal pacchetto **RODBC** ) e passare la stringa di connessione, insieme alla variabile di stringa contenente la chiamata stored procedure.

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > R Tools per Visual Studio (RTVS) offre una grande integrazione con SQL Server e R. Per altri esempi sull'uso di RODBC con una connessione SQL Server, vedere questo articolo: [Uso di SQL Server e R](https://docs.microsoft.com/visualstudio/rtvs/sql-server)

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i dati e salvare in modo permanente i modelli R sottoposti a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]training, dovrebbe essere relativamente semplice creare nuovi modelli basati su questo set di dati. Ad esempio, è possibile provare a creare questi modelli aggiuntivi:

+ Un modello di regressione che stima l'importo della mancia
+ Un modello di classificazione multiclasse che stima se il suggerimento è grande, medio o piccolo

Potrebbe inoltre essere necessario esplorare questi esempi e risorse aggiuntivi:

+ [Scenari di analisi scientifica dei dati e modelli di soluzioni](data-science-scenarios-and-solution-templates.md)
+ [Analisi avanzata nel database](sqldev-in-database-r-for-sql-developers.md)
+ [Guide alle procedure Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)
+ [Machine Learning Server risorse aggiuntive](https://docs.microsoft.com//machine-learning-server/resources-more)
