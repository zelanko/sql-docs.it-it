---
title: Trasformare i dati con RevoScaleR rxDataStep - SQL Server Machine Learning
description: Procedura dettagliata su come trasformare dati usando il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0da478798e87497da7828126b2168bbae5d980f7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962171"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>Trasformare dati tramite R (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa lezione, scoprirai le **RevoScaleR** funzioni per la trasformazione dei dati in varie fasi dell'analisi.

> [!div class="checklist"]
> * Uso **rxDataStep** per creare e trasformare un subset di dati
> * Uso **rxImport** per trasformare i dati in transito da o verso un file con estensione XDF o un frame di dati in memoria durante l'importazione

Sebbene non siano specificamente destinate allo spostamento dei dati, le funzioni **rxSummary**, **rxCube**, **rxLinMod**e **rxLogit** supportano tutte le trasformazioni dei dati.

## <a name="use-rxdatastep-to-transform-variables"></a>Usare rxDataStep per trasformare le variabili

La funzione [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) elabora i dati un blocco alla volta, leggendo da un'origine dati e scrivendo su un'altra. È possibile specificare le colonne da trasformare, le trasformazioni da caricare e così via.

Per rendere più interessante questo esempio, è possibile usare una funzione da un altro pacchetto R per trasformare i dati. Il pacchetto **Boot** è uno dei pacchetti "consigliati", per questo **Boot** è incluso in ogni distribuzione di R, ma non viene caricato automaticamente all'avvio. Pertanto, il pacchetto deve essere già disponibile nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza configurata per l'integrazione di R.

Dal **boot** del pacchetto, usare la funzione **INV. logit**, che calcola l'inverso di una funzione logit. Vale a dire, la funzione **inv.logit** converte una funzione logit di nuovo in una probabilità nella scala [0,1].

> [!TIP] 
> Un altro modo per ottenere stime in questa scala consiste nell'impostare il parametro *type* su **response** nella chiamata originale a **rxPredict**.

1. Per iniziare, creare un'origine dati per contenere i dati destinati per la tabella, `ccScoreOutput`.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. Aggiungere un'altra origine dati per contenere i dati per la tabella `ccScoreOutput2`.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    Nella nuova tabella, archiviare tutte le variabili dalla precedente `ccScoreOutput` tabella, più la variabile appena creata.
  
3. Impostare il contesto di calcolo sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Utilizzare la funzione **rxSqlServerTableExists** per verificare se la tabella di output `ccScoreOutput2` già esiste; e in questo caso, usare la funzione **rxSqlServerDropTable** per eliminare la tabella.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. Chiamare la funzione **rxDataStep** e specificare le trasformazioni appropriate in un elenco.
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    Quando si definiscono le trasformazioni applicate a ogni colonna, è possibile specificare anche eventuali pacchetti di R aggiuntivi necessari per eseguire le trasformazioni.  Per altre informazioni sui tipi di trasformazioni che è possibile eseguire, vedere [come subset e trasformare i dati con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform).
  
6. Chiamare **rxGetVarInfo** per visualizzare un riepilogo delle variabili nel set di dati nuovo.
  
```R
rxGetVarInfo(sqlOutScoreDS2)
```

**Risultati**

```R
Var 1: ccFraudLogitScore, Type: numeric
Var 2: state, Type: character
Var 3: gender, Type: character
Var 4: cardholder, Type: character
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: ccFraudProb, Type: numeric
```

I punteggi della funzione logit originali vengono mantenuti, ma una nuova colonna, *ccFraudProb*, è stata aggiunta, nella quale i punteggi della funzione logit sono rappresentati come valori tra 0 e 1.

Si noti che le variabili di fattore sono stati scritti nella tabella `ccScoreOutput2` come dati di tipo carattere. Se si vuole usarle come fattori nelle analisi successive, specificare i livelli tramite il parametro *colInfo* .

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Caricare i dati in memoria mediante rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)