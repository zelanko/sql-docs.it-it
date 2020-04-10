---
title: Visualizzare i dati con RevoScaleR
description: 'Esercitazione di RevoScaleR 6: Come visualizzare i dati usando il linguaggio R in SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4cc97db70461797e2e37614ae33d23ed51b21147
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116724"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>Visualizzare i dati di SQL Server con R (esercitazione su SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa è l'esercitazione 6 della [serie di esercitazioni per RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) dedicate all'uso delle [funzioni di RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa esercitazione si useranno le funzioni R per visualizzare la distribuzione dei valori nella colonna *creditLine* in base al sesso.

> [!div class="checklist"]
> * Creare variabili min-max per gli input dell'istogramma
> * Visualizzare i dati in un istogramma usando la funzione **rxHistogram** di **RevoScaleR**
> * Visualizzare i dati con i tracciati a dispersione usando la funzione **levelplot** del pacchetto **lattice** incluso nella distribuzione di R

Come dimostra questa esercitazione, è possibile combinare funzioni open source e specifiche di Microsoft nello stesso script.

## <a name="add-maximum-and-minimum-values"></a>Aggiungere valori minimi e massimi

Le statistiche di riepilogo calcolate nell'esercitazione precedente hanno restituito informazioni utili sui dati che è possibile inserire nell'origine dati per ulteriori calcoli. Ad esempio, i valori minimo e massimo possono essere usati per calcolare istogrammi. In questo esercizio, aggiungere i valori minimo e massimo all'origine dati **RxSqlServerData**.

1. Per iniziare si configurano alcune variabili temporanee.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Usare la variabile *ccColInfo* creata nell'esercitazione precedente per definire le colonne nell'origine dati.
  
   Aggiungere nuove colonne calcolate (*numTrans*, *numIntlTrans*e *creditLine*) alla raccolta di colonne per eseguire l'override della definizione originale. Lo script seguente aggiunge fattori basati sui valori minimo e massimo, ottenuti da sumOut, che archivia l'output in memoria di **rxSummary**. 
  
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
  
3. Dopo aver aggiornato la raccolta di colonne, applicare l'istruzione seguente per creare una versione aggiornata dell'origine dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definita in precedenza.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    L'origine dati sqlFraudDS include ora le nuove colonne aggiunte mediante *ccColInfo*.
  
A questo punto, le modifiche interessano solo l'oggetto origine dati in R, mentre nella tabella di database non sono stati ancora scritti nuovi dati. È tuttavia possibile usare i dati acquisiti nella variabile sumOut per creare visualizzazioni e riepiloghi. 

> [!TIP]
> Se non si ricorda quale contesto di calcolo si sta usando, eseguire **rxGetComputeContext()** . Il valore restituito "RxLocalSeq Compute Context" indica che si sta usando il contesto di calcolo locale.

## <a name="visualize-data-using-rxhistogram"></a>Visualizzare i dati tramite rxHistogram

1. Usare il codice di R seguente per chiamare la funzione [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) e per passare una formula e l'origine dati. È possibile innanzitutto eseguire questa procedura localmente per visualizzare i risultati previsti e il tempo necessario.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    Internamente, **rxHistogram** chiama la funzione [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) inclusa nel pacchetto **RevoScaleR** . **rxCube** restituisce un singolo elenco, o frame di dati, contenente una colonna per ogni variabile specificata nella formula, oltre a una colonna di conteggi.
    
2. A questo punto, impostare il contesto di calcolo per il computer SQL Server remoto ed eseguire di nuovo **rxHistogram**.
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. I risultati sono esattamente gli stessi perché si sta usando la stessa origine dati, ma nel secondo passaggio i calcoli vengono eseguiti sul server remoto. I risultati vengono poi restituiti alla workstation locale per eseguire il tracciato.
   
  ![Risultati dell'istogramma](media/rsql-sue-histogramresults.jpg "Risultati dell'istogramma")


## <a name="visualize-with-scatter-plots"></a>Visualizzare i dati con tracciati a dispersione

I tracciati a dispersione vengono spesso usati durante l'esplorazione dei dati per confrontare la relazione tra due variabili. A questo scopo è possibile usare i pacchetti R predefiniti, con gli input forniti dalle funzioni **RevoScaleR**.

1. Chiamare la funzione [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) per calcolare la media di *fraudRisk* per ogni combinazione di *numTrans* e *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Per specificare i gruppi usati per il calcolo delle medie, usare la notazione `F()` . In questo esempio, `F(numTrans):F(numIntlTrans)` indica che i numeri interi nelle variabili `numTrans` e `numIntlTrans` devono essere considerati come variabili di categoria, con un livello per ogni valore intero.
  
    Il valore restituito predefinito di **rxCube** è un *oggetto rxCube*che rappresenta una tabulazione incrociata. 
  
2. Chiamare la funzione [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) per convertire i risultati in un frame di dati che può essere facilmente usato in una delle funzioni di tracciato standard di R.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    La funzione **rxCube** include l'argomento facoltativo *returnDataFrame* = **TRUE**, che può essere usato per convertire direttamente i risultati in un frame di dati. Ad esempio:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    L'output di **rxResultsDF** è comunque più chiaro e mantiene i nomi delle colonne di origine. È possibile eseguire la funzione `head(cube1)` seguita da `head(cubePlot)` per confrontare l'output.
  
3. Creare una mappa termica usando la funzione **levelplot** del pacchetto **lattice** incluso in tutte le distribuzioni di R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Risultati**
  
    ![Risultati del tracciato a dispersione](media/rsql-sue-scatterplotresults.jpg "Risultati del tracciato a dispersione")
  
Da questa analisi veloce è possibile notare che il rischio di frode aumenta sia con il numero di transazioni che con il numero di transazioni internazionali.

Per altre informazioni sulla funzione **rxCube** e sulle funzioni a campi incrociati in generale, vedere [Come riepilogare i dati tramite RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Creare modelli R usando dati di SQL Server](../../machine-learning/tutorials/deepdive-create-models.md)