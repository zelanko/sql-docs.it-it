---
title: Ottimizzazione delle prestazioni per l'ottimizzazione dei dati - SQL Server Machine Learning Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b6e25ec0c7bc1ce332514910cdaf5cdf9fdb9e07
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432404"
---
# <a name="performance-for-r-services---data-optimization"></a>Prestazioni per R Services - ottimizzazione dei dati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo è il terzo di una serie che descrive l'ottimizzazione delle prestazioni per R Services basato su due casi di Studio. Questo articolo illustra le ottimizzazioni delle prestazioni per R o Python gli script eseguiti in SQL Server. Vengono inoltre descritti i metodi che è possibile usare per aggiornare il codice R, per migliorare le prestazioni e per evitare problemi noti.

## <a name="choosing-a-compute-context"></a>Scelta di un contesto di calcolo

In SQL Server 2016 e 2017, è possibile usare la **locale** oppure **SQL** contesto di calcolo durante l'esecuzione di script R o Python.

Quando si usa la **locale** contesto di calcolo, analisi viene eseguita nel computer e non nel server. Di conseguenza, se si ricevono i dati da SQL Server da usare nel codice, è necessario recuperati i dati attraverso la rete. Il calo di prestazioni riscontrato per questo trasferimento in rete dipende dalle dimensioni dei dati trasferiti, dalla velocità della rete e dagli eventuali altri trasferimenti in rete che si verificano nello stesso momento.

Quando si usa la **contesto di calcolo di SQL Server**, il codice viene eseguito nel server. Se si ricevono i dati da SQL Server, i dati dovrebbero essere locali nel server che esegue l'analisi e di conseguenza non è stato introdotto alcun overhead di rete. Se è necessario importare i dati da altre origini, prendere in considerazione la disposizione di ETL in anticipo.

Quando si usano set di dati di grandi dimensioni, è consigliabile usare sempre il contesto di calcolo SQL.

## <a name="factors"></a>Fattori

Il linguaggio R è il concetto di *fattori*, che sono variabili speciali per i dati categorici. I data Scientist possono usare variabili di fattore nelle loro formule spesso, perché la gestione di variabili categoriche come fattori assicura che i dati viene elaborato correttamente da funzioni di machine learning. Per altre informazioni, vedere [R per principianti: Variabili di fattore](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/).

Per impostazione predefinita, le variabili di fattore possono essere convertite da stringhe in numeri interi e viceversa, anche in questo caso per l'archiviazione o l'elaborazione. L'oggetto R `data.frame` funzione gestisce tutte le stringhe come variabili di fattore, a meno che l'argomento *stringsAsFactors* è impostata su **False**. Questo significa è che le stringhe vengono automaticamente convertito in un numero intero per l'elaborazione ed è quindi rimappata alla stringa originale.

Se i dati di origine per i fattori vengano archiviati come integer, le prestazioni potrebbero diminuire poiché R converte i numeri interi factor in stringhe in fase di esecuzione e quindi esegue la propria conversione stringa a numero intero interno.

Per evitare tali conversioni in fase di esecuzione, è consigliabile archiviare i valori come numeri interi nella tabella di SQL Server e usando il _colInfo_ argomento per specificare i livelli per la colonna utilizzata come fattore. La maggior parte degli oggetti origine dati in RevoScaleR accettano il parametro _colInfo_. Utilizzare questo parametro per denominare le variabili utilizzate dall'origine dei dati, specificare il tipo e definire i livelli di variabili o trasformazioni sui valori di colonna.

Ad esempio, la chiamata di funzione R seguente ottiene i numeri interi 1, 2 e 3 da una tabella, ma viene eseguito il mapping di valori da un fattore con livelli di "apple", "arancione" e "banana".

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

Quando la colonna di origine contiene stringhe, è sempre più efficiente per specificare i livelli in anticipo usando il _colInfo_ parametro. Ad esempio, il codice R seguente considera le stringhe come fattori come vengono letti.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

Se non vi è alcuna differenza semantica nella generazione del modello, il secondo approccio può comportare prestazioni migliorate.

## <a name="data-transformations"></a>Trasformazioni dei dati

I data scientist usano spesso le funzioni di trasformazione scritte in R nell'ambito dell'analisi. La funzione di trasformazione viene applicata a ogni riga recuperata dalla tabella. In SQL Server, tali trasformazioni vengono applicate a tutte le righe recuperate in un batch, che richiede la comunicazione tra l'interprete R e il motore di analitica. Per eseguire la trasformazione, i dati vengono spostati da SQL al motore di analisi e quindi al processo dell'interprete R e viceversa.

Per questo motivo, tramite trasformazioni come parte del codice R può avere un notevole effetto negativo sulle prestazioni dell'algoritmo, a seconda della quantità di dati coinvolti.

È più efficiente per disporre di tutte le colonne necessarie nella tabella o vista prima di eseguire analisi ed evitare le trasformazioni durante il calcolo. Se non è possibile aggiungere altre colonne alle tabelle esistenti, è consigliabile creare un'altra tabella o vista con le colonne trasformate e usare una query appropriata per recuperare i dati.

## <a name="batch-row-reads"></a>Letture di righe di batch

Se si usa un'origine dati SQL Server (`RxSqlServerData`) nel codice, è consigliabile provare usando il parametro _rowsPerRead_ per specificare le dimensioni del batch. Questo parametro definisce il numero di righe che vengono sottoposti a query e quindi inviati allo script esterni per l'elaborazione. In fase di esecuzione, l'algoritmo vede solo il numero specificato di righe in ogni batch.

La possibilità di controllare la quantità di dati che vengono elaborati in un momento consentono di risolvere o evitare problemi. Ad esempio, se il set di dati di input è molto ampia (include molte colonne), o se il set di dati dispone di alcune colonne di grandi dimensioni (ad esempio testo libero), è possibile ridurre le dimensioni del batch per evitare il paging dati dalla memoria.

Per impostazione predefinita, il valore di questo parametro è impostato su 50000, per garantire una prestazione soddisfacente anche in computer con memoria insufficiente. Se nel server è disponibile memoria sufficiente, se si aumenta questo valore a 500.000 o anche a un milione può garantire prestazioni migliori, in particolare per tabelle di grandi dimensioni.

I vantaggi dell'aumento delle dimensioni batch diventano evidenti in un set di dati di grandi dimensioni in un'attività che è possibile eseguire su più processi. Tuttavia, se si aumenta questo valore non produce sempre risultati ottimali. È consigliabile provare con i dati e l'algoritmo per determinare il valore ottimale.

## <a name="parallel-processing"></a>elaborazione parallela

Per migliorare le prestazioni delle **rx** funzioni analitiche, è possibile sfruttare le capacità di SQL Server per eseguire attività in parallelo in base ai core disponibili nel computer del server.

Esistono due modi per ottenere la parallelizzazione di R in SQL Server:

-   **Usare \@parallele.** Quando si usa la stored procedure `sp_execute_external_script` per eseguire uno script R, impostare il parametro `@parallel` su `1`. Si tratta del metodo migliore se non lo script R **non** usano funzioni RevoScaleR, che hanno altri meccanismi per l'elaborazione. Se lo script Usa funzioni RevoScaleR (in genere contenenti il prefisso "rx"), l'elaborazione parallela viene eseguita automaticamente e non è necessario impostare in modo esplicito `@parallel` a `1`.

    Se lo script R può essere eseguite in parallelo e, se la query SQL può essere parallelizzata, il motore di database crea più processi paralleli. Il numero massimo di processi che possono essere create è uguale per il **massimo grado di parallelismo** impostazione (MAXDOP) per l'istanza. Tutti i processi, quindi eseguire lo stesso script, ma ricevano solo una parte dei dati.
    
    Di conseguenza, questo metodo non è utile per gli script che devono visualizzare tutti i dati, ad esempio quando un modello di training. Tuttavia, è utile quando si eseguono attività come la stima in batch in parallelo. Per altre informazioni sull'uso del parallelismo con `sp_execute_external_script`, vedere la **suggerimenti per utenti esperti: l'elaborazione parallela** sezione del [usare il codice R in Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

-   **Usare numTasks = 1.** Quando si usa **rx** le funzioni in un contesto di calcolo di SQL Server, impostare il valore della _numTasks_ parametro per il numero di processi che si vuole creare. Il numero di processi creati non può mai essere oltre **MAXDOP**; tuttavia, il numero effettivo di processi creati è determinato dal motore di database e può essere minore di è richiesto.

    Se lo script R può essere eseguite in parallelo e se la query SQL può essere parallelizzata, SQL Server crea più processi paralleli durante l'esecuzione delle funzioni rx. Il numero effettivo di processi che vengono creati dipende da un'ampia gamma di fattori come la governance delle risorse, l'uso corrente delle risorse, altre sessioni e il piano di esecuzione di query per la query usata con lo script R.

## <a name="query-parallelization"></a>Parallelizzazione delle query

In Microsoft R, è possibile utilizzare con le origini dati di SQL Server tramite la definizione dei dati come un oggetto di origine dati RxSqlServerData.

Crea un'origine dati basata su un'intera tabella o vista:

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

Crea un'origine dati basata su una query SQL:

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> Se viene specificata una tabella nell'origine dei dati invece di una query, R Services Usa l'approccio euristico interno per determina le colonne necessarie per recuperare dalla tabella. Tuttavia, questo approccio è improbabile che l'esecuzione in parallelo.

Per garantire che i dati possono essere analizzati in parallelo, la query usata per recuperare i dati dovrebbe consentire in modo che il motore di database può creare un piano di query parallele. Se il codice o l'algoritmo utilizza grandi volumi di dati, assicurarsi che la query passata a `RxSqlServerData` è ottimizzato per l'esecuzione parallela. Una query che non implica un piano di esecuzione parallela può comportare un singolo processo per il calcolo.

Se è necessario lavorare con grandi set di dati, usare Management Studio o un altro SQL query analyzer prima di eseguire codice R per analizzare il piano di esecuzione. Quindi, eseguire le procedure consigliate per migliorare le prestazioni della query. Ad esempio, un indice mancante in una tabella può influire sul tempo impiegato per eseguire una query. Per altre informazioni, vedere [monitorare e ottimizzare le prestazioni](../../relational-databases/performance/monitor-and-tune-for-performance.md).

Un altro errore comune che può influire sulle prestazioni è che una query recupera più colonne di quelle richieste. Ad esempio, se una formula si basa su tre colonne, ma la tabella di origine ne include 30, si spostano dati inutilmente.

 + Evitare di usare `SELECT *`!
 + Richiedere del tempo per esaminare le colonne nel set di dati e identificare solo quelle necessarie per l'analisi
 + Rimuovi dalle query tutte le colonne che contengono i tipi di dati che non sono compatibili con il codice R, ad esempio GUID e ROWGUID
 + Controllo per i formati di ora e data non supportato
 + Invece di caricare una tabella, creare una vista che seleziona determinati valori o colonne per evitare errori di conversione viene eseguito il cast

## <a name="optimizing-the-machine-learning-algorithm"></a>Ottimizzare l'algoritmo di machine learning

In questa sezione fornisce suggerimenti e risorse che sono specifiche per RevoScaleR e altre opzioni in R. Microsoft

> [!TIP]
> Informazioni generali sull'ottimizzazione di R non sono compreso nell'ambito di questo articolo. Tuttavia, se è necessario rendere il codice più rapidamente, è consigliabile l'articolo più diffusi [The R Inferno](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf). Descrive costrutti di programmazione in R e i problemi comuni in linguaggio vivido e dettaglio e offre molti esempi specifici di tecniche di programmazione R.

### <a name="optimizations-for-revoscaler"></a>Ottimizzazioni per RevoScaleR

Molti algoritmi di RevoScaleR supportano i parametri per controllare la modalità di generazione del modello con training. Anche se la precisione e la correttezza del modello è importante, le prestazioni dell'algoritmo potrebbero essere altrettanto importante. Per ottenere il giusto equilibrio tra accuratezza e tempi di training, è possibile modificare i parametri per aumentare la velocità di calcolo e in molti casi, migliorare le prestazioni senza compromettere la precisione o la correttezza.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree` supporta il `maxDepth` parametro, che controlla la profondità dell'albero delle decisioni. Come `maxDepth` è aumentato, le prestazioni possono ridursi, pertanto è importante analizzare i vantaggi di aumento della profondità rispetto incide negativamente sulle prestazioni.

    È inoltre possibile controllare l'equilibrio tra tempo accuratezza complessità e la stima regolando parametri quali `maxNumBins`, `maxDepth`, `maxComplete`, e `maxSurrogate`. L'aumento della profondità oltre 10 o 15 può rendere il calcolo molto dispendioso.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    Provare a usare il `cube` argomento se la prima variabile dipendente della formula è una variabile di fattore.
    
    Quando `cube` è impostata su `TRUE`, la regressione viene eseguita utilizzando una funzione inversa partizionata, che potrebbe essere più veloce e Usa meno memoria rispetto al calcolo della regressione standard. Se la formula contiene un numero elevato di variabili, il miglioramento delle prestazioni può essere significativo.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    Usare il `cube` argomento se la prima variabile dipendente è una variabile di fattore.
    
    Quando `cube` è impostata su `TRUE`, l'algoritmo utilizza una funzione inversa partizionata, che potrebbe risultare più veloce e Usa meno memoria. Se la formula contiene un numero elevato di variabili, il miglioramento delle prestazioni può essere significativo.

Per altro materiale sussidiario sull'ottimizzazione di RevoScaleR, vedere questi articoli:

+ Articolo del supporto tecnico: [Le opzioni per rxDForest e rxDTree l'ottimizzazione delle prestazioni](https://support.microsoft.com/kb/3104235)

+ I metodi per il controllo modello rientrano in un modello di albero con Boosting: [Stima dei modelli con Boosting a gradienti Stocastica](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ Panoramica su come RevoScaleR Sposta ed elabora i dati: [Scrivere algoritmi personalizzati la suddivisione in blocchi in ScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ Modello di programmazione per RevoScaleR: [Gestione di thread in RevoScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ Riferimento alle funzioni per [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ Riferimento alle funzioni per [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>Usare MicrosoftML

È inoltre consigliabile valutare le nuove **MicrosoftML** pacchetto, che offre scalabilità algoritmi di apprendimento automatico che è possono usare i contesti di calcolo e le trasformazioni fornite da RevoScaleR.

+ [Introduzione a MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [Come scegliere un algoritmo di MicrosoftML](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Rendere operativa una soluzione con Microsoft R Server

Se lo scenario prevede una stima rapida basata usando un modello archiviato o l'integrazione di machine learning in un'applicazione, è possibile usare la [operazionalizzazione](https://docs.microsoft.com/r-server/what-is-operationalization) funzionalità di Microsoft R Server (precedentemente noto come DeployR).

+ Come un **esperto**, utilizzare il [pacchetto mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) condividere il codice R con altri computer e l'integrazione analitica R all'interno delle applicazioni web, desktop, mobili e dashboard: [Come pubblicare e gestire i servizi web di R in R Server](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ Come un **amministratore**, informazioni su come gestire i pacchetti, monitorare i nodi di web e i nodi di calcolo e controllare la sicurezza nei processi R: [Come interagire con e utilizzare i servizi web in R](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>Articoli di questa serie

[Le prestazioni di ottimizzazione per R - introduzione](sql-server-r-services-performance-tuning.md)

[Ottimizzazione delle prestazioni per R - configurazione SQL Server](sql-server-configuration-r-services.md)

[Ottimizzazione delle prestazioni per R - R ottimizzazione di codice e i dati](r-and-data-optimization-r-services.md)

[Ottimizzazione delle prestazioni - risultati case study](performance-case-study-r-services.md)
