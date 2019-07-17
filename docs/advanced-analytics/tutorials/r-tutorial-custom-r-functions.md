---
title: Eseguire funzioni R personalizzate in SQL Server con RevoScaleR rxExec - SQL Server Machine Learning
description: Procedura dettagliata su come eseguire lo script R in SQL Server con funzioni RevoScaleR.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: c9cb9d84637d20f3f0e73f97fa6565d84d12fb4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961959"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec"></a>Eseguire funzioni R personalizzate in SQL Server con rxExec
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

È possibile eseguire funzioni R personalizzate nel contesto di SQL Server mediante il passaggio alla funzione tramite [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec), presupponendo che le eventuali librerie lo script richiede anche installate nel server e tali librerie sono compatibili con la base distribuzione di R. 

Il **rxExec** funzionare **RevoScaleR** fornisce un meccanismo per l'esecuzione di tutti gli script R è necessario. È inoltre **rxExec** è in grado di distribuire in modo esplicito il lavoro tra più core in un singolo server, aggiunta di scalabilità per gli script che in caso contrario sono limitati per i vincoli di risorse del motore di R nativo.

In questa esercitazione si userà i dati simulati per illustrare l'esecuzione di una funzione R personalizzata che viene eseguito in un server remoto.

## <a name="prerequisites"></a>Prerequisiti

+ [Servizi (con R) SQL Server 2017 Machine Learning](../install/sql-machine-learning-services-windows-install.md) o [SQL Server 2016 R Services (in-Database)](../install/sql-r-services-windows-install.md)
  
+ [Autorizzazioni database](../security/user-permission.md) e un account di accesso di SQL Server database utente

+ [Una workstation di sviluppo con le librerie RevoScaleR](../r/set-up-a-data-science-client.md)

La distribuzione di R nella workstation client fornisce un oggetto incorporato **Rgui** strumento che è possibile usare per eseguire lo script R in questa esercitazione. È anche possibile usare un IDE, ad esempio RStudio o in R Tools per Visual Studio.

## <a name="create-the-remote-compute-context"></a>Creare il contesto di calcolo remoto

Eseguire i comandi R seguenti in una workstation client. Ad esempio, si usa **Rgui**, avviarla da questo percorso: C:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. Specificare la stringa di connessione per l'istanza di SQL Server in cui vengono eseguiti i calcoli. Il server deve essere configurato per l'integrazione di R. Il nome del database non viene usato in questo esercizio, ma la stringa di connessione richiede uno. Se si dispone di un database di esempio o test, è possibile utilizzarlo.

    **Uso di un account di accesso SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Uso dell'autenticazione di Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. Creare un contesto di calcolo remoto all'istanza di SQL Server a cui fa riferimento la stringa di connessione.

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. Attivare il contesto di calcolo e quindi restituisce la definizione dell'oggetto come un'operazione di conferma. È necessario visualizzare le proprietà dell'oggetto di contesto di calcolo.

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>Creare la funzione personalizzata

In questo esercizio si creerà una funzione R personalizzata che simula un comune casinò costituito in sequenza una coppia di dadi. Le regole del gioco determinano un risultato di perdita o win:

+ Eseguire il rollback di una 7 o 11 nel tiro iniziale, si vince.
+ Eseguire il rollback 2, 3 o 12, si perde.
+ Eseguire il rollback di un 4 e 5, 6, 8, 9 o 10, tale numero diventa il punto è possibile continuare a tirare fino a quando non si che sia distribuire nuovamente il punto (nel qual caso win) o il rollback di una 7, nel quale caso si perde.

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
  
2.  Simulare una singola giocata ai dadi, eseguire la funzione.
  
    ```R
    rollDice()
    ```
  
    Si ha vinto o si ha perso?
  
Ora che avete uno script operativo, vediamo come è possibile usare **rxExec** per eseguire la funzione più volte per creare una simulazione che consente di determinare la probabilità di vincita.

## <a name="pass-rolldice-in-rxexec"></a>Passare rollDice() rxExec

Per eseguire una funzione arbitraria nel contesto di un Server SQL remoto, chiamare il **rxExec** (funzione).

1. Chiamare la funzione personalizzata come argomento al **rxExec**, in combinazione con altri parametri che modificano la simulazione.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + Usare l'argomento *timesToRun* per indicare il numero di volte per cui eseguire la funzione.  In questo caso, i dati vengono tirati 20 volte.
  
    + Gli argomenti *RNGseed* e *RNGkind* possono essere usati per controllare la generazione casuale dei numeri. Quando *RNGseed* è impostato su **auto**, viene inizializzato un flusso di numeri casuali parallelo in ogni computer di lavoro.
  
2. La funzione **rxExec** crea un elenco con un elemento per ogni esecuzione; tuttavia, non verranno eseguite molte operazioni fino a quando l'elenco non è completato. Quando tutte le iterazioni vengono completate, la riga che inizia con **lunghezza** restituirà un valore.
  
    È quindi possibile andare al passaggio successivo per ottenere un riepilogo del record vincita-perdita.
  
3. Convertire l'elenco restituito in un vettore usando la funzione R **unlist** e creare un riepilogo dei risultati usando la funzione **table** .
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    I risultati saranno simili ai seguenti:
  
     *Perdita vincita* *12 8*

## <a name="conclusion"></a>Conclusione

Sebbene questo esercizio è semplicistico, viene illustrato un importante meccanismo per l'integrazione di funzioni R arbitrarie in script R in esecuzione in SQL Server. Per riepilogare i punti chiave che rendono possibile questa tecnica:

+ SQL Server deve essere configurato per l'integrazione di R e apprendimento automatico: [Machine Learning Services di SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) con la funzionalità di R, oppure [SQL Server 2016 R Services (in-Database)](../install/sql-r-services-windows-install.md).

+ Librerie open source o di terze parti usate nella funzione, incluse eventuali dipendenze, devono essere installate su SQL Server. Per altre informazioni, vedere [installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md).

+ Lo spostamento di script da un ambiente di sviluppo in un ambiente di produzione con protezione avanzata può introdurre restrizioni firewall e della rete. Testare attentamente per assicurarsi che lo script sia in grado di eseguire nel modo previsto.

## <a name="next-steps"></a>Passaggi successivi

Per un esempio più complesso di utilizzo **rxExec**, vedere questo articolo: [Parallelismo granulosità grossolana con foreach e rxExec](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
