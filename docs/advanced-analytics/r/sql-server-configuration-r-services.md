---
title: Configurazione per l'uso con R
description: Questo articolo include linee guida per la configurazione di hardware e rete del computer usato per eseguire R Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7d18661fadb12167fd0a443758cced1188401750
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727342"
---
# <a name="sql-server-configuration-for-use-with-r"></a>Configurazione di SQL Server per l'uso con R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo è il secondo di una serie che descrive l'ottimizzazione delle prestazioni per R Services in base a due case study.  Questo articolo include linee guida per la configurazione di hardware e rete del computer usato per eseguire R Services per SQL Server. Sono inoltre disponibili informazioni sui modi per configurare l'istanza, il database o le tabelle di SQL Server usate in una soluzione. Poiché l'uso di NUMA in SQL Server rende meno netta la distinzione tra le ottimizzazioni dell'hardware e del database, una terza sezione illustra in modo dettagliato la definizione dell'affinità della CPU e la governance delle risorse.

> [!TIP]
> Se non si ha familiarità con SQL Server, è consigliabile consultare anche la guida all'ottimizzazione delle prestazioni di SQL Server: [Monitoraggio e ottimizzazione delle prestazioni](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance).

## <a name="hardware-optimization"></a>Ottimizzazione dell'hardware

L'ottimizzazione del computer server è importante per assicurarsi di disporre delle risorse per l'esecuzione di script esterni. Quando le risorse sono limitate, è possibile che si riscontrino sintomi come i seguenti:

- L'esecuzione del processo viene posticipata o annullata per dare la priorità ad altre operazioni del database
- Errore di quota superata, che causa la terminazione dello script R senza completamento
- Troncamento dei dati caricati nella memoria R, per risultati incompleti

### <a name="memory"></a>Memoria

La quantità di memoria disponibile nel computer può avere un notevole impatto sulle prestazioni di algoritmi analitici avanzati. Una memoria insufficiente potrebbe influire sul grado di parallelismo quando si usa il contesto di calcolo SQL. Può anche influire sulle dimensioni del blocco (righe per operazione di lettura) che possono essere elaborate e sul numero di sessioni simultanee supportato.

È altamente consigliato un minimo di 32 GB. Se sono disponibili più di 32 GB, è possibile configurare l'origine dati SQL per l'uso di più righe in ogni operazione di scrittura per migliorare le prestazioni.

È anche possibile gestire la memoria usata dall'istanza. Per impostazione predefinita, nell'allocazione della memoria SQL Server ha la priorità rispetto ai processi di script esterni. In un'installazione predefinita di R Services, solo il 20% della memoria disponibile viene allocato a R.

Si tratta di una quantità in genere insufficiente per le attività di data science, ma si vuole anche evitare che la memoria per SQL Server sia troppo scarsa. È necessario sperimentare e mettere a punto l'allocazione di memoria tra il motore di database, i servizi correlati e gli script esterni, tenendo presente che la configurazione ottimale varia di caso in caso.

Per il modello per l'individuazione dei curricula corrispondenti, l'uso di script esterni è elevato e non sono in esecuzione altri servizi del motore di database. Pertanto, le risorse allocate agli script esterni vengono aumentate al 70%, che rappresenta la configurazione ottimale per le prestazioni degli script.

### <a name="power-options"></a>Opzioni di risparmio energia

Nel sistema operativo Windows è consigliabile usare l'opzione di risparmio energia **Prestazioni elevate**. L'uso di un'impostazione diversa causa prestazioni ridotte o non uniformi quando si usa SQL Server.

### <a name="disk-io"></a>I/O su disco

I processi di training e stima che usano R Services sono associati intrinsecamente all'I/O e dipendono dalla velocità dei dischi in cui è archiviato il database. Possono essere utili unità più veloci, come le unità SSD.

Sull'I/O su disco influiscono anche altre applicazioni che accedono al disco, ad esempio le operazioni di lettura su un database da parte di altri client. Le prestazioni di I/O su disco dipendono anche dalle impostazioni nel file system in uso, come le dimensioni dei blocchi usate dal file system.

Se sono disponibili più unità, archiviare i database in un'unità diversa da SQL Server, in modo che le richieste per il motore di database non raggiungano lo stesso disco delle richieste di dati archiviati nel database.

L'I/O su disco può avere un notevole impatto sulle prestazioni durante l'esecuzione di funzioni analitiche RevoScaleR che usano più iterazioni durante il training. Ad esempio, `rxLogit`, `rxDTree`, `rxDForest` e `rxBTrees` usano tutti più iterazioni. Quando l'origine dati è SQL Server, questi algoritmi usano file temporanei ottimizzati per l'acquisizione dei dati. Questi file vengono automaticamente eliminati al termine della sessione. La disponibilità di un disco ad alte prestazioni per operazioni di lettura/scrittura può migliorare significativamente il tempo trascorso totale per questi algoritmi.

> [!NOTE]
> Le versioni precedenti di R Services richiedevano il supporto dei nomi di file in formato 8.3 nei sistemi operativi Windows. Questa restrizione è stata eliminata dopo il Service Pack 1. È comunque possibile usare fsutil.exe per determinare se un'unità supporta nomi di file 8.3 o per abilitare il supporto in caso contrario.

### <a name="paging-file"></a>File di paging

Il sistema operativo Windows usa un file di paging per gestire i dump di arresto anomalo e per archiviare pagine di memoria virtuale. Se si nota un paging eccessivo, provare ad aumentare la memoria fisica nel computer. Benché la disponibilità di più memoria fisica non elimina il paging, riduce la necessità di paging.

Anche la velocità del disco in cui è archiviato il file di paging può influire sulle prestazioni. L'archiviazione del file di paging in un'unità SSD o l'uso di più file di paging su più SSD può migliorare le prestazioni.

Per informazioni sull'impostazione delle dimensioni del file di paging, vedere [Come determinare le dimensioni appropriate del file di paging per le versioni a 64 bit di Windows](https://support.microsoft.com/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Ottimizzazioni a livello di istanza o di database

L'ottimizzazione dell'istanza di SQL Server è la chiave per l'esecuzione efficiente di script esterni.

> [!NOTE]
> Le impostazioni ottimali variano a seconda delle dimensioni e del tipo di dati, nonché del numero di colonne usate per l'assegnazione dei punteggi o il training di un modello.
> 
> È possibile esaminare i risultati di ottimizzazioni specifiche nell'articolo finale: [Ottimizzazione delle prestazioni - Risultati dei case study](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> Per gli script di esempio, vedere il [repository GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) separato.

### <a name="table-compression"></a>Compressione di tabelle

Spesso le prestazioni di I/O possono essere migliorate tramite compressione o un archivio dati a colonne. Poiché in generale i dati sono spesso ripetuti in diverse colonne all'interno di una tabella, l'uso di columnstore trae vantaggio da queste ripetizioni durante la compressione dei dati.

Un columnstore può non essere altrettanto efficiente in presenza di numerosi inserimenti nella tabella, ma costituisce un'ottima scelta se i dati sono statici o cambiano solo raramente. Se un archivio a colonne non è appropriato, è possibile abilitare la compressione in una tabella principale di righe per migliorare l'I/O.

Per altre informazioni, vedere i documenti seguenti:

+ [Compressione dei dati](../../relational-databases/data-compression/data-compression.md)

+ [Abilitare la compressione in una tabella o un indice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Guida agli indici columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Tabelle con ottimizzazione per la memoria

La memoria non è attualmente più un problema per i computer moderni. Poiché le specifiche hardware continuano a migliorare, è relativamente semplice ottenere RAM con costi contenuti. Allo stesso tempo, tuttavia, i dati vengono prodotti sempre più rapidamente e devono essere elaborati con bassa latenza.

Le tabelle ottimizzate per la memoria rappresentano una soluzione, perché sfruttano la grande quantità di memoria disponibile nei computer avanzati per risolvere il problema dei Big Data. Le tabelle ottimizzate per la memoria risiedono principalmente in memoria, in modo da consentire la lettura e la scrittura dei dati in memoria. Per la durabilità, una seconda copia della tabella viene mantenuta su disco e i dati vengono letti dal disco solo durante il recupero del database.

Se è necessario leggere e scrivere frequentemente nelle tabelle, le tabelle ottimizzate per la memoria possono essere utili offrendo scalabilità elevata e bassa latenza.  Nello scenario per l'individuazione dei curricula corrispondenti, l'uso di tabelle ottimizzate per la memoria ha consentito di leggere tutte le caratteristiche dei curricula dal database e di archiviarle nella memoria principale, per trovare le corrispondenze con le nuove posizioni aperte. Questa operazione ha ridotto notevolmente l'I/O su disco.

Grazie a una tabella ottimizzata per la memoria nel processo di scrittura delle stime nel database da più batch simultanei, sono stati ottenuti ulteriori miglioramenti alle prestazioni. L'uso di tabelle ottimizzate per la memoria in SQL Server abilita la bassa latenza per le letture e le scritture delle tabelle.

L'esperienza è risultata fluida anche durante lo sviluppo. Le tabelle ottimizzate per la memoria durevoli sono state create in contemporanea con il database. Per lo sviluppo è stato pertanto usato lo stesso flusso di lavoro indipendentemente dalla posizione di archiviazione dei dati.

### <a name="processor"></a>Processore

SQL Server può eseguire attività in parallelo usando i core disponibili nel computer. Più core sono disponibili, migliori saranno le prestazioni. Anche se aumentare il numero di core potrebbe non essere utile per operazioni associate all'I/O, gli algoritmi associati alla CPU traggono vantaggio da CPU più veloci con molti core.

Dato che il server viene in genere usato da più utenti contemporaneamente, l'amministratore del database deve determinare il numero ideale di core necessari per supportare i calcoli dei carichi di lavoro nei momenti di picco.

### <a name="resource-governance"></a>Governance delle risorse

Nelle edizioni che supportano Resource Governor, è possibile usare i pool di risorse per specificare l'allocazione di un numero specifico di CPU a determinati carichi di lavoro. È anche possibile gestire la quantità di memoria allocata a carichi di lavoro specifici.

La governance delle risorse in SQL Server consente di centralizzare il monitoraggio e il controllo delle varie risorse usate da SQL Server e da R. Ad esempio, è possibile allocare metà della memoria disponibile per il motore di database, in modo da garantire che i servizi di base possano sempre essere eseguiti nonostante carichi di lavoro più pesanti temporanei.

Il valore predefinito per l'utilizzo della memoria da parte di script esterni è limitato al 20% della memoria totale disponibile per SQL Server stesso. Questo limite viene applicato per impostazione predefinita per garantire che tutte le attività che si basano sul server di database non siano influenzate gravemente dai processi R con esecuzione prolungata. Tuttavia, questi limiti possono essere modificati dall'amministratore del database. In molti casi, il limite del 20% non è adeguato per supportare carichi di lavoro di Machine Learning intensi.

Le opzioni di configurazione supportate sono **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT** e **MAX_PROCESSES**. Per visualizzare le impostazioni correnti, usare questa istruzione: `SELECT * FROM sys.resource_governor_external_resource_pools`

-  Se il server viene usato principalmente per R Services, può essere utile aumentare MAX_CPU_PERCENT al 40% o al 60%.

-  Se molte sessioni R devono usare lo stesso server contemporaneamente, tutte e tre le impostazioni devono essere aumentate.

Per modificare i valori delle risorse allocate, usare istruzioni T-SQL.

+ Questa istruzione imposta l'uso della memoria su 40%: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ Questa istruzione imposta tutti e tre i valori configurabili: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Se si modifica un'impostazione della memoria, della CPU o del numero massimo di processi e quindi si vogliono applicare immediatamente le impostazioni, eseguire l'istruzione seguente: `ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Soft-NUMA, architettura hardware NUMA e affinità della CPU

Quando si usa SQL Server come contesto di calcolo, a volte è possibile ottenere prestazioni migliori ottimizzando le impostazioni relative a NUMA e all'affinità dei processori. 

I sistemi con _hardware NUMA_ dispongono di più bus di sistema, ognuno usato da un piccolo set di processori. Ogni CPU può accedere alla memoria associata ad altri gruppi in modo coerente. Ogni gruppo viene denominato nodo NUMA. Se si dispone di hardware NUMA, è possibile che questo sia configurato in modo da utilizzare memoria interleaved anziché la modalità NUMA. In tal caso, Windows, e quindi SQL Server, non lo riconosceranno come NUMA. 

È possibile eseguire la query seguente per trovare il numero di nodi di memoria a disposizione di SQL Server:

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Se la query restituisce un solo nodo di memoria (nodo 0), non si dispone di hardware NUMA o l'hardware è configurato in modalità interleaved (non NUMA). SQL Server ignora l'hardware NUMA anche in presenza di quattro o meno CPU o se almeno un nodo dispone di una sola CPU.

Se il computer ha più processori ma non dispone di hardware-NUMA, è anche possibile usare [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) per suddividere le CPU in gruppi più piccoli.  Sia in SQL Server 2016 che in SQL Server 2017, la funzionalità Soft-NUMA viene abilitata automaticamente all'avvio del servizio SQL Server.

Quando è abilitata la funzionalità Soft-NUMA, SQL Server gestisce automaticamente i nodi. Tuttavia, per ottimizzare carichi di lavoro specifici, è possibile disabilitare l'_affinità software_ e configurare manualmente l'affinità di CPU per i nodi NUMA software. In questo modo è possibile ottenere un maggiore controllo sui carichi di lavoro assegnati ai nodi, in particolare se si usa un'edizione di SQL Server che supporta la governance delle risorse. Specificando l'affinità di CPU e allineando i pool di risorse ai gruppi di CPU, è possibile ridurre la latenza e assicurarsi che i processi correlati vengano eseguiti nello stesso nodo NUMA.

Il processo generale per la configurazione di Soft-NUMA e dell'affinità di CPU per il supporto dei carichi di lavoro R è il seguente:

1. Abilitare Soft-NUMA, se disponibile
2. Definire l'affinità dei processori
3. Creare pool di risorse per i processi esterni, usando [Resource Governor](../r/resource-governance-for-r-services.md)
4. Assegnare i [gruppi del carico di lavoro](../../relational-databases/resource-governor/resource-governor-workload-group.md) a gruppi di affinità specifici

Per informazioni dettagliate, incluso codice di esempio, vedere questa esercitazione: [SQL Optimization Tips and Tricks (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services) (Suggerimenti e trucchi per l'ottimizzazione di SQL di Ke Huang)

**Altre risorse:**

+ [Soft-NUMA in SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Come mappare i nodi Soft-NUMA alle CPU

## <a name="task-specific-optimizations"></a>Ottimizzazioni specifiche delle attività

Questa sezione riepiloga i metodi adottati in questi case study e in altri test per l'ottimizzazione di carichi di lavoro di Machine Learning specifici. I carichi di lavoro comuni includono il training del modello, l'estrazione delle caratteristiche e la progettazione delle caratteristiche, oltre a vari scenari di assegnazione dei punteggi: singola riga, batch di piccole dimensioni e batch di grandi dimensioni.

### <a name="feature-engineering"></a>Progettazione delle funzionalità

Un punto problematico per R è che in genere viene elaborato su una singola CPU. Si tratta di un importante collo di bottiglia delle prestazioni per molte attività, in particolare per la progettazione delle caratteristiche. Nella soluzione per l'individuazione dei curricula corrispondenti, solo l'attività di progettazione delle caratteristiche crea 2.500 caratteristiche di prodotto incrociato che è necessario combinare alle 100 caratteristiche originali. Questa attività richiederebbe una quantità di tempo significativa se tutte le operazioni venissero eseguite su una singola CPU.

Esistono diversi modi per migliorare le prestazioni della progettazione delle caratteristiche. È possibile ottimizzare il codice R e mantenere l'estrazione delle caratteristiche all'interno del processo di modellazione oppure spostare il processo di progettazione delle caratteristiche in SQL.

- Con R occorre definire una funzione e quindi passarla come argomento a [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) durante il training. Se il modello supporta l'elaborazione parallela, l'attività di progettazione delle caratteristiche può essere elaborata usando più CPU. Con questo approccio, il team di data science ha osservato un miglioramento delle prestazioni del 16% in termini di tempo di assegnazione dei punteggi. Questo approccio richiede tuttavia un modello che supporti la parallelizzazione e una query che possa essere eseguita usando un piano parallelo.

- Usare R con un contesto di calcolo SQL. In un ambiente multiprocessore con risorse isolate disponibili per l'esecuzione di batch distinti, è possibile ottenere una maggiore efficienza isolando le query SQL usate per ogni batch, per estrarre i dati dalle tabelle e vincolare i dati nello stesso gruppo di carico di lavoro. I metodi usati per isolare i batch includono il partizionamento e l'uso di PowerShell per eseguire query separate in parallelo.

- Esecuzione parallela ad hoc: In un contesto di calcolo di SQL Server è possibile fare affidamento sul motore di database SQL per applicare l'esecuzione parallela, se possibile e se tale opzione risulta più efficiente.

- Usare T-SQL in un processo di definizione delle caratteristiche separato. Il precalcolo dei dati delle caratteristiche con SQL è in genere più rapido.

### <a name="prediction-scoring-in-parallel"></a>Stima (assegnazione dei punteggi) in parallelo

Uno dei vantaggi di SQL Server è la possibilità di gestire un volume elevato di righe in parallelo. In nessun altro caso questo vantaggio è così evidente come per l'assegnazione dei punteggi. In genere, il modello non richiede l'accesso a tutti i dati per l'assegnazione dei punteggi, quindi è possibile partizionare i dati di input, con ogni gruppo di carico di lavoro che elabora un'attività.

È anche possibile inviare i dati di input come una singola query, che viene poi analizzata da SQL Server. Se è possibile creare un piano di query parallelo per i dati di input, vengono automaticamente partizionati i dati assegnati ai nodi e vengono eseguiti in parallelo anche i join e le aggregazioni richiesti.

Per informazioni dettagliate su come definire una stored procedure da usare per l'assegnazione dei punteggi, vedere il progetto di esempio in [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) e cercare il file "step5_score_for_matching.sql". Lo script di esempio tiene anche traccia delle ore di inizio e di fine della query e scrive l'ora nella console SQL, in modo da poter valutare le prestazioni.

### <a name="concurrent-scoring-using-resource-groups"></a>Assegnazione dei punteggi simultanea con i gruppi di risorse

Per aumentare le prestazioni per il problema di assegnazione dei punteggi, è buona norma adottare l'approccio di riduzione del mapping, in cui milioni di elementi vengono suddivisi in più batch. Più processi di assegnazione dei punteggi possono poi essere eseguiti contemporaneamente. In questo framework, i batch vengono elaborati in set di CPU diversi e i risultati vengono raccolti e scritti di nuovo nel database.

Si tratta dell'approccio usato nello scenario per l'individuazione dei curricula corrispondenti. Tuttavia, la governance delle risorse in SQL Server è essenziale per l'implementazione di questo approccio. Con la configurazione di gruppi di carico di lavoro per i processi di script esterni, è possibile indirizzare i processi di assegnazione dei punteggi R a gruppi di processori diversi e ottenere una velocità effettiva migliore.

La governance delle risorse può anche contribuire a suddividere le risorse disponibili nel server (CPU e memoria) per ridurre al minimo la concorrenza dei carichi di lavoro. È possibile configurare funzioni di classificazione per distinguere tra tipi diversi di processi R. Ad esempio, è possibile decidere che il processo di assegnazione dei punteggi chiamato da un'applicazione abbia sempre la priorità e che i processi di ripetizione del training abbiano una priorità bassa. Questo isolamento delle risorse può migliorare potenzialmente il tempo di esecuzione e offrire prestazioni più prevedibili.

### <a name="concurrent-scoring-using-powershell"></a>Assegnazione dei punteggi simultanea con PowerShell

Se si decide di partizionare manualmente i dati, è possibile usare gli script di PowerShell per eseguire più attività di assegnazione dei punteggi simultanee. A tale scopo, usare il cmdlet Invoke-SqlCmd e avviare le attività di assegnazione dei punteggi in parallelo.

Nello scenario di individuazione dei curricula corrispondenti la concorrenza è stata progettata come segue:

- 20 processori divisi in quattro gruppi di cinque CPU ciascuno. Ogni gruppo di CPU si trova nello stesso nodo NUMA.

- Il numero massimo di batch simultanei è stato impostato su otto.

- Ogni gruppo di carico di lavoro deve gestire due attività di assegnazione dei punteggi. Non appena un'attività termina la lettura dei dati e avvia l'assegnazione dei punteggi, l'altra attività può iniziare a leggere i dati dal database.

Per visualizzare gli script di PowerShell per questo scenario, aprire il file experiment.ps1 nel [progetto GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips).

### <a name="storing-models-for-prediction"></a>Archiviazione dei modelli per la stima

Al termine del training e della valutazione e dopo aver selezionato un modello ottimale, è consigliabile archiviare il modello nel database in modo che sia disponibile per le stime. Il caricamento del modello pre-calcolato dal database per la stima è efficiente, perché le funzionalità di Machine Learning di SQL Server usano algoritmi di serializzazione speciali per archiviare e caricare i modelli quando si esegue il passaggio tra R e il database.

> [!TIP]
> In SQL Server 2017 è possibile usare la funzione PREDICT per eseguire l'assegnazione dei punteggi anche se R non è installato nel server. Sono supportati tipi di modelli limitati dal pacchetto RevoScaleR.

Tuttavia, a seconda dell'algoritmo usato, alcuni modelli possono avere dimensioni molto elevate, soprattutto quando vengono sottoposti a training su un set di dati di grandi dimensioni. Ad esempio, gli algoritmi come **lm** o **glm** generano una grande quantità di dati di riepilogo insieme alle regole. Poiché esistono limiti alle dimensioni di un modello che possono essere archiviate in una colonna varbinary, è consigliabile eliminare gli artefatti superflui dal modello prima di archiviarlo nel database per la produzione.

## <a name="articles-in-this-series"></a>Articoli della serie

[Ottimizzazione delle prestazioni per R - Introduzione](../r/sql-server-r-services-performance-tuning.md)

[Ottimizzazione delle prestazioni per R - Configurazione di SQL Server](../r/sql-server-configuration-r-services.md)

[Ottimizzazione delle prestazioni per R - Codice R e ottimizzazione dei dati](../r/r-and-data-optimization-r-services.md)

[Ottimizzazione delle prestazioni - Risultati dei case study](../r/performance-case-study-r-services.md)
