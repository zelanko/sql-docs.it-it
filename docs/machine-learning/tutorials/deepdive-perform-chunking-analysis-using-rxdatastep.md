---
title: Analisi in blocchi in RevoScaleR
description: "Esercitazione di RevoScaleR 12: Come dividere i dati in blocchi per l'analisi distribuita usando il linguaggio R in SQL Server."
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a1dd8b47f7a251918eb87db9a8ec2dfd9d412a10
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179890"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Eseguire l'analisi in blocchi usando rxDataStep (esercitazione su SQL Server e RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Questa è l'esercitazione 12 della [serie di esercitazioni per RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) dedicate all'uso delle [funzioni di RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa esercitazione si userà la funzione **rxDataStep** per elaborare i dati in blocchi, anziché caricare nella memoria l'intero set di dati ed elaborarlo in una sola volta come succede nel codice R tradizionale. La funzione **rxDataStep** legge i dati in blocchi, applica le funzioni R ad ogni blocco di dati (uno per volta) e salva i risultati di riepilogo di ogni blocco in un'origine dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comune. Quando tutti i dati sono stati letti, i risultati vengono combinati.

> [!TIP]
> Per questa esercitazione si calcola una tabella di contingenza usando la funzione **table** in R. Questo esempio è stato ideato solo per scopi didattici. 
> 
> Per catalogare set di dati reali, è consigliabile usare le funzioni **rxCrossTabs** e **rxCube** di **RevoScaleR**, in quanto sono ottimizzate per questo tipo di operazione.

## <a name="partition-data-by-values"></a>Suddividere i dati in partizioni in base ai valori

1. Creare una funzione R personalizzata con la quale chiamare la funzione **table** in ogni blocco di dati e denominare la nuova funzione **ProcessChunk**.
  
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
  
3. Definire un'origine dati SQL Server per contenere i dati che si sta elaborando, assegnando prima una query SQL a una variabile. Collegare quindi la variabile all'argomento *sqlQuery* di una nuova origine dati SQL Server.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. Facoltativamente, è possibile eseguire **rxGetVarInfo** in questa origine dati. Il set di risultati, a questo punto, contiene un'unica colonna. *Var 1: DayOfWeek, Type: factor, no factor levels available*
     
5. Prima di applicare questa variabile di fattore all'origine dati, creare una tabella separata in cui includere i risultati intermedi. Anche in questo caso è sufficiente usare la funzione **RxSqlServerData** per definire i dati, accertandosi di eliminare eventuali tabelle esistenti con lo stesso nome.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Chiamare la funzione personalizzata **ProcessChunk** per trasformare i dati letti, usandola come argomento *transformFunc* per la funzione **rxDataStep**.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Per visualizzare i risultati intermedi di **ProcessChunk**, assegnare i risultati di **rxImport** a una variabile e visualizzare i risultati nella console.
  
    ```R
    iroResults <- rxImport(iroDataSource)
    iroResults
    ```

    **Risultati parziali**

    | \# riga |    1  |   2   |  3   |  4   |  5  |   6   |  7 |
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

10. Per rimuovere la tabella contenente i risultati intermedi, chiamare **rxSqlServerDropTable**.
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Esercitazioni di R per SQL Server](sql-server-r-tutorials.md)