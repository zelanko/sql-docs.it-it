---
title: 'Configurazione di SQL Server (R Services): SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f5dd6ee267b7bac933e40f90282d1bf74aa57b62
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511848"
---
# <a name="sql-server-configuration-for-use-with-r"></a>Configurazione di SQL Server per l'uso con R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo è il secondo di una serie che descrive l'ottimizzazione delle prestazioni per R Services basato su due casi di Studio.  Questo articolo fornisce indicazioni sulla configurazione hardware e di rete del computer in cui viene usato per eseguire SQL Server R Services. Include anche informazioni sui modi per configurare l'istanza di SQL Server, database o tabelle utilizzate in una soluzione. Perché usare NUMA in SQL Server applica una sfocatura la linea tra le ottimizzazioni di hardware e del database, una terza sezione vengono illustrate governance di affinità e risorse della CPU in modo dettagliato.

> [!TIP]
> Se si ha familiarità con SQL Server, è consigliabile rivedere anche la Guida di ottimizzazione delle prestazioni di SQL Server: [Monitorare e ottimizzare le prestazioni](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance).

## <a name="hardware-optimization"></a>Ottimizzazione dell'hardware

Ottimizzazione del computer del server è importante per assicurarsi di avere le risorse per l'esecuzione di script esterni. Quando le risorse sono limitate, si potrebbero verificare problemi come questi:

- L'esecuzione del processo viene posticipato o annullato per stabilire le priorità delle altre operazioni di database
- Script R che provocano errori "quota superata" per terminare senza completamento
- I dati caricati in memoria di R troncata, per ottenere risultati incompleti

### <a name="memory"></a>Memoria

La quantità di memoria disponibile nel computer può avere un notevole impatto sulle prestazioni di algoritmi analitici avanzati. Memoria insufficiente potrebbe influire sul grado di parallelismo quando si usa il contesto di calcolo SQL. Può anche influire sulle dimensioni del blocco (righe per operazione di lettura) che possono essere elaborate e sul numero di sessioni simultanee supportato.

È altamente consigliato un minimo di 32 GB. Se si dispone di più di 32 GB di spazio disponibile, è possibile configurare l'origine dati SQL per l'uso di più righe in ogni operazione di lettura per migliorare le prestazioni.

È anche possibile gestire la memoria utilizzata dall'istanza. Per impostazione predefinita, SQL Server abbia la priorità dei processi di script esterni quando la memoria viene allocata. In un'installazione predefinita di R Services, viene allocato solo il 20% della memoria disponibile per R.

In genere ciò non è sufficiente per le attività di analisi scientifica dei dati, ma non si desidera privare di SQL server della memoria. È necessario sperimentare e perfezionare l'allocazione della memoria tra il motore di database, i servizi collegati e gli script esterni, considerando che la configurazione ottimale varia caso per caso.

Per il modello di corrispondenza resume uso di script esterni è stata pesante e si sono verificati alcun altro database servizi motore di esecuzione; di conseguenza, le risorse allocate per gli script esterni sono stati aumentato fino al 70%, che era la migliore configurazione per le prestazioni di script.

### <a name="power-options"></a>Opzioni di risparmio energia

Nel sistema operativo Windows, il **ad alte prestazioni** power opzione deve essere utilizzata. Usando un'impostazione diversa comporta prestazioni ridotte o non uniformi quando si usa SQL Server.

### <a name="disk-io"></a>I/O su disco

Training e previsione processi con R Services sono intrinsecamente i/o associati e dipendono dalla velocità dei dischi in cui è archiviato il database su. Possono essere utili unità più veloci, quali le unità SSD (unità SSD).

Sull'I/O su disco influiscono anche altre applicazioni che accedono al disco, ad esempio le operazioni di lettura su un database da parte di altri client. Le prestazioni di I/O su disco dipendono anche dalle impostazioni nel file system in uso, come le dimensioni dei blocchi usate dal file system.

Se sono disponibili più unità, archivio i database in un'unità diversa rispetto a SQL Server in modo che le richieste per il motore di database che non si avvicinino stesso disco le richieste per i dati archiviati nel database.

L'I/O su disco può avere un notevole impatto sulle prestazioni durante l'esecuzione di funzioni analitiche RevoScaleR che usano più iterazioni durante il training. Ad esempio, `rxLogit`, `rxDTree`, `rxDForest`, e `rxBTrees` usano tutti più iterazioni. Se l'origine dati è SQL Server, questi algoritmi usano file temporanei ottimizzati per l'acquisizione dei dati. Questi file vengono automaticamente eliminati al termine della sessione. Con un disco ad alte prestazioni per le operazioni di lettura/scrittura può migliorare significativamente il tempo trascorso totale per questi algoritmi.

> [!NOTE]
> Le prime versioni di R Services necessari per il supporto di nome file 8.3 nei sistemi operativi Windows. Questa restrizione è stata eliminata dopo il Service Pack 1. Tuttavia, è possibile usare fsutil.exe per determinare se un'unità supporta nomi di 8.3 file o per abilitare il supporto in caso contrario.

### <a name="paging-file"></a>File di paging

Il sistema operativo Windows usa un file di paging per gestire i dump di arresto anomalo e per archiviare pagine di memoria virtuale. Se si nota un paging eccessivo, provare ad aumentare la memoria fisica nel computer. Benché la disponibilità di più memoria fisica non elimina il paging, riduce la necessità di paging.

Anche la velocità del disco in cui è archiviato il file di paging può influire sulle prestazioni. L'archiviazione del file di paging in un'unità SSD o l'uso di più file di paging su più SSD può migliorare le prestazioni.

Per informazioni sulla definizione delle dimensioni del file di paging, vedere [come determinare le dimensioni del file di pagina appropriato per le versioni a 64 bit di Windows](https://support.microsoft.com/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Ottimizzazioni a livello di istanza o un database

Ottimizzazione dell'istanza di SQL Server è la chiave per un'esecuzione efficiente di script esterni.

> [!NOTE]
> Le impostazioni ottimali differiscono a seconda della dimensione e tipo di dati, il numero di colonne che si usa per l'assegnazione dei punteggi o un modello di training.
> 
> È possibile esaminare i risultati delle ottimizzazioni specifiche nell'articolo finale: [Ottimizzazione delle prestazioni - risultati case study](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> Per gli script di esempio, vedere distinte [repository GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning).

### <a name="table-compression"></a>Compressione di tabelle

Spesso le prestazioni dei / o possono essere migliorate tramite compressione o un archivio dati a colonne. In generale, i dati sono spesso ripetuti in diverse colonne all'interno di una tabella, in modo che tramite un columnstore consente di sfruttare queste ripetizioni durante la compressione dei dati.

Un columnstore potrebbe non essere più efficiente se sono presenti numerosi inserimenti nella tabella, ma è un'ottima scelta se i dati sono statici o cambiano solo raramente. Se un archivio a colonne non è appropriato, è possibile abilitare la compressione in una tabella principale di righe per migliorare l'I/O.

Per altre informazioni, vedere i documenti seguenti:

+ [Compressione dei dati](../../relational-databases/data-compression/data-compression.md)

+ [Abilitare la compressione in una tabella o indice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Guida agli indici columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Tabelle con ottimizzazione per la memoria

Al giorno d'oggi, memoria non è più un problema per i computer moderni. Man mano che le specifiche hardware migliorare, è relativamente semplice ottenere i valori ottimali di RAM. Tuttavia, allo stesso tempo, i dati sono in fase di produzione più rapidamente rispetto al passato e i dati devono essere elaborati con latenza bassa.

Le tabelle ottimizzate per la memoria rappresentano una soluzione, dato che le estensioni si avvalgono di grandi quantità di memoria disponibile nel computer advanced affrontare il problema di big data. Le tabelle ottimizzate per la memoria si trovano principalmente in memoria, in modo che i dati viene letta dal e scritti in memoria. Per garantire una durabilità, una seconda copia della tabella viene mantenuta su disco e i dati vengono letti solo dal disco durante il recupero del database.

Se è necessario leggere e scrivere nelle tabelle di frequente, tabelle ottimizzate per la memoria possono essere utili con scalabilità elevata e bassa latenza.  Nello scenario di ripresa di ricerca, utilizzo di tabelle ottimizzate per la memoria ha permesso di leggere tutte le funzionalità di ripresa del database e archiviarle nella memoria principale, in modo che corrispondano con nuove offerte di lavoro. Ciò notevolmente ridotto dei / o disco.

Ulteriori miglioramenti delle prestazioni sono stati raggiunti con tabelle ottimizzate per la memoria nel processo di scrittura stime nuovamente al database da più batch simultanei. L'uso delle tabelle ottimizzate per la memoria in SQL Server abilitato a bassa latenza su tabella letture e scritture.

L'esperienza fu senza problemi anche durante lo sviluppo. Le tabelle durevoli ottimizzate per la memoria sono state create allo stesso tempo che il database è stato creato. Pertanto, lo sviluppo utilizzati stesso flusso di lavoro indipendentemente dalla posizione dei dati.

### <a name="processor"></a>Processore

SQL Server può eseguire attività in parallelo usando i core disponibili nel computer; il numero di core disponibili, ottenere le migliori prestazioni. Mentre l'aumento del numero di core può non essere utile per le operazioni dei / o bound, associate alla CPU algoritmi vantaggio da CPU più veloci con molti Core.

Poiché il server viene in genere usato da più utenti contemporaneamente, l'amministratore del database deve determinare il numero ideale di core necessari per supportare i calcoli del carico di lavoro di picco.

### <a name="resource-governance"></a>Governance delle risorse

Nelle edizioni che supportano Resource Governor, è possibile usare i pool di risorse per specificare che determinati carichi di lavoro vengono allocati un certo numero di CPU. È anche possibile gestire la quantità di memoria allocata per i carichi di lavoro specifici.

Governance delle risorse in SQL Server consente di centralizzare il monitoraggio e il controllo di diverse risorse usate da SQL Server e di R. Ad esempio, si potrebbe allocare metà la memoria disponibile per il motore di database, per garantire che core services può essere sempre eseguito malgrado i carichi di lavoro più pesante temporanei.

Il valore predefinito per il consumo di memoria tramite gli script esterni è limitato al 20% della memoria totale disponibile per SQL Server. Questo limite viene applicato per impostazione predefinita per garantire che tutte le attività che si basano sul server di database non causa gravi da processi con esecuzione prolungata R. Tuttavia, questi limiti possono essere modificati dall'amministratore del database. In molti casi, il limite di 20% non è sufficiente per supportare carichi di lavoro di apprendimento grave.

Le opzioni di configurazione supportate sono **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT**, e **MAX_PROCESSES**. Per visualizzare le impostazioni correnti, usare l'istruzione seguente: `SELECT * FROM sys.resource_governor_external_resource_pools`

-  Se il server viene utilizzato principalmente per R Services, potrebbe essere utile aumentare MAX_CPU_PERCENT al 40% o al 60%.

-  Se più sessioni R che è necessario usare lo stesso server allo stesso tempo, tutti e tre le impostazioni devono essere aumentate.

Per modificare i valori allocati delle risorse, usare istruzioni T-SQL.

+ Questa istruzione imposta l'utilizzo della memoria sul 40%: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ Questa istruzione imposta tutti e tre i valori configurabili: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Se si modifica una memoria, CPU o l'impostazione max di processo e quindi si desidera applicare immediatamente le impostazioni, eseguire l'istruzione seguente: `ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Affinità soft-NUMA hardware NUMA e della CPU

Quando si usa SQL Server come contesto di calcolo, è possibile ottenere prestazioni migliori in alcuni casi, ottimizzando le impostazioni relative all'affinità NUMA e del processore. 

Con i sistemi _NUMA hardware_ dispone di più di un bus di sistema, ognuno utilizzato da un piccolo set di processori. Ogni CPU può accedere alla memoria associata ad altri gruppi in modo coerente. Ogni gruppo viene denominato nodo NUMA. Se si dispone di hardware NUMA, è possibile che questo sia configurato in modo da utilizzare memoria interleaved anziché la modalità NUMA. In tal caso, Windows e pertanto SQL Server, non lo riconosceranno come NUMA. 

È possibile eseguire la query seguente per trovare il numero di nodi di memoria disponibili per SQL Server:

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Se la query restituisce un nodo di memoria (nodo 0), non è hardware NUMA o l'hardware è configurato come interleaved (non NUMA). SQL Server ignora anche hardware NUMA quando non vi CPU di un massimo di quattro, o se almeno un nodo ha solo una CPU.

Se il computer con più processori, ma non è tra architettura hardware NUMA, è anche possibile usare [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) per suddividere le CPU in gruppi più piccoli.  In SQL Server 2016 e SQL Server 2017, la funzionalità di Soft-NUMA viene abilitata automaticamente quando si avvia il servizio SQL Server.

Quando Soft-NUMA è abilitato, SQL Server gestisce automaticamente i nodi per l'utente; Tuttavia, per ottimizzare i carichi di lavoro specifici, è possibile disabilitare _affinità debole_ e configurare manualmente l'affinità di CPU per i nodi soft NUMA. Ciò consente di visualizzare un maggiore controllo su cui i carichi di lavoro vengono assegnati a quali nodi, in particolare se si usa un'edizione di SQL Server che supporta la governance delle risorse. Specificando l'affinità di CPU e allineamento dei pool di risorse con i gruppi di CPU, è possibile ridurre la latenza e verificare che i processi correlati vengano eseguiti nello stesso nodo NUMA.

Il processo generale per la configurazione soft-NUMA e affinità di CPU per supportare carichi di lavoro R è il seguente:

1. Attivare soft-NUMA, se disponibile
2. Definire l'affinità processori
3. Creare pool di risorse per processi esterni, usando [Resource Governor](../r/resource-governance-for-r-services.md)
4. Assegnare il [gruppi di carico di lavoro](../../relational-databases/resource-governor/resource-governor-workload-group.md) a specifici gruppi di affinità

Per informazioni dettagliate, incluso il codice di esempio, vedere l'esercitazione: [Suggerimenti di ottimizzazione di SQL e consigli (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Altre risorse:**

+ [Soft-NUMA in SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Come eseguire il mapping di nodi soft-NUMA alle CPU

+ [Architettura soft-NUMA automatica: Esegue semplicemente più veloce (Bob Ward)](https://blogs.msdn.microsoft.com/bobsql/2016/06/03/sql-2016-it-just-runs-faster-automatic-soft-numa/)

   Descrive cronologia e i dettagli di implementazione, le prestazioni nel server multi-core più recenti.

## <a name="task-specific-optimizations"></a>Ottimizzazioni specifiche per le attività

Questa sezione vengono riepilogati i metodi adottati in questi casi di Studio e in altri test, per l'ottimizzazione di carichi di lavoro di apprendimento automatico specifica. Carichi di lavoro comuni includono training del modello, estrazione di funzioni e la progettazione di funzionalità e diversi scenari per l'assegnazione dei punteggi: riga singola, batch di piccole dimensioni e batch di grandi dimensioni.

### <a name="feature-engineering"></a>Progettazione delle funzionalità

Un punto debole di r è che viene in genere elaborato in una singola CPU. Si tratta di un collo di bottiglia importante per molte attività, soprattutto alla progettazione di funzionalità. Nella soluzione di ripresa di ricerca, l'attività di progettazione di funzionalità da solo creato le funzionalità del prodotto incrociato 2.500 che dovevano essere combinati con le funzionalità di 100 originale. Questa operazione richiederebbe una quantità significativa di tempo se tutto ciò che è stata eseguita su una singola CPU.

Esistono diversi modi per migliorare le prestazioni di progettazione di funzionalità. È possibile ottimizzare il codice R e mantenere l'estrazione di funzioni all'interno del processo di modellazione o spostare il processo di progettazione di funzionalità in SQL.

- Usando R. Si definisce una funzione e quindi passarlo come argomento [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) durante il training. Se il modello supporta l'elaborazione parallela, l'attività di progettazione di funzionalità può essere elaborato con più CPU. Con questo approccio, il team di data science osservato un miglioramento delle prestazioni di 16% in termini di tempo di assegnazione dei punteggi. Tuttavia, questo approccio richiede un modello che supporta la parallelizzazione e una query che può essere eseguita tramite un piano parallelo.

- Contesto di calcolo usano R con un database SQL. In un ambiente multiprocessore con isolate risorse disponibili per l'esecuzione di batch separati, è possibile ottenere maggiore efficienza isolando le query SQL usate per ogni batch, per estrarre dati dalle tabelle e limitare i dati nello stesso gruppo del carico di lavoro. I metodi usati per isolare i batch includono il partizionamento e usano PowerShell per eseguire query separate in parallelo.

- Esecuzione parallela ad hoc: In un contesto di calcolo di SQL Server, è possibile basarsi sul motore di database SQL per imporre l'esecuzione parallela se possibile e se tale opzione risulta più efficiente.

- Usare T-SQL in un processo di definizione delle funzionalità separata. Precomputing i dati della funzionalità con SQL è in genere più veloce.

### <a name="prediction-scoring-in-parallel"></a>Stima (assegnazione dei punteggi) in parallelo

Uno dei vantaggi di SQL Server è la possibilità di gestire un numero elevato di righe in parallelo. Lungi dall'essere questo vantaggio così è contrassegnato come nell'assegnazione dei punteggi. In genere il modello non è necessario l'accesso a tutti i dati per il punteggio, che consentono di suddividere i dati di input con ogni gruppo di carico di lavoro una sola attività di elaborazione.

È anche possibile inviare i dati di input come una singola query e SQL Server li analizza la query. Se è possibile creare un piano di query parallele per i dati di input, automaticamente assegnati ai nodi di dati delle partizioni ed esegue in parallelo anche necessari join e aggregazioni.

Se si desidera esplorare nei dettagli di come definire una stored procedure per l'uso di assegnazione dei punteggi, vedere il progetto di esempio nella [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) e cercare il file "step5_score_for_matching.sql". L'esempio di script anche tiene traccia delle query inizio e ora di fine e scrive il tempo necessario per la console di SQL in modo che sia possibile valutare le prestazioni.

### <a name="concurrent-scoring-using-resource-groups"></a>Simultanee di assegnazione dei punteggi usando gruppi di risorse

Per aumentare il problema di assegnazione dei punteggi, è consigliabile adottare l'approccio di MapReduce in cui milioni di elementi sono suddivisi in più batch. Quindi, più processi di assegnazione dei punteggi vengono eseguiti contemporaneamente. In questo framework, i batch vengono elaborati set diversi di CPU e i risultati vengono raccolti e scritti nel database.

Si tratta dell'approccio utilizzato nello scenario di ripresa di ricerca; Tuttavia, governance delle risorse in SQL Server è essenziale per l'implementazione di questo approccio. Configurando gruppi di carico di lavoro per processi di script esterni, è possibile instradare R i processi di assegnazione dei punteggi a diversi gruppi di processori e ottenere una velocità effettiva.

Governance delle risorse consente inoltre allocare dividere le risorse disponibili nel server (CPU e memoria) per ridurre la concorrenza del carico di lavoro. È possibile configurare funzioni di classificazione per distinguere tra diversi tipi di processi R: ad esempio, si potrebbe decidere che di assegnazione dei punteggi denominato da un'applicazione sempre prioritario, mentre i processi di ripetizione del training hanno priorità bassa. Questo isolamento delle risorse può potenzialmente migliorare i tempi di esecuzione e offrono prestazioni più prevedibili.

### <a name="concurrent-scoring-using-powershell"></a>Simultanee di assegnazione dei punteggi usando PowerShell

Se si decide di partizionare manualmente i dati, è possibile utilizzare gli script di PowerShell per eseguire più attività simultanee di assegnazione dei punteggi. A tale scopo, usare il cmdlet Invoke-SqlCmd e avviare le attività di assegnazione dei punteggi in parallelo.

Nello scenario di ripresa di ricerca, la concorrenza è stata progettata come indicato di seguito:

- 20 processori diviso in quattro gruppi di cinque CPU. Ogni gruppo di CPU si trova nello stesso nodo NUMA.

- Numero massimo di batch simultanei è stata impostata su 8.

- Ogni gruppo di carico di lavoro deve gestire due attività di assegnazione dei punteggi. Non appena un'attività ha terminato la lettura dei dati e assegnazione dei punteggi si avvia, l'altra attività possibile iniziare la lettura dei dati dal database.

Per visualizzare gli script di PowerShell per questo scenario, aprire il experiment.ps1 file nei [progetto Github](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips).

### <a name="storing-models-for-prediction"></a>L'archiviazione dei modelli per la stima

Quando la formazione e al termine della valutazione e si seleziona un modello migliore, è consigliabile archiviare il modello nel database in modo che sia disponibile per le stime. Il caricamento del modello precalcolato dal database per la stima è efficiente, perché SQL Server machine learning Usa algoritmi speciale di serializzazione per archiviare e caricare i modelli durante lo spostamento tra R e il database.

> [!TIP]
> In SQL Server 2017, è possibile usare la funzione PREDICT per eseguire l'assegnazione dei punteggi anche se R non è installato nel server. Sono supportati i tipi di modelli limitate, dal pacchetto RevoScaleR.

Tuttavia, a seconda dell'algoritmo utilizzato, alcuni modelli possono essere molto grandi, specialmente quando sottoposto a training su grandi set di dati. Ad esempio, gli algoritmi, ad esempio **lm** oppure **glm** generare un numero elevato di dati di riepilogo e le regole. Poiché esistono limiti sulle dimensioni di un modello che può essere archiviato in una colonna varbinary, è consigliabile consente di eliminare elementi superflui dal modello prima di archiviare il modello nel database di produzione.

## <a name="articles-in-this-series"></a>Articoli di questa serie

[Le prestazioni di ottimizzazione per R - introduzione](../r/sql-server-r-services-performance-tuning.md)

[Ottimizzazione delle prestazioni per R - configurazione SQL Server](../r/sql-server-configuration-r-services.md)

[Ottimizzazione delle prestazioni per R - R ottimizzazione di codice e i dati](../r/r-and-data-optimization-r-services.md)

[Ottimizzazione delle prestazioni - risultati case study](../r/performance-case-study-r-services.md)
