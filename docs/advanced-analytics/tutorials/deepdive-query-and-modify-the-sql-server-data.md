---
title: Eseguire query e modificare i dati SQL Server usando RevoScaleR
description: Esercitazione dettagliata su come eseguire una query e modificare i dati usando il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3fb28d287c7b92e9b399aa7bc0bb606c618eed47
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469795"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>Eseguire query e modificare i dati di SQL Server (esercitazione SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa lezione fa parte dell' [esercitazione su RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare le [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Nella lezione precedente i dati sono stati caricati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In questo passaggio è possibile esplorare e modificare i dati usando **RevoScaleR**:

> [!div class="checklist"]
> * Restituisce informazioni di base sulle variabili
> * Creazione di dati categorici da dati non elaborati

I dati categorici o le *variabili di fattore*sono utili per le visualizzazioni dei dati esplorativi. È possibile usarli come input per gli istogrammi per ottenere un'idea di quali dati variabili sono simili.

## <a name="query-for-columns-and-types"></a>Eseguire una query per le colonne e i tipi

Usare un IDE R o RGui. exe per eseguire lo script R. 

Per prima cosa ottenere un elenco delle colonne e dei relativi tipi di dati. È possibile utilizzare la funzione [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) e specificare l'origine dati che si desidera analizzare. A seconda della versione di **RevoScaleR**, è anche possibile usare [rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames). 
  
```R
rxGetVarInfo(data = sqlFraudDS)
```

**Risultati**

```R
Var 1: custID, Type: integer
Var 2: gender, Type: integer
Var 3: state, Type: integer
Var 4: cardholder, Type: integer
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: fraudRisk, Type: integer
```

## <a name="create-categorical-data"></a>Creazione di dati categorici

Tutte le variabili vengono archiviate come numeri interi, ma alcune variabili rappresentano dati categorici, denominate *variabili di fattore* in R. Ad esempio, lo *stato* della colonna contiene numeri usati come identificatori per gli stati 50 e il distretto di Columbia. Per facilitare la comprensione dei dati, sostituire i numeri con un elenco di codici di stato.

In questo passaggio viene creato un vettore di stringa contenente le abbreviazioni, quindi viene mappato questi valori categorici agli identificatori di tipo Integer originali. Si usa quindi la nuova variabile nell'argomento *colInfo* per specificare che la colonna deve essere gestita come fattore. Ogni volta che si analizzano i dati o lo si sposta, vengono utilizzate le abbreviazioni e la colonna viene gestita come fattore.

Il mapping della colonna alle abbreviazioni prima di usarla come fattore consente di migliorare anche le prestazioni. Per altre informazioni, vedere [R e ottimizzazione dei dati](../r/r-and-data-optimization-r-services.md).

1. Per iniziare, creare una variabile R, *stateAbb*, e definire il vettore di stringhe da aggiungere, come indicato di seguito.
  
    ```R
    stateAbb <- c("AK", "AL", "AR", "AZ", "CA", "CO", "CT", "DC",
        "DE", "FL", "GA", "HI","IA", "ID", "IL", "IN", "KS", "KY", "LA",
        "MA", "MD", "ME", "MI", "MN", "MO", "MS", "MT", "NB", "NC", "ND",
        "NH", "NJ", "NM", "NV", "NY", "OH", "OK", "OR", "PA", "RI","SC",
        "SD", "TN", "TX", "UT", "VA", "VT", "WA", "WI", "WV", "WY")
    ```

2. Quindi, creare un oggetto informazioni di colonna denominato *ccColInfo*che specifichi il mapping dei valori interi esistenti ai livelli di categoria, ovvero le abbreviazioni per gli stati.
  
    Questa istruzione crea anche le variabili di fattore per gender e cardholder.
  
    ```R
    ccColInfo <- list(
    gender = list(
              type = "factor",
              levels = c("1", "2"),
              newLevels = c("Male", "Female")
              ),
    cardholder = list(
                  type = "factor",
                  levels = c("1", "2"),
                  newLevels = c("Principal", "Secondary")
                   ),
    state = list(
             type = "factor",
             levels = as.character(1:51),
             newLevels = stateAbb
             ),
    balance = list(type = "numeric")
    )
    ```
  
3. Per creare l' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origine dati che usa i dati aggiornati, chiamare la funzione **RxSqlServerData** come in precedenza, ma aggiungere l'argomento *colInfo* .
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
    table = sqlFraudTable, colInfo = ccColInfo,
    rowsPerRead = sqlRowsPerRead)
    ```
  
    - Per il parametro *table* , passare la variabile *sqlFraudTable*che contiene l'origine dati creata in precedenza.
    - Per il parametro *colInfo* , passare la variabile *ccColInfo* che contiene i tipi di dati di colonna e i livelli di fattore.

4.  È ora possibile usare la funzione **rxGetVarInfo** per visualizzare le variabili nella nuova origine dati.
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **Risultati**
    
    ```R
    Var 1: custID, Type: integer
    Var 2: gender  2 factor levels: Male Female
    Var 3: state   51 factor levels: AK AL AR AZ CA ... VT WA WI WV WY
    Var 4: cardholder  2 factor levels: Principal Secondary
    Var 5: balance, Type: integer
    Var 6: numTrans, Type: integer
    Var 7: numIntlTrans, Type: integer
    Var 8: creditLine, Type: integer
    Var 9: fraudRisk, Type: integer
    ```

A questo punto le tre variabili specificate (*gender*, *state*e *cardholder*) vengono trattate come fattori.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Definire e usare i contesti di calcolo](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)