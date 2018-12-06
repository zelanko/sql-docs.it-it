---
title: Elaborazione di query intelligenti nei database Microsoft SQL | Microsoft Docs
description: Funzionalità di elaborazione di query intelligenti e miglioramento delle prestazioni delle query in SQL Server e nel database SQL di Azure.
ms.custom: ''
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d48f9fd87ff375a518b038d9ed4ef4a8d42675cc
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52403926"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>Elaborazione di query intelligenti nei database SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

La famiglia di funzionalità di **elaborazione di query intelligenti** include funzionalità ad ampio spettro che migliorano le prestazioni di carichi di lavoro esistenti con un impegno minimo per l'implementazione.

![Funzionalità di elaborazione di query intelligenti](./media/3_IQPFeatureFamily.png)

## <a name="adaptive-query-processing"></a>Elaborazione di query adattive
La famiglia di funzionalità di elaborazione di query adattive include miglioramenti di elaborazione delle query che adattano le strategie di ottimizzazione alle condizioni di runtime del carico di lavoro dell'applicazione. Fanno parte di questi miglioramenti: 
-  Join adattivi in modalità batch
-  Feedback della concessione di memoria
-  Esecuzione interleaved per funzioni con valori di tabella a più istruzioni

### <a name="batch-mode-adaptive-joins"></a>Join adattivi in modalità batch
Questa funzionalità consente al piano di passare in modo dinamico a una strategia di join più efficace durante l'esecuzione di un singolo piano memorizzato nella cache.

Per altre informazioni sui join adattivi in modalità batch, vedere [Elaborazione di query adattive nei database SQL](../../relational-databases/performance/adaptive-query-processing.md).

### <a name="row-and-batch-mode-memory-grant-feedback"></a>Disabilita il feedback delle concessioni di memoria in modalità riga e batch
> [!NOTE]
> Il feedback delle concessioni di memoria in modalità riga è una funzionalità di anteprima pubblica.  

Questa funzionalità ricalcola la memoria effettiva necessaria per una query e poi aggiorna il valore di concessione per il piano memorizzato nella cache, riducendo il numero eccessivo di concessioni che limita la concorrenza e correggendo il numero insufficiente di concessioni che causa costose distribuzioni su disco.

Per altre informazioni sul feedback delle concessioni di memoria, vedere [Elaborazione di query adattive nei database SQL](../../relational-databases/performance/adaptive-query-processing.md).

### <a name="interleaved-execution-for-multi-statement-table-valued-functions-mstvfs"></a>Esecuzione interleaved per funzioni con valori di tabella a più istruzioni
Con l'esecuzione interleaved, il conteggio effettivo delle righe viene usato per adottare decisioni più mirate relativamente a un piano di query downstream. Per ulteriori informazioni sulle funzioni con valori di tabella con più istruzioni, vedere [Funzione con valori di tabella](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF).

Per altre informazioni sull'esecuzione interleaved, vedere [Elaborazione di query adattive nei database SQL](../../relational-databases/performance/adaptive-query-processing.md).

## <a name="table-variable-deferred-compilation"></a>Compilazione posticipata delle variabili di tabella
> [!NOTE]
> La compilazione posticipata delle variabili di tabella è una funzionalità di anteprima pubblica.  

La compilazione posticipata delle variabili di tabella migliora la qualità del piano e le prestazioni generali per le query che fanno riferimento a variabili di tabella. Durante l'ottimizzazione e la compilazione iniziale, questa funzionalità propagherà le stime della cardinalità basate sui conteggi effettivi delle righe di variabili di tabella.  Queste informazioni accurate sui conteggi di righe verranno usate per l'ottimizzazione delle operazioni del piano downstream.

Con la compilazione posticipata delle variabili di tabella, la compilazione di un'istruzione che fa riferimento a una variabile di tabella viene posticipata fino alla prima esecuzione effettiva dell'istruzione. Questo comportamento di compilazione posticipata è identico a quello delle tabelle temporanee e con questo cambiamento viene usata la cardinalità effettiva invece dell'ipotesi originale basata su una sola riga. Per abilitare l'anteprima pubblica della compilazione posticipata delle variabili di tabella nel database SQL di Azure, abilitare il livello di compatibilità del database 150 per il database a cui si è connessi quando si esegue la query.

Per altre informazioni, vedere [Compilazione posticipata delle variabili di tabella](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation ).

## <a name="scalar-udf-inlining"></a>Inlining di funzioni definite dall'utente scalari
> [!NOTE]
> L'inlining di funzioni definite dall'utente scalari è una funzionalità di anteprima pubblica.  

L'inlining di funzioni definite dall'utente scalari trasforma automaticamente le [funzioni definite dall'utente (UDF) scalari](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar) in espressioni relazionali e le incorpora nella query SQL chiamante, migliorando così le prestazioni dei carichi di lavoro che usano funzioni definite dall'utente scalari. L'inlining di funzioni definite dall'utente scalari facilita l'ottimizzazione basata sui costi delle operazioni all'interno di funzioni definite dall'utente e genera piani efficienti orientati ai set e paralleli, invece di piani di esecuzione seriali, inefficienti e iterativi. Questa funzionalità è abilitata per impostazione predefinita nel livello di compatibilità del database 150.

Per altre informazioni, vedere [Inlining di funzioni definite dall'utente scalari](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining?view=sqlallproducts-allversions).

## <a name="approximate-query-processing"></a>Elaborazione delle query approssimativa
> [!NOTE]
> APPROX_COUNT_DISTINCT è una funzionalità in anteprima pubblica.  

L'elaborazione delle query approssimative è una nuova famiglia di funzionalità progettata per fornire aggregazioni su set di dati di grandi dimensioni in cui la velocità di risposta è più importante della precisione assoluta.  Un esempio potrebbe essere il calcolo di COUNT(DISTINCT()) su 10 miliardi di righe, per la visualizzazione in un dashboard.  In questo caso, la precisione assoluta non è importante, ma la velocità di risposta è fondamentale. La nuova funzione di aggregazione APPROX_COUNT_DISTINCT restituisce il numero approssimativo di valori univoci non Null in un gruppo.

Per altre informazioni, vedere [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md).

## <a name="batch-mode-on-rowstore"></a>Modalità batch per rowstore 
> [!NOTE]
> La modalità batch per rowstore è una funzionalità in anteprima pubblica.  

### <a name="background"></a>Informazioni preliminari
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ha introdotto una nuova funzionalità per l'accelerazione dei carichi di lavoro analitici: gli indici columnstore. In ogni versione successiva sono stati estesi i casi d'uso e migliorate le prestazioni degli indici columnstore. Fino ad ora, tutte queste capacità sono state esposte e documentate come una singola funzionalità: si creano gli indici columnstore per le tabelle e il carico di lavoro analitico "è semplicemente più veloce". Dietro le quinte, tuttavia, esistono due set di tecnologie correlate ma distinte:
- Gli indici **columnstore** consentono alle query analitiche di accedere solo ai dati nelle colonne necessarie. Il formato columnstore supporta inoltre una compressione molto più efficace rispetto al risultato ottenuto con la compressione di pagina negli indici "rowstore" tradizionali. 
- L'elaborazione in **modalità batch** consente agli operatori di query di elaborare i dati in modo più efficiente intervenendo su un batch di righe alla volta, invece che su una riga alla volta. All'elaborazione in modalità batch sono associati numerosi altri miglioramenti per la scalabilità. Per altre informazioni sulla modalità batch, vedere [Modalità di esecuzione](../../relational-databases/query-processing-architecture-guide.md#execution-modes).

I due set di funzionalità interagiscono per migliorare I/O e utilizzo della CPU:
- Gli indici columnstore consentono di inserire in memoria una maggiore quantità di dati, con conseguente riduzione delle esigenze di I/O.
- L'elaborazione in modalità batch usa in modo più efficiente la CPU.

Le due tecnologie sfruttano i vantaggi reciproci laddove possibile. Ad esempio, le aggregazioni in modalità batch possono essere valutate come parte di un'analisi dell'indice columnstore. Anche l'elaborazione dei dati columnstore compressi con la codifica RLE è molto più efficiente con i join e le aggregazioni in modalità batch. 
 
Le due funzionalità sono già utilizzabili in modo indipendente: è possibile ottenere piani in modalità riga che usano indici columnstore e i piani in modalità batch che usano solo indici rowstore. Tuttavia, poiché nella maggior parte dei casi si ottengono risultati ottimali usando insieme le due funzionalità, Query Optimizer di SQL Server ha finora preso in considerazione l'elaborazione in modalità batch solo per le query che coinvolgono almeno una tabella con un indice columnstore.

Per alcune applicazioni, gli indici columnstore non sono un'opzione praticabile perché l'applicazione usa alcune altre funzionalità non supportate con gli indici columnstore (i trigger non sono supportati per le tabelle con indici columnstore cluster, ad esempio). Ancora più importante, gli indici columnstore comportano maggiore overhead per le istruzioni DELETE e UPDATE, perché le modifiche sul posto non sono compatibili con la compressione del columnstore. Per alcuni carichi di lavoro ibridi analitico-transazionali, i vantaggi offerti dagli indici columnstore per le query analitiche sono minori rispetto all'overhead per gli aspetti transazionali di un carico di lavoro. In tali scenari è possibile ottenere un migliore utilizzo della CPU con l'elaborazione in modalità batch da sola, ed è questo il motivo per cui la funzionalità della **modalità batch per rowstore** prenderà in considerazione la modalità batch per tutte le query, indipendentemente dagli indici interessati.

### <a name="what-workloads-may-benefit-from-batch-mode-on-rowstore"></a>Quali carichi di lavoro possono trarre vantaggio dalla modalità batch per rowstore
I carichi di lavoro seguenti possono trarre vantaggio dalla modalità batch per rowstore:
1.  Una parte significativa del carico di lavoro è costituita da query analitiche (come regola generale, le query con operatori come join o aggregazioni che elaborano centinaia di migliaia di righe o più), **E**
2.  Il carico di lavoro è basato su CPU (se il collo di bottiglia sono le operazioni di I/O è comunque consigliabile prendere in considerazione un indice columnstore, se possibile), **E**
3.  La creazione di un indice columnstore aggiunge un overhead eccessivo per la parte transazionale del carico di lavoro **O** la creazione di un indice columnstore non è possibile perché l'applicazione dipende da una funzionalità che non è ancora supportata con gli indici columnstore.

> [!NOTE]
> La modalità batch per rowstore consente solo di ridurre l'utilizzo di CPU. Se il collo di bottiglia è relativo alle operazioni di I/O e i dati non sono già memorizzati nella cache (cache "a freddo"), la modalità batch per rowstore NON ridurrà il tempo trascorso. Analogamente, se la memoria del computer non è sufficiente per memorizzare nella cache tutti i dati, un miglioramento delle prestazioni è improbabile.

### <a name="what-changes-with-batch-mode-on-rowstore"></a>Cosa cambia con la modalità batch per rowstore
A parte passare al livello di compatibilità 150, non è necessario modificare nulla per abilitare la modalità batch per rowstore per i carichi di lavoro candidati.

Anche se una query non coinvolge alcuna tabella con un indice columnstore, Query Processor si affida ora all'euristica per decidere se prendere in considerazione la modalità batch. L'euristica è costituita da:
1.  Un controllo iniziale delle dimensioni delle tabelle, degli operatori usati e delle cardinalità stimate nella query di input.
2.  Checkpoint aggiuntivi, man mano che Query Optimizer individua piani nuovi e più economici per la query. Se questi piani alternativi non usano in modo significativo la modalità batch, Query Optimizer smetterà di esplorare le alternative in modalità batch.

Se si usa la modalità batch per rowstore, nel piano di esecuzione della query la modalità di esecuzione effettiva sarà indicata come "modalità batch" usata dall'operatore di analisi per gli heap su disco e gli indici albero B.  Questa analisi in modalità batch può valutare i filtri bitmap in modalità batch.  Nel piano è possibile vedere anche altri operatori della modalità batch, ad esempio hash join, aggregazioni basate su hash, ordinamenti, aggregazioni finestra, filtri, concatenazione e operatori scalari di calcolo.

### <a name="remarks"></a>Remarks
1.  Non è garantito che i piani di query usino la modalità batch. Query Optimizer potrebbe decidere che la modalità batch non è utile per la query. 
2.  Dato che lo spazio di ricerca di Query Optimizer cambia, non è garantito che il piano in modalità riga eventualmente ottenuto sia uguale a quello ottenuto a un livello di compatibilità inferiore. Non vi è nemmeno alcuna garanzia che il piano in modalità batch eventualmente ottenuto sia uguale a quello che si otterrebbe con un indice columnstore. 
3.  I piani possono anche cambiare in modo non immediatamente evidente per le query che combinano gli indici columnstore e rowstore, a causa della nuova analisi rowstore in modalità batch.
4.  Limitazioni correnti per la nuova modalità batch per analisi di rowstore: non verrà applicata per le tabelle OLTP in memoria o per qualsiasi indice diverso da heap su disco e alberi B. Non verrà neanche attivata in caso di recupero o filtro di una colonna LOB. Questa limitazione include set di colonne di tipo sparse e colonne XML.
5.  Esistono query per le quali la modalità batch non viene usata anche con gli indici columnstore (ad esempio le query che richiedono cursori) e le stesse esclusioni vengono estese anche alla modalità batch per rowstore.

### <a name="configuring-batch-mode-on-rowstore"></a>Configurazione della modalità batch per rowstore
La configurazione con ambito database BATCH_MODE_ON_ROWSTORE è attivata per impostazione predefinita e può essere usata per disabilitare la modalità batch per rowstore senza richiedere una modifica del livello di compatibilità del database:

```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```

È possibile disabilitare la modalità batch per rowstore tramite la configurazione con ambito database, ma eseguire comunque l'override dell'impostazione a livello di query tramite l'hint per la query ALLOW_BATCH_MODE. L'esempio seguente abilita la modalità batch per rowstore anche con la funzionalità disabilitata tramite la configurazione con ambito database:

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```

È anche possibile disabilitare la modalità batch per rowstore per una query specifica usando l'hint per la query DISALLOW_BATCH_MODE. Ad esempio

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
