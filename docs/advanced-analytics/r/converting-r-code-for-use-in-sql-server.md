---
title: Convertire il codice R per le stored procedure
description: Eseguire la migrazione del codice R a un SQL Server stored procedure per la distribuzione della soluzione e l'accesso ai dati relazionali in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a2bd6db3aaae2c07f6f46aecce3e7df913fc2a9e
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470243"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>Conversione del codice R per l'esecuzione in istanze di SQL Server (in-database)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo fornisce indicazioni generali su come modificare il codice R per lavorare in SQL Server. 

Quando si sposta il codice R da R Studio o da un altro ambiente a SQL Server, la maggior parte delle volte il codice funziona senza ulteriori modifiche: ad esempio, se il codice è semplice, ad esempio una funzione che accetta alcuni input e restituisce un valore. È anche più facile trasferire le soluzioni che usano i pacchetti **RevoScaleR** o **MicrosoftML** , che supportano l'esecuzione in contesti di esecuzione diversi con modifiche minime.

Tuttavia, il codice potrebbe richiedere modifiche sostanziali se si verifica una delle condizioni seguenti:

+ Si usano le librerie R che accedono alla rete o che non possono essere installate in SQL Server.
+ Il codice effettua chiamate separate alle origini dati all'esterno SQL Server, ad esempio fogli di lavoro di Excel, file di condivisioni e altri database. 
+ Si vuole eseguire il codice nel *@script* parametro di [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e parametrizzare anche il stored procedure.
+ La soluzione originale include più passaggi che possono essere più efficienti in un ambiente di produzione, se eseguiti in modo indipendente, ad esempio la preparazione dei dati o la progettazione di funzionalità rispetto al training del modello, il punteggio o la creazione di report.
+ Per migliorare le prestazioni, è necessario modificare le librerie, utilizzare l'esecuzione parallela o eseguire l'offload di alcune elaborazioni in SQL Server. 

## <a name="step-1-plan-requirements-and-resources"></a>Passaggio 1. Pianificare requisiti e risorse

**Pacchetti**

+ Determinare quali pacchetti sono necessari e verificare che funzionino in SQL Server.
 
+ Installare i pacchetti in anticipo nella libreria di pacchetti predefinita utilizzata da Machine Learning Services. Le librerie utente non sono supportate.

**Origini dei dati** 

+ Se si intende incorporare il codice R in [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), identificare le origini dati primarie e secondarie. 

    + Le origini dati **primarie** sono set di dati di grandi dimensioni, ad esempio dati di training del modello o dati di input per le stime. Pianificare il mapping del set di dati più grande al parametro di input di [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + Le origini dati **secondarie** sono in genere set di dati più piccoli, ad esempio elenchi di fattori o variabili di raggruppamento aggiuntive. 
    
    Attualmente, sp_execute_external_script supporta solo un singolo set di dati come input per il stored procedure. Tuttavia, è possibile aggiungere più input scalari o binari.

    Impossibile utilizzare le chiamate di stored procedure precedute da EXECUTE come input per [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). È possibile utilizzare query, viste o qualsiasi altra istruzione SELECT valida.

+ Determinare gli output necessari. Se si esegue il codice R usando sp_execute_external_script, il stored procedure può restituire solo un frame di dati di conseguenza. Tuttavia, è anche possibile restituire più output scalari, inclusi i tracciati e i modelli in formato binario, nonché altri valori scalari derivati dal codice R o dai parametri SQL.

**Tipi di dati**

+ Creare un elenco di controllo dei possibili problemi con i tipi di dati.

    Tutti i tipi di dati R sono supportati da SQL Server Machine Learning Services. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Supporta tuttavia una maggiore varietà di tipi di dati rispetto a R. Di conseguenza, vengono eseguite alcune conversioni implicite di tipi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati quando si inviano dati a R e viceversa. Potrebbe essere necessario eseguire il cast o la conversione esplicita di alcuni dati. 

    I valori NULL sono supportati. Tuttavia, R usa il `na` costrutto dei dati per rappresentare un valore mancante, che è simile a un valore null.

+ Provare a eliminare la dipendenza dai dati che non possono essere usati da R: ad esempio, i tipi di dati ROWID e GUID da SQL Server non possono essere utilizzati da R e generano errori.

    Per altre informazioni, vedere [librerie R e tipi di dati](../r/r-libraries-and-data-types.md).

## <a name="step-2-convert-or-repackage-code"></a>Passaggio 2. Convertire o riassemblare il codice

La modifica del codice varia a seconda che si intenda inviare il codice R da un client remoto per l'esecuzione nel contesto di calcolo SQL Server o si intende distribuire il codice come parte di un stored procedure, che può offrire prestazioni migliori e sicurezza dei dati. Il wrapping del codice in una stored procedure impone alcuni requisiti aggiuntivi. 

+ Definire i dati di input primari come query SQL, laddove possibile, per evitare lo spostamento dei dati.

+ Quando si esegue R in una stored procedure, è possibile passare attraverso  più input scalari. Per tutti i parametri che si desidera utilizzare nell'output, aggiungere la parola chiave **output** . 

    Il seguente input `@model_name` scalare, ad esempio, contiene il nome del modello, che viene anche restituito nella relativa colonna nei risultati:

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ Tutte le variabili passate come parametri del stored procedure [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) devono essere mappate a variabili nel codice R. Per impostazione predefinita, il mapping delle variabili viene eseguito in base al nome.

    È necessario eseguire il mapping di tutte le colonne nel set di dati di input anche a variabili nello script R.  Si supponga, ad esempio, che lo script R includa una formula simile alla seguente:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    Se il set di dati di input non contiene colonne con i nomi corrispondenti ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour e DayOfWeek, viene generato un errore.

+ In alcuni casi, è necessario definire in anticipo uno schema di output per i risultati.

    Per inserire i dati in una tabella, ad esempio, è necessario utilizzare la clausola **with result set** per specificare lo schema.

    Lo schema di output è necessario anche se lo script R usa l' `@parallel=1`argomento. perché SQL Server potrebbe creare più processi per eseguire la query in parallelo, raccogliendo i risultati alla fine. Pertanto, lo schema di output deve essere preparato prima di poter creare i processi paralleli.
    
    In altri casi, è possibile omettere lo schema dei risultati utilizzando l'opzione **con i set di risultati non definiti**. Questa istruzione restituisce il set di dati dallo script R senza denominare le colonne o specificare i tipi di dati SQL.

+ Provare a generare dati di temporizzazione o rilevamento usando T-SQL anziché R.

    Ad esempio, è possibile passare l'ora di sistema o altre informazioni usate per il controllo e l'archiviazione aggiungendo una chiamata T-SQL che viene passata ai risultati, anziché generare dati simili nello script R. 

**Migliorare le prestazioni e la sicurezza**

+ Evitare di scrivere stime o risultati intermedi in un file. In alternativa, scrivere stime in una tabella per evitare lo spostamento dei dati.

+ Eseguire tutte le query in anticipo ed esaminare i piani di query SQL Server per identificare le attività che possono essere eseguite in parallelo.

    Se la query di input può essere eseguita in parallelo `@parallel=1` , impostare come parte degli argomenti su [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). 

    L'elaborazione parallela con questo flag è in genere possibile ogni volta che SQL Server può usare le tabelle partizionate o distribuire una query tra più processi e aggregare i risultati alla fine. L'elaborazione parallela con questo flag in genere non è possibile se si esegue il training dei modelli usando algoritmi che richiedono la lettura di tutti i dati o se è necessario creare aggregati.

+ Riesaminare il codice R per determinare se ci sono passaggi che possono essere eseguiti in modo indipendente o più efficiente, usando una chiamata alle stored procedure separata. Ad esempio, è possibile ottenere prestazioni migliori eseguendo la progettazione delle funzioni o l'estrazione delle funzionalità separatamente e salvando i valori in una tabella.

+ Cercare i modi per usare T-SQL anziché il codice R per i calcoli basati su set.

    Ad esempio, questa soluzione R Mostra come funzioni T-SQL definite dall'utente e R possono eseguire la stessa attività di progettazione delle funzionalità: [Procedura dettagliata end-to-end di Data Science](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Se possibile, sostituire le funzioni R convenzionali  con funzioni scaler che supportano l'esecuzione distribuita. Per altre informazioni, vedere [confronto tra le funzioni r di base e scale r](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Consultare uno sviluppatore di database per determinare i modi per migliorare le prestazioni usando SQL Server funzionalità come le [tabelle ottimizzate](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)per la memoria o, se si dispone di Enterprise Edition, [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)).

    Per altre informazioni, vedere [suggerimenti e consigli per l'ottimizzazione SQL Server per i servizi di analisi](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>Passaggio 3. Preparare la distribuzione

+ Inviare una notifica all'amministratore in modo che i pacchetti possano essere installati e testati prima di distribuire il codice. 

    In un ambiente di sviluppo può essere corretto installare i pacchetti come parte del codice, ma si tratta di una procedura non valida in un ambiente di produzione. 

    Le librerie utente non sono supportate, indipendentemente dal fatto che si usi un stored procedure o si esegua codice R nel contesto di calcolo SQL Server.

**Creare il pacchetto del codice R in una stored procedure**

+ Se il codice è relativamente semplice, è possibile incorporarlo in una funzione T-SQL definita dall'utente senza modifiche, come descritto in questi esempi:

    + [Creare una funzione R che viene eseguita in rxExec](../tutorials/deepdive-create-a-simple-simulation.md)
    + [Progettazione di funzionalità con T-SQL e R](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ Se il codice è più complesso, usare il pacchetto R **sqlrutils** per convertire il codice. Questo pacchetto è stato progettato per consentire agli utenti esperti di R di scrivere codice stored procedure valido. 

    Il primo passaggio consiste nel riscrivere il codice R come una singola funzione con input e output chiaramente definiti.

    Usare quindi il pacchetto **sqlrutils** per generare l'input e gli output nel formato corretto. Il pacchetto **sqlrutils** genera automaticamente il codice di stored procedure completo ed è inoltre in grado di registrare i stored procedure nel database. 

    Per ulteriori informazioni ed esempi, vedere [sqlrutils (SQL)](ref-r-sqlrutils.md).

**Integrazione con altri flussi di lavoro**

+ Sfruttare gli strumenti T-SQL e i processi ETL. Eseguire la progettazione delle funzionalità, l'estrazione delle funzionalità e la pulizia dei dati in anticipo come parte dei flussi di lavoro dei dati.

    Quando si lavora in un ambiente di sviluppo R dedicato, ad [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] esempio o rstudio, è possibile eseguire il pull dei dati nel computer, analizzare i dati in modo iterativo e quindi scrivere o visualizzare i risultati. 
    
    Tuttavia, quando si esegue la migrazione del codice R autonomo a SQL Server, gran parte di questo processo può essere semplificata o delegata ad altri strumenti di SQL Server. 

+ USA strategie di visualizzazione asincrone sicure.

    Gli utenti di SQL Server spesso non possono accedere ai file nel server e gli strumenti client SQL in genere non supportano il dispositivo grafico R. Se si generano tracciati o altri elementi grafici come parte della soluzione, è consigliabile esportare i tracciati come dati binari e salvarli in una tabella oppure scrivere.

+ Eseguire il wrapping delle funzioni di stima e assegnazione dei punteggi nelle stored procedure per l'accesso diretto da applicazioni.

### <a name="other-resources"></a>Altre risorse

Per visualizzare esempi di come una soluzione R può essere distribuita in SQL Server, vedere gli esempi seguenti:

+ [Creazione di un modello predittivo per l'azienda di noleggio di sci usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Analisi nel database per sviluppatori SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) Viene illustrato come è possibile rendere più modulare il codice R eseguendone il wrapping nelle stored procedure

+ [Soluzione di Data Science end-to-end](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) Include un confronto tra la progettazione delle funzionalità in R e T-SQL
