---
title: Funzioni R personalizzate con rxExec
description: 'Esercitazione di RevoScaleR 14: Come eseguire script R personalizzati in SQL Server usando le funzioni RevoScaleR.'
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2f4fbaaa82bf1f06819e43e0f3d69094bfb6e81b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728579"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec-sql-server-and-revoscaler-tutorial"></a>Eseguire funzioni R personalizzate in SQL Server usando rxExec (esercitazione per SQL Server e RevoScaleR)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Questa è l'esercitazione 14 della [serie di esercitazioni per RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) dedicate all'uso delle [funzioni di RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa esercitazione si useranno dati simulati per illustrare l'esecuzione di una funzione R personalizzata che viene eseguita in un server remoto.

È possibile eseguire funzioni R personalizzate nel contesto di SQL Server passando la funzione tramite [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec), presupponendo che tutte le librerie necessarie per lo script siano installate anche nel server e che tali librerie siano compatibili con la distribuzione di base di R. 

La funzione **rxExec** in **RevoScaleR** fornisce un meccanismo per l'esecuzione di qualsiasi script R necessario. Inoltre, **rxExec** è in grado di distribuire in modo esplicito il lavoro tra più core in un singolo server, aggiungendo scalabilità a script altrimenti limitati ai vincoli di risorse del motore R nativo.

## <a name="prerequisites"></a>Prerequisiti

+ [Machine Learning Services per SQL Server 2016 (con R)](../install/sql-machine-learning-services-windows-install.md) o [R Services per SQL Server 2016 (In-Database)](../install/sql-r-services-windows-install.md)
  
+ [Autorizzazioni per il database](../security/user-permission.md) e un account di accesso per un database di SQL Server

+ [Una workstation di sviluppo con le librerie RevoScaleR](../r/set-up-a-data-science-client.md)

La distribuzione di R nella workstation client fornisce uno strumento **Rgui** incorporato che si può usare per eseguire lo script R in questa esercitazione. È anche possibile usare un IDE, ad esempio RStudio o R Tools per Visual Studio.

## <a name="create-the-remote-compute-context"></a>Creare il contesto di calcolo remoto

Eseguire i comandi R seguenti in una workstation client. Ad esempio, se si usa **Rgui**, avviarlo da questo percorso: C:\Programmi\Microsoft\R Client\R_SERVER\bin\x64\.

1. Specificare la stringa di connessione per l'istanza di SQL Server in cui vengono eseguiti i calcoli. Il server deve essere configurato per l'integrazione di R. Il nome del database non viene usato in questo esercizio, ma la stringa di connessione ne richiede uno. Se si ha un database di test o di esempio, è possibile usare quello.

    **Uso di un account di accesso SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Uso dell'autenticazione di Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. Creare un contesto di calcolo remoto sull'istanza di SQL Server referenziata nella stringa di connessione.

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. Attivare il contesto di calcolo e quindi restituire la definizione dell'oggetto come passaggio di conferma. Dovrebbero essere visualizzate le proprietà dell'oggetto contesto di calcolo.

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>Creare la funzione personalizzata

In questo esercizio verrà creata una funzione R personalizzata che simula un comune gioco di casinò consistente nel lanciare due dadi. Le regole del gioco determinano un risultato di vincita o perdita:

+ Se si raggiunge un punteggio di 7 o 11 nel lancio iniziale, si vince.
+ Se si raggiunge un punteggio di 2, 3 o 12, si perde.
+ Se si raggiunge un punteggio di 4, 5, 6, 8, 9 o 10 è possibile continuare a lanciare fino a quando non si ottiene lo stesso punteggio e si vince o si ottiene 7 e si perde.

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
  
2.  Simulare un singolo lancio dei dadi eseguendo la funzione.
  
    ```R
    rollDice()
    ```
  
    Si ha vinto o si ha perso?
  
Ora che si ha uno script operativo, si vedrà come usare **rxExec** per eseguire la funzione più volte e creare una simulazione che consente di determinare la probabilità di vincita.

## <a name="pass-rolldice-in-rxexec"></a>Passare rollDice () in rxExec

Per eseguire una funzione arbitraria nel contesto di un'istanza di SQL Server remota, chiamare la funzione **rxExec**.

1. Chiamare la funzione personalizzata come argomento di **rxExec**, con altri parametri che modificano la simulazione.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + Usare l'argomento *timesToRun* per indicare il numero di volte per cui eseguire la funzione.  In questo caso, i dati vengono tirati 20 volte.
  
    + Gli argomenti *RNGseed* e *RNGkind* possono essere usati per controllare la generazione casuale dei numeri. Quando *RNGseed* è impostato su **auto**, viene inizializzato un flusso di numeri casuali parallelo in ogni computer di lavoro.
  
2. La funzione **rxExec** crea un elenco con un elemento per ogni esecuzione; tuttavia, non verranno eseguite molte operazioni fino a quando l'elenco non è completato. Quando tutte le iterazioni vengono completate, la riga che inizia con **length** restituirà un valore.
  
    È quindi possibile andare al passaggio successivo per ottenere un riepilogo del record vincita-perdita.
  
3. Convertire l'elenco restituito in un vettore usando la funzione R **unlist** e creare un riepilogo dei risultati usando la funzione **table** .
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    I risultati saranno simili ai seguenti:
  
     *Perdita  Vincita* *12  8*

## <a name="conclusion"></a>Conclusioni

Sebbene questo esercizio sia semplicistico, dimostra un meccanismo importante per l'integrazione di funzioni R arbitrarie in uno script R in esecuzione in SQL Server. Per riepilogare i punti chiave che rendono possibile questa tecnica:

+ SQL Server deve essere configurato per l'integrazione di R e Machine Learning: [Machine Learning Services per SQL Server](../install/sql-machine-learning-services-windows-install.md) con la funzionalità R o [R Services per SQL Server 2016 (In-Database)](../install/sql-r-services-windows-install.md).

+ Le librerie open source o di terze parti usate nella funzione, incluse le eventuali dipendenze, devono essere installate in SQL Server. Per altre informazioni, vedere [Installare nuovi pacchetti R](../package-management/install-additional-r-packages-on-sql-server.md).

+ Lo spostamento dello script da un ambiente di sviluppo a un ambiente di produzione con protezione avanzata può introdurre restrizioni per rete e firewall. Eseguire test accurati per verificare che lo script possa funzionare come previsto.

## <a name="next-steps"></a>Passaggi successivi

Per un esempio più complesso dell'uso di **rxExec**, vedere questo articolo: [Coarse grain parallelism with foreach and rxExec](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html) (Parallelismo a granularità grossolana con foreach e rxExec)
