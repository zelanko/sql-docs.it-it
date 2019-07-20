---
title: Configurazione di SQL Server (R Services)
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: feb59ac529b0a66603d9e8b901e9755588ac0379
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344846"
---
# <a name="sql-server-configuration-for-use-with-r"></a>Configurazione SQL Server per l'uso con R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo è il secondo di una serie che descrive l'ottimizzazione delle prestazioni per R Services in base a due case study.  In questo articolo vengono fornite informazioni aggiuntive sull'hardware e sulla configurazione di rete del computer utilizzato per eseguire R Services per SQL Server. Sono inoltre contenute informazioni sui modi per configurare l'istanza SQL Server, il database o le tabelle utilizzate in una soluzione. Poiché l'utilizzo di NUMA in SQL Server sfoca la linea tra le ottimizzazioni dell'hardware e del database, una terza sezione illustra in modo dettagliato la affinitization della CPU e la governance delle risorse.

> [!TIP]
> Se non si ha familiarità con SQL Server, è consigliabile consultare anche la Guida all'ottimizzazione delle prestazioni SQL Server: [Monitorare e ottimizzare le prestazioni](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance).

## <a name="hardware-optimization"></a>Ottimizzazione hardware

L'ottimizzazione del computer server è importante per assicurarsi di disporre delle risorse per l'esecuzione di script esterni. Quando le risorse sono limitate, è possibile che vengano visualizzati sintomi simili ai seguenti:

- L'esecuzione del processo viene posticipata o annullata per classificare in ordine di priorità altre operazioni del database
- Errore "quota superata" che causa la terminazione di uno script R senza completamento
- Dati caricati nella memoria R troncati, per risultati incompleti

### <a name="memory"></a>Memoria

La quantità di memoria disponibile nel computer può avere un notevole impatto sulle prestazioni di algoritmi analitici avanzati. Una memoria insufficiente potrebbe influire sul grado di parallelismo quando si usa il contesto di calcolo SQL. Può anche influire sulle dimensioni del blocco (righe per operazione di lettura) che possono essere elaborate e sul numero di sessioni simultanee supportato.

È consigliabile un minimo di 32 GB. Se sono disponibili più di 32 GB, è possibile configurare l'origine dati SQL in modo che utilizzi più righe in ogni operazione di lettura per migliorare le prestazioni.

È inoltre possibile gestire la memoria utilizzata dall'istanza di. Per impostazione predefinita, quando viene allocata la memoria SQL Server viene assegnata la priorità ai processi di script esterni. In un'installazione predefinita di R Services, solo il 20% della memoria disponibile viene allocato a R.

Questa operazione non è in genere sufficiente per le attività data science, ma non si desidera che il server di memoria venga esaurito. È necessario sperimentare e ottimizzare l'allocazione di memoria tra il motore di database, i servizi correlati e gli script esterni, con la consapevolezza che la configurazione ottimale varia in base al caso.

Per il modello di corrispondenza del resume, l'uso di script esterni era elevato e non erano in esecuzione altri servizi del motore di database. Pertanto, le risorse allocate agli script esterni sono state aumentate al 70%, che rappresenta la configurazione migliore per le prestazioni dello script.

### <a name="power-options"></a>Opzioni risparmio energia

Nel sistema operativo Windows, è consigliabile usare l'opzione di risparmio energia a **prestazioni elevate** . L'uso di un'impostazione di risparmio energia diversa comporta una riduzione o una riduzione delle prestazioni quando si usa SQL Server.

### <a name="disk-io"></a>I/O su disco

I processi di training e previsione che usano R Services sono associati a i/o intrinseci e dipendono dalla velocità dei dischi in cui è archiviato il database. Le unità più veloci, ad esempio unità SSD (Solid-State Drive), possono essere utili.

Sull'I/O su disco influiscono anche altre applicazioni che accedono al disco, ad esempio le operazioni di lettura su un database da parte di altri client. Le prestazioni di I/O su disco dipendono anche dalle impostazioni nel file system in uso, come le dimensioni dei blocchi usate dal file system.

Se sono disponibili più unità, archiviare i database in un'unità diversa da SQL Server in modo che le richieste per il motore di database non raggiungano lo stesso disco delle richieste di dati archiviati nel database.

L'I/O su disco può avere un notevole impatto sulle prestazioni durante l'esecuzione di funzioni analitiche RevoScaleR che usano più iterazioni durante il training. `rxLogit`Ad esempio `rxDTree` ,,`rxBTrees` , e utilizzano più iterazioni. `rxDForest` Quando l'origine dati è SQL Server, questi algoritmi utilizzano file temporanei ottimizzati per l'acquisizione dei dati. Questi file vengono automaticamente eliminati al termine della sessione. La presenza di un disco a prestazioni elevate per le operazioni di lettura/scrittura può migliorare significativamente il tempo totale trascorso per questi algoritmi.

> [!NOTE]
> Le versioni precedenti di R Services richiedevano il supporto del nome file 8,3 nei sistemi operativi Windows. Questa restrizione è stata revocata dopo il Service Pack 1. Tuttavia, è possibile utilizzare fsutil. exe per determinare se un'unità supporta i nomi file 8,3 o per abilitare il supporto in caso contrario.

### <a name="paging-file"></a>File di paging

Il sistema operativo Windows usa un file di paging per gestire i dump di arresto anomalo e per archiviare pagine di memoria virtuale. Se si nota un paging eccessivo, provare ad aumentare la memoria fisica nel computer. Benché la disponibilità di più memoria fisica non elimina il paging, riduce la necessità di paging.

Anche la velocità del disco in cui è archiviato il file di paging può influire sulle prestazioni. L'archiviazione del file di paging in un'unità SSD o l'uso di più file di paging su più SSD può migliorare le prestazioni.

Per informazioni sul dimensionamento del file di paging, vedere [come determinare le dimensioni appropriate del file di paging per le versioni di Windows a 64 bit](https://support.microsoft.com/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Ottimizzazioni a livello di istanza o di database

L'ottimizzazione dell'istanza di SQL Server è la chiave per l'esecuzione efficiente di script esterni.

> [!NOTE]
> Le impostazioni ottimali variano a seconda delle dimensioni e del tipo di dati, il numero di colonne utilizzate per il punteggio o il training di un modello.
> 
> È possibile esaminare i risultati di ottimizzazioni specifiche nell'articolo finale: [Ottimizzazione delle prestazioni-case study risultati](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> Per gli script di esempio, vedere il [repository GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)separato.

### <a name="table-compression"></a>Compressione di tabelle

Le prestazioni di i/o possono spesso essere migliorate usando la compressione o un archivio dati a colonne. In genere, i dati vengono spesso ripetuti in più colonne all'interno di una tabella, pertanto l'uso di un columnstore sfrutta i vantaggi di queste ripetizioni quando si comprimono i dati.

Un columnstore potrebbe non essere efficiente se sono presenti numerosi inserimenti nella tabella, ma è una scelta ottimale se i dati sono statici o cambiano solo raramente. Se un archivio a colonne non è appropriato, è possibile abilitare la compressione in una tabella principale di righe per migliorare l'I/O.

Per altre informazioni, vedere i documenti seguenti:

+ [Compressione dei dati](../../relational-databases/data-compression/data-compression.md)

+ [Abilitare la compressione in una tabella o un indice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Guida agli indici columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Tabelle con ottimizzazione per la memoria

Attualmente la memoria non è più un problema per i computer moderni. Poiché le specifiche hardware continuano a migliorare, è relativamente semplice ottenere RAM con valori validi. Allo stesso tempo, tuttavia, i dati vengono prodotti più rapidamente che mai e i dati devono essere elaborati con bassa latenza.

Le tabelle con ottimizzazione per la memoria rappresentano una soluzione, perché sfruttano la grande quantità di memoria disponibile nei computer avanzati per risolvere il problema del Big Data. Le tabelle con ottimizzazione per la memoria risiedono principalmente in memoria, in modo da consentire la lettura e la scrittura dei dati in memoria. Per la durabilità, una seconda copia della tabella viene mantenuta su disco e i dati vengono letti dal disco solo durante il recupero del database.

Se è necessario leggere e scrivere frequentemente nelle tabelle, le tabelle ottimizzate per la memoria possono essere utili con scalabilità elevata e bassa latenza.  Nello scenario Resume-matching, l'uso delle tabelle ottimizzate per la memoria ci ha consentito di leggere tutte le funzionalità di ripresa dal database e di archiviarle nella memoria principale, in modo che corrispondano a nuove aperture di processi. Questa operazione ha ridotto notevolmente l'i/o del disco.

Grazie a una tabella ottimizzata per la memoria nel processo di scrittura di stime nel database da più batch simultanei, sono stati apportati ulteriori miglioramenti alle prestazioni. L'utilizzo di tabelle ottimizzate per la memoria in SQL Server abilitata a bassa latenza per letture e scritture di tabelle.

L'esperienza è stata anche senza problemi durante lo sviluppo. Le tabelle durevoli con ottimizzazione per la memoria sono state create nello stesso momento in cui è stato creato il database. Lo sviluppo utilizza pertanto lo stesso flusso di lavoro indipendentemente dalla posizione in cui sono stati archiviati i dati.

### <a name="processor"></a>Processore

SQL Server possibile eseguire attività in parallelo usando i core disponibili nel computer. maggiore è il numero di core disponibili, migliori saranno le prestazioni. Mentre l'aumento del numero di core potrebbe non essere utile per le operazioni associate a IO, gli algoritmi associati alla CPU traggono vantaggio da CPU più veloci con molti core.

Poiché il server viene normalmente usato da più utenti contemporaneamente, l'amministratore del database deve determinare il numero ideale di core necessari per supportare i calcoli di picco del carico di lavoro.

### <a name="resource-governance"></a>Governance delle risorse

Nelle edizioni che supportano Resource Governor, è possibile utilizzare i pool di risorse per specificare che alcuni carichi di lavoro vengono allocati in un certo numero di CPU. È anche possibile gestire la quantità di memoria allocata per carichi di lavoro specifici.

La governance delle risorse in SQL Server consente di centralizzare il monitoraggio e il controllo delle varie risorse usate da SQL Server e da R. Ad esempio, è possibile allocare metà della memoria disponibile per il motore di database, in modo da garantire che i servizi di base possano sempre essere eseguiti nonostante carichi di lavoro più pesanti temporanei.

Il valore predefinito per l'utilizzo della memoria da parte di script esterni è limitato al 20% della memoria totale disponibile per SQL Server stesso. Questo limite viene applicato per impostazione predefinita per garantire che tutte le attività che si basano sul server di database non siano influenzate gravemente dai processi R con esecuzione prolungata. Tuttavia, questi limiti possono essere modificati dall'amministratore del database. In molti casi, il limite del 20% non è adeguato per supportare carichi di lavoro di Machine Learning gravi.

Le opzioni di configurazione supportate sono **MAX_CPU_PERCENT**, **max_memory_percent**e **MAX_PROCESSES**. Per visualizzare le impostazioni correnti, usare questa istruzione:`SELECT * FROM sys.resource_governor_external_resource_pools`

-  Se il server viene usato principalmente per R Services, può essere utile aumentare MAX_CPU_PERCENT al 40% o 60%.

-  Se molte sessioni R devono usare lo stesso server allo stesso tempo, tutte e tre le impostazioni devono essere aumentate.

Per modificare i valori delle risorse allocate, usare le istruzioni T-SQL.

+ Questa istruzione imposta l'utilizzo della memoria su 40%:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ Questa istruzione imposta tutti e tre i valori configurabili:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Se si modifica un'impostazione della memoria, della CPU o del processo massimo e si desidera applicare immediatamente le impostazioni, eseguire l'istruzione seguente:`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Soft-NUMA, hardware NUMA e affinità CPU

Quando si usa SQL Server come contesto di calcolo, è possibile a volte ottenere prestazioni migliori ottimizzando le impostazioni relative a NUMA e affinità processori. 

I sistemi con _hardware NUMA_ hanno più di un bus di sistema, ognuno dei quali serve un piccolo set di processori. Ogni CPU può accedere alla memoria associata ad altri gruppi in modo coerente. Ogni gruppo viene denominato nodo NUMA. Se si dispone di hardware NUMA, è possibile che questo sia configurato in modo da utilizzare memoria interleaved anziché la modalità NUMA. In tal caso, Windows e quindi SQL Server non lo riconosceranno come NUMA. 

È possibile eseguire la query seguente per trovare il numero di nodi di memoria disponibili per SQL Server:

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Se la query restituisce un singolo nodo di memoria (nodo 0), non si dispone di hardware NUMA o l'hardware è configurato come interfoliazione (non NUMA). SQL Server inoltre ignora l'hardware NUMA quando ci sono quattro o meno CPU o se almeno un nodo dispone di una sola CPU.

Se il computer dispone di più processori ma non di hardware-NUMA, è anche possibile utilizzare [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) per suddividere le CPU in gruppi più piccoli.  In entrambi SQL Server 2016 e SQL Server 2017, la funzionalità Soft-NUMA viene abilitata automaticamente all'avvio del servizio di SQL Server.

Quando è abilitata la funzionalità Soft-NUMA, SQL Server gestisce automaticamente i nodi. Tuttavia, per ottimizzare i carichi di lavoro specifici, è possibile disabilitare l' _affinità flessibile_ e configurare manualmente l'affinità di CPU per i nodi soft NUMA. In questo modo è possibile ottenere un maggiore controllo sui carichi di lavoro assegnati ai nodi, in particolare se si utilizza un'edizione di SQL Server che supporta la governance delle risorse. Specificando l'affinità di CPU e allineando i pool di risorse con gruppi di CPU, è possibile ridurre la latenza e assicurarsi che i processi correlati vengano eseguiti nello stesso nodo NUMA.

Il processo generale per la configurazione dell'affinità soft-NUMA e CPU per il supporto dei carichi di lavoro R è il seguente:

1. Abilita soft-NUMA, se disponibile
2. Definire l'affinità processori
3. Creare pool di risorse per i processi esterni, usando [Resource Governor](../r/resource-governance-for-r-services.md)
4. Assegnare i [gruppi del carico di lavoro](../../relational-databases/resource-governor/resource-governor-workload-group.md) a gruppi di affinità specifici

Per informazioni dettagliate, incluso il codice di esempio, vedere questa esercitazione: [Suggerimenti e trucchi per l'ottimizzazione di SQL (ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Altre risorse:**

+ [Soft-NUMA in SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Come eseguire il mapping di nodi soft-NUMA alle CPU

## <a name="task-specific-optimizations"></a>Ottimizzazioni specifiche delle attività

Questa sezione riepiloga i metodi adottati in questi casi di studio e in altri test per l'ottimizzazione di carichi di lavoro di Machine Learning specifici. I carichi di lavoro comuni includono il training del modello, l'estrazione delle funzionalità e la progettazione delle funzionalità e vari scenari di assegnazione dei punteggi: singola riga, batch di piccole dimensioni e batch di grandi dimensioni.

### <a name="feature-engineering"></a>Progettazione delle funzioni

Un punto problematico con R è che in genere viene elaborato su una singola CPU. Si tratta di un importante collo di bottiglia delle prestazioni per molte attività, in particolare per la progettazione di funzionalità. Nella soluzione Resume-matching, l'attività di progettazione delle funzioni crea da solo le funzionalità di prodotto incrociato 2.500 che devono essere combinate con le funzionalità di 100 originali. Questa attività richiederebbe una quantità di tempo significativa se tutti gli elementi sono stati eseguiti su una singola CPU.

Esistono diversi modi per migliorare le prestazioni della progettazione delle funzionalità. È possibile ottimizzare il codice R e continuare l'estrazione delle funzionalità all'interno del processo di modellazione oppure spostare il processo di progettazione delle funzionalità in SQL.

- Uso di R. È possibile definire una funzione e passarla come argomento a [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) durante il training. Se il modello supporta l'elaborazione parallela, l'attività di progettazione delle funzionalità può essere elaborata utilizzando più CPU. Con questo approccio, il team data science ha osservato un miglioramento delle prestazioni del 16% in termini di tempo di assegnazione dei punteggi. Questo approccio richiede tuttavia un modello che supporti la parallelizzazione e una query che può essere eseguita usando un piano parallelo.

- Usare R con un contesto di calcolo SQL. In un ambiente multiprocessore con risorse isolate disponibili per l'esecuzione di batch distinti, è possibile ottenere una maggiore efficienza isolando le query SQL usate per ogni batch, estrarre i dati dalle tabelle e vincolare i dati nello stesso gruppo di carico di lavoro. I metodi usati per isolare i batch includono il partizionamento e l'uso di PowerShell per eseguire query separate in parallelo.

- Esecuzione parallela ad hoc: In un contesto di calcolo SQL Server è possibile fare affidamento sul motore di database SQL per applicare l'esecuzione parallela, se possibile, e se tale opzione risulta più efficiente.

- Usare T-SQL in un processo conteggi separato. Il precalcolo dei dati delle funzionalità con SQL è in genere più rapido.

### <a name="prediction-scoring-in-parallel"></a>Stima (Punteggio) in parallelo

Uno dei vantaggi di SQL Server è la possibilità di gestire un volume elevato di righe in parallelo. Nessun altro vantaggio è così contrassegnato come per l'assegnazione dei punteggi. In genere, il modello non richiede l'accesso a tutti i dati per il punteggio, quindi è possibile partizionare i dati di input, con ogni gruppo del carico di lavoro che elabora un'attività.

È anche possibile inviare i dati di input come una singola query, quindi SQL Server analizza la query. Se è possibile creare un piano di query parallele per i dati di input, vengono automaticamente partizionati i dati assegnati ai nodi e vengono eseguiti anche i join e le aggregazioni necessari in parallelo.

Per informazioni dettagliate su come definire un stored procedure da usare per l'assegnazione dei punteggi, vedere il progetto di esempio su [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) e cercare il file "step5_score_for_matching. SQL". Lo script di esempio consente inoltre di tenere traccia delle ore di inizio e di fine della query e di scrivere l'ora nella console SQL, in modo da poter valutare le prestazioni.

### <a name="concurrent-scoring-using-resource-groups"></a>Punteggio simultaneo con i gruppi di risorse

Per scalare il problema di assegnazione dei punteggi, è consigliabile adottare l'approccio di riduzione della mappa in cui milioni di elementi sono divisi in più batch. Quindi, vengono eseguiti più processi di assegnazione dei punteggi simultaneamente. In questo Framework, i batch vengono elaborati in set di CPU diversi e i risultati vengono raccolti e scritti di nuovo nel database.

Si tratta dell'approccio usato nello scenario di riattivazione delle corrispondenze. Tuttavia, la governance delle risorse in SQL Server è essenziale per l'implementazione di questo approccio. Impostando i gruppi del carico di lavoro per i processi di script esterni, è possibile indirizzare i processi di assegnazione dei punteggi a diversi gruppi di processori e ottenere velocità effettiva più veloce

La governance delle risorse può anche contribuire a suddividere le risorse disponibili sul server (CPU e memoria) per ridurre al minimo la concorrenza del carico di lavoro. È possibile configurare le funzioni di classificazione per distinguere tra tipi diversi di processi R. ad esempio, è possibile decidere che l'assegnazione dei punteggi chiamata da un'applicazione abbia sempre la priorità, mentre i processi di ripetizione del training hanno priorità bassa. Questo isolamento delle risorse può migliorare potenzialmente il tempo di esecuzione e offrire prestazioni più prevedibili.

### <a name="concurrent-scoring-using-powershell"></a>Punteggio simultaneo con PowerShell

Se si decide di partizionare manualmente i dati, è possibile usare gli script di PowerShell per eseguire più attività di assegnazione di punteggi simultanee. A tale scopo, usare il cmdlet Invoke-SqlCmd e avviare le attività di assegnazione dei punteggi in parallelo.

Nello scenario Resume-matching, la concorrenza è stata progettata come segue:

- 20 processori divisi in quattro gruppi di cinque CPU ciascuno. Ogni gruppo di CPU si trova nello stesso nodo NUMA.

- Il numero massimo di batch simultanei è stato impostato su otto.

- Ogni gruppo del carico di lavoro deve gestire due attività di assegnazione dei punteggi. Al termine della lettura dei dati da parte di un'attività, l'altra attività può iniziare a leggere i dati dal database.

Per visualizzare gli script di PowerShell per questo scenario, aprire il file Experiment. ps1 nel [progetto GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips).

### <a name="storing-models-for-prediction"></a>Archiviazione di modelli per la stima

Al termine del training e della valutazione ed è stato selezionato un modello migliore, è consigliabile archiviare il modello nel database in modo che sia disponibile per le stime. Il caricamento del modello pre-calcolato dal database per la stima è efficiente, perché SQL Server machine learning usa algoritmi di serializzazione speciali per archiviare e caricare i modelli quando si esegue il passaggio tra R e il database.

> [!TIP]
> In SQL Server 2017, è possibile usare la funzione PREDICT per eseguire il punteggio anche se R non è installato nel server. Sono supportati i tipi di modelli limitati dal pacchetto RevoScaleR.

Tuttavia, a seconda dell'algoritmo utilizzato, alcuni modelli possono avere dimensioni molto elevate, soprattutto quando vengono sottoposti a training su un set di dati di grandi dimensioni. Ad esempio, gli algoritmi come **LM** o **GLM** generano una grande quantità di dati di riepilogo insieme alle regole. Poiché esistono limiti alla dimensione di un modello che può essere archiviato in una colonna varbinary, è consigliabile eliminare gli artefatti superflui dal modello prima di archiviare il modello nel database per la produzione.

## <a name="articles-in-this-series"></a>Articoli della serie

[Ottimizzazione delle prestazioni per R-introduzione](../r/sql-server-r-services-performance-tuning.md)

[Ottimizzazione delle prestazioni per la configurazione di R SQL Server](../r/sql-server-configuration-r-services.md)

[Ottimizzazione delle prestazioni per il codice R-R e l'ottimizzazione dei dati](../r/r-and-data-optimization-r-services.md)

[Ottimizzazione delle prestazioni-case study risultati](../r/performance-case-study-r-services.md)
