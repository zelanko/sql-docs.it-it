---
title: Visualizzare e riepilogare i dati SQL Server usando le funzioni R
description: Esercitazione che illustra come visualizzare e generare riepiloghi statistici usando le funzioni R per l'analisi nel database in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 47850bebcc20fdd357b2336a9597da067cd479ca
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715367"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>Visualizzare e riepilogare i dati SQL Server usando R (procedura dettagliata)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa lezione vengono illustrate le funzioni nel pacchetto **RevoScaleR** e vengono illustrate le attività seguenti:

> [!div class="checklist"]
> * Connessione a SQL Server
> * Definire una query che contiene i dati necessari oppure specificare una tabella o una vista
> * Definire uno o più contesti di calcolo da usare durante l'esecuzione del codice R
> * Facoltativamente, definire le trasformazioni applicate all'origine dati durante la lettura dall'origine

## <a name="define-a-sql-server-compute-context"></a>Definire un contesto di calcolo SQL Server

Eseguire le istruzioni R seguenti in un ambiente R nella workstation client. Questa sezione presuppone la [Data Science workstation con Microsoft R client](../r/set-up-a-data-science-client.md), perché include tutti i pacchetti RevoScaleR, oltre a un set semplice e leggero di strumenti R. Ad esempio, è possibile usare Rgui. exe per eseguire lo script R in questa sezione.

1. Se il pacchetto **RevoScaleR** non è già caricato, eseguire questa riga di codice R:

    ```R
    library("RevoScaleR")
    ```

     Le virgolette sono facoltative, in questo caso, anche se consigliate.
     
     Se viene ricevuto un errore, assicurarsi che l'ambiente di sviluppo R usi una raccolta che includa il pacchetto RevoScaleR. Usare un comando come `.libPaths()` per visualizzare il percorso della libreria corrente.

2. Creare la stringa di connessione per SQL Server e salvarla in una variabile R, *ConnStr dello script*.

   È necessario modificare il segnaposto "Your_Server_Name" in un nome di istanza di SQL Server valido. Per il nome del server, è possibile utilizzare solo il nome dell'istanza o potrebbe essere necessario specificare il nome completo, a seconda della rete.
    
   Per SQL Server autenticazione, la sintassi di connessione è la seguente:

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    Per l'autenticazione di Windows, la sintassi è leggermente diversa:
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    In genere, è consigliabile usare l'autenticazione di Windows, laddove possibile, per evitare di salvare le password nel codice R.

3. Definire le variabili da usare per la creazione di un nuovo *contesto di calcolo*. Dopo aver creato l'oggetto contesto di calcolo, è possibile usarlo per eseguire il codice R sull'istanza di SQL Server.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - R usa una directory temporanea per la serializzazione degli oggetti R tra la workstation e il computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . È possibile specificare la directory locale che viene usata come *sqlShareDir*o accettare quella predefinita.
  
    - Usare *sqlwait* per indicare se si vuole che R attenda i risultati del server.  Per informazioni sull'attesa rispetto ai processi non in attesa, vedere [Distributed and Parallel Computing with RevoScaleR in Microsoft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing).
  
    - Usare l'argomento *sqlConsoleOutput* per indicare che non si vuole visualizzare l'output dalla console di R.

4. Chiamare il costruttore [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) per creare l'oggetto contesto di calcolo con le variabili e le stringhe di connessione già definite e salvare il nuovo oggetto nella variabile R *SQLCC*.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. Per impostazione predefinita, il contesto di calcolo è locale, pertanto è necessario impostare in modo esplicito il contesto di calcolo *attivo* .

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) restituisce il contesto di calcolo precedentemente attivo in modo invisibile per poterlo usare
    + [rxGetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) restituisce il contesto di calcolo attivo
    
    Si noti che l'impostazione di un contesto di calcolo influiscono solo sulle operazioni che usano funzioni nel pacchetto **RevoScaleR** . il contesto di calcolo non influisce sul modo in cui vengono eseguite le operazioni R Open Source.

## <a name="create-a-data-source-using-rxsqlserver"></a>Creare un'origine dati usando RxSqlServer

Quando si usano le librerie di Microsoft R come RevoScaleR e MicrosoftML, un' *origine dati* è un oggetto creato con funzioni RevoScaleR. L'oggetto origine dati specifica un set di dati che si desidera utilizzare per un'attività, ad esempio il training del modello o l'estrazione della funzionalità. È possibile ottenere dati da un'ampia gamma di origini, tra cui SQL Server. Per l'elenco delle origini attualmente supportate, vedere [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource).

In precedenza è stata definita una stringa di connessione e le informazioni sono state salvate in una variabile R. È possibile riutilizzare tali informazioni di connessione per specificare i dati che si desidera ottenere.

1. Salvare una query SQL come variabile di stringa. La query definisce i dati per il training del modello.

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    È stata usata una clausola TOP per eseguire più velocemente le operazioni, ma le righe effettive restituite dalla query possono variare a seconda dell'ordine. I risultati di riepilogo potrebbero quindi essere diversi da quelli elencati di seguito. È possibile rimuovere la clausola TOP.

2. Passare la definizione di query come argomento alla funzione [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata).

    ```R
    inDataSource <- RxSqlServerData(
      sqlQuery = sampleDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )
    ```
    
    + L'argomento  *colClasses* specifica i tipi di colonna da usare durante lo spostamento dei dati tra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e R. Questo aspetto è importante perché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tipi di dati diversi rispetto a R e più tipi di dati. Per altre informazioni, vedere [librerie R e tipi di dati](../r/r-libraries-and-data-types.md).
  
    + L'argomento *rowsPerRead* è importante per la gestione dell'utilizzo della memoria e dei calcoli efficienti.  La maggior parte delle funzioni analitiche avanzate in[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] elabora i dati in blocchi e raggruppa risultati intermedi, restituendo i calcoli finali dopo che tutti i dati sono stati letti.  Aggiungendo il parametro *rowsPerRead* , è possibile controllare il numero di righe di dati lette in ogni blocco per l'elaborazione.  Se il valore di questo parametro è troppo grande, l'accesso ai dati potrebbe essere lento perché la memoria non è sufficiente per elaborare in modo efficiente un blocco di dati di questo tipo.  In alcuni sistemi, l'impostazione di *rowsPerRead* su un valore eccessivamente ridotto può anche offrire prestazioni più lente.

3. A questo punto, l'oggetto indatasource è stato creato, ma non contiene dati. I dati non vengono estratti dalla query SQL nell'ambiente locale fino a quando non si esegue una funzione, ad esempio [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) o [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary).

    Tuttavia, ora che sono stati definiti gli oggetti dati, è possibile usarli come argomento per altre funzioni.

## <a name="use-the-sql-server-data-in-r-summaries"></a>Usare i dati SQL Server nei riepiloghi R

In questa sezione verranno illustrate alcune delle funzioni disponibili in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] che supportano i contesti di calcolo remoti. Applicando le funzioni R all'origine dati, è possibile esplorare, riepilogare e tracciare i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati.

1. Chiamare la funzione [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) per ottenere un elenco delle variabili nell'origine dati e i relativi tipi di dati.

    **rxGetVarInfo** è una funzione utile; è possibile chiamarla in qualsiasi frame di dati o in un set di dati in un oggetto dati remoto, per ottenere informazioni quali i valori minimo e massimo, il tipo di dati e il numero di livelli nelle colonne fattore.
    
    È consigliabile eseguire questa funzione dopo qualsiasi tipo di input dei dati, dopo la trasformazione o la progettazione di una funzionalità. In questo modo, è possibile assicurarsi che tutte le funzionalità che si desidera utilizzare nel modello siano del tipo di dati previsto ed evitare errori.
  
    ```R
    rxGetVarInfo(data = inDataSource)
    ```

    **Risultati**
    
    ```R
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: integer
    Var 4: trip_time_in_secs, Type: numeric, Storage: int64
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: pickup_longitude, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: dropoff_longitude, Type: numeric
    ```

2. A questo punto, chiamare la funzione RevoScaleR [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) per ottenere statistiche più dettagliate sulle singole variabili.

    rxSummary è basato sulla funzione R `summary` , ma presenta alcune funzionalità e vantaggi aggiuntivi. rxSummary funziona in più contesti di calcolo e supporta la suddivisione in blocchi.  È anche possibile usare rxSummary per trasformare i valori o riepilogare in base ai livelli di fattore.
    
    In questo esempio viene riepilogata l'importo della tariffa in base al numero di passeggeri.
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + Il primo argomento di rxSummary specifica la formula o il termine in base al quale riepilogare. In questo caso `F()` , la funzione viene usata per convertire i valori in _conteggio passeggeri\__ in fattori prima del riepilogo. È inoltre necessario specificare il valore minimo (1) e il valore massimo (6) per la variabile del fattore di _conteggio dei passeggeri\__ .
    + Se non si specificano le statistiche per l'output, per impostazione predefinita rxSummary restituisce Mean, StDev, min, Max e il numero di osservazioni valide e mancanti.
    + Questo esempio include anche una parte di codice per tenere traccia dell'ora in cui la funzione ha inizio e termina in modo da poter confrontare le prestazioni.
  
    **Risultati**

    Se la funzione rxSummary viene eseguita correttamente, verranno visualizzati risultati simili ai seguenti, seguiti da un elenco di statistiche per categoria. 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>Esercizio bonus per Big Data

Provare a definire una nuova stringa di query con tutte le righe. È consigliabile configurare un nuovo oggetto origine dati per questo esperimento. È anche possibile provare a modificare il parametro *rowsToRead* per vedere come influisca sulla velocità effettiva.

```R
bigDataQuery  <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"

bigDataSource <- RxSqlServerData(
      sqlQuery = bigDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )

start.time <- proc.time()
rxSummary(~fare_amount:F(passenger_count,1,6), data = bigDataSource)
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
  Elapsed Time=", round(used.time[3],2),
  " seconds to summarize the inDataSource.", sep=""))
```

> [!TIP]
> Mentre è in esecuzione, è possibile usare uno strumento come [Esplora processi](https://technet.microsoft.com/sysinternals/processexplorer.aspx) o SQL Profiler per vedere come viene eseguita la connessione e il codice R viene eseguito usando SQL Server Services.
> 
> Un'altra opzione consiste nel monitorare i processi R in esecuzione in SQL Server usando questi [report personalizzati](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Creare grafici e tracciati con R](walkthrough-create-graphs-and-plots-using-r.md)