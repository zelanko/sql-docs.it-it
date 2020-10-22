---
title: Usare i contesti di calcolo di RevoScaleR
description: Informazioni sulla funzione RxInSqlServer che consente di definire un contesto di calcolo per un computer SQL Server remoto.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7bf4385405c227fb337dda910c3f1ef158eff223
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195143"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>Definire e usare i contesti di calcolo (esercitazione su SQL Server e RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Questa è l'esercitazione 4 della [serie di esercitazioni per RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) dedicate all'uso delle [funzioni di RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Nell'esercitazione precedente sono state usate le funzioni di **RevoScaleR** per esaminare gli oggetti dati. In questa esercitazione viene presentata la funzione [RxInSqlServer](/machine-learning-server/r-reference/revoscaler/rxinsqlserver), che consente di definire un contesto di calcolo per un computer SQL Server remoto. Con un contesto di calcolo remoto è possibile spostare l'esecuzione di R da una sessione locale a una sessione remota sul server. 

> [!div class="checklist"]
> * Apprendere gli elementi di un contesto di calcolo di SQL Server remoto
> * Abilitare la traccia in un oggetto contesto di calcolo

**RevoScaleR** supporta più contesti di calcolo: Hadoop, Spark su HDFS e SQL Server in-database. Per SQL Server, la funzione **RxInSqlServer** viene usata per le connessioni al server e il passaggio di oggetti tra il computer locale e il contesto di esecuzione remota.

## <a name="create-and-set-a-compute-context"></a>Creare e impostare un contesto di calcolo

La funzione **RxInSqlServer** che crea il contesto di calcolo di SQL Server usa le informazioni seguenti:

+ Stringa di connessione per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
+ Specifica della modalità di gestione dell'output
+ Specifica facoltativa di una directory di dati condivisa
+ Argomenti facoltativi che abilitano la traccia o specificano il livello di traccia

Questa sezione illustra nel dettaglio ogni parte.

1. Specificare la stringa di connessione per l'istanza in cui vengono eseguiti i calcoli. È possibile riutilizzare la stringa di connessione creata in precedenza.

    **Uso di un account di accesso SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **Uso dell'autenticazione di Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. Specificare il modo in cui si vuole gestire l'output. Lo script seguente indica alla sessione di R locale di attendere i risultati del processo R nel server prima di elaborare l'operazione successiva. Evita anche che l'output dei calcoli remoti venga visualizzato nella sessione locale.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    L'argomento *wait* per **RxInSqlServer** supporta queste opzioni:
  
    -   **TRUE**. Il processo è configurato in modalità di blocco e non restituisce risultati finché non viene completato o non ha esito negativo.  Per altre informazioni, vedere [Elaborazione parallela e distribuita in Machine Learning Server](/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. I processi sono configurati in modalità non di blocco e restituiscono immediatamente risultati, consentendo di continuare a eseguire altro codice R. Tuttavia, anche in modalità non di blocco, la connessione client con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere mantenuta durante l'esecuzione del processo.

3. Se si vuole, specificare il percorso di una directory locale per l'uso condiviso da parte della sessione R locale e del computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remoto e dei relativi account.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   Se si vuole creare manualmente una directory specifica per la condivisione, è possibile aggiungere una riga simile alla seguente:

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. Passare argomenti al costruttore **RxInSqlServer** per creare l'*oggetto contesto di calcolo*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    La sintassi per **RxInSqlServer** è quasi identica a quella della funzione **RxSqlServerData** usata in precedenza per definire l'origine dati. Esistono tuttavia alcune differenze importanti.
      
    - L'oggetto origine dati definito usando la funzione [RxSqlServerData](/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)specifica la posizione in cui vengono archiviati i dati.
    
    - Il contesto di calcolo definito usando la funzione [RxInSqlServer](/machine-learning-server/r-reference/revoscaler/rxinsqlserver) indica invece la posizione in cui eseguire le aggregazioni e altri calcoli.
    
    La definizione di un contesto di calcolo non influenza gli altri calcoli generici di R che possono essere eseguiti nella workstation e non modifica l'origine dei dati. Ad esempio, è possibile definire un file di testo locale come origine dati ma modificare il contesto di calcolo in SQL Server ed effettuare tutte le letture e i riepiloghi nei dati nel computer SQL Server.

5. Attivare il contesto di calcolo remoto.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. Restituire informazioni sul contesto di calcolo, incluse le relative proprietà.

    ```R
    rxGetComputeContext()
    ```

7. Reimpostare il contesto di calcolo sul computer locale specificando la parola chiave "local" (l'esercitazione successiva illustra l'uso del contesto di calcolo remoto).

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> Per l'elenco delle parole chiave supportate da questa funzione digitare `help("rxSetComputeContext")` da una riga di comando di R.

## <a name="enable-tracing"></a>Abilitare la traccia

A volte le operazioni vengono eseguite correttamente nel contesto locale ma si verificano problemi quando vengono eseguite in un contesto di calcolo remoto. Per analizzare i problemi o monitorare le prestazioni, è possibile abilitare la traccia nel contesto di calcolo per supportare la risoluzione dei problemi in fase di esecuzione.

1. Creare un nuovo contesto di calcolo che usa la stessa stringa di connessione, ma aggiungere gli argomenti *traceEnabled* e *traceLevel* al costruttore **RxInSqlServer**.

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

2. Usare la funzione [rxSetComputeContext](/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) per specificare il contesto di calcolo abilitato per la traccia per nome.

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come cambiare contesto di calcolo per eseguire il codice R sul server o in locale.

> [!div class="nextstepaction"]
> [Calcolare statistiche di riepilogo in contesti di calcolo locali e remoti](../../machine-learning/tutorials/deepdive-create-and-run-r-scripts.md)