---
title: Trasformare i dati con RevoScaleR
description: 'Esercitazione di RevoScaleR 9: Come trasformare dati usando il linguaggio R in SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 03f8b3f9cacd4faa77116cd560abfdb81596d074
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116734"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>Trasformare i dati con R (esercitazione su SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa è l'esercitazione 9 della [serie di esercitazioni per RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) dedicate all'uso delle [funzioni di RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa esercitazione vengono fornite informazioni sulle funzioni di **RevoScaleR** per la trasformazione dei dati in varie fasi dell'analisi.

> [!div class="checklist"]
> * Usare **rxDataStep** per creare e trasformare un subset di dati
> * Usare **rxImport** per trasformare i dati in transito da o verso un file XDF o un frame di dati in memoria durante l'importazione

Sebbene non siano specificamente destinate allo spostamento dei dati, le funzioni **rxSummary**, **rxCube**, **rxLinMod**e **rxLogit** supportano tutte le trasformazioni dei dati.

## <a name="use-rxdatastep-to-transform-variables"></a>Usare rxDataStep per trasformare le variabili

La funzione [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) elabora i dati un blocco alla volta, leggendo da un'origine dati e scrivendo su un'altra. È possibile specificare le colonne da trasformare, le trasformazioni da caricare e così via.

Per rendere più interessante questo esempio, verrà usata una funzione da un altro pacchetto R per la trasformazione dei dati. Il pacchetto **Boot** è uno dei pacchetti "consigliati", per questo **Boot** è incluso in ogni distribuzione di R, ma non viene caricato automaticamente all'avvio. Di conseguenza, il pacchetto deve essere già disponibile nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurata per l'integrazione con R.

Dal pacchetto **Boot** si attingerà alla funzione **inv.logit**, che calcola l'inverso di una funzione logit. Vale a dire, la funzione **inv.logit** converte una funzione logit di nuovo in una probabilità nella scala [0,1].

> [!TIP] 
> Un altro modo per ottenere stime in questa scala consiste nell'impostare il parametro *type* su **response** nella chiamata originale a **rxPredict**.

1. Iniziare creando un'origine dati per contenere i dati destinati alla tabella `ccScoreOutput`.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. Aggiungere un'altra origine dati per contenere i dati per la tabella `ccScoreOutput2`.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    La nuova tabella conterrà tutte le variabili della tabella `ccScoreOutput` precedente, più la variabile appena creata.
  
3. Impostare il contesto di calcolo sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Usare la funzione **rxSqlServerTableExists** per verificare se la tabella di output `ccScoreOutput2` esiste già e in tal caso usare la funzione **rxSqlServerDropTable** per eliminare la tabella.
  
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

    Quando si definiscono le trasformazioni applicate a ogni colonna, è possibile specificare anche eventuali pacchetti di R aggiuntivi necessari per eseguire le trasformazioni.  Per altre informazioni sui tipi di trasformazioni che è possibile eseguire, vedere [How to transform and subset data using RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform) (Come trasformare e creare subset di dati con RevoScaleR).
  
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

Osservare come le variabili di fattore siano state scritte nella tabella `ccScoreOutput2` come dati di tipo carattere. Se si vuole usarle come fattori nelle analisi successive, specificare i livelli tramite il parametro *colInfo* .

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Caricare i dati in memoria mediante rxImport](../../machine-learning/tutorials/deepdive-load-data-into-memory-using-rximport.md)