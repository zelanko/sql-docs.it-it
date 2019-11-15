---
title: Spostare dati con il file XDF
description: Esercitazione dettagliata su come spostare dati usando XDF e il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6935276a47061652647666184637af8ba1535edd
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727204"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>Spostare i dati tra SQL Server e il file XDF (esercitazione su SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa lezione fa parte dell'[esercitazione di RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) relativa all'uso delle [funzioni di RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questo passaggio si apprenderà come usare un file XDF per spostare i dati tra contesti di calcolo locali e remoti. L'archiviazione dei dati in un file XDF consente di eseguire trasformazioni sui dati.

Al termine, i dati saranno usati nel file per creare una nuova tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La funzione [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) può applicare le trasformazioni ai dati ed esegue la conversione tra i frame di dati e i file XDF.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Creare una tabella di SQL Server da un file XDF

Per questo esercizio si useranno di nuovo i dati relativi alle frodi con carta di credito. In questo scenario è stato richiesto di eseguire alcune analisi aggiuntive sugli utenti in California, Oregon e Washington. Per maggiore efficienza, si è deciso di archiviare i dati di questi soli tre paesi nel computer locale e di lavorare solo con le variabili sesso, titolare carta, paese e saldo.

1. Usare di nuovo la variabile `stateAbb` creata in precedenza per identificare i livelli da includere e scriverli in una nuova variabile, `statesToKeep`.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Risultati**
    
    CA|o|WA
    ----|----|----
    5|38|48
    
2. Definire i dati che si vogliono spostare da SQL Server usando una query [!INCLUDE[tsql](../../includes/tsql-md.md)] .  Questa variabile sarà poi usata come argomento *inData* per **rxImport**.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Assicurarsi che la query non contenga caratteri nascosti, ad esempio avanzamenti riga e tabulazioni.
  
3. Definire poi le colonne da usare con i dati in R. Ad esempio, nel set di dati più piccolo sono necessari solo tre livelli di fattore, poiché la query restituisce i dati solo per tre paesi.  Applicare la variabile `statesToKeep` per identificare i livelli appropriati da includere.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. Impostare il contesto di calcolo su **locale**, dal momento che devono essere considerati tutti i dati disponibili nel computer locale.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    La funzione [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) consente di importare dati da qualsiasi origine dati supportata in un file XDF locale. È utile usare una copia locale dei dati se si vogliono eseguire molte analisi diverse sui dati, ma senza continuare a ripetere la stessa query.

5. Creare l'oggetto origine dati passando le variabili definite in precedenza come argomenti a **RxSqlServerData**.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. Chiamare **rxImport** per scrivere i dati in un file denominato `ccFraudSub.xdf` nella directory di lavoro corrente.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    L'oggetto `localDs` restituito dalla funzione **rxImport** è un oggetto origine dati **RxXdfData** disattivo che rappresenta il file di dati `ccFraud.xdf` archiviato localmente sul disco.
  
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

8. È ora possibile chiamare varie funzioni R per analizzare l'oggetto **localDs**, come si è soliti fare con i dati di origine in SQL Server. Ad esempio, si potrebbero riepilogare i dati in base al sesso:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>Passaggi successivi

Questa lezione conclude la serie di esercitazioni in più parti su **RevoScaleR** e SQL Server. Sono stati presentati numerosi concetti correlati ai dati e alle operazioni di calcolo, che costituiscono una base per proseguire con i propri dati e requisiti di progetti.

Per approfondire la conoscenza di **RevoScaleR**, è possibile tornare all'elenco delle esercitazioni su R ed eseguire gli eventuali esercizi non ancora eseguiti. In alternativa, rivedere gli articoli di procedure nel sommario per informazioni sulle attività generali.

> [!div class="nextstepaction"]
> [Esercitazioni di R per SQL Server](sql-server-r-tutorials.md)