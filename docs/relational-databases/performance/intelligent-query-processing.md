---
title: Elaborazione di query intelligenti nei database Microsoft SQL | Microsoft Docs
description: Funzionalità di elaborazione di query intelligenti e miglioramento delle prestazioni delle query in SQL Server e nel database SQL di Azure.
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1b92bc15079fcc85212ea3d1b51be64a3348a4b1
ms.sourcegitcommit: 2663063e29f2868ee6b6d596df4b2af2d22ade6f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305369"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>Elaborazione di query intelligenti nei database SQL

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

La famiglia di funzionalità di elaborazione di query intelligenti include funzionalità ad ampio spettro. Tali funzionalità migliorano le prestazioni di carichi di lavoro esistenti con il minimo sforzo dal punto di vista dell'implementazione. Per trarre automaticamente vantaggio da questa famiglia di funzionalità, passare al livello di compatibilità del database applicabile.

| **Funzionalità di elaborazione di query intelligenti** | **Supporto nel database SQL di Azure** | **Supporto in SQL Server** |
| --- | --- | --- |
| [Join adattivi (modalità batch)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#batch-mode-adaptive-joins) | Sì, nel livello di compatibilità 140| Sì, a partire da SQL Server 2017 nel livello di compatibilità 140|
| [Count Distinct approssimato](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#approximate-query-processing) | Sì, anteprima pubblica| Sì, a partire da SQL Server 2019 CTP 2.0, anteprima pubblica|
| [Modalità batch per rowstore](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-on-rowstore) | Sì, nel livello di compatibilità 150, anteprima pubblica| Sì, a partire da SQL Server 2019 CTP 2.0 nel livello di compatibilità 150, anteprima pubblica|
| [Esecuzione interleaved](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#interleaved-execution-for-multi-statement-table-valued-functions) | Sì, nel livello di compatibilità 140| Sì, a partire da SQL Server 2017 nel livello di compatibilità 140|
| [Feedback delle concessioni di memoria (modalità batch)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#batch-mode-memory-grant-feedback) | Sì, nel livello di compatibilità 140| Sì, a partire da SQL Server 2017 nel livello di compatibilità 140|
| [Feedback delle concessioni di memoria (modalità riga)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#row-mode-memory-grant-feedback) | Sì, nel livello di compatibilità 150, anteprima pubblica| Sì, a partire da SQL Server 2019 CTP 2.0 nel livello di compatibilità 150, anteprima pubblica|
| [Inlining di funzioni definite dall'utente scalari](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#scalar-udf-inlining) | No, ma sarà supportato in una versione futura | Sì, a partire da SQL Server 2019 CTP 2.1 nel livello di compatibilità 150, anteprima pubblica|
| [Compilazione posticipata delle variabili di tabella](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#table-variable-deferred-compilation) | Sì, nel livello di compatibilità 150, anteprima pubblica| Sì, a partire da SQL Server 2019 CTP 2.0 nel livello di compatibilità 150, anteprima pubblica|



## <a name="adaptive-query-processing"></a>Elaborazione di query adattive

La famiglia di funzionalità di elaborazione di query adattive include i miglioramenti seguenti all'elaborazione di query adattive. Questi miglioramenti adattano le strategie di ottimizzazione alle condizioni di runtime del carico di lavoro dell'applicazione: 
- Join adattivi in modalità batch
- Feedback della concessione di memoria
- Esecuzione interleaved per funzioni con valori di tabella a più istruzioni

### <a name="batch-mode-adaptive-joins"></a>Join adattivi in modalità batch

Con questa funzionalità, il piano può passare in modo dinamico a una strategia di join più efficace durante l'esecuzione usando un singolo piano memorizzato nella cache.

Per altre informazioni sui join adattivi in modalità batch, vedere [Elaborazione di query adattive nei database SQL](../../relational-databases/performance/adaptive-query-processing.md).

### <a name="row-and-batch-mode-memory-grant-feedback"></a>Disabilita il feedback delle concessioni di memoria in modalità riga e batch

> [!NOTE]
> Il feedback delle concessioni di memoria in modalità riga è una funzionalità di anteprima pubblica.  

Questa funzionalità ricalcola la memoria effettiva necessaria per una query, quindi aggiorna il valore della concessione per il piano nella cache. Riduce il numero eccessivo di concessioni che limita la concorrenza. Questa funzionalità corregge anche il numero non sufficiente di concessioni che causa costose distribuzioni su disco.

Per altre informazioni sul feedback delle concessioni di memoria, vedere [Elaborazione di query adattive nei database SQL](../../relational-databases/performance/adaptive-query-processing.md).

### <a name="interleaved-execution-for-mstvfs"></a>Esecuzione interleaved per funzioni con valori di tabella con più istruzioni

Con l'esecuzione interleaved, il conteggio effettivo delle righe viene usato per adottare decisioni più mirate relativamente a un piano di query downstream. Per altre informazioni sulle funzioni con valori di tabella con più istruzioni, vedere [Funzione con valori di tabella](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF).

Per altre informazioni sull'esecuzione interleaved, vedere [Elaborazione di query adattive nei database SQL](../../relational-databases/performance/adaptive-query-processing.md).

## <a name="table-variable-deferred-compilation"></a>Compilazione posticipata delle variabili di tabella

> [!NOTE]
> La compilazione posticipata delle variabili di tabella è una funzionalità di anteprima pubblica.  

La compilazione posticipata delle variabili di tabella migliora la qualità del piano e le prestazioni generali per le query che fanno riferimento a variabili di tabella. Durante l'ottimizzazione e la compilazione iniziale, questa funzionalità propaga le stime della cardinalità basate sui conteggi effettivi delle righe di variabili di tabella. Queste informazioni accurate sui conteggi di righe ottimizzano le operazioni del piano downstream.

La compilazione posticipata delle variabili di tabella posticipa la compilazione di un'istruzione che fa riferimento a una variabile di tabella viene fino alla prima esecuzione effettiva dell'istruzione. Questo comportamento di compilazione posticipata è uguale a quello delle tabelle temporanee. Questa modifica determina l'uso della cardinalità effettiva invece dell'ipotesi originale basata su una sola riga. 

È possibile abilitare l'anteprima pubblica della compilazione posticipata delle variabili di tabella nel database SQL di Azure. A tale scopo, abilitare la compatibilità di livello 150 per il database a cui si è connessi quando si esegue la query.

Per altre informazioni, vedere [Compilazione posticipata delle variabili di tabella](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation).

## <a name="scalar-udf-inlining"></a>Inlining di funzioni definite dall'utente scalari

> [!NOTE]
> L'inlining di funzioni definite dall'utente scalari è una funzionalità di anteprima pubblica.  

L'inlining di funzioni definite dall'utente scalari trasforma automaticamente le [funzioni definite dall'utente scalari](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar) in espressioni relazionali e le incorpora nella query SQL chiamante. Questa trasformazione migliora le prestazioni dei carichi di lavoro che sfruttano le funzioni definite dall'utente scalari. L'inlining di funzioni definite dall'utente scalari facilita l'ottimizzazione basata sui costi delle operazioni all'interno delle funzioni definite dall'utente. I risultati sono efficienti, orientati ai set e paralleli, al contrario dei piani di esecuzione seriale iterativi e poco efficienti. Questa funzionalità è abilitata per impostazione predefinita nel livello di compatibilità del database 150.

Per altre informazioni, vedere [Inlining di funzioni definite dall'utente scalari](../user-defined-functions/scalar-udf-inlining.md).

## <a name="approximate-query-processing"></a>Elaborazione delle query approssimativa

> [!NOTE]
> **APPROX_COUNT_DISTINCT** è una funzionalità in anteprima pubblica.  

L'elaborazione delle query approssimativa è una nuova famiglia di funzionalità, che aggrega set di dati di grandi dimensioni in cui la velocità di risposta è più importante della precisione assoluta. Un esempio è il calcolo di **COUNT(DISTINCT())** su 10 miliardi di righe, per la visualizzazione in un dashboard. In questo caso, la precisione assoluta non è importante, ma la velocità di risposta è fondamentale. La nuova funzione di aggregazione **APPROX_COUNT_DISTINCT** restituisce il numero approssimativo di valori univoci non Null in un gruppo.

Per altre informazioni, vedere [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md).

## <a name="batch-mode-on-rowstore"></a>Modalità batch per rowstore 

> [!NOTE]
> La modalità batch per rowstore è una funzionalità in anteprima pubblica.  

La modalità batch per rowstore abilita l'esecuzione in modalità batch per i carichi di lavoro analitici senza richiedere indici columnstore.  Questa funzionalità supporta l'esecuzione in modalità batch e i filtri bitmap per gli heap su disco e gli indici con albero B. La modalità batch per rowstore abilita il supporto per tutti gli operatori esistenti abilitati alla modalità batch.

### <a name="background"></a>Informazioni preliminari

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ha introdotto una nuova funzionalità per accelerare i carichi di lavoro analitici: gli indici columnstore. In ogni versione successiva sono stati estesi i casi d'uso e migliorate le prestazioni degli indici columnstore. Fino ad ora, tutte queste capacità sono state esposte e documentate come una singola funzionalità. Si creano gli indici columnstore nelle tabelle e il carico di lavoro di analisi diventa più veloce. Esistono tuttavia due set di tecnologie correlate ma distinte:
- Con gli indici **columnstore**, le query analitiche accedono solo ai dati nelle colonne necessarie. La compressione di pagina nel formato columnstore è anche più efficace rispetto alla compressione di pagina negli indici **rowstore** tradizionali. 
- Con l'elaborazione in **modalità batch**, gli operatori di query elaborano i dati in modo più efficiente, perché agiscono su un batch di righe invece che su una riga per volta. All'elaborazione in modalità batch sono associati numerosi altri miglioramenti per la scalabilità. Per altre informazioni sulla modalità batch, vedere [Modalità di esecuzione](../../relational-databases/query-processing-architecture-guide.md#execution-modes).

I due set di funzionalità interagiscono per migliorare input/output (I/O) e uso della CPU:
- Usando gli indice columnstore, viene salvata in memoria una quantità maggiore di dati. Questa soluzione consente di ridurre la necessità di I/O.
- L'elaborazione in modalità batch usa in modo più efficiente la CPU.

Le due tecnologie sfruttano i vantaggi reciproci laddove possibile. Ad esempio, le aggregazioni in modalità batch possono essere valutate come parte di un'analisi dell'indice columnstore. Anche l'elaborazione dei dati columnstore compressi con la codifica RLE è molto più efficiente con i join e le aggregazioni in modalità batch. 
 
Le due funzionalità possono essere usate in modo indipendente:
* Per ottenere i piani in modalità riga che usano indici columnstore.
* Per ottenere i piani in modalità batch che usano solo indici rowstore. 

Usando le due funzionalità insieme, si ottengono in genere i risultati migliori. Fino ad ora quindi, SQL Server Query Optimizer ha considerato l'elaborazione in modalità batch solo per le query che coinvolgono almeno una tabella con un indice columnstore.

Gli indici columnstore non sono un'opzione valida per alcune applicazioni. Un'applicazione potrebbe usare altre funzionalità non supportate con gli indici columnstore. Le modifiche sul posto, ad esempio, non sono compatibili con la compressione del columnstore, quindi i trigger non sono supportati nelle tabelle con indici columnstore in cluster, ma soprattutto gli indici columnstore aggiungono un overhead per le istruzioni **DELETE** e **UPDATE**. 

Per alcuni carichi di lavoro ibridi analitico-transazionali, l'overhead per gli aspetti transazionali di un carico di lavoro è maggiore dei vantaggi offerti dagli indici columnstore. In tali scenari è possibile migliorare l'uso della CPU con l'elaborazione in modalità batch da sola. Ecco perché la modalità batch nella funzionalità rowstore prende in considerazione la modalità batch per tutte le query, indipendentemente da quali indici sono coinvolti.

### <a name="workloads-that-might-benefit-from-batch-mode-on-rowstore"></a>Carichi di lavoro che possono trarre vantaggio dalla modalità batch per rowstore

I carichi di lavoro seguenti possono trarre vantaggio dalla modalità batch per rowstore:
* Una parte significativa del carico di lavoro è costituita da query analitiche. In genere, queste query hanno operatori come join o aggregazioni che elaborano centinaia di migliaia di righe o più.
* Il carico di lavoro è basato sulla CPU. Se il collo di bottiglia sono le operazioni di I/O, è comunque consigliabile prendere in considerazione un indice columnstore, se possibile.
* La creazione di un indice columnstore aggiunge un overhead eccessivo alla parte transazionale del carico di lavoro oppure la creazione di un indice columnstore non è implementabile perché l'applicazione dipende da una funzionalità non ancora supportata con gli indici columnstore.

> [!NOTE]
> La modalità batch per rowstore consente solo di ridurre l'utilizzo della CPU. Se il collo di bottiglia è relativo alle operazioni di I/O e i dati non sono già memorizzati nella cache (cache "a freddo"), la modalità batch per rowstore non ridurrà il tempo trascorso. Analogamente, se la memoria del computer non è sufficiente per memorizzare nella cache tutti i dati, un miglioramento delle prestazioni è improbabile.

### <a name="what-changes-with-batch-mode-on-rowstore"></a>Che cosa cambia con la modalità batch per rowstore

A parte passare al livello di compatibilità 150, non è necessario modificare nulla per abilitare la modalità batch per rowstore per i carichi di lavoro candidati.

Anche se una query non coinvolge alcuna tabella con un indice columnstore, Query Processor si affida ora all'euristica per decidere se prendere in considerazione la modalità batch. L'euristica è costituita da questi controlli:
1. Un controllo iniziale delle dimensioni delle tabelle, degli operatori usati e delle cardinalità stimate nella query di input.
2. Checkpoint aggiuntivi, man mano che Query Optimizer individua piani nuovi e più economici per la query. Se questi piani alternativi non usano in modo significativo la modalità batch, Query Optimizer smette di esplorare le alternative in modalità batch.

Se la modalità batch per rowstore viene usata, la modalità di esecuzione effettiva visualizzata nel piano di query è la **modalità batch**. L'operatore di analisi usa la modalità batch per gli heap su disco e gli indici albero B. Questa analisi in modalità batch può valutare i filtri bitmap in modalità batch. Nel piano è possibile vedere anche altri operatori della modalità batch. Alcuni esempi sono gli hash join, le aggregazioni basate su hash, gli ordinamenti, le aggregazioni finestra, i filtri, la concatenazione e gli operatori scalari di calcolo.

### <a name="remarks"></a>Remarks

* I piani di query non usano sempre la modalità batch. Query Optimizer potrebbe decidere che la modalità batch non è utile per la query. 
* Lo spazio di ricerca di Query Optimizer cambia. Il piano in modalità riga eventualmente ottenuto potrebbe quindi non essere uguale a quello ottenuto a un livello di compatibilità inferiore e il piano in modalità batch eventualmente ottenuto potrebbe non essere uguale a quello ottenuto con un indice columnstore. 
* I piani potrebbero anche cambiare per le query che combinano gli indici columnstore e rowstore a causa della nuova analisi rowstore in modalità batch.
* Esistono attualmente alcune limitazioni per la nuova modalità batch per analisi di rowstore: 
    * Non verrà applicata per le tabelle OLTP in memoria o per qualsiasi indice diverso da heap su disco e alberi B. 
    * Non verrà neanche attivata in caso di recupero o filtro di una colonna LOB (Large Object). Questa limitazione include set di colonne di tipo sparse e colonne XML.
* Esistono query per le quali la modalità batch non viene usata neppure con gli indici columnstore. Un esempio sono le query che richiedono cursori. Queste stesse esclusioni vengono estese anche alla modalità batch per rowstore.

### <a name="configure-batch-mode-on-rowstore"></a>Configurare la modalità batch per rowstore

La configurazione con ambito database **BATCH_MODE_ON_ROWSTORE** è attiva per impostazione predefinita. Disabilita la modalità batch per rowstore senza richiedere modifiche nel livello di compatibilità del database:

```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```

È possibile disabilitare la modalità batch per rowstore tramite la configurazione con ambito database. È tuttavia possibile eseguire l'override dell'impostazione a livello di query usando l'hint per la query **ALLOW_BATCH_MODE**. L'esempio seguente abilita la modalità batch per rowstore anche con la funzionalità disabilitata tramite la configurazione con ambito database:

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```

È anche possibile disabilitare la modalità batch per rowstore per una query specifica usando l'hint per la query **DISALLOW_BATCH_MODE**. Vedere l'esempio seguente:

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('DISALLOW_BATCH_MODE'));
```

## <a name="see-also"></a>Vedere anche

[Centro prestazioni per il motore di database di SQL Server e il database SQL di Azure](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[Guida sull'architettura di elaborazione delle query](../../relational-databases/query-processing-architecture-guide.md)    
[Guida di riferimento a operatori Showplan logici e fisici](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Join](../../relational-databases/performance/joins.md)    
[Demonstrating Adaptive Query Processing](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)      (Dimostrazione dell'elaborazione di query adattive)  
[Demonstrating Intelligent QP](https://github.com/joesackmsft/Conferences/blob/master/IQPDemos/IQP_Demo_ReadMe.md) (Dimostrazione di Query Processor intelligente)   
