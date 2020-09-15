---
title: Ottimizzazione delle prestazioni per i risultati
description: Questo articolo riepiloga i metodi, i risultati e le conclusioni di due case study che hanno testato diversi metodi di ottimizzazione.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a6afdda3975fc8f6c269f9c1fcbca35318f0c4da
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179996"
---
# <a name="performance-for-r-services-results-and-resources"></a>Prestazioni per R Services: risultati e risorse
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Questo articolo è il quarto e ultimo di una serie che descrive l'ottimizzazione delle prestazioni per R Services. Questo articolo riepiloga i metodi, i risultati e le conclusioni di due case study che hanno testato diversi metodi di ottimizzazione.

I due case study avevano obiettivi diversi:

+ Il primo case study, del team di sviluppo di R Services, ha cercato di misurare l'effetto di tecniche di ottimizzazione specifiche
+ Il secondo case study, di un team di data scientist, ha sperimentato più metodi per determinare le ottimizzazioni migliori per uno scenario specifico di assegnazione dei punteggi a volumi elevati.

Questo argomento elenca i risultati dettagliati del primo case study. Per il secondo case study, un riepilogo descrive i risultati generali. Alla fine di questo argomento sono riportati i collegamenti a tutti gli script e ai dati di esempio e le risorse usate dagli autori originali.

## <a name="performance-case-study-airline-dataset"></a>Case study sulle prestazioni: set di dati Airline

Questo case study del team di sviluppo di R Services per SQL Server ha testato gli effetti di diverse ottimizzazioni. È stato creato un singolo modello rxLogit ed è stata eseguita l'assegnazione dei punteggi sul set di dati Airline. Le ottimizzazioni sono state applicate durante i processi di training e assegnazione dei punteggi per valutare i singoli effetti.

- GitHub: [dati e script di esempio](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) per lo studio sulle ottimizzazioni di SQL Server

### <a name="test-methods"></a>Metodi di test

1. Il set di dati Airline è costituito da una singola tabella di 10 milioni di righe. Ne è stato eseguito il download e il caricamento bulk in SQL Server.
2. Sono state create sei copie della tabella.
3. Sono state applicate diverse modifiche alle copie della tabella, per testare le caratteristiche di SQL Server, ad esempio la compressione di pagina, la compressione di riga, l'indicizzazione, l'archivio dati a colonne e così via.
4. Le prestazioni sono state misurate prima e dopo l'applicazione di ogni ottimizzazione.

| Nome tabella| Descrizione|
|------|------|
| *airline* | Dati convertiti dal file con estensione xdf originale tramite `rxDataStep`.|                          |
| *airlineWithIntCol*   | *DayOfWeek* convertito in un intero anziché in una stringa. Aggiunge anche una colonna *rowNum*.|
| *airlineWithIndex*    | Stessi dati della tabella *airlineWithIntCol*, ma con un singolo indice cluster basato sulla colonna *rowNum*.|
| *airlineWithPageComp* | Stessi dati della tabella *airlineWithIndex*, ma con la compressione di pagina abilitata. Aggiunge anche due colonne, *CRSDepHour* e *Late*, che vengono calcolate da *CRSDepTime* e *ArrDelay*. |
| *airlineWithRowComp*  | Stessi dati della tabella *airlineWithIndex*, ma con la compressione di riga abilitata. Aggiunge anche due colonne, *CRSDepHour* e *Late*, che vengono calcolate da *CRSDepTime* e *ArrDelay*. |
| *airlineColumnar*     | Archivio a colonne con un singolo indice cluster. Questa tabella viene popolata con i dati di un file pulito con estensione csv.|

Ogni test è costituito da questi passaggi:

1. Prima di ciascun test è stata generata la Garbage Collection R.
2. È stato creato un modello di regressione logistica in base ai dati della tabella. Il valore di *rowsPerRead* per ogni test è stato impostato su 500000.
3. Sono stati generati punteggi usando il modello con training
4. Ogni test è stato eseguito sei volte. La durata della prima esecuzione ("esecuzione a freddo") è stata rimossa. Per consentire l'outlier occasionale, è stato rimosso anche l'intervallo **massimo** tra le cinque esecuzioni restanti. La media delle quattro esecuzioni rimanenti è stata usata per calcolare il runtime trascorso medio di ogni test.
5. I test sono stati eseguiti usando il parametro *reportProgress* con il valore 3 (= tempistiche e stato di avanzamento del report). Ogni file di output contiene informazioni riguardanti il tempo impiegato nell'I/O, il tempo di transizione e il tempo di calcolo. Questi tempi sono utili per la diagnosi e la risoluzione dei problemi.
6. L'output della console è stato anche indirizzato a un file nella directory di output.
7. Gli script di test hanno elaborato gli intervalli di tempo in questi file per calcolare il tempo medio di esecuzione.

I risultati seguenti, ad esempio, sono i tempi di un singolo test. I principali intervalli di interesse sono quelli relativi al **tempo di lettura totale** (tempo di I/O) e al **tempo di transizione** (overhead nell'impostazione dei processi per il calcolo).

**Intervalli di esempio**

```text
Running IntCol Test. Using airlineWithIntCol table.
run 1 took 3.66 seconds
run 2 took 3.44 seconds
run 3 took 3.44 seconds
run 4 took 3.44 seconds
run 5 took 3.45 seconds
run 6 took 3.75 seconds
  
Average Time: 3.4425
metric time pct
1 Total time 3.4425 100.00
2 Overall compute time 2.8512 82.82
3 Total read time 2.5378 73.72
4 Transition time 0.5913 17.18
5 Total non IO time 0.3134 9.10
```

È consigliabile scaricare e modificare gli script di test per risolvere i problemi relativi a R Services o alle funzioni RevoScaleR.

### <a name="test-results-all"></a>Risultati del test (tutti)

Questa sezione confronta i risultati prima e dopo ogni test.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>Dimensioni dei dati con compressione e un archivio tabelle a colonne

Il primo test ha confrontato l'uso della compressione e di una tabella a colonne per ridurre le dimensioni dei dati.

| Nome tabella            | Righe     | Riservato   | Data       | index_size | Non utilizzato  | % salvataggio (riservato) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | n/d        | 368 KB  | 93%                 |

**Conclusioni**

La riduzione massima della dimensione dei dati è stata ottenuta applicando un indice columnstore, seguito dalla compressione di pagina.

#### <a name="effects-of-compression"></a>Effetti della compressione

Questo test ha confrontato i vantaggi della compressione di riga, della compressione di pagina e di nessuna compressione. È stato eseguito il training di un modello usando `rxLinMod` sui dati di tre diverse tabelle di dati. Per tutte le tabelle sono state usate la stessa formula e la stessa query.

| Nome tabella            | Nome test       | numTasks | Durata media |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression - parallel| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression - parallel | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression - parallel  | 4        | 5.2375       |

**Conclusioni**

La compressione da sola non sembra essere utile. In questo esempio l'aumento della CPU per gestire la compressione compensa la riduzione del tempo di I/O.

Tuttavia, quando il test viene eseguito in parallelo impostando *numTasks* su 4, il tempo medio diminuisce.

Per set di dati di dimensioni maggiori, l'effetto della compressione può essere più evidente. La compressione dipende dal set di dati e dai valori, pertanto potrebbe essere necessaria una sperimentazione per determinare l'effetto della compressione sul set di dati.

### <a name="effect-of-windows-power-plan-options"></a>Effetto delle opzioni di combinazione per il risparmio di energia di Windows

In questo esperimento `rxLinMod` è stato usato con la tabella *airlineWithIntCol*. La combinazione per il risparmio di energia di Windows è stata impostata su **Bilanciata** o **Prestazioni elevate**. Per tutti i test, *numTasks* è stato impostato su 1. Il test è stato eseguito sei volte ed è stato eseguito due volte in entrambe le opzioni per il risparmio di energia per esaminare la variabilità dei risultati.

Opzione per il risparmio di energia **Prestazioni elevate**:

| Nome test | Eseguire \# | Tempo trascorso | Durata media |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3,57 secondi |              |
|           | 2      | 3,45 secondi |              |
|           | 3      | 3,45 secondi |              |
|           | 4      | 3,55 secondi |              |
|           | 5      | 3,55 secondi |              |
|           | 6      | 3,45 secondi |              |
|           |        |              | 3.475        |
|           | 1      | 3,45 secondi |              |
|           | 2      | 3,53 secondi |              |
|           | 3      | 3,63 secondi |              |
|           | 4      | 3,49 secondi |              |
|           | 5      | 3,54 secondi |              |
|           | 6      | 3,47 secondi |              |
|           |        |              | 3.5075       |

Opzione per il risparmio di energia **Bilanciata**:

| Nome test | Eseguire \# | Tempo trascorso | Durata media |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3,89 secondi |              |
|           | 2      | 4,15 secondi |              |
|           | 3      | 3,77 secondi |              |
|           | 4      | 5 secondi    |              |
|           | 5      | 3,92 secondi |              |
|           | 6      | 3,8 secondi  |              |
|           |        |              | 3.91         |
|           | 1      | 3,82 secondi |              |
|           | 2      | 3,84 secondi |              |
|           | 3      | 3,86 secondi |              |
|           | 4      | 4,07 secondi |              |
|           | 5      | 4,86 secondi |              |
|           | 6      | 3,75 secondi |              |
|           |        |              | 3.88         |

**Conclusioni**

Il tempo di esecuzione è più coerente e veloce quando si usa la combinazione per il risparmio di energia **Prestazioni elevate** di Windows.

#### <a name="using-integer-vs-strings-in-formulas"></a>Uso di numeri interi o di stringhe nelle formule

Questo test ha valutato l'effetto della modifica del codice R per evitare un problema comune con i fattori di tipo stringa. In particolare, è stato eseguito il training di un modello usando `rxLinMod` con due tabelle: nella prima i fattori vengono archiviati come stringhe, nella seconda tabella i fattori vengono archiviati come numeri interi.

+ Per la tabella *airline* la colonna [DayOfWeek] contiene stringhe. Il parametro _colInfo_ è stato usato per specificare i livelli dei fattori (Monday, Tuesday, ...)

+  Per la tabella *airlineWithIndex*, [DayOfWeek] è un numero intero. Il parametro _colInfo_ non è stato specificato.

+ In entrambi i casi è stata usata la stessa formula: `ArrDelay ~ CRSDepTime + DayOfWeek`.

| Nome tabella          | Nome test   | Durata media |
|---------------------|-------------|--------------|
| *Airline*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**Conclusioni**

Quando si usano numeri interi invece di stringhe per i fattori, il vantaggio è evidente.

### <a name="avoiding-transformation-functions"></a>Evitare le funzioni di trasformazione

In questo test è stato eseguito il training di un modello usando `rxLinMod`, ma tra le due esecuzioni è stato modificato il codice:

+ Nella prima esecuzione è stata applicata una funzione di trasformazione durante la compilazione del modello. 
+ Nella seconda esecuzione i valori delle caratteristiche sono stati precalcolati ed erano disponibili, in modo che non fossero necessarie funzioni di trasformazione.

| Nome test             | Durata media |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**Conclusioni**

Il tempo di training è stato più breve quando **non** è stata usata una funzione di trasformazione. In altre parole, il training del modello è stato più veloce quando sono state usate colonne precalcolate e persistenti nella tabella.

I risparmi previsti sarebbero di gran lunga maggiori se ci fossero molte più trasformazioni e il set di dati avesse dimensioni superiori (\> 100 milioni).

### <a name="using-columnar-store"></a>Uso di un archivio a colonne

Questo test ha valutato i vantaggi in termini di prestazioni offerti dall'uso di un archivio dati a colonne e di un indice. È stato eseguito il training dello stesso modello usando `rxLinMod` e senza trasformazioni dei dati.

+ Nella prima esecuzione la tabella dati ha usato un archivio a righe standard.
+ Nella seconda esecuzione è stato usato un archivio a colonne.

| Nome tabella         | Nome test | Durata media |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**Conclusioni**

Le prestazioni sono migliori con l'archivio a colonne che con l'archivio a righe standard. È prevista una differenza significativa a livello di prestazioni in set di dati di dimensioni superiori (\> 100 milioni).

### <a name="effect-of-using-the-cube-parameter"></a>Effetto dell'uso del parametro cube

Lo scopo di questo test era determinare se l'opzione in RevoScaleR per l'uso del parametro **cube** precalcolato possa migliorare le prestazioni. È stato eseguito il training di un modello usando `rxLinMod`, con questa formula:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

Nella tabella il fattore *DayOfWeek* è archiviato come stringa.

| Nome test     | Parametro cube | numTasks | Durata media | Stima a riga singola (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8,08         | 9.959204                        |

**Conclusioni**

È evidente che l'uso dell'argomento del parametro cube migliora le prestazioni.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>Effetto della modifica di maxDepth per i modelli rxDTree

In questo esperimento è stato usato l'algoritmo `rxDTree` per creare un modello nella tabella *airlineColumnar*. Per questo test *numTasks* è stato impostato su 4. Sono stati usati alcuni valori diversi per *maxDepth* per dimostrare come la modifica della profondità dell'albero influisce sul tempo di esecuzione.

| Nome test       | maxDepth | Durata media |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**Conclusioni**

Con l'aumentare della profondità dell'albero, il numero totale di nodi aumenta in modo esponenziale. Anche il tempo trascorso per la creazione del modello è aumentato in modo significativo.

### <a name="prediction-on-a-stored-model"></a>Stima basata su un modello archiviato

Lo scopo di questo test era determinare l'impatto a livello di prestazioni sull'assegnazione dei punteggi quando il modello con training viene salvato in una tabella di SQL Server invece di essere generato come parte del codice attualmente in esecuzione. Per l'assegnazione dei punteggi, il modello archiviato viene caricato dal database e vengono effettuate stime usando un frame di dati di una riga in memoria (contesto di calcolo locale).

I risultati del test mostrano il tempo necessario per salvare il modello e il tempo impiegato per caricare il modello ed eseguire la stima.

| Nome tabella | Nome test | Tempo medio (per il training del modello) | Tempo di salvataggio/caricamento del modello|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2,09 (include il tempo per la stima) |

**Conclusioni**

Il caricamento di un modello con training da una tabella è chiaramente un modo più rapido per eseguire una stima. È consigliabile evitare di creare il modello ed eseguire l'assegnazione dei punteggi nello stesso script.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>Case study: Ottimizzazione per l'attività di individuazione dei curricula corrispondenti

Il modello per l'individuazione dei curricula corrispondenti è stato sviluppato dal data scientist di Microsoft Ke Huang per testare le prestazioni del codice R in SQL Server e consentire così ai data scientist di creare soluzioni aziendali scalabili.

### <a name="methods"></a>Metodi

Entrambi i pacchetti RevoScaleR e MicrosoftML sono stati usati per eseguire il training di un modello predittivo in una soluzione R complessa che include set di dati di grandi dimensioni. Le query SQL e il codice R erano identici in tutti i test. I test sono stati eseguiti in una singola macchina virtuale di Azure con SQL Server installato. L'autore ha quindi confrontato i tempi necessari per l'assegnazione dei punteggi con e senza le ottimizzazioni seguenti fornite da SQL Server:

- Tabelle in memoria
- Soft-NUMA
- Resource Governor

Per valutare l'effetto di soft-NUMA sull'esecuzione di script R, il team di data science ha testato la soluzione in una macchina virtuale di Azure con 20 core fisici. In questi core fisici sono stati creati automaticamente quattro nodi soft-NUMA, in modo che ogni nodo contenesse cinque core.

Nello scenario per l'individuazione di curricula corrispondenti è stata applicata la definizione dell'affinità della CPU, per valutare l'impatto sui processi R. Sono stati creati quattro **pool di risorse SQL** e quattro **pool di risorse esterne** ed è stata specificata l'affinità della CPU per garantire che in ogni nodo fosse usato lo stesso set di CPU.

Ogni pool di risorse è stato assegnato a un gruppo di carico di lavoro diverso, per ottimizzare l'utilizzo dell'hardware. Ciò è dovuto al fatto che l'affinità soft-NUMA e della CPU non possono dividere la memoria fisica nei nodi NUMA fisici, quindi per definizione tutti i nodi soft-NUMA basati sullo stesso nodo NUMA fisico devono usare la memoria nello stesso blocco di memoria del sistema operativo. In altre parole, non esiste affinità tra memoria e processore.

Per creare questa configurazione è stato usato il processo seguente:

1. Riduzione della quantità di memoria allocata per impostazione predefinita a SQL Server.

2. Creazione di quattro nuovi pool per l'esecuzione di processi R in parallelo.

3. Creazione di quattro gruppi di carico di lavoro in modo che ogni gruppo di carico di lavoro sia associato a un pool di risorse.

4. Riavvio di Resource Governor con i nuovi gruppi di carico di lavoro e le nuove assegnazioni.

5. Creazione di una funzione di classificazione definita dall'utente per assegnare attività diverse in gruppi di carico di lavoro diversi.

6. Aggiornamento della configurazione di Resource Governor per usare la funzione per i gruppi di carico di lavoro appropriati.

### <a name="results"></a>Risultati

La configurazione con le prestazioni migliori nello studio sull'individuazione dei curricula corrispondenti è stata la seguente:

-   Quattro pool di risorse interni (per SQL Server)

-   Quattro pool di risorse esterni (per i processi di script esterni)

-   Ogni pool di risorse è associato a un gruppo di carico di lavoro specifico

-   Ogni pool di risorse è assegnato a CPU diverse

-   Utilizzo massimo della memoria interna (per SQL Server) = 30%

-   Utilizzo massimo della memoria per le sessioni R = 70%

Per il modello di individuazione dei curricula corrispondenti, l'uso di script esterni era elevato e non erano in esecuzione altri servizi del motore di database. Le risorse allocate agli script esterni sono state quindi aumentate al 70%, che si è rivelata la configurazione migliore per le prestazioni dello script.

Si è giunti a questa configurazione dopo aver provato valori diversi. Con un hardware o una soluzione diversa, la configurazione ideale potrebbe essere diversa. Fare sempre più prove per trovare la configurazione più adatta alle proprie esigenze.

Nella soluzione ottimizzata è stato assegnato un punteggio a 1,1 milioni di righe di dati (con 100 funzionalità) in meno di 8,5 secondi in un computer con 20 core. Le ottimizzazioni hanno migliorato significativamente le prestazioni in termini di tempo di assegnazione dei punteggi.

I risultati hanno anche suggerito che il **numero di caratteristiche** ha avuto un impatto significativo sul tempo di assegnazione dei punteggi. Il miglioramento è stato ancora più evidente quando nel modello di stima sono state usate più caratteristiche.

Per informazioni dettagliate, vedere questo articolo di blog e la relativa esercitazione.

-   [Optimization tips and tricks for machine learning in SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/) (Suggerimenti per l'ottimizzazione di Machine Learning in SQL Server)

Molti utenti hanno notato una breve pausa quando il runtime R (o Python) viene caricato per la prima volta. Per questo motivo, come descritto in questi test, la durata della prima esecuzione viene spesso misurata, ma successivamente ignorata. La successiva memorizzazione nella cache può comportare notevoli differenze nelle prestazioni tra la prima e la seconda esecuzione. Si verifica anche un sovraccarico quando i dati vengono spostati tra SQL Server e il runtime esterno, in particolare se i dati vengono passati in rete invece di essere caricati direttamente da SQL Server.

Per tutti questi motivi, non esiste una singola soluzione per ridurre la durata del caricamento iniziale, perché l'impatto sulle prestazioni varia in modo significativo a seconda dell'attività. Per l'assegnazione dei punteggi in batch alle singole righe, ad esempio, viene eseguita la memorizzazione nella cache, quindi le operazioni successive di assegnazione dei punteggi sono molto più veloci e non vengono ricaricati né il modello né il runtime R. È anche possibile usare l'[assegnazione dei punteggi nativa](../predictions/native-scoring-predict-transact-sql.md) per evitare di caricare interamente il runtime R.

Per il training di modelli di grandi dimensioni o per l'assegnazione dei punteggi in batch di grandi dimensioni, potrebbe verificarsi un sovraccarico minimo rispetto ai vantaggi ottenuti evitando di spostare i dati o derivanti dallo streaming e dall'elaborazione parallela. Per altre indicazioni sulle prestazioni, vedere questo post di blog:

+ [Using R to detect fraud at 1 million transactions per second](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/) (Uso di R per rilevare frodi a 1 milione di transazioni al secondo)

## <a name="resources"></a>Risorse

Di seguito vengono forniti collegamenti a informazioni, strumenti e script usati nello sviluppo di questi test.

+ Script di test delle prestazioni e collegamenti ai dati: [dati e script di esempio per lo studio sulle ottimizzazioni di SQL Server](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Articolo che descrive la soluzione per l'individuazione dei curricula corrispondenti: [Optimization tip and tricks for SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/) (Suggerimenti e trucchi per l'ottimizzazione di R Services per SQL Server)

+ Script usati nell'ottimizzazione di SQL per la soluzione per l'individuazione dei curricula corrispondenti: [repository di GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips-Resume-Matching)

### <a name="learn-about-windows-server-management"></a>Informazioni sulla gestione di Windows Server

+ [How to determine the appropriate page file size for 64-bit versions of Windows](https://support.microsoft.com/kb/2860880) (Come determinare le dimensioni appropriate del file di paging per le versioni a 64 bit di Windows)

+ [Informazioni sull'architettura NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [Modifiche che consentono il supporto NUMA in SQL Server](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>Informazioni sulle ottimizzazioni di SQL Server

+ [Riorganizzare e ricompilare gli indici](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [Introduzione alle tabelle ottimizzate per la memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [Dimostrazione: miglioramento delle prestazioni di OLTP in memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [Compressione dei dati](../../relational-databases/data-compression/data-compression.md)

+ [Abilitare la compressione in una tabella o un indice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Disabilitare la compressione in una tabella o un indice](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>Informazioni sulla gestione di SQL Server

+ [Monitoraggio e ottimizzazione delle prestazioni](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)

+ [Introduzione a Resource Governor](https://technet.microsoft.com/library/bb895232.aspx)

+ [Esempio di configurazione di Resource Governor](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Strumenti

+ [Strumento di generazione del carico di archiviazione e di test delle prestazioni DISKSPD](https://github.com/microsoft/diskspd)

+ [Informazioni di riferimento sull'utilità FSUtil](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>Altri articoli della serie

[Ottimizzazione delle prestazioni per R - Introduzione](sql-server-r-services-performance-tuning.md)

[Ottimizzazione delle prestazioni per R - Configurazione di SQL Server](sql-server-configuration-r-services.md)

[Ottimizzazione delle prestazioni per R - Codice R e ottimizzazione dei dati](r-and-data-optimization-r-services.md)

[Ottimizzazione delle prestazioni - Risultati dei case study](performance-case-study-r-services.md)
