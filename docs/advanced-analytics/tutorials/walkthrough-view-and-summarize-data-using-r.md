---
title: Visualizzare e riepilogare i dati di SQL Server usando funzioni R - SQL Server Machine Learning
description: Esercitazione che illustra come visualizzare e generare riepiloghi statistici usando funzioni R per analitica nel database in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 613053b05d675963ceef89a71de4e8ac73352fad
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510908"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>Visualizzare e riepilogare i dati di SQL Server tramite R (procedura dettagliata)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questa lezione viene presentato a funzioni nel **RevoScaleR** pacchetti e la procedura per le attività seguenti:

> [!div class="checklist"]
> * Connessione a SQL Server
> * Definire una query che contiene i dati necessari oppure specificare una tabella o una vista
> * Definire uno o più contesti di calcolo da usare durante l'esecuzione del codice R
> * Facoltativamente, definire le trasformazioni applicate all'origine dei dati durante la lettura dall'origine

## <a name="define-a-sql-server-compute-context"></a>Definire un contesto di calcolo di SQL Server

Eseguire le seguenti istruzioni di R in un ambiente R nella workstation client. Questa sezione si presuppone una [workstation di analisi scientifica dei dati con Microsoft R Client](../r/set-up-a-data-science-client.md), perché include tutti i pacchetti RevoScaleR, nonché un set di base e leggero di R tools. Ad esempio, è possibile utilizzare Rgui.exe per eseguire lo script R in questa sezione.

1. Se il **RevoScaleR** pacchetto non è già caricato, eseguire la seguente riga di codice R:

    ```R
    library("RevoScaleR")
    ```

     Le virgolette sono facoltative, in questo caso, anche se consigliato.
     
     Se si verifica un errore, assicurarsi che l'ambiente di sviluppo R usi una raccolta che include il pacchetto RevoScaleR. Usare un comando, ad esempio `.libPaths()` per visualizzare il percorso di libreria corrente.

2. Creare la stringa di connessione per SQL Server e salvarlo in una variabile R *connStr*.

   È necessario modificare il segnaposto "nome_server" in un nome di istanza di SQL Server valido. Per il nome del server, è possibile usare solo il nome dell'istanza, o potrebbe essere necessario qualificare completamente il nome, a seconda della rete.
    
   Per l'autenticazione di SQL Server, la sintassi della connessione è come segue:

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    Per l'autenticazione di Windows, la sintassi è leggermente diversa:
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    In generale, è consigliabile utilizzare l'autenticazione di Windows dove possibile, per evitare di salvare le password nel codice R.

3. Definire le variabili da utilizzare per creare una nuova *contesto di calcolo*. Dopo aver creato l'oggetto di contesto di calcolo, è possibile usarlo per eseguire codice R nell'istanza di SQL Server.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - R usa una directory temporanea per la serializzazione degli oggetti R tra la workstation e il computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . È possibile specificare la directory locale che viene usata come *sqlShareDir*o accettare quella predefinita.
  
    - Uso *sqlWait* per indicare se si vuole attendere i risultati dal server di R.  Per una discussione di attesa e non in attesa dei processi, vedere [applicazione distribuita e l'elaborazione parallela con RevoScaleR in R Microsoft](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing).
  
    - Usare l'argomento *sqlConsoleOutput* per indicare che non si vuole visualizzare l'output della console di R.

4. Si chiama il [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) costruttore per creare l'oggetto di contesto di calcolo con le variabili e stringhe di connessione già definite e salvare il nuovo oggetto nella variabile R *sqlcc*.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. Per impostazione predefinita, il contesto di calcolo è locale, pertanto è necessario impostare in modo esplicito il *active* contesto di calcolo.

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) restituisce il contesto di calcolo precedentemente attivo in modo invisibile in modo che sia possibile usarlo
    + [rxGetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) restituisce il contesto di calcolo attivo
    
    Si noti che l'impostazione di un contesto di calcolo influisce solo sulle operazioni che usano funzioni dei **RevoScaleR** pacchetto; le risorse di calcolo contesto non interessano il modo in cui vengono eseguite operazioni R open source.

## <a name="create-a-data-source-using-rxsqlserver"></a>Creare un'origine dati tramite RxSqlServer

Quando si usano le librerie di Microsoft R come RevoScaleR e MicrosoftML, un *zdroj dat* è un oggetto è creare usando funzioni RevoScaleR. L'oggetto origine dati specifica i set di dati che si desidera utilizzare per un'attività, ad esempio estrazione di training o la funzionalità del modello. È possibile ottenere dati da diverse origini, tra cui SQL Server. Per l'elenco delle origini attualmente supportate, vedere [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource).

In precedenza è definita una stringa di connessione e salvare le informazioni in una variabile R. È possibile riutilizzare tali informazioni di connessione per specificare i dati si desidera ottenere.

1. Salvare una query SQL come una variabile di stringa. La query definisce i dati di training del modello.

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    Abbiamo utilizzato qui una clausola TOP per semplificare l'esecuzione più rapida, ma le righe effettive restituite dalla query possono variare a seconda dell'ordine. Di conseguenza, i risultati di riepiloghi anche potrebbero essere diversi da quelli elencati di seguito. È possibile rimuovere la clausola TOP.

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
    
    + L'argomento  *colClasses* specifica i tipi di colonna da usare durante lo spostamento dei dati tra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e R. Questo aspetto è importante perché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tipi di dati diversi rispetto a R e più tipi di dati. Per altre informazioni, vedere [librerie di R e tipi di dati](../r/r-libraries-and-data-types.md).
  
    + L'argomento *rowsPerRead* è importante per la gestione dell'utilizzo della memoria e per calcoli ottimizzati.  La maggior parte delle funzioni analitiche avanzate in[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] elabora i dati in blocchi e raggruppa risultati intermedi, restituendo i calcoli finali dopo che tutti i dati sono stati letti.  Aggiungendo il *rowsPerRead* parametro, è possibile controllare il numero di righe di dati viene lette in ogni blocco da elaborare.  Se il valore di questo parametro è troppo grande, l'accesso ai dati potrebbe essere lento perché non si dispone di memoria sufficiente per elaborare in modo efficiente una grande quantità di dati.  In alcuni sistemi, l'impostazione *rowsPerRead* su un valore eccessivamente basso può assistere rallentamento delle prestazioni.

3. A questo punto, è stato creato il *inDataSource* oggetto, ma non contiene alcun dato. I dati non vengono spostati dalla query SQL nell'ambiente locale finché non si esegue una funzione, ad esempio [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) oppure [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary).

    Tuttavia, ora che sono stati definiti gli oggetti dati, è possibile usarlo come argomento ad altre funzioni.

## <a name="use-the-sql-server-data-in-r-summaries"></a>Usare i dati di SQL Server nei riepiloghi di R

In questa sezione saranno trattate alcune delle funzioni incluse [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] contesti di calcolo remoto tale supporto. Applicando le funzioni R all'origine dati, è possibile esplorare, riepilogare e classificare i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati.

1. Chiamare la funzione [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) per ottenere un elenco delle variabili nell'origine dati e i relativi tipi di dati.

    **rxGetVarInfo** è una funzione utile; è possibile chiamarlo su qualsiasi frame di dati o in un set di dati in un oggetto dati remoto, per ottenere informazioni quali i valori massimo e minimo valori, il tipo di dati e il numero di livelli nelle colonne fattore.
    
    È consigliabile eseguire questa funzione dopo qualsiasi tipo di input dei dati, dopo la trasformazione o la progettazione di una funzionalità. In questo modo, è possibile garantire che tutte le funzionalità da usare nel modello sono i dati previsti digitare ed evitare gli errori.
  
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

    rxSummary si basa su R `summary` funzionare, ma presenta alcuni vantaggi e funzionalità aggiuntive. rxSummary funziona in più contesti di calcolo e supporta la suddivisione in blocchi.  È inoltre possibile utilizzare per trasformare i valori o riepilogare rxSummary basato su livelli di fattore.
    
    In questo esempio è riepilogare l'importo della tariffa in base al numero dei passeggeri.
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + Il primo argomento rxSummary specifica la formula o il termine da riepilogare per. In questo caso, il `F()` funzione viene usata per convertire i valori di _passeggeri\_conteggio_ in fattori prima di riepilogo. È anche necessario specificare il valore minimo (1) e il valore massimo (6) per il _passeggeri\_conteggio_ variabile di fattore.
    + Se non si specifica l'output delle statistiche, per impostazione predefinita rxSummary l'output Mean, StDev, Min, Max e il numero di osservazioni valide e mancanti.
    + Questo esempio include anche una parte di codice per tenere traccia dell'ora in cui la funzione ha inizio e termina in modo da poter confrontare le prestazioni.
  
    **Risultati**

    Se la funzione rxSummary viene eseguito correttamente, verranno visualizzati risultati simili ai seguenti, seguito da un elenco delle statistiche per categoria. 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>Esercizio aggiuntivo sui big data

Provare a definire una nuova stringa di query con tutte le righe. è consigliabile che configurare un nuovo oggetto origine dati per questo esperimento. È anche possibile provare a modificare la *rowsToRead* parametro per visualizzare il relativo impatto sulla velocità effettiva.

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
> Mentre questo è in esecuzione, è possibile usare uno strumento quale [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) o SQL Profiler per vedere come viene stabilita la connessione e il codice R viene eseguito tramite servizi di SQL Server.
> 
> In alternativa è possibile monitorare i processi R in esecuzione in SQL Server utilizzando questi [report personalizzati](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Creare grafici e tracciati con R](walkthrough-create-graphs-and-plots-using-r.md)