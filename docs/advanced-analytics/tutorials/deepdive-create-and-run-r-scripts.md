---
title: Statistiche di riepilogo in RevoScaleR
description: 'Esercitazione di RevoScaleR 5: Come calcolare statistiche di riepilogo usando il linguaggio R in SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 43745602fc099f1b992eb1d76622ff3d7e6d0916
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "74947279"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>Elaborare statistiche di riepilogo in R (esercitazione su SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa è l'esercitazione 5 della [serie di esercitazioni per RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) dedicate all'uso delle [funzioni di RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa esercitazione vengono usati le origini dati prestabilite e i contesti di calcolo creati nelle esercitazioni precedenti per eseguire script R ad alta potenza. In questa esercitazione si useranno contesti di calcolo di server locali e remoti per le attività seguenti:

> [!div class="checklist"]
> * Impostare il contesto di calcolo su SQL Server
> * Ottenere statistiche di riepilogo sui Remote Data Object
> * Elaborare un riepilogo locale

Se sono state completate le esercitazioni precedenti, dovrebbero essere disponibili i contesti di calcolo remoti seguenti: sqlCompute e sqlComputeTrace. Il contesto di calcolo sqlCompute e il contesto di calcolo locale verranno usati nelle esercitazioni successive.

In questa esercitazione usare un'IDE R o **Rgui** per eseguire lo script R.

## <a name="compute-summary-statistics-on-remote-data"></a>Calcolare statistiche di riepilogo sui dati remoti

Prima di eseguire qualsiasi codice R in remoto, è necessario specificare il contesto di calcolo remoto. Tutti i calcoli successivi si svolgono nel computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indicato nel parametro *sqlCompute*.

Un contesto di calcolo resta attivo fino a quando non lo si modifica. Tuttavia, qualsiasi script R *non* eseguibile in un contesto server remoto verrà automaticamente eseguito in locale.

Per vedere come funziona un contesto di calcolo, generare statistiche di riepilogo sull'origine dati sqlFraudDS nell'istanza remota di SQL Server. Questo oggetto origine dati è stato creato nell'[esercitazione 2](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md) e rappresenta la tabella ccFraudSmall del database RevoDeepDive. 

1. Impostare il contesto di calcolo sul contesto sqlCompute creato nell'esercitazione precedente:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. Chiamare la funzione [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) e passare gli argomenti obbligatori, ad esempio la formula e l'origine dati, e assegnare i risultati alla variabile `sumOut`.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    Con il linguaggio R sono disponibili molte funzioni di riepilogo. La funzione **rxSummary** in **RevoScaleR** supporta tuttavia l'esecuzione in diversi contesti remoti, tra cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni sulle funzioni simili, vedere [Come riepilogare i dati tramite RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).
  
3. Stampare il contenuto di sumOut nella console.
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > Se si riceve un errore, attendere alcuni minuti per essere certi che l'esecuzione sia completata prima di riprovare a eseguire il comando.

**Risultati**

```R
Summary Statistics Results for: ~gender + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Number of valid observations: 10000

 Name  Mean    StdDev  Min Max ValidObs    MissingObs
 balance       4075.0318 3926.558714            0   25626 100000
 numTrans        29.1061   26.619923 0     100 10000    0           100000
 numIntlTrans     4.0868    8.726757 0      60 10000    0           100000
 creditLine       9.1856    9.870364 1      75 10000    0          100000
 
 Category Counts for gender
 Number of categories: 2
 Number of valid observations: 10000
 Number of missing observations: 0

 gender Counts
  Male   6154
  Female 3846
```

## <a name="create-a-local-summary"></a>Creare un riepilogo locale

1. Modificare il contesto di calcolo per eseguire il lavoro localmente .
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. Quando si estraggono dati da SQL Server, per ottenere prestazioni migliori è possibile aumentare il numero di righe estratte per ogni lettura, supponendo che la maggiore dimensione del blocco possa essere adattata in memoria. Eseguire il comando seguente per aumentare il valore del parametro *rowsPerRead* nell'origine dati. In precedenza, il valore di *rowsPerRead* era impostato su 5000.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. Chiamare **rxSummary** nella nuova origine dati.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
   I risultati effettivi devono corrispondere a quelli ottenuti con l'esecuzione di **rxSummary** nel contesto del computer con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'operazione potrebbe tuttavia essere più veloce o più lenta a seconda del tipo di connessione al database. Per essere analizzati, i dati vengono infatti trasferiti nel computer locale.

4. Tornare al contesto di calcolo remoto per affrontare le esercitazioni successive.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Visualizzare i dati di SQL Server tramite R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)