---
title: Esercitazione sulla RevoScaleR di modelli R - creazione di SQL Server Machine Learning
description: Procedura dettagliata su come compilare un modello usando il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ae58ddf27628612200920899d914895d4fea3840
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513178"
---
# <a name="create-r-models-sql-server-and-revoscaler-tutorial"></a>Creare modelli R (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Ora che sono stati arricchiti i dati di training, è possibile analizzare i dati tramite modelli di regressione. I modelli lineari sono uno strumento importante nel mondo di analitica predittiva e il **RevoScaleR** pacchetto include gli algoritmi di regressione che possono suddividere il carico di lavoro ed eseguirlo in parallelo.

> [!div class="checklist"]
> * Creare un modello di regressione lineare
> * Creare un modello di regressione logistica

## <a name="create-a-linear-regression-model"></a>Creare un modello di regressione lineare

In questo passaggio, creare un semplice modello lineare che stima il saldo della carta di credito per i clienti usando come variabili indipendenti i valori di *gender* e *creditLine* colonne.
  
A questo scopo, usare il [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) funzione, che supporta contesti di calcolo remoti.
  
1. Creare una variabile R per archiviare completato modello e chiamare **rxLinMod**, passando una formula appropriata.
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. Per visualizzare un riepilogo dei risultati, chiamare R standard **riepilogo** funzione nell'oggetto modello.
  
     ```R
     summary(linModObj)
     ```

Si potrebbe trovare particolare che una funzione R semplice come **summary** funzioni in questo caso poiché nel passaggio precedente è stato impostato un contesto di calcolo del server. Tuttavia, anche quando la funzione **rxLinMod** usa il contesto di calcolo remoto per creare il modello, la funzione restituisce anche un oggetto contenente il modello alla workstation locale e lo archivia nella directory condivisa.

Di conseguenza, sarà possibile eseguire i comandi R standard sul modello come se fosse stato creato usando il contesto "locale".

**Risultati**

```R
Linear Regression Results for: balance ~ gender + creditLineData: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): balance
Total independent variables: 4 (Including number dropped: 1)
Number of valid observations: 10000
Number of missing observations: 0
Coefficients: (1 not defined because of singularities)

Estimate Std. Error t value Pr(>|t|) (Intercept)
3253.575 71.194 45.700 2.22e-16
gender=Male -88.813 78.360 -1.133 0.257
gender=Female Dropped Dropped Dropped Dropped
creditLine 95.379 3.862 24.694 2.22e-16
Signif. codes: 0  0.001  0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 3812 on 9997 degrees of freedom
Multiple R-squared: 0.05765
Adjusted R-squared: 0.05746
F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16
Condition number: 1.0184
```

## <a name="create-a-logistic-regression-model"></a>Creare un modello di regressione logistica

Successivamente, creare un modello di regressione logistica che indica se un determinato cliente rappresenta un rischio di frode. Si userà il **RevoScaleR** [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) funzione, che supporta l'adattamento di modelli di regressione logistica in remoto i contesti di calcolo.

Mantenere il contesto di calcolo già definito. Si continuerà anche a usare anche la stessa origine dati.

1. Chiamare la funzione **rxLogit** e passare la formula necessaria per definire il modello.

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS, dropFirst = TRUE)
    ```
  
    Poiché si tratta di un modello di grandi dimensioni contenente 60 variabili indipendenti, tra cui tre variabili fittizie che vengono eliminate, potrebbe essere necessario attendere che il contesto di calcolo restituisca l'oggetto.
    
    Il motivo per cui il modello è così grande è che in R e nel pacchetto **RevoScaleR** ogni livello di una variabile di fattore di categorie viene considerato automaticamente come variabile fittizia separata.
  
2. Per visualizzare un riepilogo del modello restituito, chiamare la funzione R **summary** .
  
    ```R
    summary(logitObj)
    ```
  
**Risultati parziali**

```R
Logistic Regression Results for: fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): fraudRisk
Total independent variables: 60 (Including number dropped: 3)
Number of valid observations: 10000 -2

LogLikelihood: 2032.8699 (Residual deviance on 9943 degrees of freedom)

Coefficients:
Estimate Std. Error z value Pr(>|z|)     (Intercept)
-8.627e+00  1.319e+00  -6.538 6.22e-11
state=AK                Dropped    Dropped Dropped  Dropped
state=AL             -1.043e+00  1.383e+00  -0.754   0.4511

(other states omitted)

gender=Male             Dropped    Dropped Dropped  Dropped
gender=Female         7.226e-01  1.217e-01   5.936 2.92e-09
cardholder=Principal    Dropped    Dropped Dropped  Dropped
cardholder=Secondary  5.635e-01  3.403e-01   1.656   0.0977
balance               3.962e-04  1.564e-05  25.335 2.22e-16
numTrans              4.950e-02  2.202e-03  22.477 2.22e-16
numIntlTrans          3.414e-02  5.318e-03   6.420 1.36e-10
creditLine            1.042e-01  4.705e-03  22.153 2.22e-16

Signif. codes:  0 '\*\*\*' 0.001 '\*\*' 0.01 '\*' 0.05 '.' 0.1 ' ' 1
Condition number of final variance-covariance matrix: 3997.308
Number of iterations: 15
```

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Valutare i nuovi dati](../../advanced-analytics/tutorials/deepdive-score-new-data.md)