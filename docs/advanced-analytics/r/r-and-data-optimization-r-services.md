---
title: Ottimizzazione delle prestazioni per l'ottimizzazione dei dati
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a8143bae69e85ecf0056dcb9433707a681a69077
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271889"
---
# <a name="performance-for-r-services---data-optimization"></a>Prestazioni per R Services-ottimizzazione dei dati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo è il terzo di una serie che descrive l'ottimizzazione delle prestazioni per R Services in base a due case study. Questo articolo illustra le ottimizzazioni delle prestazioni per gli script R o Python eseguiti in SQL Server. Vengono inoltre descritti i metodi che è possibile utilizzare per aggiornare il codice R, sia per migliorare le prestazioni che per evitare problemi noti.

## <a name="choosing-a-compute-context"></a>Scelta di un contesto di calcolo

In SQL Server 2016 e 2017 è possibile usare il contesto di calcolo **locale** o **SQL** quando si esegue lo script R o Python.

Quando si usa il contesto di calcolo **locale** , l'analisi viene eseguita nel computer e non nel server. Se pertanto si ricevono dati da SQL Server da usare nel codice, è necessario recuperare i dati in rete. Il calo di prestazioni riscontrato per questo trasferimento in rete dipende dalle dimensioni dei dati trasferiti, dalla velocità della rete e dagli eventuali altri trasferimenti in rete che si verificano nello stesso momento.

Quando si usa il **contesto di calcolo SQL Server**, il codice viene eseguito sul server. Se si ricevono dati da SQL Server, i dati devono essere locali rispetto al server che esegue l'analisi e pertanto non viene introdotto alcun sovraccarico di rete. Se è necessario importare dati da altre origini, provare a organizzare prima ETL.

Quando si usano set di dati di grandi dimensioni, è consigliabile usare sempre il contesto di calcolo SQL.

## <a name="factors"></a>Fattori

Il linguaggio R presenta il concetto di *fattori*, che rappresentano una variabile speciale per i dati categorici. I data scientist usano spesso variabili di fattore nella loro formula, perché la gestione di variabili categoriche come fattori garantisce che i dati vengano elaborati correttamente dalle funzioni di machine learning. Per ulteriori informazioni, vedere [R for Dummies: Variabili](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/)Factor.

Per impostazione predefinita, le variabili di fattore possono essere convertite da stringhe a numeri interi e viceversa per l'archiviazione o l'elaborazione. La funzione `data.frame` R gestisce tutte le stringhe come variabili di fattore, a meno che l'argomento *stringsAsFactors* non sia impostato su **false**. Ciò significa che le stringhe vengono convertite automaticamente in un numero intero per l'elaborazione e quindi mappate di nuovo alla stringa originale.

Se i dati di origine per i fattori vengono archiviati come Integer, le prestazioni possono risentirne, perché R converte i numeri interi del fattore in stringhe in fase di esecuzione, quindi esegue la conversione interna da stringa a intero.

Per evitare tali conversioni in fase di esecuzione, è consigliabile archiviare i valori come numeri interi nella tabella SQL Server e utilizzare l'argomento _colInfo_ per specificare i livelli per la colonna utilizzata come fattore. La maggior parte degli oggetti origine dati in RevoScaleR accetta il parametro _colInfo_. Utilizzare questo parametro per assegnare un nome alle variabili utilizzate dall'origine dati, specificarne il tipo e definire i livelli o le trasformazioni delle variabili sui valori della colonna.

Ad esempio, la chiamata di funzione R seguente ottiene i numeri interi 1, 2 e 3 da una tabella, ma esegue il mapping dei valori a un fattore con livelli "Apple", "Orange" e "banana".

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

Quando la colonna di origine contiene stringhe, è sempre più efficiente specificare i livelli in anticipo utilizzando il parametro _colInfo_ . Ad esempio, il codice R seguente considera le stringhe come fattori durante la lettura.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

Se non esiste alcuna differenza semantica nella generazione del modello, il secondo approccio può migliorare le prestazioni.

## <a name="data-transformations"></a>Trasformazioni di dati

I data scientist usano spesso le funzioni di trasformazione scritte in R nell'ambito dell'analisi. La funzione di trasformazione viene applicata a ogni riga recuperata dalla tabella. In SQL Server queste trasformazioni vengono applicate a tutte le righe recuperate in un batch, che richiede la comunicazione tra l'interprete R e il motore di analisi. Per eseguire la trasformazione, i dati vengono spostati da SQL al motore di analisi e quindi al processo dell'interprete R e viceversa.

Per questo motivo, l'uso delle trasformazioni come parte del codice R può avere un effetto negativo significativo sulle prestazioni dell'algoritmo, a seconda della quantità di dati interessati.

Prima di eseguire l'analisi, è più efficiente avere tutte le colonne necessarie nella tabella o nella vista ed evitare le trasformazioni durante il calcolo. Se non è possibile aggiungere altre colonne alle tabelle esistenti, è consigliabile creare un'altra tabella o vista con le colonne trasformate e usare una query appropriata per recuperare i dati.

## <a name="batch-row-reads"></a>Letture righe batch

Se si usa un'origine dati SQL Server (`RxSqlServerData`) nel codice, è consigliabile provare a usare il parametro _rowsPerRead_ per specificare le dimensioni del batch. Questo parametro definisce il numero di righe su cui viene eseguita la query e quindi inviato allo script esterno per l'elaborazione. In fase di esecuzione, l'algoritmo Visualizza solo il numero di righe specificato in ogni batch.

La possibilità di controllare la quantità di dati elaborati in un momento può aiutare a risolvere o evitare problemi. Se, ad esempio, il set di dati di input è molto ampio (include molte colonne) o se il set di dati contiene alcune colonne di grandi dimensioni (ad esempio testo libero), è possibile ridurre le dimensioni del batch per evitare il paging dei dati in memoria.

Per impostazione predefinita, il valore di questo parametro è impostato su 50000, per garantire prestazioni dignitose anche nei computer con memoria insufficiente. Se il server dispone di una quantità sufficiente di memoria disponibile, l'aumento di questo valore a 500.000 o pari a un milione può produrre prestazioni migliori, soprattutto per tabelle di grandi dimensioni.

I vantaggi dell'aumento delle dimensioni del batch diventano evidenti in un set di dati di grandi dimensioni e in un'attività che può essere eseguita in più processi. Tuttavia, l'aumento di questo valore non produce sempre i risultati migliori. Si consiglia di sperimentare i dati e l'algoritmo per determinare il valore ottimale.

## <a name="parallel-processing"></a>Elaborazione parallela

Per migliorare le prestazioni delle funzioni di analisi **RX** , è possibile sfruttare la capacità di SQL Server di eseguire attività in parallelo usando i core disponibili nel computer server.

Esistono due modi per ottenere la parallelizzazione con R in SQL Server:

-   **Usare \@Parallel.** Quando si usa la stored procedure `sp_execute_external_script` per eseguire uno script R, impostare il parametro `@parallel` su `1`. Questo è il metodo migliore se lo script R **non** usa le funzioni RevoScaleR, che hanno altri meccanismi di elaborazione. Se lo script usa funzioni RevoScaleR (in genere con prefisso "RX"), l'elaborazione parallela viene eseguita automaticamente e non è necessario impostare `@parallel` in modo esplicito su. `1`

    Se lo script R può essere parallelo e se la query SQL può essere eseguita in parallelo, il motore di database crea più processi paralleli. Il numero massimo di processi che è possibile creare è uguale all'impostazione **max degree of parallelism** (MAXDOP) per l'istanza di. Tutti i processi eseguono quindi lo stesso script, ma ricevono solo una parte dei dati.
    
    Questo metodo non è pertanto utile per gli script che devono visualizzare tutti i dati, ad esempio durante il training di un modello. Tuttavia, è utile quando si eseguono attività come la stima in batch in parallelo. Per altre informazioni sull'uso del parallelismo `sp_execute_external_script`con, vedere la sezione **suggerimenti avanzati: elaborazione parallela** dell' [uso del codice R in Transact-SQL](../tutorials/quickstart-r-create-script.md).

-   **Usare numTasks = 1.** Quando si usano funzioni **RX** in un contesto di calcolo SQL Server, impostare il valore del parametro _numTasks_ sul numero di processi che si desidera creare. Il numero di processi creati non può mai essere maggiore di **MAXDOP**; Tuttavia, il numero effettivo di processi creati è determinato dal motore di database e può essere minore di quello richiesto.

    Se lo script R può essere eseguito in parallelo e se la query SQL può essere eseguita in parallelo, SQL Server crea più processi paralleli quando si eseguono le funzioni RX. Il numero effettivo di processi creati dipende da diversi fattori, ad esempio la governance delle risorse, l'utilizzo corrente delle risorse, altre sessioni e il piano di esecuzione della query per la query usata con lo script R.

## <a name="query-parallelization"></a>Parallelizzazione delle query

In Microsoft R è possibile usare SQL Server origini dati definendo i dati come oggetto origine dati RxSqlServerData.

Crea un'origine dati basata su un'intera tabella o vista:

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

Crea un'origine dati basata su una query SQL:

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> Se viene specificata una tabella nell'origine dati anziché in una query, R Services USA l'euristica interna per determinare le colonne necessarie da recuperare dalla tabella. Tuttavia, è improbabile che questo approccio provochi l'esecuzione parallela.

Per garantire che i dati possano essere analizzati in parallelo, la query utilizzata per recuperare i dati deve essere incorniciata in modo tale che il motore di database possa creare un piano di query parallele. Se il codice o l'algoritmo utilizza volumi elevati di dati, verificare che la query specificata `RxSqlServerData` sia ottimizzata per l'esecuzione parallela. Una query che non implica un piano di esecuzione parallela può comportare un singolo processo per il calcolo.

Se è necessario usare set di impostazioni di grandi dimensioni, usare Management Studio o un altro analizzatore di query SQL prima di eseguire il codice R, per analizzare il piano di esecuzione. Eseguire quindi le operazioni consigliate per migliorare le prestazioni della query. Ad esempio, un indice mancante in una tabella può influire sul tempo impiegato per eseguire una query. Per altre informazioni, vedere [monitorare e ottimizzare le prestazioni](../../relational-databases/performance/monitor-and-tune-for-performance.md).

Un altro errore comune che può influire sulle prestazioni è che una query recupera più colonne rispetto a quelle richieste. Se, ad esempio, una formula è basata solo su tre colonne, ma la tabella di origine include 30 colonne, si stanno muovendo inutilmente i dati.

 + Evitare di `SELECT *`usare.
 + Esaminare le colonne nel set di dati e identificare solo quelle necessarie per l'analisi
 + Rimuovere dalle query tutte le colonne che contengono tipi di dati incompatibili con il codice R, ad esempio GUID e rowguid
 + Verifica i formati di data e ora non supportati
 + Anziché caricare una tabella, creare una vista che seleziona determinati valori o esegue il cast delle colonne per evitare errori di conversione

## <a name="optimizing-the-machine-learning-algorithm"></a>Ottimizzazione dell'algoritmo di Machine Learning

Questa sezione fornisce suggerimenti e risorse varie specifiche per RevoScaleR e altre opzioni in Microsoft R.

> [!TIP]
> Una discussione generale sull'ottimizzazione di R non rientra nell'ambito di questo articolo. Tuttavia, se è necessario velocizzare il codice, è consigliabile usare l'articolo di [R inferno](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf). Vengono illustrati i costrutti di programmazione in R e gli inconvenienti comuni nel linguaggio e nei dettagli vividi e vengono forniti molti esempi specifici di tecniche di programmazione R.

### <a name="optimizations-for-revoscaler"></a>Ottimizzazioni per RevoScaleR

Molti algoritmi RevoScaleR supportano i parametri per controllare la modalità di generazione del modello sottoposto a training. Sebbene l'accuratezza e la correttezza del modello siano importanti, le prestazioni dell'algoritmo potrebbero essere ugualmente importanti. Per ottenere il giusto equilibrio tra precisione e tempo di training, è possibile modificare i parametri per aumentare la velocità di calcolo e, in molti casi, migliorare le prestazioni senza ridurne l'accuratezza o la correttezza.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree`supporta il `maxDepth` parametro, che controlla la profondità dell'albero delle decisioni. Così `maxDepth` come è aumentata, le prestazioni possono peggiorare, quindi è importante analizzare i vantaggi dell'aumento della profondità rispetto alle prestazioni.

    È inoltre possibile controllare il saldo tra la complessità temporale e l'accuratezza della stima regolando `maxNumBins`parametri `maxDepth`quali `maxComplete`,, `maxSurrogate`e. L'aumento della profondità oltre 10 o 15 può rendere il calcolo molto dispendioso.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    Provare a usare `cube` l'argomento se la prima variabile dipendente nella formula è una variabile di fattore.
    
    Quando `cube` è impostato su `TRUE`, la regressione viene eseguita usando un inverso partizionato, che potrebbe essere più veloce e usare meno memoria rispetto al calcolo della regressione standard. Se la formula contiene un numero elevato di variabili, il miglioramento delle prestazioni può essere significativo.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    Usare l' `cube` argomento se la prima variabile dipendente è una variabile di fattore.
    
    Quando `cube` è impostato su `TRUE`, l'algoritmo usa un inverso partizionato, che potrebbe essere più veloce e usare meno memoria. Se la formula contiene un numero elevato di variabili, il miglioramento delle prestazioni può essere significativo.

Per altre indicazioni sull'ottimizzazione di RevoScaleR, vedere questi articoli:

+ Articolo del supporto tecnico: [Opzioni di ottimizzazione delle prestazioni per rxDForest e rxDTree](https://support.microsoft.com/kb/3104235)

+ Metodi per il controllo dell'adattamento del modello in un modello di albero con boosting: [Stima di modelli con boosting a gradienti stocastici](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ Panoramica del modo in cui RevoScaleR sposta ed elabora i dati: [Scrivere algoritmi di suddivisione in blocchi personalizzati in scaler](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ Modello di programmazione per RevoScaleR: [Gestione dei thread in RevoScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ Guida di riferimento alle funzioni per [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ Guida di riferimento alle funzioni per [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>Usare MicrosoftML

Si consiglia inoltre di esaminare il nuovo pacchetto **MicrosoftML** , che fornisce algoritmi di apprendimento automatico scalabili che possono usare i contesti di calcolo e le trasformazioni fornite da RevoScaleR.

+ [Introduzione a MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [Come scegliere un algoritmo MicrosoftML](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Rendere operativo una soluzione usando Microsoft R Server

Se lo scenario prevede una stima rapida usando un modello archiviato o l'integrazione di Machine Learning in un'applicazione, è possibile usare le funzionalità di [operatività](https://docs.microsoft.com/r-server/what-is-operationalization) in Microsoft R Server (precedentemente noto come deployr).

+ Come **Data Scientist**, usare il [pacchetto mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) per condividere il codice r con altri computer e integrare r Analytics all'interno di applicazioni Web, desktop, per dispositivi mobili e Dashboard: [Come pubblicare e gestire i servizi Web R in R Server](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ Come **amministratore**, informazioni su come gestire i pacchetti, monitorare i nodi Web e i nodi di calcolo e controllare la sicurezza nei processi R: [Come interagire con e utilizzare i servizi Web in R](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>Articoli della serie

[Ottimizzazione delle prestazioni per R-introduzione](sql-server-r-services-performance-tuning.md)

[Ottimizzazione delle prestazioni per la configurazione di R SQL Server](sql-server-configuration-r-services.md)

[Ottimizzazione delle prestazioni per il codice R-R e l'ottimizzazione dei dati](r-and-data-optimization-r-services.md)

[Ottimizzazione delle prestazioni-case study risultati](performance-case-study-r-services.md)
