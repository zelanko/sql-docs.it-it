---
title: Valutare nuovi dati con RevoScaleR e rxPredict - SQL Server Machine Learning
description: Procedura dettagliata su come assegnare un punteggio dei dati tramite il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b96e70a6002722063a0be42c964c5e423503a0d7
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510348"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>Valutare nuovi dati (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questo passaggio si usa il modello di regressione logistica creato nella lezione precedente, per assegnare punteggi a un altro set di dati che usa le stesse variabili indipendenti come input.

> [!div class="checklist"]
> * Assegnare un punteggio ai nuovi dati
> * Creare un istogramma dei punteggi

> [!NOTE]
> Sono necessari privilegi di amministratore DDL per alcuni di questi passaggi.

## <a name="generate-and-save-scores"></a>Generare e salvare i punteggi
  
1. Aggiornare l'origine dati sqlScoreDS (creato nella [lezione due](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)) usare le informazioni di colonna creato nella lezione precedente.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. Per assicurarsi di non perdere i risultati, creare un nuovo oggetto origine dati. Quindi, usare il nuovo oggetto origine dati per popolare una nuova tabella nel database RevoDeepDive.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    A questo punto la tabella non è stata creata. Questa istruzione definisce solo un contenitore per i dati.
     
3. Controllare il contesto di calcolo corrente utilizzando **rxGetComputeContext()** e impostare il contesto di calcolo per il server, se necessario.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Come precauzione, verificare l'esistenza della tabella di output. Se ne esiste già uno con lo stesso nome, si otterrà un errore durante il tentativo di scrivere la nuova tabella.
  
    A tale scopo, chiamare le funzioni [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) e [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable), passando il nome della tabella come input.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists** esegue una query il driver ODBC e restituisce TRUE se la tabella esiste, FALSE in caso contrario.
    + **rxSqlServerDropTable** esegue l'istruzione DDL e restituisce TRUE se la tabella è stata eliminata, FALSE in caso contrario.

5. Eseguire [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) per creare i punteggi e salvarli nella nuova tabella definita in sqlScoreDS origine dati.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    La funzione **rxPredict** è un'altra funzione che supporta l'esecuzione in contesti di calcolo remoti. È possibile usare la **rxPredict** funzione per creare i punteggi da modelli di base [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit), oppure [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm).
  
    - Il parametro *writeModelVars* è impostato su **TRUE** qui. Ciò significa che le variabili usate per la stima verranno incluse nella nuova tabella.
  
    - Il parametro *predVarNames* specifica la variabile in cui verranno archiviati i risultati. Qui si passa una nuova variabile, `ccFraudLogitScore`.
  
    - Il parametro *type* per **rxPredict** definisce la modalità di calcolo delle stime. Specificare la parola chiave **risposta** per generare punteggi basati sulla scala della variabile di risposta. In alternativa, usare la parola chiave **collegamento** per generare punteggi basati sulla funzione di collegamento sottostante, nel qual caso le stime vengono create utilizzando una scala logistica.

6. Attendere un attimo prima di aggiornare l'elenco delle tabelle in Management Studio e visualizzare la nuova tabella con i dati.

7. Per aggiungere variabili aggiuntive alle stime di output, usare l'argomento *extraVarsToWrite*.  In questo codice, ad esempio, la variabile *custID* della tabella dei dati dei punteggi viene aggiunta alla tabella di output delle stime.
  
    ```R
    rxPredict(modelObject = logitObj,
            data = sqlScoreDS,
            outData = sqlServerOutDS,
            predVarNames = "ccFraudLogitScore",
              type = "link",
            writeModelVars = TRUE,
            extraVarsToWrite = "custID",
            overwrite = TRUE)
    ```

## <a name="display-scores-in-a-histogram"></a>Punteggi di visualizzazione in un istogramma

Dopo aver creata la nuova tabella, calcolare e visualizzare un istogramma dei 10.000 punteggi stimati. Calcolo è più veloce se si specificano i valori minimo e massimo, pertanto, estrarli dal database e aggiungerli ai dati in uso.

1. Creare una nuova origine dati, sqlMinMax, che esegue una query al database per ottenere i valori minimo e massimo.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     Questo esempio spiega come è facile usare gli oggetti origine dati **RxSqlServerData** per definire set di dati arbitrari basati su query SQL, funzioni o stored procedure e usarli nel codice R. La variabile non archivia i valori effettivi, ma solo la definizione dell'origine dati. La query viene eseguita per generare i valori solo se usata in una funzione come **rxImport**.
      
2. Chiamare il [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) (funzione) per inserire i valori in un frame di dati che può essere condivisi tra i vari contesti di calcolo.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **Risultati**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. Ora che i valori minimo e massimi sono disponibili, usare i valori per creare un'altra origine dati per i punteggi generati.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. Usare il sqlOutScoreDS oggetto origine dati per ottenere i punteggi, calcolare e visualizzare un istogramma. Aggiungere il codice per impostare il contesto di calcolo, se necessario.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **Risultati**
  
    ![istogramma complesso creato da R](media/rsql-sue-complex-histogram.png "istogramma complesso creato da R")
  
## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Trasformare i dati con R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)