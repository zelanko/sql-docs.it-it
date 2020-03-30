---
title: Assegnazione dei punteggi ai dati con RevoScaleR
description: 'Esercitazione di RevoScaleR 8: Come assegnare un punteggio ai dati usando il linguaggio R in SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 26f5c7b56298e6a3bd5f1fa9d8bc1d4db79d60af
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "74947194"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>Assegnare punteggi ai nuovi dati (esercitazione su SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa è l'esercitazione 8 della [serie di esercitazioni per RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) dedicate all'uso delle [funzioni di RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa esercitazione si userà il modello di regressione logistica creato nell'esercitazione precedente per assegnare punteggi a un altro set di dati che usa le stesse variabili indipendenti come input.

> [!div class="checklist"]
> * Assegnare un punteggio ai nuovi dati
> * Creare un istogramma dei punteggi

> [!NOTE]
> Per alcuni di questi passaggi sono necessari privilegi di amministratore DDL.

## <a name="generate-and-save-scores"></a>Generare e salvare i punteggi
  
1. Aggiornare l'origine dati sqlScoreDS (creata nell'[esercitazione due](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)) per usare le informazioni sulle colonne generate nell'esercitazione precedente.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. Per avere la certezza che i risultati non vadano persi, creare un nuovo oggetto origine dati. Usare quindi il nuovo oggetto origine dati per popolare una nuova tabella nel database RevoDeepDive.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    A questo punto la tabella non è stata creata. Questa istruzione definisce solo un contenitore per i dati.
     
3. Verificare il contesto di calcolo corrente con **rxGetComputeContext()** e impostare il contesto di calcolo per il server, se necessario.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. A titolo precauzionale, verificare l'effettiva esistenza della tabella di output. Se ne esiste già uno con lo stesso nome, nel momento in cui si tenta di scrivere la nuova tabella, si otterrà un errore.
  
    A tale scopo, chiamare le funzioni [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) e [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable), passando il nome della tabella come input.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists** esegue una query sul driver ODBC e restituisce TRUE se la tabella esiste, FALSE in caso contrario.
    + **rxSqlServerDropTable** esegue l'istruzione DDL e restituisce TRUE se la tabella è stata eliminata, FALSE in caso contrario.

5. Eseguire la funzione [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) per creare i punteggi e salvarli nella nuova tabella definita nell'origine dati sqlScoreDS.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    La funzione **rxPredict** è un'altra funzione che supporta l'esecuzione in contesti di calcolo remoti. È possibile usare la funzione **rxPredict** per creare punteggi a partire da modelli basati su [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) o [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm).
  
    - Il parametro *writeModelVars* è impostato su **TRUE** qui. Ciò significa che le variabili usate per la stima verranno incluse nella nuova tabella.
  
    - Il parametro *predVarNames* specifica la variabile in cui verranno archiviati i risultati. A questo punto viene passata una nuova variabile denominata `ccFraudLogitScore`.
  
    - Il parametro *type* per **rxPredict** definisce la modalità di calcolo delle stime. Specificare la parola chiave **response** per generare i punteggi in base alla scala della variabile di risposta. In alternativa, usare la parola chiave **link** per generare i punteggi in base alla funzione di collegamento sottostante. In questo caso, le stime vengono create usando una scala logistica.

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

Dopo aver creato la nuova tabella, calcolare e visualizzare un istogramma dei 10.000 punteggi stimati. Il calcolo è più veloce se si specificano i valori minimo e massimo. Estrarli quindi dal database e aggiungerli ai dati in uso.

1. Creare una nuova origine dati, sqlMinMax, per eseguire una query sul database e ottenere i valori minimo e massimo.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     Questo esempio spiega come è facile usare gli oggetti origine dati **RxSqlServerData** per definire set di dati arbitrari basati su query SQL, funzioni o stored procedure e usarli nel codice R. La variabile non archivia i valori effettivi, ma solo la definizione dell'origine dati. La query viene eseguita per generare i valori solo se usata in una funzione come **rxImport**.
      
2. Chiamare la funzione [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) per inserire i valori in un frame di dati che può essere condiviso tra vari contesti di calcolo.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **Risultati**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. Ora che i valori minimo e massimo sono disponibili, è possibile usarli per creare un'altra origine dati per i punteggi generati.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. Usare infine l'oggetto origine dati sqlOutScoreDS per ottenere i punteggi, calcolare e visualizzare un istogramma. Aggiungere il codice per impostare il contesto di calcolo, se necessario.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **Risultati**
  
    ![istogramma complesso creato da R](media/rsql-sue-complex-histogram.png "istogramma complesso creato da R")
  
## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Trasformare i dati con R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)