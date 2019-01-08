---
title: Eseguire un'analisi in blocchi tramite rxDataStep RevoScaleR - SQL Server Machine Learning
description: Procedura dettagliata su come suddividere i dati per l'analisi distribuita usando il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c5d3b50af1f7db3a39dec0e475aa00582bc77e0a
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596032"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Eseguire un'analisi in blocchi tramite rxDataStep (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa lezione, Usa la **rxDataStep** funzione per elaborare i dati in blocchi invece di richiedere che l'intero set di dati essere caricati in memoria ed elaborati in una sola volta, come nel codice r tradizionale. Il **rxDataStep** funzioni legge i dati in blocco, si applica a sua volta di funzioni R per ogni blocco di dati e quindi Salva i risultati di riepilogo per ogni blocco a un comune [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zdroj dat. Quando tutti i dati sono stati letti, i risultati vengono combinati.

> [!TIP]
> Per questa lezione, si calcola una tabella di emergenza utilizzando il **tabella** funzione in R. Questo esempio è studiato solo per scopi didattici. 
> 
> Se è necessario catalogare set di dati reali, è consigliabile usare la **rxCrossTabs** oppure **rxCube** delle funzioni **RevoScaleR**, ottimizzati per questa sorta di operazione.

## <a name="partition-data-by-values"></a>Partizionare i dati dai valori

1. Creare una funzione R personalizzata che chiama R **tabella** funzionino in ogni blocco di dati e il nome della nuova funzione **ProcessChunk**.
  
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
  
3. Definire un'origine dati di SQL Server per contenere i dati che si sta elaborando. assegnando prima una query SQL a una variabile. Quindi, usare tale variabile nel *sqlQuery* argomento di una nuova origine dati SQL Server.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. Facoltativamente, è possibile eseguire **rxGetVarInfo** su questa origine dati. A questo punto, contiene una singola colonna: *VAR 1: DayOfWeek, Type: factor, non livelli di fattore disponibili*
     
5. Prima di applicare questa variabile di fattore all'origine dati, creare una tabella separata in cui includere i risultati intermedi. Anche in questo caso, è sufficiente utilizzare il **RxSqlServerData** (funzione) per definire i dati, assicurandosi di eliminare le tabelle esistenti con lo stesso nome.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Chiamare la funzione personalizzata **ProcessChunk** per trasformare i dati man mano che verrà letti, usandola come le *transformFunc* argomento per il **rxDataStep** (funzione).
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Per visualizzare i risultati intermedi della **ProcessChunk**, assegnare i risultati del **rxImport** a una variabile e quindi i risultati nella console.
  
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