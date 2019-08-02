---
title: Visualizzare i dati SQL Server usando RevoScaleR rxHistogram
description: Esercitazione dettagliata su come visualizzare i dati usando il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8c7e837f9ed4392a8ecfc9e7c237b95f3fdde3d3
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714855"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>Visualizzare i dati SQL Server usando R (esercitazione SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa lezione fa parte dell' [esercitazione su RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare le [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa lezione, usare le funzioni R per visualizzare la distribuzione dei valori nella colonna *creditLine* per sesso.

> [!div class="checklist"]
> * Creare variabili min-max per gli input dell'istogramma
> * Visualizzare i dati in un istogramma usando **rxHistogram** da **RevoScaleR**
> * Visualizza i grafici a dispersione usando **levelplot** da **reticolo** incluso nella distribuzione R di base

Come illustrato in questa lezione, è possibile combinare funzioni open source e specifiche di Microsoft nello stesso script.

## <a name="add-maximum-and-minimum-values"></a>Aggiungi valori massimi e minimi

In base alle statistiche di riepilogo calcolate della lezione precedente, sono state individuate alcune utili informazioni sui dati che è possibile inserire nell'origine dati per ulteriori calcoli. Ad esempio, i valori minimo e massimo possono essere usati per calcolare gli istogrammi. In questo esercizio aggiungere i valori massimo e minimo all'origine dati **RxSqlServerData** .

1. Per iniziare si configurano alcune variabili temporanee.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Utilizzare la variabile *ccColInfo* creata nella lezione precedente per definire le colonne nell'origine dati.
  
   Aggiungere nuove colonne calcolate (*numTrans*, *numIntlTrans*e *creditLine*) alla raccolta di colonne che sostituiscono la definizione originale. Lo script seguente aggiunge fattori basati sui valori minimo e massimo, ottenuti da sumOut, che archivia l'output in memoria da **rxSummary**. 
  
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
  
3. Dopo aver aggiornato la raccolta di colonne, applicare l'istruzione seguente per creare una versione aggiornata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dell'origine dati definita in precedenza.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    L'origine dati sqlFraudDS include ora le nuove colonne aggiunte mediante *ccColInfo*.
  
A questo punto, le modifiche interessano solo l'oggetto origine dati in R. non sono ancora stati scritti nuovi dati nella tabella di database. Tuttavia, è possibile usare i dati acquisiti nella variabile sumOut per creare visualizzazioni e riepiloghi. 

> [!TIP]
> Se si dimentica il contesto di calcolo in uso, eseguire **rxGetComputeContext ()** . Un valore restituito di "contesto di calcolo RxLocalSeq" indica che il contesto di calcolo locale è in esecuzione.

## <a name="visualize-data-using-rxhistogram"></a>Visualizzare i dati con rxHistogram

1. Usare il codice di R seguente per chiamare la funzione [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) e per passare una formula e l'origine dati. È possibile innanzitutto eseguire questa procedura localmente per visualizzare i risultati previsti e il tempo necessario.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    Internamente, **rxHistogram** chiama la funzione [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) inclusa nel pacchetto **RevoScaleR** . **rxCube** restituisce un singolo elenco (o frame di dati) contenente una colonna per ogni variabile specificata nella formula, oltre a una colonna counts.
    
2. A questo punto, impostare il contesto di calcolo sul computer SQL Server remoto ed eseguire di nuovo **rxHistogram** .
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. I risultati sono identici perché si sta utilizzando la stessa origine dati, ma nel secondo passaggio i calcoli vengono eseguiti nel server remoto. I risultati vengono poi restituiti alla workstation locale per eseguire il tracciato.
   
  ![risultati istogramma](media/rsql-sue-histogramresults.jpg "risultati istogramma")


## <a name="visualize-with-scatter-plots"></a>Visualizza con grafici a dispersione

I grafici a dispersione vengono spesso usati durante l'esplorazione dei dati per confrontare la relazione tra due variabili. A questo scopo, è possibile usare i pacchetti R incorporati, con gli input forniti dalle funzioni **RevoScaleR** .

1. Chiamare la funzione [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) per calcolare la media di *fraudRisk* per ogni combinazione di *numTrans* e *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Per specificare i gruppi usati per il calcolo delle medie, usare la notazione `F()` . In questo esempio, `F(numTrans):F(numIntlTrans)` indica che i numeri interi nelle variabili `numTrans` e `numIntlTrans` devono essere considerati come variabili categoriche, con un livello per ogni valore intero.
  
    Il valore restituito predefinito di **rxCube** è un *oggetto rxCube*, che rappresenta una tabulazione incrociata. 
  
2. Chiamare la funzione [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) per convertire i risultati in un frame di dati che può essere facilmente usato in una delle funzioni di tracciato standard di R.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    La funzione **rxCube** include un argomento facoltativo, *returnDataFrame* = **true**, che è possibile usare per convertire direttamente i risultati in un frame di dati. Ad esempio:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    Tuttavia, l'output di **rxResultsDF** è più pulito e conserva i nomi delle colonne di origine. È possibile eseguire `head(cube1)` seguito da `head(cubePlot)` per confrontare l'output.
  
3. Creare una mappa termica usando la funzione **levelplot** dal pacchetto **lattice** , incluso in tutte le distribuzioni R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Risultati**
  
    ![risultati grafico a dispersione](media/rsql-sue-scatterplotresults.jpg "risultati grafico a dispersione")
  
Da questa analisi rapida è possibile notare che il rischio di frode aumenta con il numero di transazioni e il numero di transazioni internazionali.

Per altre informazioni sulla funzione **rxCube** e sui campi incrociati in generale, vedere riepiloghi [dei dati con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Creare modelli R usando i dati SQL Server](../../advanced-analytics/tutorials/deepdive-create-models.md)