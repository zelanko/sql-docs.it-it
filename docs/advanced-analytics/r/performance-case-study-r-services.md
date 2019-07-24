---
title: Prestazioni per R Services per SQL Server-risultati e risorse
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 08d1fd367572561aaa7235fd037371e30f5b270e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345288"
---
# <a name="performance-for-r-services-results-and-resources"></a>Prestazioni per R Services: risultati e risorse
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo è la quarta e la fine di una serie che descrive l'ottimizzazione delle prestazioni per R Services. In questo articolo vengono riepilogati i metodi, i risultati e le conclusioni di due case study che hanno testato diversi metodi di ottimizzazione.

I due case study hanno obiettivi diversi:

+ Il primo case study, dal team di sviluppo di R Services, ha cercato di misurare l'effetto delle specifiche tecniche di ottimizzazione
+ Il secondo case study, da un team di data scientist, ha sperimentato più metodi per determinare le ottimizzazioni migliori per uno scenario specifico di assegnazione di punteggi a volumi elevati.

In questo argomento vengono elencati i risultati dettagliati del primo case study. Per la seconda case study, un riepilogo descrive i risultati generali. Alla fine di questo argomento sono riportati i collegamenti a tutti gli script e i dati di esempio e le risorse usate dagli autori originali.

## <a name="performance-case-study-airline-dataset"></a>Case study prestazioni: Set di dati Airline

Questo case study dal team di sviluppo R Services per SQL Server ha testato gli effetti di diverse ottimizzazioni. È stato creato un singolo modello rxLogit e viene eseguito il punteggio nel set di dati della compagnia aerea. Le ottimizzazioni sono state applicate durante i processi di training e assegnazione dei punteggi per valutare i singoli effetti.

- GitHub [Esempi di dati e script](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) per l'ottimizzazione SQL Server

### <a name="test-methods"></a>Metodi di test

1. Il set di dati Airline è costituito da una singola tabella di 10 milioni di righe. È stata scaricata e caricata in blocco in SQL Server.
2. Sono state effettuate sei copie della tabella.
3. Diverse modifiche sono state applicate alle copie della tabella, per testare SQL Server funzionalità, ad esempio la compressione di pagina, la compressione di riga, l'indicizzazione, l'archivio dati a colonne e così via.
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
2. Un modello di regressione logistica è stato creato in base ai dati della tabella. Il valore di *rowsPerRead* per ogni test è stato impostato su 500000.
3. I punteggi sono stati generati usando il modello sottoposto a training
4. Ogni test è stato eseguito sei volte. L'ora della prima esecuzione ("esecuzione a freddo") è stata eliminata. Per consentire l'outlier occasionale, è stato eliminato anche il tempo **massimo** tra le cinque esecuzioni rimanenti. La media delle quattro esecuzioni rimanenti è stata usata per calcolare il runtime trascorso medio di ogni test.
5. I test sono stati eseguiti utilizzando il parametro *reportProgress* con il valore 3 (= intervalli di report e stato di avanzamento). Ogni file di output contiene informazioni relative al tempo impiegato per i/o, tempo di transizione e tempo di calcolo. Questi tempi sono utili per la diagnosi e la risoluzione dei problemi.
6. Anche l'output della console è stato indirizzato a un file nella directory di output.
7. Gli script di test hanno elaborato i tempi in questi file per calcolare il tempo medio per le esecuzioni.

I risultati seguenti, ad esempio, sono i tempi di un singolo test. I principali intervalli di interesse sono quelli relativi al **tempo di lettura totale** (tempo di I/O) e al **tempo di transizione** (overhead nell'impostazione dei processi per il calcolo).

**Intervalli di campionamento**

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

Si consiglia di scaricare e modificare gli script di test per semplificare la risoluzione dei problemi relativi a R Services o con funzioni RevoScaleR.

### <a name="test-results-all"></a>Risultati test (tutti)

In questa sezione vengono confrontati i risultati prima e dopo per ogni test.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>Dimensioni dei dati con compressione e un archivio tabelle a colonne

Il primo test ha confrontato l'utilizzo della compressione e di una tabella a colonne per ridurre le dimensioni dei dati.

| Nome tabella            | Righe     | Riservato   | Data       | index_size | Non utilizzato  | % salvataggio (riservato) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | n/d        | 368 KB  | 93%                 |

**Conclusioni**

La riduzione massima della dimensione dei dati è stata realizzata applicando un indice columnstore, seguito dalla compressione di pagina.

#### <a name="effects-of-compression"></a>Effetti della compressione

Questo test ha confrontato i vantaggi della compressione di riga, della compressione di pagina e della compressione. È stato eseguito il training `rxLinMod` di un modello utilizzando sui dati di tre diverse tabelle di dati. Per tutte le tabelle sono state usate la stessa formula e la stessa query.

| Nome tabella            | Nome test       | numTasks | Durata media |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression-parallelo| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression-parallelo | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression-parallelo  | 4        | 5.2375       |

**Conclusioni**

Solo la compressione non sembra essere utile. In questo esempio, l'aumento della CPU per gestire la compressione compensa la riduzione del tempo di i/o.

Tuttavia, quando il test viene eseguito in parallelo impostando *numTasks* su 4, il tempo medio diminuisce.

Per set di dati di dimensioni maggiori, l'effetto della compressione può essere più evidente. La compressione dipende dal set di dati e dai valori, pertanto potrebbe essere necessaria una sperimentazione per determinare l'effetto della compressione sul set di dati.

### <a name="effect-of-windows-power-plan-options"></a>Effetto delle opzioni di combinazione per il risparmio di energia di Windows

In questo esperimento `rxLinMod` è stato usato con la tabella *airlineWithIntCol*. La combinazione per il risparmio di energia di Windows è stata impostata su **prestazioni**bilanciate o elevate. Per tutti i test, *numTasks* è stato impostato su 1. Il test è stato eseguito sei volte ed è stato eseguito due volte sotto entrambe le opzioni di risparmio energia per esaminare la variabilità dei risultati.

Opzione di risparmio energia a **prestazioni elevate** :

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

Il tempo di esecuzione è più coerente e più veloce quando si usa la combinazione per il risparmio di energia di Windows **High Performance** .

#### <a name="using-integer-vs-strings-in-formulas"></a>Utilizzo di Integer rispetto a stringhe nelle formule

Questo test ha valutato l'effetto della modifica del codice R per evitare un problema comune con i fattori di stringa. In particolare, è stato eseguito il `rxLinMod` training di un modello utilizzando due tabelle: nel primo, i fattori vengono archiviati come stringhe. nella seconda tabella, i fattori vengono archiviati come numeri interi.

+ Per la tabella *Airline* la colonna [DayOfWeek] contiene stringhe. Il parametro _colInfo_ è stato usato per specificare i livelli di fattore (Monday, Tuesday,...)

+  Per la tabella *airlineWithIndex* , [DayOfWeek] è un numero intero. Il parametro _colInfo_ non è stato specificato.

+ In entrambi i casi è stata usata la stessa formula: `ArrDelay ~ CRSDepTime + DayOfWeek`.

| Nome tabella          | Nome test   | Durata media |
|---------------------|-------------|--------------|
| *Aerei*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**Conclusioni**

Quando si usano numeri interi anziché stringhe per i fattori, il vantaggio è evidente.

### <a name="avoiding-transformation-functions"></a>Evitare le funzioni di trasformazione

In questo test è stato eseguito il training di `rxLinMod`un modello utilizzando, ma il codice è stato modificato tra le due esecuzioni:

+ Nella prima esecuzione è stata applicata una funzione di trasformazione nell'ambito della compilazione del modello. 
+ Nella seconda esecuzione, i valori delle funzionalità sono stati precalcolati e disponibili, in modo che non fosse richiesta alcuna funzione di trasformazione.

| Nome test             | Durata media |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**Conclusioni**

Il tempo di training è stato più breve quando **non** si utilizza una funzione di trasformazione. In altre parole, il training del modello è stato eseguito più velocemente quando si utilizzano colonne che sono pre-calcolate e rese permanente nella tabella.

Il risparmio dovrebbe essere maggiore se sono presenti molte altre trasformazioni e il set di dati è più grande (\> 100m).

### <a name="using-columnar-store"></a>Uso dell'archivio a colonne

Questo test ha valutato i vantaggi in merito alle prestazioni dell'uso di un archivio dati a colonne e di un indice. Lo stesso modello è stato sottoposto a training utilizzando `rxLinMod` e nessuna trasformazione dei dati.

+ Nella prima esecuzione la tabella dati usava un archivio di righe standard.
+ Nella seconda esecuzione è stato usato un archivio colonne.

| Nome tabella         | Nome test | Durata media |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**Conclusioni**

Le prestazioni sono migliori con l'archivio a colonne rispetto all'archivio righe standard. Una differenza significativa nelle prestazioni può essere prevista per set di dati di\> dimensioni maggiori (100 M).

### <a name="effect-of-using-the-cube-parameter"></a>Effetto dell'utilizzo del parametro Cube

Lo scopo di questo test è determinare se l'opzione in RevoScaleR per l'utilizzo del parametro del **cubo** pre-calcolato può migliorare le prestazioni. È stato eseguito il training `rxLinMod`di un modello usando, usando la formula seguente:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

Nella tabella i fattori *DayOfWeek* vengono archiviati sotto forma di stringa.

| Nome test     | Parametro cube | numTasks | Durata media | Stima di riga singola (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**Conclusioni**

L'utilizzo dell'argomento del parametro Cube consente di migliorare chiaramente le prestazioni.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>Effetto della modifica di maxDepth per i modelli rxDTree

In questo esperimento, l' `rxDTree` algoritmo è stato usato per creare un modello nella tabella *airlineColumnar* . Per questo test *numTasks* è stato impostato su 4. Sono stati usati diversi valori per *MaxDepth* per dimostrare come la modifica della profondità dell'albero influisca sulla fase di esecuzione.

| Nome test       | maxDepth | Durata media |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**Conclusioni**

Con l'aumentare della profondità dell'albero, il numero totale di nodi aumenta in modo esponenziale. Anche il tempo trascorso per la creazione del modello è aumentato in modo significativo.

### <a name="prediction-on-a-stored-model"></a>Stima su un modello archiviato

Lo scopo di questo test è determinare l'effetto sulle prestazioni durante il punteggio quando il modello sottoposto a training viene salvato in una tabella SQL Server anziché essere generato come parte del codice attualmente in esecuzione. Per l'assegnazione dei punteggi, il modello archiviato viene caricato dal database e le stime vengono create usando un frame di dati a una riga in memoria (contesto di calcolo locale).

I risultati del test mostrano il tempo necessario per salvare il modello e il tempo impiegato per caricare il modello e stimare.

| Nome tabella | Nome test | Tempo medio (per il training del modello) | Tempo di salvataggio/caricamento del modello|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2,09 (include il tempo per la stima) |

**Conclusioni**

Il caricamento di un modello sottoposto a training da una tabella è chiaramente un modo più rapido per eseguire stime. Si consiglia di evitare di creare il modello ed eseguire il Punteggio all nello stesso script.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>Case Study: Ottimizzazione per l'attività Resume-matching

Il modello Resume-matching è stato sviluppato da Microsoft Data Scientist ke Huang per testare le prestazioni del codice R in SQL Server e consentendo ai data scientist di creare soluzioni scalabili e di livello aziendale.

### <a name="methods"></a>Metodi

Entrambi i pacchetti RevoScaleR e MicrosoftML sono stati usati per eseguire il training di un modello predittivo in una soluzione R complessa che include set di impostazioni di grandi dimensioni. Le query SQL e il codice R erano identici in tutti i test. I test sono stati eseguiti in una singola macchina virtuale di Azure con SQL Server installato. L'autore ha quindi confrontato i tempi di assegnazione dei punteggi con e senza le seguenti ottimizzazioni fornite da SQL Server:

- Tabelle in memoria
- Soft-NUMA
- Resource Governor

Per valutare l'effetto di soft-NUMA sull'esecuzione di script R, il team di data science ha testato la soluzione in una macchina virtuale di Azure con 20 core fisici. In questi core fisici sono stati creati automaticamente quattro nodi soft-NUMA, in modo che ogni nodo contenesse cinque core.

Affinitization CPU è stato applicato nello scenario di riattivazione delle corrispondenze, per valutare l'effetto sui processi R. Sono stati creati quattro pool di **risorse SQL** e quattro **pool di risorse esterne** e è stata specificata l'affinità CPU per garantire che in ogni nodo venga usato lo stesso set di CPU.

Ogni pool di risorse è stato assegnato a un gruppo di carico di lavoro diverso per ottimizzare l'utilizzo dell'hardware. Il motivo è che l'affinità soft-NUMA e CPU non può dividere la memoria fisica nei nodi NUMA fisici. Pertanto, per definizione, tutti i nodi NUMA Soft basati sullo stesso nodo NUMA fisico devono usare la memoria nello stesso blocco di memoria del sistema operativo. In altre parole, non esiste alcuna affinità tra memoria e processore.

Per creare questa configurazione è stato usato il processo seguente:

1. Ridurre la quantità di memoria allocata per impostazione predefinita a SQL Server.

2. Creare quattro nuovi pool per l'esecuzione di processi R in parallelo.

3. Creare quattro gruppi di carico di lavoro in modo che ogni gruppo di carico di lavoro sia associato a un pool di risorse.

4. Riavviare Resource Governor con i nuovi gruppi del carico di lavoro e le assegnazioni.

5. Creare una funzione di classificazione definita dall'utente (UDF) per assegnare diverse attività in gruppi di carico di lavoro diversi.

6. Aggiornare la configurazione di Resource Governor per usare la funzione per i gruppi del carico di lavoro appropriati.

### <a name="results"></a>Risultati

La configurazione che ha avuto prestazioni ottimali nello studio di riattivazione delle corrispondenze è la seguente:

-   Quattro pool di risorse interni (per SQL Server)

-   Quattro pool di risorse esterne (per i processi di script esterni)

-   Ogni pool di risorse è associato a un gruppo di carico di lavoro specifico

-   Ogni pool di risorse viene assegnato a CPU diverse

-   Utilizzo massimo memoria interna (per SQL Server) = 30%

-   Memoria massima per l'uso da sessioni R = 70%

Per il modello di corrispondenza di riattivazione, l'uso di script esterni era elevato e non erano in esecuzione altri servizi del motore di database. Pertanto, le risorse allocate per gli script esterni sono state aumentate al 70%, che ha dimostrato la migliore configurazione per le prestazioni dello script.

Questa configurazione è stata raggiunta mediante la sperimentazione di valori diversi. Se si utilizza hardware diverso o una soluzione diversa, la configurazione ottimale potrebbe essere diversa. Provare sempre a trovare la configurazione migliore per il caso.

Nella soluzione ottimizzata, 1,1 milioni righe di dati (con le funzionalità 100) sono state classificate in 8,5 secondi in un computer con 20 Core. Le ottimizzazioni hanno migliorato significativamente le prestazioni in termini di tempo di assegnazione dei punteggi.

I risultati suggerivano anche che il **numero di funzionalità** ha avuto un impatto significativo sul tempo di assegnazione dei punteggi. Il miglioramento era ancora più importante quando nel modello di stima venivano utilizzate più funzionalità.

È consigliabile leggere questo articolo di Blog e l'esercitazione di accompagnamento per una discussione dettagliata.

-   [Suggerimenti e consigli sull'ottimizzazione per Machine Learning in SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

Molti utenti hanno notato una piccola pausa in quanto il runtime di R (o Python) viene caricato per la prima volta. Per questo motivo, come descritto in questi test, il tempo per la prima esecuzione viene spesso misurato ma successivamente scartato. La memorizzazione nella cache successiva può comportare notevoli differenze nelle prestazioni tra la prima e la seconda esecuzione. Si verifica anche un sovraccarico quando i dati vengono spostati tra SQL Server e il runtime esterno, in particolare se i dati vengono passati in rete anziché essere caricati direttamente da SQL Server.

Per tutti questi motivi, non esiste una singola soluzione per attenuare questo tempo di caricamento iniziale, in quanto l'effetto sulle prestazioni varia in modo significativo a seconda dell'attività. Ad esempio, la memorizzazione nella cache viene eseguita per il punteggio a riga singola in batch; di conseguenza, le operazioni di assegnazione dei punteggi successive sono molto più veloci e il modello o il runtime R non viene ricaricato. È anche possibile usare il [Punteggio nativo](../sql-native-scoring.md) per evitare di caricare completamente il runtime di R.

Per il training di modelli di grandi dimensioni o per il punteggio in batch di grandi dimensioni, l'overhead potrebbe essere minimo rispetto ai vantaggi derivanti dall'evitare lo spostamento dei dati o da flussi e elaborazione parallela. Per informazioni aggiuntive sulle prestazioni, vedere questo post di Blog:

+ [Uso di R per rilevare frodi a 1 milione transazioni al secondo](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>Risorse

Di seguito sono riportati i collegamenti a informazioni, strumenti e script usati nello sviluppo di questi test.

+ Script di test delle prestazioni e collegamenti ai dati: [Esempi di dati e script per l'ottimizzazione SQL Server](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Articolo che descrive la soluzione di riattivazione delle corrispondenze: [Suggerimenti per l'ottimizzazione per R Services per SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ Script usati nell'ottimizzazione SQL per la soluzione di riattivazione delle corrispondenze: [Repository GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>Informazioni sulla gestione di Windows Server

+ [How to determine the appropriate page file size for 64-bit versions of Windows](https://support.microsoft.com/kb/2860880) (Come determinare le dimensioni appropriate del file di paging per le versioni a 64 bit di Windows)

+ [Informazioni su NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [Modalità di supporto di NUMA in SQL Server](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>Informazioni sulle ottimizzazioni di SQL Server

+ [Riorganizzare e ricompilare gli indici](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [Introduzione alle tabelle con ottimizzazione per la memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [Dimostrazione: Miglioramento delle prestazioni di OLTP in memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [Compressione dei dati](../../relational-databases/data-compression/data-compression.md)

+ [Abilitare la compressione in una tabella o un indice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Disabilitare la compressione in una tabella o un indice](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>Informazioni sulla gestione di SQL Server

+ [Monitoraggio e ottimizzazione delle prestazioni](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)

+ [Introduzione a Resource Governor](https://technet.microsoft.com/library/bb895232.aspx)

+ [Governance delle risorse per R Services](resource-governance-for-r-services.md)

+ [Come creare un pool di risorse per R](how-to-create-a-resource-pool-for-r.md)

+ [Esempio di configurazione di Resource Governor](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Strumenti

+ [Strumento di generazione del carico di archiviazione e di test delle prestazioni DISKSPD](https://github.com/microsoft/diskspd)

+ [Informazioni di riferimento sull'utilità FSUtil](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>Altri articoli in questa serie

[Ottimizzazione delle prestazioni per R-introduzione](sql-server-r-services-performance-tuning.md)

[Ottimizzazione delle prestazioni per la configurazione di R SQL Server](sql-server-configuration-r-services.md)

[Ottimizzazione delle prestazioni per il codice R-R e l'ottimizzazione dei dati](r-and-data-optimization-r-services.md)

[Ottimizzazione delle prestazioni-case study risultati](performance-case-study-r-services.md)
