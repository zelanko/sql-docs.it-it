---
title: Converti il codice R per le stored procedure - servizi di SQL Server Machine Learning
description: Eseguire la migrazione di codice R da una stored procedure SQL Server per l'accesso soluzione di distribuzione e i dati ai dati relazionali in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: ac4c00830c9f678c467a75c1531b97fd3723c0b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962717"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>Converti il codice R per l'esecuzione in istanze di SQL Server (In-Database)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo fornisce indicazioni di alto livello su come modificare il codice R per lavorare in SQL Server. 

Quando si sposta codice R da R Studio o un altro ambiente a SQL Server, in genere il codice funziona senza ulteriori modifiche: ad esempio, se il codice è semplice, ad esempio una funzione che accetta alcuni input e restituisce un valore. È inoltre più semplice soluzioni di porta che utilizzano le **RevoScaleR** oppure **MicrosoftML** pacchetti che supportano l'esecuzione in contesti di esecuzione diversi con modifiche minime.

Tuttavia, il codice potrebbe richiedere modifiche sostanziali se una qualsiasi delle condizioni seguenti:

+ Si usano le librerie R che accedono alla rete o che non possono essere installati in SQL Server.
+ Il codice effettua una chiamata a origini dati esterne di SQL Server, ad esempio fogli di lavoro di Excel, i file nelle condivisioni e altri database. 
+ Si vuole eseguire il codice nel *@script* parametro [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e anche impostare i parametri della stored procedure.
+ La soluzione originale include più passaggi che potrebbero essere più efficienti in un ambiente di produzione se eseguita in modo indipendente, ad esempio la preparazione dei dati o la progettazione di funzionalità rispetto al modello di training, assegnazione dei punteggi o creazione di report.
+ Si vuole migliorare ottimizzare le prestazioni modificando le librerie, tramite l'esecuzione parallela o l'offload di alcune operazioni di elaborazione a SQL Server. 

## <a name="step-1-plan-requirements-and-resources"></a>Passaggio 1. Pianificare i requisiti e risorse

**Pacchetti**

+ Determinare quali pacchetti sono necessari e garantirne il funzionamento in SQL Server.
 
+ Installare i pacchetti in anticipo, nella libreria del pacchetto predefinito usata da servizi di Machine Learning. Non sono supportate nelle librerie utente.

**Origini dei dati** 

+ Se si intende incorporare il codice R in [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), identificare le origini dati primarie e secondarie. 

    + **Primario** origini dati sono grandi set di dati, ad esempio dati di training del modello o i dati di input per ottenere previsioni attendibili. Prevede di eseguire il mapping del set di dati più grande per il parametro di input dei [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + **Secondario** origini dati sono in genere più piccoli set di dati, ad esempio elenchi di fattori, o le variabili di raggruppamento aggiuntive. 
    
    Sp_execute_external_script supporta attualmente solo un singolo set di dati come input per la stored procedure. Tuttavia, è possibile aggiungere più input scalare o binary.

    Chiamate a stored procedure precedute da EXECUTE non possono essere usate come input per [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). È possibile usare le query, viste o qualsiasi altra istruzione SELECT valida.

+ Determinare l'output che è necessario. Se si esegue codice R tramite sp_execute_external_script, la stored procedure può restituire solo un frame di dati di conseguenza. Tuttavia, è anche possibile inviare più output scalari, inclusi tracciati e modelli in formato binario, nonché altri valori scalari derivato dal codice R o SQL parametri.

**Tipi di dati**

+ Creare un elenco di controllo dei possibili problemi con i tipi di dati.

    Tutti i tipi di dati R sono supportati da servizi di SQL Server machine Learning. Tuttavia, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta una varietà di tipi di dati maggiore rispetto a R. Di conseguenza, alcune conversioni di tipi di dati implicite vengono eseguite quando si inviano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati in R e viceversa. Si potrebbe essere necessario eseguire il cast o convertire alcuni dati in modo esplicito. 

    I valori NULL sono supportati. Tuttavia, Usa R il `na` costrutto di dati per rappresentare un valore mancante, che è simile a un valore null.

+ Provare a eliminare una dipendenza da dati non possono essere usati da r, ad esempio, rowid e tipi di dati GUID da SQL Server non possono essere utilizzati da R e generano errori.

    Per altre informazioni, vedere [librerie di R e tipi di dati](../r/r-libraries-and-data-types.md).

## <a name="step-2-convert-or-repackage-code"></a>Passaggio 2. Convertire o ricreare il pacchetto di codice

Quanto si modifica il codice varia a seconda che si prevede di inviare il codice R da un client remoto per l'esecuzione nel contesto di calcolo di SQL Server o intende distribuire il codice come parte di una stored procedure, che può fornire migliori prestazioni e sicurezza dei dati. Eseguire il wrapping del codice in una stored procedure vengono imposti alcuni requisiti aggiuntivi. 

+ Definire i dati di input primari come una query SQL laddove possibile, per evitare lo spostamento dei dati.

+ Durante l'esecuzione di R in una stored procedure, è possibile passare attraverso più **scalare** input. Per i parametri che si desidera utilizzare nell'output, aggiungere il **OUTPUT** (parola chiave). 

    Ad esempio, l'input scalare seguente `@model_name` contiene il nome del modello, che viene anche restituito nella rispettiva colonna nei risultati:

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ Tutte le variabili passate come parametri della stored procedure [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) deve essere mappato a variabili nel codice R. Per impostazione predefinita, il mapping delle variabili viene eseguito in base al nome.

    Tutte le colonne in set di dati di input devono essere mappate anche alle variabili nello script R.  Si supponga, ad esempio, che lo script R contenga una formula simile alla seguente:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    Se il set di dati di input non contiene colonne con i nomi ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour e DayOfWeek, viene generato un errore.

+ In alcuni casi, è necessario definire in anticipo uno schema di output per i risultati.

    Ad esempio, per inserire i dati in una tabella, è necessario usare il **con SET di risultati** clausola per specificare lo schema.

    Lo schema di output è necessario anche se lo script R Usa l'argomento `@parallel=1`. perché SQL Server potrebbe creare più processi per eseguire la query in parallelo, raccogliendo i risultati alla fine. Pertanto, è necessario preparare lo schema di output prima di possono creare i processi paralleli.
    
    In altri casi, è possibile omettere lo schema di risultati usando l'opzione **WITH RESULT SETS UNDEFINED**. Questa istruzione restituisce il set di dati dallo script R senza le colonne di denominazione o specificando i tipi di dati SQL.

+ Si consiglia di generare le tempistiche o rilevamento dati mediante T-SQL anziché di R.

    Ad esempio, è possibile passare l'ora di sistema o altre informazioni utilizzate per l'archiviazione e il controllo dall'aggiunta di una chiamata di T-SQL che viene passata ai risultati, anziché generare dati simili nello script R. 

**Migliorare le prestazioni e sicurezza**

+ Evitare di scrivere i risultati intermedi in un file o le stime. Scrivere le stime in una tabella, invece, per evitare lo spostamento dei dati.

+ Eseguire in anticipo tutte le query ed esaminare i piani di query di SQL Server per identificare le attività che possono essere eseguite in parallelo.

    Se la query di input può essere parallelizzata, impostare `@parallel=1` come parte degli argomenti per [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). 

    L'elaborazione parallela con questo flag è in genere possibile ogni volta che SQL Server può usare le tabelle partizionate o distribuire una query tra più processi e aggregare i risultati alla fine. L'elaborazione parallela con questo flag in genere non è possibile se si esegue il training dei modelli usando algoritmi che richiedono la lettura di tutti i dati o se è necessario creare aggregati.

+ Riesaminare il codice R per determinare se ci sono passaggi che possono essere eseguiti in modo indipendente o più efficiente, usando una chiamata alle stored procedure separata. Ad esempio, si potrebbero ottenere prestazioni migliori eseguendo separatamente la progettazione di funzionalità o l'estrazione di funzioni, e salvando i valori in una tabella.

+ Cercare i modi per usare T-SQL anziché come codice R per i calcoli basati su set.

    Ad esempio, questa soluzione R illustra come definito dall'utente funzioni T-SQL e R è possibile eseguire la stessa attività di progettazione di funzionalità: [Procedura dettagliata End-to-End di data Science](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Se possibile, sostituire le funzioni R convenzionali con **ScaleR** funzioni che supportano l'esecuzione distribuita. Per altre informazioni, vedere [confronto di Base R e ridimensiona le funzioni R](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Con uno sviluppatore di database per determinare come migliorare le prestazioni con funzionalità di SQL Server, ad esempio, consultare [le tabelle ottimizzate per la memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables), o, se si dispone di Enterprise Edition [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)).

    Per altre informazioni, vedere [suggerimenti di ottimizzazione di SQL Server e consigli per i servizi di Analitica](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>Passaggio 3. Preparare la distribuzione

+ Inviare una notifica all'amministratore in modo che i pacchetti possano essere installati e testati prima di distribuire il codice. 

    In un ambiente di sviluppo, potrebbe essere accettabile installare i pacchetti come parte del codice, ma si tratta di farlo in un ambiente di produzione. 

    Non sono supportate nelle librerie utente, indipendentemente dal fatto che si utilizza una stored procedure o esegue codice R nel contesto di calcolo di SQL Server.

**Comprimere il codice R in una stored procedure**

+ Se il codice è relativamente semplice, è possibile incorporarlo in una funzione T-SQL definiti dall'utente senza alcuna modifica, come descritto negli esempi seguenti:

    + [Creare una funzione R che viene eseguito in rxExec](../tutorials/deepdive-create-a-simple-simulation.md)
    + [Progettazione di funzionalità con T-SQL e R](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ Se il codice è più complessa, usare il pacchetto R **sqlrutils** per convertire il codice. Questo pacchetto è progettato per aiutare gli utenti R esperti di scrivere codice ottimale della stored procedure. 

    Il primo passaggio è necessario riscrivere il codice R come una singola funzione di chiaramente definito gli input e output.

    Quindi, usare il **sqlrutils** pacchetto per generare gli input e output nel formato corretto. Il **sqlrutils** pacchetto genera il codice completa della stored procedure per l'utente e può anche registrare la stored procedure nel database. 

    Per altre informazioni ed esempi, vedere [sqlrutils (SQL)](ref-r-sqlrutils.md).

**Integrare con altri flussi di lavoro**

+ Sfrutta gli strumenti di T-SQL e i processi ETL. Eseguire la progettazione di funzionalità, estrazione di funzioni e la pulizia dei dati in anticipo come parte dei flussi di lavoro dei dati.

    Quando si lavora in un ambiente di sviluppo R dedicato, ad esempio [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] o RStudio, si potrebbe eseguire il pull dei dati nel computer, analizzare i dati in modo iterativo e quindi scrivere o visualizzare i risultati. 
    
    Tuttavia, quando viene eseguita la migrazione di codice R autonomo a SQL Server, gran parte di questo processo può essere semplificata o delegata ad altri strumenti di SQL Server. 

+ Usare strategie di visualizzazione sicura e asincrono.

    Gli utenti di SQL Server spesso non è possibile accedere ai file nel server e gli strumenti SQL client non supportano in genere il dispositivo di grafica R. Se si generano tracciati o altri elementi grafici come parte della soluzione, è consigliabile esportare i tracciati come dati binari e salvataggio in una tabella o la scrittura.

+ Eseguire il wrapping di funzioni di assegnazione dei punteggi e stima nelle stored procedure per l'accesso diretto dalle applicazioni.

### <a name="other-resources"></a>Altre risorse

Per visualizzare esempi di come è possibile distribuire una soluzione R in SQL Server, vedere gli esempi seguenti:

+ [Compilare un modello predittivo per il noleggio di sci usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Analitica nel Database per sviluppatori SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) viene illustrato come è possibile apportare al codice R più modulare mediante il wrapping nelle stored procedure

+ [Soluzione di analisi scientifica dei dati end-to-End](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) include un confronto della progettazione di funzioni in R e T-SQL
