---
title: Elaborazione di query adattive nei database Microsoft SQL | Microsoft Docs
description: Funzionalità per l'elaborazione di query adattive e il miglioramento delle prestazioni delle query in SQL Server (2017 e versioni successive) e nel database SQL di Azure.
ms.custom: ''
ms.date: 02/15/2019
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
ms.openlocfilehash: aba4aa388cb9ffac518b09077d535b618206ab71
ms.sourcegitcommit: 769b71f01052ec9b4fc5eb02d9da9a1a58118029
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56319262"
---
# <a name="adaptive-query-processing-in-sql-databases"></a>Elaborazione di query adattive nei database SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Questo articolo presenta funzionalità per l'elaborazione di query adattive che consentono di migliorare le prestazioni delle query in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partire da [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]:
- Feedback delle concessioni di memoria in modalità batch
- Feedback delle concessioni di memoria in modalità riga (anteprima pubblica con livello di compatibilità del database 150)
- Join adattivo in modalità batch
- Esecuzione interleaved

A livello generale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue una query come indicato di seguito:
1. Il processo di ottimizzazione query genera un set di piani di esecuzione possibili per una query specifica. In questa fase viene stimato il costo dei vari piani e viene usato il piano con il costo stimato minore.
1. Il processo di esecuzione query seleziona il piano scelto da Query Optimizer e lo usa per l'esecuzione.

Per altre informazioni sulle modalità di elaborazione ed esecuzione delle query in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere la [Guida sull'architettura di elaborazione delle query](../../relational-databases/query-processing-architecture-guide.md).

In alcuni casi il piano scelto da Query Optimizer non è ottimale per diversi motivi. Ad esempio è possibile che il numero stimato di righe del flusso del piano di query non sia corretto. I costi stimati aiutano a determinare il piano che viene selezionato per l'uso nell'esecuzione. Se le stime di cardinalità non sono corrette viene comunque usato il piano originale anche se le ipotesi di partenza non erano adeguate.

### <a name="how-to-enable-adaptive-query-processing"></a>Come abilitare l'elaborazione di query adattive
È possibile impostare automaticamente i carichi di lavoro come idonei all'elaborazione di query adattive abilitando il livello di compatibilità 140 per il database.  Questa opzione è impostabile con Transact-SQL. Ad esempio  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 140;
```

## <a name="batch-mode-memory-grant-feedback"></a>Feedback delle concessioni di memoria in modalità batch
Un piano post esecuzione di una query in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include la memoria minima richiesta per l'esecuzione e la dimensione della concessione di memoria sufficiente a far sì che tutte le righe siano incluse nella memoria. Se le dimensioni della concessione di memoria non vengono impostate correttamente le prestazioni possono risultare ridotte. Le concessioni di dimensioni eccessive causano memoria non usata e riduzione della concorrenza. Le concessioni di memoria di dimensioni insufficienti causano costose distribuzioni su disco. Incentrandosi sui carichi di lavoro ripetuti, il feedback delle concessioni di memoria in modalità batch ricalcola la memoria effettiva necessaria per una query, quindi aggiorna il valore della concessione per il piano nella cache.  Quando viene eseguita un'istruzione query identica la query usa le dimensioni della concessione di memoria aggiornate, riducendo il numero eccessivo di concessioni che limita la concorrenza e correggendo il numero insufficiente di concessioni che causa costose distribuzioni su disco.
Il grafico seguente visualizza un esempio dell'uso del feedback delle concessioni di memoria in modalità batch. La durata della prima esecuzione della query è pari a  **88 secondi** a causa del numero elevato di distribuzioni:   

```sql
DECLARE @EndTime datetime = '2016-09-22 00:00:00.000';
DECLARE @StartTime datetime = '2016-09-15 00:00:00.000';
SELECT TOP 10 hash_unique_bigint_id
FROM dbo.TelemetryDS
WHERE Timestamp BETWEEN @StartTime and @EndTime
GROUP BY hash_unique_bigint_id
ORDER BY MAX(max_elapsed_time_microsec) DESC;
```

![Numero elevato di distribuzioni](./media/2_AQPGraphHighSpills.png)

Con il feedback delle concessioni di memoria attivato la durata della seconda esecuzione della query si riduce a  **1 secondo** (da 88 secondi), le distribuzioni su disco vengono rimosse completamente e la concessione è superiore: 

![Nessuna distribuzione](./media/3_AQPGraphNoSpills.png)

### <a name="memory-grant-feedback-sizing"></a>Dimensionamento tramite il feedback delle concessioni di memoria
Per una condizione di concessione di memoria di dimensioni eccessive, se la memoria concessa supera di oltre due volte la quantità di memoria realmente usata, il feedback delle concessioni di memoria ricalcola la concessione e aggiorna il piano memorizzato nella cache. I piani con concessioni di memoria di dimensioni inferiori a 1 MB non vengono ricalcolati per le eccedenze.
Per una condizione di concessione di memoria di dimensioni insufficienti che genera distribuzioni su disco per gli operatori in modalità batch, il feedback delle concessioni di memoria attiva il ricalcolo della concessione di memoria. Gli eventi di distribuzione vengono segnalati al feedback delle concessioni di memoria e possono essere esposti con l'evento xEvent *spilling_report_to_memory_grant_feedback*. Questo evento restituisce l'ID del nodo dal piano e il volume dei dati distribuiti su disco da tale nodo.

### <a name="memory-grant-feedback-and-parameter-sensitive-scenarios"></a>Feedback delle concessioni di memoria e scenari dipendenti dai parametri
Per risultati ottimali, valori dei parametri diversi possono richiedere piani di query diversi. Le query di questo tipo sono definite "sensibili ai parametri". Per i piani sensibili ai parametri il feedback delle concessioni di memoria si disattiva quando una query registra requisiti di memoria non stabili. Il piano viene disattivato dopo varie ripetizioni dell'esecuzione della query e la disattivazione può essere rilevata monitorando l'evento xEvent *memory_grant_feedback_loop_disabled*. Per altre informazioni sull'analisi e la sensibilità dei parametri, consultare la [Guida sull'architettura di elaborazione delle query](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing).

### <a name="memory-grant-feedback-caching"></a>Memorizzazione nella cache del feedback delle concessioni di memoria
Il feedback può essere archiviato nel piano memorizzato nella cache per una singola esecuzione. Tuttavia i vantaggi del feedback delle concessioni di memoria appaiono in caso di esecuzioni consecutive dell'istruzione. Questa funzionalità si applica all'esecuzione ripetuta di istruzioni. Il feedback delle concessioni di memoria modifica solo il piano memorizzato nella cache. Attualmente le modifiche non vengono acquisite in Query Store.
Se il piano viene rimosso dalla cache il feedback non viene mantenuto. Il feedback va perduto anche nel caso di un failover. Un'istruzione che usa `OPTION (RECOMPILE)` crea un nuovo piano e non lo memorizza nella cache. Dato che il piano non è memorizzato nella cache il feedback delle concessioni di memoria non viene generato e non viene archiviato per la compilazione e l'esecuzione.  Se tuttavia un'istruzione equivalente (con lo stesso hash di query) che **non** ha usato `OPTION (RECOMPILE)` è stata memorizzata nella cache e quindi rieseguita, l'istruzione consecutiva può trarre vantaggio dal feedback delle concessioni di memoria.

### <a name="tracking-memory-grant-feedback-activity"></a>Rilevamento delle attività di feedback delle concessioni di memoria
È possibile tenere traccia di eventi di feedback delle concessioni di memoria usando l'evento xEvent *memory_grant_updated_by_feedback*. Questo evento rileva la cronologia del conteggio di esecuzione corrente, il numero di volte per il quale il piano è stato aggiornato dal feedback delle concessioni di memoria, la concessione di memoria aggiuntiva ideale prima della modifica e la concessione di memoria aggiuntiva ideale dopo che il feedback delle concessioni di memoria ha modificato il piano salvato nella cache.

### <a name="memory-grant-feedback-resource-governor-and-query-hints"></a>Feedback delle concessioni di memoria, Resource Governor e hint per la query
La memoria concessa reale è conforme al limite di memoria per le query determinato da Resource Governor o dall'hint per la query.

### <a name="disabling-batch-mode-memory-grant-feedback-without-changing-the-compatibility-level"></a>Disabilitazione del feedback delle concessioni di memoria in modalità batch senza modificare il livello di compatibilità
È possibile disabilitare i commenti della concessione di memoria nell'ambito del database o dell'istruzione mantenendo comunque la compatibilità sul livello 140 o superiore. Per disabilitare i commenti della concessione di memoria in modalità batch per tutte le esecuzioni di query provenienti dal database, eseguire l'istruzione seguente all'interno del contesto del database applicabile:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

Quando è abilitata, questa impostazione viene visualizzata come abilitata in [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md).

Per abilitare nuovamente i commenti della concessione di memoria in modalità batch per tutte le esecuzioni di query provenienti dal database, eseguire l'istruzione seguente all'interno del contesto del database applicabile:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

È anche possibile disabilitare i commenti sulla concessione di memoria in modalità batch per una query specifica definendo `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK` come [hint per la query USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint). Ad esempio

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK')); 
```

L'hint per la query USE HINT ha la precedenza rispetto una configurazione con ambito database o un'impostazione del flag di traccia.

## <a name="row-mode-memory-grant-feedback"></a>Feedback delle concessioni di memoria in modalità riga
**Si applica a:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] come funzionalità di anteprima pubblica

> [!NOTE]
> Il feedback delle concessioni di memoria in modalità riga è una funzionalità di anteprima pubblica.  

Il feedback delle concessioni di memoria in modalità riga estende la funzionalità di feedback delle concessioni di memoria in modalità batch adattando le dimensioni delle concessioni di memoria sia per gli operatori in modalità batch che per quelli in modalità riga.  

Per abilitare l'anteprima pubblica dei commenti sulla concessione di memoria in modalità riga in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], abilitare il livello di compatibilità del database 150 per il database a cui si è connessi quando si esegue la query.

L'attività di feedback delle concessioni di memoria in modalità riga sarà visibile tramite l'XEvent **memory_grant_updated_by_feedback**. 

Con il feedback sulla concessione di memoria in modalità riga, vengono visualizzati due nuovi attributi di piano di query per i piani di post-esecuzione effettivi: ***IsMemoryGrantFeedbackAdjusted*** e ***LastRequestedMemory*** aggiunti all'elemento XML del piano di query *MemoryGrantInfo*. 

*LastRequestedMemory* mostra la memoria concessa in kilobyte (KB) dall'esecuzione della query precedente. L'attributo *IsMemoryGrantFeedbackAdjusted* consente di controllare lo stato dei commenti sulla concessione di memoria per l'istruzione all'interno di un piano di esecuzione query effettivo. I valori esposti in questo attributo sono i seguenti:

| Valore di IsMemoryGrantFeedbackAdjusted | Descrizione |
|---|---|
| No: First Execution | Il feedback delle concessioni di memoria non regola la memoria per la prima compilazione e l'esecuzione associata.  |
| No: Accurate Grant | In assenza di spill su disco e se l'istruzione usa almeno il 50% della memoria concessa, il feedback delle concessioni di memoria non viene attivato. |
| No: Feedback disabled | Se il feedback delle concessioni di memoria viene attivato continuamente e alterna tra operazioni di aumento della memoria e riduzione della memoria, il feedback delle concessioni di memoria verrà disabilitato per l'istruzione. |
| Yes: Adjusting | Il feedback delle concessioni di memoria è stato applicato e può essere ulteriormente regolato per l'esecuzione successiva. |
| Yes: Stable | Il feedback delle concessioni di memoria è stato applicato e la memoria concessa è ora stabile, ovvero quella concessa per l'esecuzione precedente è uguale a quella concessa per l'esecuzione corrente. |

> [!NOTE]
> Gli attributi del piano per i commenti sulla concessione di memoria in modalità riga sono visibili nei piani grafici di esecuzione delle query di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] nella versione 17.9 e nelle versioni successive. 

### <a name="disabling-row-mode-memory-grant-feedback-without-changing-the-compatibility-level"></a>Disabilitazione del feedback delle concessioni di memoria in modalità riga senza modificare il livello di compatibilità
È possibile disabilitare il feedback delle concessioni di memoria in modalità riga nell'ambito del database o dell'istruzione mantenendo comunque la compatibilità sul livello 150 o superiore. Per disabilitare il feedback delle concessioni di memoria in modalità riga per tutte le esecuzioni di query provenienti dal database, eseguire l'istruzione seguente all'interno del contesto del database applicabile:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ROW_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

Per riabilitare il feedback delle concessioni di memoria in modalità riga per tutte le esecuzioni di query provenienti dal database, eseguire l'istruzione seguente all'interno del contesto del database applicabile:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ROW_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

È anche possibile disabilitare i commenti sulla concessione di memoria in modalità riga per una query specifica definendo `DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK` come [hint per la query USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint). Ad esempio

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK')); 
```

L'hint per la query USE HINT ha la precedenza rispetto una configurazione con ambito database o un'impostazione del flag di traccia.


## <a name="batch-mode-adaptive-joins"></a>Join adattivi in modalità batch
La funzionalità di join adattivo in modalità batch consente di rimandare a **dopo** la scansione del primo input la scelta tra l'[esecuzione di un metodo hash join e l'esecuzione di un metodo join a cicli annidati](../../relational-databases/performance/joins.md). L'operatore Join adattivo definisce una soglia che viene usata per stabilire quando passare a un piano Cicli annidati. Durante l'esecuzione il piano può pertanto passare a una strategia di join più efficace.
Il funzionamento è il seguente:
-  Se il conteggio delle righe dell'input del join di compilazione è così ridotto che un join a cicli annidati è preferibile a un hash join, il piano passa a un algoritmo a cicli annidati.
-  Se l'input del join di compilazione supera una determinata soglia di numero di righe non si verifica alcun cambiamento e il piano continua con un hash join.

La query seguente illustra un esempio di join adattivo:

```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 360;
```

La query restituisce 336 righe. Se si attiva [Statistiche query dinamiche](../../relational-databases/performance/live-query-statistics.md), viene visualizzato il piano seguente:

![Risultato della query: 336 righe](./media/4_AQPStats336Rows.png)

Nel piano viene visualizzato quanto segue:
1. È presente un'Analisi indice Columnstore che specifica righe per la fase di compilazione dell'hash join.
1. È presente il nuovo operatore Join adattivo. L'operatore definisce la soglia usata per il passaggio a un piano Cicli annidati. In questo esempio la soglia corrisponde a 78 righe. Se il risultato è &gt;= 78 righe, verrà usato un hash join. Se è inferiore alla soglia, verrà usato un join a cicli annidati.
1. Poiché le righe restituite sono 336, la soglia viene superata: il secondo ramo rappresenta la fase di probe di un'operazione hash join standard. Si noti che Statistiche query dinamiche visualizza le righe del flusso tra gli operatori, in questo caso "672 di 672".
1. L'ultimo ramo è la Ricerca indice cluster che il join a cicli annidati avrebbe usato se la soglia non fosse stata superata. Il valore visualizzato è "0 di 336" righe (il ramo non viene usato).
 Ora si confronti il piano con la stessa query, ma questa volta per un valore *Quantità* che ha una sola riga nella tabella:
 
```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 361;
```
La query restituisce una riga. Se si attiva Statistiche query dinamiche viene visualizzato il piano seguente:

![Risultato della query: una riga](./media/5_AQPStatsOneRow.png)

Nel piano viene visualizzato quanto segue:
- Con una sola riga restituita, ora il flusso di righe attraversa Ricerca indice cluster.
- Poiché non è stata portata avanti la fase di compilazione dell'hash join, nessuna riga attraversa il secondo ramo.

### <a name="adaptive-join-benefits"></a>Vantaggi del join adattivo
Questa funzionalità è ottimale per i carichi di lavoro con frequenti oscillazioni tra i volumi di input di join rilevati.

### <a name="adaptive-join-overhead"></a>Sovraccarichi del join adattivo
I join adattivi presentano requisiti di memoria superiori rispetto a un piano equivalente con join a cicli annidati indicizzati. La memoria aggiuntiva risulta necessaria, come se il join a cicli annidati fosse un hash join. Si registra un sovraccarico anche per la fase di compilazione come operazione stop-and-go rispetto a un join a cicli annidati equivalente a livello di flussi. A tale costo aggiuntivo corrisponde una maggior flessibilità per gli scenari in cui i conteggi delle righe possono variare nell'input di compilazione.

### <a name="adaptive-join-caching-and-re-use"></a>Memorizzazione nella cache e riuso dei join adattivi
I join adattivi in modalità batch funzionano per l'esecuzione iniziale di un'istruzione. Dopo la compilazione, le esecuzioni consecutive restano adattive sulla base della soglia di join adattivo di compilazione e delle righe di runtime del flusso di dati della fase di compilazione dell'input esterno.

### <a name="tracking-adaptive-join-activity"></a>Rilevamento delle attività di join adattivo
L'operatore Join adattivo ha i seguenti attributi dell'operatore del piano:

| Attributo del piano | Descrizione |
|--- |--- |
| AdaptiveThresholdRows | Visualizza l'uso della soglia che determina il passaggio da un hash join a un join a cicli annidati. |
| EstimatedJoinType | Probabile tipo del join. |
| ActualJoinType | In un piano reale visualizza l'algoritmo di join scelto in base alla soglia. |

Il piano stimato visualizza la struttura del piano di join adattivo, la soglia di join adattivo definita e il tipo di join stimato.

### <a name="adaptive-join-and-query-store-interoperability"></a>Interoperabilità tra join adattivi e Archivio query
Query Store acquisisce e può imporre un piano di join adattivo in modalità batch.

### <a name="adaptive-join-eligible-statements"></a>Istruzioni idonee per i join adattivi
Alcune condizioni rendono un join logico idoneo per un join adattivo in modalità batch:
- Il livello di compatibilità del database è 140.
- La query è un'istruzione SELECT (attualmente le istruzioni di modifica dei dati non sono idonee).
- Il join è idoneo per l'esecuzione in un algoritmo fisico di join a cicli annidati indicizzati o di hash join.
- L'hash join usa la modalità batch con un indice Columnstore nella query globale o una tabella Columnstore indicizzata a cui fa riferimento direttamente il join.
- Il primo elemento figlio (riferimento esterno) deve essere identico per le soluzioni alternative generate dal join a cicli annidati e dall'hash join.

### <a name="adaptive-joins-and-nested-loop-efficiency"></a>Efficienza dei join adattivi e dei join a cicli annidati
Se un join adattivo passa al funzionamento con cicli annidati usa le righe già lette dalla compilazione hash join. L'operatore **non** legge di nuovo le righe del riferimento esterno.

### <a name="adaptive-threshold-rows"></a>Righe della soglia adattiva
Il grafico seguente visualizza un esempio di intersezione tra il costo di un hash join e il costo di un join a cicli annidati alternativo.  In questo punto di intersezione viene determinata la soglia, che a sua volta determina l'algoritmo usato per l'operazione di join.

![Soglia di join](./media/6_AQPJoinThreshold.png)

### <a name="disabling-adaptive-joins-without-changing-the-compatibility-level"></a>Disabilitazione dei join adattivi senza modificare il livello di compatibilità

È possibile disabilitare i join adattivi nell'ambito del database o dell'istruzione mantenendo comunque la compatibilità sul livello 140 o superiore.  
Per disabilitare i join adattivi per tutte le esecuzioni di query provenienti dal database, eseguire l'istruzione seguente all'interno del contesto del database applicabile:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = ON;
```

Quando è abilitata, questa impostazione viene visualizzata come abilitata in [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md).
Per abilitare nuovamente i join adattivi per tutte le esecuzioni di query provenienti dal database, eseguire l'istruzione seguente all'interno del contesto del database applicabile:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = OFF;
```

È anche possibile disabilitare i join adattivi per una query specifica, definendo `DISABLE_BATCH_MODE_ADAPTIVE_JOINS` come [hint per la query USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint). Ad esempio

```sql
SELECT s.CustomerID,
       s.CustomerName,
       sc.CustomerCategoryName
FROM Sales.Customers AS s
LEFT OUTER JOIN Sales.CustomerCategories AS sc
       ON s.CustomerCategoryID = sc.CustomerCategoryID
OPTION (USE HINT('DISABLE_BATCH_MODE_ADAPTIVE_JOINS')); 
```

L'hint per la query USE HINT ha la precedenza rispetto una configurazione con ambito database o un'impostazione del flag di traccia.

## <a name="interleaved-execution-for-multi-statement-table-valued-functions"></a>Esecuzione interleaved per funzioni con valori di tabella a più istruzioni
L'esecuzione interleaved cambia il limite unidirezionale tra le fasi di ottimizzazione ed esecuzione nel caso di un'esecuzione a query singola e consente l'adattamento dei piani in base alle stime di cardinalità aggiornate. Se durante l'ottimizzazione viene rilevato un candidato per l'esecuzione interleaved, che attualmente corrisponde a una **funzione con valori di tabella con istruzioni multiple (MSTVF, Multi-Statement Table Valued Function)** si sospende l'ottimizzazione, si esegue il sottoalbero appropriato, si acquisiscono stime di cardinalità accurate e quindi si riprende l'ottimizzazione per le operazioni downstream.   

Le funzioni con valori di tabella con istruzioni multiple (MSTVF) hanno una stima di cardinalità predefinita pari a 100 a partire da [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e pari a 1 nelle versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti. L'esecuzione interleaved riduce i problemi di prestazioni del carico di lavoro dovute alle stime della cardinalità fisse associate alle funzioni con valori di tabella con istruzioni multiple (MSTVF). Per altre informazioni sulle funzioni con valori di tabella con istruzioni multiple (MSTVF), vedere [Creazione di funzioni definite dall'utente (Motore di database)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF).

L'immagine seguente visualizza un output di [Statistiche query dinamiche](../../relational-databases/performance/live-query-statistics.md), un subset di un piano di esecuzione complessivo che visualizza l'impatto delle stime della cardinalità fisse da funzioni con valori di tabella con istruzioni multiple (MSTVF). È possibile visualizzare il flusso di righe effettivo e le righe stimate. Tre aree del piano sono degne di nota (il flusso va da destra a sinistra):
1. L'analisi di tabella MSTVF include una stima fissa pari a 100 righe. In questo esempio tuttavia il flusso della scansione di tabella MSTVF registra 527.597 righe, come visualizzato in Statistiche query dinamiche nel confronto *527597 di 100* tra valore effettivo e valore stimato. Si tratta di una deviazione notevole rispetto alla stima fissa.
1. Per l'operazione di join a cicli annidati è previsto che il lato esterno del join restituisca solo 100 righe. Dato l'elevato numero di righe di fatto restituite dalla funzione MSTVF, in questo caso può risultare utile la scelta di un altro algoritmo di join.
1. Per l'operazione Hash Match osservare il piccolo simbolo di avviso, che in questo caso indica un evento di distribuzione su disco.

![Flusso di righe effettivo e righe stimate](./media/7_AQPFlowThreeAreas.png)

Confrontare il piano precedente al piano reale generato con l'esecuzione interleaved attivata:

![Piano interleaved](./media/8_AQPInterleavedEnabledPlan.png)

1. Si noti che la scansione di tabella MSTVF ora presenta una stima di cardinalità accurata. Si noti anche il riordino della scansione di tabella e delle altre operazioni.
1. Quanto agli algoritmi di join l'operazione di join a cicli annidati è stata sostituita da un'operazione Hash Match, più indicata con un numero di righe molto elevato.
1. Si noti anche che gli avvisi di distribuzione su disco non sono più presenti, in quanto viene allocata una maggior quantità di memoria sulla base del conteggio reale delle righe del flusso della scansione di tabella MSTVF.

### <a name="interleaved-execution-eligible-statements"></a>Istruzioni idonee per l'esecuzione interleaved
Attualmente le funzioni MSTVF che fanno riferimento a istruzioni nell'esecuzione interleaved devono essere di sola lettura e non far parte di un'operazione di modifica dei dati. Le funzioni MSTV, poi, sono idonee per l'esecuzione interleaved solo se non usano costanti di runtime.

### <a name="interleaved-execution-benefits"></a>Vantaggi dell'esecuzione interleaved
In generale, maggiore è lo scarto tra il numero di righe stimato e il numero reale (associato al numero di operazioni del piano downstream), maggiore è l'impatto sulle prestazioni.
L'esecuzione interleaved può risultare vantaggiosa nelle query in cui:
1. Si registra uno scarto notevole tra il numero di righe stimato e il numero reale nel set di risultati intermedio (in questo caso la funzione MSTVF).
1. La query nel suo complesso è sensibile alla variazione delle dimensioni del risultato intermedio. Ciò accade di solito quando nel piano della query è presente un albero complesso sopra il sottoalbero.
Una semplice istruzione `SELECT *` di una funzione MSTVF non trae vantaggio dall'esecuzione interleaved.

### <a name="interleaved-execution-overhead"></a>Sovraccarichi dell'esecuzione interleaved
Il sovraccarico previsto è minimo o nullo. Le funzioni con valori di tabella con istruzioni multiple (MSTVF) venivano già materializzate prima dell'introduzione dell'esecuzione interleaved, ma ora grazie all'abilitazione dell'ottimizzazione differita tali funzioni sfruttano la stima della cardinalità del set di righe materializzate.
È possibile che in seguito alle modifiche alcuni piani registrino un miglioramento della cardinalità per il sottoalbero ma una riduzione dell'efficienza per la query nel suo complesso. La prevenzione può includere il ripristino del livello di compatibilità o l'uso dell'Archivio query per imporre la versione non regredita del piano.

### <a name="interleaved-execution-and-consecutive-executions"></a>Esecuzione interleaved ed esecuzioni consecutive
Dopo che un piano di esecuzione interleaved viene memorizzato nella cache, il piano con le stime aggiornate alla prima esecuzione viene usato per le esecuzioni consecutive e non viene creata di nuovo l'istanza di esecuzione interleaved.

### <a name="tracking-interleaved-execution-activity"></a>Rilevamento delle attività di esecuzione interleaved
È possibile visualizzare gli attributi d'uso nel piano di esecuzione query:

| Attributo del piano di esecuzione | Descrizione |
| --- | --- |
| ContainsInterleavedExecutionCandidates | Si applica al nodo *QueryPlan*. Quando è *true*, il piano contiene candidati per l'esecuzione interleaved. |
| IsInterleavedExecuted | Attributo dell'elemento *RuntimeInformation* in RelOp per il nodo TVF. Quando è *true*, l'operazione è stata materializzata come parte di un'operazione di esecuzione interleaved. |

È anche possibile rilevare le occorrenze di esecuzione interleaved con i seguenti eventi xEvent:

| xEvent | Descrizione |
| ---- | --- |
| interleaved_exec_status | Questo evento viene generato quando si verifica l'esecuzione interleaved. |
| interleaved_exec_stats_update | Questo evento descrive le stime della cardinalità aggiornate dall'esecuzione interleaved. |
| Interleaved_exec_disabled_reason | Questo evento viene generato quando in una query con un possibile candidato per l'esecuzione interleaved non viene applicata tale modalità di esecuzione. |

Per consentire all'esecuzione interleaved di rivedere le stime della cardinalità MSTVF è necessario eseguire la query. Tuttavia il piano di esecuzione stimato viene ancora visualizzato quando sono presenti candidati per l'esecuzione interleaved tramite l'attributo showplan `ContainsInterleavedExecutionCandidates`.    

### <a name="interleaved-execution-caching"></a>Memorizzazione nella cache dell'esecuzione interleaved
Se un piano è viene cancellato o espulso dalla cache, durante l'esecuzione della query l'esecuzione interleave viene usata da una nuova compilazione.
Un'istruzione che usa `OPTION (RECOMPILE)` crea un nuovo piano usando l'esecuzione interleaved e non lo memorizza nella cache.     

### <a name="interleaved-execution-and-query-store-interoperability"></a>Interoperabilità tra esecuzione interleaved e Archivio query
È possibile forzare i piani che usano l'esecuzione interleaved. Il piano è la versione che presenta stime della cardinalità corrette sulla base dell'esecuzione iniziale.    

### <a name="disabling-interleaved-execution-without-changing-the-compatibility-level"></a>Disabilitazione dell'esecuzione interleaved senza modificare il livello di compatibilità

È possibile disabilitare l'esecuzione interleaved nell'ambito del database o dell'istruzione mantenendo comunque la compatibilità sul livello 140 o superiore.  Per disabilitare l'esecuzione interleaved per tutte le esecuzioni di query provenienti dal database, eseguire l'istruzione seguente all'interno del contesto del database applicabile:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = ON;
```

Quando è abilitata, questa impostazione viene visualizzata come abilitata in [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md).
Per abilitare nuovamente l'esecuzione interleaved per tutte le esecuzioni di query provenienti dal database, eseguire l'istruzione seguente all'interno del contesto del database applicabile:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = OFF;
```

È anche possibile disabilitare l'esecuzione interleaved per una query specifica definendo `DISABLE_INTERLEAVED_EXECUTION_TVF` come [hint per la query USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint). Ad esempio

```sql
SELECT [fo].[Order Key], [fo].[Quantity], [foo].[OutlierEventQuantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Fact].[WhatIfOutlierEventQuantity]('Mild Recession',
                            '1-01-2013',
                            '10-15-2014') AS [foo] ON [fo].[Order Key] = [foo].[Order Key]
                            AND [fo].[City Key] = [foo].[City Key]
                            AND [fo].[Customer Key] = [foo].[Customer Key]
                            AND [fo].[Stock Item Key] = [foo].[Stock Item Key]
                            AND [fo].[Order Date Key] = [foo].[Order Date Key]
                            AND [fo].[Picked Date Key] = [foo].[Picked Date Key]
                            AND [fo].[Salesperson Key] = [foo].[Salesperson Key]
                            AND [fo].[Picker Key] = [foo].[Picker Key]
OPTION (USE HINT('DISABLE_INTERLEAVED_EXECUTION_TVF'));
```

L'hint per la query USE HINT ha la precedenza rispetto una configurazione con ambito database o un'impostazione del flag di traccia.

## <a name="see-also"></a>Vedere anche
[Elaborazione di query intelligenti nei database SQL](../../relational-databases/performance/intelligent-query-processing.md)   
[Centro prestazioni per il motore di database di SQL Server e il database SQL di Azure](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[Guida sull'architettura di elaborazione delle query](../../relational-databases/query-processing-architecture-guide.md)    
[Guida di riferimento a operatori Showplan logici e fisici](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Join](../../relational-databases/performance/joins.md)    
[Demonstrating Adaptive Query Processing](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)   (Dimostrazione dell'elaborazione di query adattive)  
[Hint per la query USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint)   
[Creare funzioni definite dall'utente (motore di database)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)  
