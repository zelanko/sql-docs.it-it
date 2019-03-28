---
title: Compilare un modello R e salvare in SQL Server (procedura dettagliata) - SQL Server Machine Learning
description: Esercitazione che illustra come compilare un modello di linguaggio R usato per analitica nel database di SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 039e5a8970b2161bfe54b1836f3bd12b48477e1a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513058"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>Compilare un modello R e salvare in SQL Server (procedura dettagliata)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questo passaggio, informazioni su come creare un modello di machine learning e salvare il modello in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Salvando un modello, è possibile chiamarlo direttamente dal [!INCLUDE[tsql](../../includes/tsql-md.md)] il codice, tramite la stored procedure di sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) o il [funzione PREDICT (T-SQL)](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql).

## <a name="prerequisites"></a>Prerequisiti

Questo passaggio si presuppone una sessione di R in corso in base a quello precedente in questa procedura dettagliata. Usa connessione dati e stringhe di origine oggetti creati in tali passaggi. Gli strumenti e i pacchetti seguenti vengono utilizzati per eseguire lo script.

+ Rgui.exe per eseguire i comandi di R
+ Management Studio per eseguire T-SQL
+ Pacchetto ROCR
+ Pacchetto RODBC

### <a name="create-a-stored-procedure-to-save-models"></a>Creare una stored procedure per salvare i modelli

Questo passaggio Usa una stored procedure per salvare un modello con Training in SQL Server. Creazione di una stored procedure per eseguire questa operazione semplifica l'attività.

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
> Se si verifica un errore, assicurarsi che l'account di accesso disponga dell'autorizzazione per creare oggetti. È possibile concedere autorizzazioni esplicite per creare gli oggetti eseguendo un'istruzione T-SQL simile al seguente: `exec sp_addrolemember 'db_owner', '<user_name>'`.

## <a name="create-a-classification-model-using-rxlogit"></a>Creare un modello di classificazione tramite rxLogit

Il modello è un classificatore binario che consente di prevedere se il driver di taxi è tassista riceverà una Mancia in una particolare corsa oppure No. Si userà l'origine dati creata nella lezione precedente per eseguire il training del classificatore delle mance, uso della regressione logistica.

1. Chiamare la funzione [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) inclusa nel pacchetto **RevoScaleR** per creare un modello di regressione logistica. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    La chiamata che crea il modello è racchiusa nella funzione system.time. Ciò consente di ottenere il tempo necessario per compilare il modello.

2. Dopo aver compilato il modello, è possibile esaminare utilizzando il `summary` funzione e visualizzare i coefficienti.

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

1. In primo luogo, usare il [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) (funzione) per definire un oggetto origine dati per l'archiviazione del risultato di assegnazione dei punteggi.

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + Per semplificare questo esempio, l'input per il modello di regressione logistica è la stessa origine dati di funzionalità (`sql_feature_ds`) usato per il training del modello.  Più generalmente è possibile usare nuovi dati per i punteggi oppure riservare alcuni dati per il test e non per il training.
  
    + I risultati della stima verrà salvati nella tabella _taxiscoreOutput_. Si noti che lo schema per questa tabella non è definito quando si crea usando rxSqlServerData. Lo schema viene ottenuto dall'output rxPredict.
  
    + Per creare la tabella che archivia i valori stimati, l'account di accesso SQL che esegue la funzione dati rxSqlServer deve avere privilegi DDL nel database. Se l'account di accesso non è possibile creare tabelle, l'istruzione ha esito negativo.

2. Chiamare la funzione [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) per generare i risultati.

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    Se l'istruzione ha esito positivo, dovrebbe richiedere del tempo per l'esecuzione. Al termine dell'esercitazione, è possibile aprire SQL Server Management Studio e verificare che la tabella è stata creata e che contiene la colonna di punteggio e altri output previsto.

## <a name="plot-model-accuracy"></a>Tracciare l'accuratezza del modello

Per ottenere un'idea dell'accuratezza del modello, è possibile usare la [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) funzione per tracciare la curva operativa del ricevitore. Poiché rxRoc è una delle nuove funzioni fornite dal pacchetto RevoScaleR che supporta contesti di calcolo remoti, sono disponibili due opzioni:

+ È possibile usare la funzione rxRoc per eseguire il tracciato nel contesto di calcolo remoto e quindi restituire il tracciato al client locale.

+ È inoltre possibile importare i dati nel computer client R e usare altre funzioni di tracciato R per creare il grafico delle prestazioni.

In questa sezione proverà a usare entrambe le tecniche.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Eseguire un tracciato nel contesto di calcolo remoto (SQL Server)

1. Chiamare la funzione rxRoc e fornire i dati definiti in precedenza come input.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    Questa chiamata restituisce i valori utilizzati nel calcolo grafico ROC. La colonna etichetta è _tipped_, che contiene i risultati effettivi si sta tentando di stimare, mentre le _punteggio_ della colonna è la stima.

2. Per tracciare effettivamente il grafico, è possibile salvare l'oggetto ROC e quindi disegnare con la funzione del tracciato. Il grafico viene creato nel contesto di calcolo remoti e restituito all'ambiente R.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    Visualizzare il grafico aprendo il dispositivo di grafica R oppure facendo il **tracciare** finestra in RStudio.

    ![tracciato ROC per il modello](media/rsql-e2e-rocplot.png "tracciato ROC per il modello")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Creare i tracciati nel contesto di calcolo locale usando i dati di SQL Server

È possibile verificare il contesto di calcolo è locale eseguendo `rxGetComputeContext()` al prompt dei comandi. Il valore restituito deve essere "RxLocalSeq il contesto di calcolo".

1. Per il contesto di calcolo locale, il processo è molto simile. Si utilizza il [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) funzione per portare i dati specificati nell'ambiente R locale.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. Usando i dati nella memoria locale, si caricano i **ROCR** pacchetto e usare la funzione di stima di tale pacchetto per creare alcune nuove stime.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. Generare un tracciato locale, in base ai valori archiviati nella variabile di output `pred`.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![tracciare le prestazioni del modello con R](media/rsql-e2e-performanceplot.png "tracciare le prestazioni del modello con R")

> [!NOTE]
> I grafici potrebbero essere diversi da questi elementi, a seconda del numero di punti dati è stato usato.

## <a name="deploy-the-model"></a>Distribuire il modello

Dopo aver compilato un modello e ha accertato che stia funzionando correttamente, consigliabile distribuirla in un sito in cui gli utenti o gli utenti dell'organizzazione possono rendere utilizzare il modello, o forse ripetere il training e ricalibrare il modello a intervalli regolari. Questo processo è detto *messa in funzione* un modello. In SQL Server, messa in funzione consiste nell'incorporare codice R in una stored procedure. Poiché nella procedura si trova codice, può essere chiamato da qualsiasi applicazione in grado di connettersi a SQL Server.

Prima di chiamare il modello da un'applicazione esterna, è necessario salvare il modello per il database utilizzato per la produzione. Modelli di training vengono archiviati in formato binario, in una singola colonna di tipo **varbinary (max)**.

Un flusso di lavoro di distribuzione tipica è costituita dai passaggi seguenti:

1. Serializza il modello in una stringa esadecimale
2. Trasmettere l'oggetto serializzato al database
3. Salvare il modello in una colonna varbinary (max)

In questa sezione, informazioni su come usare una stored procedure per rendere permanente il modello e renderlo disponibile per le stime. La stored procedure utilizzata in questa sezione è PersistModel. La definizione di PersistModel è [prerequisiti](#prerequisites).

1. Se non usi già, passare all'ambiente R locale serializzare il modello e salvarlo in una variabile.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. Aprire una connessione ODBC mediante **RODBC**. È possibile omettere la chiamata a RODBC se hai già il pacchetto caricato.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. Chiamare la routine PersistModel archiviati in SQL Server a transmite l'oggetto serializzato al database e archiviare la rappresentazione binaria del modello in una colonna. 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. Usare Management Studio per verificare il modello esistente. In Esplora oggetti fare clic sui **nyc_taxi_models** tabella e fare clic su **seleziona le prime 1000 righe**. Nei risultati, si dovrebbe essere una rappresentazione binaria nel **modelli** colonna.

Il salvataggio di un modello in una tabella richiede solo un'istruzione INSERT. Tuttavia, è spesso più semplice quando è stato eseguito il wrapping in una stored procedure, ad esempio *PersistModel*.

## <a name="next-steps"></a>Passaggi successivi

Nella lezione successiva e ultima informazioni su come eseguire l'assegnazione dei punteggi in uso il modello salvato [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!div class="nextstepaction"]
> [Distribuire il modello R e usare in SQL](walkthrough-deploy-and-use-the-model.md)
