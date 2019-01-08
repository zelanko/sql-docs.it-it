---
title: 'Spostare dati tra SQL Server e file XDF con RevoScaleR: SQL Server Machine Learning'
description: Procedura dettagliata su come spostare i dati con formato XDF e il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d0f097c64d48a3a2e87f01965914b3100c8a28dc
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645210"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>Spostare dati tra SQL Server e file XDF (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questo passaggio viene illustrato come utilizzare un file XDF per trasferire dati tra contesti di calcolo remoti e locali. Archiviare i dati in un file XDF consente di eseguire trasformazioni sui dati.

Al termine, si usano i dati nel file per creare un nuovo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella. La funzione [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) può applicare trasformazioni ai dati ed esegue la conversione tra i frame di dati e file con estensione xdf.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Creare una tabella di SQL Server da un file XDF

Per questo esercizio, utilizzare nuovamente i dati sulle frodi carta di credito. In questo scenario è stato richiesto di eseguire alcune analisi aggiuntive sugli utenti in California, Oregon e Washington. Per una maggiore efficienza, si è deciso di archiviare i dati solo questi stati nel computer locale e usare solo le variabili sesso, titolari di carte, stato e saldo.

1. Usare di nuovo la `stateAbb` variabile creata in precedenza per identificare i livelli per includere e scriverli in una nuova variabile, `statesToKeep`.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Risultati**
    
    CA|o|WA
    ----|----|----
    5|38|48
    
2. Definire i dati di cui si vuole rilevare da SQL Server, usando un [!INCLUDE[tsql](../../includes/tsql-md.md)] query.  In un secondo momento si utilizza questa variabile come le *inData* argomento per **rxImport**.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Assicurarsi che la query non contenga caratteri nascosti, ad esempio avanzamenti riga e tabulazioni.
  
3. Successivamente, definire le colonne da utilizzare quando si lavora con i dati in R. Ad esempio, nel set di dati più piccoli, è necessario solo tre livelli di fattore, poiché la query restituisce i dati di soli tre stati.  Applicare il `statesToKeep` variabile per identificare i livelli appropriati da includere.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. Impostare il contesto di calcolo **locale**, perché si desidera che tutti i dati disponibili nel computer locale.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    Il [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) funzione possibile importare dati da qualsiasi origine dati supportata in un file XDF locale. Usando una copia locale dei dati è utile quando si desidera analisi diverse i dati, ma evitare di eseguire ripetutamente la stessa query.

5. Creare l'oggetto origine dati passando le variabili definite precedentemente come argomenti **RxSqlServerData**.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. Chiamare **rxImport** per scrivere i dati in un file denominato `ccFraudSub.xdf`, nella directory di lavoro corrente.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    Il `localDs` oggetto restituito dal **rxImport** funzione è un leggero **RxXdfData** oggetto origine dati che rappresenta il `ccFraud.xdf` archiviato localmente sul disco file di dati.
  
7. Chiamare [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) nel file XDF per verificare che lo schema dei dati sia lo stesso.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **Risultati**
    
    ```R
    rxGetVarInfo(data = localDS)
    Var 1: gender, Type: factor, no factor levels available
    Var 2: cardholder, Type: factor, no factor levels available
    Var 3: balance, Type: integer, Low/High: (0, 22463)
    Var 4: state, Type: factor, no factor levels available
    ```

8. È ora possibile chiamare varie funzioni R per analizzare le **localDs** dell'oggetto, esattamente come farebbe con i dati di origine in SQL Server. Ad esempio, è possibile creare un riepilogo per sesso:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>Passaggi successivi

In questa lezione si conclude la serie di esercitazioni multiparte nel **RevoScaleR** e SQL Server. Descrive numerosi concetti relativi ai dati e calcolo, ti offre una base per lo spostamento in avanti con i propri requisiti di dati e di progetto.

Per approfondire la conoscenza di **RevoScaleR**, è possibile tornare all'elenco di esercitazioni di R per scorrere tutti gli esercizi potrebbe aver ignorato. In alternativa, esaminare le procedure dettagliate nella tabella dei contenuti per informazioni sulle attività generali.

> [!div class="nextstepaction"]
> [Esercitazioni di R per SQL Server](sql-server-r-tutorials.md)