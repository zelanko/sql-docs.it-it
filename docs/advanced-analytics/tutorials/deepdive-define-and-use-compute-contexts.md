---
title: Definire e usare i contesti di calcolo RevoScaleR
description: Esercitazione dettagliata su come definire un contesto di calcolo usando il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 053fc48c4117372eb3e3bebb715b4176ec1dd828
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469723"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>Definire e usare i contesti di calcolo (esercitazione SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa lezione fa parte dell' [esercitazione su RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare le [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Nella lezione precedente sono state usate le funzioni **RevoScaleR** per esaminare gli oggetti dati. In questa lezione viene introdotta la funzione [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) , che consente di definire un contesto di calcolo per un SQL Server remoto. Con un contesto di calcolo remoto, è possibile spostare l'esecuzione di R da una sessione locale a una sessione remota sul server. 

> [!div class="checklist"]
> * Informazioni sugli elementi di un contesto di calcolo di SQL Server remoto
> * Abilitare la traccia in un oggetto del contesto di calcolo

**RevoScaleR** supporta più contesti di calcolo: Hadoop, Spark in HDFS e SQL Server nel database. Per SQL Server, la funzione **RxInSqlServer** viene utilizzata per le connessioni al server e il passaggio di oggetti tra il computer locale e il contesto di esecuzione remota.

## <a name="create-and-set-a-compute-context"></a>Creare e impostare un contesto di calcolo

La funzione **RxInSqlServer** che crea il contesto di calcolo SQL Server usa le informazioni seguenti:

+ Stringa di connessione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'istanza
+ Specifica del modo in cui deve essere gestito l'output
+ Specifica facoltativa di una directory di dati condivisa
+ Argomenti facoltativi che consentono di tracciare o specificare il livello di traccia

Questa sezione illustra ogni parte.

1. Specificare la stringa di connessione per l'istanza in cui vengono eseguiti i calcoli. È possibile riutilizzare la stringa di connessione creata in precedenza.

    **Uso di un account di accesso SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **Uso dell'autenticazione di Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. Specificare il modo in cui si vuole gestire l'output. Lo script seguente indirizza la sessione di R locale per attendere i risultati del processo R nel server prima di elaborare l'operazione successiva. Evita anche che l'output dei calcoli remoti venga visualizzato nella sessione locale.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    L'argomento *wait* per **RxInSqlServer** supporta queste opzioni:
  
    -   **TRUE**. Il processo è configurato come blocco e non restituisce alcun risultato finché non viene completato o non è riuscito.  Per ulteriori informazioni, vedere [Distributed and Parallel Computing in Machine Learning server](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. I processi sono configurati come non bloccanti e vengono restituiti immediatamente, consentendo di continuare a eseguire altro codice R. Tuttavia, anche in modalità non di blocco, la connessione client con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere mantenuta durante l'esecuzione del processo.

3. Facoltativamente, specificare il percorso di una directory locale per l'uso condiviso da parte della sessione di R locale e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del computer remoto e dei relativi account.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   Se si vuole creare manualmente una directory specifica per la condivisione, è possibile aggiungere una riga simile alla seguente:

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. Passare gli argomenti al costruttore **RxInSqlServer** per creare l' *oggetto contesto di calcolo*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    La sintassi di **RxInSqlServer** è quasi identica a quella della funzione **RxSqlServerData** usata in precedenza per definire l'origine dati. Esistono tuttavia alcune differenze importanti.
      
    - L'oggetto origine dati definito usando la funzione [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)specifica la posizione in cui vengono archiviati i dati.
    
    - Al contrario, il contesto di calcolo, definito usando la funzione [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) indica dove devono essere eseguiti aggregazioni e altri calcoli.
    
    La definizione di un contesto di calcolo non influenza gli altri calcoli generici di R che possono essere eseguiti nella workstation e non modifica l'origine dei dati. Ad esempio, è possibile definire un file di testo locale come origine dati ma modificare il contesto di calcolo in SQL Server ed effettuare tutte le letture e i riepiloghi nei dati nel computer SQL Server.

5. Attivare il contesto di calcolo remoto.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. Restituisce informazioni sul contesto di calcolo, incluse le relative proprietà.

    ```R
    rxGetComputeContext()
    ```

7. Reimpostare il contesto di calcolo sul computer locale specificando la parola chiave "local". la lezione successiva illustra l'uso del contesto di calcolo remoto.

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> Per l'elenco delle parole chiave supportate da questa funzione digitare `help("rxSetComputeContext")` da una riga di comando di R.

## <a name="enable-tracing"></a>Abilita traccia

A volte le operazioni vengono eseguite correttamente nel contesto locale ma si verificano problemi quando vengono eseguite in un contesto di calcolo remoto. Se si desidera analizzare i problemi o monitorare le prestazioni, è possibile abilitare la traccia nel contesto di calcolo per supportare la risoluzione dei problemi in fase di esecuzione.

1. Creare un nuovo contesto di calcolo che usa la stessa stringa di connessione, ma aggiungere gli argomenti *traceEnabled* e *TraceLevel* al costruttore **RxInSqlServer** .

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

2. Usare la funzione [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) per specificare il contesto di calcolo abilitato per la traccia in base al nome.

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come cambiare i contesti di calcolo per eseguire il codice R sul server o in locale.

> [!div class="nextstepaction"]
> [Calcolare le statistiche di riepilogo nei contesti di calcolo locali e remoti](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)