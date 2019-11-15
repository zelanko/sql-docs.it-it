---
title: 'Esercitazione su R: Creare e salvare il modello'
description: Esercitazione che illustra come creare un modello in linguaggio R da usare per l'analisi nel database di SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4cb806c0a6286ec8a6608b346d12e666a8e9a09f
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73724525"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>Creare un modello R e salvarlo in SQL Server (procedura dettagliata)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questo passaggio si apprenderà come creare un modello di Machine Learning e salvarlo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Salvando un modello, è possibile chiamarlo direttamente dal codice [!INCLUDE[tsql](../../includes/tsql-md.md)] tramite la stored procedure di sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) o la [funzione PREDICT (T-SQL)](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql).

## <a name="prerequisites"></a>Prerequisites

Questo passaggio presuppone una sessione R in corso basata sui passaggi precedenti di questa procedura dettagliata. Usa le stringhe di connessione e gli oggetti origine dati creati in tali passaggi. Per eseguire lo script vengono usati gli strumenti e i pacchetti seguenti.

+ Rgui.exe per eseguire i comandi R
+ Management Studio per eseguire T-SQL
+ Pacchetto ROCR
+ Pacchetto RODBC

### <a name="create-a-stored-procedure-to-save-models"></a>Creare una stored procedure per salvare i modelli

In questo passaggio viene usata un stored procedure per salvare un modello sottoposto a training in SQL Server. La creazione di un stored procedure per eseguire questa operazione semplifica l'attività.

Eseguire il codice T-SQL seguente in una finestra di query in Management Studio per creare la stored procedure.

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
> Se si riceve un errore, verificare che l'account di accesso disponga dell'autorizzazione per la creazione di oggetti. È possibile concedere autorizzazioni esplicite per la creazione di oggetti eseguendo un'istruzione T-SQL simile alla seguente: `exec sp_addrolemember 'db_owner', '<user_name>'`.

## <a name="create-a-classification-model-using-rxlogit"></a>Creare un modello di classificazione tramite rxLogit

Il modello è un classificatore binario che prevede se un tassista riceverà una mancia in una particolare corsa. Si userà l'origine dati creata nella lezione precedente, per eseguire il training del classificatore delle mance tramite la regressione logistica.

1. Chiamare la funzione [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) inclusa nel pacchetto **RevoScaleR** per creare un modello di regressione logistica. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    La chiamata che crea il modello è racchiusa nella funzione system.time. Ciò consente di ottenere il tempo necessario per compilare il modello.

2. Dopo aver creato il modello, è possibile controllarlo tramite la funzione `summary` e visualizzare i coefficienti.

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

1. Prima di tutto, usare la funzione [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) per definire un oggetto origine dati per archiviare il risultato dell'assegnazione dei punteggi.

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + Per semplificare questo esempio, l'input per il modello di regressione logistica è la stessa origine dei dati delle caratteristiche (`sql_feature_ds`), usata per il training del modello.  Più generalmente è possibile usare nuovi dati per i punteggi oppure riservare alcuni dati per il test e non per il training.
  
    + I risultati della stima verranno salvati nella tabella _taxiscoreOutput_. Si noti che lo schema per questa tabella non è definito quando lo si crea con rxSqlServerData. Lo schema viene ottenuto dall'output di rxPredict.
  
    + Per creare la tabella che contiene i valori stimati, l'account di accesso SQL che esegue la funzione di dati rxSqlServer deve avere privilegi DDL nel database. Se l'account di accesso non può creare tabelle, l'istruzione ha esito negativo.

2. Chiamare la funzione [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) per generare i risultati.

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    Se l'istruzione ha esito positivo, l'esecuzione potrebbe richiedere del tempo. Al termine, è possibile aprire SQL Server Management Studio e verificare che la tabella sia stata creata e che contenga la colonna del punteggio e il resto dell'output previsto.

## <a name="plot-model-accuracy"></a>Tracciare l'accuratezza del modello

Per avere un'idea dell'accuratezza del modello, è possibile usare la funzione [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) per tracciare la curva operativa del ricevitore. Poiché rxRoc è una delle nuove funzioni offerte dal pacchetto RevoScaleR che supporta contesti di calcolo remoti, sono disponibili due opzioni:

+ È possibile usare la funzione rxRoc per eseguire il tracciato nel contesto di calcolo remoto e quindi restituire il tracciato al client locale.

+ È inoltre possibile importare i dati nel computer client R e usare altre funzioni di tracciato R per creare il grafico delle prestazioni.

In questa sezione verranno usate entrambe le tecniche.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Eseguire un tracciato nel contesto di calcolo remoto (SQL Server)

1. Chiamare la funzione rxRoc e fornire i dati definiti in precedenza come input.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    Questa chiamata restituisce i valori usati per il calcolo del grafico ROC. La colonna etichetta è _tipped_, che contiene i risultati effettivi che si sta tentando di prevedere, mentre la colonna _Score_ contiene la stima.

2. Per tracciare il grafico, è possibile salvare l'oggetto ROC, quindi disegnarlo con la funzione di creazione del tracciato. Il grafico viene creato nel contesto di calcolo remoto e restituito all'ambiente R.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    Visualizzare il grafico aprendo il dispositivo di grafica R oppure facendo clic sulla finestra **Plot** (Tracciato) in RStudio.

    ![Tracciato ROC per il modello](media/rsql-e2e-rocplot.png "Tracciato ROC per il modello")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Creare i tracciati nel contesto di calcolo locale usando i dati di SQL Server

È possibile verificare che il contesto di calcolo sia locale eseguendo `rxGetComputeContext()` al prompt dei comandi. Il valore restituito dovrebbe essere "RxLocalSeq Compute Context".

1. Per il contesto di calcolo locale, il processo è molto simile. Usare la funzione [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) per portare i dati specificati nell'ambiente R locale.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. Usando i dati nella memoria locale, caricare il pacchetto **ROCR** e usare la funzione di stima del pacchetto per creare nuove stime.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. Generare un tracciato locale in base ai valori archiviati nella variabile di output `pred`.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![traccia delle prestazioni del modello con R](media/rsql-e2e-performanceplot.png "traccia delle prestazioni del modello con R")

> [!NOTE]
> I grafici potrebbero avere un aspetto diverso da quelli illustrati qui, in base al numero di punti dati usati.

## <a name="deploy-the-model"></a>Distribuire il modello

Dopo aver creato un modello e aver verificato che funzioni correttamente, probabilmente lo si vorrà distribuire in un sito in cui gli utenti dell'organizzazione possano usarlo o anche ripetere il training e ricalibrare il modello a intervalli regolari. Questo processo viene talvolta denominato *operazionalizzazione* di un modello. In SQL Server l'operazionalizzazione si esegue incorporando il codice R in una stored procedure. Poiché il codice risiede nella stored procedure, può essere chiamato da qualsiasi applicazione in grado di connettersi a SQL Server.

Prima di poter chiamare il modello da un'applicazione esterna, è necessario salvarlo nel database usato per la produzione. I modelli sottoposti a training sono archiviati in formato binario, in un'unica colonna di tipo **varbinary(max)** .

Un flusso di lavoro di distribuzione tipico prevede i passaggi seguenti:

1. Serializzazione del modello in una stringa esadecimale
2. Trasmissione dell'oggetto serializzato al database
3. Salvataggio del modello in una colonna varbinary(max)

In questa sezione viene illustrato come usare una stored procedure per salvare in modo permanente il modello e renderlo disponibile per le stime. La stored procedure usata in questa sezione è PersistModel. La definizione di PersistModel si trova in [Prerequisiti](#prerequisites).

1. Tornare all'ambiente R locale se non lo si sta già usando, serializzare il modello e salvarlo in una variabile.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. Aprire una connessione ODBC usando **RODBC**. Se il pacchetto è già stato caricato, è possibile omettere la chiamata a RODBC.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. Chiamare la stored procedure PersistModel in SQL Server per trasmettere l'oggetto serializzato al database e archiviare la rappresentazione binaria del modello in una colonna. 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. Usare Management Studio per verificare che il modello esista. In Esplora oggetti fare clic con il pulsante destro del mouse sulla tabella **nyc_taxi_models** e scegliere **Seleziona le prime 1000 righe**. Nei risultati dovrebbe essere visualizzata una rappresentazione binaria nella colonna dei **modelli**.

Il salvataggio di un modello in una tabella richiede solo un'istruzione INSERT. Tuttavia, è spesso più semplice eseguendone il wrapping in una stored procedure, ad esempio *PersistModel*.

## <a name="next-steps"></a>Passaggi successivi

Nella prossima e ultima lezione verrà illustrato come eseguire l'assegnazione dei punteggi con il modello salvato tramite [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!div class="nextstepaction"]
> [Distribuire il modello R e usarlo in SQL](walkthrough-deploy-and-use-the-model.md)
