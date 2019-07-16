---
title: Visualizzare i dati di SQL Server tramite rxHistogram RevoScaleR - SQL Server Machine Learning
description: Procedura dettagliata su come visualizzare i dati usando il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 4092de07d19d4d33bd56025076e606269c2b04e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962158"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>Visualizzare i dati di SQL Server tramite R (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa lezione, usare le funzioni R per visualizzare la distribuzione dei valori di *creditLine* colonna in base al sesso.

> [!div class="checklist"]
> * Creare variabili min-max per gli input dell'istogramma
> * Visualizzare i dati in un istogramma tramite **rxHistogram** da **RevoScaleR**
> * Visualizzare con i grafici a dispersione usando **levelplot** dalla **reticolo** inclusi nella distribuzione base di R

Come illustrato in questa lezione, è possibile combinare funzioni specifiche di Microsoft e open source nello stesso script.

## <a name="add-maximum-and-minimum-values"></a>Aggiungere i valori minimi e massimo

Basato su statistiche di riepilogo calcolate nella lezione precedente, aver scoperto alcune informazioni utili sui dati che è possibile inserire nell'origine dati per un'ulteriore i calcoli. Ad esempio, i valori minimi e massimo utilizzabile per calcolare istogrammi. In questo esercizio, aggiungere i valori minimo e massimo per il **RxSqlServerData** origine dati.

1. Per iniziare si configurano alcune variabili temporanee.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Usare la variabile *ccColInfo* creato nella lezione precedente per definire le colonne nell'origine dati.
  
   Aggiungere nuove colonne calcolate (*numTrans*, *numIntlTrans*, e *creditLine*) alla raccolta di colonne che eseguono l'override la definizione originale. Lo script seguente consente di aggiungere fattori in base ai valori minimi e massimo, ottenuti da sumOut, che archivia l'output in memoria **rxSummary**. 
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")),
        cardholder = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
    ```
  
3. Dopo aver aggiornato la raccolta delle colonne, applicare l'istruzione seguente per creare una versione aggiornata del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origine dati definita in precedenza.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    L'origine dati sqlFraudDS include ora le nuove colonne aggiunte mediante *ccColInfo*.
  
A questo punto, le modifiche interessano solo l'oggetto di origine dati in R; Nessun nuovo dato è ancora stato scritto per la tabella di database. Tuttavia, è possibile utilizzare i dati acquisiti nella variabile sumOut per creare visualizzazioni e riepiloghi. 

> [!TIP]
> Se si ricorda il contesto di calcolo in uso, eseguire **rxGetComputeContext()** . Valore restituito di "Contesto di calcolo RxLocalSeq" indica che siano in esecuzione nel contesto di calcolo locale.

## <a name="visualize-data-using-rxhistogram"></a>Visualizzare i dati tramite rxHistogram

1. Usare il codice di R seguente per chiamare la funzione [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) e per passare una formula e l'origine dati. È possibile innanzitutto eseguire questa procedura localmente per visualizzare i risultati previsti e il tempo necessario.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    Internamente, **rxHistogram** chiama la funzione [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) inclusa nel pacchetto **RevoScaleR** . **rxCube** restituisce un singolo elenco (o un frame di dati) contenente una colonna per ogni variabile specificata nella formula, e una colonna di conteggi.
    
2. A questo punto, impostare il contesto di calcolo al computer SQL Server remoto ed eseguire **rxHistogram** nuovamente.
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. I risultati sono esattamente lo stesso perché si usa la stessa origine dati, mentre nel secondo passaggio, i calcoli vengono eseguiti nel server remoto. I risultati vengono poi restituiti alla workstation locale per eseguire il tracciato.
   
  ![risultati istogramma](media/rsql-sue-histogramresults.jpg "risultati istogramma")


## <a name="visualize-with-scatter-plots"></a>Visualizzare con i grafici a dispersione

Grafici a dispersione vengono spesso usati durante l'esplorazione dei dati per confrontare la relazione tra due variabili. È possibile usare i pacchetti R predefiniti per questo scopo, con gli input forniti da **RevoScaleR** funzioni.

1. Chiamare il [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) funzione per calcolare la media dei *fraudRisk* per ogni combinazione di *numTrans* e *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Per specificare i gruppi usati per il calcolo delle medie, usare la notazione `F()` . In questo esempio `F(numTrans):F(numIntlTrans)` indica che i numeri interi nelle variabili `numTrans` e `numIntlTrans` considerare come variabili categoriche, con un livello per ogni valore intero.
  
    Il valore predefinito restituito pari **rxCube** è un *oggetto rxCube*, che rappresenta una tabulazione incrociata. 
  
2. Chiamare [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) funzione per convertire i risultati in un frame di dati che può essere facilmente usato in una delle funzioni di tracciato standard di R.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    Il **rxCube** funzione include un argomento facoltativo *returnDataFrame* = **TRUE**, che è possibile usare per convertire direttamente i risultati in un frame di dati. Ad esempio:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    Tuttavia, l'output del **rxResultsDF** è più chiaro e mantiene i nomi delle colonne di origine. È possibile eseguire `head(cube1)` seguita da `head(cubePlot)` per confrontare l'output.
  
3. Creare una mappa termica usando la **levelplot** funzione di **reticolo** pacchetto, incluso in tutte le distribuzioni di R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Risultati**
  
    ![risultati grafico a dispersione](media/rsql-sue-scatterplotresults.jpg "risultati grafico a dispersione")
  
Questa analisi veloce, si noterà che il rischio di frode aumenta con il numero di transazioni e il numero di transazioni internazionali.

Per altre informazioni sul **rxCube** funzione e quelle dei campi incrociati in generale, vedere [riepiloghi dei dati con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Creare modelli R con dati di SQL Server](../../advanced-analytics/tutorials/deepdive-create-models.md)