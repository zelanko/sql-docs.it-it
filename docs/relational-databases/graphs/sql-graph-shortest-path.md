---
title: PERCORSO più breve (grafo SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- SHORTEST PATH
- SHORTEST_PATH
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ef8f38acbf621a9c73a0d85bca579c8b7c87aa13
ms.sourcegitcommit: 9d3ece500fa0e4a9f4fefc88df4af1db9431c619
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67463548"
---
# <a name="shortestpath-transact-sql"></a>SHORTEST_PATH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver2015-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  Specifica una condizione di ricerca per un grafico, che viene eseguita la ricerca in modo ricorsivo o ripetutamente. SHORTEST_PATH può essere utilizzata all'interno di corrispondenza con graph nodo e le tabelle bordi, nell'istruzione SELECT. 
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="shortest-path"></a>Percorso più breve
La funzione SHORTEST_PATH consente di trovare:    
* Un percorso più breve tra due nodi determinato/entità
* Singola origine percorsi più brevi.
* Percorso più breve di più nodi di origine a più nodi di destinazione.

Accetta un modello di lunghezza arbitraria come input e restituisce un percorso più breve che esiste tra due nodi. Questa funzione può essere usata solo all'interno di MATCH. La funzione restituisce solo un percorso più breve tra due nodi specificati. Se è presente, due o più percorsi più brevi della stessa lunghezza tra qualsiasi coppia di nodi di origine e di destinazione, il funzione restituisce solo un percorso che è stato trovato prima durante l'attraversamento. Si noti che, una serie di lunghezza arbitraria può essere specificata solo all'interno di una funzione SHORTEST_PATH. 

Vedere le [MATCH (grafo SQL)](../../t-sql/queries/match-sql-graph.md) per la sintassi. 

## <a name="for-path"></a>PER PERCORSO
PER percorso deve essere utilizzato con qualsiasi nome di tabella nodi o archi nella clausola FROM, che farà parte di un modello di lunghezza arbitraria. PER il percorso indica al motore che la tabella nodi o archi restituirà un insieme ordinato che rappresenta l'elenco di nodi o bordi trovati nel percorso attraversato. Gli attributi da tali tabelle non possono essere proiettati direttamente nella clausola SELECT. Per proiettare gli attributi da tali tabelle, funzioni di aggregazione tracciato del grafico deve essere utilizzato.  

## <a name="arbitrary-length-pattern"></a>Modello di lunghezza arbitraria
Questo modello include i nodi e bordi che devono essere attraversati ripetutamente fino a raggiunta il nodo desiderato o finché il numero massimo di iterazioni come specificato nel modello viene soddisfatta. Ogni volta che viene eseguita la query, il risultato dell'esecuzione di questo modello sarà una raccolta ordinata di nodi e bordi attraversati lungo il percorso dal nodo di inizio per il nodo di fine. Questo è un modello di sintassi di espressione regolare lo stile e sono supportati i quantificatori due modello seguente:

* **‘+’** : Ripetere il modello 1 o più volte. Terminare non appena viene trovato un percorso più breve.
* **{1,n}** : Ripetere il modello 1 da ' n'ore. Terminare non appena viene trovato un più breve.

## <a name="lastnode"></a>LAST_NODE
Funzione LAST_NODE() consente la concatenazione di due schemi di attraversamento di lunghezza arbitraria. Può essere utilizzato negli scenari in cui:    
* Più modelli di percorso più breve vengono utilizzati in una query e un modello in cui inizia l'ultimo nodo dello schema precedente.
* Due modelli di percorso più brevi di tipo merge nel LAST_NODE() stesso.

## <a name="graph-path-order"></a>Ordine di percorso grafico
Ordine di percorso grafico relativo all'ordine dei dati nel percorso di output. Inizia sempre l'ordine di percorso di output nella parte del modello aggiungendo i nodi/bordi che vengono visualizzati nella parte ricorsiva di non ricorsiva. L'ordine in cui viene attraversato il grafico durante l'ottimizzazione o l'esecuzione di query non ha nulla a che fare con l'ordine nell'output. Analogamente, la direzione della freccia nel modello ricorsivo non influisce l'ordine di percorso grafico. 

## <a name="graph-path-aggregate-functions"></a>Funzioni di aggregazione percorso grafico
Poiché i nodi e bordi coinvolta nel criterio di lunghezza arbitraria restituito una raccolta (di nodo/i e uno o più spigoli attraversato in tale percorso), gli utenti non è possibile proiettare gli attributi con la sintassi tablename.attributename convenzionale. Per una query in cui è necessaria per proiettare i valori di attributo da tabelle nodi o archi intermediate, nel percorso attraversato, utilizzare le seguenti funzioni di aggregazione percorso grafico: STRING_AGG, LAST_VALUE, SUM, AVG, MIN, MAX e COUNT. La sintassi generale per usare queste funzioni di aggregazione nella clausola SELECT è:

```
<GRAPH_PATH_AGGREGATE_FUNCTION>(<expression> , <separator>)  <order_clause>

    <order_clause> ::=
        { WITHIN GROUP (GRAPH PATH) }

    <GRAPH_PATH_AGGREGATE_FUNCTION> ::=
          STRING_AGG
        | LAST_VALUE
        | SUM
        | COUNT
        | AVG
        | MIN
        | MAX

```

### <a name="stringagg"></a>STRING_AGG
La funzione STRING_AGG accetta un'espressione e il separatore come input e restituisce una stringa. Gli utenti possono usare questa funzione nella clausola SELECT agli attributi di progetto dai nodi intermedi o del bordo del percorso attraversato. 

### <a name="lastvalue"></a>LAST_VALUE
Al progetto gli attributi dall'ultimo nodo del percorso attraversato, funzione di aggregazione LAST_VALUE possono essere utilizzati. È possibile specificare alias di tabella edge come input per questa funzione, solo i nomi delle tabelle di nodo o gli alias possono essere utilizzati.

**Ultimo nodo**: L'ultimo nodo corrisponde al nodo che viene visualizzato per ultimo nel percorso attraversato, indipendentemente dalla direzione della freccia nel predicato di corrispondenza. Ad esempio: `MATCH(SHORTEST_PATH(n(-(e)->p)+) )`. In questo caso l'ultimo nodo nel percorso sarà l'ultimo nodo visitato P. 

Mentre, ultimo nodo è l'ultimo nodo ennesima nel percorso grafico di output per questo modello: `MATCH(SHORTEST_PATH((n<-(e)-)+p))`    

### <a name="sum"></a>SUM
Questa funzione restituisce la somma dei valori di attributo specificato nodo/Microsoft edge o un'espressione che è disponibile nel percorso attraversato.

### <a name="count"></a>COUNT
Questa funzione restituisce il numero di valori non null dell'attributo desiderato nodo/Microsoft edge nel percorso. Supporta la funzione COUNT di ' *' operatore con un alias di tabella nodi o bordi. Senza l'alias della tabella nodi o archi, l'utilizzo di * è ambiguo e verrà generato un errore.

    {  COUNT( <expression> | <node_or_edge_alias>.* )  <order_clause>  }


### <a name="avg"></a>MEDIO
Restituisce la media dei valori di attributo specificato nodo/Microsoft edge o un'espressione che è disponibile nel percorso attraversato.

### <a name="min"></a>MIN
Restituisce il valore minimo da valori di attributo specificato nodo/Microsoft edge o espressione che appare nel percorso attraversato.

### <a name="max"></a>MAX
Restituisce il valore massimo da valori di attributo specificato nodo/Microsoft edge o espressione che appare nel percorso attraversato.

## <a name="remarks"></a>Note  
funzione shortest_path può essere utilizzata solo all'interno di MATCH.     
LAST_NODE è supportato solo all'interno di shortest_path.     
Ricerca percorso più breve ponderato, tutti i percorsi o tutti i percorsi più brevi non è supportata.         
In alcuni casi, i piani non validi possono essere generati per le query con numero maggiore di hop, con conseguente maggiore i tempi di esecuzione di query. Uso di un hint di join hash può essere utile.    


## <a name="examples"></a>Esempi 
Per le query di esempio illustrate in questo caso, si userà ot utilizzano il nodo e creare le tabelle edge in [esempio grafo SQL](./sql-graph-sample.md)

### <a name="a--find-shortest-path-between-2-people"></a>A.  Individuare il percorso più breve tra 2 persone
 Nell'esempio seguente, troviamo un percorso più breve tra Jacob e Alice. È necessario il nodo /People/Person ed edge FriendOf creati dallo script di esempio di grafico. 

 ```
SELECT PersonName, Friends
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
 ```

 ### <a name="b--find-shortest-path-from-a-given-node-to-all-other-nodes-in-the-graph"></a>B.  Individuare il percorso più breve da un determinato nodo per tutti gli altri nodi nel grafico. 
 Nell'esempio seguente consente di trovare tutte le persone che Jacob è connesso a nel grafico e il percorso più breve a partire da Jacob tutti i destinatari. 

 ```
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
AND Person1.name = 'Jacob'
 ```

### <a name="c--count-the-number-of-hopslevels-traversed-to-go-from-one-person-to-another-in-the-graph"></a>C.  Contare il numero di hop/livelli attraversate per passare da una persona a altra nel grafico.
 Nell'esempio seguente consente di trovare il percorso più breve tra Jacob e Alice e stampa il numero di hop che è necessario per passare da Jacob ad Alice. 

 ```
 SELECT PersonName, Friends, levels
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
 ```

### <a name="d-find-people-1-3-hops-away-from-a-given-person"></a>D. Trovare persone 1-3 hop lontano da un utente specifico
Nell'esempio seguente consente di trovare il percorso più breve tra Jacob e tutte le persone che si è connesso agli hop graph 1-3 lontano da quest'ultimo. 

```
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
AND Person1.name = 'Jacob'
```

### <a name="e-find-people-exactly-2-hops-away-from-a-given-person"></a>E. Trovare persone esattamente 2 hop lontano da un utente specifico
Nell'esempio seguente consente di trovare il percorso più breve tra Jacob e persone che hanno esattamente 2 hop lontano da quest'ultimo nel grafico. 

```
SELECT PersonName, Friends
FROM (
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
    AND Person1.name = 'Jacob'
) Q
WHERE Q.levels = 2
```

## <a name="see-also"></a>Vedere anche  
 [MATCH (grafo SQL)](../../t-sql/queries/match-sql-graph.md)    
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (grafo SQL)](../../t-sql/statements/insert-sql-graph.md)  
 [Graph Processing with SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md) (Elaborazione di grafi con SQL Server 2017)     
 
