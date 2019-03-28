---
title: 'Eseguire query e modificare i dati di SQL Server con RevoScaleR: SQL Server Machine Learning'
description: Procedura dettagliata su come eseguire query e modificare i dati con il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6d2768399ecd3d504e5bc51d4c7cbd151488782a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513138"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>Eseguire query e modificare i dati di SQL Server (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Nella lezione precedente, sono stati caricati i dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In questo passaggio, è possibile esplorare e modificare i dati tramite **RevoScaleR**:

> [!div class="checklist"]
> * Restituisce le informazioni di base sulle variabili
> * Creare dati categorici da dati non elaborati

Dati categorici, oppure *variabili di fattore*, sono utili per le visualizzazioni di analisi esplorativa dei dati. È possibile utilizzare tali come input per gli istogrammi per avere un'idea dell'aspetto quali dati della variabile.

## <a name="query-for-columns-and-types"></a>Query per le colonne e tipi

Usare un IDE R / RGui.exe per eseguire script R. 

Per prima cosa ottenere un elenco delle colonne e dei relativi tipi di dati. È possibile usare la funzione [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) e specificare l'origine dati da analizzare. A seconda della versione di **RevoScaleR**, è anche possibile usare [rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames). 
  
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

## <a name="create-categorical-data"></a>Creare dati categorici

Tutte le variabili vengono archiviate come numeri interi, ma alcune variabili rappresentano dati categorici, chiamati *variabili di fattore* in R. Ad esempio, la colonna *stato* contiene numeri utilizzati come identificatori per i 50 stati più District of Columbia. Per facilitare la comprensione dei dati, sostituire i numeri con un elenco di codici di stato.

In questo passaggio si crea un vettore di stringhe contenente le abbreviazioni e quindi eseguire il mapping di valori relativi alle categorie agli identificatori interi originali. Usare la nuova variabile nel *colInfo* argomento, per specificare che la colonna gestita come fattore. Ogni volta che si analizzano i dati o spostarlo, vengono usate le abbreviazioni e la colonna viene gestita come fattore.

Il mapping della colonna alle abbreviazioni prima di usarla come fattore consente di migliorare anche le prestazioni. Per altre informazioni, vedere [ottimizzazione R e i dati](../r/r-and-data-optimization-r-services.md).

1. Creare una variabile R, innanzitutto *stateAbb*e definire il vettore di stringhe da aggiungere ad esso, come indicato di seguito.
  
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
  
3. Per creare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origine dati che utilizza i dati aggiornati, chiamare il **RxSqlServerData** funzionare come in precedenza, ma aggiungere il *colInfo* argomento.
  
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