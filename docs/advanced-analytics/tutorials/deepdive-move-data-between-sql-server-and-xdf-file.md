---
title: Spostare i dati tra SQL Server e il file XDF usando RevoScaleR
description: Esercitazione dettagliata su come spostare i dati usando XDF e il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0e4c0fbdd9f625886a7d38fc80895e9f4407ce88
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344746"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>Spostare i dati tra SQL Server e il file XDF (esercitazione SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questa lezione fa parte dell' [esercitazione su RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare le [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questo passaggio viene illustrato come usare un file XDF per trasferire i dati tra contesti di calcolo locali e remoti. L'archiviazione dei dati in un file XDF consente di eseguire trasformazioni sui dati.

Al termine, usare i dati nel file per creare una nuova [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella. La funzione [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) può applicare le trasformazioni ai dati ed esegue la conversione tra i frame di dati e i file XDF.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Creare una tabella SQL Server da un file XDF

Per questo esercizio, si usano nuovamente i dati di frode della carta di credito. In questo scenario è stato richiesto di eseguire alcune analisi aggiuntive sugli utenti in California, Oregon e Washington. Per essere più efficienti, si è deciso di archiviare i dati solo per questi stati nel computer locale e si utilizzano solo le variabili Gender, titolari di carte, stato e saldo.

1. Usare nuovamente la `stateAbb` variabile creata in precedenza per identificare i livelli da includere e scriverli in una nuova variabile, `statesToKeep`.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Risultati**
    
    CA|Oppure|WA
    ----|----|----
    5|38|48
    
2. Definire i dati che si desidera riportare dalla SQL Server, utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)] una query.  In seguito si utilizzerà questa variabile  come argomento indata per **rxImport**.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Assicurarsi che la query non contenga caratteri nascosti, ad esempio avanzamenti riga e tabulazioni.
  
3. Definire quindi le colonne da usare quando si utilizzano i dati in R. Ad esempio, nel set di dati più piccolo sono necessari solo tre livelli di fattore, poiché la query restituisce i dati solo per tre stati.  Applicare la `statesToKeep` variabile per identificare i livelli corretti da includere.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. Impostare il contesto di calcolo su **local**, perché si desidera che tutti i dati siano disponibili nel computer locale.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    La funzione [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) può importare dati da qualsiasi origine dati supportata in un file XDF locale. L'uso di una copia locale dei dati è utile quando si desidera eseguire molte analisi diverse sui dati, ma si desidera evitare di eseguire la stessa query più volte.

5. Creare l'oggetto origine dati passando le variabili definite in precedenza come argomenti a **RxSqlServerData**.
  
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
  
    L' `localDs` oggetto restituito dalla funzione **rxImport** è un oggetto origine dati **RxXdfData** leggero che rappresenta il `ccFraud.xdf` file di dati archiviato localmente sul disco.
  
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

8. È ora possibile chiamare varie funzioni R per analizzare l'oggetto **localDs** , esattamente come si farebbe con i dati di origine in SQL Server. È possibile, ad esempio, riepilogare per genere:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>Passaggi successivi

Questa lezione conclude la serie di esercitazioni in più parti su **RevoScaleR** e SQL Server. Sono stati introdotti numerosi concetti correlati ai dati e di calcolo, che offrono una base per proseguire con i propri requisiti di dati e progetti.

Per approfondire la conoscenza di **RevoScaleR**, è possibile tornare all'elenco delle esercitazioni di R per esaminare tutti gli esercizi che potrebbero mancare. In alternativa, rivedere gli articoli sulle procedure del sommario per informazioni sulle attività generali.

> [!div class="nextstepaction"]
> [Esercitazioni di R per SQL Server](sql-server-r-tutorials.md)