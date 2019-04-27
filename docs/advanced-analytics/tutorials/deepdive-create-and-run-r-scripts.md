---
title: 'Calcolare le statistiche summary RevoScaleR tutorial: SQL Server Machine Learning'
description: Procedura dettagliata su come calcolare statistiche di riepilogo statistiche Usa il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 883a4afa68571c18e6dcaffe96d12644f611f99a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641347"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>Calcolare le statistiche di riepilogo in R (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Per eseguire script R avanzati in questo Usa le origini dati stabiliti e contesti di calcolo creati nelle lezioni precedenti. In questa lezione si userà i contesti di calcolo locale e remota del server per le attività seguenti:

> [!div class="checklist"]
> * Cambiare il contesto di calcolo di SQL Server
> * Ottenere le statistiche di riepilogo sugli oggetti dati remoto
> * Calcolare un riepilogo locale

Se è stato completato le lezioni precedenti, è necessario che questi contesti di calcolo remoti: sqlCompute e sqlComputeTrace. In futuro, che si utilizza sqlCompute e locale calcolerà contesto nelle lezioni successive.

Usare un IDE R oppure **Rgui** per eseguire lo script R in questa lezione.

## <a name="compute-summary-statistics-on-remote-data"></a>Calcolare le statistiche di riepilogo sui dati remoti

Prima di poter eseguire qualsiasi codice R in modalità remota, è necessario specificare contesto di calcolo remoto. Tutti i calcoli successivi essere eseguite sul [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificato nel computer la *sqlCompute* parametro.

Un contesto di calcolo rimane attivo fino alla successiva modifica. Tuttavia, qualsiasi script R *non è possibile* esecuzione in un contesto server remoto verrà automaticamente eseguito in locale.

Per verificare il funzionamento di un contesto di calcolo, genera le statistiche di riepilogo sull'origine dati sqlFraudDS nel Server SQL remoto. Questo oggetto origine dati è stato creato nel [lezione due](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md) e rappresenta la tabella ccFraudSmall nel database RevoDeepDive. 

1. Passare il contesto di calcolo a sqlCompute creato nella lezione precedente:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. Chiamare il [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) funzioni e passare gli argomenti obbligatori, ad esempio la formula e l'origine dati e assegnare i risultati alla variabile `sumOut`.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    Il linguaggio R sono disponibili molte funzioni di riepilogo, ma **rxSummary** nelle **RevoScaleR** supporta l'esecuzione in diversi contesti di calcolo remoti, tra cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni sulle funzioni simili, vedere [riepiloghi dei dati con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).
  
3. Stampare il contenuto di sumOut nella console.
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > Se si verifica un errore, attendere alcuni minuti per l'esecuzione di completamento prima di ripetere il comando.

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
  
2. Quando si estraggono dati da SQL Server, è spesso possibile ottenere prestazioni migliori, aumentando il numero di righe estratte per ogni lettura, presupponendo che la dimensione del blocco maggiore può essere organizzata in memoria. Eseguire il comando seguente per aumentare il valore per il *rowsPerRead* parametro sull'origine dati. In precedenza, il valore di *rowsPerRead* era impostato su 5000.
  
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

4. Tornare a remoto contesto di calcolo per le diverse lezioni successive.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Visualizzare i dati di SQL Server tramite R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)