---
title: Esercitazione sulle statistiche di riepilogo di calcolo RevoScaleR
description: Esercitazione dettagliata su come calcolare le statistiche di riepilogo statistico usando il linguaggio R su SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5b1ec344a2ec9728a24d45c47dd80737e6155b01
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469818"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>Statistiche di riepilogo di calcolo in R (esercitazione SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa lezione fa parte dell' [esercitazione su RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare le [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Usa le origini dati stabilite e i contesti di calcolo creati nelle lezioni precedenti per eseguire script R ad alta potenza in questo. In questa lezione si useranno i contesti di calcolo del server locale e remoto per le attività seguenti:

> [!div class="checklist"]
> * Impostare il contesto di calcolo su SQL Server
> * Ottenere statistiche di riepilogo sugli oggetti dati remoti
> * Calcolare un riepilogo locale

Se sono state completate le lezioni precedenti, è necessario disporre di questi contesti di calcolo remoti: sqlcompute e sqlComputeTrace. In futuro sarà possibile utilizzare sqlcompute e il contesto di calcolo locale nelle lezioni successive.

Usare un IDE R o **Rgui** per eseguire lo script r in questa lezione.

## <a name="compute-summary-statistics-on-remote-data"></a>Calcolo delle statistiche di riepilogo sui dati remoti

Prima di poter eseguire qualsiasi codice R in modalità remota, è necessario specificare il contesto di calcolo remoto. Tutti i calcoli successivi avvengono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel computer specificato nel parametro sqlcompute  .

Un contesto di calcolo rimane attivo fino a quando non viene modificato. Tuttavia, gli script R che *non possono essere* eseguiti in un contesto server remoto verranno eseguiti automaticamente in locale.

Per verificare il funzionamento di un contesto di calcolo, generare statistiche di riepilogo sull'origine dati sqlFraudDS nel SQL Server remoto. Questo oggetto origine dati è stato creato nella [lezione 2](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md) e rappresenta la tabella ccFraudSmall nel database RevoDeepDive. 

1. Passare il contesto di calcolo a sqlcompute creato nella lezione precedente:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. Chiamare la funzione [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) e passare gli argomenti obbligatori, ad esempio la formula e l'origine dati, e assegnare i risultati alla `sumOut`variabile.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    Il linguaggio R fornisce molte funzioni di riepilogo, ma **rxSummary** in **RevoScaleR** supporta l'esecuzione in diversi contesti di calcolo remoti, tra cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni sulle funzioni simili, vedere [riepiloghi dei dati con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).
  
3. Stampare il contenuto di sumOut nella console.
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > Se viene ricevuto un errore, attendere alcuni minuti per completare l'esecuzione prima di riprovare a eseguire il comando.

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
  
2. Quando si estraggono i dati da SQL Server, è spesso possibile ottenere prestazioni migliori aumentando il numero di righe estratte per ogni lettura, supponendo che la dimensione del blocco aumentata possa essere adattata in memoria. Eseguire il comando seguente per aumentare il valore del parametro *rowsPerRead* nell'origine dati. In precedenza, il valore di *rowsPerRead* era impostato su 5000.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. Chiamare **rxSummary** sulla nuova origine dati.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
   I risultati effettivi devono corrispondere a quelli ottenuti con l'esecuzione di **rxSummary** nel contesto del computer con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'operazione potrebbe tuttavia essere più veloce o più lenta a seconda del tipo di connessione al database. Per essere analizzati, i dati vengono infatti trasferiti nel computer locale.

4. Tornare al contesto di calcolo remoto per le varie lezioni successive.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Visualizzare i dati di SQL Server tramite R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)