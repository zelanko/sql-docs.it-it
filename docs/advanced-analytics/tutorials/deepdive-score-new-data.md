---
title: Assegnare un punteggio ai nuovi dati usando RevoScaleR e rxPredict
description: Esercitazione dettagliata su come assegnare un punteggio ai dati usando il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ff3782fb760e4d3dd1059103bc835b94d9c7581f
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714828"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>Assegnare un punteggio ai nuovi dati (esercitazione SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa lezione fa parte dell' [esercitazione su RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare le [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questo passaggio viene usato il modello di regressione logistica creato nella lezione precedente per assegnare un punteggio a un altro set di dati che usa le stesse variabili indipendenti come input.

> [!div class="checklist"]
> * Assegnare un punteggio ai nuovi dati
> * Creare un istogramma dei punteggi

> [!NOTE]
> Per alcuni di questi passaggi sono necessari i privilegi di amministratore DDL.

## <a name="generate-and-save-scores"></a>Generare e salvare i punteggi
  
1. Aggiornare l'origine dati sqlScoreDS (creata nella [lezione 2](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)) per utilizzare le informazioni sulle colonne create nella lezione precedente.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. Per assicurarsi di non perdere i risultati, creare un nuovo oggetto origine dati. Usare quindi il nuovo oggetto origine dati per popolare una nuova tabella nel database RevoDeepDive.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    A questo punto la tabella non è stata creata. Questa istruzione definisce solo un contenitore per i dati.
     
3. Controllare il contesto di calcolo corrente usando **rxGetComputeContext ()** e impostare il contesto di calcolo sul server, se necessario.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Per precauzione, verificare l'esistenza della tabella di output. Se ne esiste già uno con lo stesso nome, si otterrà un errore quando si tenta di scrivere la nuova tabella.
  
    A tale scopo, chiamare le funzioni [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) e [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable), passando il nome della tabella come input.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists** esegue una query sul driver ODBC e restituisce true se la tabella esiste, false in caso contrario.
    + **rxSqlServerDropTable** esegue il DDL e restituisce true se la tabella viene eliminata correttamente; in caso contrario, false.

5. Eseguire [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) per creare i punteggi e salvarli nella nuova tabella definita nell'origine dati sqlScoreDS.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    La funzione **rxPredict** è un'altra funzione che supporta l'esecuzione in contesti di calcolo remoti. È possibile usare la funzione **rxPredict** per creare punteggi da modelli basati su [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)o [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm).
  
    - Il parametro *writeModelVars* è impostato su **TRUE** qui. Ciò significa che le variabili usate per la stima verranno incluse nella nuova tabella.
  
    - Il parametro *predVarNames* specifica la variabile in cui verranno archiviati i risultati. Qui viene passata una nuova variabile, `ccFraudLogitScore`.
  
    - Il parametro *type* per **rxPredict** definisce la modalità di calcolo delle stime. Specificare la **risposta** alla parola chiave per generare i punteggi in base alla scala della variabile di risposta. In alternativa, usare la parola chiave **link** per generare punteggi basati sulla funzione di collegamento sottostante, nel qual caso le stime vengono create usando una scala logistica.

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

## <a name="display-scores-in-a-histogram"></a>Visualizzare i punteggi in un istogramma

Dopo aver creato la nuova tabella, calcolare e visualizzare un istogramma dei punteggi stimati 10.000. Il calcolo è più veloce se si specificano i valori minimo e massimo, quindi è possibile recuperarli dal database e aggiungerli ai dati di lavoro.

1. Creare una nuova origine dati, sqlMinMax, che esegue una query sul database per ottenere i valori minimo e massimo.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     Questo esempio spiega come è facile usare gli oggetti origine dati **RxSqlServerData** per definire set di dati arbitrari basati su query SQL, funzioni o stored procedure e usarli nel codice R. La variabile non archivia i valori effettivi, ma solo la definizione dell'origine dati. La query viene eseguita per generare i valori solo se usata in una funzione come **rxImport**.
      
2. Chiamare la funzione [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) per inserire i valori in un frame di dati che può essere condiviso tra i contesti di calcolo.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **Risultati**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. Ora che i valori massimi e minimi sono disponibili, usare i valori per creare un'altra origine dati per i punteggi generati.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. Usare l'oggetto origine dati sqlOutScoreDS per ottenere i punteggi e calcolare e visualizzare un istogramma. Aggiungere il codice per impostare il contesto di calcolo, se necessario.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **Risultati**
  
    ![istogramma complesso creato da R](media/rsql-sue-complex-histogram.png "istogramma complesso creato da R")
  
## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Trasformare i dati con R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)