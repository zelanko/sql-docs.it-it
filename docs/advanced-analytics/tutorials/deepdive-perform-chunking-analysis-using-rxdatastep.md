---
title: Eseguire l'analisi di suddivisione in blocchi usando RevoScaleR rxDataStep
description: Esercitazione dettagliata su come suddividere i dati per l'analisi distribuita usando il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ed22020b162bfac9f35eb8328ea6409903191a4c
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714890"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Eseguire un'analisi in blocchi usando rxDataStep (esercitazione SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa lezione fa parte dell' [esercitazione su RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare le [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa lezione si userà la funzione **rxDataStep** per elaborare i dati in blocchi, anziché richiedere che l'intero set di dati venga caricato in memoria ed elaborato in una sola volta, come nel tradizionale R. Le funzioni **rxDataStep** leggono i dati in blocco, applica le funzioni R a ogni blocco di dati, quindi Salva i risultati di riepilogo per ogni blocco in un'origine dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comune. Quando tutti i dati sono stati letti, i risultati vengono combinati.

> [!TIP]
> Per questa lezione, si calcola una tabella di contingenza usando la funzione **Table** in R. Questo esempio è progettato solo a scopo informativo. 
> 
> Se è necessario catalogare set di dati reali, è consigliabile usare le funzioni **rxCrossTabs** o **rxCube** in **RevoScaleR**, ottimizzate per questo tipo di operazione.

## <a name="partition-data-by-values"></a>Partizionare i dati in base ai valori

1. Creare una funzione R personalizzata che chiama la funzione di **tabella** r per ogni blocco di dati e denominare la nuova funzione **ProcessChunk**.
  
    ```R
    ProcessChunk <- function( dataList) {
    # Convert the input list to a data frame and compute contingency table
    chunkTable <- table(as.data.frame(dataList))
  
    # Convert table output to a data frame with a single row
    varNames <- names(chunkTable)
    varValues <- as.vector(chunkTable)
    dim(varValues) <- c(1, length(varNames))
    chunkDF <- as.data.frame(varValues)
    names(chunkDF) <- varNames
  
    # Return the data frame, which has a single row
    return( chunkDF )
    }
    ```

2. Impostare il contesto di calcolo server.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
3. Definire un'origine dati SQL Server per conservare i dati che si stanno elaborando. assegnando prima una query SQL a una variabile. Usare quindi tale variabile nell'argomento *sqlQuery* di una nuova origine dati SQL Server.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. Facoltativamente, è possibile eseguire **rxGetVarInfo** su questa origine dati. A questo punto, contiene una singola colonna: *Var 1: DayOfWeek, tipo: Factor, nessun livello di fattore disponibile*
     
5. Prima di applicare questa variabile di fattore all'origine dati, creare una tabella separata in cui includere i risultati intermedi. Anche in questo caso, è sufficiente utilizzare la funzione **RxSqlServerData** per definire i dati, assicurandosi di eliminare tutte le tabelle esistenti con lo stesso nome.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Chiamare la funzione personalizzata **ProcessChunk** per trasformare i dati durante la lettura, usandola come argomento *transformFunc* per la funzione **rxDataStep** .
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Per visualizzare i risultati intermedi di **ProcessChunk**, assegnare i risultati di **rxImport** a una variabile e quindi restituire i risultati alla console.
  
    ```R
    iroResults <- rxImport(iroDataSource)
    iroResults
    ```

    **Risultati parziali**

    |      |    1  |   2   |  3   |  4   |  5  |   6   |  7 |
    | --- | ---  | --- | ---  |  ---  | ---  | ---  | --- |
    | 1 | 8228 | 8924 | 6916 | 6932 | 6944 | 5602 | 6454 |
    | 2  | 8321  | 5351 | 7329 | 7411 | 7409 | 6487 | 7692 |

9. Per calcolare i risultati finali di tutti i blocchi, sommare le colonne e visualizzare i risultati nella console.

    ```R
    finalResults <- colSums(iroResults)
    finalResults
    ```

    **Risultati**

    1  |   2  |   3  |   4  |   5  |   6  |   7
    ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---
    97975 | 77725 | 78875 | 81304 | 82987 | 86159 | 94975 

10. Per rimuovere la tabella dei risultati intermedi, effettuare una chiamata a **rxSqlServerDropTable**.
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Esercitazioni di R per SQL Server](sql-server-r-tutorials.md)