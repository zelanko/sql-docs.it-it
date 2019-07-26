---
title: Eseguire funzioni R personalizzate su SQL Server usando RevoScaleR rxExec
description: Esercitazione dettagliata su come eseguire uno script R personalizzato in SQL Server usando le funzioni RevoScaleR.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: d90e2d4887154d3545884a77d0290e632f04a569
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470592"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec"></a>Eseguire funzioni R personalizzate su SQL Server usando rxExec
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

È possibile eseguire funzioni R personalizzate nel contesto di SQL Server passando la funzione tramite [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec), supponendo che tutte le librerie necessarie per lo script siano installate anche sul server e tali librerie siano compatibili con la distribuzione di base di R. 

La funzione **rxExec** in **RevoScaleR** fornisce un meccanismo per l'esecuzione di tutti gli script R necessari. Inoltre, **rxExec** è in grado di distribuire in modo esplicito il lavoro tra più core in un singolo server, aggiungendo la scalabilità agli script altrimenti limitati ai vincoli di risorse del motore R nativo.

In questa esercitazione si useranno i dati simulati per illustrare l'esecuzione di una funzione R personalizzata che viene eseguita in un server remoto.

## <a name="prerequisites"></a>Prerequisiti

+ [SQL Server 2017 Machine Learning Services (con r)](../install/sql-machine-learning-services-windows-install.md) o [SQL Server 2016 R Services (in-database)](../install/sql-r-services-windows-install.md)
  
+ [Autorizzazioni del database](../security/user-permission.md) e account di accesso utente del database SQL Server

+ [Una workstation di sviluppo con le librerie RevoScaleR](../r/set-up-a-data-science-client.md)

La distribuzione R nella workstation client fornisce uno strumento **Rgui** incorporato che è possibile usare per eseguire lo script r in questa esercitazione. È anche possibile usare un IDE, ad esempio RStudio o R Tools per Visual Studio.

## <a name="create-the-remote-compute-context"></a>Creare il contesto di calcolo remoto

Eseguire i seguenti comandi R in una workstation client. Se ad esempio si usa **Rgui**, avviarlo da questo percorso: C:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. Specificare la stringa di connessione per l'istanza di SQL Server in cui vengono eseguiti i calcoli. Il server deve essere configurato per l'integrazione con R. Il nome del database non viene usato in questo esercizio, ma la stringa di connessione ne richiede una. Se si dispone di un database di test o di esempio, è possibile utilizzarlo.

    **Uso di un account di accesso SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Uso dell'autenticazione di Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. Creare un contesto di calcolo remoto per l'istanza di SQL Server a cui si fa riferimento nella stringa di connessione.

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. Attivare il contesto di calcolo e quindi restituire la definizione dell'oggetto come passaggio di conferma. Verranno visualizzate le proprietà dell'oggetto contesto di calcolo.

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>Creare la funzione personalizzata

In questo esercizio verrà creata una funzione R personalizzata che simula un casinò comune costituito da un paio di dadi. Le regole del gioco determinano un risultato di vittoria o perdita:

+ Esegui il Rolling di 7 o 11 sul tuo Roll iniziale. Vinci.
+ Il rullo 2, 3 o 12 perde.
+ Eseguire il roll a 4, 5, 6, 8, 9 o 10, tale numero diventa il punto e si continua a eseguire il rollforward fino a quando non si esegue di nuovo il punto (in tal caso, si vince) o si esegue il roll 7, nel qual caso si perderà.

Il gioco può essere facilmente simulato in R creando una funzione personalizzata ed eseguendola più volte.

1.  Creare la funzione personalizzata usando il codice R seguente:
  
    ```R
    rollDice <- function()
    {
        result <- NULL
        point <- NULL
        count <- 1
            while (is.null(result))
            {
                roll <- sum(sample(6, 2, replace=TRUE))
  
                if (is.null(point))
                { point <- roll }
                if (count == 1 && (roll == 7 || roll == 11))
                {  result <- "Win" }
                else if (count == 1 && (roll == 2 || roll == 3 || roll == 12))
                { result <- "Loss" }
                else if (count > 1 && roll == 7 )
                { result <- "Loss" }
                else if (count > 1 && point == roll)
                { result <- "Win" }
                else { count <- count + 1 }
            }
            result
    }
    ```
  
2.  Simulare un singolo gioco di dadi eseguendo la funzione.
  
    ```R
    rollDice()
    ```
  
    Si ha vinto o si ha perso?
  
Ora che si dispone di uno script operativo, è possibile vedere come usare **rxExec** per eseguire la funzione più volte per creare una simulazione che consenta di determinare la probabilità di una vittoria.

## <a name="pass-rolldice-in-rxexec"></a>Passare rollDice () in rxExec

Per eseguire una funzione arbitraria nel contesto di un SQL Server remoto, chiamare la funzione **rxExec** .

1. Chiamare la funzione personalizzata come argomento per **rxExec**, insieme ad altri parametri che modificano la simulazione.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + Usare l'argomento *timesToRun* per indicare il numero di volte per cui eseguire la funzione.  In questo caso, i dati vengono tirati 20 volte.
  
    + Gli argomenti *RNGseed* e *RNGkind* possono essere usati per controllare la generazione casuale dei numeri. Quando *RNGseed* è impostato su **auto**, viene inizializzato un flusso di numeri casuali parallelo in ogni computer di lavoro.
  
2. La funzione **rxExec** crea un elenco con un elemento per ogni esecuzione; tuttavia, non verranno eseguite molte operazioni fino a quando l'elenco non è completato. Una volta completate tutte le iterazioni, la riga che inizia con **length** restituirà un valore.
  
    È quindi possibile andare al passaggio successivo per ottenere un riepilogo del record vincita-perdita.
  
3. Convertire l'elenco restituito in un vettore usando la funzione R **unlist** e creare un riepilogo dei risultati usando la funzione **table** .
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    I risultati saranno simili ai seguenti:
  
     *Perdita vittoria* *12 8*

## <a name="conclusion"></a>Conclusione

Sebbene questo esercizio sia semplicistico, viene illustrato un meccanismo importante per l'integrazione di funzioni R arbitrarie nello script R in esecuzione in SQL Server. Per riepilogare i punti chiave che rendono possibile questa tecnica:

+ SQL Server deve essere configurato per l'integrazione di machine learning e R: [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con la funzionalità r o [2016 SQL Server r Services (in-database)](../install/sql-r-services-windows-install.md).

+ Le librerie open source o di terze parti usate nella funzione, incluse tutte le dipendenze, devono essere installate in SQL Server. Per altre informazioni, vedere [installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md).

+ Lo sviluppo di script da un ambiente di sviluppo a un ambiente di produzione finalizzato può comportare limitazioni di rete e firewall. Eseguire un test con attenzione per assicurarsi che lo script sia in grado di funzionare come previsto.

## <a name="next-steps"></a>Passaggi successivi

Per un esempio più complesso dell'uso di **rxExec**, vedere questo articolo: [Parallelismo a grani grossolani con foreach e rxExec](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
