---
title: Join (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/18/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- HASH join
- NESTED LOOPS join
- MERGE join
- joins [SQL Server], about joins
- join hints [SQL Server]
ms.assetid: bfc97632-c14c-4768-9dc5-a9c512f4b2bd
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d9f218c3ff39e16ec656f9bbca24400920d99b76
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377013"
---
# <a name="joins-sql-server"></a>Join (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue operazioni di ordinamento, intersezione, unione e differenza tramite le tecnologie di ordinamento in memoria e di hash join. Grazie a questo tipo di piano di query, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta il partizionamento verticale delle tabelle, denominato talvolta "archiviazione a colonne".   

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza tre tipi di operazioni di join:    
-   Join a cicli annidati     
-   Merge join   
-   Hash join   

## <a name="fundamentals"></a> Nozioni di base sui join
I join consentono di recuperare dati da due o più tabelle in base alle relazioni logiche esistenti tra le tabelle stesse. I join indicano la modalità con cui Microsoft SQL Server usa i dati di una tabella per la selezione di righe in un'altra tabella.    

Una condizione di join definisce il modo in cui due tabelle sono correlate in una query in base agli elementi seguenti:    
-   L'impostazione della colonna di ogni tabella da utilizzare per il join. In una condizione di join tipica viene specificata una chiave esterna di una tabella e la chiave associata nell'altra tabella.    
-   L'impostazione dell'operatore logico (ad esempio = o <>) da utilizzare per il confronto dei valori delle colonne.    

Gli inner join possono essere specificati nelle clausole `FROM` o `WHERE`. Gli outer join possono essere specificati solo nella clausola `FROM`. Le condizioni di join vengono usate insieme alle condizioni di ricerca delle clausole `WHERE` e `HAVING` per definire le righe da selezionare nelle tabelle di base a cui viene fatto riferimento nella clausola `FROM`.    

L'impostazione delle condizioni di join nella clausola `FROM` consente di separare queste condizioni da altre condizioni di ricerca specificate nella clausola `WHERE`. Corrisponde anche al metodo consigliato per l'impostazione dei join. La sintassi ISO semplificata per la definizione di un join nella clausola FROM è la seguente:

```
FROM first_table join_type second_table [ON (join_condition)]
```

*join_type* specifica il tipo di join da eseguire: inner, outer o cross join. *join_condition* definisce il predicato da valutare per ogni coppia di righe unite in join. Di seguito è riportato un esempio di definizione di join nella clausola FROM:

```sql
FROM Purchasing.ProductVendor JOIN Purchasing.Vendor
     ON (ProductVendor.BusinessEntityID = Vendor.BusinessEntityID)
```

L'istruzione seguente è un'istruzione SELECT semplice in cui viene utilizzato tale join:

```sql
SELECT ProductID, Purchasing.Vendor.BusinessEntityID, Name
FROM Purchasing.ProductVendor JOIN Purchasing.Vendor
    ON (Purchasing.ProductVendor.BusinessEntityID = Purchasing.Vendor.BusinessEntityID)
WHERE StandardPrice > $10
  AND Name LIKE N'F%'
GO
```

L'istruzione SELECT restituisce informazioni sul prodotto e sul fornitore per ogni combinazione di prodotti con prezzo maggiore di $ 10 fornito da una società il cui nome inizia con la lettera F.   

Se in una singola query viene fatto riferimento a più tabelle, nessuno dei riferimenti alle colonne deve presentare ambiguità. Nell'esempio precedente, sia la tabella ProductVendor che la tabella Vendor avevano una colonna denominata BusinessEntityID. I nomi di colonna duplicati in due o più tabelle a cui viene fatto riferimento nella query devono essere qualificati con il nome della tabella. Nell'esempio tutti i riferimenti alle colonne Vendor sono qualificati.   

Se il nome di una colonna non è duplicato in due o più tabelle utilizzate nella query, non è necessario qualificare i riferimenti con il nome della tabella, come illustrato nell'esempio precedente. Un'istruzione SELECT di questo tipo a volte è di difficile comprensione in quanto non indica la tabella a cui appartiene ogni colonna. La query risulta più leggibile se tutte le colonne sono qualificate con i nomi delle rispettive tabelle. Il grado di leggibilità aumenta ulteriormente se si utilizzano gli alias di tabella, soprattutto quando è necessario qualificare anche i nomi delle tabelle con il nome del database e del proprietario. L'esempio seguente equivale all'esempio precedente. Per rendere la query più leggibile, sono stati però assegnati alias alle tabelle e i nomi di colonna sono stati qualificati con gli alias di tabella:

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv 
JOIN Purchasing.Vendor AS v
    ON (pv.BusinessEntityID = v.BusinessEntityID)
WHERE StandardPrice > $10
    AND Name LIKE N'F%';
```

Nell'esempio precedente le condizioni di join sono specificate nella clausola FROM (metodo consigliato). Nella query seguente la stessa condizione di join è specificata nella clausola WHERE:

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv, Purchasing.Vendor AS v
WHERE pv.BusinessEntityID=v.BusinessEntityID
    AND StandardPrice > $10
    AND Name LIKE N'F%';
```

Nell'elenco di selezione di un join è possibile fare riferimento a tutte le colonne delle tabelle unite in join o a qualsiasi subset delle colonne. Nell'elenco di selezione non è necessario specificare le colonne di ogni tabella del join. Ad esempio, in un join tra tre tabelle è possibile utilizzare una sola tabella come collegamento tra le altre due e le colonne di tale tabella non devono essere necessariamente incluse nell'elenco di selezione.   

Sebbene le condizioni di join includano in genere confronti di uguaglianza (=), è possibile specificare altri operatori di confronto o relazionali e altri predicati. Per altre informazioni, vedere [Operatori di confronto &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md) e [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md).  

Durante l'elaborazione di join in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il motore query sceglie il metodo di elaborazione di join più efficiente tra quelli possibili. L'esecuzione fisica di vari join può essere realizzata con molte ottimizzazioni diverse e pertanto non può essere stimata in maniera affidabile.   

Non è necessario che alle colonne di una condizione di join sia associato lo stesso nome o lo stesso tipo di dati. Se tuttavia i tipi di dati sono diversi, devono essere compatibili o supportare la conversione implicita di SQL Server. Se non è possibile eseguire la conversione implicita dei tipi di dati, è necessario impostare nella condizione di join la conversione esplicita tramite la funzione `CAST`. Per altre informazioni sulla conversione implicita ed esplicita dei dati, vedere [Conversione di tipi di dati &#40;motore di database&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md).    

La maggior parte delle query che includono un join possono essere riformulate specificando una subquery, ovvero una query nidificata in un'altra query. La maggior parte delle subquery possono a loro volta essere riformulate come join. Per altre informazioni sulle sottoquery, vedere [Subqueries](../../relational-databases/performance/subqueries.md) (Sottoquery).   

> [!NOTE]
> Non è possibile unire le tabelle in join direttamente in base alle colonne di tipo ntext, text o image. Tuttavia, è possibile unire le tabelle in join indirettamente in base alle colonne di tipo ntext, text o image usando `SUBSTRING`.    
> Ad esempio, `SELECT * FROM t1 JOIN t2 ON SUBSTRING(t1.textcolumn, 1, 20) = SUBSTRING(t2.textcolumn, 1, 20)` esegue un inner join tra due tabelle sui primi 20 caratteri di ogni colonna di tipo text delle tabelle t1 e t2.   
> È possibile anche confrontare colonne di tipo ntext e text di due tabelle confrontando la lunghezza delle colonne con una clausola `WHERE`, come illustrato nell'esempio seguente: `WHERE DATALENGTH(p1.pr_info) = DATALENGTH(p2.pr_info)`

## <a name="nested_loops"></a> Informazioni sui join a cicli annidati
Se l'input di un join è ridotto (inferiore a 10 righe) e l'input dell'altro join è molto esteso e indicizzato in base alle rispettive colonne di join, l'operazione di join più rapida è rappresentata dai nested loop join indicizzati poiché questi richiedono la minore quantità di I/O e il minor numero di operazioni di confronto. 

Il join a cicli annidati, detto anche *iterazione nidificata*, usa un input di join come tabella di input esterna, visualizzata come input superiore nel piano di esecuzione grafico, e un input di join come tabella di input interna (inferiore). Il ciclo esterno elabora la tabella di input esterna, una riga alla volta. Il ciclo interno, eseguito per ogni riga esterna, cerca le righe corrispondenti nella tabella di input interna.   

Nel caso più semplice, ovvero un *join a cicli annidati di tipo naive*, la ricerca comporta l'analisi di un'intera tabella o indice. Nel caso di un *join a cicli annidati indicizzato*, per la ricerca viene usato un indice. In un *join a cicli annidati temporaneo* l'indice viene creato nell'ambito del piano di query ed eliminato dopo il completamento della query. Tutte queste varianti vengono elaborate da Query Optimizer.   

Un nested loop join è particolarmente efficace se l'input esterno è di dimensioni ridotte mentre l'input interno è preindicizzato e di dimensioni notevoli. In molte transazioni di dimensioni ridotte, ad esempio quelle relative a set di righe limitati, i nested loop join indicizzati offrono prestazioni superiori rispetto ai merge join e agli hash join. Per le query di notevoli dimensioni, tuttavia, i nested loop join rappresentano raramente la scelta ottimale.    

## <a name="merge"></a> Informazioni sui merge join
Se i due input di join non sono di dimensioni ridotte, ma sono ordinati in base alla rispettiva colonna di join (ad esempio, se sono stati ottenuti tramite l'analisi di indici ordinati), l'operazione di join più rapida è rappresentata dal merge join. Se entrambi gli input di join sono di dimensioni notevoli e analoghe, un merge join con ordinamento eseguito in precedenza e un hash join offrono prestazioni simili. Le operazioni di hash join, tuttavia, risultano spesso molto più rapide se le dimensioni dei due input differiscono in modo significativo.       

Per i merge join è necessario che entrambi gli input siano ordinati in base alle colonne di merge, definite dalle clausole di uguaglianza (ON) del predicato di join. In genere Query Optimizer esegue l'analisi di un indice, se questo esiste nel set di colonne, oppure inserisce un operatore di ordinamento sotto il merge join. In rari casi possono esistere più clausole di uguaglianza, ma le colonne di merge vengono ricavate soltanto da alcune delle clausole disponibili.    

Poiché ogni input è ordinato, l'operatore **Merge Join** recupera una riga da ogni input ed esegue il confronto tra le righe. Ad esempio, per operazioni di inner join, le righe vengono restituite se sono uguali. In caso contrario, la riga con il valore minore viene scartata e dallo stesso input viene recuperata un'altra riga. Questo processo si ripete fino al completamento dell'elaborazione di tutte le righe.    

L'operazione di merge join può essere un'operazione regolare o un'operazione molti-a-molti. Un merge join molti-a-molti utilizza una tabella temporanea per l'archiviazione delle righe. Se sono presenti valori duplicati in entrambi gli input, uno degli input deve tornare all'inizio dei duplicati durante l'elaborazione di ogni duplicato dell'altro input.    

Se è presente un predicato residuo, tutte le righe conformi al predicato di merge vengono valutate da tale predicato e vengono restituite soltanto quelle che lo soddisfano.   

Il merge join è di per sé un'operazione molto rapida, ma può essere una scelta onerosa se sono necessarie operazioni di ordinamento. Se tuttavia il volume dei dati è elevato ed è possibile ottenere i dati desiderati già ordinati da indici ad albero B esistenti, il merge join risulta spesso l'algoritmo di join più veloce.    

## <a name="hash"></a> Informazioni sugli hash join
Gli hash join consentono l'elaborazione efficiente di input di grandi dimensioni, non ordinati e non indicizzati. Tali join sono utili per ottenere risultati intermedi in query complesse, in quanto:
-   I risultati intermedi non sono indicizzati, a meno che non vengano salvati esplicitamente su disco e quindi indicizzati, e spesso non vengono ordinati in modo adeguato per l'operazione successiva nel piano di query.
-   Query Optimizer stima esclusivamente le dimensioni dei risultati intermedi. Poiché le stime relative a query complesse possono essere estremamente imprecise, è necessario non solo che gli algoritmi di elaborazione dei risultati intermedi siano efficienti, ma anche che vengano ridotti gradualmente nel caso in cui un risultato intermedio risulti molto più grande del previsto.   

Gli hash join consentono di ridurre la denormalizzazione. In genere, la denormalizzazione viene utilizzata per ottenere prestazioni migliori tramite la riduzione delle operazioni di join, nonostante rischi di ridondanza quali aggiornamenti non consistenti. Gli hash join riducono la necessità di utilizzo della denormalizzazione. Gli hash join rendono il partizionamento verticale (la rappresentazione di gruppi di colonne di un'unica tabella in file o indici separati) un'opzione adeguata per la progettazione fisica dei database.     

Gli hash join prevedono due tipi di input, ovvero l'input **di compilazione** e l'input **probe**. Query Optimizer assegna all'input più piccolo il ruolo di input di compilazione.    

Gli hash join vengono utilizzati per vari tipi di operazioni di corrispondenza tra set, ovvero inner join, outer join sinistro, destro e completo, semi-join sinistro e destro, intersezione, unione e differenza. Una variante dell'hash join può anche eseguire la rimozione dei duplicati e il raggruppamento, ad esempio `SUM(salary) GROUP BY department`. Queste modifiche utilizzano un solo input sia per il ruolo di compilazione che per il ruolo probe.   

Nelle sezioni seguenti vengono descritti i diversi tipi di hash join: hash join in memoria, grace hash join e hash join ricorsivo.    

### <a name="inmem_hash"></a> Hash join in memoria

L'hash join esegue in primo luogo l'analisi o il calcolo dell'intero input di compilazione, quindi compila una tabella hash in memoria. Ogni riga viene inserita in un hash bucket in base al valore hash calcolato per la chiave hash. Se l'intero input di compilazione è inferiore alla memoria disponibile, tutte le righe possono essere inserite nella tabella hash. A questa fase di compilazione segue la fase probe. Viene eseguita l'analisi o il calcolo dell'intero input probe, una riga alla volta. Per ogni riga probe viene calcolato il valore della chiave hash, viene eseguita l'analisi dell'hash bucket corrispondente e vengono prodotte le corrispondenze.    

### <a name="grace_hash"></a> Grace hash join

Se le dimensioni dell'input di compilazione sono superiori a quelle della memoria disponibile, l'hash join viene eseguito in vari passaggi. In questo caso, l'hash join viene definito grace hash join. Ogni passaggio prevede una fase di compilazione e una fase probe. L'input di compilazione e l'input probe vengono inizialmente analizzati e partizionati in più file, tramite una funzione di hashing sulle chiavi hash. L'utilizzo della funzione di hashing sulle chiavi hash garantisce che ogni coppia di record su cui si basa il join si trovi nella stessa coppia di file. In tal modo il join di due input di grandi dimensioni risulta convertito in più istanze di dimensioni ridotte della stessa attività. L'hash join viene quindi applicato a ogni coppia di file partizionati.    

### <a name="recursive_hash"></a> Hash join ricorsivo

Se l'input di compilazione ha dimensioni tali per cui gli input per un'unione esterna standard richiedono più livelli di unione, saranno necessari più passaggi di partizionamento e più livelli di partizionamento. Se soltanto alcune partizioni sono di grandi dimensioni, i passaggi di partizionamento aggiuntivi vengono utilizzati soltanto per tali partizioni. Per velocizzare al massimo i passaggi di partizionamento vengono utilizzate operazioni di I/O asincrone di grandi dimensioni, per cui un unico thread può tenere occupate più unità disco.    

> [!NOTE]
> Se l'input di compilazione non ha dimensioni di molto superiori a quelle della memoria disponibile, gli elementi dell'hash join in memoria e del grace hash join vengono combinati in un unico passaggio, producendo un hash join ibrido.   

Durante l'ottimizzazione non sempre è possibile determinare il tipo di hash join che verrà utilizzato. Pertanto, SQL Server usa inizialmente un hash join in memoria, quindi passa gradualmente a grace hash join e hash join ricorsivo a seconda delle dimensioni dell'input di compilazione.    

Se Query Optimizer non prevede correttamente quale dei due input è il più piccolo, al quale quindi deve essere assegnato il ruolo di input di compilazione, i ruoli di input di compilazione e di input probe vengono invertiti dinamicamente. L'hash join utilizza comunque come input di compilazione il file di overflow più piccolo. Questa tecnica è detta inversione dei ruoli. L'inversione dei ruoli si verifica all'interno dell'hash join dopo l'esecuzione di almeno uno spill sul disco.     

> [!NOTE]
> L'inversione dei ruoli si verifica in maniera indipendente da qualsiasi struttura o hint per la query e inoltre non viene visualizzata nel piano di query. Quando si verifica, l'inversione dei ruoli è un'operazione trasparente all'utente.

### <a name="hash_bailout"></a> hash bailout

Il termine hash bailout è talvolta usato per descrivere grace hash join o hash join ricorsivi.    

> [!NOTE]
> Gli hash join ricorsivi e gli hash bailout causano una riduzione delle prestazioni del server. Se si nota la presenza di molti eventi di avviso di hash in una traccia, aggiornare le statistiche sulle colonne che si sta unendo in join.    

Per altre informazioni sugli hash bailout, vedere [Hash Warning - classe di evento](../../relational-databases/event-classes/hash-warning-event-class.md).    
  
## <a name="nulls_joins"></a> Valori Null e join
Gli eventuali valori Null presenti nelle colonne delle tabelle da unire in join non possono essere associati ad altri valori. La presenza di valori Null in una colonna di una delle tabelle da unire in join viene restituita solo se si usa un outer join, a meno che la clausola `WHERE` non escluda i valori Null.     

Le due tabelle riportate di seguito includono entrambe un valore Null nella colonna interessata dal join:     

```
table1                          table2
a           b                   c            d
-------     ------              -------      ------
      1        one                 NULL         two
   NULL      three                    4        four
      4      join4
```    

Un join che confronta i valori della colonna a con quelli della colonna c non consente di ottenere corrispondenze nelle colonne che includono valori NULL:

```sql
SELECT *
FROM table1 t1 JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```  

Nelle colonne a e c viene restituita una sola riga con valore 4:

```
a           b      c           d      
----------- ------ ----------- ------ 
4           join4  4           four   

(1 row(s) affected)
```   

I valori Null restituiti da una tabella di base non sono inoltre facilmente distinguibili dai valori Null restituiti da un outer join. L'istruzione `SELECT` seguente, ad esempio, esegue un left outer join sull due tabelle seguenti:   

```sql
SELECT *
FROM table1 t1 LEFT OUTER JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```   

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]   

```
a           b      c           d      
----------- ------ ----------- ------ 
NULL        three  NULL        NULL 
1           one    NULL        NULL 
4           join4  4           four   

(3 row(s) affected)
```   

Nel set di risultati non è agevole distinguere un valore NULL dei dati da un valore NULL che rappresenta un tentativo di join non riuscito. Se i dati da unire in join includono valori Null, è in genere consigliabile omettere tali valori dai risultati utilizzando un join normale.    

## <a name="see-also"></a>Vedere anche  
[Guida di riferimento a operatori Showplan logici e fisici](../../relational-databases/showplan-logical-and-physical-operators-reference.md)     
[Operatori di confronto &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)    
[Conversione di tipi di dati &#40;motore di database&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
[Subqueries](../../relational-databases/performance/subqueries.md)     (Sottoquery)  
[Join adattivi](../../relational-databases/performance/adaptive-query-processing.md#batch-mode-adaptive-joins)    


  
  
