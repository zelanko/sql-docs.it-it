---
title: Compilare un modello R e salvarlo in SQL Server (procedura dettagliata)
description: Esercitazione che illustra come creare un modello di linguaggio R usato per SQL Server analisi nel database.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: af2b1bf8f619800737863ff955011b011f4819d0
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715395"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>Compilare un modello R e salvarlo in SQL Server (procedura dettagliata)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questo passaggio si apprenderà come creare un modello di machine learning e salvare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]modello in. Salvando un modello, è possibile chiamarlo direttamente dal [!INCLUDE[tsql](../../includes/tsql-md.md)] codice, usando il stored procedure di sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) o la [funzione Predict (T-SQL)](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql).

## <a name="prerequisites"></a>Prerequisiti

Questo passaggio presuppone una sessione R in corso in base ai passaggi precedenti di questa procedura dettagliata. Usa le stringhe di connessione e gli oggetti origine dati creati in questi passaggi. Per eseguire lo script vengono usati gli strumenti e i pacchetti seguenti.

+ Rgui. exe per l'esecuzione di comandi R
+ Management Studio per eseguire T-SQL
+ Pacchetto ROCR
+ Pacchetto RODBC

### <a name="create-a-stored-procedure-to-save-models"></a>Creare una stored procedure per salvare i modelli

Questo passaggio usa un stored procedure per salvare un modello sottoposto a training in modo da SQL Server. La creazione di un stored procedure per eseguire questa operazione rende più semplice l'attività.

Eseguire il codice T-SQL seguente in una finestra di query in Management Studio per creare il stored procedure.

```sql
USE [NYCTaxi_Sample]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PersistModel')
  DROP PROCEDURE PersistModel
GO

CREATE PROCEDURE [dbo].[PersistModel] @m nvarchar(max)
AS
BEGIN
    -- SET NOCOUNT ON added to prevent extra result sets from
    -- interfering with SELECT statements.
    SET NOCOUNT ON;
    insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
END
GO
```

> [!NOTE]
> Se viene ricevuto un errore, verificare che l'account di accesso disponga dell'autorizzazione per la creazione di oggetti. È possibile concedere autorizzazioni esplicite per la creazione di oggetti eseguendo un'istruzione T-SQL simile `exec sp_addrolemember 'db_owner', '<user_name>'`alla seguente:.

## <a name="create-a-classification-model-using-rxlogit"></a>Creare un modello di classificazione usando rxLogit

Il modello è un classificatore binario che prevede se è probabile che il driver taxi ottenga un suggerimento su una particolare corsa. Si userà l'origine dati creata nella lezione precedente per eseguire il training del classificatore Tip, usando la regressione logistica.

1. Chiamare la funzione [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) inclusa nel pacchetto **RevoScaleR** per creare un modello di regressione logistica. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    La chiamata che crea il modello è racchiusa nella funzione system.time. Ciò consente di ottenere il tempo necessario per compilare il modello.

2. Dopo aver compilato il modello, è possibile esaminarlo usando la `summary` funzione e visualizzare i coefficienti.

    ```R
    summary(logitObj);
    ```

    **Risultati**
    
    ```R
     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*
     direct_distance* 
     *Data: featureDataSource (RxSqlServerData Data Source)*
     *Dependent variable(s): tipped*
     *Total independent variables: 5*
     *Number of valid observations: 17068*
     *Number of missing observations: 0*
     *-2\*LogLikelihood: 23540.0602 (Residual deviance on 17063 degrees of freedom)*
     *Coefficients:*
     *Estimate Std. Error z value Pr(>|z|)*
     *(Intercept)       -2.509e-03  3.223e-02  -0.078  0.93793*
     *passenger_count   -5.753e-02  1.088e-02  -5.289 1.23e-07 \*\*\**
     *trip_distance     -3.896e-02  1.466e-02  -2.658  0.00786 \*\**
     *trip_time_in_secs  2.115e-04  4.336e-05   4.878 1.07e-06 \*\*\**
     *direct_distance    6.156e-02  2.076e-02   2.966  0.00302 \*\**
     *---*
     *Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*
     *Condition number of final variance-covariance matrix: 48.3933*
     *Number of iterations: 4*
   ```

## <a name="use-the-logistic-regression-model-for-scoring"></a>Usare il modello di regressione logistica per assegnare i punteggi

Dopo aver compilato il modello, è possibile usarlo per prevedere se il tassista riceverà una mancia in una specifica corsa.

1. Utilizzare innanzitutto la funzione [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) per definire un oggetto origine dei dati per l'archiviazione del risultato del punteggio.

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + Per semplificare questo esempio, l'input per il modello di regressione logistica è la stessa origine dati della funzionalità (`sql_feature_ds`) utilizzata per eseguire il training del modello.  Più generalmente è possibile usare nuovi dati per i punteggi oppure riservare alcuni dati per il test e non per il training.
  
    + I risultati della stima verranno salvati nella tabella _taxiscoreOutput_. Si noti che lo schema per questa tabella non è definito quando lo si crea con rxSqlServerData. Lo schema viene ottenuto dall'output rxPredict.
  
    + Per creare la tabella in cui sono archiviati i valori stimati, è necessario che l'account di accesso SQL che esegue la funzione dati rxSqlServer disponga dei privilegi DDL nel database. Se l'account di accesso non può creare tabelle, l'istruzione ha esito negativo.

2. Chiamare la funzione [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) per generare i risultati.

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    Se l'istruzione ha esito positivo, l'esecuzione potrebbe richiedere del tempo. Al termine, è possibile aprire SQL Server Management Studio e verificare che la tabella sia stata creata e che contenga la colonna score e altro output previsto.

## <a name="plot-model-accuracy"></a>Accuratezza del modello di traccia

Per avere un'idea dell'accuratezza del modello, è possibile usare la funzione [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) per tracciare la curva operativa del ricevitore. Poiché rxRoc è una delle nuove funzioni offerte dal pacchetto RevoScaleR che supporta i contesti di calcolo remoti, sono disponibili due opzioni:

+ È possibile usare la funzione rxRoc per eseguire il tracciato nel contesto di calcolo remoto e quindi restituire il tracciato al client locale.

+ È inoltre possibile importare i dati nel computer client R e usare altre funzioni di tracciato R per creare il grafico delle prestazioni.

In questa sezione verranno sperimentate entrambe le tecniche.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Eseguire un tracciato nel contesto di calcolo remoto (SQL Server)

1. Chiamare la funzione rxRoc e fornire i dati definiti in precedenza come input.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    Questa chiamata restituisce i valori utilizzati per il calcolo del grafico ROC. La colonna dell'etichettaè tipped, con i risultati effettivi che si sta tentando di stimare, mentre nella colonna _Score_ è presente la stima.

2. Per tracciare effettivamente il grafico, è possibile salvare l'oggetto ROC, quindi disegnarlo con la funzione Plot. Il grafo viene creato nel contesto di calcolo remoto e restituito all'ambiente R.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    Visualizzare il grafico aprendo il dispositivo di grafica R oppure facendo clic sulla finestra **tracciato** in rstudio.

    ![tracciato ROC per il modello](media/rsql-e2e-rocplot.png "tracciato ROC per il modello")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Creare i tracciati nel contesto di calcolo locale usando i dati di SQL Server

È possibile verificare che il contesto di `rxGetComputeContext()` calcolo sia locale eseguendo al prompt dei comandi. Il valore restituito deve essere "contesto di calcolo RxLocalSeq".

1. Per il contesto di calcolo locale, il processo è molto simile. Usare la funzione [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) per portare i dati specificati nell'ambiente R locale.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. Utilizzando i dati nella memoria locale, è possibile caricare il pacchetto **ROCR** e utilizzare la funzione di stima del pacchetto per creare nuove stime.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. Genera un tracciato locale, in base ai valori archiviati nella variabile `pred`di output.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![tracciare le prestazioni del modello con R](media/rsql-e2e-performanceplot.png "tracciare le prestazioni del modello con R")

> [!NOTE]
> I grafici potrebbero avere un aspetto diverso da questi, a seconda del numero di punti dati usati.

## <a name="deploy-the-model"></a>Distribuire il modello

Dopo aver compilato un modello e aver verificato che funzioni correttamente, è probabile che si voglia distribuirlo in un sito in cui gli utenti o gli utenti dell'organizzazione possano usare il modello o eventualmente ripetere il training e ricalibrare il modello a intervalli regolari. Questo processo viene talvolta denominato *operatività* un modello. In SQL Server la messa in funzione viene eseguita incorporando il codice R in una stored procedure. Poiché il codice risiede nella procedura, può essere chiamato da qualsiasi applicazione in grado di connettersi a SQL Server.

Prima di poter chiamare il modello da un'applicazione esterna, è necessario salvare il modello nel database utilizzato per la produzione. I modelli sottoposti a training vengono archiviati in formato binario, in una singola colonna di tipo **varbinary (max)** .

Un flusso di lavoro di distribuzione tipico prevede i passaggi seguenti:

1. Serializzare il modello in una stringa esadecimale
2. Trasmettere l'oggetto serializzato al database
3. Salvare il modello in una colonna varbinary (max)

In questa sezione viene illustrato come utilizzare un stored procedure per salvare in modo permanente il modello e renderlo disponibile per le stime. Il stored procedure usato in questa sezione è PersistModel. La definizione di PersistModel è conforme ai [prerequisiti](#prerequisites).

1. Tornare all'ambiente R locale se non è già in uso, serializzare il modello e salvarlo in una variabile.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. Aprire una connessione ODBC utilizzando **RODBC**. Se il pacchetto è già stato caricato, è possibile omettere la chiamata a RODBC.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. Chiamare il stored procedure PersistModel su SQL Server per trasmettere l'oggetto serializzato al database e archiviare la rappresentazione binaria del modello in una colonna. 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. Utilizzare Management Studio per verificare che il modello esista. In Esplora oggetti fare clic con il pulsante destro del mouse sulla tabella **nyc_taxi_models** e scegliere **seleziona le prime 1000 righe**. Nei risultati dovrebbe essere visualizzata una rappresentazione binaria nella colonna **Models** .

Il salvataggio di un modello in una tabella richiede solo un'istruzione INSERT. Tuttavia, è spesso più semplice quando viene eseguito il wrapper in un stored procedure, ad esempio *PersistModel*.

## <a name="next-steps"></a>Passaggi successivi

Nella lezione successiva e finale, informazioni su come eseguire il punteggio rispetto al modello salvato usando [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!div class="nextstepaction"]
> [Distribuire il modello R e usarlo in SQL](walkthrough-deploy-and-use-the-model.md)
