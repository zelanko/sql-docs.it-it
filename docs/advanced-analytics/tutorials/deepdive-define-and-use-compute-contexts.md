---
title: Definire e usare i contesti di calcolo di RevoScaleR - SQL Server Machine Learning
description: Procedura dettagliata su come definire un contesto di calcolo usando il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c0ae593264abad52873cfc152da721b6c0867109
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645084"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>Definire e usare i contesti di calcolo (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Nella lezione precedente, usato **RevoScaleR** funzioni per controllare gli oggetti dati. Questa lezione viene presentato il [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) funzione, che consente di definire un contesto di calcolo per un Server SQL remoto. Con un contesto di calcolo remoto, è possibile spostare l'esecuzione di R da una sessione locale a una sessione remota nel server. 

> [!div class="checklist"]
> * Informazioni di che contesto di calcolo gli elementi di un Server SQL remoto
> * Abilitare la traccia in un oggetto di contesto di calcolo

**RevoScaleR** supporta più contesti di calcolo: Hadoop, Spark in HDFS e SQL Server nel database. Per SQL Server, il **RxInSqlServer** funzione viene utilizzata per le connessioni al server e il passaggio di oggetti tra il computer locale e il contesto di esecuzione remoto.

## <a name="create-and-set-a-compute-context"></a>Creare e impostare un contesto di calcolo

Il **RxInSqlServer** funzione che crea il contesto di calcolo di SQL Server utilizza le informazioni seguenti:

+ Stringa di connessione per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza
+ Specifica della modalità di gestione dell'output
+ Specifica facoltativa di una directory di dati condiviso
+ Argomenti facoltativi, abilitare la traccia o specificano il livello di traccia

In questa sezione illustra ogni parte.

1. Specificare la stringa di connessione per l'istanza in cui vengono eseguiti i calcoli. È possibile riutilizzare la stringa di connessione creata in precedenza.

    **Uso di un account di accesso SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **Uso dell'autenticazione di Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. Specificare il modo in cui si vuole gestire l'output. Lo script seguente indirizza la sessione R locale attendere i risultati del processo R nel server prima di elaborare l'operazione successiva. Elimina anche l'output dei calcoli remoti vengano visualizzati nella sessione locale.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    L'argomento *wait* per **RxInSqlServer** supporta queste opzioni:
  
    -   **TRUE**. Il processo è configurato come il blocco e non restituisce fino a quando non viene completato o non è riuscita.  Per altre informazioni, vedere [applicazione distribuita e l'elaborazione parallela in Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. I processi sono configurati come non di blocco e restituiranno immediatamente risultati, consentendo di continuare a eseguire altro codice R. Tuttavia, anche in modalità non di blocco, la connessione client con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere mantenuta durante l'esecuzione del processo.

3. Facoltativamente, specificare il percorso di una directory locale per l'uso condiviso dalla sessione R locale e remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computer e i relativi account.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   Se si vuole creare manualmente una directory specifica per la condivisione, è possibile aggiungere una riga simile alla seguente:

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. Passare gli argomenti per il **RxInSqlServer** costruttore per creare il *oggetto contesto di calcolo*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    La sintassi per **RxInSqlServer** quasi identica a quella delle **RxSqlServerData** funzione usato in precedenza per definire l'origine dati. Esistono tuttavia alcune differenze importanti.
      
    - L'oggetto origine dati definito usando la funzione [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)specifica la posizione in cui vengono archiviati i dati.
    
    - Al contrario, il contesto di calcolo definito usando la funzione [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) indica dove aggregazioni e altri calcoli devono aver luogo.
    
    La definizione di un contesto di calcolo non influenza gli altri calcoli generici di R che possono essere eseguiti nella workstation e non modifica l'origine dei dati. Ad esempio, è possibile definire un file di testo locale come origine dati ma modificare il contesto di calcolo in SQL Server ed effettuare tutte le letture e i riepiloghi nei dati nel computer SQL Server.

5. Attivare il contesto di calcolo remoto.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. Restituiscono informazioni sul contesto di calcolo, tra cui le relative proprietà.

    ```R
    rxGetComputeContext()
    ```

7. Ripristinare il contesto di calcolo al computer locale, specificando la parola chiave "local" (lezione successiva viene illustrato come utilizzare il contesto di calcolo remoto).

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> Per l'elenco delle parole chiave supportate da questa funzione digitare `help("rxSetComputeContext")` da una riga di comando di R.

## <a name="enable-tracing"></a>Abilitare la traccia

A volte le operazioni vengono eseguite correttamente nel contesto locale ma si verificano problemi quando vengono eseguite in un contesto di calcolo remoto. Se si desidera analizzare i problemi o monitorare le prestazioni, è possibile abilitare la traccia nel contesto di calcolo, per supportare la risoluzione dei problemi in fase di esecuzione.

1. Creare un nuovo contesto di calcolo che usa la stessa stringa di connessione, ma aggiungere gli argomenti *traceEnabled* e *traceLevel* per il **RxInSqlServer** costruttore.

    ```R
    sqlComputeTrace <- RxInSqlServer(
        connectionString = sqlConnString,
        #shareDir = sqlShareDir,
        wait = sqlWait,
        consoleOutput = sqlConsoleOutput,
        traceEnabled = TRUE,
        traceLevel = 7)
    ```
  
   Nell'esempio la proprietà *traceLevel* è impostata su 7, ovvero sulla visualizzazione di tutte le informazioni di traccia.

2. Usare la [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) funzione per specificare il contesto di calcolo di abilitazione della traccia in base al nome.

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come cambiare contesti di calcolo per eseguire codice R nel server o in locale.

> [!div class="nextstepaction"]
> [Calcolare le statistiche di riepilogo in locale e remota i contesti di calcolo](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)