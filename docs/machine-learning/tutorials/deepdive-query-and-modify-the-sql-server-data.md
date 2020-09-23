---
title: Modificare dati SQL con RevoScaleR
description: Informazioni su come modificare ed eseguire query sui dati usando il linguaggio R in SQL Server, in particolare la funzione RevoScaleR.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0120faa6d3989df7b7ae1c5da63c37423dead540
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178604"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>Modificare ed eseguire query sui dati di SQL Server (esercitazione su SQL Server e RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Questa è l'esercitazione 3 della [serie di esercitazioni per RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) dedicate all'uso delle [funzioni di RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Nell'esercitazione precedente sono stati caricati i dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In questa esercitazione è possibile esplorare e modificare i dati usando **RevoScaleR**:

> [!div class="checklist"]
> * Restituire informazioni di base sulle variabili
> * Creare dati categorici da dati non elaborati

I dati categorici, o *variabili di fattore*, sono particolarmente utili per le visualizzazioni esplorative dei dati. È possibile usarli come input di istogrammi per avere un'idea dell'aspetto dei dati variabili.

## <a name="query-for-columns-and-types"></a>Eseguire query per colonne e tipi

Usare un IDE R o RGui.exe per eseguire lo script R. 

Per prima cosa ottenere un elenco delle colonne e dei relativi tipi di dati. È possibile usare la funzione [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) e specificare l'origine dati da analizzare. A seconda della versione di **RevoScaleR**, è possibile usare anche [rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames). 
  
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

Tutte le variabili vengono archiviate come valori interi, ma alcune variabili rappresentano dati relativi alle categorie denominati *variabili di fattore* in R. Ad esempio, la colonna *stato* contiene numeri che rappresentano gli identificatori di 50 stati, più District of Columbia. Per facilitare la comprensione dei dati, sostituire i numeri con un elenco di codici di stato.

In questo passaggio si creerà un vettore di stringhe contenente le abbreviazioni e si eseguirà il mapping dei valori di categoria agli identificatori interi originali. Si userà quindi la nuova variabile nell'argomento *colInfo* per specificare che la colonna deve essere gestita come fattore. Ogni volta che si analizzano o si spostano i dati, vengono usate le abbreviazioni e la colonna viene gestita come fattore.

Il mapping della colonna alle abbreviazioni prima di usarla come fattore consente di migliorare anche le prestazioni. Per altre informazioni, vedere [R e ottimizzazione dei dati](../r/r-and-data-optimization-r-services.md).

1. Iniziare creando la variabile R *stateAbb* e definendo il vettore di stringhe da aggiungere alla variabile come segue.
  
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
  
3. Per creare l'origine dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che usa i dati aggiornati, chiamare la funzione **RxSqlServerData** come in precedenza, ma aggiungere l'argomento *colInfo*.
  
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
> [Definire e usare i contesti di calcolo](../../machine-learning/tutorials/deepdive-define-and-use-compute-contexts.md)